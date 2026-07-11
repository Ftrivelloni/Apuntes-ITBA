# Tests de Hipótesis

## Motivación

### Un cuento chino

Imaginemos cómo puede haberse dado la previa a este intercambio (película *Un cuento chino*, 2005):

- Hay una **hipótesis previa**: si bien la cantidad de tornillos por caja es a veces mayor o menor, su media es de 350 tornillos. Esta hipótesis es sostenida por el proveedor.
- Como cliente, Ricardo tiene una sospecha que esta hipótesis es falsa. Por lo tanto, plantea una **hipótesis alternativa**, contrapuesta a la del proveedor, que establece que la media de los tornillos por caja es **menor que 350**.
- Para poner a prueba estas hipótesis enfrentadas, Ricardo decide contar la cantidad de tornillos en las cajas — es decir, **recolecta evidencia** que pueda respaldar alguna de las hipótesis.
- Luego de recolectar evidencia, debe decidir por una de las hipótesis. En esta decisión puede cometer errores:
  - Puede decidir que el proveedor se equivoca, cuando éste tiene razón → llevaría a cambiar de proveedor de forma innecesaria.
  - Puede decidir que el proveedor tiene razón, cuando no la tiene → llevaría a mantener un proveedor que no cumple con su palabra.
- Para decidir, debe tener en cuenta que la cantidad de tornillos es **variable** — no cualquier valor menor que 350 es necesariamente indicio de que la hipótesis del proveedor es falsa.
- Una vez recolectada la evidencia, mientras más alejada esté de 350 la cantidad de tornillos, más sustento tiene la decisión de rechazar la hipótesis del proveedor.

### Analogía judicial

> *"Toda persona es inocente hasta que se demuestre lo contrario."*

- La **hipótesis nula** ($H_0$) es la presunción de inocencia.
- La **hipótesis alternativa** ($H_1$) es la hipótesis de culpabilidad, enfrentada a la nula.
- Se presentan todas las evidencias correspondientes al caso.
- En base a las evidencias, se toma una decisión que puede acarrear **2 tipos de errores**:
  - Se puede declarar culpable a alguien que es inocente → **Error tipo I** (se trata de evitar en casos dudosos).
  - Se puede declarar inocente a alguien culpable → **Error tipo II**.
- La decisión deberá contemplar que no cualquier evidencia incriminatoria puede ser comprobación de culpabilidad — la decisión está sujeta a dudas razonables.

---

## Planteamiento del test

### Hipótesis

Consideremos: $X_i =$ cantidad de tornillos en la $i$-ésima caja. Suponemos $X_i \sim \mathcal{N}(\mu, 10)$.

Las hipótesis enfrentadas son:

- **Hipótesis nula:** $H_0: \mu = 350$ (hipótesis del proveedor)
- **Hipótesis alternativa:** $H_1: \mu < 350$ (hipótesis de Ricardo)

### Estadístico de prueba

Para juntar evidencia, Ricardo toma una muestra de $n = 50$ cajas y calcula el promedio $\bar{X}_{50}$. Como las variables son i.i.d.:

$$\bar{X}_{50} \sim \mathcal{N}\!\left(\mu, \frac{10}{\sqrt{50}}\right)$$

Esta distribución probabilística nos permite diferenciar las observaciones razonables (probables) de lo improbable.

### Regla de decisión y tipos de error

Luego de tomar la muestra, Ricardo toma una decisión: *"Rechaza $H_0$"* si las evidencias apoyan su sospecha, y *"Acepta $H_0$"* si las evidencias no la apoyan lo suficiente.

| | Rechaza $H_0$ | Acepta $H_0$ |
|:-:|:-:|:-:|
| $H_0$ verdadera | **Error tipo I** | Decisión correcta |
| $H_0$ falsa | Decisión correcta | **Error tipo II** |

La probabilidad del **Error tipo I** se denomina **nivel de significación**, notada $\alpha$. Se elige un valor pequeño, como $\alpha = 0.05$.

> [!note] Observación
> Decimos que se "Acepta $H_0$" porque no significa que sea cierta — puede que no hayamos juntado las evidencias suficientes para rechazarla. Del mismo modo que si no se junta demasiada evidencia para probar la culpabilidad, no significa que la persona sea inocente.

---

## Tests de Hipótesis — Desvío conocido

### Valores críticos y región de rechazo

