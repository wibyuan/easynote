付费咨询真不是一个容易的活计，你对此深有体会，自从你开通了付费咨询之后，数不清的麻烦就找上了你。

比如今天，Alice 和 Bob 找到你，希望你能解决他们的争执。

事情是这样的，Bob 在报纸上看到了一道题目 $\boldsymbol x$，Alice 看了，哈哈大笑。

Bob 问 Alice 为何发笑。

Alice 说，我已经想到了这道题目的正确答案。

Bob 表示，然而我却想不到，不如让我检验一下吧，我刚刚写了一个程序 $\mathcal C$，你把你所谓的正确答案 $\boldsymbol w$ 给我，我跑一下 $\mathcal C(\boldsymbol x,\boldsymbol w)$，如果结果是 1，我就相信你，否则我就知道你并没有正确的答案。

Alice 表示，但是那样，Bob 不就白嫖了她的解法吗？

因此他们找到了你。

你听得津津有味，但你怀疑你听错了，这个答案有什么珍贵的，宁愿找个付费咨询，也不愿意直接给吗，你所在的行业，人们找到了一个难题的解法可是恨不得让所有人立刻完整理解呢。

你重新问了一遍 Alice 和 Bob：

“确认下啊，你们二位的咨询任务确实是让我设计一个协议，满足 Alice 能够在不公开答案的情况下让 Bob 相信她持有正确的答案，我在设计期间可以咨询你们的条件，在你们双方同意的情况下开展设计，直到最后得到一个你们认可的完整设计，然后你们的委托圆满结束，是吧？”

Alice 和 Bob 点点头。你捂脸，他们一直精神状态这么美丽吗？
# 初步建模

你表示很头疼，于是你打算把 Alice 和 Bob 的要求初步建模一下。

## 建立协议

你感觉很疑惑，首先 Alice 要给 Bob 发消息，其次，这两个看似矛盾的条件得同时满足：

- Alice 发出的消息需要让 Bob 相信她拥有一个元素 $\boldsymbol w\in \mathcal L$，其中 $\mathcal L$ 是你定义的解法集合，使得 $\mathcal C(\boldsymbol x,\boldsymbol w)=1$，即 Bob 相信 Alice 仅仅有可忽略的概率伪造成功。
- Alice 发出的消息需要让 Bob 在寻找 $\mathcal C(\boldsymbol x,\boldsymbol w)=1$ 问题的一个解 $\boldsymbol w\in \mathcal L$ 上，仅仅获得可忽略的增益。

这世界上哪有这么好的事情，等等？

你回想起了当年某算法发论文上库，你被拉去做 Trained Listener 做 ABX 的惨痛经历，当时你需要做这样的事情 16 轮：

- 测试界面上有 3 个按钮 A、B、X。
- A 是未经压缩的母带，B 是压缩过的音频，X 随机是 A 或 B，里面只有几秒钟的片段，响度被精细调整过控制在几乎一样的分贝。
- 你选择 X 到底是 A 还是 B。

你被允许有若干轮的走神，如果你对的次数足够多，人们就可以确认低码率下的压缩损伤。

尽管有休息时间，但后面几轮，听了几十遍还没听出区别的痛苦你还是记得的，那几轮听错的你感觉不能被单纯当作走神，但现在想来，你没有公开说明你听音的技巧，而人们相信了一个由你主导的事实——低码率算法压缩在人类听觉上体现有损，这似乎正对应着你被委托的需求。

你明白了，看起来不论最后协议长什么样子，一开始想想交互式协议总不会有大问题。
## 严格定义可忽略

你叫住了 Alice 和 Bob。

“听着，我打算设定一个安全参数 $\kappa$，然后我设计的协议是有概率出错的，但是随着 $\kappa$ 的增大，出错的概率会迅速减小，因此你们稍微调大一点点 $\kappa$，协议出错的概率就会很快小到……比你们的大脑被宇宙射线轰击出错的概率还小……所以它们实际上是安全的，明白吗？”

Alice 和 Bob 点点头，你松了一口气。

那么根据这个安全参数 $\kappa$，你打算定义可忽略函数，就是那种随着 $\kappa$ 增大，绝对值快速减小的函数啊，而且一定要好算！你可懒得想太多细节了。


>**定义（可忽略函数）**
>
>一个在定义域 $\mathbb N^+$ 上恒为正的函数 $f(\kappa)$ 是**可忽略**的，当且仅当对任意 $\mathbb R[\kappa]$ 上的，在 $\kappa$ 充分大时恒为正的多项式 $p(\kappa)$，有：
>$$\lim_{\kappa\to+\infty}p(\kappa)f(\kappa)=0$$
>全体可忽略函数组成的集合记作 $\text{negl}(\kappa)$。

你告诉 Alice 和 Bob，见过 NPC 问题嘛，计算机科学家们都认为 NPC 问题是很难的问题，就是因为现在还找不到概率多项式时间算法，因此，只要我证明你们运用概率多项式时间算法，伪造或者破解的概率在 $\text{negl}(\kappa)$ 这个量级，那你们只需要调大你们的 $\kappa$ ，就可以轻易得到极难伪造或破解的正规流程了！

总之你似乎蒙过了 Alice 和 Bob，你松了一口气，不要求信息论安全是很好的，要是和他们解释 $2^{-128}$ 的概率为什么在现实中几乎不可能发生，可能又要费一番口舌。
## 信任请求

你打算先用单轮交互搞定，这并不是因为你认为单轮交互已经足够优秀，只是你的脑子需要一个简单的锚点。

