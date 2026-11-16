---
category: general
date: 2026-11-16
description: Készíts feltételes formázást Excelben Python használatával. Tanulj meg
  feltételes formázási tartományt hozzáadni, dátumokat kiemelni, és programozottan
  egy munkafüzetet felépíteni.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: hu
lastmod: 2026-11-16
og_description: Készíts feltételes formázást Excelben Python segítségével. Ez az útmutató
  bemutatja, hogyan lehet hozzáadni egy feltételes formázási tartományt, kiemelni
  a dátumokat, és létrehozni egy munkafüzetet.
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: Feltételes formázás létrehozása Excelben Python segítségével – lépésről
  lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Hogyan készítsünk feltételes formázást Excelben Python segítségével
url: /hu/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan hozzunk létre feltételes formázást Excelben Python segítségével

Ha **feltételes formázást** kell létrehoznod egy Excel‑fájlban Pythonban, ez az útmutató pontosan megmutatja, hogyan teheted meg. Megtanulod, hogyan **hozz létre excel workbook python**‑stílusú munkafüzetet, meghatározod a formázási tartományt, és kiemelsz dátumokat anélkül, hogy elhagynád az IDE‑t.

A feltételes formázás lehetővé teszi, hogy vizuálisan jelöld meg azokat a cellákat, amelyek egy adott kritériumnak megfelelnek – tökéletes irányítópultokhoz, jelentésekhez vagy adat‑ellenőrző lapokhoz. A tutorial végére egy teljesen működő munkafüzeted lesz, amely a „Tegnap” dátumú cellákat rózsaszínre színezi, míg a többi tartomány zöld marad.

## Mit fogsz elérni

* Új munkafüzet építése a semmiből.  
* Feltételes‑formázás gyűjtemény hozzáadása egy adott cellatömbhöz.  
* **TIME_PERIOD** szabály alkalmazása, amely kiemeli a dátumokat (a „hogyan emeljük ki a dátumokat” szituáció).  
* A fájl mentése XLSX munkafüzetként, készen állva a további feldolgozásra.

**Előfeltételek**  
* Python 3.8+  
* `aspose-cells` Python csomag (`pip install aspose-cells`)  
* Alapvető ismeretek a Python `datetime` moduljáról  

---

## Hogyan hozzunk létre feltételes formázást Pythonban

Az első lépés a munkafüzet és a munkalap beállítása, amely a formázási szabályokat fogja tartalmazni.

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**Miért fontos** – A `Workbook` a belépési pont minden Excel‑művelethez. A munkafüzet programozott létrehozása helyettesíti a manuális „File → New” lépést, lehetővé téve az automatizált jelentés‑csővezetékek használatát.

---

## A feltételes‑formázás gyűjtemény előkészítése – feltételes formázási tartomány hozzáadása

Ezután definiáljuk azt a cellatömböt, amelyik megkapja a szabályt. Ebben a példában a tartomány **I19:K20**.

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**Magyarázat** – A `conditional_formattings.add` egy új gyűjteményt regisztrál a címkarakterlánchoz. Az első feltétel (`conds[0]`) „alapértelmezett” stílusként működik; a későbbi szabály felülírja, ha a kritériumai teljesülnek.

---

## TIME_PERIOD feltétel hozzáadása – hogyan emeljük ki a dátumokat

Most adjuk hozzá a tényleges logikát, amely azonosítja a „Tegnap” dátumokat és rózsaszínre festi őket.

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**Miért használjuk a TIME_PERIOD‑t?** – Az Aspose.Cells beépített enumerációkat biztosít, mint a `YESTERDAY`, `TODAY` és `LAST_WEEK`. Ezek a cella dátumértékét a rendszer aktuális dátumához viszonyítják, így nem szükséges egyedi képleteket írni.

---

## Mintaadatok feltöltése – a szabály demonstrálása

A formázás működésének megtekintéséhez beillesztünk egy dátumot, amely megfelel a szabálynak, és egy másikat, amely nem.

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**Széljegyzet** – A `TIME_PERIOD` szabály csak *valódi* dátumokkal működik. Ha egy cella szöveget tartalmaz (pl. „N/A”), a szabály figyelmen kívül marad, így elkerülhető a váratlan színváltozás.

---

## A munkafüzet mentése – add conditional formatting python

Végül írjuk a munkafüzetet a lemezre. A fájl bármely táblázatkezelő programban megnyitható a színek ellenőrzéséhez.

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**Várható eredmény**  

| I19 (zöld → rózsaszín) | J19 (zöld) | K19 (zöld) |
|------------------------|------------|------------|
| 30/07/2008 (tegnap) | – | – |
| **I20**: „Tegnap” felirat | – | – |
| I21‑K21 (zöld) | – | – |

Az **I19** cella rózsaszín háttérrel jelenik meg, mert a dátuma megfelel a „Tegnap” periódusnak, míg a **K20** zöld marad.

---

## Gyakori kérdések és gyakorlati tippek

* **Használhatok egyedi dátumtartományt a beépített periódus helyett?**  
  Igen. Cseréld le a `condition.time_period`‑t `condition.formula1 = "TODAY()-1"`‑re, és állítsd be a `condition.type = FormatConditionType.FORMULA`‑t.

* **Mi van, ha a munkafüzettel már van adat?**  
  Használd a `worksheet.cells.import_data`‑t a tömeges adatbetöltéshez, mielőtt hozzáadnád a feltételes formázási gyűjteményt.

* **Teljesítmény nagy táblázatoknál?**  
  Sok feltétel hozzáadása lelassíthatja a megjelenítést. Csoportosítsd az azonos szabállyal rendelkező cellákat egyetlen tartományba (pl. „A1:C1000”), hogy a feltételszám alacsony maradjon.

* **Keresztplatformos kompatibilitás?**  
  A generált XLSX fájl az Office Open XML szabványt követi, így Windows, macOS és Linux táblázatkezelő alkalmazásokon egyaránt működik.

---

## Összegzés

Most már tudod, hogyan **hozz létre feltételes formázást** egy Excel‑munkafüzetben Python segítségével. A tutorial bemutatta a munkafüzet létrehozását, egy **add conditional formatting range** meghatározását, egy **how to highlight dates** szabály alkalmazását, valamint a fájl mentését – mindezt az **add conditional formatting python** megközelítéssel, amelyet az Aspose.Cells biztosít.

Innen tovább:

* Bővítsd a szabálykészletet más `TimePeriodType` értékekkel (pl. `TODAY`, `LAST_MONTH`).  
* Kombinálj több feltételt ugyanazon a tartományon a gazdagabb vizuális jelzésekért.  
* Integráld ezt a munkafolyamatot automatizált jelentés‑csővezetékekbe vagy webszolgáltatásokba.

Jó kódolást, és bátran kísérletezz különböző színekkel, tartományokkal és dátumlogikákkal, hogy a jelentéseid igényeinek leginkább megfeleljen!

## Mit tanulj meg legközelebb?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Create Excel workbook Python date conditional formatting](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [How to apply time period conditional formatting in Excel using Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}