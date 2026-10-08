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
