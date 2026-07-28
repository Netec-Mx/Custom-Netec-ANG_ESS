# Instalación del software para el desarrollo con Angular

## Metadatos

| Campo            | Detalle                          |
|------------------|----------------------------------|
| **Duración**     | 49 minutos                       |
| **Complejidad**  | Fácil                            |
| **Nivel Bloom**  | Aplicar (*Apply*)                |
| **Módulo**       | 2 — Configuración del entorno    |
| **Versión guía** | 1.0                              |

---

## Descripción General

En esta práctica configurarás desde cero el entorno de desarrollo necesario para trabajar con Angular. Instalarás Node.js LTS —la plataforma de ejecución JavaScript fuera del navegador que habilita herramientas como NPM y Angular CLI—, TypeScript, Angular CLI y Visual Studio Code con sus extensiones esenciales. Al finalizar tendrás un entorno completamente funcional y verificado, listo para crear tu primera aplicación Angular en prácticas posteriores.

---

## Objetivos de Aprendizaje

Al completar este laboratorio serás capaz de:

- [ ] Instalar Node.js LTS y verificar su correcta instalación comprobando las versiones de `node` y `npm` en la terminal.
- [ ] Instalar TypeScript globalmente mediante NPM y confirmar la disponibilidad del compilador `tsc` en la línea de comandos.
- [ ] Instalar Angular CLI globalmente y verificar la instalación ejecutando `ng version` para confirmar que todas las dependencias están correctamente configuradas.
- [ ] Instalar y configurar Visual Studio Code con las extensiones esenciales para el desarrollo con Angular.
- [ ] Instalar Angular DevTools en Google Chrome y verificar que el entorno completo está operativo.

---

## Prerrequisitos

### Conocimiento previo

| Requisito | Descripción |
|-----------|-------------|
| Terminal básica | Saber abrir y ejecutar comandos en CMD, PowerShell, Terminal (macOS) o Bash/Zsh (Linux) |
| Sistema operativo | Familiaridad con la instalación de software mediante asistentes gráficos o gestores de paquetes |
| Concepto de PATH | Entender que el sistema operativo busca ejecutables en las rutas configuradas en la variable PATH |

### Acceso y permisos

| Requisito | Detalle |
|-----------|---------|
| Privilegios de administrador | Requeridos para instalar software globalmente en Windows, macOS y Linux |
| Conexión a Internet | Estable, mínimo 10 Mbps para descargar instaladores y paquetes NPM |
| Espacio en disco | Mínimo 10 GB libres |
| Sistema operativo | Windows 10/11, macOS 12+ o Ubuntu 20.04+ |

---

## Entorno de Laboratorio

### Hardware recomendado

| Componente | Mínimo | Recomendado |
|------------|--------|-------------|
| Procesador | Intel Core i5 / 1.6 GHz (64-bit) | Intel Core i7 / 2.0 GHz o superior |
| Memoria RAM | 8 GB | 16 GB |
| Almacenamiento libre | 10 GB | 20 GB SSD |
| Resolución de pantalla | 1280 × 768 | 1920 × 1080 |

### Software a instalar durante la práctica

| Herramienta | Versión objetivo | Propósito en Angular |
|-------------|-----------------|----------------------|
| Node.js | 20.x LTS | Entorno de ejecución; habilita NPM y Angular CLI |
| NPM | 10.x (incluido con Node.js 20.x) | Gestión de paquetes y dependencias |
| TypeScript | 5.x | Lenguaje base de Angular |
| Angular CLI | 17.x | Creación, compilación y gestión de proyectos |
| Visual Studio Code | 1.85+ | Editor de código principal |
| Google Chrome | 120+ | Navegador de desarrollo y pruebas |
| Angular DevTools | Última disponible | Depuración de componentes Angular en Chrome |

### Verificación previa del entorno

Antes de comenzar, abre una terminal y ejecuta los siguientes comandos para saber si ya tienes alguna herramienta instalada:

```bash
# Verificar si Node.js ya está instalado
node --version

# Verificar si NPM ya está instalado
npm --version

# Verificar si TypeScript ya está instalado
tsc --version

# Verificar si Angular CLI ya está instalado
ng version
```

> **Nota:** Si alguno de estos comandos devuelve un número de versión, anótalo. Si la versión existente es compatible con los requisitos del curso, puedes omitir ese paso de instalación. Si devuelve un error de "comando no encontrado", el software no está instalado.

---

## Instrucciones Paso a Paso

---

### Paso 1: Instalación de Node.js LTS

**Objetivo:** Instalar Node.js 20.x LTS en tu sistema operativo y verificar que tanto `node` como `npm` están disponibles en la terminal.

**Contexto:** Como aprendiste en la lección 2.1, Node.js es el entorno de ejecución que hace posible todas las herramientas de desarrollo de Angular. Sin él, no es posible instalar Angular CLI ni gestionar dependencias con NPM. Recuerda que Node.js utiliza el motor V8 de Google para ejecutar JavaScript fuera del navegador, lo que permite que herramientas como Angular CLI funcionen como procesos del sistema operativo.

#### Instrucciones para Windows