Para tomar la decisión, se calcula un **valor crítico** $x_c$ de forma que se rechace $H_0$ para todos los promedios menores que $x_c$.

Usando el nivel de significación $\alpha$:

$$\alpha = P(\text{Error tipo I}) = P(\text{Rechazar } H_0 \mid H_0 \text{ cierta}) = P(\bar{X}_{50} < x_c \mid \mu = 350)$$

Usando la estandarización, con $\bar{X}_{50} \sim \mathcal{N}(350, 10/\sqrt{50})$:

$$P(\bar{X}_{50} < x_c \mid \mu = 350) = \Phi\!\left(\frac{x_c - 350}{10/\sqrt{50}}\right) = \alpha$$

$$\frac{x_c - 350}{10/\sqrt{50}} = z_\alpha = -z_{1-\alpha} \implies x_c = 350 - z_{0.95} \cdot \frac{10}{\sqrt{50}} = 347.6738$$

**Regla de decisión:**
- Si $\bar{X}_{50} < 347.6738 \Rightarrow$ Rechaza $H_0$ → Cambia el proveedor.
- Si $\bar{X}_{50} \geq 347.6738 \Rightarrow$ Acepta $H_0$ → Mantiene el proveedor.

---

## Error tipo II y curva OC

### Cálculo del Error tipo II

El **Error tipo II** es aceptar $H_0$ cuando es falsa:

$$\beta(\mu_1) = P(\text{Error tipo II}) = P(\text{Aceptar } H_0 \mid H_0 \text{ falsa}) = P(\bar{X}_{50} \geq x_c \mid \mu = \mu_1 < 350)$$

Se evalúa como función de todos los valores posibles de $\mu_1$ (valores bajo $H_1$):

$$\beta(\mu_1) = 1 - \Phi\!\left(\frac{x_c - \mu_1}{10/\sqrt{50}}\right)$$

**Valores conocidos:**

- $\beta(x_c) = 1 - \Phi(0) = 0.5$ (por simetría de la normal)
- $\lim_{\mu_1 \to \mu_0^-} \beta(\mu_1) = 1 - \alpha = 0.95$
- $\beta(345) \approx 1 - \Phi(1.89068) \approx 0.0293$

### Curva de Operación Característica (OC)

La curva OC $\beta(\mu_1)$ tiene **forma sigmoide** con un cambio de concavidad en $x_c$. La curva "termina" en $\mu_0 = 350$ ya que a partir de ese valor deja de ser falsa la hipótesis nula.

El análisis de esta curva permite ver cuánto resignamos de Error tipo II al establecer el límite considerando sólo el Error tipo I.

### Curva de potencia

La **curva de potencia** $\pi(\mu_1)$ es complementaria a $\beta$:

$$\pi(\mu_1) = P(\text{Rechazar } H_0 \mid H_0 \text{ falsa}) = 1 - \beta(\mu_1)$$

Se busca que la potencia sea **alta**.

---

## p-Valor

El **p-Valor** se calcula *después* de tomar la muestra y da una noción de cuán probable es obtener lo observado (o algo más extremo), asumiendo que $H_0$ es verdadera.

**Ejemplo:** $x_{obs} = 323$

$$p\text{-Valor} = P(\bar{X}_{50} \leq x_{obs} \mid H_0 \text{ verdadera}) = \Phi\!\left(\frac{323 - 350}{10/\sqrt{50}}\right) \approx \Phi(-19.09) \approx 1.47 \times 10^{-81}$$

Aún dándole el beneficio de la duda al proveedor (asumiendo $H_0$ cierta), observar un número tan bajo es tan inverosímil que hay evidencia muy fuerte para rechazar su hipótesis. **Mientras más chico sea el p-Valor, más evidencia hay para rechazar $H_0$.**

> [!note] ¿Por qué "lo observado o más extremo"?
> Para identificar lo "más extremo", hay que observar la hipótesis alternativa. Como en este caso $H_1: \mu < 350$, mientras más chico sea el valor observado, más "extremo" será.
> 
> Si sólo nos basáramos en lo observado, como $\bar{X}_{50}$ es continua, $P(\bar{X}_{50} = x_{obs} \mid H_0) = 0$ para cualquier valor, lo cual deja de ser informativo.

---

## Tipos de tests (desvío conocido)

Para los tests de la media con $\sigma$ conocido se toman:
- Un valor de referencia $\mu_0$
- Un tamaño muestral $n$
- Un nivel de significación $\alpha$

