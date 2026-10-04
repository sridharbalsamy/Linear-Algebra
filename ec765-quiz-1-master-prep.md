# NITK EC765 Linear Algebra & Matrix Methods: Quiz 1 Master Study & Question Bank

---

## OVERVIEW & SCOPE
This master preparation package is built directly from the official **EC765 Linear Algebra and Matrix Methods Objective Examination (Units 1 to 4)** from the Department of Electronics & Communication Engineering, NITK.

It contains:
1. **Part 1**: Every official question from **Section I (MCQs)**, **Section II (True/False with Justifications)**, and **Section III (One-Line Answers / Fill-in-the-Blanks)** with step-by-step mathematical proofs, geometric interpretations, and complete options analysis.
2. **Part 2**: Extended Concept & Variant Question Bank designed to cover every edge case, parameter shift, and conceptual trap related to Units 1–4.
3. **Part 3**: Summary Table & Exam Fast-Track Reference.

---

# PART 1: Official Quiz 1 Questions & Comprehensive Solutions

## SECTION I: Multiple Choice Questions (1 Mark Each)

---

### Question 1
**Question**: Which of the following best describes the core mathematical operation for solving "Cause-and-Effect" engineering problems using a linear model $A\mathbf{x} = \mathbf{b}$?
* **A.** Isolating individual input weights via independent columns
* **B.** Predicting future patterns using non-existent solutions
* **C.** Calculating the trace of an underdetermined resource allocation matrix
* **D.** Finding the infinite nullspace paths of a balanced system

* **Correct Answer**: **A**
* **Detailed Justification**:
  * In the linear model $A\mathbf{x} = \mathbf{b}$, the matrix $A = [\mathbf{a}_1 \; \mathbf{a}_2 \; \dots \; \mathbf{a}_n]$ represents the system/channel transfer characteristics where each column $\mathbf{a}_j$ represents the effect of a unit input at channel/feature $j$. 
  * The column picture expands $A\mathbf{x} = \mathbf{b}$ as $x_1 \mathbf{a}_1 + x_2 \mathbf{a}_2 + \dots + x_n \mathbf{a}_n = \mathbf{b}$.
  * Solving for $\mathbf{x}$ isolates the specific weights $x_j$ assigned to each independent column (cause) to produce the observed output vector $\mathbf{b}$ (effect).
* **Why Other Choices are Incorrect**:
  * **B** is absurd because engineering models do not use non-existent solutions for prediction.
  * **C** is incorrect because the trace (sum of diagonal entries) does not solve system equations or isolate input weights.
  * **D** describes homogeneous/unconstrained systems rather than the primary goal of recovering the cause vector $\mathbf{x}$ from an observed effect $\mathbf{b}$.

---

### Question 2
**Question**: In the context of fitting linear parameters using least squares, minimizing the squared error norm $\|A\mathbf{x} - \mathbf{b}\|^2$ is geometrically equivalent to:
* **A.** Projecting $\mathbf{b}$ onto the row space of $A$
* **B.** Projecting $\mathbf{b}$ onto the column space of $A$
* **C.** Finding the intersection of the nullspace and the left nullspace
* **D.** Maximizing the margin of the hyperplane

* **Correct Answer**: **B**
* **Detailed Justification**:
  * When $A\mathbf{x} = \mathbf{b}$ is inconsistent ($\mathbf{b} 
otin C(A)$), any output $A\mathbf{x}$ must lie inside the column space $C(A)$.
  * The vector $\mathbf{p} = A\hat{\mathbf{x}} \in C(A)$ that minimizes the distance $\|A\mathbf{x} - \mathbf{b}\|$ to $\mathbf{b}$ is the unique **orthogonal projection** of $\mathbf{b}$ onto $C(A)$.
  * The error vector $\mathbf{e} = \mathbf{b} - \mathbf{p}$ is perpendicular to $C(A)$, satisfying $A^T \mathbf{e} = \mathbf{0} \implies A^T (A\hat{\mathbf{x}} - \mathbf{b}) = \mathbf{0} \implies A^T A \hat{\mathbf{x}} = A^T \mathbf{b}$.
* **Why Other Choices are Incorrect**:
  * **A**: $\mathbf{b} \in \mathbb{R}^m$, whereas the row space $C(A^T) \subseteq \mathbb{R}^n$. Projection onto the row space applies to input vectors $\mathbf{x}$, not target vectors $\mathbf{b}$.
  * **C**: $N(A) \subseteq \mathbb{R}^n$ and $N(A^T) \subseteq \mathbb{R}^m$ reside in completely different vector spaces (unless $m=n$), and their intersection is not relevant to least squares.
  * **D**: Margin maximization is the objective of Support Vector Machines (SVMs), not standard least-squares parameter fitting.

---

### Question 3
**Question**: Let $A$ be a $4 	imes 5$ matrix representing an image's pixel replication data. If the row rank of $A$ is 2, what is the dimension of the left nullspace $N(A^T)$?
* **A.** 3
* **B.** 2
* **C.** 1
* **D.** 0

