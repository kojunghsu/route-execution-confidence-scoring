# Route Execution Confidence Scoring Framework

## Overview

This project develops a confidence-scoring framework for evaluating transportation route execution using GPS data.

In real-world transportation operations, unreliable GPS signals often make it difficult to determine whether route issues are caused by actual operational problems or simply poor data quality. This project focuses on separating GPS reliability from operational execution quality to create a more trustworthy route validation process.

The framework combines GPS signal validation with execution-level indicators to assess whether completed trips can be confidently treated as successful route executions.

This project was developed as part of a live analytics consulting engagement through the Carlson Analytics Lab in collaboration with 4MATIV Technologies.

---

## Repository Contents

- [`README.md`](./README.md) — project overview, framework design, key insights and recommendations
- [`route_execution_confidence_scoring.pdf`](./route_execution_confidence_scoring.pdf) — public portfolio version of the stakeholder-facing presentation deck

---

## Problem Statement

GPS-based monitoring systems are commonly used to validate transportation route execution. However, incomplete GPS coverage, delayed signals, and inconsistent tracking behavior can make operational evaluation unreliable.

A low-quality GPS trace does not necessarily imply poor operational execution, while a seemingly complete trip may still contain meaningful execution issues.

This project addresses the challenge of distinguishing operational failure from GPS-data failure.

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

```text
Confidence Score =
GPS Reliability × Execution Score
```

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

The analysis showed that GPS availability by itself does not guarantee reliable route visibility. Some trips maintained partial continuity while still containing significant coverage gaps that reduced confidence in operational validation.

### Data Failure and Operational Failure Are Different Problems

Several lower-performing trips showed weak execution indicators despite relatively reliable GPS quality, suggesting likely operational execution issues rather than data-quality problems.

Conversely, some trips appeared problematic primarily because of degraded GPS quality, making operational conclusions uncertain without additional review.

### Confidence-Based Validation Improves Operational Interpretability

The framework demonstrated that trip completion status alone is insufficient for evaluating execution quality.

A substantial portion of trips fell into a “review required” category where GPS reliability and execution quality did not fully align. Introducing a confidence layer created a more interpretable and trustworthy operational evaluation process.

---

## Recommendations

Based on the analysis, the project recommended:

- Prioritizing operational review for trips with reliable GPS but consistently weak execution indicators
- Investigating GPS-device quality for trips with degraded signal reliability
- Separating data-quality remediation workflows from operational-performance workflows
- Using confidence-based triage rather than relying solely on raw completion status

---

## Technical Methods

| Category | Methods |
|---|---|
| Language | Python |
| Analytics | Rule-based scoring framework |
| Spatial Analysis | GPS proximity and route validation |
| Time-Series Logic | Signal continuity and timing analysis |
| Visualization | Matplotlib, Seaborn |
| Framework Design | Confidence scoring and operational validation |

---

## Data Confidentiality

This repository contains a public portfolio version of the project.

Raw GPS data, operational identifiers, route-level targeting details, and proprietary client operational information have been excluded or generalized for confidentiality purposes.