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

## Clase 3
### Conexión Remota (SSH vs HTTPS)
Es mejor configurar SSH para no tener que ingresar credenciales cada vez que hacemos un `git push`.
### Comandos Remotos
- `git remote add origin <url>`: Vincula el repo local con el de GitHub.
- `git push origin main`: Sube los cambios al servidor.
### SSH vs HTTPS


- HTTPS: Si clonas o intentas subir código usando el enlace HTTPS, GitHub te pedirá tu usuario y contraseña (o un token) cada vez que hagas un push. El Auxi lo describió como algo muy molesto.


- SSH: Es la forma recomendada. Generas una "llave" en tu computadora y la guardas en GitHub. Así, tu computadora y GitHub se reconocen automáticamente de forma segura y no tienes que poner contraseñas nunca más


## Configurar tu Llave SSH

1. Generar la llave en la terminal: `ssh-keygen -t ed25519 -C "tu-correo@email.com"`. *Usar el mismo correo con el que te registraste en GitHub.*
2. Ver la llave para copiarla: `cat ~/.ssh/id_ed25519.pub`.
3. Pegarla en GitHub: Ve a *Settings > SSH and GPG Keys > New SSH Key*, ponle un nombre (ej. "Mi PC") y pégala.
4. Probar la conexión: `ssh -T git@github.com`. (Debes escribir "yes" cuando te pregunte, y te saldrá un mensaje de éxito).

## Conectar tu Repositorio Local con GitHub
Si ya tienes tu repositorio local (el de tus apuntes) y creaste uno vacío en GitHub, debes vincularlos con estos comandos:

- Vincular el origen: `git remote add origin git@github.com:TuUser/TuRepo.git`
- Asegurar que la rama se llame main: `git branch -M main`
- Subir tus commits a la nube: `git push -u origin main`

## Subir y Bajar Cambios

- Para enviar tus nuevos commits a la nube: `git push origin main`.
- Para descargar cambios si alguien más (o tú en otra PC) modificó el repositorio en la nube: `git pull origin main`.

## comentarios
- Solución a error HTTPS: Si clonaste un repo por error con HTTPS y te pide contraseña, puedes cambiarlo a SSH usando: git remote set-url origin "git@github.com:TuUser/TuRepo.git".
- Límite de tamaño: El peso máximo de un archivo que puedes subir en un commit a GitHub es de 100 MB. Si intentas subir algo más pesado (como carpetas de node_modules o bases de datos), GitHub lo rechazará. Por eso es vital usar el .gitignore.

