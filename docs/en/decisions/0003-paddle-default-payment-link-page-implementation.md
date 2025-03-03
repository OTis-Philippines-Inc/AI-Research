# 5. How to build a default payment link page

Date: 2025-03-03

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

RikaiAI needs to implement a default payment link page that acts as a quick way to open Paddle Checkout for a transaction. It also handles cases where customers need to update their payment information or when payment recovery is needed. The default payment link serves as a fallback URL that Paddle can redirect customers to when they need to update their payment details or when automatic payment recovery attempts fail.

### Decision

~Decided to implement a separate route implementation at `https://slack-translate.rikaiai.com/checkout` that will serve as the default payment link, handling both new subscriptions and payment updates.~  
The default payment link page will be integrated into the existing checkout page using Paddle.js to minimize development effort while ensuring a seamless user experience.

### Status

Proposed

### Consequences

~Will provide clearer separation of concerns, simpler state management per route, and better align with ongoing backend refactoring efforts, but it will require managing multiple URLs in Paddle's settings.~  
Integrating the default payment link page with an existing checkout page allows for easier implementation and maintenance within current workflows. However, this approach may limit customization options, making it less flexible for unique checkout scenarios. Additionally, ensuring compliance with Paddle’s approved domain requirements remains a consideration for all implementation options.

## Decision Drivers

- **Simple to implement and extend:** The solution should be simple to develop and easy to extend with additional functionality in the future.
- **Future-proof:** The solution should align with the broader architectural direction and support long-term maintainability.

## Considered Options

- ~**Dynamic route implementation:** Implement a dynamic route that handles both new subscriptions and payment updates. In this case, a single route at `/checkout` would be implemented that determines its behavior based on URL parameters (e.g., `status`, `customerId`, `recoveryId`).~
- ~**Separate route implementation:** Implement separate routes for new subscriptions and payment updates. In this case, separate routes would be implemented like (e.g., `/checkout/new` and `/checkout/update`.)~
- **Use an existing checkout page with Paddle.js**: Integrate the payment link functionality into an already established checkout page. Paddle.js is used to automatically open the checkout when a customer accesses the payment link.
- **Create a dedicated payment link page**: Develop a separate page specifically designed for handling payment links. The page would be optimized for a seamless checkout experience while ensuring it meets Paddle's compliance requirements.
- **Dynamically override the payment link per transaction**: In this option, different payment link pages can be used dynamically by specifying a different `checkout.url` per transaction. This allows for a flexible checkout experience tailored to specific customer needs.

## Decision Outcome

~We chose `separate route implementation`  because it provides clearer separation of concerns and simpler state management per route, aligning with the current backend refactoring efforts to separate endpoints for different functionalities.~  
We chose `Use an existing checkout page with Paddle.js`, because it provides the most seamless integration with existing workflows while minimizing additional development work.

## Pros and Cons of the Options

| Option | Pros | Cons |
| --- | --- | --- |
| Use an existing checkout page with Paddle.js | - Easy integration with current workflows <br> - No extra development needed <br> - Ensures compliance with Paddle <br> - Reduces maintenance efforts by leveraging existing infrastructure | - Limited customization options for different checkout scenarios <br> - Requires adherence to the existing checkout page’s design and structure |
| Create a dedicated payment link page | - More control over the user experience <br> - Optimized specifically for payment links <br> - Allows for branding customization and tailored customer journey | - Requires additional development effort <br> - Needs ongoing maintenance and updates to remain compliant <br> - Might cause inconsistencies with other checkout experiences if not properly aligned |
| Dynamically override the payment link per transaction | - Most flexible option to customize checkout per transaction <br> - Can tailor checkout experience based on customer segments <br> - Allows handling of special promotions or discounts dynamically | - Requires additional logic and backend adjustments <br> - More complex to implement and maintain over time <br> - Must ensure all checkout URLs are pre-approved by Paddle |

## Notes

- [Payment Recovery](https://developer.paddle.com/concepts/retain/payment-recovery-dunning) (dunning) is handled by Paddle's Retain feature.
- When a payment fails, Retain can automatically:
  - Retry payments throughout the dunning window and enable Tactical Retries to attempt unsuccessful payments at the best times depending on the customer's location, the type of payment method, and other factors.
  - Send an email that has been optimized for hundreds of thousands of transactions.
  - Pause or cancel subscriptions once all attempts to collect payments have been made.
- Before building the default payment link page, the website hosting must be approved by Paddle. Add the website where your default payment link page is hosted to **Paddle > Checkout > Website approval**.
- To set the default payment link:
  - Go to **Paddle > Checkout > Checkout settings**.
  - Enter your website homepage under the **Default payment link** heading. If you don't have one, enter `https://localhost/`.
  - Click **Save** when you're done.
- This was originally inteded to propose options on how to handle the routing of the default payment link page, but has been revised to focus more on the building of the default payment link page.

## Others

### ADR Template References
- By [Michael Nygard](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)
- By [Jeff Tyree and Art Akerman](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-by-jeff-tyree-and-art-akerman)
- By the [Markdown Any Decision Records (MADR) project](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)
