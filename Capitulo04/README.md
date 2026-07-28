# Crear un componente simple que muestre el nombre de un usuario en la página web de la aplicación

## Metadatos

| Campo        | Detalle                          |
|--------------|----------------------------------|
| **Duración** | 49 minutos                       |
| **Complejidad** | Media                         |
| **Nivel Bloom** | Crear (Create)               |
| **Módulo**   | 4 — Angular CLI y Arquitectura de Componentes |
| **Versión Angular** | 17.x (modo NgModule)    |

---

## Descripción General

En esta práctica construirás una pequeña aplicación Angular que muestra una tarjeta de perfil de usuario en el navegador. Comenzarás creando un proyecto desde cero con Angular CLI, generarás un componente `usuario-perfil` y un servicio `usuario`, y conectarás ambos mediante inyección de dependencias. Al finalizar, habrás recorrido el ciclo completo de un componente Angular: decorador `@Component`, clase TypeScript con propiedades tipadas, template HTML con interpolación y comunicación con un servicio `@Injectable`.

---

## Objetivos de Aprendizaje

Al completar este laboratorio serás capaz de:

- [ ] Crear un nuevo proyecto Angular con Angular CLI usando las opciones `--routing=false --style=css`.
- [ ] Generar un componente y un servicio con `ng generate` e identificar los archivos producidos por cada comando.
- [ ] Definir propiedades tipadas en la clase del componente y mostrarlas en el template mediante interpolación `{{ }}`.
- [ ] Implementar un servicio con `@Injectable` que retorne un objeto tipado y consumirlo desde un componente mediante inyección de dependencias en el constructor.
- [ ] Verificar el árbol de componentes y las propiedades en tiempo de ejecución usando Angular DevTools.

---

## Prerrequisitos

### Conocimientos previos

| Tema | Nivel requerido |
|------|----------------|
| Laboratorio 02-00-02 completado (entorno Angular funcional) | Obligatorio |
| Laboratorio 03-00-01 completado (TypeScript básico: clases, propiedades, métodos) | Obligatorio |
| HTML5 básico (etiquetas semánticas, estructura de tarjeta) | Obligatorio |
| Conceptos de módulos y decoradores en TypeScript | Recomendado |

### Acceso y herramientas

| Herramienta | Versión mínima | Verificación |
|-------------|---------------|--------------|
| Node.js LTS | 18.x (recomendado 20.x) | `node -v` |
| npm | 9.x (recomendado 10.x) | `npm -v` |
| Angular CLI | 16.x (recomendado 17.x) | `ng version` |
| Visual Studio Code | 1.85.x | — |
| Google Chrome | 120.x | — |
| Angular DevTools (extensión Chrome) | Última disponible | Chrome Web Store |

---

## Entorno de Laboratorio

### Hardware recomendado

| Recurso | Mínimo | Recomendado |
|---------|--------|-------------|
| RAM | 8 GB | 16 GB |
| Almacenamiento libre | 10 GB | 15 GB |
| Procesador | Core i5 / 1.6 GHz 64-bit | Core i7 / 2.0 GHz |
| Resolución de pantalla | 1280 × 768 | 1920 × 1080 |
| Conexión a Internet | 10 Mbps | 20 Mbps |

### Verificación del entorno antes de comenzar

Abre una terminal y ejecuta los siguientes comandos para confirmar que el entorno está listo:

```bash
# Verificar Node.js
node -v
# Salida esperada: v20.x.x (o v18.x.x como mínimo)

# Verificar npm
npm -v
# Salida esperada: 10.x.x

# Verificar Angular CLI
ng version
# Salida esperada: Angular CLI: 17.x.x
```

> **Nota para macOS/Linux:** Si `ng version` produce un error de permisos, asegúrate de haber configurado el prefijo global de npm:
> ```bash
> npm config set prefix ~/.npm-global
> export PATH="$HOME/.npm-global/bin:$PATH"
> ```

> **Nota para Windows (PowerShell):** Si aparece un error de ejecución de scripts, ejecuta PowerShell como administrador y usa:
> ```powershell
> Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
> ```

---

## Pasos del Laboratorio

### Paso 1 — Crear el proyecto Angular

**Objetivo:** Inicializar un nuevo proyecto Angular llamado `app-usuario` usando Angular CLI con las opciones adecuadas para este laboratorio.

#### Instrucciones

1. Abre una terminal (CMD, PowerShell, Bash o Zsh según tu sistema operativo).

2. Navega al directorio donde deseas crear el proyecto (por ejemplo, tu carpeta de laboratorios del curso):

   ```bash
   # En Windows
   cd C:\cursos\angular\labs

   # En macOS/Linux
   cd ~/cursos/angular/labs
   ```

