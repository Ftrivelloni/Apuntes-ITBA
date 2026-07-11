---
tema: 4
titulo: Lenguajes Regulares
materia: Autómatas, Teoría de Lenguajes y Compiladores
autor: Lic. Ana María Arias Roig
tags:
  - TLA
  - lenguajes-regulares
  - gramáticas-regulares
  - lema-de-bombeo
  - propiedades-de-clausura
---

# 4 · Lenguajes Regulares

> [!abstract] Índice del tema
> - [[#¿Cómo demostrar que un lenguaje es regular?]]
> - [[#Conversión Autómata Finito ↔ Gramática Regular]]
> - [[#¿Cómo demostrar que un lenguaje NO es regular?]]
> - [[#Lema del bombeo para lenguajes regulares]]
> - [[#Propiedades de clausura de los lenguajes regulares]]

> [!info] Equivalencias fundamentales
> - Los autómatas finitos (AFD, AFND y AFND-λ) **reconocen** lenguajes regulares.
> - Las expresiones regulares **describen** los lenguajes regulares.
> - Las gramáticas regulares **generan** lenguajes regulares.

## ¿Cómo demostrar que un lenguaje es regular?

> [!tip] Vías equivalentes
> Un lenguaje es regular si se encuentra:
> - un **autómata finito** (AFD, AFND o AFND-λ) que lo reconozca, **o**
> - una **expresión regular** que lo describa, **o**
> - una **gramática regular** que lo genere.

## Conversión Autómata Finito ↔ Gramática Regular

> [!theorem] Teorema AF → GR
> Si $L$ es aceptado por un autómata finito $M$, existe una gramática regular $G$ tal que $L = L(M) = L(G)$.

> [!note] Algoritmo AF → GR
> **Entrada:** $M = (Q, \Sigma, q_0, F, \delta)$. **Salida:** $G = (Q, \Sigma, q_0, P)$.
> 1. Los **no terminales** de $G$ son $Q$.
> 2. Los **terminales** de $G$ son $\Sigma$.
> 3. El **símbolo inicial** es el estado inicial $q_0$.
> 4. Si $\delta(q, a) = p$, añadir la producción $q \to ap$ a $P$.
> 5. Si $q_f \in F$, añadir la producción $q_f \to \lambda$ a $P$.

> [!theorem] Teorema GR → AF
> Si $L$ es generado por una gramática regular $G$, existe un autómata finito $M$ tal que $L = L(M) = L(G)$.

> [!note] Algoritmo GR → AF
> **Entrada:** $G = (V, \Sigma, S, P)$. **Salida:** $M = (V \cup \{q_f\}, \Sigma, S, \{q_f\}, \delta)$.
> 1. Los **estados** de $M$ son los no terminales de $G$ unión un estado $q_f$.
> 2. Los **terminales** de $M$ son $\Sigma$.
> 3. El **estado inicial** es el símbolo inicial $S$.
> 4. El **estado final** es $\{q_f\}$.
> 5. Si $A \to aB \in P$, agregar $\delta(A, a) = B$.
> 6. Si $A \to a \in P$, agregar $\delta(A, a) = \{q_f\}$.
> 7. Si $A \to \lambda \in P$, agregar $\delta(A, \lambda) = \{q_f\}$.

## ¿Cómo demostrar que un lenguaje NO es regular?

> [!important]
> - **Todo lenguaje finito es regular.**
> - Si un lenguaje es **infinito**, para demostrar que no es regular se usa el **lema de bombeo**.

## Lema del bombeo para lenguajes regulares

> [!theorem] Lema del bombeo (regulares)
> Si $L$ es un lenguaje regular infinito, entonces:
> $$\exists\, n \;/\; \forall \omega \in L : |\omega| \ge n \implies \omega = xyz \text{ tal que}$$
> 1. $y \neq \lambda$
> 2. $|xy| \le n$
> 3. $\forall k \ge 0 : xy^{k}z \in L$
>
> Es decir: siempre es posible encontrar una subcadena no vacía $y$, no demasiado lejos del inicio de $\omega$, que se puede **"bombear"** (repetir cualquier número de veces o borrar) manteniendo la pertenencia al lenguaje.

> [!note]- Demostración (principio del palomar)
> Suponemos $L$ regular; entonces $L = L(A)$ para un AFD $A = (Q, \Sigma, q_0, \delta, F)$ con $\#Q = n$ estados.
>
> Sea $\omega = a_1 a_2 \dots a_m$ con $m \ge n$. Definimos $p_i = \hat{\delta}(q_0, a_1 \dots a_i)$ (estado tras leer los primeros $i$ símbolos), con $p_0 = q_0$.
>
> Hay $n+1$ estados $p_0, \dots, p_n$ pero sólo $n$ estados distintos, así que existen $0 \le i < j \le n$ con $p_i = p_j$. Descomponemos:
> $$x = a_1 \dots a_i \qquad y = a_{i+1} \dots a_j \qquad z = a_{j+1} \dots a_m$$
> con $\hat{\delta}(q_0, x) = p_i$, $\hat{\delta}(p_i, y) = p_i$. Nótese que $x$ puede ser vacía ($i=0$) y $z$ también ($j=m=n$), pero $y \neq \lambda$ porque $i < j$.
>
> - $k=0$: $\hat{\delta}(q_0, xz) = \hat{\delta}(p_i, z) = p_f \in F$, aceptada.
> - $k>0$: cada repetición de $y$ vuelve a $p_i = p_j$, luego $\hat{\delta}(q_0, xy^{k}z) = p_f \in F$, aceptada.
>
> Por lo tanto $\forall k \ge 0 : xy^{k}z \in L(A)$.

### Uso del lema para demostrar que un lenguaje NO es regular

El lema permite demostrar **por contradicción**. Como el enunciado es "existe $n$ tal que para toda $\omega$ con $|\omega| \ge n$ existe partición $xyz$ que cumple 1-3", para negarlo hay que **encontrar una palabra** que, para **toda** partición posible, falle alguna condición.

> [!warning] Negación del lema (lo que hay que probar)
> Para toda partición $\omega = xyz$:
> 1. $y = \lambda$, **o bien**
> 2. $|xy| > n$, **o bien**
> 3. $\exists\, k \ge 0 : xy^{k}z \notin L$

> [!example] $L = \{a^{m}b^{2m} : m \in \mathbb{N},\ m \ge 0\}$ no es regular
> 1. Suponemos $L$ regular.
> 2. Sea $n = N$ la constante del lema.
> 3. Elegimos $\omega = a^{N}b^{2N} \in L$, con $|\omega| = 3N \ge N$.
> 4. Toda descomposición $\omega = xyz$ con $|xy| \le N$ y $y \neq \lambda$ tiene la forma $x = a^{|x|},\ y = a^{|y|},\ z = a^{N-|xy|}b^{2N}$ (la parte $xy$ cae toda en las $a$).
> 5. Tomamos $k=0$: $xy^{0}z = xz = a^{N-|y|}b^{2N}$. Como $|y| > 0$, esta palabra tiene menos de $N$ letras $a$ pero $2N$ letras $b$, así que $a^{N-|y|}b^{2N} \notin L$.
> 6. Contradice el lema $\Rightarrow$ $L$ **no es regular**.

## Propiedades de clausura de los lenguajes regulares

> [!theorem] Los regulares son cerrados bajo…
> Si $L$ y $M$ son regulares, entonces también lo son:
> - **Unión** $L \cup M$
> - **Concatenación** $L \cdot M$
> - **Clausura** $L^{*}$
> - **Complemento** $\overline{L}$
> - **Intersección** $L \cap M$
> - **Diferencia** $L - M$
> - **Inverso / reverso** $L^{R}$

> [!note]- Demostraciones
> **Unión:** $L = L(r)$, $M = L(s)$; entonces $L(r) \cup L(s) = L(r + s)$, regular.
>
> **Concatenación** y **clausura:** análogas a la unión, usando los operadores $\cdot$ y $*$ de las ER.
>
> **Complemento:** si $A = (Q, \Sigma, \delta, q_0, F)$ reconoce $L$, entonces $B = (Q, \Sigma, \delta, q_0, Q - F)$ reconoce $\overline{L} = \Sigma^{*} - L$, ya que $\omega \in L(B) \iff \hat{\delta}(q_0, \omega) \in (Q-F) \iff \omega \notin L(A)$.
>
> **Intersección:** vía De Morgan $L \cap M = \overline{\overline{L} \cup \overline{M}}$, o directamente con el **autómata producto** $A = (Q_L \times Q_M, \Sigma, \delta, (q_L, q_M), F_L \times F_M)$ donde $\delta((p,q), a) = (\delta_L(p,a), \delta_M(q,a))$. Se cumple $\omega \in L(A) \iff \omega \in L(A_L) \wedge \omega \in L(A_M)$.
>
> **Diferencia:** $L - M = L \cap \overline{M}$, regular por lo anterior.
>
> **Inverso:** por inducción estructural sobre la ER $E$ con $L = L(E)$, construyendo una ER para $L^{R} = (L(E))^{R}$.

---
*Anterior ← [[3 - Expresiones Regulares]] · Continúa en → [[5 - Autómatas de Pila]]*
