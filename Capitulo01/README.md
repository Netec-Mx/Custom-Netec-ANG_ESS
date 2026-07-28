# Investigación sobre Angular

## Metadatos

| Campo | Detalle |
|---|---|
| **Duración estimada** | 48 minutos |
| **Complejidad** | Fácil |
| **Nivel Bloom** | Aplicar (Apply) |
| **Módulo** | Capítulo 1 — Introducción a Angular |
| **Modalidad** | Investigación guiada (sin escritura de código) |

---

## Descripción General

En esta práctica realizarás una investigación guiada y sistemática sobre el ecosistema de Angular, explorando su historia, arquitectura conceptual, posicionamiento frente a otros frameworks y los recursos disponibles para la comunidad. Utilizarás fuentes oficiales y herramientas de análisis de tendencias para construir un mapa mental completo del framework antes de comenzar a escribir código. Al finalizar, habrás producido un informe estructurado que consolidará tus hallazgos y servirá como referencia personal a lo largo del curso.

---

## Objetivos de Aprendizaje

Al completar esta práctica serás capaz de:

- [ ] Construir una línea de tiempo documentada de la evolución de Angular desde AngularJS 1.x hasta Angular 17+, identificando los cambios arquitectónicos más relevantes entre versiones.
- [ ] Elaborar una tabla comparativa fundamentada entre Angular, React y Vue.js, analizando dimensiones como curva de aprendizaje, ecosistema, rendimiento y soporte empresarial.
- [ ] Identificar y catalogar los recursos oficiales de documentación, comunidades y foros de soporte disponibles para desarrolladores Angular.
- [ ] Explicar cómo el patrón arquitectónico MVC/MVVM se manifiesta en los conceptos fundamentales de Angular (componentes, servicios y módulos).
- [ ] Documentar al menos cinco empresas reconocidas que utilizan Angular en producción, describiendo sus casos de uso específicos.

---

## Prerrequisitos

### Conocimientos Previos

| Área | Nivel Requerido | Descripción |
|---|---|---|
| HTML y CSS | Básico | Comprender la estructura de páginas web y el propósito de los templates |
| JavaScript | Básico | Contextualizar las mejoras que TypeScript aporta sobre JS |
| Lectura técnica en inglés | Básico-Intermedio | La mayoría de la documentación oficial está en inglés |
| Navegación web | Básico | Capacidad de explorar documentación, repositorios GitHub y encuestas en línea |

### Acceso Requerido

| Recurso | URL | Propósito |
|---|---|---|
| Documentación oficial Angular | https://angular.dev | Fuente primaria de investigación |
| Repositorio GitHub de Angular | https://github.com/angular/angular | Historial de versiones y changelogs |
| Blog oficial de Angular | https://blog.angular.dev | Anuncios y artículos del equipo de Angular |
| npm trends | https://npmtrends.com | Comparación de descargas entre frameworks |
| Stack Overflow Developer Survey | https://survey.stackoverflow.co | Datos de adopción y popularidad |
| State of JS | https://stateofjs.com | Encuesta anual del ecosistema JavaScript |

> **Nota:** Esta práctica requiere conexión a Internet estable (mínimo 10 Mbps) para acceder a todas las fuentes de investigación. No se requiere instalación de software adicional más allá de un navegador web moderno.

---

## Entorno de Laboratorio

### Requisitos de Hardware

| Componente | Mínimo | Recomendado |
|---|---|---|
| RAM | 4 GB | 8 GB |
| Almacenamiento libre | 500 MB (para guardar el informe) | 1 GB |
| Resolución de pantalla | 1280×768 | 1920×1080 |
| Conexión a Internet | 5 Mbps | 10 Mbps o superior |

### Requisitos de Software

| Software | Versión | Propósito |
|---|---|---|
| Google Chrome | 120.x o superior | Navegación y acceso a fuentes de investigación |
| Editor de texto / Word Processor | Cualquiera (VS Code, Word, Google Docs, Notion) | Redacción del informe de investigación |
| Angular DevTools (extensión Chrome) | Última disponible | Exploración opcional de sitios construidos con Angular |

### Configuración del Entorno de Trabajo

Antes de comenzar la investigación, prepara tu espacio de trabajo siguiendo estos pasos:

**1. Organiza las pestañas del navegador**

Abre Google Chrome y crea un grupo de pestañas para esta práctica. Abre las siguientes URLs en pestañas separadas:

```
Pestaña 1: https://angular.dev/overview
Pestaña 2: https://github.com/angular/angular/releases
Pestaña 3: https://blog.angular.dev
Pestaña 4: https://npmtrends.com/@angular/core,react,vue
Pestaña 5: https://survey.stackoverflow.co/2023
Pestaña 6: https://2022.stateofjs.com/en-US/libraries/front-end-frameworks/
```

**2. Prepara el documento de informe**

Crea un nuevo documento en tu editor preferido con la siguiente estructura base (puedes copiar y pegar este esquema):

```
# Informe de Investigación: Ecosistema Angular
## Estudiante: [Tu nombre]
## Fecha: [Fecha actual]
## Curso: Desarrollo con Angular

---
## Sección 1: Historia y Evolución de Angular
## Sección 2: Arquitectura y Patrón MVC/MVVM
## Sección 3: Comparativa Angular vs React vs Vue.js
## Sección 4: Recursos y Comunidad
## Sección 5: Empresas que Usan Angular en Producción
## Sección 6: Conclusiones Personales
```

