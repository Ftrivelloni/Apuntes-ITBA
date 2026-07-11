# Vínculos entre Variables

## Motivación — Análisis de consumo

Andrea es gerente de un supermercado y analiza los consumos en su local. Luego de varios días de análisis, concluye que los gastos $G$ (en miles de pesos) en su local siguen una distribución normal de media $75$ y desvío $15$, es decir $G \sim \mathcal{N}(75, 15)$.

Está analizando una campaña de descuentos sobre la compra total basada en el consumo de los clientes. Decide aplicar:

- $5\%$ de descuento si gastan entre $69\,000$ y $78\,000$ pesos,
- $15\%$ de descuento si gastan entre $78\,000$ y $99\,000$ pesos,
- $25\%$ de descuento si gastan más de $99\,000$ pesos.

Si gastan menos de $69\,000$ pesos, no hace descuento.

Este ejemplo motiva la idea central de toda la presentación: muchas veces el valor de una variable está **vinculado** con el de otra, y conociendo la distribución de una podemos deducir la de la otra.

---

## Funciones de una variable aleatoria

### Variable Descuento $D$

Para algunos valores de $G$ podemos establecer un único valor para el porcentaje de descuento $D$. Por lo tanto, $D$ es una **función** de $G$. Como tenemos poca información probabilística de $D$, conviene primero analizar qué valores toma para ver si es discreta o continua.

En este caso $D$ es **discreta**, ya que su recorrido es $R_D = \{0, 5, 15, 25\}$. La función que vincula $G$ con $D$ es:

$$D(G) = \begin{cases} 0 & \text{si } G < 69 \\ 5 & \text{si } 69 \leq G < 78 \\ 15 & \text{si } 78 \leq G < 99 \\ 25 & \text{si } G \geq 99 \end{cases}$$

Como $D$ es discreta, calculamos sus probabilidades puntuales a partir de la distribución de $G$:

$$P(D = 0) = P(G < 69) = \Phi\!\left(\frac{69-75}{15}\right) = \Phi(-0.4) = 0.3446$$

$$P(D = 5) = P(69 \leq G < 78) = \Phi\!\left(\frac{1}{5}\right) - \Phi\!\left(-\frac{2}{5}\right) = 0.2347$$

$$P(D = 15) = P(78 \leq G < 99) = \Phi\!\left(\frac{8}{5}\right) - \Phi\!\left(\frac{1}{5}\right) = 0.3659$$

$$P(D = 25) = P(G \geq 99) = 1 - \Phi\!\left(\frac{8}{5}\right) = 0.0548$$

Con estas probabilidades podemos calcular el valor esperado y la varianza:

$$E(D) = 0 \cdot 0.3446 + 5 \cdot 0.2347 + 15 \cdot 0.3659 + 25 \cdot 0.0548 = 8.0325$$

$$E(D^2) = 5^2 \cdot 0.2347 + 15^2 \cdot 0.3659 + 25^2 \cdot 0.0548 = 122.4533$$

$$V(D) = E(D^2) - E^2(D) = 57.9322 \implies \sigma(D) = 7.6113$$

---

### Variable Gasto con Descuento $GD$ (función continua)

También se puede analizar el gasto resultante $GD$ luego de aplicar el descuento. Nuevamente hay una función que vincula $D$ con $GD$:

$$GD = \begin{cases} G & \text{si } D = 0 \\ 0.95 \cdot G & \text{si } D = 5 \\ 0.85 \cdot G & \text{si } D = 15 \\ 0.75 \cdot G & \text{si } D = 25 \end{cases}$$

A diferencia de $D$, la variable $GD$ es **continua**. Para analizar una variable continua conviene empezar por la **distribución acumulada**, ya que es una probabilidad y podemos usar el Teorema de Probabilidad Total sobre la partición que generan los valores de $D$:

$$F_{GD}(t) = F_G(t)\, p_D(0) + F_G\!\left(\frac{t}{0.95}\right) p_D(5) + F_G\!\left(\frac{t}{0.85}\right) p_D(15) + F_G\!\left(\frac{t}{0.75}\right) p_D(25)$$

Derivando obtenemos la densidad $f_{GD}$, y aprovechando la linealidad de la integral podemos calcular el valor esperado. Por ejemplo, mediante el cambio de variable $u = \frac{20}{19} t$ en el segundo término, cada integral se reduce a un múltiplo de $E(G)$:

$$E(GD) = p_D(0) \cdot 75 + p_D(5) \cdot \tfrac{19}{20} \cdot 75 + p_D(15) \cdot \tfrac{17}{20} \cdot 75 + p_D(25) \cdot \tfrac{3}{4} \cdot 75$$

$$E(GD) = 25.8434 + 16.7211 + 23.3287 + 3.0825 = 68.9756$$

Obviamente da un valor menor al gasto sin descuento, pero le permite a la gerente evaluar la ganancia neta.

---

### Variable Distancia $X$ y Gasto Promedio $G_P$

La gerente cuenta con datos sobre la distancia $X$ (en km) entre el local y las residencias de sus clientes, que sigue una distribución **uniforme** entre $0$ y $5$, es decir $X \sim U(0, 5)$. Por lo tanto:

$$f_X(x) = \frac{1}{5} \;\; (0 \leq x \leq 5), \qquad E(X) = \frac{5}{2}, \qquad V(X) = \frac{25}{12}$$

Observa además un vínculo curioso: el gasto promedio $G_P$ (en miles de pesos) de las personas tiene una relación cuadrática con la distancia:

$$G_P = g(X) = 8X^2 - 40X + 100$$

Gráficamente es una parábola con vértice en $x = 2.5$: el gasto promedio está entre $50\,000$ y $100\,000$ pesos según la cercanía (más gasto en los extremos, menos en el medio).

#### Distribución de $G_P$ (función continua de variable continua)

$G_P$ es continua. Conviene calcular su distribución usando el vínculo con $X$, cuya $F_X$ es conocida:

$$F_{G_P}(t) = P(8X^2 - 40X + 100 \leq t)$$

Para usar $F_X$ hay que despejar $X$, es decir resolver la inecuación cuadrática. Esto depende del valor de $t$, identificando las raíces de la parábola $y = 8x^2 - 40x + 100 - t$:

- **Si $t < 50$:** el discriminante es negativo ($1600 - 3200 + 32t < 0 \Leftrightarrow t < 50$), no hay raíces, la parábola queda siempre por encima de $t$ y $F_{G_P}(t) = P(\varnothing) = 0$.
- **Si $t \geq 50$:** las raíces son $x_{1,2} = \frac{5}{2} \pm \frac{\sqrt{2t-100}}{4}$, y entonces

$$F_{G_P}(t) = F_X\!\left(\frac{5}{2} + \frac{\sqrt{2t-100}}{4}\right) - F_X\!\left(\frac{5}{2} - \frac{\sqrt{2t-100}}{4}\right)$$

Recordando que $F_X$ es partida, hay que verificar dónde caen los argumentos. Resolviendo se ve que ambos argumentos están dentro de $[0,5]$ cuando $50 \leq t \leq 100$. La conclusión es:

$$\boxed{F_{G_P}(t) = \begin{cases} 0 & \text{si } t < 50 \\ \dfrac{\sqrt{2t-100}}{10} & \text{si } 50 \leq t \leq 100 \\ 1 & \text{si } t > 100 \end{cases}}$$

Derivando, la densidad es:

$$f_{G_P}(t) = \frac{1}{10 \cdot \sqrt{2t-100}} \quad (50 \leq t \leq 100)$$

Con un cambio de variable $u = 2t - 100$, el valor esperado resulta:

$$E(G_P) = \int_{50}^{100} t \cdot \frac{1}{10\sqrt{2t-100}}\, dt = \frac{200}{3} = 66.6667$$

> [!warning] No confundir $E(G_P)$ con $G_P(E(X))$
> Calcular el valor esperado de una función NO es lo mismo que evaluar la función en el valor esperado. Aquí $E(G_P) = 66.6667$ pero $g(E(X)) = g(2.5) = 50$. Son cantidades distintas.

#### Alternativa con valores característicos

Una manera más sencilla de obtener el valor esperado de una función es usar la linealidad sobre los valores característicos de $X$, sin calcular la distribución de $G_P$:

$$E(G_P) = E(8X^2 - 40X + 100) = 8\,E(X^2) - 40\,E(X) + 100 = 8\!\left(\tfrac{25}{12} + \tfrac{25}{4}\right) - 40 \cdot \tfrac{5}{2} + 100 = \frac{200}{3}$$

usando $E(X^2) = V(X) + E^2(X)$. Estas cuentas resultan más simples, pero conviene tener ambas alternativas: con la distribución podemos calcular mucho más que un valor esperado (densidades, probabilidades, etc.).

> **Nota:** Para una función $Y = g(X)$, a cada valor de $X$ le corresponde un **único** valor de $Y$. Lo más importante al resolver es identificar si $Y$ es continua (se calcula su distribución) o discreta (se calcula su recorrido y sus probabilidades).

