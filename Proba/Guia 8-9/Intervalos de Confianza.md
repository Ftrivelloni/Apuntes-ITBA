# Intervalos de Confianza

## Motivación — Estimación por intervalos

Hasta ahora hemos visto métodos de **estimación puntual**: métodos que tratan de representar el parámetro deseado con un único valor. Por lo tanto, es muy difícil acertar al valor que generalmente se mueve en un rango continuo.

En esta línea, quizás es más informativo y certero establecer un **rango de valores** para el parámetro que se desea estimar. Nuevamente, es importante que la forma de calcular ese rango sea determinada **antes de tomar la muestra**.

Además, sería deseable que ese rango sea lo más estrecho posible, ya que daría una idea más precisa de cuál es el valor que deseamos estimar. Por ejemplo, si deseamos estimar una proporción y decimos que su valor está entre 0 y 1, estamos en lo cierto, pero no estamos siendo informativos.

A su vez, si el rango es demasiado estrecho, corremos el riesgo de no incluir el valor que se quiere estimar. Por lo tanto, el rango de valores debe cumplir el balance de ser lo más estrecho posible sin disminuir las chances de incluir al parámetro poblacional.

Como conclusión, para estimar un parámetro $\theta$, queremos encontrar dos valores $a(X_1, \dots, X_n)$ y $b(X_1, \dots, X_n)$ conocidos antes de tomar la muestra de forma que contengan al parámetro con una alta probabilidad $\gamma$:

$$P(a(X_1, \dots, X_n) \leq \theta \leq b(X_1, \dots, X_n)) = \gamma$$

---

## Construcción del intervalo (desvío conocido)

Supongamos que conocemos el desvío histórico poblacional $\sigma$ y que las variables tienen distribución normal. Por lo tanto, la media muestral sigue la siguiente distribución:

$$\bar{X}_n \sim \mathcal{N}\!\left(\mu,\, \frac{\sigma}{\sqrt{n}}\right)$$

El problema para utilizar esta distribución es que no es conocida porque $\mu$ no es conocido. Sin embargo, estandarizando, podemos obtener una distribución **normal estándar** conocida:

$$\frac{\bar{X}_n - \mu}{\sigma/\sqrt{n}} \sim \mathcal{N}(0, 1)$$

La clave para generar este rango de valores es vincular el parámetro con una distribución conocida que llamamos **"pivote"**.

### Utilización del pivote

Como sabemos que $\dfrac{\bar{X}_n - \mu}{\sigma/\sqrt{n}}$ tiene distribución normal estándar, podemos encontrar un rango de valores. Tomemos $\gamma = 0.95$:

$$P\!\left(-z_{0.975} \leq \frac{\bar{X}_n - \mu}{\sigma/\sqrt{n}} \leq z_{0.975}\right) = 0.95$$

Despejando $\mu$:

$$P\!\left(\bar{X}_n - z_{0.975} \cdot \frac{\sigma}{\sqrt{n}} \leq \mu \leq \bar{X}_n + z_{0.975} \cdot \frac{\sigma}{\sqrt{n}}\right) = 0.95$$

---

## Intervalo de Confianza para la media (desvío conocido)

A este rango de valores para $\mu$ lo llamamos **Intervalo de Confianza**. Se determina antes de tomar la muestra y llamamos **nivel de confianza** a la probabilidad $\gamma$ que se determina para que el intervalo encierre el parámetro poblacional.

Para el caso donde asumimos que las variables son normales y el desvío poblacional es conocido:

$$\boxed{IC_\gamma(\mu) = \left[\bar{X}_n - z_{\frac{1+\gamma}{2}} \cdot \frac{\sigma}{\sqrt{n}}\;;\;\bar{X}_n + z_{\frac{1+\gamma}{2}} \cdot \frac{\sigma}{\sqrt{n}}\right]}$$

> **Nota:** El área acumulada por los cuantiles es $\dfrac{1-\gamma}{2} + \gamma = \dfrac{1+\gamma}{2}$.

**Ejemplo post-muestra:** $x_{obs} = 44.966$, $\sigma = 10$, $n = 100$

