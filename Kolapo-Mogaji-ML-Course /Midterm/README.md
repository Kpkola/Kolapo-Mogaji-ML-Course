# Midterm — Cybersecurity Plan for an AI-Integrated IIoT Glucometer

> **Group Project · Defense Strategy Lead Role · April 2026**

## The Project

Group Seven was tasked with producing a comprehensive cybersecurity plan for a hypothetical AI-integrated IIoT glucometer system, aligned with industry standards including HIPAA, FDA Cybersecurity Guidance, and IEC 62443. The system was a six-layer architecture (Device → Edge → AI → Network → Cloud → Dashboard) using an ESP32 microcontroller for the device, BLE/HTTPS for transport, an LSTM/Transformer model for glucose prediction, and patient/clinician dashboards.

The deliverable covered four major workstreams: vulnerability identification across the architecture, a defense strategy spanning eight security domains, an implementation plan, and a penetration testing simulation with attack execution and findings.

## The Team

- **Cassy Cormier** — System design and implementation, penetration testing
- **Monica Joya** — Implementation plan, project coordination
- **Sufyan Rafiq** — Threat modeling, adversarial ML analysis
- **Kolapo Mogaji (me)** — **Defense Strategy Lead.** Owned the eight-domain defense architecture, IEC 62443 zone-and-conduit modeling, and the resource-constrained ESP32 trade-off analysis.

## What I Contributed

As Defense Strategy Lead, my responsibilities included:

- **Mapping the eight defense domains** to specific controls and standards: Secure by Design, Authentication and Access Control, Encryption and Data Protection, Network Security, Secure Software Development, Physical Security, Security Monitoring, and AI Model Protection.
- **Standards alignment** — connecting each control to specific clauses in HIPAA Security Rule (45 CFR §164), IEC 62443 zone-and-conduit segmentation, NIST SP 800-207 Zero Trust, NIST SP 800-82 Rev. 3 (OT security), and FDA Cybersecurity Guidance.
- **Resource-constrained design analysis** — examining what enterprise-grade controls could realistically run on an ESP32 with limited flash and processing power, and where trade-offs were necessary.
- **Usability dimension of security** — surfacing the human cost of MFA steps and short session TTLs for a diabetic patient who may be experiencing a hypoglycemic episode.

## Key Findings From the Penetration Testing Phase

The team executed simulated attacks using Kali Linux, Burp Suite, Wireshark, Nmap, and curl-based fuzzing. Several attack classes were successfully mitigated by design:

- SQL injection blocked through Pydantic validation and ORM-based queries
- Data tampering (extreme glucose values) rejected by backend constraints
- Invalid or fake authentication tokens denied
- API fuzzing produced no crashes — strong input handling

Critical vulnerabilities that *were* found:

- Missing authentication on `/devices`, `/alerts`, and `/predictions` endpoints
- MITM vulnerability — data transmitted in plain text on parts of the system
- Device spoofing — false glucose readings could be injected into the system
- Open ports increasing the attack surface

## What I Took Away From This Project

Designing defenses for a resource-constrained ESP32 *while* securing a HIPAA-regulated cloud backend was the biggest single challenge. I couldn't deploy enterprise-grade controls on a device with limited flash and processing power, so I had to make explicit trade-offs and document them. The **usability dimension** was equally challenging — a diabetic patient should not face security that feels like a bank vault. Every MFA step or short session TTL has a human cost for someone who may be experiencing a hypoglycemic episode.

The most valuable specific learning was internalizing **IEC 62443's Zone and Conduit model**. Thinking in zones (device, gateway, DMZ, application, data) and conduits (the controlled paths between them) made the architecture defensible in a way that "perimeter security" thinking never could.

If implementing this system for real, I would prioritize **federated learning** so the AI model could learn without centralizing PHI. That aspiration carried directly into my solo capstone (the Glucose Guardian), where on-device confidentiality became a first-class architectural property rather than a feature added later.

## Connection to My Capstone

This midterm became the foundation for my solo capstone project. The eight defense domains documented here carry forward unchanged into the capstone's nine-domain architecture — I added a ninth domain (Agent Governance and Autonomy Bounds) to address the new attack surfaces that autonomous decisioning and generative AI introduce. The midterm secured the device. The capstone makes it act.

See [`/Capstone`](../Capstone/) for the continuation.

## Files in This Folder

- `MT_Group_Seven_Cybersecurity_Plan.pdf` — Full group deliverable: system design, vulnerability assessment across six categories, eight-domain defense strategy, four-phase implementation plan, penetration testing simulation results, and individual reflections from each group member. References include CISA, NIST SP 800-207, NIST SP 800-82 Rev. 3, OWASP IoT, HIPAA Security Rule, and FDA Cybersecurity Guidance.

## A Note on Authorship

This is a group deliverable. The shared sections (system design, vulnerability assessment, defense strategy synthesis, penetration testing) reflect collective work. Individual reflections are clearly labeled by author in §6 of the document. My contribution as Defense Strategy Lead is most visible in §3 (Defense Strategy) and the overall coherence between vulnerabilities and controls across §2 and §3.