* **Correct Answer**: **B**
* **Detailed Justification**:
  * For any $m 	imes n$ matrix $A$, the fundamental identity of linear algebra states that $	ext{row rank}(A) = 	ext{column rank}(A) = r$. Here $m = 4$, $n = 5$, and $r = 2$.
  * The left nullspace $N(A^T)$ is a subspace of $\mathbb{R}^m = \mathbb{R}^4$.
  * By the Fundamental Theorem of Linear Algebra, $\dim N(A^T) = m - r = 4 - 2 = 2$.
* **Quick Calculation**:
  $$\dim N(A^T) = m - r = 4 - 2 = 2$$
  *(Note: $\dim N(A) = n - r = 5 - 2 = 3$, which corresponds to Choice A, a classic distractor!)*

---

### Question 4
**Question**: During the $PA = LDU$ factorization of an invertible $n 	imes n$ system used in forward propagation, what specific elements populate the diagonal matrix $D$?
* **A.** The eigenvalues of $A$
* **B.** The multipliers $l_{ij}$
* **C.** The non-zero pivots identified during elimination
* **D.** The determinants of the permutation matrix

* **Correct Answer**: **C**
* **Detailed Justification**:
  * Gaussian elimination transforms $A$ into an upper triangular matrix $U_{	ext{orig}}$ with pivots $d_1, d_2, \dots, d_n$ on its diagonal.
  * Factoring out these pivot values from each row of $U_{	ext{orig}}$ yields $U_{	ext{orig}} = D U$, where $D = 	ext{diag}(d_1, d_2, \dots, d_n)$ contains the non-zero pivots, and $U$ is a unit upper triangular matrix with 1s on its main diagonal.
  * Thus, $PA = LDU$, where $L$ is unit lower triangular, $D$ is diagonal with pivots, and $U$ is unit upper triangular.
* **Why Other Choices are Incorrect**:
  * **A**: Pivots $d_i$ are generally **not** equal to eigenvalues $\lambda_i$ (pivots change with row operations, eigenvalues do not).
  * **B**: Multipliers $l_{ij}$ populate the lower triangular matrix $L$, below its main diagonal of 1s.
  * **D**: Permutation matrix determinants are $\pm 1$ and do not populate $D$.

---

### Question 5
**Question**: The projection matrix $P = A(A^T A)^{-1} A^T$ used to project high-dimensional data onto lower-dimensional subspaces satisfies which of the following algebraic properties?
* **A.** $P = P^{-1}$ and $P = P^T$
* **B.** $P^2 = P$ and $P = P^T$
* **C.** $P^2 = I$ and $P^T = -P$
* **D.** $P = A^T A$

* **Correct Answer**: **B**
* **Detailed Justification**:
  1. **Symmetry ($P^T = P$)**:
     $$P^T = \left( A(A^T A)^{-1} A^T ight)^T = (A^T)^T \left( (A^T A)^{-1} ight)^T A^T = A (A^T A)^{-1} A^T = P$$
  2. **Idempotency ($P^2 = P$)**:
     $$P^2 = \left( A(A^T A)^{-1} A^T ight) \left( A(A^T A)^{-1} A^T ight) = A (A^T A)^{-1} (A^T A) (A^T A)^{-1} A^T = A (A^T A)^{-1} A^T = P$$
* **Physical/Geometric Meaning**:
  * Symmetry ensures orthogonal projection.
  * Idempotency means projecting an already projected vector leaves it unchanged ($P(P\mathbf{b}) = P\mathbf{b}$).

---

### Question 6
**Question**: A set of microphone inputs forms a data matrix $A$. A rank deficiency in $A$ physically implies that:
* **A.** The signals are completely uncorrelated.
* **B.** Certain microphones are capturing linearly dependent acoustic paths.
* **C.** The nullspace of the system is strictly the zero vector.
* **D.** The system requires an exact unique solution.

* **Correct Answer**: **B**
* **Detailed Justification**:
  * Each column (or row) of data matrix $A$ corresponds to an acoustic channel/microphone.
  * Rank deficiency ($r < \min(m,n)$) means the columns (or rows) are linearly dependent.
  * Physically, this signifies redundant information—i.e., one or more microphones are capturing acoustic paths that are linear combinations of the paths recorded by other microphones.
* **Why Other Choices are Incorrect**:
  * **A**: Uncorrelated signals yield linearly independent columns (full rank).
  * **C**: Rank deficiency means $\dim N(A) = n - r > 0$, so the nullspace contains non-zero vectors.
  * **D**: Rank deficiency destroys uniqueness of solutions for $A\mathbf{x} = \mathbf{b}$.

---

### Question 7
**Question**: If a homogeneous equation $A\mathbf{x} = \mathbf{0}$ is solved for a system where $n = 4$ variables and the matrix $A$ has a rank of $r = 2$, how many independent special solutions must be computed to form the complete basis for its nullspace $N(A)$?
* **A.** 0
* **B.** 1
* **C.** 2
* **D.** 4

* **Correct Answer**: **C**
* **Detailed Justification**:
  * By the Rank-Nullity Theorem, $	ext{rank}(A) + \dim N(A) = n$.
  * Given $n = 4$ and $r = 2$, the nullity is $\dim N(A) = n - r = 4 - 2 = 2$.
  * The number of special solutions obtained by setting one free variable to 1 and the others to 0 equals the number of free variables ($n - r = 2$). These 2 special solutions form a basis for $N(A)$.

---

