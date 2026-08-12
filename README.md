# Capstone-Project-Imperial Black-Box Optimisation (BBO)

## 1. Project Overview

This project explores black-box optimisation (BBO), where the objective is to maximise the output of unknown mathematical functions using only a limited number of function evaluations. Unlike traditional optimisation problems, the analytical form of each function is unavailable, meaning optimisation decisions must be made solely from previously observed inputs and outputs.

The project simulates many real-world machine learning applications where evaluating an objective is expensive, noisy or time-consuming, such as hyperparameter optimisation, engineering design, drug discovery and simulation-based optimisation. The challenge is to identify high-performing solutions while making as few queries as possible.

---

## 2. Inputs and Outputs

Each function accepts an input vector with values constrained to the interval `[0,1]`.

The dimensionality differs for each function:

- Function 1: 2 variables
- Function 2: 2 variables
- Function 3: 3 variables
- Function 4: 4 variables
- Function 5: 4 variables
- Function 6: 5 variables
- Function 7: 6 variables
- Function 8: 8 variables

Example input:

```text
Function 3:
[0.985471, 0.700565, 0.343019]
```

Each submitted query returns a single numerical objective value representing the performance of that input. The optimisation process uses these observed outputs to determine future query locations.

---

## 3. Challenge Objectives

The objective is to maximise the output of each unknown function while operating under a strict query budget. Because each function evaluation is expensive and the underlying mathematical form is unknown, every submitted query must balance learning about the search space with improving the objective value.

The primary constraints include:

- Unknown function structure
- Limited number of function evaluations
- Different input dimensionalities
- Sequential learning from previous observations

These constraints require an adaptive optimisation strategy rather than exhaustive search.

---

## 4. Technical Approach

My strategy has evolved throughout the project.

During the first iteration, I relied primarily on exploratory heuristics by selecting points that covered different regions of the search space while also considering the limited initial observations.

After receiving the first set of outputs, I began exploiting regions that appeared promising while still exploring areas where uncertainty remained high.

By the third iteration, I adopted a more systematic Bayesian optimisation strategy. I combined the original observations with the results from the first two submission rounds to fit Gaussian Process surrogate models for each function. These surrogate models estimate both the expected objective value and prediction uncertainty. I then used an Upper Confidence Bound (UCB) acquisition function to recommend new query points that balance exploration and exploitation.

My strategy varies across functions. Where previous submissions produced significant improvements, I perform local exploitation by searching near the best observations. Where outputs remain consistently poor or nearly identical, I prioritise exploration by selecting points in uncertain regions of the search space.

I also considered how other machine learning methods could support the optimisation process. For example, Support Vector Machines (SVMs) could classify regions into high- and low-performing areas using soft-margin or kernel-based classifiers, while regression models could help identify influential variables. However, Bayesian optimisation remains the primary optimisation framework because it explicitly models uncertainty, allowing more efficient selection of future queries.

This README will continue to evolve as additional optimisation rounds are completed and new evidence becomes available.
