
## [[15 - Implement user authentication and authorization Explore the Microsoft identity platform]]

> [!question] Question 1 Which of the types of permissions supported by the Microsoft identity platform is used by apps that have a signed-in user present?
> 
> - Delegated permissions
> - App-only access permissions
> - Both delegated and app-only access permissions
> 
> > [!success]- Answer 
> > Delegated permissions

> [!question] Question 2 Which of the following app scenarios require code to handle Conditional Access challenges?
> 
> - Apps performing the device-code flow
> - Apps performing the on-behalf-of flow
> - Apps performing the Integrated Windows authentication flow
> 
> > [!success]- Answer 
> > Apps performing the on-behalf-of flow

## [[16 - Implement user authentication and authorization  -Implement authentication by using the Microsoft Authentication Library]]

> [!question] Question 1 Which of the following MSAL libraries supports single-page web apps?
> 
> - MSAL Node
> - MSAL.js
> - MSAL.NET
> 
> > [!success]- Answer 
> > MSAL.js

> [!question] Question 2 What is the purpose of using `PublicClientApplicationBuilder` class in MSAL.NET?
> 
> - The class creates a new Azure account.
> - To configure and instantiate a public client application that can acquire tokens and authenticate users against the Microsoft identity platform.
> - Adds a new API permission to the registered app.
> 
> > [!success]- Answer 
> > To configure and instantiate a public client application that can acquire tokens and authenticate users against the Microsoft identity platform.

## [[17 - Implement user authentication and authorization - Implement shared access signatures]]

> [!question] Question 1 Which of the following types of shared access signatures (SAS) applies to Blob storage only?
> 
> - Account SAS
> - Service SAS
> - User delegation SAS
> 
> > [!success]- Answer 
> > User delegation SAS

> [!question] Question 2 Which of the following best practices provides the most flexible and secure way to use a service shared access signature (SAS)?
> 
> - Associate SAS tokens with a stored access policy.
> - Always use HTTPS
> - Implement a user delegation SAS
> 
> > [!success]- Answer 
> > Associate SAS tokens with a stored access policy.

## [[18 - Implement user authentication and authorization -Explore Microsoft Graph]]

> [!question] Question 1 Which HTTP method is used to partially update a resource with new values?
> 
> - POST
> - PATCH
> - PUT
> 
> > [!success]- Answer 
> > PATCH

> [!question] Question 2 Which of the components of the Microsoft 365 platform is used to deliver data external to Azure into Microsoft Graph services and applications?
> 
> - Microsoft Graph API
> - Microsoft Graph connectors
> - Microsoft Graph Data Connect
> 
> > [!success]- Answer 
> > Microsoft Graph connectors

## [[19 - Implement secure Azure solutions - Implement Azure Key Vault]]

> [!question] Question 1 Which of the below methods of authenticating to Azure Key Vault is recommended for most scenarios?
> 
> - Service principal and certificate
> - Service principal and secret
> - Managed identities
> 
> > [!success]- Answer 
> > Managed identities

> [!question] Question 2 Azure Key Vault protects data when it's traveling between Azure Key Vault and clients. What protocol does it use for encryption?
> 
> - Secure Sockets Layer
> - Transport Layer Security
> - Presentation Layer
> 
> > [!success]- Answer 
> > Transport Layer Security

## [[20 - Implement secure Azure solutions - Implement managed identities]]

> [!question] Question 1 Which of the following managed identity characteristics is indicative of user-assigned identities?
> 
> - Shared lifecycle with an Azure resource
> - Independent life-cycle
> - Can only be associated with a single Azure resource
> 
> > [!success]- Answer 
> > Independent life-cycle

> [!question] Question 2 A client app requests managed identities for an access token for a given resource. Which of the following options is the basis for the token?
> 
> - Oauth 2.0
> - Service principal
> - Virtual machine
> 
> > [!success]- Answer 
> > Service principal

## [[21 - Implement secure Azure solutions - Implement Azure App Configuration]]

> [!question] Question 1 What is the purpose of labels in Azure App Configuration?
> 
> - Labels are used to differentiate key-values with the same key in App Configuration.
> - Labels are used to encrypt key-values in App Configuration.
> - Labels are used to limit the size of key-values in App Configuration.
> 
> > [!success]- Answer 
> > Labels are used to differentiate key-values with the same key in App Configuration.

> [!question] Question 2 What is the role of a feature manager in managing application features?
> 
> - A feature manager is a rule for evaluating the state of a feature flag.
> - A feature manager is a variable with a binary state of on or off.
> - A feature manager is an application package that handles the lifecycle of all the feature flags in an application.
> 
> > [!success]- Answer 
> > A feature manager is an application package that handles the lifecycle of all the feature flags in an application.

> [!question] Question 3 What is the purpose of using customer-managed keys in Azure App Configuration?
> 
> - To enable authentication with Microsoft Entra ID
> - To permanently store the unwrapped encryption key
> - To encrypt sensitive information at rest
> 
> > [!success]- Answer 
> > To encrypt sensitive information at rest
