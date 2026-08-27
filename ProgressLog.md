# Black Box Optimisation (BBO) Capstone

## Project Overview

This project investigates the optimisation of eight unknown black-box objective functions using Bayesian Optimisation and surrogate modelling. Each function accepts between two and eight continuous inputs in the range [0,1]. The objective is to identify input combinations that maximise (or improve) the unknown objective while operating under a strict query budget.

Rather than directly observing the mathematical functions, only the evaluated input-output pairs are available. This makes the problem representative of many real-world optimisation problems where experiments are expensive and the underlying process is unknown.

---

# Repository Structure

```
BBO-Capstone/
│
├── data/
│   ├── historical_queries.csv
│   ├── outputs.csv
│
├── notebooks/
│   ├── Week1.ipynb
│   ├── Week2.ipynb
│   ├── Week3.ipynb
│   ├── Week4.ipynb
│   └── Week5.ipynb
│
├── models/
│   ├── gaussian_process.py
│   ├── extra_trees.py
│   └── acquisition_functions.py
│
├── results/
│   ├── weekly_predictions.csv
│   ├── best_queries.csv
│
└── README.md
```

---

# Optimisation Strategy

## Week 1

### Objective

Build an initial understanding of the search space.

### Strategy

- Random exploration
- Visual inspection of outputs
- Simple heuristic reasoning
- No surrogate model

### Outcome

Established initial baseline observations and identified several promising regions, particularly for Functions 4, 5 and 8.

---

## Week 2

### Strategy

Move from random exploration towards local search.

### Changes

- Increased exploitation around high-performing regions.
- Began comparing neighbouring solutions.
- Used engineering judgement to identify locally promising inputs.

### Outcome

Discovered several improved objective values and recognised that different functions required different search behaviours.

---

## Week 3

### Major change

Introduced Bayesian Optimisation.

### Models

- Gaussian Process surrogate
- Matérn kernel
- Upper Confidence Bound (UCB) acquisition

### Rationale

UCB balances

- exploitation
- exploration

by rewarding uncertain regions.

### Outcome

Although exploration increased, several functions (especially Functions 4 and 5) moved away from good regions and performance deteriorated.

---

## Week 4

### Strategy refinement

Retained the Gaussian Process surrogate but changed the acquisition strategy.

### Changes

- Replaced UCB with Expected Improvement (EI).
- Reduced unnecessary exploration.
- Increased local optimisation around known good solutions.

### Outcome

Performance improved considerably.

New best solutions were found for

- Function 6
- Function 7

Functions 2 and 5 also returned close to their historical best values.

---

## Week 5

### Advanced surrogate modelling

The optimisation strategy was expanded further.

### Models

Gaussian Process

- Automatic Relevance Determination (ARD)

Extra Trees Regressor

- used as an alternative surrogate

### Additional improvements

- Cross-validation of surrogate models
- Trust-region Bayesian Optimisation
- Local optimisation around current best solutions
- Feature importance analysis

Rather than relying on a single surrogate, predictions from multiple models were compared before selecting the next query.

### Current strategy

Different optimisation strategies are now used for different functions.

| Function | Strategy |
|-----------|----------|
| 1 | Global exploration |
| 2 | Local Bayesian optimisation |
| 3 | Local refinement |
| 4 | Trust-region recovery |
| 5 | Boundary optimisation |
| 6 | Local exploitation |
| 7 | Local exploitation |
| 8 | Local exploitation |

---

# Libraries

The project currently relies on

- NumPy
- pandas
- matplotlib
- scikit-learn
- SciPy

Gaussian Process Regression and Extra Trees are implemented using scikit-learn.

Future work may investigate

- PyTorch
- TensorFlow

if sufficient observations become available for neural-network surrogate models.

---

# Current Best Results

Throughout the optimisation process the surrogate models have progressively become more informative as additional observations have been collected.

The optimisation workflow has evolved from

Random Search

↓

Heuristic Search

↓

Bayesian Optimisation (GP + UCB)

↓

Bayesian Optimisation (GP + Expected Improvement)

↓

Hybrid Surrogate Models
(GP + Extra Trees + Trust Regions)

---

# Future Improvements

- Automatic retraining after every query
- Ensemble surrogate models
- Trust-region Bayesian Optimisation
- Feature importance analysis
- Neural-network surrogate comparison
- Automated query generation
