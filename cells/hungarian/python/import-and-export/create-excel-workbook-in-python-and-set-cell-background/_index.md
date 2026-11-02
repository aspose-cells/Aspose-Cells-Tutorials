---
category: general
date: 2026-10-07
description: Excel munkafüzet létrehozása Pythonban, cella háttérszín beállítása,
  oszlopok automatikus méretezése, és dátumok feltöltése Excelbe egy tömör kódrészlettel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: hu
lastmod: 2026-10-07
og_description: Készíts Excel munkafüzetet Pythonban, majd állítsd be a cellák háttérszínét,
  automatikusan igazítsd az oszlopok szélességét, és töltsd fel dátumokkal az Excelt.
  Kövesd ezt a lépésről‑lépésre útmutatót a TimePeriodDemo.xlsx fájl létrehozásához.
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: Excel munkafüzet létrehozása Pythonban – háttér beállítása és automatikus
  méretezés
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  headline: Create Excel workbook in Python and set cell background
  type: TechArticle
- description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  name: Create Excel workbook in Python and set cell background
  steps:
  - name: Import required namespaces and define a helper function
    text: '```python # Step 1: Import Aspose.Cells classes and supporting modules
      from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType,
      SaveFormat from aspose.pydrawing import Color from datetime import datetime
      import os ```'
  - name: Create the workbook and get the first worksheet
    text: '```python def create_workbook(): # Step 2: Instantiate a new workbook (empty
      Excel file) book = Workbook() # Aspose.Cells creates a default worksheet; we
      retrieve it for further work sheet = book.worksheets[0] return book, sheet ```'
  - name: Set cell background color with a conditional format
    text: '```python def add_yesterday_rule(sheet): # Define a conditional format
      for the range I19:K20 (Yesterday) conds = sheet.get_range("I19:K20").format_conditions
      idx = conds.add_condition(FormatConditionType.TIME_PERIOD) cond = conds[idx]'
  - name: Populate dates in Excel
    text: '```python def populate_sample_dates(sheet): # Insert a date that falls
      on yesterday relative to the demo data cell = sheet.cells.get("I19") cell.put_value(datetime(2008,
      7, 30)) # sample date cell.style.number = 30 # Excel’s date format ID cell.set_style(cell.style)'
  - name: Auto‑fit Excel columns for better visibility
    text: '```python def auto_fit_columns(sheet): # Auto‑fit column L (index 12) so
      the content is fully visible sheet.auto_fit_column(12) # <-- auto fit excel
      columns ```'
  - name: Save the workbook
    text: '```python def save_workbook(book, filename="TimePeriodDemo.xlsx"): out_path
      = os.path.join("YOUR_DIRECTORY", filename) os.makedirs(os.path.dirname(out_path),
      exist_ok=True) book.save(out_path, SaveFormat.XLSX) print(f"Workbook saved to:
      {out_path}") ```'
  - name: Full script – putting it all together
    text: '```python def main(): # Create workbook and obtain the first worksheet
      book, sheet = create_workbook()'
  type: HowTo
tags:
- Excel
- Python
- Aspose.Cells
title: Excel munkafüzet létrehozása Pythonban és a cella háttér beállítása
url: /hu/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel munkafüzet létrehozása Pythonban és cellaháttér beállítása

Excel munkafüzet létrehozása Pythonban és feltételes formázás alkalmazása néhány kódsorral. Ez a bemutató megmutatja, **how to create excel** fájlokat programozott módon, hogyan állítsuk be a cella háttérszínét, hogyan automatikusan méretezzük az Excel oszlopokat, és hogyan töltsünk fel dátumokat Excelbe az Aspose.Cells könyvtár segítségével.

Megtanulja, hogyan:
* Munkafüzet inicializálása és az első munkalap lekérése.  
* Feltételes formátum definiálása, amely kiemeli a „Yesterday” (tegnapi) dátumokat.  
* Minta dátumok beszúrása meghatározott cellákba.  
* Oszlopok automatikus méretezése, hogy az adatok jól láthatóak legyenek.  
* Munkafüzet mentése egy kiválasztott mappába.

Az egyetlen előfeltétel egy működő Python 3 környezet, a `aspose-cells` és `aspose-pydrawing` csomagok telepítésével:

```bash
pip install aspose-cells aspose-pydrawing
```

---

## Excel munkafüzet létrehozása Pythonban – lépésről lépésre

Az alábbi szakaszok a folyamatot kezelhető lépésekre bontják. Minden lépés tartalmazza a szükséges kódot, egy magyarázatot arra, hogy **miért** fontos, és egy tippet a gyakori buktatók elkerüléséhez.

### 1. lépés: Szükséges névterek importálása és segédfüggvény definiálása

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*Miért fontos*: A megfelelő osztályok importálása hozzáférést biztosít a munkafüzet létrehozásához, a feltételes formázáshoz és a színkezeléshez.  
**Pro tipp**: Tartsd az importokat a fájl tetején; ez megkönnyíti a szkript olvasását és megakadályozza a körkörös import hibákat.

### 2. lépés: Munkafüzet létrehozása és az első munkalap lekérése

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

A `Workbook()` konstruktor egy üres Excel munkafüzetet hoz létre a memóriában.  
**Miért**: Egy friss munkafüzet használata biztosítja, hogy ne legyenek maradék formázások az előző futtatásokból.

### 3. lépés: Cellaháttér szín beállítása feltételes formátummal

```python
def add_yesterday_rule(sheet):
    # Define a conditional format for the range I19:K20 (Yesterday)
    conds = sheet.get_range("I19:K20").format_conditions
    idx = conds.add_condition(FormatConditionType.TIME_PERIOD)
    cond = conds[idx]

    # Apply visual style – this is where we set the cell background color
    cond.style.background_color = Color.pink          # <-- set cell background color
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

*Miért*: Egy **time period** (időszak) feltétel használata automatikusan kiemeli azokat a cellákat, amelyek tegnapi dátumot tartalmaznak, így elkerülve a manuális dátumellenőrzéseket.  
**Tipp**: A `Color.pink` csak egy példa; használhatsz bármilyen `Color` objektumot (`Color.yellow`, `Color.light_green`, stb.).

### 4. lépés: Dátumok feltöltése Excelbe

```python
def populate_sample_dates(sheet):
    # Insert a date that falls on yesterday relative to the demo data
    cell = sheet.cells.get("I19")
    cell.put_value(datetime(2008, 7, 30))   # sample date
    cell.style.number = 30                 # Excel’s date format ID
    cell.set_style(cell.style)

    # Insert another date outside the “Yesterday” range
    cell = sheet.cells.get("K20")
    cell.put_value(datetime(2008, 8, 3))
    cell.style.number = 30
    cell.set_style(cell.style)

    # Add a label for the rule
    sheet.cells.get("I20").put_value("Yesterday")
```

Itt **dátumokat töltünk fel Excelbe** a `I19` és `K20` cellákba. Az első dátum aktiválja a feltételes formázást, míg a második nem.  
**Miért fontos**: A megfelelő és nem megfelelő értékek bemutatása segít ellenőrizni, hogy a szabály a várt módon működik.

### 5. lépés: Excel oszlopok automatikus méretezése a jobb láthatóság érdekében

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

Az `auto_fit_column` a legnagyobb cellaérték alapján állítja be az oszlop szélességét.  
**Tipp**: Hívd meg ezt az összes adat írása után; különben a szélesség hiányos tartalom alapján számítható ki.

### 6. lépés: Munkafüzet mentése

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

A fájl mentése az in‑memory munkafüzetet a lemezre írja a modern XLSX formátumban.  

### Teljes szkript – minden összeállítása

```python
def main():
    # Create workbook and obtain the first worksheet
    book, sheet = create_workbook()

    # Apply conditional formatting (set cell background color)
    add_yesterday_rule(sheet)

    # Populate the demo dates (populate dates in excel)
    populate_sample_dates(sheet)

    # Auto‑fit the relevant column (auto fit excel columns)
    auto_fit_columns(sheet)

    # Persist the file
    save_workbook(book)

if __name__ == "__main__":
    main()
```

**Várható kimenet**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Nyissa meg a generált fájlt Excelben – a `I19:K20` cellák rózsaszín háttérrel jelenítik meg a „Yesterday” (tegnap) dátumot, és az L oszlop elég széles lesz a címke megjelenítéséhez vágás nélkül.

---

## Miért működik ez a megközelítés a legjobban

* **Egylépéses munkafolyamat** – Minden művelet ugyanazon a `Workbook` példányon történik, elkerülve a felesleges I/O-t.  
* **Feltételes formázás** – A `FormatConditionType.TIME_PERIOD` használata lehetővé teszi, hogy az Excel kezelje a dátumlogikát, ami megbízhatóbb, mint egyedi Python dátumellenőrzések írása.  
* **Kifejezett stílus** – A `background_color` és a `pattern` beállítása garantálja a vizuális eredményt az Excel verziók között.  
* **Auto‑fit after data**  

## Mit érdemes következőként megtanulni?

Az alábbi bemutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódpéldákat tartalmaz lépésről lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [Excel munkafüzet létrehozása Python – Teljes útmutató](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Excel munkafüzet létrehozása Python – Teljes lépésről lépésre útmutató](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Excel munkafüzet létrehozása Python – Teljes útmutató Lambda-val](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}