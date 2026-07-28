# Ciclo de vida de un componente en Angular

## Metadatos

| Campo         | Detalle                          |
|---------------|----------------------------------|
| **Duración**  | 33 minutos                       |
| **Complejidad** | Media                          |
| **Nivel Bloom** | Aplicar (Apply)               |
| **Módulo**    | 5 — Ciclo de vida de componentes |
| **Versión Angular** | 17.x (modo NgModule)     |

---

## Descripción General

En esta práctica construirás una aplicación Angular de demostración interactiva que implementa los **ocho hooks del ciclo de vida** de un componente. Crearás un componente padre `ciclo-demo` y un componente hijo `hijo-ciclo` que se comunican mediante `@Input`, permitiéndote observar en la consola del navegador el orden exacto de ejecución de cada hook. Al finalizar, comprenderás cuándo Angular invoca cada método del ciclo de vida y cómo utilizar esa información para escribir componentes más robustos y sin fugas de memoria.

---

## Objetivos de Aprendizaje

Al completar esta práctica serás capaz de:

- [ ] Implementar los ocho hooks del ciclo de vida Angular (`ngOnChanges`, `ngOnInit`, `ngDoCheck`, `ngAfterContentInit`, `ngAfterContentChecked`, `ngAfterViewInit`, `ngAfterViewChecked`, `ngOnDestroy`) con mensajes de consola que demuestren su orden de ejecución.
- [ ] Distinguir el propósito del constructor TypeScript frente a `ngOnInit` en el contexto de Angular.
- [ ] Demostrar cómo `ngOnChanges` se dispara ante cambios en una propiedad `@Input` y acceder a los valores anterior y actual mediante `SimpleChanges`.
- [ ] Utilizar `@ViewChild` dentro de `ngAfterViewInit` para acceder a un elemento del DOM.
- [ ] Implementar `ngOnDestroy` para cancelar un `setInterval` activo y prevenir fugas de memoria.

---

## Prerrequisitos

### Conocimientos previos
- Laboratorio 04-00-01 completado: comprensión de componentes Angular y decoradores.
- Clases TypeScript: implementación de interfaces (`implements`).
- Familiaridad con la consola de desarrollador de Chrome (F12 → pestaña Console).
- Noción básica de `@Input` (se profundizará en el Módulo 6).

### Acceso y herramientas
- Node.js 20.x LTS instalado y verificado (`node -v`).
- Angular CLI 17.x instalado globalmente (`ng version`).
- Visual Studio Code con la extensión **Angular Language Service** activa.
- Google Chrome con la extensión **Angular DevTools** instalada.
- Conexión a Internet (para resolver dependencias npm si es necesario).

---

## Entorno de Laboratorio

### Hardware mínimo recomendado

| Recurso          | Mínimo           | Recomendado      |
|------------------|------------------|------------------|
| Procesador       | Intel Core i5 / 1.6 GHz | i7 / 2.0 GHz |
| RAM              | 8 GB             | 16 GB            |
| Espacio en disco | 10 GB libres     | 20 GB libres     |
| Pantalla         | 1280×768         | 1920×1080        |
| Internet         | 10 Mbps          | 25 Mbps          |

### Software requerido

| Software              | Versión mínima | Verificación              |
|-----------------------|----------------|---------------------------|
| Node.js               | 18.x LTS       | `node -v`                 |
| npm                   | 9.x            | `npm -v`                  |
| Angular CLI           | 16.x           | `ng version`              |
| TypeScript            | 4.9.x          | `tsc -v`                  |
| Visual Studio Code    | 1.85.x         | Menú Help → About         |
| Google Chrome         | 120.x          | `chrome://settings/help`  |
| Angular DevTools      | Última         | Extensiones de Chrome      |

### Verificación del entorno

Abre una terminal y ejecuta los siguientes comandos para confirmar que el entorno está listo:

```bash
node -v
npm -v
ng version
```

Deberías ver salidas similares a:

```
v20.11.0
10.2.4
Angular CLI: 17.x.x
Node: 20.11.0
```

> **Nota para Windows:** Usa PowerShell o Git Bash. Para macOS/Linux usa Terminal.

---

## Pasos del Laboratorio

### Paso 1 — Crear el proyecto Angular

**Objetivo:** Generar el proyecto base en modo NgModule (sintaxis tradicional), que es el modo recomendado para este curso introductorio.

**Instrucciones:**

1. Abre una terminal en la carpeta donde almacenas tus proyectos de laboratorio (por ejemplo, `~/labs` o `C:\labs`).

2. Crea el proyecto con el flag `--no-standalone` para usar NgModule:

```bash
ng new lab05-ciclo-vida --no-standalone --routing=false --style=css
```

3. Cuando el CLI pregunte sobre el estilo, confirma `CSS`. Cuando termine la instalación, navega al directorio del proyecto:

```bash
cd lab05-ciclo-vida
```

4. Abre el proyecto en Visual Studio Code:

```bash
code .
```

