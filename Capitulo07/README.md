# Uso de Templates

## Metadatos

| Campo | Detalle |
|---|---|
| **Duración estimada** | 99 minutos |
| **Complejidad** | Alta |
| **Nivel Bloom** | Crear |
| **Módulo** | 7 — Templates y Data Binding |
| **Versión Angular** | 17.x (modo NgModule con `--no-standalone`) |
| **Versión Bootstrap** | 5.x |

---

## Descripción General

En esta práctica construirás una aplicación Angular completa de **gestión de empleados** que demuestra de forma integrada todos los mecanismos de la sintaxis de templates: interpolación, property binding, event binding, two-way binding con `[(ngModel)]`, directivas estructurales (`*ngIf`, `*ngFor`, `*ngSwitch`), directivas de atributo (`[ngClass]`, `[ngStyle]`), template reference variables, pipes integrados y un formulario template-driven con validación visual. La interfaz utilizará Bootstrap 5 para lograr un diseño responsivo y profesional. Al finalizar tendrás una tabla interactiva de empleados con búsqueda en tiempo real, panel de detalles y formulario de alta.

---

## Objetivos de Aprendizaje

Al completar esta práctica serás capaz de:

- [ ] Aplicar interpolación, property binding, event binding y two-way binding con `[(ngModel)]` en templates Angular reales
- [ ] Implementar directivas estructurales `*ngIf`, `*ngFor` y `*ngSwitch` para renderizado condicional y de listas con variables de contexto (`index`, `even`, `odd`)
- [ ] Usar directivas de atributo `[ngClass]` y `[ngStyle]` para aplicar estilos dinámicos basados en el estado del componente
- [ ] Aplicar y encadenar pipes integrados (`DatePipe`, `CurrencyPipe`, `UpperCasePipe`, `SlicePipe`, `JsonPipe`) para transformar datos en el template
- [ ] Construir un formulario template-driven con validación visual usando `ngModel` y las clases `is-valid`/`is-invalid` de Bootstrap 5

---

## Prerrequisitos

### Conocimientos

- Laboratorios 04-00-01, 05-00-01, 06-00-01 y 06-00-02 completados
- Comprensión de la arquitectura de componentes Angular y el decorador `@Component`
- TypeScript: interfaces, arreglos, métodos `filter`, `find`, `map`
- Conocimientos básicos de CSS y clases utilitarias de Bootstrap (grid, badges, botones, formularios)
- Familiaridad con el ciclo de vida Angular (`ngOnInit`)

### Acceso y Herramientas

- Node.js 20.x LTS instalado y verificado (`node -v`)
- Angular CLI 17.x instalado globalmente (`ng version`)
- Visual Studio Code 1.85.x con extensión **Angular Language Service**
- Google Chrome 120.x con extensión **Angular DevTools**
- Conexión a Internet para descarga de paquetes npm

---

## Entorno de Laboratorio

### Hardware Mínimo Recomendado

| Recurso | Mínimo | Recomendado |
|---|---|---|
| RAM | 8 GB | 16 GB |
| Almacenamiento libre | 10 GB | 15 GB |
| Procesador | Intel Core i5 / 1.6 GHz | Intel Core i7 / 2.0 GHz |
| Resolución de pantalla | 1280×768 | 1920×1080 |

### Software Requerido

| Software | Versión mínima | Verificación |
|---|---|---|
| Node.js | 18.x LTS | `node -v` |
| npm | 9.x | `npm -v` |
| Angular CLI | 16.x | `ng version` |
| TypeScript | 4.9.x | `tsc -v` |
| Visual Studio Code | 1.85.x | Menú *Help → About* |
| Google Chrome | 120.x | `chrome://version` |

### Verificación del Entorno

Ejecuta los siguientes comandos antes de comenzar para confirmar que el entorno está listo:

```bash
node -v
npm -v
ng version
```

Deberías ver versiones compatibles con las indicadas en la tabla anterior. Si Angular CLI no está instalado:

```bash
npm install -g @angular/cli@17
```

> **Nota para macOS/Linux:** Si recibes errores de permisos, ejecuta primero:
> ```bash
> npm config set prefix ~/.npm-global
> export PATH=~/.npm-global/bin:$PATH
> ```

---

## Pasos del Laboratorio

---

### Paso 1: Crear el Proyecto Angular con NgModule

**Objetivo:** Crear un nuevo proyecto Angular 17 en modo NgModule (sin standalone) que será la base de toda la práctica.

#### Instrucciones

1. Abre una terminal y navega a tu directorio de trabajo (por ejemplo, `~/labs` en macOS/Linux o `C:\labs` en Windows).

2. Crea el proyecto Angular con la bandera `--no-standalone` para usar el modo tradicional con NgModule:

```bash
ng new lab07-templates --no-standalone --routing=false --style=css
```

Cuando el CLI pregunte sobre la configuración, acepta los valores predeterminados.

3. Ingresa al directorio del proyecto:

```bash
cd lab07-templates
```

4. Verifica que la estructura del proyecto se creó correctamente:

```bash
# macOS/Linux
ls src/app

# Windows (PowerShell)
dir src\app
```

Deberías ver los archivos: `app.component.ts`, `app.component.html`, `app.component.css`, `app.module.ts`.

5. Inicia el servidor de desarrollo en una terminal separada (déjalo corriendo durante toda la práctica):

```bash
ng serve --open
```

#### Salida Esperada

El navegador abre automáticamente `http://localhost:4200` mostrando la página de bienvenida de Angular.

#### Verificación

En la terminal debes ver:
```
✔ Compiled successfully.
```

---

### Paso 2: Integrar Bootstrap 5

**Objetivo:** Instalar Bootstrap 5 y configurarlo en `angular.json` para que sus estilos y scripts estén disponibles en toda la aplicación.

#### Instrucciones

1. Detén el servidor de desarrollo con `Ctrl + C` en la terminal donde está corriendo.

2. Instala Bootstrap 5 como dependencia del proyecto:

```bash
npm install bootstrap@5
```

3. Abre el archivo `angular.json` en la raíz del proyecto y localiza la sección `"styles"` y `"scripts"` dentro de `projects → lab07-templates → architect → build → options`. Modifícalas para incluir Bootstrap:

```json
"styles": [
  "node_modules/bootstrap/dist/css/bootstrap.min.css",
  "src/styles.css"
],
"scripts": [
  "node_modules/bootstrap/dist/js/bootstrap.bundle.min.js"
]
```

> **Importante:** La ruta `node_modules/bootstrap/...` debe estar **antes** de `src/styles.css` para que tus estilos personalizados puedan sobrescribir los de Bootstrap cuando sea necesario.

4. Abre `src/styles.css` y agrega un estilo global de prueba:

```css
/* src/styles.css */
body {
  background-color: #f8f9fa;
}

.tabla-empleados {
  font-size: 0.9rem;
}

.fila-seleccionada {
  background-color: #cfe2ff !important;
}
```

5. Reinicia el servidor de desarrollo:

```bash
ng serve --open
```

6. Reemplaza el contenido de `src/app/app.component.html` con una prueba rápida de Bootstrap:

```html
<!-- src/app/app.component.html — prueba temporal -->
<div class="container mt-4">
  <div class="alert alert-success">
    ✅ Bootstrap 5 integrado correctamente en Angular
  </div>
</div>
```

#### Salida Esperada

El navegador muestra una alerta verde con el mensaje de confirmación, con la tipografía y estilos de Bootstrap aplicados.

#### Verificación

- La alerta tiene fondo verde con texto oscuro (estilos Bootstrap).
- En la consola del navegador no hay errores de CSS ni JavaScript.
- Angular DevTools (extensión Chrome) muestra el componente `AppComponent` en el árbol.

---

### Paso 3: Definir la Interfaz y los Datos de Empleados

**Objetivo:** Crear la interfaz TypeScript `Empleado` y los datos de prueba que alimentarán toda la aplicación.

#### Instrucciones

1. Crea la interfaz `Empleado` en un archivo dedicado:

```bash
# macOS/Linux
mkdir -p src/app/models
touch src/app/models/empleado.interface.ts

# Windows (PowerShell)
New-Item -ItemType Directory -Force -Path src\app\models
New-Item -ItemType File -Path src\app\models\empleado.interface.ts
```

2. Abre `src/app/models/empleado.interface.ts` y define la interfaz:

```typescript
// src/app/models/empleado.interface.ts
export interface Empleado {
  id: number;
  nombre: string;
  apellido: string;
  departamento: 'TI' | 'RRHH' | 'Ventas' | 'Finanzas' | 'Operaciones';
  puesto: string;
  salario: number;
  fechaContratacion: Date;
  activo: boolean;
  foto: string;
  email: string;
}
```

3. Abre `src/app/app.component.ts` y reemplaza su contenido con la clase del componente principal, que incluirá los datos y toda la lógica de la aplicación:

```typescript
// src/app/app.component.ts
import { Component, OnInit } from '@angular/core';
import { Empleado } from './models/empleado.interface';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit {

  // ── Título de la aplicación ──────────────────────────────────────────
  titulo: string = 'Sistema de Gestión de Empleados';
  fechaActual: Date = new Date();
  cargando: boolean = false;

  // ── Lista completa de empleados ──────────────────────────────────────
  empleados: Empleado[] = [
    {
      id: 1,
      nombre: 'Ana',
      apellido: 'García López',
      departamento: 'TI',
      puesto: 'Desarrolladora Frontend',
      salario: 32000,
      fechaContratacion: new Date('2021-03-15'),
      activo: true,
      foto: 'https://i.pravatar.cc/48?img=1',
      email: 'ana.garcia@empresa.com'
    },
    {
      id: 2,
      nombre: 'Carlos',
      apellido: 'Mendoza Ruiz',
      departamento: 'Ventas',
      puesto: 'Ejecutivo de Ventas',
      salario: 22000,
      fechaContratacion: new Date('2020-07-01'),
      activo: true,
      foto: 'https://i.pravatar.cc/48?img=3',
      email: 'carlos.mendoza@empresa.com'
    },
    {
      id: 3,
      nombre: 'Laura',
      apellido: 'Torres Vega',
      departamento: 'RRHH',
      puesto: 'Coordinadora de Recursos Humanos',
      salario: 27500,
      fechaContratacion: new Date('2019-11-20'),
      activo: false,
      foto: 'https://i.pravatar.cc/48?img=5',
      email: 'laura.torres@empresa.com'
    },
    {
      id: 4,
      nombre: 'Roberto',
      apellido: 'Sánchez Mora',
      departamento: 'Finanzas',
      puesto: 'Analista Financiero',
      salario: 35000,
      fechaContratacion: new Date('2022-01-10'),
      activo: true,
      foto: 'https://i.pravatar.cc/48?img=7',
      email: 'roberto.sanchez@empresa.com'
    },
    {
      id: 5,
      nombre: 'María',
      apellido: 'Jiménez Castro',
      departamento: 'TI',
      puesto: 'Arquitecta de Software',
      salario: 48000,
      fechaContratacion: new Date('2018-05-30'),
      activo: true,
      foto: 'https://i.pravatar.cc/48?img=9',
      email: 'maria.jimenez@empresa.com'
    },
    {
      id: 6,
      nombre: 'Pedro',
      apellido: 'Ramírez Flores',
      departamento: 'Operaciones',
      puesto: 'Supervisor de Operaciones',
      salario: 29000,
      fechaContratacion: new Date('2020-09-14'),
      activo: false,
      foto: 'https://i.pravatar.cc/48?img=11',
      email: 'pedro.ramirez@empresa.com'
    }
  ];

  // ── Estado de la UI ──────────────────────────────────────────────────
  empleadoSeleccionado: Empleado | null = null;
  terminoBusqueda: string = '';
  mostrarFormulario: boolean = false;
  mensajeExito: string = '';

  // ── Empleados filtrados (calculado) ─────────────────────────────────
  get empleadosFiltrados(): Empleado[] {
    if (!this.terminoBusqueda.trim()) {
      return this.empleados;
    }
    const termino = this.terminoBusqueda.toLowerCase();
    return this.empleados.filter(e =>
      e.nombre.toLowerCase().includes(termino) ||
      e.apellido.toLowerCase().includes(termino) ||
      e.departamento.toLowerCase().includes(termino) ||
      e.puesto.toLowerCase().includes(termino)
    );
  }

  // ── Nuevo empleado (para el formulario) ─────────────────────────────
  nuevoEmpleado: Partial<Empleado> = this.inicializarFormulario();

  // ── Ciclo de vida ────────────────────────────────────────────────────
  ngOnInit(): void {
    console.log('AppComponent inicializado. Total empleados:', this.empleados.length);
  }

  // ── Métodos del componente ───────────────────────────────────────────

  seleccionarEmpleado(empleado: Empleado): void {
    this.empleadoSeleccionado = empleado;
  }

  limpiarSeleccion(): void {
    this.empleadoSeleccionado = null;
  }

  toggleFormulario(): void {
    this.mostrarFormulario = !this.mostrarFormulario;
    if (!this.mostrarFormulario) {
      this.nuevoEmpleado = this.inicializarFormulario();
    }
  }

  agregarEmpleado(): void {
    const empleado: Empleado = {
      id: this.empleados.length + 1,
      nombre: this.nuevoEmpleado.nombre || '',
      apellido: this.nuevoEmpleado.apellido || '',
      departamento: this.nuevoEmpleado.departamento as Empleado['departamento'] || 'TI',
      puesto: this.nuevoEmpleado.puesto || '',
      salario: Number(this.nuevoEmpleado.salario) || 0,
      fechaContratacion: new Date(this.nuevoEmpleado.fechaContratacion as any || new Date()),
      activo: true,
      foto: `https://i.pravatar.cc/48?img=${this.empleados.length + 20}`,
      email: `${(this.nuevoEmpleado.nombre || '').toLowerCase()}.${(this.nuevoEmpleado.apellido || '').toLowerCase().split(' ')[0]}@empresa.com`
    };
    this.empleados.push(empleado);
    this.mensajeExito = `✅ Empleado "${empleado.nombre} ${empleado.apellido}" agregado exitosamente.`;
    this.nuevoEmpleado = this.inicializarFormulario();
    this.mostrarFormulario = false;
    setTimeout(() => this.mensajeExito = '', 4000);
  }

  toggleEstado(empleado: Empleado): void {
    empleado.activo = !empleado.activo;
  }

  obtenerColorSalario(salario: number): string {
    if (salario >= 40000) return '#d1e7dd';
    if (salario >= 30000) return '#fff3cd';
    return '#f8d7da';
  }

  buscarConEnter(termino: string): void {
    this.terminoBusqueda = termino;
  }

  private inicializarFormulario(): Partial<Empleado> {
    return {
      nombre: '',
      apellido: '',
      departamento: 'TI',
      puesto: '',
      salario: undefined,
      fechaContratacion: undefined
    };
  }
}
```

4. Verifica que no haya errores de TypeScript en la terminal del servidor de desarrollo.

#### Salida Esperada

La terminal del servidor de desarrollo muestra `Compiled successfully.` sin errores de TypeScript.

#### Verificación

- En la consola del navegador (F12) aparece el mensaje: `AppComponent inicializado. Total empleados: 6`
- Angular DevTools muestra el `AppComponent` con las propiedades `empleados` (array de 6 elementos), `titulo` y `cargando`.

---

### Paso 4: Habilitar FormsModule en AppModule

**Objetivo:** Importar `FormsModule` en el módulo raíz para habilitar `[(ngModel)]` y las directivas de formularios template-driven.

#### Instrucciones

1. Abre `src/app/app.module.ts` y agrega `FormsModule` a los imports:

```typescript
// src/app/app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms';   // ← AGREGAR ESTA LÍNEA

import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule    // ← AGREGAR AQUÍ
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

#### Salida Esperada

El servidor de desarrollo recompila sin errores. Sin `FormsModule`, el uso de `[(ngModel)]` en el Paso 7 generaría el error: `Can't bind to 'ngModel' since it isn't a known property of 'input'`.

#### Verificación

La terminal muestra `Compiled successfully.` después del cambio.

---

### Paso 5: Construir la Navbar y la Tabla de Empleados

**Objetivo:** Implementar el template principal con la barra de navegación, el buscador con template reference variable y la tabla de empleados usando `*ngFor`, `*ngSwitch`, `[ngClass]`, `[ngStyle]` y pipes.

#### Instrucciones

1. Reemplaza completamente el contenido de `src/app/app.component.html` con el siguiente template:

```html
<!-- src/app/app.component.html -->

<!-- ═══════════════════════════════════════════════════════════
     NAVBAR — Interpolación y DatePipe
     ═══════════════════════════════════════════════════════════ -->
<nav class="navbar navbar-dark bg-primary mb-4">
  <div class="container-fluid">
    <!-- Interpolación básica -->
    <span class="navbar-brand fw-bold">
      🏢 {{ titulo }}
    </span>
    <!-- DatePipe: formato de fecha personalizado -->
    <span class="text-white-50 small">
      {{ fechaActual | date:'EEEE, d \'de\' MMMM yyyy':'':'es' }}
    </span>
  </div>
</nav>

<div class="container">

  <!-- ═══════════════════════════════════════════════════════════
       MENSAJE DE ÉXITO — *ngIf
       ═══════════════════════════════════════════════════════════ -->
  <div *ngIf="mensajeExito" class="alert alert-success alert-dismissible fade show" role="alert">
    {{ mensajeExito }}
  </div>

  <!-- ═══════════════════════════════════════════════════════════
       BARRA DE HERRAMIENTAS: Buscador + Botón Nuevo Empleado
       Template reference variable: #searchInput
       ═══════════════════════════════════════════════════════════ -->
  <div class="row mb-3 align-items-center">
    <div class="col-md-6">
      <div class="input-group">
        <!-- Template reference variable #searchInput -->
        <input
          #searchInput
          type="text"
          class="form-control"
          placeholder="Buscar por nombre, departamento o puesto..."
          [(ngModel)]="terminoBusqueda"
          (keyup.enter)="buscarConEnter(searchInput.value)"
        />
        <button
          class="btn btn-outline-secondary"
          type="button"
          (click)="terminoBusqueda = ''"
          [disabled]="!terminoBusqueda"
        >
          ✕ Limpiar
        </button>
      </div>
      <!-- Interpolación: contador de resultados -->
      <small class="text-muted">
        Mostrando {{ empleadosFiltrados.length }} de {{ empleados.length }} empleados
      </small>
    </div>
    <div class="col-md-6 text-end">
      <button
        class="btn btn-success"
        (click)="toggleFormulario()"
      >
        <!-- Property binding en el texto del botón con operador ternario -->
        {{ mostrarFormulario ? '✕ Cancelar' : '＋ Nuevo Empleado' }}
      </button>
    </div>
  </div>

  <!-- ═══════════════════════════════════════════════════════════
       TABLA DE EMPLEADOS
       *ngFor con index, even, odd + *ngSwitch + [ngClass] + [ngStyle] + pipes
       ═══════════════════════════════════════════════════════════ -->
  <div class="card shadow-sm mb-4">
    <div class="card-header bg-white d-flex justify-content-between align-items-center">
      <h5 class="mb-0">📋 Directorio de Empleados</h5>
      <!-- *ngIf con ng-template (else) -->
      <span *ngIf="!cargando; else spinnerTemplate" class="badge bg-primary rounded-pill">
        {{ empleados.length }} empleados
      </span>
      <ng-template #spinnerTemplate>
        <div class="spinner-border spinner-border-sm text-primary" role="status">
          <span class="visually-hidden">Cargando...</span>
        </div>
      </ng-template>
    </div>

    <div class="card-body p-0">
      <div class="table-responsive">
        <table class="table table-hover tabla-empleados mb-0">
          <thead class="table-dark">
            <tr>
              <th>#</th>
              <th>Foto</th>
              <th>Nombre</th>
              <th>Departamento</th>
              <th>Puesto</th>
              <th>Salario</th>
              <th>Contratación</th>
              <th>Estado</th>
              <th>Acciones</th>
            </tr>
          </thead>
          <tbody>
            <!-- *ngIf: mensaje cuando no hay resultados -->
            <tr *ngIf="empleadosFiltrados.length === 0">
              <td colspan="9" class="text-center text-muted py-4">
                🔍 No se encontraron empleados con "{{ terminoBusqueda }}"
              </td>
            </tr>

            <!-- *ngFor con todas las variables de contexto -->
            <tr
              *ngFor="let empleado of empleadosFiltrados; let i = index; let esPar = even; let esImpar = odd; let esPrimero = first; let esUltimo = last"
              (click)="seleccionarEmpleado(empleado)"
              [class.fila-seleccionada]="empleadoSeleccionado?.id === empleado.id"
              [ngClass]="{
                'table-secondary': !empleado.activo,
                'fw-bold': esPrimero
              }"
              [ngStyle]="{ 'border-left': '4px solid ' + obtenerColorSalario(empleado.salario) }"
              style="cursor: pointer;"
            >
              <!-- Índice (1-based) con badge para par/impar -->
              <td>
                <span
                  class="badge"
                  [ngClass]="esPar ? 'bg-info' : 'bg-secondary'"
                >
                  {{ i + 1 }}
                </span>
              </td>

              <!-- Foto con property binding en [src] y [alt] -->
              <td>
                <img
                  [src]="empleado.foto"
                  [alt]="'Foto de ' + empleado.nombre"
                  class="rounded-circle"
                  width="36"
                  height="36"
                />
              </td>

              <!-- Nombre con UpperCasePipe en apellido -->
              <td>
                {{ empleado.nombre }} <strong>{{ empleado.apellido | uppercase | slice:0:15 }}</strong>
                <br>
                <small class="text-muted">{{ empleado.email }}</small>
              </td>

              <!-- *ngSwitch para ícono de departamento -->
              <td>
                <span [ngSwitch]="empleado.departamento">
                  <span *ngSwitchCase="'TI'">💻</span>
                  <span *ngSwitchCase="'Ventas'">📈</span>
                  <span *ngSwitchCase="'RRHH'">👥</span>
                  <span *ngSwitchCase="'Finanzas'">💰</span>
                  <span *ngSwitchCase="'Operaciones'">⚙️</span>
                  <span *ngSwitchDefault>🏢</span>
                </span>
                {{ empleado.departamento }}
              </td>

              <!-- Puesto con SlicePipe para truncar texto largo -->
              <td>{{ empleado.puesto | slice:0:25 }}{{ empleado.puesto.length > 25 ? '...' : '' }}</td>

              <!-- Salario con CurrencyPipe -->
              <td>
                <span
                  class="fw-semibold"
                  [ngStyle]="{ color: empleado.salario >= 40000 ? '#198754' : empleado.salario >= 30000 ? '#856404' : '#842029' }"
                >
                  {{ empleado.salario | currency:'MXN':'symbol-narrow':'1.0-0' }}
                </span>
              </td>

              <!-- Fecha con DatePipe -->
              <td>{{ empleado.fechaContratacion | date:'dd/MM/yyyy' }}</td>

              <!-- Estado con badge dinámico usando [ngClass] -->
              <td>
                <span
                  class="badge"
                  [ngClass]="empleado.activo ? 'bg-success' : 'bg-danger'"
                >
                  {{ empleado.activo ? 'Activo' : 'Inactivo' }}
                </span>
              </td>

              <!-- Botón de acción: toggle estado -->
              <td>
                <button
                  class="btn btn-sm"
                  [ngClass]="empleado.activo ? 'btn-outline-danger' : 'btn-outline-success'"
                  (click)="toggleEstado(empleado); $event.stopPropagation()"
                  [title]="empleado.activo ? 'Desactivar empleado' : 'Activar empleado'"
                >
                  {{ empleado.activo ? '🚫' : '✅' }}
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>

  <!-- ═══════════════════════════════════════════════════════════
       PANEL DE DETALLES — *ngIf con empleadoSeleccionado
       ═══════════════════════════════════════════════════════════ -->
  <div *ngIf="empleadoSeleccionado; else sinSeleccion" class="card border-primary mb-4">
    <div class="card-header bg-primary text-white d-flex justify-content-between">
      <h5 class="mb-0">🔍 Detalles del Empleado</h5>
      <button class="btn btn-sm btn-outline-light" (click)="limpiarSeleccion()">✕ Cerrar</button>
    </div>
    <div class="card-body">
      <div class="row align-items-center">
        <div class="col-md-2 text-center">
          <img
            [src]="empleadoSeleccionado.foto"
            [alt]="empleadoSeleccionado.nombre"
            class="rounded-circle border border-primary"
            width="80"
            height="80"
          />
        </div>
        <div class="col-md-5">
          <!-- UpperCasePipe en nombre completo -->
          <h4>{{ (empleadoSeleccionado.nombre + ' ' + empleadoSeleccionado.apellido) | uppercase }}</h4>
          <p class="mb-1"><strong>Puesto:</strong> {{ empleadoSeleccionado.puesto }}</p>
          <p class="mb-1"><strong>Email:</strong> {{ empleadoSeleccionado.email }}</p>
          <p class="mb-0">
            <strong>Estado:</strong>
            <span
              class="badge ms-1"
              [ngClass]="empleadoSeleccionado.activo ? 'bg-success' : 'bg-danger'"
            >
              {{ empleadoSeleccionado.activo ? 'Activo' : 'Inactivo' }}
            </span>
          </p>
        </div>
        <div class="col-md-5">
          <p class="mb-1">
            <strong>Departamento:</strong> {{ empleadoSeleccionado.departamento }}
          </p>
          <!-- CurrencyPipe con configuración completa -->
          <p class="mb-1">
            <strong>Salario:</strong>
            {{ empleadoSeleccionado.salario | currency:'MXN':'symbol-narrow':'1.2-2' }} MXN/mes
          </p>
          <!-- DatePipe con formato largo -->
          <p class="mb-1">
            <strong>Contratado el:</strong>
            {{ empleadoSeleccionado.fechaContratacion | date:'dd \'de\' MMMM \'de\' yyyy':'':'es' }}
          </p>
          <!-- JsonPipe para depuración (solo en desarrollo) -->
          <details class="mt-2">
            <summary class="text-muted small" style="cursor:pointer">Ver datos en JSON (debug)</summary>
            <pre class="bg-light p-2 rounded small mt-1">{{ empleadoSeleccionado | json }}</pre>
          </details>
        </div>
      </div>
    </div>
  </div>

  <!-- ng-template para el else del panel de detalles -->
  <ng-template #sinSeleccion>
    <div class="alert alert-info mb-4">
      👆 Haz clic en cualquier fila de la tabla para ver los detalles del empleado.
    </div>
  </ng-template>

</div>
<!-- Fin del container — el formulario se agrega en el Paso 6 -->
```

