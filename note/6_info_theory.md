## Entropy

The *entropy* of a discrete random variable $X$ which takes value is defined by: 
$$
H(X) = \sum_{x\in\mathcal X} p(x)\frac{1}{\log p(x)} = \mathbb{E}[\frac{1}{\log p(x)}]
$$
The function $f(x) = \frac{1}{\log p(x)}$ is often explained in English as the *surprise*. This is in agreement with the fact that we would be more surprised by observing a value with low probability.

The *joint entropy* of two random variables $X, Y$ is given by: 
$$
H(X,Y) = \sum_{x,y\in\mathcal{X\times Y}} p(x,y)\log\frac{1}{p(x,y)}
$$
Similarly, we can define the *conditional entropy* of $Y$ given $X$: 
$$
H(Y|X) = \sum_{x,y\in \mathcal{X,Y}} p(x,y)\log \frac{1}{p(y|x)}
$$
Based on the Bayes Rule, $\log\frac{1}{p(y|x)} = \log\frac{p(x)}{p(x,y)}$. Therefore: 
$$
H(Y|X) = H(X,Y)- H(X)
$$
As mentioned before, if $X$ and $Y$ are not independent, they provide some information about each other. The mutual information measures the information about one gained from the other: 
$$
\begin{align}
I(X,Y) &= H(X) - H(X|Y)\\
&= H(Y) - H(Y|X) \\ 
&=H(X) + H(Y) - H(X,Y)
\end{align}
$$

## Source Coding

A *source coding* scheme is a mapping from the symbols $x$ in the source alphabet $\mathcal X$ to bit strings. Clearly this will have something to do with the entropy which we have been  referring to as the average number of bits of information in a random variable. 

Let the function $l(x)$ be the length of the binary string description of $x$. Consider a sequence of symbols, the binary description has the length of $l(X_1,X_2...X_n)$. 

The average bits for this sequence is $\frac{l(X_1,X_2...X_n)}{n}$. This following theorem regarding how small this average could be was stated by Shannon in $1948$. 

> **Source Coding Theorem**. For an i.i.d. sequence $X_1,X_2...X_n$ and an arbitrarily small $\epsilon > 0$. There is a source coding scheme for which: 
> $$
> \lim_{n\rightarrow \infty} \mathbb E[\frac{1}{n} l(X_1,X_2...X_n)] \leq H(X) + \epsilon
> $$
> And conversely, there is no source coding that can achieve an average less than $H(X)$ bits per symbol in expectation.

We want to assign shorter bit strings to the most probable sequences to reduce the expected length of the code. It turns out as $n$ grows large, all the probability concentrates on a much smaller subset, which is also known as the *typical set*. 

For example, consider a situation where you are flipping $n$ coins with probability $p$ coming head up. The most probable sequence will have $np$ heads and $n(1-p)$ tails. The probability of seeing that typical sentence is: 
$$
\begin{align}
& \ p^{np}\cdot (1-p)^{n(1-p)}\\
=& \ 2^{\log(p^{np}\cdot (1-p)^{n(1-p)})}\\
=& \ 2^{n(p\log p +(1-p)\log (1-p))}\\
=& \ 2^{-nH(X)}
\end{align}
$$
This example give us an idea for the definition of typical set. Formally, the $\epsilon$-typical set $A_\epsilon^{(n)}$ is the set of sequence which fit the following condition: 
$$
2^{-n(H(X) + \epsilon)}\leq p(x_1,x_2...x_n)\leq 2^{-n(H(X)-\epsilon)}
$$
We know that the sequences in the typical set contain more of the probability mass, but how much? It turns out as n grows large the typical set contains almost all of it.

> **Theorem(Asymptotic Equipartition Property)**. If $X_1,X_2...X_n$ are i.i.d., then: 
> $$
> -\frac{1}{n}\log_2p(X_1,X_2...X_n) \underset{n\rightarrow \infty}{\overset{\R}{\longrightarrow}} H(X)
> $$
> *Proof.* Through the WLLN, we have: 
> $$
> -\frac{1}{n}\sum_{i=1}^{n}\log p(X_i)\underset{n\rightarrow \infty}{\overset{\R}{\longrightarrow}} \mathbb E[\frac{1}{\log p(X)}] = H(X)
> $$
> Because $X_1,X_2...X_n$ are i.i.d: 
> $$
> -\frac{1}{n}\log_2p(X_1,X_2...X_n) = -\frac{1}{n}\sum_{i=1}^{n}\log p(X_i)
> $$
> Q.E.D.

Doing some math to write out the absolute value and get rid of the log, we get: 
$$
\mathbb P (2^{-n(H(X) + \epsilon)} \leq p(X_n) \leq 2^{n(H(X)+\epsilon)})\underset{n\rightarrow \infty}{\longrightarrow} 1
$$
What this tells us is that sequences in the typical set contain virtually all the probability mass. All other cases have a probability of $0$ so they will never be *observed*. 

The size of typical set is $2^{nH(X)}$. So the bits to encode this random sequence is $nH(x)$ and the average of bits are $H(X)$. 

