# Machine learning notebooks

This repository is a progressive set of Jupyter projects: from classical linear models and cross-validation through generative classifiers, logistic regression and neural networks, and finally transformer-based text models. The overarching goal is to **implement core methods in code**, **validate them against trusted libraries** (mainly scikit-learn and Keras/TensorFlow), and **report how design choices affect bias–variance, stability, and generalization**.

Python dependencies are pinned in `requirement.txt` (install with `pip install -r requirement.txt`). Many notebooks expect their local `data/` folders and downloaded assets to be present.

---

## Module 1 — `assignment_1/`

**Focus:** Supervised learning for **regression**: model structure, regularization, and honest evaluation.

- **Part 1 — Polynomial and linear regression**  
  Pipelines with polynomial features, ridge-style stabilization via normal equations, **k-fold cross-validation** for choosing complexity, and learning-curve style analysis. Outputs include CV error vs. polynomial degree and fitted vs. raw data plots (see `out_q1_simple/`, `out_q2_simple/`).

- **Part 2 — Robust and penalized linear models**  
  Comparisons on tabular data (e.g. bundled CSVs under `data/`), including performance summaries and **regularization paths** (RMSE and weight shrinkage vs. λ).

- **Part 3**  
  Continued regression experiments aligned with the same tooling (fold-wise preprocessing to avoid leakage).

- **Part 4 — Real tabular dataset**  
  **Wine quality** (UCI-style red wine features → quality score): loading, modeling, and interpretation in a more realistic setting.

- **`part5.ipynb`**  
  Supplementary notebook extending the same regression/CV patterns (e.g. wine data loading and splits).

**Goal:** Build intuition for **when linear/polynomial models help**, how **CV** guards against overfitting, and how **regularization** trades fit against stable weights.

---

## Module 2 — `assignment_2/`

**Focus:** **Generative classifiers** — Gaussian Discriminant Analysis (GDA) and **Naive Bayes** — with systematic comparison to scikit-learn.

- **Problems 1–3 — GDA**  
  1D and multivariate **two-class** GDA, then **K-class** GDA on continuous features (Iris), including log-posterior scoring, covariance handling, and **10-fold CV**.

- **Problem 4 — Naive Bayes for text**  
  **SMS spam** classification: text loading, vocabulary construction, **Bernoulli** bag-of-words features, training and evaluation.

- **Problem 5 — Count-based Naive Bayes**  
  **Word-count** (multinomial-style) features, derived likelihoods, and alignment with `MultinomialNB`.

- **Problems 6–7**  
  Side-by-side metrics against **LDA**, **BernoulliNB**, and **MultinomialNB**; short summary of findings and numerical stability (e.g. covariance regularization).

**Goal:** Understand **class-conditional modeling**, **priors**, and **discrete vs. count text features**, and verify from-scratch code against standard implementations.

---

## Module 3 — `assignment_3/`

**Focus:** **Discriminative** models and deep learning: **logistic regression**, **MLPs**, **Keras** text models, and **CNNs** on images.

- **Problem 1 — Logistic regression**  
  Binary and multiclass formulations (including **softmax**), **polynomial features**, **10-fold CV**, and checks against sklearn.

- **Problem 2 — Two-layer MLP**  
  **Backpropagation** (including comparing loss choices such as MSE vs. cross-entropy in the derivation), implementation of a small MLP, hyperparameters (hidden size, learning rate), and **`MLPClassifier`** comparison.

- **Problem 3 — IMDB sentiment (Keras)**  
  **Bag-of-words / one-hot** pipelines vs. **embedding** models, plus **regularization** (dropout, early stopping, L2) and validation-driven tuning.

- **Problem 4 — CIFAR-10 CNN**  
  Convolutional baseline with training curves; emphasis on **validation metrics** and **learning-rate scheduling** (e.g. `ReduceLROnPlateau`).

Artifacts such as `best_model.keras`, `run_log.txt`, and `run_plots/` support reproducibility and reporting.

**Goal:** Connect **classical optimization** (gradient-based training) to **modern feedforward and convolutional nets**, and practice **text** and **image** pipelines end to end.

---

## Module 4 — `assignmet_4/`

*(Directory name is spelled as shown in the repo.)*

**Focus:** **Transformer** models for **IMDB** sequence classification in TensorFlow/Keras, with both high-level and custom components.

- **Problem 1 — Data preparation**  
  IMDB sequences, padding, splits, and reproducible seeds; explores **`keras_hub`** transformer encoder blocks in a full model.

- **Problem 3 — Custom transformer block**  
  A hand-built **encoder-style** block: multi-head attention, feed-forward sublayer, residuals, layer normalization, and dropout—wired into the IMDB training loop, with notes on head count, depth, and overfitting/underfitting.

**Goal:** Move from fixed-length **bag-of-words** views of text to **sequence models**, and understand how **attention-based** stacks behave in practice on a standard benchmark.

---

## How the pieces fit together

| Direction | Module 1 | Module 2 | Module 3 | Module 4 |
|-----------|----------|----------|----------|----------|
| *Paradigm* | Regression / curve fitting | Generative (Bayes, GDA) | Discriminative + deep nets | Sequence models (Transformers) |
| *Data* | Synthetic + tabular + wine | Iris + SMS spam | Tabular + digits + IMDB + CIFAR-10 | IMDB sequences |
| *Core skill* | CV, polynomials, ridge | Priors, likelihoods, text vectors | MLP backprop, Keras, CNNs | Attention, encoder stacks |

Together, these modules form a single narrative: **sound experimentation** (splits, CV, baselines), **implementation literacy** (not only calling APIs), and **clear reporting** of validation vs. test performance and training dynamics.
