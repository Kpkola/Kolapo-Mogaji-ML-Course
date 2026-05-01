# Capstone — Glucose Guardian

> **Autonomous GenAI Edge Agent for Adult Type 2 Diabetes Monitoring**
> *Solo Project · Practical Path · Spring 2026*

> **The midterm secured the device. The capstone makes it act.**

## Where the Code and Documentation Live

The full Glucose Guardian capstone lives in its own dedicated repository:

### **→ [github.com/Kpkola/glucose-guardian](https://github.com/Kpkola/glucose-guardian)**

That repository contains the runnable Streamlit demo, all eight Python modules, real screenshots of the dashboard in action, and a comprehensive README walking through every architectural commitment.

## What the Project Is

The Glucose Guardian extends the Group Seven midterm cybersecurity plan into an **autonomous edge agent**. Where the midterm defended a passive system, the capstone makes that system act on its own — detecting glycemic anomalies, escalating to clinicians, and explaining its decisions through a hybrid GenAI layer — all without the agent ever bypassing its hardcoded safety boundaries.

Five architectural commitments are demonstrated live:

1. **Tiered escalation** — four tiers (LOG → NOTIFY_PATIENT → NOTIFY_CLINICIAN → EMERGENCY) per a signed escalation policy
2. **Confidence-floor fallback** — when the detector's confidence falls below 0.62, the agent degrades gracefully to deterministic rules and flags the degradation in the log
3. **Hybrid GenAI explanation** — deterministic templates as the primary path; Claude API as an optional rich path; both writing to the same audit trail
4. **HMAC-chained signed audit log** — every decision is committed; modifying any line invalidates downstream HMACs
5. **Policy hash re-verification on every decision** — a tamper of the signed escalation policy halts automatic action and triggers a clinician alert

## My Role

This is a **solo project**. I designed the architecture, wrote every line of code, drafted all six deliverables (proposal, architecture document, Streamlit demo, demo walkthrough deck, final presentation deck, reflective journal), and documented the work end-to-end.

I served as **Agent Architect** for this project — a role that emerged out of my Defense Strategy Lead role on the midterm. The defense vocabulary developed for the midterm (eight security domains) needed extension to govern an autonomous system, which is what produced the proposed **ninth domain: Agent Governance and Autonomy Bounds**.

## What's in the Capstone Repository

- **`app.py`** — Streamlit clinician dashboard with custom design-system theming
- **`streamer.py`** — Synthetic CGM data generator calibrated to the ShanghaiT2DM dataset (Zhao et al., 2023)
- **`detector.py`** — Simulated TFLite anomaly detector with the same `predict(window) → Prediction` contract a real quantized model would expose
- **`agent.py`** — Autonomous agent runtime implementing the full decision flow
- **`genai.py`** — Hybrid GenAI explanation layer (templates + Claude API)
- **`audit.py`** — Signed audit log + policy-hash verifier
- **`policy.json`** — The signed escalation policy itself
- **`screenshots/`** — Real captures of the dashboard at five demo states (baseline, severe hypo, mixed events, tamper alert, audit trail)

## How This Connects to the Rest of the Portfolio

| Course element | What it contributed to the capstone |
|---|---|
| **Lab 02** (TFLite, MNIST CNN) | The quantized inference contract |
| **Lab 03** (Edge device deployment) | The simulated edge target paradigm |
| **Lab 04** (IIoT sensor network protocols) | The MQTT-over-TLS transport pattern |
| **Lab 07** (AoI–Reliability trade-off) | Awareness that latency and reliability are coupled, not separable |
| **Assignment 03** (Liverpool Smart Pedestrians) | Privacy-preserving edge architecture pattern |
| **Assignment 09** (Autonomous Agents in Industry 4.0) | RL-style reward-as-architecture thinking carried into the agent's tier policy |
| **Midterm** (Group cybersecurity plan) | The eight-domain trust substrate the capstone extends |

## Available Capstone Deliverables

The capstone produced six files; not all are committed to the dedicated repo (some are private grading deliverables). The complete set:

1. **Proposal** (Word doc, 2 pages)
2. **Architecture Document** (Word doc, 9 pages with 4 design-system diagrams)
3. **Streamlit Demo** (full source code + screenshots — *publicly available in the linked repo*)
4. **Demo Walkthrough Deck** (PowerPoint, 9 slides with all 5 screenshots embedded)
5. **Final Presentation Deck** (PowerPoint, 12 slides covering the full project arc)
6. **Reflective Learning Journal** (Word doc, 5 pages with 10 numbered sections)

## License

The Glucose Guardian source code is released under the MIT License — see the dedicated repository for details.
