# Variables Aleatorias Discretas

## Motivación — Del experimento a la variable

Para introducir la idea de variable aleatoria partimos de un experimento sencillo. Una urna tiene **6 bolitas verdes y 4 bolitas azules**, y realizamos **4 extracciones con reposición**: antes de cada extracción la urna vuelve a su configuración inicial.

Consideramos los eventos $V_i = $ "la $i$-ésima extracción es una bolita verde" (con $1 \leq i \leq 4$). Como hay reposición, estos eventos son **independientes**: el resultado de una extracción no afecta las probabilidades de otra. Por la regla de Laplace:

$$P(V_i) = \frac{6}{4+6} = \frac{3}{5} \implies P(\overline{V_i}) = 1 - \frac{3}{5} = \frac{2}{5}$$

A partir de ahí definimos una serie de eventos referidos a la totalidad de las extracciones:

$$D_k = \text{"Entre las 4 extracciones hay exactamente } k \text{ bolitas verdes"}$$

Como se realizan 4 extracciones con reposición, los valores de $k$ que cumplen $P(D_k) > 0$ son $k \in \{0, 1, 2, 3, 4\}$: puede no salir ninguna verde ($k=0$), pueden salir las 4 ($k=4$), y todos los valores intermedios también tienen probabilidad positiva.

---

## Cálculo de las probabilidades de cada evento

Calculamos $P(D_k)$ aprovechando la independencia. Por ejemplo, para $k=0$ (ninguna verde, es decir las 4 azules):

$$P(D_0) = P(\overline{V_1} \cap \overline{V_2} \cap \overline{V_3} \cap \overline{V_4}) \overset{\text{IND}}{=} \left(\frac{2}{5}\right)^4 = \frac{16}{625}$$

Para $k=1$ hay que contabilizar las **4 maneras** en que una sola extracción puede ser la verde:

$$P(D_1) = 4 \cdot \frac{3}{5} \cdot \left(\frac{2}{5}\right)^3 = \frac{96}{625}$$

Para $k=2$ hay $\binom{4}{2} = 6$ configuraciones posibles:

$$P(D_2) = 6 \cdot \left(\frac{3}{5}\right)^2 \cdot \left(\frac{2}{5}\right)^2 = \frac{216}{625}$$

Análogamente $P(D_3) = 4 \cdot \left(\frac{3}{5}\right)^3 \cdot \frac{2}{5} = \frac{216}{625}$ y $P(D_4) = \left(\frac{3}{5}\right)^4 = \frac{81}{625}$.

En general, todas estas probabilidades se resumen en una única fórmula:

$$\boxed{P(D_k) = \binom{4}{k} \cdot \left(\frac{3}{5}\right)^k \cdot \left(\frac{2}{5}\right)^{4-k}, \qquad 0 \leq k \leq 4}$$

La interpretación es directa: hay $\binom{4}{k}$ formas de elegir cuáles extracciones son verdes, y cada una de esas configuraciones tiene probabilidad $\left(\frac{3}{5}\right)^k \left(\frac{2}{5}\right)^{4-k}$ ($k$ verdes y $4-k$ azules).

Los eventos $D_k$ son **mutuamente excluyentes** (no pueden salir distintas cantidades de bolitas verdes en las mismas extracciones) y sus probabilidades suman 1:

$$\frac{16}{625} + \frac{96}{625} + \frac{216}{625} + \frac{216}{625} + \frac{81}{625} = 1$$

Por lo tanto, los conjuntos $D_k$ forman una **partición** del espacio muestral $S$: todo resultado posible se identifica con un único evento $D_k$.

---

## Definición de variable aleatoria

Toda esa información se puede resumir definiendo:

$$D = \text{Cantidad de bolitas verdes entre las 4 extracciones}$$

donde cada evento $D_k$ se reescribe como $D = k$. Una variable construida de esta manera se denomina **variable aleatoria**:

- **Variable:** una magnitud que puede tomar varios valores.
- **Aleatoria:** un resultado que no se puede predecir.

Las variables aleatorias se notan generalmente con la letra $X$ y son **funciones que transforman el espacio muestral $S$ en valores reales**, es decir $X : S \mapsto \mathbb{R}$. La probabilidad de cada valor de $X$ está asociada a la probabilidad del evento correspondiente en $S$.

