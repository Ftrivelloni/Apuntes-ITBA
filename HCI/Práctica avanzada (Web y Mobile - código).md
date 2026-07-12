# Práctica avanzada — Web y Mobile (foco en código e implementación)

Preguntas **Verdadero/Falso** de dificultad igual o mayor a las del final, orientadas a **detalles concretos de código, sintaxis e implementación**. Cada ítem trae la respuesta (→), la justificación y la nota de referencia.

> Consejo de estudio: tapá la línea del "→" e intentá responder antes de mirar. Varias son "trampas" de sintaxis.

---

# BLOQUE 2 — Frontend Web

## HTML semántico

**W1) `<div>` y `<article>` son intercambiables porque ambos son contenedores de bloque sin significado semántico.**
→ **FALSO.** `<div>` **no tiene semántica** (agrupador genérico). `<article>` representa contenido **autocontenido y distribuible de forma independiente** (un post, una noticia, una card reutilizable). Un lector de pantalla los trata distinto.
📍 [[Clase 08 - HTML y Desarrollo Web]] · "Otras etiquetas" y "Buenas prácticas / accesibilidad"

**W2) `<section>` se usa para agrupar contenido temático (normalmente con su propio encabezado), mientras que `<div>` se usa cuando solo se necesita un contenedor para aplicar estilos o agrupar sin semántica.**
→ **VERDADERO.** `<section>` = agrupación temática; `<div>` = agrupación sin significado.
📍 [[Clase 08 - HTML y Desarrollo Web]]

**W3) El elemento `<nav>` está pensado para contener los bloques principales de enlaces de navegación del sitio.**
→ **VERDADERO.** Es un elemento semántico de HTML5 (como `<header>`, `<footer>`) que marca la zona de navegación.
📍 [[Clase 08 - HTML y Desarrollo Web]] · "Versiones de HTML (HTML5)"

**W4) `<em>` e `<i>` son idénticos: ambos solo ponen el texto en itálica.**
→ **FALSO.** `<em>` aporta **énfasis semántico** (importa para screen readers); `<i>` es meramente presentacional. HTML busca separar estructura de presentación.
📍 [[Clase 08 - HTML y Desarrollo Web]] · "Textos / información semántica"

**W5) En un `<img>` alcanza con el atributo `src`; el `alt` es opcional y solo afecta a la estética.**
→ **FALSO.** `alt` es fundamental para **accesibilidad** (screen readers) y como texto alternativo si la imagen no carga. Se debe especificar siempre.
📍 [[Clase 08 - HTML y Desarrollo Web]] · "Imágenes"

## CSS

**W6) Dado `#menu` (id), `.item` (clase) y `li` (tipo) apuntando al mismo elemento, gana la regla del selector de `id` por mayor especificidad.**
→ **VERDADERO.** Orden de especificidad: **id > clase > tipo**. Un `#menu` gana sobre `.item` y sobre `li`.
📍 [[Clase 09-10 - CSS]] · "Cascada y herencia / Especificidad"

**W7) El selector `li > a` selecciona cualquier `<a>` que esté anidado dentro de un `<li>`, sin importar cuántos niveles de profundidad.**
→ **FALSO.** `>` selecciona **hijos directos**. Para "en cualquier nivel" se usa el selector descendiente con espacio: `li a`.
📍 [[Clase 09-10 - CSS]] · "Selectores"

**W8) La propiedad `padding` define el espacio entre el borde y el contenido; `margin` define el espacio por fuera del borde, entre cajas.**
→ **VERDADERO.** (Trampa clásica invertida.)
📍 [[Clase 09-10 - CSS]] · "Borde, margen y relleno"

**W9) Por defecto, si a una caja le doy `width: 200px` y luego `padding: 20px` y `border: 5px`, el ancho total ocupado en pantalla sigue siendo 200px.**
→ **FALSO.** Con el box model por defecto, **padding y border se suman** al ancho → ocupa 200 + 20·2 + 5·2 = **250px**. (Por eso existe `box-sizing: border-box`, que hace que `width` incluya padding y borde.)
📍 [[Clase 09-10 - CSS]] · "Cajas (Box model)"

