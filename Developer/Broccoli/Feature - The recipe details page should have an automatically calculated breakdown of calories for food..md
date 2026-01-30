Parsing issues:
- 6 x potato, diced 2cm 
	- Potatoes 6.0 g (x is not parsing correctly).
- Baby Spinach
- Mediterranean spices
- sliced almonds
-  Herb aioli

---
- [ ] Need to not show the best match if below threshold.
- Need option to add new food via dialog in details.
- Use a Direct FoodName to IngridentName ignore casing.
	- ... if that fails, do a FoodNameStemmed to IngridentStem comparison.
- Stemming is not working correctly at all, example:
	```
	250g vermicelli noodl, 1 drizzl  oil, 1 drizzl  oil, 600g carrot, 1400g  free rang chicken breast, 150g singapor laksa past, 1 1/2  malaysian curri powder, 400g lite coconut milk, 1/2 cup water, 1 twin  babi bok choy  3cm, 1 tsp fish sauc, 200g mung bean sprout, 1 pinch  chilli flake
	```
	- Fix stemming
- Duplicates should be combined!
- This is not an easy problem!
- Need to simplify names of foods in database?
	- ~~Remove branded stuff, but keep lowercase and `,`, remove those before comparison so we have the correct data for display. Or create a property on the food object for comparison without those removed...
- Need a strong integration suite where I test a decent number of recipes to make sure ongoing changes don't mean those stop working.
- Need easily accessible debug /  trace logs to troubleshoot problems.
	- Need to know the result of transformation and need to know the index values of that for all of the food items.
- `foodDescription == "1 pinch of chilli flakes, optional"`
- "Salt and pepper to taste" should not be matched.
# DOD
- Integration test suite with 10 recipes parsing correctly.
	- 10 Recipes imported into production application working correctly.
- UI for feature responsive to changes of ingredients textbox.
- Accessible trace logs for web and windows maui implementations to support easy troubleshooting of future issues.
