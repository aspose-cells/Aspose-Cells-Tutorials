---
category: general
date: 2026-05-30
description: Aprende cómo crear una instancia de GridJsOptions y configurar las opciones
  de la cuadrícula en JavaScript para tablas dinámicas. Guía paso a paso con el código
  completo.
draft: false
keywords:
- create gridjsoptions instance
- configure grid options javascript
- gridjs initialization
- javascript data grid settings
- dynamic table configuration
language: es
og_description: Crea una instancia de GridJsOptions y configura las opciones de la
  cuadrícula en JavaScript en minutos. Ejemplo completo, explicaciones y consejos
  de buenas prácticas.
og_title: Crear instancia de GridJsOptions – Configurar opciones de la cuadrícula
  en JavaScript
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  headline: Create GridJsOptions Instance – Configure Grid Options JavaScript
  type: TechArticle
- description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  name: Create GridJsOptions Instance – Configure Grid Options JavaScript
  steps:
  - name: Prerequisites
    text: '- A modern browser (Chrome, Edge, Firefox) – no build tools required. -
      Basic familiarity with JavaScript (variables, objects, DOM). - The Grid.js library
      (we’ll pull it from a CDN).'
  - name: Why this matters
    text: Loading the library from a CDN ensures you always get the latest stable
      version without a local install. The `<div id="grid-wrapper">` is the placeholder
      that the Grid.js constructor will target once we **configure grid options JavaScript**.
  - name: What you’re configuring
    text: '- **NumberFormatAlignment** – aligns numeric strings automatically. - **Pagination**
      – controls page size and navigation. - **Sorting** – toggles column sorting.
      - **Columns** – defines headers, data types, and custom renderers.'
  - name: Edge‑case note
    text: If you later supply a custom data source that already returns paginated
      results, you’ll want to disable Grid.js’s built‑in pagination to avoid double‑paging.
      Simply set `gridOptions.Pagination.enabled = false;`.
  - name: Expected Output
    text: 'When you open the HTML file in a browser you should see:'
  type: HowTo
tags:
- gridjs
- javascript
- data‑grid
title: Crear instancia de GridJsOptions – Configurar opciones de la cuadrícula en
  JavaScript
url: /es/net/link-and-configuration-operations/create-gridjsoptions-instance-configure-grid-options-javascr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear instancia de GridJsOptions – Configurar Grid Options JavaScript

¿Alguna vez te has preguntado cómo **crear una instancia de GridJsOptions** sin buscar en documentación dispersa? No eres el único. Cuando necesitas una tabla elegante y ordenable en una página web, dominar cómo **configurar grid options JavaScript** es el primer paso hacia una interfaz pulida.

En este tutorial recorreremos el código exacto que necesitas, explicaremos por qué cada configuración es importante y te mostraremos un ejemplo completo y ejecutable. Al final te sentirás cómodo creando instancias de GridJsOptions, ajustando la alineación, la paginación e incluso renderizadores de celdas personalizados, todo con JavaScript puro.

## Lo que aprenderás

- Cómo **crear una instancia de GridJsOptions** desde cero.
- Las propiedades clave que te permiten **configurar grid options JavaScript** (ordenación, paginación, formato de números, etc.).
- Trampas comunes (p. ej., mezclar tipos de cadena y numéricos) y cómo evitarlas.
- Una página HTML completa que puedes copiar y pegar en cualquier proyecto y ver los resultados al instante.

### Requisitos previos

- Un navegador moderno (Chrome, Edge, Firefox) – sin necesidad de herramientas de compilación.
- Familiaridad básica con JavaScript (variables, objetos, DOM).
- La biblioteca Grid.js (la obtendremos de un CDN).

Si alguno de estos te resulta desconocido, no te preocupes; cada paso incluye un repaso rápido.

---

## Paso 1: Cargar Grid.js y preparar el esqueleto HTML

