# Clase 04 - Evaluación de Usabilidad

Etapa de UCD: **Evaluación**.

## Definición

La evaluación de usabilidad es la **medición o identificación** de posibles problemas que afectan los atributos de usabilidad de un sistema, usado por **determinados usuarios**, realizando **tareas específicas**, en **contextos particulares**. Usuarios, tareas y contextos forman parte de la definición porque los valores de los atributos varían según el conocimiento previo, las tareas y el contexto (ISO 9241-11).

- Debería realizarse **tan pronto** como se tenga un prototipo.

## Tres enfoques de evaluación

1. **Evaluación predictiva / inspección (heurística)**
2. **Evaluación empírica / experimentación (observación)**
3. **Evaluación participativa / indagación (entrevistas)**

### 1. Evaluación predictiva
- Busca **predecir** los problemas o éxitos que tendrá el usuario.
- Se basa en predicciones sobre **artefactos de diseño no funcionales** y **no requiere usuarios reales**.

**Evaluación heurística** (el método predictivo más popular):
- Un número pequeño de evaluadores (**generalmente 3 a 5**) examina **de manera independiente** el sistema y juzga su conformidad con un conjunto de reglas de interfaces usables llamadas **heurísticas**. Luego se **consolidan** las observaciones.
- Forma temprana, rápida y relativamente económica de retroalimentación.
- Aplicarla eficazmente requiere conocimiento y experiencia (expertos en usabilidad, difíciles de encontrar y costosos).
- **Jakob Nielsen**: con **cinco evaluadores** se identifica hasta el **75%** de todos los problemas. Aumentar evaluadores ayuda pero puede no valer el esfuerzo.

**Los 10 principios (heurísticas) de Jakob Nielsen**:
1. Visibilidad del estado del sistema
2. Coherencia entre el sistema y el mundo real
3. Controles y libertad del usuario
4. Consistencia y estándares
5. Prevención de errores
6. Reconocimiento en lugar de memoria
7. Flexibilidad y eficacia en el uso
8. Diseño estético y minimalista
9. Ayudar a los usuarios a reconocer, diagnosticar y recuperarse de errores
10. Ayuda y documentación

Otras heurísticas disponibles: Ben Shneiderman ("Eight Golden Rules"), Don Norman ("Seven Fundamental Design Principles"), Arnie Lund ("Expert Ratings of Usability Maxims"), Bruce Tognazzini ("First Principles of Interaction Design"). La elección depende de factores como la fidelidad del prototipo; a veces hay que generar una heurística propia.

### 2. Evaluación empírica (experimentación / observación)
- Se pide a un usuario o grupo **ejecutar un prototipo** y evaluarlo, para recolectar información y mejorar la usabilidad.
- Según Nielsen, dos formas básicas: (1) probar una interfaz **más o menos terminada** para verificar si se lograron las metas; (2) **evaluación formativa** de un sistema aún en diseño.
- Mide atributos observando **usuarios reales** interactuando con prototipos o sistemas funcionales.
- Dos formas de observación: **Directa** (investigador presente) e **Indirecta** (por video o fotografía).
- Recoge datos **cuantitativos** de rendimiento (tiempo, tasa de error) y el grado de satisfacción.

### 3. Evaluación participativa (indagación)
- Recopila información sobre atributos de usabilidad **directamente de los usuarios** mediante indagación.
- Ventaja: capta necesidades, deseos, procesos de pensamiento y experiencias difíciles de obtener de otro modo.
- Técnicas: **Encuestas** (preguntas interactivas, no estructuradas), **Cuestionarios** (listas de preguntas, esfuerzo adicional), **Entrevistas** (estímulo-respuesta).
- Preguntas ejemplo: primera impresión, adjetivos que describan el sitio, opinión sobre la organización, lo que más/menos gustó, qué mejoraría, qué falta.

## Comparación de los enfoques

| Enfoque | Participación del usuario | Tipo de medida | Propósito | Herramientas |
|---|---|---|---|---|
| **Predictiva** | No | Cualitativa / Predictiva | Verificar principios | Lista de principios |
| **Empírica** | Sí | Cualitativa + Cuantitativa | Conducta, desempeño, interacción | Lista de control, herramienta de registro |
| **Participativa** | Sí | Cualitativa + Cuantitativa + Interpretativa | Preferencias, satisfacción | Cuestionarios, encuestas, entrevistas |

## Resultados y recomendaciones

- Se realiza **primero la predictiva**, seguida por empíricas y/o participativas.
- Las hipótesis de la predictiva sirven para diseñar las tareas de la empírica.
- Los resultados de la predictiva **no necesariamente** coinciden con los de la empírica.
- Usar lo aprendido para **mejorar** el sistema; priorizar según los resultados.
- El costo de dar soporte a sistemas mal diseñados es mucho mayor que arreglarlo durante el desarrollo.

Recomendaciones:
- **Probar el sistema y NO a los usuarios.**
- Tomar métricas de rendimiento (tasa de éxito, tiempo, errores) y subjetivas (satisfacción).
- Hacer uso de lo aprendido.
- Encontrar la mejor solución dentro de las restricciones del proyecto (tiempo, presupuesto, recursos).

## Preguntas típicas V/F

- La evaluación heurística requiere la participación de usuarios reales → **Falso** (es predictiva, no requiere usuarios reales).
- Con 5 evaluadores se detecta aproximadamente el 75% de los problemas (Nielsen) → **Verdadero**.
- Se recomienda usar entre 3 y 5 evaluadores en la evaluación heurística → **Verdadero**.
- En una evaluación de usabilidad se evalúa al usuario, no al sistema → **Falso** (se prueba el sistema, no a los usuarios).
- Se recomienda hacer la evaluación empírica antes que la predictiva → **Falso** (primero la predictiva).
