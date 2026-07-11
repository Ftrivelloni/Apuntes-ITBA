# Variables Aleatorias Continuas

## Motivación — de lo discreto a lo continuo

Para introducir las variables aleatorias continuas, partimos de un ejemplo concreto: la **temperatura de verano**. Supongamos que un día de verano elegido al azar utilizamos un termómetro y registramos su temperatura. Definimos:

$$T_0 = \text{Temperatura registrada [ºC] redondeada al grado entero más próximo}$$

Esta variable es **discreta**: toma valores enteros entre 25 y 39 con una distribución de probabilidad conocida. Por ejemplo, $P(T_0 = 36) = 0.1093$. Como toda variable discreta, podemos calcular probabilidades puntuales sumando, y probabilidades de un rango sumando las puntuales que caen dentro:

$$P(35 \leq T_0 \leq 37) = P(T_0=35) + P(T_0=36) + P(T_0=37) = 0.3188$$

### Aumentando la precisión del instrumento

¿Qué sucede si conseguimos un termómetro más preciso? Definimos sucesivamente:

- $T_1$: temperatura redondeada a la **décima** de grado (150 valores posibles).
- $T_2$: temperatura redondeada a la **centésima** de grado.

A medida que el instrumento es más fino, hay más valores posibles, y como toda la probabilidad (que suma 1) debe repartirse entre más valores, las **probabilidades puntuales se vuelven cada vez más chicas**. Veamos qué le pasa a $P(X = 36)$:

| Variable | $P(X = 36)$ | $P(35 \leq X \leq 37)$ |
|:-:|:-:|:-:|
| $T_0$ (entero) | 0.109333 | 0.318756 |
| $T_1$ (décimas) | 0.011432 | 0.236760 |
| $T_2$ (centésimas) | 0.001147 | 0.227631 |

Se observan dos hechos clave:

1. La probabilidad **puntual** $P(X = 36)$ tiende a $0$ a medida que aumenta la precisión.
2. La probabilidad de un **rango** $P(35 \leq X \leq 37)$ **no** se desploma: converge a un valor (cercano a $0.2266$).

Al hacer "zoom" sobre el gráfico de $T_2$ entre 34 y 35, todavía se ve que es discreta (escalonada), pero los valores están tan apiñados que a simple vista parece una curva continua.

---

## La variable aleatoria continua

Las variables anteriores eran **redondeos** de una temperatura que en realidad no tiene un número fijo de decimales. Podemos entonces considerar directamente la variable continua:

$$T = \text{Temperatura [ºC] en un día de verano elegido al azar}$$

que toma **todos** sus valores en un intervalo continuo (asumamos $[25, 40]$). Decimos que se trata de una **variable aleatoria continua** (v.a.c.).

Por lo visto, a medida que se toman más valores las probabilidades puntuales tienden a $0$. Por lo tanto, para una v.a.c. la probabilidad de que tome exactamente un valor $t$ es **cero**:

$$\boxed{P(T = t) = 0, \quad \forall t \in [25, 40]}$$

> [!warning] No es lo mismo "probabilidad cero" que "imposible"
> Que $P(T = t) = 0$ **no** significa que sea imposible que $T$ tome el valor $t$. Significa que no podemos asignar probabilidad positiva a todos los infinitos valores del intervalo sin pasarnos del máximo total (1). Cada valor $t$ es **improbable, pero no imposible**.

---

## Densidad de probabilidad

Si quisiéramos calcular $P(35 \leq T \leq 37)$, en el caso discreto sumábamos. La extensión matemática de una suma ponderada sobre un intervalo continuo es la **integral definida**:

$$P(35 \leq T \leq 37) = \int_{35}^{37} P(T = t)\, dt$$

El problema es que $P(T = t) = 0$, por lo que esa integral daría $0$ para cualquier rango. Para resolverlo se define una **función de densidad de probabilidad** $f_T(t)$, que puede tomar valores positivos y permite que la integral dé un resultado positivo:

$$P(35 \leq T \leq 37) = \int_{35}^{37} f_T(t)\, dt$$

### Propiedades de una densidad

Dada una v.a.c. $X$, una función de densidad $f_X : \mathbb{R} \to \mathbb{R}_0^+$ debe cumplir:

$$f_X(x) \geq 0 \quad \forall x \in \mathbb{R} \qquad\text{y}\qquad \int_{-\infty}^{+\infty} f_X(x)\, dx = 1$$

Una vez definida, para cualquier $a \leq b$ se calcula:

$$\boxed{P(a \leq X \leq b) = \int_a^b f_X(x)\, dx}$$

Es decir, la probabilidad de que $X$ esté en un intervalo es el **área bajo la curva** de su densidad.

> **Comentarios importantes:**
> - El conjunto de valores donde la densidad es positiva se denomina **soporte**. Para restringir los valores posibles de $X$, se asigna $f_X(x) = 0$ fuera del soporte (en el ejemplo, $f_T(t) = 0$ si $t \notin [25,40]$).
> - Como las probabilidades se calculan con una integral, $P(X = a) = \int_a^a f_X(x)\, dx = 0$.
> - **La densidad puede ser mayor que 1**; lo importante es que no integre más que 1 en ningún intervalo.

---

## Distribución acumulada

Al igual que en el caso discreto, se define la **función de distribución acumulada**:

$$\boxed{F_X(t) = P(X \leq t) = \int_{-\infty}^{t} f_X(x)\, dx}$$

con $F_X : \mathbb{R} \to [0,1]$. Cumple las mismas propiedades que en el caso discreto: $0 \leq F_X(t) \leq 1$, es creciente, $\lim_{t\to-\infty} F_X(t) = 0$ y $\lim_{t\to+\infty} F_X(t) = 1$.

Como $X$ es continua, se agregan propiedades extra:

- $F_X$ es **continua** (no solo continua a derecha): $F_X(a) = \lim_{t \to a} F_X(t)$.
- Por el **Teorema Fundamental del Cálculo**, la densidad se obtiene derivando la acumulada:

$$\frac{dF_X(t)}{dt} = f_X(t)$$

Esto es importantísimo: desde la acumulada se obtiene la densidad derivando, y desde la densidad se calculan probabilidades, valor esperado, varianza, etc.

> **Nota:** Ante una v.a.c. de la que no se sabe mucho, conviene **empezar por la acumulada**, ya que $F_X(t) = P(X \leq t)$ es una probabilidad y valen todas las herramientas vistas (Probabilidad Total, Bayes, etc.). Esas herramientas **no** son válidas directamente sobre densidades.

### Paralelismo discreto vs. continuo

| Variable Aleatoria Discreta | Variable Aleatoria Continua |
|:--|:--|
| Probabilidad puntual: $p_X(x) \geq 0$ | Densidad: $f_X(x) \geq 0$ |
| Recorrido $R_X$ (probabilidad positiva) | Soporte $S_X$ (densidad positiva) |
| $\sum_{x \in R_X} p_X(x) = 1$ | $\int_{-\infty}^{+\infty} f_X(x)\, dx = 1$ |
| $F_X(t) = \sum_{x \leq t} p_X(x)$ | $F_X(t) = \int_{-\infty}^{t} f_X(x)\, dx$ |
| $E(X) = \sum_{x} x\, p_X(x)$ | $E(X) = \int_{-\infty}^{+\infty} x\, f_X(x)\, dx$ |
| $E(g(X)) = \sum_{x} g(x)\, p_X(x)$ | $E(g(X)) = \int_{-\infty}^{+\infty} g(x)\, f_X(x)\, dx$ |
| $V(X) = E(X^2) - E^2(X)$ | $V(X) = E(X^2) - E^2(X)$ |

---

## Ejemplo completo: temperatura

Consideremos $T$ con densidad dada por:

$$f_T(t) = \begin{cases} k \cdot (t - 25)^2 \cdot (40 - t) & \text{si } t \in [25, 40] \\ 0 & \text{si } t \notin [25, 40] \end{cases}$$

Queremos responder: el valor de $k$, $P(35 \leq T \leq 37)$, la acumulada $F_T(t)$, $E(T)$ y $V(T)$.

### Valor de $k$

La densidad debe integrar 1. Como fuera de $[25,40]$ vale $0$:

$$\int_{25}^{40} k(t-25)^2(40-t)\, dt = k \int_{25}^{40} \left(-t^3 + 90t^2 - 2625t + 25000\right) dt = k \cdot \frac{16875}{4} = 1$$

$$\boxed{k = \frac{4}{16875}}$$

> **Nota:** Los números de este ejercicio no dan "lindos", pero el procedimiento es el habitual: armar la primitiva polinómica y aplicar Barrow.

### Probabilidad de un rango

Con $k$ conocido, integramos en $[35, 37]$ usando la misma primitiva:

$$P(35 \leq T \leq 37) = \frac{4}{16875} \cdot 956 = \frac{3824}{16875} \approx 0.2266$$

Notar que coincide con el valor al que **convergían** las versiones discretas ($T_0, T_1, T_2$): a mayor precisión, las probabilidades discretas convergen a las continuas.

Además, como en una v.a.c. la probabilidad de un punto es $0$:

$$P(35 \leq T \leq 37) = P(35 < T \leq 37) = P(35 \leq T < 37) = P(35 < T < 37)$$

En general, para cualquier v.a.c.:

$$\boxed{P(a \leq X \leq b) = P(a < X \leq b) = P(a \leq X < b) = P(a < X < b)}$$

### Función de distribución

Como $f_T$ es por tramos, dividimos en tres casos:

$$F_T(t) = \begin{cases} 0 & \text{si } t < 25 \\[4pt] \dfrac{4}{16875}\left(-\dfrac{t^4}{4} + 30t^3 - \dfrac{2625\,t^2}{2} + 25000\,t - \dfrac{703125}{4}\right) & \text{si } 25 \leq t \leq 40 \\[8pt] 1 & \text{si } t > 40 \end{cases}$$

Una vez que se tiene la acumulada, cualquier probabilidad de rango es inmediata, ya que para $a < b$:

$$F_X(b) - F_X(a) = P(a < X \leq b)$$

### Valor esperado

$$E(T) = \int_{25}^{40} t \cdot f_T(t)\, dt = \frac{4}{16875}\int_{25}^{40} t\left(-t^3 + 90t^2 - 2625t + 25000\right) dt = 34$$

### Varianza

Calculamos primero $E(T^2)$:

$$E(T^2) = \int_{25}^{40} t^2 \cdot f_T(t)\, dt = 1165$$

Por lo tanto:

$$V(T) = E(T^2) - E^2(T) = 1165 - 34^2 = 9$$

### Mediana, cuantiles y percentiles

No tenemos un conjunto de datos para "partir a la mitad", así que definimos la **mediana** $x_{0.5}$ como el valor que acumula el 50% de probabilidad:

$$P(X \leq x_{0.5}) = 0.5 \implies F_X(x_{0.5}) = 0.5$$

Para esta variable, $\text{mediana}(T) \approx 34.21$. Más generalmente, para $\alpha \in (0,1)$, el **cuantil** $x_\alpha$ cumple $F_X(x_\alpha) = \alpha$. En el ejemplo: $P_5 \approx 28.73$, $Q_1 \approx 31.84$, $Q_3 \approx 36.35$.

---

## Distribución Uniforme

Otro ejemplo motivador: la **hora del amanecer**. En cierta época amanece entre las 6:15 y 6:20 AM, sin predilección por ningún momento del intervalo (densidad constante). Definimos:

$$T_A = \text{minutos desde las 6 AM en que amanece} \qquad f_{T_A}(t) = \begin{cases} k & \text{si } 15 \leq t \leq 20 \\ 0 & \text{en caso contrario} \end{cases}$$

Imponiendo que integre 1: $\int_{15}^{20} k\, dt = 5k = 1 \implies k = \tfrac{1}{5}$.

La acumulada resulta:

$$F_{T_A}(t) = \begin{cases} 0 & t < 15 \\ \dfrac{t-15}{5} & 15 \leq t \leq 20 \\ 1 & t > 20 \end{cases}$$

Y los momentos: $E(T_A) = \tfrac{35}{2} = 17.5$ (el centro del intervalo, ya que no hay tendencia a valores altos ni bajos) y $V(T_A) = \tfrac{925}{3} - 17.5^2 = \tfrac{25}{12}$.

### Generalización