---

## Inversa generalizada (simulación)

Simular datos con una distribución dada es difícil porque un algoritmo deja de ser aleatorio (por eso se habla de generadores **pseudo-aleatorios**). La probabilidad resuelve esto: a partir de una variable $U \sim U(0,1)$ se puede generar cualquier distribución $F_X$ buscando una función $g$ tal que $g(U) \sim F_X$.

Dicha función se obtiene **invirtiendo** la función de distribución. Para el gasto promedio, tomamos $y \in (0,1)$ y despejamos $t$:

$$F_{G_P}(t) = y \implies \frac{\sqrt{2t-100}}{10} = y \implies t = 50y^2 + 50$$

Por lo tanto, si $U \sim U(0,1)$, entonces $g(U) = 50 U^2 + 50$ tiene la misma distribución que $G_P$. Aplicando esta función a una muestra uniforme se obtienen datos cuya distribución coincide con la del enunciado.

### Variables discretas

Cuando la variable es discreta, la distribución da **saltos** y no se puede invertir de forma usual, pero la idea se adapta. Por ejemplo, para simular $X \sim H(10, 4, 2)$ con $R_X = \{0,1,2\}$:

$$P(X=0) = \frac{1}{3}, \quad P(X=1) = \frac{8}{15}, \quad P(X=2) = \frac{2}{15}$$

$$F_X(t) = \begin{cases} 0 & t < 0 \\ \tfrac{1}{3} & 0 \leq t < 1 \\ \tfrac{13}{15} & 1 \leq t < 2 \\ 1 & t \geq 2 \end{cases}$$

Se usan las **ubicaciones de los saltos** como imagen y los **rangos de los saltos** para transformar $U$:

$$g(U) = \begin{cases} 0 & 0 \leq U < \tfrac{1}{3} \\ 1 & \tfrac{1}{3} \leq U < \tfrac{13}{15} \\ 2 & \tfrac{13}{15} \leq U < 1 \end{cases}$$

Aplicando $g$ a una uniforme se obtienen frecuencias que coinciden con las probabilidades de la hipergeométrica.

---

## Variables Aleatorias Bidimensionales Discretas

### Ejemplo de las filas del supermercado

Andrea fija en las cajas una cantidad máxima de artículos: $20$, $40$ o $60$. Esto influye en la longitud de las filas (las cajas de menos artículos son más largas). Federico es un cliente cuyas compras son poco planificadas, por lo que puede necesitar cualquier caja. La cantidad de personas en la fila $N$ está **vinculada** con el número máximo de artículos $M$ de la caja elegida.

Como ambas variables están vinculadas, no tiene sentido analizarlas por separado. Las **probabilidades conjuntas** siguen:

$$P(M = i \cap N = j) = \binom{8 - i/10}{j} \cdot \frac{80-i}{120} \cdot \left(\frac{3}{4}\right)^j \left(\frac{1}{4}\right)^{8 - i/10 - j}$$

para $i \in \{20, 40, 60\}$ y $0 \leq j \leq 8 - i/10$, y $0$ en caso contrario. Notar que si $M=20$ el máximo de personas es $6$, si $M=40$ es $4$ y si $M=60$ es $2$. Numéricamente:

| | $N{=}0$ | $N{=}1$ | $N{=}2$ | $N{=}3$ | $N{=}4$ | $N{=}5$ | $N{=}6$ |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| $M{=}20$ | 0.000122 | 0.002197 | 0.016479 | 0.065918 | 0.148315 | 0.177979 | 0.088989 |
| $M{=}40$ | 0.001302 | 0.015625 | 0.070312 | 0.140625 | 0.105469 | 0 | 0 |
| $M{=}60$ | 0.010417 | 0.062500 | 0.093750 | 0 | 0 | 0 | 0 |

> **Nota:** A diferencia de las funciones anteriores, aquí **no hay un único valor de $N$ para cada $M$**: no existe una función que las vincule, pero sus probabilidades sí están vinculadas.

### Distribuciones marginales

Las **marginales** (en los márgenes de la tabla) se obtienen sumando con el Teorema de Probabilidad Total. Sumando por filas:

$$P(M = i) = \frac{80 - i}{120} \implies P(M=20) = \frac{1}{2}, \;\; P(M=40) = \frac{1}{3}, \;\; P(M=60) = \frac{1}{6}$$

Sumando por columnas se obtienen las de $N$:

| $j$ | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| $P(N=j)$ | $\tfrac{97}{8192}$ | $\tfrac{329}{4096}$ | $\tfrac{1479}{8192}$ | $\tfrac{423}{2048}$ | $\tfrac{2079}{8192}$ | $\tfrac{729}{4096}$ | $\tfrac{729}{8192}$ |
| valor | 0.011841 | 0.080322 | 0.180542 | 0.206543 | 0.253784 | 0.177979 | 0.088989 |

### Probabilidades condicionales

Al estar vinculadas, tienen sentido las condicionales (usan las intersecciones):

- Si se sabe que eligió la caja de $60$, nunca tendrá $6$ personas: $P(N=6 \mid M=60) = \dfrac{0}{P(M=60)} = 0$.
- Si hay $6$ personas en la fila, es seguro que eligió la de $20$: $P(M=20 \mid N=6) = \dfrac{P(N=6)}{P(N=6)} = 1$.
- $P(N=2 \mid M=40) = \dfrac{P(N=2 \cap M=40)}{P(M=40)} = \dfrac{6 \cdot \tfrac{1}{3} \cdot \left(\tfrac{3}{4}\right)^2 \left(\tfrac{1}{4}\right)^2}{\tfrac{1}{3}} = \dfrac{27}{128}$.

### Representación gráfica

Cuando se analizan variables vinculadas, **graficar las combinaciones con probabilidad positiva** es de mucha utilidad: aparecen como puntos en el plano y permiten identificar regiones, calcular marginales (fijando una variable y viendo qué valores de la otra son relevantes) e identificar qué observaciones corresponden a cada valor de una función como $K = N/M$.

Por ejemplo, para calcular $P\!\left(\frac{N}{M} \leq \frac{1}{6}\right)$, en lugar de recorrer las $15$ combinaciones conviene usar el **complemento**, ya que solo $3$ combinaciones no cumplen la condición:

$$P\!\left(\frac{N}{M} \leq \frac{1}{6}\right) = 1 - P(M{=}20 \cap N{=}4) - P(M{=}20 \cap N{=}5) - P(M{=}20 \cap N{=}6)$$

$$= 1 - \frac{1215}{8192} - \frac{729}{4096} - \frac{729}{8192} = \frac{2395}{4096} = 0.5847$$

### Definiciones formales

Dadas dos variables discretas $X$ e $Y$, $(X,Y)$ es un **vector aleatorio bidimensional**. La **distribución conjunta** es:

$$p_{X,Y}(i,j) = P(X = i \cap Y = j)$$

El recorrido del vector no es lo mismo que las combinaciones de recorridos, ya que algunas combinaciones tienen probabilidad nula. Las marginales, condicionales y su vínculo con la conjunta son:

$$p_X(i) = \sum_{j \in R_Y} p_{X,Y}(i,j), \qquad p_{X \mid Y=j}(i) = \frac{p_{X,Y}(i,j)}{p_Y(j)}$$

$$\boxed{p_{X,Y}(i,j) = p_{X \mid Y=j}(i) \cdot p_Y(j) = p_{Y \mid X=i}(j) \cdot p_X(i)}$$

### Valores esperados de funciones del vector

No tiene sentido el valor esperado de un vector, pero sí el de una función $g(X,Y)$ cuyo resultado sea real:

$$E(g(X,Y)) = \sum_{i \in R_X} \sum_{j \in R_Y} g(i,j) \cdot p_{X,Y}(i,j)$$

Aprovechando la conjunta podemos calcular las medias directamente, sin pasar por las marginales:

$$E(M) = \frac{100}{3} = 33.3333, \qquad E(N) = \frac{7}{2} = 3.5$$

---

## Independencia

Hemos visto independencia entre eventos. Cada valor que toma una variable se corresponde con un evento, y entre todos forman una partición. Decimos que **$X$ e $Y$ son independientes** si todos sus eventos asociados son independientes, lo que equivale a la factorización:

$$p_{X,Y}(i,j) = p_X(i) \cdot p_Y(j), \quad \forall\, i,j$$

También las condicionales no se ven afectadas: $p_{X \mid Y=j}(i) = p_X(i)$.

**Propiedad:** Si $X$ e $Y$ son independientes, $E(X \cdot Y) = E(X) \cdot E(Y)$.

> [!warning] No vale la recíproca
> Que se cumpla $E(X \cdot Y) = E(X)\,E(Y)$ **no** implica que las variables sean independientes. La igualdad de valores esperados es una consecuencia de la independencia, no equivalente a ella.

