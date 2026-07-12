# Clase 09-10 - CSS (Cascading Style Sheets)

## Introducción

CSS controla el **diseño/presentación** de las páginas web. Permite crear **reglas** que especifican cómo mostrar el contenido de un elemento. Aprender CSS ≈ aprender las **propiedades** disponibles.

**Modelo de cajas**: imaginar una **caja invisible** alrededor de cada elemento HTML.
- **Elementos en bloque**: comienzan en nueva línea (`<h1>`–`<h6>`, `<p>`, `<div>`).
- **Elementos en línea**: fluyen dentro del texto, no comienzan en nueva línea (`<img>`, `<em>`, `<span>`).

### Anatomía de una regla CSS
Una regla tiene dos partes: **selector** y **declaración**.
- **Selector**: indica los elementos a los que aplica.
- **Declaración**: entre `{ }`, formada por **propiedad : valor**, separadas por `;`.

Ejemplo: `p { color: black; }` — el texto de todos los `<p>` en negro.

### CSS externo, interno y en línea
- **Externo** (`<link>` en el `<head>`): atributos `href`, `rel="stylesheet"`, `type="text/css"` (no obligatorio en HTML5). **Recomendado** para sitios de más de una página (reutilizar reglas, cambiar todo en un archivo, separar contenido de presentación).
- **Interno** (`<style>` en el `<head>`).
- **En línea** (atributo `style`, HTML4): **no recomendado**.

## Selectores

| Selector | Significado | Ejemplo |
|---|---|---|
| Universal | Todos los elementos | `* {}` |
| Tipo | Elementos de cierto nombre | `h1, h2, h3 {}` |
| Clase | Atributo `class` con cierto valor | `.note {}` |
| ID | Atributo `id` | `#introduction {}` |
| Hijo | Hijos directos | `li>a {}` |
| Descendiente (espacio) | Anidados en cualquier nivel | `p a {}` |
| Hermano adyacente | Hermano inmediato siguiente | `h1+p {}` |
| Hermano general | Hermanos (no adyacentes) | `h1~p {}` |

### Selectores de atributo
- Existencia `[]`: `p[class]`
- Equivalencia `[=]`: `p[class="dog"]`
- Espacio `[~=]`: valor dentro de una lista separada por espacios
- Prefijo `[^=]`: valor que **comienza** con
- Subcadena `[*=]`: valor que **contiene**
- Sufijo `[$=]`: valor que **termina** con

## Cascada y herencia

**Cascada** (precedencia cuando varias reglas aplican):
1. **Última regla**: si los selectores son idénticos, gana el último.
2. **Especificidad**: gana el selector más específico.
3. **`!important`**: fuerza que una regla sea más importante que el resto.

**Herencia**: `font-family` y `color` **se heredan** a los hijos. `background-color` y `border` **NO se heredan**. Se puede forzar con el valor `inherit`.

## Colores

Propiedades: `color` (texto) y `background-color` (fondo; transparente por defecto). Tres formas de especificar color:
- **RGB**: `rgb(100,100,90)`
- **Hexadecimal**: `#ee3e80`
- **Nombres**: 147 nombres predefinidos (`DarkCyan`)

- **Contraste**: asegurar suficiente contraste para legibilidad (afecta a personas con discapacidad visual, pantallas de baja resolución, sol). En textos extensos, reducir levemente el contraste mejora la legibilidad.
- **Opacidad**: `opacity` (0.0–1.0, CSS3) afecta al elemento y sus hijos. **RGBA**: cuarto valor **alpha** (solo afecta al elemento aplicado).
- **HSL / HSLA** (CSS3): Matiz (0–360), Saturación (0–100%), Luminosidad (0–100%); HSLA agrega transparencia. Poner una regla de contingencia (hex/RGB) **antes** por compatibilidad.

## Tipografías

- **Serif** (Georgia, Times): detalles en trazos (serifs); para textos impresos extensos.
- **Sans-serif** (Arial, Verdana, Helvetica): líneas rectas, más limpias; mejores en pantallas con texto pequeño.
- **Monospace** (Courier): mismo ancho por letra; para código.

- `font-family`: la tipografía debe estar **instalada** en la máquina del usuario. Especificar una **lista** separada por comas con nombre genérico al final (`serif`, `sans-serif`). Nombres de dos palabras entre comillas dobles.
- `font-size`: **píxeles** (`px`, precisos, relativos a la resolución), **porcentajes** (por defecto 16px → 75%=12px, 200%=32px), **EMS** (1em = ancho de la let 'm').
- **`@font-face`**: usar una tipografía **no instalada** especificando su ruta (`src`) para descargarla. Verificar **licencia** de uso comercial.

