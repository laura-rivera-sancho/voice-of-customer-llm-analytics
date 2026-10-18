# Customer Conversation Intelligence

![Abstract teal and navy banner showing customer feedback flowing into reviewable insights](assets/repository-banner.png)

[![Repository quality](https://github.com/laura-rivera-sancho/voice-of-customer-llm-analytics/actions/workflows/ci.yml/badge.svg)](https://github.com/laura-rivera-sancho/voice-of-customer-llm-analytics/actions/workflows/ci.yml)

[Open the live dashboard](https://voice-of-customer-llm-analytics.streamlit.app/) · [Read the executive summary](docs/stakeholder_readout.md) · [Review the pilot assumptions](docs/business_case.md) · [Contact Laura](mailto:laura.riverasancho33@gmail.com)

A working reference implementation for turning high-volume customer conversations into reviewable themes, evidence-supported issue signals, and prioritized follow-up. It is designed for customer-experience, product, support, and operations teams that need to decide which recurring problems deserve investigation or action.

## The decision this supports

Which customer issues are recurring, where are they concentrated, what evidence supports each signal, and is an assisted review workflow accurate and useful enough to continue?

Model output is treated as evidence for a reviewer—not as an automated customer decision. Every classified record retains a verbatim supporting excerpt and can be corrected or escalated.

## Pilot at a glance

| Item | Typical scope |
|---|---|
| **Duration** | 3–5 weeks |
| **Inputs** | A representative, appropriately de-identified feedback sample; current taxonomy or routing rules; existing review process; subject-matter reviewers; privacy and retention constraints |
| **Week 1** | Confirm the decision, allowed uses, taxonomy, baseline, access controls, and evaluation plan |
| **Weeks 2–3** | Configure the classification workflow, validate evidence, and review category-level errors with human reviewers |
| **Weeks 4–5** | Deliver the dashboard, operating guidance, executive readout, and go / iterate / stop recommendation |
| **Buyer receives** | Decision contract, taxonomy, reproducible workflow, human-evaluation results, dashboard, review playbook, and executive recommendation |
| **Client participation** | Decision owner, data owner, and subject-matter reviewers available for taxonomy and evaluation decisions |
| **Not included** | Unreviewed automated routing, sensitive-data processing without approved controls, production authentication, enterprise integration, or long-term monitoring |

Final timing depends on data readiness, access requirements, reviewer availability, and the level of operational integration required.

## What a successful pilot demonstrates

Acceptance thresholds should be agreed after the data-readiness review. At minimum, the pilot should show:

- complete reconciliation between supplied records and reported outputs;
- traceable source evidence for every output intended to inform review;
- quality reported by important category, including ambiguous cases—not only an overall score;
- visible correction and escalation paths;
- comparison with the current process on reviewer effort or decision usefulness; and
- a clear go, iterate, or stop recommendation.

## What is available in this repository

| Evidence | Start here | What it shows |
|---|---|---|
| Live experience | [Streamlit dashboard](https://voice-of-customer-llm-analytics.streamlit.app/) | Reviewable themes, sentiment, segments, survey measures, and follow-up signals |
| Executive communication | [Stakeholder readout](docs/stakeholder_readout.md) | Findings, limitations, operational implications, and recommended next evidence |
| Pilot framing | [Business case](docs/business_case.md) | Decision context, value hypothesis, controls, and evidence required before real use |
| Evaluation | [Human-review guide and sample](data/evaluation/README.md) | Blind review design, category boundaries, disagreements, and recalculated metrics |
| Technical implementation | [Pipeline source](src) and [tests](tests) | Structured outputs, evidence checks, caching, retries, validation, and reproducibility |
| Delivery status | [Roadmap](ROADMAP.md) | Implemented capabilities and remaining production-readiness work |

## Demonstration boundary

The included organization, feedback, survey scores, action tracker, and findings are fictional or synthetic. The implementation demonstrates workflow behavior, technical controls, evaluation mechanics, and stakeholder communication; it does not claim customer impact, operational savings, or production model quality.

A real pilot would use representative, approved data and would define category-level quality thresholds, reviewer effort, escalation performance, privacy controls, and decision usefulness before launch.

## How an engagement would start

1. Identify the decision, current review process, available data, and decision owner.
2. Review a schema or de-identified sample and agree the permitted data boundary.
3. Confirm the written scope, evaluation thresholds, responsibilities, timeline, exclusions, and stop conditions.
4. Begin the pilot only after access, privacy, ownership, and review expectations are agreed.

For an initial scope discussion, [email Laura](mailto:laura.riverasancho33@gmail.com) with the decision you need to make, the available data or systems, and the target timeline.