5. Inicia el servidor de desarrollo en una terminal integrada de VS Code:

```bash
ng serve --open
```

**Salida esperada:**

```
✔ Browser application bundle generation complete.

Initial chunk files | Names         | Raw size
main.js             | main          | 177.63 kB

Build at: 2024-01-15T10:00:00.000Z - Hash: abc123 - Time: 4500ms

** Angular Live Development Server is listening on localhost:4200 **
```

El navegador se abrirá automáticamente en `http://localhost:4200` mostrando la página de bienvenida de Angular.

**Verificación:**
- La página de bienvenida de Angular aparece en el navegador sin errores en la consola.
- El terminal muestra `Compiled successfully`.

---

### Paso 2 — Generar los componentes del laboratorio

**Objetivo:** Crear los dos componentes que usaremos para la demostración: el componente padre `ciclo-demo` y el componente hijo `hijo-ciclo`.

**Instrucciones:**

1. Abre una **segunda terminal** en VS Code (sin detener `ng serve`) usando el menú Terminal → New Terminal.

2. Genera el componente padre:

```bash
ng generate component components/ciclo-demo
```

3. Genera el componente hijo:

```bash
ng generate component components/hijo-ciclo
```

4. Verifica que ambos componentes fueron creados correctamente. La estructura de carpetas debe verse así:

```
src/
└── app/
    ├── components/
    │   ├── ciclo-demo/
    │   │   ├── ciclo-demo.component.ts
    │   │   ├── ciclo-demo.component.html
    │   │   └── ciclo-demo.component.css
    │   └── hijo-ciclo/
    │       ├── hijo-ciclo.component.ts
    │       ├── hijo-ciclo.component.html
    │       └── hijo-ciclo.component.css
    ├── app.component.ts
    ├── app.component.html
    └── app.module.ts
```

5. Abre `src/app/app.module.ts` y verifica que ambos componentes están declarados automáticamente:

```typescript
// src/app/app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { CicloDemoComponent } from './components/ciclo-demo/ciclo-demo.component';
import { HijoCicloComponent } from './components/hijo-ciclo/hijo-ciclo.component';

@NgModule({
  declarations: [
    AppComponent,
    CicloDemoComponent,
    HijoCicloComponent
  ],
  imports: [BrowserModule],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

**Salida esperada en terminal:**
```
CREATE src/app/components/ciclo-demo/ciclo-demo.component.css (0 bytes)
CREATE src/app/components/ciclo-demo/ciclo-demo.component.html (...)
CREATE src/app/components/ciclo-demo/ciclo-demo.component.ts (...)
UPDATE src/app/app.module.ts (...)
```

**Verificación:**
- Ambas carpetas existen en `src/app/components/`.
- `app.module.ts` declara `CicloDemoComponent` y `HijoCicloComponent`.
- El navegador sigue mostrando la app sin errores de compilación.

---

### Paso 3 — Implementar el componente hijo `hijo-ciclo`

**Objetivo:** Construir el componente hijo que recibe una propiedad `@Input` e implementa `ngOnChanges` para registrar cada cambio recibido desde el padre.

**Instrucciones:**

1. Abre `src/app/components/hijo-ciclo/hijo-ciclo.component.ts` y reemplaza **todo** su contenido con el siguiente código:

```typescript
// src/app/components/hijo-ciclo/hijo-ciclo.component.ts
import {
  Component,
  Input,
  OnChanges,
  OnInit,
  OnDestroy,
  SimpleChanges
} from '@angular/core';

@Component({
  selector: 'app-hijo-ciclo',
  templateUrl: './hijo-ciclo.component.html',
  styleUrls: ['./hijo-ciclo.component.css']
})
export class HijoCicloComponent implements OnChanges, OnInit, OnDestroy {

  @Input() mensaje: string = '';

  // El constructor SOLO debe usarse para inyectar dependencias.
  // No coloques lógica de inicialización aquí.
  constructor() {
    console.log('%c[HijoCiclo] Constructor ejecutado', 'color: #9c27b0; font-weight: bold');
  }

  // Se ejecuta ANTES de ngOnInit y cada vez que cambia @Input
  ngOnChanges(changes: SimpleChanges): void {
    if (changes['mensaje']) {
      const cambio = changes['mensaje'];
      console.log('%c[HijoCiclo] ngOnChanges — cambio en @Input "mensaje"', 'color: #e91e63; font-weight: bold');
      console.log('  ↳ Valor anterior:', cambio.previousValue);
      console.log('  ↳ Valor actual:', cambio.currentValue);
      console.log('  ↳ ¿Es el primer cambio?', cambio.firstChange);
    }
  }

  // Se ejecuta UNA SOLA VEZ, después del primer ngOnChanges
  ngOnInit(): void {
    console.log('%c[HijoCiclo] ngOnInit — componente inicializado', 'color: #2196f3; font-weight: bold');
    // Simulación de una llamada a servicio
    setTimeout(() => {
      console.log('%c[HijoCiclo] ngOnInit — datos del servicio cargados (simulado)', 'color: #2196f3');
    }, 500);
  }

