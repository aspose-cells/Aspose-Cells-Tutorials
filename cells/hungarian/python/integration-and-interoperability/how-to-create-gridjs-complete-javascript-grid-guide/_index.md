---
category: general
date: 2026-06-30
description: Hogyan hozhatunk létre gridjs-t egyszerűen egy teljes JavaScript példával,
  amely lefedi a gridjs konfigurációt, a konténer beállítását és a renderelési folyamatot.
draft: false
keywords:
- how to create gridjs
- gridjs configuration
- gridjs render
- gridjs JavaScript
- gridjs container
language: hu
og_description: Hogyan hozhatunk létre gridjs-t egyszerűen egy teljes JavaScript példával,
  amely lefedi a gridjs konfigurációt, a konténer beállítását és a renderelési folyamatot.
og_title: Hogyan készítsünk Gridjs-et – Teljes JavaScript rács útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  headline: How to Create Gridjs – Complete JavaScript Grid Guide
  type: TechArticle
- description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  name: How to Create Gridjs – Complete JavaScript Grid Guide
  steps:
  - name: Why this configuration matters
    text: '- **Columns** – define the header text and optional width. Without this,
      Gridjs would infer column names from the first data row, which is often less
      readable. - **Data** – an array of rows, each row being an array of cell values.
      You could also supply an async function that fetches data from an API'
  - name: Expected Output
    text: '``` +----+----------------+---------------------+--------+ | ID | Name
      | Email | Role | +----+----------------+---------------------+--------+ | 1
      | Alice Johnson | alice@example.com | Admin | | 2 | Bob Smith | bob@example.com
      | Editor | +----+----------------+---------------------+--------+ [←] [1]'
  - name: Loading Data Asynchronously
    text: 'If your data lives on a server, replace the static `data` array with a
      function that returns a Promise:'
  - name: Custom Cell Rendering
    text: 'Sometimes you need icons, buttons, or formatted dates inside cells. Use
      the `formatter` property on a column:'
  - name: Multiple Grids on One Page
    text: 'Just repeat steps 2‑5 with different container IDs:'
  type: HowTo
tags:
- gridjs
- JavaScript
- web‑development
title: Hogyan hozzunk létre Gridjs-et – Teljes JavaScript rács útmutató
url: /hu/python/integration-and-interoperability/how-to-create-gridjs-complete-javascript-grid-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan hozzunk létre Gridjs‑t – Teljes JavaScript rács útmutató

Valaha is elgondolkodtál **hogyan hozzunk létre gridjs**‑t, és azonnal egy elegáns adat táblát látsz az oldalon? Nem vagy egyedül. Sok fejlesztő elakad, amikor először próbálja összekapcsolni a Gridjs‑t, különösen a konfigurációs objektumnál és a render hívásnál. A jó hír? Valójában egyszerű, ha ismered a helyes lépéseket.

Ebben az útmutatóban egy valós példán keresztül mutatjuk be, **hogyan hozzunk létre gridjs**‑t a semmiből, hogyan készítsünk megfelelő **gridjs konfigurációt**, hogyan kössük a rácsot egy **gridjs konténerhez**, és végül hogyan indítsuk el a **gridjs render**‑t. A végére egy teljesen működő rácsot kapsz, amelyet bármely projektbe beilleszthetsz – nincs rejtély, csak tiszta kód.

## Amit meg fogsz tanulni

- Minimalista HTML oldal előkészítése a Gridjs‑hez.
- **gridjs konfiguráció** objektum írása, amely meghatározza az oszlopokat, az adatokat és a beállításokat.
- A Gridjs példány csatolása egy **gridjs konténer** elemhez.
- **gridjs render** meghívása a táblázat megjelenítéséhez.
- Gyakori beállítások (lapozás, rendezés, stílus) finomhangolása és a tipikus buktatók elkerülése.

Nem szükséges külső build eszköz; minden a böngészőben fut egyetlen script tag segítségével. Kezdjünk is bele.

## Előfeltételek

Mielőtt belevágnánk, győződj meg róla, hogy rendelkezel:

1. Modern böngészővel (Chrome, Edge, Firefox, Safari) – bármelyik, amely támogatja az ES6‑ot.
2. Alapvető HTML és JavaScript ismeretekkel – keretrendszer nem kell.
3. Hozzáféréssel a Gridjs könyvtárhoz – a CDN‑ről fogjuk betölteni, így nincs szükség npm‑es telepítésre.

