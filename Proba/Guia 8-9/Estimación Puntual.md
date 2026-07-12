# Estimación Puntual

> [!abstract] ¿De qué se trata?
> Queremos aprender sobre un **parámetro poblacional** desconocido $\theta$ (una media $\mu$, una proporción $p$, una varianza $\sigma^2$, etc.) a partir de una **muestra**. La **estimación puntual** busca representar ese parámetro con un **único valor** calculado desde la muestra.

## Parámetro poblacional vs. muestral

- **Parámetro poblacional** ($\mu$, $p$, $\sigma^2$, …): característica fija de toda la población. Si pudiéramos censar todo, obtendríamos siempre el mismo valor. Es **desconocido** pero **constante**.
- **Estadístico muestral** ($\bar{X}_n$, $\hat{p}$, $S^2$, …): se calcula desde la muestra. **Antes** de tomar la muestra es una **variable aleatoria** (lo aleatorio es qué elementos entran en la muestra); **después** de tomarla es un valor fijo y conocido.

---

## Estimadores

Un **estimador** $\hat{\theta}(X_1, \dots, X_n)$ es una función de la muestra que busca aproximar el parámetro poblacional desconocido $\theta$. Por ejemplo, $\hat{\theta} = \bar{X}_n$ para estimar $\theta = \mu$.

> [!info] La idea clave
> Como el estimador se calcula a partir de la muestra, **antes** de tomarla es una **variable aleatoria**. Por eso podemos estudiar su **distribución**, su valor esperado y su desvío, y usar eso para juzgar qué tan bueno es. El estimador debe fijarse **antes** de tomar la muestra.

**Vínculo con el TCL.** Si las $X_i$ son i.i.d. con media $\mu$ y desvío $\sigma$, por el Teorema Central del Límite el estimador $\bar{X}_n$ es (aproximadamente) normal:

$$\bar{X}_n \sim \mathcal{N}\!\left(\mu,\; \frac{\sigma}{\sqrt{n}}\right)$$

Esto explica por qué al simular muchos promedios muestrales su histograma se ve acampanado y centrado en $\mu$.

---

## Propiedades deseables de un estimador

### Sesgo

El **sesgo** mide si la distribución del estimador está **centrada** en el parámetro que busca estimar:

$$\boxed{B(\hat{\theta}) = E(\hat{\theta} - \theta) = E(\hat{\theta}) - \theta}$$

- Un estimador es **insesgado** si $B(\hat{\theta}) = 0 \iff E(\hat{\theta}) = \theta$.
- Es **asintóticamente insesgado** si el sesgo tiende a $0$ cuando $n \to \infty$.

> [!info] ¿Por qué importa?
> Un estimador insesgado "acierta en promedio": si repitiéramos el muestreo muchas veces, el promedio de las estimaciones daría el valor real. Ejemplos: $\bar{X}_n$ es insesgado para $\mu$ (ya que $E(\bar{X}_n) = \mu$) y $\hat{p} = \tfrac{X_n}{n}$ es insesgado para $p$.

### Precisión (varianza)

El sesgo no alcanza: un estimador insesgado pero con **mucha varianza** es poco confiable (sus valores se dispersan mucho). Al aumentar el tamaño muestral $n$, la varianza de $\bar{X}_n$ baja ($\tfrac{\sigma^2}{n}$), logrando una estimación más precisa.

> [!tip] Criterio de elección
> Ante **dos estimadores insesgados**, conviene elegir el de **menor varianza**.

### Error cuadrático medio (ECM)

Combina sesgo y varianza en una sola medida (balance entre ambos):

$$\boxed{ECM(\hat{\theta}) = E\big((\hat{\theta} - \theta)^2\big) = V(\hat{\theta}) + B^2(\hat{\theta})}$$

> [!info] ¿Cuándo usarlo?
> Sirve para **comparar estimadores** aunque uno sea sesgado: a veces un estimador con un poco de sesgo pero **mucha menos varianza** tiene menor ECM que uno insesgado y muy disperso. Para un estimador insesgado, $ECM = V(\hat{\theta})$.

