# Plan: Vertical Slice Architecture for Broccoli.App

VSA applied to this solution means reorganising `Broccoli.App.Shared/` by **feature** rather than by technical layer. Each feature "slice" becomes a self-contained sub-folder owning its Razor pages, code-behind, CSS, service interfaces, implementations, and DI wiring. No MediatR/CQRS is needed — the existing `IXxxService` pattern is kept; the change is purely organisational. Both host projects stay thin and call per-slice DI extension methods instead of registering everything inline.

---

## Section 1 — What VSA Means Here

One folder = one feature = everything that feature needs. The existing `IRecipeService`/`CosmosRecipeService` pattern is preserved; only the physical location and namespace of files changes. The dual-host constraint (MAUI + Web) is respected by keeping `IFormFactor` and `ISecureStorageService` out of slices — they live in a `_Shared/Platform/` area and are still implemented per-host.

---

## Section 2 — Feature Slices Identified

|Slice|Pages|Components|Services|
|---|---|---|---|
|**Auth**|`Login`|`AuthorizeView`|`IAuthenticationService`, `IAuthenticationStateService`, `AuthenticationStateService`, `AuthenticationService`|
|**Recipes**|`Recipes`, `RecipeDetail`, `RecipeReadOnly`|`ImportRecipesDialog`, `MarkdownRenderer`|`IRecipeService`, `CosmosRecipeService`, `RecipeImportService`, `IImportFormat`, `PaprikaHtmlImportFormat`, `IRecipeImageService`, `CloudinaryImageService`|
|**Foods**|`Foods`|`UsdaSearchDialog`|`IUsdaFoodSearchService`, `UsdaFoodSearchService`|
|**Pantry**|`Pantry`|_(none)_|`IPantryService`, `PantryService`|
|**GroceryList**|`GroceryList`|`AddIngredientsDialog`|`IGroceryListService`, `GroceryListService`, `IngredientCartService`|
|**MealPrep**|`MealPrepPlans`|`AddRecipesToPlanDialog`|`IMealPrepPlanService`, `CosmosMealPrepPlanService`|
|**Nutrition**|`DailyFoodPlanning`, `MacroTargets`|`MacroTargetSettingsDialog`|`IDailyFoodPlanService`, `CosmosDailyFoodPlanService`, `IMacroTargetService`, `CosmosMacroTargetService`, `MacroCalculatorService`|
|**Seasonality**|_(none — service only)_|`SeasonalityBadge`, `SeasonalityPanel`|`ISeasonalityService`, `LocalJsonSeasonalityService`, `SeasonHelper`|
|**AppSettings**|_(none — dialog only)_|`AppSettingsDialog`|`IThemeService`, `ThemeService`|

**Cross-cutting (not owned by any slice):** `IngredientParserService`, `LocalJsonFoodService`, `IFoodService`, `CosmosDbService`/`ICosmosDbService`, all settings POCOs, `IFormFactor`, `ISecureStorageService`, `ParsedIngredientsTable`.

---

## Section 3 — Proposed Folder Structure (Before → After)

### Before

`Broccoli.App.Shared/     Pages/        Recipes.razor + .cs + .css        RecipeDetail.razor + .cs + .css        Foods.razor + .cs + .css        GroceryList.razor + .cs + .css        Pantry.razor + .cs + .css        MealPrepPlans.razor + .cs + .css        DailyFoodPlanning.razor + .cs + .css        MacroTargets.razor + .css        Login.razor + .css        NotFound.razor    Components/        AddIngredientsDialog.razor + .cs + .css        AddRecipesToPlanDialog.razor + .css        AppSettingsDialog.razor + .cs + .css        AuthorizeView.razor        ImportRecipesDialog.razor + .cs + .css        MacroTargetSettingsDialog.razor + .css        MarkdownRenderer.razor        ParsedIngredientsTable.razor + .cs + .css        SeasonalityBadge.razor + .css        SeasonalityPanel.razor + .css        UsdaSearchDialog.razor + .cs + .css    Services/        AuthenticationService.cs        AuthenticationStateService.cs        CloudinaryImageService.cs        ... (40+ files)        IngredientParsing/            IFoodService.cs            IngredientParserService.cs            LocalJsonFoodService.cs            ParsedIngredient.cs            ParsedIngredientMatch.cs    Configuration/    Models/    Layout/    Data/    wwwroot/`

### After

