# Estadística Descriptiva

> [!abstract] ¿De qué se trata?
> La estadística busca sacar conclusiones sobre un fenómeno a partir de datos. La parte **descriptiva** sólo busca **describir** características del conjunto de datos, sin generalizar ni inferir. La idea es resumir muchos datos en pocos números (**medidas de resumen**) y en gráficos.

## Tipos de variable

- **Cuantitativa continua:** toma valores numéricos en un rango continuo (ej.: tiempo de viaje en minutos).
- **Cuantitativa discreta:** toma valores numéricos aislados (ej.: cantidad de veces que llega tarde por semana).

La distinción importa porque cambia la herramienta gráfica: para discretas se usa un **gráfico de frecuencias**; para continuas, un **histograma** (frecuencia por intervalos).

---

## Parámetros de forma

Los parámetros de forma resumen los datos con un solo número. Se agrupan en **tendencia central** (dónde se centran), **dispersión** (cuánto se alejan del centro), **simetría** y **peso de colas**.

### Media

$$\boxed{\bar{x} = \frac{\sum_{i=1}^{n} x_i}{n}}$$

> [!info] ¿Cuándo y por qué?
> Es la medida de **tendencia central** más común: indica dónde se "equilibran" los datos sobre una recta. Cuanto más lejos está un dato de la media, más influye en el cálculo, por lo que la media es **sensible a valores atípicos** (outliers). Si hay pocos datos muy extremos, conviene mirar también la mediana.

### Desvío estándar

$$\boxed{s = \sqrt{\frac{\sum_{i=1}^{n} (x_i - \bar{x})^2}{n-1}}}$$

> [!info] ¿Cuándo y por qué?
> Es la medida de **dispersión** más usada: mide cuánto se alejan los datos de la media. Sirve sobre todo para **comparar** dos conjuntos: si tienen medias similares, el que tenga mayor $s$ está más disperso.

Detalles de la fórmula:

- Se suman **desviaciones al cuadrado**: el cuadrado hace que los datos por debajo y por encima de la media aporten igual (positivo), y penaliza más a los datos lejanos.
- Se divide por $n-1$ (no $n$): el motivo se ve en la Guía 8. Con $n$ grande, dividir por $n$ o $n-1$ es casi lo mismo.
- La **raíz** devuelve la unidad original (si $x$ está en minutos, $s^2$ está en minutos$^2$ y $s$ vuelve a minutos), facilitando la interpretación.

### Simetría (asimetría / skewness)

$$\boxed{\gamma = \frac{\sum_{i=1}^{n} (x_i - \bar{x})^3}{n \cdot s^3}}$$

Valor **adimensional** que se interpreta directamente:

| Valor de $\gamma$ | Interpretación |
|:-:|:--|
| $\gamma \approx 0$ | Distribución **simétrica** respecto de la media |
| $\gamma > 0$ | Asimetría **a derecha** (cola/valores atípicos por encima de la media) |
| $\gamma < 0$ | Asimetría **a izquierda** (cola/valores atípicos por debajo de la media) |

> [!info] ¿Cuándo y por qué?
> Distingue conjuntos con **misma media y mismo desvío** pero con tendencia a valores altos vs. bajos. Se usa el **cubo** para diferenciar datos por debajo y por encima de la media (mantiene el signo), y se divide por $s^3$ para que quede adimensional.

### Kurtosis

$$\boxed{\kappa = \frac{\sum_{i=1}^{n} (x_i - \bar{x})^4}{n \cdot s^4} - 3}$$

Mide el **peso de las colas** (cuánto pesan los datos alejados de la media), tomando como referencia la normal (por eso el $-3$):

| Valor de $\kappa$ | Interpretación |
|:-:|:--|
| $\kappa \approx 0$ | Colas similares a las de una **normal** |
| $\kappa > 0$ | Colas **pesadas** (más valores extremos que una normal) |
| $\kappa < 0$ | Colas **livianas** (menos valores extremos que una normal) |

> [!info] ¿Cuándo y por qué?
> Distingue conjuntos con misma media, desvío **y** simetría, pero distinto comportamiento en los extremos. Usa la potencia **cuarta** (no distingue signo, sólo distancia) y se divide por $s^4$ para quedar adimensional.

---

## Percentilos

Las medidas de posición **no se basan en sumas**, sino en **cantidad de datos acumulados** tras ordenar los datos. Son más **robustas a outliers** que la media y el desvío.

### Mediana

Valor que divide a los datos ordenados en dos mitades (50% a cada lado).

- **Cantidad impar de datos:** es el valor de la **posición central** de los datos ordenados. Con $n=61$, es el dato en posición $31$ (deja 30 a cada lado).
- **Cantidad par de datos:** ninguna observación divide exactamente; se toma el **promedio de los dos valores centrales**. Con $n=60$, es el promedio de las posiciones 30 y 31.

