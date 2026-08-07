---
category: general
date: 2026-07-03
description: Learn how to render Gridjs in minutes with a full HTML/JS example. Includes
  Gridjs library CDN, lazy loading, and configuration JSON tips.
draft: false
keywords:
- how to render gridjs
- gridjs configuration JSON
- gridjs lazy loading
- gridjs library CDN
- gridjs render method
language: en
og_description: 'How to render Gridjs quickly: use the CDN, fetch a configuration
  JSON, and call the render method. Perfect for dynamic data tables.'
og_title: How to Render Gridjs – Complete Implementation Guide
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to render Gridjs in minutes with a full HTML/JS example.
    Includes Gridjs library CDN, lazy loading, and configuration JSON tips.
  headline: How to Render Gridjs – Step‑by‑Step Guide for Dynamic Tables
  type: TechArticle
- description: Learn how to render Gridjs in minutes with a full HTML/JS example.
    Includes Gridjs library CDN, lazy loading, and configuration JSON tips.
  name: How to Render Gridjs – Step‑by‑Step Guide for Dynamic Tables
  steps:
  - name: Why Use the CDN?
    text: '- **Performance:** Browsers cache the file across sites, so returning visitors
      may already have it. - **Simplicity:** No bundler configuration, just a single
      `<script>` tag. - **Lazy loading:** You can defer the script with `defer` or
      load it only when needed, which ties into our next step.'
  - name: Breaking Down the Code
    text: '| Line | What It Does | Why It Matters | |------|--------------|----------------|
      | `fetch(''YOUR_DIRECTORY/lazygrid.json'')` | Retrieves the configuration JSON
      via HTTP GET. | Keeps the HTML clean and allows you to change the grid layout
      without touching the page code. | | `.then(response => response'
  - name: Sample `lazygrid.json`
    text: Below is a minimal yet functional configuration file. Save it as `lazygrid.json`
      in the same directory as your HTML (or adjust the fetch path accordingly).
  - name: 1. Using Custom Render Functions
    text: 'Sometimes you need to format a cell—say, add a badge for ages over 28.
      Extend the column definition:'
  - name: 2. Server‑Side Pagination
    text: If your dataset is huge, fetching the entire JSON can be slow. Gridjs supports
      server‑side pagination—just set `pagination.server` to `true` and implement
      an API endpoint that returns slices of data based on `page` and `limit` query
      parameters.
  - name: 3. Styling with CSS Variables
    text: 'The Mermaid theme uses CSS variables for colors. Override them in a `<style>`
      block:'
  - name: 4. Accessibility Considerations
    text: Gridjs adds ARIA attributes automatically, but you can enhance keyboard
      navigation by ensuring your placeholder `<div>` is focusable (`tabindex="0"`).
      This helps screen‑reader users interact with the table.
  type: HowTo
tags:
- JavaScript
- Front‑end
- Data Tables
title: How to Render Gridjs – Step‑by‑Step Guide for Dynamic Tables
url: /python/import-and-export/how-to-render-gridjs-step-by-step-guide-for-dynamic-tables/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Render Gridjs – Step‑by‑Step Guide for Dynamic Tables

Ever wondered **how to render Gridjs** on a plain HTML page without pulling in a heavyweight framework? You’re not alone. Many developers need a lightweight, sortable table that can be fed data from a JSON file, and Gridjs makes that a piece of cake. In this tutorial we’ll walk through every line you need, from loading the Gridjs library CDN to lazily fetching a configuration JSON and finally calling the render method.

We’ll also sprinkle in a few best‑practice tips—like why lazy loading the Gridjs configuration can improve page speed, and how to structure your JSON so the Gridjs render method works flawlessly. By the end you’ll have a fully functional grid you can drop into any project.

## What You’ll Build

- A minimal HTML page that pulls Gridjs from a CDN  
- A `lazygrid.json` file that defines columns, data, and optional plugins  
- JavaScript that fetches the JSON, creates a Gridjs instance, and renders it into a placeholder  

No build tools, no npm, just plain HTML and a bit of vanilla JS. Perfect for static sites, documentation portals, or quick prototypes.

## Prerequisites

- Basic understanding of HTML and JavaScript (no frameworks required)  
- A web server or local dev environment that can serve static files (e.g., VS Code Live Server)  
- The `lazygrid.json` file placed somewhere accessible to the browser  

If you’re comfortable with these, let’s dive in.

## Step 1: Include the Gridjs Library CDN

The fastest way to get Gridjs on the page is to reference its UMD bundle from a CDN. This eliminates the need for npm installs and keeps the tutorial lightweight.

```html
<!-- Step 1: Include the Gridjs library -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
```

> **Pro tip:** The `theme/mermaid.min.css` stylesheet adds a clean, modern look. Swap it for another theme if you prefer a different style.

### Why Use the CDN?

- **Performance:** Browsers cache the file across sites, so returning visitors may already have it.  
- **Simplicity:** No bundler configuration, just a single `<script>` tag.  
- **Lazy loading:** You can defer the script with `defer` or load it only when needed, which ties into our next step.

## Step 2: Add a Placeholder Element for the Grid

Gridjs needs a DOM node to mount the table. Create a `<div>` with a unique ID—this is where the Gridjs render method will inject the table markup.

```html
<!-- Step 2: Placeholder where Gridjs will appear -->
<div id="grid"></div>
```

You can style this container with CSS if you need custom widths or margins. For now, the default styling from the theme will keep things tidy.

## Step 3: Load a Gridjs Configuration JSON and Render the Grid

Here’s where the magic happens. We’ll fetch a JSON file (`lazygrid.json`) that describes the columns, data rows, and any plugins you want. Then we’ll instantiate Gridjs with that configuration and call its render method.

```html
<!-- Step 3: Fetch config and render Gridjs -->
<script>
  // Step 3.1: Pull the JSON config (replace the path as needed)
  fetch('YOUR_DIRECTORY/lazygrid.json')
    .then(response => {
      if (!response.ok) {
        throw new Error('Network response was not ok');
      }
      return response.json();
    })
    .then(config => {
      // Step 3.2: Create a Gridjs instance using the fetched configuration
      const grid = new GridJs(config);
      // Step 3.3: Render the grid inside the placeholder element
      grid.render(document.getElementById('grid'));
    })
    .catch(error => console.error('Error loading Gridjs config:', error));
