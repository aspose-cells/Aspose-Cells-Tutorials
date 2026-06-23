---
category: general
date: 2026-05-30
description: Tanulja meg, hogyan hozhat létre GridJsOptions példányt, és konfigurálhatja
  a rács beállításait JavaScriptben dinamikus táblázatokhoz. Lépésről‑lépésre útmutató
  teljes kóddal.
draft: false
keywords:
- create gridjsoptions instance
- configure grid options javascript
- gridjs initialization
- javascript data grid settings
- dynamic table configuration
language: hu
og_description: Hozzon létre GridJsOptions példányt, és percek alatt konfigurálja
  a rács beállításait JavaScriptben. Teljes példa, magyarázatok és legjobb gyakorlatok
  tippek.
og_title: GridJsOptions példány létrehozása – Grid opciók konfigurálása JavaScriptben
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
title: GridJsOptions példány létrehozása – Grid Options JavaScript konfigurálása
url: /hu/net/link-and-configuration-operations/create-gridjsoptions-instance-configure-grid-options-javascr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GridJsOptions példány létrehozása – Grid Options JavaScript konfigurálása

Ever wondered how to **create GridJsOptions instance** without hunting through scattered docs? You’re not the only one. When you need a slick, sortable table on a web page, mastering how to configure grid options JavaScript is the first step toward a polished UI.

Gondolkodtál már azon, hogyan **create GridJsOptions instance**-t hozhatsz létre anélkül, hogy szétszórt dokumentációkban keresgélnél? Nem vagy egyedül. Amikor egy elegáns, rendezhető táblázatra van szükséged egy weboldalon, a grid options JavaScript konfigurálásának elsajátítása az első lépés egy kifinomult felhasználói felület felé.

In this tutorial we’ll walk through the exact code you need, explain why each setting matters, and show you a complete, runnable example. By the end you’ll be comfortable creating GridJsOptions instance, tweaking alignment, pagination, and even custom cell renderers—all with plain JavaScript.

Ebben az oktatóanyagban végigvezetünk a szükséges kódon, elmagyarázzuk, miért fontos minden beállítás, és bemutatunk egy teljes, futtatható példát. A végére magabiztosan tudsz GridJsOptions instance-t létrehozni, az igazítást, lapozást és akár egyedi cella renderelőket is finomhangolni – mindezt egyszerű JavaScript használatával.

## Mit fogsz megtanulni

- How to **create GridJsOptions instance** from scratch.
- A key properties that let you **configure grid options JavaScript** (sorting, pagination, number formatting, etc.).
- Common pitfalls (e.g., mixing string and numeric types) and how to avoid them.
- A full HTML page you can copy‑paste into any project and see results instantly.

- **create GridJsOptions instance**-t hozhatsz létre a semmiből.
- A kulcsfontosságú tulajdonságok, amelyek lehetővé teszik a **configure grid options JavaScript**-t (rendezés, lapozás, számformázás stb.).
- Gyakori buktatók (pl. karakterlánc és numerikus típusok keverése) és azok elkerülése.
- Egy teljes HTML oldal, amelyet bármely projektbe másolhatsz‑beilleszthetsz, és azonnal láthatod az eredményt.

### Előfeltételek

- A modern browser (Chrome, Edge, Firefox) – no build tools required.
- Basic familiarity with JavaScript (variables, objects, DOM).
- The Grid.js library (we’ll pull it from a CDN).

- Egy modern böngésző (Chrome, Edge, Firefox) – nincs szükség build eszközökre.
- Alapvető ismeretek a JavaScriptben (változók, objektumok, DOM).
- A Grid.js könyvtár (CDN‑ről fogjuk betölteni).

If any of those sound unfamiliar, don’t panic—each step includes a quick refresher.

Ha valamelyik ismeretlennek tűnik, ne ess pánikba – minden lépés tartalmaz egy gyors ismétlést.

---