> [!info] ¿Cuándo y por qué?
> Es una medida de **tendencia central robusta**: a diferencia de la media, no la afectan los valores extremos. Útil cuando hay outliers o fuerte asimetría. Existen varias metodologías de cálculo (interpolaciones) que difieren sólo cuando hay "disputa" (caso par); todas coinciden cuando los valores en disputa coinciden.

### Cuartiles

Dividen a los datos en cuatro partes iguales (25% cada una):

- $q_1$ (**primer cuartil**): deja al menos el 25% a su izquierda y 75% a su derecha.
- $q_2$ = **mediana** (50% / 50%).
- $q_3$ (**tercer cuartil**): deja al menos el 75% a su izquierda y 25% a su derecha.

Se calculan igual que la mediana pero acumulando el 25% o el 75% de los datos (promediando posiciones cuando no cae justo).

### Rango intercuartil (IQR)

$$\boxed{IQR = q_3 - q_1}$$

> [!info] ¿Cuándo y por qué?
> Es una **medida de dispersión robusta**: contiene el 50% central de los datos. Cuanto más comprimido, menos dispersión. Se usa además para detectar outliers (regla de Tukey, ver Boxplots).

### Percentilos generales

Generalizan la idea: el **percentilo $p$** es el valor que acumula el $p\%$ de los datos. Casos particulares: quintiles (cada 20%), deciles (cada 10%), cuartiles (cada 25%).

Cuando la cantidad a acumular no es entera, se **interpola** entre datos consecutivos. Por ejemplo, para el percentilo 97 de 60 datos ($0.97 \cdot 60 = 58.2$):

$$P_{97} = \text{Dato}_{58} + 0.2 \cdot (\text{Dato}_{59} - \text{Dato}_{58})$$

---

## Boxplots (diagrama de caja)

Gráfico que resume la distribución usando los cuartiles, en vez de graficar todas las observaciones. Su construcción:

- **Línea central de la caja** = mediana.
- **Límites de la caja** = $q_1$ (abajo) y $q_3$ (arriba) → la caja es el **50% central** de los datos.
- **Bigotes** = se extienden hasta el mínimo y máximo observados **dentro** de los límites de Tukey.
- **Outliers** = puntos que caen fuera de los límites de Tukey.

> [!warning] Regla de Tukey para outliers
> $$LW = q_1 - 1.5 \cdot IQR \qquad UW = q_3 + 1.5 \cdot IQR$$
> Los datos por debajo de $LW$ o por encima de $UW$ se consideran **atípicos (outliers)**. Los bigotes llegan sólo hasta donde **hay observaciones** (no hasta el umbral de Tukey si no hay datos ahí).

> [!info] ¿Cuándo y por qué?
> El boxplot es una versión **resumida** del gráfico Valor vs. Constante. Su gran ventaja es **comparar** varios grupos: se disponen los boxplots en paralelo en el mismo gráfico y se ven de un vistazo diferencias de centro, dispersión, asimetría y outliers.

---

## Histogramas

### Variable discreta: gráfico de frecuencias

Se "apilan" los datos según su valor, así los valores más frecuentes aparecen con **mayor altura**. Permite ver de un vistazo qué valores se repiten más.

### Variable continua: frecuencia por intervalos

En una variable continua cada valor exacto aparece a lo sumo una vez, así que no tiene sentido contar valores puntuales. En su lugar se divide el recorrido en **intervalos** y se cuenta cuántos datos caen en cada uno. El **histograma** grafica esos conteos: los rangos más frecuentes tienen mayor altura.

> [!warning] Elegir la cantidad de intervalos
> No hay una cantidad óptima universal; se elige **mirando el gráfico**.
> - **Muy pocos intervalos:** todo se agolpa en el centro y se pierde información de qué rangos son más o menos frecuentes.
> - **Demasiados intervalos:** aparecen muchos intervalos con 0 datos que no son realmente "infrecuentes" (un valor sin datos rodeado de intervalos poblados).

Los histogramas también permiten ver **asimetrías** (cola hacia un lado) y el **peso de las colas** (livianas vs. pesadas), igual que $\gamma$ y $\kappa$.

---

## Medidas de resumen con datos agrupados

A veces los datos no vienen individualizados, sino en **rangos** (entre un límite inferior $L_i$ y superior $L_s$) con la **frecuencia** $f_i$ = cantidad de datos en cada intervalo. Al agrupar **se pierde información**, por lo que las medidas darán **similares** pero no idénticas a las de datos sin agrupar.

### Marca de clase

Como en un rango no hay un valor concreto para sumar, se usa un **representante** de cada intervalo, la **marca de clase** (punto medio):

$$x_i = \frac{L_{i} + L_{s}}{2}$$

