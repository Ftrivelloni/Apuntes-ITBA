# Clase 19 - Jetpack Compose

## Por qué Compose

Jetpack Compose es un moderno **kit de herramientas declarativo** de Android para compilar **IU nativas**.

- **Menos código**: más con menos código que el sistema Android View (XML); solo se escribe en **Kotlin** (no dividido entre Kotlin y XML); simple y fácil de mantener.
- **Intuitiva**: API **declarativa** (solo se describe la IU); componentes pequeños y **sin estado**; los estados son **explícitos** y se pasan al composable → **única fuente de información**; al cambiar el estado, la IU se actualiza **automáticamente**.
- **Acelera el desarrollo**: compatible con el código existente (interoperable con Views en ambos sentidos); funciona con Navigation, ViewModel y corrutinas; vista previa en vivo en Android Studio.
- **Potente**: acceso directo a las APIs de Android, soporte de Material Design, tema oscuro, animaciones.

## El paradigma declarativo

- Históricamente, la jerarquía de vistas de Android se representa como un **árbol de widgets**. Al cambiar el estado hay que **actualizar manualmente** la jerarquía (`findViewById()`, `button.setText()`, etc.) que cambian el **estado interno** del widget.
- Manipular vistas manualmente **aumenta la probabilidad de errores** (olvidar actualizar una vista, estados ilegales/conflictos). La complejidad crece con la cantidad de vistas.
- La industria migró al modelo **declarativo**: regenera **conceptualmente** toda la pantalla desde cero y aplica **solo los cambios necesarios**. Evita la complejidad de actualizar manualmente una jerarquía con estado.
- Regenerar toda la pantalla puede ser **costoso** (tiempo, cómputo, batería) → Compose elige **inteligentemente** qué partes redibujar.

## Funciones de composición (@Composable)

Una función de composición emite elementos de la IU a partir de datos. Características:
- Lleva la anotación **`@Composable`** (obligatoria; informa al compilador que convierte datos en IU).
- **Toma datos** como parámetros.
- **No devuelve nada** (describe el estado de pantalla deseado, no crea widgets).
- Es **rápida, idempotente y sin efectos secundarios** (mismo resultado con el mismo argumento; no usa variables globales ni `random()`).

## Recomposición

- En el modelo imperativo se llama a un `set` para cambiar el estado interno del widget. En Compose se **vuelve a llamar a la función** con datos nuevos → **recomposición** (los widgets emitidos se redibujan si es necesario).
- Recomponer todo el árbol es costoso → Compose usa **recomposición inteligente**: omite funciones/lambdas cuyos parámetros no cambiaron.
- **Nunca depender de efectos secundarios** (escribir una propiedad compartida, actualizar un observable del ViewModel, actualizar preferencias compartidas), porque la recomposición puede omitirse.
- Las funciones deben ser **rápidas** (operaciones costosas → corrutina en segundo plano).

Consideraciones clave:
- Las funciones pueden **ejecutarse en cualquier orden** → cada función debe ser **independiente**.
- Pueden **ejecutarse en paralelo** (varios núcleos) → ninguna debe tener efectos secundarios.
- La recomposición **omite** lo que puede.
- Es **optimista y se puede cancelar** (si un parámetro cambia antes de terminar, se cancela y reinicia).
- Puede **ejecutarse con mucha frecuencia** (cada fotograma de una animación) → mover el trabajo costoso fuera de la composición (`mutableStateOf` o `LiveData`).

## Cómo administrar estados

- El **estado** es cualquier valor que puede cambiar con el tiempo. Compose es declarativo → la única forma de actualizar es **llamar al mismo composable con argumentos nuevos**. Cada actualización de estado produce una **recomposición**. Un `TextField` **no se actualiza solo**; hay que informarle explícitamente el nuevo estado.
- **`remember`**: API para **almacenar un objeto en memoria** durante la composición (retiene el valor entre recomposiciones).
- **`mutableStateOf`**: crea un `MutableState<T>`, tipo **observable** integrado en el runtime de Compose. Cualquier cambio a `value` genera recomposición de las funciones que lo lean.
- Formas equivalentes de declarar estado:
  - `val mutableState = remember { mutableStateOf(default) }`
  - `val value by remember { mutableStateOf(default) }` (delegado `by`, requiere imports)
  - `val (value, setValue) = remember { mutableStateOf(default) }`