3. Ejecuta el siguiente comando para crear el proyecto. El flag `--no-standalone` asegura que se use la arquitectura tradicional con `NgModule`, recomendada para este curso introductorio:

   ```bash
   ng new app-usuario --routing=false --style=css --no-standalone
   ```

4. Angular CLI mostrará un asistente. Cuando pregunte `? Would you like to share pseudonymous usage data...`, escribe `N` y presiona **Enter**.

5. Espera a que Angular CLI descargue e instale todas las dependencias npm. Este proceso puede tomar entre 1 y 3 minutos dependiendo de tu conexión.

6. Una vez finalizado, ingresa al directorio del proyecto:

   ```bash
   cd app-usuario
   ```

7. Abre el proyecto en Visual Studio Code:

   ```bash
   code .
   ```

#### Salida esperada

```
✔ Packages installed successfully.
    Successfully initialized git.
```

La estructura de carpetas visible en VS Code debe incluir:
```
app-usuario/
├── src/
│   ├── app/
│   │   ├── app.component.css
│   │   ├── app.component.html
│   │   ├── app.component.spec.ts
│   │   ├── app.component.ts
│   │   └── app.module.ts
│   ├── index.html
│   └── main.ts
├── angular.json
├── package.json
└── tsconfig.json
```

#### Verificación

En la terminal, dentro del directorio `app-usuario`, ejecuta:

```bash
ng serve --open
```

El navegador debe abrirse automáticamente en `http://localhost:4200` y mostrar la página de bienvenida predeterminada de Angular con el logo y el título "app-usuario app is running!". Detén el servidor con **Ctrl + C** antes de continuar al siguiente paso.

---

### Paso 2 — Explorar la estructura del proyecto generado

**Objetivo:** Comprender el propósito de los archivos clave generados por `ng new` antes de modificarlos.

#### Instrucciones

1. En VS Code, abre el archivo `src/app/app.module.ts`. Observa que contiene el decorador `@NgModule` con las propiedades `declarations`, `imports`, `providers` y `bootstrap`. Este es el módulo raíz de la aplicación.

2. Abre `src/app/app.component.ts`. Identifica:
   - El decorador `@Component` con las propiedades `selector`, `templateUrl` y `styleUrls`.
   - La clase `AppComponent` con la propiedad `title`.

3. Abre `src/app/app.component.html`. Observa la interpolación `{{ title }}` que muestra el valor de la propiedad `title` definida en la clase.

4. Abre `angular.json` y localiza la sección `"architect" > "build" > "options"`. Observa las propiedades `outputPath`, `index` y `main` que definen las rutas de compilación.

> **Punto de reflexión:** El archivo `app.module.ts` es el registro central de la aplicación. Cada componente que generes con `ng generate` será automáticamente declarado aquí. Esta es una de las ventajas clave de Angular CLI.

#### Verificación

Responde mentalmente (o en tu cuaderno) las siguientes preguntas antes de continuar:
- ¿Qué propiedad del decorador `@Component` define el nombre de la etiqueta HTML del componente?
- ¿En qué array de `@NgModule` se registran los componentes?

---

### Paso 3 — Generar el componente `usuario-perfil`

**Objetivo:** Usar `ng generate component` para crear el componente principal del laboratorio y explorar los 4 archivos generados.

#### Instrucciones

1. Asegúrate de estar en el directorio raíz del proyecto (`app-usuario`). En la terminal ejecuta:

   ```bash
   ng generate component usuario-perfil
   ```

   > **Forma abreviada equivalente:** `ng g c usuario-perfil`

2. Observa la salida en la terminal. Angular CLI debe mostrar los 4 archivos creados y la actualización del módulo.

3. En VS Code, navega a `src/app/usuario-perfil/`. Abre cada uno de los 4 archivos y examina su contenido inicial:

   - **`usuario-perfil.component.ts`** — Clase del componente con decorador `@Component`.
   - **`usuario-perfil.component.html`** — Template HTML con contenido de marcador de posición.
   - **`usuario-perfil.component.css`** — Archivo de estilos vacío (con alcance al componente).
   - **`usuario-perfil.component.spec.ts`** — Archivo de pruebas unitarias (no se modificará en este lab).

4. Abre `src/app/app.module.ts` y verifica que Angular CLI haya agregado automáticamente `UsuarioPerfilComponent` en el array `declarations`.

#### Salida esperada en la terminal

```
CREATE src/app/usuario-perfil/usuario-perfil.component.css (0 bytes)
CREATE src/app/usuario-perfil/usuario-perfil.component.html (28 bytes)
CREATE src/app/usuario-perfil/usuario-perfil.component.spec.ts (... bytes)
CREATE src/app/usuario-perfil/usuario-perfil.component.ts (... bytes)
UPDATE src/app/app.module.ts (... bytes)
```