### Test unilateral a izquierda

- $H_0: \mu = \mu_0$ vs. $H_1: \mu < \mu_0$

$$\text{Estadístico de prueba: } Z = \frac{\bar{X}_n - \mu_0}{\sigma/\sqrt{n}}$$

$$\text{Valor crítico: } x_c = \mu_0 - z_{1-\alpha} \cdot \frac{\sigma}{\sqrt{n}} \quad \text{ó} \quad z_c = -z_{1-\alpha}$$

**Regla de decisión:**

| | |
|:--|:--|
| Si $\bar{X}_n < x_c$ | $\Rightarrow$ Se rechaza $H_0$ |
| Si $\bar{X}_n \geq x_c$ | $\Rightarrow$ Se acepta $H_0$ |
| Si $Z < z_c$ | $\Rightarrow$ Se rechaza $H_0$ |
| Si $p\text{-Valor} < \alpha$ | $\Rightarrow$ Se rechaza $H_0$ |

$$\beta(\mu_1) = 1 - \Phi\!\left(\frac{x_c - \mu_1}{\sigma/\sqrt{n}}\right)$$

$$p\text{-Valor} = \Phi\!\left(\frac{x_{obs} - \mu_0}{\sigma/\sqrt{n}}\right)$$

---

### Test unilateral a derecha

- $H_0: \mu = \mu_0$ vs. $H_1: \mu > \mu_0$

$$\text{Valor crítico: } x_c = \mu_0 + z_{1-\alpha} \cdot \frac{\sigma}{\sqrt{n}} \quad \text{ó} \quad z_c = z_{1-\alpha}$$

**Regla de decisión:**

| | |
|:--|:--|
| Si $\bar{X}_n > x_c$ | $\Rightarrow$ Se rechaza $H_0$ |
| Si $\bar{X}_n \leq x_c$ | $\Rightarrow$ Se acepta $H_0$ |
| Si $p\text{-Valor} < \alpha$ | $\Rightarrow$ Se rechaza $H_0$ |

$$\beta(\mu_1) = \Phi\!\left(\frac{x_c - \mu_1}{\sigma/\sqrt{n}}\right)$$

$$p\text{-Valor} = 1 - \Phi\!\left(\frac{x_{obs} - \mu_0}{\sigma/\sqrt{n}}\right)$$

---

### Test bilateral

- $H_0: \mu = \mu_0$ vs. $H_1: \mu \neq \mu_0$

$$\text{Valores críticos: } x_{c1} = \mu_0 - z_{1-\frac{\alpha}{2}} \cdot \frac{\sigma}{\sqrt{n}} \quad , \quad x_{c2} = \mu_0 + z_{1-\frac{\alpha}{2}} \cdot \frac{\sigma}{\sqrt{n}} \quad \text{ó} \quad z_c = z_{1-\frac{\alpha}{2}}$$

**Regla de decisión:**

| | |
|:--|:--|
| Si $\bar{X}_n < x_{c1}$ o $\bar{X}_n > x_{c2}$ | $\Rightarrow$ Se rechaza $H_0$ |
| Si $x_{c1} \leq \bar{X}_n \leq x_{c2}$ | $\Rightarrow$ Se acepta $H_0$ |
| Si $|Z| > z_c$ | $\Rightarrow$ Se rechaza $H_0$ |
| Si $p\text{-Valor} < \alpha$ | $\Rightarrow$ Se rechaza $H_0$ |

$$\beta(\mu_1) = \Phi\!\left(\frac{x_{c2} - \mu_1}{\sigma/\sqrt{n}}\right) - \Phi\!\left(\frac{x_{c1} - \mu_1}{\sigma/\sqrt{n}}\right)$$

$$p\text{-Valor} = 2 \cdot \left(1 - \Phi\!\left(\frac{|x_{obs} - \mu_0|}{\sigma/\sqrt{n}}\right)\right)$$

---

## Comentarios importantes

> [!warning] Error conceptual
> Las hipótesis se plantean sobre **parámetros poblacionales**. Sobre valores muestrales **NO** se plantean hipótesis. Es un **HORROR CONCEPTUAL** plantear:
> $$H_0: \bar{X} = 350 \quad \text{INCORRECTO} \times$$
> $$H_1: \bar{X} < 350 \quad \text{INCORRECTO} \times$$

