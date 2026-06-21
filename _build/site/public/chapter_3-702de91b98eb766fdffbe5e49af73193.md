---
title: 第3章：向量空间与子空间
date: 2024-12-01 00:00:00
---

## 1. 标准 $n$ 维空间

$\mathbb{R}^n$ 是具有 $n$ 个分量的实列向量的全体集合。

## 2. 封闭性

若 $\vec{v}$ 与 $\vec{w}$ 在向量空间 $S$ 中，则它们的任意线性组合 $c\vec{v} + d\vec{w}$ 也必在 $S$ 中。

## 3. 单点空间 $Z$

只包含零向量的空间，即 $Z = \{ \vec{0} \}$。

## 4. 直观理解

* **$\mathbb{R}^2$**：由通常的二维平面表示。$\mathbb{R}^2$ 中每个向量 $\vec{v}$ 有 $2$ 个分量，即 $\vec{v} = (x, y)$。
* **$\mathbb{R}^3$**：对应三维空间中的点 $(x, y, z)$。

## 5. 子空间 (Subspace)

向量空间的子空间是指满足以下两个条件的向量集合（必须包含 $\vec{0}$）：

若 $\vec{v}$ 和 $\vec{w}$ 都是子空间中的向量，$c$ 为任意标量，则有：

* (i) **加法封闭**：$\vec{v} + \vec{w}$ 在子空间中。
* (ii) **数乘封闭**：$c\vec{v}$ 在子空间中。

> **直观理解：** 在三维空间 $\mathbb{R}^3$ 中选取一个**过原点 $(0,0,0)$ 的平面**。该平面就自身而言是一个向量空间。但该平面并非 $\mathbb{R}^2$（因为其中的向量均有三个分量），而是 $\mathbb{R}^3$ 的一个子空间。

## 6. 每个子空间均含零向量

这是子空间定义的直接推论（令 $c=0$ 即得）。

## 7. $A$ 的列空间 (Column Space)

矩阵 $A$ 的列空间 $C(A)$ 包含 $A$ 各列的全部线性组合。这些线性组合构成了所有可能的向量 $Ax$。

> **※ 核心点：** 解 $Ax=b$ 就是判断 $b$ 是否可以表示为 $A$ 各列的一个线性组合。
> 线性方程组 $Ax=b$ 是可解的，当且仅当 $b$ 在 $A$ 的列空间 $C(A)$ 内。

* 设 $A$ 为 $m \times n$ 矩阵，它的列向量有 $m$ 个分量，故各列向量属于 $\mathbb{R}^m$。
* $A$ 的列空间是 $\mathbb{R}^m$ 的子空间。

## 8. $A$ 的零空间 (Null Space)

零空间 $N(A)$ 由 $Ax=0$ 的**全部解**构成。

* 消元法不改变零空间：$N(A) = N(U) = N(R)$。
* **强调：** 解向量 $x$ 有 $n$ 个分量，这些向量都在 $\mathbb{R}^n$ 中，因此 $N(A)$ 是 $\mathbb{R}^n$ 的子空间。

## 9. 主元列与自由列

$$
Ax=0: \quad A = \begin{bmatrix} 1 & 2 & 2 & 4 \\ 3 & 8 & 6 & 16 \end{bmatrix} \xrightarrow{\text{高斯消元}} U = \begin{bmatrix} 1 & 2 & 2 & 4 \\ 0 & 2 & 0 & 4 \end{bmatrix}
$$

* **主元列**：含主元的列（第1、2列）。
* **自由列**：不含主元的列（第3、4列）。

解向量 $x$ 有4个分量 $\vec{x} = (x_1, x_2, x_3, x_4)$，方程 $Ux=0$ 可写为：

$$
x_1\begin{bmatrix} 1 \\ 0 \end{bmatrix} + x_2\begin{bmatrix} 2 \\ 2 \end{bmatrix} + x_3\begin{bmatrix} 2 \\ 0 \end{bmatrix} + x_4\begin{bmatrix} 4 \\ 4 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix}
$$

* $x_1, x_2$ 为主元变量。
* $x_3, x_4$ 为自由变量。

对于自由变量 $x_3$ 与 $x_4$，轮流取值 $1$ 和 $0$ 以求出基础解系：

* 令 $x_3=1, x_4=0 \implies \vec{x} = \begin{bmatrix} -2 \\ 0 \\ 1 \\ 0 \end{bmatrix}$
* 令 $x_3=0, x_4=1 \implies \vec{x} = \begin{bmatrix} 2 \\ -2 \\ 0 \\ 1 \end{bmatrix}$

## 10. 最简行阶梯形矩阵 $R$ (Reduced Row Echelon Form)

