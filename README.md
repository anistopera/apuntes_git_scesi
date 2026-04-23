# Trabajo Individual - Nicole Marisol Flores Choquetopa
## Clase 1
### ¿Qué es GIT?
Es un Sistema de Control de Versiones Distribuido (VCS) creado por Linus Torvalds. Nos permite guardar archivos y sus versiones a lo largo del tiempo de manera local.
### Comandos Básicos
- `git config --global user.name "Tu Nombre"`
- `git config --global user.email "tu@correo.com"`
- Saltos de línea (Especialmente importante en Windows para evitar errores con usuarios de Linux/Mac): `git config --global core.autocrlf true`.

-Para ver tus configuraciones guardadas: `git config --global --list`


## Clase 2
### Los 3 Estados de Git
1. **Directorio de Trabajo:** Carpeta local (estado *Untracked* o *Modified*).
2. **Stage Area:** Área temporal donde preparamos lo que se va a guardar (*Staged*).
3. **Repositorio Local:** El historial confirmado (*Commited*).

###  Buenas Prácticas
- (commit) representa un único cambio lógico, pequeño y completo en el código fuente
- Usa verbos imperativo- Usa verbos imperativos


## Clase 3
### Conexión Remota (SSH vs HTTPS)
Es mejor configurar SSH para no tener que ingresar credenciales cada vez que hacemos un `git push`.
### Comandos Remotos
- `git remote add origin <url>`: Vincula el repo local con el de GitHub.
- `git push origin main`: Sube los cambios al servidor.
### SSH vs HTTPS


- HTTPS: Si clonas o intentas subir código usando el enlace HTTPS, GitHub te pedirá tu usuario y contraseña (o un token) cada vez que hagas un push. El Auxi lo describió como algo muy molesto.


- SSH: Es la forma recomendada. Generas una "llave" en tu computadora y la guardas en GitHub. Así, tu computadora y GitHub se reconocen automáticamente de forma segura y no tienes que poner contraseñas nunca más
