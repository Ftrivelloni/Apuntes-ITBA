# Procesos Estocásticos

## Motivación — La escritura de Natalia

Natalia está escribiendo una novela. La cantidad de palabras que escribe por minuto sigue una distribución Binomial, pero se ve influida por el ritmo con el que viene escribiendo: si venía escribiendo mucho, tiende a escribir más; si se bloquea, tiende a escribir menos.

La clave es que **no** estamos mirando una única variable aleatoria, sino un **conjunto** de variables relacionadas, una por cada minuto. Representan lo mismo (palabras por minuto) pero refieren a momentos distintos y sus probabilidades cambian. Por eso, no alcanza con nombrar la variable: hay que indicar también el minuto observado.

$$X(k) = \text{cantidad de palabras escritas en el } k\text{-ésimo minuto} \qquad \{X(k)\}_{k \in \mathbb{N}}$$

No se fija un máximo de minutos: interesa ver la evolución si la tendencia siguiera indefinidamente.

### Probabilidades dependientes del pasado

En el ejemplo, la distribución de cada minuto depende del anterior: $X(1) \sim \text{Bi}(3, 0.6)$ y para $k > 1$, $X(k) \sim \text{Bi}(n_k, p_k)$ donde $n_k$ sube, baja o se mantiene según cuán alto fue $X(k-1)$, y $p_k$ mezcla el promedio histórico de las $p_i$ con la última proporción observada $\frac{X(k-1)}{n_{k-1}}$.

Calcular $P(X(3) = 4)$ requiere un **árbol de probabilidad total** sobre los dos primeros minutos; sumando las ramas no nulas se obtiene $P(X(3) = 4) = 0.1648$. La moraleja: cuando las variables están muy relacionadas, calcular probabilidades es **difícil**, pero el árbol de los primeros pasos ayuda a entender el proceso, y simular es accesible si se conoce la estructura.

---

## Definiciones generales

Un **proceso estocástico** es un conjunto de variables aleatorias potencialmente relacionadas, indexadas por un parámetro que indica cómo "avanza" el proceso:

$$\{X(t)\}_{t \in I \subseteq \mathbb{R}_{\geq 0}}$$

El parámetro $t$ suele ser el tiempo, pero puede ser distancia u otra magnitud. *Proceso* = fenómeno que evoluciona; *estocástico* = aleatorio, no anticipable.

**Espacio de estados** $E$: valores que puede tomar el proceso. **Espacio del parámetro** $I$: valores del índice. Ambos pueden ser discretos o continuos, dando cuatro combinaciones:

| Estados \ Parámetro | Discreto | Continuo |
|:--|:--|:--|
| **Discreto** | Palabras por minuto | En cada instante, escribe o no una palabra |
| **Continuo** | Temperatura promedio por minuto | Temperatura en cada instante |

### Estacionariedad e incrementos

Un proceso es **estacionario** si la distribución de las variables no cambia en el tiempo: $F_{X(t+\tau)}(x) = F_{X(t)}(x)$ para todo $x, t, \tau$. Como es una igualdad de distribuciones, es muy exigente; suele analizarse la estacionariedad **en sentido amplio**:

- $E(X(t)) = \mu$ y $V(X(t)) = \sigma^2$ **constantes** (no dependen de $t$).
- $\text{Cov}(X(t), X(t+\tau))$ depende **sólo** del desfasaje $\tau$, no de $t$.

Los **incrementos** son las diferencias entre variables del proceso:

$$(\Delta_\tau X)_t = X(t + \tau) - X(t)$$

A veces conviene analizar el proceso de incrementos: hay procesos no estacionarios cuyos incrementos **sí** lo son, lo que simplifica los cálculos.

---

## Procesos de conteo

Un proceso $\{N(t)\}_{t \geq 0}$ es un **proceso de conteo** si $E = \mathbb{N}_0$ y es no decreciente ($N(s) \leq N(t)$ para $s < t$). Cuenta ocurrencias de un suceso hasta el tiempo $t$:

$$N(t) = \text{cantidad de eventos en } [0, t], \qquad \text{usualmente } N(0) = 0$$

El **incremento** $N(t) - N(s)$ cuenta las ocurrencias en el intervalo $(s, t]$. Dos propiedades importantes que pueden cumplir los incrementos:

- **Independientes:** para intervalos disjuntos $(s_1, t_1]$ y $(s_2, t_2]$, los incrementos $N(t_1) - N(s_1)$ y $N(t_2) - N(s_2)$ son independientes — lo que pasa en un intervalo no influye en el otro.
- **Estacionarios:** $N(t) - N(s)$ tiene la misma distribución que $N(t - s) - N(0)$ — la distribución del incremento depende sólo de la **longitud** del intervalo, no de dónde empieza.

---

## Procesos de Poisson

Un **Proceso de Poisson** de parámetro $\lambda$ es un proceso de conteo que cumple, además:

$$\boxed{1.\quad N(t) \sim \mathcal{P}o(\lambda t) \implies P(N(t) = k) = e^{-\lambda t}\frac{(\lambda t)^k}{k!}, \quad k \in \mathbb{N}_0}$$

$$\boxed{2.\quad \text{Incrementos independientes} \qquad 3.\quad \text{Incrementos estacionarios: } N(t) - N(s) \sim N(t - s)}$$

> $\lambda$ es la **tasa** de ocurrencia (eventos por unidad de tiempo). El valor esperado en $[0,t]$ es $E(N(t)) = \lambda t$.

### Ejemplo — Probabilidades

Las notificaciones de Natalia siguen un Poisson con $\lambda = 0.05 \ \tfrac{1}{\min}$.

**¿5 notificaciones en los primeros 20 minutos?** Como $N(20) \sim \mathcal{P}o(\lambda \cdot 20) = \mathcal{P}o(1)$:

$$P(N(20) = 5) = e^{-1}\frac{1^5}{5!} = 0.0031$$

**¿Al menos 3 en los primeros 40 minutos?** Con $N(40) \sim \mathcal{P}o(2)$:

$$P(N(40) \geq 3) = 1 - \sum_{i=0}^{2} e^{-2}\frac{2^i}{i!} = 0.3233$$

### Ejemplo — Incrementos

Usando estacionariedad (propiedad 3), el incremento entre $25$ y $40$ se comporta como $N(15) \sim \mathcal{P}o(0.75)$:

$$P\big(N(40) - N(25) \leq 3\big) = P(N(15) \leq 3) = \sum_{i=0}^{3} e^{-0.75}\frac{0.75^i}{i!} = 0.9927$$

$$E\big(N(40) - N(10)\big) = E(N(30)) = \lambda \cdot 30 = 1.5$$

### Ejemplo — Condicionales (pasado → futuro)

Para $P(N(40) = 6 \mid N(15) = 2)$, se reescribe el evento futuro como un **incremento** y se usa independencia (propiedad 2) más estacionariedad (propiedad 3):

$$P(N(40) = 6 \mid N(15) = 2) = P\big(N(40) - N(15) = 4\big) = P(N(25) = 4) = e^{-1.25}\frac{1.25^4}{4!} = 0.0291$$

> [!warning] Error común
> Es tentador escribir $P(N(40)=6 \mid N(15)=2) = \dfrac{P(N(40)-N(15)=4)}{P(N(15)=2)}$. **Está mal.** La intersección garantiza $N(15) = 2$, mientras que el incremento sólo dice qué pasa entre 15 y 40 — en los primeros 15 minutos podría pasar cualquier cosa. La simplificación correcta usa que $P(\text{incremento} \cap N(15)=2) = P(\text{incremento}) \cdot P(N(15)=2)$.

### Ejemplo — Condicional invertido (futuro → pasado)

Para $P(N(15) = 2 \mid N(40) = 6)$ el truco del incremento **no aplica directo**, hay que desarrollar la definición:

$$P(N(15) = 2 \mid N(40) = 6) = \frac{P(N(25)=4)\cdot P(N(15)=2)}{P(N(40)=6)} = \binom{6}{4}\left(\frac{1.25}{2}\right)^4\left(\frac{0.75}{2}\right)^2 = 0.3219$$

> Notar que el resultado **no** se parece a un incremento de Poisson: tiene forma de **Binomial** con $n = 6$ y $p = \tfrac{1.25}{2}$. El truco del incremento funciona cuando se condiciona el **pasado** para predecir el **futuro**, no al revés.

