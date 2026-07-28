---LAB_START---
LAB_ID: 06-00-01
---MARKDOWN---
# Decoradores @Input

## Metadatos

| Campo         | Detalle                          |
|---------------|----------------------------------|
| **Duración**  | 12 minutos                       |
| **Complejidad** | Fácil                          |
| **Nivel Bloom** | Aplicar (Apply)                |
| **Módulo**    | 6 – Comunicación entre Componentes |
| **Versión Angular** | 17.x (modo NgModule)       |

---

## Descripción General

En esta práctica construirás un sistema de **tarjeta de producto** compuesto por dos componentes Angular: un componente padre `lista-productos` que gestiona un arreglo de productos, y un componente hijo `tarjeta-producto` que recibe y muestra los datos de cada producto mediante el decorador `@Input`. Explorarás el uso de tipos primitivos, objetos tipados, alias de `@Input` y valores por defecto, consolidando así el patrón de comunicación unidireccional **padre → hijo** que es fundamental en la arquitectura de componentes de Angular.

---

## Objetivos de Aprendizaje

Al finalizar esta práctica serás capaz de:

- [ ] Implementar el decorador `@Input` en un componente hijo para recibir datos primitivos (`string`, `number`, `boolean`) y objetos tipados desde el componente padre.
- [ ] Utilizar la sintaxis de **alias** en `@Input('descuento')` para desacoplar el nombre externo del binding del nombre interno de la propiedad.
- [ ] Aplicar **property binding** con corchetes `[]` en el template del padre para pasar valores al hijo, distinguiendo claramente la diferencia respecto al binding de atributo sin corchetes.
- [ ] Implementar `ngOnChanges` en el componente hijo para detectar y registrar cambios en las propiedades `@Input`.
- [ ] Identificar y corregir errores comunes al usar `@Input`: omitir la importación, olvidar los corchetes y pasar tipos incorrectos.

---

## Prerrequisitos

### Conocimiento previo

| Tema | Nivel requerido |
|------|----------------|
| Estructura de un componente Angular (`@Component`, `selector`, `template`) | Sólido |
| Ciclo de vida Angular: `ngOnInit`, `ngOnChanges` | Básico |
| TypeScript: decoradores, interfaces, tipos primitivos | Básico |
| Property binding básico en Angular | Básico |
| Directiva `*ngFor` para iterar listas | Básico |

### Laboratorios previos completados

- **Lab 04-00-01** – Componentes Angular y su estructura.
- **Lab 05-00-01** – Ciclo de vida: `ngOnChanges`.

### Acceso requerido

- Proyecto Angular creado en un laboratorio anterior **o** capacidad de crear uno nuevo (se indica en el Paso 1).
- Terminal con Angular CLI disponible (`ng version` responde correctamente).
- Visual Studio Code abierto y funcionando.

---

## Entorno de Laboratorio

### Hardware mínimo recomendado

| Recurso | Mínimo | Recomendado |
|---------|--------|-------------|
| RAM | 8 GB | 16 GB |
| Almacenamiento libre | 10 GB | 15 GB |
| Procesador | Intel Core i5 / 1.6 GHz | Intel Core i7 / 2.0 GHz |
| Resolución de pantalla | 1280 × 768 | 1920 × 1080 |

### Software requerido

| Software | Versión mínima | Versión recomendada |
|----------|---------------|---------------------|
| Node.js | 18.x LTS | 20.x LTS |
| Angular CLI | 16.x | 17.x |
| TypeScript | 4.9.x | 5.x |
| Visual Studio Code | 1.85.x | Última estable |
| Google Chrome | 120.x | Última estable |
| Angular DevTools (extensión Chrome) | Última disponible | Última disponible |

### Verificación del entorno

Antes de comenzar, abre una terminal y ejecuta los siguientes comandos para confirmar que el entorno está listo:

```bash
node --version
# Resultado esperado: v20.x.x (o v18.x.x mínimo)

npm --version
# Resultado esperado: 10.x.x

ng version
# Resultado esperado: Angular CLI: 17.x.x
```

Si alguno de estos comandos falla, revisa la guía de instalación del curso antes de continuar.

---

## Pasos del Laboratorio

---

### Paso 1 – Crear el proyecto Angular con soporte NgModule

**Objetivo:** Generar un proyecto Angular 17 en modo tradicional (NgModule) que servirá como base para todos los componentes de esta práctica.

#### Instrucciones

1. Abre una terminal en la carpeta donde deseas crear el proyecto.

2. Ejecuta el siguiente comando para crear el proyecto **sin** el modo standalone (modo NgModule tradicional, recomendado para este curso):

   ```bash
   ng new lab-input-decorators --no-standalone --routing=false --style=css
   ```

   > **Nota:** La bandera `--no-standalone` es clave en Angular 17 para usar NgModule. Si omites esta bandera, el proyecto se creará en modo standalone por defecto.

3. Cuando Angular CLI pregunte sobre el stylesheet format, confirma **CSS**.

4. Ingresa al directorio del proyecto:

   ```bash
   cd lab-input-decorators
   ```

5. Abre el proyecto en Visual Studio Code:

   ```bash
   code .
   ```

6. Inicia el servidor de desarrollo en una terminal integrada de VS Code:

   ```bash
   ng serve --open
   ```

#### Resultado esperado

El navegador abre automáticamente `http://localhost:4200` y muestra la página de bienvenida de Angular con el logo y los enlaces de recursos.

#### Verificación

En la terminal debe aparecer:

```
✔ Compiled successfully.
```

---

### Paso 2 – Crear la interfaz `Producto`

**Objetivo:** Definir un tipo TypeScript que describa la estructura de los datos que fluirán del padre al hijo, garantizando tipado estático en toda la aplicación.

#### Instrucciones

1. En la terminal integrada (abre una segunda pestaña para no detener `ng serve`), genera la interfaz con Angular CLI:

   ```bash
   ng generate interface models/producto
   ```

   Esto crea el archivo `src/app/models/producto.ts`.

2. Abre `src/app/models/producto.ts` y reemplaza su contenido con el siguiente código:

   ```typescript
   // src/app/models/producto.ts

   export interface Producto {
     id: number;
     nombre: string;
     precio: number;
     disponible: boolean;
     imagen: string;
     descuento: number; // porcentaje de descuento (0–100)
   }
   ```

3. Guarda el archivo (`Ctrl + S` / `Cmd + S`).

#### Resultado esperado

El archivo `src/app/models/producto.ts` existe y TypeScript no reporta errores en el panel de **Problemas** de VS Code.

#### Verificación

En la terminal, el servidor de desarrollo recompila sin errores:

```
✔ Compiled successfully.
```

---

### Paso 3 – Crear el componente hijo `tarjeta-producto`

**Objetivo:** Generar el componente hijo que recibirá datos del padre mediante `@Input` y los mostrará en pantalla.

#### Instrucciones

1. En la terminal (segunda pestaña), ejecuta:

   ```bash
   ng generate component components/tarjeta-producto
   ```

   Angular CLI crea cuatro archivos dentro de `src/app/components/tarjeta-producto/` y actualiza `app.module.ts` automáticamente.

2. Abre `src/app/components/tarjeta-producto/tarjeta-producto.component.ts` y reemplaza todo el contenido con el siguiente código:

   ```typescript
   // src/app/components/tarjeta-producto/tarjeta-producto.component.ts

   import {
     Component,
     Input,
     OnChanges,
     SimpleChanges
   } from '@angular/core';

   @Component({
     selector: 'app-tarjeta-producto',
     templateUrl: './tarjeta-producto.component.html',
     styleUrls: ['./tarjeta-producto.component.css']
   })
   export class TarjetaProductoComponent implements OnChanges {

     // Propiedad @Input con valor por defecto (string)
     @Input() nombre: string = 'Producto sin nombre';

     // Propiedad @Input con valor por defecto (number)
     @Input() precio: number = 0;

     // Propiedad @Input con valor por defecto (boolean)
     @Input() disponible: boolean = true;

     // Propiedad @Input con valor por defecto (string – URL de imagen)
     @Input() imagen: string = 'https://via.placeholder.com/150';

     // Propiedad @Input con ALIAS: el padre usará [descuento],
     // pero internamente la propiedad se llama porcentajeDescuento
     @Input('descuento') porcentajeDescuento: number = 0;

     // ngOnChanges se ejecuta cada vez que cambia un @Input
     ngOnChanges(changes: SimpleChanges): void {
       // Solo registramos el cambio si la propiedad 'precio' cambió
       if (changes['precio']) {
         const anterior = changes['precio'].previousValue;
         const actual   = changes['precio'].currentValue;
         console.log(`[TarjetaProducto] Precio cambió: ${anterior} → ${actual}`);
       }
     }

     // Calcula el precio final aplicando el descuento
     get precioFinal(): number {
       return this.precio * (1 - this.porcentajeDescuento / 100);
     }
   }
   ```

   > **Puntos clave del código:**
   > - `@Input('descuento') porcentajeDescuento` demuestra el uso de **alias**: el binding externo es `[descuento]` pero la variable interna es `porcentajeDescuento`.
   > - `ngOnChanges` implementa la interfaz `OnChanges` y recibe un objeto `SimpleChanges` con los cambios de cada propiedad `@Input`.
   > - El getter `precioFinal` calcula el precio con descuento sin necesidad de un método adicional.