En el ejemplo de las filas, $M$ y $N$ **no** son independientes; basta un contraejemplo:

$$p_{M,N}(60, 6) = 0 \neq p_M(60) \cdot p_N(6) = \frac{1}{6} \cdot \frac{729}{8192}$$

---

## Covarianza y correlación

Cuando analizamos dos variables a la vez, podemos ver si sus valores tienden a crecer en conjunto o no. La **covarianza** resume esa información en un número:

$$\boxed{\text{Cov}(X,Y) = E\big((X - E(X))(Y - E(Y))\big) = E(X \cdot Y) - E(X) \cdot E(Y)}$$

- Si el producto tiende a ser **positivo**, ambas variables tienden a tener valores altos juntas o bajos juntas (tendencia **creciente**).
- Si tiende a ser **negativo**, una alta con la otra baja (tendencia **decreciente**).

Propiedades: es simétrica, $\text{Cov}(X,X) = V(X)$, y admite la forma corta de arriba.

### Coeficiente de correlación

Como la covarianza depende de las unidades, se usa el **coeficiente de correlación**, que es adimensional:

$$\boxed{\rho(X,Y) = \frac{\text{Cov}(X,Y)}{\sigma(X) \cdot \sigma(Y)}}$$

Siempre toma valores en $[-1, 1]$:

- $\rho = 1$: hay una función **lineal creciente** entre las variables ($Y = mX + b$, $m > 0$).
- $\rho = -1$: hay una función **lineal decreciente** ($m < 0$).

> [!warning] La correlación mide vínculos lineales
> $\rho$ mide únicamente si las variables tienen un vínculo **lineal**. Dos variables pueden estar fuertemente relacionadas (por ejemplo de forma cuadrática) y tener $\rho = 0$.

### Aplicación al ejemplo

Para la covarianza entre $M$ y $N$ necesitamos $E(M \cdot N)$:

$$E(M \cdot N) = \sum_{i} \sum_{j} i \cdot j \cdot p_{M,N}(i,j) = 100$$

$$\text{Cov}(M,N) = E(M \cdot N) - E(M) \cdot E(N) = 100 - \frac{100}{3} \cdot \frac{7}{2} = -\frac{50}{3}$$

El signo negativo tiene sentido: a mayor cantidad de artículos máximos, menor es la tendencia de personas en la fila.

También se puede calcular el valor esperado de funciones como $\dfrac{N}{M}$:

$$E\!\left(\frac{N}{M}\right) = \sum_{i} \sum_{j} \frac{j}{i} \cdot p_{M,N}(i,j) = 0.141667$$

---

## Variables Aleatorias Bidimensionales Continuas

Todo lo visto para el caso discreto tiene su correspondiente continuo: las probabilidades puntuales se reemplazan por una **densidad conjunta** $f_{X,Y}(x,y)$ y las sumas por integrales.

| Concepto | Discreto | Continuo |
|:--|:--|:--|
| Distribución | $p_{X,Y}(i,j)$ | $f_{X,Y}(x,y)$ |
| Recorrido / Soporte | $R_{X,Y} = \{(i,j) : p_{X,Y} > 0\}$ | $S(X,Y) = \{(x,y) : f_{X,Y} > 0\}$ |
| Probabilidad de $A$ | $\sum_{(i,j) \in R_{X,Y} \cap A} p_{X,Y}$ | $\iint_A f_{X,Y}\, dx\, dy$ |
| Marginal | $p_X(i) = \sum_j p_{X,Y}$ | $f_X(x) = \int_{-\infty}^{+\infty} f_{X,Y}\, dy$ |
| Condicional | $p_{Y \mid X=i}(j) = \tfrac{p_{X,Y}}{p_X}$ | $f_{Y \mid X=x}(y) = \tfrac{f_{X,Y}}{f_X}$ |
| Independencia | $p_{X,Y} = p_X \, p_Y$ | $f_{X,Y} = f_X \, f_Y$ |

La covarianza y la correlación se definen igual en ambos casos.

### Ejemplo: banana y dulce de leche

Andrea pone un estante de dulce de leche al lado de las bananas y analiza ambos consumos ($B$ y $D$, en miles de pesos), con densidad conjunta:

$$f_{B,D}(b,d) = \begin{cases} k & \text{si } 0 \leq b \leq 4,\; 2b \leq d \leq 4b \\ 0 & \text{en caso contrario} \end{cases}$$

Como la densidad es **constante** en el soporte (un triángulo), decimos que $(B,D)$ es **uniforme** sobre el soporte.