---

## Caso de la varianza: por qué $n-1$

Para estimar la varianza poblacional $\sigma^2$ se usa la **varianza muestral**:

$$S^2 = \frac{\sum_{i=1}^{n}(X_i - \bar{X}_n)^2}{n-1}$$

Si $X_i \sim \mathcal{N}(\mu,\sigma)$, se cumple $E(S^2) = \sigma^2$, es decir **$S^2$ es insesgado** para $\sigma^2$. Esto se apoya en que $\dfrac{(n-1)S^2}{\sigma^2} \sim \chi^2_{n-1}$.

> [!warning] Dividir por $n$ da un estimador sesgado
> Si se usa el promedio de las diferencias al cuadrado (dividiendo por $n$ en lugar de $n-1$):
> $$\hat{\sigma}^2 = \frac{\sum_{i=1}^n (X_i-\bar{X}_n)^2}{n} \implies E(\hat{\sigma}^2) = \sigma^2 \cdot \frac{n-1}{n} \xrightarrow[n\to\infty]{} \sigma^2$$
> Es **sesgado** (subestima $\sigma^2$), pero **asintóticamente insesgado**. Por eso el $n-1$ de $S^2$: corrige justamente ese sesgo.

---

## Métodos para construir estimadores

Cuando no es obvio qué estimador usar, hay dos estrategias sistemáticas.

### Método de los momentos

El **$k$-ésimo momento** de una variable es $E(X^k)$. Por la Ley de los Grandes Números, con una muestra i.i.d. grande el promedio de las potencias se parece al momento:

$$\frac{1}{n}\sum_{i=1}^{n} X_i^k \approx E(X^k)$$

Si el momento depende del parámetro, $E(X^k) = g(\theta)$, se **iguala el momento muestral al teórico y se despeja** $\theta$:

$$\boxed{\hat{\theta}_M = g^{-1}\!\left(\frac{1}{n}\sum_{i=1}^{n} X_i^k\right)}$$

> [!example] Ejemplo — Geométrica
> Si $X_i \sim \mathcal{G}e(p)$, entonces $E(X_i) = \tfrac{1}{p}$. Igualando al primer momento muestral:
> $$\bar{X}_n \approx \frac{1}{p} \implies \boxed{\hat{p}_M = \frac{n}{\sum_{i=1}^n X_i}}$$

> [!tip] Detalles prácticos
> - Se empieza por el **primer momento**; si $E(X)$ **no** depende de $\theta$, se pasa al segundo momento (o superior) hasta lograr una relación con $\theta$.
> - Para estimar **$k$ parámetros** se necesitan **$k$ momentos** (armar un sistema).
> - Requiere que las variables sean **i.i.d.**

### Método de máxima verosimilitud (MV)

Elige el valor del parámetro que hace **más coherentes** (más probables) los datos observados. La **función de verosimilitud** $L(\theta)$ es la distribución conjunta de la muestra vista como función de $\theta$:

$$\boxed{\hat{\theta}_{MV} = \arg\max_{\theta} L(\theta)}$$

$$L(\theta) = \begin{cases} p(X_1, \dots, X_n;\, \theta) = \prod_{i=1}^n p(X_i;\theta) & \text{(caso discreto)} \\[4pt] f(X_1, \dots, X_n;\, \theta) = \prod_{i=1}^n f(X_i;\theta) & \text{(caso continuo)} \end{cases}$$

(la factorización del producto vale si las $X_i$ son **independientes**).

> [!tip] Truco: maximizar el logaritmo
> Como $L(\theta)$ suele ser un **producto**, derivar es incómodo. Como el logaritmo es **creciente**, $L(\theta)$ y $\ln L(\theta)$ se maximizan en el **mismo** $\theta$. Se deriva $\ln L(\theta)$, se iguala a $0$ y se despeja (convierte productos en sumas).

