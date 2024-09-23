## Fuentes de Información

Una fuente de información se define como una tupla $(\mathcal{S},P)$ donde

- $\mathcal{S}$ es un conjunto de símbolos que pueden ser emitidos por la fuente (un alfabeto).
- $P$ es una distribución de probabilidades asociada (a la emisión) de lo los símbolos.

Las fuentes de información pueden ser contínuas (con un número de mensajes no numerable) o discretas (con un número de mensajes numerable o finito). En este curso nos centraremos en el caso discreto, por ende $S$ será un conjunto finito.

Claramente, $\forall s\in\mathcal{S}, 0\leq P(s)\leq 1$, y $\sum_{s \in\mathcal{S}} P(s) = 1$ (debido a los Axiomas de Kolmogorov).

### Fuentes de Información de Memoria Nula

En una fuente de información de memoria nula, la emisión de cada símbolo $s_i$ es independiente de los símbolos emitidos anteriormente. En este caso, la probabilidad de emitir un símbolo $s_i$ es constante e igual a $P(s_i)$.

La entropía de una fuente de información de memoria nula se define como

$$
H(\mathcal{S}) = -\sum_{s\in\mathcal{S}} P(s)\log\left(P(s)\right)
$$

### Extensión de grado $m$

Podemos imaginarnos la fuente de información de memoria nula como una máquina que emite secuencias de $x$ símbolos, palabras, $x\in\mathcal{S}^+$, de modo que los símbolos sucesivamente emitidos se eligen de acuerdo con las probabilidades $P(s)$.

Sea entonces $|x|=m$, definimos la extensión de grado $m$ de la fuente de información de memoria nula como el par $\left(\mathcal{S}^m, P^m\right)$, donde 

$$
\forall x\in\mathcal{S}^m:P(x)=\prod_{1\leq i\leq m}P(x[i])
$$

Y trivialmente, la entropía 

$$
\begin{align*}
H\left(\mathcal{S}^m\right)&=-\sum_{x\in\mathcal{S}^m}P(x)\log\left(P(x)\right)\\
&=-\sum_{x\in\mathcal{S}^m}\left(\prod_{1\leq i\leq m}P(x[i])\right)\log\left(P(\prod_{1\leq i\leq m}P(x[i]))\right)
\end{align*}
$$

En lugar de calcular los productos de probabilidades de los símbolos para cada una de las palabras de la extensión de grado $m$, se puede demostrar el siguiente útil resultado:

$$
H\left(\mathcal{S}^m\right)=mH(\mathcal{S})
$$

### Fuentes de Markov (fuente de información con memoria, de orden $m$)

En una fuente de Markov, la emisión de cada símbolo $s_i$ depende de los $m$ símbolos emitidos anteriormente (en muchas aplicaciones). En este caso, la probabilidad de emitir un símbolo $s_i$ depende de los $m$ símbolos anteriores, y se denota como la probabilidad condicional $P(s_i|s_{i-1},\ldots,s_{i-m})$, con

$$
\sum_{i=1}^{m}P(s_i|s_{i_1},\ldots,s_{i_m})= 1,\quad i_k = 1,2,\dots,n
$$

A la secuencia de símbolos emitidos se les llama **cadena de Markov**. Los estados de una fuente de Markov (de orden $m$) serán todas las posibles combinaciones de $m$ símbolos $n^m$.

Dada una fuente de Markov de orden $m$, se puede establecer su diagrama de estados que muestra los estados y las probabilidades entre ellos.

---

#### Ejemplos

A partir de un alfabeto binario $\left\\{0,1\right\\}$, se puede definir una fuente de Markov de orden 2 con los siguientes estados y probabilidades condicionales:

- $P(0|00)=P(1|11)=0.7$
- $P(1|00)=P(0|11)=0.3$
- $P(0|01)=P(1|10)=P(0|10)=P(1|01)=0.5$

El diagrama de estados es el siguiente:

![Markov diagram](./img/fuente-de-markov-diagrama-de-estados.svg)

---

Se dice que una fuente de Markov es ergódica si es posible pasar de cualquier estado a cualquier otro estado en un número finito de pasos.

---

#### Ejemplo

Una fuente ergódica podría ser la anterior (podemos alcanzar cualquier estado en un número finito de pasos a partir de otro estado).

