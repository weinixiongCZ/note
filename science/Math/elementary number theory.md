#数学

- [[Elementary Number Theory.pdf]]

# 整除

如果 $a = qb + r$ ， 那么 $\mathrm{gcd}(a, b) = \mathrm{gcd}(b, r)$。 证明如下
1. $a=qb+r$，所以 $b,r$ 的公因子是 $a$ 的因子，因此也是 $a,b$ 的公因子；
2. $r=a-qb$，所以 $a,b$ 的公因子是 $r$ 的因子，因此也是 $b,r$ 的公因子；

因此数对 $a,b$ 与 $b,r$ 有相同的公因子，所以 $\mathrm{gcd}(a,b)=\mathrm{gcd}(b,r)$。由此可以证明辗转相除法。

再由辗转相除法可证得：存在 $\displaystyle u,v\in \mathbb{Z}$，使得 $\displaystyle a,b$ 的最大公因数 $\color{red}{(a,b)=ua+vb}$

同时可以证明若存在 $\displaystyle u,v\in \mathbb{Z}$，使得 $ua+vb=1$，则 $a,b$ 互质。

[[Elementary Number Theory.pdf#page=26|两个数的最大公因数与最小公倍数之积等于这两个数之积]]

# 质数

[[Elementary Number Theory.pdf#page=35|艾森斯坦不可约判据]]：
对于整系数多项式 $f(x) = a_0 + a_1 x + \cdots+ a_n x^n$，若存在质数 $p$， 整除 $a_0,a_1,\cdots ,a_{n-1}$，但不能整除 $a_n$，$p^2$ 不能整除 $a_0$，则$f(x)$ 不可约。

质数阶分圆多项式：$f(x)=1+x+x^2+\cdots+x^{p-1}$ [[Elementary Number Theory.pdf#page=35|不可约]]。

[[Elementary Number Theory.pdf#page=44|费马数]]：
如果 $2^m+1$ 是质数，那么 $m$ 具有 $2^n$ 的形式 。

[[Elementary Number Theory.pdf#page=45|梅森数]]：
如果 $m>1$，且$a^m-1$ 是质数，那么 $a=2$，且 $m$ 是质数。

如果 $p$ 是质数，且$p^2+2$ 是质数，那么 $p=3$ , 若 $p\neq 3$ ，则 $p=3q \pm 1,p^2+1=9q^2 \pm 6q+3$

如果 $p$ 是质数，且$p^e||n!$ 是质数，那么 $e=\lfloor n/p\rfloor+\lfloor n/p^2\rfloor +\lfloor n/p^3\rfloor+\cdots$，证明思路是换一种求和方式(类似交换积分次序)。

# 同余

若 $\displaystyle ( m,n) =1$，连续的 $m$ 个整数与 $\displaystyle n$ 的乘积的结果仍属于 $\bmod m$ 的 $m$ 个不同剩余类

## 瓦利斯定理
$(p-1)!+1 \bmod p=0 \Leftrightarrow p$ 是质数

若 $(p-1)!+1 \bmod p=0$，则 $(p-1)!$ 与 $p$ 互质，即 $p$ 与小于 $p$ 的所有正数互质，所以 $p$ 是质数。

由于 $\displaystyle p$ 与 $\displaystyle 1\sim p-1$ 间的任何一个数互质，所以对于 $\displaystyle 1\sim p-1$ 这连续的 $\displaystyle p-1$ 个数与 $\displaystyle 1\sim p-1$ 间的任何一个数之积属于 $\displaystyle p-1$ 个不同剩余类，其中不包括 $\displaystyle 0$ 剩余类，所以必然包括 $\displaystyle 1$ 剩余类，若 $\displaystyle ab\equiv 1\bmod p$，记 $\displaystyle b=a^{-1}_{p}$ 称为 $\displaystyle a$ 的$\bmod p$ 倒数，易得 $\displaystyle 1^{-1}_{p} =1，\displaystyle ( p-1)^{-1}_{p} =p-1$，其他数的  $\displaystyle \bmod p$ 倒数不是本身，在剩下的 $\displaystyle p-4$ 个数中，所以 $( p-1) !\equiv \overbrace{1\times1 \cdots }^{\frac{p-3}{2} \text{对}1\times1}( p-1) \equiv p-1\equiv -1\bmod p$


## 欧拉函数

$\displaystyle {\displaystyle Z_{n}}$ 是 $\displaystyle n$ 的互质剩余类，$\displaystyle \varphi ( n$)为 ${\displaystyle Z_{n}}$ 的元素个数，$( m,l) =1$，如果 $t\in Z_{ml}$，则 $\displaystyle t\in Z_{m}$ 且 $\displaystyle t\in Z_{l}$，所以 $\displaystyle \varphi ( ml) =\varphi ( m) \varphi ( l)$。由于 $\displaystyle \varphi \left( p^{v}\right) =p^{v}\left( 1-p^{-1}\right)$，所以 $\color {red} {\displaystyle \varphi ( n) =n\prod ( 1-p^{-1}_{i})}$


### 正整数的一种分解

将满足 $\displaystyle 1\leq k\leq n$ 的正整数 $\displaystyle k$ 按 $\displaystyle ( k,n)$ 的值分类，设$\displaystyle ab=n，\displaystyle A( a) =\{\frac{k}{n} \mid ( k,n) =a,1\leq k\leq n\}，\displaystyle B( b) =\{\frac{l}{b} \mid ( l,b) =1,1\leq l\leq b\}$，按照定义知 $\displaystyle | B( b)| =\varphi ( b)$，易证 $\displaystyle A=B$，所以 $n=\sum ^{n}_{a\mid n}| A( a)| =\sum ^{n}_{a\mid n}| B( b)| =\sum ^{n}_{b\mid n} \varphi ( b)$


# 单位分数

## 莱布尼茨三角

$\begin{gathered}\end{gathered}$$\begin{gathered}a_{n,k}+a_{n,k+1}=a_{n-1,k}&a_{n,k} =({(n+1)\mathrm{C}^{k}_{n}})^{-1}\end{gathered}$
$$
\begin{array}{ c c c c c c c c c }
   &  &  &  & {\displaystyle \frac{1}{1}} &  &  &  & \\
   &  &  & {\displaystyle \frac{1}{2}} &  & {\displaystyle \frac{1}{2}} &  &  & \\
   &  & {\displaystyle \frac{1}{3}} &  & {\displaystyle \frac{1}{6}} &  & {\displaystyle \frac{1}{3}} &  & \\
   & {\displaystyle \frac{1}{4}} &  & {\displaystyle \frac{1}{12}} &  & {\displaystyle \frac{1}{12}} &  & {\displaystyle \frac{1}{4}} & \\
  {\displaystyle \cdots } &  & {\displaystyle \cdots } &  & {\displaystyle \cdots } &  & {\displaystyle \cdots } &  & {\displaystyle \cdots }
  \end{array}
$$


## 正有理数表示成分母全不相等的单位分数和

$$
\displaystyle \frac{n}{m} =\displaystyle \sum\limits ^{s}_{r=1}\frac{1}{r}+\sum ^{t}_{i=1}\frac{1}{k_{i}}\ \ \ \ \ \ \begin{cases}{\displaystyle \sum\limits ^{s}_{r=1}\frac{1}{r} < \frac{n}{m} \leqslant \sum\limits ^{s+1}_{r=1}\frac{1}{r}}\\
\displaystyle\frac{1}{k_{i}} \leqslant \frac{n}{m}-\sum\limits ^{s}_{r=1}\frac{1}{r} -\sum ^{i-1}_{j=1}\frac{1}{k_{j}} < \frac{1}{k_{i} -1} &1\leqslant i\leqslant t
\end{cases}
$$



