# Real-World Diagonalization & Spectral Theory Master Package
## Applied Problem Set & Solutions Grounded in Strang's Linear Algebra

---

## Executive Summary & Core Theoretical Pillars

Diagonalization ($A = S \Lambda S^{-1}$) is the central engine for uncoupling complex multi-variable systems into independent 1D channels. In physical engineering, machine learning, and signal processing:
1. **Eigenvalues ($\lambda_i$)** dictate system rates of growth, decay, frequency of oscillation, or energy dominance.
2. **Eigenvectors ($\mathbf{x}_i$)** define the natural modes, principal axes, or steady-state equilibrium profiles.
3. **Diagonalization ($S \Lambda S^{-1}$)** transforms coupled differential or difference equations ($\mathbf{x}[k+1] = A\mathbf{x}[k]$ or $\frac{d\mathbf{u}}{dt} = A\mathbf{u}(t)$) into uncoupled scalar equations ($\mathbf{v}[k+1] = \Lambda \mathbf{v}[k]$).

---

## Problem Set Overview

| Level | Topic & Application Theme | Core Theoretical Concept | Key Exam Trap / Shortcut |
| :--- | :--- | :--- | :--- |
| **Level 1** | **IoT Sensor Calibration Loop** | $2 \times 2$ Diagonalization & State Trajectory ($A^k = S \Lambda^k S^{-1}$) | Solving $c_1, c_2$ without inverting $S$ |
| **Level 2** | **Cloud Load Balancing & Markov Dynamics** | $2 \times 2$ Stochastic Transition Matrix ($M^k \to M^\infty$) | Steady-state shortcut $(M - I)\mathbf{x} = \mathbf{0}$ |
| **Level 3** | **Chemical Chamber Diffusion Network** | $3 \times 3$ Continuous System & Matrix Exponential ($e^{At} = S e^{\Lambda t} S^{-1}$) | Thermal/Mass conservation law check |
| **Level 4** | **Resonant Motor Control Feedback** | Tricky Non-Diagonalizable / Defective Matrix & Jordan Form | $k \lambda^{k-1}$ secular growth resonance trap |
| **Level 5** | **Acoustic Array Covariance & PCA** | Real Symmetric Spectral Theorem ($A = Q \Lambda Q^T = \sum \lambda_i \mathbf{q}_i \mathbf{q}_i^T$) | Outer product expansion & low-rank filtering |

---

## PROBLEM 1 (Level 1 — Foundational)
### Topic: IoT Dual-Sensor Cross-Sensitivity & Thermal Drift
*Grounded in Gilbert Strang, Section 5.1 & 5.2*

#### Scenario & Real-World Context:
A micro-sensor module deployed in an industrial IoT environment measures Temperature ($T[k]$) and Relative Humidity ($H[k]$) at discrete time steps $k$. Due to sensor cross-sensitivity and heat dissipation, the updated state vector $\mathbf{x}[k] = \begin{bmatrix} T[k] \\ H[k] \end{bmatrix}$ evolves according to the linear feedback model:
$$\mathbf{x}[k+1] = A \mathbf{x}[k], \quad \text{where } A = \begin{bmatrix} 4 & -5 \\ 2 & -3 \end{bmatrix}$$
The initial uncalibrated measurement state at $k=0$ is $\mathbf{x}[0] = \begin{bmatrix} 8 \\ 5 \end{bmatrix}$.

#### Questions:
1. Find the eigenvalues $\lambda_1, \lambda_2$ and corresponding eigenvector matrix $S$ for $A$.
2. Compute $S^{-1}$ and write out the explicit factorization $A = S \Lambda S^{-1}$.
3. Derive an explicit closed-form formula for $\mathbf{x}[k] = A^k \mathbf{x}[0]$ as a linear combination of pure exponential powers $\lambda_1^k \mathbf{x}_1$ and $\lambda_2^k \mathbf{x}_2$.
4. **Physical Stability Analysis**: Determine whether the system converges to equilibrium or exhibits thermal runaway as $k \to \infty$. Identify which mode dominates.

---

### Full Step-by-Step Solution:

#### Step 1: Eigenvalues and Eigenvectors
Find roots of the characteristic polynomial $\det(A - \lambda I) = 0$:
$$\det \begin{bmatrix} 4 - \lambda & -5 \\ 2 & -3 - \lambda \end{bmatrix} = (4 - \lambda)(-3 - \lambda) - (-10) = \lambda^2 - \lambda - 2 = 0$$
Factoring yields:
$$(\lambda - 2)(\lambda + 1) = 0 \implies \lambda_1 = 2, \quad \lambda_2 = -1$$

* **For $\lambda_1 = 2$**:
  $$(A - 2I)\mathbf{x}_1 = \begin{bmatrix} 2 & -5 \\ 2 & -5 \end{bmatrix} \begin{bmatrix} y \\ z \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix} \implies 2y - 5z = 0 \implies \mathbf{x}_1 = \begin{bmatrix} 5 \\ 2 \end{bmatrix}$$