2. Guarda el archivo y verifica que el servidor de desarrollo compile sin errores.

#### Salida Esperada

El navegador muestra:
- Navbar azul con el título de la aplicación y la fecha actual
- Campo de búsqueda funcional con botón "Limpiar"
- Tabla con los 6 empleados, fotos, badges de departamento con íconos, salarios en MXN, fechas formateadas y badges de estado (verde/rojo)
- Mensaje informativo debajo de la tabla invitando a seleccionar un empleado

#### Verificación

1. Escribe "TI" en el buscador → la tabla filtra y muestra solo los empleados de TI (2 filas).
2. Haz clic en un empleado → aparece el panel de detalles con todos sus datos.
3. Haz clic en el botón 🚫 de un empleado activo → el badge cambia a "Inactivo" (rojo) y la fila se atenúa.
4. En Angular DevTools, inspecciona `AppComponent` y verifica que `empleadoSeleccionado` se actualiza al hacer clic.

---

### Paso 6: Implementar el Formulario Template-Driven

**Objetivo:** Agregar el formulario de alta de empleados con validación visual usando `ngModel`, directivas de validación Angular y las clases `is-valid`/`is-invalid` de Bootstrap.

#### Instrucciones

1. Abre `src/app/app.component.html` y **antes** de la etiqueta de cierre `</div>` del contenedor principal (al final del archivo), agrega el siguiente bloque del formulario:

```html
  <!-- ═══════════════════════════════════════════════════════════
       FORMULARIO TEMPLATE-DRIVEN — *ngIf + ngModel + validación
       ═══════════════════════════════════════════════════════════ -->
  <div *ngIf="mostrarFormulario" class="card border-success mb-4">
    <div class="card-header bg-success text-white">
      <h5 class="mb-0">➕ Registrar Nuevo Empleado</h5>
    </div>
    <div class="card-body">

      <!-- Template reference variable #formEmpleado para acceder al estado del formulario -->
      <form #formEmpleado="ngForm" (ngSubmit)="formEmpleado.valid && agregarEmpleado()" novalidate>

        <div class="row g-3">

          <!-- Campo: Nombre -->
          <div class="col-md-6">
            <label for="inputNombre" class="form-label fw-semibold">
              Nombre <span class="text-danger">*</span>
            </label>
            <input
              id="inputNombre"
              name="nombre"
              type="text"
              class="form-control"
              placeholder="Ej. Juan"
              [(ngModel)]="nuevoEmpleado.nombre"
              #campoNombre="ngModel"
              required
              minlength="2"
              [ngClass]="{
                'is-valid': campoNombre.valid && campoNombre.touched,
                'is-invalid': campoNombre.invalid && campoNombre.touched
              }"
            />
            <div class="valid-feedback">✓ Nombre válido</div>
            <div class="invalid-feedback">
              <span *ngIf="campoNombre.errors?.['required']">El nombre es obligatorio.</span>
              <span *ngIf="campoNombre.errors?.['minlength']">Mínimo 2 caracteres.</span>
            </div>
          </div>

          <!-- Campo: Apellido -->
          <div class="col-md-6">
            <label for="inputApellido" class="form-label fw-semibold">
              Apellido(s) <span class="text-danger">*</span>
            </label>
            <input
              id="inputApellido"
              name="apellido"
              type="text"
              class="form-control"
              placeholder="Ej. Pérez González"
              [(ngModel)]="nuevoEmpleado.apellido"
              #campoApellido="ngModel"
              required
              minlength="2"
              [ngClass]="{
                'is-valid': campoApellido.valid && campoApellido.touched,
                'is-invalid': campoApellido.invalid && campoApellido.touched
              }"
            />
            <div class="valid-feedback">✓ Apellido válido</div>
            <div class="invalid-feedback">
              <span *ngIf="campoApellido.errors?.['required']">El apellido es obligatorio.</span>
              <span *ngIf="campoApellido.errors?.['minlength']">Mínimo 2 caracteres.</span>
            </div>
          </div>

          <!-- Campo: Departamento (select con *ngFor) -->
          <div class="col-md-4">
            <label for="inputDepartamento" class="form-label fw-semibold">
              Departamento <span class="text-danger">*</span>
            </label>
            <select
              id="inputDepartamento"
              name="departamento"
              class="form-select"
              [(ngModel)]="nuevoEmpleado.departamento"
              #campoDepartamento="ngModel"
              required
              [ngClass]="{
                'is-valid': campoDepartamento.valid && campoDepartamento.touched,
                'is-invalid': campoDepartamento.invalid && campoDepartamento.touched
              }"
            >
              <option value="">-- Seleccionar --</option>
              <option *ngFor="let dep of ['TI', 'RRHH', 'Ventas', 'Finanzas', 'Operaciones']" [value]="dep">
                {{ dep }}
              </option>
            </select>
            <div class="invalid-feedback">Selecciona un departamento.</div>
          </div>

          <!-- Campo: Puesto -->
          <div class="col-md-8">
            <label for="inputPuesto" class="form-label fw-semibold">
              Puesto <span class="text-danger">*</span>
            </label>
            <input
              id="inputPuesto"
              name="puesto"
              type="text"
              class="form-control"
              placeholder="Ej. Desarrollador Backend"
              [(ngModel)]="nuevoEmpleado.puesto"
              #campoPuesto="ngModel"
              required
              minlength="3"
              [ngClass]="{
                'is-valid': campoPuesto.valid && campoPuesto.touched,
                'is-invalid': campoPuesto.invalid && campoPuesto.touched
              }"
            />
            <div class="valid-feedback">✓ Puesto válido</div>
            <div class="invalid-feedback">
              <span *ngIf="campoPuesto.errors?.['required']">El puesto es obligatorio.</span>
              <span *ngIf="campoPuesto.errors?.['minlength']">Mínimo 3 caracteres.</span>
            </div>
          </div>

          <!-- Campo: Salario -->
          <div class="col-md-4">
            <label for="inputSalario" class="form-label fw-semibold">
              Salario Mensual (MXN) <span class="text-danger">*</span>
            </label>
            <div class="input-group">
              <span class="input-group-text">$</span>
              <input
                id="inputSalario"
                name="salario"
                type="number"
                class="form-control"
                placeholder="Ej. 25000"
                [(ngModel)]="nuevoEmpleado.salario"
                #campoSalario="ngModel"
                required
                min="5000"
                max="200000"
                [ngClass]="{
                  'is-valid': campoSalario.valid && campoSalario.touched,
                  'is-invalid': campoSalario.invalid && campoSalario.touched
                }"
              />
            </div>
            <div class="form-text">
              <!-- Two-way binding en tiempo real con CurrencyPipe -->
              <span *ngIf="nuevoEmpleado.salario">
                Equivale a: <strong>{{ nuevoEmpleado.salario | currency:'MXN':'symbol-narrow':'1.0-0' }}</strong> MXN
              </span>
            </div>
            <div
              class="invalid-feedback d-block"
              *ngIf="campoSalario.invalid && campoSalario.touched"
            >
              <span *ngIf="campoSalario.errors?.['required']">El salario es obligatorio.</span>
              <span *ngIf="campoSalario.errors?.['min']">El salario mínimo es $5,000.</span>
              <span *ngIf="campoSalario.errors?.['max']">El salario máximo es $200,000.</span>
            </div>
          </div>

          <!-- Campo: Fecha de Contratación -->
          <div class="col-md-4">
            <label for="inputFecha" class="form-label fw-semibold">
              Fecha de Contratación <span class="text-danger">*</span>
            </label>
            <input
              id="inputFecha"
              name="fechaContratacion"
              type="date"
              class="form-control"
              [(ngModel)]="nuevoEmpleado.fechaContratacion"
              #campoFecha="ngModel"
              required
              [ngClass]="{
                'is-valid': campoFecha.valid && campoFecha.touched,
                'is-invalid': campoFecha.invalid && campoFecha.touched
              }"
            />
            <div class="invalid-feedback">La fecha de contratación es obligatoria.</div>
          </div>

          <!-- Vista previa en tiempo real (two-way binding) -->
          <div class="col-12" *ngIf="nuevoEmpleado.nombre || nuevoEmpleado.apellido">
            <div class="alert alert-light border">
              <strong>Vista previa:</strong>
              {{ nuevoEmpleado.nombre | uppercase }} {{ nuevoEmpleado.apellido | uppercase }}
              <span *ngIf="nuevoEmpleado.departamento" class="badge bg-secondary ms-2">
                {{ nuevoEmpleado.departamento }}
              </span>
            </div>
          </div>

        </div><!-- /row -->

        <!-- Botones del formulario -->
        <div class="d-flex gap-2 mt-4 justify-content-end">
          <button
            type="button"
            class="btn btn-outline-secondary"
            (click)="toggleFormulario()"
          >
            Cancelar
          </button>
          <button
            type="submit"
            class="btn btn-success"
            [disabled]="formEmpleado.invalid"
          >
            💾 Guardar Empleado
          </button>
        </div>

        <!-- Estado del formulario para depuración (solo en desarrollo) -->
        <details class="mt-3">
          <summary class="text-muted small" style="cursor:pointer">
            Estado del formulario (debug) — válido: {{ formEmpleado.valid }}
          </summary>
          <pre class="bg-light p-2 rounded small mt-1">{{ nuevoEmpleado | json }}</pre>
        </details>

      </form>
    </div><!-- /card-body -->
  </div>
  <!-- ═══════════════════════════════════════════════════════════
       FIN DEL FORMULARIO
       ═══════════════════════════════════════════════════════════ -->

</div><!-- /container -->
```

2. Guarda el archivo. El servidor de desarrollo recompilará automáticamente.

