# 5. How to build a default payment link page

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

ADR Owner: Victor Caro

Stakeholders:
- AI core team

## Summary

### Issue

RikaiAI needs to implement a default payment link page that handles cases where customers need to update their payment information or when payment recovery is needed. The default payment link serves as a fallback URL that Paddle can redirect customers to when they need to update their payment details or when automatic payment recovery attempts fail.

### Decision

Decided to implement a dynamic route at `https://slack-translate.rikaiai.com/checkout` that will serve as the default payment link, handling both new subscriptions and payment updates.

### Status

Proposed

### Consequences

Will provide a consistent entry point for all payment-related activities, but requires more careful state management to handle different entry scenarios (new subscriptions vs payment updates).

## Decision Drivers

- **Payment recovery:** Need to provide a reliable way for customers to update payment information when automatic recovery fails.
- **State management:** Need to handle different entry scenarios and customer states.
- **System integration:** Need to integrate with Paddle's payment recovery system and retain features.

## Considered Options

- **Dynamic route implementation:** Implement a dynamic route that handles both new subscriptions and payment updates. In this case, a single route at `/checkout` would be implemented that determines its behavior based on URL parameters (e.g., `status`, `customerId`, `recoveryId`).
- **Separate route implementation:** Implement separate routes for new subscriptions and payment updates. In this case, separate routes would be implemented like `/checkout/new` and `/checkout/update`.
- **Paddle-hosted recovery:** Use Paddle's hosted payment update page instead of a custom solution, relying entirely on Paddle's default hosted pages for payment updates and recovery scenarios and only implementing our custom page for new subscriptions.

## Decision Outcome

We chose `dynamic route implementation` because it allows us to meet all of our decision drivers, and serves as a good middle ground between the ease of maintenance of `paddle-hosted recovery` and the control and customization in `separate route implementation`.

## Pros and Cons of the Options

| Option | Pros | Cons |
| --- | --- | --- |
| Dynamic route implementation | - It is arguably the most flexible option, as it centralizes all payment-related logic in one place.<br>- Simplifies URL management in Paddle. | - Requires more careful state management than Paddle-hosted solution.<br>- Needs more thorough testing across multiple scenarios. |
| Separate route implementation | - It is the most customizable option here.<br>- Allows for specialized handling of each payment scenario. | - It is the most complex to maintain option here.<br>- Leads to code duplication between routes. |
| Paddle-hosted recovery | - It is the least complex to maintain option here.<br>- Automatically receives security udpates from Paddle.<br>- Has built-in error handling for common payment scenarios. | - It is the least customizable option here.<br>- Difficult to add custom validation or business logic. |

## Notes

## Others

### ADR Template References
- By [Michael Nygard](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)
- By [Jeff Tyree and Art Akerman](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-by-jeff-tyree-and-art-akerman)
- By the [Markdown Any Decision Records (MADR) project](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)