* **For $\lambda_2 = -1$**:
  $$(A - (-1)I)\mathbf{x}_2 = \begin{bmatrix} 5 & -5 \\ 2 & -2 \end{bmatrix} \begin{bmatrix} y \\ z \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix} \implies y - z = 0 \implies \mathbf{x}_2 = \begin{bmatrix} 1 \\ 1 \end{bmatrix}$$

#### Step 2: Construct $S$, $S^{-1}$, and $\Lambda$
$$S = [\mathbf{x}_1 \; \mathbf{x}_2] = \begin{bmatrix} 5 & 1 \\ 2 & 1 \end{bmatrix}$$
Determinant $\det(S) = (5)(1) - (1)(2) = 3$.
$$S^{-1} = \frac{1}{3} \begin{bmatrix} 1 & -1 \\ -2 & 5 \end{bmatrix}$$
$$\Lambda = \begin{bmatrix} 2 & 0 \\ 0 & -1 \end{bmatrix}$$
Thus $A = S \Lambda S^{-1} = \begin{bmatrix} 5 & 1 \\ 2 & 1 \end{bmatrix} \begin{bmatrix} 2 & 0 \\ 0 & -1 \end{bmatrix} \begin{bmatrix} 1/3 & -1/3 \\ -2/3 & 5/3 \end{bmatrix}$.

#### Step 3: Closed-Form State Formula
The state at step $k$ is given by:
$$\mathbf{x}[k] = A^k \mathbf{x}[0] = S \Lambda^k S^{-1} \mathbf{x}[0]$$
First, calculate the combination coefficients $\mathbf{c} = \begin{bmatrix} c_1 \\ c_2 \end{bmatrix} = S^{-1} \mathbf{x}[0]$:
$$\mathbf{c} = \frac{1}{3} \begin{bmatrix} 1 & -1 \\ -2 & 5 \end{bmatrix} \begin{bmatrix} 8 \\ 5 \end{bmatrix} = \frac{1}{3} \begin{bmatrix} 8 - 5 \\ -16 + 25 \end{bmatrix} = \begin{bmatrix} 1 \\ 3 \end{bmatrix}$$
Therefore, $\mathbf{x}[k]$ is:
$$\mathbf{x}[k] = c_1 \lambda_1^k \mathbf{x}_1 + c_2 \lambda_2^k \mathbf{x}_2 = 1 \cdot (2)^k \begin{bmatrix} 5 \\ 2 \end{bmatrix} + 3 \cdot (-1)^k \begin{bmatrix} 1 \\ 1 \end{bmatrix}$$
In scalar components:
$$T[k] = 5 \cdot 2^k + 3 \cdot (-1)^k$$
$$H[k] = 2 \cdot 2^k + 3 \cdot (-1)^k$$

#### Step 4: Physical Stability Analysis
* Because $|\lambda_1| = 2 > 1$, the mode $\mathbf{x}_1 = \begin{bmatrix} 5 \\ 2 \end{bmatrix}$ grows exponentially by a factor of $2$ at every step.
* The system is **unstable** and exhibits thermal runaway. As $k \to \infty$, the state vector aligns completely with the unstable eigenvector $\mathbf{x}_1$, causing sensor output saturation.

---

### ⚡ Exam Fast-Track Shortcut (Low Marks Version)
If asked for fewer marks (e.g., 2–3 marks), skip finding $S^{-1}$!
Once you find eigenvalues $\lambda_1 = 2, \lambda_2 = -1$ and eigenvectors $\mathbf{x}_1 = \begin{bmatrix} 5 \\ 2 \end{bmatrix}, \mathbf{x}_2 = \begin{bmatrix} 1 \\ 1 \end{bmatrix}$, set up $\mathbf{x}[0] = c_1 \mathbf{x}_1 + c_2 \mathbf{x}_2$ at $k=0$:
$$\begin{bmatrix} 8 \\ 5 \end{bmatrix} = c_1 \begin{bmatrix} 5 \\ 2 \end{bmatrix} + c_2 \begin{bmatrix} 1 \\ 1 \end{bmatrix} \implies \begin{cases} 5c_1 + c_2 = 8 \\ 2c_1 + c_2 = 5 \end{cases}$$
Subtracting equations gives $3c_1 = 3 \implies c_1 = 1$, then $c_2 = 3$. Immediately write $\mathbf{x}[k] = (2)^k \begin{bmatrix} 5 \\ 2 \end{bmatrix} + 3(-1)^k \begin{bmatrix} 1 \\ 1 \end{bmatrix}$.

---

## PROBLEM 2 (Level 2 — Intermediate)
### Topic: Cloud Data Center Load Balancing & Markov Dynamics
*Grounded in Gilbert Strang, Section 5.3*

#### Scenario & Real-World Context:
A distributed cloud computing network shifts compute tasks between Server Cluster A ($u_1$) and Server Cluster B ($u_2$) every minute according to operational transition probabilities:
* $80\%$ of tasks in Cluster A stay in Cluster A; $20\%$ shift to Cluster B.
* $30\%$ of tasks in Cluster B shift to Cluster A; $70\%$ stay in Cluster B.

