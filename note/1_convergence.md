## Review

There is only one sense where a sequence of real numbers $(a_n)_{n\in\mathbb{N}}$ is said to *converge* to a limit. Namely, $a_{n}\underset{n\rightarrow \infty}{\longrightarrow}a$ if for every $\epsilon>0$ there exist a positive integer $N$ such that the sequence after $N$ is always within $\epsilon$ of the supposed limit $a$. 

Throughout this discussion, fix a probability space $\Omega$ and a sequence of random variables $(X_n)_{n\in \mathbb{N}}$. Also, let $X$ be another random variable. 

## Borel-Cantelli Lemma

Before diving into three types of convergence, we will learn and prove Borel-Cantelli lemma first. Let's state the lemma first: 

>If $\sum_{n=1}^{\infty} P(A_n) < \infty$, then the probability that $A_n$ occurs infinitely often (still occurs when $n\rightarrow \infty$) is $0$. In mathematical notion, $P(\lim\sup_{n\rightarrow \infty} A_n) = 0$

where $\lim \sup_{n\rightarrow \infty}A_n$ is defined as follow: 
$$
\lim\sup_{n\rightarrow \infty} A_n = \cap_{n=1}^{\infty}\cup_{k=n}^{\infty} A_k
$$
Let $B_k = \cup_{k=n}^{\infty}A_k$, then we have $B_1\supseteq B_2\supseteq B_3...$ and the following inequality: 
$$
P(B_k) = P(\cup_{n=k}^{\infty} A_n) \leq \sum_{n=k}^{\infty} P(A_n)
$$
Since $\sum_{n=1}^{\infty} P(A_n) < \infty$, for every $\epsilon >0$, there exist a positive integer $N$ such that for $n>N$, $\sum_{k=n}^{\infty} P(A_k) < \epsilon$ (i.e. the suffix sum converges to zero as $n$ increases). 

Therefore, $\lim_{k\rightarrow \infty} P(B_k) \leq \lim_{k\rightarrow \infty}\sum_{n=k}^{\infty} P(A_n)= 0$. By definition: 
$$
P(\lim\sup A_n) = P(\cap_{n=1}^{\infty} \cup_{k=n}^{\infty} A_k) = P(\lim_{k\rightarrow \infty} B_k)=0
$$

---

Here is another form of Borel-Cantelli Lemma: 

> If $\sum_{n=1}^{\infty} P(A_n) = \infty$ and events are pairwise independent, then the probability that $A_n$ occurs infinitely often (still occurs when $n\rightarrow \infty$) is $1$. Namely, $P(\lim\sup_{n\rightarrow \infty} A_n) = 1$

We have: 
$$
P(\lim\inf_{n\rightarrow \infty} A_n^c) = P(\lim\sup_{n\rightarrow \infty } A_n)^c = 1 - P(\lim \sup _{n\rightarrow \infty }A_n)
$$
where the superscript $c$ means opposing events and $\lim\inf_{n\rightarrow \infty} A_n^c$ is given by: 
$$
\lim\inf_{n\rightarrow \infty }A_n^x = \cup_{n=1}^{\infty}\cap_{k=n}^{\infty} A_k
$$
Some intuition about the equation: the opposing event of "$A_n$ occurs infinitely often" is "the sequence converges to $A_n^c$". 

Similarly, let $B_n = \cap_{k=n}^{\infty} A_k^c$ :
$$
P(B_n) = P(\cap_{k=n}^{\infty} A_k^c)
$$
Since $P(A_n)$ doesn't converge to zero and events are pairwise independent, by no mean will $\cap^{\infty}_{k=n} A_k^c$ holds true. Therefore $\lim_{n\rightarrow \infty}P(B_n)=0$. 
$$
P(\lim\inf_{n\rightarrow \infty} A_n^c) = \lim_{n\rightarrow \infty}P(B_n) = 0
$$
Conclusion: $P(\lim\sup_{n\rightarrow \infty} A_n) = 1-P(\lim\inf_{n\rightarrow \infty}A_n^c)=1$

>After understanding the proof, here is a better intuition about $\lim \sup A_n$ and $\lim \inf A_n$ : 
>
>- $\sup$ represents *superior*, which means the expression holds true if $A_n$ appears once. In other word, we give priority to $A_n$
>- $\inf$ represents *inferior*, which means the expression holds true when $A_n$ appears throughout the sequence(no other event). In other word, $A_n$ is inferior. 

## Almost Sure Convergence

Define $\omega$ as the outcome of the whole sequence of $(X_n)_{n\in\mathbb{N}}$ in probability space $\Omega$. The sequence $(X_n)_{n\in\mathbb{N}}$ is said to *converge almost surely* to the limit $X$, if the set of outcome $\omega\in\Omega$ for which $X_n(\omega) \underset{n\rightarrow \infty}\longrightarrow X(\omega)$ forms an event of probability one. In mathematical notion: 
$$
P(X_n(\omega)\underset{n\rightarrow \infty}\longrightarrow X(\omega))=1
$$
In other word, all *observed* realizations of sequence $(X_n)_{n\in\mathbb{N}}$ converge to limit $X$. The philosophy is to disregard events of probability zero, as they are never *observed*.  

One of the most celebrated results in probability theory is the statement that the sample average of identically distributed random variables, under very weak assumptions, converges a.s. to the expected value of their common distribution. This is known as the **Strong Law of Large Numbers (SLLN)**.

