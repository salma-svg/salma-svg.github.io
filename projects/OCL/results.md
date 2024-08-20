---
layout: default
title: Results
---

# Results

## Results Overview

The results of the optimization are exported into two Excel files:
1. **`resultats_{nom_nuance}.xlsx`**: Contains the optimal proportions of each material and their costs.
2. **`resultats_composition{nom_nuance}.xlsx`**: Contains the predicted mechanical resistance and elongation of the optimized composition.

### How to Interpret Results

- **Material Proportions**: The proportion of each material used in the optimal mix.
- **Cost**: The cost associated with each material in the mix.
- **Predictions**: Mechanical resistance and elongation predictions compared to thresholds.

## Example Results

- **Material Proportions**: See the optimal mix in the `resultats_{nom_nuance}.xlsx` file.
- **Predictions**: Check the `resultats_composition{nom_nuance}.xlsx` file for the predicted values.

## Troubleshooting

If results are not as expected:
- **Check Constraints**: Ensure all constraints are correctly defined.
- **Adjust Constraints**: If mechanical properties or elongation thresholds are not met, constraints may need adjustment.

## Code

Refer to the **[Code](code.md)** section for more details on how results are generated and saved.

