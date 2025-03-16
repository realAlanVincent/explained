# Simplex Method Solution in Tableau Form

This Markdown file provides a step‐by‐step solution to the following linear program using the simplex method:

**Problem Statement:**

\[
\begin{aligned}
\text{Maximize}\quad 
& Z = 3x_{1} + 2x_{2} + 4x_{3} \\[6pt]
\text{subject to}\quad
& 2x_{1} + 3x_{2} \le 8,\\
& 2x_{2} + 5x_{3} \le 10,\\
& x_{1},\, x_{2},\, x_{3} \ge 0.
\end{aligned}
\]

We introduce slack variables \( S_{1} \) and \( S_{2} \) to convert the constraints into equalities:

\[
\begin{aligned}
2x_{1} + 3x_{2} + S_{1} &= 8,\\
2x_{2} + 5x_{3} + S_{2} &= 10.
\end{aligned}
\]

---

## Initial Tableau

| Profit/Unit \(c_B\) | Variables in Basis (\(B\)) | \(x_1\) | \(x_2\) | \(x_3\) | \(S_1\) | \(S_2\) | \(\text{RHS}\) | Min Ratio |
|:--------------------:|:-------------------------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------------:|:---------:|
| 0                    | \(S_1\)                  | 2       | 3       | 0       | 1       | 0       | 8             |           |
| 0                    | \(S_2\)                  | 0       | 2       | 5       | 0       | 1       | 10            |           |
|                      |                          |         |         |         |         |         |               |           |
| **\(Z = 0\)**        |                          |         |         |         |         |         |               |           |
| \(c_j\)              |                          | 3       | 2       | 4       | 0       | 0       |               |           |
| \(c_j - z_j\)        |                          | 3       | 2       | 4       | 0       | 0       |               |           |

- **Basis:** \(S_1\) and \(S_2\) (each has profit 0).
- **\(\text{RHS}\)**: \(b = (8, 10)\).
- **\(c_j - z_j\)** row: Initially equals \(c_j\) because \(z_j=0\).

### Entering and Leaving Variables

- **Most positive** \(c_j - z_j\) is 4 under \(x_3\). Thus, \(x_3\) enters.
- **Min Ratio**:
  - Row \(S_1\): Coefficient of \(x_3\) is 0 (cannot pivot).
  - Row \(S_2\): \(\frac{10}{5} = 2\).
  
So \(S_2\) leaves the basis. We pivot on the entry (5) in the \(S_2\) row, \(x_3\) column.

---

## Tableau After First Pivot

1. **Normalize** the leaving row \(S_2\): Divide by 5.

   \[
   S_2\text{-row becomes: } 
   \bigl[\,0,\;0.4,\;1,\;0,\;0.2\;\big|\;2\bigr].
   \]

2. **Eliminate** \(x_3\) from other rows:

   - **Row \(S_1\)** is unchanged because its \(x_3\) coefficient is 0.
   - **\(Z\)-row**: Add \(4 \times\) the new \(x_3\)-row to eliminate the \(-4\) (or 4) under \(x_3\).

The updated tableau:

| Profit/Unit \(c_B\) | Basis Var. | \(x_1\) | \(x_2\) | \(x_3\) | \(S_1\) | \(S_2\) | \(\text{RHS}\) |
|:--------------------:|:----------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------------:|
| 0                    | \(S_1\)    | 2       | 3       | 0       | 1       | 0       | 8             |
| 0                    | \(x_3\)    | 0       | 0.4     | 1       | 0       | 0.2     | 2             |
|                      |            |         |         |         |         |         |               |
| **\(Z = 8\)**        |            | 0       | 1.6     | 0       | 0       | 0.8     | 8             |

At this point, the basis is \(\{S_1, x_3\}\). The objective function value is \(Z = 8\).

### Determine Next Entering Variable

Check \(c_j - z_j\). Equivalently, look at the row for nonbasic variables:

- \(x_1\) has coefficient in \(Z\)-row: effectively 0 in the above but we re‐compute \(c_j - z_j\) if needed.  
- \(x_2\) has a coefficient 1.6 in the \(Z\)-row? Actually, that indicates a positive margin if \(x_2\) is nonbasic. We also check the official \(c_j - z_j\) row:
  - For \(x_1\): \(c_{j}-z_{j} = 3 - 0 = 3\).
  - For \(x_2\): \(c_{j}-z_{j} = 2 - 1.6 = 0.4\).
  - For \(S_2\): \(c_{j}-z_{j} = 0 - 0.8 = -0.8\).

The **most positive** is 3 (under \(x_1\)). Thus \(x_1\) enters.

### Determine Leaving Variable

Pivot column: \(x_1\). Compute the min ratio:

- Row \(S_1\): \(\frac{8}{2} = 4\).
- Row \(x_3\): Coefficient is 0 → not considered.

Hence \(S_1\) leaves. The pivot element is 2 in the \(S_1\) row, \(x_1\) column.

---

## Second Pivot & Final Tableau

1. **Normalize** \(S_1\)-row (divide by 2):

   \[
   \bigl[\,1,\;1.5,\;0,\;0.5,\;0\;\big|\;4\bigr].
   \]
   This row now represents \(x_1\).

2. **Eliminate** \(x_1\) from the other rows:

   - Row \(x_3\) has 0 under \(x_1\), no change.
   - \(Z\)-row is already 0 in \(x_1\) if we track it carefully; so minimal or no change needed.

The final tableau:

| Profit/Unit \(c_B\) | Basis Var. | \(x_1\) | \(x_2\) | \(x_3\) | \(S_1\) | \(S_2\) | \(\text{RHS}\) |
|:--------------------:|:----------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------------:|
| 3                    | \(x_1\)    | 1       | 1.5     | 0       | 0.5     | 0       | 4             |
| 4                    | \(x_3\)    | 0       | 0.4     | 1       | 0       | 0.2     | 2             |
|                      |            |         |         |         |         |         |               |
| **\(Z = 20\)**       |            |         |         |         |         |         | 20            |

(We compute \(Z\) directly from \(x_1=4\) and \(x_3=2\).)

---

## Optimal Solution

\[
x_1 = 4,\quad x_2 = 0,\quad x_3 = 2,\quad \text{and} \quad Z_{\max} = 20.
\]

Therefore, the **maximum value** of the objective function is \(\boxed{20}\), achieved at
\[
\boxed{x_1 = 4,\; x_2 = 0,\; x_3 = 2.}
\]
