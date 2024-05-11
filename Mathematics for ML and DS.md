- [1. Linear Algebra](#1-linear-algebra)
  - [1.1. Week 1: Systems of linear equations](#11-week-1-systems-of-linear-equations)
    - [Describing singularity of systems of linear equations](#describing-singularity-of-systems-of-linear-equations)
    - [Linear dependence and independence](#linear-dependence-and-independence)
    - [Determinant](#determinant)
  - [1.2. Week 2: Solving systems of linear equations](#12-week-2-solving-systems-of-linear-equations)
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
    ((1*5*9)+     
    (2*6*7)+     
    (3*4*8)) - 
    ((7*5*3) +     
    (8*6*1) +     
    (9*4*2))
    
$$

## 1.2. Week 2: Solving systems of linear equations

## 1.3. Week 3: Vectors and Linear Transformations

## 1.4. Week 4: Determinants and Eigenvectors

<!-- # 2. Calculus
# 3. Probability & Statistics -->