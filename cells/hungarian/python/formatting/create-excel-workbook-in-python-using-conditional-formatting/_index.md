---
category: general
date: 2026-09-21
description: Tanulja meg, hogyan hozhat létre Excel munkafüzetet Pythonban, állíthatja
  be a cella háttérszínét, és alkalmazhat dátum alapú feltételes formázást az Aspose.Cells
  segítségével.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: hu
lastmod: 2026-09-21
og_description: Excel munkafüzet létrehozása Pythonban, cella háttérszín beállítása,
  és dátum alapú feltételes formázás alkalmazása az Aspose.Cells segítségével. Kövesse
  a lépésről‑lépésre útmutatót.
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: Excel munkafüzet létrehozása Pythonban feltételes formázással
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to create Excel workbook in Python, set cell background color,
    and apply date based conditional formatting with Aspose.Cells.
  headline: Create Excel workbook in Python using conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Excel munkafüzet létrehozása Pythonban feltételes formázással
url: /hu/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel munkafüzet létrehozása Pythonban feltételes formázással

Ha **excel workbook python** szkripteket szeretnél készíteni, amelyek automatikusan kiemelik a dátumokat, ez az útmutató pontosan megmutatja, hogyan. Megtanulod, hogyan **állíts be cella háttérszínt**, adj hozzá egy „Tegnap” szabályt, és mentsd el a fájlt – mindezt az Aspose.Cells for Python segítségével.

Az Excel‑fájlok programozott kezelése gyakran azt jelenti, hogy ugyanazt a formázási logikát sok munkalapon ismételjük. A tutorial végére egy újrahasználható mintát kapsz **excel conditional formatting python**‑hez, amelyet bármely projektbe beilleszthetsz.

## Előfeltételek

- Python 3.8+ telepítve  
- `aspose-cells` csomag (`pip install aspose-cells`)  
- Alapvető ismeretek a Python függvényekről és a datetime modulról  

További könyvtárak nem szükségesek; az Aspose.Cells kezeli az összes Excel‑műveletet.

## 1. lépés: A munkafüzet létrehozása és az első munkalap elérése

Az első lépés a **create excel workbook python** objektumok létrehozása és az alapértelmezett munkalap lekérése. Ez egy tiszta vászonként szolgál a további stílusokhoz.

```python
# Import required Aspose.Cells classes
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# Create a new workbook; the first worksheet is at index 0
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Miért fontos:* A `Workbook()` egy memóriában lévő Excel‑fájlt hoz létre. A `worksheets[0]` elérése elkerüli a munkalapnevek hard‑kódolását, és akkor is működik, ha az alapértelmezett név megváltozik.

## 2. lépés: Segédfüggvény a TIME_PERIOD feltételes formátum hozzáadásához

A kód rendezett tartása érdekében a feltételes formátum létrehozását egy segédfüggvénybe csomagoljuk. A függvény egy cellatartományt, egy háttérszínt és a kívánt időszak‑szabályt kapja paraméterként.

```python
def add_time_period(sheet, cell_range, bg_color, period_type):
    """
    Adds a TIME_PERIOD conditional formatting rule to `cell_range`.
    The rule paints the cells with `bg_color` when the date matches `period_type`.
    """
    # Retrieve (or create) the ConditionalFormatting collection for the range
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)

    # Insert a TIME_PERIOD condition and configure its style
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color          # set cell background color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type                # e.g., TimePeriodType.YESTERDAY
```

*Miért fontos:* A segédfüggvény elrejti a feltételes formátum létrehozásának ismétlődő lépéseit, így könnyen újrahasználható más dátumalapú szabályokhoz, például „Ma” vagy „Múlt hét” esetén.

## 3. lépés: A „Tegnap” szabály alkalmazása egy tartományra

Most a segédfüggvényt használjuk, hogy kiemeljük azokat a cellákat, amelyek a tegnapi dátumot tartalmazzák. A `I19:K20` tartomány **medium sea green** színűre vált, ha a feltétel teljesül.

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*Miért fontos:* A `TimePeriodType.YESTERDAY` az Aspose.Cells beépített enumerációjának része, így nem kell manuálisan számolni a dátumokat. A könyvtár minden alkalommal kiértékeli a szabályt, amikor a munkafüzetet megnyitják.

## 4. lépés: A tartomány feltöltése mintadátumokkal

A szabály működésének bemutatásához két dátumot írunk – egyet, amely megfelel a „Tegnap” szabálynak, és egyet, amely nem. A `number` stílus `30` egy beépített dátumformátumnak felel meg.

```python
# Cell I19 gets a date that is exactly yesterday (relative to the sample data)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))   # 30 July 2008
cell.style.number = 30                # date format

