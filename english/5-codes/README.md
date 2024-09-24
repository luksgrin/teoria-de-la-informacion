## Codes

### Introduction

As we have seen at the beginning of the syllabus, there is a component in the information transmission scheme called a **encoder**, which is responsible for transforming messages from the source (`MF`) into a suitable form for transmission through the communication channel and reception (encoded messages, `MC`), where the corresponding decoding process takes place to recover the original source message `MF`.

In a first simplified approach to this scenario, we define the encoding process through a function \( f \) such that

$$
f:\text{\texttt{MF}}\rightarrow\mathcal{P}(\text{\texttt{MC}})
$$

where \( \forall m\in\text{\texttt{MC}}: \left|f(m)\right|<\infty \) (i.e., the results of encoding the message have a finite length). Note that \( \mathcal{P}(C) \) means the power set of \( C \).

Therefore, in this context of information transmission, when a random message \( m \) is emitted, the receiver receives an encoded message \( m'\in\mathcal{P}(C) \). Then, there exists in the receiver a decoding function \( f^\star \):

$$
f^\star:\text{\texttt{MC}}\rightarrow\text{\texttt{MF}}
$$

such that

$$
\forall m\in \text{\texttt{MF}}, \quad\exists m': f^\star\left(m'\right) = m
$$

For now, we will assume that \( \forall m\in \text{\texttt{MF}}, \left|f(m)\right| = 1 \) (but we will see that we can extend to more cases).

### Encodings and Codes

Taking the previous introduction to a more particular (and familiar) case; let \( \mathcal{A} \) be an alphabet (corresponding to the zero-memory information source \( (\mathcal{A},P) \), from which the source messages \( \mathcal{A^+} \) originate) and let \( \mathcal{C} \) be the set of encoded messages `MC` (also known as the set of codes), then an encoding \( f \) is a **bijective** application:

$$
f:\mathcal{A}^+\rightarrow\mathcal{C}
$$

For this encoding to be admissible for an efficient encoding-decoding process, it must have certain characteristics that will be explained later.

Let \( \mathcal{B} \) be an alphabet (code), then \( \mathcal{C}\subseteq\mathcal{B} \). Then an admissible encoding is an injective application

$$
f:\mathcal{A}^+\rightarrow\mathcal{B}^+
$$

where we have that \( f\left(\mathcal{A}^+\right) = \mathcal{C} \). Equivalently, if we take \( f(\lambda) = \lambda \) (and also \( f^{-1}(\lambda) = \{\lambda\} \)), then we can extend this injective application to

$$
f:\mathcal{A}^\*\rightarrow\mathcal{B}^\*
$$

In this scenario, \( \mathcal{A} \) is called the "_source alphabet_" and \( \mathcal{B} \) "_code alphabet_".

### Block Coding

A block encoding \( f \) is an application that assigns to each of the symbols \( a\in\mathcal{A} \) a word from \( \mathcal{B}^+ \), and behaves like a homomorphism, which means that

$$
\forall x\in\mathcal{A}^+,\forall a\in\mathcal{A}: f(ax) = f(a)f(x)
$$

and equivalently

$$
\forall x\in\mathcal{A}^+,\forall a\in\mathcal{A}: f(xa) = f(x)f(a)
$$

and in general

$$
\forall x,y\in\mathcal{A}^+: f(xy) = f(x)f(y)
$$

Thus,

$$
\forall x\in\mathcal{A}^+: f(x) = f(x[1])\dots f(x[|x|])
$$

_(all this is equivalent, and we have seen it before in the definition of homomorphism in the language structure section)._

The set \( f(\mathcal{A})=\{f(a),\quad\forall a\in\mathcal{A}\} \) is called a "_block code_" (or simply "_code_").

#### Example 1

Let us consider the following source alphabets (\( \mathcal{A} \)) and code (\( \mathcal{B} \)):

$$
\begin{align*}
\mathcal{A} &=\{0,1,2,3,4,5,6,7,8,9\}\\
\mathcal{B} &=\{0,1\}
\end{align*}
$$

And also consider the block encoding defined by \( f \):

