# 7. Paddle Notifications Integration

Date: 2025-02-19

## Contents

- [Summary](#summary)
  - [Issue](#issue)
  - [Decision](#decision)
  - [Status](#status)
  - [Consequences](#consequences)
- [Decision Drivers](#decision-drivers)
- [Considered Options](#considered-options)
- [Decision Outcome](#decision-outcome)
- [Pros and Cons of the Options](#pros-and-cons-of-the-options)
- [Notes](#notes)
- [Others](#others)
  - [ADR Template References](#adr-template-references)

ADR Owner: **Raphael Angelo Nepomuceno**

Stakeholders:
- AI core team

## Summary

### Issue

Currently, notifications from Paddle are assued to be used only for synchronizing internal database with Paddle's database. We want to find the best way to implement this synchronization, find relevant conventions, and any other potential uses that might be overlooked. 

### Decision

Decided to implement a Hybrid Approach, combining the use of webhooks, for real-time updates, and polling, as a fallback mechanism. 

### Status

Proposed

### Consequences

- Ensures the internal database remains consistent with Paddle's record
- Potentially unlocks new use cases such as analytics or automated responses.
- Reduces reliance on a single method, improving reliability and data integrity.
- Provides an opportunity to standardize webhook handling conventions, such as idempotency, security validation, and error handling.
- Implementing additional use cases may introduce problems such as latency or processing overhead or additional computational burden, depending on the implementation. 
- Introduces some complexity in implementation and additional API calls due to polling.

## Decision Drivers

- Need for an accurate and up-to-date synchronization with Paddle.
- Potential for additional use cases from notifications such as system monitoring and automated billing alerts.
- Performance considerations for processing notifications.
- Compliance with Paddle’s best practices.
- Prevention of data loss in case of system/API failures.

## Considered Options

- **Webhook Listener**: Implement a webhook listener for Paddle notifications and update the internal database accordingly.
- **Periodic Polling**: Periodically poll Paddle’s API for changes instead of relying on notifications.
- **Hybrid Approach**: Leverage webhooks for immediate updates and periodic polling as a fallback mechanism with ease using Merge for example. 

## Decision Outcome

We chose **Hybrid Approach** because it eliminates the negative consequences of the two other options, offering a real time updates and a fallback mechanism in case the registered webhook is down, improving reliability and data integrity. Platforms like **MERGE**, lets us easily configure webhooks and polling across integrations and drastically simplifies authentication, and other related integration tasks. [MERGE](https://www.merge.dev/blog/webhooks-vs-polling)

## Pros and Cons of the Options

| Option | Pros | Cons |
| --- | --- | --- |
| **Webhook Listener** | - Real-time updates <br> - Minimal API calls <br> - Enables event-driven automation <br>| - Requires handling failures or missing notifications<br>|
| **Periodic Polling** | - Control over data retrieval <br> - No dependency on webhook reliability<br> | - More API calls increases overload <br> - No real time updates or delayed synchronization <br> |
| **Hybrid Approach** | - Ensures real time synchronization and offer a fallback mechanism <br> - Improves data reliability <br>| - More complex implementation <br> |

## Notes

- Webhooks should be secured to prevent unauthorized access.
- Periodic polling should be optimized to minized unecessary API calls.
- Implementing an idempotency mechanism will ensure duplicate notifications do not create inconsistencies in the database.

## Others

### ADR Template References
- By [Michael Nygard](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)
- By [Jeff Tyree and Art Akerman](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-by-jeff-tyree-and-art-akerman)
- By the [Markdown Any Decision Records (MADR) project](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)
