# 16. Language detectors with language whitelisting capabilities

Date: March 9, 2025

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

ADR Owner: Kenneth Brian Pine

Stakeholders:
- AI core team

## Summary

### Issue

Polyglot is a popular language detection tool that supports over 165 languages, but it does not allow strict whitelisting, meaning it may still detect unwanted languages. Rust-based alternatives like Lingua-RS, Whichlang, and Whatlang-RS offer better performance and integration for Rust applications, but they differ in accuracy and filtering capabilities. The goal is to identify the most suitable tool for enforcing strict language whitelisting while maintaining efficiency and reliability.


### Decision

Since Polyglot lacks built-in whitelisting, it is not ideal for scenarios requiring strict control over detected languages. Lingua-RS is the best Rust-based alternative due to its high accuracy and native whitelisting support. Whichlang and Whatlang-RS are faster and more lightweight but do not provide built-in whitelisting, requiring additional filtering to limit detected languages.


### Status

Proposed

### Consequences

Choosing Polyglot would require additional manual filtering, which could add complexity and slow down processing. Lingua-RS ensures only whitelisted languages are detected but has a larger model size, which may affect performance. Whichlang and Whatlang-RS offer faster, lightweight solutions but lack built-in whitelisting, requiring extra steps to filter out unwanted languages.

## Decision Drivers

- **Strict whitelisting:** Is the top priority, making Lingua-RS the best choice.
- **Accuracy:** Is important, with Lingua-RS outperforming other options in precision.
- **Performance and speed:** Matter, with Whichlang and Whatlang-RS being the fastest.
- **Language coverage:** Is a factor, with Polyglot supporting the most languages but lacking strict whitelisting.

## Considered Options

- **Polyglot:** A Python-based tool with broad language support but no strict whitelisting.
- **Lingua-RS:** A Rust-based tool with high accuracy and built-in whitelisting.
- **Whichlang:**  A lightweight Rust detector with good speed and accuracy but no whitelisting.
- **Whatlang-RS:** The fastest and most lightweight option but lacks strict whitelisting.

## Decision Outcome

Lingua-RS is the best option for strict whitelisting as it accurately detects only approved languages. Polyglot supports many languages but lacks built-in whitelisting, requiring additional filtering. Whichlang and Whatlang-RS are lightweight and fast but do not natively enforce strict whitelisting. If accuracy and control are the priority, Lingua-RS is the best choice, while Whichlang and Whatlang-RS are better for speed, and Polyglot is ideal for broad language detection without filtering.

## Pros and Cons of the Options

| Option | Pros | Cons |
| --- | --- | --- |
| **Polyglot** | - Supports 165+ languages <br>- High accuracy with machine learning <br>- Performs well on short texts | - No strict whitelisting <br>- Python dependency <br>- Slower than Rust alternatives<br> |
| **Lingua-RS** | - Most accurate Rust option <br>- Strict whitelisting supported <br>- Works well with short texts | - Larger model size <br>- More complex setup<br> |
| **Whichlang** | - Fast and simple <br>- Balanced speed and accuracy <br>- Rust-native | - Lower accuracy than Lingua-RS <br>-  No built-in whitelisting<br> |
| **Whatlang-RS** | - Lightweight and fast <br>- Easy Rust integration<br> | -  Lower accuracy for short texts <br>- No strict whitelisting<br> |

## Notes

- For strict whitelisting, Lingua-RS is the best option as it guarantees that only selected languages are detected. Whichlang and Whatlang-RS are preferable for lightweight and fast processing but require additional filtering to enforce whitelisting. Polyglot is the best choice for multilingual coverage but lacks strict whitelisting, making it unsuitable for cases where limiting detection to specific languages is essential.


## Others

 - *References*<br>[polyglot GitHub Repository](https://github.com/aboSamoor/polyglot/blob/master/docs/Detection.rst)<br>

### ADR Template References
- By [Michael Nygard](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)
- By [Jeff Tyree and Art Akerman](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-by-jeff-tyree-and-art-akerman)
- By the [Markdown Any Decision Records (MADR) project](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)
