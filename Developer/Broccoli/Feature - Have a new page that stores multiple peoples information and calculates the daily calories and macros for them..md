# Todo



![[Pasted image 20260321111710.png]]
- The editable fields are off center to the column headers:
- Calorie defect, weight goals should be per row / person, not controlled in the settings.
- Need a mention in the setting / mouse over of the row how much weight is being lost at the difference goals and how fast.
- Need to round the calculated figures to 0 decimal places.
- Include information about percentages in columns headers (Example: if protien in set to 30%, show that in parenthese in the column header).
- A common workflow is making a recipe serving match someones calories / macros per meal.
	- So need to add support to the details page to support this.

---
# How much protein should we have
https://www.youtube.com/watch?v=j1bx0GMofYw
### General protein ranges (per kg of body weight)

| Level                 | Per kg           |
| --------------------- | ---------------- |
| Almost maximized      | 1.21 – 1.39 g/kg |
| Very likely maximized | 1.41 – 1.59 g/kg |
| Definitely maximized  | 1.61 – 2.20 g/kg |

### Daily protein targets for a 115 kg person

| Level                 | Min (g/day) | Max (g/day) |
| --------------------- | ----------- | ----------- |
| Almost maximized      | 139 g       | 160 g       |
| Very likely maximized | 162 g       | 183 g       |
| Definitely maximized  | 185 g       | 253 g       |
|                       |             |             |

---
# Feature Plan: Macro / Calorie Targets Page

**Date:** March 21, 2026  
**Project:** Broccoli.App (.NET 9 MAUI Blazor Hybrid + Blazor Web)

---

## Overview

Add a new `/macro-targets` page with an inline-editable, mobile-responsive table. Users manage multiple named profiles with editable inputs (Name, Gender, Weight, Height, Age, Activity); all other fields are auto-calculated on each change and persisted to Azure Cosmos DB. A settings dialog controls formula choices and macro split methods per user.

---

## Files to Create

|File|Purpose|
|---|---|
|`Broccoli.App.Shared/Models/MacroTarget.cs`|Row data model|
|`Broccoli.App.Shared/Models/MacroTargetSettings.cs`|Per-user settings + all enums|
|`Broccoli.App.Shared/Services/IMacroTargetService.cs`|Service interface|
|`Broccoli.App.Shared/Services/CosmosMacroTargetService.cs`|Cosmos DB implementation|
|`Broccoli.App.Shared/Services/MacroCalculatorService.cs`|Pure stateless calculation logic|
|`Broccoli.App.Shared/Components/MacroTargetSettingsDialog.razor`|Settings modal component|
|`Broccoli.App.Shared/Components/MacroTargetSettingsDialog.razor.css`|Modal scoped styles|
|`Broccoli.App.Shared/Pages/MacroTargets.razor`|Main page|
|`Broccoli.App.Shared/Pages/MacroTargets.razor.css`|Page + table scoped styles|

## Files to Modify

|File|Change|
|---|---|
|`Broccoli.App/MauiProgram.cs`|Register new services|
|`Broccoli.App.Web/Program.cs`|Register + initialize new services|
|`Broccoli.App.Shared/Layout/NavMenu.razor`|Add nav link|

---

## Step-by-Step Implementation

### Step 1 — `MacroTarget.cs`

Create in `Broccoli.App.Shared/Models/`. Use `[JsonPropertyName]` attributes throughout, matching the existing `PantryItem` pattern.

**Fields:**

|Property|Type|Notes|
|---|---|---|
|`Id`|`string`|`Guid.NewGuid().ToString()`|
|`UserId`|`string`|Set by service|
|`PartitionKey`|`string`|Hard-coded `"macrotarget"`|
|`Name`|`string`|User-editable|
|`Gender`|`GenderType` enum|`Male` / `Female` / `Other`|
|`WeightKg`|`double`|Stored always in kg; display converted if Imperial|
|`HeightCm`|`double`|Stored always in cm; display converted if Imperial|
|`Age`|`int`|User-editable|
|`ActivityLevel`|`ActivityLevel` enum|See multipliers below|
|`Bmr`|`double`|Calculated, stored|
|`Tdee`|`double`|Calculated, stored|
|`RecommendedCalories`|`double`|Calculated, stored|
|`RecommendedProteinG`|`double`|Calculated, stored|
|`RecommendedCarbsG`|`double`|Calculated, stored|
|`RecommendedFatG`|`double`|Calculated, stored|
|`CreatedAt`|`DateTime`|Set on creation|
|`UpdatedAt`|`DateTime`|Updated on every save|

---

### Step 2 — `MacroTargetSettings.cs`

Create in `Broccoli.App.Shared/Models/`. One document per user in Cosmos DB.

**Fields:**