**3. Instala Angular DevTools (opcional pero recomendado)**

```
URL de instalación: https://chrome.google.com/webstore/detail/angular-devtools/ienfalfjdbdpebioblfackkekamfmbnh
```

Esta extensión te permitirá detectar visualmente cuando un sitio web está construido con Angular durante tu investigación.

---

## Pasos del Laboratorio

---

### Paso 1: Exploración de la Documentación Oficial y Visión General del Framework

**Objetivo:** Familiarizarse con la documentación oficial de Angular en `angular.dev` y extraer información fundamental sobre qué es Angular, su propósito y sus características principales.

**Duración estimada:** 8 minutos

#### Instrucciones

1. Navega a **https://angular.dev/overview** en tu navegador.

2. Lee la sección de introducción completa. Presta especial atención a cómo el equipo de Angular define el framework. Busca respuesta a las siguientes preguntas mientras lees:
   - ¿Cómo define Angular oficialmente su propósito?
   - ¿Qué tipos de aplicaciones menciona como casos de uso (SPA, PWA, SSR)?
   - ¿Qué lenguaje de programación utiliza como base?

3. En la barra de navegación lateral izquierda de `angular.dev`, explora las siguientes secciones y toma notas breves de cada una:
   - **"What is Angular?"** (o equivalente en la versión actual del sitio)
   - **"Components"** — Observa la definición oficial de componente
   - **"Templates"** — Revisa cómo se describe el sistema de plantillas
   - **"Dependency Injection"** — Lee el párrafo introductorio

4. En tu documento de informe, bajo la **Sección 1**, registra:
   - Una definición propia de Angular (con tus palabras, basada en lo leído)
   - Los tres tipos de aplicaciones que Angular permite construir
   - Los seis conceptos fundamentales listados en la tabla de la lección (Componente, Módulo, Servicio, Directiva, Pipe, Router) con la definición oficial que encuentres en la documentación

5. Navega a **https://github.com/angular/angular** y observa:
   - El número de estrellas (stars) del repositorio
   - El número de contribuidores
   - El número de issues abiertos
   - La fecha del último commit en la rama principal

   Registra estos datos en tu informe como indicadores de la actividad y salud del proyecto.

#### Resultado Esperado

Al finalizar este paso, tu informe debe contener:
- Una definición propia de Angular (mínimo 3 oraciones)
- Una tabla con los 6 conceptos fundamentales y sus definiciones
- Los datos estadísticos del repositorio de GitHub

#### Verificación

Responde mentalmente (o por escrito en tu informe) las siguientes preguntas de verificación:

- ✅ ¿Puedo explicar en mis propias palabras qué es Angular sin leer la documentación?
- ✅ ¿Conozco la diferencia entre Angular como "plataforma" vs una "biblioteca"?
- ✅ ¿Tengo registrados los datos de actividad del repositorio de GitHub?

---

### Paso 2: Línea de Tiempo — Historia y Evolución de Angular

**Objetivo:** Construir una línea de tiempo documentada de la evolución de Angular, identificando los hitos arquitectónicos más importantes desde AngularJS hasta Angular 17+.

**Duración estimada:** 12 minutos

#### Instrucciones

1. Navega a **https://github.com/angular/angular/releases** para explorar el historial oficial de versiones. Observa la frecuencia de lanzamientos y los títulos de los changelogs.

2. Complementa con la siguiente información de referencia (verificable en las fuentes indicadas) para construir tu línea de tiempo:

   | Año | Versión / Hito | Cambio Arquitectónico Clave |
   |---|---|---|
   | 2010 | AngularJS 1.0 (alpha) | Primer framework MVC de Google; data binding bidireccional; directivas |
   | 2012 | AngularJS 1.0 (release) | Lanzamiento oficial; adopción masiva en la industria |
   | 2014 | Anuncio de Angular 2 | Reescritura completa; abandono de AngularJS; TypeScript como base |
   | 2016 | Angular 2.0 (release) | Arquitectura basada en componentes; inyección de dependencias renovada |
   | 2016 | Angular 4.0 | (Saltó la versión 3 para alinear versiones internas); mejoras de rendimiento |
   | 2017 | Angular 5.0 | Build optimizer; Progressive Web Apps; HttpClient nuevo |
   | 2018 | Angular 6.0 | Angular Elements; CLI Workspaces; ng update / ng add |
   | 2018 | Angular 7.0 | Virtual scrolling; drag and drop; mejoras de CLI |
   | 2019 | Angular 8.0 | Ivy renderer (opt-in); differential loading; lazy loading con import() |
   | 2020 | Angular 9.0 | Ivy por defecto; mejoras de bundle size y tiempo de compilación |
   | 2020 | Angular 10.0 | Warnings de dependencias; modo strict por defecto |
   | 2021 | Angular 12.0 | View Engine deprecado; Webpack 5; Nullish coalescing en templates |
   | 2022 | Angular 14.0 | Standalone components (preview); typed forms; CLI autocompletion |
   | 2022 | Angular 15.0 | Standalone components estables; directive composition API |
   | 2023 | Angular 16.0 | Signals (developer preview); hydration; esbuild support |
   | 2023 | Angular 17.0 | Signals estables; nueva sintaxis @if/@for/@switch; standalone por defecto; nuevo sitio angular.dev |