#### Verificación

Abre `src/app/app.module.ts` y confirma que el archivo contiene:

```typescript
import { UsuarioPerfilComponent } from './usuario-perfil/usuario-perfil.component';

@NgModule({
  declarations: [
    AppComponent,
    UsuarioPerfilComponent   // ← debe estar presente
  ],
  ...
})
```

---

### Paso 4 — Definir la interfaz de datos del usuario

**Objetivo:** Crear una interfaz TypeScript que describa la forma del objeto de datos del usuario, aplicando tipado estático.

#### Instrucciones

1. En la terminal, crea manualmente el archivo de la interfaz. Primero crea la carpeta `models`:

   ```bash
   # En Windows (CMD)
   mkdir src\app\models

   # En macOS/Linux
   mkdir -p src/app/models
   ```

2. En VS Code, dentro de `src/app/models/`, crea un nuevo archivo llamado `usuario.model.ts`.

3. Escribe el siguiente contenido en el archivo:

   ```typescript
   // src/app/models/usuario.model.ts

   export interface Usuario {
     nombre: string;
     apellido: string;
     edad: number;
     profesion: string;
     activo: boolean;
   }
   ```

> **¿Por qué una interfaz?** Las interfaces de TypeScript no generan código JavaScript en tiempo de ejecución; solo existen en tiempo de compilación para garantizar que los objetos tengan la forma correcta. Esto es una buena práctica que evita errores difíciles de detectar.

#### Verificación

Guarda el archivo (`Ctrl + S`). VS Code no debe mostrar ningún error de TypeScript en el archivo. El ícono del archivo en el explorador no debe tener indicadores de error (puntos rojos).

---

### Paso 5 — Generar y configurar el servicio `usuario`

**Objetivo:** Crear un servicio Angular que centralice los datos del usuario y exponga un método `getUsuario()` con retorno tipado.

#### Instrucciones

1. En la terminal, ejecuta el siguiente comando para generar el servicio dentro de una subcarpeta `services`:

   ```bash
   ng generate service services/usuario
   ```

   > **Forma abreviada equivalente:** `ng g s services/usuario`

2. Angular CLI creará dos archivos:
   - `src/app/services/usuario.service.ts`
   - `src/app/services/usuario.service.spec.ts`

3. Abre `src/app/services/usuario.service.ts`. Reemplaza todo su contenido con el siguiente código:

   ```typescript
   // src/app/services/usuario.service.ts

   import { Injectable } from '@angular/core';
   import { Usuario } from '../models/usuario.model';

   @Injectable({
     providedIn: 'root'   // El servicio estará disponible en toda la aplicación
   })
   export class UsuarioService {

     /**
      * Retorna un objeto Usuario con datos de ejemplo.
      * En una aplicación real, este método haría una llamada HTTP.
      */
     getUsuario(): Usuario {
       return {
         nombre: 'Ana García',
         apellido: 'López',
         edad: 28,
         profesion: 'Desarrolladora Frontend',
         activo: true
       };
     }
   }
   ```

4. Guarda el archivo con **Ctrl + S**.

> **Nota sobre `providedIn: 'root'`:** Este parámetro del decorador `@Injectable` registra el servicio en el inyector raíz de la aplicación, lo que significa que Angular creará una única instancia compartida (singleton) disponible para cualquier componente. No es necesario agregarlo manualmente al array `providers` de `AppModule`.

#### Salida esperada en la terminal

```
CREATE src/app/services/usuario.service.spec.ts (... bytes)
CREATE src/app/services/usuario.service.ts (... bytes)
```

#### Verificación

En VS Code, verifica que no haya errores de TypeScript (líneas rojas onduladas) en `usuario.service.ts`. El decorador `@Injectable` debe importarse correctamente desde `@angular/core`.

---

### Paso 6 — Implementar la clase del componente `UsuarioPerfilComponent`

**Objetivo:** Configurar la clase del componente para inyectar el servicio, definir propiedades tipadas e inicializar los datos en `ngOnInit()`.

#### Instrucciones

1. Abre `src/app/usuario-perfil/usuario-perfil.component.ts`.

