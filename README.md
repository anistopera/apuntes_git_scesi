# Trabajo Individual - Nicole Marisol Flores Choquetopa
## Clase 1
### ¿Qué es GIT?
Es un Sistema de Control de Versiones Distribuido (VCS) creado por Linus Torvalds. Nos permite guardar archivos y sus versiones a lo largo del tiempo de manera local.
### Historia y Origen de GIT

- Fue creado por Linus Torvalds, el mismo creador del kernel de Linux.
- Antes, los desarrolladores de Linux mandaban sus contribuciones de código mediante correos electrónicos, lo cual era un proceso muy tedioso.
- Pasaron a usar un sistema llamado **BitKeeper**, el cual tenía una regla estricta: "No usarás ni tu ni tus colaboradores otro ademas de mi".
- Alguien de la comunidad rompió esa regla , y BitKeeper les quitó el acceso.
- Linus Torvalds, muy enojado ("Bueno lo hare yo mismo"), se encerró a programar y creó Git en apenas 2 a 3 semanas.
### Comandos Básicos
- `git config --global user.name "Tu Nombre"`
- `git config --global user.email "tu@correo.com"`
- Saltos de línea (Especialmente importante en Windows para evitar errores con usuarios de Linux/Mac): `git config --global core.autocrlf true`.

-Para ver tus configuraciones guardadas: `git config --global --list`

### Archivos Clave en un Repositorio

Todo repositorio debería tener al menos dos archivos:

- `README.md`: Es el archivo de presentación, el manual de usuario o la explicación de qué hace tu repositorio. Usa el formato *Markdown*.
- `.gitignore`: Sirve para ignorar archivos sensibles o basura que no quieres subir a tu historial.

---

## Clase 2
### Los 3 Estados de Git
1. Directorio de Trabajo (Working Directory)
Es tu carpeta normal. Aquí es donde tú programas, creas archivos o editas tu README.md.

Estado de los archivos: Aquí viven los archivos Untracked (nuevos) y los Modified (los que cambiaste pero aún no preparaste).

2. Área de Preparación (Staging Area)
Es como una sala de espera o una caja abierta donde vas metiendo exactamente lo que quieres guardar en tu próxima versión.

El comando: Al usar git add ., tomas los archivos del Directorio de Trabajo y los metes a esta caja.

Estado de los archivos: Pasan a estar Staged (preparados).

3. Repositorio Local (.git directory)
Es el historial permanente de tu proyecto en tu propia computadora. Es como sellar la caja de la sala de espera y ponerle una etiqueta con la fecha y la descripción.

El comando: Al usar git commit, tomas todo lo que estaba en el Área de Preparación y lo guardas en tu historial.

Estado de los archivos: Pasan a estar Committed (confirmados/guardados).
### Comandos Clave de la Sesión

- `git status`: Te muestra en qué estado están tus archivos (si están untracked, modified o staged).
- `git add <archivo>` o `git add .`: Pasa los archivos al Staging Area.
- `git restore <archivo>`: **Peligro.** Borra físicamente los cambios que hiciste en tu directorio de trabajo y devuelve el archivo a su estado original.
- `git restore --staged <archivo>`: Quita un archivo del Staging Area y lo devuelve al directorio de trabajo (sin borrar tus modificaciones).
- `git commit -m "mensaje"`: Crea el punto de guardado oficial.
- `git commit --amend`: Te permite editar el mensaje del último commit si te equivocaste.
- `git log` o `git log --oneline`: Muestra el historial de commits.

###  Buenas Prácticas
- (commit) representa un único cambio lógico, pequeño y completo en el código fuente
- Usa verbos imperativo
#### Convención de Commits : 
    saber de memoria los prefijos para los commits.
    - `feat`: Nueva funcionalidad o característica.
    - `fix`: Arreglo de un bug.
    - `docs`: Cambios en la documentación (como tu `README.md`).
    - `refactor`: Cambios en el código que no añaden funcionalidades ni arreglan bugs (ej. cambiar nombres de variables).
    - `style`: Cambios de formato (espacios, comas) que no afectan el código.
    - `test`: Añadir o corregir pruebas.

---

