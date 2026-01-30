# TODO
- Another blatant UI bug:
![[Pasted image 20260321135722.png]]
# Rouch Spec
- I want a new page in the application called Meal Prep Planning.
- It start empty, with the option of adding a new Meal Prep Plan via a button click.
- I should be able to name and edit the name of the Meal Prep Plans.
- They should persisted in the cosmos.
- Once you have created a Meal Prep Plann, you can click a button to add recipes to the plan. 
	- This should popup a dialog with a list of all of the existing recipes.
	- You can click a checkbox besides each recipes to add it to the Meal Prep Plan.
- All menus should be viewable on this page, with their menu items nested underneath them in the menu page.
- There should be an option to add ingredients from the menu to the shopping cart. This should looks and behave similar to the feature for adding to shopping car ton the Recipes page. 

# Implementation Plan: Meal Prep Planning

---

## Overview

A new **Meal Prep Plans** page lets users create named plans, attach any number of their existing recipes to each plan, and add the combined ingredient list to the grocery cart in one action. Plans are persisted per-user in CosmosDB, following exactly the same patterns as `CosmosRecipeService` and `CosmosMacroTargetService`.

---

## Codebase Context

|Concern|Where it lives today|
|---|---|
|CosmosDB service pattern|`CosmosRecipeService.cs` — partition key `/userId`, lazy-init, `EnsureAuthenticated()`|
|Grocery cart add|`AddIngredientsDialog` → `IGroceryListService.AddMultipleAsync`|
|Pantry-aware ingredient dialog|`AddIngredientsDialog.razor` — reused as-is|
|Auth helper|`IAuthenticationStateService.CurrentUserId` / `IsAuthenticated`|
|Page + code-behind pattern|`Recipes.razor` + `Recipes.razor.cs` + `Recipes.razor.css`|
|DI registration|`Broccoli.App.Web/Program.cs` and `Broccoli.App/MauiProgram.cs`|
|Nav|`Broccoli.App.Shared/Layout/NavMenu.razor`|
|CosmosDB database id|`"BroccoliAppDb"` (shared across all containers)|

---

## Step 1 — Data Model

**New file:** `Broccoli.App.Shared/Models/MealPrepPlan.cs`

