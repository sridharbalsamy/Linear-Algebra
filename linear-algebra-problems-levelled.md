# Linear Algebra Problem & Solution Master Package
### Based on Gilbert Strang's *Linear Algebra and Its Applications* (4th Edition)
**Scope:** Chapters 1, 2 (excl. 2.5, 2.6), 3 (excl. 3.5), and 5

---

## Overview & How to Use This Master Package

This comprehensive problem and solution set provides a multi-tiered revision resource designed to build deep conceptual intuition, procedural fluency, and exam readiness. 

For every topic across Chapters 1, 2, 3, and 5, you will find:
1. **Three Difficulty Levels per Topic**:
   * **Level 1 (Easy / Foundational)**: Core algorithmic mechanics, basic definitions, and standard textbook procedures.
   * **Level 2 (Intermediate / Practical Application)**: Real-world engineering, signal processing, data compression, least-squares estimation, and dynamical systems applications.
   * **Level 3 (Advanced / Tricky Exam Traps)**: Deep theoretical questions centered around classic exam trap terminology like *"full row rank"*, *"full column rank"*, *"invertible vs. diagonalizable"*, and *"projection space traps"*.
2. **Step-by-Step Rigorous Solutions**: Full mathematical derivations with explicit arithmetic.
3. **Exam Shortcuts / Quick Tricks**: Lightning-fast methods to solve 2-mark or multiple-choice questions without full scratchwork.
4. **ASCII / Geometric Visuals**: T\text-based structural diagrams illustrating the underlying geometric transformations and vector relationships.

---

# CHAPTER 1: Matrices and Gaussian Elimination

---

## Topic 1.1: Elimination, Row/Column Picture, & $LU$ Factorization

### Problem 1.1.1 (Level 1: Easy / Foundational) — Elimination & Geometric Pictures
Solve the following $2 \times 2$ system of linear equations using Gaussian elimination:
$$2x_1 + 3x_2 = 7$$
$$4x_1 + 9x_2 = 19$$

1. Find the elimination matrix $E_{21}$ that reduces the system to upper triangular form $U\mathbf{x} = \mathbf{c}$, and solve for $x_1, x_2$ via back-substitution.
2. Explain the solution geometrically from both the **Row Picture** and the **Column Picture**.

```
[ROW PICTURE: Intersecting Lines]             [COLUMN PICTURE: Linear Combination]
             ^ x_2                                         ^
             |   / L1: 2x1+3x2=7                           |      / b = [7, 19]^T
             |  /                                          |     /
    (1, 5/3) * /                                           |    /  1.67*col2
-------------+--------------> x_1             -------------+---+----------->
            / \                                            |  /
           /   \ L2: 4x1+9x2=19                            | / 1.0*col1
          /     \                                          |/
```

#### Detailed Solution:
1. **Elimination Step ($E_{21}$)**:
   Write the system in matrix form $A\mathbf{x} = \mathbf{b}$:
   $$\begin{bmatrix} 2 & 3 \ 4 & 9 \end{bmatrix} \begin{bmatrix} x_1 \ x_2 \end{bmatrix} = \begin{bmatrix} 7 \ 19 \end{bmatrix}$$
   The multiplier to eliminate $a_{21} = 4$ using pivot $a_{11} = 2$ is $\ell_{21} = \frac{4}{2} = 2$.
   Subtract $2 \times (\text{Row 1})$ from $\text{Row 2}$:
   $$\text{Row 2}^{(new)} = (4x_1 + 9x_2) - 2(2x_1 + 3x_2) = 19 - 2(7) \implies 3x_2 = 5$$
   The elimination matrix $E_{21}$ and upper triangular matrix $U$ are:
   $$E_{21} = \begin{bmatrix} 1 & 0 \ -2 & 1 \end{bmatrix}, \quad U = \begin{bmatrix} 2 & 3 \ 0 & 3 \end{bmatrix}, \quad \mathbf{c} = E_{21}\mathbf{b} = \begin{bmatrix} 7 \ 5 \end{bmatrix}$$

2. **Back-Substitution**:
   From row 2: $3x_2 = 5 \implies x_2 = \frac{5}{3}$.
   From row 1: $2x_1 + 3\left(\frac{5}{3}\right) = 7 \implies 2x_1 + 5 = 7 \implies 2x_1 = 2 \implies x_1 = 1$.
   Solution vector: $\mathbf{x} = \begin{bmatrix} 1 \ 5/3 \end{bmatrix}$.

3. **Geometric Interpretation**:
   * **Row Picture**: Two lines in the 2D $x_1$-$x_2$ plane ($2x_1 + 3x_2 = 7$ and $4x_1 + 9x_2 = 19$) intersect at the unique point $(x_1, x_2) = (1, 5/3)$.
   * **Column Picture**: The target vector $\mathbf{b} = \begin{bmatrix} 7 \ 19 \end{bmatrix}$ is expressed as a linear combination of the column vectors of $A$:
     $$1 \cdot \begin{bmatrix} 2 \ 4 \end{bmatrix} + \frac{5}{3} \cdot \begin{bmatrix} 3 \ 9 \end{bmatrix} = \begin{bmatrix} 2 \ 4 \end{bmatrix} + \begin{bmatrix} 5 \ 15 \end{bmatrix} = \begin{bmatrix} 7 \ 19 \end{bmatrix}$$

⚡ **Exam Shortcut / Quick Trick (2-Mark / Multiple Choice)**:
For a $2 \times 2$ matrix $A = \begin{bmatrix} a & b \ c & d \end{bmatrix}$, use the explicit inverse formula:
$$A^{-1} = \frac{1}{ad - bc} \begin{bmatrix} d & -b \ -c & a \end{bmatrix} = \frac{1}{18 - 12}\begin{bmatrix} 9 & -3 \ -4 & 2 \end{bmatrix} = \frac{1}{6}\begin{bmatrix} 9 & -3 \ -4 & 2 \end{bmatrix}$$
$$\mathbf{x} = A^{-1}\mathbf{b} = \frac{1}{6}\begin{bmatrix} 9(7) - 3(19) \ -4(7) + 2(19) \end{bmatrix} = \frac{1}{6}\begin{bmatrix} 63 - 57 \ -28 + 38 \end{bmatrix} = \frac{1}{6}\begin{bmatrix} 6 \ 10 \end{bmatrix} = \begin{bmatrix} 1 \ 5/3 \end{bmatrix}$$

---

### Problem 1.1.2 (Level 2: Intermediate / Practical Application) — Digital Signal Processing: Causal Moving Average Filter
In signal processing, a 3-point causal moving average filter smooths a discrete input signal $\mathbf{x} = [x_1, x_2, x_3]^T$ to yield an output signal $\mathbf{y} = [y_1, y_2, y_3]^T$ according to:
$$y_1 = x_1$$
$$y_2 = \frac{1}{2}x_1 + \frac{1}{2}x_2$$
$$y_3 = \frac{1}{3}x_1 + \frac{1}{3}x_2 + \frac{1}{3}x_3$$

1. Express this transformation as a matrix system $A\mathbf{x} = \mathbf{y}$.
2. Factor $A$ into $LU$ decomposition and find $A^{-1}$ (the inverse filter that reconstructs $\mathbf{x}$ from filtered output $\mathbf{y}$).
3. Given a measured output signal $\mathbf{y} = [2, 3, 4]^T$, solve for the original signal $\mathbf{x}$ using forward elimination and back-substitution.

```
[SIGNAL FILTER FLOW]
x_1 ----[ 1 ]-------------------------------------------> y_1 = x_1
x_2 ----[ 1/2 ]----+----[ 1/2 ]-------------------------> y_2 = (x_1 + x_2)/2
x_3 ----[ 1/3 ]----+----[ 1/3 ]----+----[ 1/3 ]---------> y_3 = (x_1 + x_2 + x_3)/3
```