#### Valor de $k$

La densidad conjunta debe integrar $1$. Basta integrar sobre el soporte:

$$1 = \int_0^4 \int_{2b}^{4b} k \, dd \, db = k \int_0^4 2b \, db = k \cdot 16 \implies k = \frac{1}{16}$$

#### Densidad marginal de $B$

Para cada $b \in [0,4]$, $d$ recorre el soporte entre $2b$ y $4b$:

$$f_B(b) = \int_{2b}^{4b} \frac{1}{16}\, dd = \frac{1}{16}(4b - 2b) = \frac{b}{8} \quad (0 \leq b \leq 4)$$

> **Nota:** Que la conjunta sea uniforme sobre el triángulo **no** implica que las marginales sean uniformes: aquí $f_B(b) = b/8$ no es constante.

#### Densidad marginal de $D$

> [!warning] Error común con los límites de integración
> Es frecuente escribir $f_D(d) = \int_{2b}^{4b} \frac{1}{16}\, db$. Esto está **mal**: los límites no pueden depender de la misma variable de integración $b$, y el resultado quedaría en función de $b$ en vez de $d$. Hay que invertir las rectas: $d = 2b \Rightarrow b = d/2$ y $d = 4b \Rightarrow b = d/4$.

Viendo el gráfico, los límites dependen del valor de $d$ (con $f_D(d) = 0$ si $d \notin [0,16]$):

- Si $0 \leq d \leq 8$, $b$ va de $\frac{d}{4}$ a $\frac{d}{2}$:

$$f_D(d) = \int_{d/4}^{d/2} \frac{1}{16}\, db = \frac{1}{16}\left(\frac{d}{2} - \frac{d}{4}\right) = \frac{d}{64}$$

- Si $8 < d \leq 16$, $b$ va de $\frac{d}{4}$ a $4$:

$$f_D(d) = \int_{d/4}^{4} \frac{1}{16}\, db = \frac{1}{16}\left(4 - \frac{d}{4}\right) = \frac{1}{4} - \frac{d}{64}$$

$$\boxed{f_D(d) = \begin{cases} \dfrac{d}{64} & 0 \leq d \leq 8 \\ \dfrac{1}{4} - \dfrac{d}{64} & 8 < d \leq 16 \\ 0 & \text{en caso contrario} \end{cases}}$$

#### Valores esperados y covarianza

Se pueden calcular usando la conjunta o la marginal (ambas dan lo mismo):

$$E(B) = \int_0^4 \int_{2b}^{4b} \frac{b}{16}\, dd\, db = \frac{8}{3}, \qquad E(D) = 8$$

Para la covarianza falta $E(B \cdot D)$:

$$E(B \cdot D) = \int_0^4 \int_{2b}^{4b} \frac{b \cdot d}{16}\, dd\, db = \frac{1}{16}\int_0^4 6b^3\, db = 24$$

$$\text{Cov}(B,D) = E(B \cdot D) - E(B) \cdot E(D) = 24 - \frac{8}{3} \cdot 8 = \frac{8}{3}$$

La covarianza es positiva, como esperábamos: al aumentar una variable tiende a aumentar la otra.

#### Probabilidad de gasto combinado

Para $P(B + D \leq 10)$ conviene graficar la región del plano. La recta $B + D = 10$ corta el soporte, partiendo la integral en dos:

$$P(B + D \leq 10) = \int_0^2 \int_{2b}^{4b} \frac{1}{16}\, dd\, db + \int_2^{10/3} \int_{2b}^{10-b} \frac{1}{16}\, dd\, db = \frac{5}{12}$$

#### Distribución del gasto total $G_T = B + D$

Para $F_{G_T}(t) = P(B + D \leq t)$ los cambios de región de integración ocurren cuando las intersecciones de la recta $B+D=t$ con los bordes del soporte dejan de estar en él. Se separan $4$ casos:

$$\boxed{F_{G_T}(t) = \begin{cases} 0 & t < 0 \\ \dfrac{t^2}{240} & 0 \leq t < 12 \\ \dfrac{t}{4} - \dfrac{3}{2} - \dfrac{t^2}{160} & 12 \leq t \leq 20 \\ 1 & t > 20 \end{cases}}$$

Con esta distribución se pueden calcular la densidad, el valor esperado y el desvío de $G_T$.

---

## Variables de mezcla

Los gastos de Federico tienen mucha variabilidad según su día. Solo puede tener uno de dos problemas (si tiene hambre no tiene sueño y viceversa), de modo que estos eventos forman una **partición**:

- $S$ = tiene sueño: $G_S \sim U(20, 50)$, con $P(S) = 0.4$.
- $H$ = tiene hambre: $G_H = 30 + Y$ con $Y \sim \mathcal{E}\!\left(\tfrac{1}{40}\right)$ (exponencial de media $40$ trasladada en $30$), con $P(H) = 0.35$.
- $R$ = ninguno: $G_R \sim \mathcal{N}(40, 5)$, con $P(R) = 0.25$.

No conocemos la distribución de $G$ directamente, solo condicional a cada escenario. Como forman una partición, aplicamos el Teorema de Probabilidad Total:

$$F_G(t) = F_{G_S}(t) \cdot P(S) + F_{G_H}(t) \cdot P(H) + F_{G_R}(t) \cdot P(R)$$

donde $F_{G_S}$ es la uniforme, $F_{G_H}(t) = 1 - e^{-\frac{t-30}{40}}$ para $t > 30$, y $F_{G_R}(t) = \Phi\!\left(\frac{t-40}{5}\right)$. Tanto la distribución como la densidad de la variable total se obtienen como **combinación lineal** de las funciones de cada escenario, ponderadas por las probabilidades:

$$\boxed{f_G(t) = f_{G_S}(t) \cdot P(S) + f_{G_H}(t) \cdot P(H) + f_{G_R}(t) \cdot P(R)}$$

### Valor esperado de una mezcla

La misma combinación lineal vale para el valor esperado (y no usa cómo se distribuye cada escenario, solo sus medias):

$$E(G) = P(S) E(G_S) + P(H) E(G_H) + P(R) E(G_R)$$

$$E(G) = 0.4 \cdot \frac{20+50}{2} + 0.35 \cdot (30 + 40) + 0.25 \cdot 40 = 48.5$$

### Desvío de una mezcla

> [!warning] La descomposición NO vale para el desvío
> En general, $\sigma(G) \neq P(S)\,\sigma(G_S) + P(H)\,\sigma(G_H) + P(R)\,\sigma(G_R)$. La combinación lineal funciona para $F_G$, $f_G$, $E(G)$ y $E(G^2)$, **pero no** para $V(G)$ ni $\sigma(G)$.

Sí vale para $E(G^2)$, que junto con $E(G)$ permite obtener la varianza. Usando $E(G_i^2) = V(G_i) + E^2(G_i)$:

$$E(G^2) = 0.4\!\left(\frac{30^2}{12} + 35^2\right) + 0.35\,(40^2 + 70^2) + 0.25\,(5^2 + 40^2) = 3201.25$$

$$V(G) = 3201.25 - 48.5^2 = 849 \implies \sigma(G) = 29.1376$$

### Definición general

Una variable de **mezcla** es una variable $X$ cuya distribución se desconoce, pero se sabe cómo se distribuye en cada escenario $A_i$ de una partición $\{A_i\}_{1 \leq i \leq n}$. Llamando $X_i = X \mid A_i$, valen:

$$F_X(t) = \sum_i F_{X_i}(t) \, P(A_i), \qquad f_X(t) = \sum_i f_{X_i}(t) \, P(A_i)$$

$$E(g(X)) = \sum_i E(g(X_i)) \, P(A_i)$$

pero **NO** vale en general $V(X) = \sum_i V(X_i) P(A_i)$ ni para $\sigma$.

---

## Esperanza y varianza condicional

Volviendo a las filas, recordemos que $N \mid M=i \sim Bi\!\left(8 - \tfrac{i}{10};\, \tfrac{3}{4}\right)$. Por lo tanto su valor esperado y varianza dependen del condicional:

$$E(N \mid M=i) = \left(8 - \frac{i}{10}\right)\frac{3}{4} = 6 - \frac{3i}{40}, \qquad V(N \mid M=i) = \frac{3}{2} - \frac{3i}{160}$$

Esto define dos **funciones** de $M$:

$$E(N \mid M) = g(M) = 6 - \frac{3M}{40}, \qquad V(N \mid M) = h(M) = \frac{3}{2} - \frac{3M}{160}$$

### Valor esperado condicional

Dadas $X$ e $Y$, $E(Y \mid X)$ es una función $g(X)$ que describe el promedio de $Y$ condicional a cada valor de $X$.

> **Propiedad clave (ley de esperanza total):**
>
> $$\boxed{E(Y) = E(E(Y \mid X)) = E(g(X))}$$
>
> Promediamos $Y$ según los valores de $X$, y luego promediamos según $X$.

