# Suma de Variables Aleatorias y Teorema Central del Límite

## Motivación — El salón de eventos

A lo largo de esta guía seguimos a **Martín**, que organiza los eventos de un salón de fiestas. Cada fin de semana tiene dos eventos (viernes y sábado a la noche) y necesita anticipar cantidades: comida, bebida, cancelaciones, demoras, basura, música, etc.

Muchas de estas cantidades se modelan como **sumas de variables aleatorias independientes**. La pregunta central es: si conozco la distribución de cada sumando, ¿qué distribución tiene la suma? En algunos casos la suma conserva una estructura conocida; en otros, no hay fórmula cerrada y conviene aproximar.

---

## Suma de variables — el método general

Para sumar dos variables independientes $X$ e $Y$ y obtener la distribución de $Z = X + Y$, se usa **probabilidad total** condicionando sobre uno de los sumandos y aprovechando la independencia:

$$P(Z = k) = \sum_i P(Y = k - i)\cdot P(X = i) \qquad \text{(caso discreto)}$$

$$f_Z(z) = \int f_Y(z - x)\, f_X(x)\, dx \qquad \text{(caso continuo)}$$

Esta operación se llama **convolución**. Para variables continuas suele ser más cómodo arrancar por la función de distribución $F_Z(z) = P(X + Y \leq z)$ y luego derivar para obtener la densidad.

### Ejemplos del salón (deducciones por convolución)

| Variable | Sumandos independientes | Distribución de la suma |
|:--|:--|:--|
| Cancelaciones $S_C = C_1 + C_2$ | $C_i \sim \text{Bi}(100,\, 0.05)$ | $S_C \sim \text{Bi}(200,\, 0.05)$ |
| Vinos $S_V = V_1 + V_2$ | $V_1 \sim \mathcal{P}o(30),\ V_2 \sim \mathcal{P}o(40)$ | $S_V \sim \mathcal{P}o(70)$ |
| TV apagada $S_T = T_1 + T_2$ | $T_i \sim \mathcal{G}e\!\left(\tfrac{1}{40}\right)$ | $S_T \sim \mathcal{NB}\!\left(2,\, \tfrac{1}{40}\right)$ |
| Demoras $S_D = D_1 + D_2$ | $D_i \sim \mathcal{E}\!\left(\tfrac{1}{5}\right)$ | $S_D \sim \Gamma\!\left(2,\, \tfrac{1}{5}\right)$ |

En cada caso se llega a la distribución de la suma resolviendo la convolución; el resultado es otra distribución conocida.

---

## Reglas de cierre por familia

Cuando los sumandos son independientes y comparten el parámetro adecuado, la suma queda **en la misma familia** (o en su generalización natural). Estas reglas evitan rehacer la convolución cada vez.

| Familia | Condición | Suma $Z = X + Y$ |
|:--|:--|:--|
| Binomial | $X \sim \text{Bi}(n,p),\ Y \sim \text{Bi}(m,p)$ — **mismo** $p$ | $\text{Bi}(n+m,\, p)$ |
| Poisson | $X \sim \mathcal{P}o(\lambda_1),\ Y \sim \mathcal{P}o(\lambda_2)$ | $\mathcal{P}o(\lambda_1 + \lambda_2)$ |
| Geométrica | $X, Y \sim \mathcal{G}e(p)$ — **mismo** $p$ | $\mathcal{NB}(2,\, p)$ |
| Binomial negativa | $X \sim \mathcal{NB}(n,p),\ Y \sim \mathcal{NB}(m,p)$ — **mismo** $p$ | $\mathcal{NB}(n+m,\, p)$ |
| Exponencial | $X, Y \sim \mathcal{E}(\lambda)$ — **mismo** $\lambda$ | $\Gamma(2,\, \lambda)$ |
| Gamma | $X \sim \Gamma(\alpha_1,\lambda),\ Y \sim \Gamma(\alpha_2,\lambda)$ — **mismo** $\lambda$ | $\Gamma(\alpha_1 + \alpha_2,\, \lambda)$ |
| Normal | $X \sim \mathcal{N}(\mu_1,\sigma_1),\ Y \sim \mathcal{N}(\mu_2,\sigma_2)$ | $\mathcal{N}\!\left(\mu_1+\mu_2,\, \sqrt{\sigma_1^2 + \sigma_2^2}\right)$ |