#### Detailed Solution:
1. **Matrix Representation**:
   $$A = \begin{bmatrix} 1 & 0 & 0 \ 1/2 & 1/2 & 0 \ 1/3 & 1/3 & 1/3 \end{bmatrix}$$

2. **$LU$ Factorization & Inverse Filter**:
   Notice that $A$ is already lower triangular! Therefore:
   $$L = A \text{ (with diagonal pivots divided out into } D\text{)}, \quad U = I$$
   Factoring $A = L D U$:
   $$A = \begin{bmatrix} 1 & 0 & 0 \ 1/2 & 1 & 0 \ 1/3 & 1 & 1 \end{bmatrix} \begin{bmatrix} 1 & 0 & 0 \ 0 & 1/2 & 0 \ 0 & 0 & 1/3 \end{bmatrix} \begin{bmatrix} 1 & 0 & 0 \ 0 & 1 & 0 \ 0 & 0 & 1 \end{bmatrix}$$
   To find $A^{-1}$, solve $A\mathbf{x} = \mathbf{y}$ row by row:
   * Row 1: $x_1 = y_1$
   * Row 2: $\frac{1}{2}x_1 + \frac{1}{2}x_2 = y_2 \implies x_1 + x_2 = 2y_2 \implies x_2 = -y_1 + 2y_2$
   * Row 3: $\frac{1}{3}(x_1 + x_2 + x_3) = y_3 \implies x_1 + x_2 + x_3 = 3y_3 \implies 2y_2 + x_3 = 3y_3 \implies x_3 = -2y_2 + 3y_3$
   
   Thus, the inverse filter matrix (a finite difference matrix) is:
   $$A^{-1} = \begin{bmatrix} 1 & 0 & 0 \ -1 & 2 & 0 \ 0 & -2 & 3 \end{bmatrix}$$

3. **Reconstructing $\mathbf{x}$ for $\mathbf{y} = [2, 3, 4]^T$**:
   $$\mathbf{x} = A^{-1}\mathbf{y} = \begin{bmatrix} 1 & 0 & 0 \ -1 & 2 & 0 \ 0 & -2 & 3 \end{bmatrix} \begin{bmatrix} 2 \ 3 \ 4 \end{bmatrix} = \begin{bmatrix} 2 \ -2 + 6 \ -6 + 12 \end{bmatrix} = \begin{bmatrix} 2 \ 4 \ 6 \end{bmatrix}$$

⚡ **Exam Shortcut / Quick Trick**:
For lower triangular systems $A\mathbf{x} = \mathbf{y}$, **never compute explicit matrix inverses**. Apply **forward substitution** directly:
$$x_1 = y_1 = 2$$
$$x_2 = 2y_2 - x_1 = 2(3) - 2 = 4$$
$$x_3 = 3y_3 - (x_1 + x_2) = 3(4) - 6 = 6$$

---

### Problem 1.1.3 (Level 3: Advanced / Tricky Exam Traps) — Singular Breakdown, Pivot Traps & Parameters
Consider the linear system $A\mathbf{x} = \mathbf{b}$ where parameter $d \in \mathbb{R}$ and $k \in \mathbb{R}$:
$$\begin{bmatrix} 1 & 2 & 1 \ 2 & 4 & d \ 3 & 6 & 3 \end{bmatrix} \begin{bmatrix} x_1 \ x_2 \ x_3 \end{bmatrix} = \begin{bmatrix} 3 \ k \ 9 \end{bmatrix}$$

1. Perform forward elimination. Identify the pivot positions and specify the conditions on $d$ and $k$ under which the system has:
   *(a)* No solution (inconsistent).
   *(b)* Infinitely many solutions with rank $r = 1$.
   *(c)* Infinitely many solutions with rank $r = 2$.
2. Can this system ever have a **unique solution**? Explain using the concept of **Full Column Rank**.

```
[STAIRCASE PIVOT STRUCTURE & BREAKDOWN]
Row 1: [ (1)   2   1 ]  ---> Pivot 1 = 1
Row 2: [  0   (0) d-2]  ---> Col 2 entry is 0! (Col 2 = 2 * Col 1)
Row 3: [  0    0   0 ]  ---> Row 3 vanishes completely!
```

#### Detailed Solution:
1. **Forward Elimination**:
   Set up augmented matrix $[A \mid \mathbf{b}]$:
   $$\begin{bmatrix} 1 & 2 & 1 & \mid & 3 \ 2 & 4 & d & \mid & k \ 3 & 6 & 3 & \mid & 9 \end{bmatrix}$$
   * Step 1: Subtract $2 \times (\text{Row 1})$ from Row 2, and $3 \times (\text{Row 1})$ from Row 3:
     $$\begin{bmatrix} 1 & 2 & 1 & \mid & 3 \ 0 & 0 & d-2 & \mid & k-6 \ 0 & 0 & 0 & \mid & 0 \end{bmatrix}$$

2. **Case Analysis**:
   * **Column 2 Breakdown**: Entry $(2,2)$ is $0$ because Column 2 is a scalar multiple of Column 1 ($\mathbf{a}_2 = 2\mathbf{a}_1$). Thus, column 2 contains no pivot.
   * **Case (a): No Solution (Inconsistent)**:
     If $d = 2$, Row 2 becomes $\begin{bmatrix} 0 & 0 & 0 & \mid & k-6 \end{bmatrix}$.
     If $k \neq 6$, Row 2 states $0x_1 + 0x_2 + 0x_3 = k-6 \neq 0$, which is an impossibility.
     $\implies \mathbf{d = 2, k \neq 6} \implies \text{No Solution}$.
   * **Case (b): Infinitely Many Solutions with Rank $r = 1$**:
     If $d = 2$ and $k = 6$, Row 2 becomes $\begin{bmatrix} 0 & 0 & 0 & \mid & 0 \end{bmatrix}$.
     The matrix has only $1$ pivot ($a_{11} = 1$). Rank $r = 1$.
     Number of free variables = $n - r = 3 - 1 = 2$ ($x_2$ and $x_3$ are free).
     $\implies \mathbf{d = 2, k = 6} \implies \infty^{2} \text{ Solutions (2D plane in } \mathbb{R}^3)$.
   * **Case (c): Infinitely Many Solutions with Rank $r = 2$**:
     If $d \neq 2$, entry $(2,3) = d-2 \neq 0$ becomes the second pivot!
     Pivots are in Column 1 and Column 3. Rank $r = 2$.
     Number of free variables = $n - r = 3 - 2 = 1$ ($x_2$ is free).
     Row 3 is $0 = 0$, which is satisfied for **any** $k$.
     From Row 2: $(d-2)x_3 = k-6 \implies x_3 = \frac{k-6}{d-2}$.
     $\implies \mathbf{d \neq 2, \text{ any } k} \implies \infty^{1} \text{ Solutions (1D line in } \mathbb{R}^3)$.

3. **Unique Solution & Full Column Rank Trap**:
   * For $A\mathbf{x} = \mathbf{b}$ to have a unique solution, the matrix must have **Full Column Rank** ($r = n = 3$). This requires $n = 3$ pivots.
   * Here, $\text{Row 3} = 3 \times \text{Row 1}$, making Row 3 permanently dependent. Max rank is $r \le 2 < n = 3$.
   * Because $r < n$, $N(A)$ contains non-zero vectors. Therefore, **a unique solution is IMPOSSIBLE for any values of $d$ and $k$**.

⚡ **Exam Shortcut / Quick Trick**:
Notice immediately that $\text{Row 3} = 3 \times \text{Row 1}$ and $\text{Col 2} = 2 \times \text{Col 1}$.
In 5 seconds: $\det(A) = 0$ permanently! You can instantly eliminate any exam option claiming a unique solution exists.

---

# CHAPTER 2: Vector Spaces & Fundamental Subspaces

---