$$
A = \begin{bmatrix} 1 & 2 & 2 & 4 \\ 3 & 8 & 6 & 16 \end{bmatrix} \xrightarrow{\text{消元}} U = \begin{bmatrix} 1 & 2 & 2 & 4 \\ 0 & 2 & 0 & 4 \end{bmatrix} \xrightarrow{\text{向上消元并单位化}} R = \begin{bmatrix} 1 & 0 & 2 & 0 \\ 0 & 1 & 0 & 2 \end{bmatrix}
$$

一般形式举例：

$$
R = \begin{bmatrix} 1 & 0 & \times & \times & 0 & \times \\ 0 & 1 & \times & \times & 0 & \times \\ 0 & 0 & 0 & 0 & 1 & \times \\ 0 & 0 & 0 & 0 & 0 & 0 \end{bmatrix} \quad (\times \text{ 表示任意实数})
$$

对于 $Rx=0$，若 $\vec{x} = (x_1, \dots, x_7)$：

* **主元变量**：对应列有主元 $1$ 的变量（如 $x_1, x_2, x_6$）。
* **自由变量**：没有主元的列对应的变量（如 $x_3, x_4, x_5, x_7$）。
* 通过设定一个自由变量取 $1$，其余自由变量取 $0$，可得到零空间的一组基。

## 11. 矩阵的秩 (Rank)

* $A$ 的秩为主元的个数，记为 $\text{rank}(A) = r$。
* $\text{rank}(A) = \text{rank}(U) = \text{rank}(R)$。
* **第二种理解：** $A, U, R$ 有 $r$ 个线性无关的行，也有 $r$ 个线性无关的列。
* **第三种理解：** $A$ 的秩 $r$ 是列空间 $C(A)$ 的维数，$n-r$ 是零空间 $N(A)$ 的维数。

## 12. $Ax=b$ 的全解

* **※ 核心理解：** $Ax=b$ 的全解结构为：
    $$
    x = x_p + x_n
    $$
    其中 $x_p$ 是**特解** (Particular Solution)，$x_n$ 是**零空间中任意元素** (Nullspace Solution)。
* **原因：** $Ax_p = b, Ax_n = 0 \implies A(x_p + x_n) = b$。
* **步骤：** 分别求出 $x_p$ 和 $x_n$，相加即为全解。

**第一步：求解 $Ax_n=0$**
将 $Ax=0$ 化为 $Rx=0$，对自由变量赋值 $1$ 和 $0$。

例：$A = \begin{bmatrix} 1 & 3 & 0 & 2 \\ 0 & 0 & 1 & 4 \\ 1 & 3 & 1 & 6 \end{bmatrix} \xrightarrow{\text{消元}} \begin{bmatrix} 1 & 3 & 0 & 2 \\ 0 & 0 & 1 & 4 \\ 0 & 0 & 0 & 0 \end{bmatrix}$

* 主元变量 $x_1, x_3$；自由变量 $x_2, x_4$。
* 令 $x_2=1, x_4=0 \implies \vec{x}_1 = \begin{bmatrix} -3 \\ 1 \\ 0 \\ 0 \end{bmatrix}$
* 令 $x_2=0, x_4=1 \implies \vec{x}_2 = \begin{bmatrix} -2 \\ 0 \\ -4 \\ 1 \end{bmatrix}$
* 零空间通解：$x_n = C_1 \begin{bmatrix} -3 \\ 1 \\ 0 \\ 0 \end{bmatrix} + C_2 \begin{bmatrix} -2 \\ 0 \\ -4 \\ 1 \end{bmatrix}$。

**第二步：求解 $Ax_p=b$**
构造**增广矩阵** $[A \ b]$ 进行消元。

$$
[A \ b] = \begin{bmatrix} 1 & 3 & 0 & 2 & 1 \\ 0 & 0 & 1 & 4 & 6 \\ 1 & 3 & 1 & 6 & 7 \end{bmatrix} \xrightarrow{\text{消元}} [R \ d] = \begin{bmatrix} 1 & 3 & 0 & 2 & 1 \\ 0 & 0 & 1 & 4 & 6 \\ 0 & 0 & 0 & 0 & 0 \end{bmatrix}
$$

对应方程组：$\begin{cases} x_1 + 3x_2 + 2x_4 = 1 \\ x_3 + 4x_4 = 6 \end{cases}$。
令所有**自由变量为 $0$**（$x_2=0, x_4=0$），解得 $x_1=1, x_3=6$。
特解：$x_p = \begin{bmatrix} 1 \\ 0 \\ 6 \\ 0 \end{bmatrix}$。

**全解总结：**

