## Códigos

### Introducción

Como hemos visto al principio del temario, existe un componente en el esquema de transmisión de información llamado **codificador**, el cual se encarga de transformar los mensajes de la fuente (`MF`) en una forma adecuada para su transmisión a través del canal de comunicación y recepción (mensajes codificados, `MC`), donde se lleva a cabo el proceso correspondiente de decodificación para la recuperación del mensaje fuente original `MF`.

En una primera aproximación simplificada a este escenario, definimos el proceso de codificación mediante una función $f$ tal que

$$
f:\text{\texttt{MF}}\rightarrow\mathcal{P}(\text{\texttt{MC}})
$$

donde $\forall m\in\text{\texttt{MC}}: \left|f(m)\right|<\infty$ (es decir que los resultados de la codificación del mensaje tienen una longitud finita). Nótese que $\mathcal{P}(C)$ significa el conjunto potencia de $C$.

Por lo tanto, en este contexto de transmisión de información, cuando se emite un mensaje aletorio $m$, el receptor recibe un mensaje codificado $m'\in\mathcal{P}(C)$. Entonces, existe en el receptor una función $f^\star$ de decodificación:

$$
f^\star:\text{\texttt{MC}}\rightarrow\text{\texttt{MF}}
$$

tal que

$$
\forall m\in \text{\texttt{MF}}, \quad\exists m': f^\star\left(m'\right) = m
$$

Por ahora asumiremos que $\forall m\in \text{\texttt{MF}}, \left|f(m)\right| = 1$ (pero veremos que nos podremos extender a más casos).

### Codificaciones y códigos

Llevando la introducción anterior a un caso más particular (y familiar); sea $\mathcal{A}$ un alfabeto (correspondiente a la fuente de información de memoria nula $(\mathcal{A},P)$, de la que se originan los mensajes fuente $\mathcal{A^+}$) y sea $\mathcal{C}$ el conjunto de los mensajes codificados `MC` (también conocido como el conjunto de códigos), entonces una codificación $f$ es una aplicación **biyectiva**:

$$
f:\mathcal{A}^+\rightarrow\mathcal{C}
$$

Para que esta codificación sea admisible para un proceso eficiente de codificación-decodificación, deberá tener unas características determinadas que se irán exponiendo más adelante.

Sea $\mathcal{B}$ un alfabeto (código), entonces $\mathcal{C}\subseteq\mathcal{B}$. Entonces una codificación admisible es una aplicación inyectiva

$$
f:\mathcal{A}^+\rightarrow\mathcal{B}^+
$$

en la que tenemos que $f\left(\mathcal{A}^+\right) = \mathcal{C}$. Equivalentemente, si tomamos $f(\lambda) = \lambda$ (y también $f^-1(\lambda) = \left\{\lambda\right\}$), entonces podemos extender esta aplicación inyectiva a

$$
f:\mathcal{A}^*\rightarrow\mathcal{B}^*
$$

En este escenario $\mathcal{A}$ recibe el nombre de "_alfabeto fuente_" y $\mathcal{B}$ "_alfabeto código_".

### Codificación Bloque

Una codificación bloque $f$ es una aplicación que le asigna a cada uno de los símbolos $a\in\mathcal{A}$ una palabra de $\mathcal{B}^+$, y se comporta como un homomorfismo, lo cual quiere decir que

$$
\forall x\in\mathcal{A}^+,\forall a\in\mathcal{A}: f(ax) = f(a)f(x)
$$

y de forma equivalente

$$
\forall x\in\mathcal{A}^+,\forall a\in\mathcal{A}: f(xa) = f(x)f(a)
$$

y de forma general

$$
\forall x,y\in\mathcal{A}^+: f(xy) = f(x)f(y)
$$

Por tanto

$$
\forall x\in\mathcal{A}^+: f(x) = f(x[1])\dots f(x[|x|])
$$