Ennyi. Ha már van egy oldalad, amelyet fejleszteni szeretnél, egyszerűen illeszd be a kódrészleteket.

## 1. lépés: Gridjs erőforrások hozzáadása az oldalhoz

Először be kell töltenünk a Gridjs CSS‑ét és JavaScript‑ét. A CDN verzió könnyű és tökéletes gyors demókhoz.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to Create Gridjs Example</title>
  <!-- Gridjs CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <!-- The grid will appear inside this div -->
  <div id="grid"></div>

  <!-- Gridjs JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
```

> **Pro tipp:** A Mermaid téma tiszta, modern megjelenést ad a táblázatnak extra CSS nélkül. Nyugodtan cseréld le `classic.min.css`‑re, ha más stílust kedvelsz.

## 2. lépés: Definiáld a **gridjs konténert**

A **gridjs konténer** egy egyszerű `<div>`, amely a renderelt táblát fogja tartalmazni. A fenti markupban már létrehoztuk a `<div id="grid"></div>` elemet. Az `id` attribútum kulcsfontosságú, mert később ezzel kötjük össze a Gridjs példányt.

Ha több rácsot szeretnél egy oldalon, adj minden konténernek egyedi azonosítót (`grid1`, `grid2`, …) és ismételd meg a kötési logikát minden esetben.

## 3. lépés: Készíts egy **gridjs konfiguráció** objektumot

Most jön a **hogyan hozzunk létre gridjs** – a konfiguráció szíve. Ez a tiszta JavaScript objektum mondja meg a Gridjs‑nek, mely oszlopok jelenjenek meg, milyen adatokat töltsön be, és mely funkciókat engedélyezze.

```html
<script>
  // Step 3: Your gridjs configuration (replace with real data)
  const config = {
    columns: [
      { name: 'ID', width: '50px' },
      { name: 'Name' },
      { name: 'Email' },
      { name: 'Role' }
    ],
    data: [
      [1, 'Alice Johnson', 'alice@example.com', 'Admin'],
      [2, 'Bob Smith', 'bob@example.com', 'Editor'],
      [3, 'Carol White', 'carol@example.com', 'Viewer'],
      [4, 'David Brown', 'david@example.com', 'Admin']
    ],
    pagination: {
      limit: 2   // Show 2 rows per page
    },
    search: true,          // Enable client‑side search box
    sort: true,            // Allow column sorting
    language: {
      'search': {
        'placeholder': '🔍 Search…'
      },
      'pagination': {
        'previous': '←',
        'next': '→',
        'showing': 'Showing',
        'results': () => 'records'
      }
    }
  };
</script>
```

### Miért fontos ez a konfiguráció

- **Columns** – meghatározza a fejléc szövegét és opcionálisan a szélességet. Enélkül a Gridjs a első adat sorból próbálja kitalálni az oszlopneveket, ami gyakran kevésbé olvasható.
- **Data** – sorok tömbje, ahol minden sor egy cellaértékek tömbje. Megadhatsz egy async függvényt is, amely API‑ból tölti be az adatokat; a könyvtár automatikusan kezeli a promise‑okat.
- **Pagination** – korlátozza a sorok számát oldalanként, megakadályozva, hogy hatalmas táblázatok elárasszák a UI‑t.
- **Search & Sort** – egyetlen boolean‑al aktiválhatod az interaktív funkciókat, így elkerülve a saját kezelők írását.
- **Language** – testreszabhatod a felhasználói felület szövegeit, ami tökéletes a lokalizációhoz vagy a márkázáshoz.

Nyugodtan cseréld le a statikus adat tömböt egy fetch hívásra később; a többi lépés változatlan marad.

## 4. lépés: Hozd létre a Gridjs‑t és csatold a **gridjs konténerhez**

A konfiguráció készen áll, most létrehozzuk az új `GridJs.Grid`‑et (az UMD buildben a class neve `gridjs.Grid`) és a konténer elemhez rendeljük.

```html
<script>
  // Step 4: Create a Gridjs instance bound to the container
  const grid = new gridjs.Grid(document.getElementById('grid'), config);
</script>
```

Vedd észre, hogy a `document.getElementById('grid')`‑t használjuk – ez a **gridjs konténer**, amelyet korábban definiáltunk. Ha több konténered van, egyszerűen ismételd meg ezt a sort a megfelelő azonosítóval.

## 5. lépés: Hívd meg a **gridjs render** metódust

A kirakós utolsó darabja a **gridjs render** metódus. Ez veszi a korábban átadott konfigurációt, és egy teljesen stílusos `<table>`‑t injektál a konténerbe.

```html
<script>
  // Step 5: Render the grid inside the container
  grid.render();