3. Guarda el archivo.

#### Resultado esperado

El servidor de desarrollo recompila sin errores. En `app.module.ts` aparece `TarjetaProductoComponent` en el arreglo `declarations`.

#### Verificación

Abre `src/app/app.module.ts` y confirma que contiene:

```typescript
declarations: [
  AppComponent,
  TarjetaProductoComponent  // ← debe estar aquí
],
```

---

### Paso 4 – Diseñar el template del componente hijo

**Objetivo:** Crear la plantilla HTML del componente hijo que muestre los datos recibidos mediante `@Input` con interpolación y estilos condicionales.

#### Instrucciones

1. Abre `src/app/components/tarjeta-producto/tarjeta-producto.component.html` y reemplaza todo su contenido con:

   ```html
   <!-- src/app/components/tarjeta-producto/tarjeta-producto.component.html -->

   <div class="tarjeta" [class.no-disponible]="!disponible">

     <!-- Imagen del producto -->
     <img [src]="imagen" [alt]="nombre" class="tarjeta-imagen">

     <!-- Nombre del producto (interpolación directa) -->
     <h3 class="tarjeta-nombre">{{ nombre }}</h3>

     <!-- Sección de precios -->
     <div class="tarjeta-precios">
       <!-- Precio original (tachado si hay descuento) -->
       <span class="precio-original" [class.tachado]="porcentajeDescuento > 0">
         ${{ precio | number:'1.2-2' }}
       </span>

       <!-- Precio final con descuento (solo visible si hay descuento) -->
       <span *ngIf="porcentajeDescuento > 0" class="precio-descuento">
         ${{ precioFinal | number:'1.2-2' }}
       </span>

       <!-- Badge de descuento -->
       <span *ngIf="porcentajeDescuento > 0" class="badge-descuento">
         -{{ porcentajeDescuento }}%
       </span>
     </div>

     <!-- Estado de disponibilidad -->
     <p class="disponibilidad" [class.disponible]="disponible" [class.agotado]="!disponible">
       {{ disponible ? '✅ Disponible' : '❌ Agotado' }}
     </p>

   </div>
   ```

   > **Observa:**
   > - `[class.no-disponible]="!disponible"` aplica la clase CSS condicionalmente usando **class binding**.
   > - `{{ precio | number:'1.2-2' }}` usa el pipe `number` para formatear el precio con dos decimales.
   > - `*ngIf="porcentajeDescuento > 0"` muestra elementos solo cuando hay descuento.

2. Abre `src/app/components/tarjeta-producto/tarjeta-producto.component.css` y agrega los estilos:

   ```css
   /* src/app/components/tarjeta-producto/tarjeta-producto.component.css */

   .tarjeta {
     border: 1px solid #ddd;
     border-radius: 8px;
     padding: 16px;
     width: 200px;
     text-align: center;
     background-color: #fff;
     box-shadow: 0 2px 6px rgba(0,0,0,0.1);
     transition: opacity 0.3s;
   }

   .tarjeta.no-disponible {
     opacity: 0.5;
     background-color: #f5f5f5;
   }

   .tarjeta-imagen {
     width: 100%;
     height: 150px;
     object-fit: cover;
     border-radius: 4px;
   }

   .tarjeta-nombre {
     font-size: 1rem;
     margin: 8px 0;
     color: #333;
   }

   .tarjeta-precios {
     display: flex;
     flex-direction: column;
     align-items: center;
     gap: 4px;
   }

   .precio-original {
     font-size: 1.1rem;
     font-weight: bold;
     color: #222;
   }

   .precio-original.tachado {
     text-decoration: line-through;
     color: #999;
     font-weight: normal;
   }

   .precio-descuento {
     font-size: 1.2rem;
     font-weight: bold;
     color: #e63946;
   }

   .badge-descuento {
     background-color: #e63946;
     color: white;
     padding: 2px 8px;
     border-radius: 12px;
     font-size: 0.75rem;
   }

   .disponibilidad {
     margin-top: 8px;
     font-size: 0.85rem;
   }

   .disponible {
     color: #2a9d8f;
   }

   .agotado {
     color: #e63946;
   }
   ```

3. Guarda ambos archivos.

#### Resultado esperado

El servidor recompila sin errores. El template está listo para recibir datos del componente padre.

#### Verificación

No hay errores en el panel de **Problemas** de VS Code para estos archivos.

---

### Paso 5 – Crear el componente padre `lista-productos`

**Objetivo:** Generar el componente padre que contendrá el arreglo de productos y renderizará múltiples instancias del componente hijo mediante `*ngFor` y property binding.

#### Instrucciones

1. En la terminal, genera el componente padre:

   ```bash
   ng generate component components/lista-productos
   ```

2. Abre `src/app/components/lista-productos/lista-productos.component.ts` y reemplaza su contenido:

   ```typescript
   // src/app/components/lista-productos/lista-productos.component.ts

   import { Component } from '@angular/core';
   import { Producto } from '../../models/producto';

   @Component({
     selector: 'app-lista-productos',
     templateUrl: './lista-productos.component.html',
     styleUrls: ['./lista-productos.component.css']
   })
   export class ListaProductosComponent {

     // Arreglo de productos que el padre pasará al hijo mediante @Input
     productos: Producto[] = [
       {
         id: 1,
         nombre: 'Laptop Pro 15',
         precio: 1299.99,
         disponible: true,
         imagen: 'https://via.placeholder.com/150/0077cc/ffffff?text=Laptop',
         descuento: 10
       },
       {
         id: 2,
         nombre: 'Mouse Inalámbrico',
         precio: 45.00,
         disponible: true,
         imagen: 'https://via.placeholder.com/150/00cc77/ffffff?text=Mouse',
         descuento: 0
       },
       {
         id: 3,
         nombre: 'Teclado Mecánico',
         precio: 89.99,
         disponible: false,
         imagen: 'https://via.placeholder.com/150/cc7700/ffffff?text=Teclado',
         descuento: 20
       },
       {
         id: 4,
         nombre: 'Monitor 4K',
         precio: 499.00,
         disponible: true,
         imagen: 'https://via.placeholder.com/150/cc0077/ffffff?text=Monitor',
         descuento: 5
       }
     ];

     // Método para simular un cambio de precio (demuestra ngOnChanges en el hijo)
     aumentarPrecio(producto: Producto): void {
       producto.precio = +(producto.precio * 1.10).toFixed(2);
     }

     // Método para alternar disponibilidad
     toggleDisponibilidad(producto: Producto): void {
       producto.disponible = !producto.disponible;
     }
   }
   ```

3. Guarda el archivo.

#### Resultado esperado

El archivo se compila sin errores y el componente queda registrado en `app.module.ts`.

#### Verificación

Confirma en `app.module.ts` que `declarations` ahora incluye:

```typescript
declarations: [
  AppComponent,
  TarjetaProductoComponent,
  ListaProductosComponent  // ← nuevo
],
```

---

### Paso 6 – Diseñar el template del componente padre

**Objetivo:** Escribir el template del padre que itera el arreglo de productos con `*ngFor` y pasa cada campo al hijo mediante **property binding** `[]`.

#### Instrucciones

