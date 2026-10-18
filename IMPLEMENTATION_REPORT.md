# Implementation Report

**Project:** Voice of Customer LLM Analytics
**Updated:** 2026-10-18
**Status:** Full synthetic inference and the 30-record human-review demonstration are complete; representative real-world and multi-reviewer validation remain outside the prototype scope.

## Delivered

- Added a deterministic generator and `data/synthetic/feedback.csv` with 120 fictional feedback records across six sources, three customer segments, five product areas, and ten issue scenarios.
- Implemented a Gemini classification pipeline with structured JSON output, controlled labels, response validation, verbatim evidence checks, input-aware per-record caching, bounded retries, quota handling, and partial result saves.
- Added `data/processed/classifications.json` with successful model outputs for all 120 records. The blind human-review worksheet contains a fixed, balanced 30-record sample; predictions are exported separately to reduce reviewer anchoring.
- Built an offline-first Streamlit dashboard for volume, sentiment, CSAT, NPS, time trends, segments, product areas, priority follow-ups, and an illustrative action tracker. A compact “Demo data” note identifies the dataset without repeating methodology caveats in the dashboard.
- Added a seeded, source/segment-balanced 30-record blind review worksheet that omits survey scores, preserves existing human labels, and keeps model predictions separate; also added labeling instructions, evaluation metrics, disagreement export, evidence audit, and complete-output validator.
- Added a local API usage ledger. Optional environment rates can estimate request cost; no provider pricing is hard-coded.
- Added setup instructions, dependency declarations, `.env.example`, Git ignore rules, and deterministic tests.

## Verification

- Gemini classification: **120/120 records succeeded** using `gemini-3.1-flash-lite`.
- Refreshed synthetic CSAT/NPS score metadata in the saved classification checkpoint; existing comment-based classifications were reused, with no additional Gemini requests.
- Evidence audit: **120 grounded excerpts, 0 missing excerpts, 0 mismatches, 0 classification errors**.
- Synthetic survey metrics: CSAT **3.8/5 average, 65% top-two-box (n=20)**; NPS **+20** (50% promoters, 20% passives, 30% detractors; n=20). Ratings are generated separately from comment text and documented as illustrative only.
- Offline tests: **8 passed** in the focused pipeline suite after survey-score and blind-worksheet updates.
- The running dashboard was visually inspected in the browser: 120 records and classifications loaded, and the CSAT and NPS cards and distributions were visible. Focused offline pipeline tests passed locally (**8 passed**) using the saved Python 3.13 environment. The hosted GitHub Actions suite also passed on Python **3.11, 3.12, and 3.13**.
- Human-review worksheet: **30 records**, all with sentiment and category labels. Against the initial blind labels, sentiment scored **80% accuracy / 0.407 macro-F1 (n=30; 3 of 4 classes represented)**, and category scored **83.3% accuracy / 0.844 macro-F1 (n=30; all 10 classes represented)**. The comparison produced **11 disagreements**: six sentiment and five category. All five category disagreements were human `Onboarding` versus Gemini `Documentation` for the same setup-guide scenario. Post-review notes judged Gemini's label more appropriate in all 11 cases; the original blind labels remain unchanged so the initial comparison is auditable. This single-reviewer, post-model review is qualitative adjudication, not an independent quality estimate.
- The usage ledger recorded **145 request events** for 117 record IDs: 135 responses and 10 failed attempts, with 23,668 input tokens and 14,025 output tokens. Twenty-one IDs have multiple events; the ledger does not retain enough detail to explain every repeat. The first three smoke-test requests predate the ledger. No cost estimate is available because token-rate values were not configured.
- The initial fast burst returned 429 rate-limit errors; later requests used an 8-second minimum interval. Transient 503 responses recovered, leaving no failed classification rows. No billing or model changes were made.
- No API keys were printed or added to project files. `.env` was not modified.

## Remaining work and limits

- Before making operational quality claims, evaluate representative, de-identified real-world language, add an independent second reviewer, cover the missing `Positive` sentiment class, and document agreement and adjudication. Keep the AI-generated review file separate from human ground truth.
- Dependency ranges are declared in `requirements.txt`, but no lockfile is provided. Optional token-rate settings are needed for estimated API costs.
- The dataset is templated synthetic data and cannot establish real-world prevalence, customer impact, or model quality.
- The repository was initialized and pushed to `main` as commit `a988fd4` after explicit approval. The reviewed 36-file allowlist excludes `.env`, `.venv`, per-record caches, Python caches, and the local API-usage ledger. A credential-pattern scan of staged text files found no hits; `.gitignore` excludes local secrets and runtime artifacts. GitHub Actions passed on Python 3.11, 3.12, and 3.13.

For setup, architecture, usage, and methodology, see [README.md](README.md). For the manual labeling protocol, see [data/evaluation/README.md](data/evaluation/README.md).
