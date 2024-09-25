## Communication

Here is the Shannon’s block diagram of a communication system: 

<img src = "C:\Users\16549\AppData\Roaming\Typora\typora-user-images\image-20240606165110889.png" width = 600>

Suppose that you want to send a message over a noisy channel. The basic steps of a digital communication system are: 

- The source message is *compressed*. 
- *Redundancy* is added to deal with the noise in the channel. 
- The coded massage is sent through the communication channel. 

## Binary Erasure Channel

In this note, we will focus on the Binary Erasure Channel (BEC), where the noise source erases the coded massage with the probability of $p\in(0,1)$. 

We are interested in the maximum number of bits that the transmitter can send over the channel per transmission without error.

Suppose that we have a message of length $L$ and we encode a message of length $n$, where $n>L$ to account for the erasures in the BEC. 

The ratio $R = \frac{L}{n}$ is therefore called the ratio of the code, which represents number of bits of information about the source message per symbol that the receiver receives. 

Accompanying any code is an *encoding function* $f_n:\mathcal X^{L}\rightarrow \mathcal X^n$ and a *decoding function* $g_n:\mathcal Y^n\rightarrow \mathcal Y^{L}$, where $\mathcal X = \{0,1\}$ and $\mathcal Y = \{0,1,e\}$.  Symbol $e$ indicates that the symbol was erased by channel. 

Let $X^{(n)} = (X_1,...,X_n)$ be the $n$ bits which are fed into the channel and let $Y^{(n)} = (Y_1,...,Y_n)$ be the $n$ bits which are the output of the channel. Then, the maximum probability of error of the code is: 
$$
P_e(n) = \max_{x\in\mathcal X^L}\mathbb P(g_n(Y^{(n)}) \not= x| X^{(n)}=f_{n}(x))
$$
We say that the rate $R$ is achievable if there exist encoding and decoding functions $(f_n,g_n)$ such that $P_e(n)\rightarrow 0$ as $n\rightarrow \infty$. The largest achievable rate of the channel is called the capacity of the channel.

> Theorem 1. The capacity of the BEC with erasure probability $p$ is $1-p$. 
>
> *Proof.* First, we will show that the capacity is no more that $1-p$. Because $R>1-p$ implies $n(1-p)<L$, where the receiver can't get that much massage. 
>
> Next, we will show $R = 1-p-\epsilon$ for any $\epsilon > 0$ can be achieved. Flip $n2^{L(n)}$ fair coins independently and fill in an $n\times 2^{L(n)}$ codebook accordingly. 
>
> <img src = "C:\Users\16549\AppData\Roaming\Typora\typora-user-images\image-20240607113040973.png" width = 400>
>
> The columns represent the codewords $c_1, . . . , c_{2^{L(n)}}$ (one codeword per possible message) and the rows represent the individual bits of the codewords.
>
> As $n\rightarrow \infty$, a fraction $p$ of the bits will be erased. Suppose the first codeword is sent. The probability of error is the probability that there exist $\geq 2$ entries in the truncated codebook which matches the received bits. Hence: 
> $$
> \mathbb P(\bigcup_{i=2}^{2^{L(n)}}\{c_1=c_i\}) \leq \sum_{i=2}^{2^{L(n)}} 2^{-n(1-p)}\leq 2^{L(n)}\cdot2^{-n(1-p)}=2^{-n(1-p-R)}
> $$
> Since $R = 1-p-\epsilon$, the probability goes to $0$ exponentially fast as $n\rightarrow \infty$. 