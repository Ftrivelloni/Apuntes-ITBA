# Clase 21 - Arquitectura de Aplicación (Android)

## Contexto: experiencias del usuario en móviles

- Una app típica de Android consta de varios componentes: **actividades, fragmentos, servicios, proveedores de contenido y receptores de emisión** (declarados en el **manifiesto**).
- Los dispositivos móviles tienen **restricciones de recursos**: el SO puede **cerrar procesos** en cualquier momento para hacer lugar.
- Los componentes pueden **iniciarse de forma individual y desordenada** y ser finalizados en cualquier momento.
- Conclusión: **no** almacenar datos ni estado en los componentes, y los componentes **no deben ser interdependientes**.

## Principios comunes de arquitectura

1. **Separación de problemas (Separation of Concerns)** — el más importante. Error común: escribir todo en una `Activity`/`Fragment`. Estas clases de la IU solo deben tener lógica de interacción con el SO y la IU. Mantenerlas limpias evita problemas de ciclo de vida y mejora la testabilidad.

2. **Controlar la IU a partir de modelos de datos** (preferentemente de **persistencia**). Los modelos de datos son **independientes** de los elementos de la UI y su ciclo de vida. Los de persistencia son ideales: los usuarios no pierden datos si el SO destruye la app; la app funciona con conexión inestable.

3. **Única fuente de datos (SSOT — Single Source of Truth)**: cada tipo de dato tiene una única fuente propietaria (la única que puede mutarlo). Expone los datos como **tipo inmutable** y, para modificarlo, expone una función o recibe eventos. Beneficios: centraliza los cambios, protege los datos, cambios rastreables (facilita encontrar bugs). En apps **offline-first**, la SSOT suele ser una **base de datos**; en otros casos, un **ViewModel**.

4. **Flujo de datos unidireccional (UDF — Unidirectional Data Flow)**: usado junto con SSOT. El **estado fluye hacia abajo** y los **eventos hacia arriba** en la jerarquía. Garantiza consistencia, es menos propenso a errores y más fácil de depurar.

## Arquitectura recomendada (capas)

Toda app debería tener al menos **dos capas**:
- **Capa de IU (presentación)**: muestra los datos en pantalla.
- **Capa de datos**: contiene la **lógica de negocio** y expone los datos.

Y opcionalmente una tercera:
- **Capa de dominio**: simplifica y reutiliza interacciones entre IU y datos.

Las flechas del diagrama representan **dependencias** entre capas (IU → dominio → datos).

### Capa de IU
- **Elementos de la IU**: renderizan los datos en pantalla.
- **Contenedores de estado (state holders)**: como los **ViewModel**, contienen datos, los exponen a la UI y controlan la lógica.

### Capa de datos
- **Repositorios**: contienen fuentes de datos. Se crea **una clase repositorio por cada tipo de dato**.
- **Fuentes de datos (data sources)**: cada una trabaja con **un solo origen** (archivo, red o base de datos local).

### Capa de dominio (opcional)
- Se ubica entre IU y datos. Encapsula lógica de negocio **compleja** o lógica **simple reutilizada** por varios ViewModels. Opcional (usar solo cuando sea necesario).
- Sus elementos se llaman **casos de uso (use cases)** o **interactuadores**; cada uno con responsabilidad sobre una **funcionalidad única**.

### Administración de dependencias
- **Inyección de dependencias (DI)**: las clases definen sus dependencias y otra clase las provee en tiempo de ejecución (biblioteca **Hilt**).
- **Localizador de servicios (Service Locator)**: registro donde las clases obtienen sus dependencias.
- Permiten escalar el código y cambiar entre implementaciones de prueba y producción.

## Capa de IU en detalle

### Estado de la IU
- Es **lo que la app establece que se debería ver**. Cualquier cambio se refleja de inmediato.
- La definición del estado de la IU es **inmutable**. Nunca modificar el estado directamente en la IU (generaría múltiples fuentes de verdad e inconsistencias).
- Convención de nombre: **funcionalidad + UiState** (ej: `NewsUiState`).

### Administrar el estado con UDF
- Un **mediador** procesa las interacciones, define la lógica por evento y transforma las fuentes de datos → la IU solo consume y muestra el estado.
- Las clases responsables de producir el estado y contener esa lógica se llaman **contenedores de estado (state holders)**. La implementación recomendada a nivel de pantalla es un **ViewModel** (sobrevive a cambios de configuración).

Implicancias del UDF:
- El ViewModel conserva y expone el estado que consumirá la IU.
- La IU notifica al ViewModel los **eventos** de usuario.
- El ViewModel controla las acciones y **actualiza el estado**.
- El estado actualizado se envía a la IU para su renderización.
- El proceso se repite ante cualquier evento que mute el estado.

Beneficios: **coherencia** de datos (una sola fuente), **testabilidad** (fuente aislada), **mantenibilidad** (mutaciones con patrón definido).

### Exponer el estado
- Exponer el estado en un **contenedor observable** (`LiveData` o `StateFlow`) para que la IU reaccione sin extraer datos manualmente.
- Patrón común: exponer un `MutableStateFlow<UiState>` como `StateFlow<UiState>` (respaldo mutable → inmutable). Acciones asíncronas: corrutina con **`viewModelScope`**.