The state transition matrix is:
$$M = \begin{bmatrix} 0.8 & 0.3 \\ 0.2 & 0.7 \end{bmatrix}$$
At time $k=0$, an incoming batch of $1000$ compute tasks is injected entirely into Cluster A: $\mathbf{u}[0] = \begin{bmatrix} 1000 \\ 0 \end{bmatrix}$.

#### Questions:
1. Prove why $\lambda_1 = 1$ is guaranteed to be an eigenvalue of $M$ without expanding $\det(M - \lambda I)$.
2. Compute the second eigenvalue $\lambda_2$ using matrix trace properties.
3. Diagonalize $M = S \Lambda S^{-1}$.
4. Derive the explicit workload distribution $\mathbf{u}[k]$ at step $k$, and calculate the long-term steady-state equilibrium $\mathbf{u}_\infty = \lim_{k \to \infty} M^k \mathbf{u}[0]$.
5. Compute the transient decay rate and determine how many minutes $k$ are required for the non-steady-state error to drop below $1\%$ of its initial value.

---

### Full Step-by-Step Solution:

#### Step 1: Proof that $\lambda_1 = 1$
Each column sum of $M$ equals $1$: $0.8 + 0.2 = 1$ and $0.3 + 0.7 = 1$.
Therefore, the rows of $M - 1 \cdot I = \begin{bmatrix} -0.2 & 0.3 \\ 0.2 & -0.3 \end{bmatrix}$ sum to zero:
$$\begin{bmatrix} 1 & 1 \end{bmatrix} (M - I) = \begin{bmatrix} 0 & 0 \end{bmatrix}$$
Thus $M - I$ is singular ($\det(M - I) = 0$), guaranteeing that $\lambda_1 = 1$ is an eigenvalue.

#### Step 2: Finding $\lambda_2$ via Trace
$$\text{trace}(M) = 0.8 + 0.7 = 1.5$$
Since $\text{trace}(M) = \lambda_1 + \lambda_2$:
$$1 + \lambda_2 = 1.5 \implies \lambda_2 = 0.5$$

#### Step 3: Eigenvectors and Diagonalization
* **For $\lambda_1 = 1$**:
  $$(M - I)\mathbf{x}_1 = \begin{bmatrix} -0.2 & 0.3 \\ 0.2 & -0.3 \end{bmatrix} \begin{bmatrix} y \\ z \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix} \implies -2y + 3z = 0 \implies \mathbf{x}_1 = \begin{bmatrix} 3 \\ 2 \end{bmatrix}$$

* **For $\lambda_2 = 0.5$**:
  $$(M - 0.5I)\mathbf{x}_2 = \begin{bmatrix} 0.3 & 0.3 \\ 0.2 & 0.2 \end{bmatrix} \begin{bmatrix} y \\ z \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix} \implies y + z = 0 \implies \mathbf{x}_2 = \begin{bmatrix} 1 \\ -1 \end{bmatrix}$$

$$S = \begin{bmatrix} 3 & 1 \\ 2 & -1 \end{bmatrix}, \quad \det(S) = -3 - 2 = -5$$
$$S^{-1} = -\frac{1}{5} \begin{bmatrix} -1 & -1 \\ -2 & 3 \end{bmatrix} = \begin{bmatrix} 1/5 & 1/5 \\ 2/5 & -3/5 \end{bmatrix}$$
$$\Lambda = \begin{bmatrix} 1 & 0 \\ 0 & 0.5 \end{bmatrix}$$

#### Step 4: Workload Formula $\mathbf{u}[k]$ and Steady-State $\mathbf{u}_\infty$
Compute $\mathbf{c} = S^{-1} \mathbf{u}[0]$:
$$\mathbf{c} = \begin{bmatrix} 1/5 & 1/5 \\ 2/5 & -3/5 \end{bmatrix} \begin{bmatrix} 1000 \\ 0 \end{bmatrix} = \begin{bmatrix} 200 \\ 400 \end{bmatrix}$$
$$\mathbf{u}[k] = c_1 \lambda_1^k \mathbf{x}_1 + c_2 \lambda_2^k \mathbf{x}_2 = 200 (1)^k \begin{bmatrix} 3 \\ 2 \end{bmatrix} + 400 (0.5)^k \begin{bmatrix} 1 \\ -1 \end{bmatrix}$$
$$\mathbf{u}[k] = \begin{bmatrix} 600 + 400(0.5)^k \\ 400 - 400(0.5)^k \end{bmatrix}$$

Taking the limit $k \to \infty$ (since $(0.5)^k \to 0$):
$$\mathbf{u}_\infty = \begin{bmatrix} 600 \\ 400 \end{bmatrix}$$
Cluster A settles at $600$ tasks ($60\%$) and Cluster B settles at $400$ tasks ($40\%$).

#### Step 5: Transient Error Decay
The transient error term is $400(0.5)^k$. Its ratio relative to initial error $400$ is $(0.5)^k$.
To find when error is $< 1\% = 0.01$:
$$(0.5)^k < 0.01 \implies 2^k > 100 \implies k \ge 7 \text{ minutes}$$

---