## 1. lépés: Grid.js betöltése és az HTML váz megkészítése

Before we can **create GridJsOptions instance**, we need the library itself. The easiest way is to use the official CDN. Below is a minimal HTML skeleton that also reserves a `<div>` where the grid will render.

Mielőtt **create GridJsOptions instance**-t tudnánk létrehozni, szükségünk van magára a könyvtárra. A legegyszerűbb módja a hivatalos CDN használata. Az alábbiakban egy minimális HTML váz található, amely egy `<div>`-et is lefoglal, ahol a rács megjelenik.

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

> **Pro tipp:** Tartsd a CSS hivatkozást a saját stílusaid előtt, hogy a grid alapértelmezett témája helyesen töltődjön be.

### Miért fontos ez

Loading the library from a CDN ensures you always get the latest stable version without a local install. The `<div id="grid-wrapper">` is the placeholder that the Grid.js constructor will target once we **configure grid options JavaScript**.

A könyvtár CDN‑ről történő betöltése biztosítja, hogy mindig a legújabb stabil verziót kapod helyi telepítés nélkül. A `<div id="grid-wrapper">` a helyőrző, amelyet a Grid.js konstruktor megcéloz, amint **configure grid options JavaScript**-t végrehajtjuk.

## 2. lépés: Új GridJsOptions példány létrehozása

Now comes the heart of the tutorial: the line that actually **creates GridJsOptions instance**. In a separate file called `grid-config.js` (referenced in the HTML above) we’ll write:

Most jön az oktatóanyag szíve: a sor, amely ténylegesen **creates GridJsOptions instance**. Egy külön fájlban, amely `grid-config.js` névre hallgat (az előző HTML‑ben hivatkozva), a következőt írjuk:

```javascript
// grid-config.js

// Step 2: Create a new GridJsOptions instance to configure grid behavior
const gridOptions = new GridJsOptions();
```

That single line gives you a clean object you can start populating with settings. Think of `gridOptions` as the control panel for every feature you’ll later enable.

Ez az egyetlen sor egy tiszta objektumot ad, amelyet beállításokkal tölthetsz fel. Tekintsd a `gridOptions`-t egy vezérlőpultnak minden később engedélyezni kívánt funkcióhoz.

### Amit konfigurálsz

- **NumberFormatAlignment** – automatikusan igazítja a numerikus karakterláncokat.
- **Pagination** – szabályozza az oldal méretét és a navigációt.
- **Sorting** – be- és kikapcsolja az oszlop rendezését.
- **Columns** – meghatározza a fejléceket, adat típusokat és egyedi renderelőket.

You can add any of these properties before you finally instantiate the Grid itself.

Bármelyik ezek közül a tulajdonságot hozzáadhatod, mielőtt végül a Grid-et példányosítanád.

## 3. lépés: Számok igazításának engedélyezése (gyakori követelmény)

Most tables contain a mix of text and numbers. By default Grid.js aligns everything left, which looks odd for monetary values. To **configure grid options JavaScript** for proper alignment, set the `NumberFormatAlignment` flag:

A legtöbb táblázat szöveg és szám keverékét tartalmazza. Alapértelmezés szerint a Grid.js mindent balra igazít, ami pénzügyi értékeknél furcsa. A megfelelő igazításhoz **configure grid options JavaScript**-t, állítsd be a `NumberFormatAlignment` jelzőt:

```javascript
// Enable left/right alignment for numeric strings
gridOptions.NumberFormatAlignment = true;
```

Why enable this? When the flag is true, Grid.js inspects each cell; if it looks like a number (e.g., “1234”, “12.34%”), it automatically right‑aligns it. This tiny tweak makes reports far more readable.

Miért engedélyezzük? Ha a jelző igaz, a Grid.js minden cellát ellenőriz; ha számnak tűnik (pl. „1234”, „12.34%”), automatikusan jobbra igazítja. Ez az apró módosítás sokkal olvashatóbbá teszi a jelentéseket.