### Tiempos entre eventos

Definimos el tiempo hasta la $k$-ésima notificación, $T(k)$, con espacio de estados continuo ($E = \mathbb{R}_{\geq 0}$) y parámetro discreto ($I = \mathbb{N}_0$, con $T(0) = 0$). Los incrementos son los **tiempos de espera** entre eventos consecutivos:

$$\tau(k) = T(k) - T(k-1)$$

**Resultado clave:** estos tiempos de espera son **i.i.d. exponenciales** de parámetro $\lambda$. La idea intuitiva: el primer evento ocurre después de $t$ **si y sólo si** no hubo eventos en $[0,t]$, es decir $\{\tau(1) > t\} = \{N(t) = 0\}$, cuya probabilidad es $e^{-\lambda t}$:

$$\boxed{\tau(k) \sim \mathcal{E}(\lambda) \text{ i.i.d.}}$$

### Tiempo hasta el $n$-ésimo evento

Las variables $T(n)$ **no** son independientes (son crecientes), pero se escriben como suma de los tiempos de espera:

$$T(n) = \sum_{k=1}^{n} \tau(k) \overset{\text{suma de exp. i.i.d.}}{\implies} \boxed{T(n) \sim \Gamma(n, \lambda)}$$

Su acumulada sólo tiene primitiva para algunos $n$, pero muchos cálculos se resuelven con las propiedades del proceso. Por ejemplo, "la tercera notificación llega después de los 40 minutos" equivale a "hubo menos de 3 eventos en 40 minutos":

$$P(T(3) > 40) = P(N(40) < 3) = \sum_{i=0}^{2} e^{-2}\frac{2^i}{i!} = 0.6767$$

Con software, `1-pgamma(40,3,rate=0.05)` da exactamente $0.6766764$.

---

## Cadenas de Markov

### La propiedad de Markov

Para acompañar la escritura, Natalia alterna su comida cada hora entre **B**izcochos, **C**ereal y **F**ruta. La primera hora elige al azar; luego las transiciones son: tras bizcochos repite con $0.75$ (si no, fruta); tras cereal repite con $0.6$ (si no, bizcochos); tras fruta siempre cereal.

Lo distintivo: la comida de la próxima hora depende **sólo** de la actual, no de toda la historia. Esa es la **propiedad de Markov**: para $r < s < t$, la distribución de $X(t)$ condicionada al presente $X(s)$ y al pasado $X(r)$ coincide con la condicionada sólo al presente:

$$\boxed{P\big(\underbrace{X(t) = s_t}_{\text{futuro}} \mid \underbrace{X(s) = s_s}_{\text{presente}}, \underbrace{X(r) = s_r}_{\text{pasado}}\big) = P\big(X(t) = s_t \mid X(s) = s_s\big)}$$

Cuando el espacio de **estados** es discreto, el proceso es una **Cadena de Markov**. Si además el parámetro es discreto ($I = \mathbb{N}$), trabajamos con cadenas a tiempo discreto. (En el ejemplo de las palabras esto **no** valía: cada minuto dependía de todos los anteriores.)

### Cálculo de probabilidades

Con un árbol y la propiedad de Markov (se puede omitir el pasado en cada transición):

$$P(X(3) = F) = \tfrac{1}{3}\cdot 0.75 \cdot 0.25 + \tfrac{1}{3}\cdot 0.4 \cdot 0.25 = 0.095833$$

$$P(X(3) = F \mid X(1) = B) = 0.75 \cdot 0.25 = 0.1875$$

En el condicional, las probabilidades iniciales al azar **no influyen**: sólo cuentan las transiciones.

### Matriz y diagrama de transición

Las probabilidades de un paso $p_{ij} = P(X(n+1) = s_j \mid X(n) = s_i)$ se juntan en la **matriz de transición** $\mathbb{P} \in \mathbb{R}^{m \times m}$. Para las comidas, con $E = \{B, C, F\}$:

$$\mathbb{P} = \begin{matrix} B \\ C \\ F \end{matrix}\begin{pmatrix} 0.75 & 0 & 0.25 \\ 0.4 & 0.6 & 0 \\ 0 & 1 & 0 \end{pmatrix}$$

