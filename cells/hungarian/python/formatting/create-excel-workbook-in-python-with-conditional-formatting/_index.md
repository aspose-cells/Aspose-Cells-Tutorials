---
category: general
date: 2026-09-05
description: Készítsen Excel munkafüzetet Pythonban, és adjon hozzá feltételes formázást
  a tegnapi cellák kiemeléséhez. Ismerje meg a teljes kódot és azt, hogy miért fontos
  minden lépés.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: hu
lastmod: 2026-09-05
og_description: Hozzon létre Excel munkafüzetet Pythonban, és adjon hozzá feltételes
  formázást a tegnapi cellák kiemeléséhez. Kövesse ezt a lépésről‑lépésre útmutatót
  a teljes megoldáshoz.
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: Excel munkafüzet létrehozása Pythonban – feltételes formázás hozzáadása
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create Excel workbook in Python and add conditional formatting to highlight
    yesterday cells. Learn the full code and why each step matters.
  headline: Create Excel workbook in Python with conditional formatting
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Excel munkafüzet létrehozása Pythonban feltételes formázással
url: /hu/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel munkafüzet létrehozása Pythonban feltételes formázással

Ha **Excel munkafüzetet kell létrehozni Pythonban** egy jelentési feladathoz, ez az útmutató megmutatja, hogyan generálj egy munkafüzetet, és alkalmazz egy feltételes formázási szabályt, amely kiemeli a tegnapi dátumokat. Meg fogod látni a pontos kódot, hogy miért van minden sor, és hogyan lehet a megoldást más dátumtartományokra adaptálni.

A feltételes formázás hatékony módja annak, hogy felhívjuk a figyelmet azokra az adatokra, amelyek egy adott feltételnek megfelelnek. Ebben a tutorialban az Aspose.Cells könyvtárat használjuk Python via .NET‑en, amely teljes Excel‑funkcionalitást biztosít Microsoft Office nélkül. A útmutató végére egy olyan fájlt kapsz, ahol az *I19:K20* tartomány cellái rózsaszínre váltanak, ha tegnapi dátumot tartalmaznak.

## Előfeltételek

Mielőtt elkezdenéd, győződj meg róla, hogy:

* Python 3.9+ telepítve van
* `aspose-cells` csomag (telepítsd a `pip install aspose-cells` paranccsal)
* Alapvető ismeretek a Python szintaxisáról
* Írási jogosultság a könyvtárban, ahová a munkafüzetet menteni fogod

A kód Windows, macOS és Linux rendszereken is működik, amennyiben a .NET runtime elérhető.

## Excel munkafüzet létrehozása Pythonban

Az első lépés egy `Workbook` objektum példányosítása és az alapértelmezett munkalap lekérése. Ez az objektum a teljes Excel‑fájlt reprezentálja a memóriában.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Miért fontos*: A `Workbook()` egy üres munkafüzetet hoz létre egyetlen munkalappal. A `worksheets[0]` elérése egy kezelőt ad, amellyel később adatokat, stílusokat és formázást adhatunk hozzá.

## Feltételes formázási tartomány hozzáadása

Ezután definiáljuk azt a területet, amelyet a feltételes szabály kiértékel. Az `I19:K20` tartomány hat cellát fed le két sorban.

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*Miért fontos*: Egy feltételes formázási gyűjtemény hozzáadása egy konkrét tartományhoz elkülöníti a szabályt, megakadályozva, hogy nem kapcsolódó cellákat érintsen. Ez teljesíti a **add conditional formatting range** követelményt.

## Szabály definiálása: cellák kiemelése dátum alapján

Most egy `TIME_PERIOD` típusú feltételt hozunk létre. Ez azt mondja az Excelnek, hogy minden cella értékét egy előre meghatározott időablakkal hasonlítsa össze.

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*Miért fontos*: A `TIME_PERIOD` az egyetlen beépített típus, amely közvetlenül támogatja a „Yesterday”, „Today”, „Last Week” stb. értékeket. A `condition.time_period` értékét `YESTERDAY`‑re állítva a szabály automatikusan a cella dátumát a jelenlegi dátum előtti naphoz hasonlítja.

## A feltételnek megfelelő cellák stílusának beállítása