### ⚡ Exam Fast-Track Shortcut (Low Marks Version)
To find $\mathbf{u}_\infty$ directly in a 2-mark question:
1. Solve $(M - I)\mathbf{u}_\infty = \mathbf{0} \implies -0.2 u_1 + 0.3 u_2 = 0 \implies u_1 = 1.5 u_2$.
2. Use total conservation of tasks $u_1 + u_2 = 1000$:
   $$1.5 u_2 + u_2 = 1000 \implies 2.5 u_2 = 1000 \implies u_2 = 400, \quad u_1 = 600$$
   Done in 20 seconds!

---

## PROBLEM 3 (Level 3 — Advanced)
### Topic: 3-Chamber Chemical Pollutant Diffusion Network
*Grounded in Gilbert Strang, Section 5.4*

#### Scenario & Real-World Context:
A chemical processing plant consists of three connected chambers ($u_1, u_2, u_3$) containing a liquid solution. Pollutant diffuses between adjacent chambers across permeable membranes. The continuous rate of concentration change $\frac{d\mathbf{u}}{dt}$ is governed by the differential system:
$$\frac{d\mathbf{u}}{dt} = A \mathbf{u}(t), \quad \text{where } A = \begin{bmatrix} -1 & 1 & 0 \\ 1 & -2 & 1 \\ 0 & 1 & -1 \end{bmatrix}$$
At time $t=0$, a spill introduces $30 \text{ mg/L}$ of pollutant into Chamber 1 while Chambers 2 and 3 are clean:
$$\mathbf{u}(0) = \begin{bmatrix} 30 \\ 0 \\ 0 \end{bmatrix}$$

#### Questions:
1. Compute the eigenvalues $\lambda_1, \lambda_2, \lambda_3$ of $A$.
2. Compute a complete set of orthogonal eigenvectors $\mathbf{x}_1, \mathbf{x}_2, \mathbf{x}_3$ and form $S$.
3. Construct the matrix exponential $e^{At} = S e^{\Lambda t} S^{-1}$.
4. Solve for the explicit time-domain response $\mathbf{u}(t) = \begin{bmatrix} u_1(t) \\ u_2(t) \\ u_3(t) \end{bmatrix}$.
5. **Conservation & Steady-State Analysis**: Show that total pollutant mass $\sum u_i(t)$ is conserved over all $t \ge 0$, and find the final equilibrium concentrations $\mathbf{u}(\infty)$.

---

### Full Step-by-Step Solution:

#### Step 1: Eigenvalues of $A$
$$\det(A - \lambda I) = \det \begin{bmatrix} -1 - \lambda & 1 & 0 \\ 1 & -2 - \lambda & 1 \\ 0 & 1 & -1 - \lambda \end{bmatrix} = 0$$
Expand cofactors along Row 1:
$$(-1 - \lambda) [(-2 - \lambda)(-1 - \lambda) - 1] - 1 [1(-1 - \lambda) - 0] = 0$$
$$(-1 - \lambda) [\lambda^2 + 3\lambda + 1] + (1 + \lambda) = 0$$
Factor out $(1 + \lambda)$:
$$(1 + \lambda) [ -(\lambda^2 + 3\lambda + 1) + 1 ] = (1 + \lambda)[-\lambda^2 - 3\lambda] = -\lambda(1 + \lambda)(\lambda + 3) = 0$$
The eigenvalues are:
$$\lambda_1 = 0, \quad \lambda_2 = -1, \quad \lambda_3 = -3$$

#### Step 2: Eigenvectors
* **For $\lambda_1 = 0$**:
  $$\begin{bmatrix} -1 & 1 & 0 \\ 1 & -2 & 1 \\ 0 & 1 & -1 \end{bmatrix} \begin{bmatrix} x \\ y \\ z \end{bmatrix} = \mathbf{0} \implies x = y = z \implies \mathbf{x}_1 = \begin{bmatrix} 1 \\ 1 \\ 1 \end{bmatrix}$$

* **For $\lambda_2 = -1$**:
  $$\begin{bmatrix} 0 & 1 & 0 \\ 1 & -1 & 1 \\ 0 & 1 & 0 \end{bmatrix} \begin{bmatrix} x \\ y \\ z \end{bmatrix} = \mathbf{0} \implies y = 0, \; x + z = 0 \implies \mathbf{x}_2 = \begin{bmatrix} 1 \\ 0 \\ -1 \end{bmatrix}$$

* **For $\lambda_3 = -3$**:
  $$\begin{bmatrix} 2 & 1 & 0 \\ 1 & 1 & 1 \\ 0 & 1 & 2 \end{bmatrix} \begin{bmatrix} x \\ y \\ z \end{bmatrix} = \mathbf{0} \implies y = -2x, \; z = x \implies \mathbf{x}_3 = \begin{bmatrix} 1 \\ -2 \\ 1 \end{bmatrix}$$

Note that $\mathbf{x}_1, \mathbf{x}_2, \mathbf{x}_3$ are mutually orthogonal ($\mathbf{x}_i^T \mathbf{x}_j = 0$ for $i \neq j$), as expected for a real symmetric matrix!

