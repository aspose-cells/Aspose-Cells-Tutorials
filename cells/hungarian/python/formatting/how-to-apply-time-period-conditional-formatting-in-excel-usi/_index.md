---
category: general
date: 2026-09-15
description: Tanulja meg, hogyan alkalmazzon időszak‑alapú feltételes formázást, és
  mentse a munkafüzetet XLSX formátumban az Aspose.Cells segítségével Pythonban. Lépésről‑lépésre
  kódot tartalmaz.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: hu
lastmod: 2026-09-15
og_description: Alkalmazzon időszakra vonatkozó feltételes formázást Excelben Python
  használatával, és mentse a munkafüzetet XLSX formátumban. Kövesse ezt a teljes útmutatót
  az Aspose.Cells-hez.
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: Időszak szerinti feltételes formázás alkalmazása Excelben Python segítségével
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  headline: How to apply time period conditional formatting in Excel using Python
  type: TechArticle
- description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  name: How to apply time period conditional formatting in Excel using Python
  steps:
  - name: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
    text: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
  - name: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
    text: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
  - name: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
    text: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
  - name: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
    text: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
  - name: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
    text: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
  - name: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
    text: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
  - name: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
    text: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
  - name: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
    text: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
  - name: The cell `I20` shows the text “Yesterday”.
    text: The cell `I20` shows the text “Yesterday”.
  - name: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
    text: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Hogyan alkalmazz időszak feltételes formázást az Excelben Python segítségével
url: /hu/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan alkalmazzunk időszak‑feltételes formázást Excelben Python segítségével

Ha **időszak‑feltételes formázásra** van szükséged egy Excel‑fájlban, ez a tutorial pontosan megmutatja, hogyan csináld Python‑nal. Látni fogsz egy teljes, futtatható példát, amely létrehozza a munkafüzetet, kiemeli a tegnapi dátumokat, és **elmenti a munkafüzetet XLSX‑ként** néhány sor kóddal.

A feltételes formázás hatékony módja annak, hogy felhívjuk a figyelmet azokra az adatokra, amelyek egy adott szabálynak megfelelnek. Ebben az útmutatóban a „Yesterday” (tegnap) időszakra koncentrálunk, de ugyanaz a minta más beépített időszakokra is működik, például Today, LastWeek és NextMonth. A tutorial végére képes leszel **excel workbook python**‑stílusú szkripteket írni, amelyek készen állnak a termelésre.

## Előfeltételek

- Python 3.8+ telepítve  
- `aspose-cells` és `aspose-pydrawing` csomagok (`pip install aspose-cells aspose-pydrawing`)  
- Alapvető ismeretek a Python szintaxisáról  

További Office‑telepítés nem szükséges, mivel az Aspose.Cells belsőleg kezeli a fájl generálását.

## Időszak‑feltételes formázás Aspose.Cells‑szel Pythonban

Ez a rész minden szükséges kódsort végigvezet a fő feladathoz. Az alábbi kódrészlet a teljes szkript; a megjegyzések magyarázzák az egyes lépések célját.

