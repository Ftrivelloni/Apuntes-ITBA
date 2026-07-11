# ITBA · Vault de apuntes

Vault de [Obsidian](https://obsidian.md) con apuntes de materias del ITBA, sincronizado vía Git/GitHub entre dispositivos.

## Contenido

- **TLA/** — Autómatas, Teoría de Lenguajes y Compiladores (apuntes por tema, del 1 al 9 + índice).
- **Proba/** — Cálculo de Probabilidades.

## Sincronización entre dispositivos

Este vault usa Git como mecanismo de sincronización. Flujo básico:

```bash
# Antes de empezar a trabajar en un dispositivo:
git pull

# Después de editar notas:
git add -A
git commit -m "Actualizo apuntes"
git push
```

> [!tip]
> En dispositivos móviles se puede usar la app **Obsidian** junto con un plugin de Git (p. ej. *obsidian-git*) para automatizar `pull`/`commit`/`push`.

## Notas

- El archivo `.obsidian/workspace.json` se ignora a propósito: guarda la disposición de paneles de cada dispositivo y genera conflictos si se sincroniza.
- Los ajustes y temas de Obsidian (`.obsidian/`) **sí** se versionan, para mantener la misma configuración en todos lados.
