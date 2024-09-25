Given a positive integer $n$ and a probability value $p\in[0,1]$, the $\mathcal G(n,p)$ random graph is an undirected graph on $n$ vertices such that each of the $n\choose 2$ edges is present independently with probability $p$. 

**Theorem 1.** Let $p(n) = \lambda\frac{\ln n}{n}$. For a constant $\lambda>0$: 

- If $\lambda<1$, then $\mathbb P(\mathcal G(n,p(n))\text{ is connected}) \rightarrow 0$
- If $\lambda >1$, then $\mathbb P(\mathcal G(n,p(n))\text{ is not connected})\rightarrow 1$