### Question 8
**Question**: Which of the following is TRUE regarding abstract vector spaces over the real numbers?
* **A.** The union of two distinct subspaces is always a subspace.
* **B.** A subspace does not strictly require the inclusion of the zero vector.
* **C.** The intersection of any two subspaces of a vector space is always a valid subspace.
* **D.** A plane not passing through the origin is a valid subspace of $\mathbb{R}^3$.

* **Correct Answer**: **C**
* **Detailed Justification**:
  * **Proof for C**: Let $V_1$ and $V_2$ be two subspaces of $V$.
    1. Zero vector: Since $\mathbf{0} \in V_1$ and $\mathbf{0} \in V_2$, $\mathbf{0} \in V_1 \cap V_2$.
    2. Additive closure: If $\mathbf{u}, \mathbf{v} \in V_1 \cap V_2$, then $\mathbf{u}+\mathbf{v} \in V_1$ (since $V_1$ is a subspace) and $\mathbf{u}+\mathbf{v} \in V_2$ (since $V_2$ is a subspace). Thus $\mathbf{u}+\mathbf{v} \in V_1 \cap V_2$.
    3. Scalar multiplication closure: If $\mathbf{u} \in V_1 \cap V_2$ and $c \in \mathbb{R}$, $c\mathbf{u} \in V_1$ and $c\mathbf{u} \in V_2$, so $c\mathbf{u} \in V_1 \cap V_2$.
    *Conclusion*: $V_1 \cap V_2$ is always a valid subspace.
* **Why Other Choices are Incorrect**:
  * **A**: The union $V_1 \cup V_2$ is generally **not** a subspace (e.g., the union of the x-axis and y-axis in $\mathbb{R}^2$ is not closed under addition: $(1,0) + (0,1) = (1,1)$, which is on neither axis).
  * **B**: Every valid subspace **must** contain the zero vector $\mathbf{0}$ to satisfy closure under multiplication by scalar $c=0$.
  * **D**: A plane not passing through the origin does not contain $\mathbf{0} = (0,0,0)$, so it is an affine subset, not a vector subspace.

---

### Question 9
**Question**: In an overdetermined system ($m > n$) with full column rank operating in a noisy physical environment, the system equations typically yield:
* **A.** An infinite number of exact solutions
* **B.** Exactly one unique exact solution
* **C.** No exact solution, requiring an approximate least squares solution
* **D.** A minimum-norm exact solution

* **Correct Answer**: **C**
* **Detailed Justification**:
  * In an overdetermined system ($m > n$), there are more equations ($m$) than unknowns ($n$).
  * Full column rank means $r = n < m$. Thus, $C(A)$ is an $n$-dimensional subspace of $\mathbb{R}^m$.
  * Because $n < m$, $C(A)$ does not fill $\mathbb{R}^m$. In a noisy physical environment, the measurement vector $\mathbf{b} \in \mathbb{R}^m$ almost certainly has a component outside $C(A)$ ($\mathbf{b} 
otin C(A)$).
  * Therefore, no exact solution exists ($A\mathbf{x} = \mathbf{b}$ is inconsistent), forcing us to solve the normal equations $A^T A \hat{\mathbf{x}} = A^T \mathbf{b}$ for the unique least-squares solution $\hat{\mathbf{x}}$.

---

### Question 10
**Question**: In support vector classifiers, a decision boundary is defined by a hyperplane $\mathbf{w}^T \mathbf{x} + b = 0$. The geometric vector $\mathbf{w}$ represents:
* **A.** A vector parallel to the decision boundary.
* **B.** The vector orthogonal (normal) to the decision boundary hyperplane.
* **C.** The exact margin of separation between the classes.
* **D.** The projection of the data points onto the left nullspace.

* **Correct Answer**: **B**
* **Detailed Justification**:
  * For any two points $\mathbf{x}_1, \mathbf{x}_2$ lying on the decision hyperplane $\mathbf{w}^T \mathbf{x} + b = 0$:
    $$\mathbf{w}^T \mathbf{x}_1 + b = 0 \quad 	ext{and} \quad \mathbf{w}^T \mathbf{x}_2 + b = 0$$
  * Subtracting the two equations gives:
    $$\mathbf{w}^T (\mathbf{x}_1 - \mathbf{x}_2) = 0$$
  * Since $\mathbf{x}_1 - \mathbf{x}_2$ is a vector parallel to the hyperplane, $\mathbf{w}^T (\mathbf{x}_1 - \mathbf{x}_2) = 0$ proves that $\mathbf{w}$ is strictly **orthogonal (normal)** to every vector in the decision boundary hyperplane.

---

## SECTION II: True/False with Justification (2 Marks Each)

---

### Question 11
**Statement**: For an underdetermined resource allocation problem modeled as $A\mathbf{x} = \mathbf{b}$ where $m < n$ and the matrix has full row rank, the system will have no solution.

* **Answer**: **FALSE**
* **Official One-Line Justification**:
  > *False — Full row rank ($r = m$) $\implies C(A) = \mathbb{R}^m$, so every $\mathbf{b}$ is reachable; with $n - m$ free variables there are infinitely many solutions.*