$$IC_{95\%}(\mu) = \left[44.966 - 1.96 \cdot \frac{10}{\sqrt{100}}\;;\;44.966 + 1.96 \cdot \frac{10}{\sqrt{100}}\right] = [43.006,\; 46.926]$$

---

## Interpretación correcta

> [!warning] Error común
> Es un error común interpretar: *"La media poblacional tiene una probabilidad del 95% de estar entre 43.006 y 46.926".*
> 
> Esta afirmación no tiene sentido, porque después de la muestra el intervalo es fijo, al igual que el parámetro poblacional. Es decir, el parámetro **está o no está** en el intervalo — no es una cuestión probabilística.

La interpretación correcta es:

> *"Si se repite el experimento varias veces, el **95% de los intervalos** construidos de esta manera incluirán al parámetro poblacional."*

Por eso el resultado final no es un intervalo de probabilidad, es un **intervalo de confianza**, ya que sería infrecuente que el intervalo obtenido no contenga el parámetro deseado.

---

## Efecto del nivel de confianza

Al aumentar el nivel de confianza, hay más chances de que el intervalo contenga al parámetro, pero a costa de que el intervalo sea **más ancho** y por lo tanto, menos informativo.

Con $x_{obs} = 44.966$, $\sigma = 10$, $n = 100$:

| Nivel $\gamma$ | Cuantil $z$ | Intervalo |
|:-:|:-:|:-:|
| 90% | 1.6449 | $[43.3211,\; 46.6109]$ |
| 95% | 1.96 | $[43.006,\; 46.926]$ |
| 99% | 2.5758 | $[42.3902,\; 47.5418]$ |

---

## Efecto del tamaño muestral

Al aumentar el tamaño muestral con el mismo nivel de confianza, los intervalos se vuelven más **angostos**, ya que disminuye el desvío del promedio.

Con $x_{obs} = 44.966$, $\sigma = 10$, $\gamma = 95\%$:

| $n$ | Intervalo |
|:-:|:-:|
| 100 | $[43.006,\; 46.926]$ |
| 400 | $[43.986,\; 45.946]$ |
| 900 | $[44.3127,\; 45.6193]$ |

---

## Intervalos asimétricos

En los casos anteriores, para construir el intervalo de nivel $\gamma = 0.95$, elegimos los cuantiles que dejan la misma área a izquierda y derecha, por eso se considera $\dfrac{1+\gamma}{2} = 0.975$.

Sin embargo, esta elección se suele hacer por simplicidad y además, resulta en **intervalos más cortos**. De todos modos, podemos distribuir estas áreas de otra manera.

Por ejemplo, con área $0.01$ a la izquierda y $0.04$ a la derecha:

- Longitud intervalo simétrico: $3.9199$
- Longitud intervalo asimétrico: $4.077$

---

## Intervalos unilaterales

A veces puede ser que el valor máximo o mínimo del parámetro sea más importante que el otro extremo. Es decir, se sacrifica precisión de un lado para mejorar la del otro.

Para una **cota inferior** para $\mu$: $P(a \leq \mu) = 0.95$

Usando el pivote $\dfrac{\bar{X}_n - \mu}{\sigma/\sqrt{n}} \sim \mathcal{N}(0,1)$:

$$\frac{\bar{X}_n - a}{\sigma/\sqrt{n}} = z_{0.95} \implies a = \bar{X}_n - z_{0.95} \cdot \frac{\sigma}{\sqrt{n}}$$

### Intervalo unilateral a izquierda

$$IC_\gamma(\mu) = \left[\bar{X}_n - z_\gamma \cdot \frac{\sigma}{\sqrt{n}}\;,\; +\infty\right)$$

**Post-muestra:** $x_{obs} = 44.966$, $n = 100$, $\sigma = 10$

$$IC_{95\%}(\mu) = \left[44.966 - 1.6449 \cdot \frac{10}{\sqrt{100}}\;,\; +\infty\right) = [44.8015,\; +\infty]$$

Asumiendo un puntaje máximo de 100: $IC_{95\%}(\mu) = [44.8015,\; 100]$