Ejemplo de diagrama de estados de una fuente **no** ergódica:

![Non ergodic Markov diagram](./img/fuente-de-markov-no-ergódico.svg)

Nótese que el nodo interior es un estado absorbente. Es decir, una vez que se llega a ese estado, no se puede salir de él.

---

Una fuente de Markov es homogénea si las probabilidades condicionales no cambian con el tiempo.

Se dice que una fuente está en estado estacionario si la probabilidad de observación de sus estados no cambia con el tiempo. Las probabilidades se pueden obtener mediante la ecuación $v=\pi\Pi$, donde $\pi$ es el vector de probabilidad de los estados y $\Pi$ es la matriz de transición.

---

#### Ejemplo

Volviendo al ejemplo inicial, la matriz de probabilidades tiene la siguiente forma:

$$
\Pi = \begin{matrix}
& \begin{matrix} 00 & 01 & 10 & 11 \end{matrix} \\\
\begin{matrix} 00 \\\ 01 \\\ 10 \\\ 11 \end{matrix} & \begin{pmatrix} 0.7 & 0.5 & 0.5 & 0.3 \\\ 0 & 0 & 0.5 & 0.5 \\\ 0.5 & 0.5 & 0 & 0 \\\ 0.3 & 0.5 & 0.5 & 0.7 \end{pmatrix}
\end{matrix}
$$

Véase que cada fila suma 1 (debido a los axiomas de Kolmogorov). Si cada columna sumase 1, entonces la matriz es doblemente estocástica y todos los estados son equiprobables.

Vayamos al cálculo de probabilidades de estados en régimen estacionario. Para ello, nos definimos las siguientes ecuaciones:

$$
\begin{align*}
&P(00) = P(0|00)\cdot P(00) + P(0|10)\cdot P(10)\\
&P(01) = P(1|00)\cdot P(00) + P(1|10)\cdot P(10)\\
&P(11) = P(1|01)\cdot P(01) + P(1|11)\cdot P(11)\\
&P(00) + P(01) + P(10) + P(11) = 1
\end{align*}
$$

Nótese que la última ecuación surge por uno de los axiomas de Kolmogorov, ya que si incluyésemos el estado $01$ en la primera ecuación, tendríamos una ecuación redundante (y por ende un sistema singular; con infinitas soluciones). Conocemos las probabilidades condicionaes, por lo que podemos resolver el sistema de ecuaciones:

$$
\begin{align*}
&P(00) = 0.7\cdot P(00) + 0.5\cdot P(10)\\
&P(01) = 0.3\cdot P(00) + 0.5\cdot P(10)\\
&P(11) = 0.5\cdot P(01) + 0.7\cdot P(11)\\
&P(00) + P(01) + P(10) + P(11) = 1
\end{align*}
$$

Este sistema tiene la siguiente solución:

$$
\pi = \begin{pmatrix} P(00) \\ P(01) \\ P(10) \\ P(11) \end{pmatrix} = \begin{pmatrix} \frac{5}{16} \\ \frac{3}{16} \\ \frac{3}{16} \\ \frac{5}{16} \end{pmatrix}
$$

Ahora, con esta información podemos calcular las probabilidades de aparición de cada símbolo:

$$
\begin{align*}
&P(0) = P(00) + P(10) = \frac{5}{16} + \frac{3}{16} = \frac{8}{16} = \frac{1}{2}\\
&P(1) = P(01) + P(11) = \frac{3}{16} + \frac{5}{16} = \frac{8}{16} = \frac{1}{2}
\end{align*}
$$

---

### Fuentes afines (adjuntas) de una fuente de Markov

Dada una fuente de Markov de orden $m$ con un alfabeto $\mathcal{S}$ y una distribución de probabilidad $P$, denominaremos a la fuente afín como a la fuente de memoria nula $(\mathcal{S},P)$. Es decir, la fuente afín es la fuente de memoria nula que emite los mismos símbolos que la fuente de Markov.

---

#### Ejemplo

Para el ejemplo de la fuente de Markov de orden 2, la fuente afín sería la fuente de memoria nula con $\mathcal{S}=\left\\{0,1\right\\}$ y $P=\left\\{\frac{1}{2},\frac{1}{2}\right\\}$.

---

