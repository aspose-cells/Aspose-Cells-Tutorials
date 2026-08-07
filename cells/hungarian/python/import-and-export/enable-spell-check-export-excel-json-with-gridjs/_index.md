---
category: general
date: 2026-06-21
description: Engedélyezze a helyesírás-ellenőrzést, miközben a GridJs segítségével
  exportálja az Excel JSON-t. Tanulja meg, hogyan konvertálja az xlsx-et JSON-re,
  állítsa be a lusta betöltést, és töltse be hatékonyan az Excel munkafüzetet.
draft: false
keywords:
- enable spell check
- export excel json
- convert xlsx to json
- configure lazy loading
- load excel workbook
language: hu
og_description: Engedélyezze a helyesírás-ellenőrzést az Excel JSON exportálásakor
  a GridJs-szel. Ez az útmutató bemutatja, hogyan konvertálhatja az xlsx-et JSON formátumba,
  hogyan konfigurálja a lusta betöltést, és hogyan tölthet be egy Excel munkafüzetet.
og_title: Engedélyezze a helyesírás-ellenőrzést & Exportálja az Excel JSON-t a GridJs-sel
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Enable spell check while you export Excel JSON using GridJs. Learn
    to convert xlsx to JSON, configure lazy loading, and load Excel workbook efficiently.
  headline: Enable Spell Check & Export Excel JSON with GridJs
  type: TechArticle
tags:
- GridJs
- Excel
- JSON
- Python
title: Helyesírás-ellenőrzés engedélyezése és Excel JSON exportálása a GridJs-sel
url: /hu/python/import-and-export/enable-spell-check-export-excel-json-with-gridjs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Helyesírás-ellenőrzés engedélyezése és Excel JSON exportálása GridJs-szel

Valaha is szükséged volt **helyesírás-ellenőrzés engedélyezésére** egy web‑alapú táblázatkezelő felhasználói felületen, és azon tűnődtél, hogyan lehet egyszerre JSON‑ként kinyerni az adatokat? Nem vagy egyedül. Sok fejlesztő ugyanazon a problémán akadt el, amikor **Excel JSON‑t exportálni** próbál egy munkafüzetből, miközben az olyan fejlett funkciók, mint a képletvalidáció, megmaradnak.

Ebben az útmutatóban egy teljes, futtatható példán keresztül vezetünk végig, amely megmutatja, hogyan **töltsd be az Excel munkafüzetet**, alakítsd JSON payload‑dá a GridJs-szel, **konfiguráld a lusta betöltést**, és természetesen **engedélyezd a helyesírás-ellenőrzést**. A végére **xlsx‑t JSON‑ná** tudod konvertálni néhány sorban – semmi rejtély, semmi hiányzó rész.

> **Mit fogsz megtanulni**  
> * Egy Python szkript, amely beolvassa a `.xlsx` fájlt, elindít egy GridJs szerver objektumot, és írja a `grid_data.json`-t.  
> * Megértés arról, miért fontos minden opció (helyesírás-ellenőrzés, képlet-ellenőrzés, lusta betöltés).  
> * Tippek a megoldás nagyobb munkafüzetekre való skálázásához.

## Előfeltételek

Mielőtt belemerülnénk, győződj meg róla, hogy a következők telepítve vannak a gépeden:

| Követelmény | Miért fontos |
|-------------|--------------|
| Python 3.9+ | A lent használt `cells` csomaghoz szükséges. |
| `cells` könyvtár (`pip install cells`) | Biztosítja a `Workbook` és `GridJs` osztályokat. |
| Egy minta Excel fájl (`sample.xlsx`) | Ez lesz a forrás, amelyből **load excel workbook**-ot fogunk betölteni. |
| Írási jogosultság a kimeneti mappához | A `grid.save()` lépéshez szükséges. |

Ha bármelyik ismeretlennek tűnik, állj meg és telepítsd előbb – különben a szkript import hibát dob.

## 1. lépés: Excel munkafüzet betöltése

Az első dolog, amit meg kell tenned, ha **convert xlsx to json**-t szeretnél, a munkafüzet megnyitása. Olyan, mintha kinyitnád az ajtót, mielőtt berakodnád a szobát.

```python
import cells

# Replace YOUR_DIRECTORY with the actual path on your system
workbook_path = "YOUR_DIRECTORY/sample.xlsx"

# Load the workbook – this is the entry point for all further operations
workbook = cells.Workbook(workbook_path)
print(f"Workbook loaded: {workbook_path}")
```

> **Pro tipp:** Ha a fájlod hatalmas, fontold meg a `cells.Workbook(..., read_only=True)` használatát a memóriafogyasztás csökkentése érdekében.