  // Se ejecuta JUSTO ANTES de que el componente sea destruido
  ngOnDestroy(): void {
    console.log('%c[HijoCiclo] ngOnDestroy — componente destruido, recursos liberados', 'color: #f44336; font-weight: bold');
  }
}
```

2. Abre `src/app/components/hijo-ciclo/hijo-ciclo.component.html` y reemplaza su contenido:

```html
<!-- src/app/components/hijo-ciclo/hijo-ciclo.component.html -->
<div class="hijo-container">
  <h4>📦 Componente Hijo (HijoCicloComponent)</h4>
  <p>
    Mensaje recibido vía <code>@Input</code>:
    <strong>{{ mensaje }}</strong>
  </p>
  <small>Observa la consola del navegador para ver ngOnChanges en acción.</small>
</div>
```

3. Agrega estilos básicos en `src/app/components/hijo-ciclo/hijo-ciclo.component.css`:

```css
/* src/app/components/hijo-ciclo/hijo-ciclo.component.css */
.hijo-container {
  border: 2px solid #9c27b0;
  border-radius: 8px;
  padding: 16px;
  margin-top: 12px;
  background-color: #f3e5f5;
}

.hijo-container h4 {
  margin: 0 0 8px 0;
  color: #6a1b9a;
}

.hijo-container code {
  background-color: #e1bee7;
  padding: 2px 6px;
  border-radius: 4px;
}
```

**Salida esperada:**
- VS Code no muestra errores de TypeScript en el archivo.
- El navegador compila sin errores (revisa el terminal de `ng serve`).

**Verificación:**
- Abre Chrome DevTools (F12) → pestaña **Console**.
- Aunque el componente hijo aún no está siendo usado, no deben aparecer errores rojos.

---

### Paso 4 — Implementar el componente padre `ciclo-demo` con todos los hooks

**Objetivo:** Construir el componente padre que implementa los ocho hooks del ciclo de vida, usa `@ViewChild` en `ngAfterViewInit` y gestiona un `setInterval` que se cancela en `ngOnDestroy`.

**Instrucciones:**

1. Abre `src/app/components/ciclo-demo/ciclo-demo.component.ts` y reemplaza **todo** su contenido:

```typescript
// src/app/components/ciclo-demo/ciclo-demo.component.ts
import {
  Component,
  OnChanges,
  OnInit,
  DoCheck,
  AfterContentInit,
  AfterContentChecked,
  AfterViewInit,
  AfterViewChecked,
  OnDestroy,
  SimpleChanges,
  ViewChild,
  ElementRef
} from '@angular/core';

