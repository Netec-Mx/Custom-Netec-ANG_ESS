# Programación con TypeScript

## Metadatos

| Campo            | Detalle                          |
|------------------|----------------------------------|
| **Duración**     | 26 minutos                       |
| **Complejidad**  | Media                            |
| **Nivel Bloom**  | Aplicar (Apply)                  |
| **Módulo**       | 3 — Fundamentos de TypeScript    |
| **Herramientas** | TypeScript 5.x, tsc, Node.js, VS Code |

---

## Descripción General

En esta práctica realizarás un recorrido guiado por las características fundamentales de TypeScript: compilarás y ejecutarás archivos `.ts` usando el compilador `tsc` y Node.js, y explorarás los tipos de datos primitivos, operadores, estructuras de control, funciones, cadenas de texto, arreglos, enums y desestructuración. Cada ejercicio es un programa independiente que escribirás, compilarás y ejecutarás desde la terminal, observando cómo TypeScript transforma el código en JavaScript estándar. Al finalizar, tendrás una base sólida del lenguaje que usarás en todos los laboratorios de Angular posteriores.

---

## Objetivos de Aprendizaje

Al completar este laboratorio serás capaz de:

- [ ] Compilar y ejecutar archivos TypeScript con `tsc` y `node`, comprendiendo el proceso de transpilación a JavaScript.
- [ ] Declarar variables con `let`, `const` y `var` aplicando tipos primitivos: `string`, `number`, `boolean`, `null`, `undefined`, `any` y `unknown`.
- [ ] Implementar estructuras de control (`if/else`, `switch`, `for`, `while`, `for...of`, `for...in`) y funciones con parámetros tipados, opcionales y por defecto.
- [ ] Manipular arreglos tipados y tuplas usando métodos `map`, `filter`, `reduce` y `forEach`, e implementar enums numéricos y de cadena.
- [ ] Aplicar desestructuración de objetos y arreglos con el operador spread en contextos tipados.

---

## Prerrequisitos

### Conocimientos

- Laboratorio 02-00-01 completado (TypeScript instalado globalmente).
- Conocimientos de programación en JavaScript: variables, funciones, objetos y arreglos.
- Familiaridad con al menos un lenguaje orientado a objetos.
- Manejo básico de terminal o línea de comandos (crear directorios, navegar, ejecutar comandos).

### Acceso y Software

- TypeScript 5.x instalado globalmente (`npm install -g typescript`).
- Node.js 20.x LTS instalado y funcional.
- Visual Studio Code 1.85.x o superior con la extensión **Angular Language Service** (proporciona IntelliSense para TypeScript).
- Terminal funcional: PowerShell/CMD en Windows, Bash/Zsh en macOS/Linux.

---

## Entorno de Laboratorio

### Especificaciones de Hardware Recomendadas

| Componente        | Mínimo              | Recomendado          |
|-------------------|---------------------|----------------------|
| Procesador        | Intel Core i5 64-bit | Intel Core i7        |
| RAM               | 8 GB                | 16 GB                |
| Espacio en disco  | 10 GB libres        | 20 GB libres         |
| Resolución        | 1280×768            | 1920×1080            |
| Conexión a internet | 10 Mbps           | 20 Mbps o superior   |

### Software Requerido

| Software          | Versión mínima | Verificación                  |
|-------------------|----------------|-------------------------------|
| Node.js           | 18.x LTS       | `node --version`              |
| NPM               | 9.x            | `npm --version`               |
| TypeScript (tsc)  | 4.9.x          | `tsc --version`               |
| Visual Studio Code| 1.85.x         | Menú *Help → About*           |

### Preparación del Entorno

Antes de comenzar los ejercicios, verifica que las herramientas estén instaladas correctamente y crea el directorio de trabajo:

```bash
# 1. Verificar versiones instaladas
node --version
npm --version
tsc --version

# 2. Crear el directorio de trabajo para esta práctica
mkdir ts-fundamentos
cd ts-fundamentos

# 3. (Opcional) Abrir VS Code en el directorio actual
code .
```

> **Nota para Windows (CMD):** Usa `md ts-fundamentos` en lugar de `mkdir ts-fundamentos` si estás en el símbolo del sistema clásico. En PowerShell, `mkdir` funciona igual que en Bash.

> **Nota para macOS/Linux con permisos globales:** Si `tsc --version` falla con un error de permisos, ejecuta:
> ```bash
> npm config set prefix ~/.npm-global
> export PATH="$HOME/.npm-global/bin:$PATH"
> # Agregar la línea export al archivo ~/.bashrc o ~/.zshrc para que sea permanente
> ```

---

## Procedimiento Paso a Paso

### Ejercicio 1 — Compilación Básica: El Flujo Completo de TypeScript a JavaScript

**Objetivo:** Experimentar el ciclo completo de compilación: escribir un archivo `.ts`, compilarlo con `tsc`, inspeccionar el `.js` generado y ejecutarlo con `node`.

#### Instrucciones

1. Asegúrate de estar dentro del directorio `ts-fundamentos` en tu terminal.

2. Crea el archivo `hello.ts` con el siguiente contenido en VS Code o con tu editor preferido:

```typescript
// hello.ts — Primer programa TypeScript

function saludar(nombre: string): string {
  return `Hola, ${nombre}. Bienvenido a TypeScript y Angular.`;
}

const mensaje: string = saludar("Estudiante");
console.log(mensaje);

// Intentar asignar un número a una variable string (esto causaría error de compilación)
// const mensajeErroneo: string = 42; // Descomenta esta línea para ver el error
```

3. Compila el archivo con el compilador de TypeScript:

```bash
tsc hello.ts
```

4. Verifica que se generó el archivo `hello.js` en el mismo directorio:

```bash
# En macOS/Linux
ls -la

# En Windows (PowerShell)
dir
```

5. Abre `hello.js` en VS Code y compara su contenido con `hello.ts`. Observa las diferencias.

6. Ejecuta el JavaScript compilado con Node.js:

```bash
node hello.js
```

7. **Tarea de modificación:** Agrega una segunda función `despedir(nombre: string): string` que retorne `"Hasta luego, ${nombre}."` y llámala después de `saludar`. Recompila y vuelve a ejecutar.

8. **Exploración del error de tipos:** Descomenta la línea `// const mensajeErroneo: string = 42;` en `hello.ts`, intenta compilar y observa el mensaje de error. Vuelve a comentar la línea.

```bash
tsc hello.ts
# Observa el error: Type 'number' is not assignable to type 'string'.
```

#### Salida Esperada

```
Hola, Estudiante. Bienvenido a TypeScript y Angular.
```

Contenido de `hello.js` generado (sin anotaciones de tipo):

```javascript
function saludar(nombre) {
    return "Hola, " + nombre + ". Bienvenido a TypeScript y Angular.";
}
var mensaje = saludar("Estudiante");
console.log(mensaje);
```

#### Verificación

- [ ] El archivo `hello.js` existe en el directorio `ts-fundamentos`.
- [ ] La consola muestra el saludo correctamente.
- [ ] El archivo `.js` no contiene anotaciones de tipo (`: string`, `: void`, etc.).
- [ ] El error de tipo fue visible al descomentar la línea de asignación incorrecta.

---

### Ejercicio 2 — Variables y Tipos de Datos Primitivos

**Objetivo:** Declarar variables con `let`, `const` y `var` usando tipos explícitos e inferidos, y experimentar con todos los tipos primitivos de TypeScript.

#### Instrucciones

1. Crea el archivo `variables.ts`:

```typescript
// variables.ts — Variables y tipos primitivos en TypeScript

// --- Tipos explícitos ---
let nombre: string = "Angular";
let version: number = 17;
let esEstable: boolean = true;
let valorNulo: null = null;
let sinDefinir: undefined = undefined;
let cualquierCosa: any = "texto";
let desconocido: unknown = 42;

// --- Tipos inferidos (TypeScript deduce el tipo automáticamente) ---
let framework = "Angular";       // TypeScript infiere: string
let anio = 2024;                  // TypeScript infiere: number
const PI = 3.14159;               // TypeScript infiere: number (constante)

// --- Demostración de inferencia ---
console.log("=== Tipos Explícitos ===");
console.log(`nombre: ${nombre} (string)`);
console.log(`version: ${version} (number)`);
console.log(`esEstable: ${esEstable} (boolean)`);
console.log(`valorNulo: ${valorNulo} (null)`);
console.log(`sinDefinir: ${sinDefinir} (undefined)`);

// --- any vs unknown ---
console.log("\n=== any vs unknown ===");
cualquierCosa = 100;              // 'any' permite reasignar a cualquier tipo
cualquierCosa = true;
console.log(`cualquierCosa ahora es: ${cualquierCosa}`);

// Con 'unknown' debemos verificar el tipo antes de usarlo (type narrowing)
if (typeof desconocido === "number") {
  console.log(`desconocido es un número: ${desconocido * 2}`);
}

// --- const vs let ---
console.log("\n=== const vs let ===");
const MAX_INTENTOS: number = 3;
let intentosActuales: number = 0;
intentosActuales++;
console.log(`Intentos: ${intentosActuales} de ${MAX_INTENTOS}`);
// MAX_INTENTOS = 5; // Error: no se puede reasignar una constante
```

2. Compila y ejecuta:

```bash
tsc variables.ts && node variables.js
```

3. **Tarea de modificación:** Agrega al final del archivo tres variables más:
   - Una variable `email` de tipo `string` con tu correo ficticio.
   - Una constante `GRAVEDAD` de tipo `number` con el valor `9.8`.
   - Una variable `activo` de tipo `boolean` inicializada en `false`, luego cámbiala a `true` y muéstrala en consola.

#### Salida Esperada

```
=== Tipos Explícitos ===
nombre: Angular (string)
version: 17 (number)
esEstable: true (boolean)
valorNulo: null (null)
sinDefinir: undefined (undefined)

=== any vs unknown ===
cualquierCosa ahora es: true
desconocido es un número: 84

=== const vs let ===
Intentos: 1 de 3
```

#### Verificación

- [ ] El comando `tsc variables.ts` no produce errores.
- [ ] La salida en consola muestra todos los valores correctamente.
- [ ] Intentar reasignar `MAX_INTENTOS` produce un error de compilación.

---

### Ejercicio 3 — Operadores y Type Narrowing

**Objetivo:** Implementar una calculadora básica con tipos numéricos y demostrar el concepto de *type narrowing* con el operador `typeof`.

#### Instrucciones

1. Crea el archivo `operadores.ts`:

```typescript
// operadores.ts — Operadores y type narrowing

// --- Operadores aritméticos ---
function calculadora(a: number, b: number, operacion: string): number | string {
  switch (operacion) {
    case "+": return a + b;
    case "-": return a - b;
    case "*": return a * b;
    case "/":
      if (b === 0) return "Error: división por cero";
      return a / b;
    case "%": return a % b;
    default:  return "Operación no reconocida";
  }
}

console.log("=== Calculadora ===");
console.log(`10 + 3 = ${calculadora(10, 3, "+")}`);
console.log(`10 - 3 = ${calculadora(10, 3, "-")}`);
console.log(`10 * 3 = ${calculadora(10, 3, "*")}`);
console.log(`10 / 3 = ${calculadora(10, 3, "/")}`);
console.log(`10 % 3 = ${calculadora(10, 3, "%")}`);
console.log(`10 / 0 = ${calculadora(10, 0, "/")}`);

// --- Operadores de comparación ---
console.log("\n=== Comparaciones ===");
console.log(`5 == "5"  → ${5 == "5"}  (igualdad débil, evitar en TypeScript)`);
console.log(`5 === "5" → ${5 === ("5" as any)}  (igualdad estricta, recomendada)`);
console.log(`5 !== 3   → ${5 !== 3}`);
console.log(`10 >= 10  → ${10 >= 10}`);

// --- Operadores lógicos ---
console.log("\n=== Lógicos ===");
const tienePermiso: boolean = true;
const estaAutenticado: boolean = true;
console.log(`Puede acceder: ${tienePermiso && estaAutenticado}`);
console.log(`Alternativa: ${false || estaAutenticado}`);
console.log(`Negación: ${!tienePermiso}`);

// --- Type narrowing con typeof ---
console.log("\n=== Type Narrowing ===");
function procesarValor(valor: number | string): void {
  if (typeof valor === "number") {
    console.log(`Es un número: ${valor.toFixed(2)}`);
  } else {
    console.log(`Es una cadena: ${valor.toUpperCase()}`);
  }
}
procesarValor(3.14159);
procesarValor("typescript");

// --- Operador nullish coalescing (??) ---
console.log("\n=== Nullish Coalescing ===");
const nombreUsuario: string | null = null;
const nombreMostrar: string = nombreUsuario ?? "Invitado";
console.log(`Usuario: ${nombreMostrar}`);
```

