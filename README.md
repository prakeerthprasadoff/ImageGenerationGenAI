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

Update 05/02- 05/05
I've been trying multiple different configurations of VAEs, GANs, and Diffusion models. None of the results are satisfactory. I tried making the networks deeper, tried different pre processing techniques on the images, and still the result didn't improve. Finally to make sure that the number of classes wasn't overwhelming the model, I cut down to just one class "Rock" and tried training the GANs, WGANs, Diffusion models, and VAEs (also tried tuning hyper parameters like learning rate, diffusions schedules-used cosine and offset cosine) but still no improvement.

These are my generated album covers for epochs 500, and 1000 using the diffusion model with an offset cosine diffusion schedule with 10 denoising steps(you had suggested).
<img width="1308" height="1354" alt="image" src="https://github.com/user-attachments/assets/eff4ba44-a46a-47db-80d3-376667c05a8b" />

<img width="1338" height="1336" alt="image" src="https://github.com/user-attachments/assets/4a216364-6512-43dd-ba34-389892b0734f" />


and the following is the actually expected album covers.
<img width="1302" height="1280" alt="image" src="https://github.com/user-attachments/assets/1066c1e9-4723-42df-b7cf-3b8b7f9df198" />



I also tried using WGANs, the output of which is follows:
<img width="1316" height="1318" alt="image" src="https://github.com/user-attachments/assets/80f75765-85a6-4846-b188-318111cdb534" />

And hence I am moving to another dataset. I have found some interesting ones. I will finalise and update the latest dataset that I am using today. (Update for 05/06)


Update 05/06
I have selected CelebA dataset. https://www.kaggle.com/datasets/jessicali9530/celeba-dataset
The dataset has ~200k pictures of celebrities in which they are annotated with attributes like bald, bangs, etc. The idea is to train a model to be able to regenerate these images conditioned on these attributes so that i can create a GUI where we can select features of the person required and it will generate a unique image including the features selected.

Update 05/06
I am currently training a WGAN-GP, a conditional VAE, diffusion model on the dataset and a WGAN-GP which is capped with 6 features and 75k images, all parallely. 

Update 05/07
The new dataset was not performing very well on the WGAN. As in, the training is going pretty well. But in the testing phase, the model was not able to learn attributes very well. The WGAN that was capped at 6 features did learn some attributes pretty well.

The Blond_Hair and Eyeglasses feature isn't perfectly learned here.
<img width="359" height="363" alt="image" src="https://github.com/user-attachments/assets/f37f7682-4742-4e35-b7e6-042ed2f77e8c" />

This picture did pretty well though.
<img width="345" height="350" alt="image" src="https://github.com/user-attachments/assets/87cded86-fd5e-4abc-b2e2-079b67a64722" />

I am continuing with the diffusion model which i feel is doing better in terms of performance.
A generation for a young, bald, male who is smiling looks as follows :

<img width="985" height="504" alt="image" src="https://github.com/user-attachments/assets/7527b3c0-0986-42da-b68b-96ca457ca262" />

Even though it may not be as clear as the WGAN, it learns the features better. It is currently training for more epochs right now.