1. Abre tu navegador y navega a [https://nodejs.org](https://nodejs.org).
2. Haz clic en el botón **"20.x.x LTS — Recommended For Most Users"**. El sitio detecta tu sistema operativo automáticamente y ofrece el instalador `.msi` correspondiente.
3. Una vez descargado el archivo `.msi`, ejecútalo con doble clic.
4. En el asistente de instalación:
   - Acepta el acuerdo de licencia.
   - Deja la ruta de instalación predeterminada (`C:\Program Files\nodejs\`).
   - En la pantalla **"Custom Setup"**, asegúrate de que la opción **"Add to PATH"** esté marcada (viene marcada por defecto).
   - En la pantalla **"Tools for Native Modules"**, puedes dejar la casilla **desmarcada** para esta práctica.
5. Haz clic en **Install** y espera a que finalice. Acepta el control de cuentas de usuario (UAC) si se solicita.
6. Haz clic en **Finish**.
7. **Cierra y vuelve a abrir** cualquier terminal que tengas abierta para que los cambios en el PATH surtan efecto.

#### Instrucciones para macOS

1. Navega a [https://nodejs.org](https://nodejs.org) y descarga el instalador `.pkg` de la versión **20.x.x LTS**.
2. Ejecuta el archivo `.pkg` descargado.
3. Sigue el asistente de instalación: acepta la licencia, confirma la ubicación de instalación y proporciona tu contraseña de administrador cuando se solicite.
4. Al finalizar, cierra y vuelve a abrir la Terminal.

> **Alternativa con Homebrew (macOS):**
> ```bash
> # Si tienes Homebrew instalado, puedes usar:
> brew install node@20
> brew link node@20
> ```

#### Instrucciones para Ubuntu/Debian (Linux)

```bash
# Paso 1: Agregar el repositorio oficial de NodeSource para Node.js 20.x
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -

# Paso 2: Instalar Node.js (incluye NPM automáticamente)
sudo apt-get install -y nodejs

# Paso 3: Verificar la instalación
node --version
npm --version
```

> **Nota para Linux — Permisos de instalación global NPM:** Para evitar problemas de permisos al instalar paquetes globales con `npm install -g`, configura NPM para que instale en tu directorio home:
> ```bash
> # Configurar directorio de paquetes globales en el home del usuario
> mkdir -p ~/.npm-global
> npm config set prefix '~/.npm-global'
>
> # Agregar al PATH (para Bash)
> echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
> source ~/.bashrc
>
> # Agregar al PATH (para Zsh)
> echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.zshrc
> source ~/.zshrc
> ```

#### Verificación de Node.js

Una vez instalado en cualquier sistema operativo, ejecuta:

```bash
# Verificar versión de Node.js
node --version
```

**Salida esperada:**
```
v20.11.1
```
*(El número de parche puede variar; lo importante es que comience con `v20.`)*

```bash
# Verificar versión de NPM
npm --version
```

**Salida esperada:**
```
10.2.4
```
*(El número exacto puede variar; lo importante es que sea 10.x)*

```bash
# Prueba adicional: ejecutar un fragmento de JavaScript directamente con Node.js
node -e "console.log('Node.js funciona correctamente en este sistema')"
```

**Salida esperada:**
```
Node.js funciona correctamente en este sistema
```

> **✅ Verificación del Paso 1:** Si los tres comandos anteriores se ejecutan sin errores y muestran versiones válidas, Node.js está correctamente instalado. Toma una captura de pantalla de la terminal con estas salidas para tu documentación.

---

### Paso 2: Instalación de TypeScript

**Objetivo:** Instalar TypeScript globalmente mediante NPM y verificar que el compilador `tsc` está disponible en la terminal.

**Contexto:** TypeScript es el lenguaje principal de Angular. Es un superconjunto de JavaScript que agrega tipado estático y características de programación orientada a objetos. Angular CLI lo gestiona automáticamente en los proyectos, pero instalar TypeScript globalmente te permite usar el compilador `tsc` de forma independiente para exploración y verificación.

#### Instrucciones

1. Abre una terminal (o usa la misma del paso anterior).

2. Ejecuta el siguiente comando para instalar TypeScript globalmente:

```bash
# Instalar TypeScript globalmente
npm install -g typescript
```

**Salida esperada durante la instalación:**
```
added 1 package in 3s
```

3. Verifica la instalación:

```bash
# Verificar la versión de TypeScript instalada
tsc --version
```

**Salida esperada:**
```
Version 5.3.3
```
*(El número exacto puede variar; lo importante es que sea 5.x)*

4. Explora brevemente TypeScript creando un archivo de prueba:

```bash
# Crear un directorio temporal de prueba
mkdir ts-test && cd ts-test

# Crear un archivo TypeScript de prueba
# En Windows (PowerShell):
echo 'const mensaje: string = "TypeScript funciona correctamente"; console.log(mensaje);' > prueba.ts

# En macOS/Linux:
echo 'const mensaje: string = "TypeScript funciona correctamente"; console.log(mensaje);' > prueba.ts
```

5. Compila y ejecuta el archivo de prueba:

```bash
# Compilar el archivo TypeScript a JavaScript
tsc prueba.ts

# Verificar que se generó el archivo JavaScript
# En Windows:
dir prueba.js

# En macOS/Linux:
ls -la prueba.js

# Ejecutar el archivo JavaScript generado
node prueba.js
```

**Salida esperada:**
```
TypeScript funciona correctamente
```

6. Regresa al directorio principal y elimina el directorio de prueba:

```bash
# Volver al directorio anterior
cd ..

# Eliminar el directorio de prueba
# En Windows (PowerShell):
Remove-Item -Recurse -Force ts-test

# En macOS/Linux:
rm -rf ts-test
```

> **✅ Verificación del Paso 2:** El comando `tsc --version` devuelve una versión 5.x y la compilación del archivo de prueba generó correctamente un `.js` ejecutable. Toma una captura de pantalla.

---

### Paso 3: Instalación de Angular CLI

**Objetivo:** Instalar Angular CLI 17.x globalmente y verificar la instalación con `ng version`, confirmando que todas las dependencias están correctamente configuradas.

**Contexto:** Angular CLI (Command Line Interface) es la herramienta de línea de comandos oficial de Angular. Permite crear proyectos, generar componentes, ejecutar el servidor de desarrollo, compilar para producción y mucho más. Angular CLI depende directamente de Node.js y NPM para funcionar.

#### Instrucciones

1. Instala Angular CLI globalmente:

```bash
# Instalar Angular CLI globalmente
npm install -g @angular/cli
```

> **Nota:** Este proceso puede tardar entre 1 y 3 minutos dependiendo de la velocidad de tu conexión a Internet, ya que descarga Angular CLI y todas sus dependencias transitivas.

**Salida esperada (fragmento):**
```
added 254 packages in 45s
```

2. Verifica la instalación con el comando de versión:

```bash
# Verificar la instalación de Angular CLI
ng version
```

**Salida esperada:**
```
     _                      _                 ____ _     ___
    / \   _ __   __ _ _   _| | __ _ _ __     / ___| |   |_ _|
   / △ \ | '_ \ / _` | | | | |/ _` | '__|   | |   | |    | |
  / ___ \| | | | (_| | |_| | | (_| | |      | |___| |___ | |
 /_/   \_\_| |_|\__, |\__,_|_|\__,_|_|       \____|_____|___|
                |___/


Angular CLI: 17.x.x
Node: 20.x.x
Package Manager: npm 10.x.x
OS: <tu sistema operativo>
```

> **Importante:** Si ves advertencias de seguridad (`npm warn`) durante la instalación, no son errores críticos. Son avisos informativos. Lo que debes evitar son mensajes de `npm error`.

3. Explora los comandos disponibles en Angular CLI:

```bash
# Ver todos los comandos disponibles en Angular CLI
ng help
```

4. Verifica que Angular CLI puede crear proyectos (sin crear uno todavía):

```bash
# Ver las opciones del comando ng new
ng new --help
```

> **Nota sobre proyectos standalone vs NgModule:** Angular 17 crea proyectos en modo *standalone* por defecto. En prácticas posteriores usaremos la opción `--no-standalone` para trabajar con NgModule, que es el enfoque tradicional recomendado para este curso introductorio.

> **✅ Verificación del Paso 3:** El comando `ng version` muestra Angular CLI 17.x con Node.js 20.x y NPM 10.x sin mensajes de error. Toma una captura de pantalla completa de la salida.

---

### Paso 4: Instalación y Configuración de Visual Studio Code

**Objetivo:** Instalar Visual Studio Code e instalar las extensiones esenciales para el desarrollo con Angular.

**Contexto:** Visual Studio Code (VS Code) es el editor de código más utilizado en el ecosistema Angular. Su integración con TypeScript es nativa y, con las extensiones correctas, proporciona autocompletado inteligente, navegación de código, detección de errores en tiempo real y formateo automático.

#### Instrucciones — Instalación de VS Code

1. Navega a [https://code.visualstudio.com](https://code.visualstudio.com).
2. Descarga el instalador correspondiente a tu sistema operativo:
   - **Windows:** Descarga el instalador `.exe` (System Installer recomendado para instalación global).
   - **macOS:** Descarga el archivo `.zip` o `.dmg`.
   - **Linux (Ubuntu/Debian):** Descarga el paquete `.deb`.
3. Ejecuta el instalador:
   - **Windows:** Durante la instalación, marca las opciones **"Add to PATH"** y **"Register Code as an editor for supported file types"**.
   - **macOS:** Arrastra VS Code a la carpeta Aplicaciones. Luego abre VS Code, abre la paleta de comandos (`Cmd+Shift+P`) y ejecuta **"Shell Command: Install 'code' command in PATH"**.
   - **Linux:** `sudo dpkg -i code_*.deb`
4. Abre VS Code. Deberías ver la pantalla de bienvenida.

#### Instrucciones — Instalación de Extensiones

Las extensiones se instalan desde el panel de extensiones de VS Code (`Ctrl+Shift+X` en Windows/Linux, `Cmd+Shift+X` en macOS) o desde la terminal usando el comando `code --install-extension`.

**Método por terminal (recomendado para rapidez):**

```bash
# Extensión 1: Angular Language Service (autocompletado y navegación en templates Angular)
code --install-extension Angular.ng-template

# Extensión 2: ESLint (análisis estático de código)
code --install-extension dbaeumer.vscode-eslint

# Extensión 3: Prettier - Code formatter (formateo automático de código)
code --install-extension esbenp.prettier-vscode

# Extensión 4: Angular Snippets (fragmentos de código para Angular)
code --install-extension johnpapa.Angular2

# Extensión 5: Material Icon Theme (iconos descriptivos para archivos del proyecto)
code --install-extension PKief.material-icon-theme
```

**Verificación de extensiones instaladas:**

```bash
# Listar todas las extensiones instaladas en VS Code
code --list-extensions
```

**Salida esperada (debe incluir estas extensiones):**
```
Angular.ng-template
dbaeumer.vscode-eslint
esbenp.prettier-vscode
johnpapa.Angular2
PKief.material-icon-theme
```

#### Instrucciones — Configuración básica de VS Code

1. Abre VS Code.
2. Abre la configuración de usuario con `Ctrl+,` (Windows/Linux) o `Cmd+,` (macOS).
3. En la barra de búsqueda de configuración, busca y configura las siguientes opciones:

| Configuración | Valor | Descripción |
|--------------|-------|-------------|
| `editor.formatOnSave` | `true` | Formatea el código automáticamente al guardar |
| `editor.defaultFormatter` | `esbenp.prettier-vscode` | Usar Prettier como formateador por defecto |
| `editor.tabSize` | `2` | Indentación de 2 espacios (estándar en Angular) |
| `editor.wordWrap` | `on` | Ajuste de línea automático |

**Alternativa — Editar directamente el archivo `settings.json`:**

Abre la paleta de comandos (`Ctrl+Shift+P` / `Cmd+Shift+P`), escribe **"Open User Settings (JSON)"** y agrega:

```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.tabSize": 2,
  "editor.wordWrap": "on",
  "files.autoSave": "onFocusChange",
  "workbench.iconTheme": "material-icon-theme"
}
```

4. Guarda el archivo de configuración (`Ctrl+S` / `Cmd+S`).

> **✅ Verificación del Paso 4:** VS Code abre correctamente, el comando `code --list-extensions` muestra las cinco extensiones instaladas y la configuración de usuario está guardada. Toma una captura de pantalla de VS Code con el panel de extensiones mostrando las extensiones activas.

---

### Paso 5: Instalación de Angular DevTools en Google Chrome

**Objetivo:** Instalar la extensión Angular DevTools en Google Chrome y verificar que el navegador puede inspeccionar aplicaciones Angular.

**Contexto:** Angular DevTools es una extensión oficial de Chrome desarrollada por el equipo de Angular. Permite inspeccionar el árbol de componentes, visualizar el estado de cada componente, analizar el rendimiento y depurar la detección de cambios directamente desde las herramientas de desarrollador del navegador.

#### Instrucciones

1. Abre Google Chrome (versión 120 o superior).

2. Navega a la Chrome Web Store:
   ```
   https://chrome.google.com/webstore/detail/angular-devtools/ienfalfjdbdpebioblfackkekamfmbnh
   ```
   O busca **"Angular DevTools"** directamente en la Chrome Web Store ([https://chrome.google.com/webstore](https://chrome.google.com/webstore)).

3. Haz clic en el botón **"Agregar a Chrome"** (Add to Chrome).

4. En el cuadro de diálogo de confirmación, haz clic en **"Agregar extensión"**.

5. Una vez instalada, verás el ícono de Angular DevTools (un escudo con el logo de Angular) en la barra de extensiones de Chrome.

#### Verificación de Angular DevTools

Para verificar que Angular DevTools está correctamente instalado:

1. Navega a una aplicación Angular de ejemplo. Puedes usar la aplicación de demostración oficial:
   ```
   https://angular.io/generated/live-examples/toh-pt6/stackblitz.html
   ```
   O cualquier aplicación Angular pública.

2. Abre las Herramientas de Desarrollador de Chrome (`F12` o `Ctrl+Shift+I` / `Cmd+Option+I`).

3. Busca la pestaña **"Angular"** en la barra de pestañas de DevTools.

4. Si la pestaña Angular aparece y muestra el árbol de componentes de la aplicación, la extensión está funcionando correctamente.

> **Nota:** En sitios web que **no** son aplicaciones Angular, la pestaña Angular aparecerá pero mostrará el mensaje *"Angular application not detected"*. Esto es el comportamiento correcto.

> **✅ Verificación del Paso 5:** La extensión Angular DevTools aparece en la barra de Chrome y la pestaña "Angular" es visible en las herramientas de desarrollador. Toma una captura de pantalla.

---

### Paso 6: Verificación Integral del Entorno

**Objetivo:** Confirmar que todas las herramientas instaladas funcionan correctamente de forma integrada.

**Contexto:** Antes de dar por concluida la configuración del entorno, es importante realizar una verificación completa que confirme que todas las herramientas pueden interactuar entre sí. Crearás un proyecto Angular mínimo de prueba para validar la integración completa.

#### Instrucciones

1. Abre una terminal nueva (para asegurarte de que tiene las variables de entorno actualizadas).

2. Navega a un directorio de trabajo temporal:

```bash
# En Windows (PowerShell):
cd $env:USERPROFILE\Desktop

# En macOS/Linux:
cd ~/Desktop
```

3. Crea un proyecto Angular de prueba:

```bash
# Crear un proyecto Angular mínimo de prueba
# --no-standalone: usa NgModule (modo tradicional, recomendado para este curso)
# --skip-git: no inicializa repositorio Git
# --skip-tests: omite archivos de prueba para simplificar
ng new verificacion-entorno --no-standalone --skip-git --skip-tests
```

Cuando Angular CLI solicite información:
- **"Which stylesheet format would you like to use?"** → Selecciona **CSS** (opción por defecto, presiona Enter).

> **Nota:** La creación del proyecto descargará las dependencias NPM necesarias. Esto puede tardar entre 2 y 5 minutos.

4. Navega al directorio del proyecto creado:

```bash
cd verificacion-entorno
```

5. Inicia el servidor de desarrollo:

```bash
# Iniciar el servidor de desarrollo de Angular
ng serve --open
```

> La opción `--open` abre automáticamente el navegador en `http://localhost:4200`.

**Salida esperada en terminal:**
```
✔ Browser application bundle generation complete.

Initial Chunk Files   | Names         |  Raw Size
vendor.js             | vendor        |   1.77 MB |
polyfills.js          | polyfills     | 314.28 kB |
styles.css, styles.js | styles        |  62.37 kB |
main.js               | main          |  19.86 kB |

                      | Initial Total |   2.16 MB

Build at: 2024-01-15T10:30:00.000Z - Hash: abc123def456 - Time: 8521ms

** Angular Live Development Server is listening on localhost:4200, open your browser on http://localhost:4200/ **


✔ Compiled successfully.
```

6. Verifica en el navegador:
   - Deberías ver la página de bienvenida de Angular con el mensaje **"verificacion-entorno app is running!"** y el logo de Angular.

7. Abre el proyecto en VS Code:

```bash
# Abrir el proyecto en Visual Studio Code
code .
```

8. Verifica que VS Code reconoce el proyecto Angular:
   - Abre el archivo `src/app/app.component.ts`.
   - Debería ver resaltado de sintaxis TypeScript y Angular Language Service activo (autocompletado al escribir).

9. Detén el servidor de desarrollo con `Ctrl+C` en la terminal.

10. Elimina el proyecto de prueba:

```bash
# Volver al directorio anterior
cd ..

# Eliminar el proyecto de prueba
# En Windows (PowerShell):
Remove-Item -Recurse -Force verificacion-entorno

# En macOS/Linux:
rm -rf verificacion-entorno
```

> **✅ Verificación del Paso 6:** El proyecto Angular se creó, compiló y ejecutó correctamente en `http://localhost:4200`. VS Code abrió el proyecto con resaltado de sintaxis activo. Toma capturas de pantalla del navegador y del editor.

---

## Validación y Pruebas

Ejecuta el siguiente bloque de comandos completo para generar un resumen del estado de todas las herramientas instaladas. Copia la salida completa como evidencia de la práctica:

```bash
# ============================================================
# RESUMEN DE VERIFICACIÓN DEL ENTORNO DE DESARROLLO ANGULAR
# ============================================================

echo "=== VERIFICACIÓN DEL ENTORNO ANGULAR ==="
echo ""

echo "--- Node.js ---"
node --version

echo ""
echo "--- NPM ---"
npm --version

echo ""
echo "--- TypeScript ---"
tsc --version

echo ""
echo "--- Angular CLI ---"
ng version

echo ""
echo "--- Visual Studio Code ---"
code --version

echo ""
echo "--- Extensiones VS Code ---"
code --list-extensions

echo ""
echo "=== FIN DE LA VERIFICACIÓN ==="
```

**Salida completa esperada:**

```
=== VERIFICACIÓN DEL ENTORNO ANGULAR ===

--- Node.js ---
v20.11.1

--- NPM ---
10.2.4

--- TypeScript ---
Version 5.3.3

--- Angular CLI ---
     _                      _                 ____ _     ___
    / \   _ __   __ _ _   _| | __ _ _ __     / ___| |   |_ _|
   / △ \ | '_ \ / _` | | | | |/ _` | '__|   | |   | |    | |
  / ___ \| | | | (_| | |_| | | (_| | |      | |___| |___ | |
 /_/   \_\_| |_|\__, |\__,_|_|\__,_|_|       \____|_____|___|
                |___/


Angular CLI: 17.x.x
Node: 20.x.x
Package Manager: npm 10.x.x
OS: <sistema operativo>

--- Visual Studio Code ---
1.85.x
<hash de commit>
<arquitectura>

--- Extensiones VS Code ---
Angular.ng-template
dbaeumer.vscode-eslint
esbenp.prettier-vscode
johnpapa.Angular2
PKief.material-icon-theme

=== FIN DE LA VERIFICACIÓN ===
```

### Lista de verificación final

Marca cada elemento completado:

- [ ] `node --version` devuelve `v20.x.x`
- [ ] `npm --version` devuelve `10.x.x`
- [ ] `tsc --version` devuelve `Version 5.x.x`
- [ ] `ng version` muestra Angular CLI 17.x sin errores
- [ ] `code --version` devuelve la versión de VS Code instalada
- [ ] Las 5 extensiones de VS Code están listadas en `code --list-extensions`
- [ ] Angular DevTools está instalado en Chrome y visible en DevTools
- [ ] El proyecto de prueba se compiló y ejecutó correctamente en `http://localhost:4200`

---

## Solución de Problemas

### Problema 1: El comando `ng` no se reconoce después de instalar Angular CLI

**Síntoma:**
```
ng : El término 'ng' no se reconoce como nombre de un cmdlet...
# (Windows PowerShell)

-bash: ng: command not found
# (macOS/Linux)
```

**Causa:**
La variable de entorno `PATH` del sistema no incluye el directorio donde NPM instala los paquetes globales, o la terminal no se actualizó para reflejar los cambios realizados durante la instalación.

**Solución:**

*En Windows:*
```powershell
# Paso 1: Verificar dónde instaló NPM los paquetes globales
npm config get prefix
# Salida típica: C:\Users\<usuario>\AppData\Roaming\npm

# Paso 2: Verificar que esa ruta está en el PATH
$env:PATH -split ";" | Where-Object { $_ -like "*npm*" }

# Paso 3: Si no aparece, agregar manualmente (sesión actual):
$env:PATH += ";C:\Users\$env:USERNAME\AppData\Roaming\npm"

# Paso 4: Cierra y vuelve a abrir PowerShell/CMD completamente
# (no solo una nueva pestaña)
```

*En macOS/Linux:*
```bash
# Paso 1: Verificar el directorio de instalación global de NPM
npm config get prefix
# Salida típica: /usr/local  o  ~/.npm-global

# Paso 2: Verificar si el bin está en el PATH
echo $PATH | grep -o '[^:]*npm[^:]*'

# Paso 3: Si usaste ~/.npm-global (configuración recomendada para Linux):
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
# O para Zsh:
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.zshrc
source ~/.zshrc

# Paso 4: Verificar
ng version
```

---

### Problema 2: Error de permisos al ejecutar `npm install -g` en macOS o Linux

**Síntoma:**
```
npm warn checkPermissions Missing write access to /usr/local/lib/node_modules
npm error code EACCES
npm error syscall access
npm error path /usr/local/lib/node_modules
npm error errno -13
npm error Error: EACCES: permission denied, access '/usr/local/lib/node_modules'
```

**Causa:**
El directorio de paquetes globales de NPM (`/usr/local/lib/node_modules`) pertenece al usuario `root`, por lo que el usuario actual no tiene permisos de escritura. Esto ocurre cuando Node.js se instaló mediante el instalador oficial en macOS o con `apt` sin configurar el directorio global personalizado en Linux.

**Solución (sin usar `sudo`):**

```bash
# Solución recomendada: Configurar NPM para usar un directorio en el home del usuario

# Paso 1: Crear el directorio para paquetes globales
mkdir -p ~/.npm-global

# Paso 2: Configurar NPM para usar ese directorio
npm config set prefix '~/.npm-global'

# Paso 3: Agregar el directorio al PATH
# Para Bash:
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
source ~/.bashrc

# Para Zsh (macOS por defecto desde Catalina):
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.zshrc
source ~/.zshrc

# Paso 4: Verificar la nueva configuración
npm config get prefix
# Salida esperada: /Users/<usuario>/.npm-global  (macOS)
#                  /home/<usuario>/.npm-global   (Linux)

# Paso 5: Reinstalar TypeScript y Angular CLI con la nueva configuración
npm install -g typescript
npm install -g @angular/cli

# Paso 6: Verificar
tsc --version
ng version
```

> **⚠️ Advertencia:** Evita usar `sudo npm install -g` como solución. Aunque funciona temporalmente, puede crear archivos propiedad de `root` en el directorio del proyecto y causar problemas de permisos más difíciles de resolver posteriormente.

---

## Limpieza

Al finalizar la práctica, el entorno debe quedar limpio. Las herramientas instaladas (Node.js, TypeScript, Angular CLI, VS Code y Angular DevTools) **deben permanecer instaladas** ya que son necesarias para todas las prácticas posteriores del curso.

Lo único que debes verificar que fue eliminado es el proyecto de prueba creado en el Paso 6:

```bash
# Verificar que el proyecto de prueba fue eliminado
# En Windows (PowerShell):
Test-Path "$env:USERPROFILE\Desktop\verificacion-entorno"
# Salida esperada: False

# En macOS/Linux:
ls ~/Desktop/verificacion-entorno 2>/dev/null && echo "EXISTE - eliminar" || echo "Eliminado correctamente"
```

Si el proyecto de prueba aún existe, elimínalo:

```bash
# En Windows (PowerShell):
Remove-Item -Recurse -Force "$env:USERPROFILE\Desktop\verificacion-entorno"

# En macOS/Linux:
rm -rf ~/Desktop/verificacion-entorno
```

### Estado final esperado del sistema

| Herramienta | Estado | Verificación |
|-------------|--------|-------------|
| Node.js 20.x LTS | ✅ Instalado | `node --version` → `v20.x.x` |
| NPM 10.x | ✅ Instalado | `npm --version` → `10.x.x` |
| TypeScript 5.x | ✅ Instalado globalmente | `tsc --version` → `Version 5.x.x` |
| Angular CLI 17.x | ✅ Instalado globalmente | `ng version` → Angular CLI 17.x |
| VS Code 1.85+ | ✅ Instalado con extensiones | `code --version` → versión válida |
| Angular DevTools | ✅ Instalado en Chrome | Pestaña Angular visible en DevTools |
| Proyecto de prueba | 🗑️ Eliminado | No debe existir en el escritorio |

---

## Resumen

En esta práctica configuraste completamente el entorno de desarrollo para Angular. Instalaste y verificaste las cinco herramientas fundamentales del ecosistema:

1. **Node.js 20.x LTS** — El entorno de ejecución JavaScript que, basado en el motor V8 de Google, permite ejecutar herramientas de desarrollo fuera del navegador. Sin Node.js, ni NPM ni Angular CLI pueden funcionar.

2. **TypeScript 5.x** — El lenguaje de programación base de Angular, instalado globalmente para tener acceso al compilador `tsc` desde cualquier directorio.

3. **Angular CLI 17.x** — La herramienta de línea de comandos oficial que gestiona todo el ciclo de vida de los proyectos Angular: creación, desarrollo, compilación y despliegue.

4. **Visual Studio Code** con las extensiones **Angular Language Service**, **ESLint**, **Prettier**, **Angular Snippets** y **Material Icon Theme** — El editor optimizado para el desarrollo con TypeScript y Angular.

5. **Angular DevTools** — La extensión de Chrome que permite inspeccionar y depurar aplicaciones Angular directamente desde el navegador.

La validación integral del Paso 6 confirmó que todas estas herramientas funcionan de forma integrada, creando y ejecutando exitosamente un proyecto Angular real.

### Conceptos clave reforzados

- Node.js no ejecuta la aplicación Angular final (eso lo hace el navegador), sino que **habilita las herramientas de desarrollo** como Angular CLI y NPM.
- El motor **V8** es el núcleo compartido entre Chrome y Node.js, lo que garantiza compatibilidad de JavaScript entre ambos entornos.
- Siempre se debe usar la versión **LTS** de Node.js en entornos de desarrollo profesional por su estabilidad y soporte extendido.
- La configuración del **PATH** del sistema es crítica para que los comandos `node`, `npm`, `tsc` y `ng` estén disponibles en cualquier terminal.

### Próximos pasos

Con el entorno completamente configurado, en la **Práctica 2.2** explorarás NPM en profundidad: aprenderás a gestionar dependencias, entenderás la estructura del archivo `package.json` y crearás tu primer proyecto Angular real utilizando Angular CLI con todas las herramientas que acabas de instalar.

### Recursos adicionales

| Recurso | URL |
|---------|-----|
| Sitio oficial de Node.js | https://nodejs.org/es |
| Tabla de compatibilidad Angular–Node.js | https://angular.dev/reference/releases |
| Documentación de Angular CLI | https://angular.dev/tools/cli |
| Documentación de TypeScript | https://www.typescriptlang.org/docs |
| Marketplace de extensiones VS Code | https://marketplace.visualstudio.com/vscode |
| Angular DevTools en Chrome Web Store | https://chrome.google.com/webstore/detail/angular-devtools/ienfalfjdbdpebioblfackkekamfmbnh |
| nvm (Node Version Manager) para gestión de versiones | https://github.com/nvm-sh/nvm |

---

---

# Crea el proyecto Hola Mundo de Angular y verifica que funcione correctamente

## 1. Metadatos

| Campo            | Valor                                      |
|------------------|--------------------------------------------|
| **Duración**     | 49 minutos                                 |
| **Complejidad**  | Fácil                                      |
| **Nivel Bloom**  | Crear (Create)                             |
| **Módulo**       | 2 — Fundamentos del entorno Angular        |
| **Laboratorio**  | 02-00-02                                   |

---

## 2. Descripción General

En este laboratorio crearás tu primer proyecto Angular real utilizando Angular CLI, explorarás en detalle la estructura de archivos y directorios generada automáticamente, y personalizarás el componente raíz para mostrar un mensaje de "Hola Mundo" con tu nombre. Además, ejecutarás el servidor de desarrollo para verificar que la aplicación funciona correctamente en el navegador y realizarás un build de producción para comprender el proceso de compilación de Angular. Esta práctica consolida la comprensión del rol de Node.js y NPM —vistos en la lección 2.1— como infraestructura que hace posible el funcionamiento de Angular CLI y el servidor de desarrollo local.

---

## 3. Objetivos de Aprendizaje

Al finalizar este laboratorio, serás capaz de:

- [ ] Crear un nuevo proyecto Angular con `ng new` configurando las opciones de routing y estilos CSS
- [ ] Identificar el propósito de cada archivo y carpeta principal generados por Angular CLI
- [ ] Ejecutar el servidor de desarrollo con `ng serve` y verificar la aplicación en `http://localhost:4200`
- [ ] Modificar `AppComponent` para mostrar un mensaje personalizado usando interpolación (`{{title}}`)
- [ ] Ejecutar `ng build` y explorar los artefactos generados en la carpeta `dist/`

---

## 4. Prerrequisitos

### Conocimientos previos
- Conceptos básicos de HTML (etiquetas, atributos, estructura de documento)
- Comprensión de qué es Node.js y su rol en el ecosistema Angular (Lección 2.1)
- Familiaridad básica con la terminal o línea de comandos del sistema operativo

### Acceso y herramientas requeridas
- Laboratorio **02-00-01 completado y verificado** (entorno de desarrollo instalado)
- Node.js 20.x LTS instalado y funcional (`node --version` devuelve `v20.x.x`)
- NPM 10.x instalado y funcional (`npm --version` devuelve `10.x.x`)
- Angular CLI 17.x instalado globalmente (`ng version` devuelve `17.x.x`)
- Visual Studio Code 1.85.x o superior con la extensión **Angular Language Service** instalada
- Google Chrome 120.x o superior con la extensión **Angular DevTools** instalada
- Conexión a Internet activa (puede requerirse para la descarga inicial de dependencias NPM)

---

## 5. Entorno de Laboratorio

### Tabla de hardware recomendado

| Componente        | Mínimo                        | Recomendado                    |
|-------------------|-------------------------------|--------------------------------|
| Procesador        | Intel Core i5 / 1.6 GHz 64-bit | Intel Core i7 / 2.0 GHz 64-bit |
| Memoria RAM       | 8 GB                          | 16 GB                          |
| Espacio en disco  | 10 GB libres                  | 20 GB libres                   |
| Resolución        | 1280×768                      | 1920×1080                      |
| Conexión a red    | 10 Mbps                       | 25 Mbps o superior             |

### Tabla de software requerido

| Software              | Versión mínima | Versión recomendada |
|-----------------------|----------------|---------------------|
| Node.js               | 18.x LTS       | 20.x LTS            |
| NPM                   | 9.x            | 10.x                |
| Angular CLI           | 16.x           | 17.x                |
| TypeScript            | 4.9.x          | 5.x                 |
| Visual Studio Code    | 1.85.x         | Última estable      |
| Google Chrome         | 120.x          | Última estable      |

### Verificación previa del entorno

Antes de comenzar, abre una terminal y ejecuta los siguientes comandos para confirmar que el entorno está listo:

```bash
# Verificar Node.js
node --version
# Salida esperada: v20.x.x

# Verificar NPM
npm --version
# Salida esperada: 10.x.x

# Verificar Angular CLI
ng version
# Salida esperada: Angular CLI: 17.x.x (entre otros datos)
```

> **⚠️ Importante:** Si alguno de estos comandos falla, regresa al Laboratorio 02-00-01 y verifica que el entorno esté correctamente configurado antes de continuar.

### Nota sobre la modalidad del proyecto

En este laboratorio se utilizará la opción `--no-standalone` para crear el proyecto en **modo tradicional con NgModule**. Esto es consistente con la recomendación del curso para aprendizaje introductorio. Angular 17 crea proyectos en modo standalone por defecto, pero usaremos la sintaxis clásica para facilitar la comprensión de la arquitectura modular.

---

## 6. Pasos del Laboratorio

---

### Paso 1: Preparar el directorio de trabajo

**Objetivo:** Crear y navegar hasta la carpeta donde se almacenarán los proyectos del curso.

#### Instrucciones

**En Windows (PowerShell o CMD):**

```powershell
# Navegar al directorio del usuario
cd %USERPROFILE%

# Crear carpeta para los proyectos del curso
mkdir angular-labs

# Navegar a la carpeta creada
cd angular-labs
```

**En macOS / Linux (Bash o Zsh):**

```bash
# Navegar al directorio del usuario
cd ~

# Crear carpeta para los proyectos del curso
mkdir angular-labs

# Navegar a la carpeta creada
cd angular-labs
```

#### Salida esperada

No se produce salida visible al crear el directorio. Al ejecutar `cd angular-labs` el prompt de la terminal cambiará para reflejar la nueva ubicación. Puedes confirmarlo con:

```bash
# En macOS/Linux
pwd
# Salida esperada: /home/tu-usuario/angular-labs  (o /Users/tu-usuario/angular-labs en macOS)

# En Windows PowerShell
Get-Location
# Salida esperada: C:\Users\tu-usuario\angular-labs
```

#### Verificación

Confirma que te encuentras dentro del directorio `angular-labs` antes de continuar al siguiente paso.

---

### Paso 2: Crear el proyecto Angular con Angular CLI

**Objetivo:** Generar un nuevo proyecto Angular llamado `hola-mundo` utilizando `ng new` con las opciones de configuración apropiadas.

#### Instrucciones

1. Asegúrate de estar dentro del directorio `angular-labs` (verificado en el Paso 1).

2. Ejecuta el siguiente comando para crear el proyecto:

```bash
ng new hola-mundo --routing=false --style=css --no-standalone
```

> **📝 Explicación de los parámetros:**
> - `hola-mundo` — nombre del proyecto y del directorio que se creará
> - `--routing=false` — no genera el módulo de enrutamiento (no necesario para este laboratorio)
> - `--style=css` — usa CSS puro como preprocesador de estilos (en lugar de SCSS, SASS o LESS)
> - `--no-standalone` — crea el proyecto en modo tradicional con NgModule (recomendado para este curso)

3. Angular CLI te preguntará si deseas compartir datos de uso anónimos. Responde según tu preferencia:

```
Would you like to share pseudonymous usage data about this project with the Angular Team
at Google under Google's Privacy Policy at https://policies.google.com/privacy. For more
details and how to change this setting, see https://angular.io/analytics.

(y/N)
```

Escribe `N` y presiona **Enter**.

4. Angular CLI comenzará a crear los archivos del proyecto e instalará las dependencias automáticamente. Este proceso puede tomar entre **1 y 5 minutos** dependiendo de la velocidad de tu conexión a Internet y el rendimiento del equipo.

#### Salida esperada

Verás una salida similar a la siguiente mientras Angular CLI trabaja:

```
CREATE hola-mundo/README.md (1067 bytes)
CREATE hola-mundo/.editorconfig (274 bytes)
CREATE hola-mundo/.gitignore (548 bytes)
CREATE hola-mundo/angular.json (2807 bytes)
CREATE hola-mundo/package.json (1042 bytes)
CREATE hola-mundo/tsconfig.json (901 bytes)
CREATE hola-mundo/tsconfig.app.json (263 bytes)
CREATE hola-mundo/tsconfig.spec.json (273 bytes)
CREATE hola-mundo/src/favicon.ico (948 bytes)
CREATE hola-mundo/src/index.html (296 bytes)
CREATE hola-mundo/src/main.ts (214 bytes)
CREATE hola-mundo/src/styles.css (80 bytes)
CREATE hola-mundo/src/app/app.module.ts (314 bytes)
CREATE hola-mundo/src/app/app.component.ts (218 bytes)
CREATE hola-mundo/src/app/app.component.html (23115 bytes)
CREATE hola-mundo/src/app/app.component.css (0 bytes)
CREATE hola-mundo/src/app/app.component.spec.ts (926 bytes)
✔ Packages installed successfully.
    Successfully initialized git.
```

#### Verificación

```bash
# Confirmar que el directorio del proyecto fue creado
ls
# En Windows: dir
# Salida esperada: hola-mundo  (directorio visible en la lista)
```

---

### Paso 3: Explorar la estructura del proyecto en Visual Studio Code

**Objetivo:** Abrir el proyecto en Visual Studio Code y comprender el propósito de cada archivo y carpeta generados por Angular CLI.

#### Instrucciones

1. Navega al directorio del proyecto:

```bash
cd hola-mundo
```

2. Abre el proyecto en Visual Studio Code:

```bash
code .
```

> **💡 Nota:** El comando `code .` abre VS Code con el directorio actual como workspace. Si el comando no es reconocido en macOS, abre VS Code manualmente, ve a **File → Open Folder** y selecciona la carpeta `hola-mundo`.

3. Una vez abierto VS Code, expande el árbol de archivos en el panel izquierdo (**Explorer**). Observa y localiza cada elemento de la siguiente tabla:

#### Estructura de archivos generada

```
hola-mundo/
├── src/
│   ├── app/
│   │   ├── app.component.css       ← Estilos específicos del componente raíz
│   │   ├── app.component.html      ← Template HTML del componente raíz
│   │   ├── app.component.spec.ts   ← Pruebas unitarias del componente raíz
│   │   ├── app.component.ts        ← Lógica TypeScript del componente raíz
│   │   └── app.module.ts           ← Módulo raíz de la aplicación (NgModule)
│   ├── assets/                     ← Archivos estáticos (imágenes, fuentes, etc.)
│   ├── favicon.ico                 ← Ícono de la pestaña del navegador
│   ├── index.html                  ← Punto de entrada HTML de la aplicación
│   ├── main.ts                     ← Punto de entrada TypeScript (bootstrap)
│   └── styles.css                  ← Estilos CSS globales de la aplicación
├── .editorconfig                   ← Configuración de formato del editor
├── .gitignore                      ← Archivos excluidos del control de versiones
├── angular.json                    ← Configuración del workspace de Angular CLI
├── package.json                    ← Dependencias NPM y scripts del proyecto
├── tsconfig.app.json               ← Configuración TypeScript para la app
├── tsconfig.json                   ← Configuración TypeScript base
└── tsconfig.spec.json              ← Configuración TypeScript para pruebas
```

4. Abre y examina cada uno de los siguientes archivos clave. Lee los comentarios de la tabla para entender su propósito:

| Archivo | Propósito principal |
|---------|---------------------|
| `src/index.html` | Documento HTML base. Contiene `<app-root>`, el selector del componente raíz donde Angular monta la aplicación |
| `src/main.ts` | Punto de entrada TypeScript. Llama a `platformBrowserDynamic().bootstrapModule(AppModule)` para iniciar la app |
| `src/app/app.module.ts` | Módulo raíz que declara componentes, importa módulos y configura providers |
| `src/app/app.component.ts` | Clase TypeScript del componente raíz con el decorador `@Component` |
| `src/app/app.component.html` | Template HTML del componente raíz (actualmente muestra el contenido por defecto de Angular) |
| `src/styles.css` | Estilos CSS globales aplicados a toda la aplicación |
| `angular.json` | Configuración del CLI: rutas de archivos, opciones de build, configuración de servidores |
| `package.json` | Lista de dependencias NPM, devDependencies y scripts (`ng serve`, `ng build`, etc.) |
| `tsconfig.json` | Opciones del compilador TypeScript: target, módulos, paths, etc. |

5. Haz clic en `src/app/app.component.ts` para abrirlo. Observa la estructura actual:

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'hola-mundo';
}
```

> **📝 Observación:** El decorador `@Component` define el selector CSS (`app-root`), la ruta del template HTML y la ruta de los estilos. La propiedad `title` es la que se usa en el template mediante interpolación.

6. Haz clic en `src/app/app.module.ts` para abrirlo y observa su estructura:

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

> **📝 Observación:** `AppModule` es el módulo raíz. La propiedad `bootstrap` indica a Angular qué componente debe renderizarse primero al iniciar la aplicación.

#### Verificación

Confirma que puedes abrir y leer sin errores los siguientes archivos en VS Code:
- [ ] `src/index.html`
- [ ] `src/main.ts`
- [ ] `src/app/app.module.ts`
- [ ] `src/app/app.component.ts`
- [ ] `angular.json`
- [ ] `package.json`

---

### Paso 4: Ejecutar el servidor de desarrollo

**Objetivo:** Iniciar el servidor de desarrollo de Angular y verificar que la aplicación por defecto se muestra correctamente en el navegador.

#### Instrucciones

1. En VS Code, abre una terminal integrada con **Terminal → New Terminal** (o `Ctrl+`` en Windows/Linux, `Cmd+`` en macOS`).

2. Asegúrate de que la terminal esté posicionada en el directorio del proyecto `hola-mundo`. Si no es así:

```bash
cd ~/angular-labs/hola-mundo
# En Windows: cd %USERPROFILE%\angular-labs\hola-mundo
```

3. Ejecuta el servidor de desarrollo con la opción `--open` para que abra el navegador automáticamente:

```bash
ng serve --open
```

4. Espera a que la compilación inicial termine. Verás una salida similar a:

```
Initial chunk files | Names         |  Raw size
main.js             | main          | 177.63 kB |
polyfills.js        | polyfills     |  83.00 kB |
styles.css, ...     | styles        |   0 bytes |

                    | Initial total | 260.63 kB

Application bundle generation complete. [4.521 seconds]

Watch mode enabled. Watching for file changes...
  ➜  Local:   http://localhost:4200/
  ➜  Network: http://192.168.x.x:4200/
```

5. Chrome se abrirá automáticamente (o navega manualmente a `http://localhost:4200`) y verás la página de bienvenida por defecto de Angular.

> **⚠️ Importante:** No cierres la terminal mientras trabajas. El servidor de desarrollo debe permanecer en ejecución. Puedes abrir una segunda terminal en VS Code con el botón **+** en el panel de terminales para ejecutar otros comandos.

#### Salida esperada

En el navegador deberías ver la página de bienvenida de Angular con el logo del framework, el nombre del proyecto y varios enlaces a recursos de documentación.

#### Verificación

- [ ] La terminal muestra `Application bundle generation complete` sin errores
- [ ] El navegador abre automáticamente `http://localhost:4200`
- [ ] Se visualiza la página de bienvenida de Angular (con el logo angular y el texto `hola-mundo app is running!`)
- [ ] La consola de Chrome DevTools (F12 → Console) no muestra errores en rojo

---

### Paso 5: Modificar AppComponent para mostrar "Hola Mundo"

**Objetivo:** Personalizar el componente raíz para mostrar un mensaje de "Hola Mundo" con tu nombre, observando el hot reload automático de Angular.

#### Instrucciones

1. En VS Code, abre el archivo `src/app/app.component.ts`.

2. Modifica la propiedad `title` para incluir tu nombre. Reemplaza `[Tu Nombre]` con tu nombre real:

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'Hola Mundo';
  nombre = 'María García';  // ← Reemplaza con tu nombre completo
  mensaje = '¡Bienvenido/a a Angular!';
}
```

3. Guarda el archivo con **Ctrl+S** (Windows/Linux) o **Cmd+S** (macOS).

4. Ahora abre el archivo `src/app/app.component.html`. **Selecciona todo el contenido** (Ctrl+A o Cmd+A) y **reemplázalo completamente** con el siguiente código:

```html
<!-- app.component.html -->
<div class="contenedor">
  <header class="encabezado">
    <h1>{{ title }}</h1>
    <h2>{{ nombre }}</h2>
  </header>

  <main class="contenido">
    <p class="mensaje-bienvenida">{{ mensaje }}</p>
    <p class="info-tecnica">
      Este proyecto fue creado con <strong>Angular CLI 17</strong>
      y ejecutado sobre <strong>Node.js 20 LTS</strong>.
    </p>
  </main>

  <footer class="pie-pagina">
    <p>Laboratorio 02-00-02 — Curso de Angular</p>
  </footer>