> **Nota:** Definir una variable aleatoria resume mucha información sobre los eventos. Además, los valores son números, y los números permiten operar (sumar, restar, multiplicar), cosa que no tiene sentido con los resultados crudos del experimento (no se puede sumar "verde" + "azul").

### Recorrido

Para cada variable aleatoria $X$, el conjunto de valores con probabilidad positiva se denomina **recorrido** y se nota $R_X$. En el ejemplo, $R_D = \{0, 1, 2, 3, 4\}$.

Cuando $R_X$ es **discreto** (se puede construir un entorno alrededor de cada elemento sin intersección con otro), se dice que $X$ es una **Variable Aleatoria Discreta (V.A.D.)**. En el caso de $D$, tomando entornos de longitud $0.5$ no hay solapamiento entre valores, por lo que el recorrido es discreto.

---

## Función de probabilidad puntual

Dada una V.A.D. $X$, se denomina **función de probabilidad puntual** $p_X$ a la función que asigna a cada valor real su probabilidad:

$$p_X : \mathbb{R} \mapsto [0,1] \;/\; p_X(k) = P(X = k)$$

Esta función toma valores en todo $\mathbb{R}$, pero a los que no pertenecen al recorrido se les asigna probabilidad nula. Para la variable $D$:

| $k$ | $p_D(k)$ |
|:-:|:-:|
| 0 | $16/625$ |
| 1 | $96/625$ |
| 2 | $216/625$ |
| 3 | $216/625$ |
| 4 | $81/625$ |
| otro | 0 |

Dos propiedades fundamentales se deducen de la partición:

- Los eventos asociados a valores diferentes de $X$ son **mutuamente excluyentes** ($X$ no puede valer dos cosas a la vez).
- Las probabilidades de todos los valores del recorrido suman 1:

$$\sum_{k \in R_X} p_X(k) = 1$$

Como esos eventos forman una partición, pueden usarse tanto para el **Teorema de la Probabilidad Total** como para el **Teorema de Bayes**.

---

## Frecuencias relativas y probabilidades

Si corremos el experimento **1000 veces** y registramos los valores de $D$, obtenemos frecuencias que se parecen a las probabilidades teóricas (interpretación frecuentista de la probabilidad):

| Valor de $D$ | Frecuencia | Frec. Relativa | $P(D=k)$ |
|:-:|:-:|:-:|:-:|
| 0 | 27 | 0.027 | 0.0256 |
| 1 | 132 | 0.132 | 0.1536 |
| 2 | 333 | 0.333 | 0.3456 |
| 3 | 383 | 0.383 | 0.3456 |
| 4 | 125 | 0.125 | 0.1296 |

Gráficamente, un diagrama de barras de las frecuencias relativas se superpone casi exactamente con el de las probabilidades, confirmando que son parecidas.

---

## Función de distribución acumulada

Para cualquier variable aleatoria $X$ se define también la **función de distribución acumulada** $F_X$, que recorre todos los reales:

$$F_X : \mathbb{R} \mapsto [0,1] \;/\; F_X(k) = P(X \leq k)$$

Sus propiedades son:

- **Monótona creciente:** si $k_1 \leq k_2 \implies F_X(k_1) \leq F_X(k_2)$, porque $\{X \leq k_1\} \subseteq \{X \leq k_2\}$.
- $\displaystyle\lim_{k \to -\infty} F_X(k) = 0$, ya que $\{X \leq k\} \to \emptyset$.
- $\displaystyle\lim_{k \to +\infty} F_X(k) = 1$, ya que $\{X \leq k\} \to S$.
- **Continua a derecha:** $\displaystyle\lim_{x \to k^+} F_X(x) = F_X(k)$.

Al haber muchos valores de probabilidad nula, esta función tiene **forma escalonada**, con saltos exactamente en los valores de probabilidad positiva (la altura de cada salto es $p_X(k)$). Por eso puede no ser continua a izquierda, pero sí a derecha.

---

## Parámetros de una variable aleatoria

### Valor esperado (media)

Para buscar un valor central de $D$, los valores de mayor probabilidad deben tener más influencia. Aprovechando que la frecuencia relativa se parece a la probabilidad, definimos el **valor esperado** (notado con la letra $E$ o con $\mu$):

$$\boxed{E(X) = \mu_X = \sum_{k \in R_X} k \cdot p_X(k)}$$

Para la variable $D$:

$$E(D) = 0 \cdot 0.0256 + 1 \cdot 0.1536 + 2 \cdot 0.3456 + 3 \cdot 0.3456 + 4 \cdot 0.1296 = 2.4$$

**Interpretación:** si se repite varias veces el experimento y se promedian los valores de $X$, ese promedio converge a $E(X)$. La simulación de 1000 experimentos arrojó un promedio de $2.447 \approx 2.4$, consistente con el cálculo teórico.

### Propiedades del valor esperado (linealidad)

- Si $c$ es constante, $E(c) = c$.
- Si $a$ es constante, $E(a \cdot X) = a \cdot E(X)$.
- Si $X, Y$ son V.A.D., $E(X + Y) = E(X) + E(Y)$.
- Combinando: $E(a \cdot X + b \cdot Y + c) = a \cdot E(X) + b \cdot E(Y) + c$.

> [!warning] No factorizar productos
> En la mayoría de los casos, $E(X \cdot Y) \neq E(X) \cdot E(Y)$. **No factorizar un valor esperado** cuando hay dos variables multiplicando sin verificar antes que pueda hacerse.

### Funciones de variables aleatorias

Si $X$ es una V.A.D. y $g : \mathbb{R} \mapsto \mathbb{R}$, entonces $Y = g(X)$ también es una V.A.D. Su valor esperado puede calcularse sin recalcular el recorrido de $Y$:

$$\boxed{E(g(X)) = \sum_{k \in R_X} g(k) \cdot p_X(k)}$$

En particular, $\displaystyle E(X^2) = \sum_{k \in R_X} k^2 \cdot p_X(k)$.

### Varianza y desvío

La **varianza** mide cuánto tienden a dispersarse (probabilísticamente) los valores alrededor del valor esperado:

$$\boxed{V(X) = E\big((X - E(X))^2\big) = \sum_{k \in R_X} (k - E(X))^2 \cdot p_X(k)}$$

El **desvío** es $\sigma(X) = \sqrt{V(X)}$, a veces notado $\sigma_X$. Para la variable $D$:

$$V(D) = (0-2.4)^2 \cdot 0.0256 + \dots + (4-2.4)^2 \cdot 0.1296 = 0.96 \implies \sigma(D) = 0.9798$$

Desarrollando el cuadrado y usando linealidad se obtiene la **fórmula práctica**:

$$\boxed{V(X) = E(X^2) - E^2(X)}$$

### Propiedades de la varianza

- Si $c$ es constante, $V(c) = \sigma(c) = 0$.
- $V(a \cdot X) = a^2 \cdot V(X) \implies \sigma(a \cdot X) = |a| \cdot \sigma(X)$.
- $V(X + c) = V(X) \implies \sigma(X + c) = \sigma(X)$.
- $V(a \cdot X + c) = a^2 \cdot V(X) \implies \sigma(a \cdot X + c) = |a| \cdot \sigma(X)$.

> [!warning] No separar la varianza de una suma
> En general $V(X + Y) \neq V(X) + V(Y)$. **No dividir la varianza por suma (o resta)** de dos variables sin verificar que pueda hacerse.

### Otras medidas de resumen

Con la misma lógica del valor esperado se definen la **simetría** y la **kurtosis**:

$$\gamma(X) = \frac{E\big((X - \mu_X)^3\big)}{\sigma_X^3}, \qquad \kappa(X) = \frac{E\big((X - \mu_X)^4\big)}{\sigma_X^4} - 3$$

> **Nota:** Cuando no se sabe mucho sobre una V.A.D., lo importante es identificar su **recorrido** y las **probabilidades** de esos valores. Con esos dos datos, todo lo demás (media, varianza, etc.) se calcula fácilmente.

---

## Estructuras conocidas

Muchas variables que aparecen en la práctica comparten una misma estructura, y reconocerla permite omitir cálculos porque sus resultados se conocen de antemano. Volvemos al ejemplo de la urna con una historia recurrente: **Agustina** va frecuentemente a un casino donde un juego consiste en sacar bolitas al azar de la urna (4 azules, 6 verdes). En cada extracción gana \$1 si sale azul, o pierde su apuesta de \$3 si sale verde.

---

## Distribución Binomial

Agustina juega **5 veces por noche con reposición**. Definimos $A_i = $ "la $i$-ésima extracción es azul" (con $P(A_i) = \tfrac{2}{5}$) y las variables:

- $B = $ cantidad de bolitas azules en las 5 extracciones con reposición.
- $G = $ ganancia del casino, donde $G = 3 \cdot (5 - B) - 4 \cdot B = 15 - 7 \cdot B$, es decir $G = G(B)$.

Como hay una **cantidad fija** de experimentos independientes ($n = 5$), cada uno con dos resultados ("éxito" = azul, "fracaso" = verde) y la **misma** probabilidad de éxito $p = \tfrac{2}{5}$, la variable $B$ que cuenta los éxitos tiene **distribución Binomial** de parámetros $n$ y $p$, notada $X \sim Bi(n, p)$.

Sea $X \sim Bi(n, p)$. Entonces:

| Característica | Fórmula |
|:-:|:-:|
| Recorrido | $R_X = \{0, 1, 2, \dots, n\}$ |
| Probabilidad | $P(X=k) = \binom{n}{k} \cdot p^k \cdot (1-p)^{n-k}$ |
| Valor esperado | $E(X) = n \cdot p$ |
| Varianza | $V(X) = n \cdot p \cdot (1-p)$ |

$$\boxed{X \sim Bi(n,p) \implies E(X) = n \cdot p, \quad V(X) = n \cdot p \cdot (1-p)}$$

La demostración de $E(X) = np$ usa la identidad $k \binom{n}{k} = n \binom{n-1}{k-1}$ y el Binomio de Newton. La de la varianza parte de $E(X^2)$ escribiendo $k^2 = k(k-1) + k$.

**Cálculos para $B \sim Bi(5, \tfrac{2}{5})$:**

$$E(B) = 5 \cdot \frac{2}{5} = 2, \qquad E(B^2) = \frac{26}{5}, \qquad V(B) = E(B^2) - E^2(B) = \frac{26}{5} - 4 = \frac{6}{5}$$

Para la ganancia del casino $G = 15 - 7B$, usando linealidad:

$$E(G) = 15 - 7 \cdot 2 = 1, \qquad V(G) = 7^2 \cdot V(B) = 49 \cdot \frac{6}{5} = \frac{294}{5}$$

El casino gana **\$1 en promedio por noche**. Si Agustina va 1.000.000 de noches, el casino ganará alrededor de \$1.000.000. *El negocio del casino está en la repetición — y por lo tanto, necesita de la adicción.*

### Bernoulli

Un caso particular es la **Bernoulli**, con único parámetro $p$, notada $X \sim Be(p)$: un único experimento con dos resultados. Equivale a una binomial con $n=1$:

$$X \sim Be(p) = Bi(1, p) \implies R_X = \{0,1\}; \; P(X=0)=1-p; \; P(X=1)=p; \; E(X)=p; \; V(X)=p(1-p)$$

> **Nota:** A veces se denota $q = 1 - p$ a la probabilidad de fracaso, de modo que $P(X=k) = \binom{n}{k} p^k q^{n-k}$ y $V(X) = n \cdot p \cdot q$.

---

## Distribución Hipergeométrica

Consideremos el mismo juego, pero ahora con **5 extracciones SIN reposición**, partiendo de la urna inicial (4 azules, 6 verdes). Las variables $B$ y $G$ se definen igual.

El recorrido cambia: aunque haya 5 extracciones, hay un **máximo de 4 azules**, por lo que $R_B = \{0, 1, 2, 3, 4\}$. Las probabilidades se calculan distinto porque **no hay independencia**. A la variable no le interesa el orden, así que contamos: $k$ azules del grupo de 4, $5-k$ verdes del grupo de 6, sobre todas las formas de sacar 5 de 10:

$$P(B = k) = \frac{\binom{4}{k} \cdot \binom{6}{5-k}}{\binom{10}{5}}$$

Esta estructura es la **distribución Hipergeométrica**: un conjunto de $N$ elementos, del cual se extraen $n \leq N$ sin reposición, con un subgrupo de interés de $M$ elementos. La variable cuenta cuántos elementos del subgrupo aparecen. Se nota $X \sim H(N, M, n)$. En el ejemplo, $N = 10$, $M = 4$, $n = 5$.

Sea $X \sim H(N, M, n)$. Entonces:

| Característica | Fórmula |
|:-:|:-:|
| Recorrido | $R_X = \{\max\{n-(N-M), 0\}; \dots; \min\{M, n\}\}$ |
| Probabilidad | $P(X=k) = \dfrac{\binom{M}{k} \cdot \binom{N-M}{n-k}}{\binom{N}{n}}$ |
| Valor esperado | $E(X) = n \cdot \dfrac{M}{N}$ |
| Varianza | $V(X) = n \cdot \dfrac{M}{N} \cdot \left(1 - \dfrac{M}{N}\right) \cdot \dfrac{N-n}{N-1}$ |

$$\boxed{X \sim H(N,M,n) \implies E(X) = n \cdot \frac{M}{N}, \quad V(X) = n \cdot \frac{M}{N}\left(1 - \frac{M}{N}\right)\frac{N-n}{N-1}}$$

> [!warning] Cuidado con el recorrido
> No siempre el máximo del recorrido es $n$ ni el mínimo es 0. El máximo es $\min\{M, n\}$ (lo que se agote primero: los elementos de interés o las extracciones). El mínimo es $\max\{n-(N-M), 0\}$: si los elementos "no interesantes" ($N-M$) son muy pocos frente a $n$, forzosamente saldrán algunos de interés. Si no se respetan estos límites, los combinatorios dan valores sin sentido (negativos o mayores al conjunto), por lo que valen 0.

**Cálculos para $B \sim H(10, 4, 5)$:**

$$E(B) = 5 \cdot \frac{4}{10} = 2, \qquad E(B^2) = \frac{14}{3}, \qquad V(B) = \frac{14}{3} - 4 = \frac{2}{3}$$

Verificando con la fórmula: $V(B) = 5 \cdot \tfrac{4}{10} \cdot \tfrac{6}{10} \cdot \tfrac{10-5}{10-1} = 5 \cdot 0.4 \cdot 0.6 \cdot \tfrac{5}{9} = \tfrac{2}{3}$.

Para la ganancia $G = 15 - 7B$:

$$E(G) = 15 - 7 \cdot 2 = 1, \qquad V(G) = 49 \cdot \frac{2}{3} = \frac{98}{3} \approx 32.67$$

> [!warning] Verificación del cálculo de la varianza
> El desarrollo "a mano" de $E(B^2)$ en estas extracciones debe dar $E(B^2) = \tfrac{14}{3}$ y por lo tanto $V(B) = \tfrac{14}{3} - 4 = \tfrac{2}{3}$, que coincide con la fórmula cerrada de la hipergeométrica. Conviene usar siempre la fórmula $V(X) = n\,\tfrac{M}{N}(1-\tfrac{M}{N})\tfrac{N-n}{N-1}$ para chequear el resultado.

La conclusión cualitativa del deck es que **la varianza sin reposición es menor** que con reposición ($\tfrac{2}{3} < \tfrac{6}{5}$): la ganancia del casino tiene el mismo promedio pero menos chances de desviarse, lo que lo hace aún más conveniente para el casino.

### Relación con la binomial y aproximación

Si llamamos $p = \tfrac{M}{N}$ a la probabilidad de que una única extracción sea "de interés", las fórmulas se parecen mucho a las de la binomial $Y \sim Bi(n; \tfrac{M}{N})$:

$$V(X) = \underbrace{n \cdot \frac{M}{N}\left(1 - \frac{M}{N}\right)}_{V(Y)} \cdot \underbrace{\frac{N-n}{N-1}}_{\text{factor de corrección}}$$

El factor $\tfrac{N-n}{N-1}$ tiene sentido: a más extracciones, menor varianza. En el caso extremo $N = n$ la varianza vale exactamente 0 (se extraen todos los elementos, por lo que la cantidad de interés es exactamente $M$, una constante).

Cuando $n \ll N$, ese factor es $\approx 1$ y la hipergeométrica se aproxima por la binomial. **Ejemplo:** con $N = 1000$, $M = 400$ y $n = 5$:

| $k$ | Binomial | Hipergeométrica |
|:-:|:-:|:-:|
| 0 | 0.07776 | 0.077241 |
| 1 | 0.25920 | 0.259199 |
| 2 | 0.34560 | 0.346467 |
| 3 | 0.23040 | 0.230592 |
| 4 | 0.07680 | 0.076415 |
| 5 | 0.01024 | 0.010087 |

Las diferencias son mínimas. Sin embargo, con $n = 100$ del mismo conjunto la diferencia ya se nota más.