1. Abre `src/app/components/lista-productos/lista-productos.component.html` y reemplaza su contenido:

   ```html
   <!-- src/app/components/lista-productos/lista-productos.component.html -->

   <div class="lista-container">
     <h2>🛒 Catálogo de Productos</h2>
     <p class="subtitulo">
       Cada tarjeta es un componente hijo que recibe datos mediante <code>@Input</code>
     </p>

     <!-- *ngFor itera el arreglo y crea una instancia de app-tarjeta-producto por cada elemento -->
     <div class="lista-grid">
       <div *ngFor="let producto of productos" class="tarjeta-wrapper">

         <!--
           PROPERTY BINDING con corchetes []:
           - [nombre]       → pasa producto.nombre   al @Input() nombre
           - [precio]       → pasa producto.precio   al @Input() precio
           - [disponible]   → pasa producto.disponible al @Input() disponible
           - [imagen]       → pasa producto.imagen   al @Input() imagen
           - [descuento]    → pasa producto.descuento al @Input('descuento') porcentajeDescuento
                              ↑ ALIAS: el padre usa 'descuento', el hijo lo llama 'porcentajeDescuento'
         -->
         <app-tarjeta-producto
           [nombre]="producto.nombre"
           [precio]="producto.precio"
           [disponible]="producto.disponible"
           [imagen]="producto.imagen"
           [descuento]="producto.descuento">
         </app-tarjeta-producto>

         <!-- Botones de control para demostrar reactividad -->
         <div class="controles">
           <button (click)="aumentarPrecio(producto)" class="btn-precio">
             💰 +10% precio
           </button>
           <button (click)="toggleDisponibilidad(producto)" class="btn-disponible">
             🔄 Toggle disponible
           </button>
         </div>

       </div>
     </div>
   </div>
   ```

   > **Puntos críticos para observar:**
   > - `[nombre]="producto.nombre"` → **property binding** (con corchetes): evalúa la expresión y pasa el *valor*.
   > - `nombre="producto.nombre"` sin corchetes → **binding de atributo**: pasaría la *cadena literal* `"producto.nombre"`, no el valor. Este es uno de los errores más comunes.
   > - `[descuento]="producto.descuento"` → el padre usa el alias `descuento`; el hijo lo recibe en `porcentajeDescuento`.

2. Abre `src/app/components/lista-productos/lista-productos.component.css` y agrega:

   ```css
   /* src/app/components/lista-productos/lista-productos.component.css */

   .lista-container {
     padding: 24px;
     font-family: Arial, sans-serif;
   }

   h2 {
     color: #333;
     margin-bottom: 4px;
   }

   .subtitulo {
     color: #666;
     font-size: 0.9rem;
     margin-bottom: 24px;
   }

   .lista-grid {
     display: flex;
     flex-wrap: wrap;
     gap: 24px;
   }

   .tarjeta-wrapper {
     display: flex;
     flex-direction: column;
     align-items: center;
     gap: 8px;
   }

   .controles {
     display: flex;
     gap: 8px;
   }

   .btn-precio,
   .btn-disponible {
     padding: 6px 10px;
     border: none;
     border-radius: 4px;
     cursor: pointer;
     font-size: 0.75rem;
   }

   .btn-precio {
     background-color: #0077cc;
     color: white;
   }

   .btn-disponible {
     background-color: #555;
     color: white;
   }

   .btn-precio:hover { background-color: #005fa3; }
   .btn-disponible:hover { background-color: #333; }
   ```

3. Guarda ambos archivos.

#### Resultado esperado

El servidor recompila sin errores.

#### Verificación

No hay líneas rojas en el panel de **Problemas** de VS Code.

---

### Paso 7 – Integrar el componente padre en `AppComponent`

**Objetivo:** Reemplazar el template por defecto de `AppComponent` para mostrar el componente `lista-productos` en la aplicación.

#### Instrucciones

1. Abre `src/app/app.component.html` y reemplaza **todo** su contenido con:

   ```html
   <!-- src/app/app.component.html -->

   <div style="min-height: 100vh; background-color: #f0f2f5;">
     <header style="background-color: #0077cc; color: white; padding: 16px 24px;">
       <h1 style="margin: 0; font-size: 1.4rem;">
         Angular @Input – Lab 06-00-01
       </h1>
     </header>

     <!-- Componente padre que gestiona la lista de productos -->
     <app-lista-productos></app-lista-productos>
   </div>
   ```

2. Abre `src/app/app.component.ts` y simplifica la clase:

   ```typescript
   // src/app/app.component.ts

   import { Component } from '@angular/core';

   @Component({
     selector: 'app-root',
     templateUrl: './app.component.html',
     styleUrls: ['./app.component.css']
   })
   export class AppComponent {
     title = 'lab-input-decorators';
   }
   ```

3. Guarda ambos archivos.

#### Resultado esperado

El navegador en `http://localhost:4200` muestra la cabecera azul y debajo el catálogo con cuatro tarjetas de producto, cada una con imagen, nombre, precio, badge de descuento (cuando aplica) y estado de disponibilidad.

#### Verificación

- Verifica visualmente que se muestran **4 tarjetas**.
- La tarjeta "Teclado Mecánico" aparece con **opacidad reducida** (no disponible).
- Las tarjetas con descuento muestran el precio original tachado y el precio final en rojo.

---

### Paso 8 – Verificar `ngOnChanges` y la reactividad de `@Input`

**Objetivo:** Confirmar que `ngOnChanges` detecta cambios en las propiedades `@Input` y que los datos en el hijo se actualizan automáticamente cuando el padre modifica sus valores.

#### Instrucciones

1. Abre las **Herramientas de Desarrollador** de Chrome (`F12` o `Ctrl+Shift+I` / `Cmd+Option+I`).

2. Ve a la pestaña **Console**.

3. En el navegador, haz clic en el botón **"💰 +10% precio"** de la tarjeta **"Laptop Pro 15"**.

4. Observa en la consola el mensaje registrado por `ngOnChanges`:

   ```
   [TarjetaProducto] Precio cambió: 1299.99 → 1429.99
   ```

5. Haz clic nuevamente:

   ```
   [TarjetaProducto] Precio cambió: 1429.99 → 1572.99
   ```

6. Haz clic en **"🔄 Toggle disponible"** de la misma tarjeta y observa que la tarjeta cambia visualmente (opacidad) sin recargar la página.

7. Ahora usa la extensión **Angular DevTools**: abre el panel `Components` y selecciona `app-tarjeta-producto`. Observa las propiedades `@Input` en el panel derecho y cómo sus valores coinciden con los datos del arreglo del padre.

#### Resultado esperado

- Cada clic en "💰 +10% precio" genera un mensaje en consola con el valor anterior y el nuevo valor.
- El precio mostrado en la tarjeta se actualiza en tiempo real sin recargar la página.
- El toggle de disponibilidad cambia la opacidad de la tarjeta instantáneamente.

#### Verificación

Confirma que en la consola **no** aparecen errores en rojo, solo los mensajes `[TarjetaProducto] Precio cambió:`.

---

### Paso 9 – Explorar errores comunes de `@Input`

**Objetivo:** Experimentar intencionalmente con los tres errores más frecuentes al usar `@Input` para comprender sus síntomas y soluciones.

#### Instrucciones

> ⚠️ **Importante:** Realiza cada experimento, observa el resultado y **revierte el cambio** antes de pasar al siguiente. Usa `Ctrl+Z` para deshacer.

**Experimento A – Olvidar los corchetes en el property binding**

1. En `lista-productos.component.html`, cambia temporalmente:

   ```html
   <!-- ANTES (correcto) -->
   [nombre]="producto.nombre"

   <!-- DESPUÉS (incorrecto, sin corchetes) -->
   nombre="producto.nombre"
   ```

2. Guarda y observa en el navegador: todas las tarjetas mostrarán el texto literal `producto.nombre` en lugar del valor real.

3. **Revierte el cambio** (`Ctrl+Z` y guarda).

**Experimento B – Pasar un tipo incorrecto**

1. En `lista-productos.component.html`, cambia temporalmente:

   ```html
   <!-- ANTES (correcto) -->
   [precio]="producto.precio"

   <!-- DESPUÉS (incorrecto, pasa string en lugar de number) -->
   precio="1299.99"
   ```

   > Aquí `precio="1299.99"` sin corchetes pasa la cadena `"1299.99"`, no el número. TypeScript puede advertir esto en modo estricto.

2. Observa que el precio se muestra, pero si Angular DevTools inspecciona el componente, el tipo será `string` en lugar de `number`. El cálculo de `precioFinal` puede comportarse inesperadamente.

3. **Revierte el cambio**.

**Experimento C – Usar el nombre interno en lugar del alias**

1. En `lista-productos.component.html`, cambia temporalmente:

   ```html
   <!-- ANTES (correcto, usa el alias externo) -->
   [descuento]="producto.descuento"

   <!-- DESPUÉS (incorrecto, usa el nombre interno de la propiedad) -->
   [porcentajeDescuento]="producto.descuento"
   ```

2. Guarda y observa: el badge de descuento desaparece y el precio original ya no aparece tachado. Angular no reconoce `porcentajeDescuento` como un binding válido porque el decorador definió `@Input('descuento')`.

3. En la consola puede aparecer:

   ```
   Can't bind to 'porcentajeDescuento' since it isn't a known property of 'app-tarjeta-producto'.
   ```

4. **Revierte el cambio**.

#### Resultado esperado

