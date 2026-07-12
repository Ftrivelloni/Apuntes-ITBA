# Clase 06 - Lineamientos de Usabilidad

Incluye tres partes: **Web** (Steve Krug), **Aplicaciones móviles** y **Google Material Design**.

---

## Parte A — Usabilidad Web (Steve Krug, "Don't Make Me Think")

**Usabilidad es**: garantizar que algo funcione correctamente y que una persona con habilidades y experiencia **promedio (o por debajo)** sea capaz de usarlo para el propósito que fue construido, **sin sentirse completamente frustrada**.

### Primera norma: "No me hagas pensar"
Toda página debe ser **obvia, evidente, clara y fácil de entender**. Nuestro trabajo es **deshacernos de las preguntas** que se pueda hacer el usuario.

Cosas que hacen pensar al usuario: terminología poco familiar (marketing, uso interno, jerga técnica); elementos ambiguos sobre los que se puede/no hacer clic; criterios de búsqueda poco claros. Preguntas que el usuario NO debería hacerse: ¿Dónde estoy? ¿Por dónde empiezo? ¿Dónde pusieron...? ¿Cuáles son las cosas importantes? Cada pregunta agrega **carga cognitiva**.

### Hechos del mundo real
1. **Los usuarios no leen las páginas, las escanean** (están apurados, no necesitan leer todo, son buenos escaneando). Lo que ven depende de la tarea, sus intereses y las palabras que causan reacción ("Gratis", "Oferta", su nombre).
2. **Los usuarios no eligen siempre la mejor opción**, sino la primera razonable (están apurados, no hay castigo por elegir mal → botón "volver", lleva menos trabajo).
3. **Los usuarios no se dan cuenta de cómo funcionan las cosas** (no les importa mientras puedan usarlas; una vez que algo funciona, se apegan a él). Arreglárselas funciona pero es ineficaz y proclive al error.

### Diseñando las páginas (7 aspectos)
1. **Crear una jerarquía visual clara**: lo importante más prominente; lo relacionado lógicamente también visualmente; lo anidado visualmente anidado.
2. **Usar convenciones existentes** (están probadas; dan familiaridad; los diseñadores son reacios a usarlas por querer "reinventar la rueda").
3. **Separar las páginas en zonas claramente definidas** (para decidir rápido dónde concentrarse — validado con eye tracking).
4. **Hacer obvios los elementos clickeables** (los usuarios buscan el próximo clic; no desaprovechar su paciencia).
5. **Minimizar el ruido visual**: dos tipos → **abarrotamiento** (todo llama la atención) y **ruido de fondo** (pequeños ruidos que agotan).
6. **Permitir decisiones ciegas y mecánicas** (no importa la cantidad de clics si cada uno es sencillo y mantiene la confianza).
7. **Evitar palabras innecesarias** (reduce ruido, destaca lo útil, acorta la página).

### Diseñando la navegación
La experiencia web carece de: sentido del **tamaño**, de la **dirección** y de la **ubicación**. Propósitos de la navegación: encontrar lo buscado, orientar al usuario, dar a conocer los contenidos, indicar cómo usar el sitio.

**Persistent/global navigation**: elementos que aparecen en cada página, en el mismo lugar. Confirma que se está en el mismo sitio y solo hay que descubrir cómo funciona una vez.

Elementos de la navegación:
- **Site ID / logo** (arriba)
- **Secciones** (navegación primaria)
- **Herramientas** (Ayuda, mapa del sitio, Acerca de, Contacto)
- **Mecanismo para volver a la página principal**
- **Mecanismo de búsqueda** (leyenda "Search" + cuadro + botón; no complicarlo)

**"Usted se encuentra aquí"**: resaltar la ubicación actual con **más de una distinción visual** (color + negrita).

**Breadcrumbs (migajas de pan)**: muestran el camino desde la página principal hasta la actual. Ubicar arriba, con **separador** (mejor `>`, también `:` o `/`), tipografía pequeña, remarcar el último nivel.

**Nombres de páginas**: cada página necesita un nombre, en el lugar adecuado, prominente (posición/tamaño/color), que **coincida con aquello sobre lo que se hizo clic**.

### Página Principal
Debe contener: identidad y misión, jerarquía del sitio, adelantos (como portada de revista), contenido actualizado, buscador, registración, atajos, mostrar lo que se busca y lo que no, mostrar por dónde empezar, y establecer **credibilidad y confianza**. A veces conviene **no usar** la navegación persistente en la principal (descripción de secciones, distinta orientación, Site ID más grande).

---

## Parte B — Usabilidad en Aplicaciones Móviles

**Dispositivo móvil**: fácilmente transportable, conectable a Internet, táctil (usualmente). Smartphones y tabletas.

**Clave**: un dispositivo móvil NO debe considerarse como una pequeña computadora de escritorio.

**Escritorio vs. Móvil**:
- Escritorio: tareas **lentas y complejas**.
- Móvil: tareas **rápidas y simples**.

Límites del dispositivo móvil: pantallas pequeñas, táctil (escribir es más difícil), batería limitada, acceso a internet inconsistente.

Lineamientos de diseño móvil:
- **Evitar pasos innecesarios** (autenticaciones, captchas).
- Ser **simples** (eliminar lo no esencial).
- UI **intuitiva** (entender comportamiento sin razón/experiencia/capacitación; encontrar lo necesario; ejecutar acciones con mínimo esfuerzo).
- Diseñar para **interacción táctil** (priorizar controles táctiles: botones, listas, menús desplegables).
- Asumir **desplazamiento vertical**.
- Esquema de colores adecuado.
- Facilitar acceso a acciones frecuentes.
- **Evitar el ingreso de texto**: eliminar ingresos innecesarios, buenos defaults, autocompletado, últimos valores, formatos adecuados (numérico, mail), no pedir registro si no es necesario, opción de ver la contraseña en claro.

### ¿App o sitio web móvil?

| Aspecto | Aplicación | Sitio Web |
|---|---|---|
| **Acceso** | Simple (un click) | Complejo (ingresar URL) |
| **Integración con el teléfono** | Estrecha (GPS, contactos, llamadas) | Limitada |
| **Historial del usuario** | Posible (almacena info/credenciales) | Posible (cookies pueden estar deshabilitadas) |
| **Funcionamiento offline** | Simple (detecta conexión) | Complejo |
| **Compatibilidad** | Baja (una versión por SO) | Alta (muchos dispositivos) |
| **Mantenimiento** | Alto (descargar, instalar, actualizar) | Bajo (sin descarga/instalación) |

---

## Parte C — Google Material Design

Sistema de diseño **inspirado en el mundo real** (reflejos de luz, sombras) desarrollado por Google. **Responsivo** (se adapta a distintos tamaños). Recomienda **imágenes más que palabras**.

- **Color**: comunica jerarquía, estado y marca. En una UI solo se usa una selección de los 13 colores de cada paleta tonal. Un **esquema** es el grupo de tonos asignados a roles específicos.
- **Elevación**: distancia entre dos superficies en el eje **z**. Permite mover superficies delante/detrás, refleja relaciones espaciales (sombra del FAB), centra la atención en la elevación más alta (diálogos).
- **Iconos**: usar **Material Symbols**. Si no existe, crearlo siguiendo los lineamientos. **Nunca importar íconos de otras plataformas.**
- **Tipografía**: por defecto **Roboto** (también Roboto Flex, Roboto Serif, Noto).
- **Componentes** (bloques interactivos), organizados por propósito: **Acción, Contenedores, Comunicación, Navegación, Selección, Ingreso de texto**.

## Preguntas típicas V/F

- Según Krug, los usuarios leen detalladamente cada página → **Falso** (la escanean).
- Los usuarios siempre eligen la mejor opción disponible → **Falso** (eligen la primera razonable).
- Un dispositivo móvil debe diseñarse como una PC de escritorio más chica → **Falso**.
- Las apps móviles tienen mayor compatibilidad entre dispositivos que los sitios web → **Falso** (la app tiene compatibilidad baja; el sitio web, alta).
- En Material Design la elevación se mide en el eje z → **Verdadero**.
- Material Design permite importar íconos de otras plataformas si no se encuentra el deseado → **Falso** (nunca; se crea siguiendo los lineamientos).
- Los breadcrumbs deben resaltar el último nivel y ubicarse en la parte superior → **Verdadero**.