## 2. lépés: GridJs szerver objektum létrehozása

Miután a munkafüzet a memóriában van, szükségünk van egy **GridJs** objektumra, amely a lapokat JSON‑ná alakítja, hogy a kliens UI felhasználhassa.

```python
# Create a GridJs instance linked to the workbook
grid = cells.GridJs(workbook)
print("GridJs server object created.")
```

A `grid` változó lényegében egy vékony burkoló a munkafüzet körül, amely tudja, hogyan sorosítsa a cellákat, képleteket és még a stílusinformációkat is.

## 3. lépés: Helyesírás-ellenőrzés engedélyezése (és képlet-ellenőrző)

Itt jön képbe a fő kulcsszó. Az `enableSpellCheck` jelző átkapcsolásával a végfelhasználók egy biztonsági hálót kapnak a gépelési hibák ellen – akárcsak az asztali Excelben.

```python
# Turn on advanced validation features
grid.options["enableFormulaChecker"] = True   # optional but handy
grid.options["enableSpellCheck"] = True       # <-- enable spell check
print("Spell check and formula checker enabled.")
```

Miért engedélyezzük mindkettőt? A helyesírás-ellenőrzés elkapja a szöveges hibákat, míg a képlet-ellenőrző megvédi a hibás számításokat. Együtt a webes UI-t olyan kifinomulttá teszik, mint a natív Excel élmény.

## 4. lépés: Lusta betöltés konfigurálása

Ha több ezer sorral dolgozol, az egész adathalmaz egyetlen payload‑ben történő küldése leterheli a böngészőt. **Konfiguráld a lusta betöltést**, hogy az adatot falatnyi darabokban (példánkban 500 sor kérésenként) küldd.

```python
# Lazy loading improves performance for large sheets
grid.options["lazyLoading"] = {"pageSize": 500}
print("Lazy loading configured: 500 rows per request.")
```

A `pageSize` értékét a hálózati feltételeidhez igazíthatod. A kisebb oldalak több körutazást jelentenek, de simább UI‑t; a nagyobb oldalak kevesebb hívást eredményeznek, de késleltetést okozhatnak.

## 5. lépés: Excel JSON exportálása

Minden nehéz munka most már a háttérben zajlik. Az utolsó lépés a **export excel json** egy olyan fájlba, amelyet a front‑end kérhet.

```python
# Destination for the generated JSON
output_path = "YOUR_DIRECTORY/grid_data.json"

# Persist the JSON representation
grid.save(output_path)
print(f"JSON exported to: {output_path}")
```

Amikor a `save` metódus befejeződik, egy rendezett `grid_data.json` áll rendelkezésedre, amely a következőket tartalmazza:

* Lapnevek és azonosítók  
* Soradatok (értékek, képletek és formázás)  
* Metaadatok az engedélyezett funkciókról (helyesírás-ellenőrzés, lusta betöltés, stb.)

Az eredményt ellenőrizheted a fájl szövegszerkesztőben való megnyitásával vagy a böngésző konzoljában való betöltésével:

```json
{
  "sheets": [
    {
      "name": "Sheet1",
      "rows": [
        {"c": [{"v": "Hello"}, {"v": 123}]},
        {"c": [{"v": "World"}, {"v": 456}]}
      ]
    }
  ],
  "options": {
    "enableSpellCheck": true,
    "enableFormulaChecker": true,
    "lazyLoading": {"pageSize": 500}
  }
}
```

Ez egy **teljes, önálló megoldás** egy Excel fájl JSON payload‑dá alakításához, miközben a helyesírás-ellenőrzés működik.

## Teljes szkript – Összeállítás

Az alábbiakban a teljes program látható, amelyet másolhatsz, módosíthatod az elérési útvonalakat, és futtathatsz. Nincsenek rejtett lépések, nincs külső szkript – csak egy fájl.

