## Recurrence & Transience

The first key insight about Markov chains is that while some states will be visited over and over again, others will only be visited a few times and then never seen again.

For each $x\in\mathcal{X}$, the random variable $T_x$ represents the first time that the chain visits state $x$, i.e., $T_x = \min\{n\in\mathbb{N}: X_n = x\}$. 

We also need the random variable $T_x^{+} = \min\{n\in\mathbb{Z_+}:X_n=x\}$, which is the hitting time for state $x$ except that we do not let $T_x = 0$ when the chain starts at $x$. 

Also, let $\mathbb{P}_x$ and $\mathbb E_x$ be the probability and expectation that the chain starts at $x$. Then, for $x,y\in\mathcal{X}$, define $\rho_{x,y}=\mathbb{P}_{x}(T_{y}^{+}<\infty)$ as the probability that we start at $x$ and eventually reach $y$. For simplicity, $\rho_x = \rho_{x,x}$. 

Now, we say that a state is **recurrent** if $\rho_x = 1$ and **transient** if $\rho_{x}<1$. 

> **Proposition 2**. A finite-state discrete-time Markov chains has at least one recurrent state. 
>
> After all, the chain has to spend its time somewhere. If it visits each of its finitely many states finitely many times, then where it could go? 
>
> However, this is not true for infinite-state Markov chains. 

## Classification of States

We say that state $x$ communicate with state $y$ if $\rho_{x,y}>0$ and $\rho_{y,x}>0$. A **communicating class** is a maximal set of states which communicate with each other. 

We say that a Markov chain is **irreducible** if it consists of a single communicating class. We call a property is **class property** if the property is shared by all members of a communicating class. 

> **Theorem 1**. Recurrence and transience are class properties. 
>
> *Proof.* From proposition $2$, it follows that every finite-state irreducible chain is recurrent. Moreover, if a state is recurrent, any state it can reach is also recurrent. 
>
> Therefore, if a communicating class has at least one recurrent state, then the communicating class is recurrent. Otherwise, it is transient. 

## Positive Recurrence & Null Recurrence

A sequence of random variable is called **stationary** if for every positive integer $k,n$ and all events $A_1, A_2...A_n$ :
$$
\mathbb{P}(X_1\in A_1, ..., X_n\in A_n) = \mathbb{P}(X_{k+1}\in A_{1},...,X_{n+k}\in A_{n})
$$
In other words, the distribution of $(X_1,...,X_n)$ is same as the joint distribution after we shift the time index by $k$ to $(X_{1+k},...,X_{n+k})$. 

For a Markov chain $(X_n)_{n\in\mathbb N}$, convince yourself that $(X_n)_{n\in\mathbb N}$ is stationary if and only if the chain is started from its stationary distribution. 

> **Theorem 2**. Suppose the Markov chain is irreducible with a stationary distribution $\pi$. Then, for each $x\in \mathcal X$ : 
> $$
> \pi(x) = \frac{1}{\mathbb E_x(T_x^+)}
> $$
> *Proof.* The Markov property says that once the current state is known, then the past history is irrelevant for predicting the future. Therefore, if at two time step we are in the same state $x$, the future of Markov chains has the same distribution. 
>
> To formalize this, define $T_x(k)$ to be the time at which we visit $x$ for the $k-th$ time after $0$, where $T_x(0) = 0$. Start the chain at state $x$. Then, the blocks
> $$
> (X_0, ...,X_{T_x(1)-1}), (X_{T_{x}(1)}, ...,X_{T_x(2)-1}),(X_{T_x(2)},...,X_{T_x(3)-1})...
> $$
> are i.i.d. Note that each block starts at state $x$. 
>
> Let $\tau_1,\tau_2...$ denote the length of each blocks. They are i.i.d and $\mathbb E[\tau_1]=\mathbb E_x[T_x^+]$. By the SLLN, $n^{-1}\sum_{i=1}^n \tau_i \rightarrow \mathbb E_x[T_x^+]$. 
>
> The average of length can also be interpreted as $\frac{t}{\sum_{i=1}^t1\{X_i=x\}}$. Therefore: 
> $$
> \frac{t}{\sum_{i=1}^t1\{X_i=x\}}\rightarrow \mathbb E_{x}[T_x^+]
> $$
> or
> $$
> t^{-1}\sum_{i=1}^t1\{X_i=x\}\rightarrow \frac{1}{\mathbb E[T_x^+]}\\
> t^{-1}\sum_{i=1}^t\mathbb P(X_i=x)\rightarrow \frac{1}{\mathbb E[T_x^+]}
> $$
> Since the Markov chain has a stationary distribution $\pi$, then $\mathbb P(X_i=x) = \pi(x)$ for all $i\in\mathbb N$, so we get $\pi(x) = \frac{1}{\mathbb E[T_x^+]}$. 

We define $x$ to be **positive recurrent** if $x$ is recurrent and $\mathbb E_x[T_x^+]<\infty$. Otherwise, we say $x$ is **null recurrent** if $x$ is recurrent and $\mathbb E_x[T_x^+] = \infty$. 

> **Theorem 3**. Positive recurrence and null recurrence are class properties. 

> **Theorem 4.** An irreducible positive recurrent Markov chain has a unique stationary distribution. Also, the converse is true. 