### Media, desvío, simetría y kurtosis agrupadas

La única diferencia con las fórmulas sin agrupar es que se **incorpora la frecuencia** $f_i$ en las sumas (para que los intervalos más poblados influyan más). Siendo $L$ la cantidad de intervalos:

| Medida | Sin agrupar | Agrupado |
|:--|:--|:--|
| Media | $\bar{x} = \dfrac{\sum x_i}{n}$ | $\bar{x}_{Ag} = \dfrac{\sum_{i=1}^{L} x_i \, f_i}{n}$ |
| Desvío | $s = \sqrt{\dfrac{\sum (x_i-\bar{x})^2}{n-1}}$ | $s_{Ag} = \sqrt{\dfrac{\sum_{i=1}^{L} (x_i-\bar{x}_{Ag})^2 \, f_i}{n-1}}$ |
| Simetría | $\gamma = \dfrac{\sum (x_i-\bar{x})^3}{n \, s^3}$ | $\gamma_{Ag} = \dfrac{\sum_{i=1}^{L} (x_i-\bar{x}_{Ag})^3 \, f_i}{n \, s_{Ag}^3}$ |
| Kurtosis | $\kappa = \dfrac{\sum (x_i-\bar{x})^4}{n \, s^4} - 3$ | $\kappa_{Ag} = \dfrac{\sum_{i=1}^{L} (x_i-\bar{x}_{Ag})^4 \, f_i}{n \, s_{Ag}^4} - 3$ |

### Frecuencia acumulada

Para percentilos (mediana, cuartiles) la lógica es distinta: no se usan marcas de clase sino la **frecuencia acumulada** $F_i$ = cantidad de datos hasta el límite superior del intervalo $i$. Se lee como "hay $F_i$ datos con valor menor a $L_{s,i}$".

### Percentilo con datos agrupados

Cuando la cantidad de datos a acumular no cae justo en un límite, se asume que los datos del intervalo se **distribuyen equitativamente** dentro de él y se **interpola**:

$$\boxed{P_{k,Ag} = L_{i} + \frac{\frac{k}{100}\cdot n - F_{i-1}}{f_i} \cdot (L_{s} - L_{i})}$$

donde $i$ es el intervalo que contiene al percentilo (el primero cuya $F_i$ alcanza la cantidad buscada), $F_{i-1}$ es la frecuencia acumulada hasta el intervalo anterior, y $f_i$ la frecuencia del intervalo.

> [!example] Ejemplo — Percentilo 15 de 60 datos
> Buscar $P_{15}$ equivale a acumular $0.15 \cdot 60 = 9$ datos. Si hasta $L=35$ se acumularon 8 datos y el intervalo $[35,37]$ tiene $f_i=7$:
> $$P_{15,Ag} = 35 + \frac{9-8}{7}\cdot 2 = 35.29$$

---

## Resumen y guía de decisión

> [!tip] ¿Qué medida usar?
> - **Centro:** media si los datos son razonablemente simétricos y sin outliers; **mediana** si hay asimetría o valores atípicos (es robusta).
> - **Dispersión:** desvío estándar $s$ para comparar (sensible a outliers); **IQR** si querés robustez.
> - **Forma:** simetría $\gamma$ (hacia qué lado se estira) y kurtosis $\kappa$ (peso de colas vs. normal).
> - **Ver la distribución:** boxplot para comparar grupos y detectar outliers; histograma para ver la forma de una variable continua; gráfico de frecuencias para discretas.

| Concepto | Fórmula |
|:--|:--|
| Media | $\bar{x} = \frac{1}{n}\sum x_i$ |
| Desvío estándar | $s = \sqrt{\frac{1}{n-1}\sum (x_i-\bar{x})^2}$ |
| Simetría | $\gamma = \frac{\sum (x_i-\bar{x})^3}{n\,s^3}$ |
| Kurtosis | $\kappa = \frac{\sum (x_i-\bar{x})^4}{n\,s^4} - 3$ |
| IQR | $q_3 - q_1$ |
| Outliers (Tukey) | $q_1 - 1.5\,IQR$ ; $q_3 + 1.5\,IQR$ |
| Media agrupada | $\bar{x}_{Ag} = \frac{1}{n}\sum x_i f_i$ (con $x_i$ = marca de clase) |
| Percentilo agrupado | $L_i + \frac{\frac{k}{100}n - F_{i-1}}{f_i}(L_s - L_i)$ |

- Las medidas basadas en **sumas** (media, $s$, $\gamma$, $\kappa$) usan marcas de clase y frecuencias al agrupar.
- Las medidas de **posición** (mediana, cuartiles, percentilos) usan frecuencias acumuladas e interpolación.
- Al **agrupar** se pierde precisión: los valores dan **parecidos** pero no exactos.
