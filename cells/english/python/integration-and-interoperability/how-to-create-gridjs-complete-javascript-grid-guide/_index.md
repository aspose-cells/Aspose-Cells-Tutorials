---
category: general
date: 2026-06-30
description: How to create gridjs easily with a full JavaScript example, covering
  gridjs configuration, container setup, and render process.
draft: false
keywords:
- how to create gridjs
- gridjs configuration
- gridjs render
- gridjs JavaScript
- gridjs container
language: en
og_description: How to create gridjs easily with a full JavaScript example, covering
  gridjs configuration, container setup, and render process.
og_title: How to Create Gridjs – Complete JavaScript Grid Guide
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  headline: How to Create Gridjs – Complete JavaScript Grid Guide
  type: TechArticle
- description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  name: How to Create Gridjs – Complete JavaScript Grid Guide
  steps:
  - name: Why this configuration matters
    text: '- **Columns** – define the header text and optional width. Without this,
      Gridjs would infer column names from the first data row, which is often less
      readable. - **Data** – an array of rows, each row being an array of cell values.
      You could also supply an async function that fetches data from an API'
  - name: Expected Output
    text: '``` +----+----------------+---------------------+--------+ | ID | Name
      | Email | Role | +----+----------------+---------------------+--------+ | 1
      | Alice Johnson | alice@example.com | Admin | | 2 | Bob Smith | bob@example.com
      | Editor | +----+----------------+---------------------+--------+ [←] [1]'
  - name: Loading Data Asynchronously
    text: 'If your data lives on a server, replace the static `data` array with a
      function that returns a Promise:'
  - name: Custom Cell Rendering
    text: 'Sometimes you need icons, buttons, or formatted dates inside cells. Use
      the `formatter` property on a column:'
  - name: Multiple Grids on One Page
    text: 'Just repeat steps 2‑5 with different container IDs:'
  type: HowTo
tags:
- gridjs
- JavaScript
- web‑development
title: How to Create Gridjs – Complete JavaScript Grid Guide
url: /python/integration-and-interoperability/how-to-create-gridjs-complete-javascript-grid-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Create Gridjs – Complete JavaScript Grid Guide

Ever wondered **how to create gridjs** and instantly see a slick data table on your page? You're not the only one. Many developers hit a wall when they first try to wire up Gridjs, especially around the configuration object and the render call. The good news? It’s actually a piece of cake once you know the right steps.

In this tutorial we’ll walk through a real‑world example that shows **how to create gridjs** from scratch, how to craft a proper **gridjs configuration**, how to bind the grid to a **gridjs container**, and finally how to trigger the **gridjs render**. By the end you’ll have a fully functional grid you can drop into any project—no mystery, just clear code.

## What You’ll Learn

- Set up a minimal HTML page ready for Gridjs.
- Write a **gridjs configuration** object that defines columns, data, and options.
- Attach the Gridjs instance to a **gridjs container** element.
- Call **gridjs render** to display the table.
- Tweak common settings (pagination, sorting, styling) and avoid typical pitfalls.

No external build tools are required; everything runs in the browser with a single script tag. Let’s get started.

## Prerequisites

Before we dive in, make sure you have:

1. A modern browser (Chrome, Edge, Firefox, Safari) – anything that supports ES6.
2. Basic knowledge of HTML and JavaScript – you don’t need a framework.
3. Access to the Gridjs library – we’ll pull it from a CDN, so no npm install needed.

That’s it. If you already have a page you want to enhance, you can paste the snippets right in.

## Step 1: Add Gridjs Assets to Your Page

First, we need to load Gridjs’s CSS and JavaScript files. The CDN version is lightweight and perfect for quick demos.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to Create Gridjs Example</title>
  <!-- Gridjs CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <!-- The grid will appear inside this div -->
  <div id="grid"></div>

  <!-- Gridjs JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
```

> **Pro tip:** The Mermaid theme gives the table a clean, modern look without any extra CSS. Feel free to swap it for `classic.min.css` if you prefer a different style.

## Step 2: Define the **gridjs container**

The **gridjs container** is just a normal `<div>` that will host the rendered table. In the markup above we already created `<div id="grid"></div>`. The `id` attribute is crucial because we’ll use it to bind the Gridjs instance later.

If you need multiple grids on the same page, give each container a unique ID (`grid1`, `grid2`, …) and repeat the binding logic for each one.

## Step 3: Craft a **gridjs configuration** Object

Now comes the heart of **how to create gridjs** – the configuration. This plain JavaScript object tells Gridjs what columns to show, what data to fill, and which features to enable.

```html
<script>
  // Step 3: Your gridjs configuration (replace with real data)
  const config = {
    columns: [
      { name: 'ID', width: '50px' },
      { name: 'Name' },
      { name: 'Email' },
      { name: 'Role' }
    ],
    data: [
      [1, 'Alice Johnson', 'alice@example.com', 'Admin'],
      [2, 'Bob Smith', 'bob@example.com', 'Editor'],
      [3, 'Carol White', 'carol@example.com', 'Viewer'],
      [4, 'David Brown', 'david@example.com', 'Admin']
    ],
    pagination: {
      limit: 2   // Show 2 rows per page
    },
    search: true,          // Enable client‑side search box
    sort: true,            // Allow column sorting
    language: {
      'search': {
        'placeholder': '🔍 Search…'
      },
      'pagination': {
        'previous': '←',
        'next': '→',
        'showing': 'Showing',
        'results': () => 'records'
      }
    }
  };