## Clase 3
### Conexión Remota (SSH vs HTTPS)
Es mejor configurar SSH para no tener que ingresar credenciales cada vez que hacemos un `git push`.
### Comandos Remotos
- `git remote add origin <url>`: Vincula el repo local con el de GitHub.
- `git push origin main`: Sube los cambios al servidor.
### SSH vs HTTPS


- HTTPS: Si clonas o intentas subir código usando el enlace HTTPS, GitHub te pedirá tu usuario y contraseña (o un token) cada vez que hagas un push. El Auxi lo describió como algo muy molesto.


- SSH: Es la forma recomendada. Generas una "llave" en tu computadora y la guardas en GitHub. Así, tu computadora y GitHub se reconocen automáticamente de forma segura y no tienes que poner contraseñas nunca más


### Configurar tu Llave SSH

1. Generar la llave en la terminal: `ssh-keygen -t ed25519 -C "tu-correo@email.com"`. *Usar el mismo correo con el que te registraste en GitHub.*
2. Ver la llave para copiarla: `cat ~/.ssh/id_ed25519.pub`.
3. Pegarla en GitHub: Ve a *Settings > SSH and GPG Keys > New SSH Key*, ponle un nombre (ej. "Mi PC") y pégala.
4. Probar la conexión: `ssh -T git@github.com`. (Debes escribir "yes" cuando te pregunte, y te saldrá un mensaje de éxito).

### Conectar tu Repositorio Local con GitHub
Si ya tienes tu repositorio local (el de tus apuntes) y creaste uno vacío en GitHub, debes vincularlos con estos comandos:

- Vincular el origen: `git remote add origin git@github.com:TuUser/TuRepo.git`
- Asegurar que la rama se llame main: `git branch -M main`
- Subir tus commits a la nube: `git push -u origin main`

### Subir y Bajar Cambios

- Para enviar tus nuevos commits a la nube: `git push origin main`.
- Para descargar cambios si alguien más (o tú en otra PC) modificó el repositorio en la nube: `git pull origin main`.

### comentarios
- Solución a error HTTPS: Si clonaste un repo por error con HTTPS y te pide contraseña, puedes cambiarlo a SSH usando: git remote set-url origin "git@github.com:TuUser/TuRepo.git".
- Límite de tamaño: El peso máximo de un archivo que puedes subir en un commit a GitHub es de 100 MB. Si intentas subir algo más pesado (como carpetas de node_modules o bases de datos), GitHub lo rechazará. Por eso es vital usar el .gitignore.

---

## Clase 4

### 1. Gestión de Conexiones: Git Remote

Cuando trabajas con repositorios en la nube (como GitHub), necesitas decirle a tu Git local a dónde enviar o de dónde traer la información.

- **Ver conexiones:** `git remote -v` te permite ver las URLs exactas donde apunta tu repositorio.
- **Vincular:** `git remote add <apodo> "url"` vincula tu repositorio local con uno en la nube. El apodo por defecto casi siempre es `origin`.
- **Cambiar conexión:** `git remote set-url <apodo> "url"` cambia la URL a la que apunta tu repositorio. El Auxi lo usó en clase para arreglar el error de haber clonado por HTTPS, cambiándolo a la ruta SSH.

### 2. Jerarquía de Configuraciones (Local vs Global)

Commits para cuentas diferentes en una misma computadora.

- Las configuraciones locales se imponen a las globales.
- Estas configuraciones locales solo funcionan para el repositorio específico en el que se aplican.
- Para hacer configuraciones locales, simplemente ejecutas los comandos dentro de la carpeta de tu repositorio sin usar la bandera `-global` (Ejemplo: `git config user.name "Mi nuevo Name"`).

### 3. Múltiples Cuentas SSH

Si tienes más de una cuenta de GitHub (ej. personal y otra del trabajo/universidad), necesitas generar un "túnel" independiente para que las llaves no choquen.

