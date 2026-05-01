# Lab 02 — AI Model Conversion & Deployment

> **TFLite, MNIST, the Sim-to-Real Workflow**

## What This Lab Was About

This lab walked through the full path of taking a trained neural network from a workstation environment to a deployable artifact for a resource-constrained edge device. The model was a feedforward CNN trained on the MNIST handwritten-digit dataset; the deployment target was a TensorFlow Lite (`.tflite`) flat-buffer suitable for hardware like a Jetson Nano or Raspberry Pi.

The point was less the model itself (MNIST is a solved problem) and more the **engineering pipeline** around it: data normalization, layer architecture, model serialization, conversion via the TFLite converter, and the sanity-check needed when feeding new data into a pre-allocated TFLite interpreter.

## What I Did

- Loaded MNIST (70,000 grayscale 28×28 images) via `tensorflow.keras.datasets.mnist`
- Normalized pixel values from [0, 255] to [0, 1] to make the loss surface more well-behaved
- Built a Sequential model: Flatten → Dense(128, ReLU) → Dense(10, Softmax)
- Trained on the workstation, then ran `TFLiteConverter` to produce a quantized `.tflite` artifact
- Wrote inference code that loads the converter output and runs predictions through the TFLite interpreter, including the `np.expand_dims` step needed to match the model's expected input shape

## What I Learned

- **The "Sim-to-Real" pipeline is its own discipline.** Training on a workstation with abundant compute and then "distilling" the model for an edge device is the standard pattern. Both halves matter; neither is enough alone.
- **Optimization vs. accuracy is a real trade-off.** The TFLite conversion preserves the model's intelligence while shrinking memory and accelerating inference — but the conversion itself is where edge cases hide (legacy `.h5` warnings, batch-dimension mismatches, version-incompatible interpreters).
- **The TFLite interpreter is more than a model loader.** Its `allocate_tensors()` step pre-allocates memory deterministically — critical for devices with limited RAM where dynamic allocation would crash the system.

## Challenges I Faced

The most useful debugging moment was an input-shape mismatch error from the TFLite interpreter. The converter expected a 4D tensor (batch, height, width, channels) but I was feeding it a single 28×28 image. The fix was a one-line `np.expand_dims(image, axis=0)` to add the batch dimension — but the lesson was bigger: the runtime contract of a deployed model is more brittle than the training-time API. Forgetting this is exactly the kind of bug that surfaces only after deployment.

A separate friction point was Keras's deprecation warning about the `.h5` save format. I learned that `.h5` is widely compatible for TFLite conversion but that the modern Keras-native `.keras` format is the current industry standard for model persistence.

## Files in This Folder

- `L02_Conceptual_Report.docx` — Engineering decisions and rationale across the full pipeline (data → architecture → training → conversion → deployment)
- `L02_Reflective_Journal.docx` — Personal reflection on challenges, learning outcomes, and real-world AI deployment implications
- `L02_Notebook_Export.html` — HTML export of the working Jupyter notebook with code cells and outputs
