#math

# 分析不等式

## 杰森不等式

如果 $\displaystyle f''>0$，我们有：$\color {red} {\displaystyle\frac{\int ^{b}_{a} f\left( g( x)\right)\mathrm{d} x}{( b-a)} \geqslant f\left({ \frac{\int ^{b}_{a} g( x)\mathrm{d} x}{b-a}}\right) }，$ 若 $\displaystyle f''< 0$，“ $\geqslant$ ”变为“ $\leqslant$ ”，在 $g'=0$ 时变为“ $=$ ”，$g(x)$ 取为分段常函数即得离散形式：$\forall a_i>0$，有 $\color {red} {\displaystyle\frac{\sum^{n}_{i=1} a_{i} f( x_{i})}{\sum^{n}_{i=1} a_{i}} \geqslant f\left(\frac{\sum ^{n}_{i=1} a_{i} x_{i}}{\sum^{n}_{i=1} a_{i}}\right)}$，证明如下

如果 $\displaystyle f''>0$，在点 $\displaystyle\frac{\int ^{b}{a} g( x)\mathrm{d} x}{b-a}$ 处，曲线总在切线上方^[$f(x)\geqslant f(x_0)+f'(x_0)(x-x_0)$]

$$
\begin{array}{ c }
{\displaystyle f\left( g( x)\right) \geqslant f\left({ \frac{\int ^{b}_{a} g( x)\mathrm{d} x}{b-a}}\right) +f'\left({ \frac{\int ^{b}_{a} g( x)\mathrm{d} x}{b-a}}\right)\left( g( x) -{\frac{\int ^{b}_{a} g( x)\mathrm{d} x}{b-a}}\right)}
\end{array}
$$

在 $a$ 到上积分得

$$
\begin{array}{ c }
{\displaystyle\int^{b}_{a}f(g(x))\mathrm{d}x\geqslant(b-a)f\left(\frac{\int ^{b}_{a}g(x)\mathrm{d}x}{b-a}\right)+f'\left(\frac{\int^{b}_{a}g(x)\mathrm{d}x}{b-a}\right)\left(\int^{b}_{a}g(x)\mathrm{d}x-(b-a)\frac{\int^{b}_{a}g(x)\mathrm{d}x}{b-a}\right)}
\end{array}
$$

整理后即可得到杰森不等式

> 💡下面的不等式都可由杰森不等式直接或间接证得

### 卡莱曼不等式

$$
\int ^{\infty }_{0}\exp\left(\displaystyle\frac{\int ^{x}_{0}\ln f(t)\mathrm{d} t}{x}\right)\mathrm{d} x\leqslant \mathrm{e}\int ^{\infty }_{0} f( x)\mathrm{d} x
$$

令 $\displaystyle f(t) =\frac{g( t)}{t}$ ，对 $\ln x$ 应用杰森不等式

$$
\begin{aligned} &\int ^{\infty }_{0}\mathrm{exp}\left(\frac{\int ^{x}_{0}\ln f(t)\mathrm{d} t}{x}\right)\mathrm{d} x \\=& \int ^{\infty }_{0}{{\mathrm{exp}\left(\frac{\int ^{x}_{0}(\ln g(t)-\ln t)\mathrm{d} t}{x}\right)}\mathrm{d} x}\\=& \int ^{\infty }_{0}\mathrm{exp}\left(\frac{\int ^{x}_{0}\ln g(t)\mathrm{d} t}{x}\right)\mathrm{exp}\left(\frac{\int ^{x}_{0} -\ln t\mathrm{d} t}{x}\right)\mathrm{d} x\\=& \int ^{\infty }_{0}\mathrm{exp}\left(\frac{\int ^{x}_{0}\ln g(t)\mathrm{d} t}{x}\right)\frac{\mathrm{e}}{x}\mathrm{d} x\\\leqslant& \int ^{\infty }_{0}\frac{\int ^{x}_{0} g( t)\mathrm{d} t}{x}\frac{\mathrm{e}}{x}\mathrm{d} x= \mathrm{e}\int ^{\infty }_{0}\int ^{x}_{0}\frac{g( t)}{x^{2}}\mathrm{d} t\mathrm{d} x\\=&\mathrm{e}\int ^{\infty }_{0} g( t)\int ^{+\infty }_{t}\frac{1}{x^{2}}\mathrm{d} x\mathrm{d} t\\=&\mathrm{e}\int ^{\infty }_{0} f(t)t\frac{1}{t}\mathrm{d} t=\mathrm{e}\int ^{\infty }_{0} f(x)\mathrm{d} x \end{aligned}
$$

### 加权平均不等式

$$
\color{red}{\frac{ax+by}{a+b} \geqslant x^{\frac{a}{a+b}} y^{\frac{b}{a+b}}}
$$

对 $\ln x$ 应用杰森不等式得到加权平均不等式

$$
\begin{array}{c}
\ln\left(\displaystyle{ \frac{\int ^{a+b}_{0} g( z)\mathrm{d} z}{a+b}}\right) \geqslant \displaystyle{}\frac{\int ^{a+b}_{0}\ln g( z)\mathrm{d} z}{a+b}\\g( z) =\begin{cases}x & 0< z< a\\
y & a< z< a+b\end{cases}\\
\ln\left(\displaystyle{}\frac{ax+by}{a+b}\right) \geqslant\displaystyle{} \frac{a\ln x+b\ln y}{a+b} =\ln\left( x^{\frac{a}{a+b}} y^{\frac{b}{a+b}}\right)\end{array}
$$

### 交换幂不等式

$$
x^x+y^y\geqslant x^y+y^x
$$

假设 $\displaystyle x\geqslant y$，当 $\displaystyle x\geqslant 1$，$\displaystyle f( t) =t^{y}\left( t^{x-y} -1\right)$ 在 $t>1$ 时为增函数且大于0，在 $t<1$ 时小于 $0$，所以 $\displaystyle f( x) \geqslant f( y)$，当 $\displaystyle 1 >x\geqslant y >0$，利用加权平均不等式

$$
\begin{aligned} & \frac{x^{x} +y^{y}}{x^{y} +y^{x}}\geqslant 1\\\Leftarrow  & \frac{y^{x}}{x^{y} +y^{x}}\left(\frac{x}{y}\right)^{x} +\frac{x^{y}}{x^{y} +y^{x}}\left(\frac{x}{y}\right)^{-y} \geqslant 1\\\Leftarrow  & \left(\frac{x}{y}\right)^{\displaystyle\frac{xy^{x} -yx^{y}}{x^{y} +y^{x}}} \geqslant 1\\\Leftarrow  & xy^{x} -yx^{y} \geqslant 0\\\Leftarrow  & \frac{\ln x}{1-x} \geqslant \frac{\ln y}{1-y}\\\Leftarrow  & \frac{\mathrm{d}\left(\displaystyle\frac{\ln x}{1-x}\right)}{\mathrm{d} x} \geqslant 0\end{aligned}
$$

### 赫尔德不等式
$$
\color{red}\int ^{h}_{l}| f(x)g(x)| dx\leq \left(\int ^{h}_{l}| f(x)| ^{p} dx\right)^{\frac{1}{p}}\left(\int ^{h}_{l}| g(x)| ^{q} dx\right)^{\frac{1}{q}}
$$

其中 $p,q>0，\displaystyle\frac{1}{p} +\frac{1}{q} = 1$，利用加权平均不等式

$$
\begin{aligned}
\Leftarrow  & {\displaystyle \int\nolimits ^{h}_{l}\left| \frac{f(x)^{p}}{{\textstyle \left(\int ^{h}_{l}| f(x)| ^{p} dx\right)}}\right| ^{\frac{1}{p}}}\left| \frac{g(x)^{q}}{{\textstyle \left(\int ^{h}_{l}| g(x)| ^{q} dx\right)}}\right|  ^{\frac{1}{q}} dx\leq 1\\
\Leftarrow  & {\displaystyle \int\nolimits ^{h}_{l}\frac{1}{p}\left| \frac{f(x)^{p}}{{\textstyle \left(\int ^{h}_{l}| f(x)| ^{p} dx\right)}}\right| } +\frac{1}{q}\left| \frac{g(x)^{q}}{{\textstyle \left(\int ^{h}_{l}| g(x)| ^{q} dx\right)}}\right| dx=1\\
\Leftarrow  & \frac{1}{p} +\frac{1}{q} =1
\end{aligned}
$$