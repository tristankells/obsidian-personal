---

tags: [azure, cloud, certification, AZ-204]
created: 2025-12-13
---
# 📝 Summary
**What is this module about?**  
After completing this module, you'll be able to:

- Describe the components, and their function, of the API Management service.
- Explain how API gateways can help manage calls to your APIs.
- Secure access to APIs by using subscriptions and certificates.
- Import and configure an API.
---
# 🔗 Links
**Useful resources and official docs:**  
- https://learn.microsoft.com/en-us/training/modules/explore-api-management/1-introduction
---
# ✅ Module Assessment
**Key questions and answers from the module assessment:**  
> [!question] Question 1 Which of the following components of the API Management service would a developer use if they need to create an account and subscribe to get API keys?
> 
> - API gateway
> - Azure portal
> - Developer portal
> 
> > [!success]- Answer 
> > Developer portal

> [!question] Question 2 Which of the following API Management policies applies a policy based on a condition?
> 
> - forward-request
> - choose
> - return-response
> 
> > [!success]- Answer 
> > choose
---
# 🧠 Flashcards
**Important terms and definitions for quick recall:**  
## Card 1: API Management Three Core Components

**Q: What are the three core components of Azure API Management and what is the primary function of each?**

**A:** (1) API gateway - accepts and routes API calls, verifies credentials, enforces quotas/rate limits, transforms requests/responses, and caches. (2) Management plane - administrative interface for configuring service settings, defining APIs, and setting policies. (3) Developer portal - automatically generated customizable website where developers access documentation, test APIs, and manage subscriptions/keys.

**Context:** All three components are Azure-hosted and fully managed by default. The gateway is the endpoint that handles runtime API calls, the management plane is where administrators configure the API program, and the developer portal is the self-service interface for API consumers.

---

## Card 2: API Management Products and Groups

**Q: What is the difference between Open and Protected products in API Management, and what are the three immutable system groups that manage product visibility?**

**A:** Open products can be used without subscription; Protected products require subscription before use. Three system groups: (1) Administrators (manage service and create APIs), (2) Developers (authenticated users building apps), (3) Guests (unauthenticated users with read-only access).

**Context:** Products are how APIs are surfaced to developers and contain one or more APIs. Subscription approval for Protected products can require administrator approval or be auto-approved. Administrators can also create custom groups or use external Microsoft Entra groups beyond the three system groups.


**Q: What are three key problems that an API gateway solves when clients would otherwise send requests directly to back-end services?**