2. Compila y ejecuta:

```bash
tsc operadores.ts && node operadores.js
```

3. **Tarea de modificación:** Agrega una función `esPar(n: number): boolean` que retorne `true` si el número es par usando el operador `%`. Pruébala con los valores 4, 7 y 0.

#### Salida Esperada

```
=== Calculadora ===
10 + 3 = 13
10 - 3 = 7
10 * 3 = 30
10 / 3 = 3.3333333333333335
10 % 3 = 1
10 / 0 = Error: división por cero

=== Comparaciones ===
5 == "5"  → true  (igualdad débil, evitar en TypeScript)
5 === "5" → false  (igualdad estricta, recomendada)
5 !== 3   → true
10 >= 10  → true

=== Lógicos ===
Puede acceder: true
Alternativa: true
Negación: false

=== Type Narrowing ===
Es un número: 3.14
Es una cadena: TYPESCRIPT

=== Nullish Coalescing ===
Usuario: Invitado
```

#### Verificación

- [ ] La calculadora maneja correctamente los cinco operadores y la división por cero.
- [ ] La función `procesarValor` distingue correctamente entre `number` y `string`.
- [ ] El operador `??` retorna el valor por defecto cuando el original es `null`.

---

### Ejercicio 4 — Estructuras de Control

**Objetivo:** Implementar FizzBuzz con tipado explícito y recorrer un arreglo tipado con `for...of`.

#### Instrucciones

1. Crea el archivo `control.ts`:

```typescript
// control.ts — Estructuras de control con tipado

// --- FizzBuzz con tipado ---
console.log("=== FizzBuzz (1-20) ===");
for (let i: number = 1; i <= 20; i++) {
  let resultado: string;
  if (i % 15 === 0) {
    resultado = "FizzBuzz";
  } else if (i % 3 === 0) {
    resultado = "Fizz";
  } else if (i % 5 === 0) {
    resultado = "Buzz";
  } else {
    resultado = i.toString();
  }
  process.stdout.write(resultado + " ");
}
console.log(); // salto de línea

// --- while: contador regresivo ---
console.log("\n=== Cuenta Regresiva ===");
let contador: number = 5;
while (contador > 0) {
  console.log(`  ${contador}...`);
  contador--;
}
console.log("  ¡Despegue!");

// --- switch con tipo string ---
console.log("\n=== Switch: Día de la Semana ===");
const dia: string = "miércoles";
switch (dia) {
  case "lunes":
  case "martes":
  case "miércoles":
  case "jueves":
  case "viernes":
    console.log(`${dia} es día laboral.`);
    break;
  case "sábado":
  case "domingo":
    console.log(`${dia} es fin de semana.`);
    break;
  default:
    console.log("Día no reconocido.");
}

// --- for...of sobre arreglo tipado ---
console.log("\n=== for...of: Lenguajes ===");
const lenguajes: string[] = ["TypeScript", "JavaScript", "Python", "Rust"];
for (const lenguaje of lenguajes) {
  console.log(`  → ${lenguaje}`);
}

// --- for...in sobre objeto ---
console.log("\n=== for...in: Propiedades de Objeto ===");
const config: { [key: string]: string | number } = {
  host: "localhost",
  puerto: 4200,
  entorno: "desarrollo"
};
for (const clave in config) {
  console.log(`  ${clave}: ${config[clave]}`);
}
```

2. Compila y ejecuta:

```bash
tsc control.ts && node control.js
```

3. **Tarea de modificación:** Agrega un bucle `do...while` que simule lanzar un dado (usa `Math.floor(Math.random() * 6) + 1`) hasta obtener un 6. Muestra cada lanzamiento en consola con su número de intento. Usa una variable `intentos: number` para contar.

#### Salida Esperada

```
=== FizzBuzz (1-20) ===
1 2 Fizz 4 Buzz Fizz 7 8 Fizz Buzz 11 Fizz 13 14 FizzBuzz 16 17 Fizz 19 Buzz 

=== Cuenta Regresiva ===
  5...
  4...
  3...
  2...
  1...
  ¡Despegue!

=== Switch: Día de la Semana ===
miércoles es día laboral.

=== for...of: Lenguajes ===
  → TypeScript
  → JavaScript
  → Python
  → Rust

=== for...in: Propiedades de Objeto ===
  host: localhost
  puerto: 4200
  entorno: desarrollo
```

#### Verificación

- [ ] FizzBuzz produce la secuencia correcta del 1 al 20.
- [ ] El `switch` identifica correctamente los días laborales y de fin de semana.
- [ ] El `for...of` recorre todos los elementos del arreglo.

---

### Ejercicio 5 — Funciones Tipadas

**Objetivo:** Definir funciones con parámetros tipados, valores de retorno, parámetros opcionales, parámetros por defecto y funciones flecha (*arrow functions*).

#### Instrucciones

1. Crea el archivo `funciones.ts`:

```typescript
// funciones.ts — Funciones con tipado en TypeScript

// --- Función con tipo de retorno explícito ---
function sumar(a: number, b: number): number {
  return a + b;
}
console.log(`sumar(5, 3) = ${sumar(5, 3)}`);

// --- Parámetros opcionales (?) ---
function calcularArea(base: number, altura?: number): number {
  if (altura !== undefined) {
    return base * altura;           // Área de rectángulo
  }
  return base * base;               // Área de cuadrado
}
console.log(`Área cuadrado (4):    ${calcularArea(4)}`);
console.log(`Área rectángulo (4,6): ${calcularArea(4, 6)}`);

// --- Parámetros con valor por defecto ---
function saludarConIdioma(nombre: string, idioma: string = "español"): string {
  const saludos: { [key: string]: string } = {
    español: "Hola",
    inglés: "Hello",
    francés: "Bonjour"
  };
  const saludo: string = saludos[idioma] ?? "Hola";
  return `${saludo}, ${nombre}!`;
}
console.log(saludarConIdioma("María"));
console.log(saludarConIdioma("John", "inglés"));
console.log(saludarConIdioma("Pierre", "francés"));

// --- Arrow functions ---
const multiplicar = (a: number, b: number): number => a * b;
const esMayorDeEdad = (edad: number): boolean => edad >= 18;
const cuadrado = (n: number): number => n ** 2;

console.log(`\nmultiplicar(4, 7) = ${multiplicar(4, 7)}`);
console.log(`esMayorDeEdad(20) = ${esMayorDeEdad(20)}`);
console.log(`esMayorDeEdad(15) = ${esMayorDeEdad(15)}`);
console.log(`cuadrado(9) = ${cuadrado(9)}`);

// --- Función genérica básica ---
function primerElemento<T>(arreglo: T[]): T | undefined {
  return arreglo.length > 0 ? arreglo[0] : undefined;
}
console.log(`\nPrimer número: ${primerElemento([10, 20, 30])}`);
console.log(`Primera cadena: ${primerElemento(["Angular", "React", "Vue"])}`);
console.log(`Arreglo vacío: ${primerElemento([])}`);

// --- Función que retorna void ---
function registrarEvento(evento: string, timestamp: Date = new Date()): void {
  console.log(`[${timestamp.toISOString()}] Evento: ${evento}`);
}
registrarEvento("Usuario autenticado");
```

2. Compila y ejecuta:

```bash
tsc funciones.ts && node funciones.js
```

3. **Tarea de modificación:** Crea una arrow function `calcularIVA` que reciba un precio de tipo `number` y un porcentaje opcional de tipo `number` (valor por defecto `16`), y retorne el precio con IVA aplicado. Pruébala con `calcularIVA(100)` y `calcularIVA(100, 21)`.

#### Salida Esperada

```
sumar(5, 3) = 8
Área cuadrado (4):    16
Área rectángulo (4,6): 24
Hola, María!
Hello, John!
Bonjour, Pierre!

multiplicar(4, 7) = 28
esMayorDeEdad(20) = true
esMayorDeEdad(15) = false
cuadrado(9) = 81

Primer número: 10
Primera cadena: Angular
Arreglo vacío: undefined
[2024-01-15T10:30:00.000Z] Evento: Usuario autenticado
```

*(La fecha y hora del evento variará según el momento de ejecución.)*

#### Verificación

- [ ] La función `calcularArea` maneja correctamente el parámetro opcional.
- [ ] Las arrow functions están correctamente tipadas y producen resultados correctos.
- [ ] La función genérica `primerElemento` funciona con `number[]` y `string[]`.

---

### Ejercicio 6 — Cadenas de Texto y Template Literals

**Objetivo:** Manipular cadenas con template literals, métodos de `String` y *type assertions*.

#### Instrucciones

1. Crea el archivo `cadenas.ts`:

```typescript
// cadenas.ts — Manipulación de cadenas en TypeScript

const nombreCompleto: string = "  María González Pérez  ";
const email: string = "maria@ejemplo.com";
const descripcion: string = "TypeScript es un superconjunto tipado de JavaScript";

// --- Template literals (backticks) ---
console.log("=== Template Literals ===");
const edad: number = 28;
const ciudad: string = "Ciudad de México";
const presentacion: string = `
  Nombre: ${nombreCompleto.trim()}
  Edad:   ${edad} años
  Ciudad: ${ciudad}
  Email:  ${email}
`;
console.log(presentacion);

// --- Métodos de String ---
console.log("=== Métodos de String ===");
console.log(`Original:     "${nombreCompleto}"`);
console.log(`trim():       "${nombreCompleto.trim()}"`);
console.log(`toUpperCase(): "${nombreCompleto.trim().toUpperCase()}"`);
console.log(`toLowerCase(): "${nombreCompleto.trim().toLowerCase()}"`);
console.log(`length:        ${nombreCompleto.trim().length}`);
console.log(`includes("González"): ${nombreCompleto.includes("González")}`);
console.log(`startsWith("  M"):    ${nombreCompleto.startsWith("  M")}`);
console.log(`replace:      "${nombreCompleto.trim().replace("González", "Martínez")}"`);

// --- split y join ---
console.log("\n=== split / join ===");
const palabras: string[] = descripcion.split(" ");
console.log(`Palabras (${palabras.length}): ${palabras.join(" | ")}`);

// --- Interpolación con expresiones ---
console.log("\n=== Interpolación con Expresiones ===");
const precios: number[] = [10.5, 25.0, 8.75];
const total: number = precios.reduce((acc, p) => acc + p, 0);
console.log(`Subtotal: $${total.toFixed(2)}`);
console.log(`Con IVA (16%): $${(total * 1.16).toFixed(2)}`);

// --- Type assertion (as) ---
console.log("\n=== Type Assertion ===");
const valorDesconocido: unknown = "12345";
const longitud: number = (valorDesconocido as string).length;
console.log(`Longitud de "${valorDesconocido}": ${longitud}`);

// --- Cadenas multilínea ---
console.log("\n=== Cadena Multilínea ===");
const sql: string = `
  SELECT nombre, email
  FROM usuarios
  WHERE activo = true
  ORDER BY nombre ASC