</script>
```

### Breaking Down the Code

| Line | What It Does | Why It Matters |
|------|--------------|----------------|
| `fetch('YOUR_DIRECTORY/lazygrid.json')` | Retrieves the configuration JSON via HTTP GET. | Keeps the HTML clean and allows you to change the grid layout without touching the page code. |
| `.then(response => response.json())` | Parses the response into a JavaScript object. | Guarantees you’re passing a proper object to Gridjs. |
| `new GridJs(config)` | Constructs a Gridjs instance with the supplied config. | This is the **gridjs render method** entry point; the config drives columns, data, and plugins. |
| `grid.render(document.getElementById('grid'))` | Inserts the table into the `<div id="grid">`. | The final step that actually **renders Gridjs** on screen. |
| `.catch(...)` | Handles network or parsing errors gracefully. | Prevents the page from breaking silently and gives you debugging info. |

### Sample `lazygrid.json`

Below is a minimal yet functional configuration file. Save it as `lazygrid.json` in the same directory as your HTML (or adjust the fetch path accordingly).

```json
{
  "columns": [
    "Name",
    "Email",
    { "id": "age", "name": "Age", "type": "number" }
  ],
  "data": [
    ["Alice", "alice@example.com", 30],
    ["Bob", "bob@example.com", 25],
    ["Carol", "carol@example.com", 27]
  ],
  "search": true,
  "pagination": {
    "enabled": true,
    "limit": 5
  }
}
```

- **gridjs configuration JSON**: The `columns` array can contain simple strings or objects for more control (e.g., custom renderers).  
- **gridjs lazy loading**: By storing this JSON separately, you can swap it out without redeploying the HTML page.  
- **gridjs render method**: The `grid.render(...)` call reads this config and builds the table dynamically.

## Step 4: Verify the Output

Open the HTML file in a browser. You should see a searchable, paginated table that matches the data in `lazygrid.json`. The default Mermaid theme adds subtle shading and hover effects.

**Expected output:**

| Name  | Email               | Age |
|-------|---------------------|-----|
| Alice | alice@example.com   | 30  |
| Bob   | bob@example.com     | 25  |
| Carol | carol@example.com   | 27  |

If you don’t see the table:

1. Open the browser console (F12) and look for errors.  
2. Ensure the path in `fetch('YOUR_DIRECTORY/lazygrid.json')` points to the correct location.  
3. Confirm the CDN script loaded (check the Network tab).  

## Advanced Tips & Edge Cases

### 1. Using Custom Render Functions

Sometimes you need to format a cell—say, add a badge for ages over 28. Extend the column definition:

```json
{
  "id": "age",
  "name": "Age",
  "formatter": (cell) => {
    return cell > 28 ? `<span style="color:red;">${cell}</span>` : cell;
  }
}
```

> **Note:** The formatter must be a JavaScript function, so you’d need to embed the config directly in the script or load it as a module if you want to keep it in JSON.

### 2. Server‑Side Pagination

If your dataset is huge, fetching the entire JSON can be slow. Gridjs supports server‑side pagination—just set `pagination.server` to `true` and implement an API endpoint that returns slices of data based on `page` and `limit` query parameters.

### 3. Styling with CSS Variables

The Mermaid theme uses CSS variables for colors. Override them in a `<style>` block:

```html
<style>
  :root {
    --gridjs-header-bg: #2c3e50;
    --gridjs-header-color: #ecf0f1;
  }