Para los tests unilaterales, es equivalente plantear $H_0: \mu \geq \mu_0$ vs. $H_1: \mu < \mu_0$ o simplemente $H_0: \mu = \mu_0$, ya que el valor crítico se calcula en función del **valor de referencia** $\mu_0$.

### Pre y post muestra

**Previo a tomar la muestra:**
- Tamaño muestral $n$
- Valor de referencia $\mu_0$
- Nivel de significación $\alpha$
- Hipótesis enfrentadas $H_0$ y $H_1$
- Estadístico de prueba $\bar{X}$ o $Z$
- Valores críticos $x_c$ o $z_c$
- Regla de decisión y regiones de rechazo
- Probabilidad de Error tipo II $\beta(\mu)$ y potencia $\pi(\mu)$

**Posterior a tomar la muestra:**
- Decisión tomada
- p-Valor

---

## Tests para proporciones

### Base teórica

Cuando lo que se quiere poner a prueba es una proporción poblacional $p$, recordemos que la proporción muestral $\hat{p}$ cumple (por aproximación normal a la binomial):

$$\hat{p} \overset{a}{\sim} \mathcal{N}\!\left(p,\, \frac{p(1-p)}{n}\right) \implies \frac{\hat{p} - p}{\sqrt{p(1-p)/n}} \overset{a}{\sim} \mathcal{N}(0, 1)$$

Si el tamaño muestral $n$ es grande, podemos utilizar esta aproximación.

### Ejemplo

El proveedor le cuenta a Ricardo que tuvo un problema en el **20%** de su producción (cajas con menos tornillos de los deseados). Ricardo sospecha que ese número es mayor. Decide revisar $n = 150$ cajas.

- $H_0: p = p_0 = 0.2$
- $H_1: p > p_0 = 0.2$

La proporción crítica con $\alpha = 0.05$:

$$p_c = 0.2 + z_{0.95} \cdot \sqrt{\frac{0.2 \cdot 0.8}{150}} = 0.2537$$

$$Z = \frac{\hat{p} - p_0}{\sqrt{p_0(1-p_0)/n}}$$

Se rechaza $H_0$ si $\hat{p} > 0.2537$ o $Z > z_{1-\alpha}$.

**Error tipo II** si la proporción real es $p_1 = 0.24$:

$$\beta(0.24) = \Phi\!\left(\frac{p_c - 0.24}{\sqrt{0.24 \cdot 0.76/150}}\right) = 0.653$$

**Post-muestra:** si se observa $\hat{p}_{obs} = 0.22 < 0.2537 = p_c$ → se acepta $H_0$.

$$p\text{-Valor} = 1 - \Phi\!\left(\frac{0.22 - 0.2}{\sqrt{0.2 \cdot 0.8 / 150}}\right) = 0.2701$$

---

### Test unilateral a izquierda (proporciones)

- $H_0: p = p_0$ vs. $H_1: p < p_0$

$$\text{Estadístico: } Z = \frac{\hat{p} - p_0}{\sqrt{p_0(1-p_0)/n}} \qquad \text{Valor crítico: } p_c = p_0 - z_{1-\alpha} \cdot \sqrt{\frac{p_0(1-p_0)}{n}}$$

$$\beta(p_1) = 1 - \Phi\!\left(\frac{p_c - p_1}{\sqrt{p_1(1-p_1)/n}}\right) \qquad p\text{-Valor} = \Phi\!\left(\frac{p_{obs} - p_0}{\sqrt{p_0(1-p_0)/n}}\right)$$

---

### Test unilateral a derecha (proporciones)

- $H_0: p = p_0$ vs. $H_1: p > p_0$

$$\text{Valor crítico: } p_c = p_0 + z_{1-\alpha} \cdot \sqrt{\frac{p_0(1-p_0)}{n}} \qquad z_c = z_{1-\alpha}$$

$$\beta(p_1) = \Phi\!\left(\frac{p_c - p_1}{\sqrt{p_1(1-p_1)/n}}\right) \qquad p\text{-Valor} = 1 - \Phi\!\left(\frac{p_{obs} - p_0}{\sqrt{p_0(1-p_0)/n}}\right)$$

---

### Test bilateral (proporciones)

- $H_0: p = p_0$ vs. $H_1: p \neq p_0$

