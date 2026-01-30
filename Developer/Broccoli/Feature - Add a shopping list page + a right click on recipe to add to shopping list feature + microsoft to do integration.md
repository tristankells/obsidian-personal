# Todo
### Testing

### Findings
Grocery List
- Items names need to be editable once added.
Pantry Items
- When "Add Ingredients from Recipe", need to improve the format of the warning.
	- Duplicate ingredients should be combine in shopping list.
	- FUTUE FEATURE (Automatically sort shopping list by aisle?)
	- Water should be a hardcoded exit for shopping list, we never need that.
	- Need to improve the parity between matching food stuff, as olive oil matches drizzle of oil in the recipes but no here.
![[Pasted image 20260321100810.png]]
- Names need to be editable here as well.
- Remove icon is only visible on mouseover
	- Is this just best practice? Does it look clean.
UI
- Need to remove Nutition Optional, as we are automatically parsing that now
![[Pasted image 20260321100440.png]]
- Add a UI hint to use grams or oz where you can, for optimal accuracies.
- When we use a "Packet", we should fail to figure out the weight of our food, and add a Yellow Warning an no information.
- The unsure food match result could look better:
 ![[Pasted image 20260321095937.png]]
- On mobile, collapsible nav bar hides logout button: 
  ![[Pasted image 20260321094408.png]]
- Resolve This:
![[Pasted image 20260321102611.png]]


# Grocery List & Pantry Feature Specification
## Project Overview
This document specifies a complete grocery list and pantry management system for the Broccoli.App recipes application. The app is a Blazor Server application using CosmosDB for data persistence.

---
## 1. Feature Summary
**Grocery List**: An editable todo-style shopping list where users can add items, check them off when purchased, and remove items. Includes a "Reset" button to clear the entire list.
**Pantry**: A personal inventory of food items the user already has at home. Each item is categorized as either "Always Have" (staples like salt, flour, water) or "Check If Have" (optional items like ketchup, mustard, apples).
**Recipe Integration**: Users can add all ingredients from any recipe to their grocery list. Before adding, a dialog shows each ingredient with checkboxes - items already in the pantry (especially "Always Have" items) are pre-unchecked.

---
## 2. Tech Stack
- **Framework**: Blazor Server (.NET 9)
- **Database**: Azure Cosmos DB (using existing `CosmosClient` pattern)
- **UI**: Razor Components with Bootstrap styling (matching existing app)
- **Authentication**: Existing user-based system ( CosmosDB with `userId` partition key)
---
## 3. Data Models
### 3.1 PantryItem
```csharp
public class PantryItem
{
    [JsonProperty("id")]
    public string Id { get; set; } = Guid.NewGuid().ToString();
    [JsonProperty("name")]
    public string Name { get; set; } = string.Empty;
    [JsonProperty("category")]
    public PantryCategory Category { get; set; } = PantryCategory.CheckIfHave;
    [JsonProperty("userId")]
    public string UserId { get; set; } = string.Empty;
    [JsonProperty("partitionKey")]
    public string PartitionKey { get; set; } = "user";
    [JsonProperty("createdAt")]
    public DateTime CreatedAt { get; set; } = DateTime.UtcNow;
}
public enum PantryCategory
{
    AlwaysHave = 0,      // Staples: salt, flour, water, sugar, oil, etc.
    CheckIfHave = 1      // Optional: ketchup, mustard, specific fruits, etc.
}
```
**Rationale**: The enum distinguishes between staples the user always has vs. items they may or may not have. When adding recipe ingredients, "AlwaysHave" items are auto-unchecked in the dialog. "CheckIfHave" items are also unchecked, but include a visual reminder that they should be checked before being added.
### 3.2 GroceryListItem
```csharp
public class GroceryListItem
{
    [JsonProperty("id")]
    public string Id { get; set; } = Guid.NewGuid().ToString();
    [JsonProperty("name")]
    public string Name { get; set; } = string.Empty;
    [JsonProperty("isChecked")]
    public bool IsChecked { get; set; } = false;
    [JsonProperty("userId")]
    public string UserId { get; set; } = string.Empty;
    [JsonProperty("partitionKey")]
    public string PartitionKey { get; set; } = "user";
    [JsonProperty("createdAt")]
    public DateTime CreatedAt { get; set; } = DateTime.UtcNow;
}
```
---
## 4. CosmosDB Schema
### 4.1 Container: PantryItems
| Property | Value |
|----------|-------|
| Container ID | `PantryItems` |
| Partition Key Path | `/partitionKey` |
| Partition Key Value | `"user"` (all items use same value) |
### 4.2 Container: GroceryListItems
| Property | Value |
|----------|-------|
| Container ID | `GroceryListItems` |
| Partition Key Path | `/partitionKey` |
| Partition Key Value | `"user"` |

