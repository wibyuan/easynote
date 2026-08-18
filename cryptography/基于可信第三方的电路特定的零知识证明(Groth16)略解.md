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
>一个在定义域 $\mathbb N^+$ 上恒为正的函数 $f(x)$ 是**可忽略**的，当且仅当对任意 $\mathbb R[x]$ 上的多项式 $p(x)$：
>$$\lim_{x\to+\infty}p(x)f(x)=0$$
>全体可忽略函数组成的集合记作 $\text{negl}(x)$。

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

完备性，即如果 Alice 确实知道一个满足要求的 $\boldsymbol w$，那么按照流程走，生成的 $\pi$ 不被 $\text{Verify}(\text{VK},\boldsymbol x,\pi)$ 的接受的概率是可忽略的，即按流程走几乎必然被接受。

知识可靠性，即如果 Alice 确实不知道一个满足要求的 $\boldsymbol w$，那么运行任意概率多项式算法，生成的 $\pi^*$ 被 $\text{Verify}(\text{VK},\boldsymbol x,\pi^*)$ 的接受的概率是可忽略的，即伪造证明几乎必然不被接受。

零知识性，即 Bob 从 Alice 的证明 $\pi$ 中，无法获得任何关于寻找 $C(\boldsymbol x,\boldsymbol w)=1$ 的解 $\boldsymbol w$ 的辅助信息。

此外， Bob 另外提出了一个要求，他表示，自己那方没有 Alice 那边的算力，因此希望自己这边的算力比较轻量，不过你当前连方案都没设计出来，你勉强表示重视，但暂时搁置了。

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

零值测试可以等价推导出等值检查。

考虑条件选择器，$\begin{cases}c\cdot (c-1)=0\\c\cdot(a-b)=(z-b)\end{cases}$，不难看出，当 $c=0$ 时，$z=b$，当 $c=1$ 时，$z=a$。

位拆分，$\begin{cases}{b_i}\cdot(b_i-1)=0&0\le i\le\lfloor\log_2 p\rfloor\\x\cdot 1=\displaystyle\sum_{i=0}^{\lfloor \log_2 p\rfloor}b_i 2^i\end{cases}$

而随机存取可以用条件选择器来实现内存读写。

因此，你看出来了，这个简单的 $(A\boldsymbol z)\circ (B\boldsymbol z)=C\boldsymbol z$ 确实可以实现任意组合逻辑。

你向 Alice 和 Bob 表示，你看看，你们的程序 $\mathcal C$ 就可以被这样拆成逻辑门来表示，不如我们以后就管 $\mathcal C$ 叫**电路**吧，他们同意了。

现在问题确实变得标准化了，但问题还是没变，怎么把证书发过去，既让 Bob 相信，又不暴露信息呢？

## Schwartz-Zippel 引理

你注意到一个事情，一个 $d$ 次多项式，它在模 $p$ 有限域中，至多只有 $d$ 个根。

换句话说：

>**定理（单变量下的 Schwartz-Zippel 引理）**
>
>如果 $\mathbb F$ 是模 $p$ 有限域， $f(x)\in \mathbb F[x]$ 是 $d$ 次非零多项式。
>
>在 $\mathbb F$ 中随机取一个元素 $\alpha$，$f(\alpha)=0$ 的概率不大于 $\dfrac d{p}$  。

**证明：**

由于 $f(x)$ 在 $\mathbb F$ 中至多有 $d$ 个根，在 $\mathbb F$ 中随机取一个元素 $\alpha$，恰好取中一个根的概率不大于 $\dfrac d{p}$  。$\blacksquare$

反过来，对于一个多项式 $f(x)$，如果它不是 0 多项式，你只需要知道 $f(\alpha)$ 的值，其中 $\alpha$ 是随机的，你错误地判断它是 0 多项式的概率是 $\dfrac dp$，而 $p$ 是 $2^{2\kappa}$ 量级，因此，错误判断的概率是可以忽略的。

类似地，也有多变量下的形式，你感觉比较容易理解，用归纳法做一个扩展即可，先记下，说不定什么时候会用到。

>**定理（多元 Schwartz-Zippel 引理）**
>
>如果 $\mathbb F$ 是模 $p$ 有限域， $f(x_1,x_2,\cdots,x_v)\in \mathbb F[x_1,x_2,\cdots,x_v]$ 是总次数为 $d$ 次非零多项式。
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

顺便定义一个消失多项式 $Z_H(x)\in \mathbb F[x]$：

$$Z_H(x)=\prod_{i=0}^{n-1}(x-\omega_i)$$
它可以快速对 $\mathbb F^{n\times m}$ 上的矩阵 $A$ 生成 $m$ 个不超过 $n-1$ 次的多项式，设 $a_{i,j}$ 表示 $A$ 第 $i$ 行第 $j$ 列的值，其中第 $j$ 个多项式 $A_j$ 满足，对任意 $i\in\{0,1,\cdots,n-1\}$ 都有：
$$A_j(\omega_i)=a_{i,j}$$
然后设总多项式 $A(x)$ 满足：
$$A(x)=\displaystyle\sum_{i=0}^{m-1}z_iA_i(x)$$
然后，对 $B,C$ 以同样的方法生成它们的总多项式 $B(x),C(x)$。

由此我们就有多项式转化，即 $(A\boldsymbol z)\circ (B\boldsymbol z)=C\boldsymbol z$ 等价于 $A(x)B(x)-C(x)$ 在 $x\in H$ 时总是为 0。

$A(x)B(x)-C(x)$ 在 $x\in H$ 时总是为 0 意味着什么呢？

