---
title: 'Understanding Matrix Multiplication with NumPy'
date: 2024-09-27
permalink: /posts/2024/09/numpy-dot-product/
tags:
  - Math
---



Matrix multiplication can be quite confusing, especially when using the versatile `np.dot()` function in NumPy. In this blog, we'll dive into the three main types of matrix multiplication: vector-vector, vector-matrix, and matrix-matrix operations. We'll clarify how these operations work and provide examples to enhance your understanding.

## 1. Vector and Vector

Let's start with the simplest case: multiplying two vectors.

Consider the vectors:

$$
\mathbf{a} = [a_1, a_2, a_3]
$$

$$
\mathbf{b} = [b_1, b_2, b_3]
$$

When we compute the dot product of these vectors, we can express it as:

$$
\text{np.dot}(\mathbf{a}, \mathbf{b}) = a_1 \cdot b_1 + a_2 \cdot b_2 + a_3 \cdot b_3
$$

This operation yields a single scalar value, which represents the cosine of the angle between the two vectors when both are treated as directed quantities.


## 2. Vector and Matrix

Now, let’s examine the case of multiplying a vector by a matrix.

Suppose we have:

* Vector  \\( \mathbf{a} = [1, 2, 3] \\)

* Matrix \\(
\mathbf{b} = 
\begin{bmatrix}
4 & 7 & 10 \\
5 & 8 & 11 \\
6 & 9 & 12 
\end{bmatrix}
\\)

Here, the shape of vector \\(\mathbf{a}\\) is (1, 3), while the shape of matrix \\(\mathbf{b}\\) is (3, 3).

When we perform:

$$
\text{np.dot}(\mathbf{a}, \mathbf{b})
$$

the operation is valid because the number of columns in \\(\mathbf{a}\\) matches the number of rows in \\(\mathbf{b}\\). The output will have the shape (1, 3) since it takes the rows from the first matrix and columns from the second matrix. The calculation can be described as:

$$
\text{np.dot}(\mathbf{a}, \mathbf{b}) = [1 \cdot 4 + 2 \cdot 7 + 3 \cdot 10, \ 1 \cdot 5 + 2 \cdot 8 + 3 \cdot 11, \ 1 \cdot 6 + 2 \cdot 9 + 3 \cdot 12]
$$

This results in:

$$
\text{np.dot}(\mathbf{a}, \mathbf{b}) = [48, 54, 60]
$$

Conversely, attempting to compute:

$$
\text{np.dot}(\mathbf{b}, \mathbf{a})
$$

would require us to represent vector \\(\mathbf{a}\\) in a column format. Thus, we convert \\(\mathbf{a}\\) to:

$$
\mathbf{a'} = 
\begin{bmatrix}
1 \\
2 \\
3 
\end{bmatrix}
$$

Now, the multiplication is valid because \\(\mathbf{b}\\) is (3, 3) and \\(\mathbf{a'}\\) is (3, 1). The operation now computes:

$$
\text{np.dot}(\mathbf{b}, \mathbf{a'}) = 
\begin{bmatrix}
4 & 7 & 10 \\
5 & 8 & 11 \\
6 & 9 & 12 
\end{bmatrix} \cdot 
\begin{bmatrix}
1 \\
2 \\
3 
\end{bmatrix}
$$

This results in a new vector:

$$
\text{np.dot}(\mathbf{b}, \mathbf{a'}) = 
\begin{bmatrix}
4 \cdot 1 + 5 \cdot 2 + 6 \cdot 3 \\
7 \cdot 1 + 8 \cdot 2 + 9 \cdot 3 \\
10 \cdot 1 + 11 \cdot 2 + 12 \cdot 3 
\end{bmatrix} = 
\begin{bmatrix}
32 \\
50 \\
68 
\end{bmatrix}
$$


## 3. Matrix and Matrix

Lastly, let’s discuss the multiplication of two matrices.

Consider:

* Matrix \\( \mathbf{a} = 
\begin{bmatrix}
a_{11} & a_{12} & a_{13} \\
a_{21} & a_{22} & a_{23} \\
a_{31} & a_{32} & a_{33}
\end{bmatrix} \\)

\\
* Matrix \\( \mathbf{b} = 
\begin{bmatrix}
b_{11} & b_{12} & b_{13} \\
b_{21} & b_{22} & b_{23} \\
b_{31} & b_{32} & b_{33}
\end{bmatrix} \\)

The multiplication \\( \text{np.dot}(\mathbf{a}, \mathbf{b}) \\) is possible if the number of columns in \\(\mathbf{a}\\) equals the number of rows in \\(\mathbf{b}\\). The output matrix will have the shape defined by the rows of \\(\mathbf{a}\\) and columns of \\(\mathbf{b}\\). For instance:

$$
\text{np.dot}(\mathbf{a}, \mathbf{b}) = 
\begin{bmatrix}
a_{11} \cdot b_{11} + a_{12} \cdot b_{21} + a_{13} \cdot b_{31} & a_{11} \cdot b_{12} + a_{12} \cdot b_{22} + a_{13} \cdot b_{32} & a_{11} \cdot b_{13} + a_{12} \cdot b_{23} + a_{13} \cdot b_{33} \\
a_{21} \cdot b_{11} + a_{22} \cdot b_{21} + a_{23} \cdot b_{31} & a_{21} \cdot b_{12} + a_{22} \cdot b_{22} + a_{23} \cdot b_{32} & a_{21} \cdot b_{13} + a_{22} \cdot b_{23} + a_{23} \cdot b_{33} \\
a_{31} \cdot b_{11} + a_{32} \cdot b_{21} + a_{33} \cdot b_{31} & a_{31} \cdot b_{12} + a_{32} \cdot b_{22} + a_{33} \cdot b_{32} & a_{31} \cdot b_{13} + a_{32} \cdot b_{23} + a_{33} \cdot b_{33}
\end{bmatrix}
$$

## Conclusion

Understanding matrix multiplication is crucial for effective data manipulation and analysis in machine learning and data science. By grasping how NumPy handles these operations, you can apply them effectively to your data processing tasks. The versatility of `np.dot()` allows for various multiplication types, but it's essential to keep track of the shapes of your matrices and vectors to avoid errors.