Esto simplifica cálculos. En lugar de la larga sumatoria para $E(N)$:

$$E(N) = E(E(N \mid M)) = E\!\left(6 - \frac{3M}{40}\right) = 6 - \frac{3}{40} \cdot E(M) = 6 - \frac{3}{40} \cdot \frac{100}{3} = \frac{7}{2}$$

Otra propiedad útil: al condicionar a $X$, esta permanece constante y se la puede sacar:

$$E(s(X) \cdot t(Y) \mid X) = s(X) \cdot E(t(Y) \mid X)$$

Aplicado a la covarianza, calculamos $E(M \cdot N)$ de forma más sencilla:

$$E(M \cdot N) = E(M \cdot E(N \mid M)) = E\!\left(M\!\left(6 - \frac{3M}{40}\right)\right) = 6\,E(M) - \frac{3}{40}\,E(M^2) = 100$$

usando $E(M^2) = V(M) + E^2(M)$, lo que reproduce $\text{Cov}(M,N) = -\frac{50}{3}$.

### Varianza condicional

> **Propiedad (ley de varianza total):**
>
> $$\boxed{V(Y) = E(V(Y \mid X)) + V(E(Y \mid X))}$$

Aplicada a $N$:

$$V(N) = E\!\left(\frac{3}{2} - \frac{3M}{160}\right) + V\!\left(6 - \frac{3M}{40}\right) = \frac{3}{2} - \frac{3}{160}E(M) + \frac{3^2}{40^2}V(M) = \frac{17}{8}$$

### Caso continuo: actualización del ejemplo banana–dulce de leche

Estas propiedades también valen para variables continuas. Supongamos que el vínculo correcto es:

$$B \sim U(0,4), \qquad D \mid B=b \sim U(2b, 4b)$$

Con esto el soporte es el mismo, pero la conjunta **deja de ser uniforme**. Conocemos:

$$E(D \mid B) = 3B, \qquad V(D \mid B) = \frac{(2B)^2}{12} = \frac{B^2}{3}$$

Por lo tanto, sin calcular la conjunta:

$$E(D) = E(E(D \mid B)) = E(3B) = 3 \cdot E(B) = 6$$

$$V(D) = E(V(D \mid B)) + V(E(D \mid B)) = E\!\left(\frac{B^2}{3}\right) + V(3B) = \frac{1}{3}(V(B) + E^2(B)) + 9\,V(B) = \frac{52}{9}$$

---

## Resumen

- **Funciones de una variable** $Y = g(X)$: a cada $X$ le corresponde un único $Y$. Lo primero es identificar si $Y$ es discreta (calcular recorrido y probabilidades) o continua (calcular $F_Y$ vía $F_X$ despejando $X$).
- $E(g(X))$ se calcula con la distribución de $g(X)$ o, más simple, con los valores característicos de $X$ ($E(X)$, $V(X)$). Cuidado: $E(g(X)) \neq g(E(X))$.
- **Inversa generalizada:** para simular cualquier distribución a partir de $U \sim U(0,1)$ se invierte $F_X$; en el caso discreto se usan las ubicaciones y rangos de los saltos.
- **Vector bidimensional discreto:** distribución conjunta $p_{X,Y}$, marginales (suma por filas/columnas), condicionales, y $E(g(X,Y)) = \sum\sum g \cdot p_{X,Y}$.
- **Independencia:** $p_{X,Y} = p_X \, p_Y$. Implica $E(XY) = E(X)E(Y)$, pero **no** vale la recíproca.
- **Covarianza** $\text{Cov}(X,Y) = E(XY) - E(X)E(Y)$ mide tendencia conjunta; la **correlación** $\rho = \frac{\text{Cov}}{\sigma_X \sigma_Y} \in [-1,1]$ es adimensional y mide vínculos **lineales**.
- **Vector bidimensional continuo:** todo lo discreto pasa a densidad conjunta $f_{X,Y}$ e integrales. Atención a los límites de integración al calcular marginales y probabilidades de regiones.
- **Mezclas:** $F_X$, $f_X$, $E(X)$ y $E(X^2)$ son combinaciones lineales de los escenarios de una partición; $V(X)$ y $\sigma(X)$ **no**.
- **Esperanza y varianza condicional:** $E(Y) = E(E(Y \mid X))$ (ley de esperanza total) y $V(Y) = E(V(Y \mid X)) + V(E(Y \mid X))$ (ley de varianza total) simplifican enormemente los cálculos cuando la distribución condicional es conocida.
