# Lab 07 — AoI–Reliability Trade-off in Heterogeneous IIoT Networks

> **Data-Driven Analysis · Random Forest · Multi-Output Neural Network · 10,000 Simulated Network Observations**

This was the most analytically demanding lab in the course. It combines a literature review of a recent IIoT communications paper with a hands-on data-driven study that corroborates the paper's analytical findings on a simulated dataset.

## The Problem

Industrial IoT networks frequently serve two coupled traffic classes that share an unreliable wireless channel:

- **AoI-oriented traffic** (periodic monitoring, generate-at-will, no retransmissions) — the design objective is *fresh information*. **Age of Information (AoI)** measures the time elapsed since the most recently received packet was generated.
- **Deadline-oriented traffic** (safety-critical events, retransmitted to a hard deadline `D`) — the design objective is *high reliability*. **Packet Loss Probability (PLP)** measures the fraction of deadline-class packets dropped without successful delivery.

The two objectives compete for the same channel. Farag, Ali, and Stefanović (2023) analyzed this trade-off via a Discrete-Time Markov Chain and showed it's governed primarily by access probabilities and the SINR capture threshold γ. This lab applies machine learning to a simulated dataset to quantify the practical structure of that trade-off.

## My Approach

### Dataset
10,000 simulated network observations with five configuration features (transmission probability, capture threshold γ, number of contending nodes, channel quality, traffic type) and two outcome variables (AoI, PLP). Approximately 14% of rows exhibited infinite AoI, concentrated at low channel quality — consistent with the paper's `Δ̄ = 1/qAoI` divergence regime. **I filtered these from the regression target rather than capping** so the model wouldn't artificially inflate its R² by hiding the failure regime.

### Method
- AoI was log-transformed (`log1p`) before training to handle the heavy tail (median ≈ 19, max ≈ 5.3 × 10⁴ slots in the finite subset)
- 80/20 train-test split, random seed 42
- Features standardized with `StandardScaler` fit on training data only
- **Random Forest regressor** (200 trees, `min_samples_leaf=2`) predicting log-AoI
- **Multi-output Keras neural network** (5 → 64 → 32 → 2, ReLU, dropout, Adam) jointly predicting AoI and PLP from a shared representation, with early stopping on validation loss
- 5-fold cross-validation on the Random Forest for stability checking

## Key Findings

**Pattern 1 — Channel quality and access probability jointly determine AoI; neither dominates.** The Random Forest's three top features are tightly bunched: transmission probability (0.34), num_nodes (0.28), channel quality (0.25). This contradicts a naïve "one knob dominates" intuition and confirms the paper's core mechanism: AoI is shaped by the *interaction* of access policy, contention, and link quality.

**Pattern 2 — A non-trivial fraction of operating points produce diverging AoI.** ~14% of configurations yield Δ̄ → ∞, almost all clustered at `channel_quality < 0.2`. Production deployments must monitor for this regime explicitly using AoI violation probability — *averages of finite values will silently miss it*.

**Pattern 3 — AoI-oriented traffic is not isolated from deadline-class behavior.** Despite the no-retransmission policy on the AoI class, median AoI was similar across both classes (~19 slots) and the upper tail was *heavier* for the AoI class — the deadline class starves it during backlog.

## Model Performance

| Model | Target | Test R² |
|-------|--------|---------|
| Random Forest | log(AoI) | **0.61** (5-fold CV: 0.64 ± 0.04) |
| Neural Network | AoI | 0.67 |
| Neural Network | PLP | **0.91** |

The striking PLP R² of 0.91 says something practically useful: **PLP is far more predictable from configuration alone than AoI is**. Deployment engineers can estimate reliability from configuration but must measure freshness online.

## What These Results Mean — Two Recommendations

**Strategy 1: Class-aware access probability scheduling.** Tune `p₁` (deadline class) and `p₂` (AoI class) independently rather than as a single network-wide MAC parameter. At low γ, raising `p₂` is a free improvement to AoI; at high γ, it inflates PLP and must be held back. Requires central scheduling (TSCH/6TiSCH-style) — pure ALOHA cannot implement this.

**Strategy 2: RF-quality–conditional retransmission for the deadline class.** Modify retransmission policy to yield the slot when estimated post-retry success × remaining slack falls below a threshold. The vanilla deadline-class policy retransmits regardless, clogging the channel in poor-quality regimes without saving the packet. Reduces wasted transmissions; depends on accurate online channel-quality estimation.

## Real-World Applications

- **Predictive maintenance on a CNC spindle.** A vibration sensor streams condensed features to an edge controller every few ms (pure AoI traffic). A 50 ms stale view during a feed-rate adjustment can mean a chipped tool. AoI–PLP awareness shifts the design specification from worst-case packet rate to a target distribution `P(Δ > 5) < 0.01`.
- **Gas-leak detection in a chemical plant.** Rare alarm packets (deadline class, 50 ms hard deadline) coexist with continuous concentration samples (AoI class). Without trade-off awareness, an engineer might raise everyone's transmission probability to "improve reliability" — but at high γ this *worsens* alarm PLP. Strategy 1 protects the alarm class with priority scheduling.

## Limitations and Future Work

- The simulated dataset uses an idealized channel model; production traffic includes burstiness, fading, and interference that aren't fully captured
- The neural network's R² for AoI is bounded by the same fundamental unpredictability that affects the Random Forest — future work could explore sequence models that exploit time-series structure
- Real deployment would require online estimation of channel quality, which itself introduces noise into Strategy 2

## Files in This Folder

- `L07_Report.pdf` — Three-page technical report with methodology, findings, recommendations, and references to peer-reviewed work
- `L07_Notebook.ipynb` — Working Jupyter notebook with the full data pipeline, feature engineering, model training, evaluation, and visualization. **GitHub renders this directly — click to view code, outputs, and plots in the browser.**

## How to Run

```bash
cd Labs/Lab07-AoI-Reliability
jupyter notebook L07_Notebook.ipynb
```

### Dependencies

```
numpy
pandas
scikit-learn
tensorflow
matplotlib
seaborn
```

## References

- Farag, H., Ali, S. M., & Stefanović, Č. (2023). On the Analysis of AoI-Reliability Tradeoff in Heterogeneous IIoT Networks. *arXiv preprint arXiv:2311.13336*.
- Sun, Y., Uysal-Biyikoglu, E., Yates, R. D., Koksal, C. E., & Shroff, N. B. (2017). Update or wait: How to keep your data fresh. *IEEE Trans. Inf. Theory*, 63(11), 7492–7508.
- Breiman, L. (2001). Random Forests. *Machine Learning*, 45(1), 5–32.
