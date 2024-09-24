## Language Structure

Before studying information sources, it's essential to define a language for representing the messages to be transmitted. In general, a language is a set of symbols and rules that allow constructing messages from these symbols.

### Alphabets and Words

An **alphabet** is a finite set of symbols. For example, our alphabet could be said to consist of the letters of the alphabet. A **symbol** is an element of an alphabet. For instance, the letter "a" is a symbol in our alphabet.

In formal mathematical language, an alphabet $\mathcal{A}$ is a finite (unless explicitly stated otherwise) and non-empty set whose elements are called **symbols**. For example, if $\mathcal{A} = \\{a, b, c\\}$, then $a$, $b$, and $c$ are symbols of $\mathcal{A}$.

Let $\mathcal{A}$ be an alphabet. A **word** $x$ is a finite sequence of symbols from $\mathcal{A}$ in the form

$$
x=a_1a_2\dots a_n, \quad a_i \in \mathcal{A}, \quad i=1,2,\dots,n
$$

We define the **length** of a word $x$ as the number of symbols it contains. The length of a word $x$ is denoted by $|x|$.

Let $\mathcal{A}^n,n\geq 1$ be the set of all words of length $n$ formed by symbols from $\mathcal{A}$.

The number of elements (also called cardinality) of $\mathcal{A}^n$ is $|\mathcal{A}|^n$.

---

#### Example

We have an alphabet $\mathcal{A}=\\{0,1\\}$, and we want to find the set of all words of length 3 formed by symbols from $\mathcal{A}$.

So, $\mathcal{A}^3=\{000,001,010,011,100,101,110,111\}$.

Since $|\mathcal{A}|=2$, the number of elements in $\mathcal{A}^3$ is $|\mathcal{A}|^3=2^3=8$.

---

Given an alphabet $\mathcal{A}$, the set of all finite (non-null) words formed by symbols from $\mathcal{A}$ is denoted by $\mathcal{A}^+$ and is defined as:

$$
\begin{align*}
\mathcal{A}^+&=\mathcal{A}^1\cup\mathcal{A}^2\cup\dots\cup\mathcal{A}^n,\quad n\geq1\\
&= \bigcup_{n\geq1}\mathcal{A}^n
\end{align*}
$$

That is, $\mathcal{A}^+$ is the union of all sets of words of length $n$ formed by symbols from $\mathcal{A}$. It is a set where words of all possible lengths up to a maximum length $n$ exist. This set is somewhat similar to natural language words, where words of different lengths exist.

_How many elements does_ $\mathcal{A}^+$ _have?_

We know that

$$
\begin{align*}
\mathcal{A}^+&= \bigcup_{n\geq1}\mathcal{A}^n\\
&=\mathcal{A}^1\cup\mathcal{A}^2\cup\dots\cup\mathcal{A}^n,\quad n\geq1\\
\end{align*}
$$

Moreover, the number of elements in $\mathcal{A}^n$ is $|\mathcal{A}|^n$. Therefore, the number of elements in $\mathcal{A}^+$ is

$$
\begin{align*}
|\mathcal{A}^+|&=|\mathcal{A}^1|+|\mathcal{A}^2|+\dots+|\mathcal{A}^n|\\
&=|\mathcal{A}|+|\mathcal{A}|^2+\dots+|\mathcal{A}|^n\\
&=\sum_{n\geq1}|\mathcal{A}|^n
\end{align*}
$$

This resembles a geometric series...

$$
\begin{align*}
\sum_{n\geq 1}|\mathcal{A}|^n&=\sum_{n\geq 0}|\mathcal{A}|^n - 1\\
&=\frac{1-|\mathcal{A}|^{n+1}}{1-|\mathcal{A}|} - 1\\
\end{align*}
$$

Therefore, the number of elements in $\mathcal{A}^+$ is

$$
|\mathcal{A}^+|=\frac{1-|\mathcal{A}|^{n+1}}{1-|\mathcal{A}|} - 1
$$

---

#### Example

We have an alphabet $\mathcal{A}=\\{0,1\\}$, and we want to find the set of all finite words (non-null, up to a maximum length of 5) formed by symbols from $\mathcal{A}$. How many elements does $\mathcal{A}^+$ have?

Without constructing each word, we can calculate the number of elements in $\mathcal{A}^+$ using the previous formula. Since $|\mathcal{A}|=2$ and $n=5$, the number of elements in $\mathcal{A}^+$ is

$$
\begin{align*}
|\mathcal{A}^+|&=\frac{1-|\mathcal{A}|^{n+1}}{1-|\mathcal{A}|} - 1\\
&=\frac{1-2^{5+1}}{1-2} - 1\\
&=\frac{1-64}{-1} - 1\\
&=62
\end{align*}
$$

