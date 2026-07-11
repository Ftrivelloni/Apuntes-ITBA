---
tema: 9
titulo: Máquinas de Turing
materia: Autómatas, Teoría de Lenguajes y Compiladores
autor: Lic. Ana María Arias Roig
tags:
  - TLA
  - máquinas-de-turing
  - computabilidad
  - church-turing
  - recursivamente-enumerables
  - decidibilidad
---

# 9 · Máquinas de Turing

> [!abstract] Índice del tema
> - [[#Introducción]]
> - [[#Definición general]]
> - [[#Configuración instantánea y movimientos]]
> - [[#Lenguaje aceptado por una MT]]
> - [[#Aceptación por parada]]
> - [[#Extensiones de la Máquina de Turing]]
> - [[#Autómatas Acotados Linealmente · AAL]]
> - [[#Funciones Recursivas Parciales]]
> - [[#Máquina de Turing Universal]]
> - [[#Hipótesis de Church-Turing]]
> - [[#Tipos de problemas]]
> - [[#Resumen · Lenguajes, gramáticas y máquinas]]

## Introducción

> [!note] Componentes de una MT
> - **Unidad de control** en uno de un conjunto finito de estados.
> - **Cinta** dividida en casillas, infinita hacia izquierda y derecha; cada casilla contiene un símbolo. Las casillas fuera de la entrada contienen el **espacio en blanco** (símbolo de cinta, **no** de entrada).
> - **Cabeza de cinta** (cursor) sobre una casilla. Inicialmente, en la casilla más a la izquierda de la entrada.
>
> En cada **movimiento**, la MT: (1) **cambia de estado** (quizá el mismo); (2) **escribe** un símbolo de cinta en la casilla actual; (3) **mueve** la cabeza a izquierda o derecha.

## Definición general

> [!definition] Máquina de Turing (MT)
> Es una tupla $MT = (Q, \Sigma, \Gamma, \delta, q_0, B, F)$ donde:
> - $Q$: conjunto finito de **estados**.
> - $\Sigma$: alfabeto de **entrada** ($\Sigma \subseteq \Gamma$).
> - $\Gamma$: alfabeto de **cinta**.
> - $\delta$: **función de transición** $\delta : Q \times \Gamma \to Q \times \Gamma \times \{I, D\}$.
> - $q_0 \in Q$: **estado inicial**.
> - $B$: símbolo de **espacio en blanco** ($B \in \Gamma$, $B \notin \Sigma$).
> - $F \subseteq Q$: conjunto de **estados finales**.

> [!definition] Función de transición
> $$\delta(q, X) = (p, Y, \text{Sentido})$$
> Dados un estado $q$ y un símbolo de cinta $X$: $p$ es el nuevo estado, $Y$ el símbolo que se **escribe**, y **Sentido** $\in \{I, D\}$ el movimiento del cabezal (izquierda o derecha). A cada par (estado, símbolo) le corresponde **uno y sólo un** resultado. La función **puede estar indefinida** para algunos argumentos.

## Configuración instantánea y movimientos

> [!definition] Configuración instantánea
> Se denota $\alpha_1\, q\, \alpha_2$, donde $q$ es el estado actual, $\alpha_1 \in \Gamma^{*}$ es el contenido de la cinta **a la izquierda** del cursor (sin la celda del cursor) y $\alpha_2 \in \Gamma^{*}$ es el contenido **a la derecha** (incluyendo la celda del cursor).

> [!note] Movimiento a izquierda · $\delta(q, X_i) = (p, Y, I)$
> $$X_1 \dots X_{i-1}\, q X_i\, X_{i+1} \dots X_n \vdash_M X_1 \dots X_{i-2}\, p X_{i-1}\, Y X_{i+1} \dots X_n$$
> **Excepciones:**
> - Si $i = 1$: la máquina se mueve al blanco a la izquierda: $q X_1 \dots X_n \vdash_M p\, B Y X_2 \dots X_n$.
> - Si $i = n$ e $Y = B$: el $B$ escrito se une a los blancos finales y no aparece: $X_1 \dots X_{n-1}\, q X_n \vdash X_1 \dots X_{n-2}\, p X_{n-1}$.

> [!note] Movimiento a derecha · $\delta(q, X_i) = (p, Y, D)$
> $$X_1 \dots X_{i-1}\, q X_i\, X_{i+1} \dots X_n \vdash_M X_1 \dots X_{i-1}\, Y\, p X_{i+1} \dots X_n$$
> **Excepciones:**
> - Si $i = n$: la casilla $i+1$ contiene un blanco: $X_1 \dots X_{n-1}\, q X_n \vdash_M X_1 \dots X_{n-1}\, Y\, p B$.
> - Si $i = 1$ e $Y = B$: el $B$ se une a los blancos iniciales: $q X_1 \dots X_n \vdash p X_2 \dots X_n$.

## Lenguaje aceptado por una MT

> [!definition] Lenguaje de una MT
> $$L(M) = \{ \omega \in \Sigma^{*} : q_0 \omega \vdash^{*} \alpha\, p\, \beta,\ p \in F \}$$

> [!example] $L = \{0^{n}1^{n} : n > 0\}$
> $M = (\{q_0, q_1, q_2, q_3, q_4\}, \{0, 1\}, \{0, 1, X, Y, B\}, \delta, q_0, B, \{q_4\})$.
>
> **Acepta $0011$:**
> $$q_0 0011 \vdash X q_1 011 \vdash X0 q_1 11 \vdash X q_2 0Y1 \vdash q_2 X0Y1 \vdash X q_0 0Y1 \vdash XX q_1 Y1 \vdash XXY q_1 1$$
> $$\vdash XX q_2 YY \vdash X q_2 XYY \vdash XX q_0 YY \vdash XXY q_3 Y \vdash XXYY q_3 B \vdash XXYYB q_4 B$$
>
> **No acepta $0010$:** llega a $XXY0 q_1 B$ donde $\delta(q_1, B)$ **no está definida**, y la máquina se detiene sin aceptar.

## Aceptación por parada

> [!definition] Aceptación por parada
> Una MT **se detiene** cuando no tiene movimiento: en estado $q$ apuntando a $X$, $\delta(q, X)$ no está definida. Se asume que una MT **siempre se detiene** en un estado de aceptación.
>
> Para decidir la pertenencia:
> - M se detiene en estado **final** $\Rightarrow \omega \in L(M)$.
> - M se detiene en estado **no final** $\Rightarrow \omega \notin L(M)$.
> - M **no se detiene** $\Rightarrow \omega \notin L(M)$.

> [!important] Recursivamente enumerables vs. recursivos
> El conjunto de lenguajes aceptados por una MT son los **lenguajes recursivamente enumerables**.
>
> Si $L$ es un lenguaje de **tipo 0 recursivo**, existe una MT que: si $\omega \in L$ se detiene aceptando, y si $\omega \notin L$ se detiene **rechazando** (siempre para).
>
> - **Recursivo** = **decidible** (existe una función recursiva que siempre termina).
> - **Enumerable**: sus cadenas pueden ser **enumeradas** (listadas) por una MT en cierto orden.

## Extensiones de la Máquina de Turing

> [!note] Cinta infinita en una sola dirección
> $L$ es reconocido por una MT con cinta infinita en **ambas** direcciones **si y sólo si** lo es por una MT con cinta infinita en **una sola** dirección.

> [!note] MT con varias cintas
> Tiene $k$ cintas independientes. Inicialmente la entrada va en la primera cinta (las demás en blanco); las cabezas de las cintas extra apuntan a casillas arbitrarias. En cada movimiento cambia de estado, escribe en cada cinta y mueve cada cabeza a izquierda, derecha o **no se mueve** (S). La función:
> $$\delta : Q \times \Gamma^{k} \to Q \times (\Gamma \times \{I, D, S\})^{k}$$
> $L$ es reconocido por una MT de **varias cintas** si y sólo si lo es por una MT de **una sola cinta**.

> [!note] MT No determinista
> La función $\delta$ devuelve un **conjunto** de tuplas para cada $(q, X)$. Si $L$ es reconocido por una MT **no determinista**, entonces lo es por una MT **determinista**.

## Autómatas Acotados Linealmente · AAL

> [!definition] AAL
> Un **Autómata Acotado Linealmente** es una MT **no determinista** que usa una cinta de longitud **finita**, función lineal de la longitud de la entrada. Tupla $AAL = (Q, \Sigma, \Gamma, \delta, q_0, B, F)$ donde $\Sigma$ contiene dos símbolos especiales, **#** y **\$** (marcadores izquierdo y derecho), inicialmente en los extremos de la entrada, que impiden que la cabeza abandone la zona de entrada.

> [!theorem] Lenguaje aceptado por un AAL
> Si $G$ es una gramática de **tipo 1** (sensible al contexto), $G = (V, \Sigma, P, S)$, entonces existe un AAL que acepta $L(G)$.

## Funciones Recursivas Parciales

> [!note] MT como computadora de funciones $\mathbb{N} \to \mathbb{N}$
> Los enteros se representan en **unario**: $i \ge 0$ es $1^{i}$. Con $k$ argumentos $i_1, \dots, i_k$ se colocan en la cinta separados por $0$ (u otro símbolo). Si la MT se detiene con la cinta $1^{M}$, entonces $f(i_1, \dots, i_k) = M$.
>
> **Ejemplo:** $f(x, y) = x + y$; $f(2, 4)$ se representa $11\,0\,1111$ (o $11*1111$) y al detenerse apunta a $111111$, pues $f(2,4) = 6$.

> [!definition] Total vs. parcial
> - Si $f(i_1, \dots, i_k)$ está definida para **toda** tupla, $f$ es una **función recursiva total**.
> - Una función computada por una MT es una **función recursiva parcial**.
> - La multiplicación, $n!$, $2^{n}$, etc. son funciones recursivas **totales**.

## Máquina de Turing Universal

> [!definition] MTU
> Es una MT capaz de **simular** el procesamiento de cualquier otra MT. Recibe como entrada una MT $M$ válida codificada en binario y una entrada también en binario, y determina si esa entrada es aceptada por $M$. Consta de **3 cintas**:
> 1. Programa de $M$ y cadena de entrada (luego la salida).
> 2. Área de trabajo.
> 3. Estado actual de la máquina simulada.

> [!note] Funcionamiento de la MTU
> 1. Copia la entrada de la cinta 1 a la cinta 2.
> 2. Graba el estado inicial en la cinta 3.
> 3. Busca una transición aplicable en la máquina codificada (cinta 1); al encontrarla, la realiza en la cinta 2 y escribe el nuevo estado en la cinta 3.
> 4. Continúa hasta el estado de parada; entonces copia la cinta 2 en la 1, posiciona la cabeza y se detiene.

## Hipótesis de Church-Turing

> [!info] Contexto histórico
> - **Hilbert** (fin s. XIX): ¿existe un algoritmo finito que decida la verdad/falsedad de cualquier proposición matemática?
> - **Gödel** (1931): teorema de **incompletitud** — todo sistema axiomático es incompleto; hay sentencias indecidibles dentro de él.
> - **Turing** (1936, *On Computable Numbers*): construye la **Máquina de Turing**, primer modelo teórico de computador programable.

> [!important] Tesis de Church-Turing
> Una función es **computable si y sólo si** puede ser computada por una máquina de Turing. Cualquier algoritmo puede representarse por un esquema funcional de Turing.
>
> **No ha sido demostrada**, pero se asume verdadera: otros formalismos (**cálculo-λ**, sistemas de **Post**, funciones recursivas generales, **RAM**) definen la **misma** clase de funciones (las recursivas parciales). Una MT puede simular una RAM y viceversa.

> [!note] MT ↔ computadora real
> - **Simular una MT con una computadora real:** posible aceptando un almacenamiento potencialmente infinito (discos extraíbles). Cuestionable por recursos finitos, pero aceptado en la práctica.
> - **Simular una computadora con una MT:** una cinta puede almacenar registros, memoria y discos. Por tanto, lo que una MT **no puede** hacer, **tampoco** lo puede una computadora real.

## Tipos de problemas

> [!definition] Clasificación
> - **Decidibles:** se resuelven mediante una MT.
> - **Indecidibles:** p. ej. el **Problema de la parada** (*Halting problem*): no es posible decidir en general si una MT se detiene ante una entrada.
> - **Tratables:** existe al menos un algoritmo que los resuelve en tiempo razonable.
> - **Intratables:** decidibles pero sin algoritmo eficiente.
>
> ```
> Problemas
>  ├── Decidibles
>  │    ├── Tratables
>  │    └── Intratables
>  └── Indecidibles
> ```

## Resumen · Lenguajes, gramáticas y máquinas

> [!summary] Jerarquía de Chomsky completa
> | Lenguaje | Máquina | Gramática |
> |----------|---------|-----------|
> | **Regular** (tipo 3) | [[2 - Autómatas Finitos\|Autómata finito]] | Regular |
> | **Libre de contexto** (tipo 2) | [[5 - Autómatas de Pila\|Autómata de pila]] | Libre de contexto |
> | **Sensible al contexto** (tipo 1) | Autómata linealmente acotado (AAL) | Sensible al contexto |
> | **Recursivamente enumerable** (tipo 0) | Máquina de Turing | Tipo 0 (sin restricciones) |

---
*Anterior ← [[8 - Gramáticas con Atributos]] · Volver al → [[00 - TLA · Índice]]*