**W10) `position: absolute` posiciona el elemento respecto de su elemento contenedor y lo saca del flujo normal (los demás actúan como si no existiera).**
→ **VERDADERO.** (En la práctica, respecto del ancestro posicionado más cercano.) Se remueve del flujo normal.
📍 [[Clase 09-10 - CSS]] · "Disposición / posicionamiento"

**W11) `display: none` y `visibility: hidden` producen el mismo efecto visual y ocupan el mismo espacio.**
→ **FALSO.** `display: none` **elimina** el elemento (ocupa 0). `visibility: hidden` lo oculta pero **conserva su espacio**.
📍 [[Clase 09-10 - CSS]] · "Tipo y visibilidad"

**W12) Los márgenes verticales de dos cajas adyacentes se suman siempre.**
→ **FALSO.** Los márgenes verticales **colapsan**: se usa el mayor de los dos y el otro se ignora.
📍 [[Clase 09-10 - CSS]] · "Margen"

## Vite / Vuetify

**W13) Vuetify es un framework de **componentes** (`<v-btn>`, `<v-card>`), mientras que Tailwind es un framework de **clases de utilidad** (`p-4`, `bg-yellow-200`).**
→ **VERDADERO.**
📍 [[Clase 10-11 - Vite y Vuetify]] · "Design Systems y Frameworks CSS"

**W14) El servidor de desarrollo de Vite empaqueta toda la app antes de servirla, por eso el arranque en frío es lento.**
→ **FALSO.** Vite sirve el código fuente sobre **ESM nativo** y transforma **a pedido**; por eso el arranque es rápido. Solo preempaqueta las dependencias (con esbuild).
📍 [[Clase 10-11 - Vite y Vuetify]] · "Cómo mejora el arranque"

## Vue.js — reactividad y sintaxis

**W15) `const count = ref(0)` crea una referencia reactiva; dentro de `<script setup>` se lee/escribe como `count.value`, pero en el `<template>` se usa directamente `count` (auto-unwrap).**
→ **VERDADERO.** En el script se accede con `.value`; en el template Vue lo "desenvuelve" automáticamente.
📍 [[Clase 12 - Vue.js]] · "Reactivity Fundamentals (Composition API)"

**W16) El resultado de `ref()` se puede asignar indistintamente a `val` o `const`.**
→ **FALSO.** `val` es de Kotlin, no existe en JavaScript. Se asigna a `const` (o `let`); el objeto ref se mantiene y se muta su `.value`.
📍 [[Clase 12 - Vue.js]]

**W17) `reactive({ ... })` se usa para objetos; si lo desestructuro (`const { a } = miReactive`), las variables extraídas conservan la reactividad.**
→ **FALSO.** Al **desestructurar** un objeto `reactive` se **pierde la reactividad**. (Para conservarla se usan refs o `toRefs`.)
📍 [[Clase 12 - Vue.js]] · "Reactivity Fundamentals"

**W18) Una `computed` se recalcula solo cuando cambian sus dependencias reactivas; si no cambian, devuelve el valor cacheado.**
→ **VERDADERO.** A diferencia de un método, la computed tiene **caché**.
📍 [[Clase 12 - Vue.js]] · "Computed Properties"

**W19) `v-if` y `v-show` son equivalentes: ambos quitan el elemento del DOM cuando la condición es falsa.**
→ **FALSO.** `v-if` **crea/destruye** el elemento en el DOM (renderizado condicional real); `v-show` solo alterna `display` (el elemento permanece en el DOM).
📍 [[Clase 12 - Vue.js]] · "Conditional Rendering"

**W20) Al usar `v-for` se recomienda enlazar una `:key` única para ayudar a Vue a identificar cada nodo de la lista.**
→ **VERDADERO.**
📍 [[Clase 12 - Vue.js]] · "List Rendering"

**W21) `v-model` en un `<input>` implementa un binding bidireccional (lee y escribe la variable enlazada).**
→ **VERDADERO.** Es azúcar sintáctico sobre `:value` + `@input` (o `modelValue` + `update:modelValue` en componentes).
📍 [[Clase 12 - Vue.js]] · "Form Input Bindings"