```python
import cells

# ----------------------------------------------------------------------
# Configuration – adjust these variables to match your environment
# ----------------------------------------------------------------------
WORKBOOK_PATH = "YOUR_DIRECTORY/sample.xlsx"
OUTPUT_JSON = "YOUR_DIRECTORY/grid_data.json"
PAGE_SIZE = 500   # rows per lazy‑load request

# ----------------------------------------------------------------------
# 1️⃣ Load the Excel workbook
# ----------------------------------------------------------------------
workbook = cells.Workbook(WORKBOOK_PATH)
print(f"[✓] Loaded workbook from {WORKBOOK_PATH}")

# ----------------------------------------------------------------------
# 2️⃣ Create GridJs server object
# ----------------------------------------------------------------------
grid = cells.GridJs(workbook)
print("[✓] GridJs instance ready")

# ----------------------------------------------------------------------
# 3️⃣ Enable spell check + formula checking
# ----------------------------------------------------------------------
grid.options["enableFormulaChecker"] = True
grid.options["enableSpellCheck"] = True
print("[✓] Spell check and formula checker enabled")

# ----------------------------------------------------------------------
# 4️⃣ Configure lazy loading for performance
# ----------------------------------------------------------------------
grid.options["lazyLoading"] = {"pageSize": PAGE_SIZE}
print(f"[✓] Lazy loading set to {PAGE_SIZE} rows per request")

# ----------------------------------------------------------------------
# 5️⃣ Export the workbook as JSON
# ----------------------------------------------------------------------
grid.save(OUTPUT_JSON)
print(f"[✓] Exported JSON to {OUTPUT_JSON}")
```

Mentsd el `export_gridjs.py` néven, és futtasd:

```bash
python export_gridjs.py
```

Egy sor `[✓]` üzenetet kell látnod, amelyek megerősítik, hogy minden lépés sikeres volt.

## Gyakori kérdések és szélhelyzetek

**Mi van, ha a munkafüzete több lapot tartalmaz?**  
A GridJs automatikusan végigiterál minden lapon, így a kapott JSON egy `sheets` tömböt tartalmaz majd. A kliensek oldalon szűrhetsz, ha csak egy részhalmazra van szükséged.

**Letilthatom a helyesírás-ellenőrzést egy adott lapon?**  
Az `options` szótár globálisan érvényes. Per‑lap kapcsoláshoz külön `GridJs` objektumokat kell létrehozni, vagy utólag feldolgozni a JSON‑t.

**A fájlom nagyobb, mint 10 MB – a lusta betöltés még mindig segít?**  
Természetesen. A lusta betöltés az API szinten működik; a szerver csak a kért oldalt streameli. Ha alacsony a hálózati késleltetés, fontold meg a `pageSize` 1000-re növelését.

**Aggódom-e az Unicode karakterek miatt?**  
A `cells` alapból kezeli az UTF‑8-at, így az emoji‑k vagy a nem latin írásrendszerek is megmaradnak a körúton.

## Pro tippek a produkcióhoz

* **Cache-eld a JSON‑t** – Ha a munkafüzet ritkán változik, cache-eld a `grid_data.json`-t egy CDN‑ben a villámgyors betöltésért.  
* **Biztonság** – Soha ne tedd elérhetővé a nyers Excel fájlt; csak a generált JSON‑t szolgáld ki.  
* **Verziókezelés** – Tedd bele a verziószámot a JSON fájlnévbe (pl. `grid_data_v2.json`), hogy elkerüld a régi adatok használatát frissítések után.  
* **Tesztelés** – Írj egy kis egységtesztet, amely betölti a JSON‑t és ellenőrzi, hogy az `enableSpellCheck` `true`. Így korán elkapja a regressziókat.

## Következtetés

Most már egy szilárd, vég‑től‑végig megoldásod van a **helyesírás-ellenőrzés engedélyezésére**, miközben a **Excel JSON‑t exportálod** a GridJs használatával. A **excel munkafüzet betöltésétől** a **lusta betöltés konfigurálásáig**, végül a **convert xlsx to json**-ig a folyamat egyértelmű és készen áll a produkcióra.  

Mi a következő lépés? Próbáld meg a generált `grid_data.json`-t egy egyszerű HTML oldalba ágyazni, amely a GridJs kliens könyvtárat használja, kísérletezz egyedi cella renderelőkkel, vagy adj hozzá hitelesítést a JSON végponthoz. A lehetőségek határtalanok, ha a helyesírás-ellenőrzést, a lusta betöltést és a zökkenőmentes Excel‑JSON konverziót kombinálod.

Van még kérdésed vagy egy nehéz munkafüzeted, amivel küzdesz? Írj egy megjegyzést alább, és jó kódolást!

![Helyesírás-ellenőrzés engedélyezése GridJs-ben](/images/enable-spell-check-gridjs.png "Képernyőkép, amely a GridJs UI-ban engedélyezett helyesírás-ellenőrzést mutat")

## Mit érdemes még megtanulni?

Az alábbi útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Exportálj Excel-t JSON-ba](/cells/english/java/excel-import-export/export-excel-to-json/)
- [JSON adatok importálása Excel-be Aspose.Cells Java használatával: Átfogó útmutató](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Hogyan szűrd hatékonyan az adatokat Excel munkafüzetek betöltésekor Aspose.Cells Java használatával](/cells/english/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}