## Topic 2.1: Fundamental Subspaces, Basis, Dimension & Rank-Nullity

### Problem 2.1.1 (Level 1: Easy / Foundational) — Constructing Fundamental Bases
Given the $3 \times 4$ matrix $A$:
$$A = \begin{bmatrix} 1 & 2 & 1 & 4 \ 2 & 4 & 3 & 10 \ 1 & 2 & 0 & 2 \end{bmatrix}$$

1. Reduce $A$ to Reduced Row Echelon Form $R = \text{rref}(A)$.
2. Identify rank $r$, pivot columns, and free variables.
3. Find explicit bases and dimensions for the Column Space $C(A)$ and Nullspace $N(A)$.
4. Verify the Rank-Nullity Theorem: $\text{rank}(A) + \dim N(A) = n$.

```
[SUB-SPACE DIMENSION SPLIT FOR 3x4 MATRIX (n=4)]
R^4 Space ----------------------------------------------------->
|--- Column Space C(A^T) [Dim r = 2] ---|--- Nullspace N(A) [Dim n-r = 2] ---|
| Pivot Vars: x_1, x_3                  | Free Vars: x_2, x_4                |
```

#### Detailed Solution:
1. **Reduce to $\text{rref}(A)$**:
   $$A = \begin{bmatrix} 1 & 2 & 1 & 4 \ 2 & 4 & 3 & 10 \ 1 & 2 & 0 & 2 \end{bmatrix}$$
   * Row operations: $R_2 \to R_2 - 2R_1$ and $R_3 \to R_3 - R_1$:
     $$\begin{bmatrix} 1 & 2 & 1 & 4 \ 0 & 0 & 1 & 2 \ 0 & 0 & -1 & -2 \end{bmatrix}$$
   * Row operation: $R_3 \to R_3 + R_2$:
     $$U = \begin{bmatrix} \mathbf{1} & 2 & 1 & 4 \ 0 & 0 & \mathbf{1} & 2 \ 0 & 0 & 0 & 0 \end{bmatrix}$$
   * Row operation: $R_1 \to R_1 - R_2$ (creating zeros above pivot in Col 3):
     $$R = \text{rref}(A) = \begin{bmatrix} \mathbf{1} & 2 & 0 & 2 \ 0 & 0 & \mathbf{1} & 2 \ 0 & 0 & 0 & 0 \end{bmatrix}$$

2. **Pivots and Rank**:
   * Pivots are in **Column 1** and **Column 3**.
   * Rank $r = 2$. Pivot variables: $x_1, x_3$. Free variables: $x_2, x_4$.

3. **Bases for $C(A)$ and $N(A)$**:
   * **Column Space $C(A)$**: Take the **pivot columns of the ORIGINAL matrix $A$** (Columns 1 and 3):
     $$\text{Basis for } C(A) = \left\{ \begin{bmatrix} 1 \ 2 \ 1 \end{bmatrix}, \begin{bmatrix} 1 \ 3 \ 0 \end{bmatrix} \right\}, \quad \dim C(A) = r = 2$$
   * **Nullspace $N(A)$**: Solve $R\mathbf{x} = \mathbf{0}$:
     $$x_1 + 2x_2 + 2x_4 = 0 \implies x_1 = -2x_2 - 2x_4$$
     $$x_3 + 2x_4 = 0 \implies x_3 = -2x_4$$
     Express $\mathbf{x}$ in vector parametric form:
     $$\mathbf{x} = \begin{bmatrix} x_1 \ x_2 \ x_3 \ x_4 \end{bmatrix} = x_2 \begin{bmatrix} -2 \ 1 \ 0 \ 0 \end{bmatrix} + x_4 \begin{bmatrix} -2 \ 0 \ -2 \ 1 \end{bmatrix}$$
     $$\text{Basis for } N(A) = \left\{ \begin{bmatrix} -2 \ 1 \ 0 \ 0 \end{bmatrix}, \begin{bmatrix} -2 \ 0 \ -2 \ 1 \end{bmatrix} \right\}, \quad \dim N(A) = n - r = 4 - 2 = 2$$

4. **Rank-Nullity Verification**:
   $$\text{rank}(A) + \dim N(A) = 2 + 2 = 4 = n \quad \checkmark$$

⚡ **Exam Shortcut / Quick Trick**:
When $R$ is partitioned as $\begin{bmatrix} I & F \ 0 & 0 \end{bmatrix}$ (after reordering columns), the nullspace matrix $N$ whose columns are the special solutions is given directly by $N = \begin{bmatrix} -F \ I \end{bmatrix}$.
Here, $F = \begin{bmatrix} 2 & 2 \ 0 & 2 \end{bmatrix} \implies -F = \begin{bmatrix} -2 & -2 \ 0 & -2 \end{bmatrix}$. Inserting 1s for free variables yields special solutions instantly!

---

### Problem 2.1.2 (Level 2: Intermediate / Practical Application) — Image Processing: Rank-1 Outer Product Decomposition
In image processing, a $3 \times 3$ image frame $A$ is represented as the sum of two rank-1 outer product feature matrices:
$$A = \mathbf{u}_1\mathbf{v}_1^T + \mathbf{u}_2\mathbf{v}_2^T$$
where:
$$\mathbf{u}_1 = \begin{bmatrix} 1 \ 2 \ 1 \end{bmatrix}, \quad \mathbf{v}_1 = \begin{bmatrix} 1 \ 0 \ -1 \end{bmatrix}, \quad \mathbf{u}_2 = \begin{bmatrix} 0 \ 1 \ 1 \end{bmatrix}, \quad \mathbf{v}_2 = \begin{bmatrix} 2 \ 1 \ 0 \end{bmatrix}$$

1. Compute the explicit $3 \times 3$ matrix $A$.
2. Determine bases for $C(A)$ and $C(A^T)$ without performing full Gaussian elimination.
3. Find a basis for the Nullspace $N(A)$ and explain what geometric information is removed/compressed by this rank-2 representation.

```
[RANK-1 OUTER PRODUCT COMPRESSION LAYER]
u_1 v_1^T = [1, 2, 1]^T * [1, 0, -1]  ---> Layer 1 (Vertical Stripes)
u_2 v_2^T = [0, 1, 1]^T * [2, 1, 0]  ---> Layer 2 (Diagonal T\texture)
------------------------------------------------------------------
Total Matrix A = Layer 1 + Layer 2   ---> Rank = 2 (1D Nullspace lost)
```

#### Detailed Solution:
1. **Compute Outer Products & Matrix $A$**:
   $$\mathbf{u}_1\mathbf{v}_1^T = \begin{bmatrix} 1 \ 2 \ 1 \end{bmatrix} \begin{bmatrix} 1 & 0 & -1 \end{bmatrix} = \begin{bmatrix} 1 & 0 & -1 \ 2 & 0 & -2 \ 1 & 0 & -1 \end{bmatrix}$$
   $$\mathbf{u}_2\mathbf{v}_2^T = \begin{bmatrix} 0 \ 1 \ 1 \end{bmatrix} \begin{bmatrix} 2 & 1 & 0 \end{bmatrix} = \begin{bmatrix} 0 & 0 & 0 \ 2 & 1 & 0 \ 2 & 1 & 0 \end{bmatrix}$$
   $$A = \begin{bmatrix} 1 & 0 & -1 \ 2 & 0 & -2 \ 1 & 0 & -1 \end{bmatrix} + \begin{bmatrix} 0 & 0 & 0 \ 2 & 1 & 0 \ 2 & 1 & 0 \end{bmatrix} = \begin{bmatrix} 1 & 0 & -1 \ 4 & 1 & -2 \ 3 & 1 & -1 \end{bmatrix}$$