3. Navega a **https://blog.angular.dev** y busca los artículos de anuncio de Angular 16 y Angular 17. Lee los títulos y los primeros párrafos para identificar cuáles fueron los cambios que el equipo de Angular destacó como más importantes.

4. En tu documento de informe, bajo la **Sección 1**, construye la línea de tiempo con la tabla anterior. Agrega una columna adicional con tu interpretación personal del impacto de cada cambio (usa: Alto / Medio / Bajo).

5. Responde las siguientes preguntas en tu informe como análisis de la línea de tiempo:

   **Pregunta A:** ¿Por qué el equipo de Angular decidió reescribir completamente el framework entre AngularJS y Angular 2? (Busca en el blog oficial o en artículos de referencia)

   **Pregunta B:** ¿Qué es el renderizador Ivy y por qué su introducción en Angular 9 fue un hito importante?

   **Pregunta C:** ¿Qué son los "Signals" introducidos en Angular 16-17 y qué problema intentan resolver?

   > **Pista para la Pregunta C:** Busca en `angular.dev/guide/signals` la descripción oficial de Signals y su relación con la reactividad.

6. Identifica y registra el **patrón de versionado semántico** que Angular utiliza (major.minor.patch) y con qué frecuencia se lanzan versiones major. Visita https://angular.dev/reference/releases para encontrar la política oficial de lanzamientos.

#### Resultado Esperado

Al finalizar este paso, tu informe debe contener:
- Tabla de línea de tiempo completa con columna de impacto personal
- Respuestas a las tres preguntas de análisis (mínimo 2 oraciones cada una)
- Descripción de la política de versionado y frecuencia de releases

#### Verificación

- ✅ ¿Puedo explicar la diferencia fundamental entre AngularJS y Angular 2+?
- ✅ ¿Entiendo por qué se saltó la versión Angular 3?
- ✅ ¿Sé cuándo se lanzó la versión de Angular que usaremos en este curso (Angular 17)?

---

### Paso 3: Arquitectura MVC/MVVM en Angular

**Objetivo:** Comprender cómo el patrón arquitectónico MVC/MVVM se manifiesta en la estructura de Angular, relacionando los conceptos teóricos con los bloques de construcción del framework.

**Duración estimada:** 8 minutos

#### Instrucciones

1. Revisa el siguiente diagrama conceptual del patrón MVC aplicado a Angular:

   ```
   ┌─────────────────────────────────────────────────────────────┐
   │                    PATRÓN MVC EN ANGULAR                     │
   ├──────────────────┬──────────────────┬────────────────────────┤
   │    MODEL         │    VIEW          │    CONTROLLER          │
   │  (Modelo)        │  (Vista)         │  (Controlador)         │
   ├──────────────────┼──────────────────┼────────────────────────┤
   │ • Servicios      │ • Templates HTML │ • Clase del Componente │
   │ • Interfaces     │ • Directivas     │ • Métodos del          │
   │   TypeScript     │ • Pipes          │   Componente           │
   │ • Clases de      │ • Estilos CSS    │ • Event Handlers       │
   │   datos          │                  │                        │
   │ • Estado de la   │                  │ En Angular, el         │
   │   aplicación     │                  │ "Controlador" es la    │
   │                  │                  │ clase TypeScript del   │
   │                  │                  │ componente             │
   └──────────────────┴──────────────────┴────────────────────────┘
   
   MVVM (Model-View-ViewModel):
   ViewModel = Clase del Componente + Data Binding bidireccional
   ```

