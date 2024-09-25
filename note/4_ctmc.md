## Poisson Process

An random process $\{N(t), t\geq 0\}$ is called to be a *counting process* if $N(t)$ is the number of events that have occurred up to time $t$ and: 

- $N(t) \in \mathbb Z$
- If $s<t$, then $N(s)\leq N(t)$ and $N(t) - N(s)$ represents the number of events that have occurred in interval $[s,t)$

A counting process is said to be a *Poisson process* with rate parameter $\lambda >0$ if it satisfies the following properties: 

- $N(0) = 0$

- The process has independent increments. 
- $\forall s,t\geq 0, P(N(s+t)-N(s) = n) = e^{-\lambda t}\frac{(\lambda t)^n}{n!}$ where $n\in \mathbb Z$

Based on the definition, let's prove $E[N(t)] = \lambda t$: 
$$
\begin{align}
E[N(t)] &= \sum_{i=0}^{\infty} i\cdot e^{-\lambda t}\frac{(\lambda t)^i}{i!}\\
&= \sum_{i=1}^{\infty}\lambda t\cdot e^{-\lambda t}\frac{(\lambda t)^{i-1}}{(i-1)!} \\
&= \lambda t\cdot e^{-\lambda t}\sum_{i=0}^{\infty}\frac{(\lambda t)^i}{i!}\\
&= \lambda t\cdot e^{-\lambda t}\cdot e^{\lambda t} = \lambda t
\end{align}
$$
Another definition of Poisson process shows as follow: 

- $N(0) = 0$
- The process has stationary independent increments. 
- $h\rightarrow 0, \exist \lambda>0, P(N(s+h) - N(s)=1) = \lambda h+o(h)$
- $h\rightarrow 0,P(N(s+h)-N(s)\geq 2) = o(h)$

The proof of why these two definition are equivalent is omitted here. 

## Intuition

In Continuous Time Markov Chain (CTMC), the states are still discrete but the transition times are continuous. Suppose we are at time $t$, in state $i$. We're interested in the distribution of $\tau$, the time until the chain jumps to a different state. 

From the property of Markov chain, $\tau$ is independent from how much time we have already spent on $i$. That is: 
$$
P(\tau \geq T+t|\tau\geq T) = P(\tau\geq t)
$$

This is the statement that $\tau$ is memoryless and we know that the unique memoryless distribution is exponential distribution. Therefore, $\tau\sim \text{Exponential}(\lambda)$. 

> Mathematically, the probability density function (PDF) of the exponential distribution is given by:
> $$
> f(\tau|\lambda) = \lambda e^{-\lambda \tau}
> $$
> where $\lambda$ is called *rate* because the expectation of $\tau$ is exactly $\frac{1}{\lambda}$: 
> $$
> \begin{align}
> E[\tau] &= \int_{\tau=0}^{\infty} \tau\lambda e^{-\lambda \tau}d \tau\\
> &= [\tau\cdot (-e^{-\lambda \tau})]_{0}^{\infty}-\int_{\tau=0}^{\infty} \lambda e^{-\lambda\tau}d\tau\\
> &= 0 - [\frac{e^{-\lambda \tau}}{\lambda}]_{0}^{\infty} = \frac{1}{\lambda}
> \end{align}
> $$

We just saw the jump times are exponential, so it makes sense to describe how fast the transition $i\rightarrow j$ by exponential distribution $\text{exponentail}(q_{i,j})$. 

Recall that the minimum of exponential random variables is also exponential, with parameter equal to the sum of the rates.

>**Proposition 1.** Suppose we have $n$ random variables $\tau_1,\tau_2,...,\tau_n$ and their exponential rates are $\lambda_1,\lambda_2,...,\lambda_n$. Then $\min \tau_i \sim \text{exponential}(\sum \lambda_i)$. 
>
>*proof*. Based on the cumulative distribution function (CDF) of exponential distribution, we have: 
>$$
>P(\tau_i\geq t) = e^{-\lambda_i t}
>$$
>if all random variables satisfy $\tau_i\geq t$, then $\min \tau_i\geq t$
>$$
>P(\min \tau_i\geq t) = \prod_{i=1}^{n}P(\tau_i\geq t) = e^{-(\sum \lambda_i)t}
>$$
>This is the cumulative distribution function of $\min \tau_i$, so: 
>$$
>\min\tau_i\sim \text{exponential}(\sum \lambda_i)
>$$

Draw proposed jump times $\tau_i\sim \text{exponential}(\sum \lambda_i)$ and jump to the state that comes first. The probability of the transition to $j$ is given by $P(\tau_j = \min \tau_i) = \frac{\lambda _j}{\sum \lambda_i}$. 

