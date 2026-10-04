---
category: general
date: 2026-10-04
description: Készíts Excel munkafüzetet Pythonban az Aspose.Cells használatával. Tanulj
  meg Excel feltételes formázást Pythonban, cella háttérszín beállítását Pythonban,
  valamint dátum formázást cellákban Pythonban egy teljes példában.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: hu
lastmod: 2026-10-04
og_description: Hozzon létre Excel munkafüzetet Pythonban az Aspose.Cells segítségével.
  Ez az útmutató lépésről‑lépésre bemutatja az Excel feltételes formázást Pythonban,
  a cella háttérszín beállítását Pythonban, valamint a cellák dátumformázását Pythonban.
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: Excel munkafüzet létrehozása Pythonban – teljes útmutató feltételes formázással
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  headline: Create Excel workbook python with conditional formatting and cell background
    color
  type: TechArticle
- description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  name: Create Excel workbook python with conditional formatting and cell background
    color
  steps:
  - name: '**create Excel workbook python** using the Aspose.Cells library.'
    text: '**create Excel workbook python** using the Aspose.Cells library.'
  - name: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
    text: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
  - name: Set the **cell background color python** to pink (or any color you prefer).
    text: Set the **cell background color python** to pink (or any color you prefer).
  - name: '**format cells date python** so the dates appear in the standard Excel
      date style.'
    text: '**format cells date python** so the dates appear in the standard Excel
      date style.'
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Excel munkafüzet létrehozása Pythonban feltételes formázással és cella háttérszínnel
url: /hu/python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel munkafüzet létrehozása Pythonban feltételes formázással és cellaháttérszínnel

Ha gyorsan **create Excel workbook python**-t kell készítened, ez az útmutató pontosan megmutatja, hogyan. Egy teljes, futtatható példát láthatsz, amely hozzáadja a **excel conditional formatting python**-t, megváltoztatja a **cell background color python**-t, és **format cells date python**-t egy „Yesterday” kiemeléshez.  

Sok jelentéskészítési helyzetben a színezett cella vizuális jelzése azonnal érthetővé teszi az adatokat. Ez a tutorial minden kódsort végigvezet, elmagyarázza, miért fontos az egyes lépések, és egy kész‑futtatható szkriptet ad, amelyet saját projektjeidhez igazíthatsz.

## Mit fogsz elérni

A cikk végére képes leszel:

1. **create Excel workbook python** az Aspose.Cells könyvtár használatával.  
2. **excel conditional formatting python** alkalmazására, amely automatikusan kiemeli a „Yesterday” napra eső dátumokat.  
3. A **cell background color python** beállítására rózsaszínre (vagy bármely általad preferált színre).  
4. **format cells date python** alkalmazására, hogy a dátumok a szokásos Excel dátumstílusban jelenjenek meg.  

Az Aspose.Cells előzetes ismerete nem szükséges – csak egy működő Python 3 környezet és pip hozzáférés.

## Előfeltételek

- Python 3.8 vagy újabb telepítve.  
- `aspose-cells` és `aspose-pydrawing` csomagok telepítve a `pip install aspose-cells aspose-pydrawing` paranccsal.  
- Alapvető ismeretek a Python szintaxisról és az Excel fogalmakról (munkafüzetek, munkalapok, cellák).  

> **Pro tip:** Ha a szkriptet virtuális környezetben futtatod, elkerülöd a verzióütközéseket más projektekhez képest.

## 1. lépés: A projekt beállítása és a szükséges osztályok importálása

Az első lépés, amikor **create Excel workbook python**-t végzel, az Aspose.Cells osztályok importálása, amelyekre szükséged lesz. Ezek az osztályok közvetlen hozzáférést biztosítanak a munkafüzet létrehozásához, a feltételes formázáshoz és a stílusokhoz.

```python
# Import Aspose.Cells core classes
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)

# Import Aspose.PyDrawing for color handling
from aspose.pydrawing import Color

# Standard library for date values
from datetime import datetime
```

*Miért fontos:* Csak a szükséges szimbólumok importálása tartja tisztán a névtér‑környezetet, és könnyebben olvashatóvá teszi a szkriptet. A `Workbook` a **create Excel workbook python** belépési pontja, míg a `FormatConditionType` és a `TimePeriodType` elengedhetetlenek a **excel conditional formatting python**-hoz.

## 2. lépés: Új munkafüzet létrehozása és az első munkalap lekérése

Most ténylegesen **create Excel workbook python**. A `Workbook()` konstruktor egy üres Excel fájlt hoz létre egy alapértelmezett munkalappal.

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Magyarázat:* Minden Excel fájl legalább egy munkalappal indul. Alapértelmezés szerint az Aspose.Cells ezt „Sheet1”-nek nevezi. Később hozzáadhatsz több lapot, de a bemutatóhoz egyetlen lap is elegendő.

## 3. lépés: A cél tartomány meghatározása a feltételes formázáshoz

A feltételes formázás egy téglalap alakú tartományon működik. Itt a `I19:K20` tartományt választjuk, amely három oszlopot és két sort biztosít.

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*Miért csináljuk:* A `get` metódus egy `ConditionalFormatting` objektumot ad vissza, amely a megadott tartományhoz van kötve. Ha a tartomány még nem rendelkezik formázással, az Aspose.Cells automatikusan létrehoz egy új gyűjteményt.

## 4. lépés: TIME_PERIOD feltétel hozzáadása és a háttérszín beállítása

