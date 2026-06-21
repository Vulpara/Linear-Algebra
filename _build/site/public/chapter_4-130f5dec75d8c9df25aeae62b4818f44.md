---
title: 第4章：正交性
date: 2024-12-04 00:00:00
---

## 1. 向量点积

当两个向量 $\vec{v}$与 $\vec{w}$ 的点积为 $0$，即 $\vec{v} \cdot \vec{w} = \vec{v}^T \vec{w} = 0$ 时，称这两个向量**正交**（垂直）。

## 2. 子空间的正交

同一向量空间中的两个子空间 $V$ 与 $W$ 正交是指：$V$ 中任意向量 $\vec{v}$ 都与 $W$ 中任意向量 $\vec{w}$ 垂直。

$$
\vec{v}^T \vec{w} = 0, \quad \forall \vec{v} \in V, \vec{w} \in W
$$

## 3. 四个基本子空间的正交关系

对于 $m \times n$ 矩阵 $A$，其基本子空间在 $\mathbb{R}^n$ 和 $\mathbb{R}^m$ 中成对正交：

* **在 $\mathbb{R}^n$ 中：** 零空间 $N(A)$ 与行空间 $C(A^T)$ 正交。
    （即 $Ax=0$ 意味着 $x$ 垂直于 $A$ 的每一行）。
* **在 $\mathbb{R}^m$ 中：** 左零空间 $N(A^T)$ 与列空间 $C(A)$ 正交。
    （即 $A^T y=0$ 意味着 $y$ 垂直于 $A$ 的每一列）。

## 4. 正交补 (Orthogonal Complement)

子空间 $V$ 的正交补 $V^\perp$ 是指由所有垂直于 $V$ 的向量构成的子空间。

## 5. 维数关系

对 $m \times n$ 矩阵 $A$（秩为 $r$）：

* 零空间 $N(A)$ 是行空间 $C(A^T)$ 在 $\mathbb{R}^n$ 中的正交补。
    $$
    n = \dim N(A) + \dim C(A^T) = (n-r) + r
    $$
* 左零空间 $N(A^T)$ 是列空间 $C(A)$ 在 $\mathbb{R}^m$ 中的正交补。
    $$
    m = \dim N(A^T) + \dim C(A) = (m-r) + r
    $$

## 6. 投影 (Projection)

将向量 $\vec{b}$ 投影到直线上，投影 $\vec{p}$ 是 $\vec{b}$ 在该直线方向上的分量。
若将 $\vec{b}$ 投影到子空间（如平面）上，投影 $\vec{p}$ 是 $\vec{b}$ 在该子空间上的最近似向量。

$$
\vec{p} = P\vec{b} \quad (P \text{ 为投影矩阵})
$$

## 7. 到直线上的投影

设直线过原点且方向向量为 $\vec{a}$，求向量 $\vec{b}$ 在该直线上的投影 $\vec{p}$。

* 设 $\vec{p} = \hat{x}\vec{a}$ ($\hat{x}$ 为标量系数)。
* 误差向量 $\vec{e} = \vec{b} - \vec{p}$ 应垂直于直线 $\vec{a}$。
    $$
    \vec{a} \cdot \vec{e} = 0 \implies \vec{a}^T (\vec{b} - \hat{x}\vec{a}) = 0
    $$
* 解得系数 $\hat{x}$：
    $$
    \hat{x} = \frac{\vec{a}^T \vec{b}}{\vec{a}^T \vec{a}}
    $$
* **投影向量**：
    $$
    \vec{p} = \hat{x}\vec{a} = \frac{\vec{a}^T \vec{b}}{\vec{a}^T \vec{a}} \vec{a}
    $$
* **投影矩阵** ($P\vec{b} = \vec{p}$)：
    $$
    P = \frac{\vec{a} \vec{a}^T}{\vec{a}^T \vec{a}}
    $$

![线性代数4.7](attachments/4.7.png)

## 8. 到子空间上的投影

问题：求向量 $\vec{b}$ 在由 $\vec{a}_1, \dots, \vec{a}_n$ 生成的子空间上的投影 $\vec{p}$。
这等价于寻找最佳线性组合 $\vec{p} = A\hat{x}$，其中 $A$ 的列为 $\vec{a}_1, \dots, \vec{a}_n$。

误差 $\vec{e} = \vec{b} - \vec{p} = \vec{b} - A\hat{x}$ 必须垂直于子空间的基向量：

