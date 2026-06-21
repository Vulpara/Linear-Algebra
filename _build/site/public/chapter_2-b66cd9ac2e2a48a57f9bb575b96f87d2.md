---
title: 第2章：线性方程组的求解
date: 2024-11-29 00:00:00
---

## 1. 线性方程组与矩阵形式

$$
\begin{cases} x - 2y = 1 \\ 3x + 2y = 11 \end{cases} \quad \longrightarrow \quad \text{系数矩阵 } A = \begin{bmatrix} 1 & -2 \\ 3 & 2 \end{bmatrix}
$$

矩阵方程 $Ax=b$ 可写作：

$$
\begin{bmatrix} 1 & -2 \\ 3 & 2 \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix} = \begin{bmatrix} 1 \\ 11 \end{bmatrix}
$$

## 2. 线性方程组矩阵形式的理解

对于如下方程组：

$$
Ax=b: \quad \begin{bmatrix} 1 & 2 & 3 \\ 2 & 5 & 2 \\ 6 & -3 & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ z \end{bmatrix} = \begin{bmatrix} 6 \\ 4 \\ 2 \end{bmatrix}
$$

**按列向量理解（逐列相乘）：**

$$
Ax = x\begin{bmatrix} 1 \\ 2 \\ 6 \end{bmatrix} + y\begin{bmatrix} 2 \\ 5 \\ -3 \end{bmatrix} + z\begin{bmatrix} 3 \\ 2 \\ 1 \end{bmatrix} = \begin{bmatrix} 6 \\ 4 \\ 2 \end{bmatrix}
$$

> **核心思想：** 将 $Ax$ 看成矩阵 $A$ 的**列向量的线性组合**。

## 3. 单位矩阵

三阶单位矩阵记为 $I$：

$$
I = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix}
$$

对于任意向量 $x$，满足 $Ix = x$。

## 4. 高斯消元法 (Gaussian Elimination)

消元的目标是将矩阵转化为一个**上三角形矩阵 $U$**。

**示例：**

$$
Ax=b: \quad \begin{bmatrix} 2 & 4 & -2 \\ 4 & 9 & -3 \\ -2 & -3 & 7 \end{bmatrix} \begin{bmatrix} x \\ y \\ z \end{bmatrix} = \begin{bmatrix} 2 \\ 8 \\ 10 \end{bmatrix}
$$

1. **确定第一个主元：** 第1行第1列的元素 $a_{11} = 2$。
2. **消去第1列下方的元素：**
    * 第2行减去第1行的 $2$ 倍（乘数 $l_{21}=2$）。
    * 第3行减去第1行的 $-1$ 倍（乘数 $l_{31}=-1$）。
    * 得到矩阵：
        $$
        \begin{bmatrix} 2 & 4 & -2 \\ 0 & 1 & 1 \\ 0 & 1 & 5 \end{bmatrix} \dots \begin{bmatrix} 2 \\ 4 \\ 12 \end{bmatrix}
        $$
3. **确定第二个主元：** 第2行第2列的元素 $a_{22} = 1$。$a_{22}
4. **消去第2列下方的元素：**
    * 第3行减去第2行的 $1$ 倍（乘数 $l_{32}=1$）。
    * 得到上三角矩阵 $U$：
        $$
        \begin{bmatrix} 2 & 4 & -2 \\ 0 & 1 & 1 \\ 0 & 0 & 4 \end{bmatrix} \dots \begin{bmatrix} 2 \\ 4 \\ 8 \end{bmatrix}
        $$
5. **确定第三个主元：** 第3行第3列的元素 $a_{33} = 4$。

此时方程组化为 $Ux=c$，可通过回代求解。

**消元注意事项：**

* 消元过程中若出现主元为 $0$ 的情况，需**交换行**以获得非零主元。
* 若不存在非零主元可交换，则消元中止（矩阵不可逆）。

**消元矩阵与 $A=LU$ 分解初步：**

将上述步骤中的乘数的相反数按下标填入单位矩阵，可得到初等消元矩阵：

