## [[23 - Explore API Management]]

### Azure Training Practical Exercises

- [ ] **1. Import an API:**
    - [ ] **Goal:** Learn how to expose an existing backend API through API Management.
    - [ ] Follow the official Microsoft Learn exercise: [Import an API into Azure API Management](https://learn.microsoft.com/en-us/training/modules/explore-api-management/8-exercise-import-api).

### Custom Practical Exercises

- [x] **2. Cost and Tier Analysis:**
    - [x] **Goal:** Understand the pricing model for API Management.
    - [x] Investigate the different pricing tiers (Consumption, Developer, Basic, Standard, Premium).
	    - The **Consumption tier** has **no fixed monthly fee**. It is a serverless option billed purely based on usage:
	    - It includes a certain number of **free API operations** (e.g., the first 1 million per subscription).
	    - The **Developer tier** has a fixed, low monthly cost (approximately **$48.04 USD** per month)
    - [x] Determine which tier would be most cost-effective for the "Envelopes" API based on expected usage.
	    - 🚨Could run a free version very easily for envelopes to explore the service further.
- [ ] **3. Deploy and Secure the "Envelopes" API:**
    - [ ] **Goal:** Place your existing "Envelopes" API behind a secure, managed gateway.
    - [ ] Deploy an API Management instance.
    - [ ] Import your "Envelopes" API.
    - [ ] **Apply a Policy:** Implement a rate-limiting policy to prevent abuse (e.g., no more than 100 requests per minute).
    - [ ] **Secure with a Subscription:** Create a "Product" for your API and require a subscription key for access.
    - [ ] **(Optional) Secure with a Certificate:** If you have a client certificate, configure a policy to validate it.

## [[24 -  Develop event-based solutions - Explore Azure Event Grid]]

### Azure Training Practical Exercises

- [ ] **1. Route Custom Events:**
    - [ ] **Goal:** Learn how to publish and subscribe to custom events using Event Grid.
    - [ ] Follow the official Microsoft Learn exercise: [Route custom events to a web endpoint with Azure Event Grid](https://learn.microsoft.com/en-us/training/modules/azure-event-grid/8-event-grid-custom-events).

## [[25 - Develop event-based solutions - Explore Azure Event Hubs]]

### Azure Training Practical Exercises

- [ ] **1. Send and Receive Events:**
    - [ ] **Goal:** Learn the basics of sending and receiving streams of events with Event Hubs.
    - [ ] Follow the official Microsoft Learn exercise: [Send and receive events with Azure Event Hubs](https://learn.microsoft.com/en-us/training/modules/azure-event-hubs/6a-event-hubs-send-receive).

## [[26 - Develop message-based solutions - Discover Azure message queues]]

### Azure Training Practical Exercises

- [ ] **1. Service Bus Queues:**
    - [ ] **Goal:** Learn how to use Service Bus queues for reliable, ordered messaging.
    - [ ] Follow the official Microsoft Learn exercise: [Send and receive messages from a Service Bus queue](https://learn.microsoft.com/en-us/training/modules/discover-azure-message-queue/6-send-receive-messages-service-bus).
- [ ] **2. Storage Queues:**
    - [ ] **Goal:** Learn how to use Azure Storage Queues for simple, large-scale messaging.
    - [ ] Follow the official Microsoft Learn exercise: [Send and receive messages from an Azure Storage queue](https://learn.microsoft.com/en-us/training/modules/discover-azure-message-queue/8a-send-receive-messages-queue-storage).