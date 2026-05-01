# Lab 03 — Deploying a CNN on a Simulated Edge Device

> **VS Code · TensorFlow · TFLite · Edge Impulse · Cortex-M4 simulation**

## What This Lab Was About

This lab took the conversion pipeline from Lab 02 and pushed it through to actual edge deployment, end-to-end. The goal was to land a trained MNIST CNN on a simulated Cortex-M4 target via Edge Impulse and validate inference on the simulated hardware. The work covered six distinct phases: environment setup, dataset preparation, model architecture, training, TFLite conversion, and Edge Impulse deployment. Terminal logs and screenshots were captured at each phase as documentation.

## What I Did

- **Environment setup** — Installed Python 3.10, VS Code 1.88, TensorFlow 2.15, Node.js 20 LTS, and the Edge Impulse CLI v1.20.0. Created an isolated virtual environment (`tf_env`) so TensorFlow wouldn't conflict with the system Python.
- **Dataset preparation** — Loaded MNIST via the Keras datasets API, normalized pixel values to [0.0, 1.0], and reshaped to add the single channel dimension required by `Conv2D` layers.
- **Model architecture** — Built a simple CNN suitable for the constrained edge target.
- **Training** — Ran training within the virtual environment, validated convergence, exported the model.
- **TFLite conversion** — Used the `TFLiteConverter` to produce a quantized flat-buffer model.
- **Edge Impulse upload and inference validation** — Pushed the converted model to Edge Impulse, deployed it to the simulated Cortex-M4 target, and verified inference results matched workstation expectations.

## What I Learned

- **The virtual environment pattern is non-negotiable for ML lab work.** A single global TensorFlow install gets corrupted the moment another project needs a different version. Adopting `tf_env`-style isolation as standard practice prevented an entire category of "works on my machine" problems.
- **Edge Impulse closes the gap between trained model and deployable artifact.** It handles the model upload, target selection, and simulated-hardware testing in a single workflow — far less friction than wiring those steps together manually.
- **Cortex-M4 is a constrained but capable target.** Even with the model quantized to TFLite, inference time and memory footprint matter. The conversion isn't free; you pay for the savings somewhere.

## Challenges I Faced

The biggest single time sink was the sequencing of CLI tool installations: Edge Impulse CLI requires Node.js, which had to be installed before the npm install would work; TensorFlow had to be installed *inside* the virtual environment, which itself had to be activated before pip would install anything to the right place. Getting the ordering wrong caused subtle errors that pointed at the wrong root cause.

The other challenge was confirming that the model running on the simulated Cortex-M4 was producing the same predictions as the workstation. A mismatch here would mean the conversion broke something — but matching outputs gave a strong signal that the deployment pipeline was sound.

## Files in This Folder

- `L03_Report.docx` — Full lab report with terminal logs, screenshots, and step-by-step documentation across all six phases. Embedded screenshots show the VS Code terminal sessions, Edge Impulse dashboard, and inference validation output.