## 4. lépés: Lapozás és rendezés hozzáadása

A real‑world grid rarely fits on a single screen. Let’s turn on pagination (10 rows per page) and allow users to sort any column.

Egy valós környezetben a rács ritkán fér el egy képernyőn. Kapcsoljuk be a lapozást (10 sor oldalanként) és engedélyezzük a felhasználóknak, hogy bármelyik oszlopot rendezzenek.

```javascript
gridOptions.Pagination = {
  limit: 10,          // rows per page
  enabled: true
};

gridOptions.Sort = true;   // enables click‑to‑sort on all columns
```

### Szél‑eset megjegyzés

If you later supply a custom data source that already returns paginated results, you’ll want to disable Grid.js’s built‑in pagination to avoid double‑paging. Simply set `gridOptions.Pagination.enabled = false;`.

Ha később egy egyedi adatforrást adsz meg, amely már lapozott eredményeket ad vissza, ki kell kapcsolnod a Grid.js beépített lapozását, hogy elkerüld a dupla lapozást. Egyszerűen állítsd be `gridOptions.Pagination.enabled = false;`.

## 5. lépés: Oszlopok és mintaadatok definiálása

Now we’ll feed the grid some mock data and tell it what each column represents. This is where the **create gridjsoptions instance** pattern really shines—everything lives in one tidy object.

Most adunk a rácsnak némi mintadatot, és megmondjuk, mit jelent minden oszlop. Itt jön igazán elő a **create gridjsoptions instance** minta – minden egy rendezett objektumban él.

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

Vedd észre, hogy a `id` oszlop értékeit azonosra hagyjuk a kulcsokkal minden adatobjektumban. Ez a konvenció lehetővé teszi, hogy a Grid.js automatikusan leképezze az értékeket, így elkerülve, hogy minden oszlophoz egyedi formázót írj.

## 6. lépés: A Grid példányosítása a beállításainkkal

We finally **configure grid options javascript** by passing the `gridOptions` object to the Grid constructor. The grid will render inside the `<div id="grid-wrapper">` we prepared earlier.

Végül **configure grid options javascript**-t hajtunk végre, a `gridOptions` objektumot átadva a Grid konstruktorának. A rács a korábban előkészített `<div id="grid-wrapper">`-ben fog megjelenni.

```javascript
// Create the Grid instance using the previously built options
const grid = new Grid(gridOptions);

// Render the grid into the page
grid.render(document.getElementById("grid-wrapper"));
```

That’s it. The whole process—from **create gridjsoptions instance** to rendering—takes less than a minute of coding.

Ennyi. Az egész folyamat – a **create gridjsoptions instance**-től a megjelenítésig – kevesebb mint egy perc kódolás.

### Várt kimenet

When you open the HTML file in a browser you should see:

- A header row with “ID”, “Employee”, “Salary ($)”, “Dept.”.
- Right‑aligned salary numbers (thanks to `NumberFormatAlignment`).
- Pagination controls at the bottom (if you added more than ten rows).
- Clickable column headers that sort ascending/descending.

- Egy fejléc sor a „ID”, „Employee”, „Salary ($)”, „Dept.” feliratokkal.
- Jobbra igazított fizetési számok (köszönhetően a `NumberFormatAlignment`-nek).
- Lapozó vezérlők alul (ha tíznél több sort adtál hozzá).
- Kattintható oszlopfejlécek, amelyek növekvő/csökkenő sorrendbe rendeznek.

If anything looks off, open the browser console (F12) and look for error messages—most bugs stem from mismatched column IDs or missing library scripts.

Ha valami nem stimmel, nyisd meg a böngésző konzolt (F12), és keresd a hibaüzeneteket – a legtöbb hiba a nem egyező oszlop‑ID‑kből vagy hiányzó könyvtár‑szkriptekből ered.

## 7. lépés: Haladó finomhangolások (opcionális)

