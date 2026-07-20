# Practice Assessment for Exam AZ-204: Developing Solutions for Microsoft Azure

Question 29 of 50

You manage a Microsoft Entra ID registered application named **app1**. App1 calls a web API, which then calls Microsoft Graph.

You need to ensure the signed-in user identity is delegated through the request chain.

Which authentication flow should you use?

Select only one answer.

Authorization code

On-Behalf-Of

**This answer is correct.**

Client credentials

**This answer is incorrect.**

Implicit

This item tests the candidate’s knowledge of accessing user data from Microsoft Graph, which is part of implementing user authentication and authorization.

OAuth 2.0 On-Behalf-Of flow (OBO) is used when an application invokes a service or web API, which in turn needs to call another service or web API. The idea is to propagate the delegated user identity and permissions through the request chain. The OAuth 2.0 authorization code grant can be used in apps that are installed on a device to gain access to protected resources, such as web APIs. The OAuth 2.0 client credentials grant flow permits a web service (confidential client) to use its own credentials, instead of impersonating a user, to authenticate when calling another web service. Implicit is a redirection-based flow. The client must be capable of interacting with the resource owner's user-agent (typically a web browser). Authorization code, On-Behalf-Of, and implicit cannot be used to delegate user permission and identity.

[Implement authentication by using the Microsoft Aut](https://learn.microsoft.com/training/modules/implement-authentication-by-using-microsoft-authentication-library/)