2. Analiza el siguiente fragmento de código (tomado de la lección) y mapea cada elemento al patrón MVC/MVVM:

   ```typescript
   // archivo: saludo.component.ts
   import { Component } from '@angular/core';

   @Component({
     selector: 'app-saludo',        // Etiqueta HTML personalizada
     template: `<h1>Hola, {{ nombre }}</h1>`,  // ← ¿Qué capa del MVC es esto?
     styles: [`h1 { color: #1976d2; }`]        // ← ¿Y esto?
   })
   export class SaludoComponent {
     nombre: string = 'Angular';   // ← ¿Y esto?
   }
   ```

   En tu informe, bajo la **Sección 2**, crea una tabla con tres columnas:
   - **Elemento del código** (ej: `template`, `styles`, `nombre: string`)
   - **Capa MVC/MVVM correspondiente** (Model / View / ViewModel)
   - **Justificación** (una oración explicando por qué pertenece a esa capa)

3. Navega a **https://angular.dev/guide/architecture** y lee la sección de arquitectura general. Identifica:
   - ¿Cómo describe Angular la relación entre componentes y templates?
   - ¿Qué rol juegan los servicios en la arquitectura?
   - ¿Cómo se relacionan los módulos con la organización de la aplicación?

4. En tu informe, responde la siguiente pregunta de análisis:

   **Pregunta:** Angular es frecuentemente descrito como un framework MVVM más que MVC puro. ¿Qué característica específica de Angular (relacionada con el data binding) justifica esta clasificación? Explica con tus propias palabras.

   > **Pista:** Investiga el concepto de "two-way data binding" en Angular y cómo la directiva `[(ngModel)]` crea un enlace bidireccional entre el ViewModel y la Vista.

5. Registra en tu informe la siguiente tabla de mapeo completa:

   | Concepto Angular | Capa MVC/MVVM | Responsabilidad Principal |
   |---|---|---|
   | Template HTML del componente | Vista (View) | Presentar datos al usuario |
   | Clase TypeScript del componente | ViewModel / Controlador | Gestionar lógica de presentación |
   | Servicio Angular | Modelo (Model) | Encapsular lógica de negocio y datos |
   | Módulo (NgModule) | Organizador | Agrupar elementos relacionados |
   | Directiva | Vista (View) | Modificar comportamiento del DOM |
   | Pipe | Vista (View) | Transformar datos para presentación |
   | Router | Controlador | Gestionar navegación entre vistas |

#### Resultado Esperado

Al finalizar este paso, tu informe debe contener:
- Tabla de mapeo del código de ejemplo al patrón MVC/MVVM
- Respuesta a la pregunta sobre MVVM vs MVC (mínimo 3 oraciones)
- Tabla completa de mapeo de conceptos Angular a capas MVC/MVVM

#### Verificación

- ✅ ¿Puedo identificar la capa MVC correspondiente de cada elemento en un componente Angular?
- ✅ ¿Entiendo por qué Angular se considera más MVVM que MVC puro?
- ✅ ¿Sé cuál es el rol de los servicios en la arquitectura de Angular?

---

### Paso 4: Comparativa Angular vs React vs Vue.js

**Objetivo:** Construir una tabla comparativa fundamentada entre los tres frameworks frontend más populares, utilizando datos de fuentes oficiales y encuestas de la industria.

**Duración estimada:** 10 minutos

#### Instrucciones

1. Navega a **https://npmtrends.com/@angular/core,react,vue** para visualizar la comparación de descargas semanales de los tres frameworks en npm. Observa y registra en tu informe:
   - ¿Cuál tiene más descargas semanales actualmente?
   - ¿Cuál ha tenido el crecimiento más sostenido en los últimos 2 años?
   - ¿Cuál es la tendencia de Angular en comparación con React?

   > **Nota:** Las descargas de npm no equivalen directamente a popularidad en producción, ya que React tiene muchas descargas por ser dependencia de otras herramientas. Toma este dato como referencia, no como conclusión definitiva.

2. Navega a **https://survey.stackoverflow.co/2023** (o la edición más reciente disponible) y busca la sección sobre frameworks web. Registra los porcentajes de uso de Angular, React y Vue.js entre los desarrolladores encuestados.

3. Navega a **https://2022.stateofjs.com/en-US/libraries/front-end-frameworks/** (o la edición más reciente) y observa los gráficos de "usage", "retention" y "interest" para los tres frameworks.

4. Con base en tu investigación, completa la siguiente tabla comparativa en tu informe bajo la **Sección 3**:

   | Dimensión | Angular | React | Vue.js |
   |---|---|---|---|
   | **Creador / Mantenedor** | Google | Meta (Facebook) | Evan You (comunidad) |
   | **Año de lanzamiento** | 2016 (Angular 2) / 2010 (AngularJS) | 2013 | 2014 |
   | **Lenguaje base** | TypeScript (obligatorio) | JavaScript / JSX (TypeScript opcional) | JavaScript / TypeScript (opcional) |
   | **Tipo** | Framework completo (opinionado) | Biblioteca de UI (flexible) | Framework progresivo (flexible) |
   | **Curva de aprendizaje** | Alta (muchos conceptos integrados) | Media (JSX + ecosistema externo) | Baja-Media (documentación amigable) |
   | **Arquitectura** | Basada en componentes + módulos + DI | Basada en componentes | Basada en componentes + Composition API |
   | **Gestión de estado** | NgRx / Services con RxJS | Redux / Zustand / Context API | Pinia / Vuex |
   | **Enrutamiento** | Integrado (@angular/router) | Externo (React Router) | Externo (Vue Router) |
   | **Formularios** | Integrado (Reactive + Template-driven) | Externo (Formik, React Hook Form) | Externo (VeeValidate) |
   | **Tamaño del bundle (aprox.)** | ~150 KB (producción, con tree-shaking) | ~40 KB (solo React + ReactDOM) | ~30 KB |
   | **Soporte empresarial** | Muy alto (Google, respaldo corporativo) | Muy alto (Meta, amplia adopción) | Alto (comunidad + patrocinadores) |
   | **Casos de uso ideales** | Aplicaciones empresariales grandes | Aplicaciones de cualquier escala | Aplicaciones medianas, proyectos rápidos |
   | **Popularidad (Stack Overflow 2023)** | [Completar con dato encontrado] | [Completar con dato encontrado] | [Completar con dato encontrado] |
   | **Descargas npm semanales (aprox.)** | [Completar con dato encontrado] | [Completar con dato encontrado] | [Completar con dato encontrado] |

   > **Instrucción:** Los campos marcados con "[Completar con dato encontrado]" deben ser llenados con los datos reales que obtengas de las fuentes de investigación en los pasos anteriores.

5. Después de completar la tabla, escribe un párrafo de análisis (mínimo 5 oraciones) respondiendo la siguiente pregunta:

   **¿En qué tipo de proyecto elegiría Angular sobre React o Vue.js, y por qué?** Considera factores como: tamaño del equipo, duración del proyecto, necesidades de escalabilidad, experiencia del equipo y requisitos de mantenimiento a largo plazo.

6. Busca en internet (puedes usar Google) al menos un artículo técnico reciente (2022-2024) que compare estos tres frameworks. Registra en tu informe:
   - Título del artículo
   - URL
   - Conclusión principal del artículo (1-2 oraciones)

#### Resultado Esperado

Al finalizar este paso, tu informe debe contener:
- Tabla comparativa completa con los datos de descargas npm y Stack Overflow rellenados
- Párrafo de análisis sobre cuándo elegir Angular
- Referencia a un artículo externo de comparación

#### Verificación

- ✅ ¿Tengo datos reales (no estimados) de popularidad de los tres frameworks?
- ✅ ¿Puedo argumentar cuándo Angular es la mejor elección frente a React o Vue.js?
- ✅ ¿Entiendo que "más descargas" no equivale necesariamente a "mejor framework"?

---

### Paso 5: Inventario de Recursos y Comunidad Angular

**Objetivo:** Catalogar los recursos oficiales, comunidades y herramientas de aprendizaje disponibles para desarrolladores Angular, construyendo una guía de referencia personal.

**Duración estimada:** 6 minutos

#### Instrucciones

1. Visita y explora brevemente cada uno de los siguientes recursos. Para cada uno, registra en tu informe (Sección 4): el nombre, la URL, el tipo de recurso y una descripción de una oración sobre qué tipo de ayuda ofrece.

   **Documentación y Referencias Oficiales:**

   | Recurso | URL | Tipo |
   |---|---|---|
   | Angular Docs | https://angular.dev | Documentación oficial completa |
   | Angular Blog | https://blog.angular.dev | Blog oficial del equipo de Angular |
   | Angular GitHub | https://github.com/angular/angular | Repositorio oficial, issues, changelogs |
   | Angular CLI Docs | https://angular.dev/tools/cli | Documentación de la herramienta CLI |
   | Angular YouTube Channel | https://www.youtube.com/@Angular | Videos oficiales y conferencias |

   **Comunidades y Foros:**

   | Recurso | URL | Tipo |
   |---|---|---|
   | Stack Overflow (tag angular) | https://stackoverflow.com/questions/tagged/angular | Foro de preguntas y respuestas |
   | Reddit r/Angular2 | https://www.reddit.com/r/Angular2/ | Comunidad de Reddit |
   | Angular Discord | https://discord.gg/angular | Servidor oficial de Discord |
   | DEV.to Angular | https://dev.to/t/angular | Artículos de la comunidad |

   **Recursos de Aprendizaje:**

   | Recurso | URL | Tipo |
   |---|---|---|
   | Angular University | https://angular-university.io | Cursos especializados en Angular |
   | Udemy (Angular courses) | https://www.udemy.com/topic/angular/ | Cursos en video |
   | Angular Challenges | https://angular-challenges.vercel.app | Ejercicios prácticos |

2. En Stack Overflow, navega a https://stackoverflow.com/questions/tagged/angular y observa:
   - ¿Cuántas preguntas tienen el tag "angular" en total?
   - ¿Cuántas preguntas se hacen por semana aproximadamente?
   - ¿Cuál es la pregunta con más votos positivos que puedas encontrar en la primera página?

   Registra estos datos en tu informe.

3. Visita el servidor de Discord de Angular (si tienes cuenta de Discord) o revisa la descripción del servidor desde el enlace de invitación. Registra cuántos miembros tiene aproximadamente.

4. En tu informe, agrega una sección de **"Recursos Personales Prioritarios"** donde listes los 3 recursos que consideras más útiles para ti como estudiante principiante de Angular, justificando brevemente cada elección (1-2 oraciones por recurso).

#### Resultado Esperado

Al finalizar este paso, tu informe debe contener:
- Tabla de inventario de recursos con descripción de cada uno
- Datos estadísticos de Stack Overflow (número de preguntas con tag angular)
- Lista de 3 recursos prioritarios personales con justificación

#### Verificación

- ✅ ¿Sé dónde buscar ayuda cuando tenga un problema técnico con Angular?
- ✅ ¿Conozco la diferencia entre la documentación oficial y los recursos de la comunidad?
- ✅ ¿Tengo identificado al menos un recurso de aprendizaje adicional al material del curso?

---

### Paso 6: Empresas que Usan Angular en Producción

**Objetivo:** Identificar aplicaciones reales construidas con Angular para dimensionar el impacto del framework en la industria y comprender los tipos de proyectos donde se aplica.

**Duración estimada:** 6 minutos

#### Instrucciones

1. Navega a **https://www.madewithangular.com** (si está disponible) o busca en Google "companies using Angular in production 2023" para encontrar casos de uso reales.

2. También puedes instalar la extensión **Angular DevTools** en Chrome y visitar los sitios web de grandes empresas para detectar si están construidos con Angular. La extensión mostrará un ícono activo cuando detecte Angular en la página.

   Algunos sitios sugeridos para verificar:
   ```
   https://gmail.com (Google - aplicaciones internas)
   https://www.upwork.com
   https://www.forbes.com
   https://www.delta.com
   https://console.firebase.google.com
   ```

3. Investiga y documenta en tu informe (Sección 5) **al menos 5 empresas** que usen Angular en producción. Para cada empresa, registra:

   | Empresa | Sector | Aplicación/Uso de Angular | Fuente |
   |---|---|---|---|
   | Google | Tecnología | Google Cloud Console, Firebase Console, Google Fonts | Declaraciones oficiales de Google |
   | Microsoft | Tecnología | Azure Portal, Office 365 (partes del frontend) | Documentación de Microsoft |
   | [Empresa 3] | [Sector] | [Descripción del uso] | [URL de la fuente] |
   | [Empresa 4] | [Sector] | [Descripción del uso] | [URL de la fuente] |
   | [Empresa 5] | [Sector] | [Descripción del uso] | [URL de la fuente] |

   > **Instrucción:** Las primeras dos filas son ejemplos verificados. Debes investigar y completar al menos 3 filas adicionales con empresas reales, verificando la información en fuentes confiables.

4. Para cada empresa que documentes, responde brevemente:
   - ¿Por qué crees que eligieron Angular para ese proyecto específico?
   - ¿Qué características de Angular (escala, TypeScript, soporte empresarial) serían más relevantes para ese caso?

5. Escribe un párrafo de reflexión en tu informe sobre el siguiente punto:

   **¿Qué patrón común observas en los tipos de aplicaciones y empresas que adoptan Angular?** (Considera: tamaño de la empresa, tipo de aplicación, sector industrial, escala del proyecto)

#### Resultado Esperado

Al finalizar este paso, tu informe debe contener:
- Tabla con mínimo 5 empresas que usan Angular, con sector, uso específico y fuente verificable
- Análisis breve de por qué cada empresa eligió Angular
- Párrafo de reflexión sobre el patrón de adopción de Angular

#### Verificación

- ✅ ¿Tengo al menos 5 empresas documentadas con fuentes verificables?
- ✅ ¿Puedo identificar el tipo de proyecto donde Angular es la elección preferida?
- ✅ ¿Entiendo por qué el soporte de Google es relevante para la adopción empresarial de Angular?

---

### Paso 7: Consolidación del Informe y Conclusiones

**Objetivo:** Revisar, completar y estructurar el informe de investigación, agregando conclusiones personales que demuestren comprensión profunda del ecosistema Angular.

**Duración estimada:** 8 minutos

#### Instrucciones

1. Revisa tu informe completo y verifica que todas las secciones estén completas. Usa la siguiente lista de verificación:

   ```
   Sección 1 — Historia y Evolución:
   [ ] Línea de tiempo con tabla completa (mínimo 10 hitos)
   [ ] Columna de impacto personal añadida
   [ ] Respuestas a las 3 preguntas de análisis
   [ ] Política de versionado documentada

   Sección 2 — Arquitectura MVC/MVVM:
   [ ] Tabla de mapeo del código de ejemplo
   [ ] Respuesta a la pregunta sobre MVVM vs MVC
   [ ] Tabla de mapeo completa de conceptos Angular

   Sección 3 — Comparativa Frameworks:
   [ ] Tabla comparativa con datos reales de npm trends y Stack Overflow
   [ ] Párrafo de análisis de elección de framework
   [ ] Referencia a artículo externo

   Sección 4 — Recursos y Comunidad:
   [ ] Tabla de inventario de recursos (mínimo 10 recursos)
   [ ] Datos estadísticos de Stack Overflow
   [ ] Lista de 3 recursos prioritarios personales

   Sección 5 — Empresas en Producción:
   [ ] Tabla con mínimo 5 empresas verificadas
   [ ] Análisis de elección por empresa
   [ ] Párrafo de reflexión sobre patrón de adopción
   ```

2. Agrega la **Sección 6: Conclusiones Personales** a tu informe. Esta sección debe responder las siguientes preguntas en un texto corrido (mínimo 200 palabras):

   - Después de esta investigación, ¿cuál es tu percepción general de Angular como framework?
   - ¿Qué aspecto de Angular te parece más interesante o innovador?
   - ¿Qué aspecto te parece más desafiante o complejo de aprender?
   - ¿En qué tipo de proyecto o empresa te imaginas usando Angular en el futuro?
   - ¿Cómo cambia tu perspectiva sobre el desarrollo web después de conocer el contexto histórico de Angular?

3. Agrega una sección de **Referencias Bibliográficas** al final de tu informe. Lista todas las URLs y fuentes que consultaste durante la investigación, usando el siguiente formato:

   ```
   [1] Angular Team. "Angular Overview". angular.dev. https://angular.dev/overview. Consultado: [fecha]
   [2] GitHub. "Angular Repository". github.com. https://github.com/angular/angular. Consultado: [fecha]
   [3] npm trends. "Comparison: @angular/core, react, vue". npmtrends.com. [URL completa]. Consultado: [fecha]
   ... (continuar con todas las fuentes)
   ```

4. Guarda el documento en formato PDF (si tu editor lo permite) o en el formato que indique tu instructor. Nombra el archivo siguiendo esta convención:

   ```
   Lab01-00-01_Investigacion_Angular_[TuApellido]_[TuNombre].pdf
   ```

   Por ejemplo:
   ```
   Lab01-00-01_Investigacion_Angular_GomezLopez_Maria.pdf
   ```

#### Resultado Esperado

Al finalizar este paso, tendrás un informe completo, estructurado y guardado correctamente que incluye:
- Todas las 6 secciones completadas
- Mínimo 200 palabras de conclusiones personales
- Lista de referencias bibliográficas
- Archivo guardado con la convención de nombre correcta

#### Verificación

- ✅ ¿El informe tiene todas las secciones completas?
- ✅ ¿Las conclusiones son personales y reflexivas (no copiadas de la documentación)?
- ✅ ¿Todas las afirmaciones tienen respaldo en una fuente verificable?
- ✅ ¿El archivo está guardado con el nombre correcto?

---

## Validación y Prueba del Aprendizaje

Antes de considerar el laboratorio completo, responde las siguientes preguntas de validación. Si no puedes responder alguna con seguridad, regresa al paso correspondiente y refuerza tu investigación.

### Preguntas de Validación

**Nivel 1 — Recordar y Comprender:**

1. ¿En qué año fue lanzada la primera versión oficial de Angular 2 (la reescritura completa)?
2. ¿Cuál es el lenguaje de programación base que Angular utiliza obligatoriamente?
3. ¿Qué tres archivos componen típicamente un componente Angular?

**Nivel 2 — Aplicar y Analizar:**

4. Si un cliente empresarial te pide construir un portal de gestión con 50+ vistas, autenticación, formularios complejos y un equipo de 8 desarrolladores, ¿qué framework recomendarías y por qué?

5. Identifica en el siguiente fragmento de código qué capa del patrón MVVM representa cada elemento:

   ```typescript
   @Component({
     selector: 'app-lista',
     template: `
       <ul>
         <li *ngFor="let item of items">{{ item.nombre }}</li>
       </ul>
     `
   })
   export class ListaComponent {
     items: Item[] = [];
     
     constructor(private itemService: ItemService) {}
     
     ngOnInit(): void {
       this.items = this.itemService.obtenerItems();
     }
   }
   ```

6. ¿Por qué la introducción del renderizador Ivy en Angular 9 fue considerada un hito importante? Menciona al menos dos beneficios concretos.

**Nivel 3 — Evaluar:**

7. Un desarrollador argumenta: "No tiene sentido aprender Angular cuando React tiene más descargas en npm". ¿Cómo refutarías este argumento usando los datos que investigaste?

### Rúbrica de Autoevaluación del Informe

| Criterio | Excelente (4) | Bueno (3) | Suficiente (2) | Insuficiente (1) |
|---|---|---|---|---|
| **Completitud** | Todas las secciones completas con datos verificados | 5 de 6 secciones completas | 4 de 6 secciones completas | Menos de 4 secciones |
| **Precisión de datos** | Todos los datos tienen fuente verificable | La mayoría de datos tienen fuente | Algunos datos tienen fuente | Sin fuentes verificables |
| **Análisis crítico** | Conclusiones propias bien argumentadas | Análisis presente pero superficial | Parafrasea fuentes sin análisis | Solo copia de fuentes |
| **Comparativa frameworks** | Tabla completa con datos reales y análisis | Tabla completa sin análisis profundo | Tabla parcial | Sin tabla comparativa |
| **Casos empresariales** | 5+ empresas con fuentes y análisis | 5 empresas sin análisis | 3-4 empresas | Menos de 3 empresas |
| **Redacción y estructura** | Claro, organizado, sin errores | Mayormente claro, pocos errores | Comprensible con algunos errores | Difícil de leer |

---

## Solución de Problemas

### Problema 1: El sitio `angular.dev` no carga o muestra contenido diferente al esperado

**Síntoma:** Al navegar a `https://angular.dev/overview`, la página no carga, muestra un error 404, o el contenido parece diferente a lo descrito en las instrucciones (los nombres de secciones no coinciden).