|Property|Type|Default|
|---|---|---|
|`Id`|`string`|`Guid.NewGuid().ToString()`|
|`UserId`|`string`|Set by service|
|`PartitionKey`|`string`|`"macrotargetsettings"`|
|`BmrFormula`|`BmrFormula` enum|`MifflinStJeor`|
|`ProteinMethod`|`ProteinMethod` enum|`RatioPercent`|
|`ProteinPercent`|`double`|`30`|
|`CarbPercent`|`double`|`40`|
|`FatPercent`|`double`|`30`|
|`ProteinGramsPerKg`|`double`|`1.8`|
|`Goal`|`Goal` enum|`Maintain`|
|`GoalCalorieDelta`|`int`|`0`|
|`UnitSystem`|`UnitSystem` enum|`Metric`|

**Enums (defined in the same file):**

`BmrFormula      : MifflinStJeor, HarrisBenedict ProteinMethod   : RatioPercent, GramsPerKg Goal            : Maintain, Lose, Gain UnitSystem      : Metric, Imperial GenderType      : Male, Female, Other ActivityLevel   : Sedentary, LightlyActive, ModeratelyActive, VeryActive, ExtraActive`

---

### Step 3 — `MacroCalculatorService.cs`

Create in `Broccoli.App.Shared/Services/`. Pure stateless service, registered as `AddSingleton`. No Cosmos DB dependency.

**Public API:**

`public void Calculate(MacroTarget target, MacroTargetSettings settings)`

Mutates the six calculated fields on `target` in-place.

**Calculation logic:**

#### Unit Conversion (always convert to metric before formulas)

- Imperial weight: `lbs ÷ 2.20462 = kg`
- Imperial height: `inches × 2.54 = cm`

#### BMR — Mifflin-St Jeor (default)

|Gender|Formula|
|---|---|
|Male|`(10 × kg) + (6.25 × cm) − (5 × age) + 5`|
|Female|`(10 × kg) + (6.25 × cm) − (5 × age) − 161`|
|Other|Average of Male and Female result|

#### BMR — Harris-Benedict (alternative)

|Gender|Formula|
|---|---|
|Male|`88.362 + (13.397 × kg) + (4.799 × cm) − (5.677 × age)`|
|Female|`447.593 + (9.247 × kg) + (3.098 × cm) − (4.330 × age)`|
|Other|Average of Male and Female result|

#### TDEE

`TDEE = BMR × ActivityMultiplier`

|ActivityLevel|Multiplier|
|---|---|
|Sedentary|`1.200`|
|LightlyActive|`1.375`|
|ModeratelyActive|`1.550`|
|VeryActive|`1.725`|
|ExtraActive|`1.900`|

#### Recommended Calories

`RecommendedCalories = TDEE + GoalCalorieDelta`

#### Macros — `ProteinMethod.RatioPercent`

`ProteinG = (RecommendedCalories × ProteinPercent / 100) / 4 CarbsG   = (RecommendedCalories × CarbPercent   / 100) / 4 FatG     = (RecommendedCalories × FatPercent    / 100) / 9`

#### Macros — `ProteinMethod.GramsPerKg`

`ProteinG         = WeightKg × ProteinGramsPerKg ProteinCalories  = ProteinG × 4 RemainingCalories = RecommendedCalories − ProteinCalories // Remaining split between Carbs and Fat by their relative ratio: carbRatio = CarbPercent / (CarbPercent + FatPercent) fatRatio  = FatPercent  / (CarbPercent + FatPercent) CarbsG = (RemainingCalories × carbRatio) / 4 FatG   = (RemainingCalories × fatRatio)  / 9`

---

### Step 4 — `IMacroTargetService.cs`

Create in `Broccoli.App.Shared/Services/`.

`Task InitializeAsync(); Task<List<MacroTarget>> GetAllAsync(string userId); Task<MacroTarget> AddAsync(MacroTarget target); Task<MacroTarget> UpdateAsync(MacroTarget target); Task DeleteAsync(string id, string userId); Task<MacroTargetSettings> GetSettingsAsync(string userId); Task<MacroTargetSettings> SaveSettingsAsync(MacroTargetSettings settings);`

---

### Step 5 — `CosmosMacroTargetService.cs`

Create in `Broccoli.App.Shared/Services/`. Mirrors `CosmosRecipeService` pattern. Inject `CosmosClient`, `IAuthenticationStateService`, `ILogger`.

**Two Cosmos DB containers (both sharing database throughput):**

|Container|Partition Key|
|---|---|
|`MacroTargets`|`/userId`|
|`MacroTargetSettings`|`/userId`|

**Key behaviour:**

- `GetSettingsAsync`: queries by `userId`; if no document exists, returns a `new MacroTargetSettings()` with all defaults — does **not** persist until the user explicitly saves.
- `SaveSettingsAsync`: upserts (replaces if exists, creates if not).
- All target operations filter by `CurrentUserId` from `IAuthenticationStateService`, matching the recipe service pattern.

