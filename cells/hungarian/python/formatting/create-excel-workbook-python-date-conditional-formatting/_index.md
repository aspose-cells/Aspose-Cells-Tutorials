---
category: general
date: 2026-08-08
description: Excel munkafüzet létrehozása Pythonban és feltételes formázás hozzáadása
  dátum alapján. Lépésről‑lépésre útmutató az Aspose.Cells használatával a tegnapi
  nap celláinak kiemeléséhez.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: hu
lastmod: 2026-08-08
og_description: Hozzon létre Excel munkafüzetet Pythonban az Aspose.Cells segítségével,
  és alkalmazzon dátum alapú feltételes formázást dinamikus táblázatokhoz.
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: Excel munkafüzet létrehozása Pythonban – dátum feltételes formázás
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Create Excel workbook Python and add conditional formatting based on
    date. Step‑by‑step guide using Aspose.Cells to highlight yesterday’s cells.
  headline: Create Excel workbook Python date conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Excel munkafüzet létrehozása Python dátum feltételes formázással
url: /hu/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel munkafüzet létrehozása Pythonban dátum alapú feltételes formázással

Ha szükséged van **create Excel workbook Python**-ra és automatikusan ki szeretnéd emelni az adott dátumnak megfelelő cellákat, ez a tutorial pontosan megmutatja, hogyan. Megtanulod, hogyan alkalmazz **conditional formatting based on date**-t, hogy a tegnapi dátumok rózsaszínre világítsanak, az Aspose.Cells könyvtár használatával.

A útmutató minden lépésen végigvezet — a SDK telepítésétől a végső .xlsx fájl mentéséig — így egy működő példát egyszerűen átmásolhatsz a saját projektedbe. Külső dokumentációra nincs szükség; minden kód és magyarázat önálló.

## Előkövetelmények

* Python 3.8 vagy újabb telepítve.
* `aspose-cells` csomag (az Aspose.Cells Python csomagja). Telepítsd a következővel:
  ```bash
  pip install aspose-cells
  ```
* Alapvető ismeretek a Pythonról és az Excel koncepciókról, mint például munkalapok és cellastílusok.

> **Pro tipp:** Az Aspose.Cells a Microsoft Excel telepítése nélkül is működik, ami ideálissá teszi szerver‑oldali automatizáláshoz.

## 1. lépés: Excel munkafüzet létrehozása Pythonban

Az első feladat egy új munkafüzet példányosítása és az alapértelmezett munkalap lekérése. Ez az objektum képviseli az egész Excel fájlt, és hozzáférést biztosít a sorokhoz, oszlopokhoz és a formázási API-khoz.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

A munkafüzet létrehozása a bármilyen további módosítás alapja, legyen szó adat, képlet vagy formázási szabály hozzáadásáról.

## 2. lépés: Dátum alapú feltételes formátum meghatározása

Most hozzáadunk **conditional formatting based on date**-t. A `FormatConditionType.TIME_PERIOD` enum lehetővé teszi beépített időszakok, például Yesterday, Today vagy LastWeek megadását.

```python
from aspose.cells import FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color

# Target range I19:K20 – three columns by two rows
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions

# Add a new time‑period condition (e.g., Yesterday)
condition_index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[condition_index]

# Set the visual style: pink solid background
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Specify that the condition should trigger for "Yesterday"
condition.time_period = TimePeriodType.YESTERDAY
```

Miért fontos ez a lépés: az Excel minden cellára kiértékeli a feltételt a tartományban. Ha egy cella értéke beleesik a meghatározott időszakba (tegnap), a hozzárendelt stílus automatikusan alkalmazásra kerül.

## 3. lépés: Tartomány feltöltése mintadátumokkal

A szabály működésének megtekintéséhez néhány `datetime` objektumot írunk a célcellákba. Az egyik szándékosan a munkafüzet belső dátumrendszeréhez képest tegnapi dátumra van beállítva.

