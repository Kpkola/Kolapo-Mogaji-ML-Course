# Lab 04 — IIoT Sensor Network: MQTT, CoAP, OPC UA

> **Industrial Internet of Things · Communication Protocols · Python Simulation**

## What This Lab Was About

This lab focused on the conceptual design and live simulation of an Industrial IoT sensor network using three architecturally different communication protocols: **MQTT** (publish/subscribe), **CoAP** (lightweight request/response), and **OPC UA** (structured industrial client/server). Each protocol was implemented through Python scripts that generated randomized temperature and humidity readings every second, simulating a live industrial telemetry environment.

The point wasn't simply to execute code — it was to understand how each protocol's architecture shapes the system around it. Running distributed communication systems requires proper environment configuration, dependency management, multi-terminal execution, and asynchronous debugging. This lab made clear that IIoT systems are interconnected architectural components, and a failure in one layer disrupts the entire pipeline.

## What I Did

- **CoAP client implementation** — Wrote the CoAP client simulation script generating randomized sensor values transmitted via POST requests over UDP. When the script failed with a connection refusal, I had to investigate at the architecture level rather than the syntax level.
- **Environment setup and dependency troubleshooting** — Built a Python virtual environment, installed `paho-mqtt`, `aiocoap`, `asyncua`, `matplotlib`, `numpy`, `pandas`. Hit and resolved a breaking-change issue in `paho-mqtt` 2.x's callback API by specifying the correct `callback_api_version` in the client initialization.
- **Cross-protocol debugging** — Resolved Matplotlib threading conflicts on macOS where network callbacks ran on background threads but graphical updates required the main thread. The fix was separating data collection from visualization logic.
- **Security hardening** — Replaced unsafe `eval()` JSON parsing with `json.loads()` to mitigate the injection risk inherent in treating external data streams as trusted input.

## What I Learned

- **MQTT's publish/subscribe model decouples producers from consumers.** Sensors publish to topics; subscribers consume through a centralized broker (Mosquitto). This decoupling allows horizontal scaling without direct dependencies, ideal for cloud-integrated IoT and high-frequency telemetry.
- **CoAP is HTTP-shaped but UDP-light.** Designed for resource-constrained devices, it reduces overhead while maintaining a familiar request/response model. Successful 2.04 Changed response codes confirmed the implementation worked.
- **OPC UA enforces structure where MQTT and CoAP are flexible.** Namespace registration, typed variables, organized object modeling — this rigidity is exactly what manufacturing and Industry 4.0 environments need for interoperability.
- **Failures in distributed systems are usually architectural, not syntactic.** The most useful mindset shift this lab produced: when a script fails, ask whether a required component is missing or misconfigured before assuming the syntax is wrong.

## Challenges I Faced

The most architecturally instructive bug was the CoAP connection failure. The lab provided a CoAP client but no corresponding server. Unlike MQTT (which uses an external Mosquitto broker) or OPC UA (which embeds a server in the script), CoAP requires both endpoints to be explicitly implemented. Recognizing this gap took longer than fixing it — and that's the lesson: **the diagnosis is the hard part, not the patch**.

The `paho-mqtt` version-mismatch issue was a more conventional dependency problem but reinforced the same principle: production systems break in subtle ways when dependencies update without notice.

## Future Applications

In real IIoT deployments, security and authentication are non-negotiable. Future enhancements would include TLS/DTLS encryption layers, certificate management, latency benchmarking across protocols, persistent database logging, and integration with physical hardware like Raspberry Pi or Arduino sensors. The architecture-thinking developed here translates directly: securing protocols is itself an architectural concern, not a code-level patch.

## Files in This Folder

- `L04_Reflective_Report.pdf` — Full reflective report covering personal goals, contributions across all three protocol implementations, protocol analysis, challenges, and future applications.