意味着存在多项式 $Q(x)$，使得 $A(x)B(x)-C(x)-Q(x)Z_H(x)\equiv 0$，恒等于 0。

但是，$A(x),B(x),C(x),Q(x)$ 在这里不再是公开信息了，它是只有 Alice 可以计算的信息，因此进行拆分。

不妨设 $A_{\text{pub}}(x)=\displaystyle\sum_{i=0}^k z_iA_i(x)=A_0(x)+\displaystyle\sum_{i=1}^k x_iA_i(x)$，和 $A_{\text{priv}}(x)=A(x)-A_{\text{pub}}(x)$。
同理有 $B_{\text{pub}}(x),C_{\text{pub}}(x),B_{\text{priv}}(x),C_{\text{priv}}(x)$。

>**定理（零知识证明的多项式转化）**
>
>对于约束 $\mathcal C(\boldsymbol x,\boldsymbol w)=1$，其中 $\mathcal C:\mathbb F^k\times \mathbb F^{l}\to \{0,1\}$， $\boldsymbol x=\begin{pmatrix}x_1&x_2&\cdots&x_k\end{pmatrix}^T\in \mathbb F^k$ 和 $\boldsymbol w=\begin{pmatrix}w_1&w_2&\cdots&w_l\end{pmatrix}^T\in \mathbb F^l$ 。
>
>其中，$\mathbb F[x]$ 上的多项式 $Z_H(x),A_{\text{pub}}(x),B_{\text{pub}}(x),C_{\text{pub}}(x)$ 是 Alice 和 Bob 共同知晓的公开信息。
>
>如果 Alice 拥有 $\mathbb F[x]$ 上的多项式 $A_{\text{priv}}(x),B_{\text{priv}}(x),C_{\text{priv}}(x),Q(x)$，并使得：
>$$(A_{\text{pub}}(x)+A_{\text{priv}}(x))\cdot (B_{\text{pub}}(x)+B_{\text{priv}}(x))-(C_{\text{pub}}(x)+C_{\text{priv}}(x))-Q(x)Z_H(x)\equiv 0$$
>其中 $A_{\text{priv}},B_{\text{priv}},C_{\text{priv}}$  Alice 不能随意构造，而必须以同一个线性组合系数 $\begin{pmatrix}z_{k+1}&z_{k+2}&\cdots&z_{m-1}\end{pmatrix}^T\in \mathbb F^{m-k-1}$ 和公共信息如下构造：
>$$A_{\text{priv}}(x)=\displaystyle\sum_{i=k+1}^{m-1} z_iA_i(x)$$
>$$B_{\text{priv}}(x)=\displaystyle\sum_{i=k+1}^{m-1} z_iB_i(x)$$
>$$C_{\text{priv}}(x)=\displaystyle\sum_{i=k+1}^{m-1} z_iC_i(x)$$
>
>则 Alice 可以利用她已知的信息获取 $\boldsymbol w$ 满足 $\mathcal C(\boldsymbol x,\boldsymbol w)=1$。

**证明：**

取线性组合系数，等价于得到了 $(A\boldsymbol z)\circ (B\boldsymbol z)=C\boldsymbol z$ 的解。$\blacksquare$

你感觉差不多了，但是还差一点点东西，你不太确定是什么。

# 多项式承诺

你最终知道了你还差什么，如果一个东西被加密了，通常情况下，它会丧失代数性质，那这种情况下，是很难把它进行各种加法和乘法的校验的，那这个问题是不是……等等！

你忽然回忆起了一些有趣的数学知识。

你告诉 Alice 和 Bob，你要从一些复杂的结构中，寻找到关于加法和乘法类似魔法一般的计算器了。

## 数学知识

你听说椭圆曲线的加法群 $\mathbb G$ 是一个困难的群，它上面未解的难题简直是批发的，其中一个是椭圆曲线的离散对数问题，具体而言：

>**困难问题（椭圆曲线上的离散对数问题）**
>
>设 $\mathbb G$ 是阶数为质数 $p$ 的循环群，其中 $p$ 约为 $2^{2\kappa}$ 量级，且 $G$ 为其生成元，从模 $p$ 有限域中均匀随机选取整数 $\alpha$，设 $\alpha G$ 为 $\alpha$ 个 $G$ 进行椭圆曲线上的点加的结果。
>
>给定群元素 $y=\alpha G$，对于任意敌手 $\mathcal A$，在已知椭圆曲线群的表达式，$G$ 和 $y$ 的前提下，运行任意概率多项式时间算法，计算出 $\alpha$ 的概率是可忽略的。

当然其实你并不知道是不是真的没有，但数学家们说没找到，你姑且假设没有。

你为此感到非常好，不是因为它很难，而是因为，在椭圆曲线上，你拿到了 $aG,bG,cG$，你把它加起来就可以判断 $a+b\stackrel{?}{=}c$ 是否成立，但你却完全无法得到 $a,b,c$。

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

你盯着 $A(x)B(x)-C(x)-Q(x)Z_H(x)\equiv 0$ 发呆。

你想象着你代入了一个随机值 $\tau$ 使得 $A(\tau)B(\tau)-C(\tau)-Q(\tau)Z_H(\tau)= 0$，但不能直接这样！

因为 Alice 可能会使得 $A(x),B(x),C(x)$ 不是真正由公开信息线性组合而来的。

这怎么破解呢？

你灵光一闪，引入了两个随机偏移量 $\alpha,\beta\in\mathbb F\setminus \{0\}$。

你注意到 $(A(\tau)+\alpha)(B(\tau)+\beta)=A(\tau)B(\tau)+\beta A(\tau)+\alpha B(\tau)+\alpha\beta$。

