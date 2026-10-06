# GST Exception Resolver

> **Help CA firms resolve GST reconciliation exceptions and explain the action required, rather than merely showing mismatched rows.**

## Status

- Rank: **#1**
- Movement: ↑ Strengthened, wedge narrowed
- Stage: **VALIDATING**
- First discovered: 2026-10-06
- Last validated: Not yet validated with customer data
- Last updated: 2026-10-07
- Recommended action: **Validate exception-resolution workflow with 3 CA firms; do not build generic reconciliation**

## TL;DR

Indian CA/accounting teams repeatedly reconcile books against GST data. The painful part is often not finding a mismatch; it is determining **why** it happened and **what to do next**.

The proposed wedge is now narrower:

> **Resolve the exceptions that block or delay ITC decisions, not another generic matching engine.**

Upload two spreadsheet exports → reconcile deterministically → classify high-value exceptions → generate the evidence/action queue for the CA team. The differentiator should be the resolution workflow: why this exception matters, what evidence is missing, and what should be checked next.

The MVP should not start with GSTN API integration or a full accounting platform.

## Problem

Typical exception categories include:

- invoice missing on one side;
- GSTIN mismatch;
- invoice-number formatting mismatch;
- tax/value mismatch;
- duplicate;
- timing/filing-period difference;
- credit-note/amendment difference.

The workflow is repetitive and spreadsheet-heavy.

## Exact user

Primary:

- CA firms
- GST practitioners
- outsourced bookkeeping/accounting teams

Secondary:

- finance teams managing large vendor populations.

## Payer

The CA/accounting firm or finance department.

## Current workaround

Likely combination of:

- accounting software;
- GST portal exports;
- Excel;
- lookup formulas;
- manual inspection;
- client/vendor follow-up.

## Proposed solution

```mermaid
flowchart LR
    A[Books XLSX] --> C[Normalize]
    B[GST data XLSX] --> C
    C --> D[Deterministic matching]
    D --> E[Exception classification]
    E --> F[Actionable report]
    E --> G[AI explanation]
```

## Evidence

### Observed

Current research found Indian practitioner discussions describing invoice-level GST reconciliation as a recurring workload, including discussions from CA professionals managing many clients.

Current evidence is stronger than the initial snapshot. GCCI recently sought action on persistent import-IGST/GSTR-2B mismatches that can delay or deny rightful ITC, showing direct working-capital consequences. At the same time, multiple products now market automated GSTR-2B reconciliation. The market validates the pain but rules out a generic matcher as the wedge.

### Inference

A narrow exception-resolution workflow may still be differentiated, but only if it handles messy cases existing matchers leave for humans: import IGST discrepancies, period/timing issues, amendments/credit notes, supplier follow-up, and evidence for the final decision.

### Hypothesis

CA firms will pay monthly if the product reliably reduces staff hours without introducing financial/compliance errors.

## Competitors

| Competitor/category | Strength | Weakness/opportunity |
|---|---|---|
| ClearTax | Broad tax/accounting ecosystem | Opportunity is to focus narrowly on exception explanation/action |
| Tally ecosystem | Deep accounting adoption | Not necessarily optimized around a lightweight exception-resolution workflow |
| GST reconciliation tools | Existing reconciliation functionality | Need evidence that users still need a better exception workflow |

Competitor research must be refreshed before launch.

## Why now?

AI makes it practical to add a useful **resolution layer** on top of deterministic reconciliation. Existing matching is increasingly commoditized; the opportunity is the human decision queue after matching.

The product can say:

> "These records match on supplier and value but fall into different filing periods; verify whether this is a timing difference."

The model should never decide the underlying financial match.

## MVP

### Must have

- XLSX upload;
- schema mapping;
- normalization;
- deterministic matching;
- exception classification;
- downloadable exception report;
- basic dashboard.

### Should have

- AI explanation;
- suggested next action;
- reusable mapping templates.

### Not now

- GSTN integration;
- accounting-system integrations;
- automated filing;
- automated client communication;
- enterprise permissions;
- complex dashboards.

## Architecture

