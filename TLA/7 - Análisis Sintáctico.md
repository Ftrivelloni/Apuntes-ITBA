---
tema: 7
titulo: Análisis Sintáctico
materia: Autómatas, Teoría de Lenguajes y Compiladores
autor: Lic. Ana María Arias Roig
bibliografia: Aho, Sethi y Ullman — Compilers, Principles, Techniques and Tools (2nd ed.)
tags:
  - TLA
  - análisis-sintáctico
  - parsing
  - LL1
  - LR
  - SLR
  - LALR
  - compiladores
---

# 7 · Análisis Sintáctico

> [!abstract] Índice del tema
> - [[#Definición]]
> - [[#Métodos de análisis sintáctico]]
> - [[#Análisis Descendente · Descenso Recursivo]]
> - [[#Eliminación de recursividad izquierda]]
> - [[#Factorización por la izquierda]]
> - [[#Conjuntos PRIMEROS y SIGUIENTES]]
> - [[#Gramáticas LL(1)]]
> - [[#Análisis predictivo no recursivo · controlado por tabla]]
> - [[#Análisis Ascendente · Desplazamiento-Reducción]]
> - [[#Análisis LR]]
> - [[#Ítems y autómata LR(0)]]
> - [[#Tabla SLR(1)]]
> - [[#Analizadores más potentes · LR(1) canónico y LALR]]
> - [[#Generador de analizadores sintácticos · Yacc]]

## Definición

> [!definition] Análisis sintáctico (parsing)
> Es el proceso de determinar cómo puede derivarse una cadena de terminales mediante una gramática. El analizador obtiene una cadena de **tokens** del analizador léxico y verifica que la cadena pueda generarse con la gramática, construyendo un **árbol de análisis** (raíz = símbolo inicial; hojas = terminales o $\lambda$).

## Métodos de análisis sintáctico

En todos los métodos, la entrada se explora de **izquierda a derecha**, un símbolo a la vez. Los métodos más eficientes (**LL** y **LR**) sólo funcionan para subclases de gramáticas, pero suficientemente expresivas para los lenguajes de programación modernos.

> [!info] Descendentes (Top-Down)
> Construyen el árbol desde la **raíz** hacia las **hojas**. Producen **derivaciones por izquierda**.

> [!info] Ascendentes (Bottom-Up)
> Construyen el árbol desde las **hojas** hacia la **raíz**. Producen **derivaciones inversas** (por derecha revertidas).

> [!example] Misma gramática, ambos sentidos
> $G = (\{S, A, B\}, \{a, b, c\}, S, P)$ con $P = \{S \to bS \mid cAB,\ A \to bA \mid a,\ B \to aBc \mid b\}$. Para $bcbab$:
> - **Descendente:** $S \Rightarrow bS \Rightarrow bcAB \Rightarrow bcbAB \Rightarrow bcbaB \Rightarrow bcbab$
> - **Ascendente:** $bcbab \Rightarrow bcbAb \Rightarrow bcAb \Rightarrow bcAB \Rightarrow bS \Rightarrow S$

## Análisis Descendente · Descenso Recursivo

El problema clave es **determinar qué producción aplicar** para cada no terminal.
- Forma general: **Descenso Recursivo** (puede requerir *backtracking*).
- Caso especial sin backtracking: **Análisis Predictivo**.
- Gramáticas que permiten analizar con $k$ símbolos de anticipación: **LL(k)**.

> [!note] Estructura del descenso recursivo
> Un conjunto de funciones, **una por cada no terminal**. La función principal invoca la del símbolo inicial y acepta si se explora toda la entrada.
> ```
> Principal:
>   t apunta al inicio de ω
>   Si S(t) y t == EOF: Acepta ω
>   Sino: No acepta ω
> ```
> Para $A \to \alpha_1 \mid \dots \mid \alpha_k$, la función $A(t)$ prueba cada alternativa hasta que una tenga éxito. `procesar(A→α, t)`, con $\alpha = X_1 X_2 \dots X_n$: si $X_j \in \Sigma$ compara y consume; si $X_j \in N$ llama a $X_j(t)$; si $X_j = \lambda$ no hace nada.

> [!example] $S \to cAd,\ A \to ab \mid a$, entrada $\omega = cad$
> `S('c')` → consume → `A('a')` → consume → retorna `True`. Vuelve a `S`, $t$ apunta a `'d'`, consume, retorna `True`. En el principal: `True` y $t$ = EOF ⇒ **aceptada**.

> [!warning] Limitaciones
> - La cadena se analiza de izquierda a derecha.
> - Siempre elige la derivación más a la izquierda.
> - Si la gramática es **recursiva por izquierda**, el analizador entra en un **ciclo infinito**.

## Eliminación de recursividad izquierda

> [!definition] Recursividad izquierda
> Una gramática es recursiva por la izquierda si tiene un no terminal $A$ con derivación $A \Rightarrow^{+} A\alpha$. Es **inmediata** si hay una producción $A \to A\alpha$.

> [!note] Eliminación de recursividad inmediata
> Se agrupan las producciones $A \to A\alpha_1 \mid \dots \mid A\alpha_m \mid \beta_1 \mid \dots \mid \beta_n$ (ninguna $\beta_i$ empieza en $A$) y se sustituyen por:
> $$A \to \beta_1 A' \mid \beta_2 A' \mid \dots \mid \beta_n A'$$
> $$A' \to \alpha_1 A' \mid \alpha_2 A' \mid \dots \mid \alpha_m A' \mid \lambda$$

> [!note] Algoritmo general (recursividad no inmediata)
> **Entrada:** $G$ sin ciclos ni producciones $\lambda$.
> 1. Ordenar los no terminales $A_1, A_2, \dots, A_n$.
> 2. Para cada $i$ de $1$ a $n$: para cada $j$ de $1$ a $i-1$, sustituir cada $A_i \to A_j\gamma$ por $A_i \to \delta_1\gamma \mid \dots \mid \delta_k\gamma$ (donde $A_j \to \delta_1 \mid \dots \mid \delta_k$). Luego eliminar la recursividad inmediata entre las producciones $A_i$.

> [!example]
> $S \to Aa \mid b,\ A \to Ac \mid Sd \mid \lambda$. Con $A_1 = S$, $A_2 = A$: sustituyendo $A \to Sd$ queda $A \to Aad \mid bd \mid Ac \mid \lambda$; eliminando recursividad inmediata:
> $$S \to Aa \mid b, \quad A \to bdA' \mid A', \quad A' \to cA' \mid adA' \mid \lambda$$

## Factorización por la izquierda

> [!note] Algoritmo de factorización
> **Entrada:** $G$ con producciones $A \to \alpha\beta_1 \mid \alpha\beta_2 \mid \dots$
> 1. Por cada no terminal $A$, encontrar el prefijo común $\alpha$ más largo.
> 2. Si $\alpha \neq \lambda$, sustituir $A \to \alpha\beta_1 \mid \dots \mid \alpha\beta_n \mid \gamma$ por:
> $$A \to \alpha A' \mid \gamma, \qquad A' \to \beta_1 \mid \beta_2 \mid \dots \mid \beta_n$$

> [!example] Gramática if-then-else
> $S \to iEtS \mid iEtSeS \mid a,\ E \to b$ (i=if, t=then, e=else). Factorizada:
> $$S \to iEtSS' \mid a, \quad S' \to eS \mid \lambda, \quad E \to b$$

## Conjuntos PRIMEROS y SIGUIENTES

> [!definition] PRIMERO(α)
> Conjunto de terminales que **empiezan** las cadenas derivadas de $\alpha$:
> $$\text{PRIMERO}(\alpha) = \{ t \in \Sigma \mid \alpha \Rightarrow^{*} t\beta \} \cup \{ \lambda \mid \alpha \Rightarrow^{*} \lambda \}$$
> **Reglas:** (1) $\forall t \in \Sigma$, $\text{PRIMERO}(t) = \{t\}$. (2) Si $X \to Y_1 \dots Y_k$, entonces $t \in \text{PRIMERO}(X)$ si $t \in \text{PRIMERO}(Y_i)$ y $\lambda \in \text{PRIMERO}(Y_1), \dots, \text{PRIMERO}(Y_{i-1})$. (3) Si $X \to \lambda$, agregar $\lambda$ a $\text{PRIMERO}(X)$.

> [!definition] SIGUIENTE(A)
> Conjunto de terminales que pueden aparecer **a la derecha** de $A$ en alguna forma sentencial:
> $$\text{SIGUIENTE}(A) = \{ t \in \Sigma \mid S \Rightarrow^{*} \alpha A t \beta \} \cup \{ \$ \mid S \Rightarrow^{*} \alpha A \}$$
> El símbolo $\$$ marca el EOF. **Reglas:** (1) Agregar $\$$ a $\text{SIGUIENTE}(S)$. (2) Si $A \to \alpha B\beta$, todo $\text{PRIMERO}(\beta) - \{\lambda\}$ está en $\text{SIGUIENTE}(B)$. (3) Si $A \to \alpha B$, o $A \to \alpha B\beta$ con $\lambda \in \text{PRIMERO}(\beta)$, entonces $\text{SIGUIENTE}(A) \subseteq \text{SIGUIENTE}(B)$.

## Gramáticas LL(1)

> [!definition] LL(1)
> **L**eft to right (explora de izquierda a derecha), **L**eftmost derivation (derivación por izquierda), **1** símbolo de anticipación.
>
> $G$ es LL(1) si para todas las producciones distintas $X \to \alpha_1 \mid \dots \mid \alpha_n$:
> - $\text{PRIMERO}(\alpha_i) \cap \text{PRIMERO}(\alpha_j) = \varnothing$
> - Si $X \Rightarrow^{*} \lambda$, entonces $\text{PRIMERO}(X) \cap \text{SIGUIENTE}(X) = \varnothing$
>
> Para ello, la gramática **no** debe ser ambigua, **no** debe tener recursividad izquierda y **debe** estar factorizada.

> [!note] Tabla de análisis predictivo
> Filas = no terminales, columnas = terminales y $\$$. Para cada $A \to \alpha$:
> 1. Por cada $a \in \text{PRIMERO}(\alpha)$, agregar $A \to \alpha$ a $M[A, a]$.
> 2. Si $\lambda \in \text{PRIMERO}(\alpha)$, por cada $b \in \text{SIGUIENTE}(A)$ agregar $A \to \alpha$ a $M[A, b]$ (incluido $\$$ si está en SIGUIENTE).
> 3. Las celdas vacías son **error**.
>
> En una gramática LL(1) cada celda identifica una **única** producción. Si hay recursividad izquierda o falta factorización, alguna celda tendrá **múltiples definiciones**.

> [!example] Gramática de expresiones LL(1)
> $E \to TE',\ E' \to +TE' \mid \lambda,\ T \to FT',\ T' \to *FT' \mid \lambda,\ F \to (E) \mid id$
>
> $\text{PRIMERO}(E) = \text{PRIMERO}(T) = \text{PRIMERO}(F) = \{(, id\}$; $\text{PRIMERO}(E') = \{+, \lambda\}$; $\text{PRIMERO}(T') = \{*, \lambda\}$.
> $\text{SIGUIENTE}(E) = \text{SIGUIENTE}(E') = \{\$, )\}$; $\text{SIGUIENTE}(T) = \text{SIGUIENTE}(T') = \{+, \$, )\}$; $\text{SIGUIENTE}(F) = \{*, +, \$, )\}$.
>
> | No term. | $id$ | $+$ | $*$ | $($ | $)$ | $\$$ |
> |----------|------|-----|-----|-----|-----|------|
> | $E$  | $E{\to}TE'$ | | | $E{\to}TE'$ | | |
> | $E'$ | | $E'{\to}{+}TE'$ | | | $E'{\to}\lambda$ | $E'{\to}\lambda$ |
> | $T$  | $T{\to}FT'$ | | | $T{\to}FT'$ | | |
> | $T'$ | | $T'{\to}\lambda$ | $T'{\to}{*}FT'$ | | $T'{\to}\lambda$ | $T'{\to}\lambda$ |
> | $F$  | $F{\to}id$ | | | $F{\to}(E)$ | | |

> [!warning] No toda gramática puede hacerse LL(1)
> La gramática if-then-else factorizada $S \to iEtSS' \mid a,\ S' \to eS \mid \lambda,\ E \to b$ **no tiene** recursividad izquierda ni necesita factorización, pero es **ambigua**, por lo que no es LL(1): la celda $M[S', e]$ tiene dos producciones ($S' \to eS$ y $S' \to \lambda$).

## Análisis predictivo no recursivo · controlado por tabla

Mantiene una **pila explícita** en vez de llamadas recursivas. Imita una derivación por la izquierda: si $\omega$ es lo relacionado, la pila contiene $\alpha$ tal que $S \Rightarrow^{*}_{lm} \omega\alpha$.

> [!note] Componentes
> Buffer de entrada (con $\$$ al final), pila (con $\$$ en el fondo y $S$ arriba al inicio), tabla $M$ y flujo de salida. Considera $X$ (tope de pila) y $a$ (entrada actual).

> [!note] Algoritmo
> ```
> Config inicial: ω$ en entrada; S sobre $ en la pila.
> Sea a = primer símbolo de ω; X = tope de la pila
> Mientras (X ≠ $):
>   Si (X == a): desapilar X, consumir a
>   Sino si (X terminal): error()
>   Sino si (M[X,a] es error): error()
>   Sino si (M[X,a] = X→Y1…Yk):
>     emitir X→Y1…Yk; desapilar X; apilar Yk…Y1 (Y1 en el tope)
>   X = tope de la pila
> ```

> [!example] Traza de $id+id*id$
> $E\$ \Rightarrow TE'\$ \Rightarrow FT'E'\$ \Rightarrow id\,T'E'\$$ → relaciona $id$ → $T'E'\$$ → $E'\$$ (emite $T'{\to}\lambda$) → $+TE'\$$ → relaciona $+$ → … → finalmente pila $\$$ y entrada $\$$, **aceptada**. Salida = derivación por la izquierda.

## Análisis Ascendente · Desplazamiento-Reducción

> [!definition] Análisis ascendente
> Proceso de **reducir** una cadena $\omega$ al símbolo inicial. En cada reducción, una subcadena $\beta$ que coincide con el cuerpo de $A \to \beta$ se reemplaza por $A$. El problema clave es **cuándo** reducir y **qué** producción aplicar. La clase más amplia de gramáticas para este método son las **LR**.

> [!definition] Conceptos clave
> - **Reducción:** reemplazar $\beta$ (cuerpo de $A \to \beta$) por $A$. Es el proceso inverso a una derivación.
> - **Pivote:** en $\alpha\rho\beta$ (forma sentencial), $\rho$ es pivote sii $\exists (N \to \rho) \in P$ y $S \Rightarrow^{*} \alpha N\beta \Rightarrow \alpha\rho\beta$. Cuando $\rho$ está en el tope de la pila, se puede reducir.
> - **Desplazamiento (shift):** mover un símbolo de la entrada al tope de la pila.
> - **Prefijo viable:** dada $\alpha\rho\beta$ (forma sentencial derecha, $\rho$ pivote), $\gamma$ es prefijo viable si es prefijo de $\alpha\rho$. El contenido de la pila siempre es un prefijo viable.

> [!example] Pivotes y prefijos viables
> $S \to ABC,\ A \to aa,\ B \to bb,\ C \to cc$. **Pivotes:** $aa, bb, cc, ABC$. **Prefijos viables:** $A, AB, ABc, ABcc, aab, Abbc, Abb, aa, a, Ab$, etc.

> [!note] Algoritmo de Desplazamiento-Reducción
> Config inicial: $\$$ en el fondo de la pila, $\omega\$$ en la entrada.
> ```
> Repetir:
>   1. Desplazar cero o más símbolos de entrada a la pila.
>   2. Reducir una cadena β del tope de la pila a A, si existe A→β.
> Hasta error, o (pila == $S y entrada == $)   → aceptar
> ```

> [!example] Traza de $id*id$ con $E \to E+T \mid T,\ T \to T*F \mid F,\ F \to (E) \mid id$
> $\$ \;|\; id \Rightarrow \$id$ (F→id) $\Rightarrow \$F$ (T→F) $\Rightarrow \$T$ · shift $*$ · shift $id$ · (F→id) $\Rightarrow \$T*F$ (T→T*F) $\Rightarrow \$T$ (E→T) $\Rightarrow \$E$ · **aceptar**.
> Derivación inversa: $id*id \Rightarrow F*id \Rightarrow T*id \Rightarrow T*F \Rightarrow T \Rightarrow E$ (derivación **más a la derecha** revertida).

> [!warning] Conflictos
> Hay GLC para las que este método no sirve porque, conociendo la pila completa y el siguiente símbolo, no se puede decidir:
> - **Conflicto D-R** (Desplazamiento-Reducción): ¿desplazar o reducir?
> - **Conflicto R-R** (Reducción-Reducción): ¿qué reducción realizar?

## Análisis LR

> [!definition] LR(k)
> **L**eft to right, **R**ightmost derivation in reverse (derivaciones por derecha revertidas), **k** símbolos de anticipación.
>
> La clase de gramáticas **LR** es un **superconjunto** de las **LL**: las gramáticas LR describen más lenguajes que las LL.

## Ítems y autómata LR(0)

> [!definition] Ítem LR(0)
> Una producción con un **punto** en cierta posición: $[A \to \alpha_1 \bullet \alpha_2]$. La producción $A \to XYZ$ genera cuatro ítems:
> - $[A \to \bullet XYZ]$ (inicial), $[A \to X \bullet YZ]$, $[A \to XY \bullet Z]$ (intermedios), $[A \to XYZ \bullet]$ (**completo**: puede reducirse $XYZ$ a $A$).
>
> $A \to \lambda$ genera un solo ítem $[A \to \bullet]$. Un **estado** es un conjunto de ítems.

> [!definition] Gramática aumentada
> Si $G$ tiene símbolo inicial $S$, entonces $G'$ es $G$ con un nuevo símbolo inicial $S'$ y la producción $S' \to S$.

> [!note] CLAUSURA(I)
> ```
> J = I
> Repetir:
>   para cada [A → α•Bβ] en J:
>     para cada B → γ en G:
>       agregar [B → •γ] a J
> hasta que no se agreguen elementos
> ```

> [!example] CLAUSURA con $E' \to E,\ E \to E+T \mid T,\ T \to T*F \mid F,\ F \to (E) \mid id$
> $\text{CLAUSURA}(\{[E' \to \bullet E]\}) = \{ [E'{\to}\bullet E], [E{\to}\bullet E{+}T], [E{\to}\bullet T], [T{\to}\bullet T{*}F], [T{\to}\bullet F], [F{\to}\bullet(E)], [F{\to}\bullet id] \}$

> [!note] IR-A (GOTO)
> $\text{IR-A}(I, X) = \text{CLAUSURA}(\{[A \to \alpha X \bullet \beta] : [A \to \alpha \bullet X\beta] \in I\})$. Especifica la **transición** del estado $I$ con entrada $X$ en el autómata LR(0).

> [!note] Colección canónica LR(0)
> ```
> C = CLAUSURA({[S' → •S]})
> Repetir:
>   para cada conjunto I en C, para cada símbolo X:
>     si IR-A(I,X) ≠ ∅ y IR-A(I,X) ∉ C: agregar IR-A(I,X) a C
> hasta que no se agreguen conjuntos
> ```
> Los conjuntos de ítems son los **estados**; $\text{IR-A}$ son las **transiciones**. Estado inicial: $\text{CLAUSURA}(\{[S' \to \bullet S]\})$.

## Estructura y algoritmo del analizador LR

> [!note] Componentes
> Entrada, salida, **pila** (secuencia de estados $s_0, s_1, \dots, s_m$), programa controlador (igual para todos los LR) y **tabla** con dos partes: **ACCIÓN** e **IR-A**. Sólo la tabla cambia entre analizadores.

> [!definition] Tabla LR
> **ACCIÓN$[i, a]$** (estado $i$, terminal $a$ o $\$$): puede ser
> - **Desplazar $j$** (shift): mete $a$ con estado $j$ en la pila.
> - **Reducir $A \to \beta$:** reemplaza $\beta$ del tope por $A$.
> - **Aceptar.**
> - **Error.**
>
> **IR-A$[i, A]$** (estado $i$, no terminal $A$) $= j$: si $\text{IR-A}(I_i, A) = I_j$.

> [!note] Algoritmo LR
> ```
> Config inicial: s0 en la pila, ω$ en la entrada.
> Sea a = primer símbolo de ω$
> Mientras(1):
>   s = tope de la pila
>   Según ACCION[s,a]:
>     desplazar t: meter t en la pila; consumir a
>     reducir A→β: sacar |β| símbolos; sea t nuevo tope; apilar IR-A[t,A]; emitir A→β
>     aceptar: break
>     error: ManejarError()
> ```

> [!example] Traza de $id*id+id$ (gramática de expresiones aumentada)
> Producciones: 0.$E'{\to}E$ 1.$E{\to}E{+}T$ 2.$E{\to}T$ 3.$T{\to}T{*}F$ 4.$T{\to}F$ 5.$F{\to}(E)$ 6.$F{\to}id$.
> La pila alterna estados y símbolos: shift $id$(5), reduce F→id, reduce T→F, shift $*$(7), shift $id$(5), reduce F→id, reduce T→T*F, reduce E→T, shift $+$(6), shift $id$(5), reduce F→id, reduce T→F, reduce E→E+T, **aceptar**.

## Tabla SLR(1)

> [!note] Algoritmo de construcción SLR(1)
> 1. Construir $C = \{I_0, \dots, I_n\}$, la colección LR(0) de $G'$.
> 2. Para el estado $i$ (de $I_i$):
>     - (a) Si $a \in \Sigma$, $[A \to \alpha \bullet a\beta] \in I_i$ y $\text{IR-A}(I_i, a) = I_j$: $\text{ACCIÓN}[i, a] = \text{desplazar } j$.
>     - (b) Si $[A \to \alpha \bullet] \in I_i$: $\text{ACCIÓN}[i, a] = \text{reducir } A \to \alpha$ para **todo** $a \in \text{SIGUIENTE}(A)$ (con $A$ = $S'$ o no).
>     - (c) Si $[S' \to S \bullet] \in I_i$: $\text{ACCIÓN}[i, \$] = \text{aceptar}$.
> Si hay acción conflictiva, la gramática **no es SLR(1)**.
> 3. Si $\text{IR-A}(I_i, A) = I_j$: $\text{IR-A}[i, A] = j$.
> 4. Las entradas no definidas quedan como **error**.
> 5. Estado inicial: el que contiene $[S' \to \bullet S]$.

> [!important] Relación de clases
> Toda gramática **SLR(1) es no ambigua**. Pero **no toda gramática no ambigua es SLR(1)**.

## Analizadores más potentes · LR(1) canónico y LALR

> [!info] Dos métodos
> 1. **LR canónico** (LR): usa ítems **LR(1)**.
> 2. **LALR** (Look-Ahead LR): tiene **menos estados** que los basados en LR(1); maneja más gramáticas que SLR con tablas no tan grandes.

> [!definition] Ítem LR(1)
> Tiene la forma $[A \to \alpha \bullet \beta,\ t]$, donde $A \to \alpha\beta$ es una producción y $t$ es un terminal o $\$$ (símbolo de anticipación de longitud 1, que da nombre al método).

> [!note] CLAUSURA para LR(1)
> ```
> J = I
> Repetir:
>   para cada [A → α•Bβ, t] en J:
>     para cada B → γ en G':
>       para cada terminal b ∈ PRIMERO(βt):
>         agregar [B → •γ, b] a J
> hasta que no se agreguen elementos
> ```
> $\text{IR-A}(I, X)$: para cada $[A \to \alpha \bullet X\beta, t] \in I$, agregar $[A \to \alpha X \bullet \beta, t]$.

> [!example] $S' \to S,\ S \to CC,\ C \to cC \mid d$
> $I_0 = \{[S \to \bullet S, \$],\ [S \to \bullet CC, \$],\ [C \to \bullet cC, c/d],\ [C \to \bullet d, c/d]\}$

> [!note] Tabla LR(1) canónica
> Igual que SLR pero: (b) si $[A \to \alpha \bullet,\ a] \in I_i$ con $A \neq S'$, $\text{ACCIÓN}[i, a] = \text{reducir } A \to \alpha$ (usa el look-ahead del ítem, **no** SIGUIENTE(A)). Si hay conflicto, la gramática **no es LR(1)**.

> [!definition] Núcleo (core) y LALR
> El **núcleo** de $[A \to \alpha \bullet \beta,\ t]$ es su primer componente $A \to \alpha\beta$. Los ítems con el mismo núcleo pueden **fusionarse** en un solo conjunto uniendo sus look-aheads. Ejemplo: $I_{36} = \{[C \to c \bullet C,\ c/d/\$],\ [C \to \bullet cC,\ c/d/\$],\ [C \to \bullet d,\ c/d/\$]\}$.

> [!note] Algoritmo tabla LALR
> 1. Construir la colección LR(1).
> 2. Para cada núcleo, **reemplazar** los ítems con ese núcleo por su **unión**.
> 3. Sea $C' = \{J_0, \dots, J_n\}$; construir ACCIÓN como en LR(1). Si hay conflicto, la gramática **no es LALR(1)**.
> 4. Si $J = I_1 \cup \dots \cup I_k$, los núcleos de $\text{IR-A}(I_i, X)$ coinciden, y $\text{IR-A}(J, X) = K$ (unión de los conjuntos con ese núcleo).

## Generador de analizadores sintácticos · Yacc

> [!info] Yacc (Yet Another Compiler-Compiler)
> Programa que, dada la especificación de una gramática, genera otro programa para analizar y traducir archivos de esa gramática. El más conocido usa el método **LALR**.
> - `traducir.y`: contiene la gramática del lenguaje $L$.
> - `y.tab.c`: analizador LALR generado, escrito en C.
> - Compilado produce `a.out`: el **compilador/traductor** que traduce entradas en $L$.

---
*Anterior ← [[6 - Gramáticas Libres de Contexto y Lema de Bombeo]] · Continúa en → [[8 - Gramáticas con Atributos]]*
