# Linear Algebra Problem Types & Solutions Master Package
### Based on the Classification in `Problems.pdf`

This master package provides **10 foundational practice problems with detailed step-by-step solutions**, categorized strictly according to the **Four System Problem Types** and **Three Real-World Goals** defined in `Problems.pdf`:

1. **The Analysis Problem (Forward / Simulation)**: Known Input ($\mathbf{x}$) and System ($A$), Unknown Output ($\mathbf{y}$).
2. **The Control Problem (Actuation / Optimization)**: Known System ($A$) and Desired Output ($\mathbf{y}_{	ext{desired}}$), Unknown Input ($\mathbf{x}$).
3. **The Inverse Problem (Diagnostics / Inference)**: Known System ($A$) and Observed Output ($\mathbf{y}_{	ext{observed}}$), Unknown Past Input ($\mathbf{x}$).
4. **The Synthesis Problem (Design / Model Identification)**: Known Inputs ($\mathbf{x}$) and Outputs ($\mathbf{y}$), Unknown System ($A$).
5. **Real-World Goal Applications**: Prediction, Cause-and-Effect Analysis, and Resource Allocation.

---

## Quick Reference Summary Table

| Problem # | Category | Problem Type | Real-World Application Theme | Unknown to Solve |
| :--- | :--- | :--- | :--- | :--- |
| **Problem 1** | Analysis | Forward / Simulation | Audio Console Signal Mixing | Output Vector $\mathbf{y} = A\mathbf{x}$ |
| **Problem 2** | Analysis | Forward / Forecasting | Market Share Transition Dynamics | Future State $\mathbf{x}_{k+1} = A\mathbf{x}_k$ |
| **Problem 3** | Control | Exact Actuation | Smart Home Dual-Zone HVAC Control | Input Vector $\mathbf{x} = A^{-1}\mathbf{y}_{	ext{desired}}$ |
| **Problem 4** | Control | Minimum-Power Control | Satellite Planar Thruster Optimization | Min-Norm Input $\mathbf{x} = A^T(AA^T)^{-1}\mathbf{y}$ |
| **Problem 5** | Inverse | Exact Diagnostic Inversion | Dual-Pixel Optical Image De-blurring | Original Input $\mathbf{x} = A^{-1}\mathbf{y}_{	ext{observed}}$ |
| **Problem 6** | Inverse | Least-Squares Diagnostics | 2D GPS Position Reconstruction | Least-Squares Input $\hat{\mathbf{x}} = (A^TA)^{-1}A^T\mathbf{y}$ |
| **Problem 7** | Synthesis | System Identification | 2-Port Circuit Filter Matrix Design | System Matrix $A$ |
| **Problem 8** | Synthesis | Model Fitting / Calibration | Linear Sensor Least-Squares Calibration | Parameters $\mathbf{c} = [C, D]^T$ |
| **Problem 9** | Resource Alloc. | Linear Programming | Factory Production Allocation | Optimal Mix $(x_1, x_2)$ for Max Profit |
| **Problem 10** | Cause-&-Effect | Redundancy & Nullspace | Multi-Sensor Network Sensitivity | Rank, Redundancy & Nullspace Basis $\mathbf{x}_n$ |

---

## Category 1: The Analysis Problem (Forward / Simulation)
* **The Question**: "What will happen?"
* **Knowns**: Input ($\mathbf{x}$) and System Matrix ($A$).
* **Unknown**: Output ($\mathbf{y} = A\mathbf{x}$).

---

### Problem 1: Audio Console Signal Mixing & Channel Gain
**Scenario**: An audio mixing console receives two microphone signals: $x_1 = 10	ext{ V}$ (vocal mic) and $x_2 = 5	ext{ V}$ (instrument mic). The mixing system passes these inputs through a gain and cross-talk matrix $A$:
$$A = \begin{bmatrix} 0.8 & 0.2 \ 0.3 & 0.7 \end{bmatrix}, \quad \mathbf{x} = \begin{bmatrix} 10 \ 5 \end{bmatrix}$$

Find the resulting output voltage vector $\mathbf{y} = \begin{bmatrix} y_1 \ y_2 \end{bmatrix}$.