> **Proposition 2.** If $\tau_i\sim \text{exponential}(\sum\lambda_i)$, then $P(\tau_j=\min \tau_i) = \frac{\lambda_j}{\sum \lambda_i}$
>
> *proof.* Calculate the probability by integral: 
> $$
> \begin{align}
> P(\tau_j = \min \tau_i) &= \int_{x=0}^{\infty} f(x|\lambda_j)\cdot\prod_{i\not=j} P(\tau_i\geq x) \cdot dx\\
> &= \int_{x=0}^{\infty} \lambda_je^{-\lambda_jx}\cdot e^{-(\sum_{i\not=j}\lambda_i)x}\cdot dx\\
> &= \lambda_j\int_{x = 0}^{\infty} e^{-(\sum\lambda_i)x}dx\\
> &= \lambda_j\cdot[-\frac{e^{-(\sum\lambda_i)x}}{\sum\lambda_i}]_{0}^{\infty} = \frac{\lambda_j}{\sum \lambda_i}
> \end{align}
> $$

## CTMC

In CTMC, our random process is defined by a *rate matrix* $Q\in \mathbb R^{|\mathcal X|\times |\mathcal X|}$ where: 

- $\forall i\not=j, Q(i,j)\geq0$
- $\sum_{j}Q(i,j) = 0$

More generally, our rate matrix looks like: 
$$
Q = \begin{bmatrix}
-\sum_{i\not=1}\lambda_{1\rightarrow i} & \lambda_{1\rightarrow 2} & \cdots &\lambda_{1\rightarrow n} \\
\lambda_{2\rightarrow 1} & -\sum_{i\not=2}\lambda_{2\rightarrow i} & \cdots & \lambda_{2\rightarrow n} \\ 
\vdots & \vdots & \ddots & \vdots \\
\lambda_{n\rightarrow 1} & \lambda_{n\rightarrow 2} & \cdots & \sum_{i\not=n} -\lambda_{n\rightarrow i}
\end{bmatrix}
$$
For simplicity, we denote $q_i = -Q(i,i)$. Consider a very short time $\epsilon \rightarrow 0$ and we can use the Taylor series expansion to approximate the CDF of exponential distribution: 
$$
P(\tau\geq \epsilon) = e^{-\lambda\epsilon} = 1-\lambda\epsilon+o(\epsilon)
$$
where $o(\epsilon)$ is a number that is negligibly small. 

Since the minimum of exponential random variables is still exponential, we can calculate the holding probability at state $i$ (transition to $j$ will not happen): 
$$
P(\min \tau _j \geq \epsilon) = 1-(\sum \lambda_j)\epsilon + o(\epsilon) = 1-q_i\epsilon+o(\epsilon)
$$
Using the proposition $2$, we can also calculate the probability of the transition $i\rightarrow j$ : 
$$
\begin{align}
P(X_{t+\epsilon} = j|X_{t} = i) &= P(\text{leave i})P(\text{go to j | leave i}) \\
&= q_i\epsilon\cdot\frac{\lambda_j}{q_i} = \lambda_j\epsilon
\end{align}
$$
Because $\epsilon\rightarrow 0$, the probability of two or more transitions is negligibly small. Therefore, we have the following properties: 

$$
P(X_{t+\epsilon}=j|X_t=i) = 
\begin{cases}
\epsilon Q(i,j) + o(\epsilon)  & i=j\\
1 + \epsilon Q(i,i) + o(\epsilon) & i\not=j
\end{cases}
$$
Based on the definition above, we can find that Poisson process is a CTMC: 

<img src = "C:\Users\16549\AppData\Roaming\Typora\typora-user-images\image-20240524162052808.png" width = 500>

## Stationary Distributions

Now we are ready to discuss stationary distributions. Recall that for DTMC, we are interested in solving for $\pi$ such that $\pi = \pi P$. However, in CTMC we need to solve for: 
$$
\pi Q =  0
$$
Since we want the distribution to be stationary all the time, the probability mass flows out of the state should equal that comes in. We can describe this process within a very short time $\epsilon$ and use the properties in the last section: 
$$
\forall i, \ \ \ \pi_i\cdot \epsilon (-Q(i,i)) = \sum_{j\not=i}\pi_j\cdot \epsilon Q(j,i)\\
\iff \pi Q = 0
$$

## Kolmogorov Equations

Let $P_{i,j}(t)$ be the probability of transition $i\rightarrow j$ in time $t$. Then, the Kolmogorov equation can be written as: 
$$
P_{i,j}(s+t) = \sum_{k\in\mathcal X} P_{i,k}(s) + P_{k,j}(t)
$$
In matrix form, we have $P(s+t) = P(s)P(t)$. Try to find the derivative of $P(t)$: 
$$
\begin{align}
P'(t) &= \lim_{\Delta t\rightarrow 0} \frac{P(t+\Delta t) - P(t)}{\Delta t}\\
&= \lim_{\Delta t\rightarrow 0} \frac{P(\Delta t)P(t) - P(t)}{\Delta t}\\
&= \Big(\lim_{\Delta t\rightarrow 0} \frac{P(\Delta t)  -I}{\Delta t}\Big)P(t)
\end{align}
$$
Because the transition equation in $\Delta t$ can be written as $P(\Delta t)  - I = \Delta t Q$. Therefore, the left term equals $Q$: 
$$
P'(t) = QP(t)
$$
We can apply matrix exponential to find $P(t)$: 
$$
P(t) = e^{Qt}
$$
Refer to `Matrix Exponential` part in my linear algebra note so you can compute $e^{Qt}$. 