---
## 5. Service Interfaces & Implementations
### 5.1 PantryService
**Interface** (`IPantryService.cs`):
```csharp
public interface IPantryService
{
    Task InitializeAsync();
    Task<List<PantryItem>> GetAllAsync(string userId);
    Task<PantryItem> AddAsync(PantryItem item);
    Task<PantryItem> UpdateAsync(PantryItem item);
    Task DeleteAsync(string id, string userId);
    Task<bool> ExistsAsync(string userId, string itemName);
}
```
**Implementation**: Uses CosmosDB container with queries by `userId`. Item name matching should be case-insensitive for existence checks.
### 5.2 GroceryListService
**Interface** (`IGroceryListService.cs`):
```csharp
public interface IGroceryListService
{
    Task InitializeAsync();
    Task<List<GroceryListItem>> GetAllAsync(string userId);
    Task<GroceryListItem> AddAsync(GroceryListItem item);
    Task<GroceryListItem> UpdateAsync(GroceryListItem item);
    Task DeleteAsync(string id, string userId);
    Task ResetAsync(string userId);  // Delete all items for user
    Task AddMultipleAsync(List<GroceryListItem> items);
}
```
---
## 6. UI Pages
### 6.1 Grocery List Page (`/grocery-list`)
**Layout**:
```
┌─────────────────────────────────────────┐
│ Grocery List                    [Reset] │
├─────────────────────────────────────────┤
│ [________________________] [Add]        │
├─────────────────────────────────────────┤
│ ☐ Milk                                  │
│ ☑ Eggs (checked = purchased)           │
│ ☐ Bread                                 │
│   ...                                   │
└─────────────────────────────────────────┘
```
**Features**:
1. **Add Item**: Text input with "Add" button. On submit, create new `GroceryListItem` with `IsChecked = false`.
2. **Check Item**: Click checkbox to toggle `IsChecked`. Checked items show strikethrough text.
3. **Delete Item**: Small trash icon next to each item. Removes from database.
4. **Reset Button**: Prompts for confirmation, then deletes ALL grocery list items for the current user.
**Behavior**:
- Items sorted by `CreatedAt` descending (newest first)
- Checked items remain in list (not deleted) - user can uncheck if needed
- Empty state: "Your grocery list is empty. Add items or add ingredients from a recipe."
### 6.2 Pantry Page (`/pantry`)
**Layout**:
```
┌─────────────────────────────────────────────────┐
│ My Pantry                                       │
├─────────────────────────────────────────────────┤
│ [________________________] [Add]               │
├─────────────────────────────────────────────────┤
│ Always Have (Staples):                          │
│   ✓ Salt           [dropdown: AlwaysHave ▼] [🗑] │
│   ✓ Flour          [dropdown: AlwaysHave ▼] [🗑] │
│                                                 │
│ Check If Have:                                  │
│   ✓ Ketchup        [dropdown: CheckIfHave ▼] [🗑]│
│   ✓ Mustard        [dropdown: CheckIfHave ▼] [🗑]│
└─────────────────────────────────────────────────┘
```
**Features**:
1. **Add Item**: Text input with "Add" button. Default category: `CheckIfHave`.
2. **Category Dropdown**: Each item has a `<select>` dropdown to change category between "Always Have" and "Check If Have". On change, update database.
3. **Delete Item**: Trash icon removes item.
4. **Grouping**: Display items grouped by category (AlwaysHave first, then CheckIfHave).
**Styling**:
- "Always Have" items: Display with distinct styling (e.g., green badge, bold text)
- "Check If Have" items: Standard styling
### 6.3 Add Ingredients Dialog (Component)
**Trigger**: "Add to Grocery List" button on each recipe card in the Recipes page.
**Dialog Layout**:
```
┌─────────────────────────────────────────────────┐
│ Add Ingredients from [Recipe Name]              │
├─────────────────────────────────────────────────┤
│ The following ingredients will be added:      │
│                                                 │
│ ☐ 2 cups Flour        (in pantry: Always Have)  │
│ ☑ 1 tsp Salt         (in pantry: Always Have)  │
│ ☐ 3 Eggs             (in pantry: Check If Have) │
│ ☑ 1 cup Milk         (not in pantry)            │
│                                                 │
│ [Cancel]                      [Add Selected (2)]│
└─────────────────────────────────────────────────┘
```
**Behavior**:
1. Parse ingredients from the recipe (use existing `IngredientParserService` if available, or split by newline)
2. Fetch user's pantry items
3. For each ingredient:
   - If pantry contains matching item with `Category.AlwaysHave`: checkbox = unchecked
   - If pantry contains matching item with `Category.CheckIfHave`: checkbox = checked (user might still need)
   - If not in pantry: checkbox = checked