#### Step-by-Step Solution:
1. **Identify the Problem Type**: This is an **Analysis Problem (Forward Simulation)** because the system matrix $A$ and input vector $\mathbf{x}$ are both completely known. We calculate the output $\mathbf{y} = A\mathbf{x}$.

2. **Matrix-Vector Multiplication**:
   $$\mathbf{y} = A\mathbf{x} = \begin{bmatrix} 0.8 & 0.2 \ 0.3 & 0.7 \end{bmatrix} \begin{bmatrix} 10 \ 5 \end{bmatrix}$$

3. **Compute Components**:
   * Output Channel 1: $y_1 = (0.8)(10) + (0.2)(5) = 8 + 1 = 9	ext{ V}$
   * Output Channel 2: $y_2 = (0.3)(10) + (0.7)(5) = 3 + 3.5 = 6.5	ext{ V}$

4. **Final Result**:
   $$\mathbf{y} = \begin{bmatrix} 9 \ 6.5 \end{bmatrix}	ext{ Volts}$$

---

### Problem 2: Market Share Transition Dynamics (Multi-Step Forecasting)
**Scenario**: Two competing streaming services (Company A and Company B) share 100,000 subscribers. Every year, Company A retains $90\%$ of its users and loses $10\%$ to B. Company B retains $80\%$ of its users and loses $20\%$ to A.
The transition matrix $A$ and initial state $\mathbf{x}_0$ are:
$$A = \begin{bmatrix} 0.9 & 0.2 \ 0.1 & 0.8 \end{bmatrix}, \quad \mathbf{x}_0 = \begin{bmatrix} 100 \ 0 \end{bmatrix} \quad 	ext{(in thousands)}$$

Calculate the subscriber distribution after 1 year ($\mathbf{x}_1$) and after 2 years ($\mathbf{x}_2$).

#### Step-by-Step Solution:
1. **Year 1 Forecast ($\mathbf{x}_1 = A\mathbf{x}_0$)**:
   $$\mathbf{x}_1 = \begin{bmatrix} 0.9 & 0.2 \ 0.1 & 0.8 \end{bmatrix} \begin{bmatrix} 100 \ 0 \end{bmatrix} = \begin{bmatrix} (0.9)(100) + (0.2)(0) \ (0.1)(100) + (0.8)(0) \end{bmatrix} = \begin{bmatrix} 90 \ 10 \end{bmatrix}$$
   *After Year 1: Company A has 90,000 users, Company B has 10,000 users.*

2. **Year 2 Forecast ($\mathbf{x}_2 = A\mathbf{x}_1$)**:
   $$\mathbf{x}_2 = \begin{bmatrix} 0.9 & 0.2 \ 0.1 & 0.8 \end{bmatrix} \begin{bmatrix} 90 \ 10 \end{bmatrix} = \begin{bmatrix} (0.9)(90) + (0.2)(10) \ (0.1)(90) + (0.8)(10) \end{bmatrix} = \begin{bmatrix} 81 + 2 \ 9 + 8 \end{bmatrix} = \begin{bmatrix} 83 \ 17 \end{bmatrix}$$

3. **Final Result**:
   * Year 1 Distribution: $\mathbf{x}_1 = \begin{bmatrix} 90 \ 10 \end{bmatrix}$ (90k for A, 10k for B)
   * Year 2 Distribution: $\mathbf{x}_2 = \begin{bmatrix} 83 \ 17 \end{bmatrix}$ (83k for A, 17k for B)

---

## Category 2: The Control Problem (Actuation / Optimization)
* **The Question**: "What do we need to do to get what we want?"
* **Knowns**: System Matrix ($A$) and Desired Output ($\mathbf{y}_{	ext{desired}}$).
* **Unknown**: Input Command Vector ($\mathbf{x}$).

---

### Problem 3: Smart Home Dual-Zone Heating Control
**Scenario**: A smart building uses two heating elements ($x_1, x_2$ in kW) to raise temperatures in Zone 1 and Zone 2. Due to heat transfer between rooms, the thermal transfer matrix $A$ relates heater inputs to temperature rises $\mathbf{y}$ (in $^\circ	ext{C}$):
$$A = \begin{bmatrix} 2 & 1 \ 1 & 3 \end{bmatrix}$$

The homeowner sets the thermostat for desired temperature increases: $\mathbf{y}_{	ext{desired}} = \begin{bmatrix} 25 \ 30 \end{bmatrix} ^\circ	ext{C}$.
Calculate the required heater inputs $x_1$ and $x_2$.

