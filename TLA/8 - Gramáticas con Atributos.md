---
tema: 8
titulo: Gramáticas con Atributos
materia: Autómatas, Teoría de Lenguajes y Compiladores
autor: Lic. Ana María Arias Roig
bibliografia: Aho, Sethi y Ullman — Compilers, Principles, Techniques and Tools (2nd ed.)
tags:
  - TLA
  - gramáticas-con-atributos
  - SDD
  - atributos-sintetizados
  - atributos-heredados
  - traducción-dirigida-por-sintaxis
  - compiladores
---

# 8 · Gramáticas con Atributos

> [!abstract] Índice del tema
> - [[#Definición Dirigida por la Sintaxis · SDD]]
> - [[#Atributos]]
> - [[#Atributos Sintetizados]]
> - [[#Atributos Heredados]]
> - [[#Orden de evaluación · Grafo de Dependencias]]
> - [[#Definiciones S-Atribuidas]]
> - [[#Definiciones L-Atribuidas]]
> - [[#Esquemas de Traducción Dirigidos por la Sintaxis · ETDS]]
> - [[#Implementación de DDS L-atribuidas]]

## Definición Dirigida por la Sintaxis · SDD

> [!definition] SDD (Syntax-Directed Definition)
> Una **Definición Dirigida por la Sintaxis** es una GLC que asocia:
> 1. A cada **símbolo**, un conjunto de **atributos**.
> 2. A cada **producción**, un conjunto de **reglas semánticas** para calcular los valores de los atributos de los símbolos de la producción.
>
> Un árbol de análisis que muestra los valores de los atributos se llama **árbol anotado** o **árbol decorado**.

## Atributos

> [!note] Atributo
> Un atributo puede ser un valor numérico, de cadena, una tabla de referencia, un objeto. Si $X$ es un símbolo y $a$ uno de sus atributos, se escribe $X.a$ para el valor de $a$ en un nodo de etiqueta $X$.
>
> **Tipos** (para no terminales): **Sintetizados** y **Heredados**. Para los **terminales**, los atributos sólo pueden ser **sintetizados**.

## Atributos Sintetizados

> [!definition] Atributo sintetizado
> Dada $A \to \alpha$ y una regla $A.a = f(\alpha_1.y_1, \dots, \alpha_n.y_n)$, $A.a$ es **sintetizado** porque depende de los atributos de los símbolos **a la derecha** de la producción (los **hijos** de $A$ en el árbol). El no terminal $A$ aparece en la **parte izquierda**.

> [!important] S-Atribuida y Gramática con Atributos
> - Una SDD donde **todos** los atributos son sintetizados se denomina **S-Atribuida**.
> - Si además **no tiene efectos globales**, se denomina **Gramática con Atributos**: sus reglas definen cada atributo exclusivamente en términos de otros atributos o constantes.
> - Efectos globales serían: actualizar una variable global, imprimir en una salida, manejar una tabla, etc.

> [!example] Evaluador de expresiones terminadas por `n`
> $G = (\{L, E, T, F\}, \{+, *, (, ), \mathbf{digit}\}, L, P)$. Todos los no terminales tienen el atributo sintetizado $val$; **digit** tiene $lexval$ (entero del analizador léxico).
>
> | Producción | Regla semántica |
> |------------|-----------------|
> | $L \to E\,\mathbf{n}$ | $L.val = E.val$ |
> | $E \to E_1 + T$ | $E.val = E_1.val + T.val$ |
> | $E \to T$ | $E.val = T.val$ |
> | $T \to T_1 * F$ | $T.val = T_1.val \times F.val$ |
> | $T \to F$ | $T.val = F.val$ |
> | $F \to (E)$ | $F.val = E.val$ |
> | $F \to \mathbf{digit}$ | $F.val = \mathbf{digit}.lexval$ |
>
> Como todos los atributos son sintetizados, se pueden evaluar los hijos antes que el padre → evaluación **ascendente**. El árbol decorado de `3 * 5 + 4 n` evalúa a $19$.

## Atributos Heredados

> [!definition] Atributo heredado
> Dada $A \to \alpha$ y una regla $\alpha_i.a = f(\alpha_1.y_1, \dots, \alpha_n.y_n, A.b)$, $\alpha_i.a$ es **heredado** porque depende de atributos de **cualquiera** de los símbolos de la producción (**hermanos** o **padre** en el árbol). El no terminal aparece en el **cuerpo** de la producción; su regla está asociada a la producción del **nodo padre**.

> [!example] Gramática apta para análisis descendente
> $G = (\{T, T', F\}, \{*, \mathbf{digit}\}, T, P)$. $T$ y $F$ tienen $val$ (sintetizado); $T'$ tiene $syn$ (sintetizado) e $inh$ (heredado).
>
> | Producción | Regla semántica |
> |------------|-----------------|
> | $T \to F T'$ | $T'.inh = F.val$;  $T.val = T'.syn$ |
> | $T' \to * F T_1'$ | $T_1'.inh = T'.inh \times F.val$;  $T'.syn = T_1'.syn$ |
> | $T' \to \lambda$ | $T'.syn = T'.inh$ |
> | $F \to \mathbf{digit}$ | $F.val = \mathbf{digit}.lexval$ |
>
> El árbol decorado de `3 * 5` evalúa a $15$ (el valor "baja" heredado por $inh$ y "sube" sintetizado por $syn$).

## Orden de evaluación · Grafo de Dependencias

> [!definition] Grafo de dependencias
> Permite determinar el orden de evaluación de los atributos para un árbol dado. Un **arco** de un atributo a otro significa que el valor del primero es necesario para calcular el segundo (restricción de una regla semántica).
>
> **Construcción:**
> ```
> Para cada nodo X del árbol, para cada atributo a de X: crear nodo X.a
> Para cada nodo X, para cada regla v := f(v1,…,vk) de su producción:
>   para i = 1..k: crear arco dirigido de vi a v
> ```

> [!note] Orden topológico
> Si hay un arco de $M$ a $N$, los atributos de $M$ deben evaluarse **antes** que los de $N$. La secuencia $N_1, N_2, \dots, N_k$ es válida si $\forall i < j$ no hay arco de $N_j$ a $N_i$.
>
> **Si hay ciclos**, no existe orden topológico y por lo tanto **no hay forma** de evaluar la SDD para ese árbol.

## Definiciones S-Atribuidas

> [!definition] S-Atribuida
> Una SDD es **S-atribuida** si todos los atributos son **sintetizados**. Se pueden evaluar en cualquier orden de **abajo hacia arriba**; lo más simple es un recorrido **post-orden**:
> ```
> Postorder(N):
>   Para cada hijo C de N (de izquierda a derecha): Postorder(C)
>   Evaluar atributos de N
> ```
> Como este orden coincide con el de las reducciones de un analizador **LR**, los atributos sintetizados pueden **almacenarse en la pila** durante el análisis, sin crear nodos explícitos.

## Definiciones L-Atribuidas

> [!definition] L-Atribuida
> Una SDD es **L-atribuida** si sus atributos son:
> 1. **Sintetizados**, o
> 2. **Heredados con reglas limitadas**, de modo que los arcos del grafo vayan de **izquierda a derecha** (*Left to right*), nunca de derecha a izquierda.
>
> Para $A \to X_1 X_2 \dots X_n$, la regla que calcula $X_i.a$ puede usar:
> - (a) Atributos **heredados** de $A$.
> - (b) Atributos (heredados o sintetizados) de $X_1, \dots, X_{i-1}$ (a la **izquierda** de $X_i$).
> - (c) Atributos de $X_i$, siempre que **no se formen ciclos**.

> [!example] L-atribuida (válida)
> En $T \to FT'$: $T'.inh = F.val$ usa $F$, a la izquierda de $T'$ → cumple (b).
> En $T' \to *FT_1'$: $T_1'.inh = T'.inh \times F.val$ usa $T'$ (padre, cumple (a)) y $F$ (a la izquierda, cumple (b)).

> [!warning] NO L-atribuida (contraejemplo)
> | Producción | Regla |
> |------------|-------|
> | $A \to BC$ | $A.s = B.b$;  $B.b = f(C.c, A.s)$ |
>
> La segunda regla define $B.b$ dependiendo de $C$ (que está **a la derecha** de $B$, viola (b)) y de $A.s$ que a su vez depende de $B.b$ → se forma un **ciclo** (viola (c)).

## Esquemas de Traducción Dirigidos por la Sintaxis · ETDS

> [!definition] ETDS (SDT)
> Un **Esquema de Traducción Dirigido por la Sintaxis** es una GLC con **fragmentos de programa** (acciones semánticas, entre **llaves**) en cualquier posición del cuerpo de las producciones. Notación complementaria a las SDD. Dos grupos:
> 1. Esquemas de Traducción **Postfija** (para S-atribuidas).
> 2. Esquemas de Traducción para **L-atribuidas**.

### Esquemas de Traducción Postfijos

> [!note] Postfijo (S-atribuida)
> Cada acción se ubica **al final** de la producción y se ejecuta al hacer la **reducción** en el análisis LR. Los atributos se ponen en la pila para poder encontrarse durante la reducción. Para $A \to XYZ$ con $A.a = f(X.x, Y.y, Z.z)$, al reducir $XYZ$ por $A$ se calcula $A.a$.

> [!example] ETDS postfijo del evaluador
> ```
> L → E n     { print(E.val); }
> E → E1 + T  { E.val = E1.val + T.val; }
> E → T       { E.val = T.val; }
> T → T1 * F  { T.val = T1.val × F.val; }
> T → F       { T.val = F.val; }
> F → ( E )   { F.val = E.val; }
> F → digit   { F.val = digit.lexval; }
> ```

### Esquemas de Traducción para L-Atribuidas

> [!note] Reglas de conversión SDD L-atribuida → ETDS
> 1. Colocar la acción que calcula los atributos **heredados** de $A$ **inmediatamente antes** de la ocurrencia de $A$ en el cuerpo. Si dependen entre sí (acíclicamente), ordenarlas.
> 2. Colocar la acción que calcula el atributo **sintetizado** de la parte izquierda **al final** del cuerpo.

> [!example] Cajas de texto tipo TeX (subíndices)
> $G = (\{B\}, \{\mathbf{sub}, (, ), \mathbf{text}\}, B, P)$ con $P = \{B \to BB \mid B\,\mathbf{sub}\,B \mid (B) \mid \mathbf{text}\}$. Es ambigua pero analizable en forma ascendente dando al subíndice **precedencia** sobre la concatenación.
>
> **Atributos:** $ps$ (point size), $ht$ (height), $dp$ (depth); la línea base (*baseline*) es la referencia. Un subíndice tiene tamaño $0.7 \times$ el del padre.
>
> | Producción | Regla semántica |
> |------------|-----------------|
> | $S \to B$ | $B.ps = 10$ |
> | $B \to B_1 B_2$ | $B_1.ps = B.ps$;  $B_2.ps = B.ps$;  $B.ht = \max(B_1.ht, B_2.ht)$;  $B.dp = \max(B_1.dp, B_2.dp)$ |
> | $B \to B_1\,\mathbf{sub}\,B_2$ | $B_1.ps = B.ps$;  $B_2.ps = 0.7 \times B.ps$;  $B.ht = \max(B_1.ht, B_2.ht - 0.25 B.ps)$;  $B.dp = \max(B_1.dp, B_2.dp + 0.25 B.ps)$ |
> | $B \to (B_1)$ | $B_1.ps = B.ps$;  $B.ht = B_1.ht$;  $B.dp = B_1.dp$ |
> | $B \to \mathbf{text}$ | $B.ht = getHt(B.ps, \mathbf{text}.lexval)$;  $B.dp = getDp(B.ps, \mathbf{text}.lexval)$ |
>
> El $ps$ **baja** (heredado); $ht$ y $dp$ **suben** (sintetizados, con máximo). El ETDS ubica las acciones de $ps$ antes de cada $B_i$ y las de $ht/dp$ al final:
> ```
> B → ( {B1.ps = B.ps;} B1 ) {B.ht = B1.ht; B.dp = B1.dp;}
> ```

## Implementación de DDS L-atribuidas

> [!note] Tres métodos
> 1. **Construir el árbol y decorarlo:** establecer un orden de traducción; si hay ciclos, no se resuelve.
> 2. **Construir el árbol, agregar acciones y ejecutar en preorden:** sirve para cualquier L-atribuida.
> ```
> Visitar(b):
>   Para cada hijo a de b:
>     Evaluar atributos heredados de a (izquierda a derecha)
>     Visitar(a)
>   Evaluar atributos sintetizados de b
> ```
> 3. **Analizador descendente recursivo:** la función del no terminal $A$ recibe sus atributos **heredados** como argumentos y **retorna** sus atributos **sintetizados**.

---
*Anterior ← [[7 - Análisis Sintáctico]] · Continúa en → [[9 - Máquinas de Turing]]*
