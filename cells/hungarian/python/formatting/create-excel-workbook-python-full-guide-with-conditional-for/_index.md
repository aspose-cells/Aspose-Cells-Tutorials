---
category: general
date: 2026-07-14
description: Excel munkafüzetet létrehozó Python kód, amely beállítja a cellák háttérszínét,
  a dátumtartomány alapján kiemeli a cellákat, és percek alatt XLSX formátumban elmenti
  a munkafüzetet.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- save workbook as xlsx
- highlight cells based on date range
- conditional formatting based on date
language: hu
lastmod: 2026-07-14
og_description: Hozzon létre Excel munkafüzetet Pythonban azonnal. Tanulja meg, hogyan
  állítsa be a cella háttérszínét, emelje ki a cellákat dátumtartomány alapján, és
  mentse a munkafüzetet XLSX formátumban az Aspose.Cells segítségével.
og_image_alt: Screenshot showing an Excel sheet created with Python highlighting yesterday's
  dates
og_title: Excel munkafüzet létrehozása Pythonban – Lépésről lépésre feltételes formázás
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Create Excel workbook Python code that sets cell background color,
    highlights cells based on date range, and saves workbook as XLSX in minutes.
  headline: Create Excel Workbook Python – Full Guide with Conditional Formatting
  type: TechArticle
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Excel munkafüzet létrehozása Pythonban – Teljes útmutató feltételes formázással
url: /hu/python/formatting/create-excel-workbook-python-full-guide-with-conditional-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel munkafüzet létrehozása Pythonban – Teljes útmutató feltételes formázással

Ever wondered how to **create excel workbook python** scripts that look polished without opening Excel manually? You're not alone. In many data‑driven projects we need to generate spreadsheets, color‑code cells, and even flag dates that fall inside a specific range—all from pure Python code.

Gondolkodtál már azon, hogyan lehet **create excel workbook python** szkripteket készíteni, amelyek kifinomultak, anélkül, hogy manuálisan megnyitnád az Excelt? Nem vagy egyedül. Sok adat‑vezérelt projektben táblázatokat kell generálni, cellákat színezni, sőt dátumokat kiemelni, amelyek egy adott tartományba esnek – mindezt tisztán Python kódból.

In this tutorial we’ll walk through a complete, ready‑to‑run example that **creates an Excel workbook python** using the Aspose.Cells library, **sets cell background color**, applies **conditional formatting based on date**, and finally **saves workbook as xlsx**. By the end you’ll have a reusable snippet you can drop into any automation pipeline.

Ebben az útmutatóban egy teljes, azonnal futtatható példán keresztül vezetünk végig, amely **creates an Excel workbook python** az Aspose.Cells könyvtár segítségével, **sets cell background color**, **conditional formatting based on date** alkalmaz, és végül **saves workbook as xlsx**. A végére egy újrahasználható kódrészletet kapsz, amelyet bármely automatizálási folyamatba beilleszthetsz.

## Amit megtanulsz

- Hogyan inicializáljunk egy munkafüzetet és vegyük fel az első munkalapot.  
- Egy segédfüggvény, amely feltételes formázási gyűjteményt ad hozzá bármely cellatartományhoz.  
- A **conditional formatting based on date** használata a tegnapi bejegyzések kiemeléséhez.  
- Az oszlopszélességek beállítása a rendezett elrendezéshez.  
- Az eredmény mentése **save workbook as xlsx** segítségével.  

Külső Excel telepítés nem szükséges – az Aspose.Cells mindent memóriában kezel.

## Előfeltételek

- Python 3.8+ telepítve.  
- `aspose-cells` csomag (`pip install aspose-cells`).  
- Alapvető ismeretek a Python függvényekkel és datetime objektumokkal.  

Ha még soha nem használtad az Aspose.Cells‑t, tekintsd egy erőteljes, tisztán Python API‑nak, amely az Excel saját objektummodelljét utánozza. Tökéletes szerver‑oldali generáláshoz, ahol az Office csomag nem elérhető.