- **`rememberSaveable`**: retiene el estado también **entre cambios de configuración** (guarda en un `Bundle`). Opciones extra: `@Parcelize`, `MapSaver`, `ListSaver`.

### Elevación de estado (state hoisting)
Patrón para **mover el estado al invocador** de un composable, haciéndolo **sin estado**. Se reemplaza la variable de estado por dos parámetros:
- **`value: T`**: valor actual a mostrar.
- **`onValueChange: (T) -> Unit`**: evento que solicita actualizar el valor.

Propiedades del estado elevado:
- **Fuente única de información** (evita duplicación → menos errores).
- **Encapsulamiento** (solo el composable con estado lo modifica).
- **Capacidad de compartir** (con varios composables).
- **Capacidad de interceptar** (el invocador puede ignorar/modificar eventos).
- **Separación** (el estado puede almacenarse en cualquier lugar).

> Patrón: **el estado baja y los eventos suben** = **flujo unidireccional de datos (UDF)**. Separa los composables que muestran el estado de las partes que lo almacenan/cambian. Más fácil de entender, reutilizar y probar.

## Ciclo de vida de los composables

- Una **Composición** describe la IU: estructura en árbol de composables. Compose registra los composables llamados en la **composición inicial**; al cambiar el estado, programa una **recomposición**.
- Si se llama varias veces a un composable, cada llamada tiene su **propio ciclo de vida** e identidad (por su **sitio de invocación** y posición en el código fuente).
- Con listas llamadas desde el mismo sitio, Compose usa el **orden de ejecución** para distinguir instancias. Reordenar/insertar/eliminar ítems recompone todas las llamadas afectadas → usar **`key`** para identificar de forma estable una parte del árbol.

## Fases de Jetpack Compose (renderiza un fotograma en 3 fases)
1. **Composición**: **qué** IU mostrar (ejecuta las funciones y crea una descripción de la IU).
2. **Diseño (Layout)**: **dónde** ubicar la IU. Algoritmo de 3 pasos: (a) medir elementos secundarios, (b) decidir su propio tamaño, (c) colocar elementos secundarios. Cada nodo termina con ancho/alto y coordenada x/y.
3. **Dibujo (Draw)**: **cómo** se renderiza (recorre el árbol de arriba abajo dibujando cada nodo).

## Diseños básicos (layouts)

Sin indicaciones, los elementos se **apilan uno sobre otro**. Composables estándar:
- **`Column`**: dispone elementos en sentido **vertical**.
- **`Row`**: dispone elementos en sentido **horizontal**.
- **`Box`**: dispone un elemento **sobre otro** (con alineación).

Compose usa **Material Design 3**.

## Preguntas típicas V/F

- Jetpack Compose usa un paradigma imperativo → **Falso** (es **declarativo**).
- Toda función de composición debe llevar la anotación `@Composable` → **Verdadero**.
- Las funciones de composición pueden tener efectos secundarios sin problema → **Falso** (deben ser puras/sin efectos secundarios; pueden ejecutarse en cualquier orden y en paralelo).
- `remember` conserva el estado a través de cambios de configuración → **Falso** (para eso se usa `rememberSaveable`).
- En la elevación de estado, el estado baja y los eventos suben (flujo unidireccional) → **Verdadero**.
- Las tres fases de Compose son Composición, Diseño y Dibujo → **Verdadero**.
- `Row` dispone los elementos verticalmente → **Falso** (`Row` = horizontal; `Column` = vertical).
- Con Compose se escribe la UI en Kotlin y XML por separado → **Falso** (solo en Kotlin).
