# Active-Probabilistic-Fast-Kernel-Extreme-Learning-Machine

This repository contains a Jupyter Notebook implementation of an active learning framework for ordinal regression using a fast Kernel-based Extreme Learning Machine (KELMOR) model. The project focuses on improving model predictions for ordinal ratings (e.g., bridge ratings) by iteratively adding informative samples based on uncertainty (entropy sampling) and comparing it with a random sampling baseline.

## Overview

The code performs the following steps:

1. **Data Preprocessing:**
   - **Loading Data:** Reads the dataset from `Final_Data.csv`.
   - **Feature Engineering:**
     - One-hot encodes categorical features (e.g., structure kind, type, deck structure type, and lowest rating).
     - Scales numerical features (e.g., ADT, span length, deck area, etc.) using MinMaxScaler.
   - **Data Splitting:**
     - Splits the data into training and testing sets based on the `CollectionYear` (training: years 2011–2020; testing: years 2021–2022).
     - Further divides the training set into an initial set (sampled proportionally by clusters) and a pool set for active learning.
   - **Target Adjustment:** Adjusts the target variable (`NEXT_LOWEST_RATING`) by subtracting a constant (3 in this case) to standardize ratings.

2. **Fast KELMOR Model:**
   - Implements an **incomplete Cholesky decomposition** to approximate the kernel matrix efficiently.
   - Defines the `kelmor` class:
     - **Initialization:** Accepts a kernel type (e.g., linear or RBF) and a regularization parameter `C`.
     - **Fit Method:** Computes the kernel matrix using scikit-learn’s `pairwise_kernels`, applies the incomplete Cholesky decomposition, and learns a coefficient vector (`beta`).
     - **Inference Method:** Predicts outputs by computing the kernel between new data and training data, then applies a soft-max function to obtain class probabilities.
   - Uses a linear kernel with `C = 5` (determined by a grid search).

3. **Active Learning Framework:**
   - **Entropy Sampling:**
     - Computes the entropy of the predicted probability distribution for each structure in the pool set.
     - Selects structures with the highest uncertainty based on the entropy value, ensuring that selections are proportional to their representation in clusters.
   - **Random Sampling (Baseline):**
     - Randomly selects structures from the pool set.
   - **Iterative Querying:**
     - In each query round, new samples are added to the training set.
     - The model is retrained, and performance is evaluated using several metrics.
   - **Evaluation Metrics:**
     - **Ranked Probability Score (RPS)**
     - **Accuracy**
     - **Precision**
     - **Recall**
     - **F1-Score**
     - **Somers' D**
     - **Confusion Matrices**
   - Saves the entropy sampling metrics to an Excel file (`entropy_sampling_metrics.xlsx`) for further analysis.

4. **Visualization:**
   - Compares the RPS performance over cumulative numbers of sampled bridges for both entropy and random sampling methods using Matplotlib.

## Project Structure

- **Data Loading & Preprocessing:**
  - Loads and preprocesses the data from `Final_Data.csv`.
  - Splits the dataset into training, initial, pool, and test sets.
- **Model Implementation:**
  - Implements the `incomplete_cholesky` function.
  - Defines the `kelmor` class for training and inference.
- **Active Learning:**
  - Contains two sampling methods:
    - `entropy_sampling_for_structure` for entropy-based active learning.
    - `random_sampling_by_structure` for random baseline sampling.
  - Includes functions `run_sampling_method` and `run_sampling_method_random` to perform iterative sampling and model updating.
- **Evaluation & Visualization:**
  - Calculates performance metrics after each query.
  - Saves metrics to an Excel file.
  - Generates plots to compare the sampling strategies.

## Requirements

- **Python 3.7+** (tested on Python 3.11)
- **Jupyter Notebook** or a similar environment for running the notebook/script.
- **Python Packages:**
  - `numpy`
  - `pandas`
  - `scikit-learn`
  - `scipy`
  - `matplotlib`

Install the required packages via pip:

```bash
pip install numpy pandas scikit-learn scipy matplotlib
