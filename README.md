# Digit Recognizer (MNIST)

Educational project: Kaggle **Digit Recognizer** competition. Path from a simple tabular baseline (CatBoost) to MLP and then CNN.

> This repository is intentionally lightweight. All experimentation lives in notebooks, and no attempt is made to provide a production-ready package, automated tests, or CI.

## Progress

- **CatBoost baseline:** 0.96328  
- **MLP baseline:** 0.97703  
- **Improved MLP (with seed averaging):** 0.99367 *(without seed averaging:  0.994)*
- **CNN_v1:** 0.99207  
- **CNN_v2 (final):** 🏁 **0.99560**  
- **Status:** competition completed


## Update — Improved MLP with Seed Averaging

Added a new notebook: `improved_mlp_with_seeds.ipynb`

This version significantly extends the baseline MLP with multiple practical improvements beyond architecture tweaks:

- Added **Dropout**, changed **activation function**, and applied **Kaiming initialization**
- Used **AdamW optimizer** with a **learning rate scheduler**
- Applied **data augmentation** and **Test-Time Augmentation (TTA)** for more robust inference
- Implemented **probability averaging across multiple random seeds**

> The final model averages class probabilities over several trained models with different seeds.  
> Despite this ensemble approach, in the Kaggle setup a single well-chosen seed achieved a slightly better score,  
> so future experiments continue from that version (without seed averaging) toward a compact CNN.


## Final step — CNN models

Added a new notebook: digit-recognizer-mnist-cnn.ipynb

This notebook contains two convolutional neural networks (CNNs) trained on the MNIST dataset.

- CNN_v1 — a baseline architecture without augmentations or additional techniques.
Achieved 0.99207 accuracy on the leaderboard.

- CNN_v2 — an improved version with BatchNorm, Dropout, GELU activation, Kaiming initialization, and a CosineAnnealingLR scheduler.
Trained on the entire training dataset without validation.
Final result — 0.99560.

During training, I experimented with various hyperparameters and methods — changing batch sizes, trying weight EMA, and TTA — but the final setup without these tricks achieved the best performance.

>This is the final version — the competition is now closed for further updates.


## Structure

- `notebooks/` — all notebooks (CatBoost, MLP, CNN)
- `submissions/` — Kaggle submission files
- `data/` — local competition data (ignored by git)
- `models/` — saved model weights (ignored by git)


## How to run locally

1. `pip install -r requirements.txt`  
2. Download `train.csv` / `test.csv` from the Kaggle competition and put them into `data/`  
3. Open any notebook in `notebooks/` to reproduce the experiments