Tras revertir todos los cambios, la aplicación funciona correctamente y se muestran las 4 tarjetas con datos reales.

#### Verificación

La consola no muestra errores en rojo y las 4 tarjetas muestran sus datos correctos.

---

## Validación y Pruebas

Ejecuta la siguiente lista de verificación para confirmar que la práctica está completa y correcta:

| # | Criterio de validación | ✅ / ❌ |
|---|------------------------|---------|
| 1 | El proyecto compila sin errores (`ng serve` sin mensajes de error) | |
| 2 | Se muestran exactamente **4 tarjetas** de producto en el navegador | |
| 3 | La tarjeta "Teclado Mecánico" aparece con opacidad reducida (no disponible) | |
| 4 | Las tarjetas con descuento > 0 muestran el precio original tachado y el precio final | |
| 5 | El botón "+10% precio" actualiza el precio en la tarjeta en tiempo real | |
| 6 | La consola muestra el mensaje de `ngOnChanges` al hacer clic en "+10% precio" | |
| 7 | El botón "Toggle disponible" cambia la opacidad de la tarjeta | |
| 8 | Angular DevTools muestra las 5 propiedades `@Input` en el componente hijo | |
| 9 | El alias `@Input('descuento')` funciona correctamente (el padre usa `[descuento]`) | |
| 10 | No hay errores en la consola del navegador durante el uso normal | |

### Prueba adicional con Angular DevTools

1. Abre Angular DevTools → pestaña **Components**.
2. Selecciona cualquier instancia de `app-tarjeta-producto` en el árbol de componentes.
3. En el panel de propiedades (derecha), confirma que aparecen:
   - `nombre` → string
   - `precio` → number
   - `disponible` → boolean
   - `imagen` → string
   - `porcentajeDescuento` → number

---

## Solución de Problemas

### Problema 1 – Error: "Can't bind to 'X' since it isn't a known property"

**Síntoma:**

La consola del navegador o la terminal muestran:

```
ERROR: Can't bind to 'nombre' since it isn't a known property of 'app-tarjeta-producto'.
```

**Causa:**

Este error ocurre por una de estas razones:
- El decorador `@Input` no fue importado desde `@angular/core` en el componente hijo.
- El componente `TarjetaProductoComponent` no está declarado en `AppModule` (en `declarations`).
- Hay un error tipográfico en el nombre del selector o del binding.

**Solución:**

1. Verifica que la importación de `@Input` esté presente en `tarjeta-producto.component.ts`:

   ```typescript
   // ✅ Correcto
   import { Component, Input, OnChanges, SimpleChanges } from '@angular/core';
   ```

2. Verifica que `TarjetaProductoComponent` esté en `declarations` de `app.module.ts`:

   ```typescript
   declarations: [
     AppComponent,
     TarjetaProductoComponent,  // ← debe estar aquí
     ListaProductosComponent
   ],
   ```

3. Si el problema persiste, detén el servidor (`Ctrl+C`) y reinícialo:

   ```bash
   ng serve
   ```

---

### Problema 2 – `ngOnChanges` no se dispara al hacer clic en el botón de precio

**Síntoma:**

Al hacer clic en "💰 +10% precio", el precio en pantalla **no se actualiza** y la consola **no muestra** el mensaje `[TarjetaProducto] Precio cambió:`.

**Causa:**

Este problema ocurre cuando el método `aumentarPrecio` en el padre **muta el objeto** en lugar de crear una nueva referencia. Angular detecta cambios en `@Input` de tipos primitivos por valor, pero para objetos detecta cambios por referencia. Sin embargo, en este laboratorio `precio` es un `number` (tipo primitivo), por lo que el problema más probable es que el método esté modificando una copia local o que la clase no implemente correctamente `OnChanges`.

**Solución:**

1. Verifica que `TarjetaProductoComponent` implemente `OnChanges` correctamente:

   ```typescript
   // ✅ Correcto
   export class TarjetaProductoComponent implements OnChanges {
     ngOnChanges(changes: SimpleChanges): void {
       if (changes['precio']) {
         console.log(`[TarjetaProducto] Precio cambió:`,
           changes['precio'].previousValue, '→',
           changes['precio'].currentValue);
       }
     }
   }
   ```

2. Verifica que `aumentarPrecio` en el padre modifique directamente la propiedad `precio` del objeto:

   ```typescript
   // ✅ Correcto – modifica la propiedad primitiva directamente
   aumentarPrecio(producto: Producto): void {
     producto.precio = +(producto.precio * 1.10).toFixed(2);
   }
   ```

3. Confirma que en el template del padre el binding sea `[precio]="producto.precio"` (con corchetes y apuntando a la propiedad `precio`, no al objeto completo).

---

## Limpieza del Entorno

Al finalizar la práctica, puedes realizar los siguientes pasos opcionales para liberar recursos:

1. **Detener el servidor de desarrollo:**

   En la terminal donde corre `ng serve`, presiona `Ctrl + C` y confirma con `Y` si es necesario.

2. **Conservar el proyecto** para referencia futura (recomendado):

   El proyecto `lab-input-decorators` servirá como base para la práctica del decorador `@Output` (Lab 06-00-02).

3. **Si deseas eliminar el proyecto** (solo si no lo necesitarás):

   ```bash
   # Windows (PowerShell)
   Remove-Item -Recurse -Force lab-input-decorators

   # macOS / Linux
   rm -rf lab-input-decorators
   ```

4. **Cerrar Angular DevTools** en Chrome si no la necesitas activa.

---

## Resumen

En esta práctica implementaste el decorador `@Input` para establecer comunicación unidireccional **padre → hijo** en Angular. Los conceptos clave que aplicaste son:

| Concepto | Lo que aprendiste |
|----------|-------------------|
| `@Input()` básico | Declarar propiedades que reciben datos del padre con tipos primitivos y valores por defecto |
| Alias `@Input('nombre-externo')` | Desacoplar el nombre del binding externo del nombre interno de la propiedad |
| Property binding `[prop]="valor"` | Pasar valores dinámicos del padre al hijo usando corchetes |
| `ngOnChanges` + `SimpleChanges` | Detectar y responder a cambios en propiedades `@Input` |
| Errores comunes | Identificar y corregir: falta de corchetes, alias incorrecto, `@Input` sin importar |

### Flujo de datos implementado

```
ListaProductosComponent (padre)
        │
        │  [nombre]="producto.nombre"
        │  [precio]="producto.precio"
        │  [disponible]="producto.disponible"
        │  [imagen]="producto.imagen"
        │  [descuento]="producto.descuento"   ← alias externo
        ▼
TarjetaProductoComponent (hijo)
   @Input() nombre
   @Input() precio              → ngOnChanges detecta cambios
   @Input() disponible
   @Input() imagen
   @Input('descuento') porcentajeDescuento   ← nombre interno
```

### Recursos adicionales

