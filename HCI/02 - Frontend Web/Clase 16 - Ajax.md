# Clase 16 - Ajax (Asynchronous JavaScript and XML)

## Introducción

**AJAX** (Asynchronous JavaScript And XML) es una técnica de desarrollo web que permite crear sitios **interactivos**, realizando cambios en las páginas **sin recargarlas por completo**, aumentando interactividad, velocidad y usabilidad.

Herramientas involucradas:
- **HTML**: da estructura al contenido.
- **DOM (Document Object Model)**: permite recorrer el HTML de la página.
- **JavaScript**: manipula el DOM y —lo más importante— establece el **canal de comunicación** entre navegador y servidor.
- **CSS**: altera la presentación (también manipulable dinámicamente vía DOM).
- **XML**: uno de los formatos para transferir datos (no el único; también JSON, HTML, etc.).

## Historia

- **1996**: Microsoft introduce el `<iframe>` (primera técnica de carga asincrónica).
- **1998**: Remote Scripting (applet de Java).
- **1999**: Microsoft introduce **XMLHttpRequest** como control ActiveX en IE5; luego nativo en Firefox y Safari.
- **2005**: surge el término **Ajax**.
- **2006**: el W3C publica el primer borrador de XMLHttpRequest; IE7 lo soporta de forma nativa.
- **2015**: surge el **API Fetch** como sucesor moderno de XMLHttpRequest y estándar de facto. Aprovecha las **promesas** → código más simple, evitando la complejidad de los callbacks.

## Modelos de sitios web

- **Modelo clásico**: cada petición requiere un viaje de ida/vuelta al servidor y una **recarga completa** de la página (parpadeo). Recarga todo (CSS, JS, imágenes) → puede demorar.
- **Modelo Ajax**: también hay viaje al servidor, pero **solo se recarga la parte** que muestra la nueva información. Permite seguir haciendo otras tareas mientras carga → experiencia similar a una app de escritorio.

## JSON

Formato de intercambio de información, subconjunto de la notación literal de JavaScript. Alternativa ligera al XML. Dos estructuras:
- **Objeto**: colección de pares nombre-valor. Empieza con `{` y termina con `}`; nombre (string) separado del valor por `:`; pares separados por `,`.
- **Arreglo**: lista ordenada de valores. Empieza con `[` y termina con `]`; valores separados por `,`.

Un **valor** puede ser: string, número, `true`, `false`, `null`, objeto o arreglo (anidables). Los formatos octal y hexadecimal **no** son válidos para números.

```javascript
// String JSON → objeto
var person = JSON.parse(jsonString);
// Objeto → string JSON
var jsonString = JSON.stringify(person);
```

### JSON vs. XML — ¿cuál es mejor?
No hay respuesta única. Consideraciones:
- **Plataforma/lenguaje**: JSON solo si el cliente tiene soporte JS o un intérprete JSON.
- **Tamaño de la información**: JSON es mejor si es grande (ocupa menos, se procesa más rápido).
- **Comodidad** (JS vs. XML): preferencia.
- **Complejidad**: JSON va bien con datos textuales; XML maneja mejor sonidos/imágenes/binarios (`<[CDATA[]]>`).
- **Control del servidor / confianza**: usar JSON de un origen no confiable **sin intérprete** es un riesgo de seguridad.

## Política de mismo origen (Same-Origin Policy)

Mecanismo de seguridad crucial que restringe la interacción de un documento/script cargado por un origen con un recurso de otro. El **origen** se define por tres elementos: **protocolo, host y puerto**. Dos documentos tienen el mismo origen **si y solo si** coinciden los tres.

Ejemplos (para `http://www.example.com/dir/page.html`):
- `http://www.example.com/dir2/other.html` → **OK**
- `https://www.example.com/secure.html` → **ERROR** (distinto protocolo)
- `http://www.example.com:81/dir/etc.html` → **ERROR** (distinto puerto)
- `http://example.com/dir/other.html` → **ERROR** (distinto host)

