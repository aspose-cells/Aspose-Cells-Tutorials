---
category: general
date: 2026-08-24
description: Készítsen feltételes formázási szabályt Pythonban az Aspose.Cells használatával
  a dátumok kiemeléséhez, automatikus oszlopszélesség beállítással és háttérszín formázással.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting rule
- auto fit column
- conditional formatting by date
- background color conditional format
- date based conditional format
language: hu
lastmod: 2026-08-24
og_description: Készítsen feltételes formázási szabályt Pythonban az Aspose.Cells
  használatával. Tanulja meg, hogyan emelhet ki dátumokat, állíthat be háttérszíneket,
  és automatikusan méretezheti az oszlopokat néhány kódsorral.
og_image_alt: Screenshot of an Excel sheet where yesterday's date cells are highlighted
  in pink
og_title: Feltételes formázási szabály létrehozása dátumokhoz Pythonban – lépésről‑lépésre
  útmutató
schemas:
- author: Aspose
  dateModified: '2026-08-24'
  description: Create conditional formatting rule in Python using Aspose.Cells to
    highlight dates, with auto‑fit column and background color formatting.
  headline: How to create conditional formatting rule for dates in Python
  type: TechArticle
tags:
- Aspose.Cells
- Python
- Excel automation
- Conditional formatting
title: Hogyan hozzunk létre feltételes formázási szabályt dátumokhoz Pythonban
url: /hu/python/formatting/how-to-create-conditional-formatting-rule-for-dates-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan hozzunk létre feltételes formázási szabályt dátumokhoz Pythonban

Ha **create conditional formatting rule**-t kell létrehoznod, amely a dátumokra reagál, ez az útmutató pontosan megmutatja, hogyan teheted ezt meg az Aspose.Cells for Python segítségével. Akár jelentéskészítő irányítópultot, akár automatizált táblázatot építesz, láthatod, hogyan emelheted ki a tegnapi dátumokat, alkalmazhatsz egy egyedi háttérszínt, és **auto fit column** szélességeket, hogy az eredmény kifinomult legyen.

Ebben az oktatóanyagról **conditional formatting by date**-t fogunk lefedni, bemutatunk egy **background color conditional format**-ot, és befejezzük a munkafüzet XLSX fájlként való mentésével. A végére egy újrahasználható segédfüggvényt kapsz, amelyet bármilyen **date based conditional format**-ra adaptálhatsz.

## Mit fogsz megtanulni

* Állíts be egy munkafüzetet és munkalapot az Aspose.Cells használatával.
* Írj egy segédfüggvényt, amely **date based conditional format**-ot ad hozzá bármely cellatartományhoz.
* Töltsd fel a cellákat mintadátumokkal, hogy a szabály kiértékelhető legyen.
* **auto fit column** alkalmazása a tartalom olvashatóvá tételéhez.
* Mentsd el a munkafüzetet, és ellenőrizd a kiemelt cellákat.

Az egyetlen előfeltétel egy működő Python környezet a `aspose-cells` csomag telepítésével.

## Előfeltételek

| Követelmény | Részletek |
|-------------|-----------|
| Python | 3.8+ |
| Aspose.Cells for Python via Java | `pip install aspose-cells` |
| Alapvető Excel ismeretek | worksheets, cells, formatting |
| Opcionális: IDE (VS Code, PyCharm, stb.) | bármely szerkesztő, amely képes Python szkripteket futtatni |

## 1. lépés: Munkafüzet létrehozása és az első munkalap lekérése

Az első lépés a **create conditional formatting rule**‑re kész objektumok létrehozása: egy `Workbook` és az alapértelmezett `Worksheet`. Ezek az objektumok a belépési pontot jelentik minden további művelethez.