* **Deep Mathematical Proof**:
  1. Full row rank means $r = m$. The column space $C(A) \subseteq \mathbb{R}^m$ has dimension $r = m$, which implies $C(A) = \mathbb{R}^m$.
  2. Since $C(A) = \mathbb{R}^m$, every target vector $\mathbf{b} \in \mathbb{R}^m$ lies inside $C(A)$. Hence, $A\mathbf{x} = \mathbf{b}$ is **always consistent**.
  3. The number of free variables is $n - r = n - m > 0$ (since $m < n$).
  4. With at least one free variable, setting free variables to arbitrary real parameters yields **infinitely many solutions**.
* **Concrete Example**:
  Let $A = egin{bmatrix} 1 & 0 & 2 \ 0 & 1 & 3 \end{bmatrix}$ ($2 	imes 3$, $m=2, n=3, r=2$). For any $\mathbf{b} = egin{bmatrix} b_1 \ b_2 \end{bmatrix}$:
  $$\mathbf{x} = egin{bmatrix} b_1 - 2x_3 \ b_2 - 3x_3 \ x_3 \end{bmatrix} = egin{bmatrix} b_1 \ b_2 \ 0 \end{bmatrix} + x_3 egin{bmatrix} -2 \ -3 \ 1 \end{bmatrix}$$
  For every $x_3 \in \mathbb{R}$, this is a valid solution.

---

### Question 12
**Statement**: The error vector $\mathbf{e} = \mathbf{b} - A\hat{\mathbf{x}}$ derived in a least squares approximation is strictly orthogonal to the left nullspace of the design matrix $A$.

* **Answer**: **FALSE**
* **Official One-Line Justification**:
  > *False — $A^T \mathbf{e} = \mathbf{0}$, so $\mathbf{e}$ lies IN the left nullspace $N(A^T)$; it is orthogonal to the column space $C(A)$, not to $N(A^T)$.*
* **Deep Mathematical Proof**:
  1. The least squares normal equations are $A^T A \hat{\mathbf{x}} = A^T \mathbf{b} \implies A^T (\mathbf{b} - A\hat{\mathbf{x}}) = \mathbf{0} \implies A^T \mathbf{e} = \mathbf{0}$.
  2. By definition, $N(A^T) = \{\mathbf{y} \in \mathbb{R}^m \mid A^T \mathbf{y} = \mathbf{0}\}$. Since $A^T \mathbf{e} = \mathbf{0}$, $\mathbf{e} \in N(A^T)$.
  3. By the Fundamental Theorem of Orthogonality, $\mathbb{R}^m = C(A) \oplus N(A^T)$, meaning $C(A) \perp N(A^T)$.
  4. Since $\mathbf{e} \in N(A^T)$, $\mathbf{e}$ is orthogonal to $C(A)$, **not** orthogonal to $N(A^T)$ (a vector cannot be orthogonal to the space it inhabits unless it is the zero vector).

---

### Question 13
**Statement**: In the factorization $A = LU$, the lower triangular matrix $L$ strictly records the elimination multipliers $l_{ij}$ and requires no row swaps to have occurred.

* **Answer**: **TRUE**
* **Official One-Line Justification**:
  > *True — $A = LU$ holds only when no row exchanges are needed (otherwise $PA = LU$); $L$ has 1s on its diagonal and the multipliers $l_{ij}$ below it.*
* **Deep Mathematical Proof**:
  1. Forward elimination without row exchanges applies lower triangular elementary matrices $E_{ij}$:
     $$E_{k} \dots E_2 E_1 A = U \implies A = (E_1^{-1} E_2^{-1} \dots E_k^{-1}) U = L U$$
  2. Each inverse $E_{ij}^{-1}$ simply puts the multiplier $l_{ij}$ in the $(i,j)$ position below the diagonal.
  3. When no row exchanges occur, the multipliers $l_{ij}$ fit directly into $L$ without shifting positions. If row exchanges are required, permutation matrix $P$ must be introduced, yielding $PA = LU$ or $A = LPU$.

---

### Question 14
**Statement**: If an autoencoder's data matrix $A$ has a nullspace containing only the zero vector, it implies the data features (columns) contain linear redundancies that can be further compressed.

* **Answer**: **FALSE**
* **Official One-Line Justification**:
  > *False — $N(A) = \{\mathbf{0}\} \implies$ the columns are linearly independent (full column rank), so there is no redundancy left to compress.*
* **Deep Mathematical Proof**:
  1. $N(A) = \{\mathbf{0}\} \iff A\mathbf{x} = \mathbf{0}$ has only the trivial solution $\mathbf{x} = \mathbf{0}$.
  2. By definition of linear independence, $x_1 \mathbf{a}_1 + x_2 \mathbf{a}_2 + \dots + x_n \mathbf{a}_n = \mathbf{0} \implies x_1 = x_2 = \dots = x_n = 0$.
  3. This means all feature columns $\mathbf{a}_j$ are linearly independent (rank $r = n$).
  4. Since no feature column can be written as a combination of others, there are zero linear redundancies among the features. Compression requires linear dependency ($r < n \implies \dim N(A) > 0$).

---

### Question 15
**Statement**: When computing the normal equations $A^T A \hat{\mathbf{x}} = A^T \mathbf{b}$, the square matrix $A^T A$ is guaranteed to be invertible as long as $A$ has full column rank.