---

## Distribución Geométrica

Ahora Agustina juega con reposición **hasta ganar por primera vez** para irse victoriosa. Definimos:

- $Z = $ cantidad de extracciones hasta que sale la primera bolita azul.
- $G = $ ganancia del casino, donde $G = 3 \cdot (Z - 1) - 4 = 3 \cdot Z - 7$ (perdió las $Z-1$ apuestas antes de ganar).

El juego podría seguir sin límite, por lo que $R_Z = \mathbb{N}$. La probabilidad $P(Z = k)$ significa que perdió las primeras $k-1$ apuestas y ganó la $k$-ésima — **no hay distintas combinaciones**:

$$P(Z = k) = \left(1 - \frac{2}{5}\right)^{k-1} \cdot \frac{2}{5}$$

Esta es la **distribución Geométrica**: experimentos independientes con dos resultados, donde el criterio de parada es el primer éxito (probabilidad $p$), y $Z$ cuenta la cantidad de experimentos hasta ese éxito. Se nota $Z \sim Ge(p)$.

Sea $Z \sim Ge(p)$, con $q = 1-p$. Entonces:

| Característica | Fórmula |
|:-:|:-:|
| Recorrido | $R_Z = \mathbb{N}$ |
| Probabilidad | $P(Z = k) = q^{k-1} \cdot p$ |
| Valor esperado | $E(Z) = \dfrac{1}{p}$ |
| Varianza | $V(Z) = \dfrac{1-p}{p^2}$ |

$$\boxed{Z \sim Ge(p) \implies E(Z) = \frac{1}{p}, \quad V(Z) = \frac{1-p}{p^2}}$$

### Apéndice: sumas parciales y series

Para calcular $E(Z) = \sum_{k=1}^{+\infty} k \cdot q^{k-1} \cdot p$ necesitamos sumar **infinitos valores**. La idea es calcular **sumas parciales** hasta un valor alto y ver a qué valor se estabilizan:

| $n=$ | 10 | 20 | 50 | 100 |
|:-:|:-:|:-:|:-:|:-:|
| $\sum_{k=1}^{n} k \, q^{k-1} p$ | 2.4244 | 2.4992 | 2.5000 | 2.5000 |

La suma se estabiliza en $2.5 = \tfrac{5}{2}$, por lo que $E(Z) = \tfrac{5}{2}$ (consistente con $\tfrac{1}{p} = \tfrac{1}{2/5}$).

Formalmente esto se justifica con la **suma geométrica** y su derivada:

$$\sum_{k=0}^{+\infty} q^k = \frac{1}{1-q} \quad (|q| < 1) \implies \sum_{k=0}^{+\infty} k \cdot q^{k-1} = \frac{1}{(1-q)^2}$$

de donde $E(Z) = p \cdot \tfrac{1}{(1-q)^2} = \tfrac{p}{p^2} = \tfrac{1}{p}$.

Para la varianza se necesita $E(Z^2)$, cuyas sumas parciales se estabilizan en 10:

| $n=$ | 10 | 20 | 50 | 100 |
|:-:|:-:|:-:|:-:|:-:|
| $\sum_{k=1}^{n} k^2 q^{k-1} p$ | 9.0325 | 9.9814 | 10.0000 | 10.0000 |

$$V(Z) = E(Z^2) - E^2(Z) = 10 - \left(\frac{5}{2}\right)^2 = \frac{15}{4} \implies \sigma(Z) = \frac{\sqrt{15}}{2}$$

**Ganancia con esta estrategia** ($G = 3Z - 7$):

$$E(G) = 3 \cdot \frac{5}{2} - 7 = \frac{1}{2}, \qquad V(G) = 9 \cdot \frac{15}{4} = \frac{135}{4}$$

El casino gana ahora **\$0.5 en promedio** y con menos varianza que jugando 5 veces fijas.

> **Nota:** El valor esperado es **inversamente proporcional a $p$**: si $p$ es chico, hacen falta más intentos para el primer éxito.

### Otra definición de la geométrica

En la literatura existe otra geométrica $Z_e$ que cuenta la cantidad de **fracasos antes** del primer éxito (mismo criterio de parada, pero cuenta otra cosa). Se cumple $Z_e = Z - 1$, y:

$$R_{Z_e} = \mathbb{N}_0, \quad P(Z_e = k) = (1-p)^k \cdot p, \quad E(Z_e) = \frac{1-p}{p}, \quad V(Z_e) = \frac{1-p}{p^2}$$

Como es un traslado, la varianza no cambia.

### Comentario: Binomial Negativa

Una extensión de la geométrica es la **Binomial Negativa**: se repite el experimento hasta llegar a $r$ éxitos. Requiere 2 parámetros, $Z_r \sim BN(r, p)$:

$$R_{Z_r} = \{r, r+1, \dots\}, \quad P(Z_r = k) = \binom{k-1}{r-1} p^r (1-p)^{k-r}, \quad E(Z_r) = \frac{r}{p}, \quad V(Z_r) = \frac{r(1-p)}{p^2}$$

Son los mismos valores de la geométrica multiplicados por $r$.

---

## Distribución de Poisson

*Pobre Agustina, ha desarrollado una ludopatía galopante.* Juega un juego similar con otra urna donde la probabilidad de éxito es mucho menor pero el retorno es mayor. Durante muchas noches perdió la cuenta de cuántas veces apostó, pero sabe que **en promedio gana 3 apuestas por noche**.

Tenemos entonces una binomial $X$ donde **no conocemos $n$** (sólo que es grande) ni $p$ (sólo que es chico), pero sí $E(X) = n \cdot p = 3 = \lambda$. Como $n$ es alto y no hay cota superior, $R_X = \mathbb{N}_0$. Usando $\lambda = np$ y haciendo $n \to +\infty$ en la fórmula binomial:

$$P(X = k) = \frac{n!}{k!(n-k)!} p^k (1-p)^{n-k} \xrightarrow{n \to +\infty} \frac{\lambda^k}{k!} e^{-\lambda}$$

Esta es la **distribución de Poisson**: cuenta la cantidad de veces que ocurre un evento de interés en un tiempo determinado (se puede pensar como "éxitos" en una ventana de tiempo, sin valor máximo). Se nota $Y \sim Po(\lambda)$.

Sea $Y \sim Po(\lambda)$. Entonces:

| Característica | Fórmula |
|:-:|:-:|
| Recorrido | $R_Y = \mathbb{N}_0$ |
| Probabilidad | $P(Y = k) = e^{-\lambda} \cdot \dfrac{\lambda^k}{k!}$ |
| Valor esperado | $E(Y) = \lambda$ |
| Varianza | $V(Y) = \lambda$ |

$$\boxed{Y \sim Po(\lambda) \implies E(Y) = \lambda, \quad V(Y) = \lambda}$$

La demostración de $E(Y) = \lambda$ y $V(Y) = \lambda$ usa la **serie de Maclaurin** de $e^x$:

$$\sum_{k=0}^{+\infty} \frac{x^k}{k!} = e^x$$

Para nuestro ejemplo, $E(X) = \lambda = 3$ y, como $p$ es pequeño, $V(X) = np(1-p) \approx \lambda \cdot 1 = 3$. Las probabilidades aproximadas son $P(X = k) \approx \tfrac{3^k}{k!} e^{-3}$.

> [!warning] Cuándo aproximar binomial por Poisson
> La Poisson permite aproximar las probabilidades de la binomial cuando $n$ es **grande** ($n > 100$) y $p$ es **chico** ($p < 0.01$), considerando $n \cdot p < 10$. En ese caso las medias coinciden y las varianzas son similares. El deck ilustra esto con dos gráficos: con $n=1000, p=0.003, \lambda=3$ las distribuciones de Binomial y Poisson se solapan casi exactamente; con $n=1000, p=0.3, \lambda=300$ (donde $p$ ya no es chico) la aproximación deja de ser buena.

**Ventajas de la Poisson:** tiene un único parámetro (más simple que la binomial), permite hacer cálculos cuando se desconocen $n$ y $p$, y evita el cálculo de factoriales de combinatorios grandes que muchas calculadoras no manejan.

---

## No siempre hay estructura

Las variables no siempre tienen una de estas estructuras conocidas; a veces hay que tratarlas como V.A.D. generales. **Ejemplo:** consideramos el juego de la urna (4 azules, 6 verdes), pero antes de extraer se tira una moneda:

- Si sale **cara** ($C$): se hacen 2 extracciones **sin** reposición.
- Si sale **ceca** ($\overline{C}$): se hacen 2 extracciones **con** reposición.