**Causa probable:** Angular actualizó su sitio de documentación y reorganizó las secciones. Esto es frecuente ya que `angular.dev` es un sitio en constante evolución. También puede deberse a problemas temporales de conectividad o caché del navegador.

**Solución:**
1. Primero, intenta limpiar la caché del navegador: `Ctrl + Shift + R` (Windows/Linux) o `Cmd + Shift + R` (macOS).
2. Si el problema persiste, intenta acceder desde una pestaña de incógnito: `Ctrl + Shift + N`.
3. Si la sección específica no existe, usa el buscador integrado del sitio (ícono de lupa) para buscar el término equivalente (ej: busca "components" o "architecture").
4. Como alternativa, accede a la versión anterior de la documentación en `https://v17.angular.io/docs` que es más estable.
5. Si hay problemas de conectividad, usa la caché de Google: busca en Google `site:angular.dev overview` y accede a la versión en caché.

---

### Problema 2: npm trends no muestra datos o los gráficos no se cargan correctamente

**Síntoma:** Al navegar a `https://npmtrends.com/@angular/core,react,vue`, la página carga pero los gráficos aparecen vacíos, muestran un error, o los datos de descargas parecen inconsistentes o extremadamente diferentes a lo esperado.

**Causa probable:** npm trends es un servicio de terceros que depende de la API de npm. Puede tener interrupciones temporales, cambios en su interfaz, o puede que el nombre de los paquetes en la URL haya cambiado. También es posible que un bloqueador de anuncios o extensión del navegador esté interfiriendo con la carga de los gráficos.