**W22) En un Single-File Component, la lógica, el template y el estilo van en tres archivos separados.**
→ **FALSO.** Un SFC (`.vue`) los **encapsula en un único archivo** (secciones `<script>`, `<template>`, `<style>`).
📍 [[Clase 12 - Vue.js]] · "Componentes de Único Archivo (SFC)"

## Vue Router

**W23) Para una ruta dinámica `/user/:id`, dentro de un componente con Composition API se accede al valor con `useRoute().params.id`.**
→ **VERDADERO.** `useRoute()` da la ruta actual (params, query); `useRouter()` da el router para navegar.
📍 [[Clase 13-14 - Vue Router]] · "Dynamic Route Matching / Composition API"

**W24) La navegación programática se hace con `router.push(...)`, y se recomienda navegar por **nombre de ruta** en lugar de escribir la URL a mano.**
→ **VERDADERO.**
📍 [[Clase 13-14 - Vue Router]] · "Programmatic Navigation / Named Routes"

**W25) El lazy loading de rutas se implementa pasando el componente como `component: () => import('./Vista.vue')`.**
→ **VERDADERO.** Import dinámico → el componente se carga bajo demanda.
📍 [[Clase 13-14 - Vue Router]] · "Lazy Loading Routes"

**W26) Un navigation guard (ej: `beforeEach`) puede **cancelar** la navegación o **redirigir** a otra ruta.**
→ **VERDADERO.**
📍 [[Clase 13-14 - Vue Router]] · "Navigation Guards"

## Pinia

**W27) Un store de Pinia se define con `defineStore('id', { state, getters, actions })`; el `state` es una **función** que retorna el objeto de estado.**
→ **VERDADERO.** `state: () => ({ count: 0 })`.
📍 [[Clase 15 - Pinia]] · "Defining a Store / State"

**W28) En Pinia, los `getters` son análogos a las `computed` y las `actions` pueden ser asíncronas.**
→ **VERDADERO.**
📍 [[Clase 15 - Pinia]] · "Getters / Actions"

**W29) `provide()` / `inject()` son la solución recomendada para reemplazar por completo a Pinia en el manejo de estado global.**
→ **FALSO.** Sirven para **mitigar el prop drilling** (inyección de dependencias entre ancestro y descendiente), pero **no reemplazan** a Pinia como store global.
📍 [[Clase 15 - Pinia]] · "La solución" · [[Clase 12 - Vue.js]] · "Provide / Inject"

## Ajax / Fetch / JSON

**W30) `fetch('/api')` devuelve una `Promise<Response>`; ante un HTTP 404 la promesa se **rechaza** y cae en el `.catch()`.**
→ **FALSO.** Un 404 **se resuelve** (la promesa solo se rechaza ante fallo de red). Hay que chequear `response.ok` / `response.status`.
📍 [[Clase 16 - Ajax]] · "Usando Fetch"

**W31) Para leer el cuerpo JSON de la respuesta se hace `const data = await response.json()`, porque `.json()` también devuelve una promesa.**
→ **VERDADERO.**
📍 [[Clase 16 - Ajax]] · "Usando Fetch"

**W32) Para un POST con fetch hay que pasar un segundo parámetro `init` con `method: 'POST'`, `headers` y `body: JSON.stringify(obj)`.**
→ **VERDADERO.**
📍 [[Clase 16 - Ajax]] · "Usando Fetch (POST)"

**W33) `JSON.parse()` convierte texto JSON a objeto y `JSON.stringify()` convierte un objeto a texto JSON.**
→ **VERDADERO.**
📍 [[Clase 16 - Ajax]] · "JSON"

**W34) Dos URLs con el mismo host y protocolo pero distinto puerto son consideradas del mismo origen.**
→ **FALSO.** El origen se define por **protocolo + host + puerto**; distinto puerto = distinto origen.
📍 [[Clase 16 - Ajax]] · "Política de mismo origen"

**W35) Con CORS, es el **servidor** el que habilita el acceso cross-origin mediante el encabezado `Access-Control-Allow-Origin`.**
→ **VERDADERO.** El navegador hace un "preflight" y el servidor explicita orígenes permitidos (o `*`).
📍 [[Clase 16 - Ajax]] · "Formas de resolver el problema"

### Respuesta corta / código (Web)

