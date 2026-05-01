# Assignment 03 — Liverpool Smart Pedestrians: Edge-Computing Case Study

> **Edge-Computing Video Analytics · Real-Time Traffic Monitoring · NVIDIA Jetson TX2 · Privacy-Preserving Architecture**

## The Problem

The Liverpool Smart Pedestrians project (Barthélemy et al., 2019) is a real-world deployment of edge-computing video analytics for multi-modal traffic monitoring in a smart-city context. The project — a one-year collaboration between Liverpool City Council (Australia) and the University of Wollongong, funded by the Smart Cities and Suburbs Program — designed a sensor that detects and tracks pedestrians, vehicles, and cyclists in real time using existing CCTV infrastructure, while ensuring full compliance with privacy regulations.

This assignment was a critical analysis of that project: examining the engineering decisions, evaluating the methodology, and assessing the implications for edge-AI deployments more broadly.

## My Approach

The analysis followed the structure required by the assignment rubric (six labeled sections), but I worked to make each section critically engaged rather than purely descriptive:

- **Introduction and Objectives** — placed the project in the context of smart-cities literature (Bibri & Krogstie 2017a, 2017b), examined the four user-derived requirements that emerged from community workshops, and identified the underlying urban-planning challenges
- **Methodology** — analyzed the user-centered, requirements-driven design process; documented the hardware stack (NVIDIA Jetson TX2 + Pycom LoPy 4 + IP67 enclosure); and evaluated the two-stage performance benchmarking against the Oxford Town Center Dataset
- **Findings** — summarized the project's quantitative results (detection accuracy, system utilization, network bandwidth)
- **Implications** — connected the architectural choices (edge-resident processing, metadata-only transmission) to the privacy and bandwidth constraints they were designed to satisfy
- **Critical Evaluation** — examined what the project did well and where it falls short of full deployability
- **Conclusion** — synthesized lessons applicable to other edge-AI deployments

## Key Insights

- **The edge-computing paradigm here solves two problems simultaneously.** Running video analytics on the device — and transmitting only metadata (object counts, trajectories, timestamps) to the IoT backend — addresses both the bandwidth constraint *and* the privacy requirement (no images leave the CCTV network). This is the kind of architectural decision that looks obvious in hindsight but represents real engineering judgment.
- **Reusing existing infrastructure unlocks real value.** Australia's CCTV networks represent major financial investments used almost exclusively for incident investigation, leaving a vast dataset effectively unused for planning purposes. Adding a sensor module that operates on the existing video feed delivers new value without compromising the network's privacy obligations or requiring a parallel installation.
- **Privacy compliance shapes system architecture, not just policy.** The "no personal data stored or transmitted" requirement isn't a checkbox on a deployment form — it's the constraint that determines where computation happens and what crosses the network boundary.
- **Community workshops produced engineering requirements.** The four core sensor requirements all emerged from a 35-participant workshop, not from a top-down technical specification. This grounding made the resulting system answerable to actual urban-planning needs rather than purely technical objectives.

## What I Took Away

The Liverpool project is a useful counterexample to the "AI in the cloud, sensors on the edge" default. Edge inference isn't always about latency — sometimes it's about *what* can cross a privacy boundary. The architectural framing here directly informed how I thought about the on-device confidentiality story in my capstone (where PHI never leaves the gateway in plaintext for the same reason video frames never leave the CCTV network in plaintext).

The case study also reinforced a general lesson about evaluation: a working simulation is necessary but not sufficient evidence that a system will hold up in deployment. The project's two-stage benchmarking — first against an annotated public dataset, then against a real CCTV feed — is a pattern worth carrying into other edge-AI work.

## Files in This Folder

- `A03_Case_Study.docx` — Full critical analysis report with all six sections, tables documenting the hardware stack and performance results, references to peer-reviewed sources, and a discussion of implications for similar deployments.

## References (Primary)

- Barthélemy, J., et al. (2019). Liverpool Smart Pedestrians project — Final report. *Smart Cities and Suburbs Program, Australian Government*.
- Bibri, S. E., & Krogstie, J. (2017). Smart sustainable cities of the future: An extensive interdisciplinary literature review. *Sustainable Cities and Society*.
- Benfold, B., & Reid, I. (2011). Stable multi-target tracking in real-time surveillance video. *CVPR 2011*.
