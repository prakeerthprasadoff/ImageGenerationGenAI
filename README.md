# Genre-Conditioned Album Cover Generation (cVAE)

MSAI 495 — Generative AI project.

Conditional VAE in PyTorch trained on the [20k Album Covers Within 20 Genres](https://www.kaggle.com/datasets/michaeljkerr/20k-album-covers-within-20-genres) dataset. Generates album covers conditioned on a chosen music genre.

## Files
- `album_cvae.ipynb` — main notebook (run on Google Colab with GPU).
- `requirements.txt`
- `GAID/` — dataset (not committed). Layout: `GAID/<Genre>/*.jpg`.

## Run
1. Upload `GAID.zip` to Google Drive.
2. Open the notebook in Colab, pick a GPU runtime.
3. Run all cells.

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