那么 $A(\tau)B(\tau)-C(\tau)-Q(\tau)Z_H(\tau)= 0$ 可以简单地变形一下：
$$(A(\tau)+\alpha)(B(\tau)+\beta)=\alpha\beta+(\beta A(\tau)+\alpha B(\tau)+C(\tau))+Q(\tau)Z_H(\tau)$$
这样子，$A(x),B(x),C(x)$ 就被搅在一起了！如果 Alice 用 $A_i,B_i,C_i$ 的不同或无效的线性组合，看起来，有了 $\alpha,\beta$，余项就会搅在一起干扰校验！

你的眉头舒缓了，但你还是觉得差一点。
## 分离公私

你还是找到了你差在哪里。

Alice 虽然被迫使用同一组线性组合，但她仍然有可能伪造 $\boldsymbol x$，或者将 $\boldsymbol z$ 的其它部分和 $\boldsymbol x,Q(x)$ 搅合在一起，必须堵死这个漏洞！

你眉头一皱，展开了式子：

$$(A(\tau)+\alpha)(B(\tau)+\beta)=\alpha\beta+\sum_{i=0}^{m-1}z_i(\beta A_i(\tau)+\alpha B_i(\tau)+C_i(\tau))+Q(\tau)Z_H(\tau)$$

你灵光一闪，引入了两个随机偏移量 $\gamma,\delta\in \mathbb F\setminus\{0\}$  使得 $\gamma\ne \delta$，并令：
$$u_{\text{pub}}=\sum_{i=0}^kz_i\dfrac{\beta A_i(\tau)+\alpha B_i(\tau)+C_i(\tau)}{\gamma}$$
$$u_{\text{priv}}=\dfrac{Q(\tau)Z_H(\tau)}{\delta}+\sum_{i=k+1}^{m-1}z_i\dfrac{\beta A_i(\tau)+\alpha B_i(\tau)+C_i(\tau)}{\delta}$$
然后就有：
$$(A(\tau)+\alpha)(B(\tau)+\beta)=\alpha\beta+\gamma u_{\text{pub}}+\delta u_{\text{priv}}$$
其中 $u_{\text{pub}}$ 控制的信息直接由 Bob 算好，不给 Alice 机会。

现在 Alice 理论上难以伪造了，但你还是莫名有些不安。

再想想。
## 加入盲化

你明白了，Alice 虽然理论上难以伪造了，但仍然有一个问题。

Alice 和 Bob 可能在同一个电路上进行多次证明。

每次，$\alpha,\beta,\gamma,\delta,\tau$ 都是固定的。

那么此时，$A(\tau)+\alpha$ 和 $B(\tau)+\beta$ 的统计规律就可能泄露隐私，有没有比较轻量级的办法，可以让 Alice 在每次生成的时候都加入一点盲化呢？

欸，不妨让 Alice 每次生成的时候都选取 $r,s\in \mathbb F$。

不妨设 $A'=A(\tau)+\alpha+r\delta$ 且 $B'=B(\tau)+\beta+s\delta$。

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
$$\{A_i(x)\}_{i=0}^{m-1},\{B_i(x)\}_{i=0}^{m-1},\{C_i(x)\}_{i=0}^{m-1},Z_H(x)$$
你提醒 Alice 和 Bob，这些参数最好选择以确定的简明算法生成的参数，以防止留有后门，一个臭名昭著的例子是 Dual_EC_DRBG，可以用它来观察那些不那么透明的参数会造成哪些恶果；此外，前面的这些步骤是完全公开透明的，你们也可以各自独立计算，而后面的步骤则需要交给第三方。

接下来可信第三方会从 $\mathbb F\setminus \{0\}$ 中随机选取 $\alpha,\beta,\gamma,\delta,\tau$ 五个参数。

接下来，可信第三方会公布 $\mathbb G_1$ 和 $\mathbb G_2$ 上的若干点，其中，被编码为 $\text{PK}$ 的点包括：
$$\alpha G_1,\{A_i(\tau)G_1\}_{i=0}^{m-1},\{B_i(\tau)G_1\}_{i=0}^{m-1},\left\{\dfrac{\beta A_i(\tau)+\alpha B_i(\tau)+C_i(\tau)}{\delta}G_1\right\}_{i=k+1}^{m-1},\left\{\dfrac{\tau ^iZ_H(\tau)}{\delta}G_1\right\}_{i=0}^{n-2}\in \mathbb G_1$$
和 $\{B_i(\tau)G_2\}_{i=0}^{m-1}\in \mathbb G_2$，此外还有两个盲化辅助项 $\beta G_1,\delta G_1$。

当然，$\text{PK}$ 还至少得包括 $p,\mathbb F,\mathbb G_1,\mathbb G_2,\mathbb G_T,G_1,G_2$。

而被编码为 $\text{VK}$ 的点包括：
$$\alpha G_1,\left\{\dfrac{\beta A_i(\tau)+\alpha B_i(\tau)+C_i(\tau)}{\gamma}G_1\right\}_{i=0}^{k}\in \mathbb G_1$$
和 $\beta G_2,\gamma G_2,\delta G_2\in \mathbb G_2$。

当然，$\text{VK}$ 还至少得包括 $p,\mathbb F,\mathbb G_1,\mathbb G_2,\mathbb G_T,G_1,G_2,e$ 。

公布完毕后，可信第三方随后物理销毁被生成且未公布的参数，尤其是 $\alpha,\beta,\gamma,\delta,\tau$。

容易看出 $\text{VK}$ 的信息量远小于 $\text{PK}$。
## 证明生成阶段

