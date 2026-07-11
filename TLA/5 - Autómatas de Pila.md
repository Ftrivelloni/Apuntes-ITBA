---
tema: 5
titulo: Autómatas de Pila
materia: Autómatas, Teoría de Lenguajes y Compiladores
autor: Lic. Ana María Arias Roig
tags:
  - TLA
  - autómatas-de-pila
  - AP
  - APD
  - lenguajes-libres-de-contexto
---

# 5 · Autómatas de Pila

> [!abstract] Índice del tema
> - [[#Definición general]]
> - [[#Configuración o descripción del autómata]]
> - [[#Lenguaje aceptado por un Autómata de Pila]]
> - [[#Equivalencia entre aceptación por pila vacía y por estado final]]
> - [[#Autómata de Pila Determinístico · APD]]

## Definición general

> [!definition] Autómata de pila (AP)
> Es una **séptupla** $AP = (\Sigma, \Gamma, Q, S, q_0, \delta, F)$ donde:
> - $\Sigma$: alfabeto de **entrada**.
> - $\Gamma$: alfabeto de **pila**.
> - $Q$: conjunto finito de **estados**.
> - $S \in \Gamma$: **símbolo inicial de la pila** (un único símbolo).
> - $q_0 \in Q$: **estado inicial**.
> - $F \subseteq Q$: conjunto de **estados finales**.
> - $\delta$: **función de transición**
> $$\delta : Q \times (\Sigma \cup \{\lambda\}) \times \Gamma \to \mathcal{P}(Q \times \Gamma^{*})$$
> donde $\mathcal{P}(Q \times \Gamma^{*})$ denota todos los subconjuntos de $Q \times \Gamma^{*}$.

> [!example] Ejemplo
> $A = (\{q_0, q_1, q_2, q_3, q_f\}, \{a, b, c\}, \{z_0, A, D\}, \delta, q_0, z_0, \{q_f\})$
>
> $$\begin{aligned}
> &\delta(q_0, a, z_0) = \{(q_1, A z_0)\} & &\delta(q_2, a, D) = \{(q_1, AD)\} \\
> &\delta(q_0, b, z_0) = \{(q_0, z_0)\}   & &\delta(q_2, b, D) = \{(q_2, D)\} \\
> &\delta(q_1, a, A) = \{(q_2, D)\}       & &\delta(q_2, c, D) = \{(q_3, D)\} \\
> &\delta(q_1, b, A) = \{(q_1, A)\}       & &\delta(q_3, a, D) = \{(q_3, D)\} \\
> &\delta(q_3, a, z_0) = \{(q_3, z_0)\}   & &\delta(q_3, b, D) = \{(q_3, \lambda)\} \\
> &\delta(q_3, \lambda, z_0) = \{(q_f, \lambda)\}
> \end{aligned}$$

## Configuración o descripción del autómata

> [!definition] Configuración instantánea
> Es una descripción del AP en un momento dado. Se denota con una **terna** $(q, \omega, \alpha) \in Q \times \Sigma^{*} \times \Gamma^{*}$:
> - $q$: estado actual.
> - $\omega$: cadena que falta consumir.
> - $\alpha$: contenido actual de la pila.
>
> Si $\omega = \lambda$, no queda nada más para analizar.

> [!definition] Configuración inicial
> $$(q_0, \omega, S)$$
> Estado inicial, al inicio de la palabra completa, con el símbolo inicial de pila $S$ en la pila.

> [!definition] Secuencia de configuraciones
> El símbolo $\vdash$ indica el **movimiento válido**:
> $$(q, a\omega, Z\alpha) \vdash (r, \omega, \beta\alpha) \iff (r, \beta) \in \delta(q, a, Z)$$
> con $a \in \Sigma$, $Z \in \Gamma$, $\omega \in \Sigma^{*}$, $\alpha, \beta \in \Gamma^{*}$. También, con transiciones-λ:
> $$(q, \omega, Z\alpha) \vdash (r, \omega, \beta\alpha) \iff (r, \beta) \in \delta(q, \lambda, Z)$$
>
> En cada transición **sólo se puede consultar el tope de la pila** (lo que implica extraerlo). Luego puede agregarse un elemento, muchos o ninguno.

## Lenguaje aceptado por un Autómata de Pila

> [!definition] Aceptación por estado final
> El AP acepta $\omega$ por estado final si desde la configuración inicial llega a un estado final al consumir la entrada:
> $$L_{pf}(A) = \{ \omega \in \Sigma^{*} \mid (q_0, \omega, S) \vdash^{*} (q_f, \lambda, \alpha) \}$$

> [!definition] Aceptación por pila vacía
> El AP acepta $\omega$ por pila vacía si, tras leer toda la cadena, llega a un estado con la pila vacía (sin importar el tipo de estado):
> $$L_{pv}(A) = \{ \omega \in \Sigma^{*} \mid (q_0, \omega, S) \vdash^{*} (p, \lambda, \lambda) \}$$

> [!example] Reconocimiento de $aacb$
> $$(q_0, aacb, z_0) \vdash (q_1, acb, A z_0) \vdash (q_2, cb, D z_0) \vdash (q_3, b, D z_0) \vdash (q_3, \lambda, z_0) \vdash (q_f, \lambda, \lambda)$$
> El autómata reconoce $aacb$ **tanto por pila vacía como por estado final**.

## Equivalencia entre aceptación por pila vacía y por estado final

> [!important]
> Un lenguaje $L$ tiene un AP que lo acepta por **estado final** si y sólo si tiene un AP que lo acepta por **pila vacía**.
>
> **Ojo:** el autómata no es necesariamente el mismo. Dado un AP, el lenguaje que reconoce por pila vacía en general **no** coincide con el que reconoce por estado final.

> [!theorem] De pila vacía a estado final
> Si $L = L_{pv}(P_v)$ para $P_v = (Q, \Sigma, \Gamma, \delta_v, q_0, S)$, existe $P_f$ con $L = L_{pf}(P_f)$.
>
> *Construcción:* $P_f = (Q \cup \{p_0, p_f\}, \Sigma, \Gamma \cup \{T\}, \delta_f, p_0, T, \{p_f\})$ con:
> 1. $\delta_f(p_0, \lambda, T) = \{(q_0, ST)\}$ — se coloca el símbolo inicial $S$ sobre un nuevo fondo $T$.
> 2. $\forall q \in Q, a \in \Sigma \cup \{\lambda\}, Y \in \Gamma :\ \delta_f(q, a, Y) = \delta_v(q, a, Y)$ — simula $P_v$.
> 3. $\forall q \in Q :\ \delta_f(q, \lambda, T) = \{(p_f, \lambda)\}$ — al quedar $T$ expuesto (pila de $P_v$ vacía), va al final.
>
> *Verificación:* $(p_0, \omega, T) \vdash (q_0, \omega, ST) \vdash^{*} (q, \lambda, T) \vdash (p_f, \lambda, \lambda)$. Las reglas 1 y 3 sólo pueden usarse al principio y al final respectivamente, por lo que $L(P_f)$ contiene exactamente las cadenas de $L_{pv}(P_v)$.

> [!theorem] De estado final a pila vacía
> Si $L = L_{pf}(P_f)$ para $P_f = (Q, \Sigma, \Gamma, \delta_f, q_0, S, F)$, existe $P_v$ con $L = L_{pv}(P_v)$.
>
> *Construcción:* $P_v = (Q \cup \{p_0, p\}, \Sigma, \Gamma \cup \{T\}, \delta_v, p_0, T)$ con:
> 1. $\delta_v(p_0, \lambda, T) = \{(q_0, ST)\}$
> 2. $\forall q \in Q, a \in \Sigma \cup \{\lambda\}, Y \in \Gamma :\ \delta_v(q, a, Y) = \delta_f(q, a, Y)$ — simula $P_f$.
> 3. $\forall q_f \in F, Y \in \Gamma \cup \{T\} :\ \delta_v(q_f, \lambda, Y) = \{(p, \lambda)\}$
> 4. $\forall Y \in \Gamma \cup \{T\} :\ \delta_v(p, \lambda, Y) = \{(p, \lambda)\}$ — el estado $p$ vacía la pila sin consumir entrada.

## Autómata de Pila Determinístico · APD

Los **APD** son importantes porque los **analizadores sintácticos** se comportan como autómatas de pila deterministas, y definen los tipos de construcciones utilizables en lenguajes de programación. Ver [[7 - Análisis Sintáctico]].

> [!definition] APD
> Un AP $(Q, \Sigma, \Gamma, \delta, q_0, z_0, F)$ es **determinista** si:
> 1. $\forall q \in Q, a \in \Sigma \cup \{\lambda\}, X \in \Gamma :\ \delta(q, a, X)$ tiene **a lo sumo un** elemento.
> 2. Si $\delta(q, a, X) \neq \varnothing$ para algún $a \in \Sigma$, entonces $\delta(q, \lambda, X) = \varnothing$ (no hay conflicto entre movimiento con entrada y movimiento-λ).

> [!theorem] Lenguajes regulares y APD
> Todos los lenguajes regulares pueden ser aceptados por un APD.
>
> *Construcción:* dado un AFD $A = (Q, \Sigma, \delta_A, q_0, F)$, se construye el APD $P = (Q, \Sigma, \{Z_0\}, \delta_P, q_0, Z_0, F)$ con $\delta_P(q, a, Z_0) = \{(p, Z_0)\}$ cuando $\delta_A(q, a) = p$. La pila nunca cambia; se prueba por inducción en $|\omega|$ que $L(A) = L(P)$.

> [!example] Lenguajes no regulares y APD
> Un APD **puede** reconocer lenguajes no regulares. Ejemplo: $L = \{\alpha c\, \alpha^{R} \mid \alpha \in \{a, b\}^{*}\}$ (palíndromos con marca central $c$) es reconocido por un APD.
>
> En cambio, $L = \{\alpha \alpha^{R} \mid \alpha \in \{a, b\}^{*}\}$ (sin marca central) **no** puede ser reconocido por un APD, aunque sí por un AP (no determinista).

> [!summary] Relación de clases
> Existen **lenguajes libres de contexto** que pueden reconocerse por un **AP** (no determinista) pero **no** por un **APD**. Por lo tanto:
> $$\text{Lenguajes regulares} \subset \text{Lenguajes reconocidos por APD} \subset \text{Lenguajes libres de contexto (AP)}$$

---
*Anterior ← [[4 - Lenguajes Regulares]] · Continúa en → [[6 - Gramáticas Libres de Contexto y Lema de Bombeo]]*