Below are a few quick ideas you can experiment with once the basic grid works.

Az alábbiakban néhány gyors ötletet találsz, amelyeket kipróbálhatsz, miután az alap rács működik.

| Feature | How to enable | Why it helps |
|---------|---------------|--------------|
| **Egyedi cella renderelő** | `gridOptions.Columns[2].formatter = (cell) => \`<b>$${cell}</b>\`;` | A fizetéseket félkövérrel emeli ki. |
| **Keresősáv** | `gridOptions.Search = true;` | Lehetővé teszi a felhasználók számára, hogy azonnal szűrjék a sorokat. |
| **Szerver‑oldali adat** | Set `gridOptions.Server = { url: "/api/employees", then: data => data.items };` | Ez több ezer sorra is skálázható. |
| **Téma váltás** | Add `gridOptions.ClassName = "gridjs-theme-dark";` | Illeszkedik a sötét módú tervekhez. |

Feel free to mix and match—Grid.js is deliberately flexible. Just remember to keep the original **create gridjsoptions instance** line at the top; all later tweaks rely on that single object.

Nyugodtan keverd és kombináld – a Grid.js szándékosan rugalmas. Csak ne feledd megtartani az eredeti **create gridjsoptions instance** sort felül; minden későbbi finomhangolás ehhez az egyetlen objektumhoz támaszkodik.

## Következtetés

We’ve just walked through a complete workflow to **create GridJsOptions instance** and **configure grid options JavaScript** for a functional, sortable, and paginated data table. Starting with a plain HTML page, we loaded the library, built an options object, enabled numeric alignment, added pagination, defined columns, and finally rendered the grid.

Most végigjártunk egy teljes munkafolyamatot a **create GridJsOptions instance** és a **configure grid options JavaScript** elvégzéséhez egy funkcionális, rendezhető és lapozott adat táblázathoz. Egy egyszerű HTML oldalról indulva betöltöttük a könyvtárat, felépítettünk egy beállítási objektumot, engedélyeztük a numerikus igazítást, hozzáadtuk a lapozást, definiáltuk az oszlopokat, és végül megjelenítettük a rácsot.

From here you can:

- Replace the static `sampleData` with an AJAX call.
- Add custom formatters for dates, currencies, or icons.
- Integrate the grid into a framework like React or Vue (the same `gridOptions` object works there too).

- Cseréld le a statikus `sampleData`-t egy AJAX hívásra.
- Adj hozzá egyedi formázókat dátumokhoz, pénznemekhez vagy ikonokhoz.
- Integráld a rácsot egy keretrendszerbe, például React vagy Vue – ugyanaz a `gridOptions` objektum ott is működik.

The possibilities are practically endless, and the pattern we used—centralizing all settings in a single `GridJsOptions` instance—keeps your code clean and maintainable.

A lehetőségek gyakorlatilag végtelenek, és a általunk használt minta – az összes beállítás központosítása egyetlen `GridJsOptions` példányban – tisztán és karbantarthatóan tartja a kódot.

Got a use‑case you’re unsure about? Drop a comment, and we’ll explore it together. Happy coding, and enjoy building dynamic tables with Grid.js!

Van egy használati eset, amiben bizonytalan vagy? Hagyj egy megjegyzést, és együtt megvizsgáljuk. Boldog kódolást, és élvezd a dinamikus táblázatok építését a Grid.js-szel!

## Mit érdemes még megtanulni?

- [Hogyan hozzunk létre és konfiguráljunk Excel munkafüzeteket az Aspose.Cells .NET segítségével: Lépésről‑lépésre útmutató](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Hogyan hozzunk létre és formázzunk Excel táblákat az Aspose.Cells for .NET használatával | Lépésről‑lépésre útmutató](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)
- [Hogyan hozzunk létre és formázzunk Excel cellákat az Aspose.Cells for Java segítségével: Lépésről‑lépésre útmutató](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}