Para el cálculo de entropía de una fuente de Markov de orden $m$, sobre un alfabeto $\mathcal{S}=\left\\{s_1,s_2,\dots,s_n\right\\}$ y distribución de probabilidad condicional $P(s_i|s_{i_1},\dots,s_{i_m})$, se cumple que $p(s_i, s_{i_1},\dots,s_{i_m}) = p(s_i|s_{i_1},\dots,s_{i_m})\cdot p(s_{i_1},\dots,s_{i_m})$, lo cual nos permite calcular la entropía condicional:

$$
H(\mathcal{S}|s_{i_1},\dots,s_{i_m}) = -\sum_{i=1}^{n}p(s_i|s_{i_1},\dots,s_{i_m})\log\left(p(s_i|s_{i_1},\dots,s_{i_m})\right)
$$

Por lo tanto, la entropía de la fuente de Markov de orden $m$ es:

$$
\begin{align*}
H(\mathcal{S}) &= \sum_{\mathcal{S}^m}p(s_{i_1},\dots,s_{i_m})H(\mathcal{S}|s_{i_1},\dots,s_{i_m})\\
&= -\sum_{\mathcal{S}^m}p(s_{i_1},\dots,s_{i_m})\left(-\sum_{s_i\in\mathcal{S}}p(s_i|s_{i_1},\dots,s_{i_m})\log\left(p(s_i|s_{i_1},\dots,s_{i_m})\right)\right)\\
&= -\sum_{\mathcal{S}^{m+1}}p(s_i, s_{i_1},\dots,s_{i_m})p(s_i|s_{i_1},\dots,s_{i_m})\log\left(p(s_i|s_{i_1},\dots,s_{i_m})\right)\\
&= -\sum_{\mathcal{S}^{m+1}}p(s_{i_1},\dots,s_{i_m},s_i)\log\left(p(s_i|s_{i_1},\dots,s_{i_m})\right)\\
\end{align*}
$$

#### Ejemplo

Tomemos una fuente de Markov de orden 2 definida por la siguientes probabilidades condicionales:

| $s_js_ks_i$ | $P(s_i\|s_js_k)$ |
|:---------------|:-------------------|
| 000            | 0.8                |
| 001            | 0.2                |
| 010            | 0.5                |
| 011            | 0.5                |
| 100            | 0.5                |
| 101            | 0.5                |
| 110            | 0.2                |
| 111            | 0.8                |

Podemos calcular las probabilidades en estado estacionario:

$$
\begin{align*}
P(00) &= P(0|00)\cdot P(00) + P(0|10)\cdot P(10)\\
P(01) &= P(1|00)\cdot P(00) + P(1|10)\cdot P(10)\\
P(10) &= P(0|01)\cdot P(01) + P(0|11)\cdot P(11)\\
1 &= P(00) + P(01) + P(10) + P(11)
\end{align*}
$$

Reescribamos el sistema de ecuaciones para luego poder pasarlo a un sistema matricial:

$$
\begin{align*}
\left(P(0|00) - 1\right)\cdot P(00) + P(0|10)\cdot P(10) &= 0\\
P(1|00)\cdot P(00) + P(1|10)\cdot P(10) - P(01)&= 0\\
P(0|01)\cdot P(01) + P(0|11)\cdot P(11) - P(10)&= 0\\
P(00) + P(01) + P(10) + P(11) &= 1
\end{align*}
$$

Esto se convierte al sistema matricial:

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

Sustituyendo los valores de las probabilidades condicionales, obtenemos:

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

Resolviendo el sistema de ecuaciones, mediante la inversa de la matriz de coeficientes, obtenemos:

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

Así que podemos rellenar la tabla de probabilidades de estados en régimen estacionario:

| $s_js_ks_i$ | $P(s_i\|s_js_k)$ | $P(s_js_k)$ |
|:-----------:|:---------------:|:-----------:|
| 000         | 0.8             | 5/14        |
| 001         | 0.2             | 5/14        |
| 010         | 0.5             | 2/14        |
| 011         | 0.5             | 2/14        |
| 100         | 0.5             | 2/14        |
| 101         | 0.5             | 2/14        |
| 110         | 0.2             | 5/14        |
| 111         | 0.8             | 5/14        |

