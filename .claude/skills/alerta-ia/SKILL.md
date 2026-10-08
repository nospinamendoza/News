---
name: alerta-ia
description: Chequeo proactivo de última hora. Revisa si en las últimas horas salió algo IMPORTANTE de IA (nuevo modelo, lanzamiento grande, cambio de precios, feature masivo) que aún no se haya reportado y, solo si lo hay, envía una alerta corta por Gmail. Úsalo para las revisiones automáticas durante el día.
---

# /alerta-ia — Alerta proactiva de última hora

El objetivo es **no molestar**: solo se envía algo si de verdad vale la pena.

## 1. Preparar

- Fecha y hora: `TZ=America/Bogota date "+%Y-%m-%d %H:%M"`.
- Lee `config/temas.md` y `estado/ultimas-noticias.json`.
- Ventana: **últimas 6 horas** (o la que indique el usuario).

## 2. Buscar

Haz 4-6 búsquedas rápidas en paralelo (WebSearch, modo estándar) sobre Anthropic, OpenAI,
Google Gemini, Microsoft Copilot y "AI launch today". Verifica en la fuente oficial lo que parezca relevante.

## 3. Decidir

Es **alerta** solo si cumple las tres condiciones:

1. Es de importancia **alta**: nuevo modelo, producto o feature disponible para el público,
   cambio de precios, cierre o cambio de un producto que el usuario usa, o una noticia que mueve la industria.
2. Fue anunciado dentro de la ventana.
3. **No** está en `estado/ultimas-noticias.json`.

Si nada cumple → responde `Sin alertas (AAAA-MM-DD HH:MM)` y termina **sin enviar correo ni hacer commit**.

## 4. Si hay alerta

1. Redacta un mensaje corto en español, máximo 1 pantalla de móvil:
   - Titular
   - Qué pasó (2-3 frases) y **cómo funciona** en una frase simple
   - 📅 Anuncio · 🚀 Disponible · 👥 Para quién
   - 💡 Una oportunidad de negocio o uso práctico
   - 🔗 Fuente oficial
2. Envíalo por Gmail al correo de `config/temas.md` con asunto `⚡ Alerta IA: {titular}`.
3. Añade la noticia a `estado/ultimas-noticias.json` para que el informe matutino no la repita como nueva
   (puede mencionarla en "Lo más importante" con la etiqueta "ya alertado").
4. Si estás en el repositorio, commit `Radar IA: alerta {titular corto}` y push.
