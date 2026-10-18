# Stakeholder readout: Voice of Customer triage prototype

## Decision question

Could a language model help a B2B SaaS team create a consistent, reviewable first-pass structure for customer feedback, while keeping a person responsible for interpretation and action?

This repository demonstrates a workflow for exploration. It is not a recommendation to automate customer decisions or route real cases without review.

## What was built

- A reproducible dataset of 120 fictional feedback records.
- A Gemini pipeline that classifies comment text into controlled fields, checks response structure and supporting evidence, caches successful results, and can resume after interruption.
- A Streamlit dashboard for feedback themes, sentiment, segments, follow-ups, and separately generated synthetic survey ratings.
- A seeded 30-record review sample and a separate prediction export. Both contain the same feedback IDs so reviewers can compare them after completing the blind worksheet.

## Dashboard preview

[![Dashboard preview showing feedback coverage, CSAT, NPS, and rating distributions](../assets/dashboard-preview.png)](https://llm-systems-framework-5yirlr2uw3lblwswidtkho.streamlit.app/)

**[Open the live interactive dashboard](https://llm-systems-framework-5yirlr2uw3lblwswidtkho.streamlit.app/)**

The image above is a static preview; clicking it opens the live Streamlit dashboard. Both use the bundled synthetic data.

## Demonstration readout

All 120 synthetic records have saved, schema-valid classifications, and the supporting excerpts match their source comments. In this intentionally constructed sample, 20 survey records have separate synthetic ratings: average CSAT is **3.8/5**, top-two-box is **65%**, and NPS is **+20**. These values demonstrate dashboard calculations; they are not observed customer satisfaction or business performance.

All 30 sampled records have sentiment and category labels. Against the initial blind labels, sentiment agreement is **80% accuracy** with **0.407 macro-F1** (three of four sentiment classes represented), and category agreement is **83.3% accuracy** with **0.844 macro-F1** (all ten categories represented). The comparison produced 11 disagreements: six sentiment and five category. All five category disagreements were human `Onboarding` versus Gemini `Documentation` for comments about a setup guide. During post-review, the reviewer judged Gemini's label more appropriate in all 11 cases; these judgments are recorded without replacing the original blind labels. Because this was a single-reviewer assessment made after seeing model output, it should be treated as qualitative adjudication rather than an independent accuracy estimate.

## Interpretation and limits

The dataset is balanced and templated, with repeated scenario language. Its category and sentiment distributions cannot estimate customer prevalence or reveal real product priorities. There is no real-customer impact measurement, manual triage baseline, reviewer-time study, or evidence that this prototype reduces effort or improves decisions. Root-cause fields are hypotheses, not verified explanations.

The dashboard should be read as an analyst exploration surface. A reviewer should open the original comment, verify the quoted evidence, correct the model output where needed, and decide whether any follow-up is appropriate. The prototype has no production access controls, persistent case workflow, or external monitoring.

## Recommendation and next evidence

Keep the workflow in a synthetic-data demonstration state. Before a real pilot, define privacy and retention controls, the triage decision and taxonomy owners, escalation rules for high-impact categories, a manual fallback, and rollback thresholds. Then compare against the current process using a representative human-labeled sample with independent reviewers, sufficient class coverage, and measured reviewer effort. Report error rates and uncertainty by class and segment before drawing any operational conclusion.

For the business hypothesis and operating risks, see the [business case](business_case.md). For the blind-labeling and metric definitions, see the [evaluation protocol](../data/evaluation/README.md).