@Component({
  selector: 'app-ciclo-demo',
  templateUrl: './ciclo-demo.component.html',
  styleUrls: ['./ciclo-demo.component.css']
})
export class CicloDemoComponent implements
  OnChanges,
  OnInit,
  DoCheck,
  AfterContentInit,
  AfterContentChecked,
  AfterViewInit,
  AfterViewChecked,
  OnDestroy {

  // Propiedad enlazada al input del template
  mensajeParaHijo: string = 'Hola desde el padre';

  // Controla si el componente hijo está visible (*ngIf)
  mostrarHijo: boolean = true;

  // Contador del setInterval para demostrar ngOnDestroy
  private contadorIntervalo: number = 0;
  private intervaloId: ReturnType<typeof setInterval> | null = null;

  // Referencia al elemento <div #panelInfo> del template
  @ViewChild('panelInfo') panelInfoRef!: ElementRef<HTMLDivElement>;

  // ─────────────────────────────────────────────
  // CONSTRUCTOR: solo para inyección de dependencias
  // ─────────────────────────────────────────────
  constructor() {
    console.log('%c[CicloDemo] ⚙️  Constructor ejecutado', 'color: #607d8b; font-weight: bold');
    console.log('  ↳ NOTA: @ViewChild NO está disponible aquí todavía.');
  }

  // ─────────────────────────────────────────────
  // HOOK 1: ngOnChanges
  // ─────────────────────────────────────────────
  ngOnChanges(changes: SimpleChanges): void {
    // Este componente no recibe @Input, pero el hook está implementado
    // para demostrar que Angular lo llama si existieran @Input
    console.log('%c[CicloDemo] 1️⃣  ngOnChanges', 'color: #e91e63; font-weight: bold', changes);
  }

  // ─────────────────────────────────────────────
  // HOOK 2: ngOnInit
  // ─────────────────────────────────────────────
  ngOnInit(): void {
    console.log('%c[CicloDemo] 2️⃣  ngOnInit — inicializando componente', 'color: #2196f3; font-weight: bold');

    // Iniciamos un intervalo para demostrar ngOnDestroy
    this.intervaloId = setInterval(() => {
      this.contadorIntervalo++;
      console.log(`%c[CicloDemo] ⏱️  Intervalo activo — tick #${this.contadorIntervalo}`, 'color: #ff9800');
    }, 3000);

    console.log('  ↳ setInterval iniciado. ID:', this.intervaloId);
    console.log('  ↳ NOTA: @ViewChild NO está disponible aquí todavía.');
  }

  // ─────────────────────────────────────────────
  // HOOK 3: ngDoCheck
  // ─────────────────────────────────────────────
  ngDoCheck(): void {
    // Se ejecuta en CADA ciclo de detección de cambios.
    // Usamos console.debug para no saturar la consola principal.
    console.debug('%c[CicloDemo] 3️⃣  ngDoCheck — ciclo de detección ejecutado', 'color: #795548');
  }

  // ─────────────────────────────────────────────
  // HOOK 4: ngAfterContentInit
  // ─────────────────────────────────────────────
  ngAfterContentInit(): void {
    console.log('%c[CicloDemo] 4️⃣  ngAfterContentInit — contenido proyectado (ng-content) listo', 'color: #009688; font-weight: bold');
  }

  // ─────────────────────────────────────────────
  // HOOK 5: ngAfterContentChecked
  // ─────────────────────────────────────────────
  ngAfterContentChecked(): void {
    console.debug('%c[CicloDemo] 5️⃣  ngAfterContentChecked — contenido proyectado verificado', 'color: #4caf50');
  }

  // ─────────────────────────────────────────────
  // HOOK 6: ngAfterViewInit
  // ─────────────────────────────────────────────
  ngAfterViewInit(): void {
    console.log('%c[CicloDemo] 6️⃣  ngAfterViewInit — vista completamente inicializada', 'color: #3f51b5; font-weight: bold');

    // @ViewChild SÍ está disponible a partir de este hook
    if (this.panelInfoRef) {
      const el = this.panelInfoRef.nativeElement;
      el.style.borderColor = '#3f51b5';
      el.style.backgroundColor = '#e8eaf6';
      console.log('  ↳ @ViewChild accedido correctamente:', el.tagName);
      console.log('  ↳ Texto del panel:', el.innerText.substring(0, 60) + '...');
    }
  }

  // ─────────────────────────────────────────────
  // HOOK 7: ngAfterViewChecked
  // ─────────────────────────────────────────────
  ngAfterViewChecked(): void {
    console.debug('%c[CicloDemo] 7️⃣  ngAfterViewChecked — vista verificada', 'color: #8bc34a');
  }

  // ─────────────────────────────────────────────
  // HOOK 8: ngOnDestroy
  // ─────────────────────────────────────────────
  ngOnDestroy(): void {
    console.log('%c[CicloDemo] 8️⃣  ngOnDestroy — limpiando recursos antes de destruir', 'color: #f44336; font-weight: bold');

    // CRÍTICO: cancelar el intervalo para evitar memory leak
    if (this.intervaloId !== null) {
      clearInterval(this.intervaloId);
      console.log('  ↳ ✅ setInterval cancelado correctamente. Ticks ejecutados:', this.contadorIntervalo);
      this.intervaloId = null;
    }
  }

  // ─────────────────────────────────────────────
  // Métodos del template
  // ─────────────────────────────────────────────
  actualizarMensaje(nuevoMensaje: string): void {
    this.mensajeParaHijo = nuevoMensaje;
  }

  toggleHijo(): void {
    this.mostrarHijo = !this.mostrarHijo;
    const accion = this.mostrarHijo ? 'CREADO' : 'DESTRUIDO';
    console.log(`%c[CicloDemo] 🔄 Componente hijo ${accion}`, 'color: #ff5722; font-weight: bold');
  }
}
```

2. Abre `src/app/components/ciclo-demo/ciclo-demo.component.html` y reemplaza su contenido:

```html
<!-- src/app/components/ciclo-demo/ciclo-demo.component.html -->
<div class="ciclo-container">

  <h2>🔄 Demostración del Ciclo de Vida Angular</h2>
  <p class="instruccion">
    Abre la <strong>consola del navegador</strong> (F12 → Console) para observar
    el orden de ejecución de los hooks del ciclo de vida.
  </p>

  <!-- Panel de información accedido con @ViewChild -->
  <div #panelInfo class="panel-info">
    <h3>📋 Panel de Información</h3>
    <p>Este elemento es accedido mediante <code>@ViewChild</code> en <code>ngAfterViewInit</code>.</p>
    <p>Observa en la consola cómo su color de borde cambia después de que la vista se inicializa.</p>
  </div>

  <!-- Sección: Cambiar mensaje del hijo -->
  <div class="seccion">
    <h3>📨 Probar ngOnChanges en el componente hijo</h3>
    <p>Escribe un nuevo mensaje y observa cómo <code>ngOnChanges</code> se dispara en el hijo:</p>

    <div class="input-group">
      <input
        type="text"
        [value]="mensajeParaHijo"
        (input)="actualizarMensaje($any($event.target).value)"
        placeholder="Escribe un mensaje para el hijo"
        class="input-mensaje"
      />
    </div>

    <p class="mensaje-actual">
      Mensaje actual: <strong>{{ mensajeParaHijo }}</strong>
    </p>
  </div>

  <!-- Sección: Crear/destruir componente hijo -->
  <div class="seccion">
    <h3>💥 Probar ngOnDestroy</h3>
    <p>
      Usa el botón para destruir y recrear el componente hijo.
      Observa <code>ngOnDestroy</code> al destruirlo y la secuencia completa al recrearlo.
    </p>

    <button (click)="toggleHijo()" class="btn-toggle">
      {{ mostrarHijo ? '🗑️ Destruir componente hijo' : '✅ Crear componente hijo' }}
    </button>
  </div>

  <!-- Componente hijo: solo existe cuando mostrarHijo es true -->
  <app-hijo-ciclo
    *ngIf="mostrarHijo"
    [mensaje]="mensajeParaHijo">
  </app-hijo-ciclo>

  <!-- Referencia de hooks -->
  <div class="referencia">
    <h3>📚 Orden de ejecución de los hooks</h3>
    <ol>
      <li><code>Constructor</code> — Inyección de dependencias</li>
      <li><code>ngOnChanges</code> — Primer cambio en @Input (si existe)</li>
      <li><code>ngOnInit</code> — Inicialización del componente</li>
      <li><code>ngDoCheck</code> — Detección de cambios personalizada</li>
      <li><code>ngAfterContentInit</code> — Contenido ng-content listo</li>
      <li><code>ngAfterContentChecked</code> — Contenido ng-content verificado</li>
      <li><code>ngAfterViewInit</code> — Vista del componente lista (@ViewChild disponible)</li>
      <li><code>ngAfterViewChecked</code> — Vista verificada</li>
      <li><code>ngOnDestroy</code> — Limpieza antes de destruir</li>
    </ol>
  </div>