$$
f(a) = \left(\left\lfloor\frac{a}{2^3}\right\rfloor\mod 2\right)\left(\left\lfloor\frac{a \mod 2^3}{2^2}\right\rfloor\mod 2\right)\left(\left\lfloor\frac{a \mod 2^2}{2^1}\right\rfloor\mod 2\right)\left(\left\lfloor\frac{a \mod 2}{2^0}\right\rfloor\mod 2\right)
$$

We clearly have that 

$$
f(\mathcal{A}) = \{0000, 0001, 0010, 0011, 0100, 0101, 0110, 0111, 1000, 1001\}
$$

It can be seen that \( f(\mathcal{A})\subset\mathcal{B}^4 \) (because there are words in \( \mathcal{B}^4 \) that do not appear in \( f(\mathcal{A}) \), such as \( 1111 \)). \( f \) is a block encoding since it assigns to each character of the source alphabet a word formed by the code alphabet.

#### Example 2: Morse

In Morse, the code alphabet consists of the elements \( \{.,-,\text{\texttt{pause}}\} \):

| Source Alphabet | Code |
|:----------------|:-------|
| A | .- |
| B | -... |
| C |  -.-. |
| D | -.. |
| E | . |
| F | ..-. |
| G | --. |
| H | .... |
| I | .. |
| J | .--- |
| K | -.- |
| L | .-.. |
| M | -- |
| N | -. |
| P | .--. |
| Q | --- |
| S | ... |
| T | - |
| U | ..- |
| V | ...- |
| W | .-- |
| X | -..- |
| Y | -.-- |
| Z | --.. |
| 1 | .---- |
| 2 | ..--- |
| 3 | ...-- |
| 4 | ....- |
| 5 | ..... |
| 6 | -.... |
| 7 | --... |
| 8 | ---.. |
| 9 | ----. |
| 0 | ----  |

When encoding a message in Morse, a separation pause must be introduced after the code associated with each symbol.

#### Example 3: ASCII

ASCII (_American Standard Code for Information Interchange_) is a block encoding of constant length (unlike Morse, which was of variable length) with code alphabet \( \mathcal{B}=\{0,1\} \) and \( f(\mathcal{A})=\{0,1\}^7 \).

#### Example 4: Extended ASCII

Extended ASCII differs from ASCII in that \( f(\mathcal{A})=\{0,1\}^8 \) (the length of the words is greater).

#### Unicode

Unicode is a universal alphabet along with the encoding of its symbols (more than a million) using a fixed-length block code and incorporates all the symbols from extended ASCII. From Unicode, among others, the variable-length block encodings UTF (Unicode Transformation Format) can be found: UTF-8 (the most common), UTF-16, and UTF-32.

### Uniquely Decodable Block Encoding

A block encoding \( f \) is called **non-singular** if

$$
\forall a,b\in\mathcal{A}: a\neq b\Rightarrow f(a)\neq f(b)
$$

#### Example 1

Let \( \mathcal{A} = \{a_1,a_2,a_3,a_4\}, \mathcal{B} = \{0,1\} \) and \( f \) defined by:

$$
f = \begin{cases}
f(a_1) &= 0\\
f(a_2) &= 11\\
f(a_3) &= 00\\
f(a_4) &= 01\\
\end{cases}
$$

It is straightforward to see that \( f \) is non-singular. However, if we extend this to words, this no longer holds since certain words from \( \mathcal{A}^+ \) are not uniquely decodable. For example:

- \( a_1a_1a_1 \neq a_1a_3 \neq a_3a_1 \) but \( 000 = f(a_1a_1a_1) = f(a_1a_3) = f(a_3a_1) \)
- \( a_1a_1a_2 \neq a_3a_2 \) but \( 0011 = f(a_1a_1a_2) = f(a_3a_2) \)

---

The extension of order \( n \geq 1 \) of a block encoding

$$
f:\mathcal{A}^+\rightarrow\mathcal{B}^+
$$

is defined as

$$
f^{(n)}:\left(\mathcal{A}^n\right)^+\rightarrow\mathcal{B}^+
$$

taking as symbols the words of \( \mathcal{A}^n \) such that

$$
\forall x\in\mathcal{A}^n: f^{(n)}(x)=f(x)
$$

The extension of order \( n \) of a block encoding is also taken, for each case, with the corresponding source alphabet \( \mathcal{A} \).

A block encoding \( f \) is said to be uniquely decodable if and only if its extension of order \( n \) is **non-singular** for every \( n \geq 1 \).