_(todo esto es equivalente, y lo hemos visto anteriormente en la definición de homomorfismo en el apartado de estructura del lenguage)_

El conjunto $f(\mathcal{A})=\left\{f(a),\quad\forall\mathcal{A}\right\}$ recibe el nombre de "_código bloque_" (o simplemente "_código_").

#### Ejemplo 1

Consideremos los siguientes alfabetos fuente ($\mathcal{A}$) y código ($\mathcal{B}$):

$$
\begin{align*}
\mathcal{A} &=\left\{0,1,2,3,4,5,6,7,8,9\right\}\\
\mathcal{B} &=\left\{0,1\right\}
\end{align*}
$$

y además consideremos la codificación de bloque definida por $f$:

$$
f(a) = \left(\left\lfloor\frac{a}{2^3}\right\rfloor\mod 2\right)\left(\left\lfloor\frac{a \mod 2^3}{2^2}\right\rfloor\mod 2\right)\left(\left\lfloor\frac{a \mod 2^2}{2^1}\right\rfloor\mod 2\right)\left(\left\lfloor\frac{a \mod 2}{2^0}\right\rfloor\mod 2\right)
$$

claramente tenemos que 

$$
f(\mathcal{A}) = \left\{0000, 0001, 0010, 0011, 0100, 0101, 0110, 0111, 1000, 1001\right\}
$$

Se puede ver que $f(\mathcal{A})\subset\mathcal{B}^4$ (porque hay palabras en $\mathcal{B}^4$ que no aparecen en $f(\mathcal{A})$, como por ejemplo $1111$). $f$ es una codificación de bloque ya que le asigna a cada caracter del alfabeto fuente, una palabra formada por el alfabeto código.

#### Ejemplo 2: Morse

En el morse, el alfabeto código consta de los elementos $\left\{\cdot,-,\text{\texttt{pausa}}\right\}$:

| Alfabeto fuente | Código |
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

Al codificar un mensaje en morse, después del código asociado a cada simbolo ha de introducirse una pausa de separación.

#### Ejemplo 3: ASCII

El ASCII (_American Standard Code for Information Interchange_) es una codificación bloque de logitud constante (no como el morse, que era de longitud variable) con alfabeto código $\mathcal{B}=\left\{0,1\right\}$ y $f(\mathcal{A})=\left\{0,1\right\}^7$.

#### Ejemplo 4: ASCII Extendido

El ASCII extendido es diferencia del ASCII por $f(\mathcal{A})=\left\{0,1\right\}^8$ (la longitud de las palabras es mayor).

#### Unicode

Unicode es un alfabeto universal junto con la codificación de sus símbolos
(más de un millón) mediante un código bloque de longitud fija e incorpora todos los símbolos del ASCII extendido. A partir de Unicode se encuentran, entre otras, las codificaciones bloques de longitud variable UTF (Unicode
Transformation Format): UTF-8 (la más común), UTF-16 y UTF-32.

### Codificación Bloque Unívocamente Decodificable

Una codificación de bloque $f$ se llama **no singular** siempre que

$$
\forall a,b\in\mathcal{A}: a\neq b\Rightarrow f(a)\neq f(b)
$$

#### Ejemplo 1

Sea $\mathcal{A} = \left\{a_1,a_2,a_3,a_4\right\}, $\mathcal{B} = \left\{0,1\right\} y $f$ definida por:

$$
f = \begin{cases}
f(a_1) &= 0\\
f(a_2) &= 11\\
f(a_3) &= 00\\
f(a_4) &= 01\\
\end{cases}
$$

Es sencilo ver que $f$ es no singular. Sin embargo, si nos extendemos a palabras, esto ya no se cumple ya que ciertas palabras de $\mathcal{A}^+$ no son unívocamente decodificables. Por ejemplo:

- $a_1a_1a_1\neq a_1a_3\neq a_3a_1$ pero $000 = f(a_1a_1a_1
) = f(a_1a_3) = f(a_3a_1)$
- $a_1a_1a_2\neq a_3a_2$ pero $0011 = f(a_1a_1a_2) = f(a_3a_2)$