#### Step-by-Step Solution:
1. **Identify the Problem Type**: This is a **Control Problem** because the system matrix $A$ and desired target output $\mathbf{y}_{	ext{desired}}$ are known, and we need to determine the required input $\mathbf{x}$ by solving $A\mathbf{x} = \mathbf{y}_{	ext{desired}}$.

2. **Invert Matrix $A$**:
   $$\det(A) = (2)(3) - (1)(1) = 6 - 1 = 5$$
   $$A^{-1} = \frac{1}{5} \begin{bmatrix} 3 & -1 \ -1 & 2 \end{bmatrix}$$

3. **Solve for Input $\mathbf{x}$**:
   $$\mathbf{x} = A^{-1} \mathbf{y}_{	ext{desired}} = \frac{1}{5} \begin{bmatrix} 3 & -1 \ -1 & 2 \end{bmatrix} \begin{bmatrix} 25 \ 30 \end{bmatrix}$$
   $$x_1 = \frac{1}{5} [ (3)(25) + (-1)(30) ] = \frac{1}{5} [75 - 30] = \frac{45}{5} = 9	ext{ kW}$$
   $$x_2 = \frac{1}{5} [ (-1)(25) + (2)(30) ] = \frac{1}{5} [-25 + 60] = \frac{35}{5} = 7	ext{ kW}$$

4. **Final Result**:
   Heater 1 power $x_1 = 9	ext{ kW}$, Heater 2 power $x_2 = 7	ext{ kW}$.

---

### Problem 4: Minimum-Power Satellite Planar Thruster Control
**Scenario**: A small satellite uses $n=3$ thrusters ($x_1, x_2, x_3$) to generate $m=2$ planar forces ($F_x, F_y$). The configuration matrix is:
$$A = \begin{bmatrix} 1 & 1 & 0 \ 0 & 1 & 1 \end{bmatrix}$$

To position the satellite, the control computer requires target forces $\mathbf{y}_{	ext{desired}} = \begin{bmatrix} 5 \ 4 \end{bmatrix}	ext{ N}$.
Since there are infinitely many valid thruster combinations ($n > m$), compute the unique **minimum-norm thruster command vector** $\mathbf{x}_{	ext{min}} = A^T (A A^T)^{-1} \mathbf{y}_{	ext{desired}}$ that minimizes fuel/power consumption $\|\mathbf{x}\|^2$.

#### Step-by-Step Solution:
1. **Compute $A A^T$**:
   $$A A^T = \begin{bmatrix} 1 & 1 & 0 \ 0 & 1 & 1 \end{bmatrix} \begin{bmatrix} 1 & 0 \ 1 & 1 \ 0 & 1 \end{bmatrix} = \begin{bmatrix} 1+1+0 & 0+1+0 \ 0+1+0 & 0+1+1 \end{bmatrix} = \begin{bmatrix} 2 & 1 \ 1 & 2 \end{bmatrix}$$

2. **Invert $(A A^T)$**:
   $$\det(A A^T) = (2)(2) - (1)(1) = 3$$
   $$(A A^T)^{-1} = \frac{1}{3} \begin{bmatrix} 2 & -1 \ -1 & 2 \end{bmatrix}$$

3. **Compute Intermediate Vector $\mathbf{w} = (A A^T)^{-1} \mathbf{y}_{	ext{desired}}$**:
   $$\mathbf{w} = \frac{1}{3} \begin{bmatrix} 2 & -1 \ -1 & 2 \end{bmatrix} \begin{bmatrix} 5 \ 4 \end{bmatrix} = \frac{1}{3} \begin{bmatrix} 10 - 4 \ -5 + 8 \end{bmatrix} = \frac{1}{3} \begin{bmatrix} 6 \ 3 \end{bmatrix} = \begin{bmatrix} 2 \ 1 \end{bmatrix}$$

4. **Calculate Minimum-Norm Input $\mathbf{x}_{	ext{min}} = A^T \mathbf{w}$**:
   $$\mathbf{x}_{	ext{min}} = \begin{bmatrix} 1 & 0 \ 1 & 1 \ 0 & 1 \end{bmatrix} \begin{bmatrix} 2 \ 1 \end{bmatrix} = \begin{bmatrix} (1)(2) + (0)(1) \ (1)(2) + (1)(1) \ (0)(2) + (1)(1) \end{bmatrix} = \begin{bmatrix} 2 \ 3 \ 1 \end{bmatrix}$$