</div>
```

5. Guarda el archivo.

6. Abre el archivo `src/app/app.component.css` y agrega los siguientes estilos:

```css
/* app.component.css */

.contenedor {
  font-family: 'Segoe UI', Arial, sans-serif;
  max-width: 800px;
  margin: 40px auto;
  padding: 20px;
  text-align: center;
}

.encabezado {
  background-color: #1976d2;
  color: white;
  padding: 30px 20px;
  border-radius: 8px 8px 0 0;
}

.encabezado h1 {
  font-size: 2.5rem;
  margin: 0 0 10px 0;
}

.encabezado h2 {
  font-size: 1.4rem;
  font-weight: 300;
  margin: 0;
  opacity: 0.9;
}

.contenido {
  background-color: #f5f5f5;
  padding: 30px 20px;
  border-left: 1px solid #ddd;
  border-right: 1px solid #ddd;
}

.mensaje-bienvenida {
  font-size: 1.3rem;
  color: #333;
  margin-bottom: 15px;
}

.info-tecnica {
  font-size: 0.95rem;
  color: #666;
}

.pie-pagina {
  background-color: #1976d2;
  color: white;
  padding: 15px;
  border-radius: 0 0 8px 8px;
  font-size: 0.85rem;
  opacity: 0.85;
}
```

7. Guarda el archivo CSS.

8. Observa la terminal donde se ejecuta `ng serve`. Verás que Angular detecta los cambios y recompila automáticamente:

```
File change detected. Starting incremental compilation...
Compilation complete. Watching for file changes...
```

#### Salida esperada

En el navegador (sin necesidad de recargar manualmente), la aplicación se actualizará automáticamente mostrando:

- Un encabezado azul con el texto **"Hola Mundo"** en grande
- Tu nombre debajo del título
- El mensaje de bienvenida en la sección central
- Un pie de página con la información del laboratorio

> **📝 Concepto clave — Hot Reload:** Angular CLI monitorea los archivos del proyecto en tiempo real. Cuando detecta un cambio y lo guarda, recompila automáticamente los módulos afectados y actualiza el navegador sin necesidad de recargar manualmente la página. Este mecanismo se llama **Hot Module Replacement (HMR)** o simplemente "hot reload".

#### Verificación

- [ ] El navegador muestra el título "Hola Mundo" sin recargar manualmente
- [ ] Tu nombre aparece correctamente bajo el título
- [ ] Los estilos CSS se aplicaron (fondo azul en encabezado, fondo gris en contenido)
- [ ] La interpolación `{{ title }}`, `{{ nombre }}` y `{{ mensaje }}` funciona correctamente
- [ ] No hay errores en la consola de Chrome DevTools

---

### Paso 6: Examinar los archivos de configuración clave

**Objetivo:** Leer e interpretar los archivos de configuración principales del proyecto para comprender cómo Angular CLI gestiona el workspace.

#### Instrucciones

1. Abre `angular.json` en VS Code y localiza las siguientes secciones. No es necesario modificar nada, solo leer y comprender:

```jsonc
// angular.json — fragmento relevante (simplificado)
{
  "$schema": "./node_modules/@angular/cli/lib/config/schema.json",
  "version": 1,
  "projects": {
    "hola-mundo": {                          // ← Nombre del proyecto
      "projectType": "application",
      "architect": {
        "build": {
          "builder": "@angular-devkit/build-angular:browser",
          "options": {
            "outputPath": "dist/hola-mundo", // ← Carpeta de salida del build
            "index": "src/index.html",       // ← Punto de entrada HTML
            "main": "src/main.ts",           // ← Punto de entrada TypeScript
            "styles": ["src/styles.css"],    // ← Estilos globales
            "assets": ["src/favicon.ico", "src/assets"]  // ← Archivos estáticos
          }
        },
        "serve": {
          "options": {
            "port": 4200                     // ← Puerto del servidor de desarrollo
          }
        }
      }
    }
  }
}
```

2. Abre `package.json` y observa las secciones principales:

```json
{
  "name": "hola-mundo",
  "version": "0.0.0",
  "scripts": {
    "ng": "ng",
    "start": "ng serve",
    "build": "ng build",
    "watch": "ng build --watch --configuration development",
    "test": "ng test"
  },
  "dependencies": {
    "@angular/animations": "^17.x.x",
    "@angular/common": "^17.x.x",
    "@angular/compiler": "^17.x.x",
    "@angular/core": "^17.x.x",
    "@angular/forms": "^17.x.x",
    "@angular/platform-browser": "^17.x.x",
    "@angular/platform-browser-dynamic": "^17.x.x",
    "@angular/router": "^17.x.x",
    "rxjs": "~7.8.x",
    "tslib": "^2.x.x",
    "zone.js": "~0.14.x"
  },
  "devDependencies": {
    "@angular-devkit/build-angular": "^17.x.x",
    "@angular/cli": "^17.x.x",
    "@angular/compiler-cli": "^17.x.x",
    "typescript": "~5.x.x"
  }
}
```

> **📝 Observación:** Las `dependencies` son los paquetes necesarios en producción (el framework Angular, RxJS, etc.). Las `devDependencies` son herramientas que solo se necesitan durante el desarrollo (Angular CLI, compilador, TypeScript).

3. Abre `tsconfig.json` y observa las opciones del compilador TypeScript:

```jsonc
{
  "compileOnSave": false,
  "compilerOptions": {
    "baseUrl": "./",
    "outDir": "./dist/out-tsc",
    "strict": true,           // ← Modo estricto de TypeScript habilitado
    "noImplicitOverride": true,
    "noPropertyAccessFromIndexSignature": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "esModuleInterop": true,
    "sourceMap": true,
    "declaration": false,
    "experimentalDecorators": true,  // ← Necesario para decoradores Angular (@Component, etc.)
    "moduleResolution": "bundler",
    "importHelpers": true,
    "target": "ES2022",       // ← Versión de JavaScript de salida
    "module": "ES2022",
    "useDefineForClassFields": false,
    "lib": ["ES2022", "dom"]  // ← Librerías de tipos disponibles
  }
}
```

> **📝 Observación:** `experimentalDecorators: true` es fundamental para Angular, ya que todo el framework se basa en decoradores TypeScript como `@Component`, `@NgModule`, `@Injectable`, etc.

#### Verificación

Responde mentalmente (o en tu cuaderno) las siguientes preguntas para confirmar tu comprensión:

- [ ] ¿En qué carpeta se generará el build de producción según `angular.json`?
- [ ] ¿Cuál es la diferencia entre `dependencies` y `devDependencies` en `package.json`?
- [ ] ¿Por qué es necesaria la opción `experimentalDecorators: true` en `tsconfig.json`?

---

### Paso 7: Ejecutar el build de producción

**Objetivo:** Compilar la aplicación para producción con `ng build` y explorar los artefactos generados en la carpeta `dist/`.

#### Instrucciones

1. Abre una **segunda terminal** en VS Code (botón **+** en el panel de terminales) para no interrumpir el servidor de desarrollo que sigue corriendo.

2. Asegúrate de estar en el directorio del proyecto:

```bash
# Confirmar ubicación
pwd
# Salida esperada: .../angular-labs/hola-mundo
```

3. Ejecuta el build de producción:

```bash
ng build
```

4. Espera a que el proceso termine. Puede tomar entre **30 segundos y 2 minutos**. Verás una salida similar a:

```
Application bundle generation complete.

