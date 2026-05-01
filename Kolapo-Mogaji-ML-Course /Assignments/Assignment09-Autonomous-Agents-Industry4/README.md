# Assignment 09 — Autonomous Agents in Industry 4.0

> **Case Study Analysis: Hjulström (2022) — DDQN-Based Self-Optimizing Warehouse AGVs**

## The Problem

Traditional automated guided vehicles (AGVs) in warehouses follow rigid, marker-based paths — fast and reliable, but inflexible. When the warehouse layout changes, AGVs need re-engineering, not retraining. Hjulström's KTH master's thesis (2022) explores a concrete alternative grounded in Industry 4.0 thinking: replace marker-following AGVs with self-optimizing learning agents that can adapt routes and manage their own batteries without centralized control.

This assignment was a critical analysis of that thesis — examining the implementation, evaluating the results, and reflecting on what the work means for autonomous systems in production environments.

## What the Original Work Did

Hjulström modeled a 10×10 grid-world warehouse with three AGVs, three task pickup/dropoff locations, and two charging stations. Each agent observes its own coordinates, target task square, current battery level, and the status of its four adjacent cells, and outputs one of four movement actions.

Learning was driven by a **Double Deep Q-Network (DDQN)** implemented in TF-Agents on TensorFlow:
- Q-network: three 100-neuron hidden layers
- Optimizer: Adam at learning rate 10⁻⁵
- Training: 200,000 episodes with a curriculum that gradually raised tasks per episode from two to six

The reward structure encodes the dual objective directly:

| Event | Reward |
|---|---|
| Task completion | +100 |
| Battery depletion | −100 |
| Collision | −70 |
| Well-timed recharge | +50 |
| Unnecessary recharge | −10 |
| Per step | −1 |

In a 300-task evaluation run, the trained agents completed every assigned task with **zero collisions and zero battery depletions**, taking only **2.59 extra steps per task** on average above the theoretical minimum.

## My Analysis

### Benefits

- **Concrete, measurable results.** Zero failures across 300 tasks is not just statistically good — it's a deployment-relevant signal.
- **Emergent trade-off management.** The most fundamental result: the agents learned to balance two competing objectives (finishing tasks quickly vs. recharging in time) without that trade-off being hand-coded. They discovered when to prioritize each.
- **Validates the Industry 4.0 claim.** Decentralized, learning-based control can replace centralized scheduling for AGV fleets — at least in simulation, with the right reward shaping.

### Honest Limitations (the author flagged most of these)

- **Simulation only.** No physical AGV deployment. Idealized batteries that drain at constant rate and recharge instantly. Static obstacles, no moving objects.
- **Sequential motion.** Agents move one at a time, sidestepping the harder problem of real-time concurrent collision avoidance.
- **Training cost.** 200,000 episodes is significant compute. The unstable-learning oscillations endemic to deep RL are present.
- **Library setup time.** A familiar friction point in applied ML.

### Future Implications I Drew Out

The most promising extensions:
1. **Treat charging stations themselves as intelligent agents** that coordinate queuing and recharge duration
2. **Sim-to-real transfer using digital twins** of actual factory layouts before physical deployment
3. **Scaling to larger environments** with concurrent motion and richer task scheduling

Combined with cloud-accelerated training, this points toward AGV fleets that can be retrained for new factory configurations in **hours rather than re-engineered over months** — a step change in manufacturing flexibility.

## My Reflection

Reading Hjulström's thesis sharpened my view of what "autonomous" actually requires. **Before, I thought of reinforcement learning as primarily a clever optimization technique; after, I see it as a way to encode trade-offs that an engineer cannot fully specify in advance.** The reward structure here — six separate components carefully weighted — does most of the intellectual work, and the DDQN agent simply finds a policy that respects it. That insight transfers directly to my own IIoT and edge-AI projects: **defining the reward landscape is the hard part, not the learning algorithm.**

What also stuck with me was the gap between "the simulation works" and "the system is deployable." The author is candid that idealized batteries, sequential motion, and a fixed map all simplify the real problem dramatically. For someone building production tools, this is a useful corrective — RL successes in simulation are necessary but not sufficient evidence that a system will hold up in a real factory.

**Sim-to-real transfer is where the engineering rigor really starts.** The thesis is honest enough to make that case for itself.

## Files in This Folder

- `A09_Case_Study.pdf` — Full case-study analysis covering implementation details, benefits, challenges, future implications, and personal reflection.

## Reference

- Hjulström, L. (2022). *Self-optimizing AGVs in warehouse environments: A reinforcement learning approach*. Master's thesis, KTH Royal Institute of Technology.
