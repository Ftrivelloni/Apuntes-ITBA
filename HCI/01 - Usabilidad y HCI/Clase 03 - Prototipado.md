# Clase 03 - Prototipado

Etapa de UCD: **Producir soluciones de diseño**.

## ¿Qué es un prototipo?

Es una **versión temprana** de un producto destinada a ser presentada a los posibles usuarios y/o para efectuarle pruebas. Aunque posiblemente no funcione completamente, brinda una **representación visual** de cómo será el producto final.

## Tipos de prototipos (según fidelidad)

- **Baja (papel)**: dibujos o impresiones en papel; **no** permiten interacción realista.
- **Media (digital)**: hechos con una herramienta de diseño; más detalle visual y cierta interacción **sin programación**.
- **Alta (nativo)**: implementados en un lenguaje de programación; detalle visual e interacciones completamente realistas.

El uso de los distintos tipos **no es excluyente**: son útiles en diferentes momentos del ciclo de vida.

### Baja fidelidad — ventajas
- Útiles para identificar **tempranamente** defectos de diseño.
- **Rápidos** de construir y modificar.
- **Económicos** (no precisan técnicos expertos).
- **Eficientes** (se evita perder horas de desarrollo codificando prototipos desechables).

### Alta fidelidad — características
- Eficaces para recolectar datos de **rendimiento** (ej: tiempo para completar una tarea).
- Eficaces para demostrar cómo se comportará finalmente la UI.
- Se construyen con herramientas especializadas (costos adicionales).
- Necesitan **mayor tiempo** de construcción.
- Pueden **crear falsas expectativas** (el usuario puede creer que hay más avance del real).

## Video prototyping

Técnica para mostrar cómo los usuarios interactuarán con la aplicación. Extiende el prototipado haciéndolo **dinámico**, transmitiendo mejor las decisiones de diseño al contemplar las mismas tareas que hará un usuario. Ejemplos: Hanmail (cliente de mail), Mundo Cine (base de datos de películas, hecho por alumnos del ITBA).

## Prototipado en papel

- Cada pestaña (tab) en una hoja separada, visible al seleccionarla.
- Cuadros de selección simulados con recuadros de papel superpuestos.
- Cuadros dinámicos / información contextual: se representan intercambiando fragmentos de papel (ej: mensaje de error en un login inválido).

### Cuándo el papel ES útil (evaluar si los usuarios comprenden)
- Los conceptos y la terminología.
- La navegación y el flujo de trabajo.
- El contenido y si permite tomar decisiones adecuadas.
- La disposición de los elementos en la pantalla.
- La funcionalidad que necesitan (evita incluir funcionalidad innecesaria).

### Cuándo el papel NO es útil (aspectos difíciles de representar)
- Tiempos de descarga y/o respuesta (simulados por una persona → artificiales).
- Desplazamientos verticales y/o horizontales.
- Colores, imágenes y tipografías (pueden diferir de la realidad; se minimiza incluyendo al diseñador gráfico).
- Factibilidad técnica (se puede prototipar algo que no se pueda implementar).

## Prototipado en dispositivos móviles

También aplica al diseño de apps móviles, con distintos niveles de fidelidad (baja → alta).

## Herramientas

- **Figma** (colaborativa)
- **Sketch** (solo Mac)
- **Lunacy** (Win, Mac, Linux; gratuita)
- **Penpot** (diseño + código, colaborativa)

## Preguntas típicas V/F

- Los prototipos de baja fidelidad son mejores para medir el tiempo exacto de completar una tarea → **Falso** (eso es alta fidelidad).
- Los prototipos de alta fidelidad pueden generar falsas expectativas en el usuario → **Verdadero**.
- El prototipado en papel permite evaluar tiempos de respuesta reales → **Falso** (son simulados/artificiales).
- Los tipos de prototipos son excluyentes entre sí → **Falso** (son útiles en distintos momentos, no excluyentes).
