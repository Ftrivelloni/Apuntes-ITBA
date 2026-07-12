# Clase 08 - HTML y Desarrollo Web

Incluye: Introducción al Desarrollo Web, Estándares Web, Herramientas y HTML.

---

## Introducción al Desarrollo Web — Las tres capas

El contenido de una página web se ve alterado por tres capas:

- **Estructura**: semántica de los fragmentos de contenido y sus relaciones → **HTML**.
- **Presentación**: cómo dar formato al contenido → **CSS**.
- **Comportamiento**: cómo reacciona el contenido a la interacción del usuario → **JavaScript**.

**Buenas prácticas**: cada capa debe estar **separada** del resto y usarse **solo para el propósito** que fue creada.

### Evolución
- **1996**: la mayoría de las páginas mezclaban las tres capas.
- **2002**: **CSS Zen Garden** demuestra que una sola página HTML puede verse de mil formas cambiando solo el CSS → buena práctica: separar **estructura** de **presentación**.
- **2005**: surge el término **AJAX** y las primeras librerías JS → buena práctica: separar el **comportamiento**.

### Beneficios de separar las capas
- **Accesibilidad** (etiquetas semánticas → screen readers).
- **Portabilidad** (reusar CSS/JS en otros proyectos).
- **Mantenibilidad** (cambiar CSS sin afectar HTML ni JS).
- **Reducción de latencia** (archivos separados se cachean).

**Mejora progresiva (Progressive Enhancement)** — no confundir con Graceful Degradation: "Una escalera mecánica no se puede romper, solo puede convertirse en una escalera." Garantiza que la interfaz funcione aunque JS esté desactivado o el CSS cargue lento.

---

## Estándares Web

**Primera guerra de los navegadores (1995-2000)**. Causas de incompatibilidad: estándares que no existían o llegaban tarde, navegadores que no los respetaban, desarrolladores que los desconocían.

- **W3C (World Wide Web Consortium)**: fundado por **Tim Berners-Lee** en **octubre de 1994**. Misión: unir a la industria para que los estándares sean compatibles. Publica **W3C Recommendations**.
  - Niveles de madurez: **Working Draft (WD)** → **Last Call WD (LCWD)** → **Candidate Recommendation (CR)** → **Proposed Recommendation (PR)** → **W3C Recommendation (REC)**.
  - Consejo: evitar borradores tempranos (WD); las notas informativas **no** son estándares.
- **WHATWG (Web Hypertext Application Technology Working Group)**: comunidad creada por **Apple, Mozilla y Opera** para mejorar HTML. Surgió por el **lento progreso del W3C** (que apostaba a XML/XHTML, no retrocompatibles). El **28 de mayo de 2019** el W3C cedió el control de HTML y DOM al WHATWG.
- **ECMA International**: estandariza JavaScript (**ECMA-262**, ECMAScript).

HTML5 → HTML Standard (whatwg.org). CSS → W3C. JavaScript → ECMA-262.

---

## Herramientas para el Desarrollo Web

- **W3C HTML Validation Service** (validator.w3.org) y **W3C CSS Validation Service** (jigsaw.w3.org/css-validator).
- **WAVE** (Web Accessibility Evaluation Tool).
- Dato: hasta sitios grandes tienen errores de validación HTML5 (Google 137 errores, Amazon 148, Wikipedia solo 3).
- **BrowserStack** (screenshots multi-navegador).
- **DevTools**: Chrome/Edge (Ctrl+Shift+I), Firebug (Firefox, F12), Web Inspector (Safari), Dragonfly (Opera).
- Extensiones: **Web Developer**, **Vue.js devtools**.
- IDE: **Visual Studio Code** + extensión oficial de Vue (Volar).
- Frameworks del curso: **Vuetify, Vue.js, Vue Router, Pinia**.

---

## HTML (HyperText Markup Language)

### Cómo accedemos a la web
- **Navegadores** (Chrome, Firefox, Edge, Safari, Opera): no confiar en que todos usan la última versión.
- **Servidores web**: computadoras conectadas constantemente, optimizadas para enviar páginas.
- **Dispositivos**: distintos tamaños de pantalla y velocidades de conexión.
- **Screen readers**: leen el contenido de la pantalla (usuarios con discapacidad visual); varios países exigen accesibilidad por ley.

### Cómo funciona la web
- El navegador se conecta primero a un servidor **DNS (Domain Name System)**, que actúa como guía telefónica y asocia una dirección **IP** al nombre de dominio.
- Cada dispositivo tiene una IP única.

### Estructura y elementos
- Las páginas HTML son documentos de **texto**.
- Usa **etiquetas (tags)** entre corchetes angulares `< >`, que hacen de contenedores.
- Etiquetas ≠ elementos (técnicamente no son lo mismo).
- Generalmente van de a pares: **apertura** y **cierre**.
- Las etiquetas de apertura pueden contener **atributos** (nombre + valor) que dan más información.

### Contenido cubierto
- **Textos**: encabezados `<h1>`–`<h6>`, párrafos, énfasis, importante; información semántica.
- **Listas**: ordenada, no ordenada y de definición (se pueden anidar).
- **Enlaces**: elemento `<a>` con atributo `href`. Preferir enlaces **relativos** dentro del mismo sitio. `mailto:` para correos. `id` como destino interno.
- **Imágenes**: `<img>` con `src` (obligatorio) y `alt` (describe el contenido). Fotografías → JPG; ilustraciones/logos de colores planos → GIF.
- **Tablas**: `<table>`, filas `<tr>`, celdas `<td>` (o `<th>` para encabezado); `rowspan`/`colspan`; tablas extensas: `<thead>`, `<tbody>`, `<tfoot>`.
- **Formularios**: `<form>`; info enviada como pares **nombre/valor**; cada control necesita `name`. HTML5 introduce nuevos elementos.

### Versiones de HTML
- **HTML 4 (1997)**: la mayoría de los elementos cotidianos ya existían; algunos elementos presentacionales que cayeron en desuso por CSS.
- **XHTML (2000)**: reformulación con reglas estrictas de XML (todo cierra, atributos en minúscula con valor entre comillas dobles).
- **HTML 5 (2014)**: no obliga a cerrar todas las etiquetas; nuevos elementos (`<header>`, `<footer>`, `<nav>`, `required`); modelos detallados de procesamiento para interoperabilidad; degrada bien en navegadores viejos.

### DOCTYPES
Cada página indica su versión de HTML al navegador (ayuda a representar correctamente — problema del **box model**).
- HTML 5: `<!DOCTYPE html>`
- HTML 4: `<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">`

### Otras etiquetas
- Comentarios: `<!-- -->`.
- `id` y `class` identifican elementos particulares.
- `<div>` (bloque) y `<span>` (línea) agrupan elementos.
- `<meta>` proporciona información sobre la página.
- Caracteres de escape para especiales (`<`, `>`, `©`).

## Preguntas típicas V/F

- HTML define la presentación de la página → **Falso** (HTML = estructura; CSS = presentación).
- El W3C fue fundado por Tim Berners-Lee en 1994 → **Verdadero**.
- El WHATWG surgió porque el W3C avanzaba lento con HTML y apostaba a XML/XHTML → **Verdadero**.
- HTML5 obliga a cerrar todas las etiquetas → **Falso** (eso era XHTML; HTML5 no obliga).
- En una imagen, el atributo `alt` es opcional → **Falso** (se debe especificar siempre, junto con `src`).
- La mejora progresiva es lo mismo que la degradación elegante → **Falso** (no confundir).