2. Reemplaza todo el contenido del archivo con el siguiente código:

   ```typescript
   // src/app/usuario-perfil/usuario-perfil.component.ts

   import { Component, OnInit } from '@angular/core';
   import { Usuario } from '../models/usuario.model';
   import { UsuarioService } from '../services/usuario.service';

   @Component({
     selector: 'app-usuario-perfil',       // Etiqueta HTML para usar el componente
     templateUrl: './usuario-perfil.component.html',
     styleUrls: ['./usuario-perfil.component.css']
   })
   export class UsuarioPerfilComponent implements OnInit {

     // Propiedad que almacenará el objeto usuario recibido del servicio
     // El signo '!' indica a TypeScript que será inicializada antes de usarse
     usuario!: Usuario;

     // Propiedades individuales con valores por defecto (se sobreescriben en ngOnInit)
     nombre: string = '';
     apellido: string = '';
     edad: number = 0;
     profesion: string = '';
     activo: boolean = false;

     /**
      * Constructor: Angular inyecta automáticamente una instancia de UsuarioService.
      * La palabra clave 'private' crea la propiedad y la asigna en un solo paso.
      */
     constructor(private usuarioService: UsuarioService) {}

     /**
      * ngOnInit: Hook del ciclo de vida. Se ejecuta una vez que Angular
      * ha inicializado todas las propiedades del componente.
      * Es el lugar correcto para obtener datos iniciales.
      */
     ngOnInit(): void {
       // Llamar al servicio para obtener los datos del usuario
       this.usuario = this.usuarioService.getUsuario();

       // Asignar los valores a las propiedades individuales del componente
       this.nombre     = this.usuario.nombre;
       this.apellido   = this.usuario.apellido;
       this.edad       = this.usuario.edad;
       this.profesion  = this.usuario.profesion;
       this.activo     = this.usuario.activo;
     }
   }
   ```

3. Guarda el archivo con **Ctrl + S**.

> **¿Por qué `ngOnInit` y no el constructor?** El constructor de Angular se usa exclusivamente para la inyección de dependencias. La lógica de inicialización (como llamar a servicios) se coloca en `ngOnInit` porque en ese momento Angular garantiza que todas las propiedades de entrada (`@Input`) ya han sido asignadas. Esta es una convención fundamental en Angular.

#### Verificación

Confirma en VS Code que:
- No hay errores de TypeScript (líneas rojas).
- El autocompletado funciona al escribir `this.usuario.` (debe sugerir `nombre`, `apellido`, etc.).
- La clase implementa correctamente `OnInit` (importado desde `@angular/core`).

---

### Paso 7 — Diseñar el template HTML del componente

**Objetivo:** Crear la vista de la tarjeta de perfil usando HTML semántico e interpolación de datos `{{ }}`.

#### Instrucciones

1. Abre `src/app/usuario-perfil/usuario-perfil.component.html`.

2. Reemplaza todo el contenido con el siguiente template:

   ```html
   <!-- src/app/usuario-perfil/usuario-perfil.component.html -->

   <div class="perfil-card">

     <!-- Encabezado de la tarjeta -->
     <div class="perfil-header">
       <div class="perfil-avatar">
         <!-- Las iniciales se construyen tomando el primer carácter de nombre y apellido -->
         <span class="avatar-iniciales">
           {{ nombre.charAt(0) }}{{ apellido.charAt(0) }}
         </span>
       </div>
       <div class="perfil-nombre">
         <h2>{{ nombre }} {{ apellido }}</h2>
         <p class="perfil-profesion">{{ profesion }}</p>
       </div>
     </div>

     <!-- Separador visual -->
     <hr class="perfil-divider">

     <!-- Cuerpo de la tarjeta con detalles -->
     <div class="perfil-body">

       <div class="perfil-detalle">
         <span class="detalle-etiqueta">Nombre completo:</span>
         <span class="detalle-valor">{{ nombre }} {{ apellido }}</span>
       </div>

       <div class="perfil-detalle">
         <span class="detalle-etiqueta">Edad:</span>
         <span class="detalle-valor">{{ edad }} años</span>
       </div>

       <div class="perfil-detalle">
         <span class="detalle-etiqueta">Profesión:</span>
         <span class="detalle-valor">{{ profesion }}</span>
       </div>

       <div class="perfil-detalle">
         <span class="detalle-etiqueta">Estado:</span>
         <span class="detalle-valor estado-badge"
               [class.activo]="activo"
               [class.inactivo]="!activo">
           {{ activo ? 'Activo' : 'Inactivo' }}
         </span>
       </div>

     </div>

     <!-- Pie de la tarjeta -->
     <div class="perfil-footer">
       <small>Datos proporcionados por UsuarioService</small>
     </div>

   </div>
   ```

3. Guarda el archivo.

> **Nota sobre `[class.activo]` y `[class.inactivo]`:** Esta es la sintaxis de *class binding* de Angular. Agrega o quita la clase CSS dependiendo del valor booleano de la expresión. Es una forma limpia de aplicar estilos condicionales sin necesidad de lógica en el componente. La verás en profundidad en el módulo de directivas.

#### Verificación

Revisa que las expresiones de interpolación `{{ }}` referencien exactamente los nombres de propiedades definidas en la clase del componente (`nombre`, `apellido`, `edad`, `profesion`, `activo`). Un error tipográfico aquí no generará un error de compilación pero sí mostrará valores vacíos en el navegador.

