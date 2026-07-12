# Clase 02 - UCD (Diseño Centrado en el Usuario)

## Definición

El **Diseño Centrado en el Usuario (User-Centered Design, UCD)** es una **filosofía de diseño** cuyo objetivo es crear productos que resuelvan las necesidades concretas de sus usuarios, logrando la mayor satisfacción y experiencia de uso posible. Se enfoca en **entender a los usuarios, sus tareas y el contexto**.

## Historia

- **Henry Dreyfuss** fue el primero en implementar UCD, en el diseño de los teléfonos de la serie 500 para Bell Telephones (**1955**).
- El **término UCD** fue usado por primera vez por **Donald Norman** en la primera CHI Conference (**1983**).

## Otros enfoques de diseño (no son incompatibles con UCD)

- **Centrado en el diseñador**: el diseñador, desde su visión personal, sabe qué es lo mejor.
- **Centrado en la empresa**: se diseña atendiendo a la estructura y necesidades de la empresa.
- **Centrado en el contenido**: la información es la base para organizar la aplicación y su navegación.
- **Centrado en la tecnología**: todo gira en torno a la tecnología elegida.

## Beneficios de UCD

- Incluir al usuario genera productos que satisfacen sus expectativas y necesidades.
- Reduce la posibilidad de situaciones de error.
- El contacto con los usuarios genera **empatía**.
- No solo es cumplir objetivos: también sirve para **analizar el valor del producto** y su capacidad de resolver necesidades reales (utilidad estratégica).

**El error más común en UCD**: no involucrar al usuario a tiempo.

## Metodología UCD según ISO 13407 (proceso iterativo)

Ciclo: **Planificación → Especificar el contexto de uso → Especificar requisitos → Producir soluciones de diseño → Evaluación → (repetir)** hasta que el sistema satisfaga los requisitos.

### 1. Especificar el contexto de uso
- **Objetivo**: identificar a las personas destino, para qué usarán el producto y en qué condiciones.
- **Consideraciones**: descubrir el modelo mental de los usuarios finales, analizar sus destrezas, empezar a pensar alternativas mejores.
- **Métodos y técnicas**: observación, eye tracking, entrevistas, encuestas y analítica web.

Técnicas:

- **Observación**: observar cómo un grupo lleva a cabo tareas, detectando dónde se equivoca o se detiene **y por qué**.
- **Eye tracking**: conjunto de tecnologías (hardware y software) que monitorean cómo una persona mira una escena: en qué áreas fija la atención, cuánto tiempo y en qué orden. Se analiza con representaciones gráficas (heatmaps).
- **Entrevistas**: herramienta **cualitativa** para descubrir deseos, motivaciones, valores y experiencias. Variante: **focus group** (grupos focales), donde un moderador entrevista a un grupo y la interacción entre participantes ofrece información adicional.
- **Encuestas**: herramienta **cuantitativa** con preguntas respondidas por una proporción estadísticamente representativa.
- **Analítica web**: medición, recolección, análisis y documentación de datos de Internet. No se basa en muestras sino en la **monitorización del total** de usuarios → fiable y económica, sin sesgo ni necesidad de reclutar participantes.

### 2. Especificar requisitos
- **Objetivo**: identificar y detallar los objetivos de los usuarios.
- **Consideraciones**: satisfacer claramente los objetivos y el alcance definido.
- **Métodos y técnicas**: **modelos de Personas**.

**Modelos de Personas**: una "Persona" representa a un grupo o subconjunto de usuarios con similitudes en su comportamiento, metas, motivaciones, necesidades, etc. Permiten consolidar un entendimiento de los usuarios y recordar/aplicar lo que sabemos de ellos durante el diseño.

### 3. Producir soluciones de diseño
- **Objetivo**: construir soluciones que cumplan con los requisitos.
- **Consideraciones**: contemplar diferentes alternativas y combinarlas para una solución superadora.
- **Métodos y técnicas**: **prototipos** y **card sorting**.

- **Prototipos**: versión temprana de un producto para presentar a usuarios y/o hacer pruebas. Aunque no funcione completamente, brinda una representación visual del producto final.
- **Card sorting** ("agrupación de tarjetas"): se pide a participantes agrupar conceptos (tarjetas) por su **similitud semántica**. Identifica qué conceptos tienen relación entre sí y el grado de esa relación. Se usa por ejemplo para armar menúes de muchas opciones.

### 4. Evaluación
- **Objetivo**: comprobar si las soluciones cumplen con el contexto de uso y satisfacen las necesidades del usuario.
- **Consideraciones**: listar aspectos positivos y negativos del prototipo respecto de los requisitos; decidir si sigue otra iteración.
- **Métodos y técnicas**: **evaluación de usabilidad**.