#### Salida Esperada

Al hacer clic en el botón "＋ Nuevo Empleado":
- Aparece el formulario con todos los campos
- Los campos muestran borde rojo (`is-invalid`) al perder el foco sin valor
- El campo de salario muestra la conversión en tiempo real (ej. `$25,000 MXN`) mientras se escribe
- La vista previa del nombre aparece en tiempo real usando two-way binding
- El botón "Guardar Empleado" permanece deshabilitado mientras el formulario sea inválido

#### Verificación

1. Haz clic en "＋ Nuevo Empleado" → el formulario aparece con animación.
2. Haz clic en el campo "Nombre" y luego presiona Tab sin escribir → aparece el borde rojo y el mensaje "El nombre es obligatorio."
3. Escribe "J" en el campo Nombre → aparece el mensaje "Mínimo 2 caracteres."
4. Escribe "Juan" → el borde cambia a verde y aparece "✓ Nombre válido."
5. Completa todos los campos con datos válidos → el botón "Guardar Empleado" se habilita.
6. Haz clic en "Guardar Empleado" → el empleado aparece al final de la tabla y se muestra el mensaje de éxito verde durante 4 segundos.

---

### Paso 7: Agregar Estilos CSS Personalizados

**Objetivo:** Complementar Bootstrap con estilos CSS propios en el componente para mejorar la experiencia visual.

#### Instrucciones

1. Abre `src/app/app.component.css` y agrega los siguientes estilos:

```css
/* src/app/app.component.css */

/* Animación de entrada para el panel de detalles y el formulario */
.card {
  animation: fadeIn 0.3s ease-in;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-8px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Resaltar la fila seleccionada */
.fila-seleccionada {
  background-color: #cfe2ff !important;
  box-shadow: inset 3px 0 0 #0d6efd;
}

/* Hover en filas de la tabla */
.tabla-empleados tbody tr:hover {
  background-color: #e8f4fd;
  transition: background-color 0.15s ease;
}

/* Estilo para el detalle JSON de depuración */
pre {
  max-height: 150px;
  overflow-y: auto;
  font-size: 0.75rem;
}

/* Estilos para el campo de búsqueda */
.input-group .form-control:focus {
  border-color: #0d6efd;
  box-shadow: 0 0 0 0.2rem rgba(13, 110, 253, 0.15);
}
```

2. Guarda el archivo y verifica los cambios en el navegador.

#### Salida Esperada

Las tarjetas (card) tienen una animación suave al aparecer. Las filas de la tabla muestran un efecto hover con transición de color.

#### Verificación

Haz clic en el botón "＋ Nuevo Empleado" y observa la animación de entrada del formulario. Pasa el cursor sobre las filas de la tabla para verificar el efecto hover.

---

## Validación y Pruebas Finales

Una vez completados todos los pasos, realiza las siguientes pruebas para confirmar que la aplicación funciona correctamente en su totalidad:

### Lista de Verificación Completa

| # | Prueba | Mecanismo Angular | Resultado Esperado |
|---|---|---|---|
| 1 | La navbar muestra el título y la fecha actual | Interpolación + DatePipe | Fecha en formato "lunes, 5 de enero 2025" |
| 2 | Escribir en el buscador filtra la tabla en tiempo real | `[(ngModel)]` + getter computado | La tabla se actualiza con cada tecla |
| 3 | Presionar Enter en el buscador ejecuta la búsqueda | `(keyup.enter)` + template ref `#searchInput` | El filtro se aplica |
| 4 | El botón "Limpiar" se deshabilita cuando el campo está vacío | `[disabled]="!terminoBusqueda"` | Botón deshabilitado al inicio |
| 5 | La tabla muestra íconos según el departamento | `*ngSwitch` | 💻 para TI, 📈 para Ventas, etc. |
| 6 | Las filas pares tienen badge azul, impares gris | `*ngFor` + `even/odd` + `[ngClass]` | Badges de colores alternados |
| 7 | El borde izquierdo de cada fila refleja el rango salarial | `[ngStyle]` + método `obtenerColorSalario()` | Verde/amarillo/rojo según salario |
| 8 | Hacer clic en una fila resalta la fila y muestra el panel | `(click)` + `[class.fila-seleccionada]` | Fila azul + panel de detalles |
| 9 | El panel de detalles muestra el nombre en mayúsculas | `UpperCasePipe` encadenado | "ANA GARCÍA LÓPEZ" |
| 10 | El salario en el panel muestra 2 decimales | `CurrencyPipe` con formato `'1.2-2'` | "$32,000.00 MXN" |
| 11 | El JsonPipe muestra el objeto completo en el panel | `JsonPipe` en `<pre>` | Objeto JSON formateado |
| 12 | El botón 🚫/✅ cambia el estado del empleado | `(click)` + `$event.stopPropagation()` | Badge cambia sin seleccionar la fila |
| 13 | El formulario muestra `is-invalid` al tocar campo vacío | `ngModel` + `[ngClass]` | Borde rojo + mensaje de error |
| 14 | El formulario muestra `is-valid` con datos correctos | `ngModel` + `[ngClass]` | Borde verde + "✓ válido" |
| 15 | La vista previa del formulario se actualiza en tiempo real | `[(ngModel)]` two-way binding | El nombre aparece en mayúsculas al escribir |
| 16 | El botón "Guardar" se habilita solo cuando el form es válido | `[disabled]="formEmpleado.invalid"` | Botón deshabilitado con campos inválidos |
| 17 | Al guardar, el nuevo empleado aparece en la tabla | `push()` en el arreglo | Nueva fila al final de la tabla |
| 18 | El mensaje de éxito desaparece tras 4 segundos | `*ngIf` + `setTimeout()` | Alerta verde que se oculta sola |

### Prueba con Angular DevTools

1. Abre Angular DevTools en Chrome (F12 → pestaña "Angular").
2. Selecciona el componente `AppComponent` en el árbol.
3. Verifica que las propiedades `empleados`, `terminoBusqueda` y `empleadoSeleccionado` son visibles.
4. Escribe en el buscador y observa cómo `terminoBusqueda` se actualiza en tiempo real en DevTools.
5. Haz clic en un empleado y confirma que `empleadoSeleccionado` muestra el objeto del empleado seleccionado.