* **Answer**: **TRUE**
* **Official One-Line Justification**:
  > *True — $A^T A \mathbf{x} = \mathbf{0} \implies \mathbf{x}^T A^T A \mathbf{x} = \|A\mathbf{x}\|^2 = 0 \implies A\mathbf{x} = \mathbf{0} \implies \mathbf{x} = \mathbf{0}$ (independent columns), so $A^T A$ is invertible.*
* **Deep Mathematical Proof**:
  1. $A^T A$ is an $n 	imes n$ square matrix. It is invertible if and only if $N(A^T A) = \{\mathbf{0}\}$.
  2. Suppose $A^T A \mathbf{x} = \mathbf{0}$.
  3. Premultiply by $\mathbf{x}^T$:
     $$\mathbf{x}^T A^T A \mathbf{x} = (A\mathbf{x})^T (A\mathbf{x}) = \|A\mathbf{x}\|^2 = 0$$
  4. $\|A\mathbf{x}\|^2 = 0 \implies A\mathbf{x} = \mathbf{0}$.
  5. Since $A$ has full column rank ($r = n$), its columns are linearly independent, so $N(A) = \{\mathbf{0}\}$.
  6. Therefore, $A\mathbf{x} = \mathbf{0} \implies \mathbf{x} = \mathbf{0}$.
  7. This proves $N(A^T A) = \{\mathbf{0}\}$, so $A^T A$ is invertible.

---

### Question 16
**Statement**: The specific pivot columns of the original matrix $A$ always form a mathematically valid basis for its Column Space $C(A)$.

* **Answer**: **TRUE**
* **Official One-Line Justification**:
  > *True — Row operations preserve column dependencies, so the columns of $A$ at $R$'s pivot positions are independent and span $C(A)$.*
* **Deep Mathematical Proof**:
  1. Elementary row operations correspond to premultiplication by an invertible matrix $M$: $R = MA$.
  2. Linear combinations among columns are preserved: $A\mathbf{x} = \mathbf{0} \iff (MA)\mathbf{x} = M\mathbf{0} \iff R\mathbf{x} = \mathbf{0}$.
  3. The pivot columns of $R$ are clearly linearly independent and span $C(R)$.
  4. Because column relationships are identical between $A$ and $R$, the corresponding columns of the **original matrix $A$** (not $R$!) are linearly independent and span $C(A)$.

---

### Question 17
**Statement**: For a non-homogeneous system $A\mathbf{x} = \mathbf{b}$ to have an exact valid solution, the target vector $\mathbf{b}$ must be strictly orthogonal to the column space $C(A)$.

* **Answer**: **FALSE**
* **Official One-Line Justification**:
  > *False — $\mathbf{b}$ must lie IN $C(A)$ ($\mathbf{b}$ must be a combination of the columns of $A$), not be orthogonal to it.*
* **Deep Mathematical Proof**:
  1. $A\mathbf{x} = x_1 \mathbf{a}_1 + x_2 \mathbf{a}_2 + \dots + x_n \mathbf{a}_n$.
  2. The set of all possible outputs $A\mathbf{x}$ is, by definition, the column space $C(A) = 	ext{span}(\mathbf{a}_1, \dots, \mathbf{a}_n)$.
  3. Thus, $A\mathbf{x} = \mathbf{b}$ has a solution if and only if $\mathbf{b} \in C(A)$.
  4. If $\mathbf{b} \perp C(A)$ and $\mathbf{b} 
eq \mathbf{0}$, then $\mathbf{b} \in N(A^T)$, meaning $\mathbf{b}$ has zero projection onto $C(A)$, making $A\mathbf{x} = \mathbf{b}$ completely unsolvable.

---

### Question 18
**Statement**: The dimension of the column space $C(A)$ plus the dimension of the row space $C(A^T)$ always equals the total number of columns $n$.

* **Answer**: **FALSE**
* **Official One-Line Justification**:
  > *False — $\dim C(A) + \dim C(A^T) = 2r$. The identity is $\dim C(A^T) + \dim N(A) = r + (n - r) = n$.*
* **Deep Mathematical Proof**:
  1. $\dim C(A) = r$ (rank) and $\dim C(A^T) = r$ (row rank = column rank).
  2. Therefore, $\dim C(A) + \dim C(A^T) = r + r = 2r$, which equals $n$ only in the special case where $2r = n \implies r = n/2$.
  3. The correct Rank-Nullity identity connecting to $n$ is:
     $$\dim C(A^T) + \dim N(A) = r + (n - r) = n$$

---

### Question 19
**Statement**: The minimum distance (margin) between two parallel hyperplanes $\mathbf{w}^T \mathbf{x} + b = 1$ and $\mathbf{w}^T \mathbf{x} + b = -1$ in a classification context is purely determined by the magnitude of the bias scalar $b$.

* **Answer**: **FALSE**
* **Official One-Line Justification**:
  > *False — Margin $= rac{2}{\|\mathbf{w}\|}$, which depends only on $\|\mathbf{w}\|$; the bias $b$ merely shifts the hyperplanes.*