$$p_{c1} = p_0 - z_{1-\frac{\alpha}{2}} \cdot \sqrt{\frac{p_0(1-p_0)}{n}} \qquad p_{c2} = p_0 + z_{1-\frac{\alpha}{2}} \cdot \sqrt{\frac{p_0(1-p_0)}{n}}$$

$$\beta(p_1) = \Phi\!\left(\frac{p_{c2} - p_1}{\sqrt{p_1(1-p_1)/n}}\right) - \Phi\!\left(\frac{p_{c1} - p_1}{\sqrt{p_1(1-p_1)/n}}\right)$$

$$p\text{-Valor} = 2 \cdot \left(1 - \Phi\!\left(\frac{|p_{obs} - p_0|}{\sqrt{p_0(1-p_0)/n}}\right)\right)$$

---

### Caso $n$ pequeño (distribución binomial)

Si $n$ es pequeño (ej. $n = 10$ cajas), no podemos usar la aproximación normal. Usamos la **distribución binomial exacta**.

Con $H_0: p = 0.2$ y $H_1: p > 0.2$, y $X_{10} \sim \text{Bi}(10, p)$:

$$\alpha = P(X_{10} \geq x_c \mid p = 0.2) = \sum_{i=x_c}^{10} \binom{10}{i} 0.2^i \cdot 0.8^{10-i}$$

| $x_c$ | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| $P(X_{10} \geq x_c)$ | 1 | 0.8926 | 0.6242 | 0.3222 | 0.1209 | **0.0328** | 0.0064 | 0.0009 | 0 | 0 | 0 |

Con $\alpha = 0.05$: si $X_{10} \geq 5$ → rechaza $H_0$; si $X_{10} \leq 4$ → acepta $H_0$.

El **p-Valor** para un $x_{obs}$ observado es directamente $P(X_{10} \geq x_{obs} \mid p = 0.2)$, que ya está calculado en la tabla.

El **Error tipo II** se calcula con la binomial:

$$\beta(p_1) = P(X_{10} \leq 4 \mid p = p_1) = \sum_{i=0}^{4} \binom{10}{i} p_1^i (1 - p_1)^{10-i}$$

---

## Tests de Hipótesis — Desvío desconocido

### Planteamiento del problema

Si Ricardo desconfía de la media, también puede desconfiar del desvío. Por lo tanto, estima $\sigma$ con el desvío muestral $s$. Con $n = 50$ grande, por TCL:

$$\frac{\bar{X}_{50} - \mu}{s/\sqrt{50}} \overset{aprox}{\sim} \mathcal{N}(0,1)$$

El estadístico de prueba es:

$$Z = \frac{\bar{X}_n - \mu_0}{s/\sqrt{n}}$$

Ya no se puede calcular un valor crítico $x_c$ antes de la muestra (pues depende de $s$, aún desconocido). Se usa directamente $Z$ con valor crítico $z_c$.

**Regla de decisión** (ej. $H_1: \mu < \mu_0$):
- Si $Z < z_c = -z_{0.95}$ → Rechaza $H_0$
- Si $Z \geq z_c$ → Acepta $H_0$

> [!note] Error tipo II con desvío desconocido
> La probabilidad de Error tipo II tampoco puede calcularse previo a la muestra, ya que dependería del desvío muestral aún desconocido. Sin embargo, si se tiene una **prueba piloto** (muestra previa pequeña con desvío $s_{\text{prev}}$), se puede estimar.

**p-Valor** (no cambia respecto al caso anterior, se calcula post-muestra):

$$p\text{-Valor} = \Phi\!\left(\frac{x_{obs} - \mu_0}{s/\sqrt{n}}\right)$$

---

### Tests con TCL (desvío desconocido, $n$ grande)

#### Test unilateral a izquierda (TCL)

- $H_0: \mu = \mu_0$ vs. $H_1: \mu < \mu_0$, con $Z = \dfrac{\bar{X}_n - \mu_0}{s/\sqrt{n}}$

$$z_c = -z_{1-\alpha}$$

$$\text{Se rechaza } H_0 \text{ si } Z < z_c \quad \text{ó} \quad p\text{-Valor} < \alpha$$

$$p\text{-Valor} = \Phi\!\left(\frac{x_{obs} - \mu_0}{s/\sqrt{n}}\right)$$

#### Test unilateral a derecha (TCL)

- $H_0: \mu = \mu_0$ vs. $H_1: \mu > \mu_0$

