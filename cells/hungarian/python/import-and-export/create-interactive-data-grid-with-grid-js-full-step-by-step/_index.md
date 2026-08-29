---
category: general
date: 2026-06-21
description: Készíts interaktív adatgridet a Grid.js használatával, és tanuld meg,
  hogyan jeleníts meg JSON adat táblát rendezéssel, lapozással és kereséssel. Tökéletes
  webes irányítópultokhoz.
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: hu
og_description: Készíts interaktív adatrácsot percek alatt. Tanuld meg, hogyan használhatod
  a Grid.js-t JSON adat táblázat megjelenítésére lapozással, rendezéssel és kereséssel.
og_title: Interaktív adatrács létrehozása Grid.js-sel – Teljes útmutató
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
title: Interaktív adatgrid létrehozása a Grid.js-szel – Teljes lépésről‑lépésre útmutató
url: /hu/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Interaktív adatgrid létrehozása Grid.js‑sel – Teljes lépésről‑lépésre útmutató

Gondolkodtál már azon, hogyan **hozhatsz létre interaktív adatgridet**, amely lehetővé teszi a felhasználók számára a sorok rendezését, keresését és lapozását anélkül, hogy backendet írnának? Nem vagy egyedül. Sok műszerfalnál a legnagyobb fájdalom pontja egy statikus JSON dump átalakítása egy elegáns, kereshető táblázattá – valami, ami olyan sima, mint egy táblázatkezelő, de teljesen a böngészőben fut.

Ebben a tutorialban végigvezetünk **a Grid.js használatán**, hogy **JSON adat táblázatot jelenítsünk meg** egy egyszerű HTML oldalon. A végére egy működő példát kapsz, amelyet bármelyik projektbe beilleszthetsz, valamint tippeket a eszköztár testreszabásához, nagy adathalmazok kezeléséhez és a gyakori hibák elkerüléséhez.

## Mit fogsz megtanulni

- Hogyan tölts le egy JSON fájlt, amely meghatározza az oszlopokat és a sorokat.
- Hogyan inicializáljuk a **Grid.js**‑t lapozással, rendezéssel, kereséssel és egy egyedi eszköztárral.
- Hogyan rendereljük a gridet egy célkonténerbe.
- Opcionális finomhangolások: egyedi cellaformázás, téma váltás és hibakezelés.
- Egy teljes, másolás‑beillesztés‑kész kódminta.

### Előfeltételek

Mielőtt belevágnánk, győződj meg róla, hogy rendelkezel:

1. Egy modern böngészővel (Chrome, Edge vagy Firefox) – a Grid.js ES6 funkciókra támaszkodik.
2. Egy helyi vagy távoli mappával, amely tartalmaz egy `grid_data.json` fájlt (a formátumot később megmutatjuk).
3. Alapvető HTML és JavaScript ismeretekkel – semmi bonyolult, csak az a képesség, hogy egy `.html` fájlt megnyithass a böngészőben.

Nincs szükség build eszközökre, npm‑installra vagy szerver‑oldali kódra. Ez a **interaktív adatgrid létrehozása** a Grid.js‑sel annyira szép: közvetlenül egy CDN‑ről működik.

---

## 1. lépés: Készítsd elő a JSON‑t, amely meghatározza a táblázatodat

Az első dolog, amire szükséged van, egy JSON payload, amely elmondja a Grid.js‑nek, milyen oszlopok vannak és milyen sorokat kell megjeleníteni. Tekintsd ezt a **JSON adat táblázat megjelenítésének** tervrajzának. Íme egy minimális példa, amelyet elmenthetsz `grid_data.json` néven ugyanabban a könyvtárban, ahol a HTML fájlod van:

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

*Miért ez a formátum?* A Grid.js elvárja, hogy a `columns` egy karakterláncok (vagy objektumok a haladó konfigurációhoz) tömbje legyen, a `rows` pedig egy tömb legyen tömbökből, ahol minden belső tömb megfelel az oszlopok sorrendjének. Természetesen hozzáadhatsz több oszlopot vagy beágyazott objektumokat – a Grid.js megjeleníti őket, amíg a struktúrák egyeznek.

> **Pro tipp:** Ha egy API‑ból húzod az adatokat, egyszerűen cseréld le a statikus `fetch('grid_data.json')` hívást a saját endpoint URL‑re. A kód többi része változatlan marad.

---

## 2. lépés: Grid.js inicializálása – a **how to use gridjs** magja

Most, hogy az adatforrás készen áll, be kell hoznunk a Grid.js‑t az oldalra, és meg kell mondanunk, hogyan viselkedjen. Itt valósítjuk meg a **interaktív adatgrid** funkciókat, mint a lapozás, rendezés és egy praktikus eszköztárgomb.

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

