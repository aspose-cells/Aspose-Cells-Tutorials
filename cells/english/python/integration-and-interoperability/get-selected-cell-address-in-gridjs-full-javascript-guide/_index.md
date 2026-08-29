---
category: general
date: 2026-06-30
description: Learn how to get selected cell address, update grid cell value and read
  input value with JavaScript using GridJs. Step‑by‑step code and tips.
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: en
og_description: Get selected cell address, update grid cell value and read input value
  with JavaScript. Follow this complete guide for a smooth GridJs integration.
og_title: Get Selected Cell Address – Complete GridJs JavaScript Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Learn how to get selected cell address, update grid cell value and
    read input value with JavaScript using GridJs. Step‑by‑step code and tips.
  headline: Get Selected Cell Address in GridJs – Full JavaScript Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- DOM manipulation
title: Get Selected Cell Address in GridJs – Full JavaScript Guide
url: /python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Get Selected Cell Address – Complete GridJs JavaScript Tutorial

Ever needed to **get selected cell address** from a GridJs table but weren’t sure which API call to use? You’re not the only one. In many admin panels, users click a cell, edit a value in a modal, and expect the grid to reflect the change instantly. This tutorial shows you exactly how to retrieve that address, read the new price from an input field, and **update grid cell value** without a page reload.

We’ll also cover **read input value with JavaScript** the right way, handle edge cases, and close the modal once the update finishes. By the end you’ll have a self‑contained snippet you can drop into any project that uses GridJs.

## What You’ll Build

- A simple HTML table powered by GridJs.
- An editing modal that appears when a cell is clicked.
- JavaScript that **gets the selected cell address**, grabs the user‑typed price, **updates the grid cell value**, and finally hides the modal.

No external libraries beyond GridJs are required, and the code works with modern browsers (Chrome 102+, Edge, Firefox). If you already have a GridJs instance on the page, you can copy‑paste the relevant parts directly.

## Prerequisites

- Basic knowledge of JavaScript and the DOM.
- GridJs library loaded (via CDN or npm).
- A page that already renders a GridJs grid (we’ll show a minimal example).

If any of those sound unfamiliar, don’t panic—each step includes a quick recap.

---

## Step 1: Set Up the HTML Skeleton

First, lay out the table container, the hidden modal, and the price input. The modal will be toggled with simple CSS classes.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>GridJs Edit Example</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Quick modal styling – feel free to replace with your UI framework */
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script src="script.js"></script>
</body>
</html>
```

> **Pro tip:** The `#editModal` uses a minimal CSS trick—just add the `active` class to show it. You can swap this for Bootstrap, Tailwind, or any modal component you already use.

---

## Step 2: Initialise GridJs and Capture Cell Clicks

Now we’ll create a grid with sample data and listen for cell selections. When a user clicks a cell, we’ll **get the selected cell address** and open the modal.

```javascript
// script.js
const grid = new gridjs.Grid({
  columns: ['Item', 'Quantity', 'Price'],
  data: [
    ['Apple', 10, 0.5],
    ['Banana', 5, 0.3],
    ['Cherry', 20, 0.2]
  ],
  pagination: { limit: 5 },
  sort: true,
  // Enable cell selection – GridJs provides a helper for this
  style: {
    table: {
      'width': '100%'
    }
  }
}).render(document.getElementById('grid'));

// Helper to store the address of the last clicked cell
let lastSelectedCell = null;

// GridJs emits a 'cell' event when any cell is clicked
grid.on('cell', (event) => {
  // Step 2a: Get selected cell address
  const address = GridJs.getSelectedCell(); // <-- primary operation
  lastSelectedCell = address; // remember for later update

  // Show the modal
  document.getElementById('editModal').classList.add('active');

  // Optional: pre‑fill the input with the current cell value
  const currentValue = event.target.innerText;
  document.getElementById('price').value = currentValue;
});
```

> **Why this works:** `GridJs.getSelectedCell()` returns a string like `"C2"` (column C, row 2). Storing it in `lastSelectedCell` lets us reference the exact location when we later **update grid cell value**.

---

## Step 3: Read the New Price from the Input Field

When the user clicks **Save**, we need to **read input value with JavaScript** safely. This step also validates that the entered price is a positive number.