即 $\text{Prove}(\text{PK},\boldsymbol x,\boldsymbol w)\to\pi$ 阶段，Alice 接受 $\text{PK}$ 和 $\boldsymbol x$，自己持有 $\boldsymbol w$。

Alice 可以快速利用 $(A\boldsymbol z)\circ (B\boldsymbol z)=C\boldsymbol z$ 这一约束得到完整的 $\boldsymbol z$，利用完整的 $\boldsymbol z$ 可以用公式：
$$A(x)=\displaystyle\sum_{i=0}^{m-1}z_iA_i(x)$$
$$B(x)=\displaystyle\sum_{i=0}^{m-1}z_iB_i(x)$$
$$C(x)=\displaystyle\sum_{i=0}^{m-1}z_iC_i(x)$$
得到完整的 $A(x),B(x),C(x)$，并利用公式 $Q(x)=\dfrac{A(x)B(x)-C(x)}{Z_H(x)}$ 得到 $Q(x)$ 的系数：
$$Q(x)=\displaystyle\sum_{i=0}^{n-2}q_ix^i$$

然后，Alice 会从 $\mathbb F$ 中均匀随机选取 $r,s$ 两个盲化因子，计算出：
$$A'G_1=\alpha G_1+ r\delta G_1+\displaystyle\sum_{i=0}^{m-1}z_i(A_i(\tau)G_1)$$