```python
from datetime import datetime

# Cell I19 – yesterday’s date (will be highlighted)
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # This date matches the "Yesterday" rule
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel’s built‑in date format
cell_i19.set_style(style_i19)

# Cell K20 – a random later date (no highlight)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Not yesterday, so no formatting
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

A `number = 30` sor azt mondja az Excelnek, hogy a standard rövid dátumformátummal jelenítse meg az értéket. Ezt az indexet bármely beépített számformátumra módosíthatod, ha más megjelenítést szeretnél.

## 4. lépés: Oszlop szélességének beállítása az olvashatóság érdekében

A dátumokat tartalmazó oszlop automatikus méretezése megkönnyíti a kimenet olvasását, különösen ha a munkafüzetet Excelben vagy nézőben nyitod meg.

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## 5. lépés: Munkafüzet mentése lemezre

Végül mentsd a munkafüzetet .xlsx fájlként. Cseréld le a `"YOUR_DIRECTORY"`-t a gépeden lévő valós útvonalra.

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Amikor megnyitod a `TimePeriodDemo.out.xlsx` fájlt Excelben, az **I19** cella rózsaszín háttérrel jelenik meg, mivel az értéke megfelel a „Yesterday” szabálynak, míg a **K20** változatlan marad.

### Várt kimenet

| I19 (dátum) | I20 (címke) | J19 | J20 | K19 | K20 (dátum) |
|------------|-------------|-----|-----|-----|------------|
| *2008‑07‑30* (rózsaszín háttér) | Tegnap | – | – | – | *2008‑08‑03* (nincs formázás) |

A rózsaszín árnyalat megerősíti, hogy a **conditional formatting based on date** a várt módon működik.

## Gyakori variációk és szélhelyzetek

| Helyzet | Hogyan módosítsuk a kódot |
|-----------|-----------------------|
| **„Today” kiemelése a „Yesterday” helyett** | Change `condition.time_period = TimePeriodType.TODAY` |
| **A szabály alkalmazása egy teljes oszlopra** | Use `worksheet.get_range("A:A").format_conditions` |
| **Egyedi dátumtartomány használata (pl. az elmúlt 7 nap)** | Replace the time‑period condition with a formula condition: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **Eltérő háttérszínek** | Set `condition.style.background_color = Color.light_green` (or any `Color` you prefer) |
| **Linuxon futtatás kijelző nélkül** | Aspose.Cells is fully headless; no extra configuration required. |

## Teljes, futtatható példa

Az alábbiakban a teljes szkriptet találod, amelyet úgy futtathatsz, ahogy van (a kimeneti könyvtár frissítése után). Minden import, megjegyzés és hibakezelési alap megtalálható.

```python
# -*- coding: utf-8 -*-
"""
Create Excel workbook Python with date conditional formatting.
Demonstrates how to highlight yesterday’s dates using Aspose.Cells.
"""

import os
from datetime import datetime
from aspose.cells import (
    Workbook, SaveFormat,
    FormatConditionType, BackgroundType,
    TimePeriodType
)
from aspose.pydrawing import Color

# ----------------------------------------------------------------------
# 1️⃣ Initialize workbook
# ----------------------------------------------------------------------
workbook = Workbook()
worksheet = workbook.worksheets[0]

# ----------------------------------------------------------------------
# 2️⃣ Add conditional formatting for "Yesterday"
# ----------------------------------------------------------------------
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions
cond_idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[cond_idx]

# Visual style: pink solid fill
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
condition.time_period = TimePeriodType.YESTERDAY

# ----------------------------------------------------------------------
# 3️⃣ Populate sample dates
# ----------------------------------------------------------------------
# Cell that should match the condition
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Yesterday relative to demo data
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel short‑date format
cell_i19.set_style(style_i19)

# Cell that does NOT match
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label
worksheet.cells.get("I20").put_value("Yesterday")

# ----------------------------------------------------------------------
# 4️⃣ Auto‑fit column for better visibility
# ----------------------------------------------------------------------
worksheet.auto_fit_column(12)   # Column L (0‑based index)

# ----------------------------------------------------------------------
# 5️⃣ Save workbook
# ----------------------------------------------------------------------
output_dir = "YOUR_DIRECTORY"   # <-- replace with a real folder
os.makedirs(output_dir, exist_ok=True)
output_path = os.path.join(output_dir, "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

A szkript futtatása egy Excel fájlt hoz létre, ahol a „Yesterday” cella automatikusan kiemelésre kerül, bemutatva a **create Excel workbook Python** és a **conditional formatting based on date** kombinációját.

## Következtetés

Most már tudod, hogyan kell **create Excel workbook Python** objektumokat létrehozni, **date‑based conditional formatting**-ot definiálni


## Mit érdemes legközelebb megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek további API funkciók elsajátításában és alternatív megvalósítási megközelítések felfedezésében a saját projektjeidben.

- [Excel munkafüzet létrehozása Aspose.Cells használatával Java-ban: lépésről‑lépésre útmutató](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Excel munkafüzet létrehozása diagramokkal Aspose.Cells .NET használatával | lépésről‑lépésre útmutató](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Excel automatizálás: munkafüzet létrehozása és ListBox hozzáadása Aspose.Cells for .NET használatával](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}