Initial chunk files           | Names         |  Raw size | Estimated transfer size
main-XXXXXXXX.js              | main          | 177.63 kB |                52.03 kB
polyfills-XXXXXXXX.js         | polyfills     |  83.00 kB |                23.01 kB
runtime-XXXXXXXX.js           | runtime       |   2.84 kB |                 1.37 kB
styles-XXXXXXXX.css           | styles        |   0 bytes |                 0 bytes

                              | Initial total | 263.47 kB |                76.41 kB

Application bundle generation complete. [12.543 seconds]
```

5. Explora la carpeta `dist/` generada. En la terminal, ejecuta:

```bash
# En macOS/Linux
ls -la dist/hola-mundo/browser/

# En Windows PowerShell
Get-ChildItem dist\hola-mundo\browser\
```

6. Observa los archivos generados. Deberías ver algo similar a:

```
dist/
└── hola-mundo/
    └── browser/
        ├── favicon.ico
        ├── index.html
        ├── main-XXXXXXXX.js          ← Código de la aplicación (minificado)
        ├── polyfills-XXXXXXXX.js     ← Polyfills para compatibilidad de navegadores
        ├── runtime-XXXXXXXX.js       ← Runtime de webpack
        └── styles-XXXXXXXX.css       ← Estilos CSS globales compilados