**Es un proceso iterativo**: se repite hasta que la evaluación confirme que el sistema satisface los requisitos especificados.

## Preguntas típicas V/F

- El término UCD fue acuñado por Henry Dreyfuss → **Falso** (Dreyfuss lo implementó primero; el término lo usó Donald Norman en 1983).
- La metodología UCD (ISO 13407) es un proceso lineal de una sola pasada → **Falso** (es iterativo).
- Las encuestas son una técnica cualitativa → **Falso** (son cuantitativas; las entrevistas son cualitativas).
- El card sorting sirve para armar menúes agrupando conceptos por similitud semántica → **Verdadero**.
- La analítica web se basa en muestras representativas → **Falso** (monitoriza el total de usuarios).

---

## Técnicas para especificar contexto de uso y requisitos (parte 2)

### Usuarios representativos
- Primer paso: decidir quiénes son los **potenciales usuarios**.
- Casi todos los sistemas los usan distintos tipos de usuarios con características particulares.
- Características a considerar: género, edad, ocupación, nacionalidad, residencia, nivel de educación, nivel socioeconómico, confort con la tecnología, etc.
- A veces se infieren de sistemas existentes; con tecnología nueva hay que analizar quiénes la usarán.

### Observación participativa
- Consiste en "ponerse en los zapatos" de los usuarios para descubrir sus valores, objetivos y necesidades.
- Inspirada en prácticas antropológicas (desarrolladas en 1914 por **Bronislaw Malinowski** en Papúa Nueva Guinea).
- Ayuda a ir más allá de lo superficial y a desarrollar **empatía**.

Aspectos clave: ¿Qué hacen las personas? ¿Qué valores y metas tienen? (no construir lo que piden, sino soluciones vinculadas a su vida cotidiana). ¿Cómo se integran las actividades particulares en una mayor? ¿Cuáles son las similitudes/diferencias? (resumirlas en Modelos de Persona).

Recomendaciones: establecer relación con los observados; aprender todos los pasos del proceso (incluyendo improvisaciones); prestar especial atención a los **errores** (mina de oro); validar lo observado; **diferenciar lo que dicen de lo que hacen** (caso encuesta Walmart).

### Entrevista — qué NO preguntar
- **Preguntas guiadas**: "¿Es importante para usted el flash de la cámara?" → casi todos dicen "sí".
- Preguntas de diseño: "¿Qué funcionalidad te gustaría tener?" → los usuarios son expertos en su vida, no en diseño de apps. Mejor preguntar sobre sus vidas y metas e **inferir** necesidades.
- Escenarios hipotéticos (difíciles de saber), frecuencia de acciones (nos mentimos → hacer preguntas concretas), escalas absolutas 1-10 (¿qué significa 7?), preguntas binarias (sí/no).

Recomendaciones: considerar distintos tipos de usuarios; una aproximación es mejor que nada; hacer **preguntas abiertas** (sobre todo al inicio); dar tiempo/silencio para responder.

### Encuesta — recomendaciones
- **Recorridos cognitivos (cognitive walkthroughs)**: validar que la redacción sea clara y alineada con el modelo mental (pedir a la audiencia que resuma cada pregunta con sus palabras).
- **Pruebas de funcionamiento (mechanical test)**: validar el comportamiento en distintos flujos, dispositivos y navegadores.
- **Pruebas de usabilidad (usability test)**: validar cómo la audiencia interactúa con la encuesta.
- Siempre hacer un **piloto reducido** antes del envío masivo.

### Otras técnicas (comportamiento a largo plazo o esporádico)
- **Diario de estudio**: los participantes registran datos (papel, diario, fotos, video, audio). Debe tener estructura y ser simple. Requiere entrenamiento y seguimiento/recordatorios.
- **Muestreo de experiencia (pager studies)**: se contacta a las personas cada intervalo regular para obtener información en ese momento. Ventaja: no necesitan recordar registrar (fuente externa que se los recuerda). Debe estar estructurado y en formato digital.
- **Usuarios líderes**: los usuarios idean soluciones inteligentes a sus problemas; el diseñador los ayuda a aplicarlas eficientemente. Funciona mejor cuando el diseñador no entiende la necesidad o el contexto cambia muy rápido.

### Modelo de Persona — contenido
- **Nombre** (real, de fantasía o rol).
- **Atributos** que afecten (o no) su interacción con el sistema.
- **Dibujo o fotografía** representativa.
- **Descripción**: debe contar su historia (cobrar vida).
- **Motivaciones**: por qué usaría el sistema (creencias, intenciones).
- **Escenarios**: situaciones concretas de uso.
- **Características deseadas**: qué funcionalidades le gustaría.
- **Comportamientos esperados**: cómo se comportará, qué funcionalidad usará más.
