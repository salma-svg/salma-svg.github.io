---
layout: default
title: Code
---

# Code

## Overview

The project code is organized into several key components:

1. **`NettoyageDonnées.py`**: Cleans and prepares the data for training.
2. **`ImportDonnees.py`**: Manages data import, including loading and preprocessing.
3. **`Fonctions.py`**: Contains utility functions for various calculations and operations, such as ONO, THIELMANN, and error handling.
4. **`ModelePrediction.py`**: Responsible for training and saving the predictive models for mechanical properties and elongation.
5. **`Optimisation.py`**: Implements the optimization algorithm and handles the export of results.

## Key Functions

### `optimiser_nuance`

The primary function for optimizing the material mix based on given constraints and predictions.

#### Parameters
- **`nom_nuance`**: The name of the material grade to be optimized. Example values include 'GS 400-15', 'GS 450-10', etc.
- **`dossier_donnees`**: The path to the directory containing the data files. This directory should include cleaned data, material prices, and constraints files.
- **`faire_prediction`**: A flag indicating whether to regenerate prediction models. Set to `oui` (yes) to train new models, or `non` (no) to use existing models.

#### Steps
1. **Data Import**: The function loads the necessary data files and predictive models from the specified directory.
2. **Optimization**: It sets up and solves the linear programming problem to determine the optimal material mix while satisfying the quality and cost constraints.
3. **Results Export**: The optimized results and predictions are saved to Excel files for further analysis.

## How to Run

To execute the optimization script, use the following command in your terminal:

```bash
python Optimisation.py {directory_name} {want_to_regenerate_prediction_model} {iron_cast_name}
```

`directory_name`: The name of the directory where your data files are located. For example, data.

`want_to_regenerate_prediction_model`: Set this to oui if you want to regenerate the prediction models or non if you want to use existing models. For example, oui or non.

`iron_cast_name`: The specific name of the iron cast grade you are optimizing. For example, 'GS 400-15'.

You can for example try :
```bash
python Optimisation.py data oui 'GS 400-15'
```