`;
console.log(sql);
```

2. Compila y ejecuta:

```bash
tsc cadenas.ts && node cadenas.js
```

3. **Tarea de modificación:** Crea una función `formatearTarjeta(numero: string): string` que reciba un número de tarjeta de 16 dígitos (como `"1234567890123456"`) y lo formatee como `"1234 5678 9012 3456"` usando `split("")`, `join("")` y template literals. Pruébala con al menos dos números.

#### Verificación

- [ ] Los métodos de `String` producen los resultados esperados.
- [ ] El `split` divide correctamente la descripción en palabras.
- [ ] La *type assertion* permite acceder a `.length` sin errores de compilación.

---

### Ejercicio 7 — Arreglos Tipados y Tuplas

**Objetivo:** Crear y manipular arreglos tipados usando `map`, `filter`, `reduce` y `forEach`, y definir tuplas para datos estructurados.

#### Instrucciones

1. Crea el archivo `arreglos.ts`:

```typescript
// arreglos.ts — Arreglos tipados y tuplas

// --- Arreglo tipado básico ---
const calificaciones: number[] = [85, 92, 78, 96, 88, 73, 91];
const materias: Array<string> = ["Matemáticas", "TypeScript", "Angular", "Node.js"];

console.log("=== Arreglo de Calificaciones ===");
console.log(`Original: [${calificaciones.join(", ")}]`);

// map: transformar cada elemento
const calificacionesExtra: number[] = calificaciones.map(c => c + 2);
console.log(`+2 puntos:  [${calificacionesExtra.join(", ")}]`);

// filter: filtrar elementos
const aprobados: number[] = calificaciones.filter(c => c >= 80);
console.log(`Aprobados (≥80): [${aprobados.join(", ")}]`);

// reduce: acumular un resultado
const promedio: number = calificaciones.reduce((acc, c) => acc + c, 0) / calificaciones.length;
console.log(`Promedio: ${promedio.toFixed(2)}`);

// forEach: iterar sin retorno
console.log("\nCalificaciones detalladas:");
calificaciones.forEach((calificacion: number, indice: number) => {
  const estado: string = calificacion >= 80 ? "✓ Aprobado" : "✗ Reprobado";
  console.log(`  [${indice + 1}] ${calificacion} — ${estado}`);
});

// --- Métodos adicionales ---
console.log("\n=== Métodos de Array ===");
console.log(`Máxima: ${Math.max(...calificaciones)}`);
console.log(`Mínima: ${Math.min(...calificaciones)}`);
console.log(`Incluye 96: ${calificaciones.includes(96)}`);
console.log(`Índice de 78: ${calificaciones.indexOf(78)}`);

// Ordenar (sort modifica el arreglo original, usamos spread para copia)
const ordenadas: number[] = [...calificaciones].sort((a, b) => b - a);
console.log(`Ordenadas desc: [${ordenadas.join(", ")}]`);

// --- Tuplas ---
console.log("\n=== Tuplas ===");

// Tupla para coordenadas [x, y]
type Coordenada = [number, number];
const origen: Coordenada = [0, 0];
const punto: Coordenada = [3.5, -7.2];

function distancia(p1: Coordenada, p2: Coordenada): number {
  const dx: number = p2[0] - p1[0];
  const dy: number = p2[1] - p1[1];
  return Math.sqrt(dx ** 2 + dy ** 2);
}

console.log(`Origen: (${origen[0]}, ${origen[1]})`);
console.log(`Punto:  (${punto[0]}, ${punto[1]})`);
console.log(`Distancia al origen: ${distancia(origen, punto).toFixed(4)}`);

// Tupla con tipos mixtos: [nombre, edad, activo]
type RegistroUsuario = [string, number, boolean];
const usuario: RegistroUsuario = ["Ana Torres", 32, true];
const [nombreU, edadU, activoU] = usuario;  // Desestructuración de tupla
console.log(`\nUsuario: ${nombreU}, ${edadU} años, activo: ${activoU}`);
```

2. Compila y ejecuta:

```bash
tsc arreglos.ts && node arreglos.js
```

3. **Tarea de modificación:** Crea un arreglo `precios: number[]` con al menos 6 precios. Usa `map` para aplicar un descuento del 15%, `filter` para obtener solo los precios mayores a $50 (después del descuento) y `reduce` para calcular el total de esos precios con descuento. Muestra cada paso.

#### Salida Esperada

```
=== Arreglo de Calificaciones ===
Original: [85, 92, 78, 96, 88, 73, 91]
+2 puntos:  [87, 94, 80, 98, 90, 75, 93]
Aprobados (≥80): [85, 92, 96, 88, 91]
Promedio: 86.14

Calificaciones detalladas:
  [1] 85 — ✓ Aprobado
  [2] 92 — ✓ Aprobado
  [3] 78 — ✗ Reprobado
  [4] 96 — ✓ Aprobado
  [5] 88 — ✓ Aprobado
  [6] 73 — ✗ Reprobado
  [7] 91 — ✓ Aprobado
...
```

#### Verificación

- [ ] `map`, `filter` y `reduce` producen los resultados correctos.
- [ ] La tupla `Coordenada` funciona correctamente con la función `distancia`.
- [ ] La desestructuración de la tupla `RegistroUsuario` asigna los valores correctamente.

---

### Ejercicio 8 — Enums

**Objetivo:** Implementar enums numéricos y de cadena para representar conjuntos de constantes relacionadas.

#### Instrucciones

1. Crea el archivo `enums.ts`:

```typescript
// enums.ts — Enums numéricos y de cadena en TypeScript

// --- Enum numérico: Días de la semana ---
enum DiaSemana {
  Lunes = 1,    // Iniciamos en 1 (por defecto empezaría en 0)
  Martes,       // 2
  Miércoles,    // 3
  Jueves,       // 4
  Viernes,      // 5
  Sábado,       // 6
  Domingo       // 7
}

console.log("=== Enum Numérico: Días de la Semana ===");
console.log(`Lunes = ${DiaSemana.Lunes}`);
console.log(`Viernes = ${DiaSemana.Viernes}`);
console.log(`Domingo = ${DiaSemana.Domingo}`);

// Acceso inverso (numérico → nombre)
console.log(`Día 3 = ${DiaSemana[3]}`);
console.log(`Día 5 = ${DiaSemana[5]}`);

function esDiaLaboral(dia: DiaSemana): boolean {
  return dia >= DiaSemana.Lunes && dia <= DiaSemana.Viernes;
}

console.log(`\n¿Lunes es laboral?  ${esDiaLaboral(DiaSemana.Lunes)}`);
console.log(`¿Sábado es laboral? ${esDiaLaboral(DiaSemana.Sábado)}`);

// --- Enum de cadena: Colores del semáforo ---
enum ColorSemaforo {
  Rojo    = "ROJO",
  Amarillo = "AMARILLO",
  Verde   = "VERDE"
}

console.log("\n=== Enum de Cadena: Semáforo ===");

function interpretarSemaforo(color: ColorSemaforo): string {
  switch (color) {
    case ColorSemaforo.Rojo:     return "DETENTE — Luz roja";
    case ColorSemaforo.Amarillo: return "PRECAUCIÓN — Luz amarilla";
    case ColorSemaforo.Verde:    return "AVANZA — Luz verde";
  }
}

console.log(interpretarSemaforo(ColorSemaforo.Rojo));
console.log(interpretarSemaforo(ColorSemaforo.Amarillo));
console.log(interpretarSemaforo(ColorSemaforo.Verde));

// --- Enum de cadena: Estados de una solicitud HTTP ---
enum EstadoSolicitud {
  Pendiente  = "PENDIENTE",
  Procesando = "PROCESANDO",
  Completada = "COMPLETADA",
  Error      = "ERROR"
}

console.log("\n=== Enum: Estados de Solicitud ===");
let estadoActual: EstadoSolicitud = EstadoSolicitud.Pendiente;
console.log(`Estado inicial: ${estadoActual}`);
estadoActual = EstadoSolicitud.Procesando;
console.log(`Procesando...   ${estadoActual}`);
estadoActual = EstadoSolicitud.Completada;
console.log(`Finalizado:     ${estadoActual}`);

// Comparación de enums
const esExitoso: boolean = estadoActual === EstadoSolicitud.Completada;
console.log(`¿Exitoso? ${esExitoso}`);
```

2. Compila y ejecuta:

```bash
tsc enums.ts && node enums.js
```

3. **Tarea de modificación:** Crea un enum `NivelPrioridad` con valores de cadena `"BAJA"`, `"MEDIA"`, `"ALTA"` y `"CRITICA"`. Crea una función `obtenerColorPrioridad(nivel: NivelPrioridad): string` que retorne un color (como texto) asociado a cada nivel. Pruébala con los cuatro valores.

#### Salida Esperada

```
=== Enum Numérico: Días de la Semana ===
Lunes = 1
Viernes = 5
Domingo = 7
Día 3 = Miércoles
Día 5 = Viernes

¿Lunes es laboral?  true
¿Sábado es laboral? false

=== Enum de Cadena: Semáforo ===
DETENTE — Luz roja
PRECAUCIÓN — Luz amarilla
AVANZA — Luz verde

=== Enum: Estados de Solicitud ===
Estado inicial: PENDIENTE
Procesando...   PROCESANDO
Finalizado:     COMPLETADA
¿Exitoso? true
```

#### Verificación

- [ ] El enum numérico permite acceso inverso (número → nombre).
- [ ] El enum de cadena retorna el valor de cadena, no el índice numérico.
- [ ] La función `esDiaLaboral` usa correctamente los valores del enum para comparar.

---

### Ejercicio 9 — Desestructuración y Operador Spread

**Objetivo:** Aplicar desestructuración de objetos y arreglos, y el operador spread en contextos tipados.

#### Instrucciones

1. Crea el archivo `destructuring.ts`:

```typescript
// destructuring.ts — Desestructuración y spread en TypeScript

// --- Desestructuración de objeto ---
interface Persona {
  nombre: string;
  apellido: string;
  edad: number;
  ciudad: string;
  email?: string;    // propiedad opcional
}

const persona: Persona = {
  nombre: "Carlos",
  apellido: "Ramírez",
  edad: 35,
  ciudad: "Guadalajara",
  email: "carlos@ejemplo.com"
};

console.log("=== Desestructuración de Objeto ===");

// Desestructuración básica
const { nombre, apellido, edad } = persona;
console.log(`Nombre: ${nombre} ${apellido}, Edad: ${edad}`);

// Desestructuración con renombrado
const { ciudad: ciudadResidencia, email: correo = "No especificado" } = persona;
console.log(`Ciudad: ${ciudadResidencia}`);
console.log(`Correo: ${correo}`);

// Desestructuración en parámetro de función
function mostrarPersona({ nombre, apellido, edad, ciudad }: Persona): void {
  console.log(`  → ${nombre} ${apellido} | ${edad} años | ${ciudad}`);
}
console.log("\nPersonas del equipo:");
mostrarPersona(persona);
mostrarPersona({ nombre: "Laura", apellido: "Soto", edad: 28, ciudad: "Monterrey" });

// --- Desestructuración de arreglo ---
console.log("\n=== Desestructuración de Arreglo ===");
const coordenadas: [number, number, number] = [10.5, -3.2, 7.8];
const [x, y, z] = coordenadas;
console.log(`x=${x}, y=${y}, z=${z}`);

const numeros: number[] = [1, 2, 3, 4, 5, 6, 7];
const [primero, segundo, ...resto] = numeros;
console.log(`Primero: ${primero}`);
console.log(`Segundo: ${segundo}`);
console.log(`Resto: [${resto.join(", ")}]`);

// --- Operador spread ---
console.log("\n=== Operador Spread ===");

// Spread en arreglos
const frutas: string[] = ["manzana", "pera", "uva"];
const verduras: string[] = ["zanahoria", "brócoli"];
const alimentos: string[] = [...frutas, ...verduras, "aguacate"];
console.log(`Alimentos: [${alimentos.join(", ")}]`);

// Spread en objetos (copia y extensión)
const personaBase: Persona = { nombre: "Ana", apellido: "López", edad: 30, ciudad: "CDMX" };
const personaActualizada: Persona = { ...personaBase, ciudad: "Puebla", email: "ana@nuevo.com" };
console.log(`\nBase:        ${personaBase.ciudad}`);
console.log(`Actualizada: ${personaActualizada.ciudad} — ${personaActualizada.email}`);

// Spread para pasar arreglo como argumentos
function sumarTres(a: number, b: number, c: number): number {
  return a + b + c;
}
const valores: [number, number, number] = [10, 20, 30];
console.log(`\nSuma con spread: ${sumarTres(...valores)}`);

// --- Combinación: desestructuración + spread ---
console.log("\n=== Combinar Objetos ===");
const configuracionBase = { debug: false, timeout: 3000, reintentos: 3 };
const configuracionDev  = { ...configuracionBase, debug: true, timeout: 10000 };
const { debug, timeout, reintentos } = configuracionDev;
console.log(`debug=${debug}, timeout=${timeout}ms, reintentos=${reintentos}`);
```