Antes de poder **crear una instancia de GridJsOptions**, necesitamos la propia biblioteca. La forma más fácil es usar el CDN oficial. A continuación se muestra un esqueleto HTML mínimo que también reserva un `<div>` donde se renderizará la cuadrícula.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Grid.js Demo – Configuring Options</title>
  <!-- Grid.js CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <h2>Simple Data Grid</h2>
  <div id="grid-wrapper"></div>

  <!-- Grid.js JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <!-- Our custom script will go here -->
  <script src="grid-config.js"></script>
</body>
</html>
```

> **Consejo profesional:** Mantén el enlace CSS antes de tus propios estilos para que el tema predeterminado de la cuadrícula se cargue correctamente.

### Por qué esto importa

Cargar la biblioteca desde un CDN garantiza que siempre obtengas la última versión estable sin una instalación local. El `<div id="grid-wrapper">` es el marcador de posición que el constructor de Grid.js apuntará una vez que **configuremos grid options JavaScript**.

---

## Paso 2: Crear una nueva instancia de GridJsOptions

Ahora llega el corazón del tutorial: la línea que realmente **crea una instancia de GridJsOptions**. En un archivo separado llamado `grid-config.js` (referenciado en el HTML anterior) escribiremos:

```javascript
// grid-config.js

// Step 2: Create a new GridJsOptions instance to configure grid behavior
const gridOptions = new GridJsOptions();
```

Esa única línea te brinda un objeto limpio que puedes comenzar a rellenar con configuraciones. Piensa en `gridOptions` como el panel de control para cada característica que habilitarás más adelante.

### Lo que estás configurando

- **NumberFormatAlignment** – alinea automáticamente cadenas numéricas.
- **Pagination** – controla el tamaño de página y la navegación.
- **Sorting** – alterna la ordenación de columnas.
- **Columns** – define encabezados, tipos de datos y renderizadores personalizados.

Puedes agregar cualquiera de estas propiedades antes de instanciar finalmente la Grid.

---

## Paso 3: Habilitar alineación numérica (un requisito común)

La mayoría de las tablas contienen una mezcla de texto y números. Por defecto Grid.js alinea todo a la izquierda, lo que se ve extraño para valores monetarios. Para **configurar grid options JavaScript** con la alineación adecuada, establece la bandera `NumberFormatAlignment`:

```javascript
// Enable left/right alignment for numeric strings
gridOptions.NumberFormatAlignment = true;
```

¿Por qué habilitar esto? Cuando la bandera es verdadera, Grid.js inspecciona cada celda; si parece un número (p. ej., “1234”, “12.34%”), lo alinea automáticamente a la derecha. Este pequeño ajuste hace que los informes sean mucho más legibles.

---

## Paso 4: Añadir paginación y ordenación

Una cuadrícula del mundo real rara vez cabe en una sola pantalla. Activemos la paginación (10 filas por página) y permitamos que los usuarios ordenen cualquier columna.

```javascript
gridOptions.Pagination = {
  limit: 10,          // rows per page
  enabled: true
};

gridOptions.Sort = true;   // enables click‑to‑sort on all columns
```

### Nota sobre casos extremos

Si más adelante proporcionas una fuente de datos personalizada que ya devuelve resultados paginados, querrás desactivar la paginación incorporada de Grid.js para evitar la paginación doble. Simplemente establece `gridOptions.Pagination.enabled = false;`.

---

## Paso 5: Definir columnas y datos de ejemplo

Ahora alimentaremos la cuadrícula con algunos datos simulados y le diremos lo que representa cada columna. Aquí es donde el patrón **create gridjsoptions instance** realmente brilla: todo vive en un único objeto ordenado.

```javascript
// Sample data array of objects
const sampleData = [
  { id: 1, name: "Alice", salary: "54000", department: "Engineering" },
  { id: 2, name: "Bob",   salary: "47000", department: "Marketing" },
  { id: 3, name: "Cara",  salary: "62000", department: "Design" },
  // ...more rows as needed
];

// Column definitions
gridOptions.Columns = [
  { id: "id",   name: "ID",          width: "5%" },
  { id: "name", name: "Employee",    width: "35%" },
  { id: "salary", name: "Salary ($)", width: "20%" },
  { id: "department", name: "Dept.",  width: "40%" }
];