- **¿Cómo se declara una variable reactiva simple y una para objetos en Vue 3?** → `const n = ref(0)` (primitivos, se usa `n.value`) y `const obj = reactive({...})` (objetos).
- **¿Cómo enlazás una clase condicional a un elemento?** → `:class="{ activa: estaActiva }"` (Class Bindings).
- **¿Diferencia entre `computed` y un método en el template?** → `computed` cachea según dependencias; el método se ejecuta en cada render.
- **¿Cómo centrás horizontalmente una caja con ancho fijo en CSS clásico?** → `width` + `margin: 0 auto`.

---

# BLOQUE 3 — Mobile

## Kotlin

**M1) `val` declara una referencia inmutable (no se puede reasignar) y `var` una mutable.**
→ **VERDADERO.** (Inmutable la referencia; el objeto apuntado puede ser mutable.)
📍 [[Clase 18 - Kotlin]] · "Declaración de variables"

**M2) El operador `?.` (safe call) evita el crash: si el receptor es `null`, la expresión devuelve `null` en lugar de lanzar una excepción.**
→ **VERDADERO.** Parte del sistema de null safety que evita los NullPointerException.
📍 [[Clase 18 - Kotlin]] · "Beneficios / código más seguro"

**M3) El operador Elvis `?:` permite dar un valor por defecto cuando la expresión de la izquierda es `null` (ej: `val n = a ?: 0`).**
→ **VERDADERO.**
📍 [[Clase 18 - Kotlin]] · "Código más seguro"

**M4) Una función marcada con `suspend` puede invocarse desde cualquier lugar, incluso fuera de una corrutina.**
→ **FALSO.** Una función `suspend` solo se llama desde **otra suspend** o dentro de una **corrutina** (ej: un scope).
📍 [[Clase 18 - Kotlin]] · "Concurrencia estructurada"

**M5) Una corrutina de Kotlin es simplemente otro nombre para un thread del sistema operativo.**
→ **FALSO.** Una corrutina **no es un thread**; es mucho más liviana y varias corrutinas pueden multiplexarse sobre pocos threads.
📍 [[Clase 18 - Kotlin]] · "Concurrencia estructurada"

**M6) Kotlin es 100% interoperable con Java (se puede llamar código Java desde Kotlin y viceversa).**
→ **VERDADERO.** Permite adopción progresiva.
📍 [[Clase 18 - Kotlin]] · "Beneficios / interoperabilidad"

## Jetpack Compose — estado y sintaxis

**M7) `val texto = remember { mutableStateOf("") }` conserva el valor entre recomposiciones; para conservarlo también ante un cambio de configuración (rotación) hay que usar `rememberSaveable`.**
→ **VERDADERO.**
📍 [[Clase 19 - Jetpack Compose]] · "El estado en funciones de composición / restablecer el estado"

**M8) `mutableStateOf(...)` crea un tipo observable: cualquier cambio a su `value` dispara la recomposición de los composables que lo leen.**
→ **VERDADERO.** Crea un `MutableState<T>` integrado en el runtime de Compose.
📍 [[Clase 19 - Jetpack Compose]] · "El estado en funciones de composición"

**M9) La sintaxis con delegado `var nombre by remember { mutableStateOf("") }` permite usar `nombre` directamente (sin `.value`), pero requiere importar `getValue`/`setValue`.**
→ **VERDADERO.**
📍 [[Clase 19 - Jetpack Compose]] · "El estado en funciones de composición"

**M10) Cualquier función de Kotlin puede emitir UI en Compose, sin necesidad de anotación especial.**
→ **FALSO.** Solo las funciones anotadas con **`@Composable`** pueden emitir/componer UI.
📍 [[Clase 19 - Jetpack Compose]] · "Funciones @Composable"

**M11) La elevación de estado (state hoisting) convierte un composable en "sin estado" reemplazando la variable interna por dos parámetros: `value: T` y `onValueChange: (T) -> Unit`.**
→ **VERDADERO.** Patrón "el estado baja, los eventos suben" (flujo unidireccional).
📍 [[Clase 19 - Jetpack Compose]] · "Elevación de estado"

