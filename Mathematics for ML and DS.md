- [1. Linear Algebra](#1-linear-algebra)
  - [1.1. Week 1: Systems of linear equations](#11-week-1-systems-of-linear-equations)
    - [Describing singularity of systems of linear equations](#describing-singularity-of-systems-of-linear-equations)
    - [Linear dependence and independence](#linear-dependence-and-independence)
    - [Determinant](#determinant)
  - [1.2. Week 2: Solving systems of linear equations](#12-week-2-solving-systems-of-linear-equations)
    - [Elimination Method](#elimination-method)
    - [Matrix Row Reduction (a.k.a. Gaussian Elimination)](#matrix-row-reduction-aka-gaussian-elimination)
    - [Row Echelon Form \& Rank](#row-echelon-form--rank)
      - [Row Echelon Form (general case)](#row-echelon-form-general-case)
      - [Reduced Row Echelon Form](#reduced-row-echelon-form)
      - [Using Gaussian Elimination Algorithm](#using-gaussian-elimination-algorithm)
  - [1.3. Week 3: Vectors and Linear Transformations](#13-week-3-vectors-and-linear-transformations)
  - [1.4. Week 4: Determinants and Eigenvectors](#14-week-4-determinants-and-eigenvectors)

# 1. Linear Algebra

## 1.1. Week 1: Systems of linear equations

Systems of equations like the one below can be thought of as dataframes:

$$
    w_1x_1^{(1)} + w_2x_2^{(1)} + \ldots + w_nx_n^{(1)} + b = y^{(1)}\\
    w_1x_1^{(2)} + w_2x_2^{(2)} + \ldots + w_nx_n^{(2)} + b = y^{(2)}\\
    \vdots\\
    w_1x_1^{(m)} + w_2x_2^{(m)} + \ldots + w_nx_n^{(m)} + b = y^{(m)}\\
$$

In other terms:

$$
    W \cdot X + b = \hat{y}\\
$$

$$
    \begin{bmatrix}
        w_1 & w_2 & w_3 & \ldots & w_n 
    \end{bmatrix}
    \begin{bmatrix}
        x_1^{(1)} & x_2^{(1)} & x_3^{(1)} & \dots & x_n^{(1)}\\
        x_1^{(2)} & x_2^{(2)} & x_3^{(2)} & \dots & x_n^{(2)}\\
        x_1^{(3)} & x_2^{(3)} & x_3^{(3)} & \dots & x_n^{(3)}\\
        \vdots\\
        x_1^{(m)} & x_2^{(m)} & x_3^{(m)} & \dots & x_n^{(m)}
    \end{bmatrix}
    =
    \begin{bmatrix}
        y^{(1)} & y^{(2)} & y^{(3)} & \ldots & y^{(m)}
    \end{bmatrix}
$$

### Describing singularity of systems of linear equations ###

* **Non-singular**: complete, one unique solution
  * Called "non-singular" because each additional equation adds valuable info to the system
* **Singular**: redundant or contradictory, multiple or no solutions

When determining if an equation is singular or non-singular, **we can set the constant to zero**. Doing so will not affect the singularity of the system, and will allows us to think in terms of matrices.

### Linear dependence and independence ###
Below: row 1 + row 2 = row 3, therefore row 3 **depends** on rows 1 and 2. This means that this system is **linearly dependent**.

$$
    a=1\\
    b=2\\
    a+b=3\\
$$

$$
    \begin{bmatrix}
    1 & 0 & 0\\
    0 & 1 & 0\\
    1 & 1 & 0
    \end{bmatrix}
$$

Below: no relations can be found between the rows. This means that this system is **linearly independent**.

$$
    a+b+c=0\\
    a+2b+c=0\\
    a+b+2c=0\\
$$

$$
    \begin{bmatrix}
    1 & 1 & 1\\
    1 & 2 & 1\\
    1 & 1 & 2
    \end{bmatrix}
$$

### Determinant ###
In a matrix of form:

$$
    \begin{bmatrix}
    a & b \\
    c & d
    \end{bmatrix}
$$

the determinant is defined as:

$$ad-bc$$

* The determinant is 0 if the matrix is singular, and non-zero if the matrix is non-singular.

In a large matrix:

$$
    \begin{bmatrix}
    1 & 2 & 3 \\
    4 & 5 & 6 \\
    7 & 8 & 9
    \end{bmatrix}
$$

$$
    (\begin{bmatrix}
    1 &  &  \\
     & 5 &  \\
     &  & 9
    \end{bmatrix} +     
    \begin{bmatrix}
     & 2 &  \\
     &  & 6 \\
    7 &  & 
    \end{bmatrix} +     
    \begin{bmatrix}
     &  & 3 \\
    4 &  &  \\
     & 8 & 
    \end{bmatrix}) - 
    (\begin{bmatrix}
     &  & 3 \\
     & 5 &  \\
    7 &  & 
    \end{bmatrix} +     
    \begin{bmatrix}
    1 &  &  \\
     &  & 6 \\
     & 8 & 
    \end{bmatrix} +     
    \begin{bmatrix}
     & 2 &  \\
    4 &  &  \\
     &  & 9
    \end{bmatrix})\\
$$

$$
    ((1\times5\times9) + (2\times6\times7) + (3\times4\times8)) - ((7\times5\times3) + (8\times6\times1) + (9\times4\times2))
$$

## 1.2. Week 2: Solving systems of linear equations

### Elimination Method
The goal is to remove a variable from the second and third equations so as to isolate it for solving.

Ex. Given 3 equations:

$$
\begin{align}
a+b+2c=12 \\
3a-3b-c=3 \\
2a-b+6c=24
\end{align}
$$

To solve, first divide all three equations by each coefficient of a:

$$
\begin{align}
a+b+2c=12 \\
a-b-(1/3)c=1 \\
a-(1/2)b+3c=12
\end{align}
$$

Next, subtract equation 1 from equations 2 and 3 and solve as usual:

$$
\begin{align}
a+b+2c=12 \\
-2b-(7/3)c=-11 \\
-(3/2)b+c=0
\end{align}
$$

### Matrix Row Reduction (a.k.a. Gaussian Elimination)
The application of elimination method to matrices via row operations

All row operations preserve singularity in a matrix. The three types of row operations are explained below:

1. **Switching rows**
    $$
    \begin{bmatrix}
    5 & 1  \\
    4 & 3  \\
    \end{bmatrix}
    
    \begin{array}{c}
    \rightarrow
    \end{array}
    
    \begin{bmatrix}
    4 & 3  \\
    5 & 1  \\
    \end{bmatrix}
    $$
    * Produces negative of original determinant value
      * 11 to -11
2. **Multiplying a row by a scalar**
    $$
    \begin{bmatrix}
    5 & 1  \\
    4 & 3  \\
    \end{bmatrix}
    
    \begin{array}{c}
    \rightarrow
    \end{array}
    
    \begin{bmatrix}
    50 & 10  \\
    4 & 3  \\
    \end{bmatrix}
    $$
    * Multiplies original determinant value by the chosen scalar
      * 11 to 110
3. **Adding a row to another row**
   $$
    \begin{bmatrix}
    5 & 1  \\
    4 & 3  \\
    \end{bmatrix}
    
    \begin{array}{c}
    \rightarrow
    \end{array}
    
    \begin{bmatrix}
    9 & 4  \\
    4 & 3  \\
    \end{bmatrix}
    $$
    * Determinant is unaffected
      * 11 to 11

### Row Echelon Form & Rank
**Rank** refers to the amount of information contained in a system.

Rank = # of rows - dimension of solution space

Thus, all non-singular systems (i.e. systems with a unique solution) all have full-rank.

#### Row Echelon Form (general case)
* "zero" rows at bottom
* each row has a pivot (left-most non-zero entry)
* every pivot is to the right of the pivots above it
* **rank = the number of pivots in row echelon form**
* a matrix is non-singular iff there are only ones in the main diagonal of the row echelon form
* note: you can divide a matrix by its pivot to achieve one's, this makes no mathematical difference in terms of rank but is preferred for formatting purposes

Example with singular matrix:

$$
    \begin{bmatrix}
    1 & 1 & 1  \\
    1 & 1 & 2  \\
    1 & 1 & 3
    \end{bmatrix}
    
    \begin{array}{c}
    \text{Subtracting row 1}\\\text{from row 2 and row 3}\\
    \rightarrow
    \end{array}
    
   \begin{bmatrix}
    1 & 1 & 1  \\
    0 & 0 & 1  \\
    0 & 0 & 2
    \end{bmatrix}

    \begin{array}{c}
    \text{Subtracting 2x row 2}\\\text{from row 3}\\
    \rightarrow
    \end{array}

    \begin{array}{c}\\\\
   \begin{bmatrix}
    1 & 1 & 1  \\
    0 & 0 & 1  \\
    0 & 0 & 0
    \end{bmatrix}\\\\
    \text{Rank = 2}
    \end{array}

$$

#### Reduced Row Echelon Form
* Is in row-echelon form
* each pivot is a 1
* any number above pivot is 0

#### Using Gaussian Elimination Algorithm
Ex:

$$
\begin{array}{rcl}
    2a - b + c & = & 1 \\
    2a + 2b + 4c & = & -2 \\
    4a + b & = & -1 
\end{array}
\quad
\begin{bmatrix}
    2 & -1 & 1 & 1  \\
    2 & 2 & 4 & -2  \\
    4 & 1 & 0 & -1
\end{bmatrix}
$$

1. Set top left as pivot, set to 1 using row operations
2. Repeat row by row to get row echelon form, applying row operations to constants

$$
\text{Row echelon form:}
\begin{bmatrix}
    1 & -1/2 & 1/2 & 1/2  \\
    0 & 1 & 1 & -1  \\
    0 & 0 & 1 & 0
\end{bmatrix}
$$

3. Apply back substitution (use pivots to create zeroes above themselves)

$$
\text{Reduced row echelon form:}
\begin{bmatrix}
    1 & 0 & 0 & 0  \\
    0 & 1 & 0 & -1  \\
    0 & 0 & 1 & 0
\end{bmatrix}
$$

* Note: in a singular case, a row of zeroes will appear. The algorithm stops here, as there will be no unique solution (0=0).

In summary:
1. Create augmented matrix
2. Get the matrix into reduced row echelon form
3. Complete back substitution
4. Stop if you encounter a row of zeroes

## 1.3. Week 3: Vectors and Linear Transformations

## 1.4. Week 4: Determinants and Eigenvectors

<!-- # 2. Calculus
# 3. Probability & Statistics -->