**Solución:**
1. Verifica que la URL sea exactamente: `https://npmtrends.com/@angular/core,react,vue` (nota el `@` antes de `angular/core`).
2. Desactiva temporalmente cualquier extensión de bloqueo de anuncios (uBlock Origin, AdBlock) y recarga la página.
3. Si el sitio sigue sin funcionar, usa la alternativa **npm-stat**: `https://npm-stat.com/charts.html?package=%40angular%2Fcore&package=react&package=vue`
4. Como segunda alternativa, busca en Google "angular vs react vs vue downloads 2023" para encontrar artículos con capturas de pantalla de los datos de npm trends que puedas referenciar en tu informe.
5. Si ninguna opción funciona, registra en tu informe que los datos de npm trends no estuvieron disponibles durante la investigación y usa los datos del Stack Overflow Developer Survey como fuente alternativa de popularidad.

---

## Limpieza del Entorno

Al finalizar esta práctica de investigación, realiza las siguientes acciones de limpieza:

1. **Cierra las pestañas del navegador** que ya no necesites. Puedes marcar como favoritas las que desees conservar para referencia futura:
   ```
   Favoritos sugeridos:
   ★ https://angular.dev — Documentación oficial (uso frecuente en el curso)
   ★ https://angular.dev/guide/architecture — Arquitectura de Angular
   ★ https://blog.angular.dev — Blog oficial para mantenerse actualizado
   ```

