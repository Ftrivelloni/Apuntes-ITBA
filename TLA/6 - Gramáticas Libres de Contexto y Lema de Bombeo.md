---
tema: 6
titulo: Gramáticas Libres de Contexto y Lema de Bombeo
materia: Autómatas, Teoría de Lenguajes y Compiladores
autor: Lic. Ana María Arias Roig
tags:
  - TLA
  - GLC
  - lenguajes-libres-de-contexto
  - forma-normal-de-chomsky
  - lema-de-bombeo
  - ambigüedad
---

# 6 · Gramáticas Libres de Contexto

> [!abstract] Índice del tema
> - [[#Definición]]
> - [[#Derivaciones]]
> - [[#Árboles de derivación]]
> - [[#Gramáticas ambiguas]]
> - [[#Formas Normales · Forma Normal de Chomsky]]
> - [[#Equivalencia entre Autómatas de Pila y GLC]]
> - [[#Lema de Bombeo para Lenguajes Independientes de Contexto]]
> - [[#Propiedades de clausura de los LLC]]

Las **gramáticas libres de contexto (GLC)** generan **lenguajes libres de contexto** (o independientes de contexto), una clase más amplia que los regulares.

## Definición

> [!definition] Gramática libre de contexto (GLC)
> Es una 4-tupla $G = (N, \Sigma, S, P)$ donde:
> - $N$: conjunto finito de **no terminales** (variables).
> - $\Sigma$: conjunto finito de **terminales** (alfabeto).
> - $S \in N$: **símbolo inicial**.
> - $P$: conjunto de **producciones** de la forma $A \to \beta$, con $A \in N$ y $\beta \in (N \cup \Sigma)^{*}$.

## Derivaciones

> [!definition] Tipos de derivación
> - **Derivación** $\Rightarrow_G$: si $\alpha A \gamma$ es una cadena en $(N \cup \Sigma)^{*}$ y $A \to \beta$ es una producción, entonces $\alpha A \gamma \Rightarrow_G \alpha \beta \gamma$.
> - **Más a la izquierda:** en cada paso se reemplaza la variable situada **más a la izquierda**.
> - **Más a la derecha:** en cada paso se reemplaza la variable situada **más a la derecha**.

> [!example] Gramática de expresiones
> $G = (\{E, I\}, \{0, 1, +, *, (, )\}, E, P)$ con
> $$P = \{\, E \to I \mid E+E \mid E*E \mid (E), \quad I \to I0 \mid I1 \mid 0 \mid 1 \,\}$$
> Genera, p. ej., $(11+0)*1$.
>
> **Derivación más a la izquierda:**
> $$E \Rightarrow E*E \Rightarrow (E)*E \Rightarrow (E+E)*E \Rightarrow (I+E)*E \Rightarrow (I1+E)*E \Rightarrow (11+E)*E$$
> $$\Rightarrow (11+I)*E \Rightarrow (11+0)*E \Rightarrow (11+0)*I \Rightarrow (11+0)*1$$
>
> **Derivación más a la derecha:**
> $$E \Rightarrow E*E \Rightarrow E*I \Rightarrow E*1 \Rightarrow (E)*1 \Rightarrow (E+E)*1 \Rightarrow (E+I)*1 \Rightarrow (E+0)*1$$
> $$\Rightarrow (I+0)*1 \Rightarrow (I1+0)*1 \Rightarrow (11+0)*1$$

## Árboles de derivación

Las derivaciones se pueden representar en forma de **árbol**, que muestra cómo los símbolos de una cadena terminal se agrupan en subcadenas. En los compiladores se usa para representar la **estructura sintáctica** del programa fuente, facilitando la traducción a código ejecutable mediante funciones recursivas.

> [!definition] Árbol de derivación $\tau(A)$
> Sea $G = (N, \Sigma, S, P)$. $\tau(A)$ es un grafo tal que:
> 1. Si $A \in N$, $\tau(A)$ es un árbol de derivación representado por un nodo.
> 2. Si $\tau(A)$ es un árbol de derivación y $X$ es una hoja con $X \in N$ y $X \to Y_1 Y_2 \dots Y_k$, entonces también es árbol de derivación el que resulta de conectar $X$ con aristas a nuevos nodos $Y_1, Y_2, \dots, Y_k$.

> [!note] Resultado de un árbol de derivación
> Es la cadena que se obtiene concatenando las hojas **desde la izquierda**. Un árbol produce una cadena del lenguaje si:
> 1. Su resultado es una cadena terminal (hojas etiquetadas con terminales o $\lambda$).
> 2. La raíz está etiquetada con el símbolo inicial $S$.

## Gramáticas ambiguas

> [!definition] Ambigüedad
> Una GLC $G = (N, \Sigma, P, S)$ es **ambigua** si existe alguna cadena que es resultado de **dos árboles de derivación distintos**:
> $$G \text{ ambigua} \iff \exists\, \alpha \in L(G) : \exists\, \tau(S), \tau'(S) \text{ con } \tau(S) \neq \tau'(S),\ \alpha \text{ base de ambos}$$
>
> **Ejemplo:** $G = (\{E\}, \{0,1,+,*\}, E, P)$ con $P = \{E \to E+E \mid E*E \mid 0 \mid 1\}$ tiene dos árboles distintos para $0+1*0$.

> [!tip] Eliminación de la ambigüedad
> **No existe un algoritmo** que decida si una GLC es ambigua. Sin embargo, a veces se encuentra una gramática equivalente no ambigua. Para las expresiones:
> $$G' = (\{E, T, I\}, \{0,1,+,*\}, E, P), \quad P = \{\, E \to E+T \mid T,\ \ T \to T*I \mid I,\ \ I \to 0 \mid 1 \,\}$$
> Elimina ambigüedades forzando **precedencia** y **asociatividad** mediante variables nuevas, cada una asociada a un nivel de "fuerza de acoplamiento".

> [!note] Derivaciones más a la izquierda y ambigüedad
> Una GLC es ambigua **si y sólo si** para alguna cadena $\omega$ existen **dos derivaciones más a la izquierda distintas** desde $S$.

> [!warning] Ambigüedad inherente
> Un lenguaje es **inherentemente ambiguo** si **todas** las gramáticas que lo generan son ambiguas.
> - El lenguaje de las expresiones **no** es inherentemente ambiguo (existe $G'$ no ambigua).
> - $L = \{a^{n}b^{n}c^{m}d^{m} : n,m \ge 1\} \cup \{a^{n}b^{m}c^{m}d^{n} : n,m \ge 1\}$ **sí** es inherentemente ambiguo.

## Formas Normales · Forma Normal de Chomsky

> [!definition] Forma Normal de Chomsky (FNC)
> Todo LLC sin $\lambda$ es generado por una GLC en la que todas las producciones son de la forma:
> $$A \to BC \qquad \text{o} \qquad A \to a$$
> con $A, B, C \in N$ y $a \in \Sigma$.

> [!important] Simplificaciones preliminares (en orden)
> 1. Eliminación de **símbolos inútiles**.
> 2. Eliminación de **producciones $\lambda$**.
> 3. Eliminación de **producciones unitarias**.

### 1 · Eliminación de símbolos inútiles

> [!note] Símbolo útil
> $X \in (N \cup \Sigma)$ es **útil** si existe una derivación $S \Rightarrow^{*} \alpha X \beta \Rightarrow^{*} \omega$ con $\omega \in \Sigma^{*}$. Un símbolo útil debe ser **productivo** Y **alcanzable**.
>
> **Símbolos productivos (generadores):**
> - **Base:** todo $a \in \Sigma$ es productivo.
> - **Paso inductivo:** si existe $A \to \alpha$ con todos los símbolos de $\alpha$ productivos, entonces $A$ es productivo.
>
> **Símbolos alcanzables:**
> - **Base:** $S$ es alcanzable.
> - **Paso inductivo:** si $A$ es alcanzable, todos los símbolos de las partes derechas de las producciones con $A$ a la izquierda son alcanzables.

### 2 · Eliminación de producciones $\lambda$

> [!note] Símbolos anulables
> - **Base:** si $A \to \lambda$ es una producción, $A$ es anulable.
> - **Paso inductivo:** si $B \to C_1 C_2 \dots C_k$ con cada $C_i$ anulable, entonces $B$ es anulable.
>
> **Algoritmo:** para cada $X$ anulable, por cada producción donde $X$ aparece a la derecha se agrega una versión sin $X$; se eliminan las producciones $X \to \lambda$; se quita $X$ de *Anulables*.

### 3 · Eliminación de producciones unitarias

> [!note] Pares unitarios
> - **Base:** $(A, A)$ es par unitario para toda variable $A$.
> - **Paso inductivo:** si $(A, B)$ es par unitario y $B \to C$ es producción con $C$ variable, entonces $(A, C)$ es par unitario.
>
> **Algoritmo:** por cada par $(A, B)$ se añaden a $P$ todas las producciones $A \to \alpha$ donde $B \to \alpha$ es una producción **no** unitaria de $B$.

### Pasos finales hacia la FNC

> [!note] Últimas dos tareas
> **(a)** Que todo cuerpo de longitud $\ge 2$ esté formado sólo por variables: para cada terminal $a$ en un cuerpo largo, crear una variable $X$ con $X \to a$ y reemplazar $a$ por $X$.
>
> **(b)** Descomponer cuerpos de longitud $\ge 3$: para $A \to B_1 B_2 \dots B_k$ ($k \ge 3$), introducir $k-2$ variables nuevas y reemplazar por:
> $$A \to B_1 C_1,\quad C_1 \to B_2 C_2,\quad \dots,\quad C_{k-2} \to B_{k-1} B_k$$
>
> Todo árbol de derivación de una gramática en FNC es un **árbol binario**.

## Equivalencia entre Autómatas de Pila y GLC

> [!theorem] De GLC a AP
> Dada una GLC $G$, se construye un AP que simula las **derivaciones más a la izquierda** de $G$.
>
> *Construcción:* $P = (\{q\}, \Sigma, N \cup \Sigma, \delta, q, S)$ con un único estado, donde:
> 1. $\forall A \to \beta \in P_g :\ \delta(q, \lambda, A) \ni (q, \beta)$ (expandir variable).
> 2. $\forall a \in \Sigma :\ \delta(q, a, a) = \{(q, \lambda)\}$ (emparejar terminal).

> [!theorem] De AP a GLC
> Dado un AP $P = (Q, \Sigma, \Gamma, \delta, q_0, z_0)$ que acepta por pila vacía, existe una GLC con $L(G) = L_{pv}(P)$.
>
> *Construcción:* $N = \{S\} \cup \{[pXq] : p, q \in Q,\ X \in \Gamma\}$, con producciones:
> 1. $\forall q \in Q :\ S \to [q_0 z_0 q]$
> 2. Si $(q_1, B_1 B_2 \dots B_m) \in \delta(q, a, A)$: $[qAp] \to a[q_1 B_1 q_2][q_2 B_2 q_3]\dots[q_m B_m q_{m+1}]$ con $q_{m+1} = p$.
> 3. Si $(p, \lambda) \in \delta(q, a, A)$: $[qAp] \to a$.
>
> Después se descartan las producciones improductivas/inalcanzables y se renombran los no terminales.

> [!note] Gramáticas ambiguas y APD
> - Todos los lenguajes aceptados por un **APD** tienen gramáticas **no ambiguas**.
> - Hay lenguajes de gramáticas no ambiguas que **no** pueden reconocerse por ningún APD. Ejemplo: $S \to 0S0 \mid 1S1 \mid \lambda$ genera $\{\omega\omega^{R} : \omega \in \{0,1\}^{*}\}$, no ambigua, pero sin APD que la reconozca.

## Lema de Bombeo para Lenguajes Independientes de Contexto

> [!theorem] Tamaño de los árboles (FNC)
> Dada $G$ en FNC y un árbol $\tau(S)$ cuyo resultado es $\omega$, si la altura (camino más largo) es $n$, entonces $|\omega| \le 2^{n-1}$.
>
> *Demostración por inducción en $n$:*
> - **Base** $n=1$: raíz $S$ y una hoja terminal; $|\omega| = 1 = 2^{0} = 2^{1-1}$.
> - **Paso inductivo:** con altura $h > 1$, la FNC obliga a empezar con $S \to BC$. Los subárboles de $B$ y $C$ tienen altura $\le h-1$, luego $|\omega_B|, |\omega_C| \le 2^{h-2}$. Así $|\omega| = |\omega_B| + |\omega_C| \le 2^{h-2} + 2^{h-2} = 2^{h-1}$.

> [!theorem] Lema de bombeo (LIC)
> Sea $L$ un LIC. Existe una constante $p$ tal que si $|\omega| \ge p$, se puede escribir $\omega = rxyzs$ con:
> 1. $|xyz| \le p$ (la parte central no es demasiado larga).
> 2. $xz \neq \lambda$ (al menos una de las cadenas a bombear no es vacía).
> 3. $\forall i \ge 0 :\ rx^{i}yz^{i}s \in L$.
>
> Simbólicamente:
> $$\forall L \text{ LIC}: \exists\, p > 0 / \forall \omega \in L : |\omega| \ge p \Rightarrow \exists\, r,x,y,z,s / \big(\omega = rxyzs \wedge |xyz| \le p \wedge (x \neq \lambda \vee z \neq \lambda) \wedge \forall i \ge 0 : rx^{i}yz^{i}s \in L\big)$$

> [!note]- Demostración
> Se toma $G$ en FNC con $L(G) = L - \{\lambda\}$ y $\#V = m$ variables. Se elige $p = 2^{m}$.
>
> Por el teorema previo, un árbol cuyo camino más largo mide $\le m$ genera $|\omega| \le 2^{m-1} = p/2 < p$. Como $|\omega| \ge p$, el árbol tiene altura $\ge m+1$ y usa $\ge m+1$ variables; por el principio del palomar, **alguna variable se repite** en el camino: $A_i = A_j = A$ (con $k-m \le i < j \le k$).
>
> Esto da:
> $$\text{I) } A_0 \Rightarrow^{*} rAs \qquad \text{II) } A \Rightarrow^{*} xAz \qquad \text{III) } A \Rightarrow^{*} y$$
> Como no hay producciones unitarias, $x$ y $z$ no pueden ser ambas $\lambda$. Se prueba por inducción que $\forall i \ge 0: rx^{i}yz^{i}s \in L$:
> - **Base** $i=0$: por I y III, $A_0 \Rightarrow^{*} rAs \Rightarrow^{*} rys = rx^{0}yz^{0}s \in L$.
> - **Paso inductivo:** usando II una vez más, $A_0 \Rightarrow^{*} rAs \Rightarrow^{*} rx^{h+1}Az^{h+1}s \Rightarrow^{*} rx^{h+1}yz^{h+1}s$.
>
> Eligiendo $A_i$ cerca de la base (con $k-i \le m$), el subárbol de raíz $A_i$ tiene altura $\le m+1$, luego $|xyz| \le 2^{m} = p$.

## Propiedades de clausura de los LLC

> [!theorem] Cerradas
> Si $L_1, L_2$ son LLC, entonces son LLC: **unión** $L_1 \cup L_2$, **concatenación** $L_1 L_2$, **clausura** $L^{+}$ y $L^{*}$, y **reverso** $L^{R}$.

> [!warning] NO cerradas
> La **intersección** de LLC **no** es cerrada. Contraejemplo:
> $$L_1 = \{0^{n}1^{n}2^{i} : n \ge 1, i \ge 1\}, \quad L_2 = \{0^{i}1^{n}2^{n} : n \ge 1, i \ge 1\}$$
> Ambos son LLC, pero $L_1 \cap L_2 = \{0^{n}1^{n}2^{n} : n \ge 1\}$ **no** lo es.

> [!theorem] Intersección con lenguaje regular
> Si $L_1$ es regular y $L_2$ es LLC, entonces $L_1 \cap L_2$ es **LLC**.

---
*Anterior ← [[5 - Autómatas de Pila]] · Continúa en → [[7 - Análisis Sintáctico]]*