### Pseudo-elementos y pseudo-clases (se especifican al final del selector)
- **Pseudo-elementos** (como un elemento extra): `:first-letter`, `:first-line`.
- **Pseudo-clases** (valor adicional de `class`): `:visited` (enlaces visitados), `:hover` (cursor encima).

## Cajas (Box model)

- **Dimensiones**: `width` y `height` (px, %, ems). Limitar: `min-width`/`max-width`, `min-height`/`max-height`, `overflow`.
- **Borde, margen y relleno**:
  - **Borde**: separa los límites de una caja de otra.
  - **Margen (`margin`)**: por fuera del borde; espacio entre cajas adyacentes. Los márgenes **colapsan** (se usa el mayor). No se hereda.
  - **Relleno (`padding`)**: espacio entre el borde y el contenido; mejora legibilidad. No se hereda.
  - Importante: borde, margen y relleno **se suman** al ancho/alto total de la caja.
- **Borde**: `border-width` (px, o thin/medium/thick), `border-style` (solid, dotted, dashed, double, groove, ridge, inset, outset, hidden/none), `border-color`. Atajo `border`. Valores por lados en sentido **horario** (arriba, derecha, abajo, izquierda).
- **Centrar contenido**: `margin` izquierdo y derecho en `auto` + asignar un `width`.
- **`display`**: `inline`, `block`, `inline-block`, `none` (elimina el elemento, ocupa 0 espacio).
- **`visibility`**: `hidden` (oculta pero **conserva el espacio**) o `visible`.

## Disposición (Layout)

**Esquemas de posicionamiento** (propiedad `position`):
- **Flujo normal (static)**: cada bloque en nueva línea, uno debajo del otro. Comportamiento por defecto (no hace falta poner `static`).
- **Relativo (`relative`)**: mueve el elemento respecto de su posición en el flujo normal; **no afecta** a los elementos que lo rodean.
- **Absoluto (`absolute`)**: mueve respecto del **elemento contenedor**; se **remueve del flujo normal** (los demás actúan como si no estuviera). Se mueve al hacer scroll.
- **Fijo (`fixed`)**: variante del absoluto, respecto de la **ventana del navegador**; **no se mueve** al hacer scroll.
- Propiedades de desplazamiento: `top`/`bottom`, `left`/`right`.

- **`z-index`**: controla la superposición (mayor valor = más al frente). Sin z-index, gana el que aparece **después** en el HTML.
- **`float`**: posiciona un elemento a la izquierda o derecha del contenedor; el resto fluye a su alrededor. Requiere especificar `width`. **`clear`**: impide que un elemento toque los bordes de otro flotante.

### Diseño de ancho fijo vs. responsivo
- **Ancho fijo** (unidad: **píxel**): preciso, gran control, longitud de línea controlada, imágenes del mismo tamaño. Desventajas: zonas vacías en los bordes, se ve pequeño en alta resolución, textos pueden no caber.
- **Responsivo** (unidad: **porcentaje**): se adapta al tamaño de ventana; tolerante a cambios de tipografía. Desventajas: puede verse distinto, líneas muy largas en pantallas anchas o palabras aplastadas en pantallas angostas.
- Recomendación: páginas de 960–1000 px de ancho, indicar de qué trata el sitio en los primeros 600 px. Los **sistemas de grillas** y **frameworks CSS** ayudan.

## Imágenes en CSS

- `height`/`width`: especificar dimensiones permite carga fluida (HTML/CSS cargan antes que las imágenes). Usar clases (small, medium, large).
- **Alineación**: `float` (horizontal) + `margin` para separar texto. Para centrar: convertir a bloque con `display` + `text-align: center` o `margin` auto.
- **Fondo**: `background-image` (`url(...)`, se repite por defecto), `background-repeat` (repeat, repeat-x, repeat-y, no-repeat), `background-attachment` (fixed/scroll), `background-position` (horizontal + vertical). Atajo `background`.
- **Sprites**: combinar varias imágenes en una para reducir descargas.

## Preguntas típicas V/F

- Una regla CSS se compone de selector y declaración → **Verdadero**.
- La propiedad `color` NO se hereda a los elementos hijos → **Falso** (sí se hereda; `background-color` y `border` no).
- `display: none` oculta el elemento pero mantiene su espacio → **Falso** (lo elimina; `visibility: hidden` sí conserva el espacio).
- Con `position: fixed` el elemento se desplaza al hacer scroll → **Falso** (queda fijo respecto de la ventana).
- El diseño responsivo usa típicamente porcentajes como unidad → **Verdadero**.
- En la cascada, un selector más específico gana sobre uno menos específico → **Verdadero**.
- `@font-face` requiere que la tipografía esté instalada en el equipo del usuario → **Falso** (justamente permite usar una no instalada).