---

### Step 6 — `MacroTargetSettingsDialog.razor`

Create in `Broccoli.App.Shared/Components/`. Follows the backdrop + modal-box pattern from `AddIngredientsDialog.razor`.

**Parameters:** `bool IsVisible`, `MacroTargetSettings Settings`, `EventCallback<MacroTargetSettings> OnSave`, `EventCallback OnCancel`

**Dialog sections:**

1. **Units** — toggle buttons: `Metric` / `Imperial`
2. **BMR Formula** — radio group: `Mifflin-St Jeor` (recommended) / `Harris-Benedict`
3. **Goal** — dropdown: `Maintain` / `Lose` / `Gain` with a number input for `GoalCalorieDelta`. When Goal changes, auto-suggest delta: Maintain → `0`, Lose → `-500`, Gain → `+250` (user can override).
4. **Protein Method** — radio group:
    - **`% of Calories`**: shows three number inputs for Protein %, Carbs %, Fat % with a live sum indicator. Save button disabled if sum ≠ 100.
    - **`g per kg of bodyweight`**: shows a single number input for `ProteinGramsPerKg` (e.g. `1.8`), plus Carbs % and Fat % inputs (these become the split ratio for remaining calories after protein is subtracted).
5. **Save / Cancel** buttons.

---

### Step 7 — `MacroTargets.razor`

Create in `Broccoli.App.Shared/Pages/` at `@page "/macro-targets"`. Wrapped in `<AuthorizeView>`.

**Page header:**

- `🎯 Macro Targets` title
- `＋ Add Person` button — creates a blank `MacroTarget`, calls `AddAsync`, runs `Calculate`, appends to list
- `⚙️ Settings` button — opens `MacroTargetSettingsDialog`; on save, re-runs `Calculate` on all rows and calls `UpdateAsync` for each

**Table columns (in order):**

|Column|Input Type|Editable?|
|---|---|---|
|Name|`<input type="text">`|✅|
|Gender|`<select>` (Male/Female/Other)|✅|
|Weight|`<input type="number">` (header: kg or lbs)|✅|
|Height|`<input type="number">` (header: cm or in)|✅|
|Age|`<input type="number">`|✅|
|Activity|`<select>` (5 predefined levels)|✅|
|BMR|Read-only text|❌|
|TDEE|Read-only text|❌|
|Calories|Read-only text|❌|
|Protein (g)|Read-only text|❌|
|Carbs (g)|Read-only text|❌|
|Fat (g)|Read-only text|❌|
|—|🗑️ Delete button|—|

**`@onchange` behaviour (all editable fields):**

1. Update the field on the `MacroTarget` object
2. Call `MacroCalculatorService.Calculate(target, settings)`
3. Call `IMacroTargetService.UpdateAsync(target)`
4. Call `StateHasChanged()`

**Empty state:** When no rows exist, show a centred empty-state card with a prompt to add a person.

**Mobile layout:** Wrap `<table>` in a `<div class="table-scroll-wrapper">` with `overflow-x: auto`. Column min-widths set so the table is readable on tablets (~768 px). On screens below 480 px, input font-size reduced slightly to fit more content.

---

### Step 8 — Register Services & Navigation

#### `MauiProgram.cs`

`builder.Services.AddSingleton<IMacroTargetService, CosmosMacroTargetService>(); builder.Services.AddSingleton<MacroCalculatorService>();`

#### `Broccoli.App.Web/Program.cs`

`builder.Services.AddSingleton<IMacroTargetService, CosmosMacroTargetService>(); builder.Services.AddSingleton<MacroCalculatorService>(); // ... var macroTargetService = app.Services.GetRequiredService<IMacroTargetService>(); await macroTargetService.InitializeAsync();`

#### `NavMenu.razor`

`<div class="nav-item px-3">     <NavLink class="nav-link" href="macro-targets">        <span aria-hidden="true">🎯</span> Macro Targets    </NavLink> </div>`

---

## Further Considerations

1. **`Other` gender in BMR** — the plan defaults `Other` to the average of the Male and Female formula constants. An alternative is to let the user select which offset to apply. Confirm this average approach is acceptable before implementation.
    
2. **Goal delta auto-suggest** — when changing the Goal dropdown, the dialog will auto-suggest a calorie delta (0 / −500 / +250) but leave it editable. This keeps the UX intuitive while allowing full override.
    
3. **Scoped CSS** — every new `.razor` file gets a companion `.razor.css` scoped stylesheet, consistent with `Pantry.razor.css`, `GroceryList.razor.css`, etc.
    
4. **Rounding** — calculated macro values will be rounded to 1 decimal place for display and storage to avoid floating-point noise in the UI.