Dado un intervalo $(a,b)$, decimos que $U$ tiene **distribución uniforme**, $U \sim \mathcal{U}(a,b)$, si su densidad es constante allí:

$$\boxed{f_U(u) = \begin{cases} \dfrac{1}{b-a} & a \leq u \leq b \\ 0 & \text{c.c.} \end{cases}} \qquad F_U(u) = \begin{cases} 0 & u < a \\ \dfrac{u-a}{b-a} & a \leq u \leq b \\ 1 & u > b \end{cases}$$

$$E(U) = \frac{b+a}{2} \qquad V(U) = \frac{(b-a)^2}{12}$$

El ejemplo del amanecer corresponde a $a = 15$, $b = 20$.

---

## Distribución Exponencial

Para modelar **tiempos de funcionamiento** (de falla), supongamos que el tiempo $T_F$ en días de un termómetro sigue:

$$f_{T_F}(t) = \begin{cases} k \cdot e^{-t/1000} & t > 0 \\ 0 & \text{c.c.} \end{cases}$$

### Apéndice: integrales impropias

Para hallar $k$ debemos integrar sobre $(0, +\infty)$. La lógica es similar a las series: integramos hasta un valor alto $M$ y hacemos crecer el límite sin tope:

$$\int_0^{+\infty} k\, e^{-t/1000}\, dt = \lim_{M\to+\infty} k\left[-1000\, e^{-t/1000}\right]_0^M = 1000\,k = 1 \implies k = \frac{1}{1000}$$

