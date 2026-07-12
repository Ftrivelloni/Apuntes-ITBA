 # Clase 20 - Navegación (Android)

## Principios de navegación

La navegación entre pantallas y apps es central para la experiencia de usuario. El **componente Navigation** implementa estos principios por defecto (aunque igual deberían seguirse aunque no se use).

1. **Destino de inicio fijo**: cada app tiene una **primera pantalla fija** (la que se ve al iniciar desde el lanzador y la última al volver a él con Atrás).

2. **El estado de la navegación es una pila de destinos (back stack)**: al iniciar se crea una **tarea** y se muestra el destino de inicio (base de la pila). La **parte superior** es la pantalla actual; los anteriores son el historial. El destino de inicio siempre está en el **fondo**. Las operaciones actúan sobre la **parte superior** (agregar o remover el destino superior).

3. **Los botones Arriba y Atrás son idénticos dentro de la tarea de la app**:
   - **Atrás**: en la barra de navegación del sistema (abajo); navega en orden cronológico inverso (remueve el destino superior de la pila).
   - **Arriba**: en la barra de la app (arriba).
   - Dentro de la tarea de una app se comportan igual.

4. **El botón Arriba nunca sale de la aplicación**: en el destino de inicio, Arriba **no aparece** (no permite salir); Atrás sí permite salir. Con un **deep link** desde otra app, Arriba devuelve a la tarea de la app (pila simulada), mientras Atrás vuelve a la otra app.

5. **Los vínculos directos (deep links) simulan la navegación manual**: al usar un deep link se **reemplaza** la pila existente por una **pila simulada realista** (coincidente con la que se lograría navegando manualmente). El componente Navigation crea esta pila realista.

## Diseño para diferentes factores de forma

- La UI **no está vinculada a un factor de forma** específico. Las apps deben adaptarse (teléfonos de 4", TVs de 50", ventanas redimensionables de Chrome OS).
- La UI se dibuja dentro de una **ventana** cuyo tamaño puede cambiar (multiventana, redimensionamiento) → distintos recursos/layouts para distintos tamaños.

### Contenido responsivo
- Aprovechar al máximo el espacio disponible; en dispositivos grandes, proporcionar más contenido (evitar espacio en blanco excesivo).
- **No** decidir según un valor fijo de hardware (¿es tableta?, ¿relación de aspecto?). Con multiventana, el **tamaño físico no es relevante**.
- Decidir según la **parte real de la pantalla asignada** a la app (métricas de ventana de **WindowManager**).
- Convertir el tamaño en una **categoría de tamaño (buckets / breakpoints)** → limita la lógica de tamaño a **una sola ubicación** que produce un estado pasado explícitamente a otros composables.
- Los composables reutilizables deben **evitar depender del tamaño real de la pantalla**; usar el ancho por el que **realmente se renderizan**.
- Para cambiar **dónde/cómo** se muestra el contenido: modificadores o layout personalizado. Para cambiar **qué** se muestra: **`BoxWithConstraints`** (proporciona restricciones de medición para llamar distintos composables según el tamaño disponible).

### UI responsiva y navegación
Adaptar la UI al ancho, altura y ancho mínimo del dispositivo: barra de app inferior, panel lateral (drawer) permanente o contraíble, riel de navegación, etc. Material Design: la UI debe adaptarse dinámicamente a los cambios del entorno (ancho, altura, orientación, idioma), llamados colectivamente **configuración del dispositivo**.

## Cómo usar el componente Navigation (con Compose)

- Agregar la dependencia en el `build.gradle` del módulo.

### NavController
- Es la **API central**. Tiene su propio estado y hace seguimiento de la **pila** de composables (pantallas) y su estado.
- Se crea con **`rememberNavController()`** dentro de un composable.
- Debe crearse en el lugar de la jerarquía donde **todos** los composables que lo necesiten puedan accederlo.

### NavHost
- Cada `NavController` se asocia a un único **`NavHost`**, que vincula el controller con un **grafo de navegación** (destinos entre los que se puede navegar). Al navegar, el contenido del `NavHost` se **recompone automáticamente**.
- Cada destino se asocia a una **ruta (route)**: una **cadena de caracteres única** que define el acceso al composable (como un deep link interno).
- Para crearlo se necesita el `NavController` y la **ruta del destino inicial**. Se usa la **sintaxis lambda del DSL** de Kotlin (en lugar de XML), agregando destinos con el método **`composable()`** (ruta + composable asociado).

### Navegar
- Usar **`navigate(ruta)`** del `NavController`. Por defecto **agrega** el destino a la pila (se puede cambiar con opciones adicionales).
- Para respetar **single source of truth**, solo el composable o contenedor del estado del `NavController` debe hacer las llamadas de navegación. Los eventos de composables profundos deben **exponerse hacia arriba** (ej: `MyAppNavHost` como fuente única; `ProfileScreen` expone un evento como lambda).
- Solo llamar a `navigate()` dentro de un **callback**, nunca durante la composición (evita llamarlo en cada recomposición).

### Navegar con argumentos
- Agregar **marcadores de posición** en la ruta.
- Por defecto todos los argumentos son **strings**. El parámetro `arguments` de `composable()` acepta `NamedNavArgument` (creados con `navArgument()` para especificar el tipo).
- Extraer argumentos de **`NavBackStackEntry`** (disponible en la lambda de `composable()`).
- **Recomendación**: NO pasar objetos de datos complejos; pasar la **info mínima** (un ID). Los objetos complejos se cargan desde una **fuente única de información** (capa de datos) usando el ID → evita pérdida de datos en cambios de configuración e incoherencias.
- Argumentos **opcionales**: sintaxis de query (`?argName={argName}`); deben tener `defaultValue` o `nullable = true`.

### Vínculos directos (deep links)
- Navigation Compose admite deep links **implícitos**, definidos en `composable()` con `deepLinks` (lista de `NavDeepLink` creados con `navDeepLink()`).
- Asocian una URL, acción o tipo MIME a un composable. Por defecto **no se exponen** a apps externas; para exponerlos hay que agregar `<intent-filter>` en el `manifest.xml`.
- Se pueden usar para construir un `PendingIntent`. Probar con adb + la herramienta de administración de actividades (`am`).

## Preguntas típicas V/F

- El botón Arriba permite salir de la aplicación desde el destino de inicio → **Falso** (Arriba nunca sale; en el inicio ni aparece; Atrás sí sale).
- El destino de inicio siempre está en el fondo de la back stack → **Verdadero**.
- El NavController se crea con `rememberNavController()` → **Verdadero**.
- Se recomienda pasar objetos complejos como argumentos de navegación → **Falso** (pasar solo un ID / info mínima).
- Cada destino del grafo de navegación se asocia a una ruta única (string) → **Verdadero**.
- Para decidir el layout responsivo conviene usar el tamaño físico de la pantalla → **Falso** (usar el espacio real asignado a la app / métricas de ventana).
- `navigate()` debe llamarse dentro de un callback, no durante la composición → **Verdadero**.