2. **Bases for $C(A)$ and $C(A^T)$ by Inspection**:
   * Every column of $A = \mathbf{u}_1\mathbf{v}_1^T + \mathbf{u}_2\mathbf{v}_2^T$ is a combination of $\mathbf{u}_1$ and $\mathbf{u}_2$.
     Since $\mathbf{u}_1 = \begin{bmatrix} 1 \ 2 \ 1 \end{bmatrix}$ and $\mathbf{u}_2 = \begin{bmatrix} 0 \ 1 \ 1 \end{bmatrix}$ are linearly independent, they form a basis for $C(A)$:
     $$\text{Basis for } C(A) = \left\{ \begin{bmatrix} 1 \ 2 \ 1 \end{bmatrix}, \begin{bmatrix} 0 \ 1 \ 1 \end{bmatrix} \right\}, \quad \dim C(A) = 2$$
   * Every row of $A$ is a combination of $\mathbf{v}_1^T$ and $\mathbf{v}_2^T$.
     Since $\mathbf{v}_1 = \begin{bmatrix} 1 \ 0 \ -1 \end{bmatrix}$ and $\mathbf{v}_2 = \begin{bmatrix} 2 \ 1 \ 0 \end{bmatrix}$ are independent, they form a basis for $C(A^T)$:
     $$\text{Basis for } C(A^T) = \left\{ \begin{bmatrix} 1 \ 0 \ -1 \end{bmatrix}, \begin{bmatrix} 2 \ 1 \ 0 \end{bmatrix} \right\}, \quad \dim C(A^T) = 2$$

3. **Nullspace $N(A)$ & Compression Interpretation**:
   Reduce $A$ to RREF:
   $$\begin{bmatrix} 1 & 0 & -1 \ 4 & 1 & -2 \ 3 & 1 & -1 \end{bmatrix} \to \begin{bmatrix} 1 & 0 & -1 \ 0 & 1 & 2 \ 0 & 1 & 2 \end{bmatrix} \to \begin{bmatrix} 1 & 0 & -1 \ 0 & 1 & 2 \ 0 & 0 & 0 \end{bmatrix}$$
   Solve $R\mathbf{x} = \mathbf{0} \implies x_1 = x_3, x_2 = -2x_3$.
   $$\text{Basis for } N(A) = \left\{ \begin{bmatrix} 1 \ -2 \ 1 \end{bmatrix} \right\}, \quad \dim N(A) = 3 - 2 = 1$$
   * **Physical Meaning**: Any signal component parallel to $\begin{bmatrix} 1 \ -2 \ 1 \end{bmatrix}$ is multiplied by $A$ to yield $\mathbf{0}$. This 1D subspace represents high-frequency pixel noise that is filtered out/compressed away by the rank-2 model.

⚡ **Exam Shortcut / Quick Trick**:
For any outer product sum $A = \sum_{i=1}^r \mathbf{u}_i \mathbf{v}_i^T$, if $\{\mathbf{u}_i\}$ are independent and $\{\mathbf{v}_i\}$ are independent, then **$\text{rank}(A) = r$ automatically**! You do not need to calculate $A$ or perform Gaussian elimination to find the dimensions.

---

### Problem 2.1.3 (Level 3: Advanced / Tricky Exam Traps) — The Master Classification of Rank $r$
For an $m \times n$ matrix $A$ of rank $r$, complete the comprehensive solvability and subspace classification table for the four structural rank cases:
1. **Full Rank (Square)**: $r = m = n$
2. **Full Column Rank ("Tall & Thin")**: $r = n < m$
3. **Full Row Rank ("Short & Wide")**: $r = m < n$
4. **Neither Full Rank**: $r < m$ and $r < n$

```
[STRANG'S BIG PICTURE OF LINEAR ALGEBRA]
           R^n (Input Space)                        R^m (Output Space)
  +---------------------------------+      +---------------------------------+
  |  Row Space C(A^T)               |      |  Column Space C(A)              |
  |  Dim = r                        |  A   |  Dim = r                        |
  |  (All x_r map 1-to-1 to C(A))   |=====>|  (Ax = b solvable if b in C(A)) |
  +---------------------------------+      +---------------------------------+
  |  Nullspace N(A)                 |      |  Left Nullspace N(A^T)          |
  |  Dim = n - r                    |      |  Dim = m - r                    |
  |  (Mapped to 0)                  |      |  (Perpendicular to C(A))        |
  +---------------------------------+      +---------------------------------+
```

#### Detailed Solution & Master Table:

| Rank Case | Matrix Shape | Solvability of $A\mathbf{x} = \mathbf{b}$ | Nullspace $N(A)$ Dim | Left Nullspace $N(A^T)$ Dim | Inverse Type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **1. $r = m = n$** | Square $n \times n$ | **Exactly 1 solution** for every $\mathbf{b}$ | $0$ (Only $\mathbf{0}$) | $0$ (Only $\mathbf{0}$) | Two-sided $A^{-1}$ |
| **2. $r = n < m$** | Tall $m \times n$ | **0 or 1 solution** ($1$ if $\mathbf{b} \in C(A)$, $0$ if not) | $0$ (Only $\mathbf{0}$) | $m - n > 0$ | Left Inverse $B = (A^TA)^{-1}A^T$ ($BA = I_n$) |
| **3. $r = m < n$** | Wide $m \times n$ | **Infinitely many solutions** for EVERY $\mathbf{b}$ | $n - m > 0$ | $0$ (Only $\mathbf{0}$) | Right Inverse $C = A^T(AA^T)^{-1}$ ($AC = I_m$) |
| **4. $r < m, r < n$** | Any $m \times n$ | **0 or $\infty$ solutions** ($0$ if $\mathbf{b} \notin C(A)$, $\infty$ if $\mathbf{b} \in C(A)$) | $n - r > 0$ | $m - r > 0$ | Pseudoinverse $A^+$ only |

#### Justifications & Exam Trap Explanations:
* **Trap 1 ("Full Column Rank implies unique solution")**:
  FALSE! Full column rank ($r = n$) guarantees *uniqueness if a solution exists*, but if $m > n$, there are $m - n$ left nullspace constraints. If $\mathbf{b} \notin C(A)$, there are **zero solutions**.
* **Trap 2 ("Full Row Rank implies invertible")**:
  FALSE! Full row rank ($r = m$) guarantees *existence of solutions for every $\mathbf{b}$*, but because $n > m$, there are $n - m$ free variables, yielding **infinitely many solutions**. It has a right inverse, but no left inverse.
* **Trap 3 ("$A^TA$ is always invertible")**:
  FALSE! $A^TA$ is $n \times n$ with $\text{rank}(A^TA) = \text{rank}(A) = r$. Thus, $A^TA$ is invertible **if and only if $A$ has Full Column Rank ($r = n$)**. If $r < n$, $A^TA$ is singular!

⚡ **Exam Shortcut / Quick Trick**:
To test if $A\mathbf{x} = \mathbf{b}$ is solvable, check if $\mathbf{b} \perp N(A^T)$.
Because $C(A)^\perp = N(A^T)$, $A\mathbf{x} = \mathbf{b}$ has a solution if and only if $\mathbf{y}^T\mathbf{b} = 0$ for every vector $\mathbf{y} \in N(A^T)$.

---

# CHAPTER 3: Orthogonality and Projections

---

## Topic 3.1: Projections, Least Squares, & Gram-Schmidt / $QR$

### Problem 3.1.1 (Level 1: Easy / Foundational) — Orthogonal Projection onto a Line
Given the vector $\mathbf{b} = \begin{bmatrix} 1 \ 2 \ 3 \end{bmatrix}$ and the line $L$ spanned by $\mathbf{a} = \begin{bmatrix} 1 \ 1 \ 1 \end{bmatrix}$:
1. Find the scalar multiplier $\hat{x}$, the projection vector $\mathbf{p} \in L$, and the projection matrix $P$.
2. Compute the error vector $\mathbf{e} = \mathbf{b} - \mathbf{p}$ and verify that $\mathbf{e} \perp \mathbf{a}$.
3. Show that $P^2 = P$ and $P^T = P$.