5. **Verification**:
   $$A \mathbf{x}_{	ext{min}} = \begin{bmatrix} 1 & 1 & 0 \ 0 & 1 & 1 \end{bmatrix} \begin{bmatrix} 2 \ 3 \ 1 \end{bmatrix} = \begin{bmatrix} 2 + 3 + 0 \ 0 + 3 + 1 \end{bmatrix} = \begin{bmatrix} 5 \ 4 \end{bmatrix} = \mathbf{y}_{	ext{desired}} \quad \checkmark$$

6. **Final Result**:
   Optimal Thruster Commands: $x_1 = 2	ext{ N}, x_2 = 3	ext{ N}, x_3 = 1	ext{ N}$.

---

## Category 3: The Inverse Problem (Diagnostics / Inference)
* **The Question**: "What caused this?"
* **Knowns**: System Matrix ($A$) and Observed Output ($\mathbf{y}_{	ext{observed}}$).
* **Unknown**: Actual Past Input ($\mathbf{x}$).

---

### Problem 5: Dual-Pixel Optical Image De-blurring
**Scenario**: A dual-pixel optical sensor records blurred light measurements $\mathbf{y}_{	ext{observed}} = \begin{bmatrix} 8 \ 7 \end{bmatrix}$ due to optical cross-talk described by blur matrix $A$:
$$A = \begin{bmatrix} 2 & 1 \ 1 & 2 \end{bmatrix}$$

Recover the true original unblurred light intensity vector $\mathbf{x} = \begin{bmatrix} x_1 \ x_2 \end{bmatrix}$.

#### Step-by-Step Solution:
1. **Identify the Problem Type**: This is an **Inverse Problem (Diagnostic Inference)** because we observe a blurred output $\mathbf{y}_{	ext{observed}}$ and know the physical blurring system $A$, and want to infer the original source input $\mathbf{x}$.

2. **Invert Matrix $A$**:
   $$\det(A) = (2)(2) - (1)(1) = 3$$
   $$A^{-1} = \frac{1}{3} \begin{bmatrix} 2 & -1 \ -1 & 2 \end{bmatrix}$$

3. **Reconstruct Input Vector $\mathbf{x}$**:
   $$\mathbf{x} = A^{-1} \mathbf{y}_{	ext{observed}} = \frac{1}{3} \begin{bmatrix} 2 & -1 \ -1 & 2 \end{bmatrix} \begin{bmatrix} 8 \ 7 \end{bmatrix}$$
   $$x_1 = \frac{1}{3} [ (2)(8) + (-1)(7) ] = \frac{1}{3} [16 - 7] = \frac{9}{3} = 3$$
   $$x_2 = \frac{1}{3} [ (-1)(8) + (2)(7) ] = \frac{1}{3} [-8 + 14] = \frac{6}{3} = 2$$

4. **Final Result**:
   True Original Light Intensities: $x_1 = 3	ext{ units}$, $x_2 = 2	ext{ units}$.

---

### Problem 6: Least-Squares 2D GPS Position Estimation
**Scenario**: A ground receiver receives distance signals from 3 satellite beacons ($m=3, n=2$). Due to measurement noise, the system of equations $A\mathbf{x} = \mathbf{y}_{	ext{observed}}$ is overdetermined and inconsistent:
$$A = \begin{bmatrix} 1 & 0 \ 0 & 1 \ 1 & 1 \end{bmatrix}, \quad \mathbf{y}_{	ext{observed}} = \begin{bmatrix} 2 \ 1 \ 3 \end{bmatrix}$$

Find the best least-squares estimated position $\hat{\mathbf{x}} = \begin{bmatrix} \hat{x}_1 \ \hat{x}_2 \end{bmatrix}$ that minimizes measurement error.

#### Step-by-Step Solution:
1. **Set Up Normal Equations**:
   $$A^T A \hat{\mathbf{x}} = A^T \mathbf{y}_{	ext{observed}}$$

