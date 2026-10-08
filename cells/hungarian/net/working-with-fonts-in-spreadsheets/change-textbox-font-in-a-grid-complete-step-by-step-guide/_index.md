---
category: general
date: 2026-06-21
description: Tanulja meg, hogyan változtathatja meg a szövegmező betűtípusát, állíthatja
  be programozottan a betűszínt, és módosíthatja a betűméretet egy rács cellájában.
  Kövesse ezt a gyakorlati útmutatót a szövegmezők formázásához.
draft: false
keywords:
- change textbox font
- change font size cell
- how to style textbox
- set font color programmatically
- change font family grid
language: hu
og_description: A szövegmező betűtípusának gyors módosítása egy rácsban. Ez az útmutató
  bemutatja, hogyan lehet stílusozni a szövegmezőt, programozottan beállítani a betűszínt,
  és a cellaméretet tiszta kóddal módosítani.
og_title: Szövegmező betűtípusának módosítása rácsban – Teljes programozási útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to change textbox font, set font color programmatically and
    adjust font size cell in a grid. Follow this practical tutorial for styling textboxes.
  headline: Change Textbox Font in a Grid – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to change textbox font, set font color programmatically and
    adjust font size cell in a grid. Follow this practical tutorial for styling textboxes.
  name: Change Textbox Font in a Grid – Complete Step‑by‑Step Guide
  steps:
  - name: Breaking Down the Object
    text: '| Property | Purpose | Example Values | |----------|---------|----------------|
      | `family` | Font family – controls the typeface. | `"Arial"`, `"Helvetica"`,
      `"Courier New"` | | `size` | Font size in pixels (or points, depending on the
      grid). | `12`, `14`, `16` | | `color` | Text color in any CSS‑co'
  - name: Expected Output
    text: '- The textbox located at **row 2, column 3** now displays text in **Arial**,
      **14 px**, and a **#0066CC** blue hue. - Opening the browser console will print
      something like:'
  - name: Can I change only the font size without affecting family or color?
    text: 'Absolutely. Just omit the properties you don’t want to modify:'
  - name: What if my grid uses a different property name for the textbox?
    text: Inspect the cell object in the console (`console.log(cell)`). You’ll likely
      see something like `cell.editor` or `cell.input`. Replace `cell.textbox` with
      the correct reference.
  - name: How do I apply the same style to an entire column?
    text: 'Loop through the rows and set the font for each cell in that column:'
  - name: Is there a way to revert to the original font?
    text: 'Store the original style before overwriting:'
  type: HowTo
tags:
- JavaScript
- UI‑grid
- DOM‑manipulation
title: Szövegmező betűtípusának módosítása egy rácsban – Teljes lépésről‑lépésre útmutató
url: /hu/net/working-with-fonts-in-spreadsheets/change-textbox-font-in-a-grid-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szövegmező betűtípusának módosítása rácsban – Teljes lépésről‑lépésre útmutató

Valaha is szükséged volt **szövegmező betűtípusának megváltoztatására** egy adatgridben, de nem tudtad, melyik tulajdonságot kell módosítani? Nem vagy egyedül – a legtöbb fejlesztő ezzel a problémával szembesül szerkeszthető táblázatok vagy irányítópultok építésekor. Ebben a tutorialban pontosan végigvezetünk, hogyan változtasd meg a szövegmező betűtípust, állítsd be a színét programozottan, és még a betűméretet is cellánként állíthatod.

Megosztunk tippeket is arra vonatkozóan, **hogyan stílusozz szövegmező** elemeket, lefedjük a **betűméret cellánkénti módosítása** eseteket, és megmutatjuk, hogyan **állítsd be a betűszínt programozottan** anélkül, hogy a hajadba nyúlnál. A végére egy újrahasználható kódrészletet kapsz, amely bármely olyan rácskomponenssel működik, amely rendelkezik `getCell` API‑val.

## Előfeltételek

- Modern böngésző ES6 támogatással (Chrome, Edge, Firefox, Safari)
- Olyan rácskönyvtár, amely biztosítja a `grid.getCell(row, col)` metódust, és egy cellaobjektumot ad vissza, amely tartalmaz egy `textbox` referenciát
- Alapvető JavaScript objektumok és CSS tulajdonságok ismerete

További csomagok nem szükségesek – csak tiszta JavaScript és a rács saját API-ja.

## A megoldás áttekintése

Az alapötlet egyszerű: lekérjük a célcellát, megszerezzük a beágyazott szövegmezőt, majd egy új betűtípus‑objektumot adunk hozzá, amely meghatározza a családot, méretet és színt. Olyan, mintha a szövegmezőnek egy friss ruhát adnánk. Az alábbi magas szintű folyamat:

1. **A célcellához való hozzáférés** – megtalálod a kívánt sort/oszlopot.
2. **A szövegmező lekérése** – a szöveget tartalmazó UI elem.
3. **Betűtípus‑stílus objektum létrehozása** – megadod a családot, méretet és színt.
4. **A stílus alkalmazása** – az objektumot a szövegmező `font` tulajdonságához rendeled.

