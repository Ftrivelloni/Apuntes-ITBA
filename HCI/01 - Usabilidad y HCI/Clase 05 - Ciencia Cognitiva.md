# Clase 05 - Ciencia Cognitiva

## ¿Qué es la ciencia cognitiva?

Estudio científico **interdisciplinario** de la mente y sus procesos. Examina la naturaleza, tareas y funciones de la cognición. Facultades de interés: **lenguaje, percepción, memoria, atención, razonamiento y emoción**. Recurre a lingüística, psicología, IA, filosofía, neurociencia y antropología.

> "El pensamiento puede entenderse mejor en términos de **estructuras representacionales en la mente** y **procedimientos computacionales** que operan sobre esas estructuras."

## Carga cognitiva

- Es el **esfuerzo mental** que una persona necesita para realizar una tarea. En una UI, la cantidad de recursos mentales para comprender y operarla.
- El cerebro tiene una cantidad **finita** de recursos ("ancho de banda"); al excederla nos sentimos sobrepasados.

Dos tipos:

- **Intrínseca**: **no puede ser eliminada**. Esfuerzo requerido para absorber la nueva información (ej: comprender los números del saldo bancario una vez visualizados).
- **Externa**: todo lo que se interpone en el camino del objetivo consumiendo recursos (recordar la contraseña, identificar la cuenta, entender la disposición). Es lo que el diseñador debe **minimizar o eliminar**.

Cómo reducir la carga externa:
- **Reducir el abarrotamiento** (quitar imágenes irrelevantes, tipografías muy decoradas).
- **Construir usando modelos mentales existentes** (respetar convenciones; no romperlas).
- **Deshacerse de tareas** (que la UI haga lo innecesario: datos biométricos en vez de contraseñas, mostrar datos previos).
- Lograr un diseño lo más **simple** posible.

## Atención selectiva

- Fenómeno por el cual las personas ignoran ciertos elementos.
- **Ceguera a los anuncios (banner blindness)**: se ignora la publicidad o lo que se le asemeja. Estudio de eyetracking de NN Group (200 personas): el **65%** ignoraba los anuncios.

Consideraciones que llevan a ignorar elementos:
- **Tamaño y forma**: una foto se identifica con visión periférica; si no interesa, se ignora.
- **Posición**: los usuarios aprenden dónde aparece cada patrón. Esperan el **logo arriba a la izquierda** (ancla para confirmar el sitio); el estudio mostró que el 50% no visualizó esa zona.
- **Carruseles**: los usuarios saben que a veces contienen publicidad y los desplazan fuera de vista. Evitar que el contenido valioso se parezca a publicidad; si no, hacerlo accesible por navegación/buscador/atajos.

**Visión de túnel**: pérdida de la visión periférica; ejemplo de atención selectiva. Los usuarios permanecen concentrados en la sección con la que interactúan. La atención selectiva es un **instinto de supervivencia** (si atendiéramos a todo, no haríamos nada).

## Peso visual (visual weight)

Representa la **importancia percibida** de un elemento en una composición; mide la atracción que genera. A mayor peso visual, más llama la atención. Factores:

- **Tamaño**: elementos grandes atraen más (se perciben más cercanos).
- **Forma**: formas simples y regulares se perciben más pesadas (las complejas parecen incompletas).
- **Color**: saturación y brillo afectan.
- **Contraste**: mayor contraste con el entorno → más atención.

## Memoria

### Corto plazo y el número mágico 7
- Capacidad de la memoria a corto plazo: **7 ± 2 ítems** (George Miller, fines de los 50).
- Lo interesante no fue el número sino que los ítems eran distintos (letras, números, palabras).
- La capacidad no se mide en **bits** sino en unidades de significado llamadas **chunks** (tan grandes como se desee). Agrupar en chunks relevantes (**chunking**) incrementa la capacidad. Proceso fundamental para memorizar.

**Uso INCORRECTO del número 7**: NO aplica a la cantidad de opciones de un menú, ítems de una lista o escalas de valuación, porque la memoria a corto plazo **no es relevante** para esas tareas (no hay que recordar las opciones del menú).

### Memoria de trabajo
- Es un **buffer** donde la mente almacena información relevante para la tarea actual. Capacidad **extremadamente limitada** (varía por persona).
- Si se excede, alguna info no se recuerda → más esfuerzo, más tiempo, más errores.
- Relacionada con la **carga cognitiva**: alta carga = uso intensivo de la memoria de trabajo. Los diseñadores deben evitar sobrecargarla.

**Memoria externa**: herramienta o característica de la UI que permite al usuario resguardar y acceder a información durante la tarea (como usar lápiz y papel para una suma). Descarga la carga cognitiva y permite realizar la tarea más rápido.

## Percepción visual — Teoría de Gestalt

La mente está programada para ver **objetos y formas completas** en lugar de líneas, espacios y bordes desconectados. "Gestalt" = forma/figura; la idea es un **conjunto unificado**: se pone el foco en la **suma de las partes** más que en los elementos individuales. Nace a comienzos de 1900 (psicólogos alemanes y austríacos).

### Principios de Gestalt