### Intervalo unilateral a derecha

$$IC_\gamma(\mu) = \left(-\infty\;,\; \bar{X}_n + z_\gamma \cdot \frac{\sigma}{\sqrt{n}}\right]$$

**Post-muestra:**

$$IC_{95\%}(\mu) = \left(-\infty,\; 44.966 + 1.6449 \cdot \frac{10}{\sqrt{100}}\right] = (-\infty,\; 45.1305]$$

Asumiendo un puntaje mínimo de 0: $IC_{95\%}(\mu) = [0,\; 45.1305]$

---

## Intervalos para proporciones

Si $n$ es suficientemente grande, podemos usar el TCL para saber la distribución de la proporción muestral:

$$\hat{p} \sim \mathcal{N}\!\left(p,\, \frac{p(1-p)}{n}\right) \implies \frac{\hat{p} - p}{\sqrt{p(1-p)/n}} \sim \mathcal{N}(0,1)$$

Resolviendo para $p$ y reemplazando $p \approx \hat{p}$ (Ley de los Grandes Números):

### Intervalo bilateral

$$\boxed{IC_\gamma(p) = \left[\hat{p} - z_{\frac{1+\gamma}{2}} \cdot \sqrt{\frac{\hat{p}(1-\hat{p})}{n}}\;;\;\hat{p} + z_{\frac{1+\gamma}{2}} \cdot \sqrt{\frac{\hat{p}(1-\hat{p})}{n}}\right]}$$

**Post-muestra:** $\hat{p}_{obs} = 0.7$, $n = 100$, $\gamma = 95\%$

$$IC_{95\%}(p) = \left[0.7 - 1.96\sqrt{\frac{0.7 \cdot 0.3}{100}}\;;\;0.7 + 1.96\sqrt{\frac{0.7 \cdot 0.3}{100}}\right] = [0.6102,\; 0.7898]$$

### Intervalo unilateral a izquierda

$$IC_\gamma(p) = \left[\hat{p} - z_\gamma \cdot \sqrt{\frac{\hat{p}(1-\hat{p})}{n}}\;,\; 1\right]$$

**Post-muestra:** $IC_{95\%}(p) = [0.6246,\; 1]$

### Intervalo unilateral a derecha

$$IC_\gamma(p) = \left[0\;,\; \hat{p} + z_\gamma \cdot \sqrt{\frac{\hat{p}(1-\hat{p})}{n}}\right]$$

**Post-muestra:** $IC_{95\%}(p) = [0,\; 0.7754]$

---

## Desvío desconocido

### Problema

Cuando el desvío $\sigma$ es desconocido, intuitivamente uno querría reemplazarlo por el desvío muestral $s$ y usar el pivote:

$$T = \frac{\bar{X}_n - \mu}{s/\sqrt{n}}$$

El problema es que el desvío es una **variable aleatoria** — para distintas muestras da distintos valores. Por lo tanto, este cociente ya no resulta en una distribución normal.

### Distribución $t$ de Student

En el caso en que las variables originales $X_i$ sean normales, este cociente tiene una distribución conocida llamada **$t$ de Student**, con un único parámetro natural llamado **"grados de libertad"**:

$$\boxed{T = \frac{\bar{X}_n - \mu}{s/\sqrt{n}} \sim t_{n-1}}$$

La distribución $t$ de Student es similar a una distribución normal estándar, aunque tiene un poco más de desvío porque contabiliza los distintos valores que puede tomar el desvío muestral $s$. A medida que aumentan los grados de libertad, la similitud es más notoria.

### Intervalo de confianza (desvío desconocido)

Asumiendo $\gamma$ como nivel de confianza:

$$P\!\left(-t_{n-1;\,\frac{1+\gamma}{2}} \leq \frac{\bar{X}_n - \mu}{s/\sqrt{n}} \leq t_{n-1;\,\frac{1+\gamma}{2}}\right) = \gamma$$