2. **Calculate $A^T A$ and $A^T \mathbf{y}_{	ext{observed}}$**:
   $$A^T A = \begin{bmatrix} 1 & 0 & 1 \ 0 & 1 & 1 \end{bmatrix} \begin{bmatrix} 1 & 0 \ 0 & 1 \ 1 & 1 \end{bmatrix} = \begin{bmatrix} 1+0+1 & 0+0+1 \ 0+0+1 & 0+1+1 \end{bmatrix} = \begin{bmatrix} 2 & 1 \ 1 & 2 \end{bmatrix}$$
   $$A^T \mathbf{y}_{	ext{observed}} = \begin{bmatrix} 1 & 0 & 1 \ 0 & 1 & 1 \end{bmatrix} \begin{bmatrix} 2 \ 1 \ 3 \end{bmatrix} = \begin{bmatrix} 2 + 0 + 3 \ 0 + 1 + 3 \end{bmatrix} = \begin{bmatrix} 5 \ 4 \end{bmatrix}$$

3. **Solve Normal Equations**:
   $$\begin{bmatrix} 2 & 1 \ 1 & 2 \end{bmatrix} \begin{bmatrix} \hat{x}_1 \ \hat{x}_2 \end{bmatrix} = \begin{bmatrix} 5 \ 4 \end{bmatrix}$$
   $$\begin{bmatrix} \hat{x}_1 \ \hat{x}_2 \end{bmatrix} = \frac{1}{3} \begin{bmatrix} 2 & -1 \ -1 & 2 \end{bmatrix} \begin{bmatrix} 5 \ 4 \end{bmatrix} = \frac{1}{3} \begin{bmatrix} 10 - 4 \ -5 + 8 \end{bmatrix} = \frac{1}{3} \begin{bmatrix} 6 \ 3 \end{bmatrix} = \begin{bmatrix} 2 \ 1 \end{bmatrix}$$

4. **Error Check**:
   $$\mathbf{p} = A \hat{\mathbf{x}} = \begin{bmatrix} 1 & 0 \ 0 & 1 \ 1 & 1 \end{bmatrix} \begin{bmatrix} 2 \ 1 \end{bmatrix} = \begin{bmatrix} 2 \ 1 \ 3 \end{bmatrix} = \mathbf{y}_{	ext{observed}} \implies 	ext{Error } \mathbf{e} = \mathbf{0}$$

5. **Final Result**:
   Least-Squares Estimated Position: $\hat{x}_1 = 2$, $\hat{x}_2 = 1$.

---

## Category 4: The Synthesis Problem (System Design / Identification)
* **The Question**: "How do we build it?"
* **Knowns**: Input Vectors ($\mathbf{x}_i$) and Output Vectors ($\mathbf{y}_i$).
* **Unknown**: System Matrix ($A$).

---

### Problem 7: System Identification of a 2-Port Circuit Filter
**Scenario**: An electrical engineer performs test measurements on an unknown black-box 2-port electronic filter (System $A$).
* Test 1: Input $\mathbf{x}_1 = \begin{bmatrix} 1 \ 0 \end{bmatrix}$ produces output $\mathbf{y}_1 = \begin{bmatrix} 2 \ 1 \end{bmatrix}$.
* Test 2: Input $\mathbf{x}_2 = \begin{bmatrix} 0 \ 1 \end{bmatrix}$ produces output $\mathbf{y}_2 = \begin{bmatrix} 1 \ 3 \end{bmatrix}$.

Determine the $2 	imes 2$ system transfer matrix $A$.

#### Step-by-Step Solution:
1. **Identify the Problem Type**: This is a **Synthesis Problem (System Identification)** because we observe inputs and outputs and must synthesize/reconstruct the internal system matrix $A$.

2. **Form Matrix Equation $A X = Y$**:
   Let $X = [\mathbf{x}_1 \; \mathbf{x}_2] = \begin{bmatrix} 1 & 0 \ 0 & 1 \end{bmatrix} = I_2$.
   Let $Y = [\mathbf{y}_1 \; \mathbf{y}_2] = \begin{bmatrix} 2 & 1 \ 1 & 3 \end{bmatrix}$.

3. **Solve for $A$**:
   $$A X = Y \implies A I_2 = Y \implies A = \begin{bmatrix} 2 & 1 \ 1 & 3 \end{bmatrix}$$

