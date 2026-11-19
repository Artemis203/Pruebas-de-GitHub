#  Guía Práctica: Git, GitHub CLI y GitHub Projects

Este repositorio es un laboratorio de aprendizaje para dominar los comandos esenciales de Git, la gestión de proyectos desde la terminal con `gh` y la configuración de tableros visuales (Backlog, Kanban, Priority Board y Roadmap) en GitHub Projects.

La filosofía es simple: **aprende haciendo**. Cada sección incluye comandos explicados y una **Tarea** para que pongas en práctica lo aprendido inmediatamente.

---

##  Parte 1: Comandos Esenciales de Git

Estos son los comandos que usarás a diario. Practícalos en tu terminal local.

### 1.1. Repositorios, Inicialización y Estado

Antes de hacer commits necesitas un **repositorio** (repo). Como ya tienes varios repos, es importante saber identificarlos, clonarlos y gestionar sus remotos sin confundirte entre ellos.

#### Trabajar con varios repositorios

| Comando | ¿Qué hace? |
| :--- | :--- |
| `git init` | Crea un nuevo repositorio Git en el directorio actual. |
| `git clone <url>` | Descarga (clona) un repositorio remoto a tu máquina local. |
| `gh repo list` | Lista todos tus repositorios en GitHub (usa `--limit 100` para ver más). |
| `gh repo view <owner>/<repo>` | Muestra información del repo (usa `--web` para abrirlo en el navegador). |
| `gh repo create <nombre>` | Crea un nuevo repositorio en GitHub desde la terminal. |
| `git remote -v` | Lista los remotos configurados en el repo actual (útil para saber **a qué repo estás apuntando**). |
| `git remote add <alias> <url>` | Añade un nuevo remoto (por ejemplo, `origin` o `upstream`). |
| `git remote set-url <alias> <url>` | Cambia la URL de un remoto existente. |
| `git remote remove <alias>` | Elimina un remoto. |

>  **Tip para varios repos:** Cuando tengas muchos repos clonados, usa `cd <carpeta>` para moverte entre ellos y **siempre** ejecuta `git remote -v` y `git status` al entrar, para confirmar en cuál estás trabajando y a qué remoto apunta.

#### Estado y commits

| Comando | ¿Qué hace? |
| :--- | :--- |
| `git status` | Muestra el estado de los archivos (modificados, en staging, sin seguimiento). |
| `git add <archivo>` | Mueve los cambios de un archivo al área de preparación (staging). |
| `git commit -m "mensaje"` | Guarda permanentemente los cambios que están en staging en el historial. |

**🔬 Tarea 1: Repositorios y tu primer commit**

1. **Lista tus repos existentes** para ubicarte: ejecuta `gh repo list` y localiza uno de tus repos.
2. **Clona uno** de tus repos (o crea uno nuevo vacío con `gh repo create mi-repo-practica --public --clone`). Si clonas: `git clone <url>`.
3. **Entra a la carpeta** del repo: `cd <nombre-del-repo>`.
4. **Verifica el remoto** con `git remote -v` para confirmar que apunta al repo correcto (importante si tienes varios).
5. **Inicializa un repo desde cero** en una carpeta nueva (opcional): crea una carpeta, entra y ejecuta `git init`.
6. Crea un archivo `README.md` con el texto `# Mi Proyecto`.
7. Usa `git status` para ver el archivo como "untracked" (sin seguimiento).
8. Añádelo con `git add README.md` y verifica el cambio de estado con `git status`.
9. Confirma el cambio con `git commit -m "docs: crear README inicial"`.
10. **Añade un segundo remoto** (por ejemplo, un fork o un repo espejo) con `git remote add upstream <url>` y compruébalo con `git remote -v`.

### 1.2. Ramas y Fusión (Branches & Merge)

| Comando | ¿Qué hace? |
| :--- | :--- |
| `git branch <nombre>` | Crea una nueva rama en el commit actual. |
| `git checkout <rama>` | Cambia de una rama a otra. |
| `git merge <rama>` | Fusiona los cambios de la rama especificada en la rama actual. |
| `git branch -d <rama>` | Elimina una rama (solo si ya fue fusionada). |

** Tarea 2: Flujo de trabajo con ramas**

1. Crea una rama llamada `feature-nueva` con `git branch feature-nueva`.
2. Cámbiate a ella con `git checkout feature-nueva`.
3. Crea un archivo `nueva-funcionalidad.txt` y haz un commit.
4. Vuelve a la rama principal (`main` o `master`) y verifica que el archivo no existe.
5. Fusiona los cambios con `git merge feature-nueva` y comprueba que el archivo ahora está presente.

### 1.3. Historial y Sincronización Remota

| Comando | ¿Qué hace? |
| :--- | :--- |
| `git log --oneline` | Muestra el historial de commits de forma resumida (una línea por commit). |
| `git remote add origin <url>` | Vincula tu repositorio local con un repositorio remoto (como GitHub). |
| `git push -u origin <rama>` | Sube los commits de tu rama local al repositorio remoto. |

** Tarea 3: Conectar con GitHub**

1. Crea un repositorio **vacío** en GitHub (sin README ni .gitignore).
2. En tu terminal, añade el remoto con `git remote add origin <tu-url-de-github>`.
3. Sube tu rama principal con `git push -u origin main` (o `master`).
4. Verifica en GitHub que tus archivos y commits están allí.

---

##  Parte 2: Gestión de Proyectos con GitHub CLI (`gh`)

El comando `gh project` te permite crear y gestionar proyectos (Projects v2) sin salir de la terminal. Todos los comandos requieren el parámetro `--owner` para especificar el usuario u organización.

### 2.1. Crear y Ver Proyectos

| Comando | ¿Qué hace? |
| :--- | :--- |
| `gh project list --owner @me` | Lista tus proyectos personales. |
| `gh project create --owner @me --title "Mi Proyecto"` | Crea un nuevo proyecto. |
| `gh project view <número> --owner @me` | Muestra los detalles de un proyecto (usa `--web` para abrirlo en el navegador). |

** Tarea 4: Crea tu primer tablero**

1. Autentica la CLI con el scope de proyectos: `gh auth refresh -s project`.
2. Crea un proyecto llamado `"Práctica Git"` con `gh project create --owner @me --title "Práctica Git"`.
3. Anota el número de proyecto que te devuelva (por ejemplo, `1`).
4. Ábrelo en el navegador con `gh project view 1 --owner @me --web`.

### 2.2. Añadir Elementos (Issues y PRs)

| Comando | ¿Qué hace? |
| :--- | :--- |
| `gh project item-add <nº-proyecto> --owner @me --url <url-issue>` | Añade un issue o Pull Request existente al proyecto. |
| `gh project item-create <nº-proyecto> --owner @me --title "Tarea"` | Crea un borrador (draft) de issue directamente en el proyecto. |
| `gh project item-list <nº-proyecto> --owner @me` | Lista los elementos del proyecto. |

** Tarea 5: Poblar el tablero**

1. En tu repositorio de GitHub, crea un Issue de prueba (puede ser tan simple como "Investigar comandos de Git").
2. Añádelo a tu proyecto con `gh project item-add 1 --owner @me --url https://github.com/tu-usuario/tu-repo/issues/1`.
3. Crea una tarea borrador adicional con `gh project item-create 1 --owner @me --title "Configurar Roadmap"`.

---

##  Parte 3: Configurando las Vistas de GitHub Projects (Backlog, Kanban, Priority, Roadmap)

Un mismo proyecto de GitHub puede visualizarse de diferentes formas. Aquí aprenderás a configurar cada vista y los campos personalizados que las alimentan.

### 3.1. Campos Personalizados (La Base de Todo)

Para que las vistas funcionen, primero necesitas definir campos estructurados. Los más comunes son:

| Campo | Tipo | Valores Sugeridos | Propósito |
| :--- | :--- | :--- | :--- |
| **Status** | Single Select | `Backlog`, `Ready`, `In Progress`, `In Review`, `Done` | Define la columna del Kanban y el estado del flujo. |
| **Priority** | Single Select | `P0 (Crítico)`, `P1 (Alto)`, `P2 (Medio)`, `P3 (Bajo)` | Permite priorizar y filtrar en el Priority Board. |
| **Size / Story Points** | Number o Select | `XS`, `S`, `M`, `L`, `XL` o `1, 2, 3, 5, 8` | Estima el esfuerzo para la planificación. |
| **Iteration / Sprint** | Iteration | Cadencia de 2 semanas (se autogenera) | Agrupa el trabajo para el Roadmap basado en sprints. |

**Crear un campo desde la CLI:**

```bash
# Crea el campo "Priority" con opciones P0, P1, P2, P3
gh project field-create 1 --owner @me --name "Priority" --data-type SINGLE_SELECT --single-select-options "P0,P1,P2,P3"
```

### 3.2. Vista de Backlog (La lista de ideas)

El **Backlog** es donde viven las ideas y tareas que aún no están listas para trabajarse. Suele ser una vista de **Tabla** (Table) filtrada para mostrar solo los elementos con estado `Backlog`.

**Configuración:**

1. Crea una nueva vista de tipo **Table**.
2. Asígnale el nombre `Backlog`.
3. Aplica un filtro: `status:Backlog` (o el nombre de tu campo de estado).
4. Ordena por `Priority` de forma descendente para ver primero lo más importante.

** Tarea 6:** Crea un issue nuevo y, usando la CLI, edita su campo `Status` para que sea `Backlog`:

```bash
# Primero obtén el ID del item y del campo con item-list y field-list
gh project item-list 1 --owner @me --format json
gh project field-list 1 --owner @me --format json

# Luego edita el valor (los IDs son numéricos y largos)
gh project item-edit --project-id <PROJECT_ID> --id <ITEM_ID> --field-id <FIELD_ID> --single-select-option-id <OPTION_ID>
```

### 3.3. Vista de Kanban (El flujo de trabajo visual)

La vista **Board** (Kanban) es el corazón del seguimiento diario. Las columnas representan el campo `Status`.

**Configuración Recomendada:**

- **Columnas:** `Backlog` → `Ready` → `In Progress` → `In Review` → `Blocked` → `Done`.
- **Agrupación:** Por el campo `Status`.
- **Ordenación:** Por `Priority` dentro de cada columna.

** Tarea 7:** En la interfaz web de tu proyecto, arrastra el issue que creaste en la Tarea 6 desde la columna **Backlog** a **In Progress**. Observa cómo el campo `Status` se actualiza automáticamente.

### 3.4. Vista de Priority Board (Enfoque en lo urgente)

Este es un tablero **filtrado** que muestra solo lo que es prioritario, ignorando el resto del ruido.

**Configuración:**

1. Crea una nueva vista de tipo **Board**.
2. Nómbrala `Priority Board`.
3. Aplica un filtro para mostrar solo prioridades altas: `priority:P0,P1`.
4. Agrupa por `Priority` (en lugar de por `Status`). Así tendrás columnas llamadas `P0` y `P1`.

**🔬 Tarea 8:** Edita un issue para que su `Priority` sea `P0`. Luego, abre la vista `Priority Board` y comprueba que el issue aparece en la columna correcta.

### 3.5. Vista de RoadMap (La línea de tiempo)

La vista **Roadmap** ofrece una perspectiva temporal para la planificación a medio y largo plazo.

**Configuración:**

- **Tipo de vista:** Roadmap.
- **Agrupación (Group by):** `Milestone` (Hito) o `Iteration` (Sprint).
- **Fechas:** Puedes usar el campo `Iteration` (que tiene fechas de inicio y fin) o crear un campo de tipo `Date` llamado `Target Date` y usarlo como eje temporal.

** Tarea 9:** Crea un **Milestone** en tu repositorio llamado `v1.0`. Asigna un issue a ese Milestone. Luego, en la vista Roadmap, agrupa por `Milestone` y verás cómo el issue aparece en la línea de tiempo correspondiente al hito.

---

##  Proyecto Final de Práctica

Para consolidar todo lo aprendido, realiza este pequeño proyecto:

1. **Crea un repositorio** en GitHub y clónalo localmente.
2. **Crea un proyecto** con `gh project create --owner @me --title "Mi Flujo de Trabajo"`.
3. **Define los campos** `Status` (con los valores del Kanban) y `Priority` (P0-P3) usando la CLI o la interfaz web.
4. **Crea 3 Issues** con diferentes prioridades y descripciones.
5. **Añádelos al proyecto** con `gh project item-add`.
6. **Configura las 4 vistas** en el proyecto: `Backlog` (Tabla filtrada), `Kanban` (Board por Status), `Priority Board` (Board filtrado por P0/P1) y `Roadmap` (por Milestone o Iteration).
7. **Mueve un issue** de `Backlog` a `Done` y observa cómo se refleja en cada vista.

---

##  Recursos Adicionales

- **Documentación oficial de GitHub CLI para Projects:** `gh project --help` o la [referencia oficial](https://cli.github.com/manual/gh_project).
- **Git Book (en español):** La referencia definitiva para Git.
- **GitHub Skills:** Cursos interactivos gratuitos de GitHub.

---

