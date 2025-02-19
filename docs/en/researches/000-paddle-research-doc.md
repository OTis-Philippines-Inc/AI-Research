# 3. Handled with a customized success page

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

### Issue

After a successful checkout transaction within Rikai AI, clients should receive a clear confirmation of their purchase. To enhance simplicity, convenience, and visual appeal, we propose a customized success page that provides a seamless and engaging post-checkout experience.

### Decision

Decision on implementing a customized success page.

### Status

### Consequences

By having to developed additional web page for Rikai AI, it will introduce additional steps to planning, designing, developing, and QA testing for the given web page.

## Decision Drivers

- **Development flexibility:** Creating a custom web page allows developers to modify and iterate on the design, accommodating both simple and complex requirements. This provides greater flexibility compared to relying on default designs.
- **Convenience to customers:** While email confirmations are possible, they are not ideal or efficient. Sensitive data should be handled securely, and a confirmation web page provides a more immediate and user-friendly solution.
- **Balancing control & minimalist:** While increased control can introduce complexity. Rikai AI as a product does not require a complex workflow to be used as confirmation purposes. By customizing, a customized web page allows for potential future scalability without unnecessary complications.

## Considered Options

- **Default Paddle Success Page:** Notifies the customer of their transaction via page and email of their order details.
- **Customized Success Page:** Redirects the customer after successful transaction to whatever data-success-url is set in HTML or the `Paddle.Checkout.open()` attribute called `successUrl` has been setted. It can also be configured during initialization step through process of `eventCallback`.
- **Email Confirmation:** Using email as source of confirmation while having the option of using Webhooks for additional control during email phase. This process skips the success page entirely.
- **Customized Success Workflow:** Maximizing control over the process using Webhooks to automate the post-purchase results like, sending API keys, the emailing of order details, and can add additional processes.

## Decision Outcome

We chose `Customized Success Page`because it allows us to have the flexible choice of displaying contents that we want for the customer while openning the door for more complex designs. While the default option maybe capable enought to display the contents that we want, if it so happends that we require more sophisticated design. With the `Customized Success Page`, changes would be least out of the other option.

## Pros and Cons of the Options

| Option | Pros | Cons |
| --- | --- | --- |
| Default Paddle Success Page | - It is the most easiest to implement out of all the options, as it requires no additional contents or configuration.  <br> - Efficient when comes to performance and the ease of use for end users. <br> - It can be appropriate for a quick confirmational result <br>  | - Flexibility is compromised given the limited control over the page that the developer has. <br> - The inability to reformat the design may impact consistency of the website. <br> - Reliance on the Paddle API maintinance. <br>|
| Customized Success Page | - It is quite accessible to developers meaning, less ambiguity. <br> - Preferably to maintain the design aspect for the page. <br> - Flexible to options given any change. <br> - Balances both control and complexity than all other options. <br> | - Additional inclusion to the development life cycle. <br> - The additional process may not be properly utilize as the simplistic naure. <br>|
| Email Confirmation | - Its simple to implement like that of the default page. <br> - The most efficient when comes to performance. <br> | - It is not reliable for notifying customers <br> - It introduce redundancy for non-sensitive date. <br> | 
| Customized Success Workflow | - It gives full control to the maintainer <br> - It completely removes ambiguity for the workflow <br> - It introduces automation of different process <br> | - It is very difficult to maintain and human error could leaked in. <br> - It is often unecessary and introduced unecessary risk. <br> - It is the most difficult to implement compare to all other options.

## Notes

## Others

### ADR Template References
- By [Michael Nygard](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)
- By [Jeff Tyree and Art Akerman](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-by-jeff-tyree-and-art-akerman)
- By the [Markdown Any Decision Records (MADR) project](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)