// Attach data source
gridOptions.Data = sampleData;
```

Observa que mantenemos los valores `id` de las columnas idénticos a las claves en cada objeto de datos. Esta convención permite que Grid.js asocie los valores automáticamente, ahorrándote escribir un formateador personalizado para cada columna.

---

## Paso 6: Instanciar la Grid con nuestras opciones

Finalmente **configuramos grid options javascript** pasando el objeto `gridOptions` al constructor de Grid. La cuadrícula se renderizará dentro del `<div id="grid-wrapper">` que preparamos antes.

```javascript
// Create the Grid instance using the previously built options
const grid = new Grid(gridOptions);

// Render the grid into the page
grid.render(document.getElementById("grid-wrapper"));
```

Eso es todo. Todo el proceso—desde **create gridjsoptions instance** hasta el renderizado—toma menos de un minuto de codificación.

### Resultado esperado

Al abrir el archivo HTML en un navegador deberías ver:

- Una fila de encabezado con “ID”, “Employee”, “Salary ($)”, “Dept.”.
- Números de salario alineados a la derecha (gracias a `NumberFormatAlignment`).
- Controles de paginación en la parte inferior (si añadiste más de diez filas).
- Encabezados de columna clicables que ordenan ascendente/descendente.

Si algo parece incorrecto, abre la consola del navegador (F12) y busca mensajes de error; la mayoría de los errores provienen de IDs de columna que no coinciden o de scripts de la biblioteca faltantes.

---

## Paso 7: Ajustes avanzados (opcional)

A continuación tienes algunas ideas rápidas que puedes experimentar una vez que la cuadrícula básica funcione.

| Funcionalidad | Cómo habilitar | Por qué ayuda |
|---------------|----------------|---------------|
| **Renderizador de celda personalizado** | `gridOptions.Columns[2].formatter = (cell) => \`<b>$${cell}</b>\`;` | Resalta los salarios en negrita. |
| **Barra de búsqueda** | `gridOptions.Search = true;` | Permite a los usuarios filtrar filas al instante. |
| **Datos del lado del servidor** | Set `gridOptions.Server = { url: "/api/employees", then: data => data.items };` | Escala a miles de filas. |
| **Cambio de tema** | Add `gridOptions.ClassName = "gridjs-theme-dark";` | Coincide con diseños de modo oscuro. |

Siéntete libre de combinar y mezclar—Grid.js es deliberadamente flexible. Solo recuerda mantener la línea original **create gridjsoptions instance** en la parte superior; todos los ajustes posteriores dependen de ese único objeto.

---

## Conclusión

Acabamos de recorrer un flujo de trabajo completo para **crear una instancia de GridJsOptions** y **configurar grid options JavaScript** para una tabla de datos funcional, ordenable y paginada. Partiendo de una página HTML simple, cargamos la biblioteca, construimos un objeto de opciones, habilitamos la alineación numérica, añadimos paginación, definimos columnas y finalmente renderizamos la cuadrícula.

A partir de aquí puedes:

- Reemplazar los `sampleData` estáticos con una llamada AJAX.
- Agregar formateadores personalizados para fechas, monedas o íconos.
- Integrar la cuadrícula en un framework como React o Vue (el mismo objeto `gridOptions` funciona allí también).

Las posibilidades son prácticamente infinitas, y el patrón que usamos—centralizar todas las configuraciones en una única instancia de `GridJsOptions`—mantiene tu código limpio y mantenible.

¿Tienes un caso de uso del que no estás seguro? Deja un comentario y lo exploraremos juntos. ¡Feliz codificación y disfruta creando tablas dinámicas con Grid.js!

## ¿Qué deberías aprender a continuación?

- [Cómo crear y configurar libros de Excel con Aspose.Cells .NET: Guía paso a paso](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Cómo crear y dar estilo a tablas de Excel usando Aspose.Cells para .NET | Guía paso a paso](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)
- [Cómo crear y formatear celdas de Excel usando Aspose.Cells para Java: Guía paso a paso](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}