---

La extensión de orden $n\geq 1$de una codificación bloque

$$
f:\mathcal{A}^+\rightarrow\mathcal{B}^+
$$

se define como

$$
f^{(n)}:\left(\mathcal{A}^n\right)^+\rightarrow\mathcal{B}^+
$$

tomando como símbolos las palabras de $\mathcal{A}^n$ de forma que

$$
\forall x\in\mathcal{A}^n: f^{(n)}(x)=f(x)
$$

La extensión de orden $n$ de una codificación bloque también lo es tomando, para cada caso, como alfabeto fuente el correspondiente $\mathcal{A}$.

Una codificación bloque $f$ se dice unívocamente decodificable sí y sólo si su extensión de orden $n$ es **no singular** para cada $n\geq 1$.

Surge una propiedad importante: una codificación bloque es unívocamente decodificable si y sólo si es inyectiva.

Diremos que un código bloque es unívocamente decodificable si proviene de una codificación bloque unívocamente decodificable, lo cual nos permite definir $f^{-1}:\mathcal{B}^+\rightarrow\mathcal{A}^+$.

**Propiedad de factorización única:**

1. Si $f:\mathcal{A}^+\rightarrow\mathcal{B}^+$ es una codificación bloque unívocamente decodificable, entonces se tiene que $\forall x_1,\dots,x_n,y_1,\dots,y_m\in f(\mathcal{A})$:

$$
x_1\dots x_n=y_1\dots y_m \Rightarrow (n = m)\wedge\left(x_i=y_i,\quad i = 1,\dots,n\right)
$$

2. $f:\mathcal{A}^+\rightarrow\mathcal{B}^+$ (que es una codificación bloque) es unívocamente decodificable si y solamente si cumple la propiedad mencionada anteriormente, y además es no singular.

La cuestión de si una codificación bloque $f$ es unívocamente decodificable o no es algorítmicamente decidible (_es decir, que hay un algoritmo para averiguar si es unívocamente decodificable o no_).

El siguiente algoritmo devuelve `true` cuando $f$ es unívocamente decodificable y `false` en caso contrario:

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

Sea $f:\mathcal{A}^+\rightarrow\mathcal{B}^+$ una codificación bloque no singular. Si todas las palabras del código bloque tienen exactamente la misma longitud, entonces el código es unívocamente decodificable.

_Piensa en el Ejemplo 1 de esta sección. ¿De dónde salían los problemas a la hora de decodificar? Surgían del hecho de que no todas lass palabras del código bloque tenían la misma longitud_

### Desigualdad de McMillan

Si $f:\mathcal{A}^+\rightarrow\mathcal{B}^+$ es una codificación bloque unívocamente decodificable y $\left|\mathcal{B}\right|=k$, entonces

$$
\sum_{x\in f(\mathcal{A})} k^{-\left|x\right|}\leq 1
$$

#### Ejemplo 1

Recuperando el ejemplo anterior de los siguientes alfabetos fuente ($\mathcal{A}$) y código ($\mathcal{B}$):

$$
\begin{align*}
\mathcal{A} &=\left\{0,1,2,3,4,5,6,7,8,9\right\}\\
\mathcal{B} &=\left\{0,1\right\}
\end{align*}
$$

con 

$$
f(\mathcal{A}) = \left\{0000, 0001, 0010, 0011, 0100, 0101, 0110, 0111, 1000, 1001\right\}
$$

La desigualdad de McMillan debería de cumplirse ya que es una codificación bloque unívocamente decodificable:

$$
\sum_{x\in f(\mathcal{A})} k^{-\left|x\right|} = \sum_{x\in f(\mathcal{A})} 2^{-4} = \frac{10}{16} < 1
$$

Vemos rápidamente que se cumple.