# Cell K20 gets a date that is outside the rule
cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))    # 3 August 2008
cell.style.number = 30
```

*Miért fontos:* Konkrét dátumok beillesztésével ellenőrizheted, hogy a feltételes formázás működik‑e anélkül, hogy egy adott napon kellene megnyitnod a fájlt.

## 5. lépés: Leíró címke hozzáadása és oszlop automatikus méretezése

Egy kis címke tisztázza a formázott tartomány célját, a `auto_fit_column` pedig olvashatóvá teszi a lapot.

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## 6. lépés: A munkafüzet mentése

Végül írjuk a munkafüzetet a lemezre. Az `os.makedirs` hívás biztosítja, hogy a célmappa létezzen.

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Amikor megnyitod a *TimePeriodDemo.xlsx* fájlt, a következőket látod:

- A **I19** cella **medium sea green** színűre van árnyalva, mert az értéke megfelel a „Tegnap” szabálynak.  
- A **K20** cella az alapértelmezett háttérrel marad, mivel a dátuma nem teljesíti a feltételt.  

Ez bemutatja, hogyan **format cells by date** egyetlen Python‑sorral.

## Teljes, futtatható példa

Az összes részt összevonva itt a teljes szkript, amelyet egyszerűen másolj‑be és futtass:

```python
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# 1️⃣ Create workbook and get first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# 2️⃣ Helper to add TIME_PERIOD conditional formatting
def add_time_period(sheet, cell_range, bg_color, period_type):
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type

# 3️⃣ Apply “Yesterday” rule (set cell background color)
add_time_period(
    worksheet,
    "I19:K20",
    Color.medium_sea_green,
    TimePeriodType.YESTERDAY
)

# 4️⃣ Fill sample dates (format cells by date)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))
cell.style.number = 30

cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))
cell.style.number = 30

# 5️⃣ Add label and auto‑fit column
worksheet.cells.get("I20").put_value("Yesterday")
worksheet.auto_fit_column(12)

# 6️⃣ Save the workbook
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Futtasd a szkriptet, nyisd meg a keletkezett fájlt, és láthatod a feltételes formázás működését.

## Gyakori variációk és szélhelyzetek

| Változat | Hogyan valósítható meg | Mikor használjuk |
|-----------|------------------------|-------------------|
| **„Ma” kiemelése** | Cseréld le a `TimePeriodType.YESTERDAY`‑t `TimePeriodType.TODAY`‑ra | Valós‑idő dashboardok |
| **Több tartomány** | Hívd meg az `add_time_period`‑t minden tartományra, különböző színekkel | Összetett jelentések |
| **Dinamikus dátumtartomány** | Használd a `TimePeriodType.LAST_7_DAYS`‑t vagy a `TimePeriodType.NEXT_MONTH`‑t | Forgó jelentések |
| **Egyedi szín** | Használd a `Color.from_argb(255, r, g, b)`‑t bármely árnyalat létrehozásához | Márka‑konzisztens stílus |

**Pro tipp:** Mindig állítsd be a `condition.style.pattern = BackgroundType.SOLID`‑t, ha szilárd kitöltést szeretnél; különben az Excel egy olyan gradientet jeleníthet meg, amely verziók között nem egységes.

## Összegzés

Most már tudod, hogyan **create Excel workbook python** szkripteket készíts, amelyek **set cell background color**, alkalmazzák a **excel conditional formatting python**‑t, és **format cells by date**‑et az Aspose.Cells segítségével. A példa egy **date based conditional formatting** szcenáriót fed le, de ugyanaz a minta bármely időszak‑szabályra alkalmazható.

A következő lépéseket is érdemes felfedezni:

- Adatsávok vagy ikonkészletek hozzáadása (`FormatConditionType.DATA_BAR`)  
- Több feltételes szabály kombinálása ugyanazon a tartományon  
- A munkafüzet exportálása PDF‑be (`SaveFormat.PDF`) jelentéskészítéshez  

Nyugodtan kísérletezz különböző színekkel, tartományokkal és időszak‑típusokkal, hogy a saját jelentési igényeidhez igazodjanak. Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Az Excel cellaformázás és munkafüzet‑kezelés elsajátítása Aspose.Cells for .NET segítségével](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel automatizálás Aspose.Cells .NET‑vel: munkafüzet létrehozása és külső hivatkozások beállítása](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Hogyan hozzunk létre munkafüzet‑szintű névvel ellátott tartományokat Excelben az Aspose.Cells .NET használatával](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}