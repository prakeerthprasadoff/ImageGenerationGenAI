# Genre-Conditioned Album Cover Generation (cVAE)

MSAI 495 — Generative AI project.

Conditional VAE in PyTorch trained on the [20k Album Covers Within 20 Genres](https://www.kaggle.com/datasets/michaeljkerr/20k-album-covers-within-20-genres) dataset. Generates album covers conditioned on a chosen music genre.

## Files
- `album_cvae.ipynb` — main notebook (Running on Quest).
- `requirements.txt`
- `GAID/` — dataset (not committed). Layout: `GAID/<Genre>/*.jpg`.


## Sections in the notebook
1. Data loading
2. cVAE model
3. Training
4. Latent space exploration / interpolation
5. Hyperparameter tuning (Hyperband)
6. Gradio GUI


Update 04/28
Ran model in google colab only for it to crash so configured quest and now training the model on quest


Update 05/01
Ran and tried some parameters on the conditional VAE but not entirely happy with the results so trying more params + looking into diffusion architectures


Update 05/02
The following is the output received from conditional VAE.
<img width="935" height="284" alt="image" src="https://github.com/user-attachments/assets/c2f0dfb3-872a-44b1-ab09-de53d382d40d" />


The following is the output recevied from Diffusion models.
<img width="923" height="154" alt="image" src="https://github.com/user-attachments/assets/e616a8d9-3407-4d99-8ecd-e1cd66bbeb0c" />

It seems that conditonal VAEs might be better. Trying to better the outputs and look into other architectures. Also analysing why this could be the case

