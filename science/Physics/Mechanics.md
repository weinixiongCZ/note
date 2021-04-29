- [[01力学.pdf]]

#物理

# Celestial mechanics

## Kepler's three laws

1. [[elementary geometry#Ellipse|Ellipse]] Orbit: ${\displaystyle \color{red} r=\frac{p}{1+e\cos \theta }}$
2. The relationship between the period and the semi-major axis of the orbit of a planet in a homologous system: ${\displaystyle\color{red} \frac{T^{2}}{a^{3}} =C_{2}}$（ $C_{2}$  is only associated with stars）
3. area velocity: $\color{red} r{\displaystyle ^{2}\frac{\mathrm{d} \theta }{\mathrm{d} t} =C_{1}}$（ $C_{1}$ A is only associated with planet）

## Newton's Law of Gravitation

long axis: ${\displaystyle a=\frac{2p}{1-e^2}}$, short axis: $b=a\sqrt{1-e^2}$, area: $\displaystyle S=\frac{\pi ab}{4}$

$$
\begin{gathered}
a_{r} ={\frac{\mathrm{d}^{2} r}{\mathrm{d} t^{2}} -r\left(\frac{\mathrm{d} \theta }{\mathrm{d} t}\right)^{2}}\\
{\displaystyle \frac{\mathrm{d} r}{\mathrm{d} t} =\frac{ep\sin \theta }{( 1+e\cos \theta )^{2}}\frac{\mathrm{d} \theta }{\mathrm{d} t} =\frac{er^{2}\sin \theta }{p}\frac{\mathrm{d} \theta }{\mathrm{d} t} =\frac{eC_{1}\sin \theta }{p}}\\
{\displaystyle \frac{\mathrm{d}^{2} r}{\mathrm{d} t^{2}} =\frac{eC_{1}\cos \theta }{p}\frac{\mathrm{d} \theta }{\mathrm{d} t} =\frac{C_{1}\left(\frac{p}{r} -1\right)}{p}\frac{{ C_{1}}}{r{ ^{2}}} =\frac{{ C^{2}_{1}}}{r^{3}} -\frac{{ C^{2}_{1}}}{pr^{2}}}\\
{ a_{r} =\frac{{ C^{2}_{1}}}{r^{3}} -\frac{{C^{2}_{1}}}{pr^{2}}} -r{ \left(\frac{{ C_{1}}}{r{ ^{2}}}\right)^{2} =-\frac{{ C^{2}_{1}}}{pr^{2}}}\\
T =\frac{{\pi ab}/{4}}{{C_{1}}/{2}} =\frac{\pi\displaystyle\frac{2p}{1-e^{2}}\frac{2p}{1-e^{2}}\sqrt{1-e^{2}}}{2C_{1}}  =\frac{2\pi p^{2}}{C_{1}\left( 1-e^{2}\right)^{\frac{3}{2}}} \\
 C_{2} ={ \frac{T^{2}}{a^{3}} =}\frac{\pi ^{2} p}{2{ C^{2}_{1}}}{\ \ }
{ a_{r} =-\frac{\frac{\pi ^{2} p}{2{ C_{2}}}}{pr^{2}} =-\frac{\pi ^{2}}{{ 2C_{2}} r^{2}}}
\end{gathered}
$$

According to Newton's second law: $F=ma_r ={\displaystyle -\frac{m\pi ^2}{{ 2C_2} r^2}}$; According to Newton's third law: $F={\displaystyle -\frac{M\pi ^{2}}{{\displaystyle 2C_{3}} r^{2}}}$, $C_{3}$ A is only associated with planet, we get: $M{ C_2 =} m{ C_3},  0=\displaystyle{ \frac{\mathrm{d} M{ C_2}}{\mathrm{d} m}} ={ \frac{\mathrm{d} m{ C_3}}{\mathrm{d} m}}$, $M C_2= m C_3 =C_4$,   $\displaystyle {\displaystyle C_{4}}$ is not related to either $M$ or $m$; To sum up the above

$$
\color{red}{F={\displaystyle-\frac{GMm}{r^2}}}
$$

## Planetary Trajectory

Konwn: planet angular-momentum $L$, energy $E$, $G$, star's $M$, planet's $m$

$$
\begin{gathered} v^{2} =v^{2}_{r} +v^{2}_{\tau } =\left(\frac{\mathrm{d} r}{\mathrm{d} t}\right)^{2} +\left( r\frac{\mathrm{d} \theta }{\mathrm{d} t}\right)^{2}\\ \frac{1}{2} v^{2} -\frac{GM}{r} =\frac{E}{m}\\ r^{2}\frac{\mathrm{d} \theta }{\mathrm{d} t} =\frac{L}{m}\\ 2\left(\frac{E}{m} +\frac{GM}{r}\right) =\left(\frac{\mathrm{d} r}{r^{2}\frac{\mathrm{d} \theta }{L/m}}\right)^{2} +\left(\frac{L/m}{r}\right)^{2}\\ \mathrm{d} \theta =\frac{L}{mr^{2}}\frac{\mathrm{d} r}{{\sqrt{2\left(\frac{E}{m} +\frac{GM}{r}\right) -\left(\frac{L/m}{r}\right)^{2}}}} \end{gathered}
$$

Discriminant of The quadratic functions $\displaystyle f\left(\frac{1}{r}\right) =-\frac{L^{2}}{m^{2}}\frac{1}{r^{2}} +\frac{2GM}{r} +\frac{2E}{m}$ inside the root sign  is $\displaystyle 4G^{2} M^{2} +\frac{8EL^{2}}{m^{3}}$, If the stellar radius is neglected, the critical energy for non-squall is $\displaystyle E_{0} =-\frac{G^{2} M^{2} m^{3}}{2L^{2}}$. According to the properties of the quadratic function there are the following conclusions: 

1. $\displaystyle E\geqslant 0$, $\displaystyle f$ There is a positive root and a non-positive root, and the planetary trajectory is [[elementary geometry#Hyperbolic|Hyperbolic]]

2. $\displaystyle E_{0} < E< 0$, $\displaystyle f$ There are two positive roots, and the planetary trajectory is [[elementary geometry#Ellipse|Ellipse]]

3. $\displaystyle E=E_{0}$, $\displaystyle f$ There are two identical positive roots, $\displaystyle \frac{\mathrm{d} r}{\mathrm{d} \theta } =0$, the planetary trajectory is [[elementary geometry#Circle|Circle]]

4. $\displaystyle E< E_{0}$, $\displaystyle f$ There is no root, planets will fall stars

# Classic Questions

## Suspended Chain Line

### General Suspension Line

![](https://gitee.com/weinixiong97/chrome-bookmark/raw/master/Image/悬链线.png)

Let the tension at the lowest point of the rope be $T$, According to the relationship between gravity and tension

$$
\begin{gathered}
\frac{\rho g\int\nolimits ^{x}_{0}\sqrt{1+y^{\prime 2}}\mathrm{d} t}{T} =y'\\
y''=C\sqrt{1+y^{\prime 2}}\\
y'^{\prime 2} =C^{2}\left( 1+y^{\prime 2}\right)\\
y'''=C^{2} y'\\
y'=C_{1}\mathrm{e}^{Cx} -C_{1}\mathrm{e}^{-Cx}
\end{gathered}
$$

Bringing the result of the fifth line into the second line gives $C_1=1/2$, Suspended chain line equation: $\displaystyle y=\frac{\cosh Cx-1}{C}$, $C$ is determined by rope length, span and rope end drop