**A:** (1) Prevents complex client code from tracking multiple endpoints and handling failures, (2) decouples client from backend (client doesn't need to know service decomposition), (3) eliminates need for each service to individually handle authentication, SSL, and rate limiting.

**Context:** Without a gateway, single operations might require calls to multiple services, services must expose client-friendly protocols (limiting communication choices), and public-facing services become attack surfaces requiring hardening. The gateway acts as a reverse proxy handling these cross-cutting concerns.

---

## Card 2: Managed vs Self-Hosted API Gateway

**Q: What is the key difference between managed and self-hosted gateways in Azure API Management, and when would you use a self-hosted gateway?**

**A:** Managed gateway is deployed in Azure (all API traffic flows through Azure regardless of backend location). Self-hosted gateway is a containerized version used for hybrid/multicloud scenarios where gateways run off Azure in the same environments as API backends.

**Context:** Managed gateway is the default component deployed for every API Management instance in every service tier. Self-hosted gateway enables customers with hybrid IT infrastructure to manage on-premises and cross-cloud APIs from a single API Management service in Azure.

## Card 1: API Management Policy Configuration Sections

**Q: What are the four sections of an API Management policy configuration XML document, and what happens to execution flow when an error occurs?**

**A:** (1) inbound (applied to request), (2) backend (before forwarding to backend), (3) outbound (applied to response), (4) on-error (error handling). When an error occurs, remaining steps in inbound/backend/outbound are skipped and execution jumps to on-error section.

**Context:** Policies are executed sequentially in order. In the on-error section, you can review errors using context.LastError, customize error responses with set-body policy, and configure error handling behavior. Policy expressions (C# statements in @(expression) format) can be used as attribute/text values.

---

## Card 2: Policy Scope Ordering with Base Element

**Q: In API Management, when both global-level and API-level policies exist, how does the `<base />` element control the order of policy execution?**

**A:** The `<base />` element determines when broader-scope (e.g., global) policies execute relative to current-scope policies. Policies before `<base />` execute first, then broader-scope policies, then policies after `<base />`.

**Context:** Example: In `<inbound><cross-domain /><base /><find-and-replace /></inbound>`, execution order is: (1) cross-domain, (2) any global policies (via base), (3) find-and-replace. This allows deterministic ordering of combined policy statements across different scopes (global, product, API, operation).

## Card 1: Forward Request Policy Behavior

**Q: What happens when you remove the forward-request policy from an API Management configuration, and when are outbound policies evaluated in this scenario?**

**A:** The request is not forwarded to the backend service. Outbound policies are evaluated immediately upon successful completion of inbound policies (no backend call is made).

**Context:** The forward-request policy forwards the incoming request to the backend service specified in the request context. The backend service URL is specified in API settings and can be changed using the set-backend-service policy. Removing forward-request is useful for mocking or cached responses.

---

## Card 2: Control Flow Policy Structure

**Q: In API Management's choose (control flow) policy, what elements are required versus optional, and how are conditions evaluated?**

**A:** Required: at least one `<when/>` element. Optional: `<otherwise/>` element. Conditions in `<when/>` elements are evaluated in order of appearance; the first true condition executes its enclosed statements. If all conditions are false, `<otherwise/>` statements execute.

**Context:** Similar to if-then-else or switch constructs in programming. Example: `<choose><when condition="Boolean expression"><!-- statements --></when><otherwise><!-- statements --></otherwise></choose>`. Policy statements within the first true `<when/>` are applied.

---

## Card 3: Limit Concurrency Policy Response

**Q: What HTTP status code does the limit-concurrency policy return when the maximum number of concurrent requests is exceeded?**

**A:** 429 Too Many Requests status code (requests fail immediately when exceeding the specified max-count).

**Context:** The limit-concurrency policy prevents enclosed policies from executing by more than the specified number of requests at any time. Format: `<limit-concurrency key="expression" max-count="number"><!-- nested policy statements --></limit-concurrency>`. Used to protect backend services from overload.

## Card 1: API Management Subscription Key Scopes

**Q: What are the three main subscription scopes in Azure API Management, ordered from broadest to most specific?**

**A:** (1) All APIs - applies to every API accessible from the gateway, (2) Single API - applies to one imported API and all its endpoints, (3) Product - a collection of one or more APIs with configurable access rules, usage quotas, and terms of use.

**Context:** Subscriptions give granular control over permissions and policies. Each subscription contains a pair of autogenerated keys (primary and secondary) that can be passed in request headers or query string parameters. Different scopes allow different levels of API access control.

---

## Card 2: Subscription Key Regeneration Strategy

**Q: Why does every API Management subscription have two keys (primary and secondary), and how does this help during key regeneration?**

**A:** Having two keys allows you to regenerate one key while using the other, avoiding downtime. For example, you can switch apps to use the secondary key, then regenerate the primary key without service interruption.

**Context:** Keys can be regenerated anytime, such as when a key is suspected to be shared with unauthorized users. Default header name is `Ocp-Apim-Subscription-Key`, and default query string is `subscription-key`. Requests without valid keys return 401 Access Denied from the API gateway.

---
## Card 1: TLS Client Certificate Properties

**Q: What are the four certificate properties that API Management gateway can inspect during TLS client authentication?**

**A:** (1) Certificate Authority (CA) - only allow certificates signed by particular CA, (2) Thumbprint - allow certificates with specified thumbprint, (3) Subject - only allow certificates with specified subject, (4) Expiration Date - don't allow expired certificates.

**Context:** These properties can be mixed together to form custom policy requirements (e.g., certificate must be signed by trusted CA AND not expired). Client certificates are signed to prevent tampering. Certificates can be verified by checking the issuer (trusted CA) or ensuring trust in self-signed certificates from known sources.

---

## Card 2: Multiple Certificate Validation in API Management

**Q: In API Management, how do you validate client certificates from multiple partners who each have different thumbprints, and what policy method checks against uploaded certificates?**

**A:** Upload partner certificates to the API Management resource via the Client certificates page in Azure portal, then use `context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint)` in the policy to check if the request certificate matches any uploaded certificate.

**Context:** This approach supports multiple customers/partners passing different certificates. The policy also checks `context.Request.Certificate.Verify()` to ensure certificate validity. If validation fails, returns 403 Invalid client certificate status. This is more scalable than hardcoding individual thumbprints.

---
# 🛠 Practice Exercises
**Hands-on tasks or labs:**  
- [ ] Investigate cost of API Management Platform.
	- [ ] Deploy one for Envelopes API.
	- [ ] Pick a policy to programmatically apply.
	- [ ] Secure your API behind an subscription.
	- [ ] Secure your API with a certificate?
- [ ] https://learn.microsoft.com/en-us/training/modules/explore-api-management/8-exercise-import-api
---
# 📚 Additional Notes
**Any extra insights, tips, or gotchas:** 