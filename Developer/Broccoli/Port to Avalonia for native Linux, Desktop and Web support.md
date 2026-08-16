This can be considered done when we can perform the end to end workflow:
- Add nutrition info for new person ->✅ 
- Select that person as the nutrition goal -> ✅ 
- Add new recipe ->  ✅
- Adjust macros for that recipes ->✅
- On the recipes list page, add ingredient from that page to list add ingredients for that recipes + one more existing recipe -> ✅
- Copy paste into Microsoft To-Do -> ✅
- Sync to google -> ✅
- Download to phone and view recipe in cooking mode there! ✅





- Grocery List
	- [ ] Add ingredients to cart
		- [ ] Button to clear all of pantry, with warning.
		- [ ] Don't change app code the code, but I want you to write a failing unit test for a bug I'm seeing on the grocery list;  Grocery list is showing stuff like (~ 1 100g). If we cannot convert to the measure, we should just not put the hint there.
- [ ] Create the list view, as table.
- [ ] Add a button to switch views.
- [ ] Add a card view..
- [ ] Do performance testing with 100, 1000 and 10000 recipes! 

---
![[Pasted image 20260724162240.png]]
## Port The Recipe List
- Add a new Avalonia project to Broccoli.
- As part of the port, obsidianify the pages.
- Do page by page.
- Recipes
	- Recipe List
	- Recipe Page
	- Recipe Read-only Page
	- Backed by a Markdown per recipe.
	- Or by SQLite




# Features
## Recipes
- Add New Recipe
- Delete Recipe
- Edit Recipe
- Filter recipes list
	- By tag, ingredient and title?

---
# Design
- High performance alternative, build index of words to recipes list of recipes.
- https://docs.avaloniaui.net/docs/how-to/mvvm-how-to#filtered-collection
- Renamed our recipes collection to FilteredRecipes.
- Store all recipes in private field \_allRecipes
- When loading recipes, store in a field.
- After editing recipe, recalculate search words.
- Tokenise search space.
- Store search words to lower invariant.
- Add a new non persisted computed property on the recipe model: SearchWords
	- A computed collection of all unique strings within the title, tags and ingredients.
	- This should be alphabetically ordered for faster searching (binary search?)
	- Example, 
		- When filter changes trigger update to FilteredItems; someone types "c"
		- We check every recipes for word in a tag, ingredient or title that begins with "c";(recipe.SearchWords.Any(searchWord.word.StartsWith(searchText)))
		- Needs to be a bit smarter to contain handle multiple words.
		- We filter recipes by this word.