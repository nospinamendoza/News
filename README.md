# 🛰️ Radar IA — Tu agente de noticias de Inteligencia Artificial

Un agente construido con **Claude Code** que todos los días te cuenta, en español y en palabras simples:

- 🏢 Las novedades de **Anthropic (Claude)**, **OpenAI (ChatGPT)**, **Google (Gemini)**, **Microsoft (Copilot)** y otras IAs importantes (Meta, xAI/Grok, Mistral, DeepSeek…).
- 📅 **Cuándo** se anunció cada cosa y **cuándo** llega al público (y para quién: planes, países).
- 🧠 **Cómo funcionan** los nuevos features, con analogías cotidianas.
- 🛠️ **Aplicaciones reales**: empresas y apps que están usando la IA de forma nueva.
- 💡 **Ideas de negocio** que surgen de estas novedades.
- 📚 **Fuentes** de referencia para cada noticia.

Funciona de dos formas:

| Modo | Cuándo | Qué hace |
|---|---|---|
| ☀️ **Informe matutino** (`/noticias-ia`) | Todos los días a las 6:53 a. m. (hora Colombia) | Informe completo de las últimas 24 h → Gmail + Google Drive + GitHub |
| ⚡ **Alerta proactiva** (`/alerta-ia`) | 10:53 a. m., 2:53 p. m. y 6:53 p. m. | Solo si salió algo **muy importante** te manda un correo corto. Si no, no molesta. |

👉 Ejemplo real: [`informes/2026-10-08.md`](informes/2026-10-08.md) (primer informe generado).

---

## 📍 ¿Dónde veo el agente funcionando?

1. **Tu Gmail** (nicolasospinamen@gmail.com) — llega el informe cada mañana con asunto `🛰️ Radar IA — …` y las alertas con `⚡ Alerta IA: …`.
2. **Google Drive** → `Claude Agentes / Agente Noticias IA / Informes` — un Google Doc por día.
   [Abrir carpeta](https://drive.google.com/drive/folders/1ngeqjITnZCOBMQ0TZgqnNLq96IscJqCe)
3. **GitHub** → carpeta [`informes/`](informes/) de este repositorio — historial completo en Markdown.
4. **claude.ai/code → Routines** (Rutinas) — ves cada ejecución, cuándo corrió y qué hizo; puedes abrir la sesión y conversar con el agente sobre el informe.

---

## 🧩 Conceptos en 1 minuto (tu primer agente)

| Concepto | Qué es | En este proyecto |
|---|---|---|
| **Claude Code** | Claude trabajando como "programador/asistente" que puede leer archivos, buscar en internet y usar herramientas. | El motor de todo. |
| **CLAUDE.md** | Las "instrucciones de la casa": Claude lo lee siempre al abrir el proyecto. | [`CLAUDE.md`](CLAUDE.md) |
| **Subagente** | Un Claude especialista con su propio rol y herramientas, al que el agente principal le delega trabajo. | [`.claude/agents/radar-ia.md`](.claude/agents/radar-ia.md) — el investigador. |
| **Skill** (habilidad) | Una "receta" guardada en un `SKILL.md`. Se invoca escribiendo `/nombre`. | `/noticias-ia` y `/alerta-ia` en [`.claude/skills/`](.claude/skills/) |
| **Conector** | Permiso para que Claude use tus apps (Gmail, Google Drive…). | Gmail para enviar, Drive para guardar. |
| **Rutina** (Routine) | Una tarea programada que corre sola en la nube, aunque tu computador esté apagado. | Informe matutino + alertas. |

```
 Rutina (6:53 a. m.)                  ┌───────────────────────────┐
 ───────────────────▶  /noticias-ia ─▶│ Subagente radar-ia        │
                        (skill)       │ busca + verifica en la web│
                           │          └─────────────┬─────────────┘
                           │◀───── hallazgos ───────┘
                           ▼
            redacta informe (plantillas/informe.md)
                           │
         ┌─────────────────┼─────────────────┐
         ▼                 ▼                 ▼
      📧 Gmail       📁 Google Drive     🗂️ GitHub (informes/)
```

---

## 🚀 Guía paso a paso

### Paso 1 — Abrir el proyecto en Claude Code

Tienes dos opciones; **la web es la más fácil** para empezar:

**Opción A · Web (recomendada)**
1. Entra a **https://claude.ai/code**.
2. Elige el repositorio `nospinamendoza/News` y empieza una sesión.
3. Claude leerá `CLAUDE.md` automáticamente y ya conoce el agente.

**Opción B · En tu computador (terminal)**
1. Instala Claude Code siguiendo la guía oficial: https://code.claude.com/docs/en/setup
2. Clona el repo y entra a la carpeta:
   ```bash
   git clone https://github.com/nospinamendoza/News.git
   cd News
   claude
   ```

### Paso 2 — Conectar Gmail y Google Drive

1. En **claude.ai → Settings (Configuración) → Connectors (Conectores)**.
2. Conecta **Gmail** y **Google Drive** con tu cuenta `nicolasospinamen@gmail.com`.
3. Sin esto el agente igual genera el informe en GitHub, pero no podrá enviarte el correo ni guardar en Drive.

### Paso 3 — Probarlo a mano

En una sesión de Claude Code dentro del proyecto escribe:

```
/noticias-ia
```

Verás cómo Claude:
1. Lee la configuración (`config/temas.md`).
2. Llama al subagente **radar-ia**, que hace varias búsquedas web en paralelo y abre las fuentes oficiales.
3. Escribe el informe en `informes/AAAA-MM-DD.md`.
4. Lo sube a Drive, te lo envía por Gmail y hace commit en GitHub.

Prueba también:
- `/alerta-ia` → chequeo rápido de las últimas horas.
- Preguntas libres: *"¿Qué cambió en Gemini esta semana?"*, *"Explícame como a un niño cómo funciona Claude Haiku 5.5"*, *"Dame 5 ideas de negocio con la nueva interfaz de GPT-6"*.

### Paso 4 — Programarlo para que corra solo (Rutinas)

Las rutinas ya quedaron creadas en tu cuenta durante la configuración:

| Rutina | Horario (America/Bogota) | Prompt |
|---|---|---|
| `Radar IA — Informe matutino` | Todos los días 6:53 a. m. | [`rutinas/prompt-matutino.md`](rutinas/prompt-matutino.md) |
| `Radar IA — Alertas proactivas` | Todos los días 10:53 a. m., 2:53 p. m., 6:53 p. m. | [`rutinas/prompt-alertas.md`](rutinas/prompt-alertas.md) |

Para verlas, pausarlas o cambiar el horario: **claude.ai/code → Routines**.

¿Quieres crear una tú mismo (para aprender)?
1. Ve a **claude.ai/code → Routines → New routine** (o escribe `/schedule` en Claude Code).
2. Elige este repositorio y el entorno.
3. Pega el contenido de `rutinas/prompt-matutino.md` como instrucción.
4. Elige el horario (ej. todos los días a las 7:00) y activa los conectores **Gmail** y **Google Drive**.
5. Guarda. Usa **Run now** para probarla sin esperar.

> 💡 Cada ejecución de una rutina consume uso de tu plan de Claude. Si quieres gastar menos, deja solo el informe matutino o reduce las alertas a 1-2 por día.

### Paso 5 — Personalizarlo

Todo lo que el agente vigila está en **[`config/temas.md`](config/temas.md)**. Puedes:
- Añadir o quitar empresas (ej. Apple, Amazon, Perplexity, Cursor).
- Cambiar el correo destino o la zona horaria.
- Cambiar las secciones del informe o las reglas de calidad.

El formato del informe está en [`plantillas/informe.md`](plantillas/informe.md). Edita y el próximo informe ya sale con los cambios. También puedes pedírselo a Claude: *"Agrega una sección de herramientas gratuitas al informe"*.

### Paso 6 — Llevar los cambios a `main`

Este agente se construyó en la rama `claude/ai-news-agent-rxr2xx`. Cuando lo hayas revisado:
1. En GitHub abre un **Pull Request** de esa rama hacia `main` (o pídele a Claude: *"crea el PR"*).
2. Haz **Merge**.
3. Desde ese momento las rutinas trabajan sobre `main`.

---

## 🗂️ Estructura del proyecto

```
News/
├── CLAUDE.md                        # Instrucciones generales para Claude
├── README.md                        # Esta guía
├── config/
│   └── temas.md                     # ⚙️ Qué vigilar, correo, IDs de Drive, reglas
├── .claude/
│   ├── agents/
│   │   └── radar-ia.md              # 🔎 Subagente investigador
│   └── skills/
│       ├── noticias-ia/SKILL.md     # ☀️ /noticias-ia  (informe completo)
│       └── alerta-ia/SKILL.md       # ⚡ /alerta-ia    (alerta de última hora)
├── plantillas/
│   └── informe.md                   # 📝 Formato del informe
├── informes/
│   └── 2026-10-08.md                # 📰 Un archivo por informe
├── estado/
│   └── ultimas-noticias.json        # 🧠 Memoria: lo ya reportado (evita repetir)
└── rutinas/
    ├── prompt-matutino.md           # Prompt de la rutina diaria
    └── prompt-alertas.md            # Prompt de la rutina de alertas
```

---

## ❓ Problemas frecuentes

| Problema | Solución |
|---|---|
| No me llega el correo | Revisa que el conector **Gmail** esté conectado y habilitado en la rutina. Mira el resultado de la ejecución en claude.ai/code → Routines. |
| No aparece el Doc en Drive | Revisa el conector **Google Drive** y que el ID de carpeta en `config/temas.md` sea correcto. |
| Algunas webs no se pueden abrir (ej. openai.com) | Algunos sitios bloquean el acceso automático. El agente usa la búsqueda web y fuentes secundarias, y marca la noticia como "(sin confirmar)". |
| Me llegan demasiadas alertas | Edita los criterios en `.claude/skills/alerta-ia/SKILL.md` o reduce los horarios de la rutina. |
| Una noticia se repite | El agente usa `estado/ultimas-noticias.json`; asegúrate de que los commits de cada ejecución se estén guardando (push). |

---

## 📖 Para aprender más

- Documentación de Claude Code: https://code.claude.com/docs
- Subagentes: https://code.claude.com/docs/en/sub-agents
- Skills: https://code.claude.com/docs/en/skills
- Claude Code en la web y rutinas: https://code.claude.com/docs/en/claude-code-on-the-web