---

For any word $x\in\mathcal{A}^+$ and $1\leq n\leq|x|$, let $x[n]=a_n$, the $n$-th symbol in the sequence. Therefore,

$$
x=x[1]\dots x[|x|]
$$

Given two words $x,y\in\mathcal{A}^+$, we say that $x$ and $y$ are **equal** if and only if:

$$
x = y \Leftrightarrow\begin{cases}
&\left(|x|=|y|\right)\\
&\wedge\left(x[i]=y[i], \forall 1\leq i\leq|x|\right)
\end{cases}
$$

That is, they are equal when they have the same length and all their symbols are the same in the same position.

Similarly, we define the **concatenation** of two words $x,y\in\mathcal{A}^+$ (which we will denote as $xy$) as the word $z\in\mathcal{A}^+$ defined by:

1. $|z| = |x| + |y|$
2. $z[i] = x[i]$ for $1\leq i\leq|x|$
3. $z[|x|+i] = y[i]$ for $1\leq i\leq |y|$

In other words, the concatenation of two words is a new word that contains all the symbols of the first word followed by all the symbols of the second word.

It's easy to see that word concatenation is an **associative** operation, that is, for any $x,y,z\in\mathcal{A}^+$, it holds that

$$
(x y) z = x (y z)
$$

However, word concatenation is **not commutative**, meaning that in general, it is not true that

$$
xy = yx
$$

_You can think of this as "adding strings" in Python... Be careful with the indexing system, as in Python indices start at 0, whereas here we start them at 1._

---

In many cases, it's useful to define an identity element for an operation (in this case, word concatenation). The identity of word concatenation is the empty word, denoted by $\lambda$ (think of the empty string `""` in Python). $\lambda$ has the following properties:

1. $|\lambda| = 0$
2. $\mathcal{A}^0 = \left\\{\lambda\right\\}$
3. $\forall x\in\mathcal{A}^+,\quad x\neq\lambda$
4. $|x| = 0 \Leftrightarrow x = \lambda$

That is, the empty word is the only word of length 0, and it is the only word that has no symbols. If a word has a length of 0, then it is the empty word, and if a word is not the empty word, then it has a length greater than 0.

Thus, we can generate another set, which includes the empty word, denoted by $\mathcal{A}^*$ and defined as

$$
\begin{align*}
\mathcal{A}^* &= \mathcal{A}^+\cup\left\\{\lambda\right\\}\\
&= \mathcal{A}^+\cup\mathcal{A}^0\\
&= \left(\bigcup_{n\geq1}\mathcal{A}^n\right)\cup\mathcal{A}^0\\
&= \bigcup_{n\geq0}\mathcal{A}^n
\end{align*}
$$

We can extend the operation of word concatenation to $\mathcal{A}^\*$, so that for any $x, y \in \mathcal{A}^*$, the above properties of concatenation hold, and also:

$$
\lambda x = x\lambda = x
$$

This makes word concatenation over $\mathcal{A}^*$ an associative operation with an identity element.

---

From word concatenation, we can define the **power** of a word. Given a word $x \in \mathcal{A}^+$ and a non-negative integer $k$, the power of $x$ raised to $k$, denoted as $x^k$, is defined as:

1. $x^0 = \lambda$
2. $x^k = x^{k-1}x$

In other words, the power of a word is the concatenation of the word with itself $k$ times.

---

#### Example

Given the word $x = 010$, we calculate $x^3$ as:

$$
\begin{align*}
x^3 &= x^2x \\
&= (xx)x \\
&= (010010)010 \\
&= 010010010
\end{align*}
$$

---

One immediately observed property is that $\left|x^k\right| = k\left|x\right|$. That is, the length of the power of a word is equal to the product of the length of the word by the exponent of the power.

Additionally, another property is that $\forall n>1,\quad x^n = x \Leftrightarrow x = \lambda$. In other words, a word raised to an exponent greater than 1 is equal to the word itself if and only if the word is the empty word.

---

It is also possible to "_extract_" segments of a word. If we have a word $x \in \mathcal{A}^+$, we define its segment $x[i:j]$ as:

$$
x[i:j] =\begin{cases}
x[i]\dots x[j],\quad 1\leq i\leq j\leq |x| \\
x[i],\quad 1\leq i = j\leq |x| \\
\lambda,\quad\text{otherwise}
\end{cases}
$$

That is, the segment of a word is the subsequence of the word from the $i$-th symbol to the $j$-th symbol, both inclusive. If $i = j$, then the segment is simply the $i$-th symbol, and if $i > j$, the segment is the empty word.