$$
E_{21} = \begin{bmatrix} 1 & 0 & 0 \\ -2 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix}, \quad E_{31} = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 1 & 0 & 1 \end{bmatrix}, \quad E_{32} = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & -1 & 1 \end{bmatrix}
$$

这些矩阵依次左乘 $A$ 得到 $U$：

$$
E_{32} \cdot E_{31} \cdot E_{21} \cdot A = U
$$

## 5. 矩阵乘法

* **可乘条件：** 若 $A$ 为 $m \times n$ 矩阵，则 $B$ 必须为 $n \times p$ 矩阵。乘积 $C = AB$ 为 $m \times p$ 矩阵。
* **基本法则：** $(AB)C = A(BC)$。注意：通常 $AB \neq BA$。

**矩阵乘法的四种理解：**

1. **元素视角（内积）：**
    $AB$ 的第 $i$ 行第 $j$ 列元素 $(AB)_{ij}$ 等于 $A$ 的第 $i$ 行向量与 $B$ 的第 $j$ 列向量的点积。

2. **列视角（左乘各列）：**
    $A$ 左乘 $B$ 的每一列。若 $B = [b_1 \ b_2 \ \dots \ b_p]$，则：
    $$
    AB = A[b_1 \ b_2 \ \dots \ b_p] = [Ab_1 \ Ab_2 \ \dots \ Ab_p]
    $$
    > **※ 结论：** $AB$ 的每一列都是 $A$ 的列向量的线性组合。

3. **行视角（各行左乘）：**
    $A$ 的每一行左乘 $B$。若 $a_i$ 为 $A$ 的第 $i$ 行，则 $AB$ 的第 $i$ 行为 $a_i B$。
    $$
    [1 \ 2 \ 3] \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9 \end{bmatrix} = 1 \cdot [1 \ 2 \ 3] + 2 \cdot [4 \ 5 \ 6] + 3 \cdot [7 \ 8 \ 9] = [30 \ 36 \ 42]
    $$
    > **※ 结论：** $AB$ 的每一行都是 $B$ 的行向量的线性组合。

4. **列乘以行（外积求和）：**
    $$
    AB = (\text{第1列})(\text{第1行}) + (\text{第2列})(\text{第2行}) + \dots + (\text{第n列})(\text{第n行})
    $$
    **示例：**
    $$
    \begin{bmatrix} a & b \\ c & d \end{bmatrix} \begin{bmatrix} E & F \\ G & H \end{bmatrix} = \begin{bmatrix} a \\ c \end{bmatrix} \begin{bmatrix} E & F \end{bmatrix} + \begin{bmatrix} b \\ d \end{bmatrix} \begin{bmatrix} G & H \end{bmatrix}
    $$
    $$
    = \begin{bmatrix} aE & aF \\ cE & cF \end{bmatrix} + \begin{bmatrix} bG & bH \\ dG & dH \end{bmatrix}
    $$

## 6. 置换矩阵 (Permutation Matrix)

置换矩阵 $P$ 用于交换矩阵的行。例如 $P_{23}$ 交换第2行与第3行：

$$
P_{23} = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 0 & 1 \\ 0 & 1 & 0 \end{bmatrix}
$$

左乘作用于行交换：

$$
P_{23} \cdot A = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 0 & 1 \\ 0 & 1 & 0 \end{bmatrix} \begin{bmatrix} 2 & 4 & 1 \\ 0 & 0 & 3 \\ 0 & 6 & 5 \end{bmatrix} = \begin{bmatrix} 2 & 4 & 1 \\ 0 & 6 & 5 \\ 0 & 0 & 3 \end{bmatrix}
$$

## 7. 增广矩阵 (Augmented Matrix)

求解 $Ax=b$ 时，将向量 $b$ 拼接在 $A$ 的右侧：

$$
[A \ b] = \begin{bmatrix} 2 & 4 & -2 & 2 \\ 4 & 9 & -3 & 8 \\ -2 & -3 & 7 & 10 \end{bmatrix}
$$