---

## Solución de Problemas

### Problema 1: `Can't bind to 'ngModel' since it isn't a known property of 'input'`

**Síntomas:**
- La aplicación no compila.
- La terminal del servidor de desarrollo muestra el error: `NG0303: Can't bind to 'ngModel' since it isn't a known property of 'input'`.
- El formulario no aparece y la consola del navegador también reporta el error.

**Causa:**
`FormsModule` no está importado en `AppModule`. Angular requiere que `FormsModule` esté declarado en el módulo para poder usar la directiva `ngModel` en los templates.

**Solución:**

Abre `src/app/app.module.ts` y verifica que `FormsModule` esté correctamente importado:

```typescript
import { FormsModule } from '@angular/forms';  // ← Verificar esta línea

@NgModule({
  imports: [
    BrowserModule,
    FormsModule    // ← Verificar que esté aquí
  ],
  // ...
})
export class AppModule { }
```

Después de guardar, el servidor de desarrollo recompilará automáticamente.

---

### Problema 2: Los estilos de Bootstrap no se aplican (la página aparece sin estilos)

**Síntomas:**
- La aplicación compila sin errores pero se ve sin estilos (texto sin formato, sin colores, sin grid).
- La navbar no tiene color azul.
- Los botones no tienen el estilo Bootstrap.

**Causa:**
Las rutas de Bootstrap en `angular.json` son incorrectas o Bootstrap no fue instalado correctamente. También puede ocurrir si se modificó `angular.json` mientras el servidor de desarrollo estaba corriendo, ya que los cambios en `angular.json` **requieren reiniciar el servidor**.

**Solución:**

1. Verifica que Bootstrap está instalado:
   ```bash
   # Debe mostrar la carpeta bootstrap dentro de node_modules
   ls node_modules | grep bootstrap
   ```

2. Si no está instalado, instálalo:
   ```bash
   npm install bootstrap@5
   ```

3. Verifica que las rutas en `angular.json` son exactamente:
   ```json
   "styles": [
     "node_modules/bootstrap/dist/css/bootstrap.min.css",
     "src/styles.css"
   ],
   "scripts": [
     "node_modules/bootstrap/dist/js/bootstrap.bundle.min.js"
   ]
   ```

4. **Detén el servidor de desarrollo** (`Ctrl + C`) y reinícialo:
   ```bash
   ng serve --open
   ```

> **Nota importante:** Cualquier cambio en `angular.json` requiere reiniciar el servidor de desarrollo. El hot-reload de Angular CLI no detecta cambios en este archivo de configuración.

---

## Limpieza

Al finalizar la práctica, puedes detener el servidor de desarrollo y opcionalmente archivar el proyecto:

```bash
# 1. Detener el servidor de desarrollo
# Presiona Ctrl + C en la terminal donde corre ng serve

# 2. (Opcional) Comprimir el proyecto para entrega
# macOS/Linux
cd ..
tar -czf lab07-templates-entrega.tar.gz lab07-templates/

# Windows (PowerShell)
Compress-Archive -Path lab07-templates -DestinationPath lab07-templates-entrega.zip

# 3. (Opcional) Limpiar la caché de Angular CLI
cd lab07-templates
ng cache clean
```

> **No elimines** el directorio `lab07-templates` si planeas usarlo como base para prácticas posteriores del curso.

---

## Resumen

En esta práctica construiste una aplicación Angular completa de gestión de empleados que integra de forma coherente todos los mecanismos de la sintaxis de templates:

| Mecanismo | Dónde se aplicó |
|---|---|
| **Interpolación `{{ }}`** | Título, contador de empleados, nombre en tabla, mensajes condicionales |
| **Property binding `[ ]`** | `[src]` en imágenes, `[disabled]` en botones, `[title]` en tooltips |
| **Event binding `( )`** | `(click)` para selección, `(keyup.enter)` para búsqueda, `(ngSubmit)` en formulario |
| **Two-way binding `[( )]`** | `[(ngModel)]` en buscador y todos los campos del formulario |
| **`*ngFor`** | Tabla de empleados con `index`, `even`, `odd`, `first`, `last` |
| **`*ngIf` / `ng-template`** | Panel de detalles, formulario, mensaje de éxito, spinner, mensaje vacío |
| **`*ngSwitch`** | Íconos de departamento en la tabla |
| **`[ngClass]`** | Badges de estado, colores de índice, validación de formulario |
| **`[ngStyle]`** | Color del borde según salario, color del texto de salario |
| **Template reference variables `#`** | `#searchInput` para búsqueda, `#formEmpleado` para estado del form, `#campoNombre` para validación |
| **Pipes** | `DatePipe`, `CurrencyPipe`, `UpperCasePipe`, `SlicePipe`, `JsonPipe` encadenados |
| **Formulario template-driven** | Validación con `required`, `minlength`, `min`, `max` y clases Bootstrap `is-valid`/`is-invalid` |

### Conceptos Clave para Recordar

- Las **expresiones de template** se evalúan en el contexto del componente y no deben tener efectos secundarios.
- El **contexto del template** incluye propiedades del componente, variables `#` y variables de directivas (`let i = index`).
- `FormsModule` es **obligatorio** para usar `[(ngModel)]`; debe importarse en el módulo correspondiente.
- Los cambios en `angular.json` (como agregar Bootstrap) **requieren reiniciar** el servidor de desarrollo.
- `$event.stopPropagation()` evita que los eventos se propaguen a elementos padre, esencial cuando hay múltiples listeners en elementos anidados.

### Recursos Adicionales

- [Documentación oficial Angular: Sintaxis de Templates](https://angular.io/guide/template-syntax)
- [Documentación oficial Angular: Directivas estructurales](https://angular.io/guide/structural-directives)
- [Documentación oficial Angular: Pipes integrados](https://angular.io/api?type=pipe)
- [Documentación oficial Angular: Formularios template-driven](https://angular.io/guide/forms)
- [Bootstrap 5: Documentación de componentes](https://getbootstrap.com/docs/5.3/components/)
- [Angular DevTools: Guía de uso](https://angular.io/guide/devtools)

---