### Consideraciones sobre el estado
- **Estados relacionados juntos**: usar una sola clase `UiState` evita inconsistencias (ej: lista de noticias + cantidad de favoritas). Propiedades derivadas (visibilidad de un botón).
- **¿Uno o varios estados?**: el criterio es la **relación entre los elementos emitidos**. Un solo flujo da comodidad y coherencia, pero: tipos de datos **no relacionados** (mejor separar); muchos campos → más emisiones → cada emisión actualiza la vista → mitigar con `distinctUntilChanged()`.

### Consumir el estado
- Según el observable: `observe()` (LiveData) o `collect()` (flujos de Kotlin).
- Tener en cuenta el **ciclo de vida**: LiveData lo maneja implícitamente; con flujos usar **`repeatOnLifecycle()`** y el alcance de corrutina (`Lifecycle.State.STARTED`).
- Estado de **carga**: un campo booleano. Estado de **error**: puede necesitar clase de datos con mensaje/acción de reintento; mostrar con un **Snackbar**.

### Eventos de IU
- Acciones que se controlan en la capa de IU (por la IU o el ViewModel).
- **Eventos de usuario**: al interactuar (tocar, gestos); la IU los consume con **callbacks**; el ViewModel controla la lógica de negocio.
- La IU controla directamente eventos que solo modifican el **estado de un elemento de la IU** (ej: expandir/contraer). Si requiere **lógica de negocio** (actualizar datos), lo procesa el ViewModel.
- Convención: funciones del ViewModel con **verbo** según la acción (`addBookmark(id)`, `logIn(username, password)`).
- **Eventos ViewModel**: acciones originadas en el ViewModel **siempre** deben resultar en una actualización del estado de la IU (cumple UDF, sobrevive a cambios de configuración, no se pierden acciones). Ej: navegar tras login.

## Capa de datos en detalle

- Contiene **datos de la aplicación y lógica de negocio**. La separación permite reutilizarla en varias pantallas y hacer pruebas unitarias fuera de la IU.
- Formada por **repositorios** (cero a muchas fuentes de datos). Un repositorio por tipo de dato.
- Responsabilidades del **repositorio**: exponer datos, centralizar cambios, resolver conflictos entre fuentes, abstraer las fuentes, contener lógica de negocio.
- Las demás capas **nunca** acceden a las fuentes de datos directamente; el **punto de entrada es siempre el repositorio**.
- Los datos expuestos deben ser **inmutables**.
- Si un repositorio tiene una sola fuente y no depende de otros, se pueden combinar ambas responsabilidades en una clase.

### Exponer las API
- **Operaciones únicas (CRUD)**: exponer **funciones de suspensión** de Kotlin (en Java, callbacks).
- **Cambios a lo largo del tiempo**: exponer **flujos** de Kotlin (en Java, callback que emite datos nuevos).

### Convenciones de nombre
- Repositorio: **tipo de datos + Repository** (ej: `NewsRepository`).
- Fuente de datos: **tipo de datos + tipo de fuente + DataSource**, usando **Remote** o **Local** (ej: `NewsRemoteDataSource`, `NewsLocalDataSource`). Nunca nombrarla por su implementación.

### Fuente de información (source of truth)
- Cada repositorio define una **única fuente de información** (consistente, correcta, actualizada). Los datos expuestos siempre provienen de ella.
- Puede ser una fuente de datos (base de datos) o una **caché en memoria** del repositorio. Para soporte **offline**, la recomendada es una **fuente de datos local (base de datos)**.

### Subprocesos (threading)
- Llamar a fuentes de datos y repositorios debe ser **seguro para el subproceso principal** (mover operaciones de bloqueo al subproceso correspondiente).
- En Kotlin: **corrutinas**. En Java: `ExecutorService`. Room y Retrofit ya ofrecen APIs seguras.

### Modelos de negocio
- Separar las clases de modelo; el repositorio expone **solo los datos que necesitan** las otras capas. Beneficios: **ahorra memoria**, adapta tipos externos a los de la app (ej: formato de fechas), mejor separación de problemas.

### Tarea común: solicitud de red
- `NewsRemoteDataSource` maneja las operaciones de red; `NewsRepository` expone la info. Una solicitud de red es una **llamada única** (`fetchLatestNews()`). La interfaz (ej: `NewsApi`) oculta la implementación (Retrofit o HttpURLConnection). Si no hay lógica extra, el repositorio actúa como **proxy** de la fuente de datos.

## Preguntas típicas V/F

- Se recomienda escribir toda la lógica de la app en la Activity/Fragment → **Falso** (viola la separación de problemas).
- El ViewModel forma parte de la capa de IU y sobrevive a los cambios de configuración → **Verdadero**.
- En el flujo unidireccional de datos, los eventos fluyen hacia abajo y el estado hacia arriba → **Falso** (el estado baja, los eventos suben).
- Las capas superiores pueden acceder directamente a las fuentes de datos → **Falso** (el punto de entrada es siempre el repositorio).
- La capa de dominio es obligatoria en toda arquitectura Android → **Falso** (es opcional).
- El estado de la IU debe ser inmutable → **Verdadero**.
- Para soporte offline, la fuente de información recomendada es una base de datos local → **Verdadero**.
- Hilt es una biblioteca de inyección de dependencias → **Verdadero**.
- Se recomienda que el repositorio exponga operaciones únicas con funciones de suspensión de Kotlin → **Verdadero**.
