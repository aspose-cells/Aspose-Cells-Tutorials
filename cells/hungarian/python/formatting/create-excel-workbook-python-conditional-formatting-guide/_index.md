---
category: general
date: 2026-07-20
description: Excel munkafüzet létrehozása Pythonban az Aspose.Cells használatával,
  cella háttérszín beállítása, és feltételes formázás hozzáadása Pythonban a cellák
  dátum szerinti stílusozásához.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: hu
lastmod: 2026-07-20
og_description: Excel munkafüzet létrehozása Pythonban az Aspose.Cells használatával.
  Tanulja meg, hogyan állíthat be cella háttérszínt, és hogyan adhat hozzá feltételes
  formázást Pythonban a cellák dátum szerinti formázásához.
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: Excel munkafüzet létrehozása Pythonban – Feltételes formázás hozzáadása
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Create Excel workbook Python with Aspose.Cells, set cell background
    color, and add conditional formatting python to style cells by date.
  headline: Create Excel Workbook Python – Conditional Formatting Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Change `"I19:K20"` to any A1‑style range, and adjust the sample
      dates accordingly.
    question: Can I target a different date range?
  - answer: Use `FormatConditionType.FORMULA` and set `condition.formula1 = "YOUR_FORMULA"`—for
      example, `=TODAY()-A1=1` to mimic yesterday.
    question: What if I need a custom formula instead of `YESTERDAY`?
  - answer: Call `conditions.add_condition` again with a different `FormatConditionType`.
      The order matters; later rules can override earlier ones.
    question: How do I apply multiple rules to the same range?
  - answer: Yes—modify `condition.style.font.color = Color.white` (or any other `Color`).
    question: Is there a way to set font colour together with background?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
title: Excel munkafüzet létrehozása Python – Feltételes formázás útmutató
url: /hu/python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel Workbook Python – Feltételes formázás útmutató

Gondolkodtál már azon, hogyan **create Excel workbook Python**-t hozhatsz létre a semmiből, és teheted azt kifinomulttá anélkül, hogy megnyitnád a felhasználói felületet? Nem vagy egyedül. Sok fejlesztő akad el, amikor **set cell background color**-t kell beállítania, vagy programozottan dátum‑alapú stílusokat kell alkalmaznia.  

Ebben az útmutatóban végigvezetünk egy teljes, futtatható példán, amely az Aspose.Cells-et használja **add conditional formatting python** szabályok hozzáadásához, dátum szerint formázza a cellákat, és a végeredményt modern XLSX fájlként menti. A végére egy önálló szkriptet kapsz, amelyet bármely projektbe beilleszthetsz.

## Mit fogsz megtanulni

- Hogyan inicializálj egy munkafüzetet és szerezd meg az első munkalapot.  
- Módszerek **set cell background color** beállítására egy teljes tartományra.  
- **aspose cells conditional formatting** használata a „Yesterday” dátumok kiemeléséhez.  
- Oszlopok automatikus méretezése és a fájl lemezre mentése.  

Nem szükséges külső konfiguráció – csak Python 3 és az Aspose.Cells csomag. Ha már telepítetted a `aspose-cells`-t, készen állsz; egyébként egy gyors `pip install aspose-cells` megteszi.

## Előfeltételek

- Python 3.8+ (a kód működik 3.9, 3.10 és újabb verziókon).  
- Aspose.Cells for Python via .NET (`aspose-cells` NuGet wrapper).  
- Alapvető ismeretek az Excel koncepcióiról (cellák, tartományok, formázás).  

Megvan? Remek – merüljünk el.

## Excel Workbook Python létrehozása – Beállítás és munkalap

Először is: szükségünk van egy új munkafüzet objektumra és egy hivatkozásra az alapértelmezett munkalapra. Ez a vászon, ahol a későbbi műveletek zajlanak.

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **Miért fontos ez:** `Workbook()` egy memóriában lévő Excel fájlt hoz létre, ezzel kiküszöbölve a bármilyen ideiglenes fájl szükségességét. A `worksheet` változó a belépési pontunk a cellaszintű műveletekhez.

## Cellák háttérszínének beállítása

Mielőtt bármilyen szabályt hozzáadnánk, jó, ha a célzott tartománynak egy alap színt adunk, hogy a feltételes formázás kiemelkedjen. Az alábbi segédfüggvény egyszerre lekéri (vagy létrehozza) a `FormatConditionCollection`-t egy adott tartományhoz, és szilárd háttérrel festi a cellákat.

```python
def get_format_condition(cell_range: str, base_color: Color):
    """
    Obtain (or create) a FormatConditionCollection for `cell_range`.
    Also set a base background colour for the whole range.
    """
    # Retrieve or add a conditional formatting entry for the range
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    # Apply the base colour to every cell in the range
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color          # set cell background color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection
```

