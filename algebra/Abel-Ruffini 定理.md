[上一篇](https://zhuanlan.zhihu.com/p/2060047607557367643)文章我们讲了 Galois 理论，这篇文章我们讲解 Abel-Ruffini 定理，即五次以及以上的代数方程不存在一般的根式求根公式。
# 前置知识

本篇文章相对较深地依赖了之前对[域](https://zhuanlan.zhihu.com/p/2059701837423497662)和[ Galois 理论](https://zhuanlan.zhihu.com/p/2060047607557367643)的讲解，而关于[群](https://zhuanlan.zhihu.com/p/2012437604285572037)的讲解，主要集中在文章的可解群这一节，主要是可解群的定义，以及 $S_5$ 不可解，这两个单点，知识点相对较浅，如果要看原文，搜索关键词为“可解序列与可解性”，“置换群基础概念回顾”，“五次及以上对称群的不可解性”，看完二级小标题下内容即可。

如果不看原文，我这里给出了它们的简单表述：
可解群的定义：

>**定义（可解群）**
>
>如果群 $G$ 存在一个序列（第一项是 $G$，最后一项是一个仅有单位元的子群）：
>$$G=G_0\rhd G_1\rhd\cdots\rhd G_{k}=\{e\}$$
>满足阶梯型（即对任意 $1\le i\le k$，都有 $G_{i}$ 是 $G_{i-1}$ 的正规子群）和简单性（即对任意 $1\le i\le k$，都有商群 $G_i/G_{i-1}$ 是交换群）。
>
>则称 $G$ 是**可解群**。

对称群的定义：

>**定义（置换和对称群）**
>
>定义 $S_n$ 为 $\{1,2,\cdots,n\}$ 上的全体双射构成的集合，特别地称这种形式的变换为**置换**，同样令$\cdot$ 为置换的复合运算，则任取一部分置换，它与置换的复合运算如果能构成群，则称作**置换群**， $[S_n,\cdot ]$ 则被称为 $n$ 次**对称群**。
>
>在不会引起混淆的前提下，也会直接将 $S_n$ 记作 $n$ 次对称群。

$S_5$ 不可解。

>**定理（五次对称群不可解）**
>
>五次对称群 $S_n$ 不是可解群。

证明见[群论篇](https://zhuanlan.zhihu.com/p/2012437604285572037)。

下面是正文内容。
# 小目录

本篇文章内容较少，主要是三个板块：
- 先单位根扩张和纯扩张：就是开根的时候，我们打算先把本原单位根添加进去，然后再是具体的 $\sqrt[n]a$，也就是我们常见的算数次方根，这样做，我们可以证明这样做 Galois 群的结构是交换群。
- 然后介绍根式扩张：如你所见，所谓开根，我们把它翻译成 $x^n-1$ 在底域的基础上求分裂域，然后，如何证明根式可解则 Galois 群可解呢，毕竟根式扩张不一定是 Galois 扩张？还是老办法，找到一个大 Galois 扩张包含它即可，然后就可以上我们先单位根扩张然后纯扩张的小连招。
- 最后证明 Abel-Ruffini 定理：用一个群论的引理，然后举一个多项式的例子 $x^5-4x+2$，算它分裂域的 Galois 群，算出来是 $S_5$，于是证明了 Abel-Ruffini 定理。

以下是正文内容，单开一篇算是奖励关。

# 单位根扩张和纯扩张

$x^n-a$ 在分裂域上的根，对于一般的 $a$ 可是不对乘法成群的，因此就拆成两个做，即单位根扩张和纯扩张，此处证明难度不高，但一些小定理还是有点意思的。
## 单位根扩张
我们首先证明一系列定理。

>**定理（零特征域下单位根的可分性）**
>
>设 $F$ 是特征为 0 的域， $f(x)=x^n-1\in F[x]$，其中 $n\ge 1$。
>则 $f(x)$ 是可分多项式。

**证明：**

考察 $f(x)$ 的形式导数 $f'(x)=nx^{n-1}$，由于域 $F$ 的特征为 0，$f'(x)$ 非零，且只有 0 是它的根。
而 0 不是 $f(x)$ 的根，因此，由重根判定定理，$f(x)$ 无重根，因此 $f(x)$ 是可分多项式。$\blacksquare$

>**定理（欧拉函数求和等式）**
>
>设 $\varphi(n)$ 为欧拉函数，即 1 到 $n$ 中与 $n$ 互素的数字个数。
>则：
>$$\displaystyle\sum_{d\mid n}\varphi(d)=n$$

**证明：**
考虑 $\dfrac 1n,\dfrac 2n,\cdots,\dfrac nn$ 这 $n$ 个分数的约分，约简后形如 $\dfrac ad$ （其中 $a,d$ 互质，且 $d\mid n$）的数恰有 $\varphi(d)$ 个，因此就有  $\displaystyle\sum_{d\mid n}\varphi(d)=n$。$\blacksquare$

>**定理（域的乘法群的有限子群是循环群）**
>
>设 $E$ 是域，$E^\times=E\setminus\{0\}$ 是其乘法群。
>
>则 $E^\times$ 的任意有限子群 $G$ 是循环群。

**证明：**
设 $G$ 的阶数为 $n$，设 $\psi(d)$ 表示群 $G$ 中阶数为 $d$ 的元素个数。

显然 $\psi(d)$ 有可能为 0，如果 $\psi(d)>0$，考虑取 $G$ 中的一个 $d$ 阶元素 $a\in G$，则生成子群 $\langle a\rangle$ 是 $d$ 阶循环群。

由于乘法群中的 $d$ 阶元素 $g\in G$ 在域 $E$ 中必有 $g^d=1$，根据域上多项式根的个数上限，知该方程在域中至多有 $d$ 个根，而循环群 $\langle a\rangle$ 恰好包含 $d$ 个满足该方程的元素，故域中所有满足 $x^d=1$ 且 $x\in E$ 的元素，从而也包括全体 $d$ 阶元素必然属于 $\langle a\rangle$。

而 $\langle a\rangle$，由循环群的性质，其中有且仅有 $\varphi(d)$ 个 $d$ 阶元。

因此，若 $\psi(d)>0$，则有 $\psi(d)=\varphi(d)$，即总有 $\psi(d)\le\varphi(d)$。

而由于 $n=\displaystyle\sum_{d\mid n}\psi(d)$，即有限群的每个元素都有阶，而由 Lagrange 定理每个元素的阶数只能是群的阶数的因子。

又因为 $\displaystyle\sum_{d\mid n}\varphi(d)=n$，因此，我们就有，对任意 $d\mid n$，都有 $\psi(d)=\varphi(d)$。

因此 $\psi(n)=\varphi(n)> 0$，我们知道了群 $G$ 中至少有一个 $n$ 阶元，即群 $G$ 是循环群。$\blacksquare$

>**定理（单位根扩张的 Galois 群是交换群）**
>
>设 $F$ 是特征为 0 的域， $f(x)=x^n-1\in F[x]$，其中 $n\ge 1$。
>
>若 $E$ 是 $f(x)$ 在 $F$ 上的分裂域。
>
>则 $\text{Gal}(E/F)$ 是交换群。

**证明：**
设 $U$ 为 $f(x)$ 在 $E$ 中的全体根构成的集合，由零特征域下单位根的可分性，$f(x)$ 无重根，因此，$f(x)$ 在 $E$ 中有 $n$ 个互不相同的根，即 $|U|=n$。

任取 $\alpha,\beta\in U$，知道 $(\alpha\beta^{-1})^n=\alpha^n(\beta^n)^{-1}=1$，故 $\alpha\beta^{-1}\in U$，故 $U$ 是 $E^{\times}$ 的有限子群，故 $U$ 是循环群，设 $U$ 的一个生成元为 $\zeta$，则 $U=\{1,\zeta,\zeta^2,\cdots,\zeta^{n-1}\}$。

由分裂域的定义，知 $E=F(\zeta)$。


因此，任取 $\sigma,\tau\in \text{Gal}(E/F)$，由于 $E=F(\zeta)$ 是单扩张，它们的映射方式由它们将 $\zeta$ 映射到哪里唯一确定。

由自同构对根的置换性质，不妨假设 $\sigma(\zeta)=\zeta^a$ 且 $\tau(\zeta)=\zeta^b$，则：
$$(\sigma\tau)(\zeta)=\sigma(\zeta^b)=\sigma(\zeta)^b=\zeta^{ab}$$
$$(\tau\sigma)(\zeta)=\tau(\zeta^a)=\tau(\zeta)^a=\zeta^{ab}$$
因此 $\sigma\tau=\tau\sigma$，即 $\text{Gal}(E/F)$ 是交换群。$\blacksquare$

由此可以定义单位根扩张。

>**定义（本原单位根与单位根扩张）**
>
>设 $F$ 是特征为 0 的域，设 $E$ 是多项式 $x^n-1\in F[x]$ 在 $F$ 上的分裂域。
>
>记 $x^n-1$ 在 $E$ 中的全体 $n$ 个互不相同的根所构成的集合为 $U$，前文已经证明 $U$ 是循环群，我们称其任意一个生成元 $\zeta_n$ 为 $E$ 中的一个**本原 $\boldsymbol n$ 次单位根**。
>
>此外，该分裂域可以直接写成 $E=F(\zeta_n)$，并称 $E$ 为 $F$ 的 $\boldsymbol n$ **阶单位根扩张**。

在上下文表意明确的情况下，$\zeta_n$ 的下标可以省略并写作 $\zeta$。

## 纯扩张

>**定义（纯扩张）**
>
>设 $E$ 是 $F$ 的扩域，若存在 $\alpha\in E$ 使得 $E=F(\alpha)$，且存在正整数 $n$ 满足 $\alpha^n=a\in F\setminus \{0\}$，则称 $E$ 是 $F$ 的一个 $\boldsymbol n$ **阶纯扩张**。

而纯扩张自然也有着我们想要的性质。

>**定理（纯扩张的 Galois 群是循环群）**
>
>设 $F$ 是特征为 0 的域，$E$ 是 $F$ 的 $n$ 阶纯扩张，即存在 $\alpha\in E$ 使得 $E=F(\alpha)$，且存在正整数 $n$ 满足 $\alpha^n=a\in F\setminus \{0\}$。
>
>若 $F$ 包含本原 $n$ 次单位根 $\zeta$，则 $\text{Gal}(E/F)$ 是循环群。

**证明：**
我们知道单位根扩张的 Galois 群是交换群，此时 $x^n-1$ 在 $F$ 上的全体根也构成了循环群，不妨设其中一个生成元为 $\zeta$，且 $U=\{1,\zeta,\zeta^2,\cdots,\zeta^{n-1}\}$，其中 $U\subseteq F$。

由于 $E=F(\alpha)$，任取 $\sigma,\tau\in \text{Gal}(E/F)$，$\sigma$ 的映射方式由 $\sigma(\alpha)$ 的值确定。

由自同构对根的置换性质，可以定义从 $\text{Gal}(E/F)$ 到模 $n$ 加法群的映射 $\Phi:\text{Gal}(E/F)\to \mathbb Z_n$，使得 $\sigma(\alpha)=\zeta^{\Phi(\sigma)}\alpha$。

由于自同构对根的置换性质，该映射是良定义的。

那么，由于 $\zeta\in F$，注意到：
$$\zeta^{\Phi(\sigma\tau)}\alpha=(\sigma\tau)(\alpha)=\sigma(\zeta^{\Phi(\tau)}\alpha)=\zeta^{\Phi(\tau)}\sigma(\alpha)=\zeta^{\Phi(\sigma)+\Phi(\tau)}\alpha$$
其中指数总是对 $n$ 取模，故该映射是群同态。

考虑到 $\ker \Phi$ 内的映射保持 $\alpha$ 不动，即相当于保持 $E$ 整个不动，因此 $\ker\Phi$ 有且仅有一个恒等映射。

因此我们有 $\text{Gal}(E/F)$ 同构于 $\mathbb Z_n$ 的一个子群，即 $\text{Gal}(E/F)$ 是循环群。$\blacksquare$

# 根式扩张

还记得开根嘛？我们这就定义根式扩张，根式扩张可不一定是 Galois 扩张，怎么办呢？我们想到了用一个更大的 Galois 扩张来套它，真是一个好办法呀。

请注意，在文章[域](https://zhuanlan.zhihu.com/p/2059701837423497662)中，为了便利，定义可分多项式为全体不可约因子无重根，如果不习惯这个定义，可以在对应的多项式中，去除重复的因式，效果也是一样的，该约定差异并不会影响整体证明。
## 根式扩张与方程可解性
> **定义（根式扩张）**
> 
> 设 $E$ 是 $F$ 的扩域，若存在一个域的有限序列使得：
> $$F=F_0\subseteq F_1\subseteq \cdots\subseteq F_k=E$$
> 其中对于任意 $1\le i\le k$，都有 $F_i=F_{i-1}(\alpha_i)$，且存在正整数 $n_i$ 使得 ${\alpha_{i}}^{n_i}\in F_{i-1}$，则称 $E$ 是 $F$ 的**根式扩张**，且 $\alpha_1,\alpha_2,\cdots,\alpha_k$ 为扩张序列的生成元。
> 
> 若 $f(x)\in F[x]$ 的分裂域被包含在 $F$ 的某个根式扩张中，则称 $f(x)$ **可用根式求解**。

也许你会疑惑，这样的定义是不是太过宽泛了？这样我们岂不是允许了一些 $\sqrt[3]{-\dfrac 12+\dfrac{\sqrt 3}{2}i}$ 之类的复数开根的奇怪嵌套，是的，出于某些原因，我们仍然把这种开根叫做根式解。
## 根式扩张的分裂域
>**定理（根式扩张的分裂域是根式扩张）**
>
>若 $E$ 是 $F$ 的根式扩张，其一个扩张序列的生成元是 $\alpha_1,\alpha_2,\cdots,\alpha_k$。
>
>设它们在 $F$ 上的极小多项式分别是 $p_1(x),p_2(x),\cdots,p_k(x)$。
>
>再设 $g(x)=\displaystyle\prod_{i=1}^kp_i(x)$ ，令 $L$ 是 $g(x)$ 在 $F$ 上的分裂域。
>
>则 $L$ 是 $F$ 的根式扩张。

**证明：**
根据根式扩张的定义，存在有限序列 $F=F_0\subseteq F_1\subseteq \cdots\subseteq F_k=E$，其中对于任意 $1\le i\le k$，都有 $F_i=F_{i-1}(\alpha_i)$，且存在正整数 $n_i$ 使得 ${\alpha_{i}}^{n_i}\in F_{i-1}$。

由于 $g(x)$ 的所有不可约因子无重根，故 $g(x)$ 是可分多项式，故 $L$ 是 $F$ 的 Galois 扩张。
不妨设 $G=\text{Gal}(L/F)$，由于 $L$ 包含 $p_1(x),p_2(x),\cdots,p_k(x)$ 所有的根，因此有 $E\subseteq L$。

任取 $\sigma\in G$，则仍然有（设 $\sigma(F_i)=\{\sigma(x)\mid x\in F_i\}$）：
$$F=\sigma(F_0)\subseteq \sigma(F_1)\subseteq \cdots\subseteq \sigma(F_k)=\sigma(E)$$
且 $\sigma({\alpha_i})^{n_i}=\sigma({\alpha_i}^{n_i})\in \sigma(F_{i-1})$。

因此，任取 $\sigma\in G$，$\sigma(E)$ 也是 $F$ 的根式扩张。

由于 $G$ 是有限群，不妨设 $G=\{\sigma_1,\sigma_2,\cdots,\sigma_m\}$，其中 $\sigma_1$ 是恒等映射。

此时，不妨设 $E_0=F$，从第 $i$ 轮开始（$i$ 从 $1$ 计数到 $m$）都如下进行扩张：
$$E_{i-1}=F_{i,0}\subseteq F_{i,1}\subseteq \cdots \subseteq F_{i,k}=E_{i}$$
其中对于任意 $1\le j\le k$，$F_{i,j}=F_{i,j-1}(\sigma_i(\alpha_j))$。

由根式扩张的定义，可知 $E_{i}$ 也是 $F$ 的根式扩张。

易知 $E_1=E$，由于 $E_m$ 恰好是 $F$ 和 $g(x)$ 的所有根生成的，故有 $E_m=L$，故可知 $L$ 也是 $F$ 的根式扩张。$\blacksquare$
## 根式可解则 Galois 群可解

> **定理（根式可解则 Galois 群可解）**
> 
> 设 $F$ 为特征为 0 的域，若多项式 $f(x)\in F[x]$ 可用根式求解，则其在 $F$ 上的分裂域 $K$ 的 Galois 群 $\text{Gal}(K/F)$ 是可解群。

**证明：**
由于 $f(x)$ 可用根式解，其分裂域 $K$ 被包含在某个根式扩张 $E$ 中。

由根式扩张的分裂域是根式扩张，存在域 $L$ 满足 $E\subseteq L$，使得 $L$ 是 $F$ 的有限 Galois 扩张，也是根式扩张。

由于 $E\subseteq L$，且 $K\subseteq E$，因此有 $K\subseteq L$。

由于 $L$ 是 $F$ 的根式扩张，存在有限序列：
$$F= L_0\subseteq L_1\subseteq \cdots\subseteq L_s=L$$
其中，对于任意 $1\le i\le s$，有 $L_i=L_{i-1}(\beta_i)$，且存在正整数 $d_i$ 使得 ${\beta_i}^{d_i}\in L_{i-1}$。

设 $n$ 是 $d_1,d_2,\cdots,d_s$ 的最小公倍数，不妨考虑本原 $n$ 次单位根 $\zeta$ 并构造如下序列：
$$F\subseteq F(\zeta)=M_0\subseteq M_1\subseteq \cdots \subseteq M_s=L(\zeta)$$
其中 $M_i=M_{i-1}(\beta_i)$，考虑扩张的性质：

由于 $L$ 是 $F$ 的有限 Galois 扩张，由 Galois 扩张的正规性与可分性，存在 $g(x)\in F[x]$，使得 $L$ 是 $g(x)$ 的分裂域。因此，$g(x)(x^n-1)\in F[x]$ 是 $F[x]$ 上的可分多项式，而 $L(\zeta)$ 就是 $g(x)(x^n-1)$ 的分裂域，故 $L(\zeta)$ 是 $F$ 的 Galois 扩张，记 $G=\text{Gal}(L(\zeta)/F)$。

考虑第一步扩张 $F\subseteq F(\zeta)=M_0$，由 $n$ 阶单位根扩张的性质，$\text{Gal}(M_0/F)$ 是交换群。

而由于 $M_0$ 是 $F$ 的有限 Galois 扩张，由 $L(\zeta)/F$ 的 Galois 对应的正规性定理，$H_0=\text{Aut}(L(\zeta)/M_0)$ 是 $G$ 的正规子群，即 $H_0\trianglelefteq G$，且满足商群同构 $G/H_0\cong \text{Gal}(M_0/F)$。
故 $G/H_0$ 是交换群。

而考虑后续的每一步扩张 $M_{i-1}\subseteq M_{i-1}(\beta_i)=M_i$，由于 ${\beta_i}^{d_i}\in M_{i-1}$，而由于 $d_i\mid n$，知 ${\zeta}^{n/d_i}$ 为 $M_{i-1}$ 的一个本原 $d_i$ 次单位根，故 $M_i$ 是 $M_{i-1}$ 的 $d_i$ 阶纯扩张，故 $\text{Gal}(M_i/M_{i-1})$ 是循环群。

而由于 $M_{i}$ 是 $M_{i-1}$ 的有限 Galois 扩张，由 $L(\zeta)/M_{i-1}$ 的 Galois 对应的正规性定理，$H_i=\text{Aut}(L(\zeta)/M_{i})$ 是 $\text{Aut}(L(\zeta)/M_{i-1})$ 的正规子群，即 $H_i\trianglelefteq H_{i-1}$，且满足商群同构 $H_{i-1}/H_i\cong \text{Gal}(M_i/M_{i-1})$。

故 $H_{i-1}/H_{i}$ 是循环群，因此是交换群。

因此，我们可以构造大群 $G$ 的一条正规子群链：
$$G\rhd H_0\rhd H_1\rhd \cdots \rhd H_s$$
其中依照定义， $H_s=\text{Gal}(L(\zeta)/L(\zeta))$，仅能包含恒等映射。

因此，$G$ 是可解群。

考虑 $\text{Gal}(K/F)$，由于 $K$ 是 $F$ 的 Galois 扩张，由  $L(\zeta)/F$ 的 Galois 对应的正规性定理，知道 $N=\text{Aut}(L(\zeta)/K)$ 是 $G$ 的正规子群，且：
$$\text{Gal}(K/F)\cong G/N$$
则令 $\psi:G\to G/N$ 为自然投影同态，由于同态保持换位子运算，有 $\psi([a,b])=[\psi(a),\psi(b)]$，可以归纳导出对应的可解列，并说明 $G/N$ 也是可解群。

即 $\text{Gal}(K/F)$ 也是可解群。$\blacksquare$ 

# Abel-Ruffini 定理

相应地，如果 $\text{Gal}(K/F)$ 不是可解群，则 $f(x)$ 不可用根式求解，接下来我们只要举出一个具体的例子作为实例即可，在此之前，我们先证明一个小引理。
## 质数对称群的生成元
> **定理（质数对称群的生成元）**
> 
> 设 $S_p$ 是 $p$ 次对称群，其中 $p$ 是质数。
> 
> 若 $S_p$ 存在子群 $G$ 满足，$G$ 包含一个对换 $\tau$ 和一个 $p$-循环置换 $\sigma$。
> 则 $G=S_p$。

**证明：**
由于 $\sigma$ 是一个包含所有元素的循环置换，由于 $p$ 是质数，由初等数论知识，容易证明对任意 $1\le k<p$，$\sigma^k$ 仍然是一个包含所有元素的循环置换。

不妨设对换为 $\tau=(a,b)$，即交换 $a,b$，通过适当取 $k$ 的值，总可以让 $a,b$ 在 $\sigma^k$ 这一循环置换中的位置是相邻的。

故可设 $\tau=(1,2)$，而 $\sigma=(1,2,3,\cdots,p)$。

然后，可归纳证明，$\sigma^k \tau \sigma^{-k}=( k\bmod p+1,(k+1)\bmod p+1)$ ，其中 $0\le k<p$。

因此，$(1,2),(2,3),\cdots,(p-1,p),(p,1)$ 等相邻对换全都在 $G$ 中。

任取一个非相邻的对换 $(a,b)$，我们知道：
$$(a,b)=(b-1,b)(b-2,b-1)\cdots (a+1,a+2)(a,a+1)(a+1,a+2)\cdots (b-2,b-1)(b-1,b)$$
故子群 $G$ 包含了 $S_p$ 中的所有对换。
由于任何一个置换都能分解成有限个对换的乘积，知 $G=S_p$。$\blacksquare$
## Abel-Ruffini 定理
>**定理（Abel-Ruffini 定理）**
>
>五次以及以上的代数方程不存在一般的根式求根公式。
>
>具体而言，五次多项式 $f(x)=x^5-4x+2\in \mathbb Q[x]$ 在 $\mathbb Q$ 上不能用根式求解。

**证明：**
首先证明 $f(x)$ 在 $\mathbb Q[x]$ 上不可约。

注意到 $f(x)\in \mathbb Z[x]$，使用 Eisenstein 判别法。

取质数 $p=2$，2 不整除首项系数 1，整除其余系数 $0,0,0,-4,2$，且 $2^2=4$ 不整除常数项 2。

故 $f(x)$ 在 $\mathbb Q[x]$ 上不可约。

考察 $f(x)$ 的根的情况，注意到 $f'(x)=5x^4-4$，单调性比较简单，令 $f'(x)=0$ 得到两个实极值点 $x=\pm \sqrt[4]{4/5}$。

$f(-\sqrt[4]{4/5})>f(-1)=5>0$，即极大值大于 0，$f(\sqrt[4]{4/5})<f(1)=-1<0$，即极小值小于 0。

故分析单调性即可知 $f(x)$ 在 $\mathbb R$ 上有且仅有 3 个实根，且都是单根。

相对应的，在 $\mathbb C\setminus \mathbb R$ 上有两个复根，考虑复共轭映射 $\tau:z\to \bar{z}$ 知这两个复根共轭。

设 $K\subset \mathbb C$ 是 $f(x)$ 在 $\mathbb Q$ 上的分裂域，设 $f(x)$ 的一个根为 $\alpha$，知 $[K:\mathbb Q]=[K:\mathbb Q(\alpha)]\cdot [\mathbb Q(\alpha):\mathbb Q]$。

由单扩张的维数定理，$[\mathbb Q(\alpha):\mathbb Q]=5$。
由有限 Galois 扩张的等价刻画，$|\text{Gal}(K/\mathbb Q)|$ 是 5 的倍数，不妨设 $G=\text{Gal}(K/\mathbb Q)$。

此时由于自同构对根的置换性质，$G$ 必定同构于 $f(x)$ 的 5 个根的置换群，不妨理解为 $G$ 同构于 $S_5$ 的一个子群 $G'$。

由于 $|G'|$ 是 5 的倍数，由 Cauchy 定理，$G'$ 必定存在一个 5 阶子群，而 5 阶群必定是循环群，取循环群的生成元，知 $G'$ 存在 5 阶元，而由于 $G'\le S_5$，知 $G'$ 中一定有一个 5 阶循环置换。

而考虑复共轭映射 $\tau:z\to\bar z$，$\tau\in G$，由于 $f(x)$ 有两个复根共轭，这说明在 $G'$ 中有一个对换。

因此 $G'=S_5$，即 $\text{Gal}(K/\mathbb Q)\cong S_5$。

由于在群论中，我们已经说明了 $S_5$ 不是可解群，因此 $\text{Gal}(K/\mathbb Q)$ 不是可解群。

因此，$f(x)$ 不可用根式求解。$\blacksquare$ 

因为存在一个具体的五次方程的实例，对于一般的 $n$ 次方程，考虑多项式 $(x-1)^{n-5}(x^5-4x+2)$，可知对 $n$ 次代数方程，不存在一般的根式求根公式。
# 尾声

还记得我们之前吐槽过的复数开根嘛，Cardano 就曾经遇到过 $x = \sqrt[3]{2 + 11i} + \sqrt[3]{2 - 11i}$ 这样的复数开根然后共轭抵消变成实数（甚至是 4）的情况。

但不论如何，出于对称美感的追求，当时的数学家们，比如 Bombelli，顶着这是一种妖术的恶心感，进一步研发高次方程的根式解，从而促成了我们现在的内容，从现在工程实用的角度，为了一个高次方程的根式解，得到一个冗长怪异，而且不可以直接用于数值计算的解是极其不实用的，即使从数学美感的角度，也有上面我们指出的问题。

但历史的巧合就在于此，正是在这些看起来研发动机都令人疑惑的东西之上，长出了一堆极其实用的学科，不得不令人感慨。

我想，很多时候这些回顾的内容，可以改变一个人对世界的观点，也许我们不得不参与这个世界的演进，但不必过于沉迷于它，毕竟，我们也许难以真正清楚，有哪些汲汲的索求，淹没在历史的尘埃，又有哪些无意的坚持，慢慢使世界换了模样。


