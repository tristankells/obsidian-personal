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