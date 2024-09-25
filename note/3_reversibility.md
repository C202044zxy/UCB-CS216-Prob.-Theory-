## Reversibility

Consider an irreducible Markov chain $(X_n)_{n\in\mathbb N}$ on finite state space $\mathcal X$ with transition matrix $P$. Fix a integer $N$ and define the **reversed chain** $Y_n = X_{N-n}$ for $n = 0, 1...N$. Then, we have $(X_N,...,X_0) = (Y_0,...,Y_N)$. 

> **Theorem 1**. If an irreducible Markov chain $(X_n)_{n\in\mathbb N}$ is started from the stationary distribution $\pi$, then the reversed chain is an irreducible Markov chain with the transition probability $\hat P(x,y) = \frac{\pi(y)P(y,x)}{\pi(x)}$ for all $x,y\in \mathcal X$. 
>
> *Proof.* For a positive integer $k<N$ and a feasible sequence of states $x_0,...,x_{k+1}$ :
> $$
> \mathbb P(Y_{k+1} = x_{k+1}|Y_k=x_k ...Y_0=x_0) = \mathbb P(X_{n-k-1}=x_{k+1}|X_{n-k}=x_k...X_n=x_0)
> $$
> After Applying the property of Markov chain, we have:  
> $$
> \begin{align}
> \hat P(x_k,x_{k+1}) &=\mathbb P(Y_{k+1}=x_{k+1}|Y_k=x_k) \\
> &= \mathbb P(X_{n-k-1}=x_{k+1}|X_{n-k}=x_k) \\
> &= \frac{\mathbb P(X_{n-k-1}=x_{k+1})\mathbb P(X_{n-k}=x_k|X_{n-k-1}=x_{k+1})}{\mathbb P(X_{n-k}=x_k)} \\
> &=	\frac{\pi(x_{k+1})P(x_{k+1},x_k)}{\pi(x_k)}
> \end{align}
> $$
> Substitute $x_{k+1}$ by $y$ and we get: $\hat P(x,y) = \frac{\pi(y)P(y,x)}{\pi(x)}$

A Markov chain whose stationary distribution $\pi$ and transition probability matrix $P$ is called reversible if and only if $P(x,y) = \hat P(x,y)$, or equivalently: 
$$
\pi(x) P(x,y) = \pi(y)P(y,x) \ \ \ \ \ \ \ \ (1)
$$

## Detailed balance

The equations $(1)$ are also called the **detailed balance equations**. In general, the condition for stationary $\pi(x) = \sum_{y\in \mathcal X}\pi(y)p(y,x)$ is called balance equations. 

The balance equations express the global condition that the total mass leaving state $y$ equals total mass entering $y$. On the other hand, the detailed balance equations reflect a local condition that the mass exchanged on each edge $(x,y)$ is balanced. 