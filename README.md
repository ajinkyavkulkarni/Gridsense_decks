This repository documents GridSense AI, a SaaS platform designed to predict electricity theft, forecast true demand, and predict transformer/blackout failures 24 hours in advance — for India's Tier 2/3 power distribution companies (DISCOMs). The product works entirely on data every DISCOM already generates (monthly billing CSVs, energy audit files, feeder logs) — no smart meters or SCADA infrastructure required.
This project was built end-to-end across two phases: a structured ideation and product-strategy phase, followed by ground-level field validation at an operational DISCOM sub-division. The repository contains all three deliverables from the sprint.

Repository Contents
2673_StartupSprint/
├── 2673_Pitchdeck_StartupSprint.pdf            # Investor-facing pitch deck
├── 2673_ProblemSolutionReport_StartupSprint.pdf # Phase 1 ideation & technical architecture report
└── 2673_SprintJourney_StartupSprint.pdf         # Phase 2 field research & implementation report

Document Overview
1. Pitch Deck — 2673_Pitchdeck_StartupSprint.pdf
The competition-facing pitch deck built for Kriti 2026. Covers:

Problem framing — India's AT&C loss crisis (15–20% losses vs. 6–7% global benchmark), the ₹1.45 lakh crore annual revenue leak, and why Junior Engineers currently operate blind with paper logbooks
Why existing solutions fail — Enterprise AI platforms (ABB, Siemens, Pravah) require smart meters and SCADA, leaving 91% of India's feeders unserved
GridSense AI's three-module solution — Theft Detection → Demand Forecasting → Blackout Prediction in a single causal pipeline
Market sizing — TAM of $75B (India's accumulated DISCOM losses), SAM of ₹6,655 Cr/year, SOM projections from Assam (Year 2) scaling to pan-India ₹8,000 Cr+ (Year 5)
Competitive landscape & SWOT — Positioning as the only zero-capex product serving the unmetered 91%, with RDSS 2026 compliance as a forcing function
Go-to-market — Free pilot with APDCL (Guwahati subdivision) → Northeast India → national rollout → global Tier 2/3 utilities across 135 countries


2. Problem–Solution Concept & Impact Rationale — 2673_ProblemSolutionReport_StartupSprint.pdf
The full Phase 1 ideation report. The most detailed document in the repository — a ground-up articulation of the problem, the product logic, and the impact case.
Problem Diagnosis
Identifies three interlocking root causes that standard solutions cannot address simultaneously:

Electricity theft adding invisible, unmetered load to feeders
Load shedding creating suppressed demand that makes standard forecasting models systematically wrong
Aging infrastructure operating under hidden stress with no predictive signal

The Causal AI Insight
GridSense AI's core innovation is not three separate models — it is a deliberate causal chain where theft scores and corrected demand forecasts are fed as input features into blackout prediction. No existing commercial product models blackout risk as a downstream consequence of theft and suppressed demand simultaneously.
Technical Architecture (Module-by-Module)
ModuleApproachKey MetricTheft Detection3-layer system: AT&C normalization → Isolation Forest (unsupervised) → Random Forest (supervised)ROC-AUC: 0.9995, Recall: 97.6%Demand ForecastingProphet + LSTM ensemble with suppressed demand correction algorithmMAPE: 5.83%Blackout PredictionRandom Forest + Gradient Boosting ensemble fed by Modules 1 & 2ROC-AUC: 0.9453, Failure Recall: 91%
The final output is a GridSense Risk Score (0–100) per feeder, combining all three signals (Blackout × 0.40 + Theft × 0.35 + Demand × 0.25), delivered to the Superintendent Engineer's dashboard by 6 AM — 12 hours before the critical evening peak window.
Data Architecture
Built under a real-world constraint: DISCOM feeder-level data is not publicly available. All synthetic data was rigorously calibrated to real CEA and PFC government benchmarks so models can be deployed on actual DISCOM data with zero code changes. Real data sources include CEA Monthly Load Reports and live Open-Meteo weather API feeds for 8 Bihar/Jharkhand cities.
Impact Quantification

₹1,450 Cr recovered revenue per 1% AT&C loss reduction → 12–36× ROI on GridSense subscription
85 BU of electricity saved per 5% AT&C reduction → ~69–70 million tonnes CO2 avoided annually
Direct RDSS 2026 compliance lever — DISCOMs failing the 12–15% AT&C target lose access to ₹3 lakh crore in central government grants
Global scalability: same product (with only festival calendar updates) deployable across Bangladesh, Nigeria, Kenya, and Indonesia


3. Sprint Journey Report — 2673_SprintJourney_StartupSprint.pdf
The Phase 2 implementation and field validation report — the actual groundwork behind the product.
Field Visit: APDCL Barpeta Road Electrical Sub-Division (9 March 2026)
The team conducted a structured 1-hour primary research visit to a live DISCOM sub-division in Assam. Interviews were conducted with the Sub-Divisional Engineer (SDE) and Junior Engineer (JE) to validate the problem hypothesis against real operational conditions.
Key findings from the SDE interview:

27 feeders managed per sub-division; transformers tolerate only ~20% overload before tripping risk rises
AT&C losses at 12–14% (confirmed B+ grade by Central Government) — exactly matching the real billing data value of 13.60%
Zero transformer failures since 2024 — but no predictive system in place; the SDE confirmed directly: "Early access to such predicted data can help us stay prepared"
Load forecasting done manually on past consumption data; no analytics tools

Key findings from the JE interview:

Feeder inspection is complaint-driven and reactive — no proactive prioritisation system
Rural feeders (40–50 km lines) face 4–5 blackouts/day; urban areas 1–2/day
Theft is detected through abnormal load patterns and physical inspection of illegal hooks — entirely manual
Operational coordination relies on WhatsApp groups and phone calls

The Strategic Insight
Barpeta Road represents Assam's best-case scenario: 80% smart meter penetration, cloud data storage, B+ AT&C rating, zero recent failures. And even here, the SDE has no predictive intelligence — he is reactive by necessity. The conclusion: if the best-performing sub-division in Assam needs GridSense AI, the other 18,000 sub-divisions across India need it urgently.
The real APDCL February 2026 Revenue Report (obtained during the visit) was used to calibrate the Isolation Forest anomaly detection model and directly validate the AT&C loss inputs feeding the blackout prediction model.

Problem Context
India's power distribution crisis is fundamentally an intelligence problem, not a generation problem:

₹1.45 lakh crore in annual DISCOM revenue loss from AT&C losses of 15–20%
600 million+ consumers in Bihar and Jharkhand alone affected by chronic blackouts
89% of feeders without smart meters — making enterprise AI platforms (ABB, Siemens) entirely non-deployable
RDSS 2026 mandate: DISCOMs must reach 12–15% AT&C losses or lose access to ₹3 lakh crore in infrastructure funding
Every 1% AT&C loss reduction = ~₹1,450 Cr in recovered revenue

GridSense AI addresses this by turning the data DISCOMs already have — billing records, energy audit CSVs, feeder logs — into a 24-hour predictive intelligence layer that currently does not exist for the unmetered 91% of India's distribution grid.
