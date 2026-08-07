---
category: general
date: 2026-06-21
description: Create interactive data grid using Grid.js and learn how to display JSON
  data table with sorting, pagination, and search. Perfect for web dashboards.
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: en
og_description: Create interactive data grid in minutes. Learn how to use Grid.js
  to display JSON data table with pagination, sorting, and search.
og_title: Create Interactive Data Grid with Grid.js – Complete Tutorial
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
title: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
url: /python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide

Ever wondered how to **create interactive data grid** that lets users sort, search, and page through rows without writing a backend? You're not alone. In many dashboards the biggest pain point is turning a static JSON dump into a slick, searchable table—something that feels as smooth as a spreadsheet but runs entirely in the browser.

In this tutorial we’ll walk through **how to use Grid.js** to **display JSON data table** on a plain HTML page. By the end you’ll have a working example that you can drop into any project, plus tips for customizing the toolbar, handling large data sets, and avoiding common pitfalls.

## What You’ll Learn

- How to fetch a JSON file that defines columns and rows.
- How to initialise **Grid.js** with pagination, sorting, searching, and a custom toolbar.
- How to render the grid into a target container.
- Optional tweaks: custom cell formatting, theme switching, and error handling.
- A complete, copy‑and‑paste‑ready code sample.

### Prerequisites

Before we dive in, make sure you have:

1. A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
2. A local or remote folder containing a `grid_data.json` file (we’ll show the format).
3. Basic familiarity with HTML and JavaScript – nothing fancy, just the ability to open a `.html` file in a browser.

No build tools, no npm install, no server‑side code. That’s the beauty of **create interactive data grid** with Grid.js: it works straight from a CDN.

---

## Step 1: Prepare the JSON That Defines Your Table

The first thing you need is a JSON payload that tells Grid.js what columns exist and what rows to show. Think of it as the blueprint for your **display JSON data table**. Here’s a minimal example you can save as `grid_data.json` in the same directory as your HTML file:

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

*Why this format?* Grid.js expects `columns` to be an array of strings (or objects for advanced configuration) and `rows` to be an array of arrays where each inner array matches the column order. You can, of course, add more columns or nested objects – Grid.js will render them as long as the shapes line up.

> **Pro tip:** If you’re pulling data from an API, just replace the static `fetch('grid_data.json')` with your endpoint URL. The rest of the code stays the same.

---

## Step 2: Initialise Grid.js – The Heart of **how to use gridjs**

Now that the data source is ready, we need to bring Grid.js onto the page and tell it how to behave. This is where we actually **create interactive data grid** functionality like pagination, sorting, and a handy toolbar button.

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

The CDN gives you the latest stable version, and the Meri­maid theme adds a clean, modern look out of the box. You could swap it for `gridjs.min.css` if you prefer the default styling.

Next, inside a `<script>` tag, fetch the JSON and initialise the grid:

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

### Breaking Down the Options

| Option | What It Does | Why It Matters |
|--------|--------------|----------------|
| `pagination` | Splits rows into pages (default 10 per page) | Keeps large tables usable without overwhelming the UI. |
| `sort` | Clickable column headers toggle ascending/descending order | Users can quickly find the highest‑value rows. |
| `search` | Adds a text input that filters rows on the fly | Great for ad‑hoc lookups without reloading data. |
| `toolbar` | Adds custom buttons or dropdowns above the grid | Perfect for “Help”, “Export”, or “Refresh” actions. |
| `formatter` | Lets you return raw HTML for a cell | Here we turn email strings into clickable mailto links. |

> **Why this approach?** By keeping the grid configuration declarative, you can easily tweak behaviour without touching the core rendering logic. This is the recommended way to **how to use Grid.js** for most projects.

---

## Step 3: Render the Grid Into Your Page

The last line of the script—`grid.render(document.getElementById('grid-container'))`—injects the fully‑functional table into a `<div>` you’ve placed somewhere in your HTML body:

```html
<div id="grid-container"></div>
```

That’s it. When the page loads, the browser fetches the JSON, builds the Grid.js instance, and paints the interactive table onto the screen. No refreshes, no server calls after the initial load.

---

## Optional: Styling and Theme Tweaks

If the default Meri­maid theme isn’t your cup of tea, you can swap it for any of the built‑in themes (`gridjs.min.css`) or write your own CSS. For example, to make the header background a soft gray:

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

Add the snippet inside a `<style>` tag or an external stylesheet. Grid.js respects standard CSS selectors, so you have full control over fonts, colors, and spacing.

---

## Common Pitfalls & How to Avoid Them

| Pitfall | Symptom | Fix |
|---------|---------|-----|
| **CORS errors** when fetching JSON from another domain | Browser console shows “Blocked by CORS policy” | Host the JSON on the same origin or enable CORS on the server. |
| **Large data sets cause lag** | Scrolling becomes choppy, pagination slow | Use `server` pagination (`pagination: { server: { url: (prev, page, limit) => … } }`) or lazy‑load rows. |
| **Toolbar button doesn’t appear** | No button visible despite `toolbar.enabled: true` | Ensure you’re using Grid.js version 2.0+; older versions had a different toolbar API. |
| **Email links not clickable** | Formatter returns plain text | Return `gridjs.html(...)` instead of a plain string, as shown in the example. |

Addressing these issues early saves you hours of debugging later.

---

## Full Working Example (Copy‑Paste Ready)

Below is the complete HTML file that you can save as `index.html`. Open it in a browser, and you’ll see a fully functional **create interactive data grid** demo that **display JSON data table** with sorting, searching, and a help button.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Create Interactive Data Grid with Grid.js</title>
  <!-- Grid.js core library -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <!-- Optional theme – Meri­maid -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Simple custom styling */
    body { font-family: Arial, sans-serif; margin: 20px; }
    .gridjs-container { max-width: 900px; margin: auto; }
    .gridjs-th { background-color: #f0f8ff; }
  </style>
</head>
<body>
  <h1>Create Interactive Data Grid with Grid.js</h1>
  <p>This page demonstrates how to <strong>display JSON data table</strong> using Grid.js. Feel free to edit <code>grid_data.json</code> and refresh.</p>

  <!-- Grid will be rendered here -->
  <div id="grid-container"></div>

  <script>
    // Load JSON data and initialise Grid.js
    fetch('grid_data.json')
      .then(r => r.json())
      .then(data => {
        const grid = new gridjs.Grid({
          columns: data.columns.map(col => {
            // Custom formatter for Email column
            if (col === 'Email') {
              return {
                name: col,
                formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
              };
            }
            return col;
          }),
          data: data.rows,
          pagination: { enabled: true, limit: 5 },
          sort: true,
          search: true,
          toolbar: {
            enabled: true,
            items: [
              {
                type: 'button',
                text: 'Formula Help',
                onClick: () => alert('Hover over a cell to see its formula description.')
              }
            ]
          }
        });

        // Render the grid
        grid.render(document.getElementById('grid-container'));
      })
      .catch(err => console.error('Error loading grid data:', err));
  </script>
</body>
</html


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create an Excel Data Validation List with Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [How to Create Checkboxes in Excel using Aspose.Cells for .NET | Data Validation Tutorial](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [Create & Import XML Data into Excel Using Aspose.Cells for Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}