$$z_c = z_{1-\alpha} \qquad p\text{-Valor} = 1 - \Phi\!\left(\frac{x_{obs} - \mu_0}{s/\sqrt{n}}\right)$$

#### Test bilateral (TCL)

- $H_0: \mu = \mu_0$ vs. $H_1: \mu \neq \mu_0$

$$z_c = z_{1-\frac{\alpha}{2}} \qquad p\text{-Valor} = 2 \cdot \left(1 - \Phi\!\left(\frac{|x_{obs} - \mu_0|}{s/\sqrt{n}}\right)\right)$$

---

### Tamaños muestrales pequeños — Distribución $t$ de Student

Si $n$ es pequeño y las variables $X_i \sim \mathcal{N}(\mu, \sigma)$:

$$T = \frac{\bar{X}_n - \mu}{s/\sqrt{n}} \sim t_{n-1}$$

Con $H_1: \mu < \mu_0$, el valor crítico es $t_c = -t_{n-1;\, 1-\alpha}$ ya que:

$$\alpha = P\!\left(\frac{X_{10} - 350}{s/\sqrt{10}} \leq -t_{9;\,0.95} \mid \mu = 350\right)$$

Se rechaza $H_0$ si $T < -t_{9;\,0.95}$.

**Comentario sobre el p-Valor:** como $t_{obs} = -1.5811$ (para $x_{obs} = 344$, $s_{obs} = 12$, $n = 10$):

$$p\text{-Valor} = P(T \leq t_{obs} \mid H_0 \text{ cierta}) = F_{T_9}(t_{obs})$$

Acotando con la tabla: $-t_{9;\,0.95} \leq t_{obs} \leq -t_{9;\,0.9}$, por lo tanto $0.05 \leq p\text{-Valor} \leq 0.1$ → se acepta $H_0$.

---

### Resumen: Tests $t$ de Student

#### Test unilateral a izquierda ($t$ de Student)

- $H_0: \mu = \mu_0$, $H_1: \mu < \mu_0$, $T = \dfrac{\bar{X}_n - \mu_0}{s/\sqrt{n}}$

$$t_c = -t_{n-1;\,1-\alpha}$$

$$\text{Se rechaza } H_0 \text{ si } T < t_c$$

$$p\text{-Valor} = F_{T_{n-1}}\!\left(\frac{x_{obs} - \mu_0}{s/\sqrt{n}}\right)$$

donde $F_{T_{n-1}}$ es la función de distribución acumulada de una $t$ de Student con $n-1$ grados de libertad.

#### Test unilateral a derecha ($t$ de Student)

$$t_c = t_{n-1;\,1-\alpha} \qquad \text{Se rechaza } H_0 \text{ si } T > t_c$$

$$p\text{-Valor} = 1 - F_{T_{n-1}}\!\left(\frac{x_{obs} - \mu_0}{s/\sqrt{n}}\right)$$

#### Test bilateral ($t$ de Student)

$$t_c = t_{n-1;\,1-\frac{\alpha}{2}} \qquad \text{Se rechaza } H_0 \text{ si } |T| > t_c$$

$$p\text{-Valor} = 2 \cdot \left(1 - F_{T_{n-1}}\!\left(\frac{|x_{obs} - \mu_0|}{s/\sqrt{n}}\right)\right)$$

---

## Identificación de escenarios

La mayoría de los casos se termina utilizando la distribución normal por el **TCL**. Aún si el desvío es conocido o desconocido, si el tamaño muestral es grande, las diferencias numéricas son despreciables.

Lo que se agrega para proporciones es la posibilidad de tests con $n$ pequeño usando distribuciones discretas (Binomial, Hipergeométrica, Geométrica, etc.).

```
                    ┌─────────────────────────────┐
                    │    Parámetro a estimar       │
                    └──────────┬──────────┬────────┘
                               │          │
                            Media      Proporción
                               │          │
                    ┌──────────┴──┐     ┌─┴──────────┐
               Variables     Variables  n grande    n chico
               Normales     No Normales  │            │
                    │             │   Cuantiles    Binomial
             ┌──────┴──┐     n grande   Normales  Hipergeom.
          Desvío    Desvío   Cuantiles             Geométrica
         Conocido  Descono.   Normales             ...
             │         │
         Cuantiles  Cuantiles
          Normales  t Student
                         │
                    Con n grande
                    vale Normal
```