---

### Paso 8 — Agregar estilos CSS al componente

**Objetivo:** Aplicar estilos encapsulados al componente para que la tarjeta de perfil tenga una apariencia profesional.

#### Instrucciones

1. Abre `src/app/usuario-perfil/usuario-perfil.component.css`.

2. Agrega el siguiente contenido:

   ```css
   /* src/app/usuario-perfil/usuario-perfil.component.css */

   /* Contenedor principal de la tarjeta */
   .perfil-card {
     max-width: 420px;
     margin: 40px auto;
     background-color: #ffffff;
     border-radius: 12px;
     box-shadow: 0 4px 16px rgba(0, 0, 0, 0.12);
     overflow: hidden;
     font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
   }

   /* Encabezado: avatar + nombre */
   .perfil-header {
     display: flex;
     align-items: center;
     gap: 16px;
     padding: 24px;
     background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
     color: white;
   }

   /* Círculo del avatar con iniciales */
   .perfil-avatar {
     width: 64px;
     height: 64px;
     border-radius: 50%;
     background-color: rgba(255, 255, 255, 0.25);
     display: flex;
     align-items: center;
     justify-content: center;
     flex-shrink: 0;
   }

   .avatar-iniciales {
     font-size: 1.6rem;
     font-weight: 700;
     color: white;
     text-transform: uppercase;
   }

   /* Nombre y profesión en el encabezado */
   .perfil-nombre h2 {
     margin: 0 0 4px 0;
     font-size: 1.2rem;
     font-weight: 600;
   }

   .perfil-profesion {
     margin: 0;
     font-size: 0.9rem;
     opacity: 0.85;
   }

   /* Separador */
   .perfil-divider {
     margin: 0;
     border: none;
     border-top: 1px solid #e9ecef;
   }

   /* Cuerpo con los detalles */
   .perfil-body {
     padding: 20px 24px;
     display: flex;
     flex-direction: column;
     gap: 12px;
   }

   /* Cada fila de detalle */
   .perfil-detalle {
     display: flex;
     justify-content: space-between;
     align-items: center;
     font-size: 0.95rem;
   }

   .detalle-etiqueta {
     color: #6c757d;
     font-weight: 500;
   }

   .detalle-valor {
     color: #212529;
     font-weight: 400;
   }

   /* Badge de estado */
   .estado-badge {
     padding: 3px 10px;
     border-radius: 12px;
     font-size: 0.82rem;
     font-weight: 600;
   }

   .activo {
     background-color: #d4edda;
     color: #155724;
   }

   .inactivo {
     background-color: #f8d7da;
     color: #721c24;
   }

   /* Pie de la tarjeta */
   .perfil-footer {
     padding: 12px 24px;
     background-color: #f8f9fa;
     text-align: center;
     color: #adb5bd;
     font-size: 0.8rem;
     border-top: 1px solid #e9ecef;
   }
   ```

3. Guarda el archivo.

> **Encapsulación de estilos en Angular:** Angular aplica automáticamente encapsulación de vista (*View Encapsulation*) a los estilos de cada componente. Esto significa que los estilos definidos en `usuario-perfil.component.css` solo afectarán al HTML de ese componente y no "escaparán" hacia otros componentes de la aplicación.

#### Verificación

No hay verificación en el navegador aún (el componente no está integrado en la app). Confirma que el archivo CSS fue guardado sin errores de sintaxis — VS Code resaltará en rojo cualquier propiedad CSS inválida.

---

### Paso 9 — Limpiar y actualizar el `AppComponent`

**Objetivo:** Eliminar el contenido predeterminado de `app.component.html` e integrar el componente `usuario-perfil` usando su selector.

#### Instrucciones

1. Abre `src/app/app.component.html`.

2. **Elimina todo el contenido** del archivo (que por defecto contiene el HTML de bienvenida de Angular, aproximadamente 500 líneas).

3. Reemplázalo con el siguiente contenido mínimo:

   ```html
   <!-- src/app/app.component.html -->

   <div class="app-container">
     <header class="app-header">
       <h1>{{ title }}</h1>
       <p>Sistema de Gestión de Usuarios</p>
     </header>

     <main class="app-main">
       <!-- Aquí se renderiza el componente usuario-perfil -->
       <!-- Angular reemplaza esta etiqueta con el template del componente -->
       <app-usuario-perfil></app-usuario-perfil>
     </main>

     <footer class="app-footer">
       <p>Laboratorio 04-00-01 — Angular Components</p>
     </footer>
   </div>
   ```