```
[ORTHOGONAL PROJECTION ONTO LINE]
         b = [1, 2, 3]^T
        /|
       / |
      /  | e = b - p = [-1, 0, 1]^T  (e PERPENDICULAR to a!)
     /   |
    +----+-----------------------> Line L (spanned by a = [1, 1, 1]^T)
    0    p = [2, 2, 2]^T
```

#### Detailed Solution:
1. **Projection Vector & Matrix**:
   $$\hat{x} = \frac{\mathbf{a}^T\mathbf{b}}{\mathbf{a}^T\mathbf{a}} = \frac{(1)(1) + (1)(2) + (1)(3)}{1^2 + 1^2 + 1^2} = \frac{6}{3} = 2$$
   $$\mathbf{p} = \hat{x}\mathbf{a} = 2 \begin{bmatrix} 1 \ 1 \ 1 \end{bmatrix} = \begin{bmatrix} 2 \ 2 \ 2 \end{bmatrix}$$
   $$P = \frac{\mathbf{a}\mathbf{a}^T}{\mathbf{a}^T\mathbf{a}} = \frac{1}{3} \begin{bmatrix} 1 \ 1 \ 1 \end{bmatrix} \begin{bmatrix} 1 & 1 & 1 \end{bmatrix} = \frac{1}{3} \begin{bmatrix} 1 & 1 & 1 \ 1 & 1 & 1 \ 1 & 1 & 1 \end{bmatrix}$$

2. **Error Vector & Orthogonality**:
   $$\mathbf{e} = \mathbf{b} - \mathbf{p} = \begin{bmatrix} 1 \ 2 \ 3 \end{bmatrix} - \begin{bmatrix} 2 \ 2 \ 2 \end{bmatrix} = \begin{bmatrix} -1 \ 0 \ 1 \end{bmatrix}$$
   $$\mathbf{a}^T\mathbf{e} = \begin{bmatrix} 1 & 1 & 1 \end{bmatrix} \begin{bmatrix} -1 \ 0 \ 1 \end{bmatrix} = -1 + 0 + 1 = 0 \quad \checkmark$$

3. **Projection Matrix Properties**:
   * **Symmetry**: $P^T = \left(\frac{1}{3} \mathbf{J}\right)^T = \frac{1}{3} \mathbf{J} = P \quad \checkmark$
   * **Idempotency**:
     $$P^2 = \left(\frac{1}{3}\begin{bmatrix} 1 & 1 & 1 \ 1 & 1 & 1 \ 1 & 1 & 1 \end{bmatrix}\right) \left(\frac{1}{3}\begin{bmatrix} 1 & 1 & 1 \ 1 & 1 & 1 \ 1 & 1 & 1 \end{bmatrix}\right) = \frac{1}{9} \begin{bmatrix} 3 & 3 & 3 \ 3 & 3 & 3 \ 3 & 3 & 3 \end{bmatrix} = \frac{1}{3} \begin{bmatrix} 1 & 1 & 1 \ 1 & 1 & 1 \ 1 & 1 & 1 \end{bmatrix} = P \quad \checkmark$$

⚡ **Exam Shortcut / Quick Trick**:
For any projection matrix $P$, $\text{trace}(P) = \text{rank}(P) = \dim(\text{Subspace})$.
Here, $\text{trace}(P) = \frac{1}{3}(1 + 1 + 1) = 1$, confirming instantly that $P$ projects onto a $1$-dimensional subspace (a line).

---

### Problem 3.1.2 (Level 2: Intermediate / Practical Application) — Least Squares Fitting & $QR$ Signal Estimation
A temperature sensor collects noisy observations $y$ at time points $t = -1, 0, 1, 2$:
$$\text{Data Points } (t_i, y_i): \quad (-1, 0), \quad (0, 1), \quad (1, 3), \quad (2, 4)$$

1. Set up the overdetermined system $A\mathbf{x} = \mathbf{b}$ for the linear model $y = C + Dt$.
2. Form and solve the Normal Equations $A^TA\hat{\mathbf{x}} = A^T\mathbf{b}$ to find the best-fit line parameters $\hat{\mathbf{x}} = [\hat{C}, \hat{D}]^T$.
3. Compute the projection vector $\mathbf{p} = A\hat{\mathbf{x}}$ and total squared error $\|E\|^2 = \|\mathbf{b} - \mathbf{p}\|^2$.
4. Compute the $QR$ factorization $A = QR$ and solve for $\hat{\mathbf{x}}$ using $R\hat{\mathbf{x}} = Q^T\mathbf{b}$.

```
[LEAST SQUARES TRENDLINE FIT]
  y ^
  4 |                                  * (2, 4)
  3 |                        * (1, 3) /  Line: y = 1.3 + 1.4t
  2 |                                /
  1 |             * (0, 1)  /
  0 |   * (-1, 0)/
----+-----+-------+--------+--------+--------> t
     -1       0        1        2
```

#### Detailed Solution:
1. **Set up $A\mathbf{x} = \mathbf{b}$**:
   $$\begin{bmatrix} 1 & -1 \ 1 & 0 \ 1 & 1 \ 1 & 2 \end{bmatrix} \begin{bmatrix} C \ D \end{bmatrix} = \begin{bmatrix} 0 \ 1 \ 3 \ 4 \end{bmatrix}$$

2. **Normal Equations**:
   $$A^TA = \begin{bmatrix} 1 & 1 & 1 & 1 \ -1 & 0 & 1 & 2 \end{bmatrix} \begin{bmatrix} 1 & -1 \ 1 & 0 \ 1 & 1 \ 1 & 2 \end{bmatrix} = \begin{bmatrix} 4 & 2 \ 2 & 6 \end{bmatrix}$$
   $$A^T\mathbf{b} = \begin{bmatrix} 1 & 1 & 1 & 1 \ -1 & 0 & 1 & 2 \end{bmatrix} \begin{bmatrix} 0 \ 1 \ 3 \ 4 \end{bmatrix} = \begin{bmatrix} 8 \ 11 \end{bmatrix}$$
   Solve $\begin{bmatrix} 4 & 2 \ 2 & 6 \end{bmatrix} \begin{bmatrix} \hat{C} \ \hat{D} \end{bmatrix} = \begin{bmatrix} 8 \ 11 \end{bmatrix}$:
   $$(A^TA)^{-1} = \frac{1}{(4)(6) - (2)(2)} \begin{bmatrix} 6 & -2 \ -2 & 4 \end{bmatrix} = \frac{1}{20} \begin{bmatrix} 6 & -2 \ -2 & 4 \end{bmatrix}$$
   $$\begin{bmatrix} \hat{C} \ \hat{D} \end{bmatrix} = \frac{1}{20} \begin{bmatrix} 6 & -2 \ -2 & 4 \end{bmatrix} \begin{bmatrix} 8 \ 11 \end{bmatrix} = \frac{1}{20} \begin{bmatrix} 48 - 22 \ -16 + 44 \end{bmatrix} = \frac{1}{20} \begin{bmatrix} 26 \ 28 \end{bmatrix} = \begin{bmatrix} 1.3 \ 1.4 \end{bmatrix}$$
   Best fit line: $y = 1.3 + 1.4t$.

3. **Projection Vector & Residual Error**:
   $$\mathbf{p} = A\hat{\mathbf{x}} = \begin{bmatrix} 1 & -1 \ 1 & 0 \ 1 & 1 \ 1 & 2 \end{bmatrix} \begin{bmatrix} 1.3 \ 1.4 \end{bmatrix} = \begin{bmatrix} -0.1 \ 1.3 \ 2.7 \ 4.1 \end{bmatrix}$$
   $$\mathbf{e} = \mathbf{b} - \mathbf{p} = \begin{bmatrix} 0 \ 1 \ 3 \ 4 \end{bmatrix} - \begin{bmatrix} -0.1 \ 1.3 \ 2.7 \ 4.1 \end{bmatrix} = \begin{bmatrix} 0.1 \ -0.3 \ 0.3 \ -0.1 \end{bmatrix}$$
   $$\|E\|^2 = (0.1)^2 + (-0.3)^2 + (0.3)^2 + (-0.1)^2 = 0.01 + 0.09 + 0.09 + 0.01 = 0.20$$

