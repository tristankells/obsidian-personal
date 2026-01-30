# Draft Specs
- When adding tags on the recipes details page, I would like autocomplete suggestions built from all of the existing tags.
# Feature: Tag Autocomplete on Recipe Detail Page

## Overview

When the user types in the "Add tag" input on the Recipe Detail / Edit page, a dropdown appears below the input showing existing tags (from all of the user's recipes) that **start with** the typed text. The user can select a suggestion with the mouse or navigate the list with the keyboard arrow keys and confirm with Enter.

---

## Files Changed

|File|Change|
|---|---|
|`Broccoli.App.Shared/Pages/RecipeDetail.razor.cs`|New fields + methods for autocomplete state|
|`Broccoli.App.Shared/Pages/RecipeDetail.razor`|Wrap tag input, bind oninput, render suggestion list|
|`Broccoli.App.Shared/Pages/RecipeDetail.razor.css`|Style the autocomplete wrapper and dropdown|

---

## 1. `RecipeDetail.razor.cs`

### 1a. New fields

`// Autocomplete state private HashSet<string> _allTags = new(StringComparer.OrdinalIgnoreCase); private List<string>    _tagSuggestions = new(); private bool            _showSuggestions; private int             _activeSuggestionIndex = -1;   // -1 = nothing selected`

### 1b. Parallel load in `LoadRecipe()`

For an **existing** recipe both `GetByIdAsync` and `GetAllAsync` are fired concurrently so neither blocks the other:

`private async Task LoadRecipe() {     isLoading = true;     _jsInitialized = false;     errorMessage = null;     try     {         if (IsNewRecipe)         {             recipe = new Recipe { Tags = new(), Images = new() };             // Still fetch tags so the user gets suggestions on a brand-new recipe             var allForNew = await RecipeService.GetAllAsync();             _allTags = allForNew                .SelectMany(r => r.Tags)                 .ToHashSet(StringComparer.OrdinalIgnoreCase);         }         else         {             // Fire both requests in parallel             var recipeTask = RecipeService.GetByIdAsync(RecipeId!);             var allTask    = RecipeService.GetAllAsync();             await Task.WhenAll(recipeTask, allTask);             recipe   = recipeTask.Result;             _allTags = allTask.Result                 .SelectMany(r => r.Tags)                 .ToHashSet(StringComparer.OrdinalIgnoreCase);             if (recipe == null)                 errorMessage = "Recipe not found.";         }     }     catch (Exception ex)     {         errorMessage = $"Error loading recipe: {ex.Message}";     }     finally     {         isLoading = false;     }     if (recipe is not null && !string.IsNullOrWhiteSpace(recipe.Ingredients))         _ = ScoreSeasonalityAsync(recipe.Ingredients); }`

> **Note:** `Task.WhenAll` propagates the first exception; individual `try/catch` inside each task is not needed because errors are surfaced the same way as before.

### 1c. New autocomplete methods

`private void OnTagInputChanged(ChangeEventArgs e) {     newTag = e.Value?.ToString() ?? string.Empty;     _activeSuggestionIndex = -1;     if (string.IsNullOrWhiteSpace(newTag))     {         _tagSuggestions.Clear();         _showSuggestions = false;         return;     }     // Suggestions: tags that start with the typed text, excluding tags     // already on this recipe, ordered alphabetically, capped at 8.     _tagSuggestions = _allTags        .Where(t => t.StartsWith(newTag, StringComparison.OrdinalIgnoreCase)                  && !(recipe?.Tags.Contains(t, StringComparer.OrdinalIgnoreCase) ?? false))         .OrderBy(t => t)         .Take(8)         .ToList();     _showSuggestions = _tagSuggestions.Count > 0; } private void SelectSuggestion(string tag) {     newTag = tag;     _showSuggestions = false;     _activeSuggestionIndex = -1;     AddTag();          // reuses existing duplicate-check + clear logic } private async Task HideSuggestions() {     // Delay lets a mousedown on a list item fire before focus leaves the wrapper.     await Task.Delay(150);     _showSuggestions = false;     _activeSuggestionIndex = -1; } private void OnTagKeyDown(KeyboardEventArgs e) {     switch (e.Key)     {         case "ArrowDown":             if (_tagSuggestions.Count == 0) break;             _showSuggestions = true;             _activeSuggestionIndex = Math.Min(_activeSuggestionIndex + 1, _tagSuggestions.Count - 1);             break;         case "ArrowUp":             if (_tagSuggestions.Count == 0) break;             _activeSuggestionIndex = Math.Max(_activeSuggestionIndex - 1, -1);             if (_activeSuggestionIndex == -1) _showSuggestions = _tagSuggestions.Count > 0;             break;         case "Enter":             if (_activeSuggestionIndex >= 0 && _activeSuggestionIndex < _tagSuggestions.Count)             {                 SelectSuggestion(_tagSuggestions[_activeSuggestionIndex]);             }             else             {                 // Fallback: enter with no selection uses the typed text (existing behaviour)                 AddTag();                 _showSuggestions = false;             }             break;         case "Escape":             _showSuggestions = false;             _activeSuggestionIndex = -1;             break;     } }`

> `OnTagKeyPress` (the existing Enter handler) is **replaced** by `OnTagKeyDown` so that Arrow keys — which do not fire `onkeypress` in modern browsers — are handled correctly.

---

## 2. `RecipeDetail.razor`

Replace the Tags section markup:

`<!-- Tags --> <div class="form-section">     <h2>Tags</h2>    <div class="tags-input-container">        <div class="tags-display">            @foreach (var tag in recipe.Tags)            {                <span class="tag-chip">                    @tag                    <button type="button" class="tag-remove" @onclick="() => RemoveTag(tag)">×</button>                </span>            }        </div>         <!-- Autocomplete wrapper — focusout fires HideSuggestions with delay -->        <div class="tag-autocomplete-wrapper" @onfocusout="HideSuggestions">            <div class="tag-input-row">                <input type="text"                       class="form-control"                       value="@newTag"                       @oninput="OnTagInputChanged"                       @onkeydown="OnTagKeyDown"                       placeholder="Add tag..."                       autocomplete="off" />                <button type="button" class="btn btn-secondary" @onclick="AddTag">Add Tag</button>            </div>             @if (_showSuggestions && _tagSuggestions.Any())            {                <ul class="tag-suggestions" role="listbox">                    @for (int i = 0; i < _tagSuggestions.Count; i++)                    {                        var suggestion = _tagSuggestions[i];                        var index      = i;                        <li class="tag-suggestion-item @(index == _activeSuggestionIndex ? "active" : "")"                            role="option"                            aria-selected="@(index == _activeSuggestionIndex)"                            @onmousedown="() => SelectSuggestion(suggestion)">                            @suggestion                        </li>                    }                </ul>            }        </div>    </div> </div>`

> **Why `@onmousedown` instead of `@onclick` on list items?**  
> `mousedown` fires before the input loses focus, so `HideSuggestions`'s 150 ms delay is enough to let the selection register before the list disappears.

> **Why split `value` + `@oninput` instead of `@bind`?**  
> Blazor's `@bind` uses the `change` event by default and `@bind:event="oninput"` cannot be combined with `@onkeydown` on the same element without interference. Explicit `value` + `@oninput` keeps full control over both events.

---

## 3. `RecipeDetail.razor.css`

Add below the existing `.tag-input-row` block:

`/* Autocomplete */ .tag-autocomplete-wrapper {     position: relative; } .tag-suggestions {     position: absolute;     top: calc(100% + 2px);     left: 0;     right: 0;     max-height: 12rem;     overflow-y: auto;     background: var(--color-bg-card, #fff);     border: 1px solid var(--color-border, #dee2e6);     border-radius: 8px;     box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);     list-style: none;     margin: 0;     padding: 0.25rem 0;     z-index: 10; } .tag-suggestion-item {     padding: 0.5rem 1rem;     cursor: pointer;     font-size: 0.875rem;     color: var(--color-text-primary, #1a1a1a);     transition: background 0.1s ease; } .tag-suggestion-item:hover, .tag-suggestion-item.active {     background: var(--color-primary-light, #e8f0fe);     color: var(--color-primary, #0066cc); }`

---

## Behaviour Summary

|Action|Result|
|---|---|
|Type into the tag input|Dropdown appears with tags that **start with** the typed text, already-added tags excluded|
|`↓` / `↑` Arrow keys|Move the highlighted item through the list|
|`Enter` with item highlighted|Selects the highlighted suggestion, clears input|
|`Enter` with nothing highlighted|Adds typed text as-is (existing behaviour)|
|`Escape`|Closes the dropdown|
|Click a suggestion|Adds it and closes the dropdown|
|Tab / click away|Closes the dropdown after 150 ms|
|List is empty|Dropdown hidden; no DOM rendered|
|Duplicate tag typed|`AddTag()` silently ignores it (existing guard)|