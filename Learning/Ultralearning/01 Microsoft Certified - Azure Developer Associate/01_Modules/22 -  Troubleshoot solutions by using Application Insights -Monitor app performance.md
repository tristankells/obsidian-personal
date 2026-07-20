---

tags: [azure, cloud, certification, AZ-204]
created: 2025-12-11
---
# 📝 Summary
**What is this module about?**  
Instrumenting and monitoring your apps helps you maximize their availability and performance.

After completing this module, you'll be able to:

- Describe how Application Insights works and how it collects events and metrics.
- Instrument an app for monitoring, and perform availability tests.
- Use Application Map to help you monitor performance and troubleshoot issues.
---
# 🔗 Links
**Useful resources and official docs:**  
https://learn.microsoft.com/en-us/training/modules/monitor-app-performance/1-introduction
---
# ✅ Module Assessment
**Key questions and answers from the module assessment:**  
> [!question] Question 1 Which of the following availability tests is recommended for authentication tests?
> 
> - URL ping
> - Standard
> - Custom TrackAvailability
> 
> > [!success]- Answer 
> > Custom TrackAvailability

> [!question] Question 2 Which of the following metric collection types provides near real-time querying and alerting on dimensions of metrics, and more responsive dashboards?
> 
> - Log-based
> - Preaggregated
> - Azure Service Bus
> 
> > [!success]- Answer 
> > Preaggregated
---
# 🧠 Flashcards
**Important terms and definitions for quick recall:**  
## Card 1: Application Insights Monitoring Timing Options

**Q: What are the two main timing approaches for instrumenting an application with Application Insights, and what is the key advantage of each?**

**A:** (1) At run time on the server - ideal for already deployed applications, avoids code updates. (2) At development time - allows customization of telemetry collection and sending additional telemetry.

**Context:** Application Insights is an Azure Monitor extension providing APM features. Both approaches enable proactive performance understanding and reactive incident review. You can also add web page instrumentation, mobile app monitoring via Visual Studio App Center, and availability tests.

## Card 2: Application Insights Distributed Tracing Feature

**Q: What is the purpose of Application Insights' Distributed Tracing feature?**

**A:** Search and visualize an end-to-end flow of a given execution or transaction.

**Context:** Distributed Tracing works alongside Application Map (high-level architecture view with component health) and Smart Detection (automatic failure/anomaly detection). It helps track requests across multiple services and components, essential for understanding performance in microservices architectures.

## Card 1: Log-Based vs Standard Metrics Use Cases

**Q: In Application Insights, when should you use standard (preaggregated) metrics versus log-based metrics?**

**A:** Standard metrics are better for dashboarding and real-time alerting (due to better query performance). Log-based metrics are superior for data analysis and ad-hoc diagnostics (due to having more dimensions).

**Context:** Standard metrics are preaggregated time series with key dimensions only, providing faster queries. Log-based metrics retain complete events with all properties, enabling detailed analysis like exact request counts by distinct users and diagnostic traces with exceptions/dependency calls.

---

## Card 2: Preaggregation and Sampling Accuracy

**Q: How does ingestion sampling affect the accuracy of preaggregated metrics in Application Insights, and why?**

**A:** Ingestion sampling never impacts the accuracy of preaggregated metrics because the collection endpoint preaggregates events before ingestion sampling occurs.

**Context:** This applies regardless of SDK version. For SDKs with preaggregation (Application Insights 2.7+), metrics are preaggregated during collection, so sampling/filtering doesn't affect accuracy. For older SDKs without preaggregation, the backend aggregates events at the collection endpoint before sampling.

## Card 1: Application Insights Instrumentation Methods

**Q: What are the two methods for instrumenting an application with Application Insights, and what is the key trade-off between them?**

**A:** (1) Autoinstrumentation - enables telemetry through configuration without code changes (more convenient but less configurable). (2) Manual instrumentation - coding against Application Insights or OpenTelemetry API (more configurable but requires managing SDK updates).

**Context:** Autoinstrumentation is the easiest method when available but isn't supported in all languages. Manual instrumentation requires installing Application Insights SDKs or Azure Monitor OpenTelemetry Distros, and is necessary for custom events/metrics, custom dependency calls, or when autoinstrumentation isn't available.


**Q: What are the three circumstances that require manual instrumentation with Application Insights SDKs instead of autoinstrumentation?**

**A:** (1) You require custom events and metrics, (2) you require control over the flow of telemetry, (3) autoinstrumentation isn't available (due to language or platform limitations).

**Context:** Manual instrumentation means installing the Application Insights SDK package in your app and instrumenting the web app, background components, and JavaScript. It requires managing SDK version updates yourself, but provides flexibility that autoinstrumentation cannot offer.

## Card 1: Application Insights Availability Test Types

**Q: What are the three types of availability tests in Application Insights, and which one is recommended over the deprecated URL ping test?**

**A:** (1) Standard test (recommended - checks availability with single request, includes TLS/SSL validation, proactive lifetime check, custom headers/data), (2) Custom TrackAvailability test (custom application using TrackAvailability() method), (3) URL ping test (classic - deprecated, retiring September 30, 2026).

**Context:** You can create up to 100 availability tests per Application Insights resource. These tests send web requests at regular intervals from points worldwide, requiring no changes to your website and working with any publicly accessible HTTP/HTTPS endpoint or REST API.


**Q: In Application Insights Application Map, what is the difference in component discovery between applications with a single Application Insights resource versus distributed applications with multiple resources?**

**A:** Single resource applications (where all components are roles within one Application Insights resource) load all components immediately without discovery. Multi-resource distributed applications use progressive discovery by following HTTP dependency calls between servers with the SDK installed.

**Context:** Application Map helps spot performance bottlenecks and failure hotspots across distributed applications. Components are independently deployable parts that can use separate instrumentation keys or different roles in a single key. The map displays the full topology across multiple levels and can visualize complex topologies with hundreds of components.

---
# 🛠 Practice Exercises
**Hands-on tasks or labs:**  
- [ ] Investigate the cost of Application Insights.
	- [ ] Implement tracing for Envelopes.
- [ ] https://learn.microsoft.com/en-us/training/modules/monitor-app-performance/6a-monitor-application-instrumentation
---
# 📚 Additional Notes
**Any extra insights, tips, or gotchas:** 