</style>
```

### 4. Accessibility Considerations

Gridjs adds ARIA attributes automatically, but you can enhance keyboard navigation by ensuring your placeholder `<div>` is focusable (`tabindex="0"`). This helps screen‑reader users interact with the table.

## Full Working Example

Putting everything together, here’s a single HTML file you can copy‑paste and run locally.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to Render Gridjs Demo</title>
  <!-- Gridjs library CDN -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
  <style>
    /* Optional custom theme tweaks */
    :root {
      --gridjs-header-bg: #34495e;
      --gridjs-header-color: #ecf0f1;
    }
  </style>
</head>
<body>
  <!-- Placeholder for the grid -->
  <div id="grid"></div>

  <!-- Fetch config and render Gridjs -->
  <script>
    fetch('lazygrid.json')
      .then(r => r.ok ? r.json() : Promise.reject('Failed to load'))
      .then(cfg => {
        const grid = new GridJs(cfg);
        grid.render(document.getElementById('grid'));
      })
      .catch(err => console.error(err));
  </script>

  <!-- Optional screenshot for documentation -->
  <img src="gridjs-screenshot.png" alt="Screenshot demonstrating how to render Gridjs grid" style="display:none;">
</body>
</html>
```

Save this as `index.html` next to `lazygrid.json`, open it in a browser, and watch the grid appear instantly.

## Conclusion

You now have a clear, end‑to‑end answer to **how to render Gridjs**: load the Gridjs library CDN, provide a `gridjs configuration JSON`, lazily fetch it, instantiate a Gridjs object, and call the `gridjs render method`. This approach keeps your HTML tidy, leverages lazy loading for better performance, and gives you full control over columns, data, and plugins.

What’s next? Try adding:

- **gridjs lazy loading** of large data sets via server‑side pagination.  
- Custom cell renderers for charts or progress bars.  
- Export plugins to let users download CSV or Excel files.  

Feel free to experiment, and if you hit any snags, drop a comment below. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Render Excel Sheets as Images Using Aspose.Cells .NET for Seamless Data Visualization](/cells/english/net/import-export/render-excel-sheets-images-aspose-cells-dotnet/)
- [How to Render Excel Sheets as Images Using Aspose.Cells for Java (Workbook Operations)](/cells/english/java/workbook-operations/render-excel-sheets-images-aspose-cells-java/)
- [How to Efficiently Filter Data While Loading Excel Workbooks Using Aspose.Cells in Java](/cells/english/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}