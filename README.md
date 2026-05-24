# Route Execution Confidence Scoring

## Overview

This project develops a confidence-scoring framework for evaluating transportation route execution using GPS data.

In real-world transportation operations, unreliable GPS signals often make it difficult to determine whether route issues are caused by actual operational problems or simply poor data quality. This project focuses on separating GPS reliability from operational execution quality to create a more trustworthy route validation process.

The framework uses a two-stage quality gate: first determining whether GPS data is reliable enough to support evaluation, then assessing whether the route was executed as planned.

This project was developed as part of a live analytics consulting engagement through the Carlson Analytics Lab in collaboration with 4MATIV Technologies.

---

## Repository Contents

- [`README.md`](./README.md) — project overview, framework design, key insights, and recommendations
- [`route_execution_confidence_scoring.pdf`](./route_execution_confidence_scoring.pdf) — public portfolio version of the stakeholder-facing presentation deck

---

## Problem Statement

GPS-based monitoring systems are commonly used to validate transportation route execution. However, incomplete GPS coverage, delayed signals, and inconsistent tracking behavior can make operational evaluation unreliable.

A low-quality GPS trace does not necessarily imply poor operational execution, while a seemingly complete trip may still contain meaningful execution issues.

This project addresses the challenge of distinguishing operational failure from GPS-data failure.

---

## Why Rule-Based Scoring

A rule-based scoring approach was selected because the project required transparent, interpretable operational logic and did not rely on labeled ground-truth route failure data.

This made the framework easier to explain to business stakeholders, more practical for operational triage, and more adaptable as additional route validation knowledge becomes available.

---

## Framework Design

The framework combines two major components:

### 1. GPS Reliability Score

Evaluates whether GPS data is reliable enough to support operational validation.

Key dimensions include:

- GPS coverage completeness
- Signal continuity
- Movement consistency
- Data availability

Trips are categorized into:

- Reliable
- Partially Reliable
- Unreliable

---

### 2. Execution Score

Measures operational route quality using multiple execution indicators:

- Spatial accuracy
- Stop coverage
- Path continuity
- Sequence adherence
- Timing adherence

The indicators are aggregated into a trip-level execution score.

---

## Confidence Score Logic

The final Confidence Score combines GPS reliability and execution quality:

**Confidence Score = GPS Reliability × Execution Score**

This design prevents degraded GPS quality from being incorrectly interpreted as operational underperformance.

The framework introduces three operational confidence categories:

| Confidence Level | Interpretation |
|---|---|
| Flagged | GPS quality too unreliable for operational evaluation |
| Review Required | Partial confidence — manual review recommended |
| Validated | High-confidence route execution |

---

## Key Insights

### GPS Availability Alone Is Insufficient

The analysis showed that GPS availability by itself does not guarantee reliable route visibility. Some trips maintained partial signal continuity while still containing coverage gaps that reduced confidence in operational validation.

### Data Failure and Operational Failure Are Different Problems

Several lower-performing trips showed weak execution indicators despite relatively reliable GPS quality, suggesting likely operational execution issues rather than data-quality problems.

Conversely, some trips appeared problematic primarily because of degraded GPS quality, making operational conclusions uncertain without additional review.

### Path Continuity Is a Critical Validation Signal

Path continuity helped identify whether missing GPS data created only minor gaps or fragmented the route trace enough to weaken execution validation.

This distinction was important because route completion alone does not confirm whether the assigned route was actually followed.

### Confidence-Based Validation Improves Operational Interpretability

The framework demonstrated that trip completion status alone is insufficient for evaluating execution quality.

A substantial portion of trips fell into a review-required category where GPS reliability and execution quality did not fully align. Introducing a confidence layer created a more interpretable and trustworthy operational evaluation process.

---

## Recommendations

Based on the analysis, the project recommended:

- Prioritizing operational review for routes or trips with reliable GPS but consistently weak execution indicators
- Investigating GPS-device quality for trips with degraded signal reliability
- Separating data-quality remediation workflows from operational-performance workflows
- Using confidence-based triage rather than relying solely on raw completion status
- Treating path continuity as a key diagnostic signal when evaluating route execution quality

---

## Technical Methods

| Category | Methods |
|---|---|
| Language | Python |
| Analytics | Rule-based scoring framework |
| Spatial Analysis | GPS proximity and route validation |
| Signal Quality Analysis | GPS coverage, continuity, and movement checks |
| Operational Validation | Confidence scoring and execution triage |
| Visualization | Matplotlib, Seaborn |

---

## Data Confidentiality

This repository contains a public portfolio version of the project.

Raw GPS data, operational identifiers, route-level targeting details, scoring thresholds, data pipeline code, and proprietary client operational information have been excluded or generalized for confidentiality purposes.