* **Deep Mathematical Proof**:
  1. Let $\mathbf{x}_1$ lie on $\mathbf{w}^T \mathbf{x} + b = 1$ and $\mathbf{x}_2$ lie on $\mathbf{w}^T \mathbf{x} + b = -1$.
  2. Subtracting the two equations gives $\mathbf{w}^T (\mathbf{x}_1 - \mathbf{x}_2) = 2$.
  3. The unit normal vector to the hyperplanes is $\hat{\mathbf{n}} = rac{\mathbf{w}}{\|\mathbf{w}\|}$.
  4. The geometric margin $M$ is the projection of $(\mathbf{x}_1 - \mathbf{x}_2)$ onto $\hat{\mathbf{n}}$:
     $$M = \hat{\mathbf{n}}^T (\mathbf{x}_1 - \mathbf{x}_2) = rac{\mathbf{w}^T (\mathbf{x}_1 - \mathbf{x}_2)}{\|\mathbf{w}\|} = rac{2}{\|\mathbf{w}\|}$$
  5. The bias scalar $b$ cancels out completely in $\mathbf{x}_1 - \mathbf{x}_2$, proving that $M$ depends solely on $\|\mathbf{w}\|$.

---

### Question 20
**Statement**: When a matrix $A$ is converted to its Reduced Row Echelon Form (RREF), the sub-block $F$ representing the free columns can be directly utilized to construct the exact nullspace basis matrix $N$.

* **Answer**: **TRUE**
* **Official One-Line Justification**:
  > *True — For $R = egin{bmatrix} I & F \ 0 & 0 \end{bmatrix}$, the nullspace matrix $N = egin{bmatrix} -F \ I \end{bmatrix}$ (up to column ordering) satisfies $RN = 0$.*
* **Deep Mathematical Proof**:
  1. Reorder variables so that the $r$ pivot columns come first:
     $$R = egin{bmatrix} I_r & F \ 0 & 0 \end{bmatrix}$$
     where $I_r$ is $r 	imes r$ and $F$ is $r 	imes (n-r)$.
  2. Partition $\mathbf{x} = egin{bmatrix} \mathbf{x}_r \ \mathbf{x}_f \end{bmatrix}$, where $\mathbf{x}_r$ are pivot variables and $\mathbf{x}_f$ are free variables.
  3. $R\mathbf{x} = \mathbf{0} \implies I_r \mathbf{x}_r + F \mathbf{x}_f = \mathbf{0} \implies \mathbf{x}_r = -F \mathbf{x}_f$.
  4. Expressing $\mathbf{x}$ in terms of free variables $\mathbf{x}_f$:
     $$\mathbf{x} = egin{bmatrix} -F \mathbf{x}_f \ \mathbf{x}_f \end{bmatrix} = egin{bmatrix} -F \ I_{n-r} \end{bmatrix} \mathbf{x}_f$$
  5. Thus, $N = egin{bmatrix} -F \ I_{n-r} \end{bmatrix}$ is the nullspace matrix whose columns are the special solutions.

---

## SECTION III: One-Line Answers / Fill in the Blanks (1 Mark Each)

---

### Question 21
**Question**: In system modeling, a matrix with full column rank but $m > n$ generally produces a(n) ________ solution rather than an exact match due to environmental noise.
* **Exact Answer**: **least squares** (or **approximate least squares**)
* **Explanation**: Overdetermined systems ($m > n$) with full column rank $r = n$ generally have $\mathbf{b} 
otin C(A)$ due to noise, requiring the minimization of $\|A\mathbf{x} - \mathbf{b}\|^2$ via least squares.

---

### Question 22
**Question**: The theorem linking the four fundamental subspaces states that the nullspace $N(A)$ is the orthogonal complement to the ________.
* **Exact Answer**: **row space $C(A^T)$** (or **row space**)
* **Explanation**: In $\mathbb{R}^n$, $N(A) = C(A^T)^\perp$. Every vector in the nullspace is perpendicular to every vector in the row space ($A\mathbf{x} = \mathbf{0}$).

---

### Question 23
**Question**: For an orthogonal projection matrix $P$, the geometric operation of projecting a vector $\mathbf{b}$ that already lies entirely within the target subspace results in what mathematical outcome?
* **Exact Answer**: $P\mathbf{b} = \mathbf{b}$ (the vector is unchanged)
* **Explanation**: If $\mathbf{b} \in C(A)$, then $\mathbf{b} = A\mathbf{x}$ for some $\mathbf{x}$. Thus $P\mathbf{b} = A(A^T A)^{-1} A^T (A\mathbf{x}) = A(A^T A)^{-1} (A^T A) \mathbf{x} = A\mathbf{x} = \mathbf{b}$.

---

### Question 24
**Question**: What specific matrix is used to systematically track and apply necessary row exchanges when a zero appears in a pivot position during Gauss-Jordan elimination?
* **Exact Answer**: **Permutation matrix $P$** (or **row-exchange matrix**)
* **Explanation**: A permutation matrix $P$ is created by permuting the rows of the identity matrix $I$. Multiplying $P A$ reorders the rows of $A$ so that non-zero entries are placed in pivot positions.

---

### Question 25
**Question**: The rank $r$ of a matrix $A$ indicates the exact number of ________ columns in the matrix.
* **Exact Answer**: **linearly independent**
* **Explanation**: By definition, $	ext{rank}(A) = r$ is the maximum number of linearly independent columns (which also equals the maximum number of linearly independent rows).

---

