# CelebA Conditional Diffusion Model

A conditional diffusion model trained on CelebA that generates 64×64 face images from user-selected facial attributes.

---

## Overview

This project implements a **denoising diffusion probabilistic model (DDPM)** conditioned on CelebA's 40 binary facial attributes (e.g. *Smiling*, *Blond hair*, *Eyeglasses*). At inference time, you select any combination of attributes and the model generates realistic faces matching those conditions.

---

## Installation & Running

The entire project lives in a single Jupyter notebook. To launch the GUI locally, just open the notebook and **run the last cell** — it starts a Gradio interface in your browser automatically.

You'll need the CelebA dataset and the trained checkpoint on your machine. Make sure the paths at the top of the notebook point to where you've saved them.

Or just use the deployed version — no setup needed:

👉 **[Try it on Hugging Face Spaces](https://huggingface.co/spaces/prakeerthprasad/ImageGenerator)**

---

## Results

Sample faces generated with the *Young woman* preset (`Young`, `Attractive`, `Blond hair`, `Smiling`, `Heavy makeup`):

<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/aca2bba1-d4bb-428d-9950-c142d23e9600" />


The model was trained for 200 epochs on CelebA. Best checkpoint selected at **epoch 120** based on FID score (99.14) — validation loss peaked later at epoch 200 but visual quality had already plateaued.

---

## Extra Criteria

**Attribute-conditioned generation + deployed React/Vite frontend**

- The UNet is conditioned on all 40 CelebA binary attributes via a learned MLP that fuses sinusoidal time embeddings with the attribute vector at every residual block.
- An EMA (exponential moving average) copy of the network is kept throughout training and used at inference for more stable, higher-quality outputs.
- A **React + Vite** frontend was built and deployed on Hugging Face Spaces. It lets you pick any combination of the 40 attributes using pill toggles, use one-click presets, control the number of images and denoising steps, and see the results in a live gallery — all in the browser, no local setup needed.

---

## Difficulties & Solutions

| Difficulty | Solution |
|---|---|
| Early training loss spike dominated loss plots | Used log-scale y-axis and percentile clipping to make the convergence curve actually readable |
| Val loss and FID disagreed on best checkpoint | Trusted FID over val loss — epoch 120 produced better images even though epoch 200 had lower noise MSE |
| Checkpoint layer names mismatched when loading into GUI | Traced the mismatched keys (`downsample` vs `ds`, `upsample` vs `us`) and restored the original names from training |
| Gradio checkbox labels clipping at narrow widths | Rewrote the attribute panel with custom CSS pill toggles using `white-space: nowrap` and a flex-wrap layout |