> [!warning] El parámetro común es clave
> Las familias **Binomial**, **Geométrica/Binomial negativa**, **Exponencial** y **Gamma** sólo cierran si el parámetro de "éxito" o de "tasa" es el **mismo** en todos los sumandos. Si $p_1 \neq p_2$ (o $\lambda_1 \neq \lambda_2$), la suma ya **no** pertenece a la familia.
> En cambio, la **Poisson** cierra siempre (los $\lambda$ pueden diferir) y la **Normal** cierra siempre (basta sumar medias y varianzas).

**Esperanza y varianza** (siempre aditivas para independientes):

$$E(X + Y) = E(X) + E(Y) \qquad V(X + Y) \overset{\text{Ind}}{=} V(X) + V(Y)$$

La interpretación combinatoria ayuda: sumar dos binomiales con el mismo $p$ es contar éxitos en $n+m$ experimentos; sumar dos geométricas es contar fracasos hasta el **segundo** éxito; sumar dos gammas con la misma tasa acumula los tiempos de espera.

---

## Desigualdades y Ley de los Grandes Números

### Desigualdad de Markov

Sea $X$ una variable **no negativa** ($P(X < 0) = 0$) con $E(X) < +\infty$. Para todo $\varepsilon > 0$:

$$\boxed{P(X \geq \varepsilon) \leq \frac{E(X)}{\varepsilon}}$$

No hace **ninguna asunción sobre la distribución**: sólo pide no negatividad. Refleja que es difícil que una variable tome valores excesivamente altos respecto de su media.

**Ejemplo (basura):** la basura $B$ por fin de semana no sigue ninguna distribución conocida, pero $E(B) = 100$ kg. El camión lleva hasta 200 kg:

$$P(B \geq 200) \leq \frac{E(B)}{200} = \frac{100}{200} = \frac{1}{2}$$

A lo sumo, la mitad de las veces el camión no podrá llevar toda la basura.

### Desigualdad de Čebyšëv

Aplicando Markov a $Y = (X - E(X))^2$ se obtiene una cota sobre el alejamiento respecto de la media. Para todo $\varepsilon > 0$:

$$\boxed{P\big(|X - E(X)| \geq \varepsilon\big) \leq \frac{V(X)}{\varepsilon^2}}$$

Enfatiza que es improbable que una variable se aleje demasiado de su valor esperado, y de nuevo **no asume la distribución**.

**Ejemplo (música):** la cantidad de canciones $M$ tiene $E(M) = 150$ y $V(M) = 500$. Martín quiere quedarse entre 100 y 200 canciones:

$$P(100 \leq M \leq 200) = 1 - P(|M - 150| \geq 51) \geq 1 - \frac{500}{51^2} = 0.8078$$

> **Nota — las cotas son del peor caso.** Como no usan la distribución, Markov y Čebyšëv suelen coincidir con el peor escenario. Si **sí** se conoce la distribución, la probabilidad real está lejos de la cota. Por ejemplo, si $M \sim \mathcal{N}(150, 500)$ entonces $P(100 \leq M \leq 200) \approx 0.9747$, muy por encima del $0.8078$ garantizado.

---

## Variables i.i.d.: suma y promedio

Una colección **V.A.I.I.D.** (Variables Aleatorias Independientes Idénticamente Distribuidas) son variables independientes con la misma distribución, por lo tanto con la misma media $E(X_i) = \mu$ y el mismo desvío $\sigma(X_i) = \sigma$.

Sean $X_1, \dots, X_n$ V.A.I.I.D. Para la **suma** $S_n = \sum_{i=1}^n X_i$ y el **promedio** $\overline{X}_n = \frac{S_n}{n}$:

| | Suma $S_n$ | Promedio $\overline{X}_n$ |
|:--|:-:|:-:|
| Media | $n\mu$ | $\mu$ |
| Varianza | $n\sigma^2$ | $\dfrac{\sigma^2}{n}$ |
| Desvío | $\sqrt{n}\,\sigma$ | $\dfrac{\sigma}{\sqrt{n}}$ |

**Pregunta clave:** ¿qué le pasa al promedio cuando $n \to +\infty$?

El promedio **siempre está centrado en $\mu$**, pero su desvío $\frac{\sigma}{\sqrt{n}} \to 0$. Es decir, $\overline{X}_n$ se concentra cada vez más alrededor de $\mu$ hasta parecer una constante. Esto se verifica simulando $M = 200$ promedios de tamaños crecientes ($n = 10, 30, 60, 100$) para distintas distribuciones (Normal, Binomial, Poisson, Exponencial): en todos los casos los histogramas se angostan alrededor de la media.

### Ley de los Grandes Números (LGN)

La concentración se demuestra con Čebyšëv aplicada al promedio:

$$P\big(|\overline{X}_n - \mu| \geq \varepsilon\big) \leq \frac{V(\overline{X}_n)}{\varepsilon^2} = \frac{\sigma^2}{n\,\varepsilon^2} \xrightarrow[n \to +\infty]{} 0$$

Esto da lugar a la **Ley de los Grandes Números**: sean $X_1, \dots, X_n$ V.A.I.I.D. de media $\mu$ y desvío finito $\sigma$; para todo $\varepsilon > 0$,

$$\boxed{P\big(|\overline{X}_n - \mu| \geq \varepsilon\big) \xrightarrow[n \to +\infty]{} 0}$$

Se dice que $\overline{X}_n$ **converge en probabilidad** a $\mu$.

### LGN y frecuencias relativas

La LGN justifica por qué la **frecuencia relativa** de un evento se parece a su probabilidad. Si $A$ es un evento con probabilidad $P(A)$ y definimos $X_i = 1$ cuando $A$ ocurre en la repetición $i$ (y $0$ si no), las $X_i$ son i.i.d. con $E(X_i) = P(A)$. El promedio $\overline{X}_n$ es exactamente la frecuencia relativa de $A$, y por la LGN converge a $P(A)$. Por eso, con muchas repeticiones, la frecuencia observada se aproxima a la probabilidad real.

---

## Teorema Central del Límite (TCL)

La LGN dice **dónde** se concentra el promedio, pero no **cómo** se distribuye alrededor de la media. El TCL responde eso: el promedio (o la suma) de muchas i.i.d. es **aproximadamente normal**, sin importar la distribución original.

Sean $X_1, \dots, X_n$ V.A.I.I.D. de **cualquier** distribución con media $\mu$ y desvío finito $\sigma$. A medida que $n \to \infty$:

$$\boxed{\overline{X}_n \overset{(aprox)}{\sim} \mathcal{N}\!\left(\mu,\, \frac{\sigma}{\sqrt{n}}\right) \implies \frac{\overline{X}_n - \mu}{\sigma/\sqrt{n}} \overset{(aprox)}{\sim} \mathcal{N}(0,1)}$$

$$\boxed{S_n \overset{(aprox)}{\sim} \mathcal{N}\!\left(n\mu,\, \sqrt{n}\,\sigma\right) \implies \frac{S_n - n\mu}{\sqrt{n}\,\sigma} \overset{(aprox)}{\sim} \mathcal{N}(0,1)}$$

En términos de la acumulada, para cualquier $t \in \mathbb{R}$:

$$F_{S_n}(t) = P(S_n \leq t) \underset{n \to +\infty}{\overset{TCL}{\approx}} \Phi\!\left(\frac{t - n\mu}{\sqrt{n}\,\sigma}\right)$$

> **Observaciones**
> - El TCL dice **más** que la LGN: permite calcular probabilidades de que el promedio (o la suma) caiga en un rango, no sólo que se concentra.
> - Vale para **CUALQUIER DISTRIBUCIÓN** (con desvío finito).
> - Regla práctica: $n \geq 50$ (a veces se pide $n \geq 100$), dependiendo de la asimetría de la variable original. Cuanto más asimétrica, más grande debe ser $n$.

### Aplicación — Demoras (variable continua)

Las demoras $D_i \sim \mathcal{E}\!\left(\tfrac{1}{5}\right)$ tienen $E(D_i) = 5$ y $\sigma(D_i) = 5$. En los $104$ eventos del año, $S_{104} = \sum_{i=1}^{104} D_i$. Aunque sabemos que $S_{104} \sim \Gamma\!\left(104, \tfrac{1}{5}\right)$, sus probabilidades son difíciles de calcular a mano. Para $P(S_{104} > 420)$ (más de 7 horas de demora acumulada):

$$P(S_{104} > 420) \overset{TCL}{\approx} P\!\left(Z > \frac{420 - 520}{\sqrt{104}\cdot 5}\right) = \Phi(1.9612) = 0.9751$$

El valor exacto de la gamma es $0.9808$: la aproximación es muy buena.

### Aplicación — Cancelaciones (variable discreta)

Con $C_i \sim \text{Bi}(100, 0.05)$ y $S_{104} = \sum C_i$, por TCL:

$$S_{104} \overset{(a)}{\sim} \mathcal{N}\!\left(104 \cdot 100 \cdot 0.05,\ \sqrt{104 \cdot 100 \cdot 0.05 \cdot 0.95}\right) = \mathcal{N}(520,\, \sqrt{494})$$

