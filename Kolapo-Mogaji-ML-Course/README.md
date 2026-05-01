# Kolapo Mogaji — ITAI 3377 Course Portfolio

**Edge AI & Embedded Systems · Houston City College · Spring 2026**

Welcome to my portfolio for ITAI 3377 (Edge AI & Embedded Systems / IIoT). This repository collects the work I produced during the semester — labs, assignments, the group midterm project, and my solo capstone. Each folder contains the deliverable itself plus a written README explaining the work, what I learned, and the engineering decisions behind it.

---

## About Me

I'm a junior at Houston City College pursuing a degree in Artificial Intelligence and Robotics, graduating May 2027. My interest in machine learning sits at the intersection of three things I care about: practical engineering, applied AI for real-world problems, and clear communication about how those systems work.

Outside of coursework I run a creative production company where I've built ETL pipelines, client dashboards, and AI-powered tools. That work is what pulled me toward formal training in edge AI in the first place — I kept hitting points where I needed to understand the systems I was integrating with, not just call their APIs. ITAI 3377 gave me that foundation.

I came into this course wanting concrete experience with the full edge-AI pipeline: data preparation, model training, quantization for resource-constrained devices, IIoT communication protocols, deployment, and the security considerations that come with putting AI into the physical world. The work in this portfolio represents that journey.

---

## Portfolio Highlights

**The two pieces I'd direct any reviewer to first:**

- **[Capstone — Glucose Guardian](Capstone/)** — solo end-to-end build of an autonomous GenAI edge agent for adult Type 2 diabetes monitoring, with HMAC-chained audit trails and policy-hash verification. Live demo at [github.com/Kpkola/glucose-guardian](https://github.com/Kpkola/glucose-guardian).
- **[Lab 07 — AoI–Reliability Trade-off](Labs/Lab07-AoI-Reliability/)** — data-driven analysis of an IIoT communication trade-off using Random Forest and a multi-output neural network on 10,000 simulated network observations.

---

## Labs

| # | Topic | Format |
|---|-------|--------|
| 02 | [AI Model Conversion & Deployment (TFLite, MNIST CNN)](Labs/Lab02-TFLite-MNIST/) | Conceptual report + reflective journal + notebook export |
| 03 | [Deploying a CNN on a Simulated Edge Device (Edge Impulse, Cortex-M4)](Labs/Lab03-EdgeDevice-Deployment/) | Step-by-step report with terminal logs |
| 04 | [IIoT Sensor Network — MQTT, CoAP, OPC UA](Labs/Lab04-IIoT-Sensor-Network/) | Reflective report on protocol simulation |
| 07 | [AoI–Reliability Trade-off in Heterogeneous IIoT Networks](Labs/Lab07-AoI-Reliability/) | Technical report + Jupyter notebook |

## Assignments

| # | Topic | Format |
|---|-------|--------|
| 03 | [Liverpool Smart Pedestrians — Edge-Computing Case Study](Assignments/Assignment03-Liverpool-Smart-Pedestrians/) | Critical analysis report |
| 09 | [Autonomous Agents in Industry 4.0 — DDQN Warehouse AGVs](Assignments/Assignment09-Autonomous-Agents-Industry4/) | Case study analysis |

## Midterm Project

| Project | Role |
|---------|------|
| [Cybersecurity Plan for an AI-Integrated IIoT Glucometer](Midterm/) | Defense Strategy Lead (group of four) |

## Capstone Project

| Project | Role |
|---------|------|
| [Glucose Guardian — Autonomous GenAI Edge Agent](Capstone/) | Solo Agent Architect |

---

## Repository Organization

```
Kolapo-Mogaji-ML-Course/
├── README.md                 ← you are here
├── LICENSE
├── .gitignore
├── Labs/
│   ├── Lab02-TFLite-MNIST/
│   ├── Lab03-EdgeDevice-Deployment/
│   ├── Lab04-IIoT-Sensor-Network/
│   └── Lab07-AoI-Reliability/
├── Assignments/
│   ├── Assignment03-Liverpool-Smart-Pedestrians/
│   └── Assignment09-Autonomous-Agents-Industry4/
├── Midterm/
└── Capstone/
```

Each folder includes a dedicated README that explains the work in plain language, so you don't have to dig through code or reports to understand what each one was about.

---

## Reflection on the Course

ITAI 3377 reframed my understanding of what "AI" means in production. Going in, I thought of machine learning as a model trained on a workstation and called via an API. By the end I was deploying quantized TFLite models to Cortex-M4 simulators, reasoning about MQTT versus CoAP versus OPC UA for industrial telemetry, and treating model security (adversarial robustness, data integrity, output bounding) as a first-class concern rather than an afterthought.

The biggest single shift came during the midterm and capstone arc. The midterm gave me a vocabulary for defending a passive system. The capstone forced me to extend that vocabulary to govern an autonomous one — a much harder problem. That extension became my proposed "ninth domain" of agent governance and autonomy bounds, which I documented in the capstone architecture and reflection.

Beyond the technical content, the course taught me to write about my work in a way that someone outside the course can actually follow — which is what every artifact in this portfolio tries to do.

---

## Contact

- **GitHub:** [@Kpkola](https://github.com/Kpkola)
- **Capstone Repository:** [github.com/Kpkola/glucose-guardian](https://github.com/Kpkola/glucose-guardian)
- **School:** Houston City College — Artificial Intelligence and Robotics, graduating May 2027

---

*Submitted as the final portfolio for ITAI 3377 — Edge AI & Embedded Systems, Spring 2026. Professor Sitaram Ayyagari.*