**M12) `Column` apila verticalmente, `Row` horizontalmente y `Box` superpone elementos (uno sobre otro).**
→ **VERDADERO.**
📍 [[Clase 19 - Jetpack Compose]] · "Diseños básicos"

**M13) Como Compose organiza los elementos automáticamente, no hace falta usar contenedores de diseño (`Column`/`Row`/`Box`).**
→ **FALSO.** Sin contenedores de diseño, los elementos se **apilan uno encima del otro** y quedan ilegibles.
📍 [[Clase 19 - Jetpack Compose]] · "Diseños básicos"

**M14) La recomposición puede ejecutarse en cualquier orden, en paralelo y con mucha frecuencia; por eso las funciones @Composable deben ser rápidas, idempotentes y sin efectos secundarios.**
→ **VERDADERO.**
📍 [[Clase 19 - Jetpack Compose]] · "Recomposición"

**M15) Es correcto que un `@Composable` actualice una variable global o dispare una llamada de red directamente en su cuerpo, ya que Compose garantiza que se ejecute una sola vez.**
→ **FALSO.** No se debe depender de efectos secundarios (la recomposición puede omitirse, repetirse o ejecutarse en paralelo). El trabajo costoso/asíncrono va fuera de la composición.
📍 [[Clase 19 - Jetpack Compose]] · "Recomposición (consideraciones)"

## Navigation (Compose)

**M16) El `NavController` se obtiene con `rememberNavController()` y debe crearse en un punto de la jerarquía accesible por todos los composables que lo necesiten.**
→ **VERDADERO.**
📍 [[Clase 20 - Navegación]] · "NavController"

**M17) El `NavHost` vincula el `NavController` con el grafo de navegación; cada destino se define con `composable("ruta") { ... }` y se requiere una `startDestination`.**
→ **VERDADERO.** Se usa el DSL de Kotlin, no XML.
📍 [[Clase 20 - Navegación]] · "NavHost"

**M18) Para navegar se llama a `navController.navigate("ruta")`, y esta llamada debe hacerse dentro de un **callback**, no durante la composición.**
→ **VERDADERO.** Llamarla en el cuerpo del composable la dispararía en cada recomposición.
📍 [[Clase 20 - Navegación]] · "Cómo navegar"

**M19) Para pasar un argumento se define la ruta con marcador (`"perfil/{userId}"`) y dentro del `composable` se extrae desde `navBackStackEntry.arguments`.**
→ **VERDADERO.** Los argumentos se declaran con `navArgument(...)` y por defecto son `String`.
📍 [[Clase 20 - Navegación]] · "Cómo navegar con argumentos"

**M20) Se recomienda pasar objetos de datos complejos completos como argumentos de navegación.**
→ **FALSO.** Se pasa la **información mínima** (un ID); el objeto se carga desde la fuente única de información con ese ID. Evita pérdida de datos en cambios de configuración.
📍 [[Clase 20 - Navegación]] · "Cómo navegar con argumentos"

**M21) El desarrollador no puede manipular la back stack porque la administra íntegramente el sistema operativo.**
→ **FALSO.** Se puede manipular con `navigate()` y sus opciones (agregar/quitar destinos, popUpTo, etc.).
📍 [[Clase 20 - Navegación]] · "back stack / navegar"

**M22) El botón Arriba (Up) nunca saca al usuario de la app; en el destino de inicio ni siquiera aparece.**
→ **VERDADERO.** El que permite salir es Atrás.
📍 [[Clase 20 - Navegación]] · "Principios de navegación"

**M23) Un deep link en Navigation Compose se declara con `deepLinks = listOf(navDeepLink { ... })`, pero para exponerlo a apps externas hay que agregar un `<intent-filter>` en el `manifest.xml`.**
→ **VERDADERO.**
📍 [[Clase 20 - Navegación]] · "Vínculos directos"

## Arquitectura (Android)

**M24) El `ViewModel` sobrevive a los cambios de configuración; para lanzar corrutinas dentro de él se usa `viewModelScope`.**
→ **VERDADERO.**
📍 [[Clase 21 - Arquitectura]] · "Capa de IU / exponer el estado"

