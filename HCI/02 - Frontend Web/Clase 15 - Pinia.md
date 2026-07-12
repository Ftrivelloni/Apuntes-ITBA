# Clase 15 - Pinia (Manejo del Estado)

## Introducción — estado en componentes

Cada componente Vue maneja su propio **estado reactivo**. Un componente es una unidad autocontenida:
- **Estado (state)**: fuente de información (source of truth).
- **Vista (view)**: mapeo declarativo del estado.
- **Acciones (actions)**: formas en las que el estado cambia a partir de la interacción del usuario.

## El problema del estado compartido

La simplicidad falla cuando **múltiples componentes comparten un estado común**:
1. Múltiples vistas dependen de la misma parte del estado.
2. Acciones de distintas vistas necesitan **mutar** la misma parte del estado.

Workarounds insuficientes:
- Para (1): **"elevar" el estado** a un ancestro y pasarlo por props → con jerarquías complejas lleva a **Prop Drilling**. Se mitiga con **provide/inject** (inyección de dependencias).
- Para (2): sincronizar copias mediante **emisión de eventos** → frágil y difícil de mantener.

## La solución: un singleton global

- Extraer el estado compartido de los componentes y administrarlo en un **"singleton" global**.
- El árbol de componentes se convierte en una gran vista; cada componente accede al estado o ejecuta acciones **sin importar su posición** en la jerarquía.
- Separar los conceptos del manejo del estado con reglas que mantengan la **independencia entre vistas y estados** → código más estructurado y mantenible.

**Pinia** es la librería **oficial** de Vue.js para el manejo del estado (**reemplazó a Vuex**), permitiendo compartir el estado entre componentes/vistas.

## Conceptos cubiertos

- **Getting Started**.
- **What is a Store?**: qué es un store.
- **Defining a Store**: definir un store.
- **State**: estado.
- **Getters**: propiedades derivadas del estado (equivalentes a computed).
- **Actions**: acciones (equivalentes a métodos; pueden ser asíncronas).

## Preguntas típicas V/F

- Pinia es la librería oficial de manejo de estado de Vue y reemplazó a Vuex → **Verdadero**.
- El "prop drilling" ocurre al pasar estado por props a través de una jerarquía compleja de componentes → **Verdadero**.
- Sincronizar estado compartido mediante emisión de eventos es la solución recomendada → **Falso** (es frágil y difícil de mantener; se recomienda un store global).
- Los getters de Pinia cumplen un rol análogo a las propiedades computadas → **Verdadero**.
- Provide/Inject es una forma de mitigar el prop drilling → **Verdadero**.