```mermaid
flowchart TD
    UI[React UI] --> API[Node/TypeScript API]
    API --> INGEST[XLSX ingestion]
    INGEST --> NORM[Normalization]
    NORM --> ENGINE[Reconciliation engine]
    ENGINE --> DB[(SQLite/Postgres)]
    ENGINE --> REPORT[Excel/CSV report]
    ENGINE --> AI[Optional LLM explanation]
```

**Critical design rule:** deterministic code owns financial truth. AI only explains already-detected exceptions.

## Build plan

### Day 1

- XLSX parser
- normalized internal model
- matching engine
- fixtures/tests

### Day 2

- exception classifications
- basic API
- report generation
- simple UI

### Day 3

- AI explanation
- end-to-end workflow
- validation with CA users

## AI-agent tasks

1. Build XLSX ingestion with tests.
2. Build normalization layer.
3. Implement deterministic matcher.
4. Generate synthetic edge-case fixtures.
5. Implement exception classifier.
6. Build report generator.
7. Build React UI.
8. Add optional LLM explanation behind a provider interface.
9. Add end-to-end tests.

Each agent task should have explicit acceptance criteria and must not silently change financial matching rules.

## Distribution

Initial:

- direct outreach to CA firms;
- local professional network;
- CA communities;
- accounting/GST communities;
- targeted demos using anonymized/synthetic examples.

Later:

- SEO around specific reconciliation problems;
- CA partnerships;
- accounting consultants;
- referral program.

## Monetization

Initial hypotheses:

- one-off reconciliation;
- small monthly plan;
- multi-client CA-firm plan.

Pricing should not be tested until the workflow proves it saves review time or protects meaningful ITC. Existing market offerings suggest users already pay for reconciliation, so the first monetization test should be against the value of exception resolution rather than commodity matching.

These are **pricing hypotheses, not market facts**.

## Validation experiment

Recruit 3 CA firms.

Ask for anonymized exports.

Measure:

- processing time;
- exception accuracy;
- useful/incorrect explanations;
- hours saved;
- willingness to continue;
- willingness to pay.

## Success criteria

Promising if:

- at least 2/3 firms use real data;
- the tool identifies useful exceptions;
- users report meaningful time savings;
- at least one wants continued use;
- at least one gives a credible paid commitment.

## Failure criteria

- existing software already solves the exact workflow;
- users do not trust automated reconciliation;
- input formats are too chaotic;
- exception accuracy is poor;
- time saved is insignificant.

## Kill conditions

Kill this wedge if repeated real-data trials show no meaningful improvement over current tools/workflows.

## Risks

- financial correctness;
- tax/compliance interpretation;
- messy input formats;
- liability expectations;
- competitor bundling;
- GST portal/API changes.

## Open questions

1. What exact files do target CA firms use?
2. Which mismatch category consumes the most time?
3. How much manual review remains after deterministic matching?
4. Will firms upload client data to a third-party SaaS?
5. What price corresponds to meaningful ROI?
6. Is an Excel-first product enough?

## Evidence log

| Date | Evidence | Interpretation |
|---|---|---|
| 2026-10-06 | Practitioner discussions describe recurring GST reconciliation work. | Strong problem signal; needs direct validation. |
| 2026-10-06 | Existing tax products document multiple reconciliation mismatch categories. | Confirms established workflow, but not necessarily unmet demand. |
| 2026-10-07 | GCCI sought urgent action on persistent import-IGST/GSTR-2B mismatches affecting ITC and working capital. | Strengthens severity and suggests a high-value exception class worth testing. |
| 2026-10-07 | TaxSolver markets automated GSTR-2B reconciliation to 250+ CA firms and handles ERP/Excel inputs. | Confirms category demand, but makes generic reconciliation a weak wedge. |
| 2026-10-07 | Mark IT offers browser-only GSTR-2B vs books reconciliation with no server upload. | Commodity matching is already easy to access; differentiation must be downstream of matching. |

## Ranking history

| Date | Rank | Stage | Movement | Reason |
|---|---:|---|---|---|
| 2026-10-06 | 1 | VALIDATING | 🆕 | Best current evidence-to-effort path. |
| 2026-10-07 | 1 | VALIDATING | ↑ | Fresh import-IGST mismatch evidence increases severity, while competitive products force a narrower exception-resolution wedge. |

## Decision history

2026-10-06 — Selected for the first validation experiment. No build commitment beyond a small prototype.