4. **Gram-Schmidt & $QR$ Factorization**:
   Columns of $A$: $\mathbf{a}_1 = [1, 1, 1, 1]^T, \mathbf{a}_2 = [-1, 0, 1, 2]^T$.
   * $\mathbf{q}_1 = \frac{\mathbf{a}_1}{\|\mathbf{a}_1\|} = \frac{1}{2} \begin{bmatrix} 1 \ 1 \ 1 \ 1 \end{bmatrix}$
   * Subtract parallel projection: $\mathbf{A}_2 = \mathbf{a}_2 - (\mathbf{q}_1^T\mathbf{a}_2)\mathbf{q}_1$
     $$\mathbf{q}_1^T\mathbf{a}_2 = \frac{1}{2}(-1 + 0 + 1 + 2) = 1$$
     $$\mathbf{A}_2 = \begin{bmatrix} -1 \ 0 \ 1 \ 2 \end{bmatrix} - 1 \left(\frac{1}{2}\begin{bmatrix} 1 \ 1 \ 1 \ 1 \end{bmatrix}\right) = \begin{bmatrix} -1.5 \ -0.5 \ 0.5 \ 1.5 \end{bmatrix} = \frac{1}{2}\begin{bmatrix} -3 \ -1 \ 1 \ 3 \end{bmatrix}$$
     $$\|\mathbf{A}_2\| = \frac{1}{2}\sqrt{9 + 1 + 1 + 9} = \frac{\sqrt{20}}{2} = \sqrt{5}$$
     $$\mathbf{q}_2 = \frac{1}{2\sqrt{5}}\begin{bmatrix} -3 \ -1 \ 1 \ 3 \end{bmatrix}$$
   
   $QR$ factors:
   $$Q = \begin{bmatrix} 1/2 & -3/(2\sqrt{5}) \ 1/2 & -1/(2\sqrt{5}) \ 1/2 & 1/(2\sqrt{5}) \ 1/2 & 3/(2\sqrt{5}) \end{bmatrix}, \quad R = \begin{bmatrix} 2 & 1 \ 0 & \sqrt{5} \end{bmatrix}$$
   Solving $R\hat{\mathbf{x}} = Q^T\mathbf{b}$:
   $$Q^T\mathbf{b} = \begin{bmatrix} 4 \ 11/\sqrt{5} \end{bmatrix}$$
   $$\begin{bmatrix} 2 & 1 \ 0 & \sqrt{5} \end{bmatrix} \begin{bmatrix} \hat{C} \ \hat{D} \end{bmatrix} = \begin{bmatrix} 4 \ 11/\sqrt{5} \end{bmatrix} \implies \sqrt{5}\hat{D} = \frac{14}{\sqrt{5}} \implies \hat{D} = 1.4, \quad 2\hat{C} + 1.4 = 4 \implies \hat{C} = 1.3 \quad \checkmark$$

⚡ **Exam Shortcut / Quick Trick**:
If time points $t_i$ are centered such that $\sum t_i = 0$ (e.g. $t = -1.5, -0.5, 0.5, 1.5$), the off-diagonal terms of $A^TA$ become **zero**!
$A^TA$ becomes purely diagonal $\begin{bmatrix} m & 0 \ 0 & \sum t_i^2 \end{bmatrix}$, allowing you to read off $\hat{C} = \frac{\sum y_i}{m}$ and $\hat{D} = \frac{\sum t_i y_i}{\sum t_i^2}$ in 10 seconds!

---

### Problem 3.1.3 (Level 3: Advanced / Tricky Exam Traps) — Projection Space Traps & Gram-Schmidt Singularities
Let $P = A(A^TA)^{-1}A^T$ be the projection matrix onto $C(A)$, where $A$ is an $m \times n$ matrix with full column rank ($r = n < m$).

1. Prove that $I - P$ is the projection matrix onto the Left Nullspace $N(A^T)$.
2. **The Invertible Matrix Trap**: What does $P = A(A^TA)^{-1}A^T$ simplify to if $A$ is a square $n \times n$ invertible matrix? Explain the geometric trap that confuses students.
3. What happens if you attempt the Gram-Schmidt process on a set of vectors $\mathbf{a}_1, \mathbf{a}_2, \mathbf{a}_3$ where $\mathbf{a}_3 = 2\mathbf{a}_1 - \mathbf{a}_2$?

```
[ORTHOGONAL DECOMPOSITION OF R^m]
               R^m Space
  +---------------------------------+
  | Column Space C(A)               | <--- Projected onto by P = A(A^TA)^-1 A^T
  | (Dim = r)                       |
  +---------------------------------+
  | Left Nullspace N(A^T)           | <--- Projected onto by I - P
  | (Dim = m - r)                   |
  +---------------------------------+
  Every b = p + e  (where p = Pb in C(A), e = (I-P)b in N(A^T))
```

#### Detailed Solution:
1. **Proof that $I - P$ Projects onto $N(A^T)$**:
   * Any vector $\mathbf{b} \in \mathbb{R}^m$ splits into $\mathbf{b} = \mathbf{p} + \mathbf{e}$, where $\mathbf{p} = P\mathbf{b} \in C(A)$ and $\mathbf{e} = (I - P)\mathbf{b} \in C(A)^\perp = N(A^T)$.
   * Check Symmetry: $(I - P)^T = I^T - P^T = I - P \quad \checkmark$
   * Check Idempotency: $(I - P)^2 = I - 2P + P^2 = I - 2P + P = I - P \quad \checkmark$
   * Check Range: For any $\mathbf{e} \in N(A^T)$, $A^T\mathbf{e} = \mathbf{0} \implies P\mathbf{e} = A(A^TA)^{-1}A^T\mathbf{e} = \mathbf{0}$.
     Thus $(I - P)\mathbf{e} = \mathbf{e} - \mathbf{0} = \mathbf{e}$. $(I - P)$ leaves $N(A^T)$ untouched.

2. **The Invertible Matrix Trap**:
   * If $A$ is square $n \times n$ and invertible, then $A$ and $A^T$ are individually invertible.
   * Applying matrix inverse algebra:
     $$P = A(A^TA)^{-1}A^T = A A^{-1} (A^T)^{-1} A^T = I_n \cdot I_n = I_n$$
   * **The Trap Explained**: Students often attempt to split $(A^TA)^{-1} = A^{-1}(A^T)^{-1}$ for rectangular $m \times n$ matrices! For $m > n$, $A$ is NOT square, so $A^{-1}$ does NOT exist. You can only split $(A^TA)^{-1}$ when $A$ is square and invertible, in which case $C(A) = \mathbb{R}^n$, so projecting onto $C(A)$ is projecting onto the whole space, yielding $P = I$.

3. **Gram-Schmidt Dependency Failure**:
   * In Gram-Schmidt, step 3 computes $\mathbf{A}_3 = \mathbf{a}_3 - (\mathbf{q}_1^T\mathbf{a}_3)\mathbf{q}_1 - (\mathbf{q}_2^T\mathbf{a}_3)\mathbf{q}_2$.
   * If $\mathbf{a}_3 \in \text{span}\{\mathbf{a}_1, \mathbf{a}_2\}$, then $\mathbf{a}_3$ lies entirely in the plane already spanned by $\mathbf{q}_1$ and $\mathbf{q}_2$.
   * Subtracting its projections yields the **zero vector**: $\mathbf{A}_3 = \mathbf{0}$.
   * Normalization fails because $\|\mathbf{A}_3\| = 0$ (division by zero!). Gram-Schmidt detects linear dependence by producing $\mathbf{A}_j = \mathbf{0}$.

