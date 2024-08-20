## Mathematical Model

The optimization problem is formulated as a linear programming problem with the objective of minimizing the cost of raw materials, subject to quality constraints.

### Objective Function

$$
\text{Minimize} \quad Z = \sum_{i=1}^{n} C_i \cdot x_i
$$

Where:

- $Z$ is the total cost.
- $C_i$ is the cost of material i.
- $x_i$ is the proportion of material i used in the recipe.

### Constraints

1. **Quality Constraints**:
   - ONO, Thielmann, and Mayer quality indices:
   $$
   \sum_{i=1}^{n} \text{QualityIndex}_i \cdot x_i \leq \text{Threshold}
   $$

2. **Chemical Composition Constraints**:
   - For each chemical element $j$:
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
  - $x_i$: Proportion of material \( i \) in the recipe.
  - Binary variables to indicate whether a material is used or not.

- **Parameters**:
  - $C_i$: Cost of material \( i \).
  - $\text{QualityIndex}_i$: Quality indices (ONO, Thielmann, Mayer) for material \( i \).
  - $\text{Composition}_{i,j}$: Composition of chemical element \( j \) in material \( i \).
  - $\text{Min}_j$, $\text{Max}_j$: Minimum and maximum allowable percentages of chemical element \( j \).
  - $\text{RM}_{pred}$, $\text{Elongation}_{pred}$: Predicted values for tensile strength and elongation.