_¿Qué condición debería cumplirse para tener la igualdad estricta?_

Imaginémonos ahora que tenemos

$$
\begin{align*}
\mathcal{A} &=\left\{0,1,2,3,4,5,6,7,8,9,a,b,c,d,e,f\right\}\\
\mathcal{B} &=\left\{0,1\right\}
\end{align*}
$$

con 

$$
f(\mathcal{A}) = \left\{0000, 0001, 0010, 0011, 0100, 0101, 0110, 0111, 1000, 1001,1010,1011,1100,1101, 1110,1111\right\}
$$

_(¿no resulta esto familiar? Es la representación en binario del hexadecimal)_

Para este caso:

$$
\sum_{x\in f(\mathcal{A})} k^{-\left|x\right|} = \sum_{x\in f(\mathcal{A})} 2^{-4} = \frac{16}{16} = 1
$$

Claramente cuando $f(\mathcal{A})\subset\mathcal{B}^+$, entonces la desigualdad es estricta. Pero cuando $f(\mathcal{A})=\mathcal{B}^+$, entonces tenemos la igualdad.

### Códigos instantáneos

Empecemos observando un ejemplo. Consideremos la codificación unívocamente decodificable $f(a)=0$ y $f(b)=01$. Para decodificar $x=01$, tendríamos que conocer de la existencia del $1$, ya que únicamente con el $0$ tenemos una ambigüedad y no sabemos si se trata de $a$ o de $b$. Al leer el $1$, resolvemos esto y podemos decodificar $x$ como $b$. Es decir, hasta no leer la palabra entera, no hemos podido saber cómo decodificarla.

Esta situación empeora cuanto más larga es la palabra, y puede llevar a que la decodificación sea impracticable.

Consideremos ahora la codificación unívocamente decodificable $f(a)=0$, $f(b)=01$ y $f(c)=11$. Sea $x=01^n$ con $n\geq 1$. Tenemos que

$$
f^-1(x) = \begin{cases}
ac^m&\quad\text{si }n\text{ es par, con }m=\frac{n}{2}\\
bc^m&\quad\text{si }n\text{ es impar, con }m=\frac{n-1}{2}
\end{cases}
$$

Veamos una serie de ejemplos:

- $f^-1(x)=f^-1(01^6)=f^-1(0111111)=accc$
- $f^-1(x)=f^-1(01^{11})=f^-1(011111111111)=bccccc$

Para decodificar, es esencial conocer cuantos $1$ tenemos en la palabra $x$. Esto no lo podemos averiguar si no leemos toda la palabra primero (independientemente de lo larga que sea esta), antes de decodificar.

Se dice que un código unívocamente decodificable es **instantáneo** cuando es posible decodificar cada símbolo de $\mathcal{A}$ de cada mensaje sin necesitar más símbolos de $\mathcal{B}$ de los estricamente necesarios. Es decir, si

$$
h:\mathcal{A}^*\rightarrow\mathcal{B}^*
$$

es una codificación bloque unívocamente decodificable, entonces es instantánea siempre que

$$
\forall x\in\mathcal{A}^*, \exists u,v\in\mathcal{A}^*,\exists a\in\mathcal{A}: x=uav
$$

tal que

$$
y=h(x)=h(u)h(a)h(v)
$$

Entonces para decodificar $y$ a $x$, para decodificar el segmento $h(a)$ a $a$ de forma inmediata, independientemente del sufijo $h(v)$, solamente hay que procesar el segmento de $y$ asociado a $h(a)$.

Entonces para descodificar el segmento $y\left[\left|h(u)\right|+1:\left|h(u)\right|+n\right]$ con, en este caso, $n = \left|h(a)\right|$:

$$
\begin{align*}
y\left[\left|h(u)\right|+1:\left|h(u)\right|+n\right] &= y\left[\left|h(u)\right|+1:\left|h(u)\right|+\left|h(a)\right|\right]\\
&= y\left[\left|h(u)\right|+1:\left|h(ua)\right|\right]
\end{align*}
$$

