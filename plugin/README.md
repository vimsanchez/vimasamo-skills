# Plugin `metodo` — Desarrollo de aplicaciones con Claude

Conjunto de **5 skills** que codifican un método probado para desarrollar aplicaciones
colaborando con Claude. Invocables **juntas o por separado**. Compone con el plugin
`superpowers` (no lo duplica): donde superpowers ya cubre una disciplina, estas skills la
referencian.

## Las skills

| Skill | Cuándo se activa | Qué aporta |
|---|---|---|
| `metodo:definir-proyecto` | arranque de proyecto nuevo (greenfield) | restricciones antes que stack; forma del sistema; contrato de dominio; UI; escalonado |
| `metodo:elicitar-requerimientos` | petición de feature en proyecto existente | checklist de invariantes; separar decidir-vs-preguntar; capturar reglas |
| `metodo:contexto-vivo` | tras una decisión, bug o regla no obvia | persistir el conocimiento (CLAUDE.md + memorias), automático, no opcional |
| `metodo:entrega-defensiva` | cambios a datos o al contrato de un backend | reversibilidad, compatibilidad hacia atrás, blast-radius |
| `metodo:guia` | organizar/arrancar un proyecto multi-sesión | mapa del ciclo sandbox→POC→producción + modos arquitecto→delegador→validador |

## Cómo se construyó

Cada skill se escribió con **TDD para skills** (`superpowers:writing-skills`): se observó el
comportamiento base de un agente *sin* la skill (RED), se escribió la skill para corregir los
fallos concretos observados (GREEN), y se verificó con subagentes que ahora cumplen. Las skills
no enseñan lo que el modelo ya hace bien; cierran las brechas que hace de forma inconsistente
(anclar stack antes de restricciones, no persistir el conocimiento, perder la compatibilidad
hacia atrás, etc.).

## Requisito

Estas skills **referencian** al plugin [`superpowers`](https://github.com/obra/superpowers) en
los momentos donde ya hay una disciplina probada (brainstorming, writing-plans, executing-plans,
test-driven-development, systematic-debugging, verification-before-completion). Instálalo también
para aprovechar la composición completa.

## Instalación

### Opción A — como plugin de Claude Code (recomendada para distribuir al equipo)

Publica este directorio `plugin/` en un repositorio git con un *marketplace* de Claude Code y
que cada persona lo instale:

```
/plugin marketplace add <tu-org>/<tu-repo>
/plugin install metodo
```

(El plugin vive en la carpeta `plugin/`; su manifiesto es `.claude-plugin/plugin.json`.)

### Opción B — como skills personales (rápido, una máquina)

Copia las carpetas de `plugin/skills/*` a tu directorio de skills personales
(`~/.claude/skills/`). Se activan igual, aunque sin el prefijo de namespace `metodo:`.

## Uso

- **Automático:** cada skill se auto-activa cuando su descripción coincide con lo que estás
  haciendo (p. ej., al arrancar un proyecto nuevo se activa `metodo:definir-proyecto`).
- **Explícito:** invócalas por nombre cuando quieras, p. ej. `metodo:guia` para organizar el
  trabajo de un proyecto, o `metodo:entrega-defensiva` antes de un cambio sensible.

## Versión

0.1.0 — conjunto inicial de 5 skills. El método y su caso de origen (anonimizado) están
documentados en la carpeta superior de este repositorio.