$$
\begin{cases} \vec{a}_1^T(\vec{b} - A\hat{x}) = 0 \\ \vdots \\ \vec{a}_n^T(\vec{b} - A\hat{x}) = 0 \end{cases} \implies A^T(\vec{b} - A\hat{x}) = 0
$$

整理得到**正规方程 (Normal Equation)**：

$$
A^T A \hat{x} = A^T \vec{b}
$$

解得 $\hat{x}$ 及投影 $\vec{p}$：

$$
\hat{x} = (A^T A)^{-1} A^T \vec{b}
$$

$$
\vec{p} = A\hat{x} = A(A^T A)^{-1} A^T \vec{b}
$$

## 9. 投影矩阵 $P$

$$
P = A(A^T A)^{-1} A^T
$$

**性质：**

1. **对称性**：$P^T = P$。
2. **幂等性**：$P^2 = P$（投影两次等于投影一次）。
3. **作用**：$P\vec{b} = \vec{p}$。

## 10. 最小二乘估计 (Least Squares)

当方程组 $Ax=b$ 无解（即 $b \notin C(A)$）时，我们寻求使得误差平方和 $E = \|Ax-b\|^2$ 最小的解 $\hat{x}$。
这等价于求解 $A^T A \hat{x} = A^T \vec{b}$。

## 11. 正交矩阵 $Q$ (Orthogonal Matrix)

若向量组 $\vec{q}_1, \vec{q}_2, \dots, \vec{q}_n$ 满足标准正交条件：

$$
\vec{q}_i^T \vec{q}_j = \begin{cases} 0 & i \neq j \text{ (正交)} \\ 1 & i = j \text{ (单位长度)} \end{cases}
$$

令 $Q = [\vec{q}_1 \ \vec{q}_2 \ \dots \ \vec{q}_n]$，则有 $Q^T Q = I$。

* 若 $Q$ 为方阵，则 $Q^T = Q^{-1}$，此时称 $Q$ 为**正交矩阵**。

## 12. 每个置换矩阵都是正交矩阵

置换矩阵 $P$ 的列向量是标准正交的，因此 $P^T = P^{-1}$。

## 13. $Q$ 的性质

正交矩阵（或具有标准正交列的矩阵）保持向量的几何性质：

* **保长**：$\|Qx\| = \|x\|$。
* **保内积**：$(Qx)^T (Qy) = x^T Q^T Q y = x^T y$。

## 14. 利用标准正交基投影

若矩阵 $A$ 的列向量已经是标准正交的（记为 $Q$），则公式大大简化。
因 $Q^T Q = I$，故：

$$
\hat{x} = (Q^T Q)^{-1} Q^T \vec{b} = Q^T \vec{b}
$$

$$
P = Q(Q^T Q)^{-1} Q^T = Q Q^T
$$

$$
\vec{p} = Q Q^T \vec{b}
$$

## 15. 格拉姆-施密特方法 (Gram-Schmidt Process)

将一组线性无关的向量 $\vec{a}, \vec{b}, \vec{c}$ 转化为标准正交向量组 $\vec{q}_1, \vec{q}_2, \vec{q}_3$。

**步骤：**

1. **确定第一个方向 $\vec{A}$：**
    $$
    \vec{A} = \vec{a}
    $$

2. **确定第二个方向 $\vec{B}$（除去 $\vec{b}$ 中在 $\vec{A}$ 方向上的分量）：**
    $$
    \vec{B} = \vec{b} - \frac{\vec{A}^T \vec{b}}{\vec{A}^T \vec{A}} \vec{A}
    $$
    （此时 $\vec{B} \perp \vec{A}$）。

3. **确定第三个方向 $\vec{C}$（除去 $\vec{c}$ 中在 $\vec{A}$ 和 $\vec{B}$ 方向上的分量）：**
    $$
    \vec{C} = \vec{c} - \frac{\vec{A}^T \vec{c}}{\vec{A}^T \vec{A}} \vec{A} - \frac{\vec{B}^T \vec{c}}{\vec{B}^T \vec{B}} \vec{B}
    $$

4. **归一化（单位化）：**
    $$
    \vec{q}_1 = \frac{\vec{A}}{\|\vec{A}\|}, \quad \vec{q}_2 = \frac{\vec{B}}{\|\vec{B}\|}, \quad \vec{q}_3 = \frac{\vec{C}}{\|\vec{C}\|}
    $$