**M25) La práctica recomendada es exponer el estado como `StateFlow<UiState>` (inmutable) respaldado por un `MutableStateFlow<UiState>` privado.**
→ **VERDADERO.** Patrón: mutable interno → inmutable expuesto.
📍 [[Clase 21 - Arquitectura]] · "Cómo exponer el estado"

**M26) El estado de la IU (`UiState`) debe ser **inmutable** y nunca modificarse directamente desde la IU.**
→ **VERDADERO.** Modificarlo en la IU genera múltiples fuentes de verdad e inconsistencias.
📍 [[Clase 21 - Arquitectura]] · "Estado de la IU"

**M27) Las capas superiores pueden acceder directamente a las fuentes de datos (Data Sources) sin pasar por el repositorio.**
→ **FALSO.** El **punto de entrada a la capa de datos es siempre el repositorio**; las fuentes no se acceden directamente.
📍 [[Clase 21 - Arquitectura]] · "Capa de datos"

**M28) En el flujo unidireccional de datos (UDF), el estado baja (ViewModel → IU) y los eventos suben (IU → ViewModel).**
→ **VERDADERO.**
📍 [[Clase 21 - Arquitectura]] · "UDF"

**M29) Es seguro hacer una consulta a base de datos o red directamente en el hilo principal (UI Thread) porque Android lo optimiza.**
→ **FALSO.** Bloquea la UI (la congela). Debe ser seguro para el hilo principal → corrutinas / segundo plano.
📍 [[Clase 21 - Arquitectura]] · "Subprocesos"

**M30) Para inyectar dependencias en Android se puede usar la biblioteca **Hilt** (patrón de Inyección de Dependencias).**
→ **VERDADERO.** Alternativa: Service Locator.
📍 [[Clase 21 - Arquitectura]] · "Administración de dependencias"

**M31) Convención de nombres: un repositorio se llama `NewsRepository` y una fuente de datos remota `NewsRemoteDataSource` (tipo de dato + Remote/Local + DataSource).**
→ **VERDADERO.** Nunca nombrar la fuente por su implementación (Retrofit, Room, etc.).
📍 [[Clase 21 - Arquitectura]] · "Convenciones de nombre"

**M32) Una `StateFlow` es un tipo más especializado de `Flow` que siempre tiene un valor actual y lo mantiene observable.**
→ **VERDADERO.**
📍 [[Clase 21 - Arquitectura]] · "Exponer el estado" · [[Clase 18 - Kotlin]]

### Respuesta corta / código (Mobile)

- **¿Cómo declarás y recordás un estado local en Compose?** → `var texto by remember { mutableStateOf("") }` (o `rememberSaveable` para sobrevivir rotación).
- **¿Cómo definís el grafo mínimo de navegación?** → `val nav = rememberNavController()` + `NavHost(nav, startDestination = "home") { composable("home") { HomeScreen() } }`.
- **¿Cómo navegás a otra pantalla desde un botón?** → dentro del `onClick`: `nav.navigate("detalle")` (nunca en el cuerpo del composable).
- **¿Cómo hacés un composable reutilizable y testeable respecto del estado?** → aplicando **state hoisting**: recibe `value` y `onValueChange` como parámetros (sin estado interno).
- **¿Cómo se lanza trabajo asíncrono desde un ViewModel?** → `viewModelScope.launch { ... }` con funciones `suspend`.

---

## Tabla de respuestas

**Web:** W1 F · W2 V · W3 V · W4 F · W5 F · W6 V · W7 F · W8 V · W9 F · W10 V · W11 F · W12 F · W13 V · W14 F · W15 V · W16 F · W17 F · W18 V · W19 F · W20 V · W21 V · W22 F · W23 V · W24 V · W25 V · W26 V · W27 V · W28 V · W29 F · W30 F · W31 V · W32 V · W33 V · W34 F · W35 V

**Mobile:** M1 V · M2 V · M3 V · M4 F · M5 F · M6 V · M7 V · M8 V · M9 V · M10 F · M11 V · M12 V · M13 F · M14 V · M15 F · M16 V · M17 V · M18 V · M19 V · M20 F · M21 F · M22 V · M23 V · M24 V · M25 V · M26 V · M27 F · M28 V · M29 F · M30 V · M31 V · M32 V
