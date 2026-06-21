---
title: 第7章：快速傅立叶变换
date: 2024-12-30 00:00:00
katex: true
---

## 1. 复向量 $z$ 的长度

$$
\| \vec{z} \| = \sqrt{\bar{z}^T z} = \sqrt{z^H z} = \sqrt{|z_1|^2 + |z_2|^2 + \cdots + |z_n|^2}
$$

其中 $z^H$ 表示 $z$ 的**共轭转置** (Conjugate Transpose)，即 $z^H = \bar{z}^T$。

## 2. 复向量 $u$ 与 $v$ 的内积

$$
u \cdot v = u^H v = \bar{u}^T v = \bar{u}_1 v_1 + \bar{u}_2 v_2 + \cdots + \bar{u}_n v_n
$$

## 3. 正交

若两个复向量的内积为 $0$，即 $u^H v = 0$，则称它们**正交**。

## 4. 共轭转置性质

$$
(AB)^H = B^H A^H
$$

## 5. 埃尔米特矩阵 (Hermitian Matrix) $S$

满足 $S = S^H$（即 $\bar{S}^T = S$）的复矩阵。

**性质：**

1. 任意实对称矩阵都是埃尔米特矩阵。
2. 若 $S=S^H$，则对于任意复向量 $z$，二次型 $z^H S z$ 必为**实数**。
    * 证明：$(z^H S z)^H = z^H S^H (z^H)^H = z^H S z$。一个数等于其共轭，故为实数。
3. 埃尔米特矩阵的**特征值均为实数**。
4. 埃尔米特矩阵对应不同特征值的**特征向量相互正交**。

## 6. 酉矩阵 (Unitary Matrix) $Q$

复数域上的标准正交矩阵，满足：

$$
Q^H Q = I
$$

若 $Q$ 为方阵，则 $Q$ 是酉矩阵，且 $Q^H = Q^{-1}$。

## 7. 单位根与傅里叶矩阵

**单位根 (Roots of Unity)：**
$n$ 次单位根满足 $w^n = 1$。
$$
w_n = e^{i \frac{2\pi}{n}} = \cos\frac{2\pi}{n} + i\sin\frac{2\pi}{n}
$$

![线性代数7.7](attachments/7.7.png)

**$n$ 阶傅里叶矩阵 $F_n$：**
矩阵元素为 $(F_n)_{jk} = w^{jk}$（行列下标从 $0$ 到 $n-1$）。

$$
F_n = \begin{bmatrix} 1 & 1 & 1 & \dots & 1 \\ 1 & w & w^2 & \dots & w^{n-1} \\ 1 & w^2 & w^4 & \dots & w^{2(n-1)} \\ \vdots & \vdots & \vdots & \ddots & \vdots \\ 1 & w^{n-1} & w^{2(n-1)} & \dots & w^{(n-1)^2} \end{bmatrix}
$$

**以 $n=4$ 为例 ($w = i$)：**

$$
F_4 = \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & i & i^2 & i^3 \\ 1 & i^2 & i^4 & i^6 \\ 1 & i^3 & i^6 & i^9 \end{bmatrix} = \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & i & -1 & -i \\ 1 & -1 & 1 & -1 \\ 1 & -i & -1 & i \end{bmatrix}
$$

**性质：**

1. $F_n$ 是对称矩阵 ($F^T = F$)，但不是埃尔米特矩阵。
2. $F_n$ 的列向量正交，模长为 $\sqrt{n}$。
3. **逆矩阵**：
    $$
    F_n^{-1} = \frac{1}{n} F_n^H = \frac{1}{n} \bar{F}_n
    $$

**离散傅里叶变换 (DFT)：**
输入向量 $c$，输出向量 $y = F_n c$。
$$
y_k = \sum_{j=0}^{n-1} w^{kj} c_j
$$

## 8. 快速傅里叶变换 (FFT)

直接计算 $F_n c$ 需要 $n^2$ 次乘法。FFT 利用矩阵分解将复杂度降为 $O(n \log n)$。

**基本思想**：将 $n$ 阶矩阵分解为两个 $n/2$ 阶矩阵。
利用 $w_{2n}^2 = w_n$，将 $F_{2n}$ 的列按偶数和奇数重排：

$$
F_{2n} = \begin{bmatrix} I_n & D_n \\ I_n & -D_n \end{bmatrix} \begin{bmatrix} F_n & 0 \\ 0 & F_n \end{bmatrix} P
$$

* $I_n$：$n$ 阶单位矩阵。
* $D_n$：对角修正矩阵，$D_n = \text{diag}(1, w, w^2, \dots, w^{n-1})$，其中 $w = e^{i 2\pi / 2n}$。
* $P$：置换矩阵，将输入向量的偶数项排在前，奇数项排在后。

**计算量分析：**
设 $T(n)$ 为计算 $n$ 阶变换所需乘法次数。
$$
T(2n) = 2T(n) + n \quad (\text{来自对角矩阵乘法})
$$
递归解得：
$$
T(n) \approx \frac{1}{2} n \log_2 n
$$
对于 $n=1024$，运算量从 $1024^2 \approx 10^6$ 降至 $5 \times 1024 \approx 5000$。