$$\boxed{IC_\gamma(\mu) = \left[\bar{X}_n - t_{n-1;\,\frac{1+\gamma}{2}} \cdot \frac{s}{\sqrt{n}}\;;\;\bar{X}_n + t_{n-1;\,\frac{1+\gamma}{2}} \cdot \frac{s}{\sqrt{n}}\right]}$$

**Post-muestra:** $x_{obs} = 44.966$, $s_{obs} = 10.5634$, $n = 10$

$$t_{9;\, 0.975} = 2.2622$$

$$IC_{95\%}(\mu) = \left[44.966 - 2.2622 \cdot \frac{10.5634}{\sqrt{10}}\;;\;44.966 + 2.2622 \cdot \frac{10.5634}{\sqrt{10}}\right] = [37.4092,\; 52.5228]$$

> **Tabla de cuantiles $t$ de Student** (filas = grados de libertad $n-1$):
> 
> | $n$ | 0.8 | 0.9 | 0.95 | 0.975 | 0.99 | 0.995 |
> |:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> | 1 | 1.3764 | 3.0777 | 6.3138 | 12.7062 | 31.8205 | 63.6567 |
> | 2 | 1.0607 | 1.8856 | 2.9200 | 4.3027 | 6.9646 | 9.9248 |
> | 5 | 0.9195 | 1.4759 | 2.0150 | 2.5706 | 3.3649 | 4.0321 |
> | 9 | 0.8834 | 1.3830 | 1.8331 | 2.2622 | 2.8214 | 3.2498 |
> | 10 | 0.8791 | 1.3722 | 1.8125 | 2.2281 | 2.7638 | 3.1693 |

---

## Cobertura: $t$ de Student vs. Normal

Es importante remarcar que utilizar los cuantiles normales para construir este intervalo (cuando el desvío es desconocido) genera diferencias numéricas.

- Con **cuantiles normales** y $n=10$: cobertura $\approx 93\%$ *(inferior al nivel deseado)*
- Con **cuantiles $t$ de Student** y $n=10$: cobertura $= 95\%$ *(correcto)*

Con muestras grandes ($n = 100$), la diferencia es mínima porque:
1. Los cuantiles son similares.
2. Se divide por un tamaño muestral más grande, reduciendo las diferencias numéricamente.

> **Regla práctica:** A partir de $n > 30$ la diferencia entre estos cálculos es despreciable. Sin embargo, vale aclarar que se parte del supuesto que las variables son normales. Si no se cumple el supuesto, el tamaño muestral deberá ser más grande para poder usar el TCL.

---

## Variables no normales — Intervalo para $\sigma^2$

Si las variables $X_i$ son normales, sabemos que:

$$\frac{\sum_{i=1}^{n}(X_i - \bar{X}_n)^2}{\sigma^2} = \frac{(n-1)S^2}{\sigma^2} \sim \chi^2_{n-1}$$

Por lo tanto, podemos usar esta distribución como pivote para construir un IC para la varianza $\sigma^2$.

### Construcción del intervalo

$$P\!\left(\chi^2_{n-1,\,\frac{1-\gamma}{2}} \leq \frac{(n-1)S^2}{\sigma^2} \leq \chi^2_{n-1,\,\frac{1+\gamma}{2}}\right) = \gamma$$

$$\boxed{IC_\gamma(\sigma^2) = \left[\frac{(n-1)S^2}{\chi^2_{n-1,\,\frac{1+\gamma}{2}}}\;;\;\frac{(n-1)S^2}{\chi^2_{n-1,\,\frac{1-\gamma}{2}}}\right]}$$

**Post-muestra:** $s_{obs} = 10.5634$, $n = 10$, $\gamma = 95\%$

$$IC_{95\%}(\sigma^2) = \left[\frac{9 \cdot 10.5634^2}{19.0228}\;;\;\frac{9 \cdot 10.5634^2}{2.7004}\right] = [52.7934,\; 371.9007]$$