```javascript
document.getElementById('saveBtn').addEventListener('click', () => {
  // Step 3a: Grab the raw string from the input
  const raw = document.getElementById('price').value;

  // Step 3b: Convert to a number and validate
  const newPrice = parseFloat(raw);
  if (isNaN(newPrice) || newPrice < 0) {
    alert('Please enter a valid positive number.');
    return;
  }

  // Proceed to update the cell
  updateSelectedCell(newPrice);
});
```

> **Note:** Using `parseFloat` ensures we accept decimals (e.g., `1.99`). The `isNaN` guard prevents accidental empty submissions.

---

## Step 4: Update the Selected Cell Value

Now we finally **update grid cell value** using the address we captured earlier. GridJs’s `updateCell` method returns a promise, so we can chain a modal‑close action.

```javascript
function updateSelectedCell(value) {
  if (!lastSelectedCell) {
    console.warn('No cell selected – nothing to update.');
    return;
  }

  // Step 4a: Call GridJs.updateCell(address, newValue)
  GridJs.updateCell(lastSelectedCell, value)
    .then(() => {
      // Step 4b: Close the modal once the grid refreshes
      document.getElementById('editModal').classList.remove('active');
      // Reset stored address
      lastSelectedCell = null;
    })
    .catch(err => {
      console.error('Failed to update cell:', err);
      alert('Could not save the new price. Try again.');
    });
}
```

> **Why use a promise?** GridJs may need to re‑render the table or sync with a backend. By waiting for the promise we guarantee the UI only hides after the grid reflects the new value.

---

## Step 5: Handle Cancel and Edge Cases

A robust solution always gives the user a way out. The **Cancel** button simply hides the modal and clears any stored address.

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### What If No Cell Is Selected?

If a user somehow triggers the **Save** button without clicking a cell first (maybe they opened the modal programmatically), `lastSelectedCell` will be `null`. The early‑return in `updateSelectedCell` prevents a runtime error and logs a helpful warning.

### Dealing with Large Grids

For grids with pagination, `GridJs.getSelectedCell()` still returns the absolute address (e.g., `"B12"`), not just the visible row. This means the update works even if the edited row lives on another page. Just be aware that the UI won’t automatically switch pages after an update—if you need that, call `grid.forceUpdate()` or navigate to the appropriate page manually.

---

## Complete Working Example

Below is the full code you can copy‑paste into a single HTML file. Open it in a browser, click any cell, change the price, and watch the grid update instantly.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Get Selected Cell Address – GridJs Demo</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal" aria-modal="true" role="dialog">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script>
  // Initialise the grid
  const grid = new gridjs.Grid({
    columns: ['Item', 'Quantity', 'Price'],
    data: [
      ['Apple', 10, 0.5],
      ['Banana', 5, 0.3],
      ['Cherry', 20, 0.2]
    ],
    pagination: { limit: 5 },
    sort: true
  }).render(document.getElementById('grid'));

  let lastSelectedCell = null;

  // Capture cell clicks – this is where we **get selected cell address**
  grid.on('cell', (event) => {
    const address = GridJs.getSelectedCell();   // primary keyword usage
    lastSelectedCell = address;
    document.getElementById('editModal').classList.add('active');
    document.getElementById('price').value = event.target.innerText;
  });

  // Save button – **read input value with JavaScript**
  document.getElementById('saveBtn').addEventListener('click', () => {
    const raw = document.getElementById('price').value;
    const newPrice = parseFloat(raw);
    if (isNaN(newPrice) || newPrice < 0) {
      alert('Please enter a valid positive number.');
      return;
    }
    updateSelectedCell(newPrice);
  });

  // Core update logic – **update grid cell value**
  function updateSelectedCell(value) {
    if (!lastSelectedCell) {
      console.warn('No cell selected – nothing to update.');
      return;
    }
    GridJs.updateCell(lastSelectedCell, value)
      .then(() => {
        document.getElementById('editModal').classList


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Get Address, Cell Count, and Offset for Entire Excel Range](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Get Address Cell Count And Offset For Entire Excel Range](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Get Address Cell Count And Offset For Entire Excel Range](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}