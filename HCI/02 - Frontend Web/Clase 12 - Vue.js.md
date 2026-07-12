# Clase 12 - Vue.js

## Introducción

- **Vue** (se pronuncia "view") es una **librería de JavaScript** para construir interfaces de usuario.
- Construida sobre estándares **HTML, CSS y JavaScript**; ofrece modelos de programación **declarativa** y **basada en componentes**.
- De uso libre y código abierto.
- Creada inicialmente por **Evan You** cuando trabajaba en Google desarrollando con Angular.
- Publicada por primera vez en **febrero de 2014**.
- Arquitectura **incremental** (aplicable a proyectos existentes).
- Compatible con navegadores modernos con soporte nativo de **ECMAScript 2015 (ES6)**.

## Componentes de Único Archivo (SFC — Single-File Component)

- Los componentes Vue se construyen en archivos `*.vue` con formato similar a HTML.
- Un SFC **encapsula en un solo archivo**: lógica (**JavaScript**), template (**HTML**) y estilo (**CSS**).
- Dos sintaxis para la lógica:
  - **Options API**: exporta un **único objeto** con variables y métodos (opciones). Las variables se acceden desde los métodos con `this`.
  - **Composition API** (disponible en Vue 3): usa **funciones del API** importadas para definir variables y métodos, combinadas con `<script setup>` para su acceso en el template.

## Conceptos cubiertos (documentación oficial)

- **Creating a Vue Application**: crear la aplicación.
- **Template Syntax**: sintaxis de plantilla.
- **Reactivity Fundamentals** (Options y Composition API): fundamentos de la reactividad.
- **Computed Properties**: propiedades computadas (derivadas del estado, con caché).
- **Class and Style Bindings**: vinculación de clase y estilo.
- **Conditional Rendering**: representación condicional (`v-if`, `v-show`).
- **List Rendering**: representación de listas (`v-for`).
- **Event Handling**: manejo de eventos (`v-on` / `@`).
- **Form Input Bindings**: vinculación de datos de formulario (`v-model`).
- **Lifecycle Hooks**: ciclo de vida del componente.
- **Watchers**: observadores.
- **Components Basics**: conceptos básicos de componentes.
- **Slots**: contenedores para pasar contenido.
- **Provide / Inject**: intercambio avanzado de datos (inyección de dependencias entre ancestro y descendiente).

## Preguntas típicas V/F

- Vue fue creado por Evan You → **Verdadero**.
- La Composition API está disponible en Vue 3 → **Verdadero**.
- Un Single-File Component separa la lógica, el template y el estilo en tres archivos distintos → **Falso** (los encapsula en un **único** archivo `.vue`).
- En la Options API las variables se acceden desde los métodos mediante `this` → **Verdadero**.
- Vue es un framework de backend → **Falso** (es una librería de UI / frontend).
