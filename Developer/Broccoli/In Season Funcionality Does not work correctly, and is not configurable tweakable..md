# Todo



- Add import and export of seasonal data to the seasonal page. Should be based json file format. Add any questions you have about implementation.



# Done
-  Fix the display of the seasonal data, in the season page. The name of the food is taking up too much relative space which is causing the other rows to be too condensed. Make them wider and make the options in the dropdown shorter so they are not cut off.
- Surface weighting data in the seasonal overview.
- In the seasonal overview on edit and view pages, please include information about the matching, and the impact on
- Replace the "Score for" filter with a simple "Month" dropdown. Move that to a "Seasonality" dropdown beside the "Search Recices". This dropdown allows us to set different month and has a nested dropdown allowing us filter by All, Green, Yellow, Red.
- Remove the "? of ? Ingredient matched" from the card, that is not helpful information.
- Add seasonality information to the edit recipe as well. Make it optional in the settings. Add hints to the original string it matched on form the ingredients and add a hint for the impact that ingredient had overall seasonality. Add mouse over per seasonal ingredient that provides more information about that specific ingredient.
- Need to review how this works.
	- Maybe we mark in three colors Green, Yellow and Red
	- The top third are always in Green, Mid 


One idea; Marks recipes as Green, Yellow or Red for the difference degrees of in season. The top third seasonality scores should be green, with upper and lower thresholds so seasonality scores above a threshold are always green, and below a threshold are not green, no matter the percentage. Bottom third should be red, with another upper and lower thresholds for the same reasons. Anything between these thirds / thresholds should be yellow.


---
I would like a new tab. This should be protected behind a feature flag following latest Avalonia, then Microsoft standards. Use libraries from those if available. 

This tab should surface seasonality data, and allow us to edit and persist edits to this data. It should allow us to add new foods to the data. It should visual indicate which food are currently in season based on the current month.



Plan a change to seasonal data, impacting this UI and seasonality information all over: 
- Instead of seasons, each fruit / vegetable should should store information about when each item is in season, partially in season and out of season. This should be represented by a enum value for every month, along with the item name.
  This should be represented in the UI, where each column is a coloured dropdown for each month, where we can set whether fruit/vege is in season or note.