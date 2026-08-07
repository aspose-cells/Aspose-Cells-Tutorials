---
category: general
date: 2026-06-30
description: Tanulja meg, hogyan lehet lekérni a kiválasztott cella címét, frissíteni
  a rácscella értékét és beolvasni a bemeneti értéket JavaScript segítségével a GridJs
  használatával. Lépésről‑lépésre kód és tippek.
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: hu
og_description: Szerezze meg a kiválasztott cella címét, frissítse a rácscella értékét,
  és olvassa be a bemeneti értéket JavaScript segítségével. Kövesse ezt a teljes útmutatót
  a zökkenőmentes GridJs integrációhoz.
og_title: A kiválasztott cella címének lekérése – Teljes GridJs JavaScript oktatóanyag
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
title: A kijelölt cella címének lekérése a GridJs-ben – Teljes JavaScript útmutató
url: /hu/python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kiválasztott cella címének lekérése – Teljes GridJs JavaScript útmutató

Szükséged volt már **kiválasztott cella címének lekérésére** egy GridJs táblázatból, de nem tudtad, melyik API‑hívást használd? Nem vagy egyedül. Sok admin felületen a felhasználók egy cellára kattintanak, egy modálban szerkesztik az értéket, és elvárják, hogy a rács azonnal frissüljön. Ez az útmutató pontosan megmutatja, hogyan szerezheted meg a címet, olvashatod ki az új árat egy input mezőből, és **frissítheted a rács cella értékét** oldalújratöltés nélkül.

Kitérünk arra is, hogyan **olvassuk be az input értékét JavaScript‑kel** helyesen, hogyan kezeljünk szélhelyzeteket, és hogyan zárjuk be a modált, amikor a frissítés befejeződött. A végére egy önálló kódrészletet kapsz, amelyet bármely GridJs‑t használó projektbe beilleszthetsz.

## Mit fogsz építeni

- Egy egyszerű HTML táblázat, amelyet a GridJs hajt végre.
- Egy szerkesztő modál, amely cellára kattintva jelenik meg.
- JavaScript, amely **lekéri a kiválasztott cella címét**, beolvassa a felhasználó által beírt árat, **frissíti a rács cella értékét**, majd elrejti a modált.

Nem szükséges semmilyen külső könyvtár a GridJs‑en kívül, a kód modern böngészőkben (Chrome 102+, Edge, Firefox) működik. Ha már van egy GridJs példányod az oldalon, a releváns részeket egyszerűen átmásolhatod.

## Előfeltételek

- Alapvető JavaScript és DOM ismeretek.
- GridJs könyvtár betöltve (CDN‑ről vagy npm‑ből).
- Egy oldal, amely már megjelenít egy GridJs rácsot (mutatunk egy minimális példát).

Ha valamelyik ismeretlennek tűnik, ne aggódj – minden lépéshez rövid összefoglaló tartozik.

---

## 1. lépés: HTML váz felépítése

Először helyezzük el a táblázat konténert, a rejtett modált és az ár input mezőt. A modált egyszerű CSS osztályokkal kapcsoljuk be és ki.

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

> **Pro tipp:** A `#editModal` egy minimális CSS trükköt használ – csak add hozzá az `active` osztályt a megjelenítéshez. Ezt kicserélheted Bootstrap‑re, Tailwind‑re vagy bármely már használt modál komponensre.

---

## 2. lépés: GridJs inicializálása és cella‑kattintások rögzítése

Most létrehozunk egy rácsot mintaadatokkal, és figyeljük a cella‑kiválasztásokat. Amikor a felhasználó egy cellára kattint, **lekérjük a kiválasztott cella címét** és megnyitjuk a modált.

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

> **Miért működik:** A `GridJs.getSelectedCell()` egy `"C2"`‑szerű karakterláncot ad vissza (C oszlop, 2. sor). Ennek tárolása a `lastSelectedCell`‑ben lehetővé teszi, hogy később **frissítsük a rács cella értékét** a pontos helyen.

---

## 3. lépés: Az új ár beolvasása az input mezőből

Amikor a felhasználó a **Mentés** gombra kattint, biztonságosan **be kell olvasnunk az input értékét JavaScript‑kel**. Ebben a lépésben ellenőrizzük is, hogy a megadott ár pozitív szám legyen.

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

> **Megjegyzés:** A `parseFloat` használata biztosítja, hogy a tizedesjegyeket is elfogadjuk (pl. `1.99`). Az `isNaN` ellenőrzés megakadályozza a véletlen üres beküldéseket.

---

## 4. lépés: A kiválasztott cella értékének frissítése

Végül **frissítjük a rács cella értékét** a korábban rögzített címmel. A GridJs `updateCell` metódusa egy ígéretet (promise) ad vissza, így láncolhatunk egy modál‑bezáró műveletet.

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

> **Miért ígéretet használunk?** A GridJs‑nek előfordulhat, hogy újra kell renderelnie a táblázatot vagy szinkronizálnia kell a backenddel. Az ígéretre várva garantáljuk, hogy a felhasználói felület csak a rács frissítése után tűnik el.

---

## 5. lépés: Mégse gomb és szélhelyzetek kezelése

Egy robusztus megoldás mindig ad kiutat a felhasználónak. A **Mégse** gomb egyszerűen elrejti a modált és törli a tárolt címet.

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### Mi van, ha nincs kiválasztott cella?

Ha a felhasználó valamilyen módon a **Mentés** gombot anélkül nyomja meg, hogy előbb cellára kattintott volna (például programból nyitotta meg a modált), a `lastSelectedCell` `null` lesz. Az `updateSelectedCell` korai visszatérése megakadályozza a futásidejű hibát, és hasznos figyelmeztetést naplóz.

### Nagy rácsok kezelése

Oldalazott rácsok esetén a `GridJs.getSelectedCell()` továbbra is az abszolút címet adja vissza (pl. `"B12"`), nem csak a látható sort. Így a frissítés akkor is működik, ha a szerkesztett sor egy másik oldalon van. Csak tudd, hogy a UI nem vált automatikusan oldalra a frissítés után – ha erre szükség van, hívd a `grid.forceUpdate()`‑et vagy navigálj manuálisan a megfelelő oldalra.

---

## Teljes működő példa

Az alábbi kódot egyszerűen másold be egy HTML fájlba. Nyisd meg a böngészőben, kattints bármely cellára, módosítsd az árat, és figyeld, ahogy a rács azonnal frissül.

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


## Mi legyen a következő tanulnivalód?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódrészleteket és lépésről‑lépésre magyarázatokat tartalmaz, hogy segítsenek az API további funkcióinak elsajátításában és alternatív megvalósítási módok felfedezésében a saját projektjeidben.

- [Get Address, Cell Count, and Offset for Entire Excel Range](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Get Address Cell Count And Offset For Entire Excel Range](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Get Address Cell Count And Offset For Entire Excel Range](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}