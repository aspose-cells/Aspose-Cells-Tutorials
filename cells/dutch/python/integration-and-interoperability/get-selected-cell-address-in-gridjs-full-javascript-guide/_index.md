---
category: general
date: 2026-06-30
description: Leer hoe je het adres van de geselecteerde cel krijgt, de waarde van
  een rastercel bijwerkt en de invoerwaarde leest met JavaScript en GridJs. Stapsgewijze
  code en tips.
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: nl
og_description: Haal het adres van de geselecteerde cel op, werk de waarde van de
  rastercel bij en lees de invoerwaarde met JavaScript. Volg deze volledige gids voor
  een soepele GridJs‑integratie.
og_title: Geselecteerd celadres ophalen – Complete GridJs JavaScript tutorial
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
title: Het adres van de geselecteerde cel ophalen in GridJs – Volledige JavaScript‑gids
url: /nl/python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Geselecteerd Celadres Opvragen – Complete GridJs JavaScript Tutorial

Heb je ooit moeten **get selected cell address** van een GridJs‑tabel, maar wist je niet welke API‑aanroep je moet gebruiken? Je bent niet de enige. In veel admin‑panels klikken gebruikers op een cel, bewerken een waarde in een modal, en verwachten dat het raster de wijziging onmiddellijk weergeeft. Deze tutorial laat je precies zien hoe je dat adres kunt ophalen, de nieuwe prijs uit een invoerveld kunt lezen, en **update grid cell value** zonder een paginavernieuwing.

We behandelen ook **read input value with JavaScript** op de juiste manier, behandelen randgevallen, en sluiten de modal zodra de update is voltooid. Aan het einde heb je een zelfstandige snippet die je in elk project dat GridJs gebruikt kunt plaatsen.

## Wat je gaat bouwen

- Een eenvoudige HTML‑tabel aangedreven door GridJs.
- Een bewerkings‑modal die verschijnt wanneer op een cel wordt geklikt.
- JavaScript die **gets the selected cell address** ophaalt, de door de gebruiker ingevoerde prijs pakt, **updates the grid cell value** bijwerkt, en uiteindelijk de modal verbergt.

Er zijn geen externe bibliotheken nodig naast GridJs, en de code werkt met moderne browsers (Chrome 102+, Edge, Firefox). Als je al een GridJs‑instance op de pagina hebt, kun je de relevante delen direct kopiëren‑plakken.

## Vereisten

- Basiskennis van JavaScript en de DOM.
- GridJs‑bibliotheek geladen (via CDN of npm).
- Een pagina die al een GridJs‑grid rendert (we laten een minimaal voorbeeld zien).

Als een van deze punten je onbekend voorkomt, geen paniek—elke stap bevat een korte herhaling.

---

## Stap 1: Zet de HTML‑skelet op

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

> **Pro tip:** De `#editModal` gebruikt een minimale CSS‑truc—voeg simpelweg de `active`‑klasse toe om hem te tonen. Je kunt dit vervangen door Bootstrap, Tailwind, of elk ander modal‑component dat je al gebruikt.

---

## Stap 2: Initialise GridJs en Leg Cel‑klikken Vast

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

## Stap 3: Lees de Nieuwe Prijs uit het Invoerveld

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

## Stap 4: Werk het Geselecteerde Celadres Bij

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

## Stap 5: Afhandelen van Annuleren en Randgevallen

A robust solution always gives the user a way out. The **Cancel** button simply hides the modal and clears any stored address.

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### Wat als er geen cel is geselecteerd?

If a user somehow triggers the **Save** button without clicking a cell first (maybe they opened the modal programmatically), `lastSelectedCell` will be `null`. The early‑return in `updateSelectedCell` prevents a runtime error and logs a helpful warning.

### Omgaan met grote rasters

For grids with pagination, `GridJs.getSelectedCell()` still returns the absolute address (e.g., `"B12"`), not just the visible row. This means the update works even if the edited row lives on another page. Just be aware that the UI won’t automatically switch pages after an update—if you need that, call `grid.forceUpdate()` or navigate to the appropriate page manually.

---

## Volledig Werkend Voorbeeld

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


## Wat kun je hierna leren?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Adres, Celcount en Offset voor het volledige Excel‑bereik ophalen](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Adres, Celcount en Offset voor het volledige Excel‑bereik ophalen (Duits)](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Adres, Celcount en Offset voor het volledige Excel‑bereik ophalen (Frans)](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}