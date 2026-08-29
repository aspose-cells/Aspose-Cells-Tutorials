---
category: general
date: 2026-06-21
description: Crea una cuadrícula de datos interactiva usando Grid.js y aprende a mostrar
  una tabla de datos JSON con ordenación, paginación y búsqueda. Perfecto para paneles
  web.
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: es
og_description: Crea una cuadrícula de datos interactiva en minutos. Aprende a usar
  Grid.js para mostrar una tabla de datos JSON con paginación, ordenación y búsqueda.
og_title: Crea una cuadrícula de datos interactiva con Grid.js – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  headline: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  name: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  steps:
  - name: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
    text: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
  - name: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
    text: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
  - name: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
    text: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
  type: HowTo
tags:
- JavaScript
- Grid.js
- Data Visualization
title: Crea una cuadrícula de datos interactiva con Grid.js – Guía completa paso a
  paso
url: /es/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear una cuadrícula de datos interactiva con Grid.js – Guía completa paso a paso

¿Alguna vez te has preguntado cómo **crear una cuadrícula de datos interactiva** que permita a los usuarios ordenar, buscar y paginar filas sin escribir un backend? No estás solo. En muchos paneles, el mayor problema es convertir un volcado estático de JSON en una tabla elegante y buscable, algo que se siente tan fluido como una hoja de cálculo pero que se ejecuta completamente en el navegador.

En este tutorial recorreremos **cómo usar Grid.js** para **mostrar una tabla de datos JSON** en una página HTML sencilla. Al final tendrás un ejemplo funcional que podrás insertar en cualquier proyecto, además de consejos para personalizar la barra de herramientas, manejar conjuntos de datos grandes y evitar errores comunes.

## Lo que aprenderás

- Cómo obtener un archivo JSON que define columnas y filas.
- Cómo inicializar **Grid.js** con paginación, ordenamiento, búsqueda y una barra de herramientas personalizada.
- Cómo renderizar la cuadrícula en un contenedor objetivo.
- Ajustes opcionales: formato de celdas personalizado, cambio de tema y manejo de errores.
- Un ejemplo de código completo, listo para copiar y pegar.

### Prerrequisitos

Antes de comenzar, asegúrate de tener:

1. Un navegador moderno (Chrome, Edge o Firefox) – Grid.js depende de características ES6.
2. Una carpeta local o remota que contenga un archivo `grid_data.json` (mostraremos el formato).
3. Familiaridad básica con HTML y JavaScript – nada sofisticado, solo la capacidad de abrir un archivo `.html` en un navegador.

Sin herramientas de compilación, sin npm install, sin código del lado del servidor. Esa es la belleza de **crear una cuadrícula de datos interactiva** con Grid.js: funciona directamente desde un CDN.

---

## Paso 1: Preparar el JSON que define tu tabla

Lo primero que necesitas es una carga JSON que indique a Grid.js qué columnas existen y qué filas mostrar. Piensa en ello como el plano de tu **tabla de datos JSON**. Aquí tienes un ejemplo mínimo que puedes guardar como `grid_data.json` en el mismo directorio que tu archivo HTML:

```json
{
  "columns": ["ID", "Name", "Email", "Country"],
  "rows": [
    [1, "Alice Johnson", "alice@example.com", "USA"],
    [2, "Bob Smith", "bob@example.com", "Canada"],
    [3, "Carlos Ruiz", "carlos@example.com", "Mexico"],
    [4, "Diana Lee", "diana@example.com", "UK"]
  ]
}
```

*¿Por qué este formato?* Grid.js espera que `columns` sea un arreglo de cadenas (o objetos para configuración avanzada) y que `rows` sea un arreglo de arreglos donde cada arreglo interno coincide con el orden de las columnas. Por supuesto, puedes añadir más columnas u objetos anidados – Grid.js los renderizará siempre que las estructuras coincidan.

> **Consejo profesional:** Si estás obteniendo datos de una API, simplemente reemplaza el `fetch('grid_data.json')` estático con la URL de tu endpoint. El resto del código permanece igual.

---

## Paso 2: Inicializar Grid.js – El corazón de **cómo usar gridjs**

Ahora que la fuente de datos está lista, necesitamos incorporar Grid.js en la página y decirle cómo debe comportarse. Aquí es donde realmente **creamos la funcionalidad de cuadrícula de datos interactiva** como paginación, ordenamiento y un práctico botón en la barra de herramientas.

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

El CDN te proporciona la última versión estable, y el tema Mermaid agrega un aspecto limpio y moderno listo para usar. Puedes cambiarlo por `gridjs.min.css` si prefieres el estilo predeterminado.

A continuación, dentro de una etiqueta `<script>`, obtén el JSON e inicializa la cuadrícula:

```javascript
// Step 2: Initialise Grid.js with pagination, sorting, searching, and a toolbar
fetch('grid_data.json')
  .then(response => response.json())
  .then(data => {
    const grid = new gridjs.Grid({
      columns: data.columns,      // Pull column headers from JSON
      data: data.rows,            // Pull row data from JSON
      pagination: { enabled: true, limit: 10 }, // Show 10 rows per page
      sort: true,                 // Enable column sorting
      search: true,               // Add a search box above the grid
      toolbar: {
        enabled: true,
        items: [
          {
            type: 'button',
            text: 'Help',
            onClick: () => alert('Use the search box to filter rows or click column headers to sort.')
          }
        ]
      },
      // Optional: custom cell formatter for the Email column
      // This demonstrates a deeper dive into how to use Grid.js
      // and shows you can embed HTML inside cells.
      columns: data.columns.map(col => {
        if (col === 'Email') {
          return {
            name: col,
            formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
          };
        }
        return col; // Simple string for other columns
      })
    });

    // Step 3: Render the grid into the target container
    grid.render(document.getElementById('grid-container'));
  })
  .catch(err => console.error('Failed to load grid data:', err));
```

### Desglosando las opciones

| Opción | Qué hace | Por qué es importante |
|--------|----------|-----------------------|
| `pagination` | Divide las filas en páginas (por defecto 10 por página) | Mantiene tablas grandes utilizables sin saturar la UI. |
| `sort` | Los encabezados de columna clicables alternan orden ascendente/descendente | Los usuarios pueden encontrar rápidamente las filas de mayor valor. |
| `search` | Añade un campo de texto que filtra filas al instante | Ideal para búsquedas ad‑hoc sin recargar datos. |
| `toolbar` | Añade botones o menús desplegables personalizados sobre la cuadrícula | Perfecto para acciones de “Ayuda”, “Exportar” o “Actualizar”. |
| `formatter` | Permite devolver HTML sin procesar para una celda | Aquí convertimos cadenas de correo electrónico en enlaces mailto clicables. |

> **¿Por qué este enfoque?** Al mantener la configuración de la cuadrícula declarativa, puedes ajustar fácilmente el comportamiento sin tocar la lógica central de renderizado. Esta es la forma recomendada de **cómo usar Grid.js** para la mayoría de los proyectos.

---

## Paso 3: Renderizar la cuadrícula en tu página

La última línea del script—`grid.render(document.getElementById('grid-container'))`—inyecta la tabla completamente funcional en un `<div>` que hayas colocado en algún lugar del cuerpo de tu HTML:

```html
<div id="grid-container"></div>
```

Eso es todo. Cuando la página se carga, el navegador obtiene el JSON, construye la instancia de Grid.js y dibuja la tabla interactiva en la pantalla. Sin recargas, sin llamadas al servidor después de la carga inicial.

---

## Opcional: Ajustes de estilo y tema

Si el tema Mermaid predeterminado no es de tu agrado, puedes cambiarlo por cualquiera de los temas incorporados (`gridjs.min.css`) o escribir tu propio CSS. Por ejemplo, para hacer que el fondo del encabezado sea un gris suave:

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

Añade el fragmento dentro de una etiqueta `<style>` o una hoja de estilos externa. Grid.js respeta los selectores CSS estándar, por lo que tienes control total sobre fuentes, colores y espaciado.

---

## Problemas comunes y cómo evitarlos

| Problema | Síntoma | Solución |
|----------|---------|----------|
| **Errores CORS** al obtener JSON de otro dominio | La consola del navegador muestra “Blocked by CORS policy” | Aloja el JSON en el mismo origen o habilita CORS en el servidor. |
| **Conjuntos de datos grandes provocan retrasos** | El desplazamiento se vuelve entrecortado, la paginación lenta | Usa paginación `server` (`pagination: { server: { url: (prev, page, limit) => … } }`) o carga perezosa de filas. |
| **El botón de la barra de herramientas no aparece** | No se ve ningún botón a pesar de `toolbar.enabled: true` | Asegúrate de usar Grid.js versión 2.0+; versiones anteriores tenían una API de barra de herramientas diferente. |
| **Los enlaces de correo no son clicables** | El formatter devuelve texto plano | Devuelve `gridjs.html(...)` en lugar de una cadena simple, como se muestra en el ejemplo. |

Abordar estos problemas temprano te ahorra horas de depuración más adelante.

---

## Ejemplo completo (listo para copiar y pegar)

A continuación se muestra el archivo HTML completo que puedes guardar como `index.html`. Ábrelo en un navegador y verás una demostración totalmente funcional de **crear una cuadrícula de datos interactiva** que **muestra una tabla de datos JSON** con ordenamiento, búsqueda y un botón de ayuda.



## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo crear una lista de validación de datos de Excel con Aspose.Cells para Java: Guía paso a paso](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [Cómo crear casillas de verificación en Excel usando Aspose.Cells para .NET | Tutorial de validación de datos](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [Crear e importar datos XML a Excel usando Aspose.Cells para Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}