> [!warning] Filas suman 1, columnas no
> Las **filas** de $\mathbb{P}$ suman 1 (desde un estado, se va a *algún* estado: forman una partición). Las **columnas NO tienen por qué sumar 1**, porque recorren distintos eventos condicionantes y no cumplen los axiomas de Kolmogorov.

### Transiciones en múltiples pasos

Por probabilidad total y la propiedad de Markov, la probabilidad de ir de $s_i$ a $s_j$ en $k$ pasos es la coordenada $(i,j)$ de la $k$-ésima potencia de la matriz:

$$\boxed{P(X(n+k) = s_j \mid X(n) = s_i) = (\mathbb{P}^k)_{ij}}$$

Por ejemplo, $P(X(3) = F \mid X(1) = B) = 0.1875$ coincide con $(\mathbb{P}^2)_{BF}$:

$$\mathbb{P}^2 = \begin{pmatrix} 0.5625 & 0.25 & 0.1875 \\ 0.54 & 0.36 & 0.1 \\ 0.4 & 0.6 & 0 \end{pmatrix}, \qquad \mathbb{P}^4 = \begin{pmatrix} 0.5264 & 0.3431 & 0.1305 \\ 0.5382 & 0.3246 & 0.1373 \\ 0.549 & 0.316 & 0.135 \end{pmatrix}$$

Esto es muy útil cuando el árbol se ramifica demasiado.

### Vector de distribución

Las probabilidades **sin condicionar** de estar en cada estado en el tiempo $n$ forman el **vector de distribución** $\vec{p}(n) = (P(X(n)=s_1), \dots, P(X(n)=s_m))$, cuyas componentes suman 1. Cumple:

$$\boxed{\vec{p}(n+1) = \vec{p}(n) \times \mathbb{P} \implies \vec{p}(n+k) = \vec{p}(n) \times \mathbb{P}^k}$$

Con $\vec{p}(1) = (\tfrac13,\tfrac13,\tfrac13)$ se reobtiene $\vec{p}(3) = (0.5008,\ 0.4033,\ 0.0958)$, cuya tercera componente es el $P(X(3)=F)$ calculado antes.

> **Cuidado con el sentido temporal.** $(\mathbb{P}^k)_{ij}$ sólo sirve "hacia el futuro". Para un condicional invertido hay que usar Bayes: $P(X(1)=B \mid X(3)=F) = \dfrac{P(X(3)=F\mid X(1)=B)\,P(X(1)=B)}{P(X(3)=F)} = \dfrac{15}{23} = 0.6522$.

---

## Comportamiento a largo plazo

### Distribución estacionaria

Iterando las potencias de $\mathbb{P}$ (en las comidas: $\mathbb{P}^{16}, \mathbb{P}^{32}, \dots$), las filas se **estabilizan** en un mismo vector. Decimos que la cadena tiene **distribución estacionaria** $\vec{\pi}$ si existe el límite y todas sus filas son iguales:

$$\exists \lim_{n \to +\infty} \mathbb{P}^n = \begin{pmatrix} \vec{\pi} \\ \vec{\pi} \\ \vdots \\ \vec{\pi} \end{pmatrix}$$

$\vec{\pi}$ refleja el comportamiento de la cadena a largo plazo, **independiente del estado inicial**.

### Cadenas regulares

- Un estado $s_j$ es **accesible** desde $s_i$ si $(\mathbb{P}^k)_{ij} > 0$ para algún $k$.
- Una cadena es **regular** si $\exists k$ tal que $\mathbb{P}^k$ tiene **todas** sus coordenadas estrictamente positivas (implica accesibilidad mutua, pero no al revés).

$$\boxed{\text{Si la cadena es regular} \implies \text{tiene distribución estacionaria } \vec{\pi}, \text{ y } \vec{\pi} = \vec{\pi} \times \mathbb{P}}$$

Es decir, $\vec{\pi}$ es un **autovector a izquierda** de $\mathbb{P}$ con autovalor 1.

> [!warning] Suficiente, no necesaria
> La regularidad es **condición suficiente, no necesaria**. Una cadena puede tener distribución estacionaria sin ser regular; y si un $\vec{\pi}$ cumple $\vec{\pi} = \vec{\pi}\times\mathbb{P}$, no necesariamente es *la* estacionaria si la cadena no es regular.

