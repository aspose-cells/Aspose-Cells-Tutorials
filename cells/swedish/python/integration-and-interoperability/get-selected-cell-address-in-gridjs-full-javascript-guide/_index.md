---
category: general
date: 2026-06-30
description: Lär dig hur du får den valda cellens adress, uppdaterar cellvärdet i
  rutnätet och läser inmatningsvärdet med JavaScript och GridJs. Steg‑för‑steg‑kod
  och tips.
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: sv
og_description: Hämta den valda cellens adress, uppdatera rutnätscellens värde och
  läs inmatningsvärdet med JavaScript. Följ den här kompletta guiden för en smidig
  GridJs‑integration.
og_title: Hämta vald celladress – Komplett GridJs JavaScript‑handledning
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
title: Hämta vald celladress i GridJs – Fullständig JavaScript‑guide
url: /sv/python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hämta vald celladress – Komplett GridJs JavaScript‑handledning

Har du någonsin behövt **get selected cell address** från en GridJs‑tabell men var osäker på vilket API‑anrop du ska använda? Du är inte ensam. I många admin‑paneler klickar användare på en cell, redigerar ett värde i en modal, och förväntar sig att rutnätet omedelbart visar förändringen. Denna handledning visar exakt hur du hämtar den adressen, läser det nya priset från ett inmatningsfält, och **update grid cell value** utan att ladda om sidan.

Vi kommer också att gå igenom **read input value with JavaScript** på rätt sätt, hantera kantfall, och stänga modalen när uppdateringen är klar. I slutet har du ett självständigt kodsnutt som du kan lägga in i vilket projekt som helst som använder GridJs.

## Vad du kommer att bygga

- En enkel HTML‑tabell driven av GridJs.
- En redigeringsmodal som visas när en cell klickas.
- JavaScript som **gets the selected cell address**, hämtar det användar‑skrivna priset, **updates the grid cell value**, och slutligen döljer modalen.

Inga externa bibliotek utöver GridJs krävs, och koden fungerar i moderna webbläsare (Chrome 102+, Edge, Firefox). Om du redan har en GridJs‑instans på sidan kan du kopiera‑klistra in de relevanta delarna direkt.

## Förutsättningar

- Grundläggande kunskap om JavaScript och DOM.
- GridJs‑biblioteket laddat (via CDN eller npm).
- En sida som redan renderar ett GridJs‑rutnät (vi visar ett minimalt exempel).

Om någon av dessa känns obekant, panik inte—varje steg innehåller en snabb sammanfattning.

---

## Steg 1: Skapa HTML‑skelettet

Först, lägg ut tabellcontainern, den dolda modalen och pris‑inmatningsfältet. Modalen kommer att växlas med enkla CSS‑klasser.

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

> **Pro tip:** `#editModal` använder ett minimalt CSS‑trick—lägg bara till `active`‑klassen för att visa den. Du kan byta ut detta mot Bootstrap, Tailwind, eller någon annan modal‑komponent du redan använder.

---

## Steg 2: Initiera GridJs och fånga cellklick

Nu skapar vi ett rutnät med exempeldata och lyssnar på cellval. När en användare klickar på en cell, kommer vi att **get the selected cell address** och öppna modalen.

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

> **Why this works:** `GridJs.getSelectedCell()` returnerar en sträng som `"C2"` (kolumn C, rad 2). Att lagra den i `lastSelectedCell` låter oss referera till den exakta platsen när vi senare **update grid cell value**.

---

## Steg 3: Läs det nya priset från inmatningsfältet

När användaren klickar på **Save**, måste vi **read input value with JavaScript** på ett säkert sätt. Detta steg validerar också att det angivna priset är ett positivt tal.

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

> **Note:** Att använda `parseFloat` säkerställer att vi accepterar decimaler (t.ex. `1.99`). `isNaN`‑skyddet förhindrar oavsiktliga tomma inmatningar.

---

## Steg 4: Uppdatera den valda cellens värde

Nu uppdaterar vi äntligen **update grid cell value** med adressen vi fångade tidigare. GridJs `updateCell`‑metod returnerar ett promise, så vi kan kedja en modal‑stängningsåtgärd.

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

> **Why use a promise?** GridJs kan behöva rendera om tabellen eller synkronisera med en backend. Genom att vänta på promiset garanterar vi att UI bara döljs efter att rutnätet har reflekterat det nya värdet.

---

## Steg 5: Hantera avbryt och kantfall

En robust lösning ger alltid användaren en möjlighet att avbryta. **Cancel**‑knappen döljer helt enkelt modalen och rensar eventuell lagrad adress.

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### Vad händer om ingen cell är vald?

Om en användare på något sätt aktiverar **Save**‑knappen utan att först klicka på en cell (kanske öppnade de modalen programatiskt), blir `lastSelectedCell` `null`. Det tidiga `return`‑uttrycket i `updateSelectedCell` förhindrar ett körningsfel och loggar en hjälpsam varning.

### Hantera stora rutnät

För rutnät med paginering returnerar `GridJs.getSelectedCell()` fortfarande den absoluta adressen (t.ex. `"B12"`), inte bara den synliga raden. Detta innebär att uppdateringen fungerar även om den redigerade raden finns på en annan sida. Var dock medveten om att UI inte automatiskt byter sida efter en uppdatering—om du behöver det, anropa `grid.forceUpdate()` eller navigera till rätt sida manuellt.

---

## Komplett fungerande exempel

Nedan är hela koden som du kan kopiera‑klistra in i en enda HTML‑fil. Öppna den i en webbläsare, klicka på en cell, ändra priset, och se hur rutnätet uppdateras omedelbart.

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


## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hämta adress, cellantal och offset för hela Excel‑intervallet](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Hämta adress, cellantal och offset för hela Excel‑intervallet](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Hämta adress, cellantal och offset för hela Excel‑intervallet](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}