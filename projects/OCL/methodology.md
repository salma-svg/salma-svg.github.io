---
layout: default
title: Methodology
---

# Methodology

## Data Import

The project starts by importing data from Excel and CSV files, including:
- **`data_nettoyées.xlsx`**: Cleaned data about raw materials.
- **`MP.xlsx`**: Data on material prices.
- **`Contraintes_composants.csv`**: Constraints on chemical composition.

## Predictive Models

Depending on user input, the project either:
- **Generates new prediction models** using provided data.
- **Loads existing models** for mechanical properties and elongation from saved files.

### Predictive Models Used

- **`rf_model_rm`**: Random Forest model for predicting mechanical resistance.
- **`rf_model_all`**: Random Forest model for predicting elongation.

## Optimization Algorithm

The optimization process involves the following steps:

1. **Define Variables**: Create decision variables for the proportions of each raw material.
2. **Objective Function**: Minimize the total cost of the selected materials.
3. **Constraints**:
   - **Material Proportions**: Ensure proportions are within specified minimum and maximum limits.
   - **Quality Constraints**: Meet quality criteria using ONO, Thielmann, and Mayer metrics.
   - **Chemical Composition**: Adhere to constraints for each chemical element.

## Solver

The problem is solved using the CBC or COIN-OR solvers. If the initial solution is infeasible, constraints are adjusted and the problem is re-solved.

## Code

Refer to the **[Code](code.md)** section for detailed implementation and usage instructions.