4. Abre `src/app/app.component.ts` y actualiza la propiedad `title`:

   ```typescript
   // src/app/app.component.ts
   import { Component } from '@angular/core';

   @Component({
     selector: 'app-root',
     templateUrl: './app.component.html',
     styleUrls: ['./app.component.css']
   })
   export class AppComponent {
     title = 'Perfil de Usuario';
   }
   ```

5. Abre `src/app/app.component.css` y agrega estilos básicos para el layout:

   ```css
   /* src/app/app.component.css */

   * {
     box-sizing: border-box;
     margin: 0;
     padding: 0;
   }

   body {
     background-color: #f0f2f5;
   }

   .app-container {
     min-height: 100vh;
     display: flex;
     flex-direction: column;
     background-color: #f0f2f5;
   }

   .app-header {
     background-color: #3f51b5;
     color: white;
     padding: 20px 32px;
     text-align: center;
   }

   .app-header h1 {
     font-size: 1.8rem;
     font-family: 'Segoe UI', sans-serif;
     margin-bottom: 4px;
   }

   .app-header p {
     font-size: 0.95rem;
     opacity: 0.8;
   }

   .app-main {
     flex: 1;
     padding: 20px;
   }

   .app-footer {
     background-color: #3f51b5;
     color: rgba(255, 255, 255, 0.7);
     text-align: center;
     padding: 12px;
     font-size: 0.8rem;
   }
   ```

6. Guarda todos los archivos modificados.

> **El selector `<app-usuario-perfil>`:** Corresponde exactamente a la propiedad `selector: 'app-usuario-perfil'` definida en el decorador `@Component` del componente. Angular busca esta etiqueta en el template de `AppComponent` y la reemplaza con el template de `UsuarioPerfilComponent` durante la compilación.

#### Verificación

En VS Code, confirma que:
- `app.component.html` contiene la etiqueta `<app-usuario-perfil></app-usuario-perfil>`.
- `app.component.ts` tiene `title = 'Perfil de Usuario'`.
- No hay errores de TypeScript en ninguno de los archivos modificados.

---

### Paso 10 — Ejecutar la aplicación y verificar en el navegador

**Objetivo:** Iniciar el servidor de desarrollo y confirmar que la tarjeta de perfil se muestra correctamente con los datos del servicio.

#### Instrucciones

1. En la terminal (asegúrate de estar en el directorio `app-usuario`), ejecuta:

   ```bash
   ng serve --open
   ```

2. El navegador se abrirá automáticamente en `http://localhost:4200`. Debes ver:
   - Un encabezado azul con el título "Perfil de Usuario".
   - Una tarjeta blanca con un avatar morado que muestra las iniciales "AL" (Ana López).
   - Los datos completos de Ana García López en la tarjeta.
   - Un badge verde que indica "Activo".
   - Un footer azul con el texto del laboratorio.

3. Abre las **Herramientas de Desarrollador** de Chrome (F12) y ve a la pestaña **Console**. Confirma que no hay errores en rojo.

4. En la barra de direcciones, confirma que la URL es `http://localhost:4200`.

#### Salida esperada en el navegador

La página debe mostrar una interfaz similar a esta estructura visual:

```
┌─────────────────────────────────────┐
│  Perfil de Usuario                  │  ← Header azul
│  Sistema de Gestión de Usuarios     │
├─────────────────────────────────────┤
│                                     │
│  ┌───────────────────────────────┐  │
│  │  [AL]  Ana García López       │  │  ← Header de tarjeta (gradiente morado)
│  │        Desarrolladora Frontend│  │
│  ├───────────────────────────────┤  │
│  │  Nombre completo: Ana García López │
│  │  Edad:            28 años     │  │
│  │  Profesión:       Desarrolladora Frontend │
│  │  Estado:          [Activo]    │  │  ← Badge verde
│  ├───────────────────────────────┤  │
│  │  Datos proporcionados por...  │  │
│  └───────────────────────────────┘  │
│                                     │
├─────────────────────────────────────┤
│  Laboratorio 04-00-01               │  ← Footer azul
└─────────────────────────────────────┘
```

#### Verificación

- [ ] El nombre "Ana García López" se muestra en el encabezado de la tarjeta.
- [ ] Las iniciales "AL" aparecen en el círculo del avatar.
- [ ] La edad "28 años" se muestra en la sección de detalles.
- [ ] El badge "Activo" aparece en color verde.
- [ ] No hay errores en la consola del navegador.

---

### Paso 11 — Inspeccionar el árbol de componentes con Angular DevTools

**Objetivo:** Usar Angular DevTools para explorar el árbol de componentes en tiempo de ejecución y verificar las propiedades del componente `UsuarioPerfilComponent`.

#### Instrucciones

