---
category: general
date: 2026-05-30
description: Learn how to create GridJsOptions instance and configure grid options
  JavaScript for dynamic tables. Step‑by‑step guide with full code.
draft: false
keywords:
- create gridjsoptions instance
- configure grid options javascript
- gridjs initialization
- javascript data grid settings
- dynamic table configuration
language: en
og_description: Create GridJsOptions instance and configure grid options JavaScript
  in minutes. Full example, explanations, and best‑practice tips.
og_title: Create GridJsOptions Instance – Configure Grid Options JavaScript
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
title: Create GridJsOptions Instance – Configure Grid Options JavaScript
url: /net/link-and-configuration-operations/create-gridjsoptions-instance-configure-grid-options-javascr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create GridJsOptions Instance – Configure Grid Options JavaScript

Ever wondered how to **create GridJsOptions instance** without hunting through scattered docs? You’re not the only one. When you need a slick, sortable table on a web page, mastering how to configure grid options JavaScript is the first step toward a polished UI.

In this tutorial we’ll walk through the exact code you need, explain why each setting matters, and show you a complete, runnable example. By the end you’ll be comfortable creating GridJsOptions instance, tweaking alignment, pagination, and even custom cell renderers—all with plain JavaScript.

## What You’ll Learn

- How to **create GridJsOptions instance** from scratch.
- The key properties that let you **configure grid options JavaScript** (sorting, pagination, number formatting, etc.).
- Common pitfalls (e.g., mixing string and numeric types) and how to avoid them.
- A full HTML page you can copy‑paste into any project and see results instantly.

### Prerequisites

- A modern browser (Chrome, Edge, Firefox) – no build tools required.
- Basic familiarity with JavaScript (variables, objects, DOM).
- The Grid.js library (we’ll pull it from a CDN).

If any of those sound unfamiliar, don’t panic—each step includes a quick refresher.

---

## Step 1: Load Grid.js and Prepare the HTML Skeleton

Before we can **create GridJsOptions instance**, we need the library itself. The easiest way is to use the official CDN. Below is a minimal HTML skeleton that also reserves a `<div>` where the grid will render.

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

> **Pro tip:** Keep the CSS link before your own styles so the grid’s default theme loads correctly.

### Why this matters

Loading the library from a CDN ensures you always get the latest stable version without a local install. The `<div id="grid-wrapper">` is the placeholder that the Grid.js constructor will target once we **configure grid options JavaScript**.

---

## Step 2: Create a New GridJsOptions Instance

Now comes the heart of the tutorial: the line that actually **creates GridJsOptions instance**. In a separate file called `grid-config.js` (referenced in the HTML above) we’ll write:

```javascript
// grid-config.js

// Step 2: Create a new GridJsOptions instance to configure grid behavior
const gridOptions = new GridJsOptions();
```

That single line gives you a clean object you can start populating with settings. Think of `gridOptions` as the control panel for every feature you’ll later enable.

### What you’re configuring

- **NumberFormatAlignment** – aligns numeric strings automatically.
- **Pagination** – controls page size and navigation.
- **Sorting** – toggles column sorting.
- **Columns** – defines headers, data types, and custom renderers.

You can add any of these properties before you finally instantiate the Grid itself.

---

## Step 3: Enable Number Alignment (A Common Requirement)

Most tables contain a mix of text and numbers. By default Grid.js aligns everything left, which looks odd for monetary values. To **configure grid options JavaScript** for proper alignment, set the `NumberFormatAlignment` flag:

```javascript
// Enable left/right alignment for numeric strings
gridOptions.NumberFormatAlignment = true;
```

Why enable this? When the flag is true, Grid.js inspects each cell; if it looks like a number (e.g., “1234”, “12.34%”), it automatically right‑aligns it. This tiny tweak makes reports far more readable.

---

## Step 4: Add Pagination and Sorting

A real‑world grid rarely fits on a single screen. Let’s turn on pagination (10 rows per page) and allow users to sort any column.

```javascript
gridOptions.Pagination = {
  limit: 10,          // rows per page
  enabled: true
};

gridOptions.Sort = true;   // enables click‑to‑sort on all columns
```

### Edge‑case note

If you later supply a custom data source that already returns paginated results, you’ll want to disable Grid.js’s built‑in pagination to avoid double‑paging. Simply set `gridOptions.Pagination.enabled = false;`.

---

## Step 5: Define Columns and Sample Data

Now we’ll feed the grid some mock data and tell it what each column represents. This is where the **create gridjsoptions instance** pattern really shines—everything lives in one tidy object.

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

Notice we keep the column `id` values identical to the keys in each data object. This convention lets Grid.js map values automatically, saving you from writing a custom formatter for every column.

---

## Step 6: Instantiate the Grid with Our Options

We finally **configure grid options javascript** by passing the `gridOptions` object to the Grid constructor. The grid will render inside the `<div id="grid-wrapper">` we prepared earlier.

```javascript
// Create the Grid instance using the previously built options
const grid = new Grid(gridOptions);

// Render the grid into the page
grid.render(document.getElementById("grid-wrapper"));
```

That’s it. The whole process—from **create gridjsoptions instance** to rendering—takes less than a minute of coding.

### Expected Output

When you open the HTML file in a browser you should see:

- A header row with “ID”, “Employee”, “Salary ($)”, “Dept.”.
- Right‑aligned salary numbers (thanks to `NumberFormatAlignment`).
- Pagination controls at the bottom (if you added more than ten rows).
- Clickable column headers that sort ascending/descending.

If anything looks off, open the browser console (F12) and look for error messages—most bugs stem from mismatched column IDs or missing library scripts.

---

## Step 7: Advanced Tweaks (Optional)

Below are a few quick ideas you can experiment with once the basic grid works.

| Feature | How to enable | Why it helps |
|---------|---------------|--------------|
| **Custom cell renderer** | `gridOptions.Columns[2].formatter = (cell) => \`<b>$${cell}</b>\`;` | Highlight salaries in bold. |
| **Search bar** | `gridOptions.Search = true;` | Lets users filter rows instantly. |
| **Server‑side data** | Set `gridOptions.Server = { url: "/api/employees", then: data => data.items };` | Scales to thousands of rows. |
| **Theme switching** | Add `gridOptions.ClassName = "gridjs-theme-dark";` | Matches dark‑mode designs. |

Feel free to mix and match—Grid.js is deliberately flexible. Just remember to keep the original **create gridjsoptions instance** line at the top; all later tweaks rely on that single object.

---

## Conclusion

We’ve just walked through a complete workflow to **create GridJsOptions instance** and **configure grid options JavaScript** for a functional, sortable, and paginated data table. Starting with a plain HTML page, we loaded the library, built an options object, enabled numeric alignment, added pagination, defined columns, and finally rendered the grid.

From here you can:

- Replace the static `sampleData` with an AJAX call.
- Add custom formatters for dates, currencies, or icons.
- Integrate the grid into a framework like React or Vue (the same `gridOptions` object works there too).

The possibilities are practically endless, and the pattern we used—centralizing all settings in a single `GridJsOptions` instance—keeps your code clean and maintainable.

Got a use‑case you’re unsure about? Drop a comment, and we’ll explore it together. Happy coding, and enjoy building dynamic tables with Grid.js!


## What Should You Learn Next?

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [How to Create and Style Excel Tables Using Aspose.Cells for .NET | Step‑By‑Step Guide](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}