> [!warning] Distribución correcta
> Si hubiéramos tomado cuantiles $t$ de Student para el intervalo del desvío, la cobertura parecería perfecta (100%), pero solo porque *sobreestima* los valores — la distribución utilizada es incorrecta.
> 
> Cuando utilizamos la distribución $\chi^2$ adecuada, la cobertura es similar al nivel de confianza deseado ($\approx 94.8\%$).
> 
> Con muestras grandes, el TCL permite aproximar tanto la $\chi^2$ como la $t$ de Student por una distribución normal, y los resultados de cobertura son similares entre ambas.

---

## Identificación de escenarios

La mayoría de los casos se termina utilizando la distribución normal por el **Teorema Central del Límite**. Aún si el desvío es conocido o desconocido, si el tamaño muestral es grande, las diferencias numéricas son despreciables entre usar el desvío poblacional o el muestral.

```
                    ┌─────────────────────────────┐
                    │    Parámetro a estimar       │
                    └──────────┬──────────┬────────┘
                               │          │
                            Media      Proporción
                               │          │
                    ┌──────────┴──┐     Cuantiles
                    │             │      Normales
              Variables       Variables
              Normales        No Normales
                    │             │
             ┌──────┴──┐     n grande →
          Desvío    Desvío   Cuantiles
         Conocido  Descon.    Normales
             │         │
         Cuantiles  Cuantiles
          Normales  t Student
                         │
                    Con n grande
                    vale Normal
```

---

## Cálculo de tamaño muestral

### Margen de error

El **margen de error** $\Delta$ es la semilongitud del intervalo de confianza. Dado un nivel $\gamma$ y un margen deseado, podemos calcular el tamaño muestral necesario *antes* de tomar la muestra.

### Tamaño muestral — desvío conocido

Con $\sigma$ conocido, el margen de error del IC para la media es:

$$\Delta = z_{\frac{1+\gamma}{2}} \cdot \frac{\sigma}{\sqrt{n}}$$

Despejando $n$:

$$\Delta \leq z_{\frac{1+\gamma}{2}} \cdot \frac{\sigma}{\sqrt{n}} \implies n \geq \left(z_{\frac{1+\gamma}{2}} \cdot \frac{\sigma}{\Delta}\right)^2$$

**Ejemplo:** $\sigma = 10$, $\Delta = 0.5$, $\gamma = 95\%$

$$n \geq \left(1.96 \cdot \frac{10}{0.5}\right)^2 = 1536.58 \implies n = 1537$$

### Tamaño muestral — desvío desconocido

Cuando el desvío es desconocido, se puede usar una **primera estimación** del desvío obtenida de una muestra previa. Por la Ley de los Grandes Números, ese valor no debería estar muy lejos del desvío poblacional.

**Ejemplo:** $s_{obs} = 10.5634$ (muestra previa de $n=100$), $\Delta = 0.5$

$$n \geq \left(1.96 \cdot \frac{10.5634}{0.5}\right)^2 = 1714.62 \implies n = 1715$$

*Verificación:* con la nueva muestra $s_{obs} = 9.2945$:

$$\Delta = 1.96 \cdot \frac{9.2945}{\sqrt{1715}} = 0.4399 \leq 0.5 \checkmark$$

### Tamaño muestral — proporciones

El margen de error para una proporción es:

$$\Delta = z_{\frac{1+\gamma}{2}} \cdot \sqrt{\frac{\hat{p}(1-\hat{p})}{n}}$$

**Caso peor** (sin información previa): como $\hat{p}(1-\hat{p}) \leq \tfrac{1}{4}$ para todo $\hat{p} \in [0,1]$:

$$\Delta \leq z_{\frac{1+\gamma}{2}} \cdot \sqrt{\frac{1/4}{n}} \leq 0.01 \implies n \geq (z_{0.975})^2 \cdot \frac{1/4}{0.01^2} = 9603.65 \implies n = 9604$$

**Con estimación previa:** $\hat{p}_{obs} = 0.7$ (muestra de $n=100$):

$$n \geq (1.96)^2 \cdot \frac{0.7 \cdot 0.3}{0.01^2} = 8067.06 \implies n = 8068$$

> **Conclusión:** Contar con una primera estimación de $\hat{p}$ resulta en un ligero alivio a la hora de reclutar participantes respecto del peor caso.
