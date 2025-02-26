# 5. How to build a default payment link page

Date: 2025-02-26

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

ADR Owner: Victor Caro

Stakeholders:
- AI core team

## Summary

### Issue

RikaiAI needs to implement a default payment link page that acts as a quick way to open Paddle checkout for a transaction. It also handles cases where customers need to update their payment information or when payment recovery is needed. The default payment link serves as a fallback URL that Paddle can redirect customers to when they need to update their payment details or when automatic payment recovery attempts fail.

### Decision

Decided to implement a separate route implementation at `https://slack-translate.rikaiai.com/checkout` that will serve as the default payment link, handling both new subscriptions and payment updates.

### Status

Proposed

### Consequences

Will provide clearer separation of concerns, simpler state management per route, and better align with ongoing backend refactoring efforts, but it will require managing multiple URLs in Paddle's settings.

## Decision Drivers

- **Simple to implement and extend:** The solution should be simple to develop and easy to extend with additional functionality in the future.
- **Future-proof:** The solution should align with the broader architectural direction and support long-term maintainability.

## Considered Options

- **Dynamic route implementation:** Implement a dynamic route that handles both new subscriptions and payment updates. In this case, a single route at `/checkout` would be implemented that determines its behavior based on URL parameters (e.g., `status`, `customerId`, `recoveryId`).
- **Separate route implementation:** Implement separate routes for new subscriptions and payment updates. In this case, separate routes would be implemented like (e.g., `/checkout/new` and `/checkout/update`.)

## Decision Outcome

We chose `separate route implementation`  because it provides clearer separation of concerns and simpler state management per route, aligning with the current backend refactoring efforts to separate endpoints for different functionalities.

## Pros and Cons of the Options

| Option | Pros | Cons |
| --- | --- | --- |
| Dynamic route implementation | - Single entry point for all payment activities.<br>- Simplifies URL management in Paddle settings. | - More complex state management.<br>- Requires careful handling of different scenarios. |
| Separate route implementation | - Clearer separation of concerns.<br>- Simpler state management per route. | - Multiple URLs to manage in Paddle settings.<br>- Requires consistent branding across routes. |

## Notes

- [Payment Recovery](https://developer.paddle.com/concepts/retain/payment-recovery-dunning) (dunning) is handled by Paddle's Retain feature.
- When a payment fails, Retain can automatically:
  - Retry payments throughout the dunning window and enable Tactical Retries to attempt unsuccessful payments at the best times depending on the customer's location, the type of payment method, and other factors.
  - Send an email that has been optimized for hundreds of thousands of transactions.
  - Pause or cancel subscriptions once all attempts to collect payments have been made.

## Others

### ADR Template References
- By [Michael Nygard](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)
- By [Jeff Tyree and Art Akerman](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-by-jeff-tyree-and-art-akerman)
- By the [Markdown Any Decision Records (MADR) project](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)