2. **Guarda una copia de respaldo** de tu informe en la nube (Google Drive, OneDrive o similar) para evitar pérdida de datos.

3. **Organiza tus archivos** en una carpeta del curso con la siguiente estructura:
   ```
   Curso-Angular/
   └── Lab01-Investigacion/
       ├── Lab01-00-01_Investigacion_Angular_[Apellido]_[Nombre].pdf
       └── recursos/
           └── (opcional: capturas de pantalla de npm trends, etc.)
   ```

4. Si instalaste Angular DevTools durante la práctica, puedes mantenerla instalada ya que será útil en los laboratorios de código más adelante en el curso.

---

## Resumen

En esta práctica realizaste una investigación sistemática del ecosistema Angular que te permitió construir el contexto conceptual necesario para el resto del curso. Los puntos clave que debes haber consolidado son:

| Área Investigada | Hallazgo Principal |
|---|---|
| **Historia y Evolución** | Angular tiene una historia de más de 13 años, con una reescritura completa en 2016 (de AngularJS a Angular 2) y lanzamientos major cada 6 meses |
| **Arquitectura MVC/MVVM** | Angular implementa MVVM donde el componente (clase TS + template) actúa como ViewModel, los servicios como Model y los templates como View |
| **Comparativa Frameworks** | Angular es la elección preferida para aplicaciones empresariales grandes; React domina en popularidad general; Vue.js destaca en facilidad de aprendizaje |
| **Recursos y Comunidad** | Existe un ecosistema robusto de documentación oficial, comunidades activas y recursos de aprendizaje especializados |
| **Adopción Industrial** | Grandes empresas tecnológicas (Google, Microsoft) y diversas industrias usan Angular para aplicaciones críticas de negocio |

