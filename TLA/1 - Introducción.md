---
tema: 1
titulo: Introducción
materia: Autómatas, Teoría de Lenguajes y Compiladores
autor: Lic. Ana María Arias Roig
tags:
  - TLA
  - teoria-de-lenguajes
  - autómatas
  - introducción
  - gramáticas
---

# 1 · Introducción

> [!abstract] Índice del tema
> - [[#¿Qué es la teoría de autómatas?]]
> - [[#Conceptos fundamentales]]
> - [[#Definiciones recursivas]]
> - [[#Inducción estructural]]
> - [[#Gramáticas]]
> - [[#Clasificación de gramáticas · Jerarquía de Chomsky]]

## ¿Qué es la teoría de autómatas?

La teoría de autómatas es el estudio de **"máquinas abstractas"**.

Ya en los años 30, antes de que existieran las computadoras, **Alan Turing** estudió las máquinas abstractas e intentó describir de forma precisa los límites entre lo que una máquina de cálculo podía y no podía hacer.

La investigación de estas máquinas abstractas permitió modelar el funcionamiento de una computadora ideal y también separar aquellos problemas que se podían resolver de forma eficiente mediante una computadora de aquellos que son insolubles (o *NP-difíciles*).

El estudio de las máquinas abstractas se complementa con el de las **gramáticas formales**, idea de **Noam Chomsky** para modelar los lenguajes.

> [!note] ¿Para qué sirve?
> - Los autómatas y determinados tipos de gramáticas formales se emplean en el diseño y construcción de software.
> - Las **máquinas de Turing** ayudan a comprender lo que podemos esperar de nuestro software.
> - La teoría de los problemas intratables nos permite deducir si podremos enfrentarnos a un problema y escribir un programa para resolverlo o si, por el contrario, tenemos que hallar una forma diferente de resolverlo (una aproximación, un método heurístico u otra).

## Conceptos fundamentales

> [!definition] Alfabeto
> Un **alfabeto** $\Sigma$ es un conjunto finito no vacío de símbolos.
>
> **Ejemplos:**
> 1. $\Sigma = \{0, 1\}$, el alfabeto binario.
> 2. $\Sigma = \{a, b, c, \dots, z\}$, el alfabeto de letras minúsculas.

> [!definition] Cadena (o palabra)
> Una **cadena** o **palabra** es una secuencia finita de símbolos seleccionados de algún alfabeto.
>
> **Ejemplo:** $00001010$ es una palabra dentro del alfabeto binario.

> [!definition] Longitud de una cadena
> La **longitud** de una cadena es la cantidad de posiciones que ocupan los símbolos que tiene.
>
> **Ejemplo:** $|00001010| = 8$.

> [!definition] Cadena vacía
> La **cadena vacía** es una cadena de longitud $0$. La denotaremos con $\lambda$.
>
> Aunque en alguna bibliografía también se denota con el símbolo $\varepsilon$.

### Potencias de un alfabeto

Si $\Sigma$ es un alfabeto, podemos expresar el conjunto de todas las cadenas de una determinada longitud de dicho alfabeto utilizando una notación exponencial:

$$\Sigma^{k} = \{ w : |w| = k,\ w \text{ sobre } \Sigma \}$$

> [!example]
> Si $\Sigma = \{0, 1\}$, entonces:
> $$\Sigma^{0} = \{\lambda\}$$
> $$\Sigma^{1} = \{0, 1\}$$
> $$\Sigma^{2} = \{00, 01, 10, 11\}$$
> $$\Sigma^{3} = \{000, 001, 010, 011, 100, 101, 110, 111\}$$
> Etc.

### Clausuras de un alfabeto

> [!definition] Clausura de Kleene y clausura positiva
> A la unión generalizada de todas las potencias de un alfabeto se la denomina **clausura de Kleene**:
> $$\Sigma^{*} = \bigcup_{i=0}^{\infty} \Sigma^{i}$$
>
> Si se excluye la cadena vacía se denomina **clausura positiva**:
> $$\Sigma^{+} = \bigcup_{i=1}^{\infty} \Sigma^{i} = \Sigma^{*} - \{\lambda\}$$

### Concatenación de cadenas

Sean $x$ e $y$ dos cadenas. Entonces $xy$ denota la **concatenación** de $x$ e $y$, es decir, la cadena formada por una copia de $x$ seguida de una copia de $y$.

Si $x$ es la cadena compuesta por $i$ símbolos $x = a_1 a_2 \dots a_i$ y $y$ es la cadena compuesta por $j$ símbolos $y = b_1 b_2 \dots b_j$, entonces $xy$ es la cadena de $i+j$ símbolos:
$$xy = a_1 a_2 \dots a_i\, b_1 b_2 \dots b_j$$

> [!definition] Prefijos y sufijos
> Si $z$ está formada por la concatenación de las cadenas $x$ e $y$ ($z = xy$), se dice que:
> - $x$ es **prefijo** de $z$.
> - $y$ es **sufijo** (posfijo) de $z$.
>
> Se llama **prefijo propio** (o posfijo propio) si es distinto de $\lambda$.

> [!theorem] Propiedades de la concatenación
> - **Cerrada:** $\forall x, y \in \Sigma^{*} : x \cdot y \in \Sigma^{*}$ (la concatenación de palabras es otra palabra sobre el mismo alfabeto).
> - **Asociatividad:** $\forall x, y, z \in \Sigma^{*} : x(yz) = (xy)z$.
> - **Elemento neutro:** $\forall x \in \Sigma^{*} : \lambda x = x \lambda = x$.

### Reverso de una palabra

> [!definition] Reverso (o reflejo)
> Si $w = a_1 a_2 \dots a_n$ es una palabra sobre $\Sigma$, entonces la palabra **inversa** o **refleja** de $w$ se define como:
> $$w^{R} = a_n a_{n-1} \dots a_1$$

### Lenguaje sobre un alfabeto

> [!definition] Lenguaje
> Un **lenguaje** sobre $\Sigma$ es cualquier subconjunto de $\Sigma^{*}$. Es decir:
> $$L \subseteq \Sigma^{*}$$

### Operaciones con lenguajes

Como con cualquier conjunto, se pueden realizar las operaciones de **unión**, **intersección** y **diferencia** de lenguajes. Además existen las siguientes:

> [!definition] Operaciones específicas
> - **Producto (concatenación) de lenguajes:**
> $$L_1 \cdot L_2 = \{ w : w = xy,\ x \in L_1 \wedge y \in L_2 \}$$
> - **Potencia de lenguajes:** el lenguaje resultante de concatenar el lenguaje consigo mismo $i$ veces.
> $$L^{i} = \underbrace{L \cdot L \cdots L}_{i \text{ veces}}$$
> - **Clausura positiva de un lenguaje:**
> $$L^{+} = \bigcup_{i=1}^{\infty} L^{i}$$
> - **Clausura de Kleene de un lenguaje:**
> $$L^{*} = \bigcup_{i=0}^{\infty} L^{i}$$

## Definiciones recursivas

Las **definiciones recursivas** tienen un **caso base**, en el que se definen una o más estructuras elementales, y un **paso de inducción**, en el que se definen estructuras más complejas en términos de estructuras previamente definidas.

> [!definition] Definición alternativa de cadena
> Formalmente las cadenas pueden definirse inductivamente a partir de una constante —la cadena vacía— y de un constructor $\cdot$ que permite agregar un símbolo a la cabeza de una cadena.
> - **Base:** $\lambda$ es una cadena.
> - **Paso inductivo:** si $t \in \Sigma$ y $\alpha$ ya es una cadena, entonces $t \cdot \alpha$ es una cadena.

> [!definition] Definición alternativa de potencia de un alfabeto
> Se puede definir $\Sigma^{i}$ inductivamente como:
> - **Base:** si $i = 0$, entonces $\Sigma^{i} = \{\lambda\}$.
> - **Paso inductivo:** si $i > 0$, entonces $\Sigma^{i} = \{ a\alpha : a \in \Sigma,\ \alpha \in \Sigma^{i-1} \}$.

> [!definition] Definición alternativa de reverso de una palabra
> - **Base:** el reverso de $\lambda$ es $\lambda$.
> - **Paso inductivo:** si $t \in \Sigma$ y $\alpha \in \Sigma^{*}$, entonces $(t\alpha)^{R} = (\alpha)^{R}\, t$.

## Inducción estructural

Cuando una estructura fue definida recursivamente, se pueden probar teoremas acerca de ella utilizando la siguiente forma de demostración, que recibe el nombre de **inducción estructural**.

Sea $S(X)$ una proposición acerca de estructuras $X$ definidas mediante alguna definición recursiva determinada.

> [!note] Esquema de inducción estructural
> 1. Como **base**, se prueba $S(X)$ para la(s) estructura(s) base $X$.
> 2. Para el **paso de inducción**, se toma una estructura $X$ que, según la definición recursiva, está formada a partir de $Y_1, Y_2, \dots, Y_k$; se dan por ciertas las proposiciones $S(Y_1), S(Y_2), \dots, S(Y_k)$ y se utilizan para probar $S(X)$.

> [!example] "El número de nodos de un árbol es superior al de arcos en una unidad"
> **Definición recursiva de un ÁRBOL:**
> - **Base:** un único nodo es un árbol.
> - **Paso inductivo:** si $T_1, T_2, \dots, T_k$ son árboles, se puede construir un nuevo árbol así:
>   1. Se comienza con un nuevo nodo $N$, que es la raíz del árbol.
>   2. Se añaden copias de todos los árboles $T_1, T_2, \dots, T_k$.
>   3. Se añaden arcos desde el nodo $N$ hasta las raíces de cada uno de los árboles $T_1, T_2, \dots, T_k$.
>
> **Prueba:** "Si $T$ es un árbol con $n$ nodos y $e$ arcos, entonces $n = e + 1$."
>
> **Base:** el caso base ocurre cuando $T$ es un único nodo. Entonces hay $0$ arcos y se cumple $1 = 0 + 1$, así que $n = e + 1$ es verdadera.
>
> **Paso inductivo:** sea $T$ un árbol construido de la forma indicada. Se da por cierto que la propiedad se cumple para $T_1, T_2, \dots, T_k$; entonces para cada uno $n_i = e_i + 1$.
> - Total de nodos del nuevo árbol: $n = n_1 + n_2 + \dots + n_k + 1$ (todos los nodos de cada árbol más el nodo raíz).
> - Total de arcos del nuevo árbol: $e = e_1 + e_2 + \dots + e_k + k$ (todos los arcos de cada árbol más los que unen el nodo raíz con cada árbol).
>
> Como la propiedad se cumple para cada $T_i$, el total de nodos es:
> $$(e_1 + 1) + (e_2 + 1) + \dots + (e_k + 1) + 1 = e_1 + e_2 + \dots + e_k + k + 1 = e + 1$$

## Gramáticas

> [!definition] Gramática
> Una **gramática** es un sistema matemático para definir un lenguaje. Define la estructura de las palabras de un lenguaje.
>
> Es una 4-tupla $G = (N, \Sigma, P, S)$, donde:
> - $N$ es un conjunto finito de símbolos **no terminales** (variables o categorías sintácticas).
> - $\Sigma$ es un conjunto finito de símbolos **terminales**, con $N \cap \Sigma = \varnothing$.
> - $P$ es un conjunto de **producciones**. Un elemento $(\alpha, \beta) \in P$ se escribe $\alpha \to \beta$ y se llama producción.
> - $S$ es un símbolo distinguido en $N$, llamado **sentencia** o **símbolo inicial**.

> [!definition] Forma sentencial
> La **forma sentencial** de una gramática es una cadena especial que se define recursivamente:
> - **Base:** $S$ es una forma sentencial.
> - **Paso inductivo:** si $\alpha\beta\gamma$ es una forma sentencial y $\beta \to \delta \in P$, entonces $\alpha\delta\gamma$ también es una forma sentencial.
>
> Una forma sentencial de $G$ que sólo contiene símbolos terminales (o es la palabra vacía) se llama **sentencia** generada por $G$.

> [!definition] Derivación
> - **Derivación** ($\Rightarrow_G$): si $\alpha\beta\gamma$ es una cadena en $(N \cup \Sigma)^{*}$ y $\beta \to \delta$ es una producción, entonces $\alpha\beta\gamma \Rightarrow_G \alpha\delta\gamma$.
> - **Derivación** $\Rightarrow^{*}_G$: en $0$ o más pasos.

> [!definition] Lenguaje generado por una gramática
> El lenguaje generado por una gramática $G$, es decir $L(G)$, es el conjunto de sentencias generadas por $G$. Usando el concepto de derivación:
> $$L(G) = \{ \omega \in \Sigma^{*} : S \Rightarrow^{*} \omega \}$$

## Clasificación de gramáticas · Jerarquía de Chomsky

Las gramáticas pueden clasificarse según el formato de sus producciones. Si un lenguaje es generado por una gramática de tipo $X$, entonces el lenguaje es de tipo $X$.

> [!info] Tipo 0 · Gramáticas sin restricciones
> Son las más generales. Las producciones pueden ser de cualquier tipo permitido, es decir de la forma $\alpha \to \beta$ con $\alpha, \beta \in (N \cup \Sigma)^{*}$ y $\alpha \neq \lambda$.
>
> Los lenguajes generados son los **lenguajes con estructura de frase** (clase $L_0$), también conocidos como **lenguajes recursivamente enumerables**.

> [!info] Tipo 1 · Gramáticas sensibles al contexto
> Las producciones son de la forma $\alpha \to \beta$ con $|\alpha| \le |\beta|$, excepto para $S \to \lambda$.
>
> Los lenguajes generados son los **lenguajes sensibles al contexto** ($L_1$).

> [!info] Tipo 2 · Gramáticas libres de contexto
> Las producciones son de la forma $A \to \beta$ (con $A \in N$).
>
> Los lenguajes generados son los **lenguajes libres de contexto** ($L_2$). Ver [[6 - Gramáticas Libres de Contexto y Lema de Bombeo]].

> [!info] Tipo 3 · Gramáticas regulares
> - **Lineales por derecha:** producciones de la forma $A \to aB$ o $A \to a$.
> - **Lineales por izquierda:** producciones de la forma $A \to Ba$ o $A \to a$.
>
> Los lenguajes generados son los **lenguajes regulares** ($L_3$). Ver [[4 - Lenguajes Regulares]].

> [!summary] Resumen de la jerarquía
> $$L_3 \subset L_2 \subset L_1 \subset L_0$$
> | Tipo | Gramática | Lenguaje | Reconoce |
> |------|-----------|----------|----------|
> | 0 | Sin restricciones | Recursivamente enumerable | [[9 - Máquinas de Turing\|Máquina de Turing]] |
> | 1 | Sensible al contexto | Sensible al contexto | Autómata linealmente acotado |
> | 2 | Libre de contexto | Libre de contexto | [[5 - Autómatas de Pila\|Autómata de pila]] |
> | 3 | Regular | Regular | [[2 - Autómatas Finitos\|Autómata finito]] |

---
*Continúa en → [[2 - Autómatas Finitos]]*