4. Show "(in pantry: Always Have)" or "(in pantry: Check If Have)" or "(not in pantry)" next to each item
5. On "Add Selected": Create `GroceryListItem` for each checked ingredient
6. On "Cancel": Close dialog, no changes
**Matching Logic**:
- Case-insensitive partial match (e.g., "salt" matches "Sea Salt", "2 cups Flour" matches "Flour")
- Match on ingredient name/quantity text
---
## 7. Recipe Page Integration
### 7.1 Update Recipes.razor
Add a third button on each recipe card:
```
[Edit] [Delete] [🛒 Add to List]
```
**On Click**:
1. Parse ingredients from `recipe.Ingredients` (newline-separated string)
2. Open Add Ingredients Dialog
3. On dialog confirm, redirect to Grocery List page (optional)
---
## 8. Navigation
### 8.1 Update NavMenu.razor
Add new nav items under existing links:
```html
<div class="nav-item px-3">
    <NavLink class="nav-link" href="grocery-list">
        🛒 Grocery List
    </NavLink>
</div>
<div class="nav-item px-3">
    <NavLink class="nav-link" href="pantry">
        🗄️ Pantry
    </NavLink>
</div>
```
---
## 9. Service Registration (Program.cs)
In `Broccoli.App.Web/Program.cs`, add:
```csharp
// Add new services
builder.Services.AddSingleton<IPantryService, PantryService>();
builder.Services.AddSingleton<IGroceryListService, GroceryListService>();
```
Initialize new containers after CosmosDB init:
```csharp
var pantryService = app.Services.GetRequiredService<IPantryService>();
await pantryService.InitializeAsync();
var groceryListService = app.Services.GetRequiredService<IGroceryListService>();
await groceryListService.InitializeAsync();
```
---
## 10. File Structure
Create the following files:
```
Broccoli.App.Shared/
├── Models/
│   ├── PantryItem.cs           (new)
│   └── GroceryListItem.cs      (new)
├── Services/
│   ├── IPantryService.cs      (new)
│   ├── PantryService.cs        (new)
│   ├── IGroceryListService.cs (new)
│   └── GroceryListService.cs  (new)
├── Pages/
│   ├── GroceryList.razor       (new)
│   ├── GroceryList.razor.cs   (new)
│   ├── Pantry.razor           (new)
│   └── Pantry.razor.cs        (new)
└── Components/
    ├── AddIngredientsDialog.razor   (new)
    └── AddIngredientsDialog.razor.cs (new)
```
**Update existing files**:
- `Broccoli.App.Shared/Layout/NavMenu.razor` - Add nav links
- `Broccoli.App.Shared/Pages/Recipes.razor` - Add "Add to Grocery List" button
- `Broccoli.App.Web/Program.cs` - Register services, init containers
- `Broccoli.App.Shared/Services/CosmosDbService.cs` - Add new containers
---
## 11. Implementation Notes
### Authentication Context
- All services require `userId` from `IAuthenticationStateService`
- Inject `IAuthenticationStateService` into pages to get `CurrentUserId`
- Pass `userId` to all service method calls
### Existing Code Patterns to Follow
- Use same service registration pattern as `CosmosRecipeService`
- Use same model structure as `User.cs` (with `partitionKey`)
- Use same UI patterns as `Recipes.razor` (loading states, empty states)
- Use same dialog pattern (Bootstrap modal)
- Follow existing styling (Bootstrap classes)
### Error Handling
- Wrap service calls in try-catch
- Show user-friendly error messages
- Log errors to console/logger
---
## 12. Acceptance Criteria
1. ✅ User can add items to grocery list via text input
2. ✅ User can check/uncheck items in grocery list
3. ✅ User can delete individual items from grocery list
4. ✅ User can reset entire grocery list with confirmation
5. ✅ User can add items to pantry with category selection
6. ✅ User can change category of pantry items via dropdown
7. ✅ User can delete items from pantry
8. ✅ User can click "Add to Grocery List" on any recipe
9. ✅ Dialog shows all recipe ingredients with checkboxes
10. ✅ Dialog auto-unchecks ingredients that are "Always Have" in pantry
11. ✅ Dialog shows pantry status next to each ingredient
12. ✅ Only checked ingredients are added to grocery list
13. ✅ New nav links appear for Grocery List and Pantry pages
14. ✅ All data persists to CosmosDB
15. ✅ Works for authenticated users only