>**Theorem 1** (Strong Law of Large Numbers). If $(X_n)_{n\in\mathbb{N}}$ are pairwise independent and identically distributed with $E[|X_1|]<\infty$, then $n^{-1}\sum_{i=1}^nX_i \overset{a.s.}{\underset{n\rightarrow \infty}\longrightarrow}E[X_1]$

## Convergence In Probability

Next, $(X_n)_{n\in\mathbb{N}}$ is said to *converge in probability* to $X$, denoted $X_n\underset{n\rightarrow \infty}{\overset{\mathbb P}{\longrightarrow}} X$, if for every $\epsilon>0, P(|X_n-X|>\epsilon) \underset{n\rightarrow \infty}{\longrightarrow} 0$. 

In other words, for any fixed $\epsilon$, the probability that the sequence deviates from $X$ becomes vanishingly small (note that the probability also forms a sequence). Here, we are going to prove that a.s. convergence implies convergence in probability. 

> **Theorem 2**. If $X_n\underset{n\rightarrow \infty}{\overset{a.s.}{\longrightarrow}} X$, then $X_n\underset{n\rightarrow \infty}{\overset{\mathbb P}{\longrightarrow}} X$. 
>
> Fix $\epsilon >0$. Define $A_n = \cup_{m=n}^{\infty} \{|X_m-X|>\epsilon\}$ to be the event that at least one of $X_n,X_{n+1}...$ deviates from $X$ by more than $\epsilon$. Observe that $A_1\supseteq A_2\supseteq A_3...$ decreases to an event $A$ which has probability $0$, since a.s. convergence requires for all outcome $\omega\in \Omega$, $\big(X_n(\omega)\big)_{n\in\mathbb N}$ converges to $X(\omega)$. Therefore, $\lim _{n\rightarrow \infty}P(A_n) = 0$. 
>
> Then, we can conclude that: 
> $$
> P(|X_n-X|>\omega)\geq P(A_n)\underset{n\rightarrow\infty}\longrightarrow 0
> $$
> Q.E.D. 

However, the converse is not true. 

>**Example 1.** A sequence that converges in prob. but not a.s. is as follow. First, set $X_n = 0$ for all $n\in \mathbb{N}$. Then, for each $j\in \mathbb N$, randomly pick an index $N_j$ from $[2^j,2^{j+1}-1]$ and assign $X_{N_j}=1$. Obverse that $P(X_n=1) =2^{-\lfloor\log_2n\rfloor}\underset{n\rightarrow \infty}\longrightarrow0$, so $X_n\underset{n\rightarrow \infty}{\overset{\mathbb P}{\longrightarrow}} 0$. 
>
>But the sequence do not satisfy a.s. convergence obvious. You can conclude from the construction process: $1$ will appear infinite often(though the density of $1$ is zero) for any outcome $\omega\in\Omega$. Therefore, $P(X_n(\omega)\underset{n\rightarrow \infty}\longrightarrow X(\omega))=0$

According to Theorem $1$ and $2$, we can obtain **Weak Law of Large Numbers (WLLN)**. 

> **Theorem 3** (Weak Law of Large Numbers). If $(X_n)_{n\in\mathbb{N}}$ are pairwise independent and identically distributed with $E[|X_1|]<\infty$, then $n^{-1}\sum_{i=1}^nX_i \overset{\mathbb P}{\underset{n\rightarrow \infty}\longrightarrow}E[X_1]$

## Convergence in Distribution

The last mode of convergence is *convergence in distribution*. If for each $x\in \mathbb{R}$ such that $P(X=x)=0$ we have $P(X_n\leq x) = P(X\leq x)$, then $X_n\underset{n\rightarrow \infty}{\overset{\mathbb d}\longrightarrow }X$. 

Next, we will show converge in probability implies converge in distribution. 

>**Theorem 4**. If  $X_n\underset{n\rightarrow \infty}{\overset{\mathbb P}\longrightarrow }X$, then $X_n\underset{n\rightarrow \infty}{\overset{\mathbb d}{\longrightarrow}} X$. 
>
>Let $x$ be a point $P(X = x)=0$. For a fixed $\epsilon>0$, we can write: 
>$$
>\begin{align}
>P(X_n\leq x) &=P(X_n\leq x, |X-X_n|\leq \epsilon)+P(X_n\leq x, |X-X_n|>\epsilon)\\
>&\leq P(X\leq x+\epsilon)+P(|X-X_n|>\epsilon)
>\end{align}
>$$
> and: 
>$$
>\begin{align}
>P(X\leq x - \epsilon) &= P(X\leq x-\epsilon, |X-X_n|\leq \epsilon)+P(X\leq x-\epsilon,|X-X_n|>\epsilon)\\
>&\leq P(X_n\leq x)+P(|X-X_n|>\epsilon)
>\end{align}
>$$
>According to the definition of convergence in probability, we can conclude that: 
>$$
>P(X\leq x-\epsilon)\leq P(X_n\leq x) \leq P(X\leq x+\epsilon)
>$$
>Let $\epsilon\rightarrow 0$, we have $P(X_n\leq x) = P(X\leq x)$, which implies convergence in distribution. 

But the converse is not true. For example, let $X_0\sim \text{Uniform}[-1,1]$, and define $X_n = (-1)^n X_0$. It is obvious $X_n\underset{n\rightarrow \infty}{\overset{\mathbb d}\longrightarrow }X_0$ because they are all uniform distributions. However, since $\{X_n\}$ are pairwise corelated, they will not converge to any $X$. 