4. **Verification**:
   * $A \mathbf{x}_1 = \begin{bmatrix} 2 & 1 \ 1 & 3 \end{bmatrix} \begin{bmatrix} 1 \ 0 \end{bmatrix} = \begin{bmatrix} 2 \ 1 \end{bmatrix} = \mathbf{y}_1 \quad \checkmark$
   * $A \mathbf{x}_2 = \begin{bmatrix} 2 & 1 \ 1 & 3 \end{bmatrix} \begin{bmatrix} 0 \ 1 \end{bmatrix} = \begin{bmatrix} 1 \ 3 \end{bmatrix} = \mathbf{y}_2 \quad \checkmark$

5. **Final Result**:
   Synthesized System Matrix: $A = \begin{bmatrix} 2 & 1 \ 1 & 3 \end{bmatrix}$.

---

### Problem 8: Sensor Calibration via Least-Squares Line Fitting
**Scenario**: A temperature sensor is calibrated by taking output voltage readings $y$ at three known reference temperatures $t$:
* At $t = 0^\circ	ext{C}$, $y = 1	ext{ V}$
* At $t = 1^\circ	ext{C}$, $y = 2	ext{ V}$
* At $t = 2^\circ	ext{C}$, $y = 6	ext{ V}$

Synthesize the best linear calibration model $y = C + D t$ using least squares.

#### Step-by-Step Solution:
1. **Set Up System $A \mathbf{c} = \mathbf{b}$**:
   $$\begin{bmatrix} 1 & 0 \ 1 & 1 \ 1 & 2 \end{bmatrix} \begin{bmatrix} C \ D \end{bmatrix} = \begin{bmatrix} 1 \ 2 \ 6 \end{bmatrix}$$

2. **Compute $A^T A$ and $A^T \mathbf{b}$**:
   $$A^T A = \begin{bmatrix} 1 & 1 & 1 \ 0 & 1 & 2 \end{bmatrix} \begin{bmatrix} 1 & 0 \ 1 & 1 \ 1 & 2 \end{bmatrix} = \begin{bmatrix} 1+1+1 & 0+1+2 \ 0+1+2 & 0+1+4 \end{bmatrix} = \begin{bmatrix} 3 & 3 \ 3 & 5 \end{bmatrix}$$
   $$A^T \mathbf{b} = \begin{bmatrix} 1 & 1 & 1 \ 0 & 1 & 2 \end{bmatrix} \begin{bmatrix} 1 \ 2 \ 6 \end{bmatrix} = \begin{bmatrix} 1 + 2 + 6 \ 0 + 2 + 12 \end{bmatrix} = \begin{bmatrix} 9 \ 14 \end{bmatrix}$$

3. **Solve Normal Equations $(A^T A)\hat{\mathbf{c}} = A^T \mathbf{b}$**:
   $$\det(A^T A) = (3)(5) - (3)(3) = 15 - 9 = 6$$
   $$\begin{bmatrix} \hat{C} \ \hat{D} \end{bmatrix} = \frac{1}{6} \begin{bmatrix} 5 & -3 \ -3 & 3 \end{bmatrix} \begin{bmatrix} 9 \ 14 \end{bmatrix} = \frac{1}{6} \begin{bmatrix} 45 - 42 \ -27 + 42 \end{bmatrix} = \frac{1}{6} \begin{bmatrix} 3 \ 15 \end{bmatrix} = \begin{bmatrix} 0.5 \ 2.5 \end{bmatrix}$$

4. **Final Result**:
   Synthesized Calibration Formula: $y = 0.5 + 2.5t$ (Offset $C = 0.5	ext{ V}$, Sensitivity $D = 2.5	ext{ V/}^\circ	ext{C}$).

---

## Category 5: Resource Allocation & Cause-and-Effect Analysis
* **The Question**: "How do we allocate inputs or diagnose variable influence?"
* **Knowns**: System Constraints / Sensitivity Matrix.
* **Unknown**: Optimal Input Mix / Nullspace Redundancies.

---

### Problem 9: Factory Production Resource Allocation (Linear Programming)
**Scenario**: A manufacturing plant produces two items ($x_1$ and $x_2$ units).
* Profit function to maximize: $Z = 3x_1 + 2x_2$
* Raw material constraint: $x_1 + x_2 \le 4$
* Machine hours constraint: $2x_1 + x_2 \le 6$
* Nonnegativity constraints: $x_1 \ge 0, x_2 \ge 0$