A CDN a legújabb stabil verziót biztosítja, a Mermaid téma pedig egy tiszta, modern megjelenést ad „out of the box”. Ha a default stílusokat részesíted előnyben, cseréld le a `gridjs.min.css`‑re.

Ezután, egy `<script>` tagben, töltsd le a JSON‑t és inicializáld a gridet:

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

### Az opciók részletes bontása

| Opció | Mit csinál | Miért fontos |
|--------|--------------|----------------|
| `pagination` | Sorokat oldalakra bont (alapértelmezett 10 sor/oldal) | Nagy táblázatok használhatóak maradnak anélkül, hogy túlterhelnék a felhasználói felületet. |
| `sort` | Kattintható oszlopfejlécek váltják a növekvő/csökkenő sorrendet | A felhasználók gyorsan megtalálhatják a legmagasabb értékű sorokat. |
| `search` | Egy szövegbeviteli mezőt ad hozzá, amely valós időben szűri a sorokat | Ideális ad‑hoc keresésekhez újratöltés nélkül. |
| `toolbar` | Egyedi gombokat vagy legördülőket helyez el a grid felett | Tökéletes „Súgó”, „Export” vagy „Frissítés” műveletekhez. |
| `formatter` | Lehetővé teszi, hogy nyers HTML‑t adj vissza egy cellához | Itt az e‑mail címeket kattintható mailto linkké alakítjuk. |

> **Miért ezt a megközelítést?** A grid konfiguráció deklaratív megtartásával könnyen finomhangolhatod a viselkedést anélkül, hogy a renderelés logikáját módosítanád. Ez a **how to use Grid.js** ajánlott módja a legtöbb projektben.

---

## 3. lépés: Rendereld a gridet az oldaladra

A script utolsó sorában – `grid.render(document.getElementById('grid-container'))` – a teljesen működő táblázatot egy `<div>`‑be injektálja, amelyet valahol a HTML‑body‑ban elhelyeztél:

```html
<div id="grid-container"></div>
```

Ennyi. Amikor az oldal betöltődik, a böngésző letölti a JSON‑t, felépíti a Grid.js példányt, és megjeleníti az interaktív táblát a képernyőn. Nincs újratöltés, nincs további szerverhívás az első betöltés után.

---

## Opcionális: Stílus- és téma finomhangolások

Ha a default Mermaid téma nem nyerte el a tetszésed, cseréld le bármely beépített témára (`gridjs.min.css`) vagy írj saját CSS‑t. Például, ha a fejléc háttérszínét egy lágy szürkére szeretnéd állítani:

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

Add hozzá a kódrészletet egy `<style>` tagbe vagy egy külső stylesheet‑be. A Grid.js tiszteletben tartja a szabványos CSS szelektorokat, így teljes kontrollod van a betűtípusok, színek és távolságok felett.

---

## Gyakori hibák és elkerülésük

| Hiba | Tünet | Megoldás |
|---------|---------|-----|
| **CORS hibák** JSON másik domainről történő lekérésekor | A böngésző konzolja “Blocked by CORS policy” üzenetet mutat | Tedd a JSON‑t ugyanarra a domainre, vagy engedélyezd a CORS‑t a szerveren. |
| **Nagy adathalmazok lassulása** | Görgetés akadozik, a lapozás lassú | Használj `server` pagination‑t (`pagination: { server: { url: (prev, page, limit) => … } }`) vagy lazy‑load sorokat. |
| **Az eszköztár gomb nem jelenik meg** | A `toolbar.enabled: true` ellenére nem látszik gomb | Győződj meg róla, hogy a Grid.js 2.0+ verzióját használod; a régebbi verziók más API‑t tartalmaztak. |
| **Az e‑mail linkek nem kattinthatók** | A formatter egyszerű szöveget ad vissza | Adj vissza `gridjs.html(...)`‑t egyszerű karakterlánc helyett, ahogy a példában látható. |

Ezeknek a problémáknak a korai kezelése órákat spórolhat meg a későbbi hibakeresésben.

---

## Teljes működő példa (másolás‑beillesztés‑kész)

Az alábbiakban a teljes HTML fájl látható, amelyet elmenthetsz `index.html` néven. Nyisd meg egy böngészőben, és egy teljesen funkcionális **interaktív adatgrid** demót látsz, amely **JSON adat táblázatot** jelenít meg rendezéssel, kereséssel és egy súgó gombbal.

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


## Mit érdemes még megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [How to Create an Excel Data Validation List with Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [How to Create Checkboxes in Excel using Aspose.Cells for .NET | Data Validation Tutorial](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [Create & Import XML Data into Excel Using Aspose.Cells for Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}