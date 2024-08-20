---
layout: default
title: Methodology
---

# Methodology



## Predictive Models

### Data cleaning

The data cleaning process involved several steps to prepare and integrate data from different sources for analysis. Initially, raw data from traction and spectrochemical analyses were imported from Excel files. Spectrochemical data was filtered to retain only relevant measurements and columns, removing rows with missing values and focusing on specific measurement types. Columns with inconsistent naming were standardized, and unnecessary columns were dropped.

Traction data was similarly cleaned by renaming columns for consistency and correcting format discrepancies. Numeric columns were converted to the appropriate data types, and invalid entries were removed. Both datasets were aggregated to compute mean values where necessary, followed by merging based on common identifiers such as furnace number and nuance.

Duplicate records were eliminated to ensure uniqueness. The final cleaned dataset contains each observations chemical compositions (explicative features) and the traction results (value to predict).
THis dataset was saved in an Excel file, ready for further analysis.
### Overview

The predictive modeling process is designed to estimate the mechanical properties of materials using Random Forest algorithms. The approach depends on whether new models are generated or existing ones are utilized.

### Model Generation

1. **Data Preparation**:
   - **Import Data**: The cleaned dataset (`data_nettoyées.xlsx`) is loaded.
   - **Feature and Target Variables**:
     - **Explanatory Features (`X`)**: All columns except for the target variables (`Rm` and `Moyenne allongement`) are used. Features are normalized by subtracting the mean and dividing by the standard deviation to ensure consistent scaling.
     - **Target Variables (`y_rm` and `y_allongement`)**: The variables to be predicted, specifically the mechanical resistance and average elongation.

2. **Model Training**:
   - **Random Forest Regressor for `Rm`**:
     - A Random Forest model (`rf_model_rm`) is trained to predict mechanical resistance. It uses 50 estimators and a fixed random state for reproducibility.
   - **Random Forest Regressor for `Moyenne allongement`**:
     - Another Random Forest model (`rf_model_all`) is trained to predict average elongation. It uses 30 estimators with a different random state.

3. **Model Evaluation**:
   - **Metrics**:
     - **R² Score**: Measures the proportion of variance in the target variable explained by the model.
     - **Root Mean Squared Error (RMSE)**: Assesses the model’s prediction accuracy by measuring the square root of the average squared errors.

4. **Model Saving**:
   - Models, along with normalization parameters (mean and standard deviation), are saved to disk using joblib for future use. This includes:
     - **`rf_model_rm.pkl`**: Trained model for predicting `Rm`.
     - **`rf_model_all.pkl`**: Trained model for predicting `Moyenne allongement`.
     - **`moyenne.pkl`**: Mean values used for normalization, it will be needed for further predictions.
     - **`ecart_type.pkl`**: Standard deviations used for normalization,  it will be needed for further predictions.

### Model Loading

If pre-existing models are used (up to the user to decide):
   - **Model Files**:
     - **`rf_model_rm.pkl`**: Pre-trained model for mechanical resistance.
     - **`rf_model_all.pkl`**: Pre-trained model for elongation.
     - **`moyenne.pkl`** and **`ecart_type.pkl`**: Normalization parameters previously saved.

## Optimization
### Data Import

The optimisation part starts by importing data from Excel and CSV files, including:
- **`data_nettoyées.xlsx`**: Cleaned data about raw materials for prediction.
- **`MP.csv`**: Data on material prices.
- **`Contraintes_composants.csv`**: Constraints on chemical composition.

### Optimization Algorithm

The optimization process involves the following steps:

1. **Define Variables**: Create decision variables for the proportions of each raw material.
2. **Objective Function**: Minimize the total cost of the selected materials.
3. **Constraints**:
   - **Material Proportions**: Ensure proportions are within specified minimum and maximum limits.
   - **Quality Constraints**: Meet quality criteria using ONO, Thielmann, and Mayer metrics.
   - **Chemical Composition**: Adhere to constraints for each chemical element.

### Solver

The problem is solved using the CBC or COIN-OR solvers in the Pulp, a python library .

### Embedding the learned models as constraints in the optimization model

The initial solution is used as an input to the prediction model. If the output doesnt respect the quality threshold value, the linear constraints are adjusted in a way to exclude this solution and the problem is re-solved.
If the adjustation leads to an unfeasable reagion. The code stops and returns the last feasible solution found.

## Code

Refer to the **[Code](code.md)** section for detailed implementation and usage instructions.