```python
# Step 1 – initialize workbook and worksheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create a new, empty workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Miért fontos:* A `Workbook` tartalmazza az egész Excel fájlt, míg a `Worksheet` az, ahol cellákat, stílusokat és **conditional formatting by date**-t alkalmazol. Ezek az objektumok nélkül a kód többi része sehova sem tud hatni.

## 2. lépés: Segédfüggvény építése TIME_PERIOD feltételes formátum hozzáadásához

Ahelyett, hogy minden tartományra ugyanazt a sablont ismételnénk, a logikát egy segédfüggvénybe foglaljuk. Ez a függvény egy **background color conditional format**-ot csatol, amely a cellákat egy `TimePeriodType` (pl. Yesterday, Today, LastWeek) alapján színezi.

```python
def add_time_period_condition(cell_range: str, bg_color: Color, period: TimePeriodType):
    """
    Attach a TIME_PERIOD conditional format to `cell_range`.
    The rule highlights cells that fall within `period` using `bg_color`.

    Args:
        cell_range: A1‑style range string, e.g., "I19:K20".
        bg_color:   Desired background color for matching cells.
        period:     Aspose.Cells TimePeriodType enum value.
    Returns:
        The FormatConditionCollection for further customization if needed.
    """
    # 1️⃣ Attach a new ConditionalFormatting block to the specified range
    worksheet.conditional_formattings.add(cell_range)

    # 2️⃣ Grab the collection of conditions for that block
    conditions = worksheet.conditional_formattings[-1].format_conditions

    # 3️⃣ (Optional) Set a default background for the whole range
    conditions.back_color = bg_color

    # 4️⃣ Add a TIME_PERIOD condition and configure its appearance
    idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[idx]

    # Apply the visual style – pink background in this example
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Define which period triggers the formatting
    condition.time_period = period

    return conditions
```

*Miért használunk segédfüggvényt:* Elkülöníti a **date based conditional format** logikát, megkönnyítve a kód olvasását, tesztelését és újrahasználatát több munkalapon vagy projektben.

## 3. lépés: Feltételes formázási szabály alkalmazása egy adott tartományra

Most a segédfüggvényt használjuk a “Yesterday” tartalmú cellák kiemelésére. Ez a **create conditional formatting rule** műveletünk középpontja.

```python
# Step 3 – highlight cells I19:K20 that contain “Yesterday”
add_time_period_condition(
    cell_range="I19:K20",
    bg_color=Color.medium_sea_green,   # optional default background for the whole range
    period=TimePeriodType.YESTERDAY   # the date‑based trigger
)
```

Amikor a munkafüzetet megnyitják, az `I19:K20` tartományban bármely cella, amelynek dátuma megegyezik a tegnapi dátummal, rózsaszín kitöltéssel jelenik meg (a segédfüggvényben beállított stílus). A `bg_color` argumentum azt mutatja, hogyan helyezhetsz alapértelmezett háttérszínt a feltételes szín mögé, ha szükséges.

## 4. lépés: Tartomány feltöltése mintadátumokkal

A feltételes szabály csak akkor válik láthatóvá, ha a munkalap olyan adatot tartalmaz, amely teljesíti a feltételt. Két dátumot fogunk beilleszteni: egyet, amely megfelel a “Yesterday”-nek, és egyet, amely kívül esik az időszakon.

```python
# Step 4 – insert sample dates for demonstration

# Cell I19 will match the YESTERDAY period
yesterday_cell = worksheet.cells.get("I19")
yesterday_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008 is “yesterday” relative to 31‑Jul‑2008
yesterday_cell.get_style().number = 30          # 30 = built‑in date format
yesterday_cell.set_style(yesterday_cell.get_style())

# Cell K20 will NOT match the period (it’s a later date)
outside_cell = worksheet.cells.get("K20")
outside_cell.put_value(datetime(2008, 8, 3))     # 03‑Aug‑2008 is outside “Yesterday”
outside_cell.get_style().number = 30
outside_cell.set_style(outside_cell.get_style())

