# 4. Handled success page with customization

Date: 2025-02-18 

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

ADR Owner: Isiah Jordan Dimaunahan

Stakeholders:

## Summary

- AI core team

### Issue

After a successful checkout transaction within Rikai AI, clients should receive a clear confirmation of their purchase. To enhance simplicity, convenience, and visual appeal, we propose a customized success page that provides a seamless and engaging post-checkout experience.

### Decision

Decision on creating a web page to accommadate customers succesful transaction to then be routed using `successUrl` for the intended webpage that confirms the subscription rights and the plan aggreement details.

### Status

Proposed

### Consequences

By having to developed additional web page for Rikai AI, it will introduce additional steps to planning, designing, developing, and QA testing for the given web page.

## Decision Drivers

- **Development flexibility:** Creating a custom web page allows developers to modify and iterate on the design, accommodating both simple and complex requirements. This provides greater flexibility compared to relying on default design choices.
- **Convenience to customers:** While email confirmations are possible, they are not ideal and inapproriate for alerting customers subscription outcome. Sensitive data should be handled securely, and a confirmation web page provides a more immediate and user-friendly solution.
- **Balancing control & minimalist:** While increased control can introduce complexity. Rikai AI as a product does not require a complex workflow to be used as confirmation purposes. By customizing, a customized web page allows for potential future scalability without unnecessary complications.

## Considered Options

- **Default paddle success page:** Notifies the customer of their transaction via page and email of their order details.
- **Customized success page:** Redirects the customer after successful transaction to whatever data-success-url is set in HTML or the `Paddle.Checkout.open()` attribute called `successUrl` has been setted. It can also be configured during initialization step through process of `eventCallback`.
- **Email confirmation:** Using email as source of confirmation while having the option of using `Webhooks` for additional control during email phase. This process skips the success page entirely through routing back to main page or closure of the checkout.
- **Customized success workflow:** Maximizing control over the process using `Webhooks` to automate the post-purchase results like, sending API keys, the emailing of order details, and can add additional processes.

## Decision Outcome

We chose `Customized Success Page`because it allows us to have the flexible choice of displaying contents that we want for the customer while openning the door for more complex designs. While the default option maybe capable enought to display the contents that we want, if it so happends that we require more sophisticated design. With the `Customized Success Page`, changes would be least out of the other option.

## Pros and Cons of the Options

| **Option** | **Pros** | **Cons** |  
|------------|---------|---------|  
| **Default paddle success page** | - The easiest option to implement, requiring no additional content or configuration. <br> - Efficient in terms of performance and ease of use for end users. <br> - Suitable for providing a quick confirmation result. <br> | - Limited flexibility due to restricted control over the page. <br> - Inability to customize the design may impact website consistency. <br> |  
| **Customized success page** | - Easily accessible to developers, reducing ambiguity. <br> - Allows greater control over the confirmation details provided to the customer. <br> - Acts as a middle ground between a simple notification and a fully customized workflow via `Webhooks`. <br> - While not the easiest option, it is still relatively simple to integrate by adding a `successUrl` argument. <br> | - Adds an extra step to the development process. <br> - May not always be fully utilized due to its relatively simple nature. <br> |  
| **Email confirmation** | - Simple to implement, similar to the default success page. <br> - The most efficient option in terms of performance. <br> | - Not always reliable for notifying customers. <br> - Introduces redundancy for non-sensitive data. <br> |  
| **Customized success workflow** | - Provides full control to the maintainer. <br> - Eliminates ambiguity in the workflow. <br> - Enables automation of various processes, allowing for seamless pipeline integration. <br> | - Often unnecessary if only simple confirmation is required, introducing unnecessary complexity and risk. <br> - The most difficult option to implement compared to others. <br> - May introduce redundancy that outweighs the benefits of increased control. <br> |  


## Notes

- Each option provided is interconnected and often built in conjunction with others. For example, email confirmation is automatically handled by the Paddle checkout and invoice but can be added separately in cases where exclusion from the web page is chosen. In such cases, additional steps would be required to include confirmation with the email billing details.

## Others

### ADR Template References
- By [Michael Nygard](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)
- By [Jeff Tyree and Art Akerman](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-by-jeff-tyree-and-art-akerman)
- By the [Markdown Any Decision Records (MADR) project](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)