## 1. lépés: A munkafüzet inicializálása (Create Excel Workbook Python)

Először is: egy **create excel workbook python** stílusú üres munkafüzet objektumot kell létrehoznunk, és a alapértelmezett munkalapra kell mutatnunk.

```python
# Step 1 – create a fresh workbook and get the first sheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, Color, SaveFormat
from datetime import datetime

workbook = Workbook()                     # <-- creates a new Excel file in memory
worksheet = workbook.worksheets[0]        # the default (first) sheet
```

> **Miért fontos:** A `Workbook` osztály minden Excel művelet belépési pontja. Programozottan létrehozva elkerülhetjük a manuális fájlkezelést.

## 2. lépés: Segédfüggvény a feltételes formázási gyűjtemény hozzáadásához (Set Cell Background Color)

A feltételes formázás egy *gyűjtemény* részeként él, amely egy tartományhoz van csatolva. Csomagoljuk be ezt a sablont egy kis segédfüggvénybe, amely lehetővé teszi a **set cell background color** alkalmazását az egész tartományra.

```python
def add_time_period_condition(cell_range: str, highlight_color: Color):
    """
    Adds a conditional‑formatting collection to `cell_range` and
    applies `highlight_color` as the base fill.
    """
    worksheet.conditional_formattings.add(cell_range)   # attach to the range
    cf = worksheet.conditional_formattings[-1]           # grab the newly added collection
    cf.style.background_color = highlight_color
    cf.style.pattern = BackgroundType.SOLID
    return cf
```

> **Pro tipp:** Segédfüggvény használata tisztán tartja a fő folyamatot, és megkönnyíti ugyanazon logika többszöri felhasználását különböző tartományokhoz.

## 3. lépés: Feltételes formázás alkalmazása dátum alapján (Highlight Cells Based on Date Range)

Most már ténylegesen **highlight cells based on date range**. A példa a „tegnapra” fókuszál, de a `TimePeriodType.YESTERDAY`-t kicserélheted `TODAY`, `LAST_WEEK` stb. értékekre.

```python
# Step 3 – create a TIME_PERIOD rule for I19:K20 (yesterday)
cf = add_time_period_condition("I19:K20", Color.medium_sea_green)

condition_index = cf.add_condition(FormatConditionType.TIME_PERIOD)
condition = cf[condition_index]

# Define the visual style for the matching cells
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# The actual rule: any cell whose date is yesterday gets the pink fill
condition.time_period = TimePeriodType.YESTERDAY
```

> **Mi történik?**  
> 1. Először a teljes tartománynak semleges zöld háttérszínt adunk.  
> 2. Ezután egy `TIME_PERIOD` feltételt adunk hozzá, amely rózsaszínre változtatja a kitöltést **csak** akkor, ha a cella dátuma tegnapra esik.  
> 3. A `TimePeriodType` enum elrejti a dátuszámítást, így nem kell egyedi logikát írnod.

## 4. lépés: Minta dátumok feltöltése (So the Rule Can Be Evaluated)

A szabály működésének megtekintéséhez néhány dátumot helyezünk a táblázatba. Az egyik a „tegnap” időablakba esik, a másik nem.

