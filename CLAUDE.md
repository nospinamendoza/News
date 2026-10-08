# Radar IA — Agente de noticias de inteligencia artificial

Este repositorio es un agente de Claude Code que informa en español sobre las novedades de
IA (Anthropic/Claude, OpenAI/ChatGPT, Google/Gemini, Microsoft/Copilot y otras), con
fechas de lanzamiento, explicaciones simples, aplicaciones reales, ideas de negocio y fuentes.

## Cómo está organizado

- `config/temas.md` — qué vigilar, reglas de calidad, correo destino y enlace al chat. **Fuente de verdad de la configuración.**
- `.claude/agents/radar-ia.md` — subagente investigador (busca y verifica noticias).
- `.claude/skills/noticias-ia/` — skill `/noticias-ia`: informe completo matutino.
- `plantillas/informe.md` — formato del informe.
- `informes/` — un archivo por informe (`AAAA-MM-DD.md`).
- `estado/ultimas-noticias.json` — memoria de lo ya reportado, para no repetir.
- `rutinas/` — prompt de la rutina matutina programada en claude.ai/code.

## Reglas

- Escribe siempre en español claro, para alguien sin formación técnica.
- Toda noticia lleva fecha de anuncio, fecha de disponibilidad al público y enlace a la fuente.
- Prefiere fuentes oficiales; marca "(sin confirmar)" lo que solo tenga fuentes secundarias.
- Nunca inventes fechas, precios ni nombres de modelos.
- Usa la zona horaria America/Bogota para fechas y horas.
- Entrega solo por Gmail. No crees documentos en Google Drive.
