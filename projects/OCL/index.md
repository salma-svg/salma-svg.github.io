---
layout: default
title: Iron Casting Optimization with Constraint Learning
---

# Iron Casting Optimization with Constraint Learning

Welcome to the **Iron Casting Optimization with Constraint Learning** project. During my three-month internship at **Fonderie de Niederbronn**, I focused on optimizing iron casting recipes. The objective is to minimize material costs while ensuring the highest quality of the final products. This project employs advanced constraint learning techniques, predictive modeling, and mathematical optimization.

## Project Overview

The project is structured into several key phases:

1. **Data Cleaning**: Processing raw data, merging datasets, and extracting essential features for analysis.
2. **Data Import**: Loading and preparing data related to raw materials and production constraints.
3. **Model Prediction**: Employing predictive models to estimate mechanical properties like tensile strength and elongation, which can only be measured after production.
4. **Optimization**: Minimizing material costs while adhering to quality constraints using a mathematical optimization model.
5. **Results Export**: Saving and exporting final results and predictions to Excel files for further use.

## Mathematical Model

The optimization problem is formulated as a linear programming problem with the objective of minimizing the cost of raw materials, subject to quality constraints.

### Objective Function

$$
\text{Minimize} \quad Z = \sum_{i=1}^{n} C_i \cdot x_i
$$

Where:

- $Z$ is the total cost.
- \( C_i \) is the cost of material \( i \).
- \( x_i \) is the proportion of material \( i \) used in the recipe.

### Constraints

1. **Quality Constraints**:
   - ONO, Thielmann, and Mayer quality indices:
   $$
   \sum_{i=1}^{n} \text{QualityIndex}_i \cdot x_i \leq \text{Threshold}
   $$

2. **Chemical Composition Constraints**:
   - For each chemical element \( j \):
   $$
   \text{Min}_j \leq \sum_{i=1}^{n} \text{Composition}_{i,j} \cdot x_i \leq \text{Max}_j
   $$

3. **Proportion Constraint**:
   $$
   \sum_{i=1}^{n} x_i = 1
   $$

4. **Mechanical Properties Prediction**:
   - Tensile strength (RM) and elongation must satisfy specific thresholds:
   $$
   \text{RM}_{pred} \geq \text{RM}_{threshold}, \quad \text{Elongation}_{pred} \geq \text{Elongation}_{threshold}
   $$

### Variables

- **Decision Variables**:
  - \( x_i \): Proportion of material \( i \) in the recipe.
  - Binary variables to indicate whether a material is used or not.

- **Parameters**:
  - \( C_i \): Cost of material \( i \).
  - \( \text{QualityIndex}_i \): Quality indices (ONO, Thielmann, Mayer) for material \( i \).
  - \( \text{Composition}_{i,j} \): Composition of chemical element \( j \) in material \( i \).
  - \( \text{Min}_j \), \( \text{Max}_j \): Minimum and maximum allowable percentages of chemical element \( j \).
  - \( \text{RM}_{pred} \), \( \text{Elongation}_{pred} \): Predicted values for tensile strength and elongation.

## Key Components

- **[Methodology](methodology.md)**: Detailed explanations of the algorithms and methods used in the project.
- **[Results](results.md)**: Insights and interpretations of the project results.
- **[Code](code.md)**: A comprehensive guide to the code structure and how to use it.

## Getting Started

To get started with this project, please refer to the **[Code](code.md)** section for setup instructions and usage guidelines.

## About

This project was developed by Salma Bouaouda. For more information, visit my [GitHub profile](https://github.com/salma-svg) or connect with me on [LinkedIn](https://linkedin.com/in/your-profile).

## Contact

Feel free to reach out via email: [bouaouda.salma@gmail.com](mailto:bouaouda.salma@gmail.com)
