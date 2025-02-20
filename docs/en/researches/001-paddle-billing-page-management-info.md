# 6. User Payment Information Management in Paddle

Date: 2025-02-20

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

ADR Owner: [Developer Name]

Stakeholders:
- AI Core Team
- Security Compliance Team

## Summary

### Issue

Workspace owners and admins need a seamless and secure way to manage their payment information for RikaiAI through Paddle. The current challenge is ensuring:
- Secure and controlled access to payment information.
- Multi-user accessibility for updating payment information.
- RikaiAI's Slack frontend does not have direct access to sensitive payment data.

### Decision

We will implement an integrated **Paddle API proxy solution** that enables workspace owners and admins to securely manage payment details from within Slack while still leveraging Paddle’s infrastructure. Instead of fully relying on the Paddle customer portal, RikaiAI will provide a lightweight UI inside Slack that facilitates common actions such as viewing billing status, updating payment methods, and accessing invoices through secure API calls to Paddle.

### Status

Proposed

### Consequences

- Users can manage payment details directly within Slack, improving user experience.
- RikaiAI does not store payment data, ensuring security and compliance.
- Reduces manual steps by allowing API-based interactions for essential billing actions.
- Dependence on Paddle API stability and service availability remains but is mitigated by local caching and proactive failure handling.

## Decision Drivers

- **Security and Compliance:** No direct handling or storage of payment data within RikaiAI.
- **User Convenience:** Ensures workspace owners/admins can manage payments without leaving Slack while still maintaining security.
- **Scalability:** Provides a flexible foundation for future billing automation or notifications.
- **Implementation Complexity:** Balances a minimal in-app integration with reliance on Paddle’s existing infrastructure.
- **Reliability:** Minimizes reliance on external UI while still leveraging Paddle for secure transactions.

## Considered Options

- **Paddle API Proxy with Slack UI:** Use Paddle’s API to fetch and update payment details securely while providing a Slack-based UI for user actions.

- **Full Paddle Customer Portal Integration:** Redirect users to Paddle’s customer portal for all payment management tasks.

- **Internal Payment Management:** Store and manage payment details within RikaiAI, allowing full control but adding security risks.

## Decision Outcome

We chose `Paddle API Proxy with Slack UI` because it enables direct access to payment management within Slack while keeping RikaiAI’s backend free of sensitive financial data. This approach provides flexibility for automation and billing insights, ensuring a balance between user convenience, security, and compliance.


## Pros and Cons of the Options

| Option | Pros | Cons |
| --- | --- | --- |
| **Paddle API Proxy with Slack UI** | - Provides a seamless user experience within Slack.<br>- Allows controlled access to payment features without storing data.<br>- Enables future enhancements like notifications for billing issues.<br>- Reduces dependency on Paddle’s UI limitations. | - Requires moderate development effort.<br>- Relies on Paddle API stability.<br>- Must implement caching/fallback handling for API failures. |
| **Full Paddle Customer Portal Integration** | - No development effort required for UI.<br>- Ensures full compliance with Paddle’s security model.<br>- Lowers risk of API failures affecting user actions. | - Requires users to leave Slack for payment updates.<br>- No control over user experience.<br>- Limited ability to provide proactive notifications. |
| **Internal Payment Management** | - Provides full control over UI and workflows.<br>- No reliance on Paddle’s UI constraints. | - High security and compliance risks.<br>- Significant development effort.<br>- Increases liability for handling financial data. |

## Notes

- Paddle provides a self-service portal that supports multiple authorized users managing payment details, addressing the issue of inactive workspace owners.
- Additional considerations may be needed for access recovery in cases where all authorized users become inactive.

## Others

### ADR Template References
- By [Michael Nygard](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)
- By [Jeff Tyree and Art Akerman](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-by-jeff-tyree-and-art-akerman)
- By the [Markdown Any Decision Records (MADR) project](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)