- **Paso 1:** Generar la llave con un nombre diferente usando el comando `ssh-keygen -t ed25519 -C "micorreo@gmail.com" -f ~/.ssh/id_miname`. El parámetro `f` especifica el nombre del archivo para no sobreescribir tu llave principal.
- **Paso 2:** Crear un archivo llamado `config` en la carpeta `~/.ssh/` para administrar qué llave usar. Dentro debes definir estos bloques:
    - **Host:** Es el apodo o alias que le pones a la conexión (lo que escribirás después de `git@`).
    - **HostName:** Es la dirección real del servidor, que para GitHub siempre será `github.com`.
    - **User:** El nombre del usuario remoto, siempre debe ser `git`.
    - **IdentityFile:** Es la ruta exacta hacia la llave privada que quieres usar para ese Host.
- **Paso 3:** Verificar la conexión ejecutando `ssh -T git@<tu_nuevo_host>`.
- **Importante:** Cuando clones un repositorio para esta segunda cuenta, no puedes usar la URL normal. Debes cambiarla en la terminal por tu nuevo Host: `git clone git@<tu_nuevo_host>:usuario/repo.git`.

### 4. Git Checkout y el Estado "Detached HEAD"

El comando `git checkout` permite desplazar el HEAD (tu "lector" actual) hacia un punto específico de la historia o a una rama distinta. Sirve para inspeccionar código antiguo, restaurar archivos borrados o experimentar.

- **Viajar al pasado:** Usas `git checkout <hash_antiguo>` (el hash es el código del commit).
- **Detached HEAD (Cabeza Desacoplada):** Al viajar a un commit específico, entras en este estado. Significa que el HEAD apunta directamente a un Commit fijo, no a una Rama.
    - Eres solo un espectador en el pasado.
    - Si haces cambios aquí y te vas al presente sin "encarnar" en una rama, tus cambios se pierden en el vacío.
    - Si decides que quieres conservar los cambios experimentales que hiciste, debes ejecutar `git checkout -b rama_nueva`.
- **Volver al presente:** Ejecutas `git checkout <rama>` (ej. `git checkout main`).
- **Buenas prácticas:** Antes de viajar al pasado, debes limpiar tu directorio de trabajo asegurándote de haber hecho commit de tus cambios actuales; de lo contrario, Git no te dejará viajar.

---
## Clase 5

### 1.Conceptos Técnicos: Ramas (Branches)

Las ramas son bifurcaciones del estado del código que crean un nuevo camino paralelo. Permiten a varias personas trabajar al mismo tiempo sin arruinar el código principal original.

**Comandos de Ramas que debes saber para el examen:**

- `git branch`: Lista las ramas disponibles y muestra en cuál está el HEAD (tu ubicación actual).
- `git branch <rama>`: Crea una nueva rama a partir de la rama en la que estás posicionado.
- `git checkout <rama>` o `git switch <rama>`: Te cambia a la rama especificada (tu directorio de trabajo debe estar limpio sin cambios sin guardar).
- `git checkout -b <rama>`: Crea la rama y te mueve a ella directamente en un solo paso.
- `git branch -D <rama>`: Borra la rama especificada.

---

### 2. GitFlow Básico (El estándar de la SCESI)

GitFlow es un marco de trabajo que establece reglas para usar las ramas de manera ordenada. El Auxi hizo mucho énfasis en que evalúa que usen esta estructura en sus proyectos:

**Ramas Principales:**

- `main` (o master): Es sagrada. Su propósito es contener el código que se encuentra en producción. Aquí solo va el código estable y final. Jamás muere.
- `develop`: Es la rama de "pre-producción". Aquí se integran las nuevas características que funcionarán en el futuro. Es el entorno del día a día del equipo. Jamás muere.

**Ramas de Apoyo:**

- `feature/*`: Se usa para trabajar en una nueva característica (ej. `feature/sum-function`).
    - **Regla:** Nacen de `develop`, y cuando se terminan, se fusionan de vuelta en `develop` y se eliminan. Jamás uses espacios en los nombres, usa guiones o barras bajas.
- `release/*`: Se usa cuando preparas el lanzamiento de una nueva versión (fase de pruebas o QA). Nacen de `develop` y mueren en `main` y `develop`.
- `hotfix/*`: Se usa para arreglar un error crítico o "incendio" directamente en producción. Nacen directo de `main` y, al arreglar el bug, mueren fusionándose en `main` y en `develop`.

## clase 6

### Fetch vs. Pull

