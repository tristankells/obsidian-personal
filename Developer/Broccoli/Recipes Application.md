# Vision
Cronometer + Paprika

# Features
Have a textbox to type, copy paste the recipes.
Have the calories calculated + macros calculated live.
Maintain a shopping list, which you can add too.
Maintain a Pantry list (not automatically added to).
# Notes
- Recreate the UI for both.
- Use json blob / NOSQL makes more sense for the recipes
# Models
Food
- Name (Unique)
- Calories (per g)
- Protein (per g)
- Fat
- Sodium
- Carbohydrates

Recipes
- ID
- Names
- Instructions
- Ingredients
	- Food
	- Quantity
- Tags
- 