### Formas de resolver el problema (cross-origin)
- **Cross-Domain Proxy**: un proxy en el servidor que hospeda la página hace la solicitud al servidor destino y retransmite la respuesta.
- **CORS (Cross-Origin Resource Sharing)**: extiende HTTP con el encabezado de solicitud **Origin** y el de respuesta **Access-Control-Allow-Origin**. Usa una solicitud **"preflight"**. El servidor explicita la lista de orígenes permitidos o usa comodín (`*`).
- **On-Demand JavaScript / JSONP**: agregar dinámicamente elementos `<script>` con `src` generado; el servicio debe enviar JSON. Yahoo propuso especificar una función **callback** en el query string.

## API Fetch

- Interfaz para recuperar recursos (incluso remotos). Más potente y flexible que XMLHttpRequest.
- Soporte: Firefox 34+, Safari 10.1+, Chrome 42+, Edge 14+, Opera 28+. **Ninguna versión de Internet Explorer** lo soporta (existe polyfill con restricciones).

Uso:
- `fetch(url)` retorna una **Promise**. Al resolverse, entrega un objeto **Response** al `then()`; si falla, el error va al `catch()`.
- **Importante**: respuestas inválidas como **404 también se resuelven satisfactoriamente**. La promesa solo se **rechaza** si la solicitud **no se puede completar** (ej: falla de conexión). Por eso hay que evaluar `response.ok`, `response.status`, `response.statusText`.
- Interpretar la respuesta: `Response.json()`, `Response.text()`, `Response.blob()`.
- Por defecto usa **GET**; se pueden usar POST, PUT, DELETE especificando el parámetro `init` (con `method`, `headers`, `body`).

```javascript
// GET (ES7 async/await)
async function fetchData() {
  let response = await fetch('examples/example.json');
  if (!response.ok) { throw Error(response.statusText); }
  return response.json();
}
```

```javascript
// POST
var init = {
  method: 'POST',
  headers: { 'Content-Type': 'application/json; charset=utf-8' },
  body: JSON.stringify(comment)
};
await fetch('someurl/comment', init);
```

## Aplicaciones single-page (SPA)

Sitio JavaScript que requiere la carga de una **única página**. Poca cantidad de JS de inicio + una página inicial; luego JS descarga más código bajo demanda (históricamente vía XMLHttpRequest y `eval()`), carga información y usa el DOM para mostrarla.

## Riesgos asociados con Ajax

- **Depende de JavaScript** (debe estar activado). Sin él, el sitio debe contemplar **mejora progresiva** o una versión alternativa.
- **Favoritos/bookmarks**: el estado no se puede guardar porque Ajax **no altera la URL** por defecto. Solución: un link que conserve el estado.
- **Botones back/forward**: Ajax los rompe (el "back" vuelve a la URL anterior al sitio). Se puede insertar una entrada ficticia en el historial (con incompatibilidades entre navegadores).
- **Seguridad**: HTTP envía en texto claro → usar **HTTPS** para información sensible. Riesgo de **cross-site scripting (XSS)**.
- **Falta de feedback**: sin el parpadeo de recarga, el usuario no sabe que algo sucede → agregar indicador (texto o animación de carga).

## Usos de Ajax

- **Validación en tiempo real** de formularios (ej: unicidad de nombre de usuario).
- **Autocompletado**.
- **Carga bajo demanda** (info en segundo plano).
- **Controles de UI y efectos** (árboles, menús, tablas, editores, calendarios, barras de progreso).
- **Refresco de información** sin recargar.
- **Envío parcial de información**.
- **Mashups** (mezclar datos externos, ej: Google Maps).
- **La página como aplicación** (single-page que se siente como app de escritorio).

## Preguntas típicas V/F

- Ajax requiere recargar la página completa en cada petición → **Falso** (solo recarga la parte necesaria; eso es el modelo clásico).
- Una respuesta HTTP 404 hace que la promesa de `fetch` se rechace (va al `catch`) → **Falso** (se resuelve satisfactoriamente; hay que chequear `response.ok`).
- Dos URLs con distinto puerto tienen el mismo origen → **Falso** (distinto puerto = distinto origen).
- CORS usa una solicitud "preflight" y el encabezado `Access-Control-Allow-Origin` → **Verdadero**.
- El API Fetch está soportado por todas las versiones de Internet Explorer → **Falso** (ninguna versión de IE lo soporta).
- Ajax rompe el comportamiento por defecto de los botones back/forward → **Verdadero**.
- JSON admite números en formato hexadecimal → **Falso** (no son válidos).