$$
x = x_p + x_n = \begin{bmatrix} 1 \\ 0 \\ 6 \\ 0 \end{bmatrix} + C_1 \begin{bmatrix} -3 \\ 1 \\ 0 \\ 0 \end{bmatrix} + C_2 \begin{bmatrix} -2 \\ 0 \\ -4 \\ 1 \end{bmatrix}
$$

## 13. 列满秩 ($r=n$)

$m \times n$ 矩阵 $A$ 的秩等于列数。

**性质：**

1. $A$ 的各列均为主元列。
2. 没有自由变量。
3. 零空间 $N(A)$ 只有零向量 $\{\vec{0}\}$。
4. 若 $Ax=b$ 有解，则只有**唯一解**（各列线性无关）。

## 14. 行满秩 ($r=m$)

$m \times n$ 矩阵 $A$ 的秩等于行数。

**性质：**

1. 各行均有主元，$R$ 没有全 $0$ 行。
2. 对于任意 $b$，方程组 $Ax=b$ **均有解**。
3. 列空间为整个 $\mathbb{R}^m$。
4. 零空间 $N(A)$ 包含 $n-m$ 个自由变量对应的特殊解。

## 15. 线性方程组解的四种情形

根据系数矩阵的秩 $r$ 分类：

1. $r=m=n$：$A$ 可逆，$Ax=b$ 有唯一解。
2. $r=m<n$：$A$ 为矮宽矩阵，$Ax=b$ 有无穷多解。
3. $r=n<m$：$A$ 为高瘦矩阵，$Ax=b$ 无解或有唯一解。
4. $r<m$ 且 $r<n$：$A$ 不满秩，$Ax=b$ 无解或有无穷多解。

## 16. 线性无关

向量 $v_1, v_2, \dots, v_k$ 线性无关，是指满足 $c_1 v_1 + \dots + c_k v_k = 0$ 的系数只能是 $c_1 = \dots = c_k = 0$。
这等价于 $Ax=0$ 只有唯一解 $x=0$。

## 17. 生成空间 (Spanning a Space)

若向量空间中的任意向量都能表示为一组向量的线性组合，则称这组向量**生成**了该空间。

## 18. 行空间 (Row Space)

$m \times n$ 矩阵 $A$ 的行空间是 $\mathbb{R}^n$ 的子空间，由 $A$ 的各行向量生成。
行空间通常记为 $C(A^T)$（即 $A^T$ 的列空间）。

## 19. 向量空间的基 (Basis)

向量空间的**基**是满足以下两个条件的一组向量：

1. **线性无关**。
2. **生成整个空间**。

## 20. 基的性质

* 若一组向量 $v_1, \dots, v_n$ 构成 $n \times n$ 可逆矩阵的列，则它们是 $\mathbb{R}^n$ 的一组基。
* $\mathbb{R}^n$ 中有无穷多组不同的基。

## 21. 矩阵空间的基

* $A$ 的**主元列**是列空间 $C(A)$ 的一组基。
* $A$ 的**主元行**（或者更准确地说是 $R$ 的非零行）是行空间 $C(A^T)$ 的一组基。

## 22. $A$ 与 $R$ 的关系

矩阵 $A$ 与其最简行阶梯形 $R$：

* **列空间不同**。
* **行空间相同**。

## 23. 向量空间的维数

向量空间 $V$ 的维数 $\dim(V)$ 是该空间任一组基中包含的**向量个数**。

## 24. 四个基本子空间

对于 $m \times n$ 矩阵 $A$，秩为 $r$：

1. **行空间 $C(A^T)$**：$\mathbb{R}^n$ 的子空间，维数为 $r$。
2. **列空间 $C(A)$**：$\mathbb{R}^m$ 的子空间，维数为 $r$。
3. **零空间 $N(A)$**：$\mathbb{R}^n$ 的子空间，维数为 $n-r$。
4. **左零空间 $N(A^T)$**：$\mathbb{R}^m$ 的子空间，维数为 $m-r$。

**示例分析：**

$$
R = \begin{bmatrix} 1 & 3 & 5 & 0 & 7 \\ 0 & 0 & 0 & 1 & 2 \\ 0 & 0 & 0 & 0 & 0 \end{bmatrix}
$$

* $m=3, n=5, r=2$。
* 主元行：第 1, 2 行 $\implies \dim C(A^T) = 2$。
* 主元列：第 1, 4 列 $\implies \dim C(A) = 2$。
* 自由列：第 2, 3, 5 列 $\implies$ 3 个特殊解 $\implies \dim N(A) = 5-2=3$。
* 左零空间：$A^T y = 0$，维数为 $m-r = 3-2=1$。

## 25. 维数总结

* $A$ 的列空间维数等于行空间维数，均等于秩 $r$。
* **列秩 = 行秩**。
* 线性无关列的数目 = 线性无关行的数目。
