# CAWI: Copula–Aligned Weight Initialization for Randomized Neural Networks

Mushir Akhtar, M. Tanveer, & Mohd. Arshad
CAWI: Copula-Aligned Weight Initialization for Randomized Neural Networks
Proceedings of the 29th International Conference on Artificial Intelligence and Statistics (AISTATS 2026)
https://openreview.net/forum?id=fwqydIjLn6

---

## OVERVIEW

This repository provides the official MATLAB implementation of CAWI (Copula-Aligned Weight Initialization), proposed in our AISTATS 2026 paper.

Randomized neural networks (e.g., RVFL) rely on fixed random input-to-hidden weights. Standard i.i.d. initializations ignore inter-feature dependence, which can distort hidden projections and degrade performance.

CAWI addresses this limitation by sampling hidden weights from a data-fitted copula that matches the empirical dependence structure of the input features. This preserves dependence-aware projections while retaining the closed-form training advantage of randomized neural networks.

---

## HOW CAWI WORKS (high level):


Fit a copula to rank-transformed training features (pseudo-observations).

Sample each column w_j of W from the fitted dependence.

Apply a fixed inverse marginal transform (e.g., standard normal or uniform) to set scale.

Training remains backpropagation-free with a closed-form readout (ridge).
a.

---

## IMPLEMENTATION SCOPE

This repository contains the reference implementation of CAWI for:

* Random Vector Functional Link Network (RVFL)

Supported weight initializations:

Baseline:

* i.i.d. Uniform initialization

CAWI (Elliptical copulas):

* Gaussian
* t

CAWI (Archimedean copulas):

* Clayton
* Frank
* Gumbel

---

## ⚙️EXPERIMENTAL SETUP

All the experiments are implemented using MATLAB R2023a and executed on a Windows 10 PC equipped with an Intel(R) Core(TM) i7-6700 CPU @ 3.40GHz (4 cores, 8 logical processors) and 16 GB RAM. Each dataset is preprocessed by normalizing the input features to have zero mean and unit variance. A $5$-fold cross-validation procedure is employed to ensure reliable and unbiased evaluation. In each fold, the dataset is split into $80\%$ training data and $20\%$ testing data. For every combination of hyperparameters, the model is trained on the training data and evaluated on the testing data across all $5$ folds. The testing accuracy is recorded for each fold. The final testing accuracy for each dataset is computed as the mean testing accuracy across the five folds, providing a robust estimate of the model's performance.

To eliminate any possibility of data leakage, all copula estimation steps are performed strictly within each training split. For every fold, the pseudo-observations and copula parameters are computed exclusively using the training features of that fold. The fitted copula is then used to sample the hidden-layer weights, which are subsequently evaluated on the disjoint test set. At no stage is information from the test portion used during copula fitting or weight initialization.

Hyperparameter tuning is performed using a grid search strategy to identify the optimal settings for each model. For each model, the regularization parameter (\( \lambda \)) is selected from \( \{10^i \mid i = -6, -5, \ldots, 6\} \). For RVFL, the number of hidden nodes (\( h \)) varies from \( [3:20:203] \), and seven activation functions (Sigmoid (1), Sine (2), Tribas (3), Radbas (4), Tansig (5), ReLU (6), and SELU (7)) are evaluated. 


---

## 📂 DATASETS

Dataset loaders assume .mat or .txt formats.

* Dataset directories are specified via placeholders in scripts
* Replace paths with your local dataset locations
* Result directories can be similarly configured

---

## HOW TO RUN

1. Place datasets in your local data directory
2. Update dataset and result paths in scripts
3. Select copula type and RVFL settings
4. Run the main experiment script

---

## CITATION

If you use this code, please cite:

@inproceedings{akhtar2026cawi,
title={CAWI: Copula-Aligned Weight Initialization for Randomized Neural Networks},
author={Akhtar, Mushir and Tanveer, M. and Arshad, Mohd.},
booktitle={Proceedings of the 29th International Conference on Artificial Intelligence and Statistics},
year={2026},
url={[https://openreview.net/forum?id=fwqydIjLn6}](https://openreview.net/forum?id=fwqydIjLn6})
}

---

## CONTACT

For any questions or issues related to the code or paper, please contact at phd2101241004@iiti.ac.in

---