你先问了一下，Alice 和 Bob，你们是否愿意信任和你们利益无关的第三方，这个第三方不需要知道 Alice 的秘密，但是你们要信任它会遵守流程而不会偏向某一方。

Alice 和 Bob 同意了，你松了一口气，这样大概率会让你的设计变得容易一点吧。
## 流程设定

你的流程需要三个组件，$\text{Setup},\text{Prove},\text{Verify}$。

当流程开始时，一个可信的第三方运行 $\text{Setup}(1^{\kappa},\mathcal C)\to (\text{PK},\text{VK})$，具体而言，可信第三方接受 $\kappa$ 和 $\mathcal C$，并生成一对 $(\text{PK},\text{VK})$，形式上，$\text{PK}$ 代表 Alice 需要知道的内容，$\text{VK}$ 代表 Bob 需要知道的内容，但 $(\text{PK},\text{VK})$ 对双方都共享，可信第三方不能透露更多的信息，在这一流程结束后，可信第三方不应该参与剩余流程。

然后，Alice 自己运行 $\text{Prove}(\text{PK},\boldsymbol x,\boldsymbol w)\to\pi$，生成证明 $\pi$ 发给 Bob。

最后，Bob 自己运行 $\text{Verify}(\text{VK},\boldsymbol x,\pi)\to \{0,1\}$ 如果结果是 1，则相信 Alice，否则不信。

哇，看起来很好耶，但是交互又到哪里去呢，你不太在意，在你看来，也许打个补丁可以解决，但是现在你懒得想交互的事情了。
## 安全性约束

然后为了满足 Alice 和 Bob 的要求，你打算形式化他们的需求，主要是三个要素。

你的原则是，既然雇主已经允许了低概率的失误，那就不要把安全条件放得太高，至于你最后的协议如果达到了更强的安全条件，你当然值得自得一番，但如果一开始就定太高的标准，可能就会出事。

因此你打算先把所有安全约束都加上可忽略的失误概率，具体如下：

完备性，即如果 Alice 确实知道一个满足要求的 $\boldsymbol w$，那么按照流程走，生成的 $\pi$ 不被 $\text{Verify}(\text{VK},\boldsymbol x,\pi)$ 的接受的概率是可忽略的，即按流程走几乎必然被接受。

知识可靠性，即如果 Alice 确实不知道一个满足要求的 $\boldsymbol w$，那么运行任意概率多项式算法，生成的 $\pi^*$ 被 $\text{Verify}(\text{VK},\boldsymbol x,\pi^*)$ 的接受的概率是可忽略的，即伪造证明几乎必然不被接受。反过来说，就是，如果 Alice 造出了一个被接受的证明，排除掉发生概率可忽略的情况，则 Alice 必须可以被看作拥有 $\boldsymbol w$。 

零知识性，即 Bob 从 Alice 的证明 $\pi$ 中，除了获得“Alice 确实拥有 $C(\boldsymbol x,\boldsymbol w)=1$ 的 $\boldsymbol w$ ”可以直接推导出的信息之外，无法获得任何关于寻找 $C(\boldsymbol x,\boldsymbol w)=1$ 的解 $\boldsymbol w$ 的辅助信息。

此外， Bob 另外提出了一个要求，他表示，自己那方没有 Alice 那边的算力，因此希望自己这边的算力比较轻量，并且，自己那边的网不太好，所以希望 Alice 传输的证明的大小比较小。

“很好嘛，证明的验证必须轻量且简洁。”你点点头。

不过你当前连方案都没设计出来，你勉强表示重视，但暂时搁置了。

好的，那么接下来如何编写可以利用这三个要素的协议呢？
# 协议构造

你看向了 Alice 和 Bob 给出的函数 $\mathcal C$，你觉得这玩意简直太抽象了，可不可以用更好的方式建模呢。

## 组合完备初探

你听说了一个叫做模 $p$ 有限域的东西，听说在它上面，可以任意进行加减乘除，而只要运算合法，比如不除以 0，那么就不会有任何误差，欸，你正好要寻找一个不会有任何误差的精确结构！

于是你注意到了模质数 $p$ 的有限域，不妨假设 $p$ 在 $2^{2\kappa}$ 这个量级，记模 $p$ 有限域为 $\mathbb F$。

那么你发现域上的加法和乘法本质上是似乎组合完备的。

因为，如果 $\kappa>1$，且 $x,y\in\{0,1\}$。

则 $\neg x=1-x$，$x\land y=xy$，且 $x\lor y=x+y-xy$。

欸，竟然与或非都表示出来了，那就有说法，可以用域上的运算对这个 $\mathcal C(\boldsymbol x,\boldsymbol w)=1$ 进行建模了。

首先对 $\boldsymbol x$ 和 $\boldsymbol w$ 进行参数化，不妨设 $\boldsymbol x=\begin{pmatrix}x_1&x_2&\cdots&x_k\end{pmatrix}^T\in \mathbb F^k$ 且 $\boldsymbol w=\begin{pmatrix}w_1&w_2&\cdots&w_l\end{pmatrix}^T\in \mathbb F^l$，那么 $\mathcal C$ 就可以理解为 $\mathcal C:\mathbb F^k\times \mathbb F^{l}\to \{0,1\}$ 的函数了。

## R1CS

你好像听人说过，如果只有线性组合，你最后只会得到一个线性函数。你深以为然，看起来你的与和或运算都用到了一次乘法，那能不能将一次乘法的操作标准化，配合上线性组合，进而使得整个 $\mathcal C$ 能够用精确的数学语言被描述出来呢？