An important property arises: a block encoding is uniquely decodable if and only if it is injective.

We will say that a block code is uniquely decodable if it comes from a uniquely decodable block encoding, which allows us to define \( f^{-1}:\mathcal{B}^+\rightarrow\mathcal{A}^+ \).

**Unique Factorization Property:**

1. If \( f:\mathcal{A}^+\rightarrow\mathcal{B}^+ \) is a uniquely decodable block encoding, then it holds that \( \forall x_1,\dots,x_n,y_1,\dots,y_m\in f(\mathcal{A}) \):

$$
x_1\dots x_n=y_1\dots y_m \Rightarrow (n = m)\wedge\left(x_i=y_i,\quad i = 1,\dots,n\right)
$$

2. \( f:\mathcal{A}^+\rightarrow\mathcal{B}^+ \) (which is a block encoding) is uniquely decodable if and only if it satisfies the aforementioned property, and is also non-singular.

The question of whether a block encoding \( f \) is uniquely decodable or not is algorithmically decidable (i.e., _there exists an algorithm to determine whether it is uniquely decodable or not_).

The following algorithm returns `true` when \( f \) is uniquely decodable and `false` otherwise:

$$
\begin{align*}
&\text{if }\left(\exists a,b\in\mathcal{A}: (a\neq b)\wedge(f(a)=f(b))\right)\text{then:}\\
&\quad\quad\text{return \texttt{false}}\\
&A=\left\{u: \left(\exists x,y\in f(\mathcal{A}):(x\neq y)\wedge (xu=y)\right)\right\}\\
&\text{if}\left(A\cap f(A)\neq\emptyset\right)\text{ then:}\\
&\quad\quad\text{return \texttt{false}}\\
&A'=\emptyset\\
&\text{while }A\neq\emptyset:\\
&\quad\quad A'=A\cup A'\\
&\quad\quad B = \left\{u:\left(\left(\exists x\in f(\mathcal{A}): xu\in A\right)\vee\left(\exists x\in A: xu\in f(\mathcal{A})\right)\right)\right\}\\
&\quad\quad A = B - A'\\
&\quad\quad\text{if }\left(A\cap f(\mathcal{A})\neq\emptyset\right)\text{ then:}\\
&\quad\quad\quad\quad\text{return \texttt{false}}\\
&\text{return \texttt{true}}\\
\end{align*}
$$

Let \( f:\mathcal{A}^+\rightarrow\mathcal{B}^+ \) be a non-singular block encoding. If all the words of the block code have exactly the same length, then the code is uniquely decodable.

_Think of Example 1 in this section. Where did the problems arise when decoding? They arose from the fact that not all words in the block code had the same length._

### McMillan's Inequality

If \( f:\mathcal{A}^+\rightarrow\mathcal{B}^+ \) is a uniquely decodable block encoding and \( \left|\mathcal{B}\right|=k \), then

$$
\sum_{x\in f(\mathcal{A})} k^{-\left|x\right|}\leq 1
$$

#### Example 1

Recalling the previous example of the following source alphabets \( (\mathcal{A}) \) and code \( (\mathcal{B}) \):

$$
\begin{align*}
\mathcal{A} &=\left\{0,1,2,3,4,5,6,7,8,9\right\}\\
\mathcal{B} &=\left\{0,1\right\}
\end{align*}
$$

with 

$$
f(\mathcal{A}) = \left\{0000, 0001, 0010, 0011, 0100, 0101, 0110, 0111, 1000, 1001\right\}
$$

McMillan's inequality should hold since it is a uniquely decodable block encoding:

$$
\sum_{x\in f(\mathcal{A})} k^{-\left|x\right|} = \sum_{x\in f(\mathcal{A})} 2^{-4} = \frac{10}{16} < 1
$$

We quickly see that it holds.

_What condition should be met for strict equality?_

Now imagine that we have

$$
\begin{align*}
\mathcal{A} &=\left\{0,1,2,3,4,5,6,7,8,9,a,b,c,d,e,f\right\}\\
\mathcal{B} &=\left\{0,1\right\}
\end{align*}
$$

with 

$$
f(\mathcal{A}) = \left\{0000, 0001, 0010, 0011, 0100, 0101, 0110, 0111, 1000, 1001, 1010, 1011, 1100, 1101, 1110, 1111\right\}
$$