1. Asegúrate de tener instalada la extensión **Angular DevTools** en Chrome. Si no la tienes, instálala desde [Chrome Web Store — Angular DevTools](https://chrome.google.com/webstore/detail/angular-devtools/ienfalfjdbdpebioblfackkekamfmbnh).

2. Con la aplicación corriendo en `http://localhost:4200`, abre las Herramientas de Desarrollador de Chrome (**F12**).

3. Haz clic en la pestaña **Angular** (aparece al final de las pestañas, puede requerir hacer clic en `»` para verla).

4. En el panel izquierdo verás el **árbol de componentes**. Expande los nodos y debes ver la jerarquía:
   ```
   AppComponent
   └── UsuarioPerfilComponent
   ```

5. Haz clic en **UsuarioPerfilComponent** en el árbol. En el panel derecho verás las propiedades del componente en tiempo de ejecución.

6. Verifica que las propiedades muestren los valores correctos:
   - `nombre`: `"Ana García"`
   - `apellido`: `"López"`
   - `edad`: `28`
   - `profesion`: `"Desarrolladora Frontend"`
   - `activo`: `true`

7. **Experimento interactivo:** En el panel de propiedades de Angular DevTools, haz doble clic en el valor de `activo` y cámbialo a `false`. Observa cómo el badge en la página cambia instantáneamente de "Activo" (verde) a "Inactivo" (rojo). Esto demuestra el *data binding* en acción.

8. **Captura de pantalla (opcional):** Toma una captura del árbol de componentes con las propiedades visibles para documentar tu trabajo.

#### Verificación

- [ ] El árbol de componentes muestra `AppComponent > UsuarioPerfilComponent`.
- [ ] Las propiedades del componente son visibles y tienen los valores correctos.
- [ ] Al cambiar `activo` a `false`, el badge cambia de color en tiempo real.

---

## Validación y Pruebas

Una vez completados todos los pasos, realiza las siguientes verificaciones finales:

### Lista de verificación completa

| # | Verificación | Resultado esperado |
|---|-------------|-------------------|
| 1 | `ng serve` ejecuta sin errores de compilación | Terminal muestra `✔ Compiled successfully` |
| 2 | Página carga en `http://localhost:4200` | Tarjeta de perfil visible |
| 3 | Nombre completo mostrado | "Ana García López" |
| 4 | Iniciales en el avatar | "AL" |
| 5 | Edad mostrada | "28 años" |
| 6 | Profesión mostrada | "Desarrolladora Frontend" |
| 7 | Badge de estado | Verde con texto "Activo" |
| 8 | Consola del navegador | Sin errores (0 errores) |
| 9 | Angular DevTools — árbol | `AppComponent > UsuarioPerfilComponent` |
| 10 | Angular DevTools — propiedades | Valores correctos en todas las propiedades |

### Prueba de modificación de datos

Para confirmar que el flujo de datos funciona correctamente, realiza esta prueba:

1. En VS Code, abre `src/app/services/usuario.service.ts`.
2. Cambia `activo: true` por `activo: false`.
3. Guarda el archivo. Angular CLI recargará automáticamente la página.
4. Verifica que el badge cambia a "Inactivo" en color rojo.
5. Revierte el cambio a `activo: true` y guarda.

Esta prueba confirma que el componente obtiene sus datos del servicio y que cualquier cambio en el servicio se refleja automáticamente en la vista.

---

## Resolución de Problemas

### Problema 1: Error `'app-usuario-perfil' is not a known element`

**Síntoma:** El navegador muestra una página en blanco o la consola de Chrome muestra el error:
```
Error: 'app-usuario-perfil' is not a known element:
1. If 'app-usuario-perfil' is an Angular component, then verify that it is part of this @NgModule.
```
También puede aparecer en la terminal de Angular CLI durante la compilación.

**Causa:** El componente `UsuarioPerfilComponent` no está declarado en el array `declarations` de `AppModule`. Esto ocurre cuando el componente fue creado manualmente (sin `ng generate`) o cuando se editó accidentalmente `app.module.ts`.

**Solución:**
1. Abre `src/app/app.module.ts`.
2. Verifica que exista la importación y la declaración:
   ```typescript
   import { UsuarioPerfilComponent } from './usuario-perfil/usuario-perfil.component';

   @NgModule({
     declarations: [
       AppComponent,
       UsuarioPerfilComponent  // ← debe estar aquí
     ],
     ...
   })
   ```
3. Si falta, agrégalo manualmente y guarda el archivo.
4. Si el error persiste, detén el servidor con **Ctrl + C** y reinícialo con `ng serve`.

---

### Problema 2: Las propiedades del componente muestran valores vacíos o `0` en el navegador

**Síntoma:** La tarjeta de perfil se renderiza pero los campos muestran valores vacíos (nombre en blanco, edad "0 años", profesión vacía) en lugar de los datos de Ana García.

**Causa:** El método `ngOnInit()` no está siendo llamado porque la clase no implementa correctamente la interfaz `OnInit`, o el servicio no está siendo inyectado correctamente. Otra causa común es un error tipográfico en el nombre del método (por ejemplo, `ngoninit` en minúsculas en lugar de `ngOnInit`).

**Solución:**
1. Abre `src/app/usuario-perfil/usuario-perfil.component.ts`.
2. Verifica que la declaración de la clase sea exactamente:
   ```typescript
   export class UsuarioPerfilComponent implements OnInit {
   ```
3. Confirma que `OnInit` está importado:
   ```typescript
   import { Component, OnInit } from '@angular/core';
   ```
4. Verifica que el método tenga la firma exacta (respeta mayúsculas):
   ```typescript
   ngOnInit(): void {
     this.usuario = this.usuarioService.getUsuario();
     this.nombre = this.usuario.nombre;
     // ... resto de asignaciones
   }
   ```
5. Confirma que el constructor inyecta el servicio:
   ```typescript
   constructor(private usuarioService: UsuarioService) {}
   ```
6. Guarda y verifica en el navegador.

---

## Limpieza del Entorno

Al finalizar el laboratorio, realiza los siguientes pasos para dejar el entorno ordenado:

1. **Detener el servidor de desarrollo:** En la terminal donde corre `ng serve`, presiona **Ctrl + C**. Confirma con `S` o `Y` si el sistema lo solicita.

2. **Guardar el trabajo:** Asegúrate de que todos los archivos estén guardados en VS Code (sin puntos de cambio pendientes en las pestañas).

3. **Commit opcional con Git** (recomendado para conservar el progreso):
   ```bash
   # Dentro del directorio app-usuario
   git add .
   git commit -m "Lab 04-00-01: Componente usuario-perfil con servicio e inyección de dependencias"
   ```

4. **Comprimir el proyecto** (si el instructor lo solicita para entrega):
   ```bash
   # En Windows (PowerShell)
   Compress-Archive -Path app-usuario -DestinationPath lab-04-00-01.zip

   # En macOS/Linux
   zip -r lab-04-00-01.zip app-usuario/ --exclude "app-usuario/node_modules/*"
   ```

   > **Importante:** Excluye la carpeta `node_modules` al comprimir. Esta carpeta puede pesar más de 300 MB y sus contenidos se pueden restaurar con `npm install`.

5. **Cerrar VS Code** si no continuarás con otro laboratorio.

---

## Resumen

En este laboratorio construiste una aplicación Angular completa que demuestra los conceptos fundamentales de la arquitectura de componentes:

| Concepto | Implementación realizada |
|----------|-------------------------|
| **Angular CLI** | `ng new`, `ng generate component`, `ng generate service`, `ng serve` |
| **Decorador `@Component`** | `selector`, `templateUrl`, `styleUrls` en `UsuarioPerfilComponent` |
| **Decorador `@Injectable`** | `providedIn: 'root'` en `UsuarioService` |
| **Interfaz TypeScript** | `Usuario` en `usuario.model.ts` con 5 propiedades tipadas |
| **Interpolación de datos** | `{{ nombre }}`, `{{ apellido }}`, `{{ edad }}`, etc. en el template |
| **Inyección de dependencias** | `UsuarioService` inyectado en el constructor del componente |
| **Ciclo de vida** | `ngOnInit()` para inicializar datos desde el servicio |
| **Class binding** | `[class.activo]` y `[class.inactivo]` para estilos condicionales |
| **Angular DevTools** | Inspección del árbol de componentes y propiedades en tiempo real |

### Flujo de datos implementado

```
UsuarioService.getUsuario()
        ↓
  (retorna objeto Usuario tipado)
        ↓
UsuarioPerfilComponent.ngOnInit()
        ↓
  (asigna propiedades: nombre, apellido, edad, profesion, activo)
        ↓
Template HTML (interpolación {{ }})
        ↓
  Vista renderizada en el navegador
```

### Recursos adicionales

- [Documentación oficial de Angular — Componentes](https://angular.io/guide/component-overview)
- [Guía de Inyección de Dependencias en Angular](https://angular.io/guide/dependency-injection)
- [Hooks del ciclo de vida de componentes](https://angular.io/guide/lifecycle-hooks)
- [Referencia de comandos Angular CLI](https://angular.io/cli)
- [Angular DevTools — Chrome Web Store](https://chrome.google.com/webstore/detail/angular-devtools/ienfalfjdbdpebioblfackkekamfmbnh)

---
*Lab 04-00-01 — Duración estimada: 49 minutos — Nivel Bloom: Crear*