# Optional label for clarity – not part of the rule
worksheet.cells.get("I20").put_value("Yesterday")
```

*Miért fontos:* `datetime` objektumok használatával biztosítjuk, hogy az Excel valódi dátumként kezelje az értékeket, ami szükséges a **conditional formatting by date** helyes működéséhez. A numerikus formátum (`30`) garantálja, hogy a cellák felismerhető dátumként jelenjenek meg.

## 5. lépés: Oszlop automatikus méretezése és a munkafüzet mentése

Miután az adatok és a formázás helyre került, az utolsó simítás a **auto fit column** szélességek beállítása, hogy a dátumok teljesen láthatóak legyenek. Ezután a fájlt lemezre írjuk.

```python
# Step 5 – adjust column width and save the file

# Auto‑fit column 12 (the column that contains our sample data)
worksheet.auto_fit_column(12)

# Save the workbook as an XLSX file
output_path = "YOUR_DIRECTORY/TimePeriodDemo.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

Az `auto_fit_column` hívás a 12. oszlopban (ami az Excel **L** oszlopának felel meg) a leghosszabb tartalmat vizsgálja, és ennek megfelelően növeli a szélességet. Ez a kis lépés megakadályozza a dátumok csonkítását, és a **background color conditional format** egyértelműen láthatóvá válik.

### Várható eredmény

Amikor megnyitod a `TimePeriodDemo.out.xlsx` fájlt:

| I19 (dátum) | I20 (címke) | K20 (dátum) |
|------------|------------|------------|
| 30‑Jul‑2008 (rózsaszín kiemelve) | Tegnap | 03‑Aug‑2008 (nincs kiemelés) |

* A tegnapi dátumot tartalmazó cella rózsaszín háttérrel jelenik meg, mert a **create conditional formatting rule** egyezett a `YESTERDAY` időszakkal.
* Minden más cella megtartja az alapértelmezett háttérszínt (vagy a megadott opcionális `medium_sea_green`-t).
* Az L oszlop automatikusan szélesedik, így a dátumok teljesen olvashatóak.

## Gyakori variációk és szélhelyzetek

| Helyzet | Hogyan módosítsuk a kódot |
|-----------|-----------------------|
| **Highlight “Today” instead of “Yesterday”** | Replace `TimePeriodType.YESTERDAY` with `TimePeriodType.TODAY`. |
| **Use a different background color** | Change `condition.style.background_color = Color.pink` to any other `Color` (e.g., `Color.light_sky_blue`). |
| **Apply the rule to a non‑contiguous range** | Call `add_time_period_condition` multiple times with different `cell_range` strings (e.g., `"A1:A10", "C1:C10"`). |
| **Work with a pre‑existing workbook** | Load the file with `Workbook("myfile.xlsx")` instead of creating a new one. |
| **Multiple date‑based conditions on the same range** | After the first `add_time_period_condition` call, add another condition with `conditions.add_condition(FormatConditionType.TIME_PERIOD)` and set a different `time_period`. |

## Következtetés

Most már tudod, hogyan **create conditional formatting rule**-t hozhatsz létre, amely a dátumokra reagál, hogyan alkalmazz **background color conditional format**-ot, és hogyan **auto fit column** szélességeket az Aspose.Cells for Python használatával. A segédfüggvény elvonja a logikát, lehetővé téve, hogy ugyanazt a mintát újrahasználd bármilyen **conditional formatting by date** helyzetben – legyen az „Yesterday”, „LastWeek” vagy egy egyedi tartomány.

Ezután érdemes lehet:

* **icon sets** vagy **data bars** hozzáadása a dátumszabályok mellé.
* Dinamikus jelentések generálása, amelyek adatbázisból húznak dátumokat.
* Több **date based conditional format** szabály kombinálása egyetlen munkalapon.

Nyugodtan kísérletezz különböző színekkel, időszakokkal és tartományokkal, hogy megfeleljenek a projekted igényeinek. Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Az Excel feltételes formázásának mestersége Aspose.Cells .NET használatával: Átfogó útmutató](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Hogyan nyerjünk ki feltételes formázási színeket az Aspose.Cells for .NET használatával](/cells/english/net/formatting/extract-conditional-formatting-colors-aspose-cells-net/)
- [Feltételes formázás mestersége egyedi betűtípusokkal Excelben az Aspose.Cells for .NET és C# használatával](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}