### Conexión con los Siguientes Laboratorios

Este laboratorio de investigación establece la base conceptual para los próximos pasos del curso:

- **Lab 01-00-02** — Instalación del entorno de desarrollo (Node.js, Angular CLI, VS Code)
- **Lab 01-00-03** — Creación del primer proyecto Angular y exploración de su estructura
- **Módulo 2** — Construcción de componentes reales aplicando los conceptos investigados hoy

### Recursos de Referencia Adicionales

| Recurso | URL | Para qué usarlo |
|---|---|---|
| Angular Update Guide | https://update.angular.io | Guía oficial para migrar entre versiones de Angular |
| Angular Roadmap | https://angular.dev/roadmap | Ver las próximas características planificadas |
| Awesome Angular | https://github.com/PatrickJS/awesome-angular | Lista curada de recursos, librerías y herramientas de la comunidad |
| Angular in 100 Seconds | https://www.youtube.com/watch?v=Ata9cSC2WpM | Video introductorio de Fireship (inglés, 100 segundos) |
| Angular Blog — v17 Release | https://blog.angular.dev/introducing-angular-v17-4d7033312e4b | Artículo oficial del lanzamiento de Angular 17 |

---

> **Nota para el instructor:** Este laboratorio está diseñado como actividad de investigación sin escritura de código. El informe resultante puede evaluarse usando la rúbrica incluida en la sección de Validación. Se recomienda dedicar 5-10 minutos al final de la sesión para que los estudiantes compartan en grupo sus hallazgos más interesantes, especialmente de la sección de empresas en producción y la comparativa de frameworks.
