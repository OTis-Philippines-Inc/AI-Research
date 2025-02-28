# 6. User Payment Information Management in Paddle

Date: 2025-02-27

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

ADR Owner: John Andrei C. Cabili

Stakeholders:
- AI Core Team

## Summary

### Issue

Workspace owners and admins need a seamless and secure way to manage their payment information for RikaiAI through Paddle. The current challenge is ensuring:
- Secure and controlled access to payment information.
- Multi-user accessibility for updating payment information.
- RikaiAI's Slack frontend does not have direct access to sensitive payment data.

### Decision

We will proceed with **Full Paddle Customer Portal Integration**, directing users to Paddle’s self-service portal for all payment management tasks. This approach ensures that all sensitive financial operations remain within Paddle’s secure ecosystem, reducing compliance risks while using Paddle’s built-in authorization and recovery mechanisms.

### Status

Proposed

### Consequences

- Ensures full compliance with Paddle’s security and compliance requirements.
- Eliminates the need for RikaiAI to handle payment-related operations, reducing liability and implementation complexity.
- Provides a reliable and standardized way to manage payments without introducing API-layer dependencies within RikaiAI.
- Users may need to leave Slack for payment updates, but this maintains a clear separation of concerns between RikaiAI and Paddle.

## Decision Drivers

- **Security and Compliance:** All payment operations remain within Paddle’s secure environment, ensuring compliance with financial regulations.
- **Maintainability:** Reduces long-term development and operational overhead by avoiding custom integrations with Paddle’s API.
- **Reliability:** Avoids API-layer dependencies, ensuring that billing and payment processes remain fully functional regardless of RikaiAI’s infrastructure.
- **User Convenience:** Provides a direct and supported way to manage payments with Paddle’s existing UI.
- **Implementation Efficiency:** Uses Paddle’s existing self-service portal, minimizing the need for additional backend or frontend development.

## Considered Options

- **Full Paddle Customer Portal Integration:** Redirect users to Paddle’s customer portal for all payment management tasks.
- **Paddle API Proxy with Slack UI:** Use Paddle’s API to fetch and update payment details securely while providing a Slack-based UI for user actions.
- **Internal Payment Management:** Store and manage payment details within RikaiAI, allowing full control but adding security risks.
- **Manage Payment Details in Paddle through the Slack Frontend:** The Slack frontend queries Paddle and displays the information, but all management actions are still handled in Paddle. This provides a more native Slack experience while maintaining Paddle as the system of record.

## Decision Outcome

We chose `Full Paddle Customer Portal Integration` because it ensures a secure, compliant, and low-maintenance approach to payment management. By using Paddle’s existing self-service portal, RikaiAI avoids handling financial data while benefiting from Paddle’s built-in authentication, authorization, and multi-user access recovery. This approach eliminates the need for additional API-layer dependencies and reduces the risk of payment-related issues within RikaiAI’s infrastructure.

## Pros and Cons of the Options

| Option | Pros | Cons |
| --- | --- | --- |
| **Full Paddle Customer Portal Integration** | - Ensures full compliance with Paddle’s security model.<br>- Eliminates API dependencies for payment management.<br>- Reduces long-term maintenance and security risks.<br>- Uses Paddle’s existing infrastructure for multi-user access and recovery. | - Requires users to leave Slack for payment updates.<br>- Limited ability to provide proactive notifications within Slack. |
| **Paddle API Proxy with Slack UI** | - Provides a seamless user experience within Slack.<br>- Allows controlled access to payment features without storing data.<br>- Enables future enhancements like notifications for billing issues.<br>- Reduces dependency on Paddle’s UI limitations. | - Requires moderate development effort.<br>- Relies on Paddle API stability.<br>- Must implement caching/fallback handling for API failures. |
| **Manage Payment Details in Paddle through the Slack Frontend** | - Provides a native Slack experience.<br>- Keeps Paddle as the backend of record.<br>- Reduces security risks by avoiding direct financial data handling. | - Still requires some API integration.<br>- Limited to what Paddle’s API allows for external UIs.<br>- Adds complexity without significant compliance or security benefits over Full Paddle Portal Integration. |
| **Internal Payment Management** | - Provides full control over UI and workflows.<br>- No reliance on Paddle’s UI constraints. | - High security and compliance risks.<br>- Significant development effort.<br>- Increases liability for handling financial data. |

## Notes

- Paddle provides a self-service portal that supports multiple authorized users managing payment details, addressing the issue of inactive workspace owners.
- Additional considerations may be needed for access recovery in cases where all authorized users become inactive.
- Paddle’s webhooks can be used to notify RikaiAI about subscription status changes, allowing the system to react accordingly, such as sending Slack notifications for failed payments or upcoming renewals.

## Others

### ADR Template References
- By [Michael Nygard](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)
- By [Jeff Tyree and Art Akerman](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-by-jeff-tyree-and-art-akerman)
- By the [Markdown Any Decision Records (MADR) project](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)