```python
# Populate I19 with a date that is yesterday (relative to the hard‑coded date)
date_cell = worksheet.cells.get("I19")
date_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008
date_style = date_cell.get_style()
date_style.number = 30                     # Excel’s built‑in date format
date_cell.set_style(date_style)

# Populate K20 with a date that is NOT yesterday
date_cell = worksheet.cells.get("K20")
date_cell.put_value(datetime(2008, 8, 3))    # 03‑Aug‑2008
date_style = date_cell.get_style()
date_style.number = 30
date_cell.set_style(date_style)

# Add a label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

> **Különleges eset megjegyzés:** Ha a munkafüzetet különböző helyi beállításokban nyitják meg, fontold meg a `date_style.custom = "dd‑mm‑yyyy"` használatát a konzisztens megjelenítés érdekében.

## 5. lépés: Elrendezés rendbetétele (Auto‑Fit Columns)

Egy zsúfolt táblázat amatőrnek tűnik. Végezzünk **adjust column width for a tidy output**.

```python
# Auto‑fit column L (index 12) to show the full content without truncation
worksheet.auto_fit_column(12)
```

> **Miért auto‑fit?** Biztosítja, hogy a hosszú címkék vagy dátumok teljesen láthatóak legyenek, ami különösen fontos, ha a fájlt nem‑technikai érintettekkel osztod meg.

## 6. lépés: A munkafüzet mentése (Save Workbook As XLSX)

Végül **save workbook as xlsx** a választott helyre mentjük. A `SaveFormat.XLSX` állandó azt mondja az Aspose.Cells‑nek, hogy a modern OpenXML formátumba írja.

```python
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Az eredmény, amit látnod kell:**  
> - Az I19 és K20 cellák dátumot tartalmaznak.  
> - Az I19 (tegnap) rózsaszínre van kiemelve, míg a K20 zöld marad.  
> - Az L oszlop automatikusan kibővül, hogy elférjen a „Yesterday” címke.

Ha megnyitod a `TimePeriodDemo.xlsx` fájlt Excelben, a feltételes formázás már alkalmazva lesz – nincs szükség további lépésekre.

![Excel táblázat, amely a kiemelt tegnapi dátumot mutatja](https://example.com/images/excel-demo.png "A generált Excel fájl képernyőképe kiemelt cellákkal")

*Az fenti kép a végső munkafüzetet ábrázolja; vedd észre a rózsaszín kiemelést a tegnapi dátumot tartalmazó cellán.*

## Összefoglalás: Mit értünk el

- **Created an Excel workbook python** a semmiből az Aspose.Cells használatával.  
- **Set cell background color** egy teljes tartományra, hogy vizuális jelzést adjon a lapnak.  
- **conditional formatting based on date** alkalmazása a tegnapi bejegyzések automatikus jelzéséhez.  
- **Saved workbook as xlsx** – készen áll a terjesztésre vagy további feldolgozásra.  

Mindezt kevesebb mint 60 Python sorban valósítottuk meg, és a kód bármely, az Aspose.Cells futtatókörnyezetet támogató platformon működik.

## Következő lépések és kapcsolódó témák

Ha hasznosnak találtad, érdemes lehet még megtekinteni:

- **set cell background color** teljes sorokra állapotértékek alapján (pl. „Completed”, „Pending”).  
- **highlight cells based on date range** használata gördülő ablakok létrehozásához (utolsó 7 nap, aktuális hónap).  
- Exportálás más formátumokba, mint a **CSV** vagy **PDF** a `SaveFormat.CSV` vagy `SaveFormat.PDF` segítségével.  
- **charts** programozott hozzáadása az adatok vizualizálásához, amelyeket épp formáztál.  

Nyugodtan módosítsd a dátumlogikát, cseréld ki a színpalettát, vagy bővítsd a tartományt, hogy egész oszlopokat fedjen le. A minta ugyanaz marad: hozz létre egy munkafüzetet, csatolj egy feltételes formázási gyűjteményt, definiáld a szabályt, és mentsd el.

Van kérdésed egy konkrét felhasználási esettel kapcsolatban? Írj egy megjegyzést alább, és jó kódolást!

## Mit érdemes legközelebb megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Excel automatizálás Aspose.Cells .NET: Munkafüzet létrehozása és külső hivatkozások beállítása](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Excel munkafüzet létrehozása és mentése Aspose Cells Java](/cells/hongkong/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Excel munkafüzet létrehozása és mentése Aspose Cells .NET](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}