```

> **📝 Observación:** Los nombres de archivo incluyen un **hash** (ej. `main-a1b2c3d4.js`). Este hash cambia cada vez que el contenido del archivo cambia, lo que invalida el caché del navegador automáticamente y garantiza que los usuarios siempre reciban la versión más reciente. Esta técnica se llama **cache busting**.

7. Abre el archivo `dist/hola-mundo/browser/index.html` en VS Code y observa cómo Angular inyectó automáticamente las referencias a los archivos JavaScript y CSS generados.

8. (Opcional) Abre uno de los archivos `.js` generados en VS Code. Observa que el código está **minificado** (comprimido, sin espacios ni nombres legibles). Esto reduce el tamaño de los archivos para mejorar el tiempo de carga en producción.

#### Salida esperada

- La carpeta `dist/hola-mundo/browser/` existe y contiene los archivos listados arriba
- No hay errores en la salida del comando `ng build`
- Los archivos `.js` están minificados (el contenido no es legible directamente)

#### Verificación

- [ ] El comando `ng build` completó sin errores
- [ ] La carpeta `dist/hola-mundo/browser/` fue creada con los artefactos
- [ ] Los archivos JavaScript tienen hashes en sus nombres
- [ ] El archivo `index.html` en `dist/` referencia correctamente los archivos generados

---

### Paso 8: Verificar la aplicación con Angular DevTools

**Objetivo:** Usar la extensión Angular DevTools de Chrome para inspeccionar el árbol de componentes de la aplicación.

#### Instrucciones

1. Regresa al navegador Chrome con la aplicación corriendo en `http://localhost:4200` (servidor de desarrollo del Paso 4).

