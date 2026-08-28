# Todo
- Search recipe filtering is lagging for multiple inputs.
	- Leads me to believe the UI thread is getting 
		- `RecipeListPageViewModel.ApplyFilter()`
	- Can you make this method async?
# Done
- Please plan a fix for this:
- When I filter to a low number of recipes, they are align center instead of from the left.
	- For example, the window size means I get 5 recipes per row. If I go down to 2 reipces, instead of the row being filled two from the left, they look center aligned. 
- C:\Dev\Github\Broccoli.App\Broccoli.Avalonia\Broccoli.Avalonia\Slices\Recipes\RecipeDetailView.axaml 
	- When deleting a recipe say from the edit recipe view, I would like a seperate windows popup to confirm I would like to delete, instead of the in line popup we have now.