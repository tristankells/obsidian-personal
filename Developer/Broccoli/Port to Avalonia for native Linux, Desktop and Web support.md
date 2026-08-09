- [x] Go through the getting started tutorial for Avalonia.
- [x] Fix the black screen when trying to debug.
- [x] Get a list of item printing to screen, hard coded.
- [x] Vibe to get to a list of recipes and a simple edit screen.
- [x] Move to Feature slices to manage complexity.
- [x] Import 5 most important recipes, manually.
- [x] Implements search function.
	- [x] Confirm tests are there.
	- [x] Add test case for multiple words in the ingredients.
	- [x] Add UI to change _searchWordSource.
	- [ ] Add helpful tags to recipes recipe,
	- [ ] 

- Couple fixes
	- Clicking the anywhere on the card should take you to the not just the name of the recipes / text.
	- I would like another optional element added to the recipes cards, controlled by settings; calories match current user macros. This should be a right aligned overlay, like the seasonality score. I should be able to control in the setting what is considered acceptable of target, the percentage under or over that is considered acceptable. If within range, the overlay should be tick 
	- 

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


- Where the setting for 





Here are the common foods missing from your database, organized by category:

**Proteins:**

- Chicken Thigh (skinless), Chicken Thigh (with skin), Chicken Wings
- Pork Mince, Pork Chops, Pork Loin, Pork Belly
- Beef Steak (sirloin/scotch/rump), Beef Roast, Beef Mince (regular), Chuck Steak
- Lamb Chops, Lamb Shoulder/Roast
- Turkey Breast, Turkey Mince
- Bacon (streaky, middle, shortcut)
- Salmon (fresh, Atlantic), Tuna (canned in water/springwater/oil), White Fish (Cod, Hoki, Snapper), Prawns/Shrimp
- Tofu (firm, silken), Tempeh
- Sausages (beef, pork)

**Dairy & Eggs:**

- Cheddar Cheese, Mozzarella, Parmesan
- Cream (fresh/pouring), Cream (whipped)
- Cream Cheese, Cottage Cheese, Ricotta
- Plain Yoghurt (full-fat, low-fat)
- Whole Egg (already there — just "Egg") — check it's per-egg measure

**Grains, Pasta & Bread:**

- Pasta (Spaghetti, Penne, Fusilli), White Rice (short/medium grain)
- Rolled Oats, Quick Oats
- Quinoa, Pearl Barley
- White Bread, Wholemeal/Wholegrain Bread, Wraps/Tortillas (flour, corn)
- Noodles (Rice Vermicelli, Udon, Soba)

**Vegetables:**

- Tomatoes (fresh), Cherry Tomatoes
- Avocado, Sweet Potato/Kumara, Pumpkin/Butternut
- Cauliflower, Cabbage (Green, Red), Brussels Sprouts
- Celery, Lettuce (Iceberg, Cos/Romaine, Rocket/Arugula)
- Spinach (regular), Kale, Silverbeet
- Snow Peas, Green Peas (fresh), Asparagus
- Eggplant/Aubergine, Radish
- Capsicum (already there — verify it's per-medium)

**Fruits:**

- Apple, Banana, Orange, Pear
- Grapes (red, green), Strawberries, Blueberries, Raspberries
- Mango, Pineapple, Watermelon, Rockmelon/Cantaloupe
- Kiwifruit (green, gold), Cherries, Peaches, Nectarines

**Legumes:**

- Chickpeas (canned, dried), Black Beans (canned), Kidney Beans (canned)
- Lentils (Red, Brown/Green, dried)
- Edamame, Baked Beans

**Oils & Fats:**

- Coconut Oil, Avocado Oil, Peanut Oil
- Butter (already there — confirm it's per-tablespoon)

**Nuts & Seeds:**

- Almonds (raw, roasted), Walnuts, Pecans
- Sunflower Seeds, Pumpkin Seeds/Pepitas
- Chia Seeds, Flaxseed/Linseed
- Macadamia Nuts, Brazil Nuts, Pistachios

**Condiments & Sauces:**

- Ketchup/Tomato Sauce, BBQ Sauce, Worcestershire Sauce
- Sriracha, Oyster Sauce, Pesto (basil)
- Vinegar (White, Apple Cider, Balsamic)
- Curry Paste (Green, Yellow, Massaman)

**Herbs & Spices:**

- Black Pepper (ground), Cinnamon (ground), Nutmeg
- Basil (dried), Thyme, Rosemary, Italian Herb Mix
- Paprika, Turmeric, Chilli Powder, Cayenne Pepper

**Baking & Sweeteners:**

- White Sugar (granulated, caster), Icing Sugar, Cocoa Powder
- Maple Syrup, Vanilla Extract
- Dark Chocolate, Milk Chocolate
- Baking Powder, Baking Soda, Cornstarch (already there as Cornflour)

**Canned & Jarred:**

- Chopped Tomatoes (canned), Whole Peeled Tomatoes, Tomato Paste
- Coconut Cream, Evaporated Milk

**Frozen:**

- Frozen Mixed Vegetables, Frozen Berries (mixed)
- Frozen Corn, Frozen Spinach

The biggest gaps are in **fresh proteins** (pork, bacon, salmon, tuna, prawns), **dairy** (cheddar, mozzarella, cream, cottage cheese), **pasta/grains** (spaghetti, oats, quinoa), **vegetables** (tomatoes, avocado, sweet potato, cabbage, lettuce varieties), and **canned legumes** (chickpeas, black beans, lentils).

