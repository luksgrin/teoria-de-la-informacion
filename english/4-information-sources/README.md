## Information Sources

An information source is defined as a tuple $(\mathcal{S},P)$ where:

- $\mathcal{S}$ is a set of symbols that can be emitted by the source (an alphabet).
- $P$ is a probability distribution associated with the emission of the symbols.

Information sources can be continuous (with an uncountable number of messages) or discrete (with a countable or finite number of messages). In this course, we will focus on the discrete case, so $S$ will be a finite set.

Clearly, $\forall s \in \mathcal{S}, 0 \leq P(s) \leq 1$, and $\sum_{s \in \mathcal{S}} P(s) = 1$ (due to Kolmogorov's Axioms).

### Memoryless Information Sources

In a memoryless information source, the emission of each symbol $s_i$ is independent of the previously emitted symbols. In this case, the probability of emitting a symbol $s_i$ is constant and equal to $P(s_i)$.

The entropy of a memoryless information source is defined as:

$$
H(\mathcal{S}) = -\sum_{s \in \mathcal{S}} P(s) \log\left( P(s) \right)
$$

### Extension of Degree $m$

We can imagine a memoryless information source as a machine that emits sequences of $x$ symbols, words, $x \in \mathcal{S}^+$, so that the successively emitted symbols are chosen according to the probabilities $P(s)$.

Let $|x| = m$, we define the extension of degree $m$ of the memoryless information source as the pair $\left(\mathcal{S}^m, P^m\right)$, where:

$$
\forall x \in \mathcal{S}^m : P(x) = \prod_{1 \leq i \leq m} P(x[i])
$$

And trivially, the entropy is:

$$
\begin{align*}
H\left(\mathcal{S}^m\right) &= -\sum_{x \in \mathcal{S}^m} P(x) \log\left( P(x) \right) \\
&= -\sum_{x \in \mathcal{S}^m} \left(\prod_{1 \leq i \leq m} P(x[i])\right) \log\left(P\left(\prod_{1 \leq i \leq m} P(x[i])\right)\right)
\end{align*}
$$

Instead of calculating the products of symbol probabilities for each word of the extension of degree $m$, the following useful result can be demonstrated:

$$
H\left(\mathcal{S}^m\right) = m H(\mathcal{S})
$$

### Markov Sources (Information Source with Memory, of Order $m$)

In a Markov source, the emission of each symbol $s_i$ depends on the $m$ previously emitted symbols (in many applications). In this case, the probability of emitting a symbol $s_i$ depends on the $m$ previous symbols and is denoted as the conditional probability $P(s_i|s_{i-1}, \ldots, s_{i-m})$, with:

$$
\sum_{i=1}^{m} P(s_i|s_{i-1}, \ldots, s_{i-m}) = 1, \quad i_k = 1, 2, \dots, n
$$

The sequence of emitted symbols is called a **Markov chain**. The states of a Markov source (of order $m$) will be all possible combinations of $m$ symbols $n^m$.

Given a Markov source of order $m$, its state diagram can be established, showing the states and the probabilities between them.

---

#### Examples

From a binary alphabet $\left\\{0,1\right\\}$, a second-order Markov source can be defined with the following states and conditional probabilities:

- $P(0|00) = P(1|11) = 0.7$
- $P(1|00) = P(0|11) = 0.3$
- $P(0|01) = P(1|10) = P(0|10) = P(1|01) = 0.5$

The state diagram is as follows:

![Markov diagram](./img/fuente-de-markov-diagrama-de-estados.svg)

---

A Markov source is said to be ergodic if it is possible to move from any state to any other state in a finite number of steps.

---

#### Example

An ergodic source could be the previous one (we can reach any state in a finite number of steps from another state).

Example of a state diagram of a **non**-ergodic source:

![Non-ergodic Markov diagram](./img/fuente-de-markov-no-ergódico.svg)

Note that the inner node is an absorbing state. That is, once you reach that state, you cannot exit it.

---

A Markov source is homogeneous if the conditional probabilities do not change over time.

A source is said to be in a stationary state if the probability of observing its states does not change over time. The probabilities can be obtained using the equation $v = \pi\Pi$, where $\pi$ is the state probability vector and $\Pi$ is the transition matrix.

---

#### Example

Returning to the initial example, the probability matrix has the following form:

$$
\Pi = \begin{matrix}
& \begin{matrix} 00 & 01 & 10 & 11 \end{matrix} \\\
\begin{matrix} 00 \\\ 01 \\\ 10 \\\ 11 \end{matrix} & \begin{pmatrix} 0.7 & 0.5 & 0.5 & 0.3 \\\ 0 & 0 & 0.5 & 0.5 \\\ 0.5 & 0.5 & 0 & 0 \\\ 0.3 & 0.5 & 0.5 & 0.7 \end{pmatrix}
\end{matrix}
$$

Note that each row sums to 1 (due to Kolmogorov's axioms). If each column also summed to 1, then the matrix is doubly stochastic, and all states are equally probable.

Let's calculate the stationary state probabilities. To do so, we define the following equations:

$$
\begin{align*}
&P(00) = P(0|00) \cdot P(00) + P(0|10) \cdot P(10) \\
&P(01) = P(1|00) \cdot P(00) + P(1|10) \cdot P(10) \\
&P(11) = P(1|01) \cdot P(01) + P(1|11) \cdot P(11) \\
&P(00) + P(01) + P(10) + P(11) = 1
\end{align*}
$$

Note that the last equation arises from one of Kolmogorov's axioms. If we included state $01$ in the first equation, we would have a redundant equation (and hence a singular system with infinite solutions). Since we know the conditional probabilities, we can solve the system of equations:

$$
\begin{align*}
&P(00) = 0.7 \cdot P(00) + 0.5 \cdot P(10) \\
&P(01) = 0.3 \cdot P(00) + 0.5 \cdot P(10) \\
&P(11) = 0.5 \cdot P(01) + 0.7 \cdot P(11) \\
&P(00) + P(01) + P(10) + P(11) = 1
\end{align*}
$$

This system has the following solution:

$$
\pi = \begin{pmatrix} P(00) \\ P(01) \\ P(10) \\ P(11) \end{pmatrix} = \begin{pmatrix} \frac{5}{16} \\ \frac{3}{16} \\ \frac{3}{16} \\ \frac{5}{16} \end{pmatrix}
$$

Now, with this information, we can calculate the occurrence probabilities of each symbol:

$$
\begin{align*}
&P(0) = P(00) + P(10) = \frac{5}{16} + \frac{3}{16} = \frac{8}{16} = \frac{1}{2} \\
&P(1) = P(01) + P(11) = \frac{3}{16} + \frac{5}{16} = \frac{8}{16} = \frac{1}{2}
\end{align*}
$$

---

### Affine Sources of a Markov Source

Given a Markov source of order $m$ with an alphabet $\mathcal{S}$ and a probability distribution $P$, we will call the affine source the memoryless source $(\mathcal{S},P)$. That is, the affine source is the memoryless source that emits the same symbols as the Markov source.

---

#### Example

For the example of the second-order Markov source, the affine source would be the memoryless source with $\mathcal{S}=\left\\{0,1\right\\}$ and $P=\left\\{\frac{1}{2},\frac{1}{2}\right\\}$.

---

For the entropy calculation of a Markov source of order $m$, over an alphabet $\mathcal{S}=\left\\{s_1,s_2,\dots,s_n\right\\}$ and conditional probability distribution $P(s_i|s_{i_1},\dots,s_{i_m})$, we have that $p(s_i, s_{i_1},\dots,s_{i_m}) = p(s_i|s_{i_1},\dots,s_{i_m})\cdot p(s_{i_1},\dots,s_{i_m})$, which allows us to calculate the conditional entropy:

$$
H(\mathcal{S}|s_{i_1},\dots,s_{i_m}) = -\sum_{i=1}^{n}p(s_i|s_{i_1},\dots,s_{i_m})\log\left(p(s_i|s_{i_1},\dots,s_{i_m})\right)
$$

Therefore, the entropy of the $m$-order Markov source is:

$$
\begin{align*}
H(\mathcal{S}) &= \sum_{\mathcal{S}^m}p(s_{i_1},\dots,s_{i_m})H(\mathcal{S}|s_{i_1},\dots,s_{i_m})\\
&= -\sum_{\mathcal{S}^m}p(s_{i_1},\dots,s_{i_m})\left(-\sum_{s_i\in\mathcal{S}}p(s_i|s_{i_1},\dots,s_{i_m})\log\left(p(s_i|s_{i_1},\dots,s_{i_m})\right)\right)\\
&= -\sum_{\mathcal{S}^{m+1}}p(s_i, s_{i_1},\dots,s_{i_m})p(s_i|s_{i_1},\dots,s_{i_m})\log\left(p(s_i|s_{i_1},\dots,s_{i_m})\right)\\
&= -\sum_{\mathcal{S}^{m+1}}p(s_{i_1},\dots,s_{i_m},s_i)\log\left(p(s_i|s_{i_1},\dots,s_{i_m})\right)\\
\end{align*}
$$

#### Example

Let’s consider a second-order Markov source defined by the following conditional probabilities:

| $s_js_ks_i$ | $P(s_i\|s_js_k)$ |
|:------------|:-----------------|
| 000         | 0.8              |
| 001         | 0.2              |
| 010         | 0.5              |
| 011         | 0.5              |
| 100         | 0.5              |
| 101         | 0.5              |
| 110         | 0.2              |
| 111         | 0.8              |

We can calculate the steady-state probabilities:

$$
\begin{align*}
P(00) &= P(0|00)\cdot P(00) + P(0|10)\cdot P(10)\\
P(01) &= P(1|00)\cdot P(00) + P(1|10)\cdot P(10)\\
P(10) &= P(0|01)\cdot P(01) + P(0|11)\cdot P(11)\\
1 &= P(00) + P(01) + P(10) + P(11)
\end{align*}
$$

We can rewrite the system of equations so that it can be converted into a matrix system:

$$
\begin{align*}
\left(P(0|00) - 1\right)\cdot P(00) + P(0|10)\cdot P(10) &= 0\\
P(1|00)\cdot P(00) + P(1|10)\cdot P(10) - P(01) &= 0\\
P(0|01)\cdot P(01) + P(0|11)\cdot P(11) - P(10) &= 0\\
P(00) + P(01) + P(10) + P(11) &= 1
\end{align*}
$$

This becomes the matrix system:

$$
\begin{pmatrix}
P(0|00) - 1 & 0 & P(0|10) & 0\\
P(1|00) & -1 &P(1|10) & 0\\
0 & P(0|01) & -1 & P(0|11)\\
1 & 1 & 1 & 1
\end{pmatrix}\begin{pmatrix}
P(00)\\
P(01)\\
P(10)\\
P(11)
\end{pmatrix} = \begin{pmatrix}
0\\
0\\
0\\
1
\end{pmatrix}
$$

Substituting the values of the conditional probabilities, we get:

$$
\begin{pmatrix}
-0.2 & 0 & 0.5 & 0\\
0.2 & -1 & 0.5 & 0\\
0 & 0.5 & -1 & 0.2\\
1 & 1 & 1 & 1
\end{pmatrix}\begin{pmatrix}
P(00)\\
P(01)\\
P(10)\\
P(11)
\end{pmatrix} = \begin{pmatrix}
0\\
0\\
0\\
1
\end{pmatrix}
$$

By solving the system of equations using the inverse of the coefficient matrix, we obtain:

$$
\begin{pmatrix}
P(00)\\
P(01)\\
P(10)\\
P(11)
\end{pmatrix} = \begin{pmatrix}
-0.2 & 0 & 0.5 & 0\\
0.2 & -1 & 0.5 & 0\\
0 & 0.5 & -1 & 0.2\\
1 & 1 & 1 & 1
\end{pmatrix}^{-1}\begin{pmatrix}
0\\
0\\
0\\
1
\end{pmatrix}
= \begin{pmatrix}
\frac{5}{14}\\
\frac{2}{14}\\
\frac{2}{14}\\
\frac{5}{14}
\end{pmatrix}
$$

Thus, we can fill in the table for the steady-state probabilities:

| $s_js_ks_i$ | $P(s_i\|s_js_k)$ | $P(s_js_k)$ |
|:-----------:|:----------------:|:-----------:|
| 000         | 0.8              | 5/14        |
| 001         | 0.2              | 5/14        |
| 010         | 0.5              | 2/14        |
| 011         | 0.5              | 2/14        |
| 100         | 0.5              | 2/14        |
| 101         | 0.5              | 2/14        |
| 110         | 0.2              | 5/14        |
| 111         | 0.8              | 5/14        |

The next step is to calculate the joint probability of each state, i.e., $P(s_i,s_j,s_k)$, knowing that $P(s_i,s_j,s_k) = P(s_i|s_j,s_k)\cdot P(s_j,s_k)$:

| $s_js_ks_i$ | $P(s_i\|s_j,s_k)$ | $P(s_j,s_k)$ | $P(s_i,s_j,s_k)$ |
|:-----------:|:-----------------:|:------------:|:----------------:|
| 000         | 0.8               | 5/14         | 4/14             |
| 001         | 0.2               | 5/14         | 1/14             |
| 010         | 0.5               | 2/14         | 1/14             |
| 011         | 0.5               | 2/14         | 1/14             |
| 100         | 0.5               | 2/14         | 1/14             |
| 101         | 0.5               | 2/14         | 1/14             |
| 110         | 0.2               | 5/14         | 1/14             |
| 111         | 0.8               | 5/14         | 4/14             |

Finally, we can calculate the entropy of the second-order Markov source:

$$
\begin{align*}
H(\mathcal{S}) &= -\sum_{\mathcal{S}^{m+1}}p(s_i,s_{i_1},s_{i_2})\log\left(p(s_i\|s_{i_1},s_{i_2})\right)\\
&= -\left(\frac{4}{14}\log(0.8) + \frac{1}{14}\log(0.2) + \frac{1}{14}\log(0.5) + \frac{1}{14}\log(0.5) + \frac{1}{14}\log(0.5) + \frac{1}{14}\log(0.5) + \frac{1}{14}\log(0.2) + \frac{4}{14}\log(0.8)\right)\\
&= \text{Entropy value to be calculated.}
\end{align*}
$$

### Bernoulli and Binomial Sources

Consider the source $\left(\mathcal{S},P\right)$ where $\mathcal{S}=\left\\{x_1,x_2,\dots,x_n\right\\}$ and $p(x_i)=p_i$, and suppose we take a sequence $X_1,X_2,\dots,X_n$ of independent values.

_What frequency of occurrence of the element_ $x_i$ _do we expect in the sequence?_

- Each value in the sequence is a Bernoulli trial, where if $X_q = x_i$, we have a success, and if $X_q \neq x_i$, we have a failure (the probability of success is $p_i$).
- The number of successes in the sequence is a random variable $\mathcal{S}_i$ that follows a binomial distribution with

$$
P(\mathcal{S}_i=k) = \binom{n}{k}p_i^k(1-p_i)^{n-k}
$$

with a mean $\mu_i = np_i$ and a variance $\sigma_i^2 = np_i(1-p_i)$.

We can use Chebyshev's inequality to bound the probability that the random variable deviates from its mean:

$$
P\left(\left|\frac{\mathcal{S}_i-\mu_i}{\sigma_i}\right|\geq k\right)\leq\frac{1}{k^2}
$$

Consider the information source $\left(\mathcal{S},P\right)$ with $\mathcal{S}=\left\\{x_1,x_2,\dots,x_n\right\\}$ and $p(x_i)=p_i$, and suppose we take a sequence $\alpha = \left\langle\alpha_1,\alpha_2,\dots,\alpha_n\right\rangle$ of independent values. We will say that $\alpha$ is a $k$-typical sequence if the following holds:

$$
\forall i: 1\leq i\leq n, \left|\frac{\mathcal{S}_i-\mu_i}{\sigma_i}\right|\leq k
$$

which, in the case of the binomial distribution, translates to

$$
\forall i: 1\leq i\leq n, \left|\frac{\mathcal{S}_i-np_i}{\sqrt{np_i(1-p_i)}}\right|\leq k
$$

This means that in the sequence $\alpha$, the frequency of occurrence of each symbol $x_i$ is within $k$ standard deviations from the mean.

There is a relationship between $k$-typical sequences and the entropy of the information source. If $n$ is sufficiently large, then the probability that a random sequence of length $n$ is $k$-typical is very close to 1. Therefore, the entropy of the information source can be approximated by the entropy of the $k$-typical sequences.

The number of $k$-typical sequences of length $n$ is equal to $m^{nH_m(X)}$.

# [Codes (click to access content)](../5-codes/README.md)

