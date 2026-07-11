# Cálculo de Probabilidades

## Motivación — El juego de cartas

Para introducir las ideas de probabilidad partimos de un experimento concreto. Supongamos que tenemos un mazo de 5 cartas numeradas del 1 al 5 y realizamos el siguiente procedimiento: se mezclan las cartas, se extrae una al azar, se registra su número, se repone la carta, se vuelven a mezclar y se extrae una segunda carta al azar registrando su número. Es decir, hacemos **dos extracciones con reposición**.

Antes de operar conviene hacerse dos preguntas. La primera: **¿se puede saber de antemano cuál va a ser el resultado?** Claramente no, porque las cartas se eligen al azar. Tomaremos como definición de **aleatorio** a aquellos fenómenos cuyo resultado no podemos predecir; en este caso estamos ante un **experimento aleatorio**.

La segunda pregunta es: **¿se puede saber de antemano cuáles son los resultados posibles?** Que no podamos anticipar el resultado no significa que no sepamos nada. Sabemos que hay dos extracciones, que se registran números del 1 al 5 y que pueden repetirse (porque se repone la carta). Podemos entonces describir el conjunto de resultados posibles, que es lo que llamamos **espacio muestral** $S$:

$$S = \{(i,j)\in\mathbb{N}^2 \;/\; 1 \le i,j \le 5\}$$

Este conjunto tiene los pares $(1,1), (1,2), \dots, (5,5)$, en total 25 resultados posibles.

> [!info] Definición
> El **espacio muestral** $S$ es el conjunto de todos los resultados posibles de un experimento aleatorio.

---

## Sucesos y álgebra de sucesos

Más allá de los números concretos que salgan, podríamos interesarnos por qué podría "suceder" en el experimento. Por ejemplo, definimos tres sucesos que reaparecerán durante toda la teoría:

- $A=$ los números extraídos son iguales.
- $B=$ los números extraídos suman un número impar.
- $C=$ el máximo número obtenido es por lo menos 4.

Lo importante es que cada uno de estos enunciados se identifica con un **subconjunto del espacio muestral**. A esos subconjuntos los llamamos **eventos** o **sucesos**:

- $A = \{(1,1);(2,2);(3,3);(4,4);(5,5)\} \subseteq S$
- $B = \{(1,2);(1,4);(2,1);(2,3);(2,5);(3,2);(3,4);(4,1);(4,3);(4,5);(5,2);(5,4)\} \subseteq S$
- $C = \{(1,4);(1,5);\dots;(5,4);(5,5)\} \subseteq S$

Cuando dos eventos no pueden ocurrir al mismo tiempo decimos que son **mutuamente excluyentes**. En el ejemplo, $A$ y $B$ lo son: si los números son iguales, su suma es par (no impar); y si la suma es impar, los números no pueden ser iguales.

Como los sucesos se comportan como conjuntos, podemos combinarlos con las operaciones habituales:

- **Complemento** $\overline{A}$: ocurre todo lo que no es $A$. Por ejemplo $\overline{C}=$ el máximo número obtenido es menor a 4.
- **Intersección** $A\cap B$: ocurren ambos. Dos sucesos son mutuamente excluyentes cuando su intersección es vacía: $A\cap B=\varnothing$, mientras que $A\cap C=\{(4,4);(5,5)\}$.
- **Unión** $A\cup B$: ocurre al menos uno de los dos.

Conviene recordar las **Leyes de De Morgan**, que se visualizan fácilmente con un diagrama de Venn (dos círculos $A$ y $B$ dentro del rectángulo $S$, donde el complemento de la unión es la región exterior a ambos círculos, y el complemento de la intersección es todo salvo la lúnula central):

$$\boxed{\overline{A\cup B} = \overline{A}\cap\overline{B} \qquad \overline{A\cap B} = \overline{A}\cup\overline{B}}$$

---

## Frecuencia, repetición y probabilidad

Sabemos que todos estos eventos pueden suceder, pero surge la pregunta: **¿algún suceso tiene más chance de ocurrir que otro?** Y para responderla, **¿cómo le damos un valor a esa "chance"?**

La clave es pensar en la **frecuencia** con la que ocurren los resultados. El problema es que el experimento se hace una única vez, y es imposible evaluar una frecuencia con un solo ensayo. Por eso recurrimos a una abstracción que será recurrente en toda la materia: imaginar un número grande $n$ de experimentos "imaginarios" y ver en cuántos ocurre cada evento.

