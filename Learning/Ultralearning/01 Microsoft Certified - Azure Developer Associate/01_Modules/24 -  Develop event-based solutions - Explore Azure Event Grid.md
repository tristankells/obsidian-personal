---

tags: [azure, cloud, certification, AZ-204]
created: 2025-12-13
---
# 📝 Summary
**What is this module about?**

After completing this module, you'll be able to:
- Describe how Event Grid operates and how it connects to services and event handlers.
- Explain how Event Grid delivers events and how it handles errors.
- Implement authentication and authorization.
- Route events to a custom endpoint.
---
# 🔗 Links
**Useful resources and official docs:**  
- https://learn.microsoft.com/en-us/training/modules/azure-event-grid/1-introduction
---
# ✅ Module Assessment
**Key questions and answers from the module assessment:**  
> [!question] Question 1 Which of the following event schema properties requires a value?
> 
> - Topic
> - Data
> - Subject
> 
> > [!success]- Answer 
> > Subject

> [!question] Question 2 Which of the following Event Grid built-in roles is appropriate for managing Event Grid resources?
> 
> - Event Grid Contributor
> - Event Grid Subscription Contributor
> - Event Grid Data Sender
> 
> > [!success]- Answer 
> > Event Grid Contributor

> [!question] Question 3 What is the purpose of the CloudEvents schema in Azure Event Grid?
> 
> - To provide a proprietary event schema specific to Azure services.
> - To simplify interoperability by providing a common event schema for publishing and consuming cloud-based events.
> - To replace the Event Grid event schema entirely for all event types.
> 
> > [!success]- Answer 
> > To simplify interoperability by providing a common event schema for publishing and consuming cloud-based events.

> [!question] Question 4 What happens when Event Grid receives a 400 (Bad Request) or 413 (Request Entity Too Large) response code during event delivery?
> 
> - Event Grid retries the delivery indefinitely until the endpoint responds.
> - Event Grid schedules the event for dead-lettering if a dead-letter location is configured.
> - Event Grid immediately drops the event without further action.
> 
> > [!success]- Answer 
> > Event Grid schedules the event for dead-lettering if a dead-letter location is configured.

> [!question] Question 5 What is the purpose of the validation handshake in Azure Event Grid when using a custom webhook endpoint?
> 
> - To prove ownership of the webhook endpoint before delivering events
> - To ensure the webhook endpoint is hosted on Azure infrastructure
> - To encrypt the event data being sent to the webhook endpoint
> 
> > [!success]- Answer 
> > To prove ownership of the webhook endpoint before delivering events
---
# 🧠 Flashcards
**Important terms and definitions for quick recall:**  
## Card 1: Event Grid Topic Types

**Q: What are the three types of topics in Azure Event Grid, and what distinguishes each type?**

**A:** (1) System topics - built-in topics from Azure services (publisher owns, not visible in your subscription), (2) Custom topics - application and third-party topics (visible in your subscription when created or assigned access), (3) Partner topics - used to subscribe to events from partner systems via Partner Events feature.

**Context:** Topics hold events published to Event Grid. To receive events, subscribers create event subscriptions on topics. System topics require providing resource information to subscribe; custom topics appear in your subscription; partner topics enable integration with external partner systems.

---

## Card 2: Event Grid Delivery Methods

**Q: What are the two delivery patterns Event Grid supports for message consumption, and how do they differ in how subscribers receive events?**

**A:** (1) Push delivery - Event Grid sends events to subscribers (proactive), (2) Pull delivery - subscribers connect to Event Grid to read events (reactive/on-demand).

**Context:** Event Grid supports both HTTP and MQTT protocols. For push delivery with HTTP webhook handlers, events are retried until handler returns 200 OK. For Azure Storage Queue handlers, events are retried until Queue service successfully processes the message. Event subscriptions can filter events by type or subject pattern.

---

## Card 3: CloudEvents Format in Event Grid

**Q: What is the maximum allowed event size in Azure Event Grid, and how are events larger than 64 KB charged?**

**A:** Maximum allowed size is 1 MB. Events over 64 KB are charged in 64-KB increments.

**Context:** Event Grid conforms to Cloud Native Computing Foundation's CloudEvents 1.0 specification using HTTP protocol binding with JSON format. Events contain common information (source, time, unique ID) and specific information relevant to the event type. This standardization provides interoperability across systems.

## Card 1: Event Grid Array Size Limits and Charging

**Q: When posting events to an Event Grid topic, what are the size limits for the event array and individual events, and how are operations charged for events over 64 KB?**

**A:** Array total size: up to 1 MB. Individual event limit: 1 MB. Events over 64 KB are charged in 64-KB increments (e.g., a 130 KB event incurs charges as three separate events).

**Context:** Event sources send events in an array with multiple event objects, but Event Grid sends events to subscribers in an array with a single event. Exceeding size limits returns "413 Payload Too Large" response. Operations are charged in 64-KB increments even though individual events can be up to 1 MB.

---

## Card 2: Event Subject Path Filtering Strategy

**Q: In Azure Event Grid custom topics, how should publishers structure event subjects to enable effective subscriber filtering, and what is an example of narrow vs. broad filtering?**