## 8. 逆矩阵 (Inverse Matrix)

* **前提：** $A$ 必须为方阵。
* **可逆条件：** 行列式 $\det A \neq 0 \iff$ $A$ 有 $n$ 个主元 $\iff$ $A$ 的列向量线性无关。
* **定义：** 若 $A$ 可逆，则存在唯一矩阵 $A^{-1}$ 使得 $A A^{-1} = I$ 且 $A^{-1} A = I$。
* **性质：**
    1. 若存在非零向量 $x$ 使 $Ax=0$，则 $A$ 不可逆。
    2. $(AB)^{-1} = B^{-1} A^{-1}$ (**逆序相乘**)。
    3. $Ax=b$ 的唯一解为 $x = A^{-1}b$。
    4. 对角矩阵（对角元非零）可逆，其逆矩阵为对角元取倒数。

* **计算方法 (Gauss-Jordan 消元)：**
    构造增广矩阵 $[K \ I]$，利用行变换将其化为 $[I \ K^{-1}]$。

    **示例：**
    $$
    [K \ I] = \left[ \begin{array}{ccc|ccc} 2 & -1 & 0 & 1 & 0 & 0 \\ -1 & 2 & -1 & 0 & 1 & 0 \\ 0 & -1 & 2 & 0 & 0 & 1 \end{array} \right]
    $$
    消元变为上三角形式：
    $$
    \xrightarrow{\text{消元}} \left[ \begin{array}{ccc|ccc} 2 & -1 & 0 & 1 & 0 & 0 \\ 0 & \frac{3}{2} & -1 & \frac{1}{2} & 1 & 0 \\ 0 & 0 & \frac{4}{3} & \frac{1}{3} & \frac{2}{3} & 1 \end{array} \right]
    $$
    向上回代并单位化：
    $$
    \xrightarrow{\text{向上回代}} \left[ \begin{array}{ccc|ccc} 1 & 0 & 0 & \frac{3}{4} & \frac{1}{2} & \frac{1}{4} \\ 0 & 1 & 0 & \frac{1}{2} & 1 & \frac{1}{2} \\ 0 & 0 & 1 & \frac{1}{4} & \frac{1}{2} & \frac{3}{4} \end{array} \right] = [I \ K^{-1}]
    $$

## 9. $A=LU$ 分解

任何可逆矩阵 $A$（在不需行交换的情况下）均可分解为下三角矩阵 $L$ 和上三角矩阵 $U$ 的乘积。

回顾第4节的例子：$E_{32} E_{31} E_{21} A = U$。
因为 $E_{ij}$ 可逆，则：
$$
A = (E_{21}^{-1} E_{31}^{-1} E_{32}^{-1}) U = LU
$$

$$
\begin{bmatrix} 2 & 4 & -2 \\ 4 & 9 & -3 \\ -2 & -3 & 7 \end{bmatrix} = \underbrace{\begin{bmatrix} 1 & 0 & 0 \\ 2 & 1 & 0 \\ -1 & 1 & 1 \end{bmatrix}}_{L} \underbrace{\begin{bmatrix} 2 & 4 & -2 \\ 0 & 1 & 1 \\ 0 & 0 & 4 \end{bmatrix}}_{U}
$$

> **观察 $L$：** $L$ 的主对角线元素全为 $1$，下三角部分的元素正是消元过程中使用的**乘数**（$l_{21}=2, l_{31}=-1, l_{32}=1$）。

## 10. 转置 (Transpose)

矩阵 $A$ 的转置记为 $A^T$，定义为：
$$
A^T_{ij} = A_{ji}
$$
即 $A^T$ 的第 $i$ 行是 $A$ 的第 $i$ 列。

* **性质：**
  * $(A+B)^T = A^T + B^T$
  * $(AB)^T = B^T A^T$ （**逆序转置**）
  * $(A^{-1})^T = (A^T)^{-1}$
* **对称矩阵 (Symmetric Matrix)：** 满足 $A^T = A$ 的矩阵。
* **置换矩阵性质：** $P^{-1} = P^T$。
