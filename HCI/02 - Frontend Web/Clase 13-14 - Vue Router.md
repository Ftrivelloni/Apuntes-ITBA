# Clase 13-14 - Vue Router (Ruteo / Navegación)

## Introducción

- Los sitios hechos con Vue.js son **aplicaciones de una sola página (SPA — Single Page Application)**, por lo que necesitan un sistema de **ruteo** que dé soporte a la navegación.
- **Vue Router** es el sistema de ruteo **oficial** de Vue.js.

Características que soporta:
- **Rutas anidadas**
- **Ruteo dinámico**
- Configuración modular basada en componentes
- Rutas con **parámetros, cadena de consulta (query) y comodines**
- **Efectos de transiciones** (basados en el sistema de transiciones de Vue.js)
- Total **control** sobre la navegación
- Customización del comportamiento del **desplazamiento vertical (scroll)**
- Correcta **codificación de las URLs**

## Conceptos cubiertos (documentación oficial)

- **Installation** / **Getting Started**.
- **Dynamic Route Matching with Params**: rutas dinámicas con parámetros.
- **Routes Matching Syntax**: sintaxis de definición de rutas.
- **Nested Routes**: rutas anidadas.
- **Programmatic Navigation**: navegación programática (ej: `router.push()`).
- **Named Routes**: rutas con nombre.
- **Passing Props to Route Components**: enviar propiedades a un componente desde una ruta.
- **Navigation Guards**: agentes de navegación (protegen/interceptan la navegación).
- **Route Meta Fields**: metadatos de una ruta.
- **Vue Router and the Composition API**: integración con Composition API.
- **Transitions**: transiciones.
- **Lazy Loading Routes**: carga diferida de rutas (mejora el rendimiento inicial).

## Preguntas típicas V/F

- Vue Router es el router oficial de Vue.js → **Verdadero**.
- Vue Router se necesita porque las aplicaciones Vue son SPA (una sola página) → **Verdadero**.
- Vue Router no soporta rutas anidadas ni parámetros → **Falso** (soporta ambas).
- Los Navigation Guards permiten interceptar/controlar la navegación → **Verdadero**.
- La carga diferida (lazy loading) de rutas carga todos los componentes al inicio → **Falso** (los carga bajo demanda).