We can quickly deduce that $x = x[1:|x|]$. That is, a word is equal to its segment that goes from the first symbol to the last symbol.

### Alphabetical Orders

Given an alphabet $\mathcal{A}$, it is possible to define an **alphabetical order** on the symbols of $\mathcal{A}$. An alphabetical order is a ranking given by enumerating (without repetition) the symbols of $\mathcal{A}$. If $\mathcal{A}=\{a_1,a_2,\dots,a_n\}$ is an enumeration without repetition, then:

$$
a_i < a_j \Leftrightarrow i < j
$$

That is, the alphabetical order of the symbols of $\mathcal{A}$ follows the order of this enumeration.

---

This alphabetical order can be extended to the words of $\mathcal{A}^*$ in the following way. Given two words $x, y \in \mathcal{A}^+$, we say that $x$ is **less than** $y$ in the alphabetical order if and only if:

$$
x < y \Leftrightarrow \begin{cases}
\left(\exists u\in\mathcal{A}^+:y=xu\right) \\
\vee \left(\exists u,v,w\in\mathcal{A}^*, \exists a,b\in\mathcal{A}: \left(x=uav\right) \wedge \left(y=ubw\right) \wedge \left(a < b\right)\right)
\end{cases}
$$

That is, one word is less than another in the alphabetical order if and only if it is a prefix of the other word, or if both words share a common prefix and the next symbol of one is less than the next symbol of the other. Note that the common prefix can be the empty word since $\lambda$ is a prefix of any word and $u, v, w \in \mathcal{A}^*$.

Note the following trivial properties:

1. $\forall x\in\mathcal{A}^+: \lambda < x$
2. $\forall x, y \in \mathcal{A}^*: x \neq y \Rightarrow ((x<y) \vee (y<x))$
3. Over every alphabet $\mathcal{A}$, there can be $\left|\mathcal{A}\right|!$ different alphabetical orders.

---

#### Example 1

Let the words $x=010$ and $y=011$. What is the alphabetical order relation between $x$ and $y$?

To determine the alphabetical order relation between $x$ and $y$, we first check if $x$ is a prefix of $y$ or vice versa. In this case, $x$ is not a prefix of $y$, and $y$ is not a prefix of $x$. Therefore, we check if they have a common prefix. Here, the common prefix is the word $01$. Consequently, we check if the next symbol of $x$ is less than the next symbol of $y$. In this case, the next symbol of $x$ is 0, and the next symbol of $y$ is 1. Since 0 is less than 1, we conclude that $x < y$ in alphabetical order.

---

### Prefixes, Suffixes, and Segments

Earlier, we briefly defined the segment of a word. Now, we will more precisely define the concepts of prefixes, suffixes, and segments, as we have indirectly used these concepts in the definition of alphabetical orders.

#### Prefixes

We say that for $x, y \in \mathcal{A}^*$, $x$ is a **prefix** of $y$ whenever:

$$
\exists u \in \mathcal{A}^*: y = xu
$$

That is, a word is a prefix of another word if and only if the other word is the concatenation of the first word with any other word.

The following properties hold trivially:

1. $\forall x \in \mathcal{A}^*: \lambda$ is a prefix of $x$ (the empty word is a prefix of any word).
2. $\forall x \in \mathcal{A}^*: x$ is a prefix of $x$ (a word is a prefix of itself).
3. $\forall x, y \in \mathcal{A}^*: x$ is a prefix of $y \Leftrightarrow |x| \leq |y|$ in alphabetical order (if a word is a prefix of another, its length is less than or equal to the length of the word of which it is a prefix).
4. $\forall x, y \in \mathcal{A}^*: x$ is a prefix of $y \Leftrightarrow \exists i: 1 \leq i \leq |y| / x = y[1:i]$ (a word is a prefix of another if and only if it is the segment of the other word from the first symbol to any symbol).
5. $\forall x, y \in \mathcal{A}^*: x$ is a prefix of $y \Rightarrow x \leq y$ in any alphabetical order of $\mathcal{A}$ (if a word is a prefix of another, it is less than or equal to the other word in alphabetical order).

#### Suffixes

Suffixes are defined similarly to prefixes. We say that for $x, y \in \mathcal{A}^*$, $x$ is a **suffix** of $y$ whenever:

$$
\exists u \in \mathcal{A}^*: y = ux
$$

The following properties hold (similar to those for prefixes):