### Question 26
**Question**: State the specific mathematical equation (normal equations) derived by taking the calculus derivative of the squared error norm $\|A\mathbf{x} - \mathbf{b}\|^2$ and setting it to zero.
* **Exact Answer**: $A^T A \hat{\mathbf{x}} = A^T \mathbf{b}$
* **Explanation**: Expanding $E(\mathbf{x}) = (A\mathbf{x} - \mathbf{b})^T (A\mathbf{x} - \mathbf{b}) = \mathbf{x}^T A^T A \mathbf{x} - 2\mathbf{x}^T A^T \mathbf{b} + \mathbf{b}^T \mathbf{b}$. Taking the gradient $
abla_{\mathbf{x}} E = 2 A^T A \mathbf{x} - 2 A^T \mathbf{b} = \mathbf{0} \implies A^T A \hat{\mathbf{x}} = A^T \mathbf{b}$.

---

### Question 27
**Question**: In a cause-and-effect matrix model, if the data columns are found to be perfectly linearly dependent, the matrix is said to be ________.
* **Exact Answer**: **rank deficient** (or **singular**)
* **Explanation**: When columns are linearly dependent, $r < \min(m,n)$, which is the definition of rank deficiency.

---

### Question 28
**Question**: In the complete factorization $PA = LDU$, what does the matrix $U$ stand for after the pivots have been extracted into the $D$ matrix?
* **Exact Answer**: **Unit upper triangular matrix** (or **upper triangular matrix with 1s on the diagonal**)
* **Explanation**: Extracting pivot values $d_i$ into $D = 	ext{diag}(d_1, \dots, d_n)$ leaves $1$s on the main diagonal of $U$.

---

### Question 29
**Question**: If a $5 	imes 7$ matrix $A$ has a rank of 3, what is the exact dimension of the left nullspace $N(A^T)$?
* **Exact Answer**: **2**
* **Explanation**: Here $m = 5$, $n = 7$, $r = 3$. The left nullspace $N(A^T) \subseteq \mathbb{R}^m = \mathbb{R}^5$, so $\dim N(A^T) = m - r = 5 - 3 = 2$.

---

### Question 30
**Question**: When establishing a decision boundary $\mathbf{w}^T \mathbf{x} + b = 0$, if the norm $\|\mathbf{w}\|$ is intentionally minimized during optimization, what happens to the geometric width of the classification margin?
* **Exact Answer**: **The margin width increases** (or **widens / is maximized**)
* **Explanation**: The classification margin is $M = rac{2}{\|\mathbf{w}\|}$. Minimizing $\|\mathbf{w}\|$ in the denominator maximizes $M$.

---

# PART 2: Comprehensive Nook-and-Corner Variant Questions

This section provides 10 extra exam-style questions with full solutions to ensure no topic from Units 1–4 goes unmastered.

---

### Variant Problem 1: Dimension Counting Across Subspaces
**Question**: Suppose $A$ is an $8 	imes 6$ matrix with a nullspace $N(A)$ spanned by 2 independent vectors.
1. What is the rank $r$ of matrix $A$?
2. What are the dimensions of all four fundamental subspaces?
3. Is the system $A\mathbf{x} = \mathbf{b}$ guaranteed to be solvable for every $\mathbf{b} \in \mathbb{R}^8$?

**Solution**:
1. **Rank $r$**: $m = 8$, $n = 6$. $\dim N(A) = n - r \implies 2 = 6 - r \implies r = 4$.
2. **Dimensions of Four Subspaces**:
   * $\dim C(A) = r = 4$
   * $\dim C(A^T) = r = 4$
   * $\dim N(A) = n - r = 6 - 4 = 2$
   * $\dim N(A^T) = m - r = 8 - 4 = 4$
3. **Solvability**: No. $C(A)$ is a 4-dimensional subspace of $\mathbb{R}^8$. Since $r = 4 < m = 8$, $C(A) 
eq \mathbb{R}^8$. Any $\mathbf{b}$ with a component in $N(A^T)$ cannot be reached.

---

### Variant Problem 2: Projection Matrix Properties
**Question**: Let $P$ be an $m 	imes m$ projection matrix onto a subspace $S$. Prove that:
1. $I - P$ is also a projection matrix.
2. The column space of $I - P$ is $S^\perp$.
3. $P(I - P) = \mathbf{0}$.

**Solution**:
1. **Symmetry**: $(I - P)^T = I^T - P^T = I - P$ (since $P^T = P$).
   **Idempotency**: $(I - P)^2 = I - 2P + P^2 = I - 2P + P = I - P$ (since $P^2 = P$). Thus $I - P$ is a projection matrix.
2. For any $\mathbf{b} \in \mathbb{R}^m$, $\mathbf{b} = P\mathbf{b} + (I - P)\mathbf{b} = \mathbf{p} + \mathbf{e}$. Since $\mathbf{p} \in S$, the error $\mathbf{e} = (I - P)\mathbf{b}$ is orthogonal to $S$, so $C(I - P) = S^\perp = N(A^T)$.
3. $P(I - P) = P - P^2 = P - P = \mathbf{0}$. This confirms that any vector projected by $I - P$ lies in the nullspace of $P$.

---

### Variant Problem 3: Least Squares & $QR$ Factorization
**Question**: Given $A = QR$ where $Q$ is $m 	imes n$ with orthonormal columns ($Q^T Q = I_n$) and $R$ is $n 	imes n$ upper triangular and invertible:
1. Express the least-squares solution $\hat{\mathbf{x}}$ in terms of $Q, R,$ and $\mathbf{b}$.
2. Express the projection matrix $P$ onto $C(A)$ in terms of $Q$.