> [!example] Ejemplo discreto — Geométrica
> $L(p) = \prod (1-p)^{X_i-1} p = (1-p)^{\sum X_i - n} p^n$. Maximizando $\ln L(p)$:
> $$\hat{p}_{MV} = \frac{n}{\sum_{i=1}^n X_i}$$
> Coincide con el de momentos (no siempre pasa).

> [!example] Ejemplo continuo — Pareto
> Con densidad $f(x;\alpha) = \frac{\alpha \cdot 10^\alpha}{x^{\alpha+1}}$ para $x > 10$: se maximiza la **densidad conjunta**. Como $\ln L(\alpha) = n\ln\alpha + n\alpha\ln 10 - (\alpha+1)\sum \ln X_i$, derivando:
> $$\hat{\alpha}_{MV} = \frac{n}{\sum_{i=1}^n \ln\!\left(\frac{X_i}{10}\right)}$$
> Nota: en el caso continuo se maximiza la **densidad** (la probabilidad puntual es $0$). El soporte importa: si algún $X_i \le 10$ la densidad se anula, así que se exige $\min\{X_i\} > 10$.

---

## ¿Qué método conviene?

> [!tip] Momentos vs. Máxima Verosimilitud
> - **Momentos:** rápido y sencillo, pero **requiere variables i.i.d.** y que algún momento dependa del parámetro. Puede dar fórmulas con restricciones de validez (p. ej. $E(X)$ de una Pareto sólo vale si $\alpha > 1$).
> - **Máxima verosimilitud:** mucho más **versátil** — sólo necesita la distribución conjunta (las variables pueden estar correlacionadas o tener distintas distribuciones). Su contra: la derivada de $L$ no siempre es sencilla.
> - **No siempre coinciden** los estimadores; a veces uno de los métodos no se puede aplicar o es inconveniente, y se usa el otro.

---

## Resumen

- **Parámetro poblacional** $\theta$: fijo y desconocido. **Estimador** $\hat{\theta}(X_1,\dots,X_n)$: variable aleatoria antes de muestrear; se juzga por su distribución. Debe fijarse **antes** de tomar la muestra.
- **Sesgo:** $B(\hat{\theta}) = E(\hat{\theta}) - \theta$. Insesgado si $E(\hat{\theta}) = \theta$; asintóticamente insesgado si $B \to 0$.
- **Varianza:** entre insesgados, elegir el de menor varianza. Más $n$ ⟹ menos varianza.
- **ECM** $= V(\hat{\theta}) + B^2(\hat{\theta})$: balance sesgo–varianza para comparar estimadores.
- $S^2$ (con $n-1$) es **insesgado** para $\sigma^2$; dividir por $n$ da un estimador sesgado pero asintóticamente insesgado.
- **Método de los momentos:** igualar momentos muestrales a teóricos y despejar (requiere i.i.d.).
- **Máxima verosimilitud:** maximizar $L(\theta)$ (probabilidad/densidad conjunta), usando $\ln L$ para simplificar. Más versátil.

| Estimador | Estima | Propiedad |
|:--|:--|:--|
| $\bar{X}_n$ | $\mu$ | insesgado; $\sim \mathcal{N}(\mu, \sigma/\sqrt{n})$ por TCL |
| $\hat{p} = \tfrac{X_n}{n}$ | $p$ | insesgado |
| $S^2 = \tfrac{\sum(X_i-\bar{X}_n)^2}{n-1}$ | $\sigma^2$ | insesgado |
| $\hat{\theta}_M$ (momentos) | $\theta$ | requiere i.i.d. |
| $\hat{\theta}_{MV}$ (verosimilitud) | $\theta$ | versátil; maximiza $L(\theta)$ |

> [!note] Sigue en...
> Una vez elegido un estimador puntual, el paso siguiente es dar un **rango** de valores plausibles: ver [[Intervalos de Confianza]]. Para contrastar hipótesis sobre el parámetro: ver [[Tests de Hipótesis]].