$$B'G_2=\beta G_2+ s\delta G_2+\displaystyle\sum_{i=0}^{m-1}z_i(B_i(\tau)G_2)$$
$$C'G_1=s(A'G_1)+r\left(\beta G_1+\sum_{i=0}^{m-1}z_i(B_i(\tau)G_1)\right)+\sum_{i=k+1}^{m-1}z_i\left(\dfrac{\beta A_i(\tau)+\alpha B_i(\tau)+C_i(\tau)}{\delta}G_1\right)+\sum_{i=0}^{n-2}q_i\left(\dfrac{\tau ^iZ_H(\tau)}{\delta}G_1\right)$$
将 $\pi=(A'G_1,B'G_2,C'G_1)$ 作为证书发送给 Bob。
## 验证阶段

即 $\text{Verify}(\text{VK},\boldsymbol x,\pi)\to \{0,1\}$ 阶段，Bob 接受 $\text{VK}$ 和 $\pi$，自己持有 $\boldsymbol x$。

Bob 首先计算 $u_{\text{pub}}G_1$：
$$u_{\text{pub}}G_1=\dfrac{\beta A_0(\tau)+\alpha B_0(\tau)+C_0(\tau)}{\gamma}G_1+\displaystyle\sum_{i=1}^{k}x_i\left(\dfrac{\beta A_i(\tau)+\alpha B_i(\tau)+C_i(\tau)}{\gamma}G_1\right)$$
随后验证等式是否成立：
$$e(A'G_1,B'G_2)\stackrel{?}{=}e(\alpha G_1,\beta G_2)\cdot e(u_{\text{pub}}G_1,\gamma G_2)\cdot e(C'G_1,\delta G_2)$$
其中 $e(\alpha G_1,\beta G_2)$ 也可以由可信第三方代为计算。

如果等式成立，$\text{Verify}$ 返回 1，Bob 相信 Alice 持有合法的 $\boldsymbol w$，否则不信。

你感觉这个算法很有道理啊，那么，要如何蒙……啊不，严谨地展示给 Alice 和 Bob，使得他们相信你呢？
# 正确性与安全性证明

你回忆了一下一开始 Alice 和 Bob 的要求是什么。

好像是四个，完备性，即 Alice 的正确证明总能被 Bob 接受；知识可靠性，Alice 不知道 $\boldsymbol w$ 则伪证被 Bob 接受的概率可忽略；零知识性，即可信第三方可以造出没人能分清的 $(\text{PK}^*,\pi^*)$；还有高效性，让 Bob 的计算量比较小。

其中高效性这个已经可以看出来了，Bob 需要计算椭圆曲线上点的一个线性组合，还有至少三次双线性配对，那么，你注意到，如果将椭圆曲线的点加法计算、双线性配对计算和域上乘法运算看成常数值，整个计算复杂度仅与 $\boldsymbol x$ 的长度 $k$ 成正比，即 $O(k)$，与电路大小和 $\boldsymbol w$ 的长度都无关，应当还是较为高效的。

虽然你听说双线性配对计算起来比较慢，但你想了一下，Bob 只需要计算三次，应该还可以。

而且就算不高效了，我这个都已经写出来了，难道还回炉重造？你对自己说。

但其它的呢？

## 完美完备性

其中完备性在你看来是最简单的了。

>**定理（完美完备性）**
>
>在第三方可信的前提下，Alice 如果持有能使得 $\mathcal C(\boldsymbol x,\boldsymbol w)=1$ 的 $\boldsymbol w$。
>按照流程生成的证明 $\pi=\text{Prove}(\text{PK},\boldsymbol x,\boldsymbol w)$ 必定有 $\text{Verify}(\text{VK},\boldsymbol x,\pi)=1$。

**证明：**

由于前文的推导，Alice 如果持有能使得 $\mathcal C(\boldsymbol x,\boldsymbol w)=1$ 的 $\boldsymbol w$，那么 Alice 计算出的 $A'G_1,B'G_2,C'G_1$ 必然满足：
$$A'B'=\alpha\beta+\gamma u_{\text{pub}}+\delta C'$$
用双线性配对来描述，就其实是：
$$e(A'G_1,B'G_2)=e(\alpha G_1,\beta G_2)\cdot e(u_{\text{pub}}G_1,\gamma G_2)\cdot e(C'G_1,\delta G_2)$$
等式必然成立，故 $\text{Verify}(\text{VK},\boldsymbol x,\pi)=1$。$\blacksquare$

因此，Alice 如果持有 $\boldsymbol w$ 并且遵守规则，则 Alice 的证明 $\pi$ 必定被 Bob 接受。
## 知识可靠性

假设在第三方可信的前提下，Alice 在流程中仍然通过运行一个概率多项式算法以不可忽略的概率找到了一个伪证 $\pi^*$，使得 $\text{Verify}(\text{VK},\boldsymbol x,\pi^*)=1$。

你表示，Bob 呀，遇到这种情况，我一者为你悲伤，二者为你道喜呀！恭喜 Bob 可以解决难题了！

你看如果 Alice 找到了伪证 $\pi^*$ 你就可以解决离……啊？还不能？

你表示有些尴尬，你赶紧查了一下论文。

啊，啊哈哈哈，你眼珠一转，有了！

与其寻找假设，不如自己创造一个假设！

>**假设（代数群模型）**
>
>对一个 $p$ 阶椭圆曲线群 $\mathbb G$，其中 $p$ 约为 $2^{2\kappa}$ 量级，且 $\mathbb F$ 是模 $p$ 有限域，可信第三方已公开了 $P_1,P_2,\cdots,P_N$ 这些群元素，如果敌手 $\mathcal A$ 输出了一个元素 $Y\in\mathbb G$，则 $\mathcal A$ 一定已知并能同时输出一组标量系数 $\begin{pmatrix}c_1&c_2&\cdots&c_N\end{pmatrix}\in \mathbb F^N$，满足：
>$$Y=\displaystyle\sum_{i=1}^{N}c_iP_i$$

诶呀，Bob，这真不是我瞎编的。

Bob，我知道在椭圆曲线上随便找一个点是容易的，但是，如果你在椭圆曲线上随便找一个点，那么它几乎不可能满足我们那个严苛的双线性配对等式的，所以如果 Alice 是一个有点智商的人，她也会选择用线性组合的方式来制作伪证。

Bob，这真不是我乱编的，虽然你可能没有在 16 年之前的论文中看到过这个，但，但，其实，它，哦对，它是基于对椭圆曲线的正确认识而来的，所以实则很有道理！

但你回头看了一下，你好像还不够证啊！

啊……你终于找到了，诶呀，有权威背书的感觉真好。

>**困难问题（$t$-离散对数困难假设）**
>
>对两个 $p$ 阶椭圆曲线群 $\mathbb G_1,\mathbb G_2$，其中 $p$ 约为 $2^{2\kappa}$ 量级，且 $\mathbb F$ 是模 $p$ 有限域。
> 
> 其中 $\mathbb G_1$ 的生成元是 $G_1$ 和 $\mathbb G_2$ 的生成元是 $G_2$，$\tau$ 从 $\mathbb F\setminus\{0\}$ 中随机选取。
>
>给定 $G_1,\tau G_1,\tau^2 G_1,\cdots,\tau^t G_1$ 和 $G_2,\tau G_2,\tau^2 G_2,\cdots,\tau^t G_2$。
>
>敌手 $\mathcal A$ 运行概率多项式时间算法得到 $\tau$ 的概率是可忽略的。

啊，Bob 你看那些顶级密码学家也是在这蒙……啊不，严谨地定义的，你看是不是使得我的假设更加令人信服了呢？

你似乎蒙过了 Bob，你大为满意。

总之你继续开始了推导。

在此之前，你回忆了一下你的数学知识，确认了最后一个事实：

>**简单问题（有限域多项式求根）**
>
>设 $\mathbb F$ 是模质数 $p$ 下的有限域，$f(x)\in \mathbb F[x]$ 是一个次数为 $d$ 的非零多项式。
>
>则存在概率多项式时间算法，能在 $O(d\cdot \log d\cdot \log p)$ 时间复杂度内求出 $f(x)$ 在 $\mathbb F$ 中的所有根。

你感觉你脑中的一根线通了。

>**定理（知识可靠性）**
>
>在第三方可信的前提下，Alice 如果用概率多项式算法以不可忽略的概率 $\varepsilon$，生成了证明 $\pi^*$ 使得 $\text{Verify}(\text{VK},\boldsymbol x,\pi^*)=1$。
>
>并且承认代数群模型假设和$t$-离散对数困难假设为真。
>
>则存在提取器，可以使用概率多项式时间的算法以 $\varepsilon-\text{negl}(\kappa)$ 的概率从 Alice 那里提取出满足 $\mathcal C(\boldsymbol x,\boldsymbol w)=1$ 的 $\boldsymbol w$。

Bob 啊，这个提取器你可以想象成你拥有一个超能力，比如你拥有：

- 读心术，你可以读到 Alice 必须知道的知识。
- 时间回溯，如果你对一次的结果不满意你可以倒带，不过这里用不上，因为它是非交互式的。

众所周知，拥有一点超能力并不会让你变得聪明，所以如果你用提取器提取出了 $\boldsymbol w$，那这个知识产权本质上是归属于 Alice 的，也就证明了 Alice 拥有确实知识，即知识可靠性。

**证明：**

当 Alice 生成的证明 $\pi=(A^*G_1,B^*G_2,C^*G_1)$ 能够满足等式：
$$e(A^*G_1,B^*G_2)=e(\alpha G_1,\beta G_2)\cdot e(u_{\text{pub}}G_1,\gamma G_2)\cdot e(C^*G_1,\delta G_2)$$
则由 代数群模型假设 $A^*,B^*,C^*$ 必定对应一组系数展开，Bob，你动用超能力可以得到这组展开，不妨将其写为展开系数的形式：
$$A^*(\tau) = a_\alpha \alpha + a_\beta \beta + a_\delta \delta + \sum_{i=0}^{m-1} a_{A, i} A_i(\tau) + \sum_{i=0}^{m-1} a_{B, i} B_i(\tau) + \sum_{i=0}^k a_{\text{pub}, i} \frac{\beta A_i(\tau) + \alpha B_i(\tau) + C_i(\tau)}{\gamma} + \sum_{i=k+1}^{m-1} a_{\text{priv}, i} \frac{\beta A_i(\tau) + \alpha B_i(\tau) + C_i(\tau)}{\delta} + \sum_{j=0}^{n-2} a_{H, j} \frac{\tau^j Z_H(\tau)}{\delta}$$
$$B^*(\tau) = b_\beta \beta + b_\gamma \gamma + b_\delta \delta + \sum_{i=0}^{m-1} b_{B, i} B_i(\tau)$$

$$C^*(\tau) = c_\alpha \alpha + c_\beta \beta + c_\delta \delta + \sum_{i=0}^{m-1} c_{A, i} A_i(\tau) + \sum_{i=0}^{m-1} c_{B, i} B_i(\tau) + \sum_{i=0}^k c_{\text{pub}, i} \frac{\beta A_i(\tau) + \alpha B_i(\tau) + C_i(\tau)}{\gamma} + \sum_{i=k+1}^{m-1} c_{\text{priv}, i} \frac{\beta A_i(\tau) + \alpha B_i(\tau) + C_i(\tau)}{\delta} + \sum_{j=0}^{n-2} c_{H, j} \frac{\tau^j Z_H(\tau)}{\delta}$$
那么，由于 $\text{Verify}(\text{VK},\boldsymbol x,\pi^*)=1$，我们有：
$$A^* (\tau) B^*(\tau) - \alpha\beta - \sum_{i=0}^k z_i \Big( \beta A_i(\tau) + \alpha B_i(\tau) + C_i(\tau) \Big) - \delta  C^* (\tau)=0$$
虽然式子中有分式，但可以将其有理化，因此亦可等价于不超过 $3n+1$ 次多项式方程看待。

现在的问题是，如果将 $\alpha,\beta,\gamma,\delta,\tau$ 看作形式变量，多元有理分式：
$$F(\alpha,\beta,\gamma,\delta,\tau)=A^* (\tau) B^*(\tau) - \alpha\beta - \sum_{i=0}^k z_i \Big( \beta A_i(\tau) + \alpha B_i(\tau) + C_i(\tau) \Big) - \delta  C^* (\tau)$$

是否恒等于 0？

如果多元有理分式不恒等于 0 ，Alice 恰好蒙出了一组根，那么，考虑到 $F(\alpha,\beta,\gamma,\delta,\tau)\delta^2\gamma^2$ 是各项次数仍然不大于 $3n+1$ 的多元多项式，由多元 Schwartz-Zippel 引理，该情况发生的概率是可忽略的。

如果多元有理分式不恒等于 0 ，Alice 的惊世智慧发力了，找到了 $\alpha,\beta,\gamma,\delta,\tau$ 的某些性质，但是 Bob 的机会也来了，他可以随机挑一个变量，然后用超能力买通（注意这个买通是为了构造解决困难问题的反证，后续证明仍假设没有买通）可信第三方，让可信第三方出示其它变量，然后，Bob 只需要解一个不超过 $3n+1$ 次的方程就可以解决 $t$-离散对数困难问题，而由于这个问题我们假设是困难的，因此这种情况发生的概率也是可忽略的。

因此剩下的概率不可忽略，即多元有理分式 $F(\alpha,\beta,\gamma,\delta,\tau)$ 恒等于 0。

那么，不妨构造 $\boldsymbol  z'$ 和 $Q'(x),A'(x),B'(x),C'(x)$ 使得：$$\boldsymbol z'=\begin{pmatrix}1&x_1&x_2&\cdots&x_k&c_{\text{priv},k+1}&c_{\text{priv},k+2}&\cdots&c_{\text{priv},m-1}\end{pmatrix}^T\in \mathbb F^m$$$$Q'(x)=\displaystyle\sum_{i=0}^{n-2}c_{H,i}x^i$$
$$A'(x)=\displaystyle\sum_{i=0}^{m-1}{z_i}'A_i(x),B'(x)=\displaystyle\sum_{i=0}^{m-1}{z_i}'B_i(x),C'(x)=\displaystyle\sum_{i=0}^{m-1}{z_i}'C_i(x)$$
考察 $F(\alpha,\beta,\gamma,\delta,\tau)$ 的 $\alpha\beta$ 项：
$$\alpha\beta (a_\alpha b_\beta-1)$$
故 $a_\alpha b_\beta=1$，由线性放缩，不妨取 $a_{\alpha}=b_{\beta}=1$。

考虑 $F(\alpha,\beta,\gamma,\delta,\tau)$ 的 $\alpha \gamma$ 项：
$$\alpha\gamma b_\gamma a_{\alpha}$$
由于 $A^*(\tau)$ 含有 $a_\alpha$ 项必然非零，所以 $b_{\gamma}=0$ 必然成立，因此无需担心后续 $\gamma$ 和 $\gamma^{-1}$ 对消，含 $\gamma$ 的项在证明中始终为 0。

考察 $F(\alpha,\beta,\gamma,\delta,\tau)$ 的 $\alpha$ 项（不含 $\beta$ 或 $\gamma^{-1}$ 项）：
$$\alpha \left( b_\delta \delta + \sum_{i=0}^{m-1} b_{B, i} B_i(\tau) - \sum_{i=0}^k z_i B_i(\tau) - \sum_{i=k+1}^{m-1} c_{\text{priv}, i} B_i(\tau) \right)$$
因此 $B'(x)=\displaystyle\sum_{i=0}^{m-1}{z_i}'B_i(x)=\displaystyle\sum_{i=0}^{m-1}b_{B,i}B_i(x)$。
再考察 $F(\alpha,\beta,\gamma,\delta,\tau)$ 的 $\beta$ 项（不含 $\alpha$ 或 $\gamma^{-1}$ 项）：
$$\beta \left( a_\beta \beta + a_\delta \delta + \sum_{i=0}^{m-1} a_{A, i} A_i(\tau) + \sum_{i=0}^{m-1} a_{B, i} B_i(\tau) - \sum_{i=0}^k z_i A_i(\tau) - \sum_{i=k+1}^{m-1} c_{\text{priv}, i} A_i(\tau) \right)$$
因此 $A'(x)=\displaystyle\sum_{i=0}^{m-1}{z_i}'A_i(x)=\displaystyle\sum_{i=0}^{m-1}a_{A,i}A_i(x)$
再考察 $F(\alpha,\beta,\gamma,\delta,\tau)$ 中不含 $\alpha,\beta,\gamma,\delta$ 的项：
$$A'(\tau) B'(\tau) - \left( \sum_{i=0}^k z_i C_i(\tau) + \sum_{i=k+1}^{m-1} c_{\text{priv}, i} C_i(\tau) \right) - \left( \sum_{j=0}^{n-2} c_{H, j} \tau^j \right) Z_H(\tau) \equiv 0$$
也就恰好有：
$$A'(x)B'(x)-C'(x)-Q'(x)Z_H(x)\equiv 0$$
因此，也就有 $(A\boldsymbol z')\circ (B\boldsymbol z')\equiv C\boldsymbol z'$，取 $\boldsymbol w=\begin{pmatrix}c_{\text{priv},k+1}&c_{\text{priv},k+2}&\cdots&c_{\text{priv},k+l}\end{pmatrix}^T\in \mathbb F^l$，即可使得 $\mathcal C(\boldsymbol x,\boldsymbol w)=1$。因此提取器以不可忽略的概率得到了解，即证实了知识可靠性。$\blacksquare$

## 完美零知识性

此时你看向 Alice，不知道为什么，你感觉这个证明其实是有点偏爱 Alice 的，因为你忽然发现，这个流程实际上具有完美零知识性，也就是说，模拟器造出来的模拟证明根本无法被区分。

至少 Bob 算得方便了，你想着。

>**定理（完美零知识性）**
>
>在 Groth16 协议的流程中存在概率多项式时间的模拟器 $\text{Sim}$，它由两个部分 $\text{Sim}_1$ 和 $\text{Sim}_2$ 组成，其中：
>
>$\text{Sim}_1(1^{\kappa},\mathcal C)\to (\text{td},\text{PK}^*,\text{VK}^*)$ 接受安全参数 $\kappa$ 和电路 $\mathcal C$ 生成带有陷门 $\text{td}$ 的参考串 $(\text{PK}^*,\text{VK}^*)$。
>
>$\text{Sim}_2(\text{td},\boldsymbol x)\to \pi^*$ 在不输入见证 $\boldsymbol w$ 的前提下，生成模拟证明 $\pi^*$。
>
>其中设 $\mathbb F$ 是模 $p$ 有限域。
>
>设 $\mathcal R=\{(\boldsymbol x,\boldsymbol w)\in \mathbb F^k\times\mathbb F^l\mid\mathcal C(\boldsymbol x,\boldsymbol w)=1\}$ 为关系。
>
>则真实实验 $(\text{PK},\text{VK},\boldsymbol x,\text{Prove}(\text{PK},\boldsymbol x,\boldsymbol w))$ 和模拟实验 $(\text{PK}^*,\text{VK}^*,\boldsymbol x,\text{Sim}_2(\text{td},\boldsymbol x))$ 的输出分布统计完全同一，即任何算力不受限的区分器都无法区分。

你告诉 Bob，注意了啊，模拟器能制造模拟证明，是因为它有更高级的权限，例如打破第三方的可信度，在现实中，只要第三方仍然可信，再满足一点点数学假设，模拟证明就造不出来，这是由知识可靠性来决定的。

既然模拟器除了权限一点关于 $\boldsymbol w$ 知识都没有，那么这个意义上的无法区分就说明证明中确实没有透露一点关于 $\boldsymbol w$ 的信息。

**证明：**

这当然是因为模拟器从可信第三方入手简直和开了挂一样。

其中 $\text{Sim}_1(1^{\kappa},\mathcal C)\to (\text{td},\text{PK}^*,\text{VK}^*)$ 用和 $\text{Setup}(1^{\kappa},\mathcal C)\to (\text{PK},\text{VK})$ 生成 $(\text{PK},\text{VK})$ 完全一样的方法生成 $(\text{PK}^*,\text{VK}^*)$，但是保留 $(\alpha,\beta,\gamma,\delta,\tau)$ 编码进 $\text{td}$ 并输出。

此外，$\text{td}$ 还得包括 $p,\mathbb F,\mathbb G_1,\mathbb G_2,\mathbb G_T,G_1,G_2$，以及 $\{A_i(x)\}_{i=0}^k,\{B_i(x)\}_{i=0}^k,\{C_i(x)\}_{i=0}^k$，当然，这些是公开信息，写在这里只是为了说清楚信息量。

而 $\text{Sim}_2(\text{td},\boldsymbol x)\to \pi^*$ 从 $\mathbb F$，即模 $p$ 有限域中随机采样两个标量 $a,b$。

利用公开输入计算：
$$u_{\text{pub}}=\dfrac{\beta A_0(\tau)+\alpha B_0(\tau)+C_0(\tau)}{\gamma}+\sum_{i=1}^kx_i\dfrac{\beta A_i(\tau)+\alpha B_i(\tau)+C_i(\tau)}{\gamma}$$
然后利用 $\text{td}$ 提供的标量 $\delta$ 计算标量 $c$ 满足：
$$c=\delta^{-1}(ab-\alpha\beta-\gamma\cdot u_{\text{pub}})$$

然后输出模拟证明 $\pi^*=(aG_1,bG_2,cG_1)$。

这里，由于 $\text{Sim}_1$ 和 $\text{Setup}$ 的采样完全一致，故 $(\text{PK},\text{VK})$ 和 $(\text{PK}^*,\text{VK}^*)$ 的分布统计完全一致。

考虑在真实证明 $\pi$ 中的 $A'G_1$ 和模拟证明 $\pi^*$ 中的 $aG_1$，其中真实证明 $\pi$ 中：
$$A'G_1=\alpha G_1+ r\delta G_1+\displaystyle\sum_{i=0}^{m-1}z_i(A_i(\tau)G_1)$$
由于加入了独立均匀选取的盲化因子 $r$ 且 $\delta\ne 0$，故 $A'G_1$ 独立于 $\text{PK}$ 在 $\mathbb G_1$ 中服从均匀分布。

而 $aG_1$ 独立于 $\text{PK}^*$ 在 $\mathbb G_1$ 中也服从均匀分布。

因此 $(\text{PK},\text{VK},A'G_1)$ 联合分布与 $(\text{PK}^*,\text{VK}^*,aG_1)$ 联合分布相同。

考虑在真实证明 $\pi$ 中的 $B'G_2$ 和模拟证明 $\pi^*$ 中的 $bG_2$，其中真实证明 $\pi$ 中：
$$B'G_2=\beta G_2+ s\delta G_2+\displaystyle\sum_{i=0}^{m-1}z_i(B_i(\tau)G_2)$$
由于加入了独立均匀选取的盲化因子 $s$ 且 $\delta\ne 0$，由于 $s$ 是独立均匀选取的，故 $B'G_2$ 独立于 $A' G_1$ 在 $\mathbb G_2$ 中服从均匀分布。

而 $bG_2$ 也独立于 $aG_1$在 $\mathbb G_2$ 中服从均匀分布。

因此 $(\text{PK},\text{VK},A'G_1,B'G_2)$ 联合分布与 $(\text{PK}^*,\text{VK}^*,aG_1,bG_2)$ 联合分布相同。

考虑在真实证明 $\pi$ 中的 $C'G_1$ 和模拟证明 $\pi^*$ 中的 $cG_1$，其中真实证明 $\pi$ 中 $C'G_1$ 是满足关于 $P$ 的方程：
$$e(A'G_1,B'G_2){=}e(\alpha G_1,\beta G_2)\cdot e(u_{\text{pub}}G_1,\gamma G_2)\cdot e(P,\delta G_2)$$
的唯一解。

而模拟证明 $\pi^*$ 中 $cG_1$ 是满足关于 $Q$ 的方程：
$$e(aG_1,bG_2){=}e(\alpha G_1,\beta G_2)\cdot e(u_{\text{pub}}G_1,\gamma G_2)\cdot e(Q,\delta G_2)$$
的唯一解。

由于联合分布和方程形式都相同，因此 $(\text{PK},\text{VK},\pi)$ 联合分布与 $(\text{PK}^*,\text{VK}^*,\pi^*)$ 联合分布相同。即输出分布统计完全同一。$\blacksquare$

你松了一口气，也许 Alice 那边会比较好说服一点。

你提醒 Alice 和 Bob，Alice 如果要向 Bob 提交一个证明，最好将全部能被 Bob 识别的信息作为公开输入 $\boldsymbol x$ 的一部分，因为如果 $\pi=(A'G_1,B'G_2,C'G_1)$ 是一个合法的证明，任取 $u\in \mathbb F\setminus\{0\}$，$\pi^*=(u^{-1}A'G_1,uB'G_2,C'G_1)$ 也是合法的，这种情况可能会被恶意攻击者利用，但如果攻击者不能篡改 $\boldsymbol x$，通常就无法达到目的。

当然，这绝不是说前面的安全性是假的，只是现实总是复杂的，密码学要考虑很多情况的安全性。

# 尾声

在这之后，Alice 和 Bob 似乎对这个协议比较满意了，他们使用了很长一段时间，不过有的时候，也听到他们向你吐槽一些事情。

比如说他们有的时候会怀疑可信第三方是不是真的可信，为此你表示，或许可以把 $\text{Setup}$ 做成多方参与的形式，只要一方诚实地销毁了自己的参数，整个流程就是安全的，然而，你确实感觉你一开始的 $\text{Setup}$ 流程设计太过麻烦，如果拆成多方计算，需要相对复杂的流程，你感觉你的脑细胞不够用了。

此外，他们有时也会抱怨如果更换一个电路 $\mathcal C$，就得重新请第三方搞一次计算操作，这你也无奈，这是流程初始设计埋下的暗坑。

然而，有的时候你还是会回想起 Alice 和 Bob，想到这一串有趣的推导流程。