</div>
```

3. Agrega estilos en `src/app/components/ciclo-demo/ciclo-demo.component.css`:

```css
/* src/app/components/ciclo-demo/ciclo-demo.component.css */
.ciclo-container {
  max-width: 800px;
  margin: 20px auto;
  padding: 24px;
  font-family: 'Segoe UI', sans-serif;
}

.ciclo-container h2 {
  color: #1a237e;
  border-bottom: 3px solid #3f51b5;
  padding-bottom: 8px;
}

.instruccion {
  background-color: #fff9c4;
  border-left: 4px solid #f9a825;
  padding: 10px 14px;
  border-radius: 4px;
  margin-bottom: 20px;
}

.panel-info {
  border: 2px solid #ccc;
  border-radius: 8px;
  padding: 16px;
  margin-bottom: 20px;
  transition: border-color 0.3s, background-color 0.3s;
}

.panel-info h3 {
  margin: 0 0 8px 0;
}

.seccion {
  background-color: #fafafa;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  padding: 16px;
  margin-bottom: 16px;
}

.seccion h3 {
  margin: 0 0 10px 0;
  color: #37474f;
}

.input-group {
  display: flex;
  gap: 10px;
  margin-bottom: 8px;
}

.input-mensaje {
  flex: 1;
  padding: 8px 12px;
  border: 1px solid #90caf9;
  border-radius: 4px;
  font-size: 14px;
  outline: none;
}

.input-mensaje:focus {
  border-color: #1976d2;
  box-shadow: 0 0 0 2px rgba(25, 118, 210, 0.2);
}

.mensaje-actual {
  font-size: 13px;
  color: #546e7a;
  margin: 0;
}

.btn-toggle {
  padding: 10px 20px;
  border: none;
  border-radius: 6px;
  background-color: #3f51b5;
  color: white;
  font-size: 14px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.btn-toggle:hover {
  background-color: #303f9f;
}

.referencia {
  background-color: #f5f5f5;
  border-radius: 8px;
  padding: 16px;
  margin-top: 20px;
}

.referencia h3 {
  margin: 0 0 10px 0;
  color: #37474f;
}

.referencia ol {
  margin: 0;
  padding-left: 20px;
  line-height: 1.8;
}

code {
  background-color: #e8eaf6;
  color: #283593;
  padding: 2px 6px;
  border-radius: 3px;
  font-size: 13px;
}
```

**Salida esperada:**
- VS Code no muestra errores TypeScript en ninguno de los archivos.
- El terminal de `ng serve` muestra `Compiled successfully`.

**Verificación:**
- Guarda todos los archivos y verifica que no hay errores de compilación en el terminal.

---

### Paso 5 — Conectar el componente padre con `AppComponent`

**Objetivo:** Reemplazar el contenido por defecto de `AppComponent` para mostrar el componente `ciclo-demo` en la aplicación.

**Instrucciones:**

1. Abre `src/app/app.component.html` y reemplaza **todo** su contenido con:

```html
<!-- src/app/app.component.html -->
<div style="padding: 16px;">
  <app-ciclo-demo></app-ciclo-demo>
</div>
```

2. Abre `src/app/app.component.ts` y simplifica el componente:

```typescript
// src/app/app.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'lab05-ciclo-vida';
}
```

3. Abre `src/app/app.component.css` y limpia su contenido (déjalo vacío o agrega un reset básico):

```css
/* src/app/app.component.css */
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  background-color: #f0f4f8;
}
```

4. Verifica que `app.module.ts` tiene `FormsModule` si es necesario. Para este laboratorio **no** lo necesitamos porque usamos event binding nativo. Confirma que el módulo luce así:

```typescript
// src/app/app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { CicloDemoComponent } from './components/ciclo-demo/ciclo-demo.component';
import { HijoCicloComponent } from './components/hijo-ciclo/hijo-ciclo.component';

