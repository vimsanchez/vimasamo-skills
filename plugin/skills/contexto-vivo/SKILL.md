---
name: contexto-vivo
description: Usar al tomar una decisión de arquitectura no obvia, encontrar la causa raíz de un bug, acordar una regla de negocio, o recibir una corrección/preferencia del usuario en un proyecto que dura más de una sesión — para no perder ese conocimiento.
---

# Mantener el contexto vivo (CLAUDE.md + memorias)

## Overview

El conocimiento no obvio que se genera durante el trabajo —una decisión de arquitectura, la
causa raíz de un bug, una regla de negocio, una corrección del usuario— **se pierde si solo
vive en el chat**. Persistirlo es **parte de terminar la tarea, no un extra opcional**.

El error típico no es no saber documentar: es tratar la captura como un *"¿quieres que lo
documente?"* que termina en *"lo dejamos aquí"*.

> Principio: si una decisión o causa raíz no obvia no queda en un archivo, se re-litiga o se
> re-rompe. Capturar es automático, no opcional.

## Cuándo usar

Dispara esta skill (sin que te lo pidan) justo después de:
- Tomar una **decisión de arquitectura** no obvia.
- Encontrar la **causa raíz de un bug**.
- Acordar una **regla de negocio**.
- Recibir una **corrección o preferencia** del usuario sobre cómo trabajar.

No aplica a proyectos de una sola sesión sin continuidad.

## Qué persistir y dónde

- **CLAUDE.md** — contexto operativo del proyecto: mapa de carpetas, comandos verificados,
  decisiones de arquitectura fechadas, restricciones y advertencias.
- **Memorias** — journal de decisiones/bugs/reglas; una por tema, con índice (`MEMORY.md`).

| Evento | Dónde se captura | Qué incluir |
|---|---|---|
| Decisión de arquitectura | nota fechada en `CLAUDE.md` | el porqué + alternativa descartada |
| Causa raíz de bug | memoria | síntoma + causa + comando de diagnóstico + cómo evitar regresión |
| Regla de negocio | memoria | la regla + su porqué + dónde vive en el código |
| Corrección/preferencia del usuario | memoria (`feedback`); si es duradera, también `CLAUDE.md` | qué + por qué + cómo aplicarla |

**No preguntes "¿quieres que lo documente?" como si fuera opcional.** Hazlo y avisa, o propón
el texto concreto a registrar.

## Cómo escribirlo bien (útil, no decorativo)

- **El "por qué" pegado a cada regla.** Ninguna advertencia (`never`/`⚠️`) sin la mecánica o el
  incidente que la originó. Una regla con razón se transfiere; un dogma se ignora.
- **Fecha las decisiones.** Marca lo obsoleto como "histórico" en vez de borrarlo (conserva el
  contexto de por qué se hizo así).
- **Evidencia concreta** en memorias de bug: IDs, fechas, comando de diagnóstico, y un dataset
  de regresión si existe.
- **Plantilla de memoria:** qué pasa / por qué importa / cómo aplicarla; enlaza memorias
  relacionadas.
- **Documenta las decisiones de NO-hacer** con su razón (evita re-litigar y re-romper).
- **Documenta las limitaciones de la plataforma/infra** (versión de motor, clock skew, gotchas)
  — ahí se esconden los bugs no obvios.

## Errores comunes

- **Tratar la captura como opcional** ("¿quieres que lo documente?" → "lo dejamos").
- Documentar la regla **sin el porqué**.
- **Borrar lo obsoleto** en vez de marcarlo histórico.
- Memoria de bug **sin causa raíz** ni cómo reproducir/diagnosticar.
- Dejar el conocimiento **solo en el chat**.
