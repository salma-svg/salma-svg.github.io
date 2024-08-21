---
layout: default
title: Methodology
---

# Methodology

## Predictive Models

### Data cleaning

The data cleaning process involved several steps to prepare and integrate data from different sources for analysis. Initially, raw data from traction and spectrochemical analyses were imported from Excel files. Spectrochemical data was filtered to retain only relevant measurements and columns, removing rows with missing values and focusing on specific measurement types. Columns with inconsistent naming were standardized, and unnecessary columns were dropped.

Traction data was similarly cleaned by renaming columns for consistency and correcting format discrepancies. Numeric columns were converted to the appropriate data types, and invalid entries were removed. Both datasets were aggregated to compute mean values where necessary, followed by merging based on common identifiers such as furnace number and nuance.

Duplicate records were eliminated to ensure uniqueness. The final cleaned dataset contains each observation's chemical compositions (explicative features) and the traction results (value to predict). This dataset was saved in an Excel file, ready for further analysis.

### Overview

The predictive modeling process estimates the mechanical properties of materials using **Random Forest algorithms**. This ensemble learning method constructs multiple decision trees and aggregates their results to make predictions. It is well-suited for handling complex and non-linear relationships in data, which is our case.

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
      -  **R² Score**: Measures the proportion of variance in the target variable explained by the model. A higher R² score indicates a better fit of the model to the data.
      - **Root Mean Squared Error (RMSE)**: Assesses the model’s prediction accuracy by measuring the square root of the average squared errors. Lower RMSE values indicate better predictive accuracy.
        
        #### For Mechanical Resistance (Rm):
         - **Random Forest R²**: 0.83
         - **Random Forest RMSE**: 34.70
         
        #### For Elongation (Allongement):
         - **Random Forest R²**: 0.70
         - **Random Forest RMSE**: 2.60

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

The optimization part starts by importing data from Excel and CSV files, including:
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

### Mathematical Model

Let  ${x_i}$ be the proportion of each raw material \( i \).

**Objective Function**:
Minimize the total cost of materials:

\[
\text{Minimize} \quad Z = \sum_{i} c_i \cdot x_i
\]

where \( c_i \) is the cost of material \( i \).

**Subject to**:

1. **Material Proportions**:
   \[
   x_{\text{min}, i} \leq x_i \leq x_{\text{max}, i} \quad \forall i
   \]

2. **Quality Constraints**:
   - ONO Quality:
   \[
   \sum_{i} \text{ONO}_i \cdot x_i \leq \text{ONO}_{\text{threshold}}
   \]
   - Thielmann Quality:
   \[
   \sum_{i} \text{Thielmann}_i \cdot x_i \leq \text{Thielmann}_{\text{threshold}}
   \]
   - Mayer Quality:
   \[
   \sum_{i} \text{Mayer}_i \cdot x_i \leq \text{Mayer}_{\text{threshold}}
   \]

3. **Chemical Composition**:
   For each chemical element \( e \):
   \[
   \text{min}_e \leq \sum_{i} \text{comp}_{i, e} \cdot x_i \leq \text{max}_e
   \]

where \( \text{comp}_{i, e} \) is the composition of element \( e \) in material \( i \).

### Solver

The problem is solved using the CBC or COIN-OR solvers in the Pulp Python library.

### Embedding Learned Models as Constraints in the Optimization Model

Since the approximated constraint is highly nonlinear and cannot be directly incorporated into a linear programming model, an alternative method was developed to include it in the optimization process. The approach involves integrating the learned models by using the initial solution as input for the prediction model. If the predicted values fail to meet the required quality thresholds, the constraints are modified to exclude this solution, and the optimization problem is re-solved.

If these adjustments result in an infeasible region with no valid solutions, the process stops, and the last feasible solution is returned. While this method provides a way to incorporate complex constraints, it is not perfect, as it may still yield a solution that does not fully satisfy the constraints if no feasible region exists.