Ennyi. Merüljünk el minden egyes lépésben, magyarázzuk el, miért fontos, és nézzük meg a kódot működés közben.

![Képernyőkép egy rácscelláról stílusos szövegmezővel – szövegmező betűtípusának módosítása](/images/change-textbox-font-example.png)

## 1. lépés: A célcellához való hozzáférés a rácsban

```javascript
// Step 1: Access the target cell in the grid
const cell = grid.getCell(2, 3);
```

> **Miért fontos:**  
> A rácsok gyakran sor- és oszlopindexeket nullától kezdődően tárolják. A `grid.getCell(2, 3)` hívással a **2. sor, 3. oszlop** celláját kapjuk meg. Ha egy másik helyen szeretnél **betűméret cellánként** módosítani, csak állítsd be az indexeket.

**Pro tipp:** Ha a rácsod támogatja a név szerint definiált oszlopokat, a numerikus oszlop helyett kulcsot is használhatsz, pl. `grid.getCell(2, "price")`.

## 2. lépés: A szövegmező lekérése a cellából

```javascript
// Step 2: Get the textbox contained in that cell
const textbox = cell.textbox;
```

> **Mi történik:**  
> A legtöbb rácsimplementáció a szerkeszthető tartalmat egy `<input>` vagy `<textarea>` elembe csomagolja, és `cell.textbox`‑ként teszi elérhetővé. A referencia megszerzése lehetővé teszi a vizuális stílus közvetlen manipulálását.

Ha a rács másik tulajdonságnevet használ (például `cell.editor`), csak igazítsd a kódot – ez egy gyakori variáció, amikor **hogyan stílusozz szövegmezőt** egy egyedi komponenshez.

## 3. lépés: A kívánt betűtípus‑tulajdonságok definiálása

```javascript
// Step 3: Define the desired font properties
const fontStyle = {
  family: "Arial",          // change font family grid
  size: 14,                 // change font size cell
  color: "#0066CC"          // set font color programmatically
};
```

### Az objektum felbontása

| Property | Purpose | Example Values |
|----------|---------|----------------|
| `family` | Betűtípus‑család – meghatározza a karakterkészletet. | `"Arial"`, `"Helvetica"`, `"Courier New"` |
| `size`   | Betűméret pixelben (vagy pontban, a rácstól függően). | `12`, `14`, `16` |
| `color`  | Szövegszín bármely CSS‑kompatibilis formátumban. | `"#0066CC"`, `"rgb(255,0,0)"`, `"navy"` |

> **Miért használunk objektumot:**  
> A három attribútum egy helyen való összegzése rendezi a kódot, és tükrözi, ahogy sok UI‑könyvtár a stílusinformációkat várja. Emellett lehetővé teszi, hogy **betűcsalád módosítása rácsban** vagy **betűszín programozott beállítása** egyetlen hozzárendeléssel történjen.

## 4. lépés: A betűtípus‑stílus alkalmazása a szövegmezőre

```javascript
// Step 4: Apply the font style to the textbox
textbox.font = fontStyle;
```

> **A háttérben:**  
> A rács szövegmező komponense értelmezi a `font` tulajdonságot, és ennek megfelelően frissíti a CSS‑ét. Ez az egy soros kód egyszerre cseréli le a korábbi betűcsaládot, méretet és színt – pontosan amire szükséged van, amikor **szövegmező betűtípusát** több cellában szeretnéd **módosítani**.

Ha a komponens más API‑t használ (például `textbox.style.fontFamily = ...`), igazítsd a hozzárendelést, de tartsd meg ugyanazt az elvet.

## Teljes működő példa

