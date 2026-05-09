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

**[Try it on Hugging Face Spaces](https://huggingface.co/spaces/prakeerthprasad/ImageGenerator)**

---

## Results

Sample faces generated with the *Young woman* preset (`Young`, `Attractive`, `Blond hair`, `Smiling`):

<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/aca2bba1-d4bb-428d-9950-c142d23e9600" />


The model was trained for 200 epochs on CelebA. Best checkpoint selected at **epoch 120** based on FID score (99.14) — validation loss peaked later at epoch 200 but visual quality had already plateaued.

---

## Extra Criteria

**Attribute-conditioned generation + deployed React/Vite frontend**

- The UNet is conditioned on all 40 CelebA binary attributes via a learned MLP that fuses sinusoidal time embeddings with the attribute vector at every residual block.
- An EMA (exponential moving average) copy of the network is kept throughout training and used at inference for more stable, higher-quality outputs.
- A **React + Vite** frontend was built and deployed on Hugging Face Spaces. It lets you pick any combination of the 40 attributes using pill toggles, use one-click presets, control the number of images and denoising steps, and see the results in a live gallery — all in the browser, no local setup needed.

---

## Difficulties
 
The biggest challenge was getting any model to produce decent generations at all. I started with an **album art cover dataset** and trained a WGAN, GAN, cVAE, and a diffusion model on it — none of them produced satisfying results despite a lot of hyperparameter tuning, architecture tweaks, and multiple training runs. Album art is just too visually diverse for these model sizes to learn a coherent distribution.
 
After spending a significant amount of time on that, I switched to **CelebA**, which has much more structural consistency across images. I then trained a WGAN (including a variant using only 6 attributes capped at 75k images), a VAE, and a diffusion model, and compared them side by side. The diffusion model was clearly the best of the three visually, so I stuck with it and focused on making it conditional on attributes.
 
To save time across all these experiments, I ran **6 notebooks in parallel on the same node**, each with a different model configuration. This let me compare results across architectures and hyperparameter settings much faster than training them sequentially would have allowed.
 