`Broccoli.App.Shared/     _Imports.razor    Routes.razor         Slices/        Auth/            Login.razor + .css            AuthorizeView.razor            IAuthenticationService.cs            IAuthenticationStateService.cs            AuthenticationService.cs            AuthenticationStateService.cs            AuthSliceExtensions.cs           ← services.AddAuthSlice(...)                 Recipes/            Recipes.razor + .cs + .css            RecipeDetail.razor + .cs + .css            RecipeReadOnly.razor + .cs + .css            MarkdownRenderer.razor            Import/                ImportRecipesDialog.razor + .cs + .css                IImportFormat.cs                RecipeImportService.cs                PaprikaHtmlImportFormat.cs            IRecipeService.cs            IRecipeImageService.cs            CosmosRecipeService.cs            CloudinaryImageService.cs            SupabaseImageService.cs            RecipesSliceExtensions.cs                 Foods/            Foods.razor + .cs + .css            UsdaSearchDialog.razor + .cs + .css            IUsdaFoodSearchService.cs            UsdaFoodSearchService.cs            FoodsSliceExtensions.cs                 Pantry/            Pantry.razor + .cs + .css            IPantryService.cs            PantryService.cs            PantrySliceExtensions.cs                 GroceryList/            GroceryList.razor + .cs + .css            AddIngredientsDialog.razor + .cs + .css            IGroceryListService.cs            GroceryListService.cs            IngredientCartService.cs            GroceryListSliceExtensions.cs                 MealPrep/            MealPrepPlans.razor + .cs + .css            AddRecipesToPlanDialog.razor + .css            IMealPrepPlanService.cs            CosmosMealPrepPlanService.cs            MealPrepSliceExtensions.cs                 Nutrition/            DailyFoodPlanning.razor + .cs + .css            MacroTargets.razor + .css            MacroTargetSettingsDialog.razor + .css            IDailyFoodPlanService.cs            CosmosDailyFoodPlanService.cs            IMacroTargetService.cs            CosmosMacroTargetService.cs            MacroCalculatorService.cs            NutritionSliceExtensions.cs                 Seasonality/            ISeasonalityService.cs            LocalJsonSeasonalityService.cs            SeasonHelper.cs            SeasonalityBadge.razor + .css            SeasonalityPanel.razor + .css            SeasonalitySliceExtensions.cs                 AppSettings/            AppSettingsDialog.razor + .cs + .css            IThemeService.cs            ThemeService.cs            AppSettingsSliceExtensions.cs         _Shared/        Infrastructure/            CosmosDbService.cs            ICosmosDbService.cs        IngredientParsing/            IFoodService.cs            IngredientParserService.cs            LocalJsonFoodService.cs            ParsedIngredient.cs            ParsedIngredientMatch.cs            ParsedIngredientsTable.razor + .cs + .css            IngredientParsingExtensions.cs        Platform/            IFormFactor.cs            ISecureStorageService.cs         Configuration/        ← unchanged    Models/               ← unchanged (Broccoli.Data.Models namespace preserved)    Data/                 ← unchanged    Layout/               ← unchanged    wwwroot/              ← unchanged`

**Namespace convention:**

- Slice files → `Broccoli.App.Shared.Slices.<SliceName>`
- `_Shared/Infrastructure/` → `Broccoli.App.Shared.Infrastructure`
- `_Shared/IngredientParsing/` → `Broccoli.App.Shared.IngredientParsing`
- `_Shared/Platform/` → `Broccoli.App.Shared.Platform`

---

## Section 4 — Cross-Cutting Concerns

|Concern|Resolution|
|---|---|
|**Auth guard (`Routes.razor`)**|Stays at root; injects `IAuthenticationStateService` from Auth slice namespace. No structural change.|
|**IngredientParsing pipeline**|Lives in `_Shared/IngredientParsing/`. Registered via `AddIngredientParsing(services, foodDbPath)`. Consumed by GroceryList, DailyFoodPlanning, and MealPrep via normal DI injection.|
|**Feature flags**|`FeatureFlagsSettings` stays in `Configuration/`. `FoodsSliceExtensions.cs` accepts `FeatureFlagsSettings` and conditionally registers `IUsdaFoodSearchService`: `if (flags.FoodDatabaseEditing) services.AddScoped<IUsdaFoodSearchService, UsdaFoodSearchService>();`. MAUI passes `FoodDatabaseEditing = false` — no USDA service registered, same as today.|
|**Platform abstractions**|`IFormFactor` and `ISecureStorageService` move to `_Shared/Platform/`. Both host-side implementations continue to implement these interfaces unchanged.|
|**CosmosDB `InitializeAsync()`**|Hosts keep explicit `await xyzService.InitializeAsync()` startup calls. Slice extensions only register services. (A future `IStartupInitializer` pattern could clean this up later.)|
|**`_Imports.razor`**|Add `@using Broccoli.App.Shared.Slices` and `@using Broccoli.App.Shared.IngredientParsing` so Razor markup resolves types without per-component using statements.|

---

## Section 5 — Phased Migration

Each phase keeps the build green. Files are moved and namespaces updated in the same commit; dependent `using` statements are updated at the same time.

### Phase 1 — Scaffold (no moves yet)

- Create `Slices/` and `_Shared/` directories
- Write one complete worked example: `Slices/Auth/AuthSliceExtensions.cs`
- Update `AGENTS.md` with new structure conventions

### Phase 2 — Infrastructure + Cross-cutting (no Razor pages, low risk)

