# ELO Rating Hyperparameter Tuning with Optuna

## Overview

This project aims to optimize the hyperparameters (`k` values) of an ELO rating system using Optuna, a Bayesian optimization framework. The code provides an efficient approach to hyperparameter tuning, overcoming the limitations of traditional grid search methods, which are computationally expensive and time-consuming.

## What is ELO?

The ELO rating system is a method for calculating the relative skill levels of players in two-player games such as chess or competitive sports like mixed martial arts (MMA). Each player has a rating, which is updated based on the outcome of matches. The core principle of the ELO system is to predict the probability of a player winning a match based on their rating relative to their opponent's rating.

## What are `k` Values?

In the ELO rating system, the `k` value (or K-factor) determines how much a player's rating changes after a match. Higher `k` values lead to larger changes in ratings, making the system more sensitive to individual match outcomes. Different methods of victory (e.g., knockout, submission, decision) can have different `k` values, reflecting their relative significance.

## Why Optuna?

Using grid search for hyperparameter tuning can be extremely resource-intensive. For example, with the given ranges for `k` values:

```python
k_values_ranges = {
    'Decision - Unanimous': range(10, 200, 5),
    'KO/TKO': range(10, 200, 5),
    'Submission': range(10, 200, 5),
    'Decision - Split': range(10, 200, 5),
    'Decision - Majority': range(10, 200, 5),
    'TKO - Doctor\'s Stoppage': range(10, 200, 5),
    'Overturned': range(1, 31, 2),
    'Could Not Continue': range(10, 60, 5),
    'DQ': range(1, 11, 2),
    'Other': range(1, 11, 2)
}
```
The total number of combinations for grid search is 11,291,011,440,000. Such an exhaustive search is infeasible.

Optuna leverages Bayesian optimization, which uses a probabilistic model to predict the performance of different hyperparameter sets. This allows it to focus on the most promising regions of the search space, significantly reducing the number of evaluations needed to find the optimal parameters.