Se cuenta $X = $ cantidad de bolitas azules extraídas. No conocemos la distribución de $X$, pero podemos descomponer en variables conocidas:

- $X_1 = $ azules cuando sale cara $\sim H(10, 4, 2)$.
- $X_2 = $ azules cuando sale ceca $\sim Bi\left(2, \tfrac{2}{5}\right)$.

Como $R_X = \{0, 1, 2\}$, aplicamos el **Teorema de la Probabilidad Total** con $P(C) = P(\overline{C}) = \tfrac{1}{2}$:

$$P(X = k) = P(X = k \mid C) \cdot P(C) + P(X = k \mid \overline{C}) \cdot P(\overline{C}) = \frac{1}{2}\big(P(X_1 = k) + P(X_2 = k)\big)$$

Calculando cada término:

$$P(X = 0) = \frac{1}{2}\left(\frac{\binom{6}{2}}{\binom{10}{2}} + \left(\frac{3}{5}\right)^2\right) = \frac{26}{75} \approx 0.3467$$

$$P(X = 1) = \frac{1}{2}\left(\frac{\binom{4}{1}\binom{6}{1}}{\binom{10}{2}} + 2 \cdot \frac{3}{5} \cdot \frac{2}{5}\right) = \frac{38}{75} \approx 0.5067$$

$$P(X = 2) = \frac{1}{2}\left(\frac{\binom{4}{2}}{\binom{10}{2}} + \left(\frac{2}{5}\right)^2\right) = \frac{11}{75} \approx 0.1467$$

Estas probabilidades suman 1 ($\tfrac{26+38+11}{75} = 1$). Con estos datos se pueden calcular la media y la varianza con todo lo visto anteriormente.

---

## Resumen

- Una **variable aleatoria** $X : S \mapsto \mathbb{R}$ resume eventos del experimento en números. Es **discreta** cuando su recorrido $R_X$ es discreto.
- Queda caracterizada por su **recorrido** y su **función de probabilidad puntual** $p_X(k) = P(X = k)$, que cumple $\sum_{k \in R_X} p_X(k) = 1$. La **acumulada** $F_X(k) = P(X \leq k)$ es escalonada, creciente y continua a derecha.
- Parámetros clave: $E(X) = \sum k \, p_X(k)$ (lineal), $V(X) = E(X^2) - E^2(X)$ (con $V(aX+c) = a^2 V(X)$). Cuidado: en general $E(XY) \neq E(X)E(Y)$ y $V(X+Y) \neq V(X)+V(Y)$.

Distribuciones discretas conocidas:

| Distribución | Notación | $P(X=k)$ | $E(X)$ | $V(X)$ |
|:-:|:-:|:-:|:-:|:-:|
| Bernoulli | $Be(p)$ | $p^k(1-p)^{1-k}$ | $p$ | $p(1-p)$ |
| Binomial | $Bi(n,p)$ | $\binom{n}{k}p^k(1-p)^{n-k}$ | $np$ | $np(1-p)$ |
| Hipergeométrica | $H(N,M,n)$ | $\dfrac{\binom{M}{k}\binom{N-M}{n-k}}{\binom{N}{n}}$ | $n\dfrac{M}{N}$ | $n\dfrac{M}{N}\!\left(1-\dfrac{M}{N}\right)\!\dfrac{N-n}{N-1}$ |
| Geométrica | $Ge(p)$ | $(1-p)^{k-1}p$ | $\dfrac{1}{p}$ | $\dfrac{1-p}{p^2}$ |
| Binomial Negativa | $BN(r,p)$ | $\binom{k-1}{r-1}p^r(1-p)^{k-r}$ | $\dfrac{r}{p}$ | $\dfrac{r(1-p)}{p^2}$ |
| Poisson | $Po(\lambda)$ | $e^{-\lambda}\dfrac{\lambda^k}{k!}$ | $\lambda$ | $\lambda$ |

- **Aproximaciones:** la Hipergeométrica se aproxima por la Binomial cuando $n \ll N$ (factor $\tfrac{N-n}{N-1} \approx 1$); la Binomial se aproxima por la Poisson cuando $n$ es grande y $p$ chico ($\lambda = np < 10$).
- Cuando una variable **no tiene estructura conocida**, se la trata como V.A.D. general descomponiéndola con el Teorema de la Probabilidad Total a partir de variables conocidas.