1. $\forall x \in \mathcal{A}^*: \lambda$ is a suffix of $x$ (the empty word is a suffix of any word).
2. $\forall x \in \mathcal{A}^*: x$ is a suffix of $x$ (a word is a suffix of itself).
3. $\forall x, y \in \mathcal{A}^*: x$ is a suffix of $y \Leftrightarrow |x| \leq |y|$ in alphabetical order (if a word is a suffix of another, its length is less than or equal to the length of the word of which it is a suffix).
4. $\forall x, y \in \mathcal{A}^*: x$ is a suffix of $y \Leftrightarrow \exists i: 1 \leq i \leq |y| / x = y[i:|y|]$ (a word is a suffix of another if and only if it is the segment of the other word from any symbol to the last symbol).

No properties related to alphabetical order can be deduced from suffixes, as there is no direct relationship between suffixes and alphabetical orders.

#### Segments

Next, we will give a more precise definition of a segment. Given two words $x,y\in\mathcal{A}^*$, we say that $x$ is a **segment** of $y$ whenever:

$$
\exists u,v\in\mathcal{A}^*:y=uxv
$$

We can see that if $u=\lambda$, then $x$ is a prefix of $y$, and if $v=\lambda$, then $x$ is a suffix of $y$. Therefore, segments are a generalization of prefixes and suffixes. Trivially, if both $u$ and $v$ are the empty word, then $x=y$. Similarly, the following properties hold:

1. $\forall x\in\mathcal{A}^*:\lambda$ is a segment of $x$ (the empty word is a segment of any word).
2. $\forall x\in\mathcal{A}^*:x$ is a segment of $x$ (a word is a segment of itself).
3. $\forall x,y\in\mathcal{A}^*:x$ is a segment of $y \Leftrightarrow |x| \leq |y|$ (if a word is a segment of another, its length is less than or equal to the length of the word of which it is a suffix).
4. $\forall x,y\in\mathcal{A}^*:x$ is a segment of $y \Leftrightarrow \exists i,j: 1\leq i\leq j\leq |y| / x=y[i:j]$ (a word is a segment of another if and only if it is the segment of the other word that goes from any symbol to any other symbol). This is the definition we have used earlier.

### Homomorphisms

Given two alphabets $\mathcal{A}$ and $\mathcal{B}$ (not necessarily distinct), a mapping 

$$
h:\mathcal{A}^\*\rightarrow\mathcal{B}^\*
$$

is a homomorphism whenever:

$$
\forall x,y\in\mathcal{A}^*:h(xy)=h(x)h(y)
$$

That is, homomorphisms preserve word concatenation operations; hence, they preserve the structure of words. Consequently, $\mathcal{B}^\*$ is entirely determined by $\mathcal{A}^\*$ and the homomorphism $h$ over each element of $\mathcal{A}$.

An important property is that $h(\lambda)=\lambda$, meaning that the homomorphism of the empty word is the empty word.

Homomorphisms are a very useful tool for studying the structure of words, as they allow the transformation of words from one alphabet to another while preserving their structure. For example, if we have a homomorphism $h$ that transforms vowels in one alphabet to consonants in another, we can transform words from one alphabet to another while maintaining the structure of the words.

### Left Circular Permutations

Let $a\in\mathcal{A}$, $x,y\in\mathcal{A}^*$ and $x = ay$, then the operation of **left circular permutation**, denoted by $\hookrightarrow$, on $x$ is defined as:

$$
\hookrightarrow(x) = ya
$$

Then:

1. $\forall x\in\mathcal{A}^+:\hookrightarrow(x)=x[2:|x|]x[1]$
2. In particular, if $|x| = 1$, then $\hookrightarrow(x) = x$.

Moreover, repeated application of the left circular permutation on a word $x$ generates a cycle, such that when applied $|x|$ times, the original word $x$ is obtained again. This is denoted as $\hookrightarrow^{|x|}(x) = x$.

### Word Sequences and Orderings

Let $\boldsymbol{x} = \left\langle x_1,x_2,\dots,x_n\right\rangle$ be a sequence of words $x_i\in\mathcal{A}^\*,i=1,\dots,n$, and assume an alphabetical ordering over $\mathcal{A}^*$ (as explained earlier). Then, the ordered sequence $\boldsymbol{z}$ is defined as:

$$
\boldsymbol{z} = \text{ord}\left(\boldsymbol{x}\right)
$$

It is a permutation of $\boldsymbol{x}$ such that:

$$
\boldsymbol{z} = \left\langle x_1',x_2',\dots,x_n'\right\rangle
$$

where $x_i' \leq x_j'$ for any $i,j=1,\dots,n$.

For $\boldsymbol{x}$, we denote its $i$-th component as $x(i)$, with $1\leq i\leq n$.

# [Information Sources (click to access the content)](../4-information-sources/README.md)