Find the optimal resource allocation $(x_1, x_2)$ and maximum profit $Z$.

#### Step-by-Step Solution:
1. **Identify Corner Points of Feasible Region**:
   * Corner O: $(0, 0)$
   * Corner A ($x_2 = 0$): $2x_1 \le 6 \implies (3, 0)$
   * Corner B ($x_1 = 0$): $x_2 \le 4 \implies (0, 4)$
   * Corner C (Intersection of $x_1 + x_2 = 4$ and $2x_1 + x_2 = 6$):
     Subtracting equations: $(2x_1 + x_2) - (x_1 + x_2) = 6 - 4 \implies x_1 = 2$.
     Then $x_2 = 4 - 2 = 2 \implies (2, 2)$.

2. **Evaluate Profit $Z = 3x_1 + 2x_2$ at Each Corner**:
   * At O $(0, 0)$: $Z = 3(0) + 2(0) = 0$
   * At A $(3, 0)$: $Z = 3(3) + 2(0) = 9$
   * At B $(0, 4)$: $Z = 3(0) + 2(4) = 8$
   * At C $(2, 2)$: $Z = 3(2) + 2(2) = 6 + 4 = 10 \quad 	ext{(Maximum)}$

3. **Final Result**:
   Optimal Allocation: $x_1 = 2	ext{ units}$, $x_2 = 2	ext{ units}$. Maximum Profit $Z = \$10$.

---

### Problem 10: Cause-and-Effect Analysis & Redundancy Diagnosis
**Scenario**: A 3-sensor environmental monitoring system maps 3 physical causes ($x_1, x_2, x_3$) to 3 sensor outputs via sensitivity matrix $A$:
$$A = \begin{bmatrix} 1 & 2 & 3 \ 2 & 4 & 6 \ 1 & 1 & 1 \end{bmatrix}$$

1. Determine the rank $r$ of the system. Are the sensor equations fully independent?
2. Find the basis vector for the nullspace $N(A)$, which represents unobservable input fluctuations that cause zero output change.

#### Step-by-Step Solution:
1. **Reduce $A$ to Row Echelon Form**:
   * Operation $R_2 	o R_2 - 2R_1$:
     $$\begin{bmatrix} 1 & 2 & 3 \ 0 & 0 & 0 \ 1 & 1 & 1 \end{bmatrix}$$
   * Swap $R_2 \leftrightarrow R_3$:
     $$\begin{bmatrix} 1 & 2 & 3 \ 1 & 1 & 1 \ 0 & 0 & 0 \end{bmatrix}$$
   * Operation $R_2 	o R_2 - R_1$:
     $$\begin{bmatrix} 1 & 2 & 3 \ 0 & -1 & -2 \ 0 & 0 & 0 \end{bmatrix}$$
   Pivots are in Columns 1 and 2. **Rank $r = 2$**.
   Since $r = 2 < 3$, Row 2 is completely redundant ($2 	imes 	ext{Row 1}$).

2. **Find Nullspace Basis $N(A)$**:
   Set up $R\mathbf{x} = \mathbf{0}$ with free variable $x_3 = 1$:
   $$-x_2 - 2x_3 = 0 \implies x_2 = -2x_3 = -2$$
   $$x_1 + 2x_2 + 3x_3 = 0 \implies x_1 + 2(-2) + 3(1) = 0 \implies x_1 - 1 = 0 \implies x_1 = 1$$

3. **Nullspace Basis Vector**:
   $$\mathbf{x}_n = \begin{bmatrix} 1 \ -2 \ 1 \end{bmatrix}$$

4. **Physical Interpretation**:
   Any input variation along the direction $\mathbf{x}_n = [1, -2, 1]^T$ satisfies $A\mathbf{x}_n = \mathbf{0}$, meaning it produces **zero response** across all sensors and is completely unobservable.

5. **Final Result**:
   * System Rank $r = 2$ (1 redundant sensor equation).
   * Nullspace Basis: $\mathbf{x}_n = \begin{bmatrix} 1 \ -2 \ 1 \end{bmatrix}$ (Nullity = $n - r = 3 - 2 = 1$).
