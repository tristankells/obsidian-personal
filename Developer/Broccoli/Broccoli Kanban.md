---

kanban-plugin: board

---

## Technical Debt

- [ ] Broccoli.App.Web/Program.cs has messy and unclear setup invokes. Random file path checking to find database is not good too.


## Bugs



## Backlog

**Complete**
- [x] Get rid of all the warnings in IDE
- [x] Track prices of stuff at supermarkets!
- [x] Suggest tags based on the ingredients and existing tags?
- [x] [[Add seasonality data]]
- [x] [[Resolve Client Secrets in git history]]


## Ready

- [ ] Can we combine meal prep and daily food planning pages?
- [ ] A searching dialog that lets us do a fuzzy search for recipes that match a list of food we want to get rid of / use up?
- [ ] Expand food database
- [ ] [[Reserach - Build a list of missing features by looking at your competing app (aka how does my wife need )]]
- [ ] Add grid view and picture view
- [ ] Add - Animations
- [ ] Combine Grocery List and Pantry
- [ ] [[Flesh out food database]]
- [ ] Make an setting that converts all grocery items to grams or pounds at the time they are added to the list, where possible. So if example I add one onion, then I want to convert to grams before adding it to the list, then have the amount of onions visible as hint. This normalizes the items on the list and makes them consistent to shop for despite the recipe.
- [ ] Fix the Mobile View!
- [ ] Create a suite of UI tests to protect against regression!
- [ ] After using app for a bit, getting over 300mbs... double check if this can be smaller. Write a vanilla Avalonia app and see what the size is.
- [ ] Add search / filter to food database.
- [ ] Right click edit option on the recipes lists.
- [ ] 🐛 Edit of groceries items is not working, only updates after shifting tab.
- [ ] Check in the auto-sync, how often is it? Should be UI indicator somewhere?
- [ ] [[After sync we get a ugly popup, need to review why we are getting conflict popups.]]
- [ ] Add last edit information to footer when recipe is open, number of items in history etc...
	- Make footer appearance configurable.


## In Progress

- [ ] 🐛 Need to the the development features of USDA imports for missing food from recipe details
	
	- Button
	- Button > loading icon > list of items possible items on the right > macros on the side left
- [ ] [[In Season Funcionality Does not work correctly, and is not configurable tweakable.]]
- [ ] [[Auto balance - Add functionality to auto balance the macros calories of a recipes against a given users goals (using the lead source of protein carbohydrates)]]


## In Testing



## Completed

- [ ] [[Feature - Maintain a history of recipes ingredients as they might be changing quickly as we change diet and we might want to know what the original recipes was.]]
- [ ] I want to include information about the amount of storage the applications is taking up, as google storage is the main storage system. I want to differentiate between markdown recipes, backups, images and data stored in the database.
- [ ] Markdown backed recipes?
- [ ] Backup to google drive
- [ ] Get it working 100% locally removing backend
- [ ] "Obsidianfy" the UI
- [ ] [[Port to Avalonia for native Linux, Desktop and Web support]]
- [ ] [[Feature - Have a new page that stores multiple peoples information and calculates the daily calories and macros for them.]]
- [ ] [[Vertical Slice Architecture]]
- [ ] Address IDE warnings, configure Central Package management, strong roslyn based editor config settings.
- [ ] [[Feature - Support markdown when it comes to instructions.]]
- [ ] [[Feature - Make it do you can pick existing tag or they are autocompleted once typing.]]
- [ ] [[Feature - Add App Settings dialog. Add dark mode support.]]
- [ ] [[Feature - Add support for favouriting recipes]]
- [ ] [[Feature - An development mode feature to food database to add item to database and import from cronometer.]]
- [ ] [[Feature - Add ability to add jpeg]]
- [ ] [[Feature - Add a page for daily food planning.]]
- [ ] [[Feature - Add a Meal Prep Planning page to your application.]]
- [ ] [[Feature - Keep track of what fruit and vegetables are in season]]
- [ ] [[Feature - Support importing recipes from paprika.]]
- [ ] [[Feature - Add a shopping list page + a right click on recipe to add to shopping list feature + microsoft to do integration]]
- [ ] [[Feature - The recipe details page should have an automatically calculated breakdown of calories for food.]]
- [ ] Remove the boilerplate navigation items and page. Make the recipes list the default page.


## Abandoned



***

## Archive

- [x] Edit and view the seasonality data you have: \

%% kanban:settings
```
{"kanban-plugin":"board","list-collapse":[false,false,false,false,false,false,false,false]}
```
%%