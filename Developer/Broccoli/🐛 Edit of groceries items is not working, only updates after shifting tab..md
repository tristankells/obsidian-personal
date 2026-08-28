# In Progress
- BUG: Checkmark is not working on groceries list.
	- In addition, when checked, we should cross out the text, and move the item below any unchecked items. If we uncheck a check item, we should put it above any checked item, bottom of unchecked item. Also un cross it.
- Edit and New share some code.
- 
# Complete
- BUG: When food doesn't have a possible way of measuring quantity, `Cheese` then we are still getting grams in hint.
	- Must be matching on something, but we are getting no hint...
	- How to control what is worth matching and what is not?
		- Only when serving equals each?
		- Or when `"Measure"` contains name of food
		- New type of search, where we only match on 
		- I would like a hint on the what the matched food was on the grocery item row, if there was a quantity hint. Include the fuzzy percentage etc.. to not clog the UI, put this information on mouse over on the row.