⚡ **Exam Shortcut / Quick Trick**:
If an exam question asks for the projection of $\mathbf{b}$ onto $C(A)$ where $A$ is a square invertible matrix, **do zero calculations**! The answer is $\mathbf{p} = \mathbf{b}$ and $P = I$.

---

# CHAPTER 5: Eigenvalues and Eigenvectors

---

## Topic 5.1: Eigenvalues, Diagonalization, & Real Symmetric Matrices

### Problem 5.1.1 (Level 1: Easy / Foundational) — Eigenvalues, Eigenvectors, & Matrix Powers
Given the matrix $A = \begin{bmatrix} 4 & 2 \ 1 & 3 \end{bmatrix}$:
1. Find the eigenvalues $\lambda_1, \lambda_2$ and their corresponding eigenvectors $\mathbf{x}_1, \mathbf{x}_2$.
2. Verify trace and determinant properties.
3. Diagonalize $A$ into $S\Lambda S^{-1}$ and use it to compute $A^5$.

```
[EIGENVECTOR AXES ROTATION]
          y ^                      y ^
            |  x_2 = [-1, 1]^T       |      x_1 = [2, 1]^T
            | /                      |     /
            |/                       |    /
  ----------+-----------> x  --------+---+-------> x
           /                         |  /
          /                          | /
         / (Lambda_2 = 2)            |/ (Lambda_1 = 5)
```

#### Detailed Solution:
1. **Eigenvalues**:
   $$\det(A - \lambda I) = \det\begin{bmatrix} 4-\lambda & 2 \ 1 & 3-\lambda \end{bmatrix} = (4-\lambda)(3-\lambda) - 2 = \lambda^2 - 7\lambda + 10 = 0$$
   $$(\lambda - 5)(\lambda - 2) = 0 \implies \lambda_1 = 5, \quad \lambda_2 = 2$$

2. **Eigenvectors**:
   * For $\lambda_1 = 5$:
     $$(A - 5I)\mathbf{x} = \begin{bmatrix} -1 & 2 \ 1 & -2 \end{bmatrix} \begin{bmatrix} x_1 \ x_2 \end{bmatrix} = \begin{bmatrix} 0 \ 0 \end{bmatrix} \implies -x_1 + 2x_2 = 0 \implies \mathbf{x}_1 = \begin{bmatrix} 2 \ 1 \end{bmatrix}$$
   * For $\lambda_2 = 2$:
     $$(A - 2I)\mathbf{x} = \begin{bmatrix} 2 & 2 \ 1 & 1 \end{bmatrix} \begin{bmatrix} x_1 \ x_2 \end{bmatrix} = \begin{bmatrix} 0 \ 0 \end{bmatrix} \implies x_1 + x_2 = 0 \implies \mathbf{x}_2 = \begin{bmatrix} -1 \ 1 \end{bmatrix}$$

3. **Trace and Determinant Check**:
   $$\text{trace}(A) = 4 + 3 = 7, \quad \lambda_1 + \lambda_2 = 5 + 2 = 7 \quad \checkmark$$
   $$\det(A) = (4)(3) - (2)(1) = 10, \quad \lambda_1 \cdot \lambda_2 = (5)(2) = 10 \quad \checkmark$$

4. **Diagonalization & Matrix Power $A^5$**:
   $$S = \begin{bmatrix} 2 & -1 \ 1 & 1 \end{bmatrix}, \quad \det(S) = 2 - (-1) = 3 \implies S^{-1} = \frac{1}{3}\begin{bmatrix} 1 & 1 \ -1 & 2 \end{bmatrix}$$
   $$\Lambda = \begin{bmatrix} 5 & 0 \ 0 & 2 \end{bmatrix} \implies \Lambda^5 = \begin{bmatrix} 3125 & 0 \ 0 & 32 \end{bmatrix}$$
   $$A^5 = S \Lambda^5 S^{-1} = \begin{bmatrix} 2 & -1 \ 1 & 1 \end{bmatrix} \begin{bmatrix} 3125 & 0 \ 0 & 32 \end{bmatrix} \left(\frac{1}{3}\begin{bmatrix} 1 & 1 \ -1 & 2 \end{bmatrix}\right)$$
   $$A^5 = \frac{1}{3} \begin{bmatrix} 6250 & -32 \ 3125 & 32 \end{bmatrix} \begin{bmatrix} 1 & 1 \ -1 & 2 \end{bmatrix} = \frac{1}{3} \begin{bmatrix} 6282 & 6186 \ 3093 & 3189 \end{bmatrix} = \begin{bmatrix} 2094 & 2062 \ 1031 & 1063 \end{bmatrix}$$

⚡ **Exam Shortcut / Quick Trick**:
For any $2 \times 2$ matrix, the characteristic equation is **always**:
$$\lambda^2 - \text{trace}(A)\lambda + \det(A) = 0$$
Skip computing $\det(A - \lambda I)$ manually! Just write $\lambda^2 - 7\lambda + 10 = 0$.

---

### Problem 5.1.2 (Level 2: Intermediate / Practical Application) — Dynamical Systems & Markov Chain Equilibrium
Two competing digital streaming services (Service A and Service B) share a total subscriber base. Every year:
* $20\%$ of Service A users switch to B ($80\%$ stay with A).
* $10\%$ of Service B users switch to A ($90\%$ stay with B).

1. Construct the Markov transition matrix $M$.
2. Find the eigenvalues and eigenvectors of $M$.
3. Find the steady-state subscriber distribution $\mathbf{u}_\infty$ as time $k \to \infty$.
4. Given an initial state $\mathbf{u}_0 = \begin{bmatrix} 0.6 \ 0.4 \end{bmatrix}$, derive the exact expression for $\mathbf{u}_k = M^k \mathbf{u}_0$ at year $k$.

```
[MARKOV TRANSITION GRAPH]
         0.80                      0.90
       +------+                  +------+
       |      |                  |      |
       v      |                  v      |
    (Service A) ---- 0.20 ----> (Service B)
                <--- 0.10 -----
```

#### Detailed Solution:
1. **Transition Matrix $M$**:
   Columns represent initial state, rows represent destination state:
   $$M = \begin{bmatrix} 0.8 & 0.1 \ 0.2 & 0.9 \end{bmatrix}$$

2. **Eigenvalues & Eigenvectors**:
   * $\text{trace}(M) = 0.8 + 0.9 = 1.7$.
   * $\det(M) = (0.8)(0.9) - (0.1)(0.2) = 0.72 - 0.02 = 0.70$.
   * Characteristic polynomial: $\lambda^2 - 1.7\lambda + 0.70 = (\lambda - 1)(\lambda - 0.7) = 0$.
     $$\lambda_1 = 1, \quad \lambda_2 = 0.7$$
   
   * **Eigenvector for $\lambda_1 = 1$**:
     $$(M - I)\mathbf{x} = \begin{bmatrix} -0.2 & 0.1 \ 0.2 & -0.1 \end{bmatrix} \begin{bmatrix} x_1 \ x_2 \end{bmatrix} = \mathbf{0} \implies -2x_1 + x_2 = 0 \implies \mathbf{x}_1 = \begin{bmatrix} 1 \ 2 \end{bmatrix}$$
   * **Eigenvector for $\lambda_2 = 0.7$**:
     $$(M - 0.7I)\mathbf{x} = \begin{bmatrix} 0.1 & 0.1 \ 0.2 & 0.2 \end{bmatrix} \begin{bmatrix} x_1 \ x_2 \end{bmatrix} = \mathbf{0} \implies x_1 + x_2 = 0 \implies \mathbf{x}_2 = \begin{bmatrix} 1 \ -1 \end{bmatrix}$$