$$P(S_{104} \leq 490) \overset{TCL}{\approx} 1 - \Phi\!\left(\frac{30}{\sqrt{494}}\right) = 1 - \Phi(1.3498) = 0.0885$$

---

## Corrección por continuidad

Al aproximar una variable **discreta** por una **normal** (continua), hay un desajuste: la discreta tiene "vacíos" de probabilidad nula entre valores enteros que la normal no tiene. La **corrección por continuidad** toma el punto **intermedio** de ese vacío.

En el ejemplo, $P(S_{104} \leq 490)$ coincide con $P(S_{104} \leq t)$ para todo $t \in (490, 491)$, así que se evalúa la normal en el punto medio $490.5$:

$$P(S_{104} \leq 490) = P(S_{104} \leq 490.5) \overset{TCL}{\approx} \Phi\!\left(\frac{490.5 - 520}{\sqrt{494}}\right) = 0.0922$$

Esto mejora la aproximación (el valor real es $\approx 0.0913$). Integrar hasta $490.5$ da mejor resultado que hasta $490$ ó $490.9$.

> [!warning] ¿Sumar o restar 0.5?
> No memorizar una fórmula: **razonar qué valores del recorrido quedan incluidos** antes y después de la corrección. La corrección es válida cuando el conjunto de enteros incluidos no cambia.
>
> Recordando que el recorrido es entero:
> - $P(S \geq 510)$ incluye $\{510, 511, \dots\}$ → corregir a $P(S \geq 509.5)$.
> - $P(S > 510)$ incluye $\{511, 512, \dots\}$ → corregir a $P(S \geq 510.5)$.
> - $P(S \leq 510)$ incluye $\{\dots, 510\}$ → corregir a $P(S \leq 510.5)$.
> - $P(S < 510)$ incluye $\{\dots, 509\}$ → corregir a $P(S \leq 509.5)$.

> **Nota:** la corrección mejora la **mayoría** de las aproximaciones, pero no necesariamente **todas** para toda distribución discreta.

---

## Condiciones para aproximar Binomial/Poisson por Normal

Aunque $\text{Bi}(100, 0.05)$ es suma de 100 Bernoulli, su aproximación normal falla al segundo decimal cuando se evalúa un único evento. El problema aparece cuando $p$ es **muy chico** ($p \approx 0$) o **muy grande** ($p \approx 1$): la binomial queda demasiado **sesgada** para parecerse a una normal.

Por eso, para aproximar una **Binomial** por una Normal se pide:

$$\boxed{n \cdot p > 10 \qquad \text{y} \qquad n \cdot (1 - p) > 10}$$

Esto asegura un tamaño efectivo suficiente incluso en valores extremos de $p$.

Para una **Poisson**, recordando que se deduce como límite de la binomial, se pide:

$$\boxed{\lambda = n \cdot p > 10}$$

### Aplicación — Variables de distribución desconocida

El TCL también sirve cuando **no se conoce la distribución**, con tal de conocer media y varianza. Para las canciones, $E(M_i) = 150$ y $V(M_i) = 500$. El promedio anual:

$$\overline{M}_{104} = \frac{\sum_{i=1}^{104} M_i}{104} \overset{TCL}{\sim} \mathcal{N}\!\left(150,\, \sqrt{\frac{500}{104}}\right)$$

$$P\big(148 \leq \overline{M}_{104} \leq 153\big) \approx \Phi(1.3682) - \Phi(-0.9121) = 0.7335$$

---

## Resumen

- **Sumar variables:** por convolución (probabilidad total / integral). Varias familias **cierran**: Binomial, Poisson, (Binomial) Negativa, Gamma y Normal — casi todas exigen el **mismo parámetro** salvo Poisson y Normal.
- **Esperanza y varianza** son siempre aditivas para variables independientes.
- **Markov y Čebyšëv:** cotas válidas sin conocer la distribución; corresponden al peor caso.
- **LGN:** el promedio de i.i.d. converge en probabilidad a $\mu$ (su desvío $\to 0$).
- **TCL:** el promedio/suma de i.i.d. es aproximadamente **normal** para cualquier distribución con desvío finito; permite calcular probabilidades en un rango.
- **Corrección por continuidad** al aproximar discretas; condiciones $np > 10$ y $n(1-p) > 10$ (o $\lambda > 10$) para que la aproximación sea buena.

> **Cierre.** El TCL es, en palabras de la presentación, *"el mejor teorema del mundo mundial"*. **Ojo:** no vale si las variables promediadas **no son independientes** o **no tienen la misma distribución**.