**Cálculo (comidas).** La cadena es regular ($\mathbb{P}^4 > 0$). Se resuelve $\vec{\pi} = \vec{\pi}\times\mathbb{P}$ junto con $a+b+c = 1$ (las ecuaciones del sistema son linealmente dependientes; la normalización las cierra):

$$\vec{\pi} = \left(\tfrac{8}{15},\ \tfrac{1}{3},\ \tfrac{2}{15}\right) = (0.5333,\ 0.3333,\ 0.1333)$$

coincide con $\mathbb{P}^{32}$.

---

## Estados especiales y cadenas no regulares

### Estados absorbentes

Si Natalia oscila cada 5 min entre **E**scribir y **P**rocrastinar hasta **T**erminar (estado del que no se sale), con $E = \{E, P, T\}$:

$$\mathbb{P} = \begin{pmatrix} 0.5 & 0.3 & 0.2 \\ 0.2 & 0.7 & 0.1 \\ 0 & 0 & 1 \end{pmatrix}$$

Un estado $s_i$ es **absorbente** si $p_{ii} = 1$ (una vez allí, nunca sale). La cadena **no es regular** (la fila de $T$ siempre tiene ceros). Las potencias convergen a filas $(0, 0, 1)$: con un **único** estado absorbente accesible desde todos, la cadena termina allí **sin importar dónde empiece**.

### Múltiples absorbentes

Agregando **R**enunciar (segundo absorbente), las potencias de $\mathbb{P}$ **no** convergen a un único vector: la probabilidad de terminar en T o en R **depende del estado inicial**. Por lo tanto, con **más de un estado absorbente, la cadena NO tiene distribución estacionaria**.

### Estados transientes

Un estado es **transiente** si se puede no volver a él con probabilidad positiva (ej.: el Kale, al que no se regresa una vez que se prueba otra comida). A largo plazo se llega a un transiente con probabilidad **cero**; el resto del vector se completa con los valores límite de los estados recurrentes. Ej.: $\vec{\pi} = \left(0, \tfrac{8}{15}, \tfrac13, \tfrac{2}{15}\right)$.

### Cadenas periódicas

Si Natalia alterna determinísticamente entre Contenta y Triste, $\mathbb{P} = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}$, entonces $\mathbb{P}^2 = \mathbb{I}$ y las potencias alternan entre $\mathbb{P}$ (impares) e $\mathbb{I}$ (pares). Las coordenadas **no convergen**: la cadena **NO tiene distribución estacionaria**.

---

## Cadenas absorbentes: matriz fundamental

Para una cadena con estados transitorios y absorbentes, se reordena $\mathbb{P}$ en bloques:

$$\mathbb{P} = \begin{pmatrix} \mathbb{Q} & \mathbb{F} \\ \mathbb{O} & \mathbb{I} \end{pmatrix}$$

donde $\mathbb{Q}$ recoge las transiciones entre transitorios, $\mathbb{F}$ de transitorios a absorbentes, $\mathbb{I}$ identidad (absorbentes) y $\mathbb{O}$ ceros. La **matriz fundamental** es:

$$\boxed{\mathbb{M} = (\mathbb{I} - \mathbb{Q})^{-1}}$$

**Pasos en cada estado.** $\mathbb{M}_{ij}$ es el número esperado de pasos en el transitorio $s_j$ partiendo de $s_i$, antes de la absorción. Para el ejemplo E/P/T/R:

$$\mathbb{M} = \begin{pmatrix} 0.5 & -0.3 \\ -0.1 & 0.4 \end{pmatrix}^{-1} = \frac{100}{17}\begin{pmatrix} 0.4 & 0.3 \\ 0.1 & 0.5 \end{pmatrix} \approx \begin{pmatrix} 2.353 & 1.765 \\ 0.588 & 2.941 \end{pmatrix}$$

**Tiempos de absorción.** Sumando por filas (multiplicando por un vector de unos) se obtiene el número esperado de pasos hasta la absorción:

$$\mathbb{M} \times \begin{pmatrix} 1 \\ 1 \end{pmatrix} = \begin{pmatrix} E(T_E) \\ E(T_P) \end{pmatrix} \approx \begin{pmatrix} 4.118 \\ 3.529 \end{pmatrix}$$

**Probabilidades de absorción.** $\mathbb{M} \times \mathbb{F}$ da la probabilidad de terminar en cada absorbente según el estado inicial:

$$\mathbb{M} \times \mathbb{F} = \begin{pmatrix} \tfrac{33}{85} & \tfrac{52}{85} \\ \tfrac{5}{34} & \tfrac{29}{34} \end{pmatrix} \approx \begin{pmatrix} P(A_T\mid E) & P(A_R\mid E) \\ P(A_T\mid P) & P(A_R\mid P) \end{pmatrix} = \begin{pmatrix} 0.388 & 0.612 \\ 0.147 & 0.853 \end{pmatrix}$$

Todos estos valores coinciden con los obtenidos por simulación. Empezando a escribir, la novela tiene más chances de **terminarse** (y tarda más en absorberse) que empezando a procrastinar.

---

## Cadenas regulares: tiempos de espera

En una cadena regular se visita todo estado tarde o temprano. Interesa $T_{i,j}$ = cantidad de pasos hasta llegar a $s_j$ partiendo de $s_i$. Como $\mathbb{P}$ no tiene bloque identidad, **no** sirve $(\mathbb{I} - \mathbb{P})^{-1}$ (no es inversible). Se usa la matriz $\mathbb{W}$ con $\vec{\pi}$ en todas sus filas y se define:

$$\boxed{\mathbb{Z} = (\mathbb{I} - \mathbb{P} + \mathbb{W})^{-1}}$$

Con $w_j$ la $j$-ésima coordenada de $\vec{\pi}$:

$$E(T_{i,j}) = \frac{\mathbb{Z}_{jj} - \mathbb{Z}_{ij}}{w_j} \ (i \neq j), \qquad E(T_{i,i}) = \frac{1}{w_i}$$

El **tiempo de retorno** a un estado es el recíproco de su probabilidad estacionaria. Para las comidas, con $\vec{\pi} = \left(\tfrac{8}{15}, \tfrac13, \tfrac{2}{15}\right)$, se obtiene una matriz de tiempos esperados que coincide con la simulación (p. ej. $E(T_{B,B}) = \tfrac{15}{8} = 1.875$, $E(T_{F,C}) = 1$).

---

## Resumen

- Un **proceso estocástico** es una familia de variables $\{X(t)\}$ indexadas por tiempo/espacio; se clasifica según estados/parámetro discretos o continuos.
- **Proceso de Poisson** ($\lambda$): conteo con $N(t) \sim \mathcal{P}o(\lambda t)$, incrementos independientes y estacionarios. Los tiempos entre eventos son **exponenciales i.i.d.**; el tiempo al $n$-ésimo evento es **$\Gamma(n,\lambda)$**. Se cuenta hacia el futuro con incrementos; hacia el pasado hay que usar Bayes.
- **Cadena de Markov**: el futuro depende sólo del presente. Se describe con la **matriz de transición** $\mathbb{P}$ (filas suman 1); las transiciones en $k$ pasos son $(\mathbb{P}^k)_{ij}$ y la distribución evoluciona como $\vec{p}(n+1) = \vec{p}(n)\,\mathbb{P}$.
- **Largo plazo:** las cadenas **regulares** tienen distribución estacionaria $\vec{\pi} = \vec{\pi}\,\mathbb{P}$ (suficiente, no necesaria). Los estados **absorbentes**, **transientes** y las cadenas **periódicas** rompen este comportamiento.
- **Cadenas absorbentes:** la matriz fundamental $\mathbb{M} = (\mathbb{I}-\mathbb{Q})^{-1}$ da pasos por estado, tiempos de absorción ($\mathbb{M}\mathbf{1}$) y probabilidades de absorción ($\mathbb{M}\mathbb{F}$).
- **Cadenas regulares:** $\mathbb{Z} = (\mathbb{I}-\mathbb{P}+\mathbb{W})^{-1}$ permite calcular tiempos de espera y de retorno ($E(T_{i,i}) = 1/w_i$).