- `CosmosDbService`/`ICosmosDbService` → `_Shared/Infrastructure/`
- `IFormFactor`, `ISecureStorageService` → `_Shared/Platform/`
- `Services/IngredientParsing/` + `ParsedIngredientsTable` → `_Shared/IngredientParsing/`
- `SeasonHelper`, `ISeasonalityService`, `LocalJsonSeasonalityService`, `SeasonalityBadge`, `SeasonalityPanel` → `Slices/Seasonality/`
- ✅ Build + test after

### Phase 3 — Auth + AppSettings slices

- Move `Login.razor`, `AuthorizeView.razor`, auth service files → `Slices/Auth/`
- Move `AppSettingsDialog`, `IThemeService`, `ThemeService` → `Slices/AppSettings/`
- Create `AuthSliceExtensions.cs`, `AppSettingsSliceExtensions.cs`
- Replace inline DI in both host `Program.cs`/`MauiProgram.cs` with `services.AddAuthSlice()` etc.
- ✅ Build + run unit tests

### Phase 4 — Pantry + GroceryList slices

- Move `Pantry.razor` group + services → `Slices/Pantry/`
- Move `GroceryList.razor` group + `AddIngredientsDialog` + services → `Slices/GroceryList/`
- ✅ Build + test

### Phase 5 — Foods slice

- Move `Foods.razor` group, `UsdaSearchDialog`, USDA services → `Slices/Foods/`
- `IFoodService` stays in `_Shared/IngredientParsing/` (used by parser — not Foods-exclusive)
- Implement conditional USDA registration in `FoodsSliceExtensions.cs`
- ✅ Build + test

### Phase 6 — Recipes slice

- Move `Recipes.razor`, `RecipeDetail.razor`, `RecipeReadOnly.razor`, `MarkdownRenderer` → `Slices/Recipes/`
- Move import sub-feature → `Slices/Recipes/Import/`
- Move all recipe services and image services → `Slices/Recipes/`
- ✅ Build + test

### Phase 7 — MealPrep + Nutrition slices

- Move `MealPrepPlans.razor`, `AddRecipesToPlanDialog`, Cosmos service pair → `Slices/MealPrep/`
- Move `DailyFoodPlanning.razor`, `MacroTargets.razor`, `MacroTargetSettingsDialog`, all macro/daily services → `Slices/Nutrition/`
- ✅ Build + test

### Phase 8 — Namespace normalisation sweep

- Rename `Broccoli.Shared.Services` → `Broccoli.App.Shared.Slices.Xxx` for all moved Cosmos services
- Update `_Imports.razor` to reflect final namespaces
- Fix all test project `using` references
- ✅ Full `dotnet test` run

---

## Section 6 — Test Reorganisation

Mirror the slice structure inside each test project:

`Broccoli.App.UnitTests/     Slices/        IngredientParsing/            IngredientParserServiceTests.cs        Seasonality/            SeasonalityServiceTests.cs        Recipes/            RecipeImportServiceTests.cs        GroceryList/            IngredientCartServiceTests.cs Broccoli.App.IntegrationTests/     Slices/        IngredientParsing/            IngredientParserServiceTests.cs`

Test namespaces follow `Broccoli.App.Tests.Slices.<SliceName>`. No test behaviour changes — only locations and namespace declarations.

---

## Section 7 — Risks and Trade-offs

|Risk|Mitigation|
|---|---|
|**Namespace irregularity amplifies scope.** Three root namespaces mean every file move also requires a namespace rename and `using` updates across many files.|Phase 8 deliberately separates structural moves from namespace normalisation. Run `dotnet build` after each phase before committing.|
|**`IFoodService` is not slice-exclusive.** It is implemented by `LocalJsonFoodService` (cross-cutting) but also logically relates to the Foods page.|Place the interface in `_Shared/IngredientParsing/` — the contract matters where parsing happens, not where food data is edited.|
|**Blazor routing is assembly-based, not folder-based.** Moving pages between folders doesn't break `@page "/recipes"` routes.|`NotFound.razor` is referenced by `Routes.razor` via type — update the reference when it moves.|
|**Scoped CSS isolation is not path-dependent.** CSS isolation keys off the component class name.|Moving `.razor.css` files is safe — no changes needed.|
|**`_Imports.razor` must be updated per-phase.** New slice namespaces won't resolve in Razor markup until added to imports.|Add the `@using` for each slice namespace at the same time as the move — not in a final batch.|
|**`AddRecipesToPlanDialog` has no `.cs` file.** All logic is inline in markup.|If it gains code-behind during migration it belongs in `Slices/MealPrep/`. No action needed now.|
|**MAUI hardcodes `FoodDatabaseEditing = false`.**|`FoodsSliceExtensions.cs(services, FeatureFlagsSettings flags)` — MAUI passes `flags` before calling `AddFoodsSlice()`. No USDA service is registered; same behaviour as today.|