- [Documentación oficial Angular – Component Inputs](https://angular.dev/guide/components/inputs)
- [Guía de TypeScript sobre decoradores](https://www.typescriptlang.org/docs/handbook/decorators.html)
- [Angular DevTools – Chrome Web Store](https://chrome.google.com/webstore/detail/angular-devtools/ienfalfjdbdpebioblfackkekamfmbnh)
- [SimpleChanges API Reference](https://angular.dev/api/core/SimpleChanges)

> **Próximo laboratorio:** Lab 06-00-02 – Decoradores `@Output` y `EventEmitter`: aprenderás a completar el ciclo de comunicación implementando el flujo **hijo → padre** mediante eventos personalizados.

---
LAB_END---

---

# Comunicando un componente Hijo con su componente Padre utilizando @Output

## 1. Metadatos

| Campo | Detalle |
|---|---|
| **Duración estimada** | 13 minutos |
| **Complejidad** | Media |
| **Nivel Bloom** | Crear |
| **Módulo** | 6 — Comunicación entre Componentes |
| **Práctica anterior requerida** | Lab 06-00-01 (decorador `@Input`) |

---

## 2. Descripción General

Esta práctica completa el ciclo de comunicación entre componentes Angular iniciado en el laboratorio anterior. Extenderás el proyecto de tarjetas de producto para que el componente hijo `tarjeta-producto` pueda **emitir eventos tipados** hacia su componente padre mediante el decorador `@Output` y la clase `EventEmitter<T>`. Al finalizar, tendrás un flujo completo y bidireccional: el padre envía datos al hijo mediante `@Input`, y el hijo notifica acciones del usuario al padre mediante `@Output`.

El resultado final será una tienda de productos interactiva donde el usuario puede seleccionar un producto, agregarlo al carrito (con cantidad) y eliminarlo, observando en tiempo real cómo el componente padre actualiza su estado en respuesta a cada evento.

---

## 3. Objetivos de Aprendizaje

Al completar esta práctica, serás capaz de:

- [ ] Implementar el decorador `@Output` con `EventEmitter<T>` en un componente hijo para emitir eventos personalizados tipados hacia el padre.
- [ ] Suscribirte a eventos del hijo desde el padre usando event binding con la sintaxis de paréntesis `(nombreEvento)="manejador($event)"`.
- [ ] Emitir objetos complejos junto con los eventos y acceder a sus propiedades en el padre mediante `$event`.
- [ ] Combinar `@Input` y `@Output` en un mismo componente para lograr comunicación bidireccional entre componentes padre e hijo.
- [ ] Construir un flujo completo de interacción usuario → hijo → padre → actualización de estado visible en el template.

---

## 4. Prerrequisitos

### Conocimientos previos
- Laboratorio 06-00-01 completado: dominio del decorador `@Input` y property binding.
- Comprensión del event binding en Angular (sintaxis `(evento)="método()"`).
- Conocimiento de TypeScript: interfaces, generics básicos (`EventEmitter<T>`), tipos de unión.
- Familiaridad con eventos del DOM en JavaScript/TypeScript.

### Acceso y recursos
- Proyecto Angular generado en el Lab 06-00-01 con el componente `tarjeta-producto` funcional.
- Visual Studio Code con la extensión **Angular Language Service** instalada.
- Google Chrome con la extensión **Angular DevTools** instalada.
- Terminal (PowerShell en Windows / Bash o Zsh en macOS/Linux).

---

## 5. Entorno de Laboratorio

### Hardware recomendado

| Recurso | Mínimo | Recomendado |
|---|---|---|
| RAM | 8 GB | 16 GB |
| Almacenamiento libre | 10 GB | 15 GB |
| Procesador | Intel Core i5 / 1.6 GHz 64-bit | Intel Core i7 / 2.0 GHz |
| Resolución de pantalla | 1280 × 768 | 1920 × 1080 |
| Conexión a Internet | 10 Mbps | 20 Mbps |

### Software requerido

| Herramienta | Versión mínima | Versión recomendada |
|---|---|---|
| Node.js LTS | 18.x | 20.x LTS |
| NPM | 9.x | 10.x |
| Angular CLI | 16.x | 17.x |
| TypeScript | 4.9.x | 5.x |
| Visual Studio Code | 1.85.x | Última estable |
| Google Chrome | 120.x | Última estable |

### Verificación del entorno

Abre una terminal y confirma que tu entorno está listo antes de comenzar:

```bash
node --version        # Debe mostrar v18.x o v20.x
npm --version         # Debe mostrar 9.x o 10.x
ng version            # Debe mostrar Angular CLI 16.x o 17.x
```

### Posicionarse en el proyecto existente

```bash
# Navega al directorio del proyecto creado en el Lab 06-00-01
cd tienda-componentes

# Verifica que el servidor de desarrollo puede iniciarse
ng serve --open
```

> **Nota para instructores:** Si algún estudiante no completó el Lab 06-00-01, puede clonar el estado inicial desde el repositorio del curso o solicitar el archivo ZIP al instructor antes de continuar.

---

## 6. Desarrollo Paso a Paso

### Paso 1 — Revisar el estado actual del proyecto y la interfaz `Producto`

**Objetivo:** Confirmar que el proyecto del Lab 06-00-01 está operativo y que la interfaz `Producto` está disponible para usarla como tipo en los nuevos `EventEmitter`.

#### Instrucciones

1. Abre el proyecto `tienda-componentes` en Visual Studio Code:

```bash
code .
```

2. Localiza y abre el archivo `src/app/models/producto.interface.ts`. Debe contener la interfaz `Producto` creada en el laboratorio anterior. Si no existe, créala ahora:

```typescript
// src/app/models/producto.interface.ts
export interface Producto {
  id: number;
  nombre: string;
  precio: number;
  descripcion: string;
  imagen: string;
  disponible: boolean;
}
```

3. Abre `src/app/app.component.ts` y verifica que ya tienes un arreglo `productos: Producto[]` con al menos tres elementos de ejemplo.

4. Abre `src/app/tarjeta-producto/tarjeta-producto.component.ts` y confirma que tiene al menos las propiedades `@Input() producto!: Producto`.

#### Salida esperada

El servidor de desarrollo (`ng serve`) muestra las tarjetas de producto renderizadas correctamente en el navegador sin errores en la consola del navegador ni en la terminal.

#### Verificación

```bash
# En la terminal donde corre ng serve, no debe haber errores de compilación.
# En Chrome DevTools (F12) > Console, no debe haber errores en rojo.
```

---

### Paso 2 — Agregar las propiedades `@Output` al componente hijo

**Objetivo:** Declarar los tres eventos de salida en `TarjetaProductoComponent` usando `@Output` y `EventEmitter<T>` con tipos específicos.

#### Instrucciones

1. Abre `src/app/tarjeta-producto/tarjeta-producto.component.ts`.

2. Agrega `Output` y `EventEmitter` a los imports de `@angular/core`:

```typescript
import { Component, Input, Output, EventEmitter, OnInit } from '@angular/core';
import { Producto } from '../models/producto.interface';
```

3. Dentro de la clase `TarjetaProductoComponent`, declara las tres propiedades `@Output` **después** de las propiedades `@Input` existentes:

```typescript
export class TarjetaProductoComponent implements OnInit {

  // ── @Input existentes del Lab 06-00-01 ──────────────────────────────────
  @Input() producto!: Producto;

  // ── @Output nuevos ───────────────────────────────────────────────────────

  /**
   * Emite el objeto Producto completo cuando el usuario hace clic en la tarjeta.
   */
  @Output() productoSeleccionado = new EventEmitter<Producto>();

  /**
   * Emite un objeto con el producto y la cantidad cuando el usuario
   * hace clic en el botón "Agregar al carrito".
   */
  @Output() agregarAlCarrito = new EventEmitter<{ producto: Producto; cantidad: number }>();

  /**
   * Emite el ID numérico del producto cuando el usuario hace clic en "Eliminar".
   */
  @Output() productoEliminado = new EventEmitter<number>();

  // Propiedad local para manejar la cantidad seleccionada en la tarjeta
  cantidad: number = 1;

  ngOnInit(): void {
    console.log(`[TarjetaProducto] Inicializado: ${this.producto?.nombre}`);
  }
}
```

#### Salida esperada

El compilador de Angular no reporta errores. En la terminal donde corre `ng serve` verás el mensaje de recompilación exitosa:

```
✔ Compiled successfully.
```

#### Verificación

Abre **Angular DevTools** en Chrome (`F12` → pestaña *Components*), selecciona una instancia de `app-tarjeta-producto` y confirma que en la sección **Outputs** aparecen los tres eventos: `productoSeleccionado`, `agregarAlCarrito` y `productoEliminado`.

---

### Paso 3 — Agregar los métodos emisores en el componente hijo

**Objetivo:** Implementar los métodos de la clase que invocan `emit()` con los datos correspondientes cuando el usuario interactúa con los botones de la tarjeta.

#### Instrucciones

1. En `tarjeta-producto.component.ts`, agrega los siguientes métodos dentro de la clase, debajo de `ngOnInit()`:

```typescript
/**
 * Llamado cuando el usuario hace clic en el contenedor de la tarjeta.
 * Emite el objeto Producto completo al componente padre.
 */
onSeleccionar(): void {
  this.productoSeleccionado.emit(this.producto);
}

/**
 * Llamado cuando el usuario hace clic en "Agregar al carrito".
 * Emite el producto junto con la cantidad seleccionada.
 * Detiene la propagación para evitar que también se dispare onSeleccionar().
 */
onAgregarAlCarrito(event: Event): void {
  event.stopPropagation();
  this.agregarAlCarrito.emit({
    producto: this.producto,
    cantidad: this.cantidad
  });
}

/**
 * Llamado cuando el usuario hace clic en "Eliminar".
 * Emite únicamente el ID del producto.
 */
onEliminar(event: Event): void {
  event.stopPropagation();
  this.productoEliminado.emit(this.producto.id);
}

/**
 * Incrementa la cantidad, con un máximo de 10.
 */
incrementarCantidad(): void {
  if (this.cantidad < 10) {
    this.cantidad++;
  }
}

/**
 * Decrementa la cantidad, con un mínimo de 1.
 */
decrementarCantidad(): void {
  if (this.cantidad > 1) {
    this.cantidad--;
  }
}
```

2. El archivo completo `tarjeta-producto.component.ts` debe quedar así:

```typescript
// src/app/tarjeta-producto/tarjeta-producto.component.ts
import { Component, Input, Output, EventEmitter, OnInit } from '@angular/core';
import { Producto } from '../models/producto.interface';

@Component({
  selector: 'app-tarjeta-producto',
  templateUrl: './tarjeta-producto.component.html',
  styleUrls: ['./tarjeta-producto.component.css']
})
export class TarjetaProductoComponent implements OnInit {

  @Input() producto!: Producto;

  @Output() productoSeleccionado = new EventEmitter<Producto>();
  @Output() agregarAlCarrito     = new EventEmitter<{ producto: Producto; cantidad: number }>();
  @Output() productoEliminado    = new EventEmitter<number>();

  cantidad: number = 1;

  ngOnInit(): void {
    console.log(`[TarjetaProducto] Inicializado: ${this.producto?.nombre}`);
  }

  onSeleccionar(): void {
    this.productoSeleccionado.emit(this.producto);
  }

  onAgregarAlCarrito(event: Event): void {
    event.stopPropagation();
    this.agregarAlCarrito.emit({ producto: this.producto, cantidad: this.cantidad });
  }

  onEliminar(event: Event): void {
    event.stopPropagation();
    this.productoEliminado.emit(this.producto.id);
  }

  incrementarCantidad(): void {
    if (this.cantidad < 10) this.cantidad++;
  }

  decrementarCantidad(): void {
    if (this.cantidad > 1) this.cantidad--;
  }
}
```

#### Salida esperada

```
✔ Compiled successfully.
```

No se producen errores de TypeScript. Los métodos son accesibles desde el template.

#### Verificación

Revisa en la terminal que no haya errores de tipo. Si TypeScript reporta `Property 'producto' has no initializer`, asegúrate de que el `@Input()` usa el operador de aserción no nula (`!`) como se muestra arriba.

---

### Paso 4 — Actualizar el template del componente hijo

**Objetivo:** Conectar los métodos emisores con los eventos del DOM en el template HTML del componente hijo, incluyendo los controles de cantidad y los botones de acción.

#### Instrucciones

1. Abre `src/app/tarjeta-producto/tarjeta-producto.component.html` y reemplaza su contenido por el siguiente template:

```html
<!-- src/app/tarjeta-producto/tarjeta-producto.component.html -->
<div class="card h-100 shadow-sm tarjeta-producto"
     (click)="onSeleccionar()"
     style="cursor: pointer;">

  <!-- Imagen del producto -->
  <img [src]="producto.imagen"
       [alt]="producto.nombre"
       class="card-img-top"
       style="height: 180px; object-fit: cover;">

  <div class="card-body d-flex flex-column">

    <!-- Nombre y precio -->
    <h5 class="card-title">{{ producto.nombre }}</h5>
    <p class="card-text text-muted small flex-grow-1">{{ producto.descripcion }}</p>
    <p class="card-text fw-bold text-success fs-5">
      $ {{ producto.precio | number:'1.2-2' }}
    </p>

    <!-- Indicador de disponibilidad -->
    <span class="badge mb-2"
          [class.bg-success]="producto.disponible"
          [class.bg-secondary]="!producto.disponible">
      {{ producto.disponible ? 'Disponible' : 'Agotado' }}
    </span>

    <!-- Control de cantidad -->
    <div class="input-group input-group-sm mb-3" (click)="$event.stopPropagation()">
      <button class="btn btn-outline-secondary"
              type="button"
              (click)="decrementarCantidad()">−</button>
      <span class="input-group-text flex-grow-1 justify-content-center">
        {{ cantidad }}
      </span>
      <button class="btn btn-outline-secondary"
              type="button"
              (click)="incrementarCantidad()">+</button>
    </div>

    <!-- Botones de acción -->
    <div class="d-flex gap-2">
      <button class="btn btn-primary btn-sm flex-grow-1"
              [disabled]="!producto.disponible"
              (click)="onAgregarAlCarrito($event)">
        🛒 Agregar
      </button>
      <button class="btn btn-outline-danger btn-sm"
              (click)="onEliminar($event)">
        🗑
      </button>
    </div>

  </div>
</div>
```

2. Agrega estilos básicos en `tarjeta-producto.component.css` para resaltar la tarjeta al pasar el cursor:

```css
/* src/app/tarjeta-producto/tarjeta-producto.component.css */
.tarjeta-producto {
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.tarjeta-producto:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15) !important;
}
```

#### Salida esperada

Las tarjetas en el navegador muestran ahora:
- La imagen, nombre, descripción y precio del producto.
- El badge de disponibilidad con color verde (disponible) o gris (agotado).
- Un control de cantidad con botones `−` y `+`.
- Un botón **Agregar** (deshabilitado si el producto está agotado) y un botón de eliminar 🗑.
- Efecto de elevación al pasar el cursor sobre la tarjeta.

#### Verificación

Abre Chrome DevTools → pestaña **Console**. Al hacer clic en una tarjeta, verifica que **no** aparezcan errores de binding. Los clics en los botones no deben propagar el evento al contenedor de la tarjeta (gracias a `stopPropagation()`).

---

### Paso 5 — Agregar los métodos manejadores en el componente padre

**Objetivo:** Implementar en `AppComponent` los tres métodos que recibirán los eventos emitidos por el componente hijo y actualizarán el estado del padre.

#### Instrucciones

1. Abre `src/app/app.component.ts`.

2. Agrega la importación de la interfaz `Producto` si no está ya importada:

```typescript
import { Component } from '@angular/core';
import { Producto } from './models/producto.interface';
```

3. Dentro de la clase `AppComponent`, agrega las propiedades de estado y los métodos manejadores:

```typescript
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {

  // ── Datos del catálogo ────────────────────────────────────────────────────
  productos: Producto[] = [
    {
      id: 1,
      nombre: 'Laptop UltraBook Pro',
      precio: 1299.99,
      descripcion: 'Procesador i7, 16 GB RAM, SSD 512 GB. Ideal para desarrollo.',
      imagen: 'https://placehold.co/300x180?text=Laptop',
      disponible: true
    },
    {
      id: 2,
      nombre: 'Monitor Curvo 27"',
      precio: 449.50,
      descripcion: 'Resolución QHD, 144 Hz, panel IPS con excelente reproducción de color.',
      imagen: 'https://placehold.co/300x180?text=Monitor',
      disponible: true
    },
    {
      id: 3,
      nombre: 'Teclado Mecánico RGB',
      precio: 89.99,
      descripcion: 'Switches Cherry MX Red, retroiluminación RGB personalizable.',
      imagen: 'https://placehold.co/300x180?text=Teclado',
      disponible: false
    },
    {
      id: 4,
      nombre: 'Mouse Inalámbrico Ergonómico',
      precio: 55.00,
      descripcion: 'Batería recargable, DPI ajustable, receptor USB-C.',
      imagen: 'https://placehold.co/300x180?text=Mouse',
      disponible: true
    }
  ];

  // ── Estado del panel lateral ──────────────────────────────────────────────
  productoSeleccionado: Producto | null = null;

  // ── Estado del carrito ────────────────────────────────────────────────────
  contadorCarrito: number = 0;
  itemsCarrito: Array<{ producto: Producto; cantidad: number }> = [];

  // ── Registro de actividad ─────────────────────────────────────────────────
  ultimaAccion: string = 'Ninguna acción aún.';

  // ── Manejadores de eventos (@Output) ─────────────────────────────────────

  /**
   * Recibe el producto completo cuando el usuario hace clic en una tarjeta.
   * Actualiza el panel lateral con la información del producto seleccionado.
   */
  onProductoSeleccionado(producto: Producto): void {
    this.productoSeleccionado = producto;
    this.ultimaAccion = `Seleccionado: "${producto.nombre}"`;
    console.log('[AppComponent] Producto seleccionado:', producto);
  }

  /**
   * Recibe el objeto { producto, cantidad } cuando el usuario agrega al carrito.
   * Actualiza el contador y la lista de items del carrito.
   */
  onAgregarAlCarrito(data: { producto: Producto; cantidad: number }): void {
    const itemExistente = this.itemsCarrito.find(
      item => item.producto.id === data.producto.id
    );

    if (itemExistente) {
      itemExistente.cantidad += data.cantidad;
    } else {
      this.itemsCarrito.push({ ...data });
    }

    this.contadorCarrito = this.itemsCarrito.reduce(
      (total, item) => total + item.cantidad, 0
    );

    this.ultimaAccion =
      `Agregado: "${data.producto.nombre}" × ${data.cantidad} unidad(es)`;
    console.log('[AppComponent] Agregar al carrito:', data);
  }

  /**
   * Recibe el ID del producto a eliminar.
   * Filtra el arreglo de productos para removerlo del catálogo.
   */
  onProductoEliminado(id: number): void {
    const productoAEliminar = this.productos.find(p => p.id === id);
    this.productos = this.productos.filter(p => p.id !== id);

    // Si el producto eliminado era el seleccionado, limpia el panel lateral
    if (this.productoSeleccionado?.id === id) {
      this.productoSeleccionado = null;
    }

    this.ultimaAccion = `Eliminado: "${productoAEliminar?.nombre}"`;
    console.log('[AppComponent] Producto eliminado con ID:', id);
  }
}
```

#### Salida esperada

```
✔ Compiled successfully.
```

TypeScript valida correctamente los tipos de los parámetros de cada manejador contra los tipos declarados en los `EventEmitter<T>` del hijo.

#### Verificación

Revisa que no haya errores de tipo en la terminal. En particular, TypeScript debe aceptar sin queja que `onAgregarAlCarrito` recibe `{ producto: Producto; cantidad: number }` porque coincide con el genérico del `EventEmitter` declarado en el hijo.

---

### Paso 6 — Actualizar el template del componente padre con event binding

**Objetivo:** Conectar los eventos del hijo con los manejadores del padre en el template `app.component.html`, y agregar el panel lateral de detalle y el contador del carrito.

#### Instrucciones

1. Abre `src/app/app.component.html` y reemplaza su contenido por el siguiente template:

```html
<!-- src/app/app.component.html -->
<div class="container-fluid py-4">

  <!-- ── Encabezado ─────────────────────────────────────────────────── -->
  <div class="row mb-4 align-items-center">
    <div class="col">
      <h1 class="h3 fw-bold mb-0">🏪 Tienda Angular — Comunicación @Input / @Output</h1>
      <p class="text-muted small mb-0">
        Práctica 6.2: Flujo completo de comunicación entre componentes
      </p>
    </div>
    <div class="col-auto">
      <!-- Contador del carrito -->
      <button class="btn btn-warning position-relative">
        🛒 Carrito
        <span class="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-danger">
          {{ contadorCarrito }}
        </span>
      </button>
    </div>
  </div>

  <!-- ── Panel de última acción ────────────────────────────────────── -->
  <div class="alert alert-info py-2 mb-4">
    <strong>Última acción registrada en el padre:</strong> {{ ultimaAccion }}
  </div>

  <div class="row">

    <!-- ── Columna principal: Catálogo de productos ───────────────── -->
    <div [class]="productoSeleccionado ? 'col-md-8' : 'col-12'">
      <h2 class="h5 mb-3">Catálogo de Productos ({{ productos.length }} disponibles)</h2>

      <div class="row row-cols-1 row-cols-sm-2 row-cols-lg-3 g-4">
        <div class="col" *ngFor="let prod of productos">

          <!--
            app-tarjeta-producto:
              [producto]       → @Input:  el padre envía datos al hijo
              (productoSeleccionado) → @Output: el hijo notifica al padre
              (agregarAlCarrito)     → @Output: el hijo notifica al padre
              (productoEliminado)    → @Output: el hijo notifica al padre
          -->
          <app-tarjeta-producto
            [producto]="prod"
            (productoSeleccionado)="onProductoSeleccionado($event)"
            (agregarAlCarrito)="onAgregarAlCarrito($event)"
            (productoEliminado)="onProductoEliminado($event)">
          </app-tarjeta-producto>

        </div>
      </div>

      <!-- Mensaje cuando no hay productos -->
      <div *ngIf="productos.length === 0"
           class="alert alert-warning mt-4 text-center">
        <strong>El catálogo está vacío.</strong>
        Recarga la página para restaurar los productos.
      </div>
    </div>

    <!-- ── Panel lateral: Producto seleccionado ───────────────────── -->
    <div class="col-md-4" *ngIf="productoSeleccionado">
      <div class="card border-primary shadow">
        <div class="card-header bg-primary text-white fw-bold">
          📋 Detalle del Producto Seleccionado
        </div>
        <img [src]="productoSeleccionado.imagen"
             [alt]="productoSeleccionado.nombre"
             class="card-img-top"
             style="height: 200px; object-fit: cover;">
        <div class="card-body">
          <h5 class="card-title">{{ productoSeleccionado.nombre }}</h5>
          <p class="card-text text-muted">{{ productoSeleccionado.descripcion }}</p>
          <ul class="list-group list-group-flush mb-3">
            <li class="list-group-item d-flex justify-content-between">
              <span>Precio:</span>
              <strong class="text-success">
                $ {{ productoSeleccionado.precio | number:'1.2-2' }}
              </strong>
            </li>
            <li class="list-group-item d-flex justify-content-between">
              <span>ID:</span>
              <strong>{{ productoSeleccionado.id }}</strong>
            </li>
            <li class="list-group-item d-flex justify-content-between">
              <span>Estado:</span>
              <span class="badge"
                    [class.bg-success]="productoSeleccionado.disponible"
                    [class.bg-secondary]="!productoSeleccionado.disponible">
                {{ productoSeleccionado.disponible ? 'Disponible' : 'Agotado' }}
              </span>
            </li>
          </ul>
          <button class="btn btn-outline-secondary btn-sm w-100"
                  (click)="productoSeleccionado = null">
            ✕ Cerrar panel
          </button>
        </div>
      </div>

      <!-- Resumen del carrito -->
      <div class="card mt-3" *ngIf="itemsCarrito.length > 0">
        <div class="card-header fw-bold">🛒 Resumen del Carrito</div>
        <ul class="list-group list-group-flush">
          <li class="list-group-item d-flex justify-content-between align-items-center"
              *ngFor="let item of itemsCarrito">
            <span class="small">{{ item.producto.nombre }}</span>
            <span class="badge bg-primary rounded-pill">× {{ item.cantidad }}</span>
          </li>
        </ul>
        <div class="card-footer text-muted small text-end">
          Total de unidades: <strong>{{ contadorCarrito }}</strong>
        </div>
      </div>

    </div>
    <!-- fin panel lateral -->

  </div>
</div>
```

#### Salida esperada

El navegador muestra:
- El encabezado con el botón de carrito y su contador (inicialmente en `0`).
- El panel de "Última acción" con el texto inicial.
- Las tarjetas de producto en un grid responsivo.
- Al hacer clic en una tarjeta, aparece el panel lateral con el detalle del producto.
- Al hacer clic en **Agregar**, el contador del carrito se incrementa.
- Al hacer clic en 🗑, la tarjeta desaparece del catálogo.

#### Verificación

Abre la consola de Chrome y verifica los mensajes `console.log` de cada manejador:

```
[AppComponent] Producto seleccionado: {id: 1, nombre: 'Laptop UltraBook Pro', ...}
[AppComponent] Agregar al carrito: {producto: {...}, cantidad: 2}
[AppComponent] Producto eliminado con ID: 3
```

---

### Paso 7 — Verificar el flujo completo @Input/@Output con Angular DevTools

**Objetivo:** Usar Angular DevTools para inspeccionar visualmente el flujo de datos entre componentes y confirmar que los decoradores funcionan correctamente.

#### Instrucciones

1. Asegúrate de que `ng serve` está corriendo y la aplicación está abierta en Chrome.

2. Abre **Angular DevTools** (`F12` → pestaña *Angular* o *Components*).

3. En el árbol de componentes, expande `AppComponent` y selecciona una instancia de `TarjetaProductoComponent`.

4. En el panel derecho, verifica la sección **Inputs**:
   - Debe mostrar `producto` con el objeto del producto asignado.

5. En la sección **Outputs** (o **Properties** según la versión de DevTools), verifica que aparecen:
   - `productoSeleccionado`
   - `agregarAlCarrito`
   - `productoEliminado`

6. Ahora selecciona `AppComponent` en el árbol y observa la sección **Properties**:
   - `productoSeleccionado`: inicialmente `null`, cambia al objeto cuando haces clic en una tarjeta.
   - `contadorCarrito`: se incrementa al agregar productos.
   - `productos`: el arreglo se reduce al eliminar un producto.

7. Haz clic en una tarjeta y observa en tiempo real cómo `productoSeleccionado` cambia en el panel de DevTools.

#### Salida esperada

Angular DevTools muestra en tiempo real los cambios de estado en `AppComponent` como respuesta a los eventos emitidos por `TarjetaProductoComponent`. Las propiedades se actualizan instantáneamente sin necesidad de recargar la página.

#### Verificación

| Acción del usuario | Cambio esperado en AppComponent |
|---|---|
| Clic en tarjeta | `productoSeleccionado` ← objeto `Producto` |
| Clic en **Agregar** (cantidad: 2) | `contadorCarrito` += 2, `itemsCarrito` crece |
| Clic en 🗑 | `productos.length` disminuye en 1 |
| Clic en **Agregar** del mismo producto | `itemsCarrito` acumula la cantidad |

---

## 7. Validación y Pruebas

Una vez completados todos los pasos, realiza las siguientes pruebas funcionales para confirmar que la implementación es correcta:

### Prueba 1 — Emisión de `productoSeleccionado`

1. Haz clic en la tarjeta "Laptop UltraBook Pro".
2. **Resultado esperado:** El panel lateral aparece a la derecha mostrando el nombre, imagen, precio y estado del producto. El texto de "Última acción" muestra: `Seleccionado: "Laptop UltraBook Pro"`.
3. Haz clic en "✕ Cerrar panel". El panel debe desaparecer y el grid debe volver a ocupar el ancho completo.

### Prueba 2 — Emisión de `agregarAlCarrito` con cantidad

1. En la tarjeta "Monitor Curvo 27"", usa los botones `+` para aumentar la cantidad a **3**.
2. Haz clic en **🛒 Agregar**.
3. **Resultado esperado:** El badge del botón "Carrito" en el encabezado muestra **3**. El resumen del carrito (visible si el panel lateral está abierto) muestra "Monitor Curvo 27" × 3".
4. Haz clic en **Agregar** nuevamente (con cantidad 1). El carrito debe mostrar **4** unidades del monitor.

### Prueba 3 — Emisión de `productoEliminado`

1. Haz clic en el botón 🗑 de la tarjeta "Teclado Mecánico RGB".
2. **Resultado esperado:** La tarjeta desaparece del grid. El texto de "Última acción" muestra: `Eliminado: "Teclado Mecánico RGB"`. El grid ahora muestra 3 tarjetas.
3. Selecciona el teclado antes de eliminarlo y verifica que el panel lateral también se cierra.

### Prueba 4 — Producto agotado

1. Verifica que la tarjeta "Teclado Mecánico RGB" (si no fue eliminada) muestra el botón **Agregar** deshabilitado (atributo `disabled`).
2. El clic sobre el botón deshabilitado **no** debe emitir ningún evento.

### Prueba 5 — `stopPropagation` funciona correctamente

1. Haz clic en el botón **Agregar** de cualquier tarjeta.
2. **Resultado esperado:** Solo se registra la acción "Agregado: ...", **no** "Seleccionado: ...". El panel lateral no aparece porque el evento de clic no se propagó al contenedor de la tarjeta.

---

## 8. Resolución de Problemas

### Problema 1 — El evento `@Output` no llega al padre (no se ejecuta el manejador)

**Síntoma:** Al hacer clic en los botones de la tarjeta, el estado del padre no cambia, no aparecen mensajes en la consola y el panel lateral no se actualiza.

**Causa probable:** El event binding en el template del padre está mal escrito. Los errores más comunes son:
- Usar corchetes `[]` en lugar de paréntesis `()` para el binding del evento.
- El nombre del evento en el template no coincide exactamente (mayúsculas/minúsculas) con el nombre declarado en el `@Output()`.
- Olvidar el prefijo `on` al invocar el manejador: `(productoSeleccionado)="productoSeleccionado($event)"` en lugar de `(productoSeleccionado)="onProductoSeleccionado($event)"`.

**Solución:**

```html
<!-- ❌ INCORRECTO: usa corchetes (property binding) -->
<app-tarjeta-producto [productoSeleccionado]="onProductoSeleccionado($event)">
</app-tarjeta-producto>

<!-- ✅ CORRECTO: usa paréntesis (event binding) -->
<app-tarjeta-producto (productoSeleccionado)="onProductoSeleccionado($event)">
</app-tarjeta-producto>
```

Verifica también que el nombre en el `@Output()` del hijo y en el template del padre sean idénticos:

```typescript
// Hijo — debe coincidir exactamente
@Output() productoSeleccionado = new EventEmitter<Producto>();
```

```html
<!-- Padre — mismo nombre entre paréntesis -->
(productoSeleccionado)="onProductoSeleccionado($event)"
```

---

### Problema 2 — Al hacer clic en "Agregar" también se dispara `onProductoSeleccionado`

**Síntoma:** Cada vez que el usuario hace clic en el botón **Agregar** o en el botón 🗑, el panel lateral también se abre (como si también se hubiera hecho clic en la tarjeta). Los `console.log` muestran dos acciones simultáneas: "Agregado: ..." **y** "Seleccionado: ...".

**Causa probable:** El método `onAgregarAlCarrito` o `onEliminar` no llama a `event.stopPropagation()`, por lo que el evento de clic del botón se propaga hacia arriba hasta el `<div>` contenedor de la tarjeta, que tiene el binding `(click)="onSeleccionar()"`.

**Solución:**

Verifica que los métodos en el componente hijo reciben el objeto `Event` y llaman a `stopPropagation()`:

```typescript
// ❌ INCORRECTO: no detiene la propagación
onAgregarAlCarrito(): void {
  this.agregarAlCarrito.emit({ producto: this.producto, cantidad: this.cantidad });
}

// ✅ CORRECTO: detiene la propagación del evento DOM
onAgregarAlCarrito(event: Event): void {
  event.stopPropagation();  // <-- imprescindible
  this.agregarAlCarrito.emit({ producto: this.producto, cantidad: this.cantidad });
}
```

Y en el template del hijo, asegúrate de pasar `$event` al método:

```html
<!-- ❌ INCORRECTO: no pasa el evento -->
<button (click)="onAgregarAlCarrito()">Agregar</button>

<!-- ✅ CORRECTO: pasa $event para poder llamar stopPropagation() -->
<button (click)="onAgregarAlCarrito($event)">Agregar</button>
```

---

## 9. Limpieza del Entorno

Al finalizar la práctica, realiza las siguientes acciones:

1. **Detén el servidor de desarrollo** en la terminal con `Ctrl + C`.

2. **Guarda todos los archivos modificados** en VS Code (`Ctrl + K S` en Windows/Linux, `⌘ + K S` en macOS).

3. **Confirma los cambios con Git** (recomendado para mantener un historial del progreso):

```bash
cd tienda-componentes
git add .
git commit -m "feat: implementar @Output y EventEmitter en tarjeta-producto (Lab 06-00-02)"
```

4. **Cierra las pestañas de Chrome** que ya no necesites, especialmente si Angular DevTools estaba abierto, para liberar memoria RAM.

5. El proyecto queda en un estado **funcional y guardado** para ser utilizado como base en prácticas futuras del módulo.

---

## 10. Resumen

### Lo que construiste

En esta práctica completaste el ciclo de comunicación bidireccional entre componentes Angular:

| Mecanismo | Dirección | Implementación |
|---|---|---|
| `@Input()` | Padre → Hijo | `[producto]="prod"` en el template del padre |
| `@Output()` + `EventEmitter` | Hijo → Padre | `(productoSeleccionado)="onProductoSeleccionado($event)"` |

### Conceptos clave reforzados

- **`@Output` es un decorador de propiedad** que expone un `EventEmitter` como canal de salida de eventos del componente.
- **`EventEmitter<T>` es genérico**: el tipo `T` define qué datos viajan con el evento, garantizando seguridad de tipos en tiempo de compilación.
- **`emit(valor)`** es el método que dispara el evento; el valor pasado se convierte en `$event` en el template del padre.
- **`event.stopPropagation()`** es esencial cuando hay elementos anidados con listeners de clic para evitar disparos no deseados.
- **`@Output` solo funciona para comunicación padre-hijo directa**. Para comunicación entre componentes no relacionados jerárquicamente se debe usar un servicio con `Subject` o `BehaviorSubject` de RxJS.

### Diferencia fundamental entre eventos nativos y `@Output`

| Característica | Evento nativo DOM | `@Output` + EventEmitter |
|---|---|---|
| Propagación | Se propaga por el árbol DOM | No se propaga; solo llega al padre directo |
| Tipado | No tipado (`Event`) | Tipado con genéricos (`EventEmitter<T>`) |
| Alcance | Cualquier ancestro en el DOM | Solo el componente padre inmediato |
| Uso | Interacciones del usuario con el DOM | Comunicación entre componentes Angular |

### Recursos adicionales

- [Documentación oficial de Angular: Component Interaction](https://angular.dev/guide/components/inputs)
- [Referencia de la API: EventEmitter](https://angular.dev/api/core/EventEmitter)
- [Guía oficial: Sharing data between child and parent directives and components](https://angular.dev/guide/components/outputs)
- [Angular DevTools — Chrome Web Store](https://chrome.google.com/webstore/detail/angular-devtools/ienfalfjdbdpebioblfackkekamfmbnh)

---