@NgModule({
  declarations: [
    AppComponent,
    CicloDemoComponent,
    HijoCicloComponent
  ],
  imports: [
    BrowserModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

**Salida esperada:**
- El navegador en `http://localhost:4200` muestra la interfaz de demostración con el panel de información, el input de mensaje y el botón para destruir/crear el componente hijo.
- El componente hijo `HijoCicloComponent` es visible con el borde morado.

**Verificación:**
- La página carga sin errores en la consola de Chrome (F12).
- Se ven los mensajes iniciales del ciclo de vida en la consola.

---

### Paso 6 — Observar el ciclo de vida en la consola del navegador

**Objetivo:** Analizar el orden de ejecución de los hooks durante la carga inicial, los cambios de `@Input` y la destrucción del componente.

**Instrucciones:**

1. Abre Chrome DevTools presionando **F12** y navega a la pestaña **Console**.

2. Asegúrate de que el nivel de log muestra `Verbose` o al menos `Debug` para ver los mensajes de `console.debug`. En la consola, haz clic en el menú desplegable que dice `Default levels` y activa **Verbose**.

3. **Recarga la página** (Ctrl+R / Cmd+R) y observa los mensajes que aparecen. Deberías ver la siguiente secuencia (los mensajes de `console.debug` aparecen en gris/azul claro):

```
[CicloDemo] ⚙️  Constructor ejecutado
[CicloDemo] 1️⃣  ngOnChanges  ← (puede no aparecer si no hay @Input en CicloDemo)
[CicloDemo] 2️⃣  ngOnInit — inicializando componente
[HijoCiclo] Constructor ejecutado
[HijoCiclo] ngOnChanges — cambio en @Input "mensaje"
  ↳ Valor anterior: undefined
  ↳ Valor actual: Hola desde el padre
  ↳ ¿Es el primer cambio? true
[HijoCiclo] ngOnInit — componente inicializado
[CicloDemo] 3️⃣  ngDoCheck
[CicloDemo] 4️⃣  ngAfterContentInit
[CicloDemo] 5️⃣  ngAfterContentChecked
[CicloDemo] 6️⃣  ngAfterViewInit — vista completamente inicializada
  ↳ @ViewChild accedido correctamente: DIV
[CicloDemo] 7️⃣  ngAfterViewChecked
[HijoCiclo] ngOnInit — datos del servicio cargados (simulado)  ← después de ~500ms
[CicloDemo] ⏱️  Intervalo activo — tick #1  ← después de ~3 segundos
```

4. **Prueba 1 — Cambiar el mensaje:** Escribe en el campo de texto. Observa cómo cada pulsación de tecla dispara:
   - `[HijoCiclo] ngOnChanges` con el nuevo valor
   - `[CicloDemo] ngDoCheck` (en modo debug)
   - `[CicloDemo] ngAfterContentChecked` (en modo debug)
   - `[CicloDemo] ngAfterViewChecked` (en modo debug)

5. **Prueba 2 — Destruir el componente hijo:** Haz clic en el botón **"🗑️ Destruir componente hijo"**. Observa:
   ```
   [HijoCiclo] ngOnDestroy — componente destruido, recursos liberados
   [CicloDemo] 🔄 Componente hijo DESTRUIDO
   ```

6. **Prueba 3 — Recrear el componente hijo:** Haz clic en **"✅ Crear componente hijo"**. Observa la secuencia completa de creación nuevamente (Constructor → ngOnChanges → ngOnInit → ...).

7. **Prueba 4 — Esperar el intervalo:** Espera 3 segundos sin interactuar. Observa los mensajes del `setInterval` en la consola. Luego destruye el componente `ciclo-demo` navegando a otra pestaña y regresando; si el componente padre se destruyera, los ticks deberían detenerse.

**Salida esperada:**
La consola muestra mensajes con colores distintos para cada hook, permitiendo distinguir visualmente su orden y frecuencia.

**Verificación:**
- Puedes identificar claramente cuáles hooks se ejecutan una sola vez (ngOnInit, ngAfterContentInit, ngAfterViewInit) versus los que se repiten (ngDoCheck, ngAfterContentChecked, ngAfterViewChecked).
- `ngOnChanges` del componente hijo se dispara con cada cambio en el input de texto.
- `ngOnDestroy` aparece al destruir el componente hijo.

---

### Paso 7 — Explorar con Angular DevTools

**Objetivo:** Utilizar la extensión Angular DevTools para complementar la observación del ciclo de vida.

**Instrucciones:**

1. Con la aplicación corriendo en Chrome, abre DevTools (F12).

2. Busca la pestaña **Angular** (instalada por la extensión Angular DevTools). Si no aparece, haz clic en el ícono `>>` para ver pestañas adicionales.

3. En la pestaña Angular, selecciona la vista **Components** (árbol de componentes).

4. Observa la jerarquía:
   ```
   AppComponent
   └── CicloDemoComponent
       └── HijoCicloComponent (solo si mostrarHijo = true)
   ```

5. Haz clic en `HijoCicloComponent` en el árbol y observa sus propiedades en el panel derecho. Deberías ver la propiedad `mensaje` con su valor actual.

6. Haz clic en el botón **"🗑️ Destruir componente hijo"** en la aplicación y observa cómo `HijoCicloComponent` desaparece del árbol en Angular DevTools.

7. Haz clic en **"✅ Crear componente hijo"** y observa cómo reaparece en el árbol.

8. En Angular DevTools, navega a la pestaña **Profiler** y haz clic en el botón de grabar (círculo rojo). Interactúa con el input de texto y luego detén la grabación. Observa qué componentes se re-renderizaron con cada cambio.

**Salida esperada:**
- Angular DevTools muestra el árbol de componentes actualizado en tiempo real.
- El Profiler muestra que `HijoCicloComponent` y `CicloDemoComponent` se actualizan con cada cambio en el input.

**Verificación:**
- El árbol de componentes en Angular DevTools refleja correctamente el estado de `*ngIf` sobre `HijoCicloComponent`.

---

## Validación y Pruebas

Completa la siguiente lista de verificación para confirmar que el laboratorio fue implementado correctamente:

### Lista de verificación

| # | Verificación | Resultado esperado |
|---|---|---|
| 1 | La aplicación compila sin errores (`ng serve`) | Terminal muestra `Compiled successfully` |
| 2 | Al cargar la página, la consola muestra el Constructor antes de ngOnInit | ✅ Orden correcto |
| 3 | `ngOnChanges` del hijo muestra `firstChange: true` en la primera carga | ✅ Primer cambio identificado |
| 4 | Al escribir en el input, `ngOnChanges` del hijo se dispara con cada letra | ✅ `previousValue` y `currentValue` distintos |
| 5 | `@ViewChild` en `ngAfterViewInit` modifica el color del panel correctamente | ✅ Panel cambia a azul índigo |
| 6 | El `setInterval` emite mensajes cada 3 segundos en la consola | ✅ Ticks visibles |
| 7 | Al destruir el hijo, aparece `ngOnDestroy` en la consola | ✅ Mensaje de destrucción |
| 8 | Al recrear el hijo, aparece la secuencia completa de hooks en la consola | ✅ Constructor → ngOnChanges → ngOnInit → ... |
| 9 | Angular DevTools muestra el árbol de componentes correctamente | ✅ Jerarquía visible |
| 10 | `ngDoCheck` aparece en modo Verbose de la consola | ✅ Mensajes en gris/azul claro |

### Pregunta de reflexión

Responde mentalmente (o en tu cuaderno) las siguientes preguntas para confirmar tu comprensión:

1. **¿Por qué no se debe hacer una llamada HTTP en el constructor?**
   > El constructor se ejecuta antes de que Angular haya procesado los `@Input` y antes de que la vista esté lista. Las llamadas a servicios deben hacerse en `ngOnInit`.

2. **¿Qué problema ocurriría si no cancelamos el `setInterval` en `ngOnDestroy`?**
   > El intervalo seguiría ejecutándose en memoria aunque el componente ya no exista en el DOM, causando una **fuga de memoria** (*memory leak*) y posibles errores al intentar actualizar una vista destruida.

3. **¿En qué se diferencia `ngAfterContentInit` de `ngAfterViewInit`?**
   > `ngAfterContentInit` se dispara cuando el contenido proyectado via `<ng-content>` está listo. `ngAfterViewInit` se dispara cuando la vista propia del componente y sus hijos están completamente inicializados.

---

## Solución de Problemas

### Problema 1: `@ViewChild` retorna `undefined` en `ngAfterViewInit`

**Síntoma:** La consola muestra el mensaje de `ngAfterViewInit` pero también un error como `Cannot read properties of undefined (reading 'nativeElement')`, o el panel no cambia de color.

**Causa:** El elemento referenciado con `#panelInfo` en el template no existe en el DOM en el momento en que `ngAfterViewInit` se ejecuta. Esto puede ocurrir si el elemento está dentro de un `*ngIf` que evalúa a `false`, o si el nombre de la referencia en el template no coincide exactamente con el string en `@ViewChild`.

**Solución:**
1. Verifica que el template contiene exactamente `<div #panelInfo ...>` (sin espacios ni mayúsculas incorrectas).
2. Confirma que `@ViewChild('panelInfo')` usa el mismo nombre: `'panelInfo'`.
3. Si el elemento pudiera no existir, usa el operador de encadenamiento opcional:

```typescript
ngAfterViewInit(): void {
  if (this.panelInfoRef) {  // Verificación de seguridad
    const el = this.panelInfoRef.nativeElement;
    el.style.borderColor = '#3f51b5';
  } else {
    console.error('panelInfoRef no encontrado. Verifica la referencia #panelInfo en el template.');
  }
}
```

4. Asegúrate de que el elemento **no** está dentro de un `*ngIf` que pueda estar evaluando a `false`.

---

### Problema 2: `ngOnChanges` no se dispara en `CicloDemoComponent`

**Síntoma:** Al recargar la página, el mensaje `1️⃣ ngOnChanges` de `CicloDemoComponent` no aparece en la consola, aunque el hook está implementado.

**Causa:** `ngOnChanges` **solo se dispara cuando el componente tiene al menos una propiedad decorada con `@Input` que recibe un valor desde su componente padre**. `CicloDemoComponent` en este laboratorio no tiene propiedades `@Input` propias (es el componente padre), por lo que `ngOnChanges` nunca se invoca en él. Esto es comportamiento correcto de Angular, no un error.

**Solución:**
Este comportamiento es el esperado. Para verificar que `ngOnChanges` funciona correctamente, observa los mensajes del **componente hijo** `HijoCicloComponent`, que sí tiene la propiedad `@Input() mensaje` y muestra `ngOnChanges` con cada cambio. Si quieres ver `ngOnChanges` en `CicloDemoComponent`, necesitarías que `AppComponent` le pasara una propiedad `@Input`, lo cual está fuera del alcance de este laboratorio pero es un buen ejercicio adicional:

```typescript
// Ejercicio adicional: agregar @Input a CicloDemoComponent
@Input() titulo: string = 'Demo';
```

```html
<!-- En app.component.html -->
<app-ciclo-demo [titulo]="'Laboratorio 05'"></app-ciclo-demo>
```

---

## Limpieza

Una vez completado el laboratorio, realiza los siguientes pasos para dejar el entorno ordenado:

1. **Detén el servidor de desarrollo** en el terminal con `Ctrl+C`.

2. **Guarda todos los archivos** en VS Code con `Ctrl+K S` (Windows/Linux) o `Cmd+K S` (macOS).

3. **Comprime el proyecto** para entrega si es requerido:

```bash
# Desde la carpeta padre del proyecto
# En Windows (PowerShell):
Compress-Archive -Path lab05-ciclo-vida -DestinationPath lab05-ciclo-vida.zip

# En macOS/Linux:
zip -r lab05-ciclo-vida.zip lab05-ciclo-vida/ --exclude "*/node_modules/*"
```

4. **Opcional — Eliminar node_modules** si necesitas liberar espacio en disco (puedes reinstalar con `npm install`):

```bash
# Windows:
rmdir /s /q lab05-ciclo-vida\node_modules

# macOS/Linux:
rm -rf lab05-ciclo-vida/node_modules
```

> ⚠️ **No elimines** el directorio `node_modules` si vas a continuar trabajando en el proyecto inmediatamente.

---

## Resumen

En esta práctica implementaste los **ocho hooks del ciclo de vida** de Angular en una aplicación interactiva de demostración. Los conceptos clave que practicaste son:

| Concepto | Lo que aprendiste |
|---|---|
| **Constructor vs ngOnInit** | El constructor es solo para inyección de dependencias; la lógica de inicialización va en `ngOnInit` |
| **ngOnChanges** | Se dispara antes de `ngOnInit` y con cada cambio en `@Input`; recibe `SimpleChanges` con valores anterior y actual |
| **ngDoCheck** | Se ejecuta en cada ciclo de detección de cambios; usar con precaución por su impacto en rendimiento |
| **ngAfterViewInit + @ViewChild** | El momento correcto para acceder a elementos del DOM referenciados con `@ViewChild` |
| **ngOnDestroy** | Obligatorio para cancelar `setInterval`, `setTimeout` y suscripciones para prevenir memory leaks |
| **`*ngIf` y ciclo de vida** | Destruir y recrear un componente con `*ngIf` dispara el ciclo completo de destrucción y creación |

### Recursos adicionales

- 📖 [Documentación oficial — Lifecycle hooks (Angular)](https://angular.dev/guide/components/lifecycle)
- 📖 [SimpleChanges API Reference](https://angular.dev/api/core/SimpleChanges)
- 🔧 [Angular DevTools — Chrome Web Store](https://chrome.google.com/webstore/detail/angular-devtools/ienfalfjdbdpebioblfackkekamfmbnh)
- 📹 [Angular University — Component Lifecycle Deep Dive](https://angular-university.io)

---
*Lab 05-00-01 — Ciclo de vida de componentes Angular | Versión 1.0 | Angular 17.x (NgModule)*
