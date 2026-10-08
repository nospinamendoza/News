---
name: noticias-ia
description: Genera el informe diario "Radar IA" con las últimas novedades de Claude, ChatGPT, Gemini, Copilot y otras IAs, explicaciones simples, aplicaciones reales e ideas de negocio, con fechas de lanzamiento y fuentes. Lo guarda en el repo y lo envía por Gmail. Úsalo cuando el usuario pida el informe, las noticias de IA o el resumen de la mañana.
---

# /noticias-ia — Informe matutino Radar IA

Sigue estos pasos en orden. Si un paso falla (por ejemplo, falta un conector), anótalo
al final del informe y continúa con el siguiente.

## 1. Preparar

- Obtén la fecha y hora actuales con `date` (zona `America/Bogota`): `TZ=America/Bogota date "+%Y-%m-%d %H:%M"`.
- Lee `config/temas.md` (qué vigilar, reglas, correo destino).
- Lee `estado/ultimas-noticias.json` (lo ya reportado) y `plantillas/informe.md` (formato).
- Ventana de tiempo por defecto: **últimas 24 horas**. Si el usuario indica otra, úsala.

## 2. Investigar

Usa el subagente **radar-ia** (herramienta Agent, `subagent_type: radar-ia`) con este encargo:

> Hoy es {fecha}. Busca y verifica las noticias de IA de las últimas {ventana}. Cubre
> Anthropic, OpenAI, Google, Microsoft, otras IAs de `config/temas.md`, nuevas apps/casos
> de uso e ideas de negocio. Excluye lo que ya esté en `estado/ultimas-noticias.json`.
> Devuelve los hallazgos en el formato definido en tus instrucciones.

Si el subagente no está disponible, haz tú mismo la investigación siguiendo
`.claude/agents/radar-ia.md`.

## 3. Redactar

- Escribe el informe en español siguiendo `plantillas/informe.md`.
- **Cada noticia debe tener fecha de anuncio, fecha de disponibilidad al público y enlace.**
- En "Cómo funciona" elige 1-2 features y explícalos como a alguien sin formación técnica,
  con una analogía cotidiana.
- En "Ideas de negocio" da 2-3 ideas concretas, cada una ligada a una novedad del informe.
- Guarda el archivo en `informes/AAAA-MM-DD.md` (si ya existe, añade la hora: `AAAA-MM-DD-HHMM.md`).

## 4. Actualizar la memoria

Añade a `estado/ultimas-noticias.json` una entrada por noticia reportada
(`id`, `titulo`, `empresa`, `fecha_anuncio`, `url`, `reportado_en`). Conserva solo los
últimos 30 días para que el archivo no crezca indefinidamente.

## 5. Entregar

1. **Gmail** — envía el informe en HTML (con su versión en texto plano) al correo de
   `config/temas.md`, asunto `🛰️ Radar IA — {DD} {mes}: {titular principal}`.
   Al final del correo incluye el enlace al chat del agente (en `config/temas.md`)
   con el texto "¿Preguntas? Sigue la conversación aquí".
   **No crees documentos en Google Drive.**
2. **Git** — haz commit de `informes/` y `estado/` con el mensaje
   `Radar IA: informe AAAA-MM-DD` y push a la rama actual.

## 6. Responder

Deja en el chat los 3 titulares principales y cualquier paso que haya fallado. Después
quédate disponible: el usuario puede preguntar sobre el informe en este mismo chat
(profundizar una noticia, explicar un feature, desarrollar una idea de negocio).