</script>
</body>
</html>
```

Ennyi! Amikor megnyitod az oldalt a böngészőben, egy kereshető, lapozható táblázatot látsz a négy általunk definiált sorral. A keresőmező automatikusan megjelenik a tetején, a lapozó vezérlők pedig alul.

### Várható kimenet

```
+----+----------------+---------------------+--------+
| ID | Name           | Email               | Role   |
+----+----------------+---------------------+--------+
| 1  | Alice Johnson  | alice@example.com   | Admin  |
| 2  | Bob Smith      | bob@example.com     | Editor |
+----+----------------+---------------------+--------+
[←] [1] [2] [→]   Search: 🔍 Search…
```

A felhasználói felület reagál, ha a keresőmezőbe gépelsz, vagy a oszlopfejekre kattintva rendezel.

## Gyakori variációk és szélhelyzetek

### Aszinkron adatbetöltés

Ha az adataid egy szerveren vannak, cseréld le a statikus `data` tömböt egy olyan függvényre, amely Promise‑t ad vissza:

```js
const config = {
  columns: ['ID', 'Name', 'Email', 'Role'],
  data: () => fetch('/api/users')
                .then(res => res.json())
                .then(users => users.map(u => [u.id, u.name, u.email, u.role])),
  pagination: { limit: 10 },
  search: true,
  sort: true
};
```

A Gridjs egy betöltési spinner‑t mutat, amíg a promise feloldódik, majd automatikusan rendereli a táblázatot.

### Egyedi cella renderelés

Néha ikonokra, gombokra vagy formázott dátumokra van szükség a cellákban. Használd a `formatter` tulajdonságot egy oszlopnál:

```js
{
  name: 'Role',
  formatter: (cell) => {
    const color = cell === 'Admin' ? 'red' : 'gray';
    return gridjs.h('span', { style: { color } }, cell);
  }
}
```

A `gridjs.h` segédfüggvény virtuális DOM elemeket hoz létre anélkül, hogy React‑et kellene betölteni.

### Több rács egy oldalon

Egyszerűen ismételd meg a 2‑5. lépéseket különböző konténer ID‑kkel:

```html
<div id="usersGrid"></div>
<div id="ordersGrid"></div>

<script>
  const usersGrid = new gridjs.Grid(document.getElementById('usersGrid'), usersConfig);
  const ordersGrid = new gridjs.Grid(document.getElementById('ordersGrid'), ordersConfig);
  usersGrid.render();
  ordersGrid.render();
</script>
```

Minden rács önállóan működik, így keverheted a lapozási korlátokat, oszlopkészleteket és akár a témákat is.

## Pro tippek és elkerülendő hibák

- **Ne felejtsd el a CSS‑t** – a stíluslap nélkül a táblázat egyszerű HTML táblázatként jelenik meg, elveszítve a szép stílusokat és a lapozó vezérlőket.
- **Kerüld az azonos ID‑k duplikálását** – minden **gridjs konténer** egyedi azonosítóval kell rendelkezzen; különben a Gridjs felülírja az első példányt.
- **Figyelj az adat struktúrára** – az oszlopok számának meg kell egyeznie a sorokban lévő cellák számával; a nem egyező tömbök csendes elrendezési hibákat okozhatnak.
- **Használd a `gridjs.h`‑t komplex cellákhoz** – a nyers HTML stringek injektálása megtörheti a virtuális DOM diff algoritmust.
- **Figyelj a verzióra** – a fenti CDN link a legújabb 5.x kiadást mutatja (2026. június állapot szerint). Ha régebbi verzióra zárolsz, egyes opciók (például `language`) hiányozhatnak.

## Teljes működő példa (másold be)

Az alábbi teljes HTML fájlt mentsd el `gridjs-demo.html` néven, és nyisd meg közvetlenül a böngészőben.



## Mit érdemes még megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy könnyedén elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Aspose.Cells for Java: Hogyan hozzunk létre és formázzunk Excel munkafüzeteket hatékonyan](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Hogyan exportáljunk Excel‑t HTML‑re Aspose.Cells Java‑val | Munkafüzet műveletek útmutató](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Hogyan hozzunk létre és egyesítsünk Excel munkafüzeteket Aspose.Cells for Java‑val | Teljes útmutató](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}