Ez a **excel conditional formatting python** magja. Egy `TIME_PERIOD` szabályt adunk hozzá, amely kiemeli azokat a cellákat, amelyek dátuma „Yesterday”.

```python
# Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Access the newly created condition
condition = conditional_formatting[condition_index]

# Configure the condition to target “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Set the cell background color – this is the cell background color python part
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

*Mélyebb elemzés:*  
- `FormatConditionType.TIME_PERIOD` azt mondja az Excelnek, hogy a dátumokat a jelenlegi dátumhoz viszonyítva értékelje.  
- `TimePeriodType.YESTERDAY` egy beépített enum, amely naponta automatikusan frissül, így a munkafüzet mindig a legutóbbi „Yesterday” napot emeli ki.  
- A `background_color` `Color.pink`‑re és a mintára `SOLID` beállításával elérjük a **cell background color python** hatást extra VBA kód nélkül.

## 5. lépés: A tartomány feltöltése minta dátumokkal és dátumformázás alkalmazása

A feltételes formázás működésének láthatóságához valódi dátumértékekre van szükség. Emellett **format cells date python**-t kell alkalmazni, hogy az Excel dátumként kezelje őket, ne egyszerű számként.

```python
# Helper function to set a cell's date style and value
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    # Excel’s built‑in date format code 30 = "m/d/yy"
    style.number = 30
    cell.set_style(style)
    cell.put_value(date_value)

# Populate I19 with a date that is “yesterday” relative to the sample data
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”

# Populate K20 with another arbitrary date
set_date("K20", datetime(2008, 8, 3))    # Not “yesterday”
```

*Magyarázat:*  
- A `style.number = 30` sor a **format cells date python** lépés. A 30-as formátuskód a rövid dátumformátumnak (`m/d/yy`) felel meg.  
- Egy segédfüggvény használata DRY‑t (Don’t Repeat Yourself) tart, és egyszerűvé teszi további dátumok hozzáadását később.

## 6. lépés: Leíró címke hozzáadása

Egy kis címke segít mindenki számára, aki megnyitja a munkafüzetet, megérteni, miért színeződnek a cellák.

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## 7. lépés: A munkafüzet mentése lemezre

Végül **create Excel workbook python**-t mentünk lemezre a `save` hívásával. A `SaveFormat.XLSX` állandó biztosítja, hogy a fájl a modern Office Open XML formátumban legyen.

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Amikor megnyitod a `TimePeriodDemo.xlsx` fájlt Excelben, a következőket fogod látni:

- Az `I19` és `K20` cellák dátumot tartalmaznak.  
- Az a cella, amely megfelel a „Yesterday” szabálynak (ebben a statikus példában az `I19`) rózsaszínre van kiemelve.  
- A „Yesterday” címke az `I20`‑ban jelenik meg.  

> **Tip:** Ha a szkriptet más napon futtatod, a feltételes formázás továbbra is kiemeli azt a cellát, amelynek dátuma pontosan egy nappal korábbi a rendszer aktuális dátumánál – kódmódosítás nélkül.

## Teljes szkript – készen áll a másolásra és futtatásra

Az alábbiakban a teljes, önálló program látható, amely tartalmazza a fentieket. Másold egy `conditional_format_demo.py` nevű fájlba, állítsd be a `YOUR_DIRECTORY`‑t, majd futtasd a `python conditional_format_demo.py` paranccsal.

```python
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the cell range that will receive the conditional format
target_range = "I19:K20"
conditional_formatting = worksheet.conditional_formattings.get(target_range)

# Step 3: Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Step 4: Configure the condition to highlight “Yesterday” dates
condition = conditional_formatting[condition_index]
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Helper to set date value and style
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    style.number = 30          # Excel date format code 30 = short date
    cell.set_style(style)
    cell.put_value(date_value)

# Step 5: Populate the range with sample dates (excel conditional formatting python)
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”
set_date("K20", datetime(2008, 8, 3))    # Another sample date

# Step 6: Add a label describing the condition
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Várható kimenet

A szkript futtatása egy megerősítő sort ír ki:

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

A generált fájl megnyitása mutatja a rózsaszín háttérszínt azon a cellán, amely megfelel a „Yesterday” szabálynak, ezzel megerősítve, hogy a **excel conditional formatting python** és a **cell background color python** együtt működnek.

## Gyakori variációk és szélhelyzetek

| Szituáció | Hogyan kell módosítani a kódot |
|-----------|-------------------------------|
| **Másik kiemelési szín** | Cseréld a `Color.pink`‑t bármely más `Color` konstansra, például `Color.light_green`. |
| **„Today” kiemelése a „Yesterday” helyett** | Állítsd be a `condition.time_period = TimePeriodType.TODAY` értéket. |
| **Formázás alkalmazása egy teljes oszlopra** | Használj olyan tartományt, mint `"A:A"`, és ennek megfelelően módosítsd a `target_range` változót. |
| **Egyedi dátumformátum használata** | Cseréld a `style.number = 30`‑t `style.custom = "dd-mmm-yyyy"`‑re egy olvashatóbb formátumért. |
| **Több feltétel ugyanazon a tartományon** |  |

## Mit érdemes legközelebb megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek további API‑funkciók elsajátításában és alternatív megvalósítási megközelítések felfedezésében saját projektjeidben.

- [Excel munkafüzet létrehozása Pythonban – Teljes útmutató Lambda-val](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [Excel munkafüzet létrehozása és mentése PDF‑ként ASP.NET‑ben az Aspose.Cells használatával](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Excel munkafüzet létrehozása és mentése ODS formátumban az Aspose.Cells for .NET használatával](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}