> **Pro tipp:** Ha ugyanazt a tartományt több szabállyal szeretnéd újrahasználni, hívd meg ezt a segédfüggvényt egyszer, és tartsd meg a visszaadott gyűjteményt; ez néhány API hívást takarít meg.

## Feltételes formázás hozzáadása Pythonban dátumtartományokhoz

Most jön a szórakoztató rész: létrehozunk egy **time‑period conditional formatting** szabályt, amely kiemeli a tegnapi dátumot tartalmazó cellákat. Ez bemutatja a **format cells by date** erejét az Aspose.Cells használatával.

```python
def apply_yesterday_rule():
    """
    Apply a “Yesterday” conditional formatting rule to the range I19:K20.
    Cells that match will turn pink; others stay with the base colour.
    """
    # Obtain the condition collection for the target range
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)

    # Create a TIME_PERIOD condition (this is the aspose cells conditional formatting type we need)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]

    # Define the appearance for cells that meet the condition
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Set the time period to “Yesterday”
    condition.time_period = TimePeriodType.YESTERDAY

    # Populate sample dates to demonstrate the rule
    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))   # matches “Yesterday”
    cell_i19.style.number = 30                 # Excel number format for dates
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))    # does NOT match
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    # Add a label for clarity
    worksheet.cells.get("I20").put_value("Yesterday")
```

> **Miért használjuk a `TIME_PERIOD`-t?** Elrejti a saját képletek írásának szükségességét. Az Aspose.Cells a dátumot a jelenlegi rendszer dátummal hasonlítja össze, így a szabály mindig releváns marad.

### A szabály futtatása

```python
apply_yesterday_rule()
```

Amikor megnyitod a keletkezett fájlt, az `I19` cellák rózsaszínre világítanak (mert „Tegnap” dátumot tartalmaznak), míg a `K20` a alap zöld színt megtartja.

## Oszlopok automatikus méretezése és a munkafüzet mentése

Egy rendezett táblázat professzionális benyomást kelt. Az automatikus méretezés biztosítja, hogy az adataink ne legyenek szorultak.

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Szélsőséges eset:** Ha egy nem létező könyvtárra célozol, a `workbook.save` hibát dob. Ha elegáns kezelést szeretnél, tedd a mentést egy `try/except` blokkba.

### Teljes szkript (másolás-beillesztés kész)

Az alábbiakban a teljes szkript látható, készen áll a futtatásra. Csak cseréld le a `YOUR_DIRECTORY`-t egy érvényes mappára a gépeden.

```python
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create the workbook and worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

def get_format_condition(cell_range: str, base_color: Color):
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection

def apply_yesterday_rule():
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = TimePeriodType.YESTERDAY

    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))
    cell_i19.style.number = 30
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    worksheet.cells.get("I20").put_value("Yesterday")

apply_yesterday_rule()
worksheet.auto_fit_column(12)

output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

A szkript futtatása létrehozza a `TimePeriodExample.xlsx` fájlt a leírt feltételes formázással.

## Gyakori kérdések és tippek

- **Célzhatok másik dátumtartományt?**  
  Természetesen. Módosítsd a `"I19:K20"`-t bármely A1‑stílusú tartományra, és ennek megfelelően állítsd be a minta dátumokat.

- **Mi van, ha egy egyedi képletre van szükségem a `YESTERDAY` helyett?**  
  Használd a `FormatConditionType.FORMULA`-t, és állítsd be a `condition.formula1 = "YOUR_FORMULA"`‑t – például `=TODAY()-A1=1` a tegnap szimulálásához.

- **Hogyan alkalmazhatok több szabályt ugyanarra a tartományra?**  
  Hívd meg újra a `conditions.add_condition`‑t egy másik `FormatConditionType`‑val. A sorrend számít; a későbbi szabályok felülírhatják a korábbiakat.

- **Van mód a betűszín beállítására a háttérrel együtt?**  
  Igen – módosítsd a `condition.style.font.color = Color.white`‑t (vagy bármely más `Color`‑t).

## Összegzés

Most már tudod, hogyan **create Excel workbook Python**-t használj az Aspose.Cells segítségével, **set cell background color**-t, és **add conditional formatting python**-t, amely dátum szerint formázza a cellákat. A szkript teljesen működőképes, kezeli a szélsőséges eseteket, mint a hiányzó könyvtárak, és kiterjeszthető összetettebb forgatókönyvekre, például több szabályos feltételes logikára vagy dinamikus tartománydetektálásra.

Készen állsz a következő lépésre? Próbáld ki a „Yesterday” szabályt „Last Week”-re cserélni, kísérletezz gradient kitöltésekkel, vagy generálj egy teljes jelentést tucatnyi formázott táblázattal. Az építőelemek mind itt vannak, és most már elsajátítottad a **aspose cells conditional formatting** alapjait Pythonban.

Boldog kódolást, és nyugodtan oszd meg saját változataidat a megjegyzésekben!

## Mit érdemes legközelebb megtanulni?

Az alábbi útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}