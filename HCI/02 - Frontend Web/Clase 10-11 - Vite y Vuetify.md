# Clase 10-11 - Vite y Vuetify

---

## Vite

### ¿Por qué existe?
- Antes de los **módulos ES** nativos no había mecanismo para crear JS modular en el navegador.
- Surgieron **bundlers** (webpack, Rollup, Parcel) que analizan, procesan y **concatenan** el código (empaquetamiento).
- Al crecer las aplicaciones, estas herramientas presentaban **cuellos de botella de rendimiento** (minutos para levantar el servidor de desarrollo), afectando la productividad.

### ¿Qué es Vite?
- "Vite" = "rápido" en francés (se pronuncia "veet"). Herramienta de **compilación (build)** para una experiencia de desarrollo más rápida.
- Dos partes:
  1. **Servidor de desarrollo** con mejoras sobre módulos ES nativos, incluyendo **Hot Module Replacement (HMR)** extremadamente rápido.
  2. **Comando de compilación** que empaqueta con **Rollup**, preconfigurado para generar recursos estáticos optimizados para producción.
- Es **dogmático** (opinionated), con configuraciones por defecto listas para usar, pero altamente extensible vía plugins.

### Cómo mejora el arranque
Vite divide los módulos en dos categorías:
- **Dependencias**: JS plano que casi no cambia. Vite las **preempaqueta** usando un bundler escrito en **Go** (esbuild), 10–100× más rápido que los basados en JavaScript.
- **Código fuente**: JS "no puro" que necesita transformación (JSX, CSS, componentes Vue) y se edita seguido. Vite lo sirve sobre **ESM nativo**, transformando y sirviendo **a pedido** según lo solicita el navegador.

> Nota: la presentación menciona "Rollup está escrito en Go" — en la práctica, la preempaquetación de dependencias la hace **esbuild** (escrito en Go); Rollup se usa para el build de producción.

---

## Vuetify

### Contexto: Design Systems y Frameworks CSS
- Los **sistemas de diseño (Design Systems)** establecen un diseño y una experiencia de usuario **consistentes**. **Material Design** (Google) es uno de los más populares.
- Los **Frameworks CSS** pueden estar basados en:
  - **Clases "utilidad"**: clases CSS para dar estilo individual a cada elemento (ej: `p-4`, `bg-yellow-200`). Ejemplo: **Tailwind CSS**.
  - **Componentes**: bloques reutilizables predefinidos con estilos y variaciones (ej: `<v-btn>`, `<v-card>`). Ejemplo: **Vuetify, Bootstrap**.
- Frameworks CSS famosos: Bootstrap, Tailwind CSS, Foundation, Bulma, Skeleton.

### ¿Qué es Vuetify?
- Biblioteca **multiplataforma de componentes reutilizables de Vue.js**, construidos según la especificación de **Material Design**.
- De uso libre y código abierto. Creada inicialmente por **John Leider**. Publicada por primera vez en **diciembre de 2016**.
- Arquitectura **incremental** (aplicable a proyectos existentes).
- Compatible con Chromium (Chrome/Edge) 90+, Firefox 88+, Safari 15+ (otros vía polyfills).
- Basada en **componentes** (framework de componentes, no de utilidades).

### Temas cubiertos
- Diseños prefabricados / wireframes.
- Colores y tipografías (paleta Material).
- Botones e íconos (Material Design Icons).
- **Puntos de quiebre (breakpoints)** y visibilidad (display helpers).
- Espaciado (spacing).
- Temas (theme configuration / generator).
- **Sistema de grilla** y **Flex**.
- Componentes de UI (application layout).

## Preguntas típicas V/F

- Vite usa Rollup para el build de producción → **Verdadero**.
- Vite requiere empaquetar toda la aplicación antes de servir el servidor de desarrollo → **Falso** (sirve el código fuente sobre ESM nativo, a pedido).
- Vuetify es un framework CSS basado en clases de utilidad → **Falso** (está basado en **componentes**; Tailwind es el de utilidades).
- Vuetify implementa la especificación de Material Design → **Verdadero**.
- HMR (Hot Module Replacement) es una funcionalidad del servidor de desarrollo de Vite → **Verdadero**.
