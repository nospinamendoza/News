# 🛰️ Radar IA — Tu agente de noticias de Inteligencia Artificial

Un agente construido con **Claude Code** que cada mañana te cuenta, en español y en palabras simples:

- 🏢 Las novedades de **Anthropic (Claude)**, **OpenAI (ChatGPT)**, **Google (Gemini)**, **Microsoft (Copilot)** y otras IAs importantes (Meta, xAI/Grok, Mistral, DeepSeek…).
- 📅 **Cuándo** se anunció cada cosa y **cuándo** llega al público (y para quién: planes, países).
- 🧠 **Cómo funcionan** los nuevos features, con analogías cotidianas.
- 🛠️ **Aplicaciones reales**: empresas y apps que están usando la IA de forma nueva.
- 💡 **Ideas de negocio** que surgen de estas novedades.
- 📚 **Fuentes** de referencia para cada noticia.

## ☀️ Cómo funciona

| Qué | Cuándo | Dónde |
|---|---|---|
| **Informe matutino** (`/noticias-ia`) | Todos los días a las **6:53 a. m.** (hora Colombia) | 📧 Tu Gmail + 💬 el chat del agente |

1. A las 6:53 a. m. la rutina despierta **siempre el mismo chat** del agente:
   👉 **https://claude.ai/code/session_0177XdtyLdurJP2rgXrtCv6J** (título: *Radar IA — Informe diario de IA (chat)*).
2. El agente investiga las últimas 24 h, redacta el informe y te lo envía por **Gmail**.
3. Deja los 3 titulares en ese chat y queda listo para que le preguntes lo que quieras.

👉 Ejemplo real: [`informes/2026-10-08.md`](informes/2026-10-08.md) (primer informe generado).

---

## 💬 Conversar con el agente

Abre el chat (el enlace viene al final de cada correo) y pregunta, por ejemplo:

- *"Explícame más fácil cómo funciona la interfaz de GPT-6."*
- *"¿Qué de esto me sirve a mí como usuario de Gemini gratis?"*
- *"Desarrolla la idea de negocio 2: costos, clientes y primeros pasos."*
- *"Hazme el informe de nuevo pero de toda la semana."* (ejecuta `/noticias-ia` con otra ventana)
- *"Agrega Apple y Perplexity a lo que vigilas."* (edita `config/temas.md`)

Como es siempre el mismo chat, el agente recuerda los informes anteriores y lo que ya conversaron.

---

## 🧩 Conceptos en 1 minuto (tu primer agente)

| Concepto | Qué es | En este proyecto |
|---|---|---|
| **Claude Code** | Claude trabajando como asistente que puede leer archivos, buscar en internet y usar herramientas. | El motor de todo. |
| **CLAUDE.md** | Las "instrucciones de la casa": Claude lo lee siempre al abrir el proyecto. | [`CLAUDE.md`](CLAUDE.md) |
| **Subagente** | Un Claude especialista con su propio rol y herramientas, al que el agente principal le delega trabajo. | [`.claude/agents/radar-ia.md`](.claude/agents/radar-ia.md) — el investigador. |
| **Skill** (habilidad) | Una "receta" guardada en un `SKILL.md`. Se invoca escribiendo `/nombre`. | `/noticias-ia` en [`.claude/skills/`](.claude/skills/) |
| **Conector** | Permiso para que Claude use tus apps. | Gmail, para enviarte el informe. |
| **Rutina** (Routine) | Una tarea programada que corre sola en la nube, aunque tu computador esté apagado. | El informe de las 6:53 a. m. |

```
 Rutina 6:53 a. m. ──▶ chat del agente ──▶ /noticias-ia ──▶ subagente radar-ia
                         (siempre el mismo)       │            (busca y verifica)
                                                  ▼
                                    redacta el informe
                                                  │
                         ┌────────────────────────┼──────────────────┐
                         ▼                        ▼                  ▼
                    📧 Gmail          💬 titulares en el chat    🗂️ GitHub (informes/)
```

---

## 🚀 Guía paso a paso

### Paso 1 — Abrir el chat del agente
Entra a **https://claude.ai/code/session_0177XdtyLdurJP2rgXrtCv6J**. Ahí corre el informe cada mañana y ahí le haces preguntas.

### Paso 2 — Probarlo a mano
En el chat escribe `/noticias-ia` (o simplemente *"dame el informe de hoy"*). Verás cómo:
1. Lee la configuración (`config/temas.md`).
2. Llama al subagente **radar-ia**, que hace varias búsquedas web en paralelo y abre las fuentes oficiales.
3. Escribe el informe en `informes/AAAA-MM-DD.md` y te lo envía por Gmail.

### Paso 3 — Ver o cambiar la rutina
En **claude.ai/code → Routines** está `Radar IA — Informe matutino`. Ahí puedes pausarla, cambiar la hora o pulsar **Run now** para probarla.

> 💡 Cada ejecución consume uso de tu plan de Claude (una vez al día).

### Paso 4 — Personalizarlo
Todo lo que el agente vigila está en **[`config/temas.md`](config/temas.md)**: empresas, correo, reglas de calidad y secciones. El formato del informe está en [`plantillas/informe.md`](plantillas/informe.md). También puedes pedírselo en el chat.

### Paso 5 — Llevar los cambios a `main` (opcional)
El agente está en la rama `claude/ai-news-agent-rxr2xx`. Cuando quieras, abre un Pull Request hacia `main` en GitHub (o pídele al agente *"crea el PR"*) y haz Merge. La rutina usa `main` en cuanto contenga el agente.

---

## 🗂️ Estructura del proyecto

```
News/
├── CLAUDE.md                        # Instrucciones generales para Claude
├── README.md                        # Esta guía
├── config/
│   └── temas.md                     # ⚙️ Qué vigilar, correo, enlace al chat, reglas
├── .claude/
│   ├── agents/radar-ia.md           # 🔎 Subagente investigador
│   └── skills/noticias-ia/SKILL.md  # ☀️ /noticias-ia (informe matutino)
├── plantillas/informe.md            # 📝 Formato del informe
├── informes/                        # 📰 Un archivo por informe
├── estado/ultimas-noticias.json     # 🧠 Memoria: lo ya reportado (evita repetir)
└── rutinas/prompt-matutino.md       # Prompt de la rutina diaria
```

---

## ❓ Problemas frecuentes

| Problema | Solución |
|---|---|
| No me llega el correo | Abre el chat del agente y mira el último mensaje: ahí dice si algo falló. Revisa que Gmail siga conectado en claude.ai/customize/connectors. |
| Algunas webs no se pueden abrir (ej. openai.com) | El agente usa la búsqueda web y fuentes secundarias, y marca la noticia como "(sin confirmar)". |
| Una noticia se repite | El agente usa `estado/ultimas-noticias.json`; revisa que los commits de cada informe se estén guardando. |

---

## 📖 Para aprender más

- Documentación de Claude Code: https://code.claude.com/docs
- Subagentes: https://code.claude.com/docs/en/sub-agents
- Skills: https://code.claude.com/docs/en/skills
- Claude Code en la web y rutinas: https://code.claude.com/docs/en/claude-code-on-the-web