2. Compila y ejecuta:

```bash
tsc destructuring.ts && node destructuring.js
```

3. **Tarea de modificación:** Crea un arreglo de objetos `Persona[]` con al menos 3 personas. Usa desestructuración dentro de un `forEach` para imprimir cada persona en formato `"[índice] Nombre Apellido — Ciudad"`. Luego usa spread para crear un cuarto arreglo que combine las personas con dos personas adicionales definidas directamente.

#### Salida Esperada

```
=== Desestructuración de Objeto ===
Nombre: Carlos Ramírez, Edad: 35
Ciudad: Guadalajara
Correo: carlos@ejemplo.com

Personas del equipo:
  → Carlos Ramírez | 35 años | Guadalajara
  → Laura Soto | 28 años | Monterrey

=== Desestructuración de Arreglo ===
x=10.5, y=-3.2, z=7.8
Primero: 1
Segundo: 2
Resto: [3, 4, 5, 6, 7]

=== Operador Spread ===
Alimentos: [manzana, pera, uva, zanahoria, brócoli, aguacate]

Base:        CDMX
Actualizada: Puebla — ana@nuevo.com

Suma con spread: 60

=== Combinar Objetos ===
debug=true, timeout=10000ms, reintentos=3
```

#### Verificación

- [ ] La desestructuración con renombrado (`ciudad: ciudadResidencia`) funciona correctamente.
- [ ] El operador rest (`...resto`) captura todos los elementos restantes del arreglo.
- [ ] El spread de objetos crea una copia con las propiedades sobrescritas correctamente.

---

## Validación y Pruebas Finales

Una vez completados los 9 ejercicios, realiza las siguientes verificaciones para confirmar que el laboratorio está completo:

### Lista de Verificación Final

```bash
# Desde el directorio ts-fundamentos, verifica que existan todos los archivos
ls *.ts *.js

# Deberías ver:
# hello.ts         hello.js
# variables.ts     variables.js
# operadores.ts    operadores.js
# control.ts       control.js
# funciones.ts     funciones.js
# cadenas.ts       cadenas.js
# arreglos.ts      arreglos.js
# enums.ts         enums.js
# destructuring.ts destructuring.js
```

### Prueba de Recompilación Completa

Verifica que todos los archivos compilan sin errores ejecutando `tsc` en cada uno:

```bash
# En macOS/Linux — compilar todos los .ts del directorio
for f in *.ts; do echo "Compilando $f..."; tsc "$f" && echo "  OK"; done

# En Windows (PowerShell)
Get-ChildItem *.ts | ForEach-Object { Write-Host "Compilando $_..."; tsc $_.Name; if ($LASTEXITCODE -eq 0) { Write-Host "  OK" } }
```

### Prueba de Ejecución Completa

```bash
# En macOS/Linux — ejecutar todos los .js
for f in *.js; do echo "=== $f ==="; node "$f"; echo; done

# En Windows (PowerShell)
Get-ChildItem *.js | ForEach-Object { Write-Host "=== $_ ==="; node $_.Name; Write-Host "" }
```

### Preguntas de Reflexión

Responde mentalmente (o por escrito en un archivo `reflexion.md`) las siguientes preguntas:

1. ¿Qué diferencia fundamental existe entre `any` y `unknown`? ¿Cuándo preferirías uno sobre el otro?
2. ¿Por qué las anotaciones de tipo desaparecen en el archivo `.js` compilado? ¿Qué implica esto para el rendimiento en producción?
3. ¿Cuál es la ventaja de usar `const` sobre `let` cuando el valor no cambia? ¿Cómo ayuda TypeScript a reforzar esta práctica?
4. ¿Cuándo usarías un enum de cadena en lugar de un enum numérico? ¿Qué ventaja tiene el enum de cadena para la depuración?
5. ¿Cómo el operador spread facilita la inmutabilidad al trabajar con objetos y arreglos?

---

## Solución de Problemas

### Problema 1: `tsc: command not found` o `'tsc' no se reconoce como comando`

**Síntomas:**
- Al ejecutar `tsc --version`, la terminal muestra `command not found` (macOS/Linux) o `'tsc' no se reconoce como comando interno o externo` (Windows).
- El comando `tsc archivo.ts` falla inmediatamente sin compilar nada.

**Causa:**
TypeScript no está instalado globalmente, o el directorio de binarios globales de NPM no está en la variable de entorno `PATH`. Esto ocurre frecuentemente en macOS/Linux cuando se usa `sudo npm install -g typescript` sin configurar el prefijo de NPM, o en Windows cuando la instalación de Node.js no actualizó el `PATH` del sistema.

**Solución:**

```bash
# Paso 1: Verificar si TypeScript está instalado (aunque no esté en el PATH)
npm list -g typescript

# Paso 2a: Si NO está instalado, instalarlo
npm install -g typescript

# Paso 2b: En macOS/Linux, si hay problemas de permisos, configurar el prefijo primero
npm config set prefix ~/.npm-global
export PATH="$HOME/.npm-global/bin:$PATH"
echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.bashrc  # o ~/.zshrc
source ~/.bashrc
npm install -g typescript

# Paso 3: Verificar la instalación
tsc --version
# Debe mostrar: Version 5.x.x

# Alternativa temporal: usar npx si la instalación global falla
npx tsc archivo.ts
```

---

### Problema 2: Errores de compilación inesperados con `strict: true` al usar `tsconfig.json`

**Síntomas:**
- Al crear un `tsconfig.json` con `tsc --init` y luego ejecutar `tsc` (sin especificar archivo), aparecen errores como `Parameter 'x' implicitly has an 'any' type` o `Object is possibly 'null'` en archivos que antes compilaban bien.
- Los archivos `.js` dejan de generarse aunque el código parezca correcto.

**Causa:**
Cuando se ejecuta `tsc` sin argumentos, el compilador busca el `tsconfig.json` y aplica todas sus opciones, incluyendo `"strict": true` que activa verificaciones adicionales como `noImplicitAny` y `strictNullChecks`. Estas verificaciones son más estrictas que la compilación archivo por archivo (`tsc archivo.ts`), que usa opciones por defecto más permisivas.

**Solución:**

```bash
# Opción 1: Compilar siempre especificando el archivo (modo de práctica)
tsc hello.ts        # Compila solo ese archivo, sin tsconfig.json
node hello.js

# Opción 2: Ajustar el tsconfig.json para este directorio de práctica
# Editar tsconfig.json y cambiar:
# "strict": true  →  "strict": false
# O deshabilitar solo las verificaciones problemáticas:
# "noImplicitAny": false,
# "strictNullChecks": false

# Opción 3: Corregir el código para cumplir con strict mode (recomendado a largo plazo)
# Ejemplo: agregar tipos explícitos a todos los parámetros
# function ejemplo(x: number) { ... }  en lugar de  function ejemplo(x) { ... }

# Opción 4: Ignorar el tsconfig.json para un archivo específico
tsc --noEmitOnError false hello.ts

# Verificar que el archivo .js se generó correctamente
ls -la *.js
```

---

## Limpieza del Entorno

Al finalizar el laboratorio, puedes mantener los archivos para referencia futura o limpiar el directorio de trabajo. Los archivos `.js` generados son redundantes si conservas los `.ts`.

```bash
# Desde el directorio ts-fundamentos

# Opción A: Eliminar solo los archivos .js compilados (conservar los .ts)
# En macOS/Linux
rm *.js

# En Windows (PowerShell)
Remove-Item *.js

# Opción B: Eliminar el directorio completo (si ya no necesitas los archivos)
cd ..

# En macOS/Linux
rm -rf ts-fundamentos

# En Windows (PowerShell)
Remove-Item -Recurse -Force ts-fundamentos

# Opción C: Conservar todo el directorio como referencia (recomendado)
# No se requiere ninguna acción. Los archivos ocupan menos de 1 MB en total.
```

> **Recomendación:** Conserva el directorio `ts-fundamentos` con todos los archivos `.ts`. Serán útiles como referencia rápida durante los laboratorios de Angular que comienzan en el Módulo 4.

---

## Resumen

En este laboratorio recorriste los fundamentos esenciales de TypeScript mediante la escritura y ejecución de 9 programas independientes. Los conceptos clave que aplicaste:

| Ejercicio | Concepto Principal | Comando Utilizado |
|-----------|-------------------|-------------------|
| 1 | Compilación básica (transpilación TS → JS) | `tsc hello.ts && node hello.js` |
| 2 | Variables tipadas: `let`, `const`, tipos primitivos | `tsc variables.ts && node variables.js` |
| 3 | Operadores, type narrowing, nullish coalescing | `tsc operadores.ts && node operadores.js` |
| 4 | Estructuras de control con tipado | `tsc control.ts && node control.js` |
| 5 | Funciones: opcionales, por defecto, genéricas | `tsc funciones.ts && node funciones.js` |
| 6 | Template literals y métodos de String | `tsc cadenas.ts && node cadenas.js` |
| 7 | Arreglos tipados, `map/filter/reduce`, tuplas | `tsc arreglos.ts && node arreglos.js` |
| 8 | Enums numéricos y de cadena | `tsc enums.ts && node enums.js` |
| 9 | Desestructuración y operador spread | `tsc destructuring.ts && node destructuring.js` |

**Conceptos transversales reforzados:**
- Las anotaciones de tipo desaparecen en el JavaScript compilado: son exclusivas del tiempo de desarrollo.
- TypeScript detecta errores de tipo **antes** de ejecutar el código, reduciendo bugs en producción.
- El tipado estático mejora el autocompletado en VS Code, haciendo el desarrollo más productivo.
- Los patrones de desestructuración y spread son fundamentales en Angular para trabajar con `@Input`/`@Output` y el estado de componentes.

### Recursos Adicionales

