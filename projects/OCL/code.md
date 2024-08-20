---
layout: default
title: Code
---

# Code

## Overview

The code is organized into several key components:

1. **ImportDonnees.py**: Handles data import.
2. **Fonctions.py**: Contains utility functions such as ONO, THIELMANN, MAYER, etc.
3. **ModelePrediction.py**: Manages model prediction and training.
4. **Optimization Script**: Implements the optimization algorithm and handles result export.

## Key Functions

### `optimiser_nuance`

The main function for optimizing the material mix based on given constraints and predictions.

#### Parameters
- **`nom_nuance`**: The name of the material grade.
- **`dossier_donnees`**: Path to the data directory.
- **`faire_prediction`**: Whether to generate new predictions or use existing models.

#### Steps
1. **Data Import**: Load necessary data and models.
2. **Optimization**: Set up and solve the linear programming problem.
3. **Results Export**: Save results to Excel files.

## How to Run

To run the script, use the following command:
