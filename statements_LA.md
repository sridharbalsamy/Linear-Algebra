


Here is a collection of fundamental, geometrically intuitive statements in linear algebra that connect matrix operations, vector spaces, and projections.
## 🏠 Fundamental Subspaces (The "Big Picture")

* The nullspace of $A$ is strictly perpendicular to the row space of $A$. Every vector that gets crushed to zero by matrix $A$ hits the rows at a perfect $90^\circ$ angle ($A\mathbf{x} = \mathbf{0}$).
* The left nullspace of $A$ (the nullspace of $A^T$) is strictly perpendicular to the column space of $A$.
* The rank of a matrix is always exactly equal to the rank of its transpose ($\text{rank}(A) = \text{rank}(A^T)$). A matrix has the exact same number of linearly independent rows as it does independent columns, no matter its shape.

## 📐 Orthogonality & Projections

* If a matrix $Q$ has orthogonal columns of length 1, multiplying a vector by its transpose ($Q^T\mathbf{x}$) preserves lengths and angles. It acts as a pure rotation or reflection, never stretching space.
* For any matrix $A$, the square matrix $A^TA$ is always symmetric and positive semidefinite. Its eigenvalues are never negative, and it shares the exact same nullspace as $A$.
* A projection matrix $P$ multiplied by itself is just $P$ ($P^2 = P$). Once you project a vector onto a subspace, projecting it a second time changes absolutely nothing because the vector is already there.

## 🔄 Determinants & Eigenvalues

* The determinant of a matrix represents the volume scaling factor of the transformation. If $\det(A) = 2$, the matrix doubles the volume of any shape it transforms; if $\det(A) = 0$, it flattens the entire space into a lower dimension.
* The trace (sum of the diagonal) of a matrix is always equal to the sum of its eigenvalues, and the determinant is always equal to the product of its eigenvalues.
* Every symmetric matrix ($A = A^T$) has entirely real eigenvalues, and its eigenvectors are always perpendicular to each other.


the error vector in the least squares method is perpendicular (orthogonal) to the column space of matrix A