```python
# -*- coding: utf-8 -*-
"""
Apply time period conditional formatting to highlight yesterday's dates
and save the workbook as XLSX using Aspose.Cells for Python.
"""

from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the range that will receive the conditional formatting rule
cell_range = "I19:K20"
cond_format = worksheet.conditional_formattings.add(cell_range)

# Step 3: Add a TIME_PERIOD condition for “Yesterday” and style it
condition_index = cond_format.add_condition(FormatConditionType.TIME_PERIOD)
condition = cond_format[condition_index]
condition.style.background_color = Color.pink          # Highlight colour
condition.style.pattern = BackgroundType.SOLID        # Solid fill
condition.time_period = TimePeriodType.YESTERDAY      # Built‑in “Yesterday” period

# Step 4: Populate the range with sample dates (Excel number format 30 = short date)
date_cells = ["I19", "K20"]                           # Cells that will contain dates
sample_dates = [datetime(2008, 7, 30), datetime(2008, 8, 3)]
for cell_ref, date_val in zip(date_cells, sample_dates):
    cell = worksheet.cells.get(cell_ref)
    cell.put_value(date_val)                         # Write the Python datetime
    style = cell.get_style()
    style.number = 30                                 # Excel short date format
    cell.set_style(style)

# Step 5: Add a label so the user knows what the rule represents
worksheet.cells.get("I20").put_value("Yesterday")

# Step 6: Auto‑fit the column for better readability (column L is index 12)
worksheet.auto_fit_column(12)

# Step 7: Save the workbook – this demonstrates “save workbook as xlsx”
output_path = "TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

### Miért fontos minden egyes lépés

1. **A munkafüzet létrehozása** egy memóriában lévő Excel‑fájlt ad, amelyet manipulálhatsz anélkül, hogy megnyitnád az Excelt.  
2. **A tartomány meghatározása** (`I19:K20`) megmondja az Aspose.Cells‑nek, hol érvényesüljön a szabály, így a logika elkülönül.  
3. **TIME_PERIOD feltétel hozzáadása** az Aspose beépített enumerációjával `TimePeriodType.YESTERDAY`. Ez elkerüli a manuális dátumszámításokat, és automatikusan frissül, ha a fájlt más napon nyitják meg.  
4. **A stílus beállítása** (`background_color` és `pattern`) meghatározza, hogyan jelenjenek meg a kiemelt cellák. A `Color.pink` használata könnyen észrevehetővé teszi a szabályt.  
5. **Minta dátumok írása** a 30-as számformátummal biztosítja, hogy az Excel rövid dátumként, ne sorozatszámként jelenítse meg őket.  
6. **Az oszlop automatikus méretezése** javítja a későbbi olvashatóságot.  
7. **XLSX‑ként mentés** széles körben kompatibilis fájlt hoz létre, amely megnyitható Excelben, Google Sheets‑ben vagy bármely modern táblázatkezelőben.

## Hogyan hozzunk létre Excel munkafüzetet Python‑stílusban Aspose.Cells‑szel

A fenti szkript már bemutatja a **how to create excel workbook python** minimális lépéseit. Gyakorlatban előfordulhat, hogy szeretnél:

- Több munkalapot hozzáadni (`workbook.worksheets.add("Report")`).  
- Nagy adat táblákat feltölteni ciklusokkal vagy pandas DataFrame‑ekkel (`worksheet.cells.import_data_table`).  
- További formázásokat alkalmazni (betűtípusok, szegélyek) a `cell.get_style()` használatával.

Mindezek a műveletek ugyanazt a mintát követik: lekérdezed az objektumot, módosítod a tulajdonságait, és meghívod a `set_style` vagy `save` metódust.

## Feltételes formázás Python‑ban – egyéb hasznos minták

A „Yesterday” példán túl az Aspose.Cells több feltételes formázási típust is támogat:

| FormatConditionType                     | Tipikus felhasználási eset |
|-----------------------------------------|----------------------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION`      | Egyedi képletek (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE`      | Egyszerű összehasonlítások (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE`     | Színátmenetes skálák |
| `FORMAT_CONDITION_TYPE_DATA_BAR`        | Cellán belüli sávos megjelenítés |

Ahhoz, hogy **add conditional formatting python** egy numerikus küszöbértékhez, cseréld le a `FormatConditionType.TIME_PERIOD`‑t `FormatConditionType.CELL_VALUE`‑ra, és állítsd be a `condition.operator_type` és `condition.formula1` értékeket.

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## Munkafüzet mentése XLSX‑ként – legjobb gyakorlatok

Amikor **save workbook as xlsx**‑t hajtasz végre, vedd figyelembe:

- **A megfelelő `SaveFormat` megadása** (`SaveFormat.XLSX`) a régi formátumok elkerülése érdekében.  
- **Determinista fájlnév használata** ha a szkript ciklusban fut (`f"report_{datetime.now():%Y%m%d}.xlsx"`).  
- **Erőforrások lezárása** (`workbook.dispose()`) hosszú futású szolgáltatásoknál a natív memória felszabadításához.

A példa már a `SaveFormat.XLSX`‑et használja, amely modern, zip‑alapú munkafüzetet hoz létre, és megtartja az összes feltételes formázási szabályt.

## Tegnap kiemelése Excelben – ellenőrzési lépések

A szkript futtatása után nyisd meg a `TimePeriodExample.xlsx` fájlt:

1. Az `I19` és `K20` cellák a `30‑07‑2008` és `03‑08‑2008` dátumokat tartalmazzák.  
2. Az `I20` cella a „Yesterday” szöveget mutatja.  
3. Ha a rendszer dátumát **2008. július 30‑ra** állítod, és újra megnyitod a fájlt, a megfelelő dátumokkal rendelkező cellák automatikusan rózsaszínre színeződnek.  
4. A rendszer dátumának bármely más napra változtatása eltávolítja a rózsaszín kitöltést, ezzel megerősítve, hogy a szabály a **time period conditional formatting** logikára reagál.

## Gyakori hibák és elkerülésük

- **Hiányzó `aspose-pydrawing`** – a `Color` osztály ebben a csomagban van; ha nem telepíted, `ImportError` keletkezik.  
- **Helytelen számformátum** – az alapértelmezett General formátum sorozatszámokat (pl. 39822) mutat; mindig állítsd `style.number = 30`‑ra a rövid dátumokhoz.  
- **Tartomány eltérés** – a feltételes formázási tartománynak tartalmaznia kell a kiemelni kívánt cellákat; ellenkező esetben a szabály nem lesz hatásos.

## Pro tipp: a formázási rutin újrahasználata

Ha ugyanazt a „Yesterday” szabályt több munkafüzetben is használni szeretnéd, csomagold be egy segédfüggvénybe:

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

Hívd meg `apply_yesterday_highlight(worksheet, "A1:A10")`‑t bárhol, ahol szükséges.

## Összegzés

Ez az útmutató megmutatta, hogyan valósítsd meg a **time period conditional formatting**‑t Excelben Python segítségével, hogyan **save workbook as XLSX**, és hogyan **highlight yesterday in Excel** egyetlen, újrahasználható szkripttel. Most már szilárd alapod van a **add conditional formatting python** kód beillesztéséhez bármilyen automatizálási projekthez, legyen szó napi jelentések generálásáról, irányítópultok építéséről vagy adatexportok előkészítéséről.

**Következő lépések**

- Fedezd fel a többi `TimePeriodType` értéket, például `TODAY` vagy `LAST_WEEK`.  
- Kombinálj több feltételes szabályt ugyanazon a tartományon a gazdagabb vizuális jelzésekért.  
- Integráld a munkafüzet-generálást egy webszolgáltatásba vagy ütemezett feladatba.

Boldog kódolást, és élvezd a feltételes formázás által nyújtott vizuális tisztaságot Excel automatizálásodban!

## Mit tanulj meg legközelebb?

A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Master Conditional Formatting in Excel Using Aspose.Cells .NET : A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Master Aspose.Cells .NET : Apply Conditional Formatting to Alternate Rows in Excel](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [Master Conditional Formatting with Custom Fonts in Excel using Aspose.Cells for .NET and C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}