Llamamos **frecuencia relativa** de un suceso $A$ a:

$$f_A = \frac{n_A}{n}$$

donde $n_A$ es la cantidad de veces que ocurre $A$ en $n$ experimentos equivalentes. Por ejemplo, simulando $n=50$ repeticiones del experimento de cartas se observó: $A$ ocurrió 10 veces, $B$ 25 veces y $C$ 29 veces, de modo que $f_A=0.2$, $f_B=0.5$ y $f_C=0.58$. Esto ya confirma la intuición de que $C$ es el evento más frecuente.

Si seguimos aumentando las repeticiones, las frecuencias relativas se **estabilizan** en un valor límite:

| $n$ | $f_A$ | $f_B$ | $f_C$ |
|:-:|:-:|:-:|:-:|
| 50 | 0.2000 | 0.5000 | 0.5800 |
| 100 | 0.2100 | 0.5000 | 0.6200 |
| 500 | 0.2120 | 0.4740 | 0.6260 |
| 1000 | 0.2010 | 0.4810 | 0.6400 |
| 10000 | 0.1963 | 0.4887 | 0.6342 |

A medida que $n\to\infty$ se observa $f_A\to 0.2$, $f_B\to 0.48$ y $f_C\to 0.64$.

Cuando hablamos de la **probabilidad** de un suceso $A$ (la notamos $P(A)$) nos referimos justamente a ese valor límite de la frecuencia relativa cuando el experimento se repite un gran número de veces. En este caso $P(A)=0.2$, $P(B)=0.48$ y $P(C)=0.64$. Gracias a esta abstracción podemos hablar de la frecuencia de resultados aunque el experimento se realice una sola vez.

---

## Axiomas de Kolmogorov

La probabilidad es una función que toma un suceso (subconjunto de $S$) y devuelve un número entre 0 y 1, es decir $P:\mathcal{P}(S)\to[0,1]$. Para que esta función sea coherente con la idea de frecuencia, le exigimos tres reglas básicas llamadas **axiomas**, que serán la base de todo lo que sigue:

$$\boxed{\;1)\;\; P(A)\ge 0 \qquad 2)\;\; P(S)=1 \qquad 3)\;\; A\cap B=\varnothing \Rightarrow P(A\cup B)=P(A)+P(B)\;}$$

Cada axioma tiene una justificación intuitiva desde la frecuencia: el primero, porque las frecuencias relativas son siempre $\ge 0$ (y también su límite); el segundo, porque $S$ contiene todos los resultados posibles, así que en cada repetición ocurre alguno y $f_S=\frac{n_S}{n}=1$ siempre; el tercero, porque si los eventos son mutuamente excluyentes, las ocurrencias de la unión son la suma de las ocurrencias de cada uno:

$$f_{A\cup B}=\frac{n_{A\cup B}}{n}=\frac{n_A+n_B}{n}=\frac{n_A}{n}+\frac{n_B}{n}\;\xrightarrow{n\to\infty}\;P(A)+P(B)$$

---

## Propiedades derivadas

Lo notable es que con solo estos tres axiomas se demuestran muchas propiedades útiles. Todas se prueban escribiendo un evento como unión de partes mutuamente excluyentes y aplicando el tercer axioma.

**Vacío:** $P(\varnothing)=0$. Como $S$ y $\varnothing$ son excluyentes y $S\cup\varnothing=S$, resulta $P(S)+P(\varnothing)=P(S)$, de donde $P(\varnothing)=0$.

**Complemento:** $A$ y $\overline{A}$ son excluyentes y $A\cup\overline{A}=S$, por lo tanto:

$$\boxed{P(\overline{A})=1-P(A)}$$

**Monotonía:** si $B\subseteq A$, escribiendo $A=B\cup(A\setminus B)$ con partes excluyentes:

$$B\subseteq A \;\Rightarrow\; P(B)\le P(A)$$

**Resta inclusiva:** si $B\subseteq A$, entonces $P(A\setminus B)=P(A)-P(B)$.

**Resta no inclusiva:** en general, $P(A\setminus B)=P(A)-P(A\cap B)$.

**Unión inclusiva (principio de inclusión-exclusión):** escribiendo $A\cup B=A\cup(B\setminus A)$:

$$\boxed{P(A\cup B)=P(A)+P(B)-P(A\cap B)}$$

### Ejemplos con los sucesos del mazo