**A:** Provide a hierarchical path for where the event happened (e.g., /A/B/C). Subscribers can filter broadly by first segment (/A gets events with /A/B/C and /A/D/E) or narrowly by more segments (/A/B gets only /A/B/* events).

**Context:** Example from Storage Accounts: subject `/blobServices/default/containers/testcontainer/blobs/file.txt` lets subscribers filter by container path for container-specific events or by suffix `.txt` for text files only. This enables subscribers to decide if they're interested in the event without processing it.


## Card 1: Event Grid Non-Retryable Errors

**Q: What are the error codes that cause Event Grid to immediately dead-letter or drop events (without retry) for Azure Resources and Webhook endpoints?**

**A:** Azure Resources: 400 (Bad Request), 413 (Request Entity Too Large). Webhooks: 400 (Bad Request), 413 (Request Entity Too Large), 401 (Unauthorized).

**Context:** These are configuration-related errors that can't be fixed with retries. If dead-letter isn't configured, events are dropped when these errors occur. For 400 and 413 responses, Event Grid immediately schedules the event for dead-lettering (if configured). Consider configuring dead-letter to prevent event loss.

---

## Card 2: Event Grid Retry Policy Configuration

**Q: What are the two configurable parameters for Event Grid's retry policy, and what are their default values and allowed ranges?**

**A:** (1) Maximum number of attempts: default 30, range 1-30. (2) Event time-to-live (TTL): default 1440 minutes, range 1-1440 minutes. Event is dropped if either limit is reached.

**Context:** Event Grid uses exponential backoff retry policy. After 30 seconds without response, messages are queued for retry with small randomization added to retry steps. If endpoint responds within 3 minutes, Event Grid attempts to remove event from retry queue (duplicates may still occur).

---

## Card 3: Event Grid Output Batching Settings

**Q: What are the two settings for Event Grid's output batching feature, and what are their constraints?**

**A:** (1) Max events per batch: must be between 1 and 5,000 (Event Grid won't exceed this number). (2) Preferred batch size in kilobytes: target ceiling for batch size (batch can be larger if a single event exceeds preferred size).

**Context:** Batching improves HTTP performance in high-throughput scenarios but is turned off by default. Example: if preferred size is 4 KB but a 10 KB event arrives, the 10 KB event is delivered in its own batch rather than being dropped. Event Grid doesn't delay events to create a batch.


## Card 1: Event Grid Built-in Roles

**Q: What are the four built-in roles in Azure Event Grid, and what is the key distinction between the Subscription Contributor/Reader roles versus the Contributor role?**

**A:** (1) Event Grid Subscription Reader, (2) Event Grid Subscription Contributor, (3) Event Grid Contributor, (4) Event Grid Data Sender. Subscription roles manage event subscriptions only (important for event domains) but don't grant access to create topics; Contributor role allows creating and managing Event Grid resources.

**Context:** Subscription Reader/Contributor roles are focused on event subscription operations and give users permissions to subscribe to topics in event domains. Event Grid Contributor has broader permissions for resource management. Event Grid Data Sender allows sending events to Event Grid topics.

---

## Card 2: Event Subscription Permission Requirements

**Q: What permission is required to create an event subscription for a non-WebHook event handler, and how does the resource scope differ between system topics and custom topics?**

**A:** Requires `Microsoft.EventGrid/EventSubscriptions/Write` permission. System topics: scope is the resource publishing the event (`/subscriptions/{id}/resourceGroups/{rg}/providers/{provider}/{type}/{name}`). Custom topics: scope is the Event Grid topic (`/subscriptions/{id}/resourceGroups/{rg}/providers/Microsoft.EventGrid/topics/{topic-name}`).

**Context:** This permission is needed because you're writing a new subscription at the resource scope. The permissions check prevents unauthorized users from sending events to your resource. Event handlers like event hubs or queue storage require this permission (WebHooks are treated differently).

## Card 1: Event Grid Event Type Filtering

**Q: When creating an Event Grid event subscription, what is the default behavior for event types, and how do you specify filtering to receive only specific event types?**

**A:** Default: all event types for the event source are sent to the endpoint. To filter: provide an array with specific event types in `includedEventTypes` (e.g., `["Microsoft.Resources.ResourceWriteFailure", "Microsoft.Resources.ResourceWriteSuccess"]`) or specify `All` for all types.

**Context:** Example use case: get notified of resource updates but not deletions by filtering for `Microsoft.Resources.ResourceWriteSuccess` event type only. This is one of three filtering options available when creating event subscriptions (along with subject filtering and advanced filtering).

---

## Card 2: Event Grid Advanced Filtering Components

**Q: What are the three components you must specify when using Event Grid's advanced filtering option?**

**A:** (1) operator type - the type of comparison (e.g., `NumberGreaterThanOrEquals`, `StringContains`), (2) key - the field in event data used for filtering (can be number, boolean, or string), (3) value or values - the value(s) to compare to the key.

**Context:** Advanced filtering filters by values in data fields. Example: `{"operatorType": "NumberGreaterThanOrEquals", "key": "Data.Key1", "value": 5}` or `{"operatorType": "StringContains", "key": "Subject", "values": ["container1", "container2"]}`. This is more powerful than subject filtering (begins with/ends with).

---
# 🛠 Practice Exercises
**Hands-on tasks or labs:**  
- [ ] https://learn.microsoft.com/en-us/training/modules/azure-event-grid/8-event-grid-custom-events
---
# 📚 Additional Notes
**Any extra insights, tips, or gotchas:** 