3. **Steady-State Distribution $\mathbf{u}_\infty$**:
   Normalize $\mathbf{x}_1$ so components sum to $1$ ($x_1 + x_2 = 1$):
   $$\mathbf{u}_\infty = \frac{1}{1 + 2} \begin{bmatrix} 1 \ 2 \end{bmatrix} = \begin{bmatrix} 1/3 \ 2/3 \end{bmatrix} \approx \begin{bmatrix} 33.3\% \ 66.7\% \end{bmatrix}$$

4. **Exact Formula for $\mathbf{u}_k$**:
   Express $\mathbf{u}_0 = \begin{bmatrix} 0.6 \ 0.4 \end{bmatrix}$ as a linear combination of eigenvectors $c_1 \mathbf{x}_1 + c_2 \mathbf{x}_2$:
   $$\begin{bmatrix} 1 & 1 \ 2 & -1 \end{bmatrix} \begin{bmatrix} c_1 \ c_2 \end{bmatrix} = \begin{bmatrix} 0.6 \ 0.4 \end{bmatrix} \implies c_1 = 1/3, \quad c_2 = 4/15$$
   Applying $M^k$:
   $$\mathbf{u}_k = M^k \mathbf{u}_0 = c_1 \lambda_1^k \mathbf{x}_1 + c_2 \lambda_2^k \mathbf{x}_2 = \frac{1}{3} (1)^k \begin{bmatrix} 1 \ 2 \end{bmatrix} + \frac{4}{15} (0.7)^k \begin{bmatrix} 1 \ -1 \end{bmatrix}$$
   As $k \to \infty$, $(0.7)^k \to 0$, leaving $\mathbf{u}_\infty = \begin{bmatrix} 1/3 \ 2/3 \end{bmatrix}$.

⚡ **Exam Shortcut / Quick Trick**:
For any Markov matrix (positive entries, column sums = 1), **$\lambda_1 = 1$ is ALWAYS guaranteed**!
To find the steady state, skip eigenvalues entirely and solve $(M - I)\mathbf{x} = \mathbf{0}$ directly.

---

### Problem 5.1.3 (Level 3: Advanced / Tricky Exam Traps) — Invertibility vs. Diagonalizability & Spectral Theorem
1. **Diagonalizability vs. Invertibility**:
   *(a)* Construct a $2 \times 2$ matrix $A_1$ that is **Invertible but NOT Diagonalizable** (defective).
   *(b)* Construct a $2 \times 2$ matrix $A_2$ that is **Singular but Diagonalizable**.
2. **Spectral Theorem Decomposition**:
   For the real symmetric matrix $A = \begin{bmatrix} 3 & 1 \ 1 & 3 \end{bmatrix}$, express $A$ as a linear combination of rank-1 orthogonal projection matrices:
   $$A = \lambda_1 \mathbf{q}_1\mathbf{q}_1^T + \lambda_2 \mathbf{q}_2\mathbf{q}_2^T$$

```
[SPECTRAL DECOMPOSITION FOR SYMMETRIC MATRICES]
Matrix A = 4 * [1/2  1/2]  +  2 * [ 1/2 -1/2] = [3  1]
               [1/2  1/2]         [-1/2  1/2]   [1  3]
               (Eigenspace 1)     (Eigenspace 2)
```

#### Detailed Solution:
1. **Constructing Counterexample Matrices**:
   * *(a)* **Invertible but NOT Diagonalizable ($A_1$)**:
     Take $A_1 = \begin{bmatrix} 2 & 1 \ 0 & 2 \end{bmatrix}$.
     * $\det(A_1) = 4 \neq 0 \implies A_1$ is **Invertible**.
     * Eigenvalues: $\lambda_1 = \lambda_2 = 2$ (algebraic multiplicity 2).
     * Geometric multiplicity: $(A_1 - 2I)\mathbf{x} = \begin{bmatrix} 0 & 1 \ 0 & 0 \end{bmatrix}\mathbf{x} = \mathbf{0} \implies \mathbf{x} = c \begin{bmatrix} 1 \ 0 \end{bmatrix}$ (only 1 independent eigenvector).
     * Since geometric multiplicity ($1$) < algebraic multiplicity ($2$), $A_1$ is **defective / non-diagonalizable**.
   * *(b)* **Singular but Diagonalizable ($A_2$)**:
     Take $A_2 = \begin{bmatrix} 1 & 1 \ 1 & 1 \end{bmatrix}$.
     * $\det(A_2) = 0 \implies A_2$ is **Singular**.
     * Eigenvalues: $\lambda_1 = 2, \lambda_2 = 0$ (two distinct real eigenvalues).
     * Since $A_2$ has $n = 2$ distinct eigenvalues, $A_2$ is **fully diagonalizable**!

2. **Spectral Theorem Decomposition of $A = \begin{bmatrix} 3 & 1 \ 1 & 3 \end{bmatrix}$**:
   * Eigenvalues: $\text{trace} = 6, \det = 8 \implies \lambda^2 - 6\lambda + 8 = 0 \implies \lambda_1 = 4, \lambda_2 = 2$.
   * **Unit Eigenvectors**:
     * For $\lambda_1 = 4$: $(A - 4I)\mathbf{x} = \begin{bmatrix} -1 & 1 \ 1 & -1 \end{bmatrix}\mathbf{x} = \mathbf{0} \implies \mathbf{x}_1 = \begin{bmatrix} 1 \ 1 \end{bmatrix} \implies \mathbf{q}_1 = \frac{1}{\sqrt{2}}\begin{bmatrix} 1 \ 1 \end{bmatrix}$.
     * For $\lambda_2 = 2$: $(A - 2I)\mathbf{x} = \begin{bmatrix} 1 & 1 \ 1 & 1 \end{bmatrix}\mathbf{x} = \mathbf{0} \implies \mathbf{x}_2 = \begin{bmatrix} -1 \ 1 \end{bmatrix} \implies \mathbf{q}_2 = \frac{1}{\sqrt{2}}\begin{bmatrix} -1 \ 1 \end{bmatrix}$.
   * **Rank-1 Projection Matrices**:
     $$P_1 = \mathbf{q}_1\mathbf{q}_1^T = \frac{1}{2}\begin{bmatrix} 1 \ 1 \end{bmatrix} \begin{bmatrix} 1 & 1 \end{bmatrix} = \begin{bmatrix} 1/2 & 1/2 \ 1/2 & 1/2 \end{bmatrix}$$
     $$P_2 = \mathbf{q}_2\mathbf{q}_2^T = \frac{1}{2}\begin{bmatrix} -1 \ 1 \end{bmatrix} \begin{bmatrix} -1 & 1 \end{bmatrix} = \begin{bmatrix} 1/2 & -1/2 \ -1/2 & 1/2 \end{bmatrix}$$
   * **Spectral Expansion**:
     $$\lambda_1 P_1 + \lambda_2 P_2 = 4 \begin{bmatrix} 1/2 & 1/2 \ 1/2 & 1/2 \end{bmatrix} + 2 \begin{bmatrix} 1/2 & -1/2 \ -1/2 & 1/2 \end{bmatrix} = \begin{bmatrix} 2 & 2 \ 2 & 2 \end{bmatrix} + \begin{bmatrix} 1 & -1 \ -1 & 1 \end{bmatrix} = \begin{bmatrix} 3 & 1 \ 1 & 3 \end{bmatrix} = A \quad \checkmark$$

⚡ **Exam Shortcut / Quick Trick**:
Remember the golden rules for exam conceptual questions:
1. **Invertibility depends on $\lambda \neq 0$** ($\det(A) \neq 0$).
2. **Diagonalizability depends on having $n$ independent eigenvectors** (geometric multiplicity = algebraic multiplicity).
3. Invertibility and Diagonalizability are **completely independent properties**!
