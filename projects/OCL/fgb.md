The optimization problem for determining the optimal blend of materials to produce a specific alloy (referred to as "nuance") can be mathematically formulated as follows:

### Decision Variables:
- \( x_i \): Proportion of material \( i \) in the final blend. (Continuous decision variable)
- \( y_i \): Binary variable indicating whether material \( i \) is used in the blend. \( y_i = 1 \) if used, otherwise \( y_i = 0 \).

### Objective Function:
Minimize the total cost of the blend:
\[
\text{Minimize } \sum_{i} c_i \cdot x_i
\]
where \( c_i \) is the cost of material \( i \).

### Constraints:

1. **Composition Constraints:**
   - For each chemical element \( e \), the total proportion of that element in the blend must lie within specified bounds:
   \[
   \sum_{i} a_{ie} \cdot x_i \geq \text{min\_bound}_e \quad \forall e
   \]
   \[
   \sum_{i} a_{ie} \cdot x_i \leq \text{max\_bound}_e \quad \forall e
   \]
   where \( a_{ie} \) is the proportion of element \( e \) in material \( i \).

2. **Quality Constraints:**
   - The blend must meet certain quality thresholds defined by functions ONO, THIELMANN, and MAYER:
   \[
   \sum_{i} \text{ONO}(i) \cdot x_i \leq \text{seuil\_qualite\_ONO}
   \]
   \[
   \sum_{i} \text{THIELMANN}(i) \cdot x_i \leq \text{seuil\_qualite\_Thielmann}
   \]
   \[
   \sum_{i} \text{MAYER}(i) \cdot x_i \leq \text{seuil\_qualite\_Mayer}
   \]

3. **Material Proportion Constraints:**
   - For certain materials, the proportion used in the blend is restricted between specific bounds:
   \[
   0.1 \cdot y_i \leq x_i \leq 0.5 \cdot y_i \quad \text{for specific materials \( i \)}
   \]
   - For specific return materials:
   \[
   x_{\text{return}} = 0.3
   \]

4. **Proportion Sum Constraint:**
   - The sum of the proportions for metallic materials must equal 1:
   \[
   \sum_{i \in \text{metallic}} x_i = 1
   \]

### Special Constraints:
- For specific nuances like 'GS 450-10' or 'GS 500-7', an additional constraint on the Aluminum (Al) content:
   \[
   \sum_{i} a_{i, \text{Al}} \cdot x_i = 0.02
   \]

### Binary Constraints:
- Each \( x_i \) is bounded by its corresponding binary variable \( y_i \):
   \[
   y_i \in \{0, 1\}
   \]

This mathematical model is solved using linear programming, with the objective to minimize the cost while satisfying the constraints on chemical composition, quality, and material usage proportions. The problem is solved using the `PuLP` library in Python, and the optimal solution indicates the proportion of each material to be used in the alloy.