#### Step 3: Construct $S$ and $S^{-1}$
$$S = \begin{bmatrix} 1 & 1 & 1 \\ 1 & 0 & -2 \\ 1 & -1 & 1 \end{bmatrix}$$
Using orthogonality of columns ($\|\mathbf{x}_1\|^2 = 3, \|\mathbf{x}_2\|^2 = 2, \|\mathbf{x}_3\|^2 = 6$):
$$S^{-1} = \begin{bmatrix} \mathbf{x}_1^T / 3 \\ \mathbf{x}_2^T / 2 \\ \mathbf{x}_3^T / 6 \end{bmatrix} = \begin{bmatrix} 1/3 & 1/3 & 1/3 \\ 1/2 & 0 & -1/2 \\ 1/6 & -1/3 & 1/6 \end{bmatrix}$$

#### Step 4: Time-Domain Response $\mathbf{u}(t)$
Compute constants $\mathbf{c} = S^{-1} \mathbf{u}(0)$:
$$\mathbf{c} = \begin{bmatrix} 1/3 & 1/3 & 1/3 \\ 1/2 & 0 & -1/2 \\ 1/6 & -1/3 & 1/6 \end{bmatrix} \begin{bmatrix} 30 \\ 0 \\ 0 \end{bmatrix} = \begin{bmatrix} 10 \\ 15 \\ 5 \end{bmatrix}$$

The general matrix exponential solution $\mathbf{u}(t) = c_1 e^{\lambda_1 t} \mathbf{x}_1 + c_2 e^{\lambda_2 t} \mathbf{x}_2 + c_3 e^{\lambda_3 t} \mathbf{x}_3$ becomes:
$$\mathbf{u}(t) = 10 e^{0t} \begin{bmatrix} 1 \\ 1 \\ 1 \end{bmatrix} + 15 e^{-t} \begin{bmatrix} 1 \\ 0 \\ -1 \end{bmatrix} + 5 e^{-3t} \begin{bmatrix} 1 \\ -2 \\ 1 \end{bmatrix}$$

Component-wise solution:
$$u_1(t) = 10 + 15 e^{-t} + 5 e^{-3t}$$
$$u_2(t) = 10 - 10 e^{-3t}$$
$$u_3(t) = 10 - 15 e^{-t} + 5 e^{-3t}$$

#### Step 5: Conservation & Equilibrium Analysis
Summing all three components:
$$\sum_{i=1}^3 u_i(t) = (10+10+10) + (15+0-15)e^{-t} + (5-10+5)e^{-3t} = 30 \text{ mg/L}$$
Mass is strictly conserved for all $t$.
Taking $t \to \infty$, the decaying exponentials $e^{-t}, e^{-3t} \to 0$:
$$\mathbf{u}(\infty) = \begin{bmatrix} 10 \\ 10 \\ 10 \end{bmatrix}$$
All three chambers equalize to an even $10 \text{ mg/L}$ concentration.

---

### ⚡ Exam Fast-Track Shortcut (Low Marks Version)
If asked only for $\mathbf{u}(\infty)$ in a continuous Markov/diffusion system:
Notice column sums of $A$ equal $0 \implies \frac{d}{dt}\left(\sum u_i\right) = 0 \implies \text{Total Mass} = 30$.
Since $A$ is symmetric, the zero-eigenvalue steady state vector must be constant $\mathbf{x}_1 = \begin{bmatrix} 1 & 1 & 1 \end{bmatrix}^T$.
Equating $c_1 (1 + 1 + 1) = 30 \implies c_1 = 10 \implies \mathbf{u}(\infty) = \begin{bmatrix} 10 \\ 10 \\ 10 \end{bmatrix}$. No integrals or matrix exponentials required!

---

## PROBLEM 4 (Level 4 — Tricky Non-Diagonalizable / Defective)
### Topic: Resonant Control Loop & Failure of Diagonalization
*Grounded in Gilbert Strang, Section 5.2 & 5.6*

#### Scenario & Real-World Context:
A high-precision servo-motor feedback controller updates its state $\mathbf{x}[k] = \begin{bmatrix} \theta[k] \\ \omega[k] \end{bmatrix}$ (position and angular velocity) across discrete processing frames:
$$\mathbf{x}[k+1] = A \mathbf{x}[k], \quad \text{where } A = \begin{bmatrix} 2 & -1 \\ 1 & 0 \end{bmatrix}$$
An initial disturbance vector is injected at frame $k=0$: $\mathbf{x}[0] = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$.

#### Questions:
1. Find the eigenvalues of $A$ and show that $\lambda = 1$ is a repeated eigenvalue with algebraic multiplicity $2$.
2. Calculate the rank of $A - I$ to determine the geometric multiplicity. Explain why $A$ is **defective** and cannot be diagonalized into $S \Lambda S^{-1}$.
3. Construct the **Jordan Normal Form** $J = M^{-1} A M = \begin{bmatrix} 1 & 1 \\ 0 & 1 \end{bmatrix}$ using an eigenvector and a generalized eigenvector.
4. Calculate $J^k$ and derive the closed-form response $\mathbf{x}[k] = M J^k M^{-1} \mathbf{x}[0]$.
5. **Control Resonance Trap**: Identify the term causing linear growth $k \lambda^{k-1}$ and explain why defective matrices lead to secular instability in control systems.

---

### Full Step-by-Step Solution:

#### Step 1: Algebraic Multiplicity
$$\det(A - \lambda I) = \det \begin{bmatrix} 2 - \lambda & -1 \\ 1 & -\lambda \end{bmatrix} = \lambda^2 - 2\lambda + 1 = (\lambda - 1)^2 = 0$$
The matrix has a single repeated eigenvalue $\lambda_1 = \lambda_2 = 1$ with **algebraic multiplicity = 2**.

#### Step 2: Geometric Multiplicity & Diagonalization Failure
Compute $A - 1 \cdot I$:
$$A - I = \begin{bmatrix} 1 & -1 \\ 1 & -1 \end{bmatrix}$$
The rank of $A - I$ is $1$.
By the Rank-Nullity Theorem, the dimension of the eigenspace (nullspace of $A - I$) is:
$$\text{geometric multiplicity} = n - \text{rank}(A - I) = 2 - 1 = 1$$
There is only **one** linearly independent eigenvector:
$$(A - I)\mathbf{x}_1 = \mathbf{0} \implies \begin{bmatrix} 1 & -1 \\ 1 & -1 \end{bmatrix} \begin{bmatrix} y \\ z \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix} \implies \mathbf{x}_1 = \begin{bmatrix} 1 \\ 1 \end{bmatrix}$$
Because geometric multiplicity ($1$) < algebraic multiplicity ($2$), $A$ lacks a complete basis of $2$ independent eigenvectors. **$A$ cannot be diagonalized** ($S$ would be singular and non-invertible).

#### Step 3: Generalized Eigenvector & Jordan Form $J$
To construct the Jordan transform matrix $M = [\mathbf{x}_1 \; \mathbf{x}_2]$, we find a **generalized eigenvector** $\mathbf{x}_2$ satisfying:
$$(A - I)\mathbf{x}_2 = \mathbf{x}_1$$
$$\begin{bmatrix} 1 & -1 \\ 1 & -1 \end{bmatrix} \begin{bmatrix} y_2 \\ z_2 \end{bmatrix} = \begin{bmatrix} 1 \\ 1 \end{bmatrix} \implies y_2 - z_2 = 1$$
Choosing $z_2 = 0 \implies y_2 = 1$, we get $\mathbf{x}_2 = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$.

Form $M$ and $M^{-1}$:
$$M = \begin{bmatrix} 1 & 1 \\ 1 & 0 \end{bmatrix}, \quad \det(M) = -1$$
$$M^{-1} = \begin{bmatrix} 0 & 1 \\ 1 & -1 \end{bmatrix}$$

Verify Jordan Normal Form $J = M^{-1} A M$:
$$A M = \begin{bmatrix} 2 & -1 \\ 1 & 0 \end{bmatrix} \begin{bmatrix} 1 & 1 \\ 1 & 0 \end{bmatrix} = \begin{bmatrix} 1 & 2 \\ 1 & 1 \end{bmatrix}$$
$$J = M^{-1} (AM) = \begin{bmatrix} 0 & 1 \\ 1 & -1 \end{bmatrix} \begin{bmatrix} 1 & 2 \\ 1 & 1 \end{bmatrix} = \begin{bmatrix} 1 & 1 \\ 0 & 1 \end{bmatrix}$$

#### Step 4: State Response $\mathbf{x}[k]$
For a Jordan block $J = \begin{bmatrix} \lambda & 1 \\ 0 & \lambda \end{bmatrix}$, its $k$-th power is:
$$J^k = \begin{bmatrix} \lambda^k & k \lambda^{k-1} \\ 0 & \lambda^k \end{bmatrix} \xrightarrow{\lambda=1} \begin{bmatrix} 1 & k \\ 0 & 1 \end{bmatrix}$$

Compute $\mathbf{x}[k] = M J^k M^{-1} \mathbf{x}[0]$:
$$M^{-1} \mathbf{x}[0] = \begin{bmatrix} 0 & 1 \\ 1 & -1 \end{bmatrix} \begin{bmatrix} 1 \\ 0 \end{bmatrix} = \begin{bmatrix} 0 \\ 1 \end{bmatrix}$$
$$J^k (M^{-1} \mathbf{x}[0]) = \begin{bmatrix} 1 & k \\ 0 & 1 \end{bmatrix} \begin{bmatrix} 0 \\ 1 \end{bmatrix} = \begin{bmatrix} k \\ 1 \end{bmatrix}$$
$$\mathbf{x}[k] = M \begin{bmatrix} k \\ 1 \end{bmatrix} = \begin{bmatrix} 1 & 1 \\ 1 & 0 \end{bmatrix} \begin{bmatrix} k \\ 1 \end{bmatrix} = \begin{bmatrix} k + 1 \\ k \end{bmatrix}$$

#### Step 5: Control Resonance Analysis
* Component response: Position $\theta[k] = k + 1$, Angular Velocity $\omega[k] = k$.
* The term $k \lambda^{k-1} = k$ grows **linearly without bound** as $k \to \infty$.
* **Exam Warning**: Even though $|\lambda| = 1$ suggests neutral stability in ordinary systems, defective matrices introduce polynomial multiplier terms ($k, k^2$) that cause internal control loop resonance and system destruction!