es suficiente, en cualquier caso, para la correcta decodificación. Eso quiere decir que

$$
\forall a,b\in\mathcal{A}:h(a)\text{ es prefijo de }h(b)\Rightarrow a = b
$$

Una vez más, diremos que un código bloque es instantáneo cuando proviene de una codificación bloque instantánea. También podemos llamarlo código bloque prefijo o simplemente código prefijo.

---

Sea $f:\mathcal{A}^*\rightarrow\mathcal{B}^*$ una codificación de bloque. Diremos que $f$ es **estable** siempre que:

1. Sea unívocamente decodificable.
2. $\forall x\in\mathcal{A}^*,f(x)=u$ se cumple que $\forall v\in\mathcal{B}^*$, si $\exists y\in\mathcal{A}^*,f(y)=uv\Rightarrow y=xz$ para algún $z\in\mathcal{A}^*$

Tenemos entonces la siguiente propiedad: sea $f:\mathcal{A}^*\rightarrow\mathcal{B}^*$ una codificación bloque. Entonces, **$f$ es estable si y sólo si es instantánea.

---

### Desigualdad de Kraft

Veamos cómo estad características cualitativas se traducen cuantitativamente. Sea la codificación bloque:

$$
f:\mathcal{A}^*\rightarrow\mathcal{B}^*
$$

con $\mathcal{A}=\left\{a_1,\dots,a_n\right\}$, $\mathcal{B}=\left\{b_1,\dots,b_k\right\}$ y $f\left(\mathcal{A}\right)=\left\{x_1,\dots,x_n\right\}$, con $l_i = \left|x_i\right|$. La desigualdad de Kraft nos da la condición **necesaria** y **suficiente** para que exista un código bloque instantáneo con palabras de su código bloque de longitud $l_1,\dots,l_n$ sobre un alfabeto con $k$ símbolos:

$$
\sum_{1\leq i\leq n}k^{-l_i}\leq 1
$$

Cuando esto es una igualdad estricta, se conoce como la igualdad de Kraft.

Como consecuencia inmediata, a partir de la desigualdad de McMillan, se tiene que para cada código unívocamente decodificable se tiene un código instantáneo con las mismas longitudes de las palabras de su código bloque.

### Códigos Completos

Sea la codificación de bloque:

$$
f:\mathcal{A}^*\rightarrow\mathcal{B}^*
$$

diremos que es completa si:ç

1. Es instantánea.
2. Cumple que $\forall x\in\mathcal{B}^*,\exists a\in\mathcal{A}^*\Rightarrow\left(\left(h(a)\text{ es prefijo de }x\right)\vee\left(x\text{ es prefijo de }h(a)\right)\right)$.

Tenemos entonces la siguiente propiedad: si $\left|\mathcal{A}\right|\geq 2$ y $\left|\mathcal{B}\right|=2$, entonces sólo existe una codificación de bloque completa

$$
f':\mathcal{A}^*\rightarrow\mathcal{B}^*
$$

tal que $\forall a\in\mathcal{A}:\left|f'(a)\right|\leq\left|f(a)\right|$.

Nuevamente, un código bloque es completo si proviene de una codificación de bloque completa.

## Codificaciones de Fuentes de Información

### Longitud media de un código

Para un $\mathcal{A}^*$ y $\mathcal{B}^*$, es posible definir más de una codificación instantánea o unívocamente decodificable. Esto requiere entonces que intentemos elegir las más eficientes con el objetivo de tener una transmisión de información óptima.

Un criterio natural de selección (aún cuando no es el único posible) es el de la mínima longitud media.

