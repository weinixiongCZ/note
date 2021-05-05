#math

# games

## take away seeds

There are three piles of seeds. The rule is that you can only take them from one pile at a time. The one who takes the last seeds wins. Write the number of sunflower seeds as binary number, stipulate the new addition: sums are recorded as 1 for odd numbers and 0 for even numbers, no carry. The conclusion is that if and only if the sum contains 1, the precedence wins, because the largest number can control the result of each bit, the way the precedence holds is to change the maximum number so that each bit is 0, no matter what the second hand holds, it will make the result contain 1, only the precedence can make the result zero, so the precedence wins. On the contrary, the second player will win.

$$
\begin{array}{ c r r r }     & 100100000110 & \Large\longrightarrow   & 011001111101\\    + & 11001011110  &     + & 11001011110\\    + & 100011       &     + & 100011\\    \hline    = & 111101111011 &     = & 000000000000\\    \end{array}
$$

egs：The above equation indicates that the numbers of seeds the precedence needs to  take away is $100100000110-011001111101$

# Combinatorial

## No one is sitting in the corresponding seat

People with numbers $1\sim n$ sit in seats with $1\sim n$, No one is sitting in the corresponding seat. Suppose there are $f_n$ cases, Let's construct recursive equation, The first can sit in $2 \sim n$ seats, suppose first sit in second seat, this case can be divided to two cases: one is second sit in first seat, there are $f_{n-2}$ cases, the other is second not sit in first seat, that is people with numbers $2,3,...,n$ not sit in seats with $1,3,...,n$, there are $f_{n-1}$ cases, so the recursive equation is $f_{n} =( n-1)( f_{n-1} +f_{n-2})$

$$
\begin{gathered}
f_{n} =( n-1)( f_{n-1} +f_{n-2})\\
f_{n} -nf_{n-1} =-\left( f_{n-1} -( n-1) f_{n-2}\right)\\
f_{n} -nf_{n-1} =( -1)^{n-2}( f_{2} -2f_{1}) =( -1)^{n}\\
\displaystyle\frac{f_{n}}{n!} -\frac{f_{n-1}}{( n-1) !} =\frac{( -1)^{n}}{n!}\\
\displaystyle\frac{f_{n}}{n!} =\sum ^{n}_{2}\frac{( -1)^{k}}{k!} =\sum ^{n}_{0}\frac{( -1)^{k}}{k!}\\
\displaystyle\color{red}{f_{n} =n!\left( \sum ^{n}_{k=0}\frac{( -1)^{k}}{k!}\right)}
\end{gathered}
$$