**Solution**:
1. Normal equations: $A^T A \hat{\mathbf{x}} = A^T \mathbf{b}$.
   Substitute $A = QR$:
   $$(QR)^T (QR) \hat{\mathbf{x}} = (QR)^T \mathbf{b} \implies R^T (Q^T Q) R \hat{\mathbf{x}} = R^T Q^T \mathbf{b}$$
   Since $Q^T Q = I$:
   $$R^T R \hat{\mathbf{x}} = R^T Q^T \mathbf{b}$$
   Multiply by $(R^T)^{-1}$ (since $R$ is invertible):
   $$R \hat{\mathbf{x}} = Q^T \mathbf{b} \implies \hat{\mathbf{x}} = R^{-1} Q^T \mathbf{b}$$
2. Projection vector:
   $$\mathbf{p} = A \hat{\mathbf{x}} = (QR) (R^{-1} Q^T \mathbf{b}) = Q Q^T \mathbf{b}$$
   Therefore, the projection matrix is simply $P = Q Q^T$.

---

### Variant Problem 4: SVM Hyperplane Geometry
**Question**: A linear classifier in $\mathbb{R}^2$ has the decision boundary $3x_1 - 4x_2 + 6 = 0$.
1. Find the normal vector $\mathbf{w}$ and bias $b$.
2. Calculate the perpendicular distance from the origin $(0,0)$ to the boundary.
3. If the margin hyperplanes are $3x_1 - 4x_2 + 6 = 1$ and $3x_1 - 4x_2 + 6 = -1$, calculate the exact margin width $M$.

**Solution**:
1. $\mathbf{w} = egin{bmatrix} 3 \ -4 \end{bmatrix}$, $b = 6$.
2. Perpendicular distance from origin:
   $$d = rac{|b|}{\|\mathbf{w}\|} = rac{|6|}{\sqrt{3^2 + (-4)^2}} = rac{6}{5} = 1.2$$
3. Margin width:
   $$M = rac{2}{\|\mathbf{w}\|} = rac{2}{\sqrt{9 + 16}} = rac{2}{5} = 0.4$$

---

### Variant Problem 5: Rank & Subspace Relations
**Question**: True or False? "If $A$ and $B$ are $n 	imes n$ matrices of rank $n$, then $A + B$ must also have rank $n$." Provide a proof or counterexample.

**Solution**:
* **Answer**: **FALSE**
* **Counterexample**:
  Let $A = I_n = egin{bmatrix} 1 & 0 \ 0 & 1 \end{bmatrix}$ ($	ext{rank} = 2$) and $B = -I_n = egin{bmatrix} -1 & 0 \ 0 & -1 \end{bmatrix}$ ($	ext{rank} = 2$).
  $$A + B = egin{bmatrix} 0 & 0 \ 0 & 0 \end{bmatrix} \implies 	ext{rank}(A + B) = 0 
eq 2$$
* **Key Concept**: Rank is **subadditive**: $	ext{rank}(A + B) \le 	ext{rank}(A) + 	ext{rank}(B)$, but invertibility/full rank is not preserved under matrix addition.

---

# PART 3: Summary Table & Exam Fast-Track Reference

| Concept / Fundamental Subspace | Mathematical Definition | Containing Vector Space | Dimension Formula | Orthogonal Complement |
| :--- | :--- | :--- | :--- | :--- |
| **Column Space $C(A)$** | $	ext{span}(	ext{columns of } A)$ | $\mathbb{R}^m$ | $r$ (rank) | $N(A^T)$ (Left Nullspace) |
| **Row Space $C(A^T)$** | $	ext{span}(	ext{rows of } A)$ | $\mathbb{R}^n$ | $r$ (row rank = rank) | $N(A)$ (Nullspace) |
| **Nullspace $N(A)$** | $\{\mathbf{x} \in \mathbb{R}^n \mid A\mathbf{x} = \mathbf{0}\}$ | $\mathbb{R}^n$ | $n - r$ (nullity) | $C(A^T)$ (Row Space) |
| **Left Nullspace $N(A^T)$** | $\{\mathbf{y} \in \mathbb{R}^m \mid A^T \mathbf{y} = \mathbf{0}\}$ | $\mathbb{R}^m$ | $m - r$ | $C(A)$ (Column Space) |

### Key Identities to Memorize for Exams:
1. **Rank-Nullity Theorem**: $	ext{rank}(A) + \dim N(A) = n$
2. **Left Nullspace Dimension**: $	ext{rank}(A) + \dim N(A^T) = m$
3. **Least Squares Normal Equations**: $A^T A \hat{\mathbf{x}} = A^T \mathbf{b}$
4. **Projection Matrix**: $P = A(A^T A)^{-1} A^T \quad (P^2 = P, P^T = P)$
5. **Simplified Projection with Orthonormal $Q$**: $P = Q Q^T \quad (Q^T Q = I)$
6. **SVM Margin**: $M = rac{2}{\|\mathbf{w}\|}$
7. **Factorization**: $PA = LDU$ ($L$: unit lower triangular, $D$: diagonal pivots, $U$: unit upper triangular)