**SIEMPRE** se deben ejecutar estos comandos antes de subir o fusionar cambios:

- `git fetch`: Es como el "vecino chismoso". Va al servidor remoto (GitHub) y revisa si alguien más subió cambios a la rama (ej. `develop`). **No descarga los cambios**, solo te informa si el servidor está más adelantado que tu código local.
- `git pull origin <rama>`: Este comando **sí descarga e integra** los cambios del repositorio remoto a tu computadora.
- **Regla de Oro:** Si vas a integrar tu trabajo, siempre haz `git fetch` seguido de `git pull origin develop` para no generar conflictos catastróficos con el trabajo de tus compañeros.

### Git Merge y el "No Fast Forward"

- `git merge --no-ff <rama>`: El comando `-no-ff` (No Fast Forward) fuerza a Git a crear un *commit* de fusión.
- **¿Por qué es obligatorio usarlo?** Si no lo usas, Git "aplana" el historial (Fast Forward) y hace parecer que tu rama secundaria nunca existió. Usar `-no-ff` mantiene la "burbuja" visual en el gráfico (`git log --graph`), lo cual es vital para la auditoría y para que el Auxi vea que realmente creaste y trabajaste en una rama separada.
- **Limpieza:** Después de hacer el merge exitosamente, siempre debes eliminar la rama local con `git branch -D <rama>` (Min 18:33).

### Jerarquía de Configuraciones: Local vs. Global

- **Configuración Global** (`git config --global user.name`): Se aplica a todos los repositorios de tu computadora.
- **Configuración Local** (`git config user.name` sin `-global`): Se aplica **únicamente** al repositorio en el que estás trabajando.
- **Pregunta de Examen:** **La configuración Local siempre tiene prioridad sobre la Global.** Si configuras un usuario localmente, Git ignorará el global para esa carpeta. Es útil cuando tienes una cuenta del trabajo y una personal en la misma PC.

---

### Resolución de Conflictos

Un conflicto ocurre cuando dos personas modifican las mismas líneas exactas de un archivo y Git no sabe cuál versión conservar.

**¿Cómo identificar y solucionar el conflicto?**

1. Git marcará el archivo con error y pondrá símbolos extraños en tu código:
    - `<<<<<<< HEAD`: Indica el inicio del código que tú tienes actualmente.
    - `=======`: Es el separador. Divide tu código del código que viene de la otra rama.
    - `>>>>>>> <nombre_de_la_rama>`: Indica el fin del código entrante.
2. **Solución Manual:** Debes abrir el archivo, leer ambas partes y borrar manualmente el código que no sirve, junto con los símbolos de Git (`<<<`, `===`, `>>>`).
3. **Finalizar el Merge:** Una vez que el archivo esté limpio y guardado, ejecutas `git add <archivo>` y luego `git commit` (sin `m`) para que Git genere automáticamente el mensaje de resolución de conflicto (Min 32:50).

---

### La "Buena Práctica" Suprema para Mergear

Truco de la industria para no arruinar la rama principal (`develop`) al fusionar:

1. **NO fusiones directamente en `develop`:** Si tu rama (`feature`) es muy antigua, fusionarla en `develop` puede causar errores en código que tú ni siquiera tocaste.
2. **El método seguro:**
    - Estando en tu rama (`feature`), trae los cambios recientes: `git fetch` y `git pull origin develop`.
    - Haz el merge de `develop` **HACIA** tu rama: `git merge develop`.
    - Si hay conflictos, los resuelves ahí mismo, dentro de tu rama (donde si algo explota, solo te afecta a ti).
    - Una vez que tu rama funciona perfectamente con los cambios nuevos integrados, cambias a develop (`git switch develop`) y haces el merge definitivo: `git merge --no-ff <tu_rama>`.

---
## Clase 7

### Flujo de Trabajo en Equipo

Cómo fusionar el trabajo de varios integrantes si no tienen configuradas restricciones en GitHub.

**El Flujo Completo (Paso a Paso):**

1. **Actualizar todo antes de empezar:**`git checkout developgit fetch` (Busca si hay cambios en el servidor)`git pull origin develop` (Descarga los cambios)
2. **Crear o ir a tu rama de trabajo:**`git switch -c feature/tu-rama` (o `git checkout -b feature/tu-rama`)
3. **Trabajar y asegurar cambios:**
    
    `git add .`
    
    `git commit -m "feat: add user authentication"`
    
