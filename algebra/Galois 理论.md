[上一篇](https://zhuanlan.zhihu.com/p/2059701837423497662)我们讲了域的基础知识，这一篇我们讲 Galois 理论。
## 前置知识

这篇在进行代数基本定理的证明时，需要引用[群论篇](https://zhuanlan.zhihu.com/p/2012437604285572037)中 Sylow 第一定理的内容，具体而言，如果你想在我的文章中看证明的话，有两条路径：
- 点开文章，搜索“Sylow 第一定理”和“Sylow 第一定理的推论”，你可以看到两个比较正规的，基于群作用的证明。
- 点开文章，搜索“Frobenius 定理”，你可以看到一个对前文依赖关系更少，主要基于群作用，证明思路简短且更加巧妙，并且证明的结论也比前两个词条下的证明要强的证明，在不打算看完群论篇全文的情况下，看这个也许更好。
当然如果你懒得看证明，也可以直接看 Sylow 第一定理的表述。

>**定理（Sylow 第一定理及其推论）**
>
>若有限群 $G$ 的阶数为 $n$ 且 $p$ 是质数。
>
>如果整数 $k$ 使得 $p^k\mid n$，则 $G$ 必存在一个子群 $H$，满足其阶数为 $p^k$。

证明见[群论篇](https://zhuanlan.zhihu.com/p/2012437604285572037)。

下面是小目录。
## 小目录

本篇文章内容较为连贯，分为 5 个板块：
- 第一步是建立群与域的双向通道，即自同构群与固定域的映射：想象一下，你在一座桥上，向左走是保持子域不动的大域自同构群，你看了看桥，桥说保持子域不动的大域自同构只能在根与根之间置换，你向又看，右边是自同构群作用下保持不动的元素集合，也就是固定域。
- 第二步是进行映射的定量分析：自同构的个数不能超过域的扩张次数，引入简单线性代数工具，证明 Artin 固定域定理，也是定量的关系。
- 第三步是在刻画 Galois 扩张：我们借由 Artin 固定域定理，将其定为，映射时的定量关系比较好，即取到前面定量分析的界限，则为 Galois 扩张，然后我们说它好在哪，它好就好在它基本上是一个可分多项式的分裂域呀。
- 第四步证明 Galois 基本定理，简单而言，刻画 Galois 对应，并证明它拥有很好的性质，比如反序包含，数量关系，当然，还有至关重要的正规性质。
- 第五步就是证明代数基本定理，我们用两个初等的分析性质，证明代数基本定理，体现一下 Galois 理论的强大之处。

下面是正文。
# 自同构与固定域的映射

本部分定义较多，定理辅助于定义，难度较低。
## 域的自同构群
> **定义（域的自同构和自同构群）**
> 
> 设 $E$ 是一个域，若映射 $\sigma:E\to E$ 是双射环同态，则称 $\sigma$ 是 $E$ 的一个**自同构**。
>  $E$ 的全体自同构构成的集合关于映射的复合运算构成群，记作 $\text{Aut}(E)$，即 $E$ 的**自同构群**。

在扩域的语境下，我们通常关心的是保持子域不动的自同构，这个名字可能有点长，你也许会好奇为什么不取一个短名字，我也好奇：

> **定义（保持子域固定的自同构群）**
> 
> 设 $E$ 是 $F$ 的扩域。若自同构 $\sigma\in \text{Aut}(E)$ 使得对于任意 $a\in F$，总有 $\sigma(a)=a$，则称 $\sigma$ 保持 $F$ **逐点固定**。
> 全体保持 $F$ 固定的 $E$ 的自同构组成的集合记作 $\text{Aut}(E/F)$。

显然，保持子域固定的自同构群是子群。

>**定理（保持子域固定的自同构群是子群）**
>
>设 $E$ 是 $F$ 的扩域，则 $\text{Aut}(E/F)$ 是 $\text{Aut}(E)$ 的子群。

**证明：**
恒等映射属于 $\text{Aut}(E/F)$，因此 $\text{Aut}(E/F)$ 非空。
任取 $\sigma,\tau\in \text{Aut}(E/F)$，对任意 $a\in F$。
总有 $\sigma(a)=\tau(a)=a$。
因此，$\tau^{-1}(a)=a$，因此 $(\sigma\tau^{-1})(a)=a$，故 $\sigma\tau^{-1}\in \text{Aut}(E/F)$。$\blacksquare$

我们之所以如此关心保持子域不动的自同构，是因为它对多项式的根的作用很特别。
## 自同构对多项式根的作用
自同构只能把多项式的一个根映射到该多项式的另一个根上，具体而言：
>**定理（自同构对根的置换性质）**
>
>设 $E$ 是 $F$ 的扩域，任取 $f(x)\in F[x]$。
>若 $\alpha\in E$ 是 $f(x)$ 的一个根，则对于任意 $\sigma\in \text{Aut}(E/F)$，则 $\sigma(\alpha)$ 也是 $f(x)$ 的一个根。

**证明：**
设 $f(x) = \displaystyle\sum_{i=0}^n c_i x^i$，其中 $c_i\in F$ ，则 $\displaystyle\sum_{i=0}^n c_i \alpha^i = 0$。
在等式两边施加自同构：
$$\sigma\left( \displaystyle\sum_{i=0}^n c_i \alpha^i \right) = \sigma(0) = 0$$
而自同构保持加法和乘法，故有 $\sigma\left( \displaystyle\sum_{i=0}^n c_i \alpha^i \right) =\displaystyle \sum_{i=0}^n \sigma(c_i) \sigma(\alpha)^i=\displaystyle \sum_{i=0}^n c_i\sigma(\alpha)^i=f(\sigma(\alpha))$。
代入就得到 $f(\sigma(\alpha))=0$，即 $\sigma(\alpha)$ 是 $f(x)$ 的一个根。$\blacksquare$

## 固定域
群可以作用于域，而群作用下保持不动的元素集合则是一个子域。
>**定义（固定域）**
>
>设 $E$ 是域，$H$ 是 $\text{Aut}(E)$ 的一个子群。
>定义 $H$ 在 $E$ 中的**固定域**为在 $H$ 的所有自同构作用下均不变的元素集合，记作 $E^H$，具体而言：
>$$E^H=\{x\in E\mid \forall\sigma\in H,\sigma(x)=x\}$$

很自然地，固定域也是子域。
>**定理（固定域是子域）**
>
>设 $E$ 是域，$H$ 是 $\text{Aut}(E)$ 的一个子群，则固定域 $E^H$ 是 $E$ 的子域。

**证明：**

在域的分析中，自同构映射总是保持零元和幺元不动，故 $\sigma(1_E)=1_E,\sigma(0_E)=0_E$ 对任意 $\sigma\in H$ 都成立，因此 $E^H$ 非空。

任取 $x,y\in E^H$，故 $\sigma(x-y)=\sigma(x)-\sigma(y)=x-y$ 故 $x-y\in E^H$ 。

任取 $x,y\in E^H$，且 $y\ne 0_E$，由于自同构映射保持乘法逆元，总有 $\sigma(y^{-1})=\sigma(y)^{-1}$，故 $\sigma(xy^{-1})=\sigma(x)\sigma(y^{-1})=\sigma(x)\sigma(y)^{-1}=xy^{-1}$。

故 $xy^{-1}\in E^{H}$。故由子域的定义，$E^H$ 是 $E$ 的子域。$\blacksquare$

# 映射的定量分析

本部分证明较为优美，自同构群的上界的证明，其核心思想是对映射的定义域进行限制，并以此为依据进行集合划分，从而实现计数。
而 Artin 固定域定理则采用了经典的无穷递降的思想，假设存在一个最小元，通过更小元不存在，来强制满足一些性质。
## 自同构群的上界
我们考虑定义一个更宽泛的映射集合。
> **定义（域的嵌入映射集合）**
> 
> 设 $E$ 是 $F$ 的扩域，且 $L$ 是包含 $F$ 的任何一个域。
> 定义从 $E$ 到 $L$ 且保持 $F$ 逐点固定的全体单射环同态组成的集合为 $\text{Hom}_F(E,L)$。
> 显然有 $\text{Aut}(E/F)\subseteq \text{Hom}_F(E,E)$。

那么，嵌入映射数量的上界是自同构群大小的上界。

> **定理（嵌入映射数量的上界）**
> 
> 设 $E$ 是 $F$ 的有限扩张，且 $L$ 是包含 $F$ 的任何一个域，则 $\text{Hom}_F(E,L)$ 是有限集：
> $$|\text{Hom}_F(E,L)|\le [E:F]$$
> 因此，必有 $|\text{Aut}(E/F)|\le [E:F]$

由于 $E$ 是 $F$ 的有限扩张，可设 $E=F(\alpha_1,\alpha_2,\cdots,\alpha_k)$。
对 $k$ 使用归纳法。

**基础步骤**，当 $k=0$ 时，$E=F$，$[E:F]=1$，此时 $\text{Hom}_F(E,L)$ 中，有且仅有一个自然的包含映射，满足条件。

**归纳假设**对于所有由少于 $k$ 个元素生成的有限扩张，定理均成立。

**递推步骤**设 $K=F(\alpha_1,\alpha_2,\cdots,\alpha_{k-1})$，由归纳假设，$|\text{Hom}_F(K,L)|\le [K:F]$。
设这些同态映射为 $\text{Hom}_F(K,L)=\{\tau_1,\tau_2,\cdots,\tau_m\}$，其中 $m\le [K:F]$。
考虑对集合 $\text{Hom}_F(E,L)$ 进行划分，将其划分成 $S_1,S_2,\cdots, S_m$，使得：
$$S_i=\{\sigma\in \text{Hom}_F(E,L)\mid \forall x\in K,\sigma(x)=\tau_i(x)\}$$
由于对于任意 $\sigma\in \text{Hom}_F(E,L)$，将其定义域限制在 $K$ 以内了之后，自然属于 $\text{Hom}_F(K,L)$，因此，这样的划分不重不漏，故有：
$$|\text{Hom}_F(E,L)|=\displaystyle\sum_{i=1}^m |S_i|$$
考虑 $S_i$ 的大小，注意到 $E=K(\alpha_k)$ 是 $K$ 的单扩张，设 $\alpha_k$ 在 $K$ 上的极小多项式 $p(x)$ 。
根据单扩张的维数定理，$p(x)$ 次数为 $d=[E:K]$，不妨设 $p(x)=\displaystyle\sum_{j=0}^{d} c_j{x} ^j$，其中 $c_d=1_E$。
且任一元素 $\chi\in E$ 均可表示成$\chi=\displaystyle\sum_{j=0}^{d-1} b_j{\alpha_k} ^j$，其中 $b_j\in K$。
任取 $\sigma\in S_i$，则必有 $\sigma(\chi)=\displaystyle\sum_{j=0}^{d-1}\tau_i(b_j)\sigma(\alpha_k)^j$，即 $S_i$ 确定时， $\sigma(\alpha_k)$ 的取值唯一确定了 $\sigma$ 的映射方式。

注意到 $p(\alpha_k)=0_E$，同时施加 $\sigma$，即得到 $0_L=\displaystyle\sum_{j=0}^{d} \tau_i(c_j){\sigma(\alpha_k)} ^j$，其中 $\tau_i(c_d)=1_L$，它的次数仍然是 $d$ 次，因此，考虑多项式 $p_i(x)=\displaystyle\sum_{j=0}^{d} \tau_i(c_j){x} ^j$，由域中多项式根的个数上限，它在 $L$ 中至多有 $d$ 个根。
因此，$|S_i|\le d=[E:K]$。

因此：
$$|\text{Hom}_F(E,L)|=\displaystyle\sum_{i=1}^m |S_i|\le d\cdot m=[E:K]\cdot [K:F]$$
由扩域的塔定理，即有 $|\text{Hom}_F(E,L)|\le [E:F]$。$\blacksquare$

那么也就有 $|\text{Aut}(E/F)|\le [E:F]$

## 齐次线性方程组的非零解定理

> **定理（齐次线性方程组的非零解定理）**
> 
> 设 $F$ 是一个域，考虑如下包含 $m$ 个方程 $n$ 个未知数的齐次线性方程组：
> $$   \begin{cases}  a_{1,1} x_1 + a_{1,2} x_2 + \dots + a_{1,n} x_n = 0 \\  a_{2,1}x_1 + a_{2,2} x_2 + \dots + a_{2,n} x_n = 0 \\  \quad \vdots \\  a_{m,1} x_1 + a_{m,2} x_2 + \dots + a_{m,n} x_n = 0  \end{cases}$$
> 其中，系数 $a_{i,j}\in F$，若未知数个数严格大于方程个数，即 $n>m$，则该方程组在 $F$ 中一定存在一组不全为零的解 $\begin{pmatrix}x_1&x_2&\cdots&x_n\end{pmatrix}\ne\begin{pmatrix}0&0&\cdots&0\end{pmatrix}$。

**证明：**

考虑域 $F$ 上全体 $m$ 维向量组成的空间 $F^m$，由维数的定义，可以取一组基：
$$e_1=\begin{pmatrix}1&0&\cdots&0\end{pmatrix}^T,e_2=\begin{pmatrix}0&1&\cdots&0\end{pmatrix}^T,\cdots,e_m=\begin{pmatrix}0&0&\cdots&1\end{pmatrix}^T$$
由此可知，$\dim_F(F^m)=m$。

将方程的系数写成 $n$ 个 $F^m$ 中的列向量：
$$\alpha_1=\begin{pmatrix}a_{1,1}&a_{2,1}&\cdots&a_{m,1}\end{pmatrix}^T,\alpha_2=\begin{pmatrix}a_{1,2}&a_{2,2}&\cdots&a_{m,2}\end{pmatrix}^T,\cdots,\alpha_n=\begin{pmatrix}a_{1,n}&a_{2,n}&\cdots&a_{m,n}\end{pmatrix}^T$$
由 Steinitz 替换引理，线性无关集的元素个数不超过基的元素个数，因此，这 $n$ 个向量在 $F$ 上线性相关。

由线性相关的定义，必定存在一组不全为 0 的标量 $x_1,x_2,\cdots,x_n$，使得它们的线性组合为零向量。
而这组不全为零的标量即为线性方程组的非零解。$\blacksquare$
## Artin 固定域定理
>**定理（Artin 固定域定理）**
>
>设域 $E$ 的自同构群 $\text{Aut}(E)$ 的一个有限子群为 $G$，且 $F=E^G$ 为 $G$ 在 $E$ 中的固定域。
>
>则 $E$ 是 $F$ 的有限扩张，且扩张次数等于 $G$ 的阶数。
>$$[E:E^G]=|G|$$
>并且，保持 $F$ 逐点固定的全体自同构群就是 $G$，即 $G=\text{Aut}(E/E^G)$。

**证明：**

不妨设 $|G|=n$。

**先证明 $\boldsymbol{[E:F]\le n}$**，根据扩张次数的定义，只需证明，如果 $m>n$，任取 $E$ 中的 $m$ 个元素 $\alpha_1,\alpha_2,\cdots,\alpha_m$，它们在域 $F$ 上线性相关。

利用群 $G$ 的 $n$ 个自同构，构造如下域 $E$ 上的线性方程组，其中，由于恒等映射总是在 $G$ 中，不妨假定 $\sigma_1$ 是恒等映射：
$$\begin{cases}
\sigma_1(\alpha_1) x_1 + \sigma_1(\alpha_2) x_2 + \dots + \sigma_1(\alpha_m) x_m = 0 \\
\sigma_2(\alpha_1) x_1 + \sigma_2(\alpha_2) x_2 + \dots + \sigma_2(\alpha_m) x_m = 0 \\
\quad \vdots \\
\sigma_n(\alpha_1) x_1 + \sigma_n(\alpha_2) x_2 + \dots + \sigma_n(\alpha_m) x_m = 0
\end{cases}$$
由于 $m>n$，由齐次线性方程组的非零解定理，存在非零解 $\begin{pmatrix}x_1&x_2&\cdots&x_m\end{pmatrix}\in E^m$。
但这还不足以说明 $\alpha_1,\alpha_2,\cdots,\alpha_m$ 在域 $F$ 上线性相关，因为线性方程组在 $E$ 上。

考虑从全体非零解中取非零坐标数最少的一组解，假设非零坐标有 $r$ 个，并通过重排 $\alpha_1,\alpha_2,\cdots,\alpha_m$ 使得前 $r$ 个坐标非零，其他坐标为 0，即 $\begin{pmatrix}x_1&x_2&\cdots&x_r&0&\cdots&0\end{pmatrix}\in E^m$，由于方程组齐次，可设 $y_i={x_r}^{-1}x_i$，可得 $\begin{pmatrix}y_1&y_2&\cdots&y_{r-1}&1&0&\cdots&0\end{pmatrix}\in E^m$ 也是齐次方程组的一组非零解。

有两种情况：

第一种情况，存在 $u$ 使得 $y_u\notin F$，由于 $F=E^G$，由 $E^G$ 的定义，此时必定存在 $k$ 使得 $\sigma_k(y_u)\ne y_u$，不妨将 $\sigma_k$ 代入等式，对于第 $i$ 个方程，有 $\displaystyle\sum_{j=1}^{r-1}\sigma_k(\sigma_i(\alpha_j))\sigma_k(y_j)+\sigma_k(\sigma_i(\alpha_r))=0$。
由群的性质，$\sigma_k\sigma_i$ 复合在 $i$ 从 1 到 $n$ 取遍时，恰好也取遍 $\sigma_1,\sigma_2,\cdots,\sigma_n$。
因此，$\begin{pmatrix}\sigma_k(y_1)&\sigma_k(y_2)&\cdots&\sigma_k(y_{r-1})&1&0&\cdots&0\end{pmatrix}\in E^m$ 也是该线性齐次方程组的一组非零解。
因此，$\begin{pmatrix}y_1-\sigma_k(y_1)&y_2-\sigma_k(y_2)&\cdots&y_{r-1}-\sigma_k(y_{r-1})&0&0&\cdots&0\end{pmatrix}\in E^m$，由于 $y_u-\sigma_k(y_u)\ne 0$，也是该线性方程组的一组非零坐标数更少的非零解。
由于这个推导与 $\begin{pmatrix}x_1&x_2&\cdots&x_r&0&\cdots&0\end{pmatrix}\in E^m$ 是非零坐标数最少的一组解矛盾，因此第一种情况实际上不可能发生。

因此，第二种情况，只可能是，对任意 $u$，都有 $y_u\in F$，由于 $\sigma_1$ 是恒等映射，立刻有 $\displaystyle\sum_{i=1}^{r-1}\alpha_iy_i+\alpha_r=0$。这足以说明 $\alpha_1,\alpha_2,\cdots,\alpha_m$ 在域 $F$ 上线性相关。也就足以说明 $[E:F]\le n$。

**再证明 $\boldsymbol{[E:F]= n}$**，由于嵌入映射数量上界的推论，我们有自同构群数量的上界 $|\text{Aut}(E/F)|\le [E:F]$。

而由于群 $G$ 的每一个自同构都保持了 $F$ 的逐点固定，必有 $G\subseteq \text{Aut}(E/F)$。

从基数上，我们就有 $n=|G|\le |\text{Aut}(E/F)|\le [E:F]\le n$，注意到不等式链的开头和结尾都相等。
因此，从基数上，我们就有 $|G|=|\text{Aut}(E/F)|=[E:F]=n$。

而又因为 $G\subseteq \text{Aut}(E/F)$，因此就有 $G=\text{Aut}(E/F)$。$\blacksquare$

# Galois 扩张的刻画

本部分证明大部分不长，而“可分多项式的分裂域必为 Galois 扩张”一节中，较长的证明沿用“自同构群的上界”的证明思路，对自同构群进行划分，从而推导定量关系。

此外，在上一篇[域](https://zhuanlan.zhihu.com/p/2059701837423497662)中，为了便利，定义可分多项式为全体不可约因子无重根，如果不习惯这个定义，可以在对应的多项式中，去除重复的因式，效果也是一样的，该约定差异并不会影响整体证明。
## Galois 扩张和 Galois 群

> **定义（Galois 扩张和 Galois 群）**
> 
> 设 $E$ 是 $F$ 的代数扩张，若保持 $F$ 固定的自同构群的固定域恰好为 $F$ 本身：
> $$E^{\text{Aut}(E/F)}=F$$
> 则称 $E$ 是 $F$ 的 **Galois 扩张**。
> 
> 为了表示敬佩，自同构群 $\text{Aut}(E/F)$ 被正式称为 $E$ 在 $F$ 上的 **Galois 群**，记作 $\text{Gal}(E/F)$ 。

当然，出于某些原因我们会使用更加简洁的刻画。

> **定义（有限 Galois 扩张的等价刻画）**
> 
> 设 $E$ 是 $F$ 的有限扩张，则 $E$ 是 $F$ 的 Galois 扩张等价于保持 $F$ 固定的自同构数恰好等于扩张次数，即 $|\text{Aut}(E/F)|=[E:F]$。

**证明：**

不妨设 $G=\text{Aut}(E/F)$。

如果 $E$ 是 $F$ 的 Galois 扩张，则 $E^G=F$，由 Artin 固定域定理有 $[E:F]=|\text{Aut}(E/F)|=|G|$。

而如果 $|G|=[E:F]$，根据固定域的定义，显然有包含关系 $F\subseteq E^G$，由 Artin 固定域定理有 $[E:E^G]=|G|$，可是又有 $[E:F]=|G|$，由扩域的塔定理有 $[E:F]=[E:E^G]\cdot [E^G:F]$。
故可知 $[E^G:F]=1$，即 $F=E^G$。$\blacksquare$
这个等价刻画有的时候可能好用一点。
## 分裂域与 Galois 扩张

那么什么样的域扩张能保证这个苛刻的条件成立呢？

> **定理（可分多项式的分裂域必为 Galois 扩张）**
> 
> 设 $E$ 是可分多项式 $f(x)\in F[x]$ 在 $F$ 上的分裂域。
> 则 $|\text{Aut}(E/F)|=[E:F]$，即 $E$ 是 $F$ 的有限 Galois 扩张。

**证明：**

设 $[E:F]=n$，对 $n$ 使用归纳法。

**基础步骤**，当 $n=1$ 时，此时 $E=F$，自同构群 $\text{Aut}(E/F)$ 仅包含恒等映射，大小为 1，结论成立。

**归纳假设**，对于所有扩张次数小于 $n$ 的可分多项式的分裂域，定理均成立。

**递推步骤**，假设 $[E:F]=n$，且 $n>1$，那么，$f(x)$ 在 $F[x]$ 中一定包含一个次数大于 1 的不可约多项式 $p(x)$。
由于 $f(x)$ 是可分多项式，则 $p(x)$ 也是可分多项式，设 $p(x)$ 的次数为 $d$，则记 $p(x)$ 在 $E$ 中的根为 $\alpha_1,\alpha_2,\cdots,\alpha_d$ ，它们两两不同。
不妨设 $\alpha=\alpha_1$，则考虑单扩张 $F(\alpha)$，根据单扩张的维数定理，必有 $[F(\alpha):F]=d$。

考虑对 $\text{Aut}(E/F)$ 进行划分，划分为 $d$ 个不相交集合 $S_1,S_2,\cdots,S_d$，使得：
$$S_i=\{\sigma \in \text{Aut}(E/F)\mid \sigma(\alpha)=\alpha_i\}$$
根据自同构对根的置换性质定理，任意 $\sigma\in\text{Aut}(E/F)$ 必定会将 $p(x)$ 的根 $\alpha$ 映射到 $p(x)$ 的某个根，而 $\alpha_1,\alpha_2,\cdots,\alpha_d$ 就是 $p(x)$ 在 $E$ 中的全体互不相同的根，故 $\sigma(\alpha)$ 必然属于且仅属于其中的一个集合。 
因此，这样的划分不重不漏，因此：
$$|\text{Aut}(E/F)|=\displaystyle\sum_{i=1}^d|S_i|$$
首先说明每个 $S_i$ 非空，考虑子域 $F(\alpha)$ 和$F(\alpha_i)$，由单扩张的同构延拓，知存在环同构映射 $\tau:F(\alpha)\to F(\alpha_i)$，使得对任意 $b\in F$ 有 $\tau(b)=b$，而且有 $\tau(\alpha)=\alpha_i$，而对于多项式 $f(x)$，知 $E$ 是 $f(x)$ 在 $F(\alpha)$ 上的分裂域，且 $E$ 是 $f(x)$ 在 $F(\alpha_i)$ 上的分裂域。

根据分裂域的唯一性定理，必定存在 $\sigma_i:E\to E$，满足 $\sigma_i$ 保持 $F$ 逐点固定，且 $\sigma_i(\alpha)=\alpha_i$，这就意味着 $\sigma_i\in S_i$，所以 $S_i$ 必定是非空的。

因此，任取 $\sigma_i\in S_i$，构造映射 $\Psi:S_i\to \text{Aut}(E/F(\alpha))$，使得 $\Psi(\sigma)={\sigma_i}^{-1}\sigma$，即复合上 $\sigma_i$ 的逆映射，我们来研究它的性质，不妨设 $\rho={\sigma_i}^{-1}\sigma$：

- 良定义：对任意 $\sigma\in S_i$，$\rho$ 仍然是自同构，且由于 $\sigma_i(\alpha)=\sigma(\alpha)=\alpha_i$，则必有 $\rho(\alpha)={\sigma_{i}}^{-1}(\sigma(\alpha))=\alpha$，任取 $y\in F(\alpha)$，不妨表示成 $y=\displaystyle\sum_{j=0}^rc_j \alpha^j$ 其中 $c_i\in F$，则 $\rho(y)=\displaystyle\sum_{j=0}^r\rho(c_j) \rho(\alpha)^j=\displaystyle\sum_{j=0}^rc_j\alpha^j=y$，故 $\rho$ 是保持 $F(\alpha)$ 不动的自同构，即 $\rho\in\text{Aut}(E/F(\alpha))$。
- 单射性：由于映射形成群，其复合运算满足消去律，故 $\Psi$ 是单射。
- 满射性：任取 $\rho\in \text{Aut}(E/F(\alpha))$，取 $\sigma={\sigma_{i}}\rho$  即可复原原像。

因此 $\Psi$ 是双射，即 $|S_i|=|\text{Aut}(E/F(\alpha))|$，而 $[E:F(\alpha)]=\dfrac nd<n$，由归纳假设，知 $|\text{Aut}(E/F(\alpha))|=[E:F(\alpha)]$，因此，可知 $|\text{Aut}(E/F)|=[E:F(\alpha)] \cdot [F(\alpha):F]=[E:F]$。$\blacksquare$
## Galois 扩张的正规性与可分性
> **定理（Galois 扩张的正规性与可分性）**
> 
> 设 $E$ 是 $F$ 的 Galois 扩张。
> 则对于任意 $\alpha\in E$，其在 $F$ 上的极小多项式 $p(x)\in F[x]$ 能够在 $E[x]$ 中完整分解为一次因式的乘积，且多项式无重根。 

**证明：**

记 $G=\text{Aut}(E/F)$，由于 $E$ 是 $F$ 的 Galois 扩张，知 $E^G=F$。

让群 $G$ 作用在元素 $\alpha\in E$ 上，设 $\alpha$ 在 $G$ 的全体自同构作用下形成的轨道为 $O_\alpha$，即：
$$O_\alpha=\{\sigma(\alpha)\mid \sigma\in G\}$$
考虑 $\alpha$ 在 $F$ 上的极小多项式 $p(x)$，由于自同构对根的置换性质， $O_\alpha$ 的任何一个元素，都必须是 $p(x)$ 的根，而由于域中多项式根的个数上限，$p(x)$ 的根的个数有限，故 $O_\alpha$ 是有限集，不妨标号 $O_\alpha=\{\alpha_1,\alpha_2,\cdots,\alpha_r\}$，其中 $\alpha_1=\alpha$。

不妨构造多项式 $g(x)=\displaystyle\prod_{i=1}^r(x-\alpha_i)$，此时多项式 $g(x)$ 展开的各项系数是关于 $\alpha_1,\alpha_2,\cdots,\alpha_r$ 的基本对称多项式，也就是说，变元任意置换，结果保持不变，因此，其各项系数在 $\sigma$ 的作用下不动，因此属于 $F$ ，故 $g(x)\in F[x]$。

我们注意到 $g(x)$ 可以在 $E[x]$ 中完整分解为一次因式的乘积，且没有重根。

而 $\alpha$ 在 $F$ 上的极小多项式 $p(x)$，由极小多项式的性质，必有 $p(x)\mid g(x)$。
因此 $p(x)$ 可以在 $E[x]$ 中完整分解为一次因式的乘积，且没有重根。$\blacksquare$

我们之前证明了可分多项式的分裂域必为 Galois 扩张，那么有限 Galois 扩张的正规性与可分性就有一个可能更加有用一点的推论。

>**定理（有限 Galois 扩张必定是可分分裂域）**
>
>设 $E$ 是 $F$ 的有限 Galois 扩张，则必定存在 $F[x]$ 上的可分多项式 $f(x)$，使得 $E$ 是 $f(x)$ 在 $F$ 上的分裂域。

**证明：**

由于 $E$ 是 $F$ 的有限扩张，不妨设 $E=F(\alpha_1,\alpha_2,\cdots,\alpha_r)$，分别找出 $\alpha_1,\alpha_2,\cdots,\alpha_r$ 在 $F$ 上的极小多项式 $p_1(x),p_2(x),\cdots,p_r(x)$，再设 $f(x)\in F[x]$ 满足：
$$f(x)=\displaystyle\prod_{i=1}^rp_i(x)$$
根据我们对可分多项式的定义，$f(x)$ 是可分多项式。

由于有限 Galois 扩张的正规性与可分性，$p_1(x),p_2(x),\cdots,p_r(x)$ 都可以在 $E[x]$ 中完整分解为一次因式的乘积，因此，$f(x)$ 可以在 $E[x]$ 中完全分解为一次因式的乘积。

而由于 $\alpha_1,\alpha_2,\cdots,\alpha_r$ 是 $f(x)$ 的根的一部分，因此，$F$ 和 $f(x)$ 的全体根生成 $E$。即证明了 $E$ 是 $f(x)$ 在 $F$ 上的分裂域。$\blacksquare$

# Galois 基本定理

本部分的证明，重点在于“Galois”对应的正规性的证明，核心是将自同构群的正规性翻译成域的性质，明确了这一点之后，再沿用限制映射，就可以比较自然地推导而来。
## Galois 对应
> **定理（Galois 对应）**
> 
> 设 $E$ 是 $F$ 的有限 Galois 扩张，其 Galois 群为 $G=\text{Gal}(E/F)$。
> 
> 令 $\mathcal K$ 为包含 $F$ 且被 $E$ 包含的所有中间域 $K$ 的集合，即 $F\subseteq K\subseteq E$。
> 
> 令 $\mathcal H$ 为 $G$ 的全体子群 $H$ 的集合。
> 
> 定义两个映射：
> 
> 将子群映射为其固定域的映射 $\Phi:\mathcal H\to \mathcal K$，使得 $\Phi(H)=E^H$。
> 
> 将域映射为保持该域不动的自同构群 $\Psi:\mathcal K\to\mathcal H$，使得 $\Psi(K)=\text{Aut}(E/K)$。
> 
> 则 $\Phi$ 和 $\Psi$ 互为逆映射，即在 $\mathcal K$ 和 $\mathcal H$ 建立起双射，我们将这种中间域和自同构子群的双射关系称为 $E/F$ 的 **Galois 对应**。

**证明：**

**先证明** $\boldsymbol{\Psi(\Phi(H))=H}$，任取 $G$ 的子群 $H$，其固定域为 $E^H$。
由 Artin 固定域定理，$H=\text{Aut}(E/E^H)$，故 $\Psi(\Phi(H))=H$ 成立。

**再证明** $\boldsymbol{\Phi(\Psi(K))=K}$，任取域 $K$ 满足 $F\subseteq K\subseteq E$，由于有限 Galois 扩张必定是可分分裂域，即存在可分多项式 $f(x)\in F[x]$，使得 $E$ 是 $f(x)$ 在 $F$ 上的分裂域。

那么，$f(x)\in K[x]$，此时它仍然是可分多项式，因此 $E$ 也是 $f(x)$ 在 $K$ 上的分裂域，由于可分多项式的分裂域必为 Galois 扩张，故 $E$ 是 $K$ 的 Galois 扩张。
由定义，就有 $E^{\text{Aut}(E/K)}=K$，即 $\Phi(\Psi(K))=K$ 。$\blacksquare$

证明过程中有一个比较好用的推论，先单独列出来。

> **推论（Galois 对应的推论）**‘
> 
> 设 $E$ 是 $F$ 的有限 Galois 扩张，则对 $E/F$ 的 Galois 对应的中间域 $K$。
> 
> 总有 $E$ 是 $K$ 的有限 Galois 扩张。

此外，有两个并不难证的性质，一并给出证明。

>**定理（Galois 对应的反序包含性质）**
>
> 设 $E$ 是 $F$ 的有限 Galois 扩张，其 Galois 群为 $G=\text{Gal}(E/F)$。
> 
> 若 $E/F$ 的 Galois 对应中，中间域 $K_1,K_2$ 对应自同构子群 $H_1,H_2$，则：
> 
> $K_1\subseteq K_2$ 当且仅当 $H_1\ge H_2$（即 $H_2$ 是 $H_1$ 的子群）。

**证明：**

**必要性**，若 $K_1\subseteq K_2$，任取 $\sigma\in H_2=\text{Aut}(E/K_2)$。由于 $\sigma$ 保持 $K_2$ 中的所有元素逐点固定，而 $K_1\subseteq K_2$，$\sigma$ 保持 $K_1$ 中的所有元素逐点固定，即 $\sigma\in \text{Aut}(E/K_1)=H_1$，即 $H_2\le H_1$。

**充分性**，若 $H_1\ge H_2$，任取 $x\in K_1=E^{H_1}$，由于 $x$ 被 $H_1$ 中的所有自同构固定，而 $H_1\ge H_2$，$x$ 被 $H_2$ 中的所有自同构固定，即 $x\in E^{H_2}=K_2$，即 $K_1\subseteq K_2$。$\blacksquare$

>**定理（Galois 对应的数量关系）**
>
>设 $E$ 是 $F$ 的有限 Galois 扩张，其 Galois 群为 $G=\text{Gal}(E/F)$。
>
> 若 $E/F$ 的 Galois 对应中，中间域 $K$ 对应自同构子群 $H$，则有：
> 
> $[E:K]=|H|$ 且 $[K:F]=[G:H]$。
> 
> 其中 $[G:H]$ 是子群的指数。

**证明：**

由 Galois 对应的推论知 $E$ 是 $K$ 的 Galois 扩张，且对应的 Galois 群是 $H=\text{Aut}(E/K)$。

因此，根据有限 Galois 扩张的等价刻画，直接就有 $[E:K]=|H|$。

同样，由于 $E$ 是 $F$ 的 Galois 扩张，直接就有 $[E:F]=|G|$。

由子群的 Lagrange 定理，$|G|=|H|\cdot [G:H]$。

由扩域的塔定理，$[E:F]=[E:K]\cdot [K:F]$。

联立得到 $|H|\cdot [G:H]=[E:K]\cdot [K:F]$，消去 $[E:K]=|H|$，得到 $[K:F]=[G:H]$。$\blacksquare$
## Galois 对应的正规性
它虽然仍然是 Galois 对应的性质，但它特别重要，故单开。

>**定理（Galois 对应的正规性）**
>
>设 $E$ 是 $F$ 的有限 Galois 扩张，其 Galois 群为 $G=\text{Gal}(E/F)$。
>
> 若 $E/F$ 的 Galois 对应中，中间域 $K$ 对应自同构子群 $H$，则有：
> 
> $H$ 是 $G$ 的正规子群（即 $H\trianglelefteq G$）当且仅当 $K$ 是 $F$ 的 Galois 扩张。
> 
> 并且，如果上述条件成立，则必有 $\text{Gal}(K/F)\cong G/H$。

**证明：**

为了研究自同构子群 $H$ 与中间域 $K$ 的对应，条件里有正规，那就想到共轭，任取 $\sigma\in G$，考察共轭子群 $\sigma H\sigma^{-1}$ 对应的固定域。

不妨取 $x\in K,h\in H$，考虑其自同构 $\sigma h\sigma^{-1}$ 作用于 $\sigma(x)$ 的结果，即 $(\sigma h\sigma^{-1})(\sigma(x))=(\sigma h)(x)$，那么由于 $h\in H=\text{Aut}(E/K)$，$(\sigma h)(x)=\sigma(x)$，即若 $x\in K$，自同构 $\sigma h\sigma^{-1}$ 恰好保持 $\sigma(x)$ 固定。

反之，如果 $\sigma(x)$ 能被 $\sigma H\sigma^{-1}$ 中的所有元素固定，对任意 $h\in H$，总有 $(\sigma h\sigma^{-1})(\sigma(x))=\sigma(x)$，即可推出 $h(x)=x$，那么 $x$ 被 $H$ 中所有元素固定，即可推出 $x\in E^H=K$。

因此，若设 $\sigma(K)=\{\sigma(x)\mid x\in K\}$，我们有自同构子群 $\sigma H\sigma^{-1}$ 对应中间域 $\sigma(K)$。

那么，如果 $H\trianglelefteq G$ ，则 $\forall\sigma \in G,\sigma H\sigma^{-1}=H$，则由 Galois 对应， $\sigma(K)=K$ 必定成立。
反之，如果 $\forall\sigma \in G,\sigma(K)= K$，则由 $E/F$ 的 Galois 对应，必有 $\sigma H\sigma^{-1}=H$，因此 $H\trianglelefteq G$。
也就是说，$H\trianglelefteq G$ 当且仅当 $\forall\sigma \in G,\sigma(K)= K$。

**必要性**，如果 $H\trianglelefteq G$，则必有 $\forall\sigma \in G,\sigma(K)= K$，我们记 $\sigma |_K$ 为将 $\sigma$ 的映射方式不变，但定义域和值域都限制在 $K$ 以内得到的新映射。那么 $\sigma|_K:K\to K$ 仍然是双射，且仍然保持 $F$ 逐点固定，故 $\sigma|_K\in \text{Aut}(K/F)$。

那么，构造群同态 $\varphi:G\to \text{Aut}(K/F)$，映射规则正是 $\varphi(\sigma)=\sigma|_K$。

注意到核 $\ker \varphi$，即映射到 $K$ 上的恒等映射的那些自同构，即保持 $K$ 不动的 $E$ 的自同构，故 $\ker\varphi=\text{Aut}(E/K)=H$。

由群的第一同构定理：
$$G/H\cong \text{Im}(\varphi)$$
显然 $\text{Im}(\varphi)\subseteq \text{Aut}(K/F)$，即 $|\text{Im}(\varphi)|\le |\text{Aut}(K/F)|$。

在 Galois 对应的数量关系中，我们已经知道 $|G/H|=[G:H]=[K:F]$，而由于 $|G/H|=|\text{Im}(\varphi)|$，我们有 $[K:F]=|\text{Im}(\varphi)|\le |\text{Aut}(K/F)|$，而由嵌入映射的数量上界，我们有 $|\text{Aut}(K/F)|\le[K:F]$。

从基数上，我们总有 $[K:F]=|\text{Im}(\varphi)|\le |\text{Aut}(K/F)|\le [K:F]$，注意到不等式链的开头和结尾都相等，因此必有 $|\text{Im}(\varphi)|= |\text{Aut}(K/F)|= [K:F]$ ，由有限 Galois 扩张的等价刻画， $K$ 是 $F$ 的 Galois 扩张。而结合 $\text{Im}(\varphi)\subseteq \text{Aut}(K/F)$，我们就有 $\text{Im}(\varphi)= \text{Aut}(K/F)$，即 $G/H\cong \text{Gal}(K/F)$。

**充分性**，若 $K$ 是 $F$ 的 Galois 扩张（由于 $E$ 是 $F$ 的有限 Galois 扩张，$K$ 也是 $F$ 的有限 Galois 扩张），由于有限 Galois 扩张必定是可分分裂域，存在可分多项式 $f(x)\in F[x]$，使得 $K$ 是 $f(x)$ 在 $F$ 上的分裂域，任取大群的自同构 $\sigma\in G$，由于 $\sigma$ 保持 $F$ 不动，由自同构对根的置换性质，知 $\sigma$ 将 $f(x)$ 的根映射为 $f(x)$ 的根，不妨设 $f(x)$ 的根为 $\alpha_1,\alpha_2,\cdots,\alpha_r$，则任取 $\beta\in K$，则必可以表示成 $F$ 中元素和 $\alpha_1,\alpha_2,\cdots,\alpha_r$ 的有限次四则运算的结果，由于 $\sigma(\alpha_i)$ 仍然是 $f(x)$ 的根，$\sigma(\beta)\in K$。
因此，必有 $\sigma(K)\subseteq K$，由于 $\sigma^{-1}\in G$ 也成立，因此 $\sigma^{-1}(K)\subseteq K$，即 $K\subseteq \sigma(K)$，因此 $K=\sigma(K)$。

由于 $\forall\sigma \in G,\sigma(K)= K$，必有 $H\trianglelefteq G$，在必要性中，我们已经证明了只要 $H\trianglelefteq G$ ，就有 $G/H\cong \text{Gal}(K/F)$，不再重证。$\blacksquare$

# 代数基本定理的 Galois 证明

我想，都到这里了，你可以放松一点。
## 两个初等的分析学公理

>**公理（实数域的奇次多项式必有实根）**
>
>任何奇数次的实系数多项式 $f(x)\in \mathbb R[x]$，在 $\mathbb R$ 中至少有一个根。
>
>（在分析学中，由连续函数的介值定理保证，因为奇数次实系数多项式在正负无穷大处符号异号）


>**推论（实数域不存在大于 1 的奇数次有限扩域）**
>
>若 $K$ 是 $\mathbb R$ 的有限扩张，且 $[K:\mathbb R]=m$ 为奇数，则 $m=1$。 

**证明：**

设 $K$ 是 $\mathbb R$ 的有限扩张，且 $[K:\mathbb R]=m$ 为奇数，由于 $\mathbb R$ 的特征为 0，由本原元定理，存在 $\gamma\in K$，使得 $K=\mathbb R(\gamma)$，由于 $K$ 是 $\mathbb R$ 的有限扩张，它必定是代数扩张，$\gamma$ 在 $\mathbb R$ 上存在极小多项式 $p(x)$，由单扩张的维数定理，$p(x)$ 的次数为 $m$，且是 $R[x]$ 上的不可约多项式，由公理，$p(x)$ 在 $\mathbb R$ 上必定有根，因此 $p(x)$ 的次数必定为 1，即 $m=1$。$\blacksquare$

>**公理（复数域可以开平方）**
>
>对任意复数 $z\in\mathbb C$，一定存在$w\in\mathbb C$，使得 $w^2=z$。
>
>（由复数的极坐标表示，比较容易看出这个公理的正确性，若 $z=re^{i\theta}$，则取 $w=\sqrt re^{i\theta/2}$）


>**推论（复数域不存在次数为 2 的有限扩域）**
>
>若 $K$ 是 $\mathbb C$ 的有限扩张，则 $[K:\mathbb C]\ne 2$。

**证明**：

若 $[K:\mathbb C]=2$，由本原元定理，存在 $\gamma\in K$，使得 $K=\mathbb C(\gamma)$，由于 $K$ 是 $\mathbb C$ 的有限扩张，它必是代数扩张，$\gamma$ 在 $\mathbb C$ 上存在极小多项式 $p(x)$，由单扩张的维数定理，$p(x)$ 次数为 2，不妨设 $p(x)=x^2+bx+c$（由于 $\mathbb C$ 的特征为 0，除以 2 和 4 被允许），注意到 $p(x)=\left(x+\dfrac b2\right)^2+c-\dfrac{b^2}{4}$，由公理，存在 $w\in \mathbb C$，使得 $w^2=\dfrac{b^2}{4}-c$，因此 $p(x)=\left(x+\dfrac b2\right)^2-w^2=\left(x+\dfrac b2-w\right)\left(x+\dfrac b2+w\right)$ 。

那么 $p(x)$ 在 $\mathbb C[x]$ 中可以分解为一次因式的乘积，与它是极小多项式矛盾。故 $[K:\mathbb C]\ne 2$。$\blacksquare$

## 代数基本定理

先证明一个引理。
>**定理（复数域扩域的 Galois 闭包）**
>
>若 $E$ 是 $\mathbb C$ 的有限扩张，存在 $E$ 的扩域 $L$，使得 $L$ 是 $\mathbb R$ 的有限 Galois 扩张。

**证明：**
由于 $E$ 是 $\mathbb C$ 的有限扩张，$\mathbb C=\mathbb R(\text i)$ 是 $\mathbb R$ 的有限扩张，由本原元定理，存在 $\gamma\in E$ 使得 $E=\mathbb R(\gamma)$。

不妨设 $\gamma$ 在 $\mathbb R$ 上的极小多项式 $p(x)$，由于零特征域上不可约多项式可分， $p(x)$ 是可分多项式。
设 $L$ 是 $p(x)$ 在 $\mathbb R$ 上的分裂域，由于可分多项式的分裂域必为 Galois 扩张，$L$ 是 $\mathbb R$ 的有限 Galois 扩张，同时，$L$ 包含 $p(x)$ 的根 $\gamma$ ，故 $L$ 是 $E$ 的扩域。$\blacksquare$

>**定理（代数基本定理）**
>
>若 $E$ 是 $\mathbb C$ 的有限扩张，则 $E=\mathbb C$。

**证明：**

若 $E$ 是 $\mathbb C$ 的有限扩张，存在 $E$ 的扩域 $L$ 使得 $L$ 是 $\mathbb R$ 的有限 Galois 扩张。
由于 $L$ 是 $\mathbb R$ 的有限 Galois 扩张，由 Galois 对应的推论，$L$ 是 $\mathbb C$ 的有限 Galois 扩张。
不妨设 $G=\text{Gal}(L/\mathbb R)$，考虑 $[E:\mathbb C]$。
设 $|G|=2^km$，其中 $m$ 是奇数，由 Sylow 第一定理，$G$ 存在一个大小为 $2^k$ 的子群 $H$。

考虑 $L/\mathbb R$ 的 Galois 对应中，$H$ 对应的固定域 $K=L^H$，则 $[K:\mathbb R]=[G:H]=\dfrac{2^k m}{2^k}=m$。
而由于实数域不存在大于 1 的奇数次有限扩域，知 $m=1$，因此 $|G|=2^k$。

注意到 $[\mathbb C:\mathbb R]=2$ ，不妨设 $G_1=\text{Aut}(L/\mathbb C)$，由 Galois 对应的数量关系：
$$|G_1|=[L:\mathbb C]=\dfrac{[L:\mathbb R]}{[\mathbb C:\mathbb R]}=2^{k-1}$$
如果 $L\ne \mathbb C$，则 $k>1$，由 Sylow 第一定理的推论，知 $G_1$ 一定存在阶数为 $2^{k-2}$ 的子群，不妨记为 $H_1$。
考虑 $L/\mathbb C$ 的 Galois 对应中，$H_1$ 对应的固定域 $K_1=L^{H_1}$，则 $[K_1:\mathbb C]=[G_1:H_1]=2$。
但，由于复数域不存在次数为 2 的有限扩域，这种情况又是不可能发生的。
因此，必有 $L=\mathbb C$。$\blacksquare$

这意味着，对 $\mathbb C[x]$ 上的任意多项式 $f(x)$，由于 $f(x)$ 在 $\mathbb C$ 上的分裂域必定存在，且只能为 $\mathbb C$ 的有限扩张，故 $f(x)$ 在 $\mathbb C$ 上的分裂域就是 $\mathbb C$，即 $f(x)$ 在 $\mathbb C[x]$ 上总能分解为一次因式的乘积。

同样地，对于 $\mathbb R[x]$ 上的任意多项式 $f(x)$，$f(x)$ 在 $\mathbb R$ 上的分裂域必定是 $\mathbb C$ 的子域，由于这是有限扩张，$f(x)$ 的分裂域要么是 $\mathbb R$ 要么是 $\mathbb C$，任取 $f(x)$ 的根 $\alpha$，其极小多项式次数要么是 1 要么是 2，即 $f(x)$ 在 $R[x]$ 上总能分解为一次或二次因式的乘积。
# 尾声

我想，在代数基本定理的对应实例中，你可以看到一个有趣的范式，即找到一个更大的域是 Galois 扩张，把条件翻译成群的性质，然后将其求解，这也是后续 Abel-Ruffini 定理会沿用的范式。

本篇由于所举例子相对抽象，也很难就着具体的实例去画一个图，这的确是一个缺点，然而，读者心中应当对 Galois 对应有一个直观的印象，只不过它可能难以由一篇简短，具体实例较少的文章给予。

后续还有一篇短文，简单地证明 Abel-Ruffini 定理，即可收尾。