---

## PROBLEM 5 (Level 5 — Real Symmetric & Spectral Decomposition)
### Topic: Acoustic Microphone Array Covariance & Principal Component Analysis (PCA)
*Grounded in Gilbert Strang, Section 5.5*

#### Scenario & Real-World Context:
A 2-channel directional microphone array processes noisy spatial audio signals. The empirical spatial covariance matrix of the dual sensor signals is given by the real symmetric matrix:
$$R = \begin{bmatrix} 5 & 4 \\ 4 & 5 \end{bmatrix}$$

#### Questions:
1. Find the eigenvalues $\lambda_1, \lambda_2$ and orthonormal eigenvectors $\mathbf{q}_1, \mathbf{q}_2$ of $R$.
2. Construct the orthogonal matrix $Q = [\mathbf{q}_1 \; \mathbf{q}_2]$ and verify the Spectral Theorem factorization $R = Q \Lambda Q^T$.
3. Express $R$ as its explicit **Spectral Decomposition** sum of rank-1 projection matrices:
$$R = \lambda_1 \mathbf{q}_1 \mathbf{q}_1^T + \lambda_2 \mathbf{q}_2 \mathbf{q}_2^T$$
4. **PCA Noise Filtering**: Construct the dominant rank-1 principal component approximation $R_{\text{rank-1}} = \lambda_1 \mathbf{q}_1 \mathbf{q}_1^T$. Compute the residual noise error matrix $E = R - R_{\text{rank-1}}$ and its Frobenius norm $\|E\|_F$.
5. Draw the geometric orientation of the principal signal energy axis relative to the sensor channels.

---

### Full Step-by-Step Solution:

#### Step 1: Eigenvalues and Orthonormal Eigenvectors
$$\det(R - \lambda I) = \det \begin{bmatrix} 5 - \lambda & 4 \\ 4 & 5 - \lambda \end{bmatrix} = (5 - \lambda)^2 - 16 = 0$$
$$(5 - \lambda) = \pm 4 \implies \lambda_1 = 9, \quad \lambda_2 = 1$$

* **For $\lambda_1 = 9$ (Dominant Acoustic Signal)**:
  $$(R - 9I)\mathbf{x}_1 = \begin{bmatrix} -4 & 4 \\ 4 & -4 \end{bmatrix} \begin{bmatrix} y \\ z \end{bmatrix} = \mathbf{0} \implies y = z \implies \mathbf{x}_1 = \begin{bmatrix} 1 \\ 1 \end{bmatrix}$$
  Normalizing to unit length ($\|\mathbf{x}_1\| = \sqrt{2}$):
  $$\mathbf{q}_1 = \frac{1}{\sqrt{2}} \begin{bmatrix} 1 \\ 1 \end{bmatrix}$$

* **For $\lambda_2 = 1$ (Background Noise Floor)**:
  $$(R - I)\mathbf{x}_2 = \begin{bmatrix} 4 & 4 \\ 4 & 4 \end{bmatrix} \begin{bmatrix} y \\ z \end{bmatrix} = \mathbf{0} \implies y = -z \implies \mathbf{x}_2 = \begin{bmatrix} 1 \\ -1 \end{bmatrix}$$
  Normalizing to unit length ($\|\mathbf{x}_2\| = \sqrt{2}$):
  $$\mathbf{q}_2 = \frac{1}{\sqrt{2}} \begin{bmatrix} 1 \\ -1 \end{bmatrix}$$

#### Step 2: Verification of Spectral Theorem $R = Q \Lambda Q^T$
$$Q = \frac{1}{\sqrt{2}} \begin{bmatrix} 1 & 1 \\ 1 & -1 \end{bmatrix}, \quad Q^T = \frac{1}{\sqrt{2}} \begin{bmatrix} 1 & 1 \\ 1 & -1 \end{bmatrix}$$
Check $Q^T Q = I$:
$$Q^T Q = \frac{1}{2} \begin{bmatrix} 2 & 0 \\ 0 & 2 \end{bmatrix} = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} \quad \checkmark$$

Check $Q \Lambda Q^T$:
$$Q \Lambda Q^T = \frac{1}{2} \begin{bmatrix} 1 & 1 \\ 1 & -1 \end{bmatrix} \begin{bmatrix} 9 & 0 \\ 0 & 1 \end{bmatrix} \begin{bmatrix} 1 & 1 \\ 1 & -1 \end{bmatrix} = \frac{1}{2} \begin{bmatrix} 9 & 1 \\ 9 & -1 \end{bmatrix} \begin{bmatrix} 1 & 1 \\ 1 & -1 \end{bmatrix} = \frac{1}{2} \begin{bmatrix} 10 & 8 \\ 8 & 10 \end{bmatrix} = \begin{bmatrix} 5 & 4 \\ 4 & 5 \end{bmatrix} \quad \checkmark$$

#### Step 3: Spectral Decomposition Into Rank-1 Projections
Compute projection matrix $P_1 = \mathbf{q}_1 \mathbf{q}_1^T$:
$$P_1 = \left( \frac{1}{\sqrt{2}} \begin{bmatrix} 1 \\ 1 \end{bmatrix} \right) \left( \frac{1}{\sqrt{2}} \begin{bmatrix} 1 & 1 \end{bmatrix} \right) = \begin{bmatrix} 1/2 & 1/2 \\ 1/2 & 1/2 \end{bmatrix}$$