- **Similitud**: ítems que comparten una característica visual (color, forma, tamaño, tipografía, orientación, movimiento) se perciben más relacionados. El **color** tiende a ser más potente que la forma. En UI: un mismo color comunica funcionalidad común (hipervínculos).
- **Proximidad**: ítems cercanos se perciben relacionados; separados, en grupos distintos. Puede **anular** color y forma. Clave del espacio en blanco (negativo) para agrupar.
- **Cierre**: las personas completan los espacios para percibir un objeto completo. Usado en carruseles (muestran parcialmente ítems que no caben). Se aplica con espacio positivo, negativo o contraste (Jarrón de Rubin). Debe existir balance → validar con usuarios.
- **Conectividad**: elementos conectados o que comparten un borde se perciben como una misma unidad. Puede anular la proximidad. Usado en secuencias de estados (checkout), bordes contenedores, barras de navegación.
- **Destino común**: objetos sincronizados/coordinados en su movimiento se agrupan como uno (bandada de pájaros, íconos al deslizar escritorios). Clave: misma velocidad, mismo tiempo, misma dirección. Ejemplos UI: dropdowns, menús expandibles, acordeones, parallax/scroll. Se puede usar la **disrupción** (movimiento inesperado) a favor.
- **Continuidad**: el ojo sigue rutas y secuencias visuales; prefiere los caminos más simples. En UI: cuadrículas de formularios, grillas de e-commerce, historias de Instagram (círculo cortado sugiere continuidad).
- **Figura y fondo**: se visualizan objetos como **figura** (primer plano) y **fondo** (segundo plano). Simplifica la escena y reduce carga cognitiva. Se logra con: fondos difuminados, tamaño, contraste de color, aislamiento.

## Percepción motriz — Ley de Fitts

Paul Fitts (**1954**): el **tiempo** para alcanzar un objetivo depende de la **distancia** a este pero es **inversamente proporcional a su tamaño**. Movimientos rápidos y objetivos pequeños → más errores (equilibrio velocidad/precisión).

- Influyó en la convención de hacer **botones grandes** (sobre todo en móviles); la distancia entre el foco de atención y el botón debe ser mínima.
- Se aplica a movimientos rápidos de apuntado, **no** a movimientos continuos (dibujar).
- **Índice de dificultad**: `ID = log₂(2D/W)` (D = distancia, W = ancho del objetivo).
- **Índice de rendimiento**: `IP = ID/MT` (bits por segundo, MT = tiempo de movimiento).
- Ecuación de regresión: `MT = a + b·ID = a + b·log₂(2D/W)` (a y b constantes empíricas según el dispositivo).

## Razonamiento — Ley de Hick

Ley de Hick (o Hick-Hyman): cuantas **más opciones** se presentan, **más tiempo** tarda la persona en decidir. El tiempo aumenta **logarítmicamente** con el número de opciones (el incremento se vuelve menos significativo a más opciones). Crucial al diseñar listas cortas (menús de navegación, botones de acción). Demasiadas opciones → saturación → mayor tasa de rebote.

## Lenguaje claro y sencillo

- Mito: el lenguaje claro reduce la calidad. Falso: frases largas y palabras vistosas **reducen la legibilidad**.
- Objetivo principal de la comunicación: **transmitir información**.
- Beneficios: menos esfuerzo para descifrar, beneficia a todos (avanzados e internacionales), mejores resultados en motores de búsqueda (vocabulario del usuario).

## Emociones — Don Norman (3 niveles)

- **Visceral**: respuesta inconsciente, instintiva, no relacionada con el razonamiento (oler comida, un ruido fuerte sube el ritmo cardíaco).
- **Conductual**: análisis de una experiencia transformada en acción; tiene que ver con confort, facilidad de uso o consecuencias (caja automática rápida → volver a usarla; perder trabajo → furia).
- **Reflexivo**: el más alto; pensamientos conscientes, interpretación y razonamiento; autoconocimiento y lo que queremos que otros piensen de nosotros (primera clase en avión, correos sin leer y la imagen ante el jefe).

¿Por qué importa? Permite mitigar emociones negativas y mejorar las positivas:
- **Visceral**: el razonamiento no ayuda → evitar los disparadores de emociones negativas.
- **Conductual**: manejar expectativas, adherir a estándares/convenciones, mejorar la usabilidad.
- **Reflexivo**: menos usabilidad y más comunicación (recordar cómo las acciones ayudan a lograr objetivos).

## Preguntas típicas V/F

- La carga cognitiva intrínseca puede eliminarse con buen diseño → **Falso** (la intrínseca no se elimina; se minimiza la externa).
- El número mágico 7 justifica limitar los menús a 7 opciones → **Falso** (es un uso incorrecto; la memoria a corto plazo no es relevante ahí).
- La ley de Fitts dice que el tiempo es inversamente proporcional al tamaño del objetivo → **Verdadero**.
- Según la ley de Hick, el tiempo de decisión crece linealmente con el número de opciones → **Falso** (crece logarítmicamente).
- El principio de proximidad puede anular al de similitud (color/forma) → **Verdadero**.
- El nivel visceral de emociones se puede mejorar con más información contextual → **Falso** (en el visceral el razonamiento no ayuda).
