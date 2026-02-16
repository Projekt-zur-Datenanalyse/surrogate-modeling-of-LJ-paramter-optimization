# Surrogate Models for Molecular Dynamics Simulations

Molecular Dynamics (MD) simulations provide highly accurate insights into complex physical systems, but they are computationally expensive and time-consuming. Exploring large parameter spaces or performing repeated simulations for optimization quickly becomes impractical.

This project investigates whether machine learning–based surrogate models can approximate MD simulation outputs with sufficient accuracy to reduce computational cost. In particular, different Active Learning strategies are evaluated to determine whether the required number of simulation samples can be significantly reduced without sacrificing predictive performance.

In this project, MD simulations based on Lennard-Jones potential parameters are used to predict the resulting system density. In addition to the simulation results, the dataset provides an estimate of the intrinsic simulation uncertainty (estimErr), allowing model performance to be evaluated relative to physical simulation accuracy.

The central question is:

> Can surrogate models replace MD simulations - or are they limited to accelerating parameter exploration?

---

## Objectives

1. Train a neural network surrogate model on MD simulation data.

2. Compare:

  - Random sampling
  - Boundary-based sampling
  - Active learning strategies

3. Evaluate predictive performance using:

  - RMSE
  - MAE
  - relative to simulation uncertainty

4. Assess whether surrogate models can replace MD simulations within acceptable uncertainty bounds.

---

## Project Structure

```text
.
├── data/                           # Dataset
├── final/
│   ├── data/                       # Test set
│   ├── loss/                       # Losses over Training per model
│   ├── models/                     # Best models and over epochs per model
│   └── scalers/                    # Best scalers and over epochs per model
├── plots/                          # Plots for visualization and presentation purposes
├── over_50_with_estimErr.csv       # Cleaned Dataset with `estimErr` column
├── surrogate-modelling.ipynb       # Notebook with guide, explanation and code
└── README.md
```

---

## Requirements

Used Python version: Python 3.10

Dependencies can be found in the first code cell of the notebook.

For modeling and evaluation purposes, main dependencies were:

- numpy
- sklearn
- torch

---

## Notebook Workflow

1. Data Loading
2. Data Cleaning and Explorative Data Analysis
3. Training of a simple Neural Network (NN)
4. Training of the same architecture NN with different Active Learning Strategies
  - Random Sampling
  - Boundary Sampling
  - Sparse Sampling
  - Error-based Sampling
  - Query-By-Committee (QBC)
5. Evaluation of different models and strategies

---

## Results

- Active Learning **reduces required training data by ~50%** for comparable performance
- Median model error remains **1.5–2× higher** than simulation uncertainty
- Worst 10% of predictions exceed simulation uncertainty by **7–10×**

---

## Can Surrogate Models replace MD Simulations?

**They can approximate them, but not universally replace them.**

Surrogate models are capable of learning the input–output relationships of MD simulations with good accuracy within the domain covered by the training data. In well-sampled regions of the parameter space, they can provide fast and reasonably reliable predictions.

However, they should not be used as a standalone replacement for MD simulations.

- Their main strength lies in accelerating exploration and optimization. Surrogate models are particularly useful for:
- Narrowing down large parameter spaces
- Identifying promising regions for further investigation
- Reducing the number of expensive MD simulations
- Performing rapid sensitivity studies

In this context, computational speed often outweighs the need for perfect accuracy. Once a promising region is identified, full MD simulations should be performed for validation and high-precision analysis.

> Surrogate models are powerful acceleration tools for parameter exploration and optimization, but they should complement, not fully replace, MD simulations.


