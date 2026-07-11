---
titulo: TLA · Índice general
materia: Autómatas, Teoría de Lenguajes y Compiladores
autor: Lic. Ana María Arias Roig
tags:
  - TLA
  - MOC
  - índice
---

# 🧭 TLA · Índice general (MOC)

> [!info] Sobre estos apuntes
> Transcripción por tema de los apuntes de **Autómatas, Teoría de Lenguajes y Compiladores** (Lic. Ana María Arias Roig). Cada nota usa callouts, LaTeX y frontmatter con tags para navegar el vault como grafo.

## 📚 Temas

1. [[1 - Introducción]] — Alfabetos, cadenas, lenguajes, inducción estructural, gramáticas y **jerarquía de Chomsky**.
2. [[2 - Autómatas Finitos]] — AFD, AFND, AFND-λ, minimización y construcción de subconjuntos.
3. [[3 - Expresiones Regulares]] — Definición, propiedades, **Análisis y Síntesis de Kleene**, Lema de Arden.
4. [[4 - Lenguajes Regulares]] — AF ↔ Gramática Regular, **lema de bombeo** y propiedades de clausura.
5. [[5 - Autómatas de Pila]] — AP, aceptación por estado final / pila vacía, APD.
6. [[6 - Gramáticas Libres de Contexto y Lema de Bombeo]] — Ambigüedad, **Forma Normal de Chomsky**, AP ↔ GLC, lema de bombeo para LIC.
7. [[7 - Análisis Sintáctico]] — Parsing descendente (**LL(1)**) y ascendente (**LR, SLR, LALR**), Yacc.
8. [[8 - Gramáticas con Atributos]] — SDD, atributos sintetizados/heredados, S- y L-atribuidas, ETDS.
9. [[9 - Máquinas de Turing]] — MT, extensiones, AAL, funciones recursivas, **Church-Turing**, decidibilidad.

## 🗺️ Mapa conceptual · Jerarquía de Chomsky

> [!abstract] De lo más restringido a lo más general
> $$\text{Regular} \subset \text{Libre de contexto} \subset \text{Sensible al contexto} \subset \text{Recursivamente enumerable}$$
>
> | Tipo | Lenguaje | Gramática | Máquina | Notas |
> |------|----------|-----------|---------|-------|
> | 3 | Regular | Regular | [[2 - Autómatas Finitos\|Autómata finito]] | [[3 - Expresiones Regulares\|ER]], [[4 - Lenguajes Regulares\|lema de bombeo]] |
> | 2 | Libre de contexto | Libre de contexto | [[5 - Autómatas de Pila\|Autómata de pila]] | [[6 - Gramáticas Libres de Contexto y Lema de Bombeo\|FNC, ambigüedad]] |
> | 1 | Sensible al contexto | Sensible al contexto | Autómata linealmente acotado | [[9 - Máquinas de Turing#Autómatas Acotados Linealmente · AAL\|AAL]] |
> | 0 | Recursivamente enumerable | Sin restricciones | [[9 - Máquinas de Turing\|Máquina de Turing]] | [[9 - Máquinas de Turing#Tipos de problemas\|decidibilidad]] |

## 🏷️ Tags principales

`#TLA` · `#autómatas` · `#lenguajes-regulares` · `#expresiones-regulares` · `#GLC` · `#autómatas-de-pila` · `#lema-de-bombeo` · `#análisis-sintáctico` · `#gramáticas-con-atributos` · `#máquinas-de-turing` · `#compiladores`
