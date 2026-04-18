# Todo
- Group nagivation items in sub headers; Recipes and Planning/Health.
- Feature
	- The type of tuning we want to do for calories normally excludes seasoning / vegetables, most fat sources, empty carbohydrates and protein sources.
	- So, we might be able to make an automatic balancer of some kind...
	- Easy way would be to identify the main sources of any of the macros.
# Azure Resources
- 
# MVP
Recipe Page
Text boxdasd 
Process
- Enter new line separate list of ingredients.
- Parse block of text into list of items: RawIngridents { string Serving, string Name} - Using regex, this can nearly be a oneline in the parse ingredients
- Pass list of RawIngridents into 
1. Lets get a list of food parsed first.
2. TDD on a "FoodService"
3. ~~Design a model for recipes based on paprika. 
4. Lets try a free NoSql database, how about cosmos DB?
5. The application itself ships with a Json file (for), that contains all of the food macros.
6. Use an azure function as the backend?
7. Store food database centrally, but have each application maintain its own cached sqlite database of the food items. So we don't need to ship as much and can centrally update, but also get quick matching times.
# Models
```

Recipe (Thinking of saving to a nosql database. Production would use CosmosDb and loca would use DuckDb?) {
	ID (Unique identifier of recipe)
	Name (Name of recipe)
	Ingridents (Long text block of new line seperate recipe ingridents)
	Directions (Long unformed text block of recipe directions)
	Notes (Any additional notes from the chef, might include cooking tips or alternative ingridents etc...)
	Servings (Intended servings)
	Prep Time (Time to prep)
	Cook Time (Time to cook)
	Source (Where the recipe is from)
	Url (Optional, if the recipe was got from online)
	Tags (An list of tags describing the recipes; eg Beef, Chicken, Freezable)
	Images (List of images asociated with the recipe)
	UserId (Id of user who owns the recipes)
}

Food {
	ID ()
	Name (Name Of Food)
	Measure (How we meaure, this could be Tablespoon, Cup, Tsp, a Piece (like a single fruit or vegetable))
	Grams (How much does a single measure weigh in grams?)
	Notes (Generic notes)
	Calories (How many calories per 100g?)
	Fat (How much fat in 100g)
	Carbohydrates (How much carbohydrates in 100g?)
	Protein (How much Protein in 100g?)
}

RecipeFood (Mapping object, not saved to database) {
	Food {}
	Grams {} 
}

User (This is a small app to share with friends, I just want to support a user name and password for login and accessing there data. This would be stored in CosmosDb and development would use DuckDb){
	ID
	UserName
	Password
}

}
```

![[Drawing 2026-01-24 16.43.16.excalidraw]]

---
# Cosmos DB
## Development
- Start Azure Cosmos DB Emulator
	- Press `Start` on keyboard and enter `Azure Cosmos`.

# Appsettings
## Production
```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning",
      "Broccoli.App.Shared.Services.IngredientParsing": "Trace"
    }
  },
  "Cloudinary": {
    "CloudName": "dmpzvstgn",
    "ApiKey": "477495389986689",
    "ApiSecret": "6qg6nQtXPa0tLf4TtnNtJWOGPqM",
    "Folder": "recipes"
  },
  "CosmosDb": {
    "EndpointUri": "https://cosmosdb-account-broccoli.documents.azure.com:443/",
    "PrimaryKey": "????",
    "DatabaseName": "BroccoliAppDb",
    "BypassSslValidation": false
  },
  "FeatureFlags": {
    "FoodDatabaseEditing": false
  },
  "Usda": {
    "ApiKey": "SZSHCYB0prd6cVyuMlcgmzfqhMRaletpeeXYy6Od"
  }
}
```

## Development
```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning",
      "Broccoli.App.Shared.Services.IngredientParsing": "Trace"
    }
  },
  "Cloudinary": {
    "CloudName": "dmpzvstgn",
    "ApiKey": "477495389986689",
    "ApiSecret": "6qg6nQtXPa0tLf4TtnNtJWOGPqM",
    "Folder": "recipes"
  },
  "CosmosDb": {
    "EndpointUri": "https://localhost:8081",
    "PrimaryKey": "????",
    "DatabaseName": "BroccoliAppDb",
    "BypassSslValidation": true
  },
  "FeatureFlags": {
    "FoodDatabaseEditing": true
  },
  "Usda": {
    "ApiKey": "SZSHCYB0prd6cVyuMlcgmzfqhMRaletpeeXYy6Od"
  },
  "DevCredentials": {
    "Username": "admin",
    "Password": "admin"
  }
}
```

# USDA Food API
- https://fdc.nal.usda.gov/api-guide
# Cloudinary
- Used for storing recipe images.
- https://console.cloudinary.com/app/c-474b664a7c2bd7c65b1755bee96e94/home/dashboard
# Inspiration
- [Mealie.io](https://mealie.io/)
- https://mycookbook.com/
- Paprika