4. **La "Buena Práctica" Suprema antes del Merge:**
Como pudiste tardar varios días, es posible que alguien más haya modificado `develop` mientras tanto. Para evitar dolores de cabeza y resolver conflictos en *tu* rama y no en la principal:
    - Cambias a develop: `git checkout develop`
    - Actualizas: `git fetch` y `git pull origin develop`
    - Vuelves a tu rama: `git checkout feature/tu-rama`
    - **Traes develop hacia ti:** `git merge develop` (Aquí resuelves conflictos si los hay)
5. **El Merge Final (Seguro):**
    - Ya que tu rama está actualizada y sin conflictos, cambias a `develop`: `git switch develop`
    - Fusionas manteniendo el historial: `git merge --no-ff feature/tu-rama`
    - Empujas a la nube: `git push origin develop`
6. **Limpieza:** Eliminas tu rama local: `git branch -D feature/tu-rama`.

---

### Resolución de Conflictos (A Manito)

Un conflicto surge cuando dos personas han modificado las mismas líneas exactas de un mismo archivo en ramas distintas. Git pausa la fusión y marca el archivo para que el humano lo revise.

**¿Cómo se ve un conflicto en el código?**

HTML

`<<<<<<< HEAD (Tu código actual)
<header><h1>Autores de la Web</h1></header>
======= (Separador)
<header><h1>Nuestros Creadores</h1></header>
>>>>>>> feature/otra-rama (Código entrante que causa conflicto)`

**Pasos para resolverlo:**

1. Abres el archivo en tu editor de código o terminal (`nano`).
2. Borras manualmente los símbolos extraños (`<<<<<<< HEAD`, `=======`, `>>>>>>>`).
3. Decides qué código borrar, qué código mantener o cómo combinar ambas partes.
4. Guardas el archivo y le dices a Git que ya está resuelto: `git add <archivo>`.
5. Finalizas ejecutando `git commit` sin mensaje (Git abrirá el editor para que guardes el mensaje de merge automático).

---

### 4. Flujo de Trabajo Profesional: Los Pull Requests (PRs)

Los PRs son la forma profesional de trabajar con Git/GitHub. Crean una solicitud formal en GitHub para unir el código de tu rama (`feature`) a la rama base (`develop`), permitiendo que tus compañeros vean qué quieres fusionar antes de aceptarlo.

**¿Por qué usar Pull Requests? (Pregunta de Examen)**
Se usan por temas de seguridad. Limitan la colaboración, obligan al debate/deliberación y evitan que cualquier persona pueda subir código malicioso o inestable directamente a la rama principal sin que el resto del equipo lo revise y lo apruebe.

### ¿Cómo configurar GitHub para requerir PRs? (Protección de Ramas)

El administrador del repositorio debe hacer lo siguiente para bloquear fusiones directas:

1. Ir a **Settings > Branches** y añadir un *Rule Set*.
2. En **Target Branch**, incluir las ramas a proteger (ej. `~default` y `develop`).
3. Activar la opción: **Require a pull request before merging**.
4. Configurar la cantidad de aprobaciones necesarias (ej. requerir la aprobación de 3 miembros de un equipo de 4).

### ¿Cómo crear un Pull Request? (Paso a Paso)

1. Has terminado tu trabajo y subes tu rama a GitHub: `git push -u origin feature/tu-rama`.
2. Entras a la página de tu repositorio en `github.com`.
3. Te aparecerá un botón verde que dice **"Compare & pull request"**. Si no sale, ve a la pestaña *Pull requests* y dale a *New pull request*.
4. Configuras las ramas: **base:** `develop` (a dónde quieres fusionar) `<--` **compare:** `feature/tu-rama` (de dónde viene tu código).
5. Escribes un título descriptivo y un comentario explicando detalladamente qué cambios hiciste.
6. Le das a **Create pull request**.

---
Notas con apoyo de gemini , basicamente le di los comandos usados en clase y los apuntes y me ayudo a estructurarlo