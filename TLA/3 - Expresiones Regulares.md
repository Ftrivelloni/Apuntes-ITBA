---
tema: 3
titulo: Expresiones Regulares
materia: Autómatas, Teoría de Lenguajes y Compiladores
autor: Lic. Ana María Arias Roig
tags:
  - TLA
  - expresiones-regulares
  - lenguajes-regulares
  - kleene
  - lema-de-arden
---

# 3 · Expresiones Regulares

> [!abstract] Índice del tema
> - [[#Definición · construcción recursiva]]
> - [[#Lenguaje descripto por una ER]]
> - [[#Precedencia de los operadores]]
> - [[#Propiedades de las Expresiones Regulares]]
> - [[#Autómatas Finitos y Expresiones Regulares]]
> - [[#Conversión de un AFD en una ER · Teorema de Análisis de Kleene]]
> - [[#Conversión de ER en autómatas · Teorema de Síntesis de Kleene]]

Las expresiones regulares pueden definir los mismos lenguajes que describen los distintos tipos de autómatas: los **lenguajes regulares**. Sin embargo, las ER ofrecen una forma **declarativa** para expresar las cadenas que se desea aceptar.

## Definición · construcción recursiva

> [!definition] Expresión regular (ER)
> Dado un alfabeto $\Sigma$, los símbolos $\lambda$, $\varnothing$ y los operadores $+$ (unión), $\cdot$ (concatenación) y $*$ (clausura) y los paréntesis, se define una **ER** sobre $\Sigma$ como:
>
> **Base:**
> - El símbolo $\varnothing$ es una ER.
> - El símbolo $\lambda$ es una ER.
> - Cualquier símbolo $a \in \Sigma$ es una ER.
>
> **Paso inductivo** (si $\alpha$ y $\beta$ son ER):
> - $\alpha + \beta$ es una ER.
> - $\alpha \cdot \beta$ es una ER.
> - $\alpha^{*}$ es una ER.
> - $(\alpha)$ es una ER.

## Lenguaje descripto por una ER

> [!definition] $L(\alpha)$
> **Base:**
> - Si $\alpha = \varnothing$, entonces $L(\alpha) = \varnothing$.
> - Si $\alpha = \lambda$, entonces $L(\alpha) = \{\lambda\}$.
> - Si $\alpha = a$ con $a \in \Sigma$, entonces $L(\alpha) = \{a\}$.
>
> **Paso inductivo** (si $\alpha$, $\beta$ son ER):
> - $L(\alpha + \beta) = L(\alpha) \cup L(\beta)$
> - $L(\alpha \cdot \beta) = L(\alpha) \cdot L(\beta)$
> - $L(\alpha^{*}) = (L(\alpha))^{*}$
> - $L((\alpha)) = L(\alpha)$

## Precedencia de los operadores

> [!note] Orden de precedencia (de mayor a menor)
> 1. **Asterisco** $*$ — el de mayor precedencia.
> 2. **Concatenación** ("punto") — asociativa; si hay que elegir, se aplica por la izquierda. Ej.: $012$ se aplica como $(01)2$.
> 3. **Unión** $+$ — asociativa; se calcula empezando por la izquierda.

## Propiedades de las Expresiones Regulares

> [!definition] Equivalencia de ER
> Dos ER $r_1$ y $r_2$ son **equivalentes** si describen el mismo lenguaje: $L(r_1) = L(r_2)$.

> [!theorem] Propiedades de la unión $+$
> - **Asociativa:** $(\alpha + \beta) + \gamma = \alpha + (\beta + \gamma)$
> - **Conmutativa:** $\alpha + \beta = \beta + \alpha$
> - **Neutro:** $\alpha + \varnothing = \alpha$
> - **Idempotencia:** $\alpha + \alpha = \alpha$
>
> *Se demuestran usando $L(\alpha + \beta) = L(\alpha) \cup L(\beta)$ y las propiedades de la unión de conjuntos.*

> [!theorem] Propiedades de la concatenación
> - **Neutro:** $\alpha \cdot \lambda = \alpha$
> - **Absorbente (neutro de $+$):** $\alpha \cdot \varnothing = \varnothing$
> - **Asociativa:** $(\alpha\beta)\gamma = \alpha(\beta\gamma)$
> - **Distributiva respecto de $+$:** $\alpha(\beta + \gamma) = \alpha\beta + \alpha\gamma$
>
> *Demostración de $\alpha\cdot\varnothing = \varnothing$:* como $L(\alpha\cdot\varnothing) = L(\alpha)\cdot L(\varnothing) = L(\alpha)\cdot\varnothing$ y por definición del producto de lenguajes se requiere $\omega_2 \in \varnothing$ (imposible), el resultado es $\varnothing$.

> [!theorem] Clausura de $\lambda$ y de $\varnothing$
> $$\lambda^{*} = \lambda \qquad \varnothing^{*} = \lambda$$
> *Demostración:* $\varnothing^{*} = \bigcup_{i=0}^{\infty}\varnothing^{i} = \varnothing^{0} \cup \varnothing^{1} \cup \dots = \{\lambda\} \cup \varnothing \cup \dots = \{\lambda\}$. Análogo para $\lambda^{*}$.

## Autómatas Finitos y Expresiones Regulares

Las ER definen los mismos lenguajes que los autómatas finitos. Como los AFD, AFND y AFND-λ definen los mismos lenguajes (ver [[2 - Autómatas Finitos]]), alcanza con mostrar que:

> [!important] Doble inclusión
> 1. Todo lenguaje definido mediante un **AFD** también se define mediante una **ER**.
> 2. Todo lenguaje definido por una **ER** puede definirse mediante un **AFND-λ**.

## Conversión de un AFD en una ER · Teorema de Análisis de Kleene

> [!theorem] Teorema de Análisis de Kleene
> Si $L$ es un lenguaje aceptado por un autómata finito $M$, entonces existe una ER $\alpha$ tal que $L = L(M) = L(\alpha)$.

### Ecuaciones de expresiones regulares

Una **ecuación de ER** con incógnitas $x_1, x_2, \dots, x_n$ es del tipo:
$$x_i = \alpha_{i0} + \alpha_{i1} x_1 + \dots + \alpha_{in} x_n$$
donde cada coeficiente $\alpha_{ij}$ es una ER. A una ecuación de la forma $X = \alpha X + \beta$ se la llama **ecuación fundamental**.

> [!theorem] Lema de Arden
> Sea $X = \alpha X + \beta$ la ecuación fundamental. Entonces $X = \alpha^{*}\beta$ es una solución, y es **única** si $\lambda \notin L(\alpha)$. Es decir:
> $$X = \alpha X + \beta \iff X = \alpha^{*}\beta$$
>
> *Demostración ($\Leftarrow$, verificación):*
> $X = \alpha^{*}\beta = (\alpha^{+} + \lambda)\beta = \alpha^{+}\beta + \beta = (\alpha\alpha^{*})\beta + \beta = \alpha(\alpha^{*}\beta) + \beta = \alpha X + \beta$.
>
> *Demostración ($\Rightarrow$):* se prueba $X \subseteq \alpha^{*}\beta$ y $\alpha^{*}\beta \subseteq X$ por inducción en $|\omega|$.
> - **Base** $|\omega|=0$: $\omega = \lambda \in X$; como $\lambda \notin \alpha$, entonces $\omega \notin \alpha X$, luego $\omega = \lambda \in \beta \subseteq \alpha^{*}\beta$.
> - **Paso inductivo:** si $\omega \in \beta$, listo. Si $\omega \notin \beta$, entonces $\omega \in \alpha X$, o sea $\omega = \omega_1\omega_2$ con $\omega_1 \in \alpha$ ($|\omega_1|\ge 1$) y $\omega_2 \in X$ ($|\omega_2| < |\omega|$). Por hipótesis inductiva $\omega_2 \in \alpha^{*}\beta$, luego $\omega \in \alpha(\alpha^{*}\beta) = \alpha^{+}\beta \subseteq \alpha^{*}\beta$.
>
> **Unicidad** (si $\lambda \notin L(\alpha)$): cualquier término espurio $\alpha^{n+1}S$ tendría longitud mínima $n+1$, lo que se descarta, forzando $S = \alpha^{*}\beta$.

> [!note] Algoritmo · ER a partir de un AF
> **Entrada:** $M = (Q, \Sigma, q_0, \delta, F)$. **Salida:** $\alpha$ tal que $L(\alpha) = L(M)$.
> 1. **Obtener las ecuaciones características.** $\forall q_i \in Q$, la ecuación tiene en el primer miembro el estado $q_i$ y en el segundo una suma de términos $a\,q_j$ por cada $\delta(q_i, a) = q_j$. Si $q_i \in F$, agregar el término $\lambda$.
> 2. **Resolver el sistema** usando el Lema de Arden y las propiedades de las ER.
> 3. La **solución para el estado inicial** es la ER buscada.

> [!example] Ejemplo completo
> $M = (\{q_0, q_1, q_2\}, \{0,1\}, q_0, \{q_1\}, \delta)$. Ecuaciones:
> $$q_0 = 0q_0 + 1q_1$$
> $$q_1 = 0q_0 + 1q_2 + \lambda$$
> $$q_2 = 1q_1 + 0q_2$$
> Desde la última, por Arden: $q_2 = 0^{*}1q_1$. Sustituyendo en la segunda:
> $$q_1 = 0q_0 + 10^{*}1q_1 + \lambda \;\Rightarrow\; q_1 = (10^{*}1)^{*}(0q_0 + \lambda)$$
> Sustituyendo en la primera:
> $$q_0 = 0q_0 + 1(10^{*}1)^{*}(0q_0 + \lambda) = 0q_0 + 1(10^{*}1)^{*}0q_0 + 1(10^{*}1)^{*}$$
> Por distributiva y Arden, la única solución es:
> $$\boxed{q_0 = \big(0 + 1(10^{*}1)^{*}0\big)^{*}\, 1(10^{*}1)^{*}}$$

## Conversión de ER en autómatas · Teorema de Síntesis de Kleene

> [!theorem] Teorema de Síntesis de Kleene
> Si $L$ es el lenguaje asociado a la ER $\alpha$, existe un autómata finito $M$ tal que $L = L(M) = L(\alpha)$.

### Método de composición de autómatas

El autómata construido tiene un **único estado de aceptación** y **ningún arco** que entre al estado inicial o que salga del estado de aceptación. Se demuestra por **inducción estructural** sobre la ER.

> [!note] Base
> - $\alpha = \lambda$: autómata con $q_0 \xrightarrow{\lambda} q_f$, $L(M) = \{\lambda\}$.
> - $\alpha = \varnothing$: autómata sin arco, $L(M) = \varnothing$.
> - $\alpha = a_1$ con $a_1 \in \Sigma$: autómata con $q_0 \xrightarrow{a_1} q_f$, $L(M) = \{a_1\}$.

> [!note] Paso inductivo · combinadores de Thompson
> Suponiendo que cada subexpresión es el lenguaje de un AFND-λ con único estado de aceptación:
> - **Unión** $R_1 + R_2$: nuevo estado inicial con $\lambda$ hacia los iniciales de $R_1$ y $R_2$; sus estados de aceptación se unen con $\lambda$ a un nuevo estado final. $L(M) = L(R_1) \cup L(R_2)$.
> - **Concatenación** $R_1 R_2$: el inicial de $R_1$ es el inicial del conjunto; el de aceptación de $R_2$ es el final; se conectan en serie. $L(M) = L(R_1)L(R_2)$.
> - **Clausura** $R^{*}$: permite (a) ir directo del inicial al final por $\lambda$ (acepta $\lambda$) y (b) recorrer el autómata de $R$ una o más veces. Cubre $L(R^{+})$ y $\lambda$, es decir $L(R^{*})$.
> - **Paréntesis** $(R)$: el mismo autómata de $R$ sirve, pues $L((R)) = L(R)$.
>
> El autómata resultante mantiene: único estado de aceptación y ningún arco de entrada al inicial ni de salida del final.

---
*Anterior ← [[2 - Autómatas Finitos]] · Continúa en → [[4 - Lenguajes Regulares]]*
