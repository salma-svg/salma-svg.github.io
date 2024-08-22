---
layout: default
title: Code
---

# Code

## Overview

The project [code](https://github.com/salma-svg/ICOCL.git) is organized into several key components:

1. **`NettoyageDonnées.py`**: Cleans and prepares the data for training.
2. **`ImportDonnees.py`**: Manages data import, including loading and preprocessing.
3. **`Fonctions.py`**: Contains utility functions for various calculations and operations, such as ONO, THIELMANN, and error handling.
4. **`ModelePrediction.py`**: Responsible for training and saving the predictive models for mechanical properties and elongation.
5. **`Optimisation.py`**: Implements the optimization algorithm and handles the export of results.
6. **`app.py`**: Provides a Streamlit-based web application interface, allowing users to interact with the project's functionalities, in a more user-friendly manner.


## Key Function

### `optimiser_nuance`

The primary function for optimizing the material mix based on given constraints and predictions.

#### Parameters
- **`nom_nuance`**: The name of the material grade to be optimized. Example values include 'GS 400-15', 'GS 450-10', etc.
- **`dossier_donnees`**: The path to the directory containing the data files. This directory should include cleaned data, material prices, and constraints csv files.
- **`faire_prediction`**: A flag indicating whether to regenerate prediction models. Set to `oui` (yes) to train new models, or `non` (no) to use existing models.

#### Steps
1. **Data Import**: The function loads the necessary data files and predictive models from the specified directory.
2. **Optimization**: It sets up and solves the linear programming problem to determine the optimal material mix while satisfying the quality and cost constraints.
3. **Results Export**: The optimized results and predictions are saved to Excel files for further analysis.
4. **Adjustment**: After the initial optimization, the solution is checked against the mechanical constraints (e.g., tensile strength, elongation). If the solution does not meet these constraints, the algorithm adjusts the material mix as closely as possible to ensure compliance.

## How to Run

### Part 1: Running Without Streamlit

To execute the optimization script in a standard terminal environment (without Streamlit), use the following command:

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
This will run the script and produce the output directly in your terminal, with results saved to the appropriate files.

### Part 2: Running with Streamlit

To use Streamlit for a more interactive experience, follow these steps:
1. **Install Streamlit**: Ensure you have Streamlit installed in your environment. You can install it using pip:
   ```bash
    pip install streamlit
    ```
2. **Run the Streamlit App**:
   ```bash
   streamlit run app.py
   ```
This will open the app in your browser, allowing you to interact with the optimization process through a web interface.