Partiendo de $P(A)=0.2$, $P(B)=0.48$, $P(C)=0.64$ (y de $P(A\cap C)=0.08$, $P(B\cap C)=0.32$, $P(A\cap B)=0$ obtenidos por repetición), aplicamos las propiedades:

| Cálculo | Resultado |
|:--|:-:|
| $P(\overline{A})=1-0.2$ | $0.8$ |
| $P(\overline{B})=1-0.48$ | $0.52$ |
| $P(\overline{C})=1-0.64$ | $0.36$ |
| $P(A\setminus C)=0.2-0.08$ | $0.12$ |
| $P(C\setminus A)=0.64-0.08$ | $0.56$ |
| $P(B\setminus C)=0.48-0.32$ | $0.16$ |
| $P(A\cup C)=0.2+0.64-0.08$ | $0.76$ |
| $P(B\cup C)=0.48+0.64-0.32$ | $0.80$ |

---

## Cálculo de probabilidades sin repetición

Hasta acá calculamos probabilidades simulando infinitas repeticiones y deduciendo otras con las propiedades. Pero las propiedades solo sirven cuando ya hay probabilidades calculadas; todavía no vimos cómo calcular una probabilidad **sin** recurrir a la repetición. La herramienta para eso es el **conteo**.

### Conteo y la regla del producto

En el experimento de cartas con reposición hay 5 opciones para la primera extracción y, para cada una, 5 opciones para la segunda. La multiplicación no es más que sumar varias veces lo mismo:

$$\underbrace{5+5+5+5+5}_{5\text{ veces}}=5\cdot 5 = 5^2 = 25$$

Por eso $\#S=25$. Esta forma de pensar (estructuras que se repiten, suma transformada en multiplicación) se generaliza a experimentos enormes que no podríamos contar a mano.

### Espacios equiprobables y Regla de Laplace

Como las selecciones son al azar, ninguna combinación tiene más chance que otra: cada uno de los 25 resultados tiene la misma probabilidad $p$. Como son mutuamente excluyentes y sus probabilidades suman 1:

$$\underbrace{p+p+\cdots+p}_{25\text{ veces}}=25\cdot p = 1 \;\Rightarrow\; p=\frac{1}{25}=\frac{1}{\#S}$$

Cuando todos los resultados son igual de probables decimos que el espacio es **equiprobable**, y la probabilidad de un evento se calcula con la **Regla de Laplace**:

$$\boxed{P(A)=\frac{\#A}{\#S}=\frac{\text{casos favorables}}{\text{casos totales}}}$$

En el ejemplo, las probabilidades por Laplace coinciden exactamente con las obtenidas por repetición: $P(A)=\tfrac{5}{25}=0.2$, $P(B)=\tfrac{12}{25}=0.48$, $P(C)=\tfrac{16}{25}=0.64$, $P(A\cup B)=\tfrac{17}{25}=0.68$, $P(A\cup C)=\tfrac{19}{25}=0.76$, $P(B\cup C)=\tfrac{20}{25}=0.8$.

> [!warning] La regla de Laplace no siempre vale
> La Regla de Laplace **solo** se aplica cuando el espacio es equiprobable, y eso depende de qué resultados se registren. Por ejemplo, si solo nos interesa ganar un juego que se gana al sacar dos cartas iguales, el espacio es $S=\{\text{Gana},\text{Pierde}\}$, pero **no** son igual de probables: $P(\text{Gana})=0.2$ y $P(\text{Pierde})=0.8$.

---

## Variantes del experimento: reposición y orden

### Sin reposición, con orden

Si la primera carta no se repone, la segunda extracción tiene una opción menos: $\#S = 5\cdot 4 = 20$. Recalculamos los sucesos:

- $A$ (números iguales): imposible sin reposición, $P(A)=\tfrac{0}{20}=0$.
- $B$ (suma impar): para que la suma sea impar, uno debe ser par y el otro impar. Conviene definir $B_i=$ "la $i$-ésima extracción es impar" y escribir $B=(B_1\cap\overline{B_2})\cup(\overline{B_1}\cap B_2)$, que son excluyentes. Contando, $\#(B_1\cap\overline{B_2})=3\cdot 2=6$ y $\#(\overline{B_1}\cap B_2)=2\cdot 3=6$, de modo que $P(B)=\tfrac{6+6}{20}=\tfrac{3}{5}=0.6$.
- $C$ (máximo $\ge 4$): conviene el complemento. Si el máximo no es $\ge 4$, ambos números están por debajo de 4 (3 o menos): $\#(\overline{C_1}\cap\overline{C_2})=3\cdot 2=6$, así que $P(C)=1-\tfrac{6}{20}=\tfrac{14}{20}=\tfrac{7}{10}=0.7$.

### Sin orden (extracción simultánea)

Si las dos cartas se extraen a la vez, no hay "primera" carta: $(1,2)$ y $(2,1)$ son el mismo resultado $\{1,2\}$. La cantidad de resultados es un número combinatorio:

$$\#S=\binom{5}{2}=\frac{5!}{2!\,3!}=\frac{5\cdot 4}{2}=10$$

Calculando con Laplace se obtienen los **mismos** valores que en el caso con orden: $P(A)=0$, $P(B)=\tfrac{3}{5}$, $P(C)=\tfrac{7}{10}$. Esto ocurre porque tanto el numerador como el denominador se reducen a la mitad y la división se equilibra.

> [!warning] Error común al contar
> Un error frecuente es pensar $P(C)$ como "elijo 1 carta mayor o igual a 4 y la otra puede ser cualquiera de las 4 restantes": $\frac{\binom{2}{1}\binom{4}{1}}{\binom{5}{2}}=\frac{8}{10}=\frac{4}{5}$. Esto está **MAL**: el conjunto $\{4,5\}$ se cuenta **dos veces**. La multiplicación solo vale si se divide el espacio en eventos mutuamente excluyentes; si no, se "cuentan casos de más" y se pueden obtener probabilidades mayores que 1. La forma correcta separa por la cantidad exacta de cartas $\ge 4$: con $C_i=$ "se extraen exactamente $i$ números $\ge 4$", $C=C_1\cup C_2$ son excluyentes y $P(C)=\dfrac{\binom{2}{1}\binom{3}{1}+\binom{2}{2}\binom{3}{0}}{\binom{5}{2}}=\dfrac{7}{10}$.

### Fórmulas generales de conteo

Con un mazo de $n$ cartas y $k$ extracciones:

| Experimento | $\#S$ |
|:--|:-:|
| Con reposición | $n^k$ |
| Sin reposición, con orden | $\dfrac{n!}{(n-k)!}=n(n-1)\cdots(n-k+1)$ |
| Sin reposición, sin orden | $\dbinom{n}{k}=\dfrac{n!}{(n-k)!\,k!}$ |

El caso sin orden divide al caso con orden por las $k!$ permutaciones, que aquí representan el mismo resultado.

---

## Probabilidad condicional

### Restricción de casos

Volvamos a la repetición, ahora con el experimento sin reposición. La pregunta de la **probabilidad condicional** es: si sabemos que ocurre $C$, **¿con qué frecuencia ocurre $B$?** En una simulación de $n=50$ ensayos, $C$ ocurrió 32 veces. Si nos restringimos a esos 32 casos (los "casos totales" ya no son 50), $B$ ocurre en 19 de ellos, así que la frecuencia de $B$ sabiendo $C$ es $\tfrac{19}{32}\approx 0.59$.

La cuenta general es la cantidad de veces que ocurren $B$ y $C$ sobre la cantidad de veces que ocurre $C$, que se reescribe convenientemente:

$$\frac{n_{B\cap C}}{n_C}=\frac{n_{B\cap C}/n}{n_C/n}\;\xrightarrow{n\to\infty}\;\frac{P(B\cap C)}{P(C)}$$

### Definición

> [!info] Definición
> Dado un evento $B$ con $P(B)>0$, la probabilidad de $A$ **condicional** a $B$ es:
> $$\boxed{P(A\mid B)=\frac{P(A\cap B)}{P(B)}}$$

El evento de la derecha ($B$) se llama **evento condicionante**. Es clave distinguir la condicional de la intersección: la intersección mide la frecuencia de $A$ y $B$ **en simultáneo** sobre el total; la condicional mide la frecuencia de $A$ **sabiendo** que ocurre $B$, donde los casos totales cambian. De la definición sale una identidad muy usada (la **regla del producto**):

$$\boxed{P(A\cap B)=P(A\mid B)\cdot P(B)=P(B\mid A)\cdot P(A)}$$

### Utilidad: descomponer probabilidades difíciles

La condicional es útil cuando una probabilidad es difícil de calcular directamente porque depende de otro evento. En el experimento sin reposición, calcular $P(B_2)$ (que la segunda extracción sea impar) es complicado porque depende de la primera. En cambio es fácil ver que $P(B_2\mid B_1)=\tfrac{2}{4}$ y $P(B_2\mid\overline{B_1})=\tfrac{3}{4}$. Como $B_1$ y $\overline{B_1}$ son excluyentes:

$$P(B_2)=P(B_2\mid B_1)\,P(B_1)+P(B_2\mid\overline{B_1})\,P(\overline{B_1})=\frac{2}{4}\cdot\frac{3}{5}+\frac{3}{4}\cdot\frac{2}{5}=\frac{3}{5}$$

### Diagrama de árbol

Una herramienta gráfica muy útil es el **diagrama de árbol**. En un primer nivel se ramifica $B_1$ / $\overline{B_1}$, y en un segundo nivel $B_2$ / $\overline{B_2}$. Los "pesos" de cada rama son las probabilidades **condicionales a todo lo que está por encima** en el árbol. Para calcular la probabilidad de un camino se **multiplican** las ramas, y para un evento que abarca varios caminos se **suman**. Así, $P(B_2)=\tfrac{3}{5}\cdot\tfrac{1}{2}+\tfrac{2}{5}\cdot\tfrac{3}{4}=\tfrac{3}{5}$, que es exactamente la misma cuenta de antes.

### La condicional cumple los axiomas

Si fijamos el condicionante $B$, la función $P(\cdot\mid B)$ es a su vez una probabilidad: cumple los tres axiomas de Kolmogorov (es $\ge 0$, vale $P(S\mid B)=1$, y es aditiva para excluyentes) y por lo tanto **todas** las propiedades derivadas: $P(\varnothing\mid B)=0$, $P(\overline{A}\mid B)=1-P(A\mid B)$, monotonía, etc.

> [!warning] El condicionante debe quedar fijo
> Las propiedades de la condicional solo valen mientras el condicionante **no cambie**. Un error muy común es escribir:
> $$\text{MAL:}\qquad P(A\mid \overline{B})=1-P(A\mid B)$$
> Esto no tiene por qué cumplirse, porque al cambiar el condicionante (de $B$ a $\overline{B}$) cambian los casos totales. Lo correcto es $P(\overline{A}\mid B)=1-P(A\mid B)$, manteniendo el mismo $B$.

---

## Independencia

Cambiemos de ejemplo a un **dado** equiprobable, $S=\{1,2,3,4,5,6\}$, con los eventos:

- $D=$ el resultado es mayor que 4 $=\{5,6\}$, $P(D)=\tfrac{1}{3}$.
- $E=$ el resultado es 2 $=\{2\}$, $P(E)=\tfrac{1}{6}$.
- $F=$ el resultado es par $=\{2,4,6\}$, $P(F)=\tfrac{1}{2}$.

Al calcular las condicionales se observa que casi todas cambian respecto de las marginales: $P(D\mid E)=0$, $P(E\mid F)=\tfrac{1}{3}$, etc. Pero hay una excepción notable:

$$P(D\mid F)=\frac{1}{3}=P(D) \qquad P(F\mid D)=\frac{1}{2}=P(F)$$

Es decir, **saber que ocurrió $D$ no afecta la probabilidad de $F$ y viceversa**. Esto motiva la definición.

> [!info] Definición
> Dos eventos $A$ y $B$ son **independientes** si y solo si:
> $$\boxed{P(A\cap B)=P(A)\cdot P(B)}$$

Esto es equivalente a que las condicionales no se vean afectadas: $P(A\mid B)=\dfrac{P(A)P(B)}{P(B)}=P(A)$. En el dado, $D$ y $F$ son independientes porque $P(D\cap F)=P(\{6\})=\tfrac{1}{6}=\tfrac{1}{3}\cdot\tfrac{1}{2}=P(D)P(F)$.

**Propiedades:** si $A$ y $B$ son independientes, también lo son los pares $\overline{A}$ y $B$; $A$ y $\overline{B}$; $\overline{A}$ y $\overline{B}$. Además, **dos eventos de probabilidad positiva no pueden ser a la vez mutuamente excluyentes e independientes**, porque la exclusión da $P(A\cap B)=0$ mientras la independencia exigiría $P(A)P(B)>0$.

> [!warning] Independiente no significa "no afecta"
> Se suele creer (erróneamente) que independencia significa que un evento "no afecta" al otro. En el dado, al saber que ocurre $D=\{5,6\}$, la única opción par es $\{6\}$: cambia el **resultado** posible, pero la **proporción** en que ocurre $F$ sigue siendo $\tfrac{1}{2}$. La independencia dice que cambian los resultados, pero **no** las probabilidades.

### Aplicación: cartas con moneda

Complejicemos el experimento de cartas. Se lanza una moneda: si sale cara ($M$) se hacen 2 extracciones con reposición, y si sale ceca ($\overline{M}$) se hacen 3. Se gana ($G$) si se extrae a lo sumo 1 carta par. Definimos $B_i=$ "la $i$-ésima extracción es impar". Como las extracciones son con reposición, los $B_i$ son **independientes entre sí**; y como la moneda solo decide cuántas extracciones hay (no la composición del mazo), $M$ es independiente de los $B_i$. No podemos asumir independencia de $G$.

Por probabilidad total sobre la moneda, con $P(M)=P(\overline{M})=\tfrac{1}{2}$:

$$P(G)=P(G\mid M)\,P(M)+P(G\mid \overline{M})\,P(\overline{M})$$

Con $P(B_i)=\tfrac{3}{5}$ (3 impares de 5), usando independencia:

$$P(G\mid M)=P(B_1\cap B_2)+P(B_1\cap\overline{B_2})+P(\overline{B_1}\cap B_2)=\frac{3}{5}\cdot\frac{3}{5}+\frac{3}{5}\cdot\frac{2}{5}+\frac{2}{5}\cdot\frac{3}{5}=\frac{21}{25}$$

$$P(G\mid \overline{M})=\left(\tfrac{3}{5}\right)^3+\binom{3}{1}\left(\tfrac{3}{5}\right)^2\tfrac{2}{5}=\frac{81}{125}$$

$$\boxed{P(G)=\frac{21}{25}\cdot\frac{1}{2}+\frac{81}{125}\cdot\frac{1}{2}=\frac{93}{125}=0.744}$$

---

## Particiones y Teorema de Probabilidad Total

Consideremos un mazo de 10 cartas (5 impares, 5 pares) del que se hacen 4 extracciones **sin reposición**. Cada extracción afecta a las siguientes. Definimos $B_i=$ "la $i$-ésima extracción es impar" y $H_j=$ "se extraen exactamente $j$ números impares en las 4 extracciones". Para calcular $P(H_2)$, que es difícil directamente, **partimos** el espacio en partes mutuamente excluyentes según lo que ocurre en cada extracción, calculamos la probabilidad en cada parte y sumamos. Esto se formaliza con dos conceptos.

> [!info] Definición — Partición
> Una colección de eventos $\{A_i\}_{1\le i\le n}$ es una **partición** de $S$ si:
> - **Abarca todo el espacio:** $\bigcup_{i=1}^{n} A_i = S$.
> - **Sus eventos son mutuamente excluyentes:** $A_i\cap A_j=\varnothing$ si $i\ne j$.
>
> Es decir, cada resultado posible pertenece a un único $A_i$. La colección puede ser infinita.

> [!info] Teorema de Probabilidad Total
> Dada $\{A_i\}$ una partición de $S$, para cualquier evento $B$:
> $$\boxed{P(B)=\sum_{i=1}^{n}P(B\cap A_i)=\sum_{i=1}^{n}P(B\mid A_i)\,P(A_i)}$$

La versión con condicionales suele ser más cómoda, porque las condicionales son más fáciles de calcular que las intersecciones. (Nota: en un diagrama de árbol, en cada nivel de división se debe usar una partición; si no, el cálculo inducido por el árbol no es válido.)

### Ejemplo: cálculo de $P(H_2)$

Definamos $I_j^{k}=$ "hasta la $k$-ésima extracción se obtuvieron exactamente $j$ impares", de modo que $H_2=I_2^{4}$. Usando la partición $\{I_0^3; I_1^3; I_2^3; I_3^3\}$, los términos con $I_0^3$ e $I_3^3$ se anulan (no se puede llegar a 2 impares si ya hay 0 o 3), quedando:

$$P(H_2)=P(I_2^4\mid I_1^3)\,P(I_1^3)+P(I_2^4\mid I_2^3)\,P(I_2^3)=\frac{4}{7}\cdot\frac{15}{36}+\frac{4}{7}\cdot\frac{15}{36}=\frac{30}{63}$$

donde $P(I_1^3)=P(I_2^3)=\tfrac{15}{36}$ y, dado 1 (o 2) impares en 3 extracciones, la probabilidad condicional de cerrar en 2 impares es $\tfrac{4}{7}$ (quedan 4 cartas favorables de 7). No es casualidad que los sumandos válidos sean 6: hay $\binom{4}{2}=6$ formas de elegir cuáles 2 de las 4 extracciones son impares.

---

## Teorema de Bayes

A veces tenemos una condicional difícil pero la condicional "en el otro sentido" es fácil. Como $P(A\cap B)$ se puede escribir de dos formas con la regla del producto, podemos invertir el condicionante. Combinando la definición de condicional con el Teorema de Probabilidad Total en el denominador se obtiene:

> [!info] Teorema de Bayes
> Dada $\{A_i\}$ una partición de $S$:
> $$\boxed{P(A_i\mid B)=\frac{P(B\mid A_i)\,P(A_i)}{\displaystyle\sum_{j=1}^{n}P(B\mid A_j)\,P(A_j)}}$$

En el denominador aparece el evento $B$ descompuesto por **toda** la partición (probabilidad total), mientras que en el numerador aparece **solo** el término de la partición que figura en la condicional deseada. Es muy útil cuando la condicional buscada es desconocida pero las condicionales en el otro sentido son conocidas o más fáciles.

### Ejemplo: invertir el condicionante

Supongamos que sabemos que al final hubo exactamente 2 impares en las 4 extracciones ($I_2^4$) y queremos saber qué tan probable es que viniera de haber acumulado 1 impar en las primeras 3 ($I_1^3$). Es difícil pensar $P(I_1^3\mid I_2^4)$ directamente, pero la condicional inversa $P(I_2^4\mid I_1^3)=\tfrac{4}{7}$ es fácil. Como ya tenemos el denominador $P(I_2^4)=\tfrac{30}{63}$, basta usar la definición:

$$P(I_1^3\mid I_2^4)=\frac{P(I_2^4\mid I_1^3)\,P(I_1^3)}{P(I_2^4)}=\frac{\frac{4}{7}\cdot\frac{15}{36}}{\frac{30}{63}}=\frac{1}{2}$$

Cuando el denominador **no** se conoce de antemano, se lo calcula con Probabilidad Total sobre una partición (por ejemplo $\{I_0^2; I_1^2; I_2^2\}$), que es exactamente la estructura completa del Teorema de Bayes.

---

## Resumen

- Un **experimento aleatorio** tiene resultados impredecibles; el conjunto de todos los resultados posibles es el **espacio muestral** $S$, y sus subconjuntos son los **sucesos**, que se combinan con complemento, unión e intersección (Leyes de De Morgan).
- La **probabilidad** $P(A)$ es el límite de la **frecuencia relativa** $f_A=\tfrac{n_A}{n}$ cuando $n\to\infty$.
- Toda la teoría se construye sobre los tres **axiomas de Kolmogorov** ($P(A)\ge 0$, $P(S)=1$, aditividad para excluyentes), de los que se derivan complemento, monotonía e inclusión-exclusión $P(A\cup B)=P(A)+P(B)-P(A\cap B)$.
- En espacios **equiprobables** vale la **Regla de Laplace** $P(A)=\tfrac{\#A}{\#S}$; el conteo se hace con la regla del producto y los números combinatorios ($n^k$, $\tfrac{n!}{(n-k)!}$, $\binom{n}{k}$), cuidando de partir en eventos excluyentes para no contar de más.
- La **probabilidad condicional** $P(A\mid B)=\tfrac{P(A\cap B)}{P(B)}$ restringe los casos totales; de ella sale la **regla del producto** $P(A\cap B)=P(A\mid B)P(B)$ y la herramienta del **diagrama de árbol**.
- Dos eventos son **independientes** si $P(A\cap B)=P(A)P(B)$, lo que equivale a que el condicionante no altera las probabilidades (no a que "no se afecten").
- El **Teorema de Probabilidad Total** descompone $P(B)=\sum_i P(B\mid A_i)P(A_i)$ sobre una **partición**, y el **Teorema de Bayes** invierte el condicionante: $P(A_i\mid B)=\dfrac{P(B\mid A_i)P(A_i)}{\sum_j P(B\mid A_j)P(A_j)}$.