A feltételes formázásnak vizuális stílusra is szüksége van. Itt egy rózsaszín szilárd kitöltést választunk, hogy a megfelelő cellák kiemelkedjenek.

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*Miért fontos*: A style objektum határozza meg, hogyan jeleníti meg az Excel a feltételnek megfelelő cellákat. Egy szilárd rózsaszín kitöltés teljesíti a **highlight cells based on date** követelményt, és könnyen ellenőrizhető eredményt ad.

## Minta dátumok betöltése a kiértékeléshez

A szabály működésének bemutatásához két dátumot illesztünk be – egyet, amely tegnapi dátumra esik, és egyet, amely nem. A `number` formátum `30` a beépített `mm-dd-yy` dátumformátumnak felel meg.

```python
from datetime import datetime

# Cell I19: a date that matches “Yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Example date; adjust as needed
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

# Cell K20: a date outside the “Yesterday” period
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Example date; adjust as needed
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Optional label for the range
worksheet.cells.get("I20").put_value("Yesterday")
```

*Miért fontos*: Egy egyező és egy nem egyező dátum biztosítása lehetővé teszi, hogy ellenőrizd a feltételes formázás helyes működését. A szkripted futtatásakor állítsd a dátumokat az aktuális hónapra, vagy cseréld dinamikus értékekre.

## Munkafüzet mentése

Végül a fájlt leírjuk a lemezre. A `SaveFormat.XLSX` állandó biztosítja, hogy a kimenet egy modern Excel‑fájl legyen.

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*Miért fontos*: A munkafüzet perzisztálása lehetővé teszi, hogy megnyisd Excelben, LibreOffice‑ban vagy bármely XLSX‑t támogató megjelenítőben. A kiírt útvonal megerősíti, hogy hová lett a fájl mentve.

## Teljes szkript

Az összes részt egyesítve, a teljes, futtatható szkript a következő:

```python
# -*- coding: utf-8 -*-
"""
Create an Excel workbook in Python, add a conditional formatting rule,
and highlight yesterday's cells.
"""

from aspose.cells import (
    Workbook, SaveFormat, FormatConditionType,
    BackgroundType, TimePeriodType
)
from aspose.pydrawing import Color as DrawingColor
from datetime import datetime

# Step 1: Create a new workbook and access the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Add a conditional formatting rule for the range I19:K20
condition_collection = worksheet.conditional_formattings.add("I19:K20")
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Step 3: Define the visual style for cells that meet the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID

# Step 4: Set the time‑period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Step 5: Populate sample dates for evaluation
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # yesterday relative to the example
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # outside the period
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Step 6: Add a label for the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Várt kimenet

Amikor megnyitod a `TimePeriodExample.xlsx` fájlt:

* Az **I19** cella rózsaszín háttérrel jelenik meg, mert az értéke tegnapra esik.
* A **K20** cella az alapértelmezett háttérrel marad, mert a dátuma kívül esik a perióduson.
* A **“Yesterday”** felirat az I20 cellában látható a tisztább érthetőség kedvéért.

## Gyakori variációk és szélhelyzetek

| Helyzet | Módosítás |
|-----------|------------|
| **A mai nap kiemelése a tegnap helyett** | Állítsd `condition.time_period = TimePeriodType.TODAY`‑ra. |
| **A szabály nagyobb területre alkalmazása** | Módosítsd a `add("I19:K20")` tartományt például `"A1:Z100"`‑ra. |
| **Másik kitöltőszín használata** | Cseréld a `DrawingColor.pink`‑t bármely más `DrawingColor`‑ra (pl. `DrawingColor.light_green`). |
| **Dinamikus dátumok kezelése** | Számold ki a `datetime.now() - timedelta(days=1)` értéket tegnapra, és írd be a cellákba a szabály alkalmazása előtt. |

**Pro tip:** Ha a munkafüzetet programozottan sok felhasználó számára generálod, tartsd a feltételes formázási definíciót külön a adatbeszúrástól. Így ugyanazt a stílust újra felhasználhatod több munkalapon anélkül, hogy kódot duplikálnál.

## Az eredmény programozott ellenőrzése (opcionális)

Ha szeretnéd a formázást Excel megnyitása nélkül ellenőrizni, a mentés után megvizsgálhatod egy cella stílusát:



## Mi a következő tanulnivaló?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljesen működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Create Excel Workbook and Add Labels with Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}