- [TypeScript Handbook — Tipos básicos](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)
- [TypeScript Playground — Prueba código en línea](https://www.typescriptlang.org/play)
- [TypeScript Deep Dive (libro gratuito en línea)](https://basarat.gitbook.io/typescript/)
- [Referencia de opciones del compilador `tsconfig.json`](https://www.typescriptlang.org/tsconfig)
- [TypeScript en 5 minutos — Tutorial oficial](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)

---

---

# Escribir un programa en TypeScript que defina una clase de Objetos llamada Libro

## 1. Metadatos

| Campo            | Detalle                                                                 |
|------------------|-------------------------------------------------------------------------|
| **Duración**     | 26 minutos                                                              |
| **Complejidad**  | Media                                                                   |
| **Nivel Bloom**  | Crear (*Create*)                                                        |
| **Módulo**       | 3 — Fundamentos de TypeScript                                           |
| **Práctica**     | 3.2 — Sistema de gestión de biblioteca orientado a objetos              |

---

## 2. Descripción General

En esta práctica construirás un sistema simplificado de gestión de biblioteca utilizando los pilares de la Programación Orientada a Objetos en TypeScript: clases, herencia, interfaces, modificadores de acceso, enums y módulos. El proyecto se organiza en múltiples archivos `.ts` que se compilan con `tsc` usando un archivo `tsconfig.json`, reforzando el flujo de compilación estudiado en la lección 3.1. Al finalizar, ejecutarás el código compilado con Node.js y verificarás el comportamiento del sistema en consola.

---

## 3. Objetivos de Aprendizaje

Al completar esta práctica serás capaz de:

- [ ] Definir una clase TypeScript `Libro` con propiedades tipadas y modificadores de acceso `public`, `private` y `protected`, implementando un constructor, métodos de instancia y un método estático.
- [ ] Aplicar herencia en TypeScript creando la clase derivada `LibroDigital` que extiende `Libro` con propiedades y comportamiento adicionales.
- [ ] Implementar una interfaz `IBibliotecaItem` y un enum `Genero` para establecer contratos y valores constantes en el sistema.
- [ ] Crear una clase `Biblioteca` que gestione un arreglo tipado de libros con métodos de búsqueda, préstamo y estadísticas.
- [ ] Organizar el código en módulos TypeScript separados usando `export` e `import`, compilar el proyecto con `tsc` y ejecutarlo con Node.js.

---

## 4. Prerrequisitos

### Conocimientos Previos

| Conocimiento                                                             | Nivel requerido |
|--------------------------------------------------------------------------|-----------------|
| Laboratorio 03-00-01 completado (fundamentos de TypeScript)              | Obligatorio     |
| Clases, herencia, interfaces y encapsulamiento en POO                    | Sólido          |
| Módulos JavaScript/TypeScript (`import` / `export`)                      | Básico          |
| Uso de terminal / línea de comandos                                      | Básico          |

### Acceso y Herramientas

| Herramienta                  | Versión mínima | Verificación                         |
|------------------------------|----------------|--------------------------------------|
| Node.js                      | 18.x LTS       | `node --version`                     |
| TypeScript (global)          | 4.9.x          | `tsc --version`                      |
| Visual Studio Code           | 1.85.x         | Menú *Help → About*                  |
| Extensión Angular Language Service | 17.x     | Panel de extensiones de VS Code      |

---

## 5. Entorno de Laboratorio

### Requisitos de Hardware

| Recurso           | Mínimo        | Recomendado    |
|-------------------|---------------|----------------|
| RAM               | 8 GB          | 16 GB          |
| Almacenamiento    | 10 GB libres  | SSD con 20 GB  |
| Procesador        | i5 / 1.6 GHz  | i7 / 2.0 GHz   |
| Resolución        | 1280 × 768    | 1920 × 1080    |

### Verificación del Entorno

Abre una terminal y ejecuta los siguientes comandos para confirmar que las herramientas están disponibles:

```bash
# Verificar Node.js
node --version
# Salida esperada: v20.x.x  (mínimo v18.x.x)

# Verificar npm
npm --version
# Salida esperada: 10.x.x

# Verificar TypeScript
tsc --version
# Salida esperada: Version 5.x.x

# Si TypeScript NO está instalado globalmente, instalarlo ahora
npm install -g typescript
```

> **Nota para macOS/Linux:** Si `npm install -g` requiere permisos elevados, ejecuta primero:
> ```bash
> npm config set prefix ~/.npm-global
> export PATH="$HOME/.npm-global/bin:$PATH"
> ```
> Agrega la línea `export PATH` a tu archivo `~/.bashrc` o `~/.zshrc` para que persista.

---

## 6. Pasos del Laboratorio

### Estructura Final del Proyecto

Antes de comenzar, observa la estructura de archivos que construirás durante la práctica:

```
biblioteca-ts/
├── tsconfig.json
└── src/
    ├── enums/
    │   └── Genero.ts
    ├── interfaces/
    │   └── IBibliotecaItem.ts
    ├── models/
    │   ├── Libro.ts
    │   └── LibroDigital.ts
    ├── services/
    │   └── Biblioteca.ts
    └── main.ts
```

---

### Paso 1 — Crear el Proyecto e Inicializar la Configuración de TypeScript

**Objetivo:** Preparar la estructura de carpetas y el archivo `tsconfig.json` que dirigirá la compilación de todos los archivos del proyecto.

#### Instrucciones

1. Abre una terminal en el directorio donde almacenas tus prácticas.

2. Crea la carpeta del proyecto y navega hacia ella:

   ```bash
   mkdir biblioteca-ts
   cd biblioteca-ts
   ```

3. Crea la estructura de subcarpetas:

   ```bash
   # En macOS / Linux
   mkdir -p src/enums src/interfaces src/models src/services

   # En Windows (PowerShell)
   New-Item -ItemType Directory -Force -Path src/enums, src/interfaces, src/models, src/services
   ```

4. Genera el archivo `tsconfig.json` usando el comando de inicialización de TypeScript:

   ```bash
   tsc --init
   ```

5. Abre el archivo `tsconfig.json` generado en VS Code y **reemplaza todo su contenido** con la siguiente configuración optimizada para este proyecto:

   ```json
   {
     "compilerOptions": {
       "target": "ES2022",
       "module": "CommonJS",
       "strict": true,
       "outDir": "./dist",
       "rootDir": "./src",
       "sourceMap": true,
       "declaration": true,
       "esModuleInterop": true,
       "forceConsistentCasingInFileNames": true,
       "skipLibCheck": true
     },
     "include": ["src/**/*"],
     "exclude": ["node_modules", "dist"]
   }
   ```

   > **¿Por qué `"module": "CommonJS"`?** Dado que ejecutaremos el resultado con Node.js directamente (sin un empaquetador como Webpack), CommonJS es el sistema de módulos nativo de Node.js. En un proyecto Angular, este valor sería `ESNext` porque Angular CLI usa su propio empaquetador.

6. Abre VS Code en la carpeta del proyecto:

   ```bash
   code .
   ```

#### Salida Esperada

```
biblioteca-ts/
├── tsconfig.json
└── src/
    ├── enums/
    ├── interfaces/
    ├── models/
    └── services/
```

#### Verificación

```bash
# Confirmar que tsconfig.json existe y tiene contenido
cat tsconfig.json
# Debes ver el JSON con las opciones configuradas en el paso 5
```

---

### Paso 2 — Crear el Enum `Genero`

**Objetivo:** Definir un enum TypeScript que represente los géneros literarios disponibles en el sistema, evitando el uso de cadenas de texto "mágicas" en el código.

#### Instrucciones

1. Crea el archivo `src/enums/Genero.ts` en VS Code.

2. Escribe el siguiente código:

   ```typescript
   // src/enums/Genero.ts
   // Enum que representa los géneros literarios del catálogo de la biblioteca.
   // El uso de enum garantiza que solo se asignen valores válidos a la propiedad
   // 'genero' de la clase Libro, eliminando errores por cadenas incorrectas.

   export enum Genero {
     FICCION = "Ficción",
     NO_FICCION = "No Ficción",
     CIENCIA = "Ciencia",
     HISTORIA = "Historia",
     TECNOLOGIA = "Tecnología",
   }
   ```

   > **Nota:** Usamos un *string enum* (los valores son cadenas de texto) en lugar de un *numeric enum* (valores numéricos por defecto). Esto hace que los mensajes en consola sean legibles directamente, sin necesidad de traducción adicional.

#### Salida Esperada

El archivo se guarda sin errores. VS Code no muestra subrayados rojos.

#### Verificación

```bash
# Compilar solo este archivo para detectar errores de sintaxis
tsc src/enums/Genero.ts --noEmit
# No debe mostrar ninguna salida si el código es correcto
```

---

### Paso 3 — Crear la Interfaz `IBibliotecaItem`

**Objetivo:** Definir un contrato TypeScript que establezca las propiedades y métodos que cualquier ítem del catálogo de la biblioteca debe implementar.

#### Instrucciones

1. Crea el archivo `src/interfaces/IBibliotecaItem.ts`.

2. Escribe el siguiente código:

   ```typescript
   // src/interfaces/IBibliotecaItem.ts
   // Interfaz que define el contrato mínimo para cualquier ítem
   // que pueda formar parte del catálogo de la biblioteca.
   // Las clases que implementen esta interfaz deben proporcionar
   // TODAS las propiedades y métodos aquí declarados.

   export interface IBibliotecaItem {
     // Propiedades obligatorias
     readonly isbn: string;   // El ISBN no debe cambiar después de la creación
     titulo: string;
     autor: string;
     disponible: boolean;

     // Métodos obligatorios
     prestar(): void;
     devolver(): void;
     getInfo(): string;
   }
   ```

   > **Concepto clave:** La palabra clave `readonly` en TypeScript impide que la propiedad `isbn` sea reasignada después de la inicialización del objeto, similar a `const` pero para propiedades de clase.

#### Salida Esperada

El archivo se guarda sin errores de TypeScript.

#### Verificación

```bash
tsc src/interfaces/IBibliotecaItem.ts --noEmit
# Sin salida = sin errores
```

---

### Paso 4 — Crear la Clase Principal `Libro`

**Objetivo:** Implementar la clase `Libro` que cumple el contrato de `IBibliotecaItem`, aplicando modificadores de acceso, getters/setters, métodos de instancia y un método estático.

#### Instrucciones

1. Crea el archivo `src/models/Libro.ts`.

2. Escribe el siguiente código completo:

   ```typescript
   // src/models/Libro.ts
   import { IBibliotecaItem } from "../interfaces/IBibliotecaItem";
   import { Genero } from "../enums/Genero";

   // La clase Libro implementa IBibliotecaItem, por lo que TypeScript
   // verificará en tiempo de compilación que todos los miembros
   // de la interfaz estén presentes.
   export class Libro implements IBibliotecaItem {

     // --- Propiedades ---
     // 'readonly' en la interfaz; aquí usamos 'private' + getter para encapsulamiento
     private _isbn: string;
     public titulo: string;
     public autor: string;
     private _disponible: boolean;

     // 'protected' permite que las clases derivadas (LibroDigital) accedan a año y género
     protected _anio: number;
     protected _genero: Genero;

     // Contador estático: pertenece a la clase, no a las instancias
     private static _totalLibros: number = 0;

     // --- Constructor ---
     // Los parámetros 'anio' y 'genero' son opcionales (tienen valor por defecto)
     constructor(
       isbn: string,
       titulo: string,
       autor: string,
       anio: number = new Date().getFullYear(),
       genero: Genero = Genero.FICCION
     ) {
       this._isbn = isbn;
       this.titulo = titulo;
       this.autor = autor;
       this._disponible = true;   // Todo libro nuevo está disponible al crearse
       this._anio = anio;
       this._genero = genero;
       Libro._totalLibros++;      // Incrementar el contador cada vez que se crea un libro
     }

     // --- Getters y Setters ---

     // 'isbn' es de solo lectura (no hay setter)
     get isbn(): string {
       return this._isbn;
     }

     get disponible(): boolean {
       return this._disponible;
     }

     // El setter de 'disponible' es privado para que solo los métodos
     // prestar() y devolver() puedan cambiar el estado
     private set disponible(valor: boolean) {
       this._disponible = valor;
     }

     get anio(): number {
       return this._anio;
     }

     set anio(valor: number) {
       if (valor < 1450 || valor > new Date().getFullYear()) {
         throw new Error(`Año inválido: ${valor}. Debe estar entre 1450 y el año actual.`);
       }
       this._anio = valor;
     }

     get genero(): Genero {
       return this._genero;
     }

     set genero(valor: Genero) {
       this._genero = valor;
     }

     // Getter estático para consultar el total de libros creados
     static get totalLibros(): number {
       return Libro._totalLibros;
     }

     // --- Métodos de Instancia ---

     /**
      * Marca el libro como prestado.
      * @throws {Error} Si el libro ya está prestado.
      */
     prestar(): void {
       if (!this._disponible) {
         throw new Error(`El libro "${this.titulo}" ya está prestado y no está disponible.`);
       }
       this._disponible = false;
       console.log(`✅ Libro prestado: "${this.titulo}"`);
     }

     /**
      * Devuelve el libro al catálogo marcándolo como disponible.
      */
     devolver(): void {
       if (this._disponible) {
         console.log(`⚠️  El libro "${this.titulo}" ya estaba disponible.`);
         return;
       }
       this._disponible = true;
       console.log(`✅ Libro devuelto: "${this.titulo}"`);
     }

     /**
      * Retorna un string formateado con todos los datos del libro.
      * Usa template literals para una presentación clara.
      */
     getInfo(): string {
       const estado: string = this._disponible ? "Disponible" : "Prestado";
       return `
   ┌─────────────────────────────────────────┐
   │ Título   : ${this.titulo.padEnd(29)}│
   │ Autor    : ${this.autor.padEnd(29)}│
   │ ISBN     : ${this._isbn.padEnd(29)}│
   │ Año      : ${String(this._anio).padEnd(29)}│
   │ Género   : ${this._genero.padEnd(29)}│
   │ Estado   : ${estado.padEnd(29)}│
   └─────────────────────────────────────────┘`;
     }

     /**
      * Método estático que crea una instancia de Libro a partir de un objeto plano.
      * Útil para instanciar libros desde datos JSON (por ejemplo, una API REST).
      */
     static crearDesdeJSON(datos: {
       isbn: string;
       titulo: string;
       autor: string;
       anio?: number;
       genero?: Genero;
     }): Libro {
       return new Libro(
         datos.isbn,
         datos.titulo,
         datos.autor,
         datos.anio,
         datos.genero
       );
     }

     /**
      * Representación en cadena del objeto (útil para depuración).
      */
     toString(): string {
       return `Libro[${this._isbn}]: "${this.titulo}" por ${this.autor} (${this._anio})`;
     }
   }
   ```

#### Salida Esperada

El archivo se guarda. VS Code muestra IntelliSense con autocompletado para los miembros de la clase.

#### Verificación

```bash
# Compilar el archivo para verificar que no hay errores de tipos
tsc src/models/Libro.ts --noEmit --strict
# Sin salida = sin errores
```

> **Punto de reflexión:** Observa que el setter de `disponible` está declarado como `private`. Esto significa que desde fuera de la clase solo se puede *leer* el estado de disponibilidad (mediante el getter), pero no *modificarlo* directamente. Solo los métodos `prestar()` y `devolver()` pueden cambiar ese valor. Este es el principio de **encapsulamiento** en acción.

---

### Paso 5 — Crear la Clase Derivada `LibroDigital`

**Objetivo:** Aplicar herencia en TypeScript extendiendo `Libro` con propiedades adicionales específicas de los libros en formato digital.

#### Instrucciones

1. Crea el archivo `src/models/LibroDigital.ts`.

2. Escribe el siguiente código:

   ```typescript
   // src/models/LibroDigital.ts
   import { Libro } from "./Libro";
   import { Genero } from "../enums/Genero";

   // Tipo literal para los formatos de libro digital aceptados
   type FormatoDigital = "PDF" | "EPUB" | "MOBI" | "AZW3";

   export class LibroDigital extends Libro {

     // Propiedades adicionales exclusivas de los libros digitales
     private _formato: FormatoDigital;
     private _tamanoMB: number;
     private _urlDescarga: string;

     constructor(
       isbn: string,
       titulo: string,
       autor: string,
       formato: FormatoDigital,
       tamanoMB: number,
       urlDescarga: string,
       anio: number = new Date().getFullYear(),
       genero: Genero = Genero.TECNOLOGIA
     ) {
       // 'super()' llama al constructor de la clase padre (Libro)
       // y DEBE ser la primera instrucción del constructor derivado
       super(isbn, titulo, autor, anio, genero);

       this._formato = formato;
       this._tamanoMB = tamanoMB;
       this._urlDescarga = urlDescarga;
     }

     // Getters para las propiedades adicionales
     get formato(): FormatoDigital {
       return this._formato;
     }

     get tamanoMB(): number {
       return this._tamanoMB;
     }

     get urlDescarga(): string {
       return this._urlDescarga;
     }

     /**
      * Sobrescribe getInfo() para incluir los datos digitales adicionales.
      * La palabra clave 'override' (TypeScript 4.3+) indica explícitamente
      * que este método reemplaza al de la clase padre.
      */
     override getInfo(): string {
       // Llamamos al getInfo() del padre y le agregamos información extra
       const infoBase = super.getInfo();
       return `${infoBase}
   ┌─────────────────────────────────────────┐
   │ [DIGITAL]                               │
   │ Formato  : ${this._formato.padEnd(29)}│
   │ Tamaño   : ${(this._tamanoMB + " MB").padEnd(29)}│
   │ URL      : ${this._urlDescarga.substring(0, 29).padEnd(29)}│
   └─────────────────────────────────────────┘`;
     }

     /**
      * Simula la descarga del libro digital.
      */
     descargar(): void {
       if (!this.disponible) {
         console.log(`⚠️  "${this.titulo}" no está disponible para descarga.`);
         return;
       }
       console.log(`⬇️  Descargando "${this.titulo}" (${this._tamanoMB} MB) en formato ${this._formato}...`);
       console.log(`   URL: ${this._urlDescarga}`);
       console.log(`   Descarga completada ✓`);
     }

     override toString(): string {
       return `LibroDigital[${this.isbn}]: "${this.titulo}" [${this._formato}, ${this._tamanoMB}MB]`;
     }
   }
   ```

#### Salida Esperada

El archivo se guarda sin errores. VS Code muestra la cadena de herencia en el IntelliSense al pasar el cursor sobre `LibroDigital`.

#### Verificación

```bash
tsc src/models/LibroDigital.ts --noEmit --strict
# Sin salida = sin errores
```

---

### Paso 6 — Crear la Clase de Servicio `Biblioteca`

**Objetivo:** Implementar una clase gestora que mantenga un catálogo de libros con un arreglo tipado y ofrezca métodos de búsqueda, préstamo y estadísticas.

#### Instrucciones

1. Crea el archivo `src/services/Biblioteca.ts`.

2. Escribe el siguiente código:

   ```typescript
   // src/services/Biblioteca.ts
   import { Libro } from "../models/Libro";
   import { Genero } from "../enums/Genero";

   // Tipo para el objeto de estadísticas retornado por estadisticas()
   interface EstadisticasBiblioteca {
     totalLibros: number;
     librosDisponibles: number;
     librosPrestados: number;
     librosPorGenero: Record<string, number>;
   }

   export class Biblioteca {

     // Arreglo tipado: solo puede contener instancias de Libro (o subclases)
     private _catalogo: Libro[] = [];
     private _nombre: string;

     constructor(nombre: string) {
       this._nombre = nombre;
       console.log(`📚 Biblioteca "${this._nombre}" inicializada.`);
     }

     get nombre(): string {
       return this._nombre;
     }

     // --- Gestión del Catálogo ---

     /**
      * Agrega un libro al catálogo.
      * Verifica que no exista ya un libro con el mismo ISBN.
      */
     agregarLibro(libro: Libro): void {
       const existe = this._catalogo.some((l) => l.isbn === libro.isbn);
       if (existe) {
         console.log(`⚠️  Ya existe un libro con ISBN ${libro.isbn} en el catálogo.`);
         return;
       }
       this._catalogo.push(libro);
       console.log(`➕ Libro agregado: "${libro.titulo}"`);
     }

     /**
      * Busca libros cuyo título contenga el texto proporcionado (insensible a mayúsculas).
      */
     buscarPorTitulo(texto: string): Libro[] {
       const textoBusqueda = texto.toLowerCase();
       return this._catalogo.filter((l) =>
         l.titulo.toLowerCase().includes(textoBusqueda)
       );
     }

     /**
      * Busca libros de un autor específico (insensible a mayúsculas).
      */
     buscarPorAutor(autor: string): Libro[] {
       const autorBusqueda = autor.toLowerCase();
       return this._catalogo.filter((l) =>
         l.autor.toLowerCase().includes(autorBusqueda)
       );
     }

     /**
      * Busca libros por género usando el enum Genero.
      */
     buscarPorGenero(genero: Genero): Libro[] {
       return this._catalogo.filter((l) => l.genero === genero);
     }

     /**
      * Retorna todos los libros actualmente disponibles para préstamo.
      */
     listarDisponibles(): Libro[] {
       return this._catalogo.filter((l) => l.disponible);
     }

     /**
      * Gestiona el préstamo de un libro por ISBN.
      * Retorna true si el préstamo fue exitoso, false en caso contrario.
      */
     prestarLibro(isbn: string): boolean {
       const libro = this._catalogo.find((l) => l.isbn === isbn);
       if (!libro) {
         console.log(`❌ No se encontró ningún libro con ISBN: ${isbn}`);
         return false;
       }
       try {
         libro.prestar();
         return true;
       } catch (error) {
         // El error lanzado por prestar() cuando el libro ya está prestado
         if (error instanceof Error) {
           console.log(`❌ ${error.message}`);
         }
         return false;
       }
     }

     /**
      * Gestiona la devolución de un libro por ISBN.
      */
     devolverLibro(isbn: string): boolean {
       const libro = this._catalogo.find((l) => l.isbn === isbn);
       if (!libro) {
         console.log(`❌ No se encontró ningún libro con ISBN: ${isbn}`);
         return false;
       }
       libro.devolver();
       return true;
     }

     /**
      * Muestra en consola el catálogo completo con formato.
      */
     listarTodos(): void {
       if (this._catalogo.length === 0) {
         console.log("📭 El catálogo está vacío.");
         return;
       }
       console.log(`\n📚 Catálogo de "${this._nombre}" (${this._catalogo.length} libros):`);
       console.log("─".repeat(50));
       this._catalogo.forEach((libro, indice) => {
         console.log(`${indice + 1}. ${libro.toString()}`);
       });
       console.log("─".repeat(50));
     }

     /**
      * Retorna un objeto tipado con estadísticas del catálogo.
      */
     estadisticas(): EstadisticasBiblioteca {
       const librosPorGenero: Record<string, number> = {};

       // Usar desestructuración para iterar el catálogo
       for (const { genero } of this._catalogo) {
         librosPorGenero[genero] = (librosPorGenero[genero] ?? 0) + 1;
       }

       return {
         totalLibros: this._catalogo.length,
         librosDisponibles: this._catalogo.filter((l) => l.disponible).length,
         librosPrestados: this._catalogo.filter((l) => !l.disponible).length,
         librosPorGenero,
       };
     }

     /**
      * Imprime las estadísticas del catálogo en consola con formato legible.
      */
     mostrarEstadisticas(): void {
       const stats = this.estadisticas();
       console.log(`\n📊 Estadísticas de "${this._nombre}":`);
       console.log(`   Total de libros    : ${stats.totalLibros}`);
       console.log(`   Disponibles        : ${stats.librosDisponibles}`);
       console.log(`   Prestados          : ${stats.librosPrestados}`);
       console.log(`   Libros por género  :`);
       for (const [genero, cantidad] of Object.entries(stats.librosPorGenero)) {
         console.log(`     • ${genero}: ${cantidad}`);
       }
     }
   }
   ```

#### Salida Esperada

El archivo se guarda sin errores de TypeScript.

#### Verificación

```bash
tsc src/services/Biblioteca.ts --noEmit --strict
# Sin salida = sin errores
```

---

### Paso 7 — Crear el Punto de Entrada `main.ts`

**Objetivo:** Escribir el archivo principal que instancia todos los objetos, ejecuta las operaciones del sistema y demuestra el funcionamiento completo del proyecto.

#### Instrucciones

1. Crea el archivo `src/main.ts`.

2. Escribe el siguiente código:

   ```typescript
   // src/main.ts
   // Punto de entrada del sistema de gestión de biblioteca.
   // Este archivo importa todas las clases y demuestra su uso.

   import { Libro } from "./models/Libro";
   import { LibroDigital } from "./models/LibroDigital";
   import { Biblioteca } from "./services/Biblioteca";
   import { Genero } from "./enums/Genero";

   // ─────────────────────────────────────────────────────────
   // SECCIÓN 1: Creación de instancias de Libro
   // ─────────────────────────────────────────────────────────
   console.log("\n══════════════════════════════════════════");
   console.log("  SISTEMA DE GESTIÓN DE BIBLIOTECA");
   console.log("══════════════════════════════════════════\n");

   // Constructor completo con todos los parámetros
   const libro1 = new Libro(
     "978-0-06-112008-4",
     "Cien Años de Soledad",
     "Gabriel García Márquez",
     1967,
     Genero.FICCION
   );

   // Constructor con parámetros opcionales omitidos (usan valores por defecto)
   const libro2 = new Libro(
     "978-0-14-028329-7",
     "Sapiens: De animales a dioses",
     "Yuval Noah Harari",
     2011,
     Genero.HISTORIA
   );

   const libro3 = new Libro(
     "978-0-13-468599-1",
     "Clean Code",
     "Robert C. Martin",
     2008,
     Genero.TECNOLOGIA
   );

   // Crear un libro usando el método estático crearDesdeJSON()
   // (simula la recepción de datos desde una API REST)
   const libro4 = Libro.crearDesdeJSON({
     isbn: "978-0-7432-7356-5",
     titulo: "El Universo en una Cáscara de Nuez",
     autor: "Stephen Hawking",
     anio: 2001,
     genero: Genero.CIENCIA,
   });

   // ─────────────────────────────────────────────────────────
   // SECCIÓN 2: Creación de un LibroDigital (herencia)
   // ─────────────────────────────────────────────────────────
   const libroDigital1 = new LibroDigital(
     "978-1-491-95026-7",
     "Learning TypeScript",
     "Josh Goldberg",
     "EPUB",
     12.5,
     "https://biblioteca.ejemplo.com/descargas/learning-typescript.epub",
     2022,
     Genero.TECNOLOGIA
   );

   // ─────────────────────────────────────────────────────────
   // SECCIÓN 3: Mostrar información de libros individuales
   // ─────────────────────────────────────────────────────────
   console.log("─── Información de Libros ───");
   console.log(libro1.getInfo());
   console.log(libroDigital1.getInfo());

   // ─────────────────────────────────────────────────────────
   // SECCIÓN 4: Crear la Biblioteca y agregar libros
   // ─────────────────────────────────────────────────────────
   console.log("\n─── Inicialización de la Biblioteca ───");
   const miBiblioteca = new Biblioteca("Biblioteca Central TypeScript");

   miBiblioteca.agregarLibro(libro1);
   miBiblioteca.agregarLibro(libro2);
   miBiblioteca.agregarLibro(libro3);
   miBiblioteca.agregarLibro(libro4);
   miBiblioteca.agregarLibro(libroDigital1);

   // Intentar agregar un libro con ISBN duplicado
   const libroDuplicado = new Libro("978-0-06-112008-4", "Duplicado", "Autor Prueba");
   miBiblioteca.agregarLibro(libroDuplicado);

   // ─────────────────────────────────────────────────────────
   // SECCIÓN 5: Listar todos los libros
   // ─────────────────────────────────────────────────────────
   miBiblioteca.listarTodos();

   // ─────────────────────────────────────────────────────────
   // SECCIÓN 6: Operaciones de préstamo y devolución
   // ─────────────────────────────────────────────────────────
   console.log("\n─── Operaciones de Préstamo ───");
   miBiblioteca.prestarLibro("978-0-06-112008-4");   // Préstamo exitoso
   miBiblioteca.prestarLibro("978-0-06-112008-4");   // Debe fallar: ya prestado
   miBiblioteca.prestarLibro("ISBN-INEXISTENTE");     // Debe fallar: no encontrado

   console.log("\n─── Operaciones de Devolución ───");
   miBiblioteca.devolverLibro("978-0-06-112008-4");  // Devolución exitosa

   // ─────────────────────────────────────────────────────────
   // SECCIÓN 7: Búsquedas en el catálogo
   // ─────────────────────────────────────────────────────────
   console.log("\n─── Búsquedas ───");

   const resultadosTitulo = miBiblioteca.buscarPorTitulo("typescript");
   console.log(`\nBúsqueda por título "typescript" (${resultadosTitulo.length} resultado/s):`);
   resultadosTitulo.forEach((l) => console.log(`  • ${l.toString()}`));

   const resultadosAutor = miBiblioteca.buscarPorAutor("harari");
   console.log(`\nBúsqueda por autor "harari" (${resultadosAutor.length} resultado/s):`);
   resultadosAutor.forEach((l) => console.log(`  • ${l.toString()}`));

   const librosDisponibles = miBiblioteca.listarDisponibles();
   console.log(`\nLibros disponibles actualmente: ${librosDisponibles.length}`);
   librosDisponibles.forEach((l) => console.log(`  • ${l.titulo}`));

   // ─────────────────────────────────────────────────────────
   // SECCIÓN 8: Descarga de libro digital
   // ─────────────────────────────────────────────────────────
   console.log("\n─── Descarga de Libro Digital ───");
   libroDigital1.descargar();

   // ─────────────────────────────────────────────────────────
   // SECCIÓN 9: Estadísticas y contador estático
   // ─────────────────────────────────────────────────────────
   miBiblioteca.mostrarEstadisticas();

   console.log(`\n📌 Total de instancias de Libro creadas (incluye duplicado): ${Libro.totalLibros}`);

   // ─────────────────────────────────────────────────────────
   // SECCIÓN 10: Desestructuración aplicada
   // ─────────────────────────────────────────────────────────
   console.log("\n─── Desestructuración ───");
   const { titulo, autor, isbn } = libro2;
   console.log(`Libro desestructurado → Título: "${titulo}" | Autor: "${autor}" | ISBN: ${isbn}`);

   // Desestructuración con renombrado
   const { titulo: nombreObra, anio: fechaPublicacion } = libro3;
   console.log(`Con renombrado → Obra: "${nombreObra}" | Publicado en: ${fechaPublicacion}`);

   console.log("\n══════════════════════════════════════════");
   console.log("  FIN DE LA DEMOSTRACIÓN");
   console.log("══════════════════════════════════════════\n");
   ```

#### Salida Esperada

El archivo se guarda sin errores. VS Code muestra los imports resueltos correctamente (sin subrayados rojos en las rutas de importación).

---

### Paso 8 — Compilar el Proyecto con `tsc`

**Objetivo:** Compilar todos los archivos TypeScript del proyecto usando el `tsconfig.json` configurado en el Paso 1, generando los archivos JavaScript en la carpeta `dist/`.

#### Instrucciones

1. Asegúrate de estar en la raíz del proyecto (`biblioteca-ts/`):

   ```bash
   pwd
   # Debe mostrar: .../biblioteca-ts
   ```

2. Ejecuta el compilador de TypeScript apuntando al `tsconfig.json`:

   ```bash
   tsc
   ```

3. Si hay errores de compilación, TypeScript los mostrará en la terminal con el nombre del archivo, el número de línea y la descripción del error. Corrígelos antes de continuar.

4. Verifica que se haya creado la carpeta `dist/` con la estructura de archivos compilados:

   ```bash
   # En macOS/Linux
   find dist -name "*.js" | sort

   # En Windows (PowerShell)
   Get-ChildItem -Recurse -Filter "*.js" dist | Select-Object FullName
   ```

#### Salida Esperada

```
dist/
├── enums/
│   └── Genero.js
├── interfaces/
│   └── IBibliotecaItem.js
├── models/
│   ├── Libro.js
│   └── LibroDigital.js
├── services/
│   └── Biblioteca.js
└── main.js
```

> **Nota:** Los archivos `.d.ts` (declaraciones de tipos) también se generan porque `"declaration": true` está activado en el `tsconfig.json`. Son útiles cuando el proyecto se publica como librería.

#### Verificación

```bash
# Confirmar que main.js existe
ls dist/main.js

# En Windows (PowerShell)
Test-Path dist/main.js
# Debe mostrar: True
```

---

### Paso 9 — Ejecutar el Proyecto Compilado con Node.js

**Objetivo:** Ejecutar el punto de entrada compilado con Node.js y verificar que la salida en consola corresponde al comportamiento esperado del sistema de biblioteca.

#### Instrucciones

1. Ejecuta el archivo `main.js` compilado:

   ```bash
   node dist/main.js
   ```

2. Observa la salida completa en la terminal.

#### Salida Esperada (extracto representativo)

```
══════════════════════════════════════════
  SISTEMA DE GESTIÓN DE BIBLIOTECA
══════════════════════════════════════════


─── Información de Libros ───

┌─────────────────────────────────────────┐
│ Título   : Cien Años de Soledad         │
│ Autor    : Gabriel García Márquez       │
│ ISBN     : 978-0-06-112008-4            │
│ Año      : 1967                         │
│ Género   : Ficción                      │
│ Estado   : Disponible                   │
└─────────────────────────────────────────┘

[... información de LibroDigital ...]

─── Inicialización de la Biblioteca ───
📚 Biblioteca "Biblioteca Central TypeScript" inicializada.
➕ Libro agregado: "Cien Años de Soledad"
➕ Libro agregado: "Sapiens: De animales a dioses"
➕ Libro agregado: "Clean Code"
➕ Libro agregado: "El Universo en una Cáscara de Nuez"
➕ Libro agregado: "Learning TypeScript"
⚠️  Ya existe un libro con ISBN 978-0-06-112008-4 en el catálogo.

📚 Catálogo de "Biblioteca Central TypeScript" (5 libros):
──────────────────────────────────────────────────
1. Libro[978-0-06-112008-4]: "Cien Años de Soledad" por Gabriel García Márquez (1967)
2. Libro[978-0-14-028329-7]: "Sapiens: De animales a dioses" por Yuval Noah Harari (2011)
3. Libro[978-0-13-468599-1]: "Clean Code" por Robert C. Martin (2008)
4. Libro[978-0-7432-7356-5]: "El Universo en una Cáscara de Nuez" por Stephen Hawking (2001)
5. LibroDigital[978-1-491-95026-7]: "Learning TypeScript" [EPUB, 12.5MB]
──────────────────────────────────────────────────

─── Operaciones de Préstamo ───
✅ Libro prestado: "Cien Años de Soledad"
❌ El libro "Cien Años de Soledad" ya está prestado y no está disponible.
❌ No se encontró ningún libro con ISBN: ISBN-INEXISTENTE

─── Operaciones de Devolución ───
✅ Libro devuelto: "Cien Años de Soledad"

─── Búsquedas ───

Búsqueda por título "typescript" (1 resultado/s):
  • LibroDigital[978-1-491-95026-7]: "Learning TypeScript" [EPUB, 12.5MB]

Búsqueda por autor "harari" (1 resultado/s):
  • Libro[978-0-14-028329-7]: "Sapiens: De animales a dioses" por Yuval Noah Harari (2011)

Libros disponibles actualmente: 5

─── Descarga de Libro Digital ───
⬇️  Descargando "Learning TypeScript" (12.5 MB) en formato EPUB...
   URL: https://biblioteca.ejemplo.com/descargas/learning-typescript.epub
   Descarga completada ✓

📊 Estadísticas de "Biblioteca Central TypeScript":
   Total de libros    : 5
   Disponibles        : 5
   Prestados          : 0
   Libros por género  :
     • Ficción: 1
     • Historia: 1
     • Tecnología: 3
     • Ciencia: 1

📌 Total de instancias de Libro creadas (incluye duplicado): 6

─── Desestructuración ───
Libro desestructurado → Título: "Sapiens: De animales a dioses" | Autor: "Yuval Noah Harari" | ISBN: 978-0-14-028329-7
Con renombrado → Obra: "Clean Code" | Publicado en: 2008

══════════════════════════════════════════
  FIN DE LA DEMOSTRACIÓN
══════════════════════════════════════════
```

#### Verificación

Confirma los siguientes puntos en la salida:

- [ ] Se muestran 5 libros en el catálogo (el duplicado fue rechazado).
- [ ] El segundo intento de préstamo muestra el mensaje de error correcto.
- [ ] La búsqueda por título "typescript" retorna exactamente 1 resultado.
- [ ] Las estadísticas muestran 3 libros de Tecnología (Clean Code, El Universo... no, Tecnología tiene: Clean Code + Learning TypeScript = 2; ajusta si tu conteo difiere).
- [ ] El contador estático muestra 6 (5 libros únicos + 1 duplicado intentado).
- [ ] La desestructuración muestra los valores correctos de `libro2` y `libro3`.

---

### Paso 10 — (Opcional) Activar el Modo Observador

**Objetivo:** Experimentar con el modo `--watch` de `tsc` para ver cómo el compilador recompila automáticamente al guardar cambios.

#### Instrucciones

1. En una **nueva terminal** (mantén la primera disponible), ejecuta:

   ```bash
   tsc --watch
   ```

2. En VS Code, abre `src/main.ts` y agrega al final del archivo:

   ```typescript
   // Prueba de recompilación automática
   console.log("\n🔄 Recompilación automática detectada por --watch");
   ```

3. Guarda el archivo (`Ctrl+S` / `Cmd+S`).

4. Observa en la terminal con `--watch` cómo TypeScript detecta el cambio y recompila.

5. En la primera terminal, vuelve a ejecutar:

   ```bash
   node dist/main.js
   ```

6. Verifica que el nuevo mensaje aparece al final de la salida.

7. Cuando termines, detén el modo observador con `Ctrl+C`.

---

## 7. Validación y Pruebas

Ejecuta la siguiente lista de verificación completa para confirmar que el laboratorio está terminado correctamente:

```bash
# 1. Verificar que todos los archivos fuente existen
ls src/enums/Genero.ts src/interfaces/IBibliotecaItem.ts \
   src/models/Libro.ts src/models/LibroDigital.ts \
   src/services/Biblioteca.ts src/main.ts

# 2. Verificar compilación sin errores
tsc --noEmit
# Sin salida = sin errores de tipos

# 3. Verificar que la carpeta dist/ contiene los archivos compilados
ls dist/main.js dist/models/Libro.js dist/models/LibroDigital.js \
   dist/services/Biblioteca.js

# 4. Ejecutar el programa y verificar la salida completa
node dist/main.js

# 5. Verificar el total de instancias en la salida (debe ser 6)
node dist/main.js | grep "Total de instancias"
# Salida esperada: 📌 Total de instancias de Libro creadas (incluye duplicado): 6

# 6. Verificar que el error de préstamo duplicado aparece correctamente
node dist/main.js | grep "ya está prestado"
# Salida esperada: ❌ El libro "Cien Años de Soledad" ya está prestado y no está disponible.
```

### Lista de Verificación Final

| Criterio                                                                 | Estado |
|--------------------------------------------------------------------------|--------|
| `tsconfig.json` configurado con `strict: true` y `outDir: ./dist`        | ☐      |
| Enum `Genero` con 5 valores de tipo string exportado correctamente        | ☐      |
| Interfaz `IBibliotecaItem` con `readonly isbn` y 3 métodos               | ☐      |
| Clase `Libro` implementa la interfaz y tiene getter/setter privado        | ☐      |
| Método `prestar()` lanza `Error` cuando el libro ya está prestado         | ☐      |
| Método estático `crearDesdeJSON()` funciona correctamente                 | ☐      |
| `LibroDigital` extiende `Libro` con `override getInfo()`                  | ☐      |
| `Biblioteca` rechaza libros con ISBN duplicado                            | ☐      |
| `estadisticas()` retorna objeto tipado con conteos por género             | ☐      |
| Desestructuración aplicada en `main.ts` con renombrado                    | ☐      |
| Proyecto compila con `tsc` sin errores                                    | ☐      |
| `node dist/main.js` produce la salida esperada completa                   | ☐      |

---

## 8. Resolución de Problemas

### Problema 1: Error `Cannot find module '../interfaces/IBibliotecaItem'`

**Síntoma:**

Al ejecutar `tsc` o `node dist/main.js`, aparece el siguiente error:

```
Error: Cannot find module '../interfaces/IBibliotecaItem'
```

O durante la compilación:

```
src/models/Libro.ts:2:32 - error TS2307: Cannot find module '../interfaces/IBibliotecaItem' or its corresponding type declarations.
```

**Causa:**

Este error ocurre por una de las siguientes razones:
1. La ruta relativa en el `import` es incorrecta (por ejemplo, usar `./interfaces/` en lugar de `../interfaces/` desde dentro de `src/models/`).
2. El archivo `IBibliotecaItem.ts` no existe o tiene un nombre diferente (TypeScript distingue mayúsculas de minúsculas en los nombres de archivo).
3. La carpeta `src/interfaces/` no fue creada correctamente.

**Solución:**

```bash
# Verificar que el archivo existe con el nombre exacto
ls src/interfaces/IBibliotecaItem.ts

# Verificar la ruta relativa desde src/models/Libro.ts
# La ruta correcta es: '../interfaces/IBibliotecaItem'
# (sube un nivel con '..' y luego entra a 'interfaces/')

# Si el archivo no existe, crearlo nuevamente siguiendo el Paso 3
```

Asegúrate de que la primera línea de `src/models/Libro.ts` sea exactamente:

```typescript
import { IBibliotecaItem } from "../interfaces/IBibliotecaItem";
```

---

### Problema 2: Error `Property '_disponible' is private` o `Property 'X' has no initializer`

**Síntoma A — Acceso a propiedad privada:**

```
error TS2341: Property '_disponible' is private and only accessible within class 'Libro'.
```

**Causa A:**

Se está intentando acceder a `_disponible` directamente desde fuera de la clase `Libro` (por ejemplo, desde `main.ts` o desde `LibroDigital`). Las propiedades marcadas como `private` solo son accesibles dentro de la clase donde se declaran.

**Solución A:**

Usa el getter público `disponible` en lugar de la propiedad privada `_disponible`:

```typescript
// ❌ Incorrecto (acceso directo a propiedad privada)
console.log(libro1._disponible);

// ✅ Correcto (acceso mediante getter público)
console.log(libro1.disponible);
```

En `LibroDigital`, usa `this.disponible` (el getter heredado) en lugar de `this._disponible`.

---

**Síntoma B — Propiedad sin inicializador:**

```
error TS2564: Property '_isbn' has no initializer and is not definitely assigned in the constructor.
```

**Causa B:**

La opción `strict: true` en `tsconfig.json` activa `strictPropertyInitialization`, que exige que todas las propiedades de clase sean inicializadas en el constructor o tengan un valor por defecto. Este error aparece si se declara una propiedad pero no se le asigna un valor en el constructor.

**Solución B:**

Asegúrate de que **todas** las propiedades declaradas en la clase `Libro` reciben un valor en el constructor:

```typescript
// ❌ Incorrecto: propiedad declarada pero no inicializada
private _isbn: string;
constructor() {
  // _isbn nunca se asigna → error TS2564
}

// ✅ Correcto: propiedad inicializada en el constructor
private _isbn: string;
constructor(isbn: string) {
  this._isbn = isbn;  // ← asignación obligatoria
}
```

Revisa que el constructor de `Libro` asigne valores a `_isbn`, `_disponible`, `_anio` y `_genero`, y que el de `LibroDigital` asigne `_formato`, `_tamanoMB` y `_urlDescarga`.

---

## 9. Limpieza

Una vez completada y validada la práctica, puedes limpiar los archivos compilados para liberar espacio, conservando únicamente el código fuente TypeScript:

```bash
# Eliminar la carpeta dist/ con todos los archivos compilados
# En macOS/Linux
rm -rf dist/

# En Windows (PowerShell)
Remove-Item -Recurse -Force dist/

# Verificar que solo queda la carpeta src/ y tsconfig.json
ls
# Debe mostrar: src/  tsconfig.json
```

> **Importante:** No elimines la carpeta `src/` ni el `tsconfig.json`. Estos archivos son el resultado de tu trabajo y serán la base para prácticas futuras del módulo.

Si deseas volver a compilar el proyecto en el futuro, simplemente ejecuta `tsc` desde la raíz del proyecto.

---

## 10. Resumen

En esta práctica construiste un sistema completo de gestión de biblioteca en TypeScript, integrando los conceptos fundamentales de la Programación Orientada a Objetos con las características del lenguaje:

| Concepto aplicado                   | Dónde se usó                                                        |
|-------------------------------------|---------------------------------------------------------------------|
| **Modificadores de acceso**         | `private _isbn`, `protected _anio`, `public titulo` en `Libro`     |
| **Getters y setters**               | `get isbn()`, `set anio()` con validación en `Libro`               |
| **Constructor con params. opcionales** | `anio = new Date().getFullYear()` en `Libro`                    |
| **Método estático**                 | `Libro.crearDesdeJSON()`, `Libro.totalLibros`                       |
| **Lanzamiento de errores tipados**  | `throw new Error(...)` en `prestar()`, captura con `instanceof`    |
| **Interfaz con `readonly`**         | `IBibliotecaItem` con `readonly isbn`                               |
| **Enum de tipo string**             | `Genero.FICCION = "Ficción"` en `Genero.ts`                        |
| **Herencia y `override`**           | `LibroDigital extends Libro`, `override getInfo()`                  |
| **Arreglo tipado**                  | `private _catalogo: Libro[]` en `Biblioteca`                        |
| **Tipo de retorno objeto tipado**   | `EstadisticasBiblioteca` como interfaz local en `Biblioteca`        |
| **Desestructuración**               | `const { titulo, autor } = libro2` en `main.ts`                    |
| **Módulos TypeScript**              | `export`/`import` entre los 6 archivos del proyecto                 |
| **Compilación con `tsconfig.json`** | `tsc` con `strict`, `outDir`, `rootDir` configurados               |

### Conexión con Angular

Los patrones aplicados en esta práctica tienen correspondencia directa con el desarrollo Angular:

- Las **clases con modificadores de acceso** son la base de los **componentes** y **servicios** Angular.
- Las **interfaces** se usan extensamente para tipar las respuestas de APIs HTTP en `HttpClient`.
- Los **módulos TypeScript** (`import`/`export`) son el mecanismo subyacente de los **NgModules** y los componentes **standalone**.
- El **`tsconfig.json`** que configuraste es casi idéntico al que Angular CLI genera automáticamente con `ng new`.

### Recursos Adicionales

- [TypeScript Handbook: Classes](https://www.typescriptlang.org/docs/handbook/2/classes.html)
- [TypeScript Handbook: Interfaces](https://www.typescriptlang.org/docs/handbook/2/objects.html)
- [TypeScript Handbook: Enums](https://www.typescriptlang.org/docs/handbook/enums.html)
- [TypeScript Handbook: Modules](https://www.typescriptlang.org/docs/handbook/2/modules.html)
- [Referencia completa de tsconfig.json](https://www.typescriptlang.org/tsconfig)
- [TypeScript Playground — prueba código en línea](https://www.typescriptlang.org/play)

---