La acumulada es $F_{T_F}(t) = 1 - e^{-t/1000}$ para $t > 0$. Para los momentos se usa **integración por partes** (y L'Hôpital para el límite del término evaluado): $E(T_F) = 1000$ y $E(T_F^2) = 2 \cdot 1000^2$, de donde $V(T_F) = 2\cdot1000^2 - 1000^2 = 1000^2$.

### Generalización

Una variable que modela tiempos de ocurrencia se llama **exponencial**, con un único parámetro $\lambda > 0$. Escribimos $T \sim \mathcal{E}(\lambda)$:

$$\boxed{f_T(t) = \lambda\, e^{-\lambda t} \;\;(t>0) \qquad F_T(t) = 1 - e^{-\lambda t}\;\;(t>0)}$$

$$E(T) = \frac{1}{\lambda} \qquad V(T) = \frac{1}{\lambda^2}$$

El ejemplo corresponde a $\lambda = \tfrac{1}{1000}$.

### Falta de memoria

> [!warning] La exponencial "no tiene desgaste"
> La exponencial cumple la propiedad de **falta de memoria**: para $a, b > 0$,
> $$P(T > a + b \mid T > a) = P(T > b)$$
> Si $T$ se mide en horas, $a = 10$, $b = 1$: la probabilidad de que el dispositivo dure más de 11 horas (sabiendo que ya duró 10) es la misma que la de durar más de 1 hora **desde cero**. Es como si el dispositivo "volviera a empezar" sin desgaste. Esta es una suposición fuerte y muchas veces poco realista.

La demostración usa $P(T>t) = e^{-\lambda t}$:

$$P(T > a+b \mid T > a) = \frac{P(T > a+b)}{P(T > a)} = \frac{e^{-\lambda(a+b)}}{e^{-\lambda a}} = e^{-\lambda b} = P(T > b)$$

> **Cuidado:** la propiedad vale **solo en ese sentido**. NO valen $P(T<a+b\mid T>a)=P(T<b)$ ni $P(T>a+b\mid T<a)=P(T>b)$.

---

## Distribución Gamma

Una variable que **sí tiene desgaste** es una generalización de la exponencial: la **Gamma**, $X \sim \Gamma(\alpha, \lambda)$, con un segundo parámetro $\alpha > 0$. Cuando $\alpha = n$ es natural, la densidad es:

$$f_X(x) = \frac{\lambda^n}{(n-1)!} \cdot x^{n-1} \cdot e^{-\lambda x} \qquad (x > 0)$$

> **Nota:** Si $n = 1$, la Gamma **es** una exponencial: $\mathcal{E}(\lambda) = \Gamma(1, \lambda)$. Por eso se la llama generalización. La Gamma **no** tiene fórmula cerrada para su acumulada $F_X(x)$.

Cuando $\alpha$ no es natural, el factorial no tiene sentido y se reemplaza por la **función gamma** $\Gamma(\alpha)$ (extensión continua del factorial vía una integral):

$$f_X(x) = \frac{\lambda^\alpha}{\Gamma(\alpha)} \cdot x^{\alpha-1} \cdot e^{-\lambda x} \qquad (x > 0)$$

Sus momentos son:

$$E(T) = \frac{\alpha}{\lambda} \qquad V(T) = \frac{\alpha}{\lambda^2}$$

Comparando gráficamente: al aumentar $\alpha$ suben el valor esperado y la varianza (los dispositivos duran más); al aumentar $\lambda$ bajan ambos (duran menos).

---

## Variable Aleatoria Normal

Último ejemplo motivador: la **longitud de los termómetros**. La especificación dice 10 cm, pero es difícil lograr el número exacto. La longitud $X$ (en cm) sigue:

$$f_X(x) = \frac{10}{\sqrt{2\pi}} \cdot e^{-50(x-10)^2}$$

Esta densidad **no tiene primitiva**, así que la acumulada se aproxima numéricamente. Por software se obtiene, por ejemplo, $P(X \leq 10) = 0.5$, $P(X \leq 9.9) = 0.1587$, $P(X \leq 10.1) = 0.8413$. Es muy improbable que mida $9.5$ cm o menos, y casi seguro que mida $10.5$ cm o menos.

> **Nota:** Aunque el soporte de la normal es todo $\mathbb{R}$ (admitiría longitudes negativas), la probabilidad de valores absurdos es ínfima, por lo que funciona bien como modelo de longitud.

### Definición general

Una variable así se llama **normal**, con parámetros media $\mu$ y desvío $\sigma$. Escribimos $X \sim \mathcal{N}(\mu, \sigma)$:

$$\boxed{f_X(x) = \frac{1}{\sqrt{2\pi}\,\sigma} \cdot e^{-\frac{(x-\mu)^2}{2\sigma^2}}}$$

Su gran utilidad es que se puede construir con **cualquier** media y **cualquier** desvío, a diferencia de las otras variables vistas (más limitadas o poco realistas). El ejemplo de la longitud corresponde a $\mu = 10$, $\sigma = 0.1$.

Interpretación gráfica:

- El máximo está en $x = \mu$ (coincide con el valor esperado).
- Si $\sigma$ **aumenta**, la densidad baja más lento al alejarse de $\mu$ (más dispersión).
- Si $\sigma$ **disminuye**, la densidad baja bruscamente (la variable se aleja menos de $\mu$).

### Varianza

Se demuestra (con la sustitución $z = \tfrac{x-\mu}{\sigma}$ y las integrales notables de la normal estándar) que:

$$E(X^2) = \mu^2 + \sigma^2 \implies V(X) = E(X^2) - E^2(X) = \mu^2 + \sigma^2 - \mu^2 = \sigma^2$$

---

## Normal estándar y estandarización

La acumulada de la normal no tiene primitiva, pero con la sustitución $z = \tfrac{x-\mu}{\sigma}$ obtenemos:

$$F_X(t) = P(X \leq t) = \int_{-\infty}^{\frac{t-\mu}{\sigma}} \frac{1}{\sqrt{2\pi}}\, e^{-z^2/2}\, dz$$

La densidad resultante es la de una normal con **media 0 y desvío 1**, llamada **normal estándar** $Z \sim \mathcal{N}(0,1)$, cuya acumulada se nota $\Phi(t)$. Así, para cualquier $\mu$ y $\sigma$:

$$\boxed{F_X(t) = \Phi\!\left(\frac{t-\mu}{\sigma}\right)}$$

Es decir: basta calcular numéricamente **una sola** acumulada (la estándar) para obtener las probabilidades de **todas** las normales. Las probabilidades de todas las normales están vinculadas entre sí según **cuántos desvíos** se aleja el valor de la media.

### Estandarización (ejemplo)

Para la longitud ($\mu = 10$, $\sigma = 0.1$), calculamos $F_X(10.05)$ restando la media y dividiendo por el desvío:

$$F_X(10.05) = P\!\left(\frac{X-10}{0.1} \leq \frac{10.05 - 10}{0.1}\right) = \Phi(0.5) = 0.6915$$

---

## Uso de la tabla normal estándar

Se utiliza una tabla de $\Phi(t)$ donde las **filas** dan $t$ hasta el primer decimal y las **columnas** el segundo decimal.

| $t$ | 0.00 | 0.01 | 0.02 | 0.03 | 0.04 | 0.05 | 0.06 | 0.07 | 0.08 | 0.09 |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.0 | 0.5000 | 0.5040 | 0.5080 | 0.5120 | 0.5160 | 0.5199 | 0.5239 | 0.5279 | 0.5319 | 0.5359 |
| 0.3 | 0.6179 | 0.6217 | 0.6255 | 0.6293 | 0.6331 | 0.6368 | 0.6406 | 0.6443 | 0.6480 | 0.6517 |
| 0.6 | 0.7257 | 0.7291 | 0.7324 | 0.7357 | 0.7389 | 0.7422 | 0.7454 | 0.7486 | 0.7517 | 0.7549 |
| 0.8 | 0.7881 | 0.7910 | 0.7939 | 0.7967 | 0.7995 | 0.8023 | 0.8051 | 0.8078 | 0.8106 | 0.8133 |
| 1.0 | 0.8413 | 0.8438 | 0.8461 | 0.8485 | 0.8508 | 0.8531 | 0.8554 | 0.8577 | 0.8599 | 0.8621 |

Por ejemplo: $\Phi(0.36) = 0.6406$, $\Phi(1.03) = 0.8485$, $\Phi(0.60) = 0.7257$.

### Simetría: valores negativos

> [!warning] La tabla no trae valores negativos
> La tabla solo muestra $t \geq 0$. Para $t$ negativo se usa la **simetría** de la normal. Por ejemplo, para $\Phi(-1.04)$:
> $$\boxed{\Phi(z) = 1 - \Phi(-z)}$$
> Así, $\Phi(-1.04) = 1 - \Phi(1.04) = 1 - 0.8508 = 0.1492$.

### Interpolación lineal

Si necesitamos más decimales (p. ej. $\Phi(0.668)$), no hay valor exacto en la tabla. Se aproxima con **interpolación lineal**: para $a < b$ con $\Phi(a), \Phi(b)$ conocidos y $c \in (a,b)$:

$$\Phi(c) \approx \Phi(a) + \frac{\Phi(b) - \Phi(a)}{b - a} \cdot (c - a)$$

Con $\Phi(0.66) = 0.7454$ y $\Phi(0.67) = 0.7486$:

$$\Phi(0.668) \approx 0.7454 + \frac{0.7486 - 0.7454}{0.01}\cdot 0.008 = 0.7479315$$

muy cercano al valor real $\Phi(0.668) = 0.7479332$. Interpolar es **mucho más preciso** que redondear al valor de tabla más próximo.

---

## Cuantiles de la normal

El problema **inverso**: se conoce la acumulada $\alpha$ y se busca el valor que la acumula. Se nota $\Phi^{-1}(\alpha)$ o $z_\alpha$, y cumple $F_Z(z_\alpha) = \alpha$.

Se usa una **tabla de cuantiles** donde las filas dan los primeros decimales de $\alpha$ y las columnas el tercer decimal. Por ejemplo:

| $\alpha$ | $z_\alpha = \Phi^{-1}(\alpha)$ |
|:-:|:-:|
| 0.564 | 0.1611 |
| 0.546 | 0.1156 |
| 0.600 | 0.2533 |
| 0.582 | 0.2070 |
| 0.575 | 0.1891 |

### Cuantiles por debajo de 0.5

Por la simetría, no hace falta tabular $\alpha < 0.5$: el valor que acumula $\alpha$ a izquierda es el **opuesto** del que acumula $\alpha$ a derecha. Por ejemplo, para $\alpha = 0.452$:

$$z_{0.452} = -z_{0.548} = -0.1206$$

(el valor de tabla $z_{0.548} = 0.1206$, con signo negativo).

---

## Propiedades clave de la normal

- **Combinación lineal:** cualquier función lineal de una normal es normal, solo cambian los parámetros:

$$\boxed{X \sim \mathcal{N}(\mu, \sigma) \implies Y = aX + b \sim \mathcal{N}(a\mu + b,\; |a|\sigma)}$$

- **Regla empírica (68 – 95 – 99.7):** el desvío de la normal permite interpretar qué valores son comunes:

| Intervalo | Probabilidad |
|:-:|:-:|
| $[\mu - \sigma,\; \mu + \sigma]$ | $68.27\%$ |
| $[\mu - 2\sigma,\; \mu + 2\sigma]$ | $95.45\%$ |
| $[\mu - 3\sigma,\; \mu + 3\sigma]$ | $99.73\%$ |

Es muy probable que los valores estén a menos de dos desvíos de la media, y prácticamente imposible que estén a más de tres.

- **Simetría:** la normal es simétrica respecto de $\mu$, por lo que su **asimetría (skewness)** es nula:

$$E\!\left[\frac{(X-\mu)^3}{\sigma^3}\right] = 0$$

- **Exceso de kurtosis nulo:** la normal sirve como referencia para el peso de las colas:

$$E\!\left[\frac{(X-\mu)^4}{\sigma^4}\right] - 3 = 0$$

Cuando calculamos la kurtosis de una variable, en realidad estamos comparando el peso de sus colas con el de una normal.

---

## Resumen

- Una **variable aleatoria continua** toma valores en un intervalo continuo y cumple $P(X = t) = 0$ para todo $t$ (probabilidad cero $\neq$ imposible). Surge como límite de variables discretas cada vez más precisas.
- Las probabilidades se calculan como **área bajo la densidad** $f_X$: $P(a \leq X \leq b) = \int_a^b f_X$. La densidad cumple $f_X \geq 0$ e integra 1, y puede superar 1 puntualmente.
- La **acumulada** $F_X(t) = \int_{-\infty}^t f_X$ es continua, y derivándola se recupera la densidad ($F_X' = f_X$). Conviene partir de ella porque es una probabilidad. Para v.a.c. todas las desigualdades estrictas y no estrictas dan el mismo valor.
- **Momentos:** $E(X) = \int x f_X$, $E(g(X)) = \int g(x) f_X$, $V(X) = E(X^2) - E^2(X)$. La mediana y los cuantiles $x_\alpha$ se definen vía $F_X(x_\alpha) = \alpha$.
- Distribuciones conocidas:

| Distribución | Densidad / Soporte | $E$ | $V$ |
|:--|:--|:-:|:-:|
| Uniforme $\mathcal{U}(a,b)$ | $\tfrac{1}{b-a}$ en $[a,b]$ | $\tfrac{a+b}{2}$ | $\tfrac{(b-a)^2}{12}$ |
| Exponencial $\mathcal{E}(\lambda)$ | $\lambda e^{-\lambda t}$, $t>0$ | $\tfrac{1}{\lambda}$ | $\tfrac{1}{\lambda^2}$ |
| Gamma $\Gamma(\alpha,\lambda)$ | $\tfrac{\lambda^\alpha}{\Gamma(\alpha)}x^{\alpha-1}e^{-\lambda x}$, $x>0$ | $\tfrac{\alpha}{\lambda}$ | $\tfrac{\alpha}{\lambda^2}$ |
| Normal $\mathcal{N}(\mu,\sigma)$ | $\tfrac{1}{\sqrt{2\pi}\sigma}e^{-(x-\mu)^2/2\sigma^2}$ | $\mu$ | $\sigma^2$ |

- La **exponencial** tiene falta de memoria (sin desgaste); la **Gamma** la generaliza ($\Gamma(1,\lambda) = \mathcal{E}(\lambda)$) y sí modela desgaste.
- La **normal** se construye con cualquier $\mu$ y $\sigma$. Mediante **estandarización** $z = \tfrac{x-\mu}{\sigma}$ toda probabilidad se reduce a la normal estándar $\Phi$: $F_X(t) = \Phi\!\left(\tfrac{t-\mu}{\sigma}\right)$. Se usa la tabla con simetría $\Phi(z) = 1 - \Phi(-z)$ e interpolación lineal. Cumple la regla 68–95–99.7 y es la referencia para asimetría y kurtosis.
