---
tema: 2
titulo: Autómatas Finitos
materia: Autómatas, Teoría de Lenguajes y Compiladores
autor: Lic. Ana María Arias Roig
tags:
  - TLA
  - autómatas
  - AFD
  - AFND
  - minimización
---

# 2 · Autómatas Finitos

> [!abstract] Índice del tema
> - [[#Definición general]]
> - [[#Representación · tabla y diagrama]]
> - [[#Autómatas Finitos Determinísticos · AFD]]
> - [[#AFD Mínimo]]
> - [[#Autómatas Finitos No Determinísticos · AFND]]
> - [[#Equivalencia entre AFD y AFND · construcción de subconjuntos]]
> - [[#AFND con transiciones λ · AFND-λ]]

## Definición general

> [!definition] Autómata finito
> Es una quíntupla $M = (Q, \Sigma, \delta, q_0, F)$ donde:
> - $Q$: conjunto finito de **estados**.
> - $\Sigma$: **alfabeto** de entrada.
> - $q_0 \in Q$: **estado inicial**.
> - $F \subseteq Q$: conjunto de **estados finales** o de aceptación.
> - $\delta$: **función de transición** $\delta : Q \times \Sigma \to \mathcal{P}(Q)$, donde $\mathcal{P}(Q)$ denota todos los subconjuntos de $Q$.

## Representación · tabla y diagrama

La función de transición se puede representar de dos formas: mediante una **tabla de transición** o mediante un **diagrama de transición**.

> [!note] Diagrama de transición (grafo)
> - Cada círculo (nodo) representa un **estado**.
> - Cada círculo **doble** representa un estado **final**.
> - Una flecha apuntando a un estado indica que es el **inicial**.
> - Cada arco dirigido representa una parte de la función de transición.
> - El símbolo o etiqueta sobre el arco indica qué se consumió de la entrada al efectuar esa transición.

> [!example] Ejemplo
> $M = (\{q_0, q_1, q_2, q_3, t\}, \{0,1\}, \delta, q_0, \{q_3\})$
>
> $$\begin{aligned}
> &\delta(q_0, 0) = q_1 & &\delta(q_0, 1) = t \\
> &\delta(q_1, 0) = q_2 & &\delta(q_1, 1) = q_3 \\
> &\delta(q_2, 0) = t   & &\delta(q_2, 1) = q_3 \\
> &\delta(q_3, 0) = t   & &\delta(q_3, 1) = t \\
> &\delta(t, 0) = t     & &\delta(t, 1) = t
> \end{aligned}$$
>
> **Tabla de transición** ($*$ marca el estado final):
>
> | $\delta$ | $0$ | $1$ |
> |----------|-----|-----|
> | $q_0$    | $q_1$ | $t$ |
> | $q_1$    | $q_2$ | $q_3$ |
> | $q_2$    | $t$   | $q_3$ |
> | $*\,q_3$ | $t$   | $t$ |
> | $t$      | $t$   | $t$ |

## Autómatas Finitos Determinísticos · AFD

> [!definition] Función de transición de un AFD
> En los AFD la función de transición se define $\delta : Q \times \Sigma \to Q$.
>
> A cada par (estado, símbolo) le corresponde **uno y sólo un** estado.

### Función de transición extendida

La función de transición extendida $\hat{\delta}$ describe lo que ocurre cuando se parte de cualquier estado y se sigue una secuencia de entradas. Se construye por inducción a partir de $\delta$.

> [!definition] $\hat{\delta}$ por inducción sobre la longitud de la cadena
> - **Base:** $\hat{\delta}(q, \lambda) = q$
> - **Paso inductivo:** siendo $\omega = \omega' a$,
> $$\hat{\delta}(q, \omega) = \hat{\delta}(q, \omega' a) = \delta\big(\hat{\delta}(q, \omega'),\, a\big)$$

> [!example] Cálculo de $\hat{\delta}(q_0, \text{"001"})$
> $$\hat{\delta}(q_0, \lambda) = q_0$$
> $$\hat{\delta}(q_0, \text{"0"}) = \delta(\hat{\delta}(q_0, \lambda), 0) = \delta(q_0, 0) = q_1$$
> $$\hat{\delta}(q_0, \text{"00"}) = \delta(\hat{\delta}(q_0, \text{"0"}), 0) = \delta(q_1, 0) = q_2$$
> $$\hat{\delta}(q_0, \text{"001"}) = \delta(\hat{\delta}(q_0, \text{"00"}), 1) = \delta(q_2, 1) = q_3$$
> Es decir, $\hat{\delta}(q_0, \text{"001"}) = q_3$.

### Configuración instantánea

> [!definition] Configuración instantánea
> Es una descripción del autómata en un momento dado. Se denota con un par $(q, \omega)$, donde $q$ es un estado y $\omega \in \Sigma^{*}$.
>
> El símbolo $\vdash$ indica el **movimiento válido** entre dos configuraciones:
> $$(q, a\omega) \vdash (p, \omega) \iff \delta(q, a) = p$$

> [!definition] Secuencia de configuraciones (por inducción)
> - **Base:** si $I$ es una configuración instantánea, $I \vdash^{*} I$ es una secuencia válida.
> - **Paso inductivo:** $I \vdash^{*} J$ es válida si existe una configuración $K$ tal que $I \vdash K$ y $K \vdash^{*} J$.

> [!example]
> $$(q_0, \text{"001"}) \vdash (q_1, \text{"01"}) \vdash (q_2, \text{"1"}) \vdash (q_3, \lambda)$$
> Es decir, $(q_0, \text{"001"}) \vdash^{*} (q_3, \lambda)$.

### Lenguaje aceptado por un AFD

> [!definition] Lenguaje de un AFD
> $$L(M) = \{ \omega \in \Sigma^{*} : \hat{\delta}(q_0, \omega) \in F \}$$
> Equivalentemente:
> $$L(M) = \{ \omega \in \Sigma^{*} : (q_0, \omega) \vdash^{*} (p, \lambda),\ p \in F \}$$

> [!theorem] Determinismo
> Dada una palabra $\omega \in \Sigma^{*}$ y un AFD, sólo hay **una** secuencia de configuraciones $(q_0, \omega) \vdash \dots \vdash (q_{\text{final}}, \lambda)$. (Se demuestra por inducción en la longitud de $\omega$ y contradicción.)

> [!definition] Equivalencia de autómatas
> Dos AFD $M$ y $M'$ son **equivalentes** si y sólo si $L(M) = L(M')$; es decir, reconocen el mismo lenguaje.

## AFD Mínimo

### Estados accesibles

> [!definition] Estado accesible
> Un estado $q_i \in Q$ es **accesible** si:
> $$\exists\, \omega \in \Sigma^{*} : \hat{\delta}(q_0, \omega) = q_i$$
> equivalentemente, si $(q_0, \omega) \xrightarrow{*} (q_i, \lambda)$.

> [!note] Construcción inductiva del conjunto de estados accesibles
> - **Base:** el conjunto $Q' = \{q_0\}$ es accesible, ya que $\hat{\delta}(q_0, \lambda) = q_0$.
> - **Paso inductivo:** si $S \subseteq Q$ es un conjunto de estados accesibles, para cada $a \in \Sigma$ y $q_i \in S$, el conjunto $S' = \{ q_j \in Q : \delta(q_i, a) = q_j \}$ es de estados accesibles.

### Estados equivalentes o indistinguibles

> [!definition] Estados indistinguibles
> Los estados $p$ y $q$ son **indistinguibles** si para toda cadena $\omega$, $\hat{\delta}(p, \omega)$ es de aceptación si y sólo si $\hat{\delta}(q, \omega)$ lo es:
> $$\forall \omega \in \Sigma^{*} : \hat{\delta}(p, \omega) \in F \iff \hat{\delta}(q, \omega) \in F$$
>
> Los estados $p$ y $q$ son **distinguibles** si existe al menos una cadena $\omega$ tal que $\hat{\delta}(p, \omega)$ es de aceptación y $\hat{\delta}(q, \omega)$ no lo es (o viceversa).

> [!note] Algoritmo para detectar estados distinguibles
> - **Base:** si $p$ es un estado de aceptación y $q$ no lo es, el par $\{p, q\}$ es distinguible (existe la cadena $\lambda$ que los distingue).
> - **Paso inductivo:** si para alguna entrada $a$ se tiene $\delta(p, a) = r$ y $\delta(q, a) = s$, y $\{r, s\}$ son distinguibles, entonces $\{p, q\}$ son distinguibles.

> [!theorem] La indistinguibilidad es una relación de equivalencia
> - **Reflexiva:** $p$ es indistinguible de $p$.
> - **Simétrica:** si $p$ es indistinguible de $q$, entonces $q$ lo es de $p$.
> - **Transitiva:** si $\{p,q\}$ y $\{q,r\}$ son indistinguibles, entonces $\{p,r\}$ también.
>
> *Demostración de la transitividad (por absurdo):* supongamos que $\{p,r\}$ fueran distinguibles; entonces existe $\omega$ tal que $\hat{\delta}(p,\omega)$ es de aceptación y $\hat{\delta}(r,\omega)$ no (o viceversa). Analizando $\hat{\delta}(q,\omega)$: si es de aceptación, $\{q,r\}$ sería distinguible; si no lo es, $\{p,q\}$ sería distinguible. En ambos casos se contradice la hipótesis. Absurdo.

### Indistinguibilidad de orden $k$

La **indistinguibilidad de orden $k$** considera palabras de una misma longitud $k$. Es una relación de equivalencia y determina una partición del conjunto de estados en clases de equivalencia. Sea $E_k$ dicha relación.

> [!theorem] Lema base
> $$\frac{Q}{E_0} = \{ F,\ Q - F \}$$
> Si consideramos palabras de longitud $0$: $\hat{\delta}(p, \lambda) \in F \iff \hat{\delta}(q, \lambda) \in F$, o sea $p \in F \iff q \in F$.

> [!theorem] Lema del paso inductivo
> Dado un autómata y dos estados $p, q \in Q$:
> $$\big(\forall a \in \Sigma : \delta(p, a)\, E_n\, \delta(q, a)\big) \implies p\, E_{n+1}\, q$$

### Algoritmo de construcción del conjunto cociente

> [!note] Algoritmo · conjunto cociente $Q / E$
> **Entrada:** $Q$. **Salida:** conjunto cociente $Q / E$.
> 1. $\dfrac{Q}{E_0} = \{ F,\ Q - F \}$
> 2. Generar $\dfrac{Q}{E_{i+1}}$ a partir de $\dfrac{Q}{E_i}$: $p$ y $q$ pertenecen a la misma clase en $\dfrac{Q}{E_{i+1}}$ $\iff$
>     - $p$ y $q$ están en la misma clase en $\dfrac{Q}{E_i}$, **y**
>     - $\forall a \in \Sigma$, $\delta(p, a)$ y $\delta(q, a)$ están en la misma clase en $\dfrac{Q}{E_i}$.
> 3. Si $\dfrac{Q}{E_{i+1}} = \dfrac{Q}{E_i}$, entonces $\dfrac{Q}{E} = \dfrac{Q}{E_i}$. Si no, volver al paso 2.

> [!example] Ejemplo
> $A = (\{p, r, q, s, t\}, \{0,1\}, \delta, p, \{s, t\})$
>
> | $\delta$ | $0$ | $1$ |
> |----------|-----|-----|
> | $p$ | $r$ | $q$ |
> | $r$ | $q$ | $*s$ |
> | $q$ | $q$ | $*t$ |
> | $*s$ | $*s$ | $*s$ |
> | $*t$ | $*t$ | $*t$ |
>
> $\dfrac{Q}{E_0} = \{ \{s, t\},\ \{p, r, q\} \}$
>
> Analizando transiciones (las de $s,t$ van a estados finales; las de $p,r,q$ mezclan finales y no finales, pero se mantienen juntas porque sus imágenes caen en las mismas clases):
> $$\frac{Q}{E_1} = \{ \{s, t\},\ \{p, r, q\} \} \qquad \frac{Q}{E_2} = \{ \{s, t\},\ \{p, r, q\} \}$$
> Como $\dfrac{Q}{E_2} = \dfrac{Q}{E_1}$, el algoritmo termina:
> $$\frac{Q}{E} = \{ \{s, t\},\ \{p, r, q\} \}$$

### Algoritmo de construcción del AFD mínimo

> [!note] Algoritmo · AFD mínimo
> **Entrada:** $A = (Q, \Sigma, \delta, q_0, F)$. **Salida:** $A' = (Q', \Sigma, \delta', q_0', F')$ equivalente con mínima cantidad de estados.
> 1. Eliminar estados **inaccesibles** desde $q_0$.
> 2. Construir el conjunto cociente $Q / E$.
> 3. Definir $A' = (Q', \Sigma, \delta', q_0', F')$ donde:
>     - $Q' = Q / E$
>     - $q_0'$ es la clase donde está $q_0$.
>     - $F' = \{ \bar{s} \in Q/E : \exists\, p \in \bar{s} \text{ tal que } p \in F \}$ (las clases que contienen estados finales).
>     - $\delta'(\bar{s_i}, a) = \bar{s_j} \iff \exists\, p \in \bar{s_i},\, q \in \bar{s_j} : \delta(p, a) = q$

> [!example] AFD mínimo del ejemplo anterior
> $Q' = \{ S, P, Q \}$ con $S = \{s, t\}$, $P = \{p\}$, $Q = \{r, q\}$; $q_0' = P$; $F' = \{S\}$.
>
> | $\delta'$ | $0$ | $1$ |
> |-----------|-----|-----|
> | $P$ | $Q$ | $Q$ |
> | $Q$ | $Q$ | $*S$ |
> | $*S$ | $*S$ | $*S$ |

> [!theorem] Teorema de minimalidad
> El autómata $A'$ obtenido con el algoritmo es **equivalente** a $A$ y es **mínimo** (su número de estados es menor o igual que el de cualquier otro AFD equivalente a $A$).
>
> *Idea de la demostración:* cada transición $\delta(p, x) = q$ de $A$ se corresponde con la equivalente $\delta'(P, x) = Q$ (con $p \in P$, $q \in Q$), de modo que $A$ y $A'$ aceptan las mismas palabras. Si existiera un $A'$ equivalente con menos estados, dos palabras $\omega$ y $\alpha$ que llevan a estados **distinguibles** $p, q$ de $A$ llevarían al mismo estado $r$ de $A'$; pero entonces $A'$ aceptaría ambas o rechazaría ambas, contradiciendo que $A$ las distingue. Absurdo.
>
> El **AFD mínimo es único**, salvo por un posible cambio de nombre de los estados.

## Autómatas Finitos No Determinísticos · AFND

> [!definition] Función de transición de un AFND
> $$\delta : Q \times \Sigma \to \mathcal{P}(Q)$$
> donde $\mathcal{P}(Q)$ denota todos los subconjuntos de $Q$. A cada par (estado, símbolo) le corresponde un **conjunto** de estados.

> [!definition] $\hat{\delta}$ para un AFND (por inducción)
> - **Base:** $\hat{\delta}(q, \lambda) = \{q\}$
> - **Paso inductivo:** dada $\omega = \omega' a$, si $\hat{\delta}(q, \omega') = \{p_1, p_2, \dots, p_k\}$ y $\bigcup_{i=1}^{k} \delta(p_i, a) = \{r_1, r_2, \dots, r_m\}$, entonces:
> $$\hat{\delta}(q, \omega) = \hat{\delta}(q, \omega' a) = \{r_1, r_2, \dots, r_m\}$$

> [!definition] Secuencia de configuraciones y lenguaje
> $$(q, a\omega) \vdash (p, \omega) \iff p \in \delta(q, a)$$
> $$L(M) = \{ \omega \in \Sigma^{*} : \hat{\delta}(q_0, \omega) \cap F \neq \varnothing \}$$

> [!example]
> $M = (\{q_0, q_1, q_2\}, \{0,1\}, \delta, q_0, \{q_2\})$. Se tiene $\hat{\delta}(q_0, 00101) = \{q_0, q_2\}$. Como $\{q_0, q_2\} \cap \{q_2\} \neq \varnothing$, entonces $00101 \in L(M)$.

## Equivalencia entre AFD y AFND · construcción de subconjuntos

> [!theorem] Equivalencia
> Todo lenguaje que puede ser reconocido por un AFND puede ser reconocido por un AFD, y viceversa.

> [!definition] Construcción de subconjuntos
> Sea $N = (Q_N, \Sigma, \delta_N, q_0, F_N)$ un AFND. Se define el AFD $D = (Q_D, \Sigma, \delta_D, \{q_0\}, F_D)$ donde:
> - $Q_D = \mathcal{P}(Q_N)$
> - $F_D = \{ S \subseteq Q_N : S \cap F_N \neq \varnothing \}$
> - $\forall a \in \Sigma,\ \forall S \subseteq Q_N :\ \delta_D(S, a) = \bigcup_{p \in S} \delta_N(p, a)$

> [!note] Construcción "perezosa" (lazy) · sólo estados accesibles
> **Entrada:** $\mathcal{P}(Q_N)$ y $Q_D = \varnothing$. **Salida:** $Q_D$ con sólo estados accesibles.
> 1. Agregar $\{q_0\}$ a $Q_D$.
> 2. $\forall a \in \Sigma,\ \forall S \in Q_D$, si $\delta_D(S, a) \notin Q_D$, agregar $\delta_D(S, a)$ a $Q_D$.

> [!theorem] $L(D) = L(N)$
> *Demostración:* se prueba por inducción en la longitud de $\omega$ que $\hat{\delta}_D(\{q_0\}, \omega) = \hat{\delta}_N(q_0, \omega)$.
> - **Base:** $\omega = \lambda$. $\hat{\delta}_D(\{q_0\}, \lambda) = \{q_0\}$ y $\hat{\delta}_N(q_0, \lambda) = \{q_0\}$.
> - **Paso inductivo:** $\omega = \alpha t$. Por hipótesis $\hat{\delta}_D(\{q_0\}, \alpha) = \hat{\delta}_N(q_0, \alpha) = \{p_1,\dots,p_k\}$. Entonces $\hat{\delta}_N(q_0, \alpha t) = \bigcup_{i=1}^{k} \delta_N(p_i, t)$ y, por la construcción, $\hat{\delta}_D(\{q_0\}, \alpha t) = \delta_D(\{p_1,\dots,p_k\}, t) = \bigcup_{i=1}^{k} \delta_N(p_i, t)$, que coinciden.
>
> De aquí, $\omega \in L(N) \iff \hat{\delta}_N(q_0, \omega) \cap F_N \neq \varnothing \iff \hat{\delta}_D(\{q_0\}, \omega) \in F_D \iff \omega \in L(D)$.

## AFND con transiciones λ · AFND-λ

> [!definition] Función de transición de un AFND-λ
> $$\delta : Q \times (\Sigma \cup \{\lambda\}) \to \mathcal{P}(Q)$$
> Se pueden tener transiciones en las que **no se consume ningún símbolo** de la entrada.

> [!definition] Clausura-λ de un estado
> De manera informal, la **clausura respecto de $\lambda$** de un estado $q$ es el conjunto de todos los estados a los que se puede llegar desde $q$ siguiendo cualquier camino cuyos arcos estén etiquetados con $\lambda$.
> - **Base:** $q \in \text{claus}(q)$
> - **Paso inductivo:** si $p \in \text{claus}(q)$ y $r \in \delta(p, \lambda)$, entonces $r \in \text{claus}(q)$

> [!example] Cálculo de clausuras-λ
> $M = (\{p, q, r, s\}, \{a, b\}, \delta, p, \{p, s\})$
>
> | $\delta$ | $a$ | $b$ | $\lambda$ |
> |----------|-----|-----|-----------|
> | $*p$ | $\{q\}$ | | |
> | $q$ | $\{q, r, s\}$ | $\{p, r\}$ | $\{s\}$ |
> | $r$ | | $\{p, s\}$ | $\{r, s\}$ |
> | $*s$ | | | $\{r\}$ |
>
> $$\text{claus}(p) = \{p\} \quad \text{claus}(q) = \{q, s, r\} \quad \text{claus}(r) = \{r, s\} \quad \text{claus}(s) = \{s, r\}$$

> [!definition] $\hat{\delta}$ para un AFND-λ (por inducción)
> - **Base:** $\hat{\delta}(q, \lambda) = \text{claus}(q)$
> - **Paso inductivo:** dada $\omega = \omega' a$, si $\hat{\delta}(q, \omega') = \{p_1, \dots, p_k\}$ y $\bigcup_{i=1}^{k} \delta(p_i, a) = \{r_1, \dots, r_m\}$, entonces:
> $$\hat{\delta}(q, \omega) = \bigcup_{j=1}^{m} \text{claus}(r_j)$$

> [!definition] Lenguaje de un AFND-λ
> $$L(M) = \{ \omega \in \Sigma^{*} : \hat{\delta}(q_0, \omega) \cap F \neq \varnothing \}$$
> **Ejemplo:** $\hat{\delta}(p, \text{"}aab\text{"}) = \{p, r, s\}$; como $\{p,r,s\} \cap \{p,s\} \neq \varnothing$, entonces $aab \in L(M)$.

### Eliminación de las transiciones λ

> [!definition] Construcción del AFD equivalente
> Sea $E = (Q_E, \Sigma, \delta_E, q_0, F_E)$ un AFND-λ. El AFD $D = (Q_D, \Sigma, \delta_D, q_D, F_D)$ se define así:
> - $Q_D$ = conjuntos $S \subseteq Q_E$ tales que $S = \text{claus}(S)$.
> - $q_D = \text{claus}(q_0)$
> - $F_D$ = todos los conjuntos que contienen al menos un estado de aceptación de $E$.
> - $\delta_D(S, a)$ para todo $a \in \Sigma$ y todo $S \in Q_D$: siendo $S = \{p_1, \dots, p_k\}$, se calcula $\bigcup_{i=1}^{k} \delta(p_i, a) = \{r_1, \dots, r_m\}$ y luego $\delta_D(S, a) = \bigcup_{j=1}^{m} \text{claus}(r_j)$.

> [!example] Resultado de la construcción sobre $M$
> | $\delta_D$ | $a$ | $b$ |
> |------------|-----|-----|
> | $\to \{p\}$ | $\{q, r, s\}$ | $\varnothing$ |
> | $\{q, r, s\}$ | $\{q, r, s\}$ | $\{p, r, s\}$ |
> | $\{p, r, s\}$ | $\{q, r, s\}$ | $\{p, r, s\}$ |
>
> $Q_D = \{ \{p\}, \{q, r, s\}, \varnothing, \{p, r, s\} \}$, con $F_D = \{ \{p\}, \{q, r, s\}, \{p, r, s\} \}$.

> [!theorem] $L$ es aceptado por un AFND-λ $\iff$ $L$ es aceptado por un AFD
> **($\Leftarrow$)** Si $L$ es aceptado por un AFD $D$, se transforma en AFND-λ añadiendo, para cada $q$, $\delta_E(q, \lambda) = \varnothing$ y conservando $\delta_E(q, a) = \{\delta_D(q, a)\}$. Como las transiciones no cambian, toda palabra aceptada por $D$ lo es por $E$.
>
> **($\Rightarrow$)** Si $L$ es aceptado por un AFND-λ $E$, se aplica la construcción anterior para obtener el AFD $D$. Se prueba por inducción en $|\omega|$ que $\hat{\delta}_E(q_0, \omega) = \hat{\delta}_D(q_D, \omega)$:
> - **Base:** $\omega = \lambda$: $\hat{\delta}_E(q_0, \lambda) = \text{claus}(q_0) = q_D = \hat{\delta}_D(q_D, \lambda)$.
> - **Paso inductivo:** $\omega = \alpha t$; por hipótesis $\hat{\delta}_E(q_0, \alpha) = \hat{\delta}_D(q_D, \alpha) = \{p_1, \dots, p_k\}$, y ambas definiciones producen $\bigcup_{j=1}^{m}\text{claus}(r_j)$ con $\{r_1,\dots,r_m\} = \bigcup_{i=1}^{k}\delta_E(p_i, t)$. Por lo tanto coinciden.

---
*Anterior ← [[1 - Introducción]] · Continúa en → [[3 - Expresiones Regulares]]*
