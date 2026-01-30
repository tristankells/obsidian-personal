- Front End - https://app-envelopes-app-dev-ro5pojtby3wwy.azurewebsites.net/
	- API - https://app-envelopes-api-dev-gsyykfmj4a4kk.azurewebsites.net
		- Database - https://turso-envelopes-dev-tristankells.aws-ap-south-1.turso.io
# Todo

### Infra
- [ ] Automate deployment with CI/CD to deveops repos.
	- [ ] Do via pipeline files in a repeatable way.

### Envelopes API
- Fix the broken swagger page (https://localhost:7089/swagger/index.html)
- Resolve the project warnings.
- Resolve the preview version of dotnet warning.
### Envelopes App
- How should we handle the category ID on credit transactions...
	- (Currently...) Hardcoded ID == 100 category?
- Should be able to move money from a category to cover a -negative overall balance.
- Fixes to import
	- See if we can make it faster.
		- [] Guide for rider performance debugging.
		- Implement bulk insert endpoint.
	- Implement loading on the beginning of import.
	- Loading at the end of import.
	- Implement duplication detection.
	- Add notes when you import.
- 
---
# Features
[[Update parser to respect new ASB bank format]]
# Documentation
# Envelopes App - Azure Resource Group Naming Convention
**Format**: `rg-envelopes-{environment}`
**Environments**:
- `dev` - Development/testing
- `prod` - Production (live app)
**Examples**:
- `rg-envelopes-dev`
- `rg-envelopes-prod`
**Notes**:
- Solo developer, personal project
- Keep it simple - just 2 environments for now
---
# Database
```bash
cd C:\Dev\Git\Envelopes.Api;
dotnet ef migrations add InitialCreate --project Envelopes.Api;
dotnet ef migrations script --project Envelopes.Api --output migration.sql;
```
- Remove all of the `COMMIT;` and `START TRANSACTION;` from migration.sql.
- Open the SQL console for you Turoso database: [tristankells | Turso App](https://app.turso.tech/tristankells/databases/turso-envelopes-dev/data?view=sql-console)
- 
---
```bash
dotnet user-secrets set "ConnectionStrings:TursoAuthToken" "eyJhbGciOiJFZERTQSIsInR5cCI6IkpXVCJ9.eyJhIjoicnciLCJpYXQiOjE3NjQzNzAzNTEsImlkIjoiMjU3MDc2YzktZjc1MC00MWQ5LTk0NjMtYTg0MWQ5NTYzMjRmIiwicmlkIjoiYWQyMzFjNGQtZGQ2Yi00N2YwLWJmNTctZGI2NzlkNWQ1MDJiIn0.Gqo-QcET9vlFWTMVq08WyqEczoejtT6OkjcTa10H92g2T5fy-9-h3lTDgZoNp7rgaeglag4sm7k4NeOTU984Dw"

dotnet user-secrets set "ConnectionStrings:TursoUrl" "https://turso-envelopes-dev-tristankells.aws-ap-south-1.turso.io/v2/pipeline"
```

## How to migrate data from local SQLite to Turso?
1. {find local slqlite}
2. {download sqlite}
3. {execute command to export to csv}
4. Remove the bottom row of the csv, otherwise causes issue during import.
5. Download DBbeaver
6. Connect to libSql database.
7. Right click table, click import data.
8. Import, make sure to change to UTF-18 encoding..


---
# Envelopes App
- [https://app-envelopes-app-dev-gsyykfmj4a4kk.azurewebsites.net](https://app-envelopes-app-dev-ro5pojtby3wwy.azurewebsites.net/)
---
# Envelopes API
- https://app-envelopes-api-dev-gsyykfmj4a4kk.azurewebsites.net
## Environment Variable
## appsettings.Production.json
```json
{  
  "ConnectionStrings": {  
    "EnvelopesDatabase": ""  
  },  
  "Turso": {  
    "Url": "https://turso-envelopes-dev-tristankells.aws-ap-south-1.turso.io/v2/pipeline",  
    "AuthToken": "eyJhbGciOiJFZERTQSIsInR5cCI6IkpXVCJ9.eyJhIjoicnciLCJpYXQiOjE3Njk3Mzg1OTEsImlkIjoiMjU3MDc2YzktZjc1MC00MWQ5LTk0NjMtYTg0MWQ5NTYzMjRmIiwicmlkIjoiYWQyMzFjNGQtZGQ2Yi00N2YwLWJmNTctZGI2NzlkNWQ1MDJiIn0.NwRJp7D2KjSQR1VAbZ9Wr7deWV1LXwreACmyTVSABpoTVxWkmZSMycxBXj40Oiz-rgr8p3XmHHzSvUztuFabDA"  
  },  
  "Logging": {  
    "LogLevel": {  
      "Default": "Information",  
      "Microsoft.AspNetCore": "Warning"  
    }  
  },  "AllowedHosts": "*"  
}
```
## appsettings.Development.json
```json
{  
  "ConnectionStrings": {  
    "EnvelopesDatabase": "Data Source=envelopes.db",  
    "TursoUrl": "",  
    "TursoAuthToken": ""  
  },  
  "Logging": {  
    "LogLevel": {  
      "Default": "Information",  
      "Microsoft.AspNetCore": "Warning"  
    }  
  },  "AllowedHosts": "*"  
}
```

---
# GraphQL
- When running Envelopes.Api locally, this is the GraphQl endpoint: `https://localhost:7089/graphql`
- And example POST request for accounts looks like this:
	```json
	{
	  accounts {
	    id
	    name
	    balance
	  }
	}
	```






[[YNAB Reference Material]]

---
# Entity Framework
## Get detailed logging and debug info
- Add `EnableDetailedErrors`, `LogTo(Console.WriteLine, LogLevel.Information)` and `EnableSensitiveDataLogging`.
- This will log all the SQL queries being executed.
- Example:
	```c#
	    // Use Turso (libSQL) connection  
	    string connectionString = $"{tursoUrl};{tursoAuthToken}";  
	    builder.Services.AddDbContext<EnvelopesDbContext>(options =>  
	        options.UseLibSql(connectionString)
	        // ADD THESE 3 LINES 
	            .EnableDetailedErrors()  
	            .LogTo(Console.WriteLine, LogLevel.Information)  
	            .EnableSensitiveDataLogging());
	```

---
# Fiddler
## Inspect HTTP traffic from visual studio debugger.
- To use Fiddler to inspect traffic, the application must send traffic via the Fiddler proxy (listening on `8888`).
	- Install fiddler classic.
	- Enable HTTPS decryption.
	- Add the following environment variable via launchSettings.json
		- `"HTTPS_PROXY": "http://127.0.0.1:8888"`
	- Example:
		```json
		"https (Production)": {  
		  "commandName": "Project",  
		  "launchBrowser": true,  
		  "launchUrl": "swagger",  
		  "environmentVariables": {  
		    "ASPNETCORE_ENVIRONMENT": "Production",  
		    // ADD THIS LINE
		    "HTTPS_PROXY": "http://127.0.0.1:8888"  
		  },  
		  "dotnetRunMessages": true,  
		  "applicationUrl": "https://localhost:7089;http://localhost:5047"  
		},
		```

---
# Bicep
- If you recieve this `OSError: [WinError 193] %1 is not a valid Win32 application`, bicep.exe from your computer and run  `az bicep install` again.
### Commands
```shell
# 1. Build your bicep files
az bicep build-params --file C:\Dev\Devops\envelopes.infra\params\dev.bicepparam

# Deploy you bicep files.
az deployment sub create --location newzealandnorth --parameters C:\Dev\Devops\envelopes.infra\params\dev.bicepparam


az deployment group create \ --resource-group YourResourceGroupName \ --template-file main.bicep
```
---
# Prompt
I'm deploying the app "C:\Dev\Devops\Envelopes.App" to Azure App Service. I'm using infrastructure deploy via the bicep file in "C:\Dev\Devops\envelopes.infra". The deployment is automated via Azure Repos setup in Deployment Center. I'm getting this error, how would I resolve it:
```
2026-03-06T00:26:47.4449395Z    _____
2026-03-06T00:26:47.444968Z   /  _  \ __________ _________   ____
2026-03-06T00:26:47.4449707Z  /  /_\  \\___   /  |  \_  __ \_/ __ \
2026-03-06T00:26:47.4449765Z /    |    \/    /|  |  /|  | \/\  ___/
2026-03-06T00:26:47.4449783Z \____|__  /_____ \____/ |__|    \___  >
2026-03-06T00:26:47.4449801Z         \/      \/                  \/
2026-03-06T00:26:47.4449819Z A P P   S E R V I C E   O N   L I N U X
2026-03-06T00:26:47.4449835Z
2026-03-06T00:26:47.4449854Z Documentation       : http://aka.ms/webapp-linux
2026-03-06T00:26:47.4449875Z Dotnet quickstart   : https://aka.ms/dotnet-qs
2026-03-06T00:26:47.4449892Z ASP .NETCore Version: 9.0.12
2026-03-06T00:26:47.4449911Z Instance Name       : 10-30-0-140
2026-03-06T00:26:47.4449935Z Instance Id         : 9be4b8e022d07610be288d9acbc9280ae50fd944942360603a31288ed1ee591e
2026-03-06T00:26:47.4449951Z
2026-03-06T00:26:47.4449982Z Note: Any data outside '/home' is not persisted
2026-03-06T00:26:49.2701889Z Starting OpenBSD Secure Shell server: sshd.
2026-03-06T00:26:49.276361Z WEBSITES_INCLUDE_CLOUD_CERTS is not set to true.
2026-03-06T00:26:49.3073092Z Updating certificates in /etc/ssl/certs...
2026-03-06T00:26:53.8127416Z rehash: warning: skipping duplicate certificate in azl_SSL.com_TLS_ECC_Root_CA_2022.pem
2026-03-06T00:26:53.8137136Z rehash: warning: skipping duplicate certificate in azl_SSL.com_TLS_RSA_Root_CA_2022.pem
2026-03-06T00:26:53.8890683Z rehash: warning: skipping ca-certificates.crt,it does not contain exactly one certificate or CRL
2026-03-06T00:26:53.977732Z 4 added, 0 removed; done.
2026-03-06T00:26:53.9777669Z Running hooks in /etc/ca-certificates/update.d...
2026-03-06T00:26:53.980087Z done.
2026-03-06T00:26:53.985017Z CA certificates copied and updated successfully.
2026-03-06T00:26:54.0934285Z Starting periodic command scheduler: cron.
2026-03-06T00:26:54.0960575Z Running oryx create-script -appPath /home/site/wwwroot -output /opt/startup/startup.sh -defaultAppFilePath /defaulthome/hostingstart/hostingstart.dll     -bindPort 8080 -bindPort2 '' -userStartupCommand ''
2026-03-06T00:26:54.1854374Z Found build manifest file at '/home/site/wwwroot/oryx-manifest.toml'. Deserializing it...
2026-03-06T00:26:54.1925876Z Build Operation ID: 9e81de2008a76008
2026-03-06T00:26:54.1983929Z
2026-03-06T00:26:54.1984315Z Agent extension
2026-03-06T00:26:54.1988326Z Before if loop >> DotNet Runtime 9.0.12
2026-03-06T00:26:54.4250884Z DotNet Runtime 9.0.12Writing output script to '/opt/startup/startup.sh'
2026-03-06T00:26:54.4811067Z Found startup DLL name from manifest file
2026-03-06T00:26:54.4817954Z Running the command: dotnet "Envelopes.App.dll"
2026-03-06T00:26:54.5032237Z The command could not be loaded, possibly because:
2026-03-06T00:26:54.5032753Z   * You intended to execute a .NET application:
2026-03-06T00:26:54.5032845Z       The application 'Envelopes.App.dll' does not exist.
2026-03-06T00:26:54.5035051Z   * You intended to execute a .NET SDK command:
2026-03-06T00:26:54.5035126Z       No .NET SDKs were found.
2026-03-06T00:26:54.5035142Z
2026-03-06T00:26:54.5035161Z Download a .NET SDK:
2026-03-06T00:26:54.503518Z https://aka.ms/dotnet/download
2026-03-06T00:26:54.5035192Z
2026-03-06T00:26:54.5035207Z Learn about SDK resolution:
2026-03-06T00:26:54.5035222Z https://aka.ms/dotnet/sdk-not-found
```


It looks like Blazor WebAssembly only works with windows, not Linux app service. Can you update the bicep accordingly?