Compute projection matrix $P_2 = \mathbf{q}_2 \mathbf{q}_2^T$:
$$P_2 = \left( \frac{1}{\sqrt{2}} \begin{bmatrix} 1 \\ -1 \end{bmatrix} \right) \left( \frac{1}{\sqrt{2}} \begin{bmatrix} 1 & -1 \end{bmatrix} \right) = \begin{bmatrix} 1/2 & -1/2 \\ -1/2 & 1/2 \end{bmatrix}$$

Spectral expansion:
$$R = 9 P_1 + 1 P_2 = 9 \begin{bmatrix} 1/2 & 1/2 \\ 1/2 & 1/2 \end{bmatrix} + 1 \begin{bmatrix} 1/2 & -1/2 \\ -1/2 & 1/2 \end{bmatrix} = \begin{bmatrix} 4.5 & 4.5 \\ 4.5 & 4.5 \end{bmatrix} + \begin{bmatrix} 0.5 & -0.5 \\ -0.5 & 0.5 \end{bmatrix}$$

#### Step 4: PCA Low-Rank Reconstruction & Error Norm
The dominant rank-1 approximation capturing $90\%$ of total signal power ($\frac{\lambda_1}{\lambda_1 + \lambda_2} = \frac{9}{10}$) is:
$$R_{\text{rank-1}} = 9 P_1 = \begin{bmatrix} 4.5 & 4.5 \\ 4.5 & 4.5 \end{bmatrix}$$

The noise error residual matrix is:
$$E = R - R_{\text{rank-1}} = 1 P_2 = \begin{bmatrix} 0.5 & -0.5 \\ -0.5 & 0.5 \end{bmatrix}$$

Frobenius Norm of Error:
$$\|E\|_F = \sqrt{\sum e_{ij}^2} = \sqrt{0.25 + 0.25 + 0.25 + 0.25} = \sqrt{1} = 1$$
Notice that $\|E\|_F = \lambda_2 = 1$! The error norm in rank-1 PCA approximation exactly equals the discarded smaller eigenvalue.

#### Step 5: Geometric Interpretation
* The principal component axis $\mathbf{q}_1 = \frac{1}{\sqrt{2}}\begin{bmatrix} 1 \\ 1 \end{bmatrix}$ points at $+45^\circ$ in the 2-sensor measurement space, representing **in-phase acoustic signal energy**.
* The secondary axis $\mathbf{q}_2 = \frac{1}{\sqrt{2}}\begin{bmatrix} 1 \\ -1 \end{bmatrix}$ points at $-45^\circ$, representing **uncorrelated differential noise**.
* Filtering out $P_2$ removes the isotropic noise component while preserving $90\%$ of signal energy.

---

### ⚡ Exam Fast-Track Shortcut (Low Marks Version)
For any $2 \times 2$ symmetric matrix $R = \begin{bmatrix} a & b \\ b & a \end{bmatrix}$:
1. Eigenvalues are always $\lambda_1 = a + b, \; \lambda_2 = a - b$.
2. Eigenvectors are always $\mathbf{q}_1 = \frac{1}{\sqrt{2}}\begin{bmatrix} 1 \\ 1 \end{bmatrix}$ and $\mathbf{q}_2 = \frac{1}{\sqrt{2}}\begin{bmatrix} 1 \\ -1 \end{bmatrix}$.
3. You can write down $\lambda_1 = 5+4 = 9$ and $\lambda_2 = 5-4 = 1$ instantly in 5 seconds!

---

## Master Reference Table: Diagonalization Concepts Across Systems

| Concept | Matrix Operator | Discrete Time $\mathbf{x}[k+1] = A\mathbf{x}[k]$ | Continuous Time $\frac{d\mathbf{u}}{dt} = A\mathbf{u}(t)$ |
| :--- | :--- | :--- | :--- |
| **Solution Form** | $A = S \Lambda S^{-1}$ | $\mathbf{x}[k] = S \Lambda^k S^{-1} \mathbf{x}[0]$ | $\mathbf{u}(t) = S e^{\Lambda t} S^{-1} \mathbf{u}(0)$ |
| **Asymptotic Stability** | Real/Complex $\lambda_i$ | Strict stability if $|\lambda_i| < 1$ | Strict stability if $\text{Re}(\lambda_i) < 0$ |
| **Neutral Stability** | Markov / Conservative | $\lambda_1 = 1$, others $|\lambda_i| < 1$ | $\lambda_1 = 0$ or pure imaginary $\pm i \omega$ |
| **Defective Systems** | Jordan Block $J_i$ | Secular growth $k \lambda^{k-1}$ | Secular growth $t e^{\lambda t}$ |
| **Symmetric / Hermitian** | $A = Q \Lambda Q^T$ | $A = \sum \lambda_i \mathbf{q}_i \mathbf{q}_i^T$ (Rank-1 spectral projections) | Energy orthogonal modes |

---
