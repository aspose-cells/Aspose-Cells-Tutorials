---
category: general
date: 2026-06-30
description: Naučte se, jak získat adresu vybrané buňky, aktualizovat hodnotu buňky
  v gridu a načíst hodnotu vstupu pomocí JavaScriptu s GridJs. Krok za krokem kód
  a tipy.
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: cs
og_description: Získejte adresu vybrané buňky, aktualizujte hodnotu buňky v mřížce
  a načtěte hodnotu vstupu pomocí JavaScriptu. Postupujte podle tohoto kompletního
  návodu pro plynulou integraci GridJs.
og_title: Získat adresu vybrané buňky – Kompletní tutoriál GridJs JavaScript
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
title: Získat adresu vybrané buňky v GridJs – Kompletní průvodce JavaScriptem
url: /cs/python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Získání adresy vybrané buňky – Kompletní GridJs JavaScript tutoriál

Už jste někdy potřebovali **získat adresu vybrané buňky** z tabulky GridJs, ale nebyli jste si jisti, kterou API metodu použít? Nejste v tom sami. V mnoha administrativních panelech uživatelé kliknou na buňku, upraví hodnotu v modálním okně a očekávají, že se změna projeví v gridu okamžitě. Tento tutoriál vám přesně ukáže, jak tuto adresu získat, přečíst novou cenu z vstupního pole a **aktualizovat hodnotu buňky v gridu** bez nutnosti znovu načítat stránku.

Také se podíváme na **čtení hodnoty vstupu pomocí JavaScriptu** správným způsobem, ošetříme okrajové případy a po dokončení aktualizace zavřeme modální okno. Na konci budete mít samostatný úryvek kódu, který můžete vložit do libovolného projektu používajícího GridJs.

## Co vytvoříte

- Jednoduchou HTML tabulku poháněnou GridJs.
- Editační modální okno, které se zobrazí po kliknutí na buňku.
- JavaScript, který **získá adresu vybrané buňky**, načte uživatelem zadanou cenu, **aktualizuje hodnotu buňky v gridu** a nakonec skryje modální okno.

Nejsou potřeba žádné externí knihovny kromě GridJs a kód funguje v moderních prohlížečích (Chrome 102+, Edge, Firefox). Pokud již na stránce máte instanci GridJs, můžete přímo zkopírovat relevantní části.

## Předpoklady

- Základní znalost JavaScriptu a DOM.
- Načtená knihovna GridJs (přes CDN nebo npm).
- Stránka, která již vykresluje GridJs grid (ukážeme minimální příklad).

Pokud vám některý z těchto bodů není známý, nepanikařte – každý krok obsahuje stručné shrnutí.

---

## Krok 1: Nastavení HTML kostry

Nejprve vytvořte kontejner pro tabulku, skryté modální okno a vstup pro cenu. Modální okno bude přepínáno pomocí jednoduchých CSS tříd.

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

> **Tip:** `#editModal` používá minimální CSS trik – stačí přidat třídu `active`, aby se zobrazilo. Můžete to nahradit Bootstrapem, Tailwindem nebo jakoukoli komponentou modálního okna, kterou již používáte.

---

## Krok 2: Inicializace GridJs a zachycení kliknutí na buňky

Nyní vytvoříme grid s ukázkovými daty a budeme poslouchat výběr buněk. Když uživatel klikne na buňku, **získáme adresu vybrané buňky** a otevřeme modální okno.

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

> **Proč to funguje:** `GridJs.getSelectedCell()` vrací řetězec jako `"C2"` (sloupec C, řádek 2). Uložení do `lastSelectedCell` nám umožní později **aktualizovat hodnotu buňky v gridu** pomocí přesné adresy.

---

## Krok 3: Načtení nové ceny z vstupního pole

Když uživatel klikne na **Uložit**, musíme **číst hodnotu vstupu pomocí JavaScriptu** bezpečně. Tento krok také ověří, že zadaná cena je kladné číslo.

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

> **Poznámka:** Použití `parseFloat` zajistí, že přijmeme desetinná čísla (např. `1.99`). Ochrana `isNaN` zabraňuje nechtěným prázdným odesláním.

---

## Krok 4: Aktualizace hodnoty vybrané buňky

Nyní konečně **aktualizujeme hodnotu buňky v gridu** pomocí dříve zachycené adresy. Metoda `updateCell` v GridJs vrací promise, takže můžeme řetězit akci zavření modálního okna.

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

> **Proč použít promise?** GridJs může potřebovat znovu vykreslit tabulku nebo synchronizovat s backendem. Čekáním na promise zajistíme, že UI se skryje až po tom, co grid zobrazí novou hodnotu.

---

## Krok 5: Zpracování zrušení a okrajových případů

Robustní řešení vždy poskytuje uživateli možnost odjít. Tlačítko **Zrušit** jednoduše skryje modální okno a vymaže jakoukoli uloženou adresu.

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### Co když není vybrána žádná buňka?

Pokud uživatel nějakým způsobem spustí tlačítko **Uložit** bez předchozího kliknutí na buňku (např. otevřel modální okno programově), `lastSelectedCell` bude `null`. Včasný návrat v `updateSelectedCell` zabrání runtime chybě a vypíše užitečné varování.

### Práce s velkými gridy

U gridů s stránkováním `GridJs.getSelectedCell()` stále vrací absolutní adresu (např. `"B12"`), nikoli jen viditelný řádek. To znamená, že aktualizace funguje i když upravovaná řada leží na jiné stránce. Buďte však vědomi, že UI automaticky nepřepne stránku po aktualizaci – pokud to potřebujete, zavolejte `grid.forceUpdate()` nebo přejděte na požadovanou stránku ručně.

---

## Kompletní funkční příklad

Níže je celý kód, který můžete zkopírovat do jediného HTML souboru. Otevřete jej v prohlížeči, klikněte na libovolnou buňku, změňte cenu a sledujte okamžitou aktualizaci gridu.

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


## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohly zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Získat adresu, počet buněk a offset pro celý Excel rozsah](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Získat adresu, počet buněk a offset pro celý Excel rozsah](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Získat adresu, počet buněk a offset pro celý Excel rozsah](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}