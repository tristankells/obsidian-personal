- [x] Go through the getting started tutorial for Avalonia.
- [x] Fix the black screen when trying to debug.
- [x] Get a list of item printing to screen, hard coded.
- [x] Vibe to get to a list of recipes and a simple edit screen.
- [x] Move to Feature slices to manage complexity.
- [ ] Import 5 most important recipes, manually.
- [ ] Implements search function.
- [ ] Pick a missing feature to start working.
- [ ] Create the list view, as table.
- [ ] Add a button to switch views.
- [ ] Add a card view.
- [ ] Debug through the codebase to understand what is happening, and what can be simplified.
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







The tabs need a clearer signify which tab is selected. Make sure you are using native avalonia controls where you can.

