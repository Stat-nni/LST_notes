# 极限理论笔记
—— Stat_Nni
这篇笔记将汇总极限理论课程中涉及的内容，课程主题如下：
* Modes of convergence
* Lindeberg’s central limit theorem
* Hajek’s projection method
* Rank statistics method
* Convergence of random functions
* Empirical process method
* Other topics : Von Mises differentiablefunctional
## Chapter 1: 收敛模式
### 1.1 依概率收敛
利用Chebychev inequality，我们通常只需要验证$E|X_n-X|^2\rightarrow0$，即可说明$X_n$依概率收敛于$X$.

**常用的不等式有：**
* **Chebychev inequality**
* **Markov inequality**

**Remark:** Suppose $h(y)$ is a continuous function, then $Y_n\rightarrow Y$ in probability implies $h(Y_n) \rightarrow h(Y)$ in probability.

### 1.2 以概率1收敛（几乎处处收敛）
除了我们常见的“几乎处处收敛”的定义之外，这里关于几乎处处收敛的定义如下：
> **几乎处处收敛：**
> We say that the sequence $Y_n$ converges with probability one to the random variable $Y$, and write  $Y_n\rightarrow Y$ a.s., if $\max_{n\leq k}|Y_k-Y|\rightarrow 0$ in probability as $n\rightarrow \infty$.

我们可以自然而然地得到如下结论：
* **几乎处处收敛**可以推出**依概率收敛**
* 对于**单调**序列，**依概率收敛**与**几乎处处收敛等价**

> **Proposition 1.1（Borel-Cantelli lemma）**
> $\sum_{k=1}^\infty P(|Y_k-Y|\geq\epsilon)<\infty$ for each $\epsilon>0$ implies $Y_k\rightarrow Y$ a.s.

**例子（加深理解“依概率收敛”与“几乎处处收敛”的区别）**：$[0,1)$区间，有一个随机变量序列$X_{i,j}$如下，将区间平均划分为$i$份，当$\omega$落入$[\frac{j-1}{2^i},\frac{j}{2^i}]$时，$X_{i,j}$取值为1，其余地方取值为0。然后再按顺序将其命名为$Y_1,Y_2,...$，可知，随机变量序列$Y_n$满足依概率收敛，却不满足几乎处处收敛。

**Remark 1.2:** 依概率收敛的随机变量序列可以找到几乎处处收敛的子列。

> **Proposition 1.2 (几乎处处收敛的等价定义)**
> $Y_n\rightarrow Y$当且仅当$P(\omega:\lim_{n\rightarrow\infty}|Y_n(\omega)-Y(\omega)|=0)=1$.

可知，当我们讨论几乎处处收敛时，说明可以找到一个测度为1的集合$A$，当$\omega\in A$时，可知$Y_n\rightarrow Y$.在之前的例子中，我们可以发现找不到这样的一个集合，所以其并不满足几乎处处收敛的性质（用之前的定义去做也得不到这一性质）。更进一步的，我们知道几乎处处收敛这一性质要比处处收敛（point-wise convergence）更弱。

在我们讨论收敛时，也并不一定要在**欧氏空间**中讨论，只要在**complete separable space**下就可以讨论相关概念。当然，在讨论收敛时，我们都会有相应的“距离”概念来帮助判断收敛。

### 1.3 依分布收敛
> **依分布收敛的定义**
> We say that Yn converges in distribution to $Y$ and write $Y_n  \overset{L}{\rightarrow} Y$ if and only if $F_{Y_n}(y) → F_{Y}(y)$for each $y$ in the continuity set of $F_Y$.
>
所以我们讨论“依分布收敛”时，只需要关注在**极限分布的连续点集**上是否收敛即可，这一点也是非常值得注意的，常常会产生误解。

接下来是十分重要的关于依分布收敛的等价条件：
> **Theorem 1.1** 下列命题是等价的。
> * $Y_n\overset{L}{\rightarrow}Y$.
> * For each bounded and continuous $g$, $Eg(Y_n)\rightarrow Eg(Y)$.
> * For each bounded and uniformly continuous $g$,
$Eg(Yn)\rightarrow Eg(Y)$.

事实上，还可以针对有界且无穷次可微的函数来进行讨论，从而得到依分布收敛，这一条件将在后续进一步讨论。

>**Proposition 1.3**
> * $Y_n\overset{P}{\rightarrow}Y\Rightarrow Y_n\overset{L}{\rightarrow}Y$
> * 当$Y$为一个常数时，其逆命题成立。
>
这个的证明很有意思，命题一要学会利用示性函数进行分解；命题二要注意依分布收敛是在分布函数的连续点上才有收敛性。

**Continuous mapping theorem:**
* 如果$Y_n\overset{L}{\rightarrow}Y$，且$g$为连续函数，则有$g(Y_n)\overset{L}{\rightarrow}g(Y)$.（连续函数的条件可以放松为：**连续点集的测度为1的函数**）

> **Lemma 1.1 (Slutsky lemma)**
>  Suppose $a$ and $b$ are constantsand $A_n\overset{P}{\rightarrow}a$ and $B_n \overset{P}{\rightarrow} b$, and suppose $X_n\overset{L}{\rightarrow}X$. Then $A_nX_n + B_n\overset{L}{\rightarrow}aX + b$. 
> 
> **这个引理相当重要且有意思**, 因为老师每年上课都会讲这个，PPT关于这个引理的证明存在问题，出现了倒果为因的证明方式(PPT没写完，但如果是采用加一项减一项的方式就存在这种问题)，所以需要重新再证明一次。
> 
> **Proof思路:**
> 主要包括三个步骤：
> * 说明$X_n\overset{L}{\rightarrow}X$时，$(X_n,C)\overset{L}{\rightarrow}(X,C)$
> * 说明$X_n\overset{L}{\rightarrow}X$, 且$Y_n\overset{P}{\rightarrow}X_n$时，有$Y_n\overset{L}{\rightarrow}X$
> * 再加上连续映射定理，即可得证。
>
> 第二点说明了虽然**依分布收敛不具有传递性**，但是可通过**依概率收敛**将**依分布收敛**传递出去。
> 
> 其实感觉将常数项的依概率收敛改为依分布收敛仍然成立，因为常数情况下，依分布收敛与依概率收敛等价。

**Example 1.18(进一步阐述了依分布收敛的性质)**
* $Y_n\overset{L}{\rightarrow}Y，a_n\rightarrow a$，那么是否有$$P(Y_n\leq a_n)\rightarrow P(Y\leq a)?$$
答案是不一定的，要看$0$是否是$Y-a$的分布函数的连续点。

**Delta method（Delta方法，很重要）**

该方法有助于我们在已经有了一个非常熟悉的统计量后，去求对其进行变换之后的新统计量的极限分布。