El siguiente paso es calcular la probabilidad conjunta de cada estado, es decir $P(s_i,s_j,s_k)$, sabiendo que $P(s_i,s_j,s_k) = P(s_i|s_j,s_k)\cdot P(s_j,s_k)$:

| $s_js_ks_i$ | $P(s_i\|s_j,s_k)$ | $P(s_j,s_k)$ | $P(s_i,s_j,s_k)$ |
|:-----------:|:---------------:|:-----------:|:---------------:|
| 000         | 0.8             | 5/14        | 4/14            |
| 001         | 0.2             | 5/14        | 1/14            |
| 010         | 0.5             | 2/14        | 1/14            |
| 011         | 0.5             | 2/14        | 1/14            |
| 100         | 0.5             | 2/14        | 1/14            |
| 101         | 0.5             | 2/14        | 1/14            |
| 110         | 0.2             | 5/14        | 1/14            |
| 111         | 0.8             | 5/14        | 4/14            |

Finalmente, podemos calcular la entropía de la fuente de Markov de orden 2:

$$
\begin{align*}
H(\mathcal{S}) &= -\sum_{\mathcal{S}^3}P(s_i,s_j,s_k)\log\left(P(s_i|s_j,s_k)\right)\\
&= -\left(2\cdot\frac{4}{14}\log\left(0.8\right)+2\cdot\frac{1}{14}\log\left(0.2\right)+4\cdot\frac{1}{14}\log\left(0.5\right)\right)\\
&\approx 0.8
\end{align*}
$$

### Fuentes de Bernoulli y Binomiales

Sea la fuente $\left(\mathcal{S},P\right)$ donde $\mathcal{S}=\left\\{x_1,x_2,\dots,x_n\right\\}$ y $p(x_i)=p_i$ y supongamos que tomamos una secuencia $X_1,X_2,\dots,X_n$ de valores independientes.

_¿Qué frecuencia de aparición del elemento_ $x_i$ _esperamos en la secuencia?_

- Cada valor de la secuencia es una prueba de Bernoulli, donde si $X_q = x_i$ tenemos un éxito y si $X_q\neq x_i$ tenemos un fracaso (la probabilidad de éxito es $p_i$).
- El número de éxitos en la secuencia es una variable aleatoria $\mathcal{S}_i$ que sigue una distribución binomial con

$$
P(\mathcal{S}_i=k) = \binom{n}{k}p_i^k(1-p_i)^{n-k}
$$

con una media $\mu_i = np_i$ y una varianza $\sigma_i^2 = np_i(1-p_i)$.

Podemos usar la desigualdad de Chebyshev para acotar la probabilidad de que la variable aleatoria se aleje de su media:

$$
P\left(\left|\frac{\mathcal{S}_i-\mu_i}{\sigma_i}\right|\geq k\right)\leq\frac{1}{k^2}
$$

Sea la fuente de información $\left(\mathcal{S},P\right)$ con $\mathcal{S}=\left\\{x_1,x_2,\dots,x_n\right\\}$ y $p(x_i)=p_i$, y supongamos que tomamos una secuencia $\alpha = \left\langle\alpha_1,\alpha_2,\dots,\alpha_n\right\rangle$ de valores independientes. Diremos que $\alpha$ es una secuencia $k$-típica si se cumple que´

$$
\forall i: 1\leq i\leq n, \left|\frac{\mathcal{S}_i-\mu_i}{\sigma_i}\right|\leq k
$$

que en el caso de la distribución binomial se traduce en

$$
\forall i: 1\leq i\leq n, \left|\frac{\mathcal{S}_i-np_i}{\sqrt{np_i(1-p_i)}}\right|\leq k
$$

lo cual significa que en la secuencia $\alpha$ la frecuencia de aparición de cada símbolo $x_i$ está dentro de un rango de $k$ desviaciones estándar de la media.

Hay una relación entre las secuencias $k$-típicas y la entropía de la fuente de información. Si $n$ es suficientemente grande, entonces la probabilidad de que una secuencia aleatoria de longitud $n$ sea $k$-típica es muy cercana a 1. Por lo tanto, la entropía de la fuente de información se puede aproximar mediante la entropía de las secuencias $k$-típicas.

El número de secuencias $k$-típicas de longitud $n$ es igual a $m^{nH_m(X)}$.

# [Códigos (click para acceder al contenido)](../5-codigos/README.md)