2. Abre las herramientas de desarrollador de Chrome con **F12** o **Ctrl+Shift+I** (Windows/Linux) / **Cmd+Option+I** (macOS).

3. En la barra de pestañas de DevTools, busca la pestaña **"Angular"** (instalada por la extensión Angular DevTools). Si no aparece, haz clic en el botón **»** para ver más pestañas.

4. En la pestaña Angular, observa el árbol de componentes:

```
AppComponent
  └── (sin componentes hijos en este proyecto simple)
```

5. Haz clic sobre `AppComponent` en el árbol. En el panel derecho observarás las propiedades del componente:

```
Properties:
  title: "Hola Mundo"
  nombre: "María García"    ← (o el nombre que ingresaste)
  mensaje: "¡Bienvenido/a a Angular!"
```

6. (Opcional) Modifica el valor de `title` directamente desde Angular DevTools haciendo clic en el valor y escribiendo un nuevo texto. Observa cómo el navegador se actualiza instantáneamente.

#### Verificación

- [ ] La pestaña "Angular" aparece en Chrome DevTools
- [ ] Se visualiza `AppComponent` en el árbol de componentes
- [ ] Las propiedades `title`, `nombre` y `mensaje` muestran los valores correctos

---

## 7. Validación y Pruebas

Al finalizar todos los pasos, verifica que tu laboratorio está completo revisando cada punto:

### Lista de verificación final

| # | Verificación | Estado |
|---|-------------|--------|
| 1 | El proyecto `hola-mundo` fue creado con `ng new` sin errores | ☐ |
| 2 | La estructura de archivos coincide con la descrita en el Paso 3 | ☐ |
| 3 | El servidor de desarrollo responde en `http://localhost:4200` | ☐ |
| 4 | La aplicación muestra "Hola Mundo" y tu nombre en el navegador | ☐ |
| 5 | Los estilos CSS se aplicaron correctamente (encabezado azul) | ☐ |
| 6 | El hot reload funcionó al guardar cambios (sin recargar manualmente) | ☐ |
| 7 | `ng build` completó sin errores y generó la carpeta `dist/` | ☐ |
| 8 | Angular DevTools muestra `AppComponent` con las propiedades correctas | ☐ |

### Prueba de regresión rápida

Realiza la siguiente prueba para confirmar que todo funciona correctamente:

1. Con el servidor de desarrollo corriendo, abre `src/app/app.component.ts`
2. Cambia el valor de `mensaje` a `'¡Angular es increíble!'`
3. Guarda el archivo
4. Verifica que el navegador se actualiza automáticamente mostrando el nuevo mensaje
5. Revierte el cambio al valor original y guarda nuevamente