_(Doesn't this seem familiar? It is the binary representation of hexadecimal.)_

For this case:

$$
\sum_{x\in f(\mathcal{A})} k^{-\left|x\right|} = \sum_{x\in f(\mathcal{A})} 2^{-4} = \frac{16}{16} = 1
$$

Clearly, when \( f(\mathcal{A})\subset\mathcal{B}^+ \), then the inequality is strict. But when \( f(\mathcal{A})=\mathcal{B}^+ \), then we have equality.

### Instantaneous Codes

Let's start by observing an example. Consider the uniquely decodable encoding \( f(a)=0 \) and \( f(b)=01 \). To decode \( x=01 \), we would need to know about the existence of the \( 1 \), since with only the \( 0 \), we have ambiguity and do not know whether it is \( a \) or \( b \). By reading the \( 1 \), we resolve this and can decode \( x \) as \( b \). That is, until we read the entire word, we cannot determine how to decode it.

This situation worsens the longer the word is, and can lead to decoding being impractical.

Now consider the uniquely decodable encoding \( f(a)=0 \), \( f(b)=01 \), and \( f(c)=11 \). Let \( x=01^n \) with \( n\geq 1 \). We have that

$$
f^{-1}(x) = \begin{cases}
ac^m & \quad\text{if } n \text{ is even, with } m=\frac{n}{2}\\
bc^m & \quad\text{if } n \text{ is odd, with } m=\frac{n-1}{2}
\end{cases}
$$

Let's look at a series of examples:

- \(f^{-1}(x)=f^{-1}(01^6)=f^{-1}(0111111)=accc\)
- \(f^{-1}(x)=f^{-1}(01^{11})=f^{-1}(011111111111)=bccccc\)

To decode, it is essential to know how many \(1\)s we have in the word \(x\). We cannot find this out without reading the entire word first (regardless of how long it is) before decoding.

A code that is uniquely decodable is said to be **instantaneous** when it is possible to decode each symbol of \(\mathcal{A}\) from each message without needing more symbols from \(\mathcal{B}\) than are strictly necessary. That is, if

$$
h:\mathcal{A}^\*\rightarrow\mathcal{B}^\*
$$

is a uniquely decodable block encoding, then it is instantaneous as long as

$$
\forall x\in\mathcal{A}^*, \exists u,v\in\mathcal{A},\exists a\in\mathcal{A}: x=uav
$$

such that

$$
y=h(x)=h(u)h(a)h(v)
$$

Then to decode \(y\) to \(x\), to decode the segment \(h(a)\) to \(a\) immediately, regardless of the suffix \(h(v)\), one only needs to process the segment of \(y\) associated with \(h(a)\).

Thus, to decode the segment \(y\left[\left|h(u)\right|+1:\left|h(u)\right|+n\right]\) with, in this case, \(n = \left|h(a)\right|\):

$$
\begin{align*}
y\left[\left|h(u)\right|+1:\left|h(u)\right|+n\right] &= y\left[\left|h(u)\right|+1:\left|h(u)\right|+\left|h(a)\right|\right]\\
&= y\left[\left|h(u)\right|+1:\left|h(ua)\right|\right]
\end{align*}
$$

is sufficient, in any case, for correct decoding. This means that

$$
\forall a,b\in\mathcal{A}:h(a)\text{ is a prefix of }h(b)\Rightarrow a = b
$$

Once again, we say that a block code is instantaneous when it comes from an instantaneous block encoding. We can also call it a prefix block code or simply a prefix code.

---

Let \(f:\mathcal{A}^*\rightarrow\mathcal{B}^*\) be a block encoding. We will say that \(f\) is **stable** if and only if:

1. It is uniquely decodable.
2. \(\forall x\in\mathcal{A}^*,f(x)=u\) holds that \(\forall v\in\mathcal{B}^*\), if \(\exists y\in\mathcal{A}^*,f(y)=uv\Rightarrow y=xz\) for some \(z\in\mathcal{A}^*\)

We then have the following property: let \(f:\mathcal{A}^*\rightarrow\mathcal{B}^*\) be a block encoding. Then, **\(f\)** is stable if and only if it is instantaneous.

---

### Kraft's Inequality

Let’s see how qualitative characteristics translate quantitatively. Let the block encoding:

$$
f:\mathcal{A}^\*\rightarrow\mathcal{B}^\*
$$

with \(\mathcal{A}=\{a_1,\dots,a_n\}\), \(\mathcal{B}=\{b_1,\dots,b_k\}\) and \(f(\mathcal{A})=\{x_1,\dots,x_n\}\), with \(l_i = |x_i|\). Kraft's inequality gives us the **necessary** and **sufficient** condition for the existence of an instantaneous block code with code words of lengths \(l_1,\dots,l_n\) over an alphabet with \(k\) symbols:

$$
\sum_{1\leq i\leq n}k^{-l_i}\leq 1
$$

When this is a strict equality, it is known as Kraft's equality.

As an immediate consequence, from McMillan's inequality, it follows that for every uniquely decodable code, there exists an instantaneous code with the same lengths of its block code words.

### Complete Codes

Let the block encoding:

$$
f:\mathcal{A}^\*\rightarrow\mathcal{B}^\*
$$

be complete if:

1. It is instantaneous.
2. It satisfies \(\forall x\in\mathcal{B}^*,\exists a\in\mathcal{A}^*\Rightarrow\left(\left(h(a)\text{ is a prefix of }x\right)\vee\left(x\text{ is a prefix of }h(a)\right)\right)\).

We then have the following property: if \(|\mathcal{A}|\geq 2\) and \(|\mathcal{B}|=2\), then there exists only one complete block encoding

$$
f':\mathcal{A}^\*\rightarrow\mathcal{B}^\*
$$

such that \(\forall a\in\mathcal{A}:\left|f'(a)\right|\leq\left|f(a)\right|\).

Again, a block code is complete if it comes from a complete block encoding.

## Information Source Encodings

### Average Length of a Code

For \(\mathcal{A}^\*\) and \(\mathcal{B}^\*\), it is possible to define more than one instantaneous or uniquely decodable encoding. This then requires us to try to choose the most efficient ones with the aim of achieving optimal information transmission.

A natural selection criterion (even though it is not the only possible one) is that of minimum average length.

Let a block code that associates the symbols of a **zero-memory information source** \(FI = (\mathcal{A},P)\) where \(\mathcal{A}=\{a_1,\dots,a_n\}\) and \(|\mathcal{B}|=k\) through the encoding \(f:\mathcal{A}^*\rightarrow\mathcal{B}^*\) with the words \(f(a_i)=x_i\), with \(l_i=|x_i|,i=1,\dots,n\). We define the average length as the **expected value of the length of the block codes**:

$$
\mathcal{L}_f=\mathbb{E}[l]=\mathbb{E}[|x|]=\mathbb{E}[|f(a)|]=\sum_{i=1}^n |f(a_i)|p(a_i)
$$

### Optimal Codes

Let a uniquely decodable block code that associates the symbols of the zero-memory source \(FI = (\mathcal{A},P)\) with words formed by an alphabet \(|\mathcal{B}|=k\). We will say it is **compact** or **optimal** concerning the information source if its average length is less than or equal to the average length of each of the uniquely decodable block codes that can be defined between the source and code alphabets with \(k\) symbols.

It arises from here the observation that, since this only affects the lengths, the search can be reduced by McMillan's inequality to instantaneous codes.

Moreover, if we have \(|\mathcal{A}|\geq 2\) and \(|\mathcal{B}| = 2\), if a block code is optimal, then it is complete.

The property also holds that if \(f\) is an optimal code, then

$$
\forall a,b\in\mathcal{A}:p(a)<p(b)\Rightarrow |f(a)|\geq|f(b)|
$$

### First Shannon Theorem (Noiseless Coding Theorem)

Consider a zero-memory source \(FI\) whose symbols \(a_1,\dots,a_n\) with probabilities \(p_1,\dots,p_n\) are encoded each into a word of length \(l_i\) in an alphabet with \(k\) symbols through the encoding \(f\). Then we have that \(H_k(FI)\leq\mathcal{L}_f\).

If we assume that we are in the case of equality, that is, \(H_k(FI)=\mathcal{L}_f\):

$$
\begin{align*}
H_k(FI)&=\mathcal{L}_f\\
\sum_{i=1}^np_i\log_k\left(\frac{1}{p_i}\right)&=\sum_{i=1}^np_il_i
\end{align*}
$$

we infer that if we take code lengths \(l_i=|x_i|=|f(a_i)|\), we will have that the codes obtained for each \(a_i\) will be instantaneous, complete, and optimal with an average length that matches the entropy in base \(k\) of the information source (clearly assuming that \(\log_k\left(\frac{1}{p_i}\right)\) is an integer \(\forall 1\leq i\leq n\)).

Let's see an example: suppose we have \( FI = \left( \{ a_1, a_2, a_3 \}, \left\{ \frac{1}{2}, \frac{1}{4}, \frac{1}{4} \right\} \right) \). Then the block coding:

$$
h: \\{ a_1, a_2, a_3 \\}^* \rightarrow \\{ 0, 1 \\}^\*
$$

defined by taking the lengths of the codes as \( \log \left( \frac{1}{p_i} \right) \):

$$
h = \begin{cases}
h(a_1) &= 1 \\
h(a_2) &= 00 \\
h(a_3) &= 01
\end{cases}
$$

is instantaneous, complete, and optimal with \( \mathcal{L}_h = H(FI) \).

But what happens if it turns out that \( \log_k \left( \frac{1}{p_i} \right) \) are not integers? It seems intuitive and appropriate in this context to round the obtained value up, to choose \( l_i \) (although clearly in this case, the obtained code does not have to be optimal). So if \( l_i = \left\lceil \log_k \left( \frac{1}{p_i} \right) \right\rceil \), it follows that

$$
\log_k \left( \frac{1}{p_i} \right) \leq l_i \leq \log_k \left( \frac{1}{p_i} \right) + 1
$$

It can be proven that the Kraft inequality holds. Let’s take \( \log_k \left( \frac{1}{p_i} \right) \leq l_i \):

$$
\begin{align*}
\log_k \left( \frac{1}{p_i} \right) & \leq l_i \\
k^{\log_k \left( \frac{1}{p_i} \right)} & \leq k^{l_i} \\
\frac{1}{p_i} & \leq k^{l_i} \\
\frac{1}{k^{l_i}} & \leq p_i \\
k^{-l_i} & \leq p_i, \quad \forall 1 \leq i \leq n \\
\sum_{i=1}^n k^{-l_i} & \leq \sum_{i=1}^n p_i \\
\sum_{i=1}^n k^{-l_i} & \leq 1
\end{align*}
$$

Consequently, instantaneous block codes can be associated with them.

Returning to the following inequality:

$$
\log_k \left( \frac{1}{p_i} \right) \leq l_i \leq \log_k \left( \frac{1}{p_i} \right) + 1
$$

Multiplying all terms by \( p_i \):

$$
p_i \log_k \left( \frac{1}{p_i} \right) \leq p_i l_i \leq p_i \log_k \left( \frac{1}{p_i} \right) + p_i
$$

and summing since the inequality holds \( \forall 1 \leq i \leq n \):

$$
\begin{align*}
\sum_{i=1}^n p_i \log_k \left( \frac{1}{p_i} \right) & \leq \sum_{i=1}^n p_i l_i \leq \sum_{i=1}^n p_i \log_k \left( \frac{1}{p_i} \right) + \sum_{i=1}^n p_i \\
H_k(FI) & \leq \mathcal{L}_f \leq H_k(FI) + \sum_{i=1}^n p_i \\
H_k(FI) & \leq \mathcal{L}_f \leq H_k(FI) + 1 \\
\end{align*}
$$

This also holds for any optimal code, which constitutes the initial formulation of Shannon's first theorem.

Since this can also be applied to any degree \( m \) extension of a zero-memory source...

$$
\begin{align*}
H_k \left( FI^{(m)} \right) & \leq \mathcal{L}_f^m \leq H_k \left( FI^{(m)} \right) + 1 \\
m H_k \left( FI \right) & \leq \mathcal{L}_f^m \leq m H_k \left( FI \right) + 1 \\
H_k \left( FI \right) & \leq \frac{\mathcal{L}_f^m}{m} \leq H_k \left( FI \right) + \frac{1}{m} \\
\end{align*}
$$

Thus obtaining **Shannon's first theorem**, which is one of the fundamental theorems of information theory.

An interesting property arises when we try to see what happens when the degree \( m \) extension of our zero-memory information source emits long words. For this, we need to see what happens when \( m \to \infty \):

$$
\begin{align*}
\lim_{m \to \infty} H_k \left( FI \right) & \leq \lim_{m \to \infty} \frac{\mathcal{L}_f^m}{m} \leq \lim_{m \to \infty} H_k \left( FI \right) + \lim_{m \to \infty} \frac{1}{m} \\
H_k \left( FI \right) & \leq \lim_{m \to \infty} \frac{\mathcal{L}_f^m}{m} \leq H_k \left( FI \right) + 0 \\
\end{align*}
$$

Since \( \lim_{m \to \infty} \frac{\mathcal{L}_f^m}{m} \) is bounded above and below by \( H_k \left( FI \right) \), we have proven through the "_sandwich theorem_" that

$$
\lim_{m \to \infty} \frac{\mathcal{L}_f^m}{m} = H_k \left( FI \right)
$$

Note that \( \frac{\mathcal{L}_f^m}{m} \) is the average number of symbols from the code alphabet (\( \mathcal{B} \)) used in the encoding of a symbol from the source alphabet (\( \mathcal{A} \)) when sequences of length \( m \) are emitted, that is, as symbols from the alphabet \( \mathcal{A}^{(m)} \).

---

#### Applied Example

Let a zero-memory source \( FI \) defined by \( \mathcal{A} = \{ a_1, a_2, a_3 \} \) with \( P = \left\{ \frac{3}{4}, \frac{1}{12}, \frac{2}{12} \right\} \), and additionally \( \mathcal{B} = \{ 0, 1 \} \). Let's build a table using `python`, `pandas`, and `numpy`:

```python
import pandas as pd
import numpy as np
df = pd.DataFrame(
    np.array([[3/4, 1/12, 2/12]]).T,
    columns=["p"],
    index=["a_1", "a_2", "a_3"]
)
```

resulting in the table:

|    |         p |
|:---|----------:|
| a1 | 0.75      |
| a2 | 0.0833333 |
| a3 | 0.166667  |

_(if you want to generate tables for markdown or latex from a `pandas` `DataFrame`, you can use the methods `DataFrame.to_markdown()` and `DataFrame.to_latex()`)_

Our next step is to calculate the information $I(a_i) = \log\left(\frac{1}{p_i}\right)$ for each symbol:

```python
df["log2(1/p)"] = np.log2(1/df["p"])
```

resulting in the table:

|    |         $p$ |   $\log_2(1/p)$ |
|:---|----------:|------------:|
| $a_1$ | 0.75      |    0.415037 |
| $a_2$ | 0.0833333 |    3.58496  |
| $a_3$ | 0.166667  |    2.58496  |

Next, we calculate the lengths $l_i = \left\lceil\log\left(\frac{1}{p_i}\right)\right\rceil$:

```python
df["l"] = np.ceil(df["log2(1/p)"])
```

resulting in the table:

|    |         $p$ |   $\log_2(1/p)$ |   l |
|:---|----------:|------------:|----:|
| $a_1$ | 0.75      |    0.415037 |   1 |
| $a_2$ | 0.0833333 |    3.58496  |   4 |
| $a_3$ | 0.166667  |    2.58496  |   3 |

Therefore, we can propose an instantaneous code given by these lengths and using the previously mentioned code alphabet. For example:

|    |         $p$ |   $\log_2(1/p)$ |   l | codigo |
|:---|----------:|------------:|----:|-------:|
| $a_1$ | 0.75      |    0.415037 |   1 |   1 |
| $a_2$ | 0.0833333 |    3.58496  |   4 |  0001 |
| $a_3$ | 0.166667  |    2.58496  |   3 |   001 |

If we wanted to calculate the average length

```python
(df["p"]*df["l"]).sum()
```

we obtain $L_f\approx 1.58$. If we wanted to calculate the entropy

```python
(df["p"]*df["log2(1/p)"]).sum()
```

resulting in $H(FI) \approx 1.04$.

### Performance and Redundancy of a Uniquely Decodable Code

In the context we were discussing, the performance $\eta$ of a code is defined as

$$
\eta = \frac{H_k(FI)}{L_f}
$$

and the redundancy as

$$
1 - \eta = 1 - \frac{H_k(FI)}{L_f} = \frac{L_f - H_k(FI)}{L_f}
$$

An optimal code has maximum performance and minimum redundancy.