![](http://localhost:63342/markdownPreview/800732062/)

`using System.Text.Json.Serialization; namespace Broccoli.Data.Models; public class MealPrepPlan {     [JsonPropertyName("id")]     public string Id { get; set; } = Guid.NewGuid().ToString();     /// <summary>User-chosen display name, e.g. "Week 1 – Bulking".</summary>     [JsonPropertyName("name")]     public string Name { get; set; } = string.Empty;     /// <summary>     /// Ordered list of recipe IDs included in this plan.     /// The full Recipe objects are loaded and joined in memory on the client.     /// </summary>     [JsonPropertyName("recipeIds")]     public List<string> RecipeIds { get; set; } = new();     [JsonPropertyName("userId")]     public string UserId { get; set; } = string.Empty;     [JsonPropertyName("createdAt")]     public DateTime CreatedAt { get; set; } = DateTime.UtcNow;     [JsonPropertyName("updatedAt")]     public DateTime? UpdatedAt { get; set; } }`

**Design notes:**

- Only `RecipeIds` is stored — not embedded recipe copies. This avoids CosmosDB document size concerns and stale-data problems: if a recipe is renamed or deleted, the plan simply drops the missing entry at render time.
- Partition key is `/userId`, matching `Recipes` and `MacroTargets` containers.

---

## Step 2 — Service Interface

**New file:** `Broccoli.App.Shared/Services/IMealPrepPlanService.cs`

![](http://localhost:63342/markdownPreview/800732062/)

`using Broccoli.Data.Models; namespace Broccoli.App.Shared.Services; public interface IMealPrepPlanService {     Task InitializeAsync();     Task<List<MealPrepPlan>> GetAllAsync();     Task<MealPrepPlan> AddAsync(MealPrepPlan plan);     Task<MealPrepPlan> UpdateAsync(MealPrepPlan plan);     Task DeleteAsync(string planId); }`

---

## Step 3 — Service Implementation

**New file:** `Broccoli.App.Shared/Services/CosmosMealPrepPlanService.cs`

Follow `CosmosRecipeService` exactly:

- Constructor: `CosmosClient`, `IAuthenticationStateService`, `ILogger<CosmosMealPrepPlanService>`
- Constants: `DatabaseId = "BroccoliAppDb"`, `ContainerId = "MealPrepPlans"`
- `InitializeAsync()`: `CreateContainerIfNotExistsAsync` with `PartitionKeyPath = "/userId"` — no dedicated throughput (shares database RU/s)
- `EnsureInitializedAsync()` + `EnsureAuthenticated()` + `CurrentUserId` property — identical pattern to `CosmosRecipeService`

**Method implementations:**

|Method|Notes|
|---|---|
|`GetAllAsync()`|`SELECT * FROM c WHERE c.userId = @userId ORDER BY c.createdAt DESC`|
|`AddAsync(plan)`|Set `plan.UserId`, `plan.Id = Guid.NewGuid()`, `plan.CreatedAt`, then `CreateItemAsync`|
|`UpdateAsync(plan)`|Load existing first, verify ownership, set `plan.UpdatedAt`, then `ReplaceItemAsync`|
|`DeleteAsync(planId)`|Load to verify ownership, then `DeleteItemAsync`|

---

## Step 4 — `AddRecipesToPlanDialog` Component

**New files:**

- `Broccoli.App.Shared/Components/AddRecipesToPlanDialog.razor`
- `Broccoli.App.Shared/Components/AddRecipesToPlanDialog.razor.css`

A modal dialog that shows the user's full recipe list as a checkbox list. Recipes already in the plan are pre-checked.

**Parameters:**

![](http://localhost:63342/markdownPreview/800732062/)

`[Parameter] public bool IsVisible { get; set; } [Parameter] public string? PlanName { get; set; }          // shown in the dialog title [Parameter] public List<Recipe> AllRecipes { get; set; } = new(); [Parameter] public List<string> AlreadySelectedIds { get; set; } = new(); [Parameter] public EventCallback OnCancel { get; set; } [Parameter] public EventCallback<List<string>> OnConfirm { get; set; }  // returns selected IDs`

**Layout:**

![](http://localhost:63342/markdownPreview/800732062/)

`┌──────────────────────────────────────────────┐ │  📋  Add Recipes — "Week 1"              [×] │ ├──────────────────────────────────────────────┤ │  🔍  [Search recipes...              ]       │ │                                              │ │  ☑ Butter Chicken                           │ │  ☐ Peanut Noodles                           │ │  ☑ Green Smoothie                           │ │  ...                                         │ ├──────────────────────────────────────────────┤ │  [Cancel]              [Add Selected (2)]    │ └──────────────────────────────────────────────┘`

- A local `searchTerm` string filters the displayed list in real time (`recipe.Name.Contains`).
- Pre-check any recipe whose ID is already in `AlreadySelectedIds`.
- `OnConfirm` returns the **full** list of currently-checked IDs (not just new additions) so the parent can simply replace `plan.RecipeIds` with the returned list.

**CSS** should match `AddIngredientsDialog.razor.css` (same modal backdrop, modal-content-box, header/body/footer layout).

---

## Step 5 — Meal Prep Plans Page

**New files:**

- `Broccoli.App.Shared/Pages/MealPrepPlans.razor`
- `Broccoli.App.Shared/Pages/MealPrepPlans.razor.cs`
- `Broccoli.App.Shared/Pages/MealPrepPlans.razor.css`

Route: `@page "/meal-prep"`

### Injections

![](http://localhost:63342/markdownPreview/800732062/)

`@inject IMealPrepPlanService MealPrepPlanService @inject IRecipeService RecipeService @inject IGroceryListService GroceryListService @inject IPantryService PantryService @inject IAuthenticationStateService AuthStateService @inject IJSRuntime JSRuntime`

### Page layout

![](http://localhost:63342/markdownPreview/800732062/)

`┌──────────────────────────────────────────────────────┐ │  Meal Prep Plans                   [+ New Plan]      │ ├──────────────────────────────────────────────────────┤ │                                                      │ │  ▼  Week 1 – Bulking  [✏ rename] [🛒 Add to Cart] [🗑] │ │  ├── Butter Chicken                                  │ │  ├── Peanut Noodles                                  │ │  └── [+ Add Recipes]                                 │ │                                                      │ │  ▶  Quick Dinners                                    │ │                                                      │ └──────────────────────────────────────────────────────┘`

### State fields

![](http://localhost:63342/markdownPreview/800732062/)

`private List<MealPrepPlan> _plans = new(); private List<Recipe> _allRecipes = new(); private List<PantryItem> _pantryItems = new(); private bool _isLoading = true; // Inline rename state private string? _editingPlanId;       // ID of the plan currently being renamed private string _editingName = string.Empty; // AddRecipesToPlanDialog state private bool _showAddRecipesDialog; private MealPrepPlan? _targetPlan;    // which plan the dialog is for // AddIngredientsDialog state (cart) private bool _showCartDialog; private MealPrepPlan? _cartPlan;      // which plan is being sent to cart private string _combinedIngredients = string.Empty; private string _combinedPlanName = string.Empty;`

### `OnInitializedAsync`

1. `await MealPrepPlanService.GetAllAsync()` → populate `_plans`
2. `await RecipeService.GetAllAsync()` → populate `_allRecipes` (needed for joining recipe names and combining ingredients)
3. `await PantryService.GetAllAsync(userId)` → populate `_pantryItems` (passed to cart dialog)

### Plan card behaviour

**Expand/collapse:** Each card is expanded by default. Track with a `HashSet<string> _expandedPlanIds`. Clicking the plan header toggles.

**Inline rename:**

- Clicking ✏ sets `_editingPlanId = plan.Id` and `_editingName = plan.Name`.
- Renders an `<input>` in place of the name `<span>` — focus it automatically with `@ref` + `ElementReference.FocusAsync()`.
- Pressing Enter or blurring the input calls `SaveRename()`.
- `SaveRename()` updates `plan.Name`, calls `await MealPrepPlanService.UpdateAsync(plan)`.

**New plan:**

- Clicking **+ New Plan** creates a `MealPrepPlan { Name = "New Plan" }`, calls `AddAsync`, inserts it into `_plans`, then immediately opens inline rename on it so the user can type the name straight away.

**Delete plan:**

- `await JSRuntime.InvokeAsync<bool>("confirm", ...)` → `MealPrepPlanService.DeleteAsync(plan.Id)` → remove from `_plans`.

**Add Recipes button (per plan):**

- Sets `_targetPlan = plan` and `_showAddRecipesDialog = true`.
- `AddRecipesToPlanDialog` is opened with `AllRecipes = _allRecipes` and `AlreadySelectedIds = plan.RecipeIds`.
- `OnConfirm(List<string> selectedIds)` handler:
    - Sets `plan.RecipeIds = selectedIds`.
    - Calls `await MealPrepPlanService.UpdateAsync(plan)`.
    - Closes dialog.

**Displaying recipe rows under a plan:**

![](http://localhost:63342/markdownPreview/800732062/)

`// In the razor template — join in memory @foreach (var recipeId in plan.RecipeIds) {     var recipe = _allRecipes.FirstOrDefault(r => r.Id == recipeId);     if (recipe is not null)     {         // render recipe row     }     // silently skip deleted recipes }`

**🛒 Add to Cart (per plan):**

Reuses the existing `AddIngredientsDialog` component without modification. Behaviour:

1. Clicking the button builds a combined ingredient string:
    
    ![](http://localhost:63342/markdownPreview/800732062/)
    
    `_combinedIngredients = string.Join("\n",     plan.RecipeIds         .Select(id => _allRecipes.FirstOrDefault(r => r.Id == id))         .Where(r => r is not null)         .Select(r => r!.Ingredients)); _combinedPlanName = plan.Name; _cartPlan = plan; _showCartDialog = true;`
    
2. `AddIngredientsDialog` is opened with `IngredientsText="@_combinedIngredients"` and `RecipeName="@_combinedPlanName"`.
3. `OnConfirm(List<string> selectedLines)` handler is identical to the one in `Recipes.razor.cs` — maps lines to `GroceryListItem` objects and calls `GroceryListService.AddMultipleAsync`.

---

## Step 6 — DI Registration

### `Broccoli.App.Web/Program.cs`

Add alongside the other service registrations:

![](http://localhost:63342/markdownPreview/800732062/)

`builder.Services.AddSingleton<IMealPrepPlanService, CosmosMealPrepPlanService>();`

And in the startup initialisation block (after `macroTargetService.InitializeAsync()`):

![](http://localhost:63342/markdownPreview/800732062/)

`var mealPrepPlanService = app.Services.GetRequiredService<IMealPrepPlanService>(); await mealPrepPlanService.InitializeAsync();`

### `Broccoli.App/MauiProgram.cs`

Add alongside the other services:

![](http://localhost:63342/markdownPreview/800732062/)

`builder.Services.AddSingleton<IMealPrepPlanService, CosmosMealPrepPlanService>();`

MAUI services are lazy-initialised (the container is created on first use) so no explicit `InitializeAsync()` call is needed at startup — `EnsureInitializedAsync()` handles it.

---

## Step 7 — Navigation

**File:** `Broccoli.App.Shared/Layout/NavMenu.razor`

Add a new nav item below **Recipes**:

![](http://localhost:63342/markdownPreview/800732062/)

`<div class="nav-item px-3">     <NavLink class="nav-link" href="meal-prep">        <span aria-hidden="true">📋</span> Meal Prep    </NavLink> </div>`

---

## Step 8 — Unit Tests (optional, recommended)

**New file:** `Broccoli.App.UnitTests/Services/MealPrepPlanServiceTests.cs`

Since the service is a thin CosmosDB wrapper, unit tests should mock `IMealPrepPlanService` rather than the concrete class. Focus on page-level logic:

|Test|Scenario|
|---|---|
|`BuildCombinedIngredients_MultipleRecipes_ConcatenatesCorrectly`|Joining ingredient strings from multiple recipes|
|`HandleAddRecipesConfirm_ReplacesRecipeIds`|Confirm dialog → `plan.RecipeIds` updated|
|`DeletePlan_RemovesFromLocalList`|After delete, plan is removed from `_plans`|
|`SaveRename_UpdatesPlanName`|Rename flow calls `UpdateAsync` with new name|
|`NewPlan_AppearsInListAndEntersEditMode`|New plan → added to `_plans`, `_editingPlanId` set|

---

## File Summary

|Status|Path|
|---|---|
|**New**|`Broccoli.App.Shared/Models/MealPrepPlan.cs`|
|**New**|`Broccoli.App.Shared/Services/IMealPrepPlanService.cs`|
|**New**|`Broccoli.App.Shared/Services/CosmosMealPrepPlanService.cs`|
|**New**|`Broccoli.App.Shared/Components/AddRecipesToPlanDialog.razor`|
|**New**|`Broccoli.App.Shared/Components/AddRecipesToPlanDialog.razor.css`|
|**New**|`Broccoli.App.Shared/Pages/MealPrepPlans.razor`|
|**New**|`Broccoli.App.Shared/Pages/MealPrepPlans.razor.cs`|
|**New**|`Broccoli.App.Shared/Pages/MealPrepPlans.razor.css`|
|**Modified**|`Broccoli.App.Web/Program.cs` — register + initialise service|
|**Modified**|`Broccoli.App/MauiProgram.cs` — register service|
|**Modified**|`Broccoli.App.Shared/Layout/NavMenu.razor` — add nav item|
|**New** _(optional)_|`Broccoli.App.UnitTests/Services/MealPrepPlanServiceTests.cs`|

---

## Open Questions / Decisions Deferred

1. **Recipe removal from a plan.** The spec doesn't mention removing individual recipes from a plan. The `AddRecipesToPlanDialog` approach (replace the full ID list on confirm) naturally handles this — unchecking a recipe removes it.
    
2. **Empty ingredient lines between recipes.** When building `_combinedIngredients`, consider whether a blank separator line between each recipe's block helps the existing `IngredientParserService` or causes noise. The parser already skips empty lines, so it should be harmless.
    
3. **Plan ordering.** Plans are returned `ORDER BY c.createdAt DESC` (newest first). A drag-to-reorder feature could be added later by storing an explicit `sortOrder` integer on the model.
    
4. **Recipe display in plan cards.** The spec doesn't require showing recipe images or macros inside the plan card — just names. If richer recipe rows are wanted later, the card can embed a lightweight read-only recipe summary using existing model data.
    
5. **"Add to Cart" scope.** Currently specified as "add all ingredients from the plan". A per-recipe "Add to Cart" button inside the expanded card would be a straightforward addition (simply pass that single recipe's `Ingredients` to `AddIngredientsDialog`).