不妨尝试一下，你努力想想了一个全是加法和乘法的密密麻麻的 $\mathcal C$，$\boldsymbol x$ 和 $\boldsymbol w$ 的每个分量在其中用加法和乘法进行组合，最后得到了一个介于 $\{0,1\}$ 的结果，你试着简化它。

很显然，为了处理各种奇奇怪怪的需求，你需要加入中间变量 $\boldsymbol v=\begin{pmatrix}v_1&v_2&\cdots&v_{m-l-k-1}\end{pmatrix}^T\in \mathbb F^{m-l-k-1}$。

那么，不妨设 $\boldsymbol z=\begin{pmatrix}1&\boldsymbol x^T&\boldsymbol w^T&\boldsymbol v^T\end{pmatrix}^T\in \mathbb F^{m}$ 

然后我们定义 $A,B,C\in \mathbb F^{n\times m}$。

那么我们就可以把一般程序的约束表示为：
$$(A\boldsymbol z)\circ (B\boldsymbol z)=C\boldsymbol z$$
其中 $\circ$ 指的是对应位置相乘。

看似复杂，其实拆开来看就是 $n$ 条约束，每条都是线性组合乘线性组合等于线性组合的形式，也就是 R1CS 转化。

你给 Alice 和 Bob 举了一个例子，例如你要解的关于 $w$ 的方程是 $w^3+w+x=1$，其中 $x$ 是已知量，那么你就可以建立三个约束 $\begin{cases}w\cdot w=v_1\\v_1\cdot w=v_2\\(v_2+w+x)\cdot 1=1\end{cases}$，每一行都是一次线性组合乘一次线性组合等于一次线性组合的形式。

>**定义（R1CS 转化）**
>
>对于约束 $\mathcal C(\boldsymbol x,\boldsymbol w)=1$，其中 $\mathcal C:\mathbb F^k\times \mathbb F^{l}\to \{0,1\}$， $\boldsymbol x=\begin{pmatrix}x_1&x_2&\cdots&x_k\end{pmatrix}^T\in \mathbb F^k$ 和 $\boldsymbol w=\begin{pmatrix}w_1&w_2&\cdots&w_l\end{pmatrix}^T\in \mathbb F^l$ 。
>
>其 **R1CS 转化**形如：
>$$(A\boldsymbol z)\circ (B\boldsymbol z)=C\boldsymbol z$$
>
>其中 $\boldsymbol z=\begin{pmatrix}1&\boldsymbol x^T&\boldsymbol w^T&\boldsymbol v^T\end{pmatrix}^T\in \mathbb F^{m}$，$A,B,C\in \mathbb F^{n\times m}$。
> 
> 且 $\mathcal C(\boldsymbol x,\boldsymbol w)=1$ 当且仅当存在一组 $\boldsymbol v=\begin{pmatrix}v_1&v_2&\cdots&v_{m-l-k-1}\end{pmatrix}^T\in \mathbb F^{m-l-k-1}$ 使得 $(A\boldsymbol z)\circ (B\boldsymbol z)=C\boldsymbol z$。

不难看出，$A,B,C$ 的建模意图是，利用域的组合完备性，使得 $\mathcal C(\boldsymbol x,\boldsymbol w)=1$ 当且仅当，在 $\boldsymbol x$ 和 $\boldsymbol w$
 已知的前提下，$(A\boldsymbol z)\circ (B\boldsymbol z)=C\boldsymbol  z$ 有解，而且最好这个解比较容易求。

解比较容易求这个还是容易实现的，建立约束的时候简单一点就行了。

你打算再次确认组合完备性是否保持。
## 组合完备的校验

域上的加法就是线性组合，不显式增加约束，实在想写可以写 $(x+y)\cdot 1=z$。

布尔逻辑门，可以采用 $b\cdot (1-b)=0$ 形式的约束，使得 $b\in\{0,1\}$ 这个条件被强制保持。

然后就有与或非，即 $\neg x=1-x$，$x\land y=xy$，且 $x\lor y=x+y-xy$。

考虑零值测试，$\begin{cases}x\cdot y=1-z\\x\cdot z=0\end{cases}$，无其它限制，此时若 $x=0$ 则 $z=1$，若 $x\ne 0$ 则 $z=0,y=x^{-1}$。
（注意到 $x=0$ 时 $y$ 可取任意值，如果有额外要求，需要增加额外约束）

零值测试可以等价推导出等值检查。

考虑条件选择器，$\begin{cases}c\cdot (c-1)=0\\c\cdot(a-b)=(z-b)\end{cases}$，不难看出，当 $c=0$ 时，$z=b$，当 $c=1$ 时，$z=a$。

位拆分，$\begin{cases}{b_i}\cdot(b_i-1)=0&0\le i\le\lfloor \log_2 p\rfloor\\x\cdot 1=\displaystyle\sum_{i=0}^{\lfloor \log_2 p\rfloor}b_i 2^i\end{cases}$
（这里是用于存储的唯一拆分，完整域元素拆分需要配合范围检查）

而随机存取可以用条件选择器来实现内存读写。

因此，你看出来了，这个简单的 $(A\boldsymbol z)\circ (B\boldsymbol z)=C\boldsymbol z$ 确实可以实现任意组合逻辑。

你向 Alice 和 Bob 表示，你看看，你们的程序 $\mathcal C$ 就可以被这样拆成逻辑门来表示，不如我们以后就管 $\mathcal C$ 叫**电路**吧，他们同意了。

现在问题确实变得标准化了，但问题还是没变，怎么把证书发过去，既让 Bob 相信，又不暴露信息呢？

## Schwartz-Zippel 引理

你注意到一个事情，一个 $d$ 次多项式，它在模 $p$ 有限域中，至多只有 $d$ 个根。

换句话说：

>**定理（域上非零单变量多项式根的性质）**
>
>如果 $\mathbb F$ 是模 $p$ 有限域， $f(X)\in \mathbb F[X]$ 是 $d$ 次非零多项式。
>
>在 $\mathbb F$ 中随机取一个元素 $\alpha$，$f(\alpha)=0$ 的概率不大于 $\dfrac d{p}$  。

**证明：**

由于 $f(X)$ 在 $\mathbb F$ 中至多有 $d$ 个根，在 $\mathbb F$ 中随机取一个元素 $\alpha$，恰好取中一个根的概率不大于 $\dfrac d{p}$  。$\blacksquare$

反过来，对于一个多项式 $f(X)$，如果它不是 0 多项式，你只需要知道 $f(\alpha)$ 的值，其中 $\alpha$ 是随机的，你错误地判断它是 0 多项式的概率是 $\dfrac dp$，而 $p$ 是 $2^{2\kappa}$ 量级，因此，错误判断的概率是可以忽略的。

类似地，也有多变量下的形式，你感觉比较容易理解，用归纳法做一个扩展即可，先记下，说不定什么时候会用到。

>**定理（Schwartz-Zippel 引理）**
>
>如果 $\mathbb F$ 是模 $p$ 有限域， $f(X_1,X_2,\cdots,X_v)\in \mathbb F[X_1,X_2,\cdots,X_v]$ 是总次数为 $d$ 次非零多项式。
>
>任取 $S\subseteq \mathbb F$，从 $S$ 中均匀独立选取 $r_1,r_2,\cdots,r_v$，则 $f(r_1,r_2,\cdots,r_v)=0$ 的概率不大于 $\dfrac{d}{|S|}$。

你大体上明白了，对于一个多项式，你只要从足够大的空间中随机取一个点代入得到 0，那么这个多项式就是全 0 的，一次快速的压缩校验，几乎不透露太多信息，却能让你完整地清楚多项式的系数情况，似乎和你的要求相符。

你看了看你当前的式子，$(A\boldsymbol z)\circ (B\boldsymbol z)=C\boldsymbol z$，它能不能转变为多项式的校验呢？
## 多项式插值

你想到了一个办法，那就是连点成线，即：

- 把矩阵的行看成一个一个的约束门。
- 把矩阵的列看成一个一个的散点，连点形成曲线。

用 $\boldsymbol z$ 将多项式曲线线性组合之后，恰好就得到了经过特定点的曲线，那就是约束！

你听说过有一个拉格朗日插值的方法，具体而言，在有限域上选定 $n$ 个不同的元素集合：

$$H=\{\omega_0,\omega_1,\cdots,\omega_{n-1}\}\subseteq \mathbb F$$
听说人们会让 $H$ 恰好和域的乘法构成一个循环群且 $n$ 是 2 的幂来加速整个流程，但你对此不是很了解，先不管了。

为了方便起见，对 $\boldsymbol z,A,B$ 也采用 0 开头的索引，例如：
$$\boldsymbol z=\begin{pmatrix}z_0&z_1&\cdots&z_{m-1}\end{pmatrix}^T\in \mathbb F^{m}$$

顺便定义一个消失多项式 $Z_H(X)\in \mathbb F[X]$：

$$Z_H(X)=\prod_{i=0}^{n-1}(X-\omega_i)$$

那么，考虑多项式插值，我们可以利用多项式插值快速对 $\mathbb F^{n\times m}$ 上的矩阵 $A$ 生成 $m$ 个不超过 $n-1$ 次的多项式，设 $a_{i,j}$ 表示 $A$ 第 $i$ 行第 $j$ 列的值，其中第 $j$ 个多项式 $A_j$ 满足，对任意 $i\in\{0,1,\cdots,n-1\}$ 都有：
$$A_j(\omega_i)=a_{i,j}$$
然后设总多项式 $A(X)$ 满足：
$$A(X)=\displaystyle\sum_{i=0}^{m-1}z_iA_i(X)$$
然后，对 $B,C$ 以同样的方法生成它们的总多项式 $B(X),C(X)$。

由此我们就有多项式转化，即 $(A\boldsymbol z)\circ (B\boldsymbol z)=C\boldsymbol z$ 等价于 $A(\omega_i)B(\omega_i)-C(\omega_i)$ 在 $\omega_i\in H$ 时总是为 0。

那么， $A(\omega_i)B(\omega_i)-C(\omega_i)$ 在 $\omega_i\in H$ 时总是为 0 意味着什么呢？

意味着存在（次数不超过 $n-2$ 的）多项式 $Q(X)$，使得 $A(X)B(X)-C(X)-Q(X)Z_H(X)\equiv 0$，恒等于 0。

但是，$A(X),B(X),C(X),Q(X)$ 在这里不再是公开信息了，它是只有 Alice 可以计算的信息，因此进行拆分。

不妨设 $A_{\text{pub}}(X)=\displaystyle\sum_{i=0}^k z_iA_i(X)=A_0(X)+\displaystyle\sum_{i=1}^k x_iA_i(X)$，和 $A_{\text{priv}}(X)=A(X)-A_{\text{pub}}(X)$。
同理有 $B_{\text{pub}}(X),C_{\text{pub}}(X),B_{\text{priv}}(X),C_{\text{priv}}(X)$。

>**定理（零知识证明的多项式转化）**
>
>对于约束 $\mathcal C(\boldsymbol x,\boldsymbol w)=1$，其中 $\mathcal C:\mathbb F^k\times \mathbb F^{l}\to \{0,1\}$， $\boldsymbol x=\begin{pmatrix}x_1&x_2&\cdots&x_k\end{pmatrix}^T\in \mathbb F^k$ 和 $\boldsymbol w=\begin{pmatrix}w_1&w_2&\cdots&w_l\end{pmatrix}^T\in \mathbb F^l$ 。
>
>其中，$\mathbb F[X]$ 上的多项式 $Z_H(X),A_{\text{pub}}(X),B_{\text{pub}}(X),C_{\text{pub}}(X)$ 是 Alice 和 Bob 共同知晓的公开信息。
>
>如果 Alice 拥有 $\mathbb F[X]$ 上的多项式 $A_{\text{priv}}(X),B_{\text{priv}}(X),C_{\text{priv}}(X),Q(X)$，并使得：
>$$(A_{\text{pub}}(X)+A_{\text{priv}}(X))\cdot (B_{\text{pub}}(X)+B_{\text{priv}}(X))-(C_{\text{pub}}(X)+C_{\text{priv}}(X))-Q(X)Z_H(X)\equiv 0$$
>其中 $A_{\text{priv}},B_{\text{priv}},C_{\text{priv}}$  Alice 不能随意构造，而必须以同一个线性组合系数 $\begin{pmatrix}z_{k+1}&z_{k+2}&\cdots&z_{m-1}\end{pmatrix}^T\in \mathbb F^{m-k-1}$ 和公共信息如下构造：
>$$A_{\text{priv}}(X)=\displaystyle\sum_{i=k+1}^{m-1} z_iA_i(X)$$
>$$B_{\text{priv}}(X)=\displaystyle\sum_{i=k+1}^{m-1} z_iB_i(X)$$
>$$C_{\text{priv}}(X)=\displaystyle\sum_{i=k+1}^{m-1} z_iC_i(X)$$
>
>则 Alice 可以利用她已知的信息获取 $\boldsymbol w$ 满足 $\mathcal C(\boldsymbol x,\boldsymbol w)=1$。

**证明：**

取线性组合系数 $\boldsymbol z$，其中前 $k+1$ 个分量被公开参数固定，可以看作是 1 和 $\boldsymbol x=\begin{pmatrix}x_1&x_2&\cdots&x_k\end{pmatrix}^T$。

由于对任意 $\omega_i\in H$，就有 $A(\omega_i)B(\omega_i)-C(\omega_i)=0$，根据拉格朗日插值 $A(\omega_i)$ 相当于 $A$ 对应行乘上 $\boldsymbol z$ 的值，代入，等价于得到了 $(A\boldsymbol z)\circ (B\boldsymbol z)=C\boldsymbol z$ 的解。$\blacksquare$

你感觉差不多了，但是还差一点点东西，你不太确定是什么。

# 多项式承诺

你最终知道了你还差什么，如果一个东西被加密了，通常情况下，它会丧失代数性质，那这种情况下，是很难把它进行各种加法和乘法的校验的，那这个问题是不是……等等！

你忽然回忆起了一些有趣的数学知识。

你告诉 Alice 和 Bob，你要从一些复杂的结构中，寻找到关于加法和乘法类似魔法一般的计算器了。

## 数学知识

你听说椭圆曲线的加法群 $\mathbb G$ 是一个困难的群，它上面未解的难题简直是批发的，其中一个是椭圆曲线的离散对数问题，比如这是其中一个例子：

>**困难问题（椭圆曲线上的离散对数问题）**
>
>设 $\mathbb G$ 是阶数为质数 $p$ 的循环群，其中 $p$ 约为 $2^{2\kappa}$ 量级，且 $G$ 为其生成元，从模 $p$ 有限域中均匀随机选取整数 $\alpha$，设 $\alpha G$ 为 $\alpha$ 个 $G$ 进行椭圆曲线上的点加的结果。
>
>给定群元素 $y=\alpha G$，对于任意敌手 $\mathcal A$，在已知椭圆曲线群的表达式，$G$ 和 $y$ 的前提下，运行任意概率多项式时间算法，计算出 $\alpha$ 的概率是可忽略的。

当然其实你并不知道是不是真的没有，但数学家们说没找到，你姑且假设没有。

你为此感到非常好，不是因为它很难，而是因为，在椭圆曲线上，你拿到了 $aG,bG,cG$，你把它加起来就可以判断 $a+b\stackrel{?}{=}c$ 是否成立，但你却完全无法得到 $a,b,c$（你心里嘀咕，这个“完全无法得到”是不是比求不出来更强一点，但你姑且先继续推导吧）。

你感到很有意思，但是还缺一个乘法呀，于是你就多看了几篇有关的文章。

然后你就听说有人为了攻击椭圆曲线，发明了一个有趣的配对方法。

>**定义（第三类双线性配对）**
>
>设 $\mathbb G_1,\mathbb G_2,\mathbb G_T$ 是阶数为质数 $p$ 的群，其中 $p$ 约为 $2^{2\kappa}$ 量级，且 $G_1,G_2$ 分别为其生成元，任取整数 $\alpha$，设 $\alpha G$ 为 $\alpha$ 个 $G$ 进行椭圆曲线上的点加的结果，$\mathbb F$ 是模 $p$ 有限域。
>
>则映射 $e:\mathbb G_1\times \mathbb G_2\to \mathbb G_T$ 被称为**第三类双线性配对**，当且仅当满足四个条件：
>
>第一是双线性性，即对任意 $\alpha,\beta\in \mathbb F$，$P\in \mathbb G_1,Q\in \mathbb G_2$，均有 $e(\alpha P,\beta Q)= e(P,Q)^{\alpha\beta}$。
>
>第二是非退化性，即 $e(G_1,G_2)\ne 1_{\mathbb G_T}$，其中 $1_{\mathbb G_T}$ 是目标群 $\mathbb G_T$ 的单位元。
>
>第三是可计算性，映射 $e$ 可以被高效计算。
>
>第四是非对称性，即 $\mathbb G_1\ne\mathbb G_2$ 且不存在可在概率多项式时间计算的 $\varphi:\mathbb G_1\to \mathbb G_2$ 或 $\psi:\mathbb G_2\to \mathbb G_1$ 使得 $\varphi$ 或 $\psi$ 是非平凡的群同态映射。

你看着这些信息，灵光一闪。

同样地，你现在知道，你拿到了 $aG_1,bG_2,cG_1$，你只需要计算 $e(aG_1,bG_2)\stackrel{?}{=}e(cG_1,G_2)$ 是否成立即可判断 $a\cdot b=c$ 是否成立，但仍然对 $a,b,c$ 一无所知。

你看了看你式子的加法和乘法，你发现你的乘法也是只有一次的，有了。
## 初始思考

你盯着 $A(X)B(X)-C(X)-Q(X)Z_H(X)\equiv 0$ 发呆。

你想象着你代入了一个随机值 $\tau$ 使得 $A(\tau)B(\tau)-C(\tau)-Q(\tau)Z_H(\tau)= 0$。

然后给出 $\{A_i(\tau)G_1\}_{i=0}^{m-1},\{B_i(\tau)G_2\}_{i=0}^{m-1},\{C_i(\tau)G_1\}_{i=0}^{m-1},\{\tau^iZ_H(\tau)G_1\}_{i=0}^{n-2}$，其中 $G_1,G_2$ 分别是椭圆曲线群 $\mathbb G_1,\mathbb G_2$ 的生成元，Alice 就只能用这些已知的基多项式来校验线性组合了。

你眉头一皱，你意识到不能直接这样。

因为 Alice 可能会使得 $A(X),B(X),C(X)$ 不是真正由公开信息线性组合而来的，形式化而言，Alice 可能会用三个不同的向量 $\boldsymbol z_1,\boldsymbol z_2,\boldsymbol z_3$，满足 $(A\boldsymbol z_1)\circ (B\boldsymbol z_2)=C\boldsymbol z_3$。

实际上，Alice 甚至可能能凑出$(C\boldsymbol z_1)\circ (B\boldsymbol z_2)=C\boldsymbol z_3$，当前你给出的方案并没有禁止 Alice 这样凑，但这和你约束的转化大相径庭。

这怎么破解呢？

你灵光一闪，引入了两个随机偏移量 $\alpha,\beta\in\mathbb F\setminus \{0\}$。

你注意到 $(A(\tau)+\alpha)(B(\tau)+\beta)=A(\tau)B(\tau)+\beta A(\tau)+\alpha B(\tau)+\alpha\beta$。

那么 $A(\tau)B(\tau)-C(\tau)-Q(\tau)Z_H(\tau)= 0$ 可以简单地变形一下：
$$(A(\tau)+\alpha)(B(\tau)+\beta)=\alpha\beta+(\beta A(\tau)+\alpha B(\tau)+C(\tau))+Q(\tau)Z_H(\tau)$$
这样子，$A(X),B(X),C(X)$ 就被搅在一起了！

这样，你一开始只给出，$\{A_i(\tau)G_1\}_{i=0}^{m-1},\{B_i(\tau)G_2\}_{i=0}^{m-1},\{(\beta A_i(\tau)+\alpha B_i(\tau)+C_i(\tau))G_1\}_{i=0}^{m-1},\{\tau^iZ_H(\tau)G_1\}_{i=0}^{n-2}$。

独立的 $C_i(\tau)G_1$ 不给了！

如果 Alice 用 $A_i,B_i,C_i$ 的不同或无效的线性组合，看起来，由于 Alice 不知道 $\alpha,\beta$，如果她伪造，余项就会搅在一起让校验不通过！

你的眉头舒缓了，但你还是觉得差一点。
## 分离公私

你还是找到了你差在哪里。

Alice 虽然被迫使用同一组线性组合，但她仍然有可能伪造 $\boldsymbol x$，或者将 $\boldsymbol z$ 的其它部分（例如 Alice 本来就掌控的秘密信息 $\boldsymbol w,\boldsymbol v$）和 $\boldsymbol x,Q(X)$ 搅合在一起。

例如，Alice 可能伪造一个 $\boldsymbol z$，满足 $(A\boldsymbol z)\circ (B\boldsymbol z)=C\boldsymbol z$，但是 $\boldsymbol z$ 的前 $k+1$ 个分量不是 1 和 $\boldsymbol x$。

必须堵死这个漏洞！

你眉头一皱，展开了式子：

$$(A(\tau)+\alpha)(B(\tau)+\beta)=\alpha\beta+\sum_{i=0}^{m-1}z_i(\beta A_i(\tau)+\alpha B_i(\tau)+C_i(\tau))+Q(\tau)Z_H(\tau)$$

你灵光一闪，引入了两个随机偏移量 $\gamma,\delta\in \mathbb F\setminus\{0\}$  使得 $\gamma\ne \delta$，并令：
$$u_{\text{pub}}=\sum_{i=0}^kz_i\dfrac{\beta A_i(\tau)+\alpha B_i(\tau)+C_i(\tau)}{\gamma}$$
$$u_{\text{priv}}=\dfrac{Q(\tau)Z_H(\tau)}{\delta}+\sum_{i=k+1}^{m-1}z_i\dfrac{\beta A_i(\tau)+\alpha B_i(\tau)+C_i(\tau)}{\delta}$$
然后就有：
$$(A(\tau)+\alpha)(B(\tau)+\beta)=\alpha\beta+\gamma u_{\text{pub}}+\delta u_{\text{priv}}$$
其中 $u_{\text{pub}}$ 控制的信息直接由 Bob 算好，不给 Alice 机会，这样，你一开始给出：
$$\{A_i(\tau)G_1\}_{i=0}^{m-1},\{B_i(\tau)G_2\}_{i=0}^{m-1},\left\{\dfrac{\beta A_i(\tau)+\alpha B_i(\tau)+C_i(\tau)}{\gamma}G_1\right\}_{i=0}^{k}$$
$$\left\{\dfrac{\beta A_i(\tau)+\alpha B_i(\tau)+C_i(\tau)}{\delta}G_1\right\}_{i=k+1}^{m-1},\left\{\dfrac{\tau^iZ_H(\tau)}{\delta}G_1\right\}_{i=0}^{n-2}$$
带有 $\gamma$ 的项和 $\alpha G_1,\beta G_2$ 的双线性配对完全可以留给 Bob 独立计算，带有 $\delta$ 的项才是 Alice 算的，此外，Alice 仍然需要凑出完整的 $A,B$。

由于 Alice 不知道 $\gamma,\delta$，如果她伪造，这些 Alice 不知道的参数仍然会让校验不通过。

现在 Alice 理论上难以伪造了，但你还是莫名有些不安。

再想想。
## 加入盲化

你明白了，Alice 虽然理论上难以伪造了，但仍然有一个问题。

Alice 和 Bob 可能在同一个电路上进行多次证明。

每次，$\alpha,\beta,\gamma,\delta,\tau$ 都是固定的。

那么此时，$A(\tau)+\alpha$ 和 $B(\tau)+\beta$ 的统计规律就可能泄露隐私，有没有比较轻量级的办法，可以让 Alice 在每次生成的时候都加入一点盲化呢？

欸，不妨让 Alice 每次生成的时候都选取 $r,s\in \mathbb F$。

不妨设 $A'=A(\tau)+\alpha+r\delta$ 且 $B'=B(\tau)+\beta+s\delta$，注意到，这样就将 $A',B'$ 伪装成随机的群元素了，事实上，它们在统计上确实是均匀随机的。

就注意到：
$$A'B'=(A(\tau)+\alpha)(B(\tau)+\beta)+s\delta(A(\tau)+\alpha)+r\delta(B(\tau)+\beta)+rs\delta^2$$
代入原有等式就得到：
$$A'B'=\alpha\beta+\gamma u_{\text{pub}}+\delta \left(u_{\text{priv}}+s(A(\tau)+\alpha)+r(B(\tau)+\beta)+rs\delta\right)$$
换个写法：
$$A'B'=\alpha\beta+\gamma u_{\text{pub}}+\delta \left(u_{\text{priv}}+sA'+rB'-rs\delta\right)$$
你感觉好像可以构造最终的方案了。
# Groth16 协议

你不太确定你拍脑袋出来的东西能否说服 Alice 和 Bob，但你打算先把方案写出来。

## 初始化阶段

即 $\text{Setup}(1^{\kappa},\mathcal C)\to (\text{PK},\text{VK})$ 阶段，由可信第三方接管。

可信第三方会挑选一个大小为 $2^{2\kappa}$ 的特殊质数 $p$ 、模 $p$ 域 $\mathbb F$、两个 $p$ 阶椭圆曲线群 $\mathbb G_1,\mathbb G_2$ 和一个 $p$ 阶群 $\mathbb G_T$ ，以及双线性配对映射 $e:\mathbb G_1\times \mathbb G_2\to \mathbb G_T$，公开的信息还包括 $\mathbb G_1$ 的生成元 $G_1$ 和 $\mathbb G_2$ 的生成元 $G_2$。

可信第三方通过 $\mathcal C$ 和 $\mathbb F$ 可以计算出完整的 $n\times m$ 的矩阵 $A,B,C$ 并通过插值得到公开的多项式：
$$\{A_i(X)\}_{i=0}^{m-1},\{B_i(X)\}_{i=0}^{m-1},\{C_i(X)\}_{i=0}^{m-1},Z_H(X)$$
你提醒 Alice 和 Bob，这些参数最好选择以确定的简明算法生成的参数，以防止留有后门，一个臭名昭著的例子是 Dual_EC_DRBG，可以用它来观察那些不那么透明的参数会造成哪些恶果；此外，前面的这些步骤是完全公开透明的，你们也可以各自独立计算，而后面的步骤则需要交给第三方。

接下来可信第三方会从 $\mathbb F\setminus \{0\}$ 中随机选取 $\alpha,\beta,\gamma,\delta,\tau$ 五个参数。

接下来，可信第三方会公布 $\mathbb G_1$ 和 $\mathbb G_2$ 上的若干点，其中，被编码为 $\text{PK}$ 的点包括：
$$\alpha G_1,\{A_i(\tau)G_1\}_{i=0}^{m-1},\{B_i(\tau)G_1\}_{i=0}^{m-1},\left\{\dfrac{\beta A_i(\tau)+\alpha B_i(\tau)+C_i(\tau)}{\delta}G_1\right\}_{i=k+1}^{m-1},\left\{\dfrac{\tau ^iZ_H(\tau)}{\delta}G_1\right\}_{i=0}^{n-2}\in \mathbb G_1$$
和 $\{B_i(\tau)G_2\}_{i=0}^{m-1}\in \mathbb G_2$，此外还有盲化辅助项 $\beta G_1,\delta G_1,\beta G_2,\delta G_2$ 。

当然，$\text{PK}$ 还至少得包括 $p,\mathbb F,\mathbb G_1,\mathbb G_2,\mathbb G_T$。

而被编码为 $\text{VK}$ 的点包括：
$$\alpha G_1,\left\{\dfrac{\beta A_i(\tau)+\alpha B_i(\tau)+C_i(\tau)}{\gamma}G_1\right\}_{i=0}^{k}\in \mathbb G_1$$
和 $\beta G_2,\gamma G_2,\delta G_2\in \mathbb G_2$。

当然，$\text{VK}$ 还至少得包括 $p,\mathbb F,\mathbb G_1,\mathbb G_2,\mathbb G_T,e$ 。

公布完毕后，可信第三方随后物理销毁被生成且未公布的参数，尤其是 $\alpha,\beta,\gamma,\delta,\tau$。

容易看出 $\text{VK}$ 的信息量远小于 $\text{PK}$。
## 证明生成阶段

即 $\text{Prove}(\text{PK},\boldsymbol x,\boldsymbol w)\to\pi$ 阶段，Alice 接受 $\text{PK}$ 和 $\boldsymbol x$，自己持有 $\boldsymbol w$。

Alice 可以快速利用 $(A\boldsymbol z)\circ (B\boldsymbol z)=C\boldsymbol z$ 这一约束得到完整的 $\boldsymbol z$，利用完整的 $\boldsymbol z$ 可以用公式：
$$A(X)=\displaystyle\sum_{i=0}^{m-1}z_iA_i(X)$$
$$B(X)=\displaystyle\sum_{i=0}^{m-1}z_iB_i(X)$$
$$C(X)=\displaystyle\sum_{i=0}^{m-1}z_iC_i(X)$$
得到完整的 $A(X),B(X),C(X)$，并利用公式 $Q(X)=\dfrac{A(X)B(X)-C(X)}{Z_H(X)}$ 得到 $Q(X)$ 的系数（由于次数可计算得 $Q(X)$ 的次数不超过 $n-2$）：
$$Q(X)=\displaystyle\sum_{i=0}^{n-2}q_iX^i$$

然后，Alice 会从 $\mathbb F$ 中均匀随机选取 $r,s$ 两个盲化因子，计算出：
$$A'G_1=\alpha G_1+ r\delta G_1+\displaystyle\sum_{i=0}^{m-1}z_i(A_i(\tau)G_1)$$

$$B'G_2=\beta G_2+ s\delta G_2+\displaystyle\sum_{i=0}^{m-1}z_i(B_i(\tau)G_2)$$
$$C'G_1=s(A'G_1)+r\left(\beta G_1+\sum_{i=0}^{m-1}z_i(B_i(\tau)G_1)\right)+\sum_{i=k+1}^{m-1}z_i\left(\dfrac{\beta A_i(\tau)+\alpha B_i(\tau)+C_i(\tau)}{\delta}G_1\right)+\sum_{i=0}^{n-2}q_i\left(\dfrac{\tau ^iZ_H(\tau)}{\delta}G_1\right)$$
（这里的计算式实际上是 $A'B'=\alpha\beta+\gamma u_{\text{pub}}+\delta \left(u_{\text{priv}}+sA'+r(B'-s\delta)\right)$，因为 $B'-s\delta=\beta+B(\tau)$，可以节省运算，式子中写的就是 $\beta+B(\tau)$ 的形式，没有 $-rs\delta$）

将 $\pi=(A'G_1,B'G_2,C'G_1)$ 作为证书发送给 Bob。
## 验证阶段

即 $\text{Verify}(\text{VK},\boldsymbol x,\pi)\to \{0,1\}$ 阶段，Bob 接受 $\text{VK}$ 和 $\pi$，自己持有 $\boldsymbol x$。

Bob 首先计算 $u_{\text{pub}}G_1$：
$$u_{\text{pub}}G_1=\dfrac{\beta A_0(\tau)+\alpha B_0(\tau)+C_0(\tau)}{\gamma}G_1+\displaystyle\sum_{i=1}^{k}x_i\left(\dfrac{\beta A_i(\tau)+\alpha B_i(\tau)+C_i(\tau)}{\gamma}G_1\right)$$
随后验证等式是否成立：
$$e(A'G_1,B'G_2)\stackrel{?}{=}e(\alpha G_1,\beta G_2)\cdot e(u_{\text{pub}}G_1,\gamma G_2)\cdot e(C'G_1,\delta G_2)$$
其中 $e(\alpha G_1,\beta G_2)$ 也可以由可信第三方代为计算，或 Bob 在收到证明之前预先计算。

如果等式成立，$\text{Verify}$ 返回 1，Bob 相信 Alice 持有合法的 $\boldsymbol w$，否则不信。

你拍拍手，感觉这个算法还是很有道理的。

# 尾声

目前，你的协议是完整设计出来了，但你目前还并不想将它们拉去见 Alice 和 Bob，原因很简单，风险。

“以他们这种美丽的精神状态，要是找一个第三方审计找到协议的缺陷，我这个付费咨询的牌子就砸了……”你捂脸。

不论如何，你得设计一套方案，明确安全的边界，你确保了在什么前提下的安全，你的设计本意保证了什么的安全，这些都要写一套说明。

你不期待 Alice 或者 Bob 逐条审阅，但当事情出了岔子，它们就是你的保险。

你打开一页草稿纸。

“开始写吧。”

