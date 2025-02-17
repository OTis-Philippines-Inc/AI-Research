# 2. Switch to hybrid architecture

Date: 2024-01-19

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

ADR Owner: Kyle Aquino

Stakeholders:
- AI core team

## Summary

### Issue

All components of HoshicoAI, which include the bakcend server, have varying hardware requirements and usage patterns. To enable horizontal scaling and flexibility in deployment infrastructure while minimizing costs, we propose introducing microservices into the system and to switch to a hybrid architecture.

### Decision

Decided in favor of switching to a hybrid architecture.

### Status

Accepted

### Consequences

Horizontal scaling will be much more feasible, but this will introduce more complexity to the deployment process and any sort of automation and monitoring.

## Decision Drivers

- **Scalability requirements:** Each component of HoshicoAI has to scale differently and independently to meet demand. A single backend server instance can handles hundreds of requests per second, but an ASR server instance has to be scaled dozens of times to meet the same demand.
- **Deployment flexibility:** Each component of HoshicoAI has different hardware requirements. For example, the ASR server requires a GPU to run efficiently, while the backend server can run on a CPU.
- **Minimizing latency:** While a pure microservices architecture will meet the above requirements, it will introduce a lot of latency due to the need to communicate between different servers. For some processes that can only be done server-side (e.g. text embedding), but does not require a lot of resources (e.g., user queries), it is better to keep it integrated with the backend server.

## Considered Options

- **Hybrid architecture:** A combination of the monolithic architecture and microservices architecture. In this case, the backend server and text embedding model will be kept combined in a single application, while all other components (e.g., ASR) will be maintained and deployed separately.
- **Microservices architecture:** Where each component of the system is/can be deployed and maintained separately. In this case, each component of HoshicoAI will be deployed and maintained separately, including the text embedding model.
- **Monolithic architecture:** Where all components of the system are combined into a singe application and are maintained and deployed as one.

## Decision Outcome

We chose `hybrid architecture` because it allows us to meet all of our decision drivers, and serves as a good middle ground between the scalability and flexibility of `microservices architecture` and the minimal latency in `monolithic architecture`.

## Pros and Cons of the Options

| Option | Pros | Cons |
| --- | --- | --- |
| Hybrid architecture | - It is the second most scalable option here.<br>- It is arguably the most flexible option, as services can be combined or separated depending on the use case and circumstance.<br>- It has less latency than a full microservices architecture. | - It is more complex and harder to automate than monolithic architecture.<br>- Which services should be combined or separated would be another point of contention. |
| Microservices architecture | - It is the most scalable option here.<br>- Each component can be deployed completely independent from one another.<br>- All components of HoshicoAI can also be utilized by other projects (especially text embedding). | - It is the most complex and hardest to automate option here.<br>- It tends to introduce latency needlessly (especially for text embedding). |
| Monolithic architecture | - It is the least complex and easiest to automate option here.<br>- It has the least latency of all options here. | - It is the least scalable option here.<br>- It is the least flexible option here. |

## Notes

- This was originally intended to propose adopting a microservices architecture, but has been revised to propose a hybrid architecture instead. No records of the original proposal were kept as this record was not finalized at the time.

## Others

### ADR Template References
- By [Michael Nygard](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)
- By [Jeff Tyree and Art Akerman](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-by-jeff-tyree-and-art-akerman)
- By the [Markdown Any Decision Records (MADR) project](https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates/decision-record-template-of-the-madr-project)