</script>
```

### Why this configuration matters

- **Columns** – define the header text and optional width. Without this, Gridjs would infer column names from the first data row, which is often less readable.
- **Data** – an array of rows, each row being an array of cell values. You could also supply an async function that fetches data from an API; the library will handle promises automatically.
- **Pagination** – limits rows per page, preventing huge tables from overwhelming the UI.
- **Search & Sort** – turn on interactive features with a single boolean, saving you from writing custom handlers.
- **Language** – customize UI strings, perfect for localisation or branding.

Feel free to swap the static data array with a fetch call later; the rest of the steps stay exactly the same.

## Step 4: Instantiate Gridjs and Bind to the **gridjs container**

With configuration ready, we create a new `GridJs.Grid` (the class name is `gridjs.Grid` in the UMD build) and point it at our container element.

```html
<script>
  // Step 4: Create a Gridjs instance bound to the container
  const grid = new gridjs.Grid(document.getElementById('grid'), config);
</script>
```

Notice we used `document.getElementById('grid')`—that’s the **gridjs container** we defined earlier. If you have multiple containers, just repeat this line with the appropriate ID.

## Step 5: Trigger the **gridjs render** Call

The final piece of the puzzle is the **gridjs render** method. It takes the configuration we passed earlier and injects a fully‑styled `<table>` into the container.

```html
<script>
  // Step 5: Render the grid inside the container
  grid.render();
</script>
</body>
</html>
```

That’s it! When you open the page in a browser, you’ll see a searchable, paginated table with the four rows we defined. The search box appears automatically at the top, and the pagination controls sit at the bottom.

### Expected Output

```
+----+----------------+---------------------+--------+
| ID | Name           | Email               | Role   |
+----+----------------+---------------------+--------+
| 1  | Alice Johnson  | alice@example.com   | Admin  |
| 2  | Bob Smith      | bob@example.com     | Editor |
+----+----------------+---------------------+--------+
[←] [1] [2] [→]   Search: 🔍 Search…
```

The UI will adapt when you type into the search box or click column headers to sort.

## Common Variations & Edge Cases

### Loading Data Asynchronously

If your data lives on a server, replace the static `data` array with a function that returns a Promise:

```js
const config = {
  columns: ['ID', 'Name', 'Email', 'Role'],
  data: () => fetch('/api/users')
                .then(res => res.json())
                .then(users => users.map(u => [u.id, u.name, u.email, u.role])),
  pagination: { limit: 10 },
  search: true,
  sort: true
};
```

Gridjs will display a loading spinner until the promise resolves, then render the table automatically.

### Custom Cell Rendering

Sometimes you need icons, buttons, or formatted dates inside cells. Use the `formatter` property on a column:

```js
{
  name: 'Role',
  formatter: (cell) => {
    const color = cell === 'Admin' ? 'red' : 'gray';
    return gridjs.h('span', { style: { color } }, cell);
  }
}
```

The `gridjs.h` helper creates virtual DOM elements without pulling in React.

### Multiple Grids on One Page

Just repeat steps 2‑5 with different container IDs:

```html
<div id="usersGrid"></div>
<div id="ordersGrid"></div>

<script>
  const usersGrid = new gridjs.Grid(document.getElementById('usersGrid'), usersConfig);
  const ordersGrid = new gridjs.Grid(document.getElementById('ordersGrid'), ordersConfig);
  usersGrid.render();
  ordersGrid.render();
</script>
```

Each grid operates independently, so you can mix pagination limits, column sets, and even themes.

## Pro Tips & Pitfalls to Avoid

- **Don’t forget the CSS** – without the stylesheet the table will appear as a plain HTML table, losing all the nice styling and pagination controls.
- **Avoid duplicate IDs** – each **gridjs container** must have a unique ID; otherwise Gridjs will overwrite the first instance.
- **Watch the data shape** – the number of columns must match the number of cells in each row; mismatched arrays cause silent layout glitches.
- **Use `gridjs.h` for complex cells** – trying to inject raw HTML strings can break the virtual DOM diffing algorithm.
- **Mind the version** – the CDN link above points to the latest 5.x release (as of June 2026). If you lock to an older version, some options (like `language`) might be missing.

## Full Working Example (Copy‑Paste)

Below is the complete HTML file you can save as `gridjs-demo.html` and open directly in a browser.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to Create Gridjs Example</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <!-- Gridjs container -->
  <div id="grid"></div>

  <!-- Gridjs library -->
  <script


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Aspose.Cells for Java&#58; How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Create and Merge Excel Workbooks Using Aspose.Cells for Java | Complete Guide](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}