Sea un código bloque que asocia los símbolos de una **fuente de información de memoria nula** $FI = \left(\mathcal{A},P\right)$ donde $\mathcal{A}=\left\{a_1,\dots,a_n\right\}$ y $\left|\mathcal{B}\right|=k$ mediante la codificación $f:\mathcal{A}^*\rightarrow\mathcal{B}^*$ con las palabras $f\left(a_i\right)=x_i$, con $l_i=\left|x_i\right|,i=1,\dots,n$. Definimos la lonfitud media como la **esperanza matemática de la longitud de los códigos bloque**:

$$
\mathcal{L}_f=\mathbb{E}\left[l\right]=\mathbb{E}\left[\left|x\right|\right]=\mathbb{E}\left[\left|f(a)\right|\right]=\sum_{i=1}^n \left|f(a_i)\right|p(a_i)
$$

### Códigos óptimos

Sea un código bloque unívocamente decodificable que asocia los símbolos de la fuente de memoria nula $FI = \left(\mathcal{A},P\right)$ con palabras formadas por un alfabeto $\left|\mathcal{B}\right|=k$. Diremos que es **compacto** u **óptimo** con respecto a la fuente de información si su longitud media es menor o igual que la longitud media de cada uno de los códigos bloque unívocamente decodificables que pueden definirse entre la fuente y alfabetos códigos con $k$ símbolos.

Surge de aquí la observación de que, puesto que esto incide únicamente sobre las logitudes, la búsqueda puede reducirse por la desigualdad de McMillan a códigos instantáneos.

Además, si se tiene que $\left|\mathcal{A}\right|\geq 2$ y $\left|\mathcal{B}\right| = 2$, si un código bloque es óptimo, entonces es completo.

También se tiene la propiedad de si $f$ es un código óptimo, entonces

$$
\forall a,b\in\mathcal{A}:p(a)<p(b)\Rightarrow \left|f(a)\right|\geq\left|f(b)\right|
$$

### Primer Teorema de Shannon _(teorema de la codificación sin ruido)_

Consideremos una fuente de memoria nula $FI$ cuyos símbolos $a_1,\dots,a_n$ con probabilidades $p_1,\dots,p_n$ se codifican cada uno en una palabra de longitud $l_i$ en un alfabeto con $k$ símbolos mediante la codificación $f$. Entonces se tiene que $H_k\left(FI\right)\leq\mathcal{L}_f$.

Si suponemos que nos encontramos en el caso de la igualdad, es decir, $H_k\left(FI\right)=\mathcal{L}_f$:

$$
\begin{align*}
H_k\left(FI\right)&=\mathcal{L}_f\\
\sum_{i=1}^np_i\log_k\left(\frac{1}{p_i}\right)&=\sum_{i=1}^np_il_i
\end{align*}
$$

inferimos que si tomamos longitudes de código $l_i=\left|x_i\right|=\left|f(a_i)\right|$, tendremos que los códigos obtenidos para cada $a_i$ serán instantáneos, completos y óptimos con una longitud media que coincide con la entropía en base $k$ de la fuente de información (asumiendo claramente que $\log_k\left(\frac{1}{p_i}\right)$ es un número entero $\forall 1\leq i\leq n$).

Veamos un ejemplo: supón que tenemos $FI=\left(\left\{a_1,a_2,a_3\right\},\left\{\frac{1}{2},\frac{1}{4},\frac{1}{4}\right\}\right)$, entonces la codificación de bloque:

$$
h:\left\{a_1,a_2,a_3\right\}^*\rightarrow\left\{0,1\right\}^*
$$

definida tomando las longitudes de los códigos como $\log\left(\frac{1}{p_i}\right)$:

$$
h=\begin{cases}
h\left(a_1\right) &= 1\\
h\left(a_2\right) &= 00\\
h\left(a_3\right) &= 01
\end{cases}
$$

es instantánea, completa y óptima con $\mathcal{L}_h=H\left(FI\right)$.

Pero, ¿qué sucede si resulta que $\log_k\left(\frac{1}{p_i}\right)$ no resultan ser números enteros? Parece intuitivo y apropiado en este contexto redondear el valor obtenido hacia arriba, para elegir $l_i$ (aunque claramente en este caso, el código obtenido no tiene por qué ser 
optimo). Entonces si $l_i=\left\lceil\log_k\left(\frac{1}{p_i}\right)\right\rceil$, por definición se tiene que

$$
\log_k\left(\frac{1}{p_i}\right)\leq l_i\leq\log_k\left(\frac{1}{p_i}\right) + 1
$$

Se puede demostrar que se cumple la desigualdad de Kraft. Tomemos $\log_k\left(\frac{1}{p_i}\right)\leq l_i$:

$$
\begin{align*}
\log_k\left(\frac{1}{p_i}\right)&\leq l_i\\
k^{\log_k\left(\frac{1}{p_i}\right)}&\leq k^{l_i}\\
\frac{1}{p_i}&\leq k^{l_i}\\
\frac{1}{k^{l_i}}&\leq p_i\\
k^{-l_i}&\leq p_i,\quad\forall 1\leq i\leq n\\
\sum_{i=1}^nk^{-l_i}&\leq\sum_{i=1}^n p_i\\
\sum_{i=1}^nk^{-l_i}&\leq 1
\end{align*}
$$

En consecuencia, pueden asociárseles códigos bloque instantáneos.

Volviendo a la siguiente desigualdad:

$$
\log_k\left(\frac{1}{p_i}\right)\leq l_i\leq\log_k\left(\frac{1}{p_i}\right) + 1
$$

Multiplicando todos los términos por $p_i$:

$$
p_i\log_k\left(\frac{1}{p_i}\right)\leq p_il_i\leq p_i\log_k\left(\frac{1}{p_i}\right) + p_i
$$

y sumando ya que la desigualdad se cumple $\forall 1\leq i\leq n$:

$$
\begin{align*}
\sum_{i=1}^np_i\log_k\left(\frac{1}{p_i}\right)&\leq\sum_{i=1}^np_il_i\leq \sum_{i=1}^np_i\log_k\left(\frac{1}{p_i}\right) + \sum_{i=1}^np_i\\
H_k\left(FI\right)&\leq\mathcal{L}_f\leq H_k\left(FI\right) + \sum_{i=1}^np_i\\
H_k\left(FI\right)&\leq\mathcal{L}_f\leq H_k\left(FI\right) + 1\\
\end{align*}
$$

Cumpliéndose esto también para cualquier código óptimo, lo que constituye la formulación inicial del primer teorema de Shannon.

Puesto que esto puede aplicarse además a cualquier extensión de grado $m$ de una fuente de memoria nula...

$$
\begin{align*}
H_k\left(FI^{(m)}\right)&\leq\mathcal{L}_f^m\leq H_k\left(FI^{(m)}\right) + 1\\
mH_k\left(FI\right)&\leq\mathcal{L}_f^m\leq mH_k\left(FI\right) + 1\\
H_k\left(FI\right)&\leq\frac{\mathcal{L}_f^m}{m}\leq H_k\left(FI\right) + \frac{1}{m}\\
\end{align*}
$$

Obteniendo así **el primer teorema de Shannon**, que es uno de los teoremas fundamentales de la teoría de la información.

Una propiedad interesante surge cuando intentamos ver qué pasa cuando la extensión de grado $m$ de nuestra fuente de información de memoria nula emite palabras largas. Para ello tenemos que ver qué sucede cuando $m\to\infty$:

$$
\begin{align*}
\lim_{m\to\infty}H_k\left(FI\right)&\leq\lim_{m\to\infty}\frac{\mathcal{L}_f^m}{m}\leq \lim_{m\to\infty}H_k\left(FI\right) + \lim_{m\to\infty}\frac{1}{m}\\
H_k\left(FI\right)&\leq\lim_{m\to\infty}\frac{\mathcal{L}_f^m}{m}\leq H_k\left(FI\right) + 0\\
\end{align*}
$$

Como $\lim_{m\to\infty}\frac{\mathcal{L}_f^m}{m}$ queda acotado por arriba y por abajo por $H_k\left(FI\right)$, hemos demostrado mediante "_el teorema del sándwich_" que

$$
\lim_{m\to\infty}\frac{\mathcal{L}_f^m}{m} = H_k\left(FI\right)
$$

Nótese que $\frac{\mathcal{L}_f^m}{m}$ es el **número medio de símbolos del alfabeto código ($\mathcal{B}$) empleados en la codificación de un símbolo del alfabeto fuente ($\mathcal{A}$) cuando se emiten secuencias de longitud $m$, es decir, como símbolos del alfabeto $\mathcal{A}^{(m)}$.

---

#### Ejemplo Aplicado

Sea una fuente de $FI$ de memoria nula definida por $\mathcal{A}=\left\{a_1,a_2,a_3\right\}$ con $P=\left\{\frac{3}{4},\frac{1}{12},\frac{2}{12}\right\}$, y además $\mathcal{B}=\left\{0,1\right\}$. Construyámonos una tabla con `python`, `pandas` y `numpy`:

```python
import pandas as pd
import numpy as np
df = pd.DataFrame(
    np.array([[3/4, 1/12, 2/12]]).T,
    columns=["p"],
    index=["a_1","a_2","a_3"]
)
```

obteniéndose la tabla:

|    |         p |
|:---|----------:|
| a1 | 0.75      |
| a2 | 0.0833333 |
| a3 | 0.166667  |

_(si queréis generar tablas para markdown o latex a partir de un `DataFrame` de `pandas`, podéis emplear los métodos `DataFrame.to_markdown()` y `DataFrame.to_latex()`)_

Nuestro siguiente paso es calcular la información $I(a_i) = \log\left(\frac{1}{p_i}\right)$ para cada símbolo:

```python
df["log2(1/p)"] = np.log2(1/df["p"])
```

obteniéndose la tabla

|    |         p |   log2(1/p) |
|:---|----------:|------------:|
| a1 | 0.75      |    0.415037 |
| a2 | 0.0833333 |    3.58496  |
| a3 | 0.166667  |    2.58496  |

y a continuación calculamos las longitudes $l_i = \left\lceil\log\left(\frac{1}{p_i}\right)\right\rceil$:

```python
df["l"] = np.ceil(df["log2(1/p)"])
```

obteniéndose la tabla

|    |         p |   log2(1/p) |   l |
|:---|----------:|------------:|----:|
| a1 | 0.75      |    0.415037 |   1 |
| a2 | 0.0833333 |    3.58496  |   4 |
| a3 | 0.166667  |    2.58496  |   3 |

Por lo tanto podemos proponer un código instantáneo dado por estas longitudes y empleando el alfabeto código mencionado anteriormente. Por ejemplo:

|    |         p |   log2(1/p) |   l |   codigo |
|:---|----------:|------------:|----:|---------:|
| a1 | 0.75      |    0.415037 |   1 |        1 |
| a2 | 0.0833333 |    3.58496  |   4 |     0001 |
| a3 | 0.166667  |    2.58496  |   3 |      001 |

Si quisiéramos calcular la longitud media

```python
(df["p"]*df["l"]).sum()
```

obteniéndose $L_f\approx 1.58$. Si quisiéramos calcular la entropía

```python
(df["p"]*df["log2(1/p)"]).sum()
```

obteniéndose $H(FI)\approx 1.04$.

### Rendimiento y redundancia de un código unívocamente decodificable

Se define en el contexto en el que hablábamos, el rendimiento $\eta$ de un código como

$$
\eta = \frac{H_k(FI)}{L_f}
$$

y la redundancia como

$$
1 - \eta = 1 - \frac{H_k(FI)}{L_f} = \frac{L_f - H_k(FI)}{L_f}
$$

Un código óptimo tiene máximo rendimiento y mínima redundancia.