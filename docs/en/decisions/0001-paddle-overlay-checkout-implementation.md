# 3. Implementing Overlay Checkout

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
  - [Positive Consequences](#positive-consequences)
  - [Negative Consequences](#negative-consequences)
- [Pros and Cons of the Options](#pros-and-cons-of-the-options)
- [Notes](#notes)
- [Others](#others)
  - [ADR Template References](#adr-template-references)

ADR Owner: Isiah Jordan Dimaunahan

Stakeholders:
- AI core team

## Summary

### Issue

Customers who have chosen a subscription plan for Rakai AI will need to provide their details. For this request, a checkout UI is required and should be integrated to accept user input. The Paddle API offers a checkout feature that enables quick implementation through an overlay method in which we proposed the implementation steps.

### Decision

Final decisions are to implement the overlay checkout through `Javascript`, by setting the default payment link first via the Paddle.com webiste. After that, taking the `https://cdn.paddle.com/paddle/v2/paddle.js` URL and including it using `<script>` tag. We initialize paddle by generate a token side client in the Paddle dashboard and call on the method `Paddle.Checkout.open()` within JS, which several arguments presented as an object can be toggle or set like: `successUrl`, `theme`, `settings`, and many more. An important setting that is needed is the `displayMode`. To set the checkout as a proper overlay, the 'displayMode: 'overlay'' would be instagated within the execution. Another important argument is the item list. From the dashboard, product needs to be generated with the price and subcription plan in inclusion. A token would be generated per subscription plan in price that would be passed as `items` argument with a quantity of 1. This would be executed through a click event in a pricing page.

### Status

Proposed

### Consequences

Quick integration is a benifit of using overlay checkout, but in exchange for fast integration, flexibility has to be compromised to do so.

## Decision Drivers

- **Simple to Implement:** The process requires only the Paddle dashboard and then the URL for the API module. While during integration, initializing then executing the `Paddle.Checkout.open` method are the only steps in minimum required to run an overlay within the website. As for the dashboard, a product with price and subscription created is needed with the client token and the default permanent link set to your website. 
- **Most Flexible Option:** Developing in JS for the Paddle API yields all the feature provided by Paddle, giving all access to checkouts, events, notification, or even customized workflow. 
- **Dynamic Features:** Since events are provided, a callback mechanism can distinguish different states of the billing process. This introduced customizeable pipeline for the payment and the subscription plan access.
- **Organize Workflow:** In comparison to options taken, it's more proper to collect the logic of the Paddle process in a single location within thet codebase. This is contrary for using `HTML` data attribute with other programming languages, that may not support the Paddle API to the full extent. 

## Considered Options

**Implementing using JS:** Using `Javascript` to instantiate the Paddle API to a website and call in the overlay checkout. It is what the Paddle documentation uses often and the entire process can be integrable to a single JS process with dynamic features.
**Implementing using HTML:** While `Javascript` can be used, Paddle API introduces data attributes via the tag `<a href="#">` would be used as a button that calls for the overlay checkout.
**Prefill Customer Information using Account Details:** It is provided by the API that we can automate the fill out process for the customer, with confirmation and account details provided. The repetative process of fill out can be removed and the UI for  overlay excluded from the process. It may require a customized page for some of the processes like confirmation or additional entry for payment method. The option yields the most convenient for the customer.

## Decision Outcome

We chose to integrate the API via the `Javascript` programming language, this allows a fast integration with the most flexible option. Unlike `HTML` data attributes, it allows for `eventCallback` to be used to monitor states of the workflows and especially, it is best when comes to easy implemention with a dynamic process through the JS with minimal effort.

## Pros and Cons of the Options

| Option | Pros | Cons |
| --- | --- | --- |
| **Implementing using JS** | - It is more flexible and dynamic than the `HTML` approach, with the tools that `Javascript` avails for the developers. <br> - It organize logical components, APIs, or backend features appropriately to a programming language as suppose to a markup language. <br> - While being flexible, the Paddlejs API provides many different features not accessible to `HTML` like events handling. <br> | - If the checkout process is the only feature that the development plan requires, it really doesn't need the dynamic tools JS need and thus introduce more complexity than required. <br> |
| **Implementing using HTML** | - The simlpest option compare to others <br> - Using other programming language as backend and accessing the Paddle checkout components can be now easily manipulated during rendering. <br> | - There is redundancy being introduced since not utilizing `Javasccript` may not ideal for most website development. <br> - Restricting the usage of Paddle API due to the several features that are in provision, can only be accessed through JS. <br> - It could clutter the `HTML` code base, inconsistency may occur. |
| **Prefill Customer Information using Account Details** | - It makes the process of filling out convenient to customer based on time <br> - It minimize the subscription plan cycle process and thus, accessibility is a benifit for customers. <br> | - It requires an additional user interface to confirm transaction and update . <br> - It needs to have additional semantics to make sure that the parameters reflect to the user details. <br> |

## Notes

- There many more features that can be set for the overlay checkout. One of them is the `variant` argument to wether set the overlay with the page or a different page all together. This can be in consideration, depending on preference for the frontend team. This feature was left out like many, since the priority of this researcher is to integrate an overlay and thus, note this as a consideration.
- While the prefill is separate, it can still be used alongside the overlay in JS/HTML. The separation is intentional, as the research focuses on implementing an overlay. The third option—excluding the overlay or replacing it with a custom modal—is based on the absence of a UI element, not the prefill feature.

## Others

### ADR Template References
- By [Michael Nygard](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)
- By [Jeff Tyree and Art Akerman](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-by-jeff-tyree-and-art-akerman)
- By the [Markdown Any Decision Records (MADR) project](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)