Si la actualización automática funciona, el entorno de desarrollo está configurado correctamente.

---

## 8. Solución de Problemas

### Problema 1: El puerto 4200 ya está en uso

**Síntoma:**

Al ejecutar `ng serve`, la terminal muestra el siguiente error:

```
Port 4200 is already in use. Use '--port' to specify a different port.
Error: listen EADDRINUSE: address already in use :::4200
```

**Causa:**

Otro proceso (posiblemente una instancia anterior de `ng serve` que no se cerró correctamente, o una aplicación diferente) está usando el puerto 4200.

**Solución:**

**Opción A — Usar un puerto diferente:**
```bash
ng serve --open --port 4201
# La aplicación estará disponible en http://localhost:4201
```

**Opción B — Identificar y terminar el proceso que usa el puerto 4200:**

En macOS/Linux:
```bash
# Identificar el proceso
lsof -ti:4200

# Terminar el proceso (reemplaza PID con el número obtenido)
kill -9 PID
```

En Windows (PowerShell como Administrador):
```powershell
# Identificar el proceso
netstat -ano | findstr :4200

# Terminar el proceso (reemplaza PID con el número obtenido)
taskkill /PID <PID> /F
```

Después de terminar el proceso, ejecuta `ng serve --open` nuevamente.

---

### Problema 2: Error de compilación TypeScript al modificar app.component.ts

**Síntoma:**

Al guardar cambios en `app.component.ts`, la terminal muestra errores similares a:

```
✖ Failed to compile.

src/app/app.component.ts:9:3 - error TS2322: Type 'number' is not assignable to type 'string'.

9   nombre = 123;
    ~~~~~~
```

O en el navegador aparece una pantalla roja con el mensaje de error de compilación.

**Causa:**

TypeScript está configurado en modo estricto (`"strict": true` en `tsconfig.json`). Esto significa que el compilador infiere el tipo de las propiedades basándose en su valor inicial y no permite asignar valores de tipos incompatibles. Por ejemplo, si `nombre` fue inicializado como `string`, no se puede reasignar un valor `number`.

**Solución:**

Revisa el archivo `app.component.ts` y asegúrate de que los valores asignados a las propiedades sean del tipo correcto:

```typescript
// ❌ Incorrecto — TypeScript infiere 'nombre' como string, no acepta número
nombre = 123;

// ✅ Correcto — valor string entre comillas
nombre = 'María García';
```

Si necesitas declarar explícitamente el tipo de una propiedad:

```typescript
// Declaración explícita de tipo
nombre: string = 'María García';
titulo: string = 'Hola Mundo';
contador: number = 0;
activo: boolean = true;
```

Guarda el archivo corregido. Angular CLI recompilará automáticamente y el error desaparecerá.

---

## 9. Limpieza

Al finalizar el laboratorio, sigue estos pasos para dejar el entorno ordenado:

1. **Detener el servidor de desarrollo:** En la terminal donde se ejecuta `ng serve`, presiona **Ctrl+C** y confirma con `S` (Windows) o simplemente `Ctrl+C` (macOS/Linux).

```bash
# Salida al detener el servidor
^C
```

2. **Conservar el proyecto:** El directorio `angular-labs/hola-mundo/` debe **conservarse** ya que puede ser referenciado en laboratorios futuros del curso.

3. **Cerrar terminales adicionales:** Cierra cualquier terminal secundaria abierta durante el laboratorio.

4. **Guardar el trabajo en Git** (opcional pero recomendado):

```bash
# Desde el directorio hola-mundo
git add .
git commit -m "Lab 02-00-02: Proyecto Hola Mundo completado"
```

> **💡 Nota:** Angular CLI inicializa un repositorio Git automáticamente al crear el proyecto (`Successfully initialized git.`), por lo que el directorio ya está bajo control de versiones.

5. **Verificar que no quedan procesos de Node.js activos** (opcional):

```bash
# En macOS/Linux
ps aux | grep node

# En Windows PowerShell
Get-Process node
```

Si aparecen procesos de Node.js que no reconoces, puedes terminarlos con `kill <PID>` (macOS/Linux) o `Stop-Process -Id <PID>` (Windows).

---

## 10. Resumen

En este laboratorio completaste con éxito los siguientes logros:

| Actividad | Herramienta/Concepto |
|-----------|---------------------|
| Creación del proyecto con opciones configuradas | `ng new --routing=false --style=css --no-standalone` |
| Exploración de la arquitectura de archivos Angular | Estructura `src/app/`, `angular.json`, `package.json`, `tsconfig.json` |
| Ejecución del servidor de desarrollo | `ng serve --open` → `http://localhost:4200` |
| Personalización del componente raíz | `AppComponent`, interpolación `{{ }}`, hot reload |
| Build de producción y análisis de artefactos | `ng build` → carpeta `dist/` con archivos minificados y hasheados |
| Inspección con Angular DevTools | Árbol de componentes, propiedades en tiempo real |

### Conexión con la lección teórica

Este laboratorio pone en práctica el rol de **Node.js** descrito en la Lección 2.1: Node.js no ejecuta la aplicación Angular final (eso lo hace el navegador), sino que actúa como la **plataforma de soporte** que hace posible Angular CLI (`ng new`, `ng serve`, `ng build`), la gestión de dependencias con NPM (`node_modules/`) y el servidor de desarrollo local en `localhost:4200`. Cada vez que ejecutaste un comando `ng`, fue Node.js quien lo procesó en segundo plano.

### Recursos adicionales

- [Documentación oficial de Angular CLI — ng new](https://angular.dev/cli/new)
- [Guía de estructura de proyectos Angular](https://angular.dev/reference/configs/file-structure)
- [Documentación de Angular DevTools](https://angular.dev/tools/devtools)
- [Referencia de angular.json](https://angular.dev/reference/configs/workspace-config)
- [Guía de TypeScript para Angular](https://angular.dev/guide/typescript-configuration)

---

> **📌 Próximo laboratorio:** En el Laboratorio 02-00-03 explorarás NPM en profundidad, aprenderás a gestionar dependencias del proyecto y comprenderás cómo el ecosistema de paquetes potencia el desarrollo con Angular.
