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
