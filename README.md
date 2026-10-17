# Claude Code CLI Agents

**Pasos de instalación en Windows**
1. Clonar el repositorio.
    ```
    git clone git@github.com:SoyTrunix/Claude-Code.git
    ```
3. Ir a la carpeta global de Claude Code: **C:\\users\\tu_usuario\\.claude**
4. Mover los agentes, skills y settings del repositorio clonado a la carpeta global de Claude (recuerda remplazar o sobreescribir tus cambios por estos nuevos).
5. Instalar Graphify a traves de python v3.10+ (opcional si quieres usar la Skill Graphify)

   Instalar Python y Graphify:
    ```bash
    winget install Python.Python.3.14
    pip install graphifyy && graphify install
    ```
Graphify es una herramienta en la que sirve para "remplazar" la exploración masiva de archivos en los proyectos, generando gastos innecesario de tokens.

<br>

**Pasos de instalación en Linux (Debian/Ubuntu)**
1. Clonar el repositorio.
    ```
    git clone git@github.com:SoyTrunix/Claude-Code.git
    ```
3. Ir a la carpeta global de Claude Code: **~/.claude/** o **/home/tu_usuario/.claude**
4. Mover los agentes, skills y settings del repositorio clonado a la carpeta global de Claude.
5. Instalar Graphify a traves de python v3.10+ y UV (opcional si quieres usar la Skill Graphify):
   
    Instalar Python:
    ```bash
    sudo add-apt-repository ppa:deadsnakes/ppa
    sudo apt update
    sudo apt install python3.14 python3.14-venv
    ```
    Instalar Graphify:
    ```bash
    curl -LsSf https://astral.sh/uv/install.sh | sh
    uv tool install graphifyy
    ```

<br>

## Agentes disponibles

Cada agente vive como un archivo en `agents/<nombre>.md`. Se invocan desde el agente principal
(`build`/`plan`) vía la herramienta `Agent`, o directamente con `@<nombre>` según el flujo de Claude Code.

### Orquestadores

<details>
<summary><strong>Build</strong> — Orquestador principal</summary>

Agente principal orquestador de Claude Code: no hace el trabajo de
detalle inline, dirige todo delegando SIEMPRE a subagentes especializados vía la herramienta `Agent`
(graphify, architect, fullstack-dev, code-reviewer, etc.), integra y verifica sus resultados.
</details>

<details>
<summary><strong>Plan</strong> — Orquestador read-only (modo Plan)</summary>

Orquestador read-only que delega SIEMPRE la investigación y el
análisis a subagentes read-only (graphify, deep-web-search, security-auditor,
web-performance-auditor, architect) y entrega un plan, sin editar código.
</details>

### Reconocimiento / investigación (solo lectura)

<details>
<summary><strong>graphify</strong> — Exploración del codebase vía knowledge graph</summary>

ÚNICO agente de reconocimiento/exploración del codebase (reemplaza por completo a `explore`). Consulta
el knowledge graph de Graphify (`graphify-out/`) para arquitectura, relaciones, flujos de datos y
contenido sin búsquedas manuales de archivos; si el grafo no existe, lo construye él mismo.
</details>

<details>
<summary><strong>deep-web-search</strong> — Investigación web profunda</summary>

Investigación web profunda y solo lectura: múltiples búsquedas iterativas, cruce de fuentes,
documentación oficial, changelogs, issues de GitHub y CVEs recientes. Útil para validar librerías/APIs
o verificar vigencia antes de implementar algo. No modifica archivos.
</details>

<details>
<summary><strong>security-auditor</strong> — Auditoría de seguridad</summary>

Auditor de seguridad y revisor de código de solo lectura: detecta vulnerabilidades (OWASP Top 10),
secretos expuestos, CVEs en dependencias y malas prácticas de auth/authz. Entrega un reporte priorizado,
no modifica archivos.
</details>

<details>
<summary><strong>web-performance-auditor</strong> — Auditoría de performance web</summary>

Ingeniero de performance web enfocado en Core Web Vitals, loading, rendering y optimización de red.
Identifica anti-patrones estructurales de performance. No edita.
</details>

### Implementación por dominio

<details>
<summary><strong>architect</strong> — Arquitectura de software</summary>

Arquitecto de software senior: diseña arquitecturas de sistemas, elige stack tecnológico, define
patrones de diseño, estrategia de datos y evalúa trade-offs de escalabilidad, costo y mantenibilidad.
Úsalo antes de features grandes o refactors estructurales. No edita código directamente.
</details>

<details>
<summary><strong>fullstack-dev</strong> — Desarrollo full-stack multi-lenguaje</summary>

Experto full-stack en React, Vue, Angular, Svelte, Next.js, Nuxt, Remix, Node/Express/NestJS, Python
(Django, FastAPI, Flask), Go, Rust, Java/Spring Boot, .NET/C#, PHP/Laravel, Rails, GraphQL y APIs REST.
El agente por defecto cuando no se especifica tecnología.
</details>

<details>
<summary><strong>android-dev</strong> — Desarrollo Android / multiplataforma</summary>

Apps Android nativas (Kotlin, Jetpack Compose, Views/XML, MVVM/MVI/Clean Architecture, Coroutines/Flow,
Room, Hilt/Koin, Retrofit, WorkManager, Gradle) y multiplataforma (KMP, Flutter, React Native).
</details>

<details>
<summary><strong>web-design</strong> — UI/UX y frontend visual</summary>

Diseñador/desarrollador frontend experto en UI/UX, diseño responsive, sistemas de diseño, tipografía,
color, accesibilidad WCAG, HTML/CSS moderno, Tailwind y animaciones. Para landing pages y componentes
visuales.
</details>

<details>
<summary><strong>devops-deploy</strong> — CI/CD e infraestructura</summary>

Ingeniero DevOps/SRE: CI/CD (GitHub Actions, GitLab CI, Jenkins), Docker, Kubernetes, Terraform/Pulumi,
despliegue en AWS/GCP/Azure/Vercel/Netlify/Railway, monitoreo (Prometheus/Grafana/Sentry) y gestión de
secretos.
</details>

<details>
<summary><strong>code-optimizer</strong> — Reducción y optimización de código</summary>

Elimina redundancias, duplicación (DRY), código muerto y complejidad innecesaria, y mejora el
rendimiento SIN romper funcionalidad existente. Verifica con tests/build que todo siga funcionando.
</details>

<details>
<summary><strong>cache-cleaner</strong> — Limpieza de caché y temporales</summary>

Analiza el sistema (du/df/ncdu), detecta y limpia cachés de paquetes (npm/pip/apt/cargo/gradle/maven),
cachés de apps y basura de builds de forma segura, sin borrar datos de usuario, y reporta el espacio
liberado.
</details>

### Calidad y cierre

<details>
<summary><strong>test-engineer</strong> — Estrategia y escritura de tests</summary>

Ingeniero de QA especializado en diseño de suites de tests, escritura de tests para código existente y
análisis de cobertura.
</details>

<details>
<summary><strong>code-reviewer</strong> — Revisión de código antes de merge</summary>

Revisor senior que evalúa cambios en cinco dimensiones: corrección, legibilidad, arquitectura, seguridad
y performance. Entrega veredicto y hallazgos categorizados (Crítico/Importante/Sugerencia). No edita.
</details>

<details>
<summary><strong>pr-summary</strong> — Resumen final para Pull Request</summary>

Genera el resumen final de una feature o cambio terminado, listo para copiar y pegar como descripción de
Pull Request (qué se hizo, archivos tocados, tests, pendientes). Se usa al cerrar una tarea, antes de
subir a GitHub. Solo lectura (`git log`/`git diff`/`git status`), nunca commitea ni pushea.
</details>

<details>
<summary><strong>general</strong> — Fallback para research/trabajo paralelo</summary>

Research multi-paso y unidades de trabajo paralelas (puede editar archivos). Se usa como fallback cuando
ningún especialista del catálogo aplica.
</details>

<br>

## Cómo se crean los agentes (estructura y cómo correrlos en Claude Code)

Un agente de Claude Code es un archivo Markdown en `agents/<nombre-del-agente>.md`. El **nombre del
archivo** (sin `.md`) es el identificador que usás para invocarlo.

### Estructura de un agente

```markdown
---
name: mi-agente
description: >-
  Descripción concisa de qué hace y CUÁNDO usarlo. Esto es lo que lee el
  orquestador (build/plan) para decidir si te delega una tarea, así que debe
  ser específica y mencionar los casos de uso típicos.
tools: Read, Write, Edit, MultiEdit, NotebookEdit, Glob, Grep, Bash, PowerShell, WebFetch, WebSearch, TodoWrite, Skill, ToolSearch, LSP
disallowedTools: Write, Edit, MultiEdit, NotebookEdit
---

# Título del agente

Cuerpo en markdown: acá va el system prompt completo del agente. Definí su
rol, áreas de dominio, cómo debe trabajar paso a paso, formato de salida
esperado, y reglas/restricciones. Entre más específico, más consistente el
resultado.
```

**Campos del frontmatter:**

| Campo | Obligatorio | Qué hace |
|---|---|---|
| `name` | Sí | Identificador del agente (debe matchear el nombre del archivo). |
| `description` | Sí | Usado por el orquestador para decidir cuándo delegarle trabajo. Debe incluir disparadores/casos de uso explícitos. |
| `tools` | No | Lista de herramientas permitidas. Si se omite, hereda todas las disponibles. |
| `disallowedTools` | No | Lista de herramientas explícitamente prohibidas (ej. agentes read-only bloquean `Write, Edit, MultiEdit, NotebookEdit`). |

El cuerpo markdown (todo lo que va después del segundo `---`) es el **system prompt** del agente: ahí se
define su personalidad, metodología de trabajo, formato de entrega y reglas. Mirá cualquier archivo en
`agents/` como referencia de estilo y nivel de detalle.

### Cómo correrlo dentro de Claude Code

1. **Guardá el archivo** en `~/.claude/agents/<nombre>.md` (global, disponible en todos los proyectos) o
   en `<proyecto>/.claude/agents/<nombre>.md` (solo para ese proyecto).
2. **No hace falta reiniciar nada**: Claude Code lee la carpeta `agents/` al resolver qué subagentes
   existen.
3. **Invocarlo**:
   - **Automáticamente**: si estás usando un orquestador (`build`/`plan`), este decide delegarle la
     tarea en base al campo `description` — no necesitás nombrarlo vos.
   - **Explícitamente**: pedile a Claude "usá el agente `<nombre>` para..." o delegalo vos mismo con la
     herramienta `Agent` indicando `subagent_type: "<nombre>"`.
4. **Verificación rápida** de que el archivo está bien formado:
   ```bash
   # Debe listar tu agente nuevo
   ls ~/.claude/agents/
   ```
   Si el agente no aparece como opción al delegar, revisá que el frontmatter YAML esté bien cerrado
   (dos líneas `---`) y que `name` coincida con el nombre del archivo.
5. Si el agente es de solo lectura (research, auditoría, revisión), agregale `disallowedTools: Write,
   Edit, MultiEdit, NotebookEdit` para que Claude Code le bloquee la escritura a nivel de herramienta,
   no solo por instrucción en el prompt.