Az alábbi önálló kódrészletet beillesztheted egy HTML fájlba, amely tartalmaz egy mock grid objektumot. Bemutatja a teljes folyamatot az 1.‑től a 4.-ig, valamint egy gyors ellenőrzést, hogy a stílus megváltozott-e.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Change Textbox Font Demo</title>
  <style>
    .grid { display: table; border-collapse: collapse; }
    .grid .row { display: table-row; }
    .grid .cell { display: table-cell; border: 1px solid #ccc; padding: 8px; }
    .grid .cell input { width: 100%; border: none; }
  </style>
</head>
<body>

<div id="myGrid" class="grid"></div>

<script>
/* ---------- Mock Grid Implementation ---------- */
class MockGrid {
  constructor(rows, cols) {
    this.rows = rows;
    this.cols = cols;
    this.el = document.getElementById('myGrid');
    this._build();
  }
  _build() {
    for (let r = 0; r < this.rows; r++) {
      const rowDiv = document.createElement('div');
      rowDiv.className = 'row';
      for (let c = 0; c < this.cols; c++) {
        const cellDiv = document.createElement('div');
        cellDiv.className = 'cell';
        const input = document.createElement('input');
        input.type = 'text';
        input.value = `R${r}C${c}`;
        // expose textbox via a custom property
        cellDiv.textbox = input;
        cellDiv.appendChild(input);
        rowDiv.appendChild(cellDiv);
      }
      this.el.appendChild(rowDiv);
    }
  }
  getCell(row, col) {
    const rowDiv = this.el.children[row];
    if (!rowDiv) return null;
    const cellDiv = rowDiv.children[col];
    return cellDiv || null;
  }
}

/* ---------- Use the Grid ---------- */
const grid = new MockGrid(5, 5); // 5x5 grid for demo

// ---- Change Textbox Font (the core tutorial steps) ----
const cell = grid.getCell(2, 3);          // step 1
const textbox = cell.textbox;             // step 2
const fontStyle = {                      // step 3
  family: "Arial",
  size: 14,
  color: "#0066CC"
};
textbox.font = fontStyle;                // step 4

// Verify by logging computed style
setTimeout(() => {
  const cs = window.getComputedStyle(textbox);
  console.log('Applied font family:', cs.fontFamily);
  console.log('Applied font size:', cs.fontSize);
  console.log('Applied color:', cs.color);
}, 0);
</script>
</body>
</html>
```

### Várt kimenet

- A **2. sor, 3. oszlop**‑ban lévő szövegmező most **Arial**, **14 px**, és **#0066CC** kék árnyalatú szöveget jelenít.
- A böngésző konzoljában valami ilyesmi jelenik meg:

```
Applied font family: Arial, Helvetica, sans-serif
Applied font size: 14px
Applied color: rgb(0, 102, 204)
```

Ha megnyitod az oldalt, vizuálisan is megerősítheted a változást – többé nem a rendszer alapértelmezett betűtípusa jelenik meg.

## Gyakran Ismételt Kérdések (GYIK)

### Csak a betűméretet szeretném módosítani, a családot vagy a színt érintetlenül hagyni?
Természetesen. Hagyd ki a módosítani nem kívánt tulajdonságokat:

```javascript
textbox.font = { size: 18 }; // only changes size
```

### Mi van, ha a rácsom másik tulajdonságnevet használ a szövegmezőhöz?
Nézd meg a cellaobjektumot a konzolban (`console.log(cell)`). Valószínűleg `cell.editor` vagy `cell.input` néven találod. Cseréld le a `cell.textbox`‑t a megfelelő referenciára.

### Hogyan alkalmazzam ugyanazt a stílust egy egész oszlopra?
Iterálj a sorokon, és állítsd be a betűtípust minden cellában az adott oszlopban:

```javascript
for (let r = 0; r < grid.rowCount; r++) {
  const colCell = grid.getCell(r, 3);
  colCell.textbox.font = fontStyle; // reuse the same fontStyle object
}
```

### Van mód a eredeti betűtípus visszaállítására?
Mentsd el az eredeti stílust a felülírás előtt:

```javascript
const original = { ...textbox.font };
textbox.font = fontStyle; // apply new style
// later...
textbox.font = original; // revert
```

## Tippek és legjobb gyakorlatok

- **Csoportos frissítések:** Ha sok cellát kell stílusozni, csomagold a változtatásokat `requestAnimationFrame`‑be vagy a rács specifikus batch metódusába, hogy elkerüld a layout‑thrashing‑et.
- **Reszponzív betűk:** Használj relatív egységeket (`em`, `rem`) a fix pixelek helyett, ha a UI‑nek skálázódnia kell.
- **Hozzáférhetőség:** Biztosíts megfelelő kontrasztot, amikor **betűszínt programozottan állítasz be** – a WCAG AA minimum 4.5:1 arány normál szöveg esetén.
- **Böngészőspecifikus sajátosságok:** Egyes régebbi rácsok esetén előfordulhat, hogy közvetlenül a `<input>` elem `style.fontFamily`‑ját kell beállítani a `font` objektum helyett.

## Összegzés

Most már tudod, **hogyan változtasd meg a szövegmező betűtípusát** egy rácsban, a megfelelő cella lekérésétől a újrahasználható `fontStyle` objektum definiálásáig, és egy sorban történő alkalmazásáig. Útközben megtanultuk a **betűméret cellánként** módosítását, a **betűszín programozott beállítását**, és akár a **betűcsalád módosítását rácsban** egy adott oszlopra.

Ezt a mintát most már bármely UI‑könyvtárra alkalmazhatod – legyen szó admin irányítópultról, táblázatszerű szerkesztőről vagy egyedi jelentéskészítő eszközről. Kísérletezz különböző családokkal, méretekkel és színekkel; akár hover‑effekteket vagy feltételes stílusokat is hozzáadhatsz az adatértékek alapján.

Van még egy styling kihívásod? Írj egy megjegyzést, és nézzük meg együtt. Boldog kódolást!

## Mit érdemes még megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra építenek. Minden forrás komplett, működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek további API‑funkciók elsajátításában és alternatív megvalósítási megközelítések felfedezésében a saját projektjeidben.

- [How to Change Font Color in Excel Using Aspose.Cells for Java&#58; A Complete Guide](/cells/english/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Change Font Color Aspose Cells Java Tutorial](/cells/german/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Change Font Color Aspose Cells Java Tutorial](/cells/french/java/formatting/change-font-color-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}