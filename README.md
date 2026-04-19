Billing Anomaly Detection + LLM Alert Explainer

> ML-powered billing integrity system that detects anomalous transactions 
> and converts each flag into a structured, plain-English operational alert.

Problem Statement

Billing errors — duplicate charges, zero-charge revenue leakage, pricing 
misconfigurations — directly damage revenue and customer trust. Detecting 
them automatically and explaining them clearly to operations teams is a 
core challenge for any subscription billing platform.

Dataset

- Type: Synthesised billing transaction dataset
- Size: 1,000 records with 4 injected anomaly types
- Anomaly types: Duplicate charges · Zero-charge leakage · 
  Overcharges (10x pricing) · Plan-price mismatches
- Generation: Python (Pandas + Faker)

Approach

Stage 1 — Data Generation
- Generated 950 normal + 50 anomalous transactions
- Injected 4 distinct billing failure modes with controlled frequency

Stage 2 — Anomaly Detection
- Engineered features: price deviation ratio, plan encoding
- Applied Isolation Forest (contamination = 5%) for unsupervised detection
- Scored all transactions by anomaly probability

Stage 3 — LLM Alert Explainer
- Built structured prompt: transaction metadata + deviation + anomaly context
- Called Groq API (LLaMA 3.1) to generate a 4-field structured alert
- Alert fields: Anomaly Type · Root Cause · Revenue Impact · Recommended Action
- Stored all alerts in SQLite

Business Impact

Billing operations teams typically need a data analyst to interpret 
anomaly detection output. This system removes that dependency — every 
flagged transaction arrives with a ready-to-act plain-English alert 
including the probable cause and specific recommended action.
