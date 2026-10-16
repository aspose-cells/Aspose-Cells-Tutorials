---
category: general
date: 2026-09-21
description: Naučte se, jak vytvořit sešit Excel v Pythonu, nastavit barvu pozadí
  buňky a použít podmíněné formátování založené na datu pomocí Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: cs
lastmod: 2026-09-21
og_description: Vytvořte Excel sešit v Pythonu, nastavte barvu pozadí buňky a použijte
  podmíněné formátování založené na datu pomocí Aspose.Cells. Postupujte podle krok‑za‑krokem
  průvodce.
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: Vytvořte Excel sešit v Pythonu s podmíněným formátováním
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
title: Vytvořte Excel sešit v Pythonu pomocí podmíněného formátování
url: /cs/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořte Excel sešit v Pythonu pomocí podmíněného formátování

Pokud potřebujete **create Excel workbook python** skripty, které automaticky zvýrazní data, tento průvodce vám ukáže přesně jak. Uvidíte, jak **set cell background color**, přidat pravidlo „Yesterday“ a uložit soubor — vše s Aspose.Cells pro Python.

Práce s Excel soubory programově často znamená opakování stejné logiky formátování napříč mnoha listy. Na konci tohoto tutoriálu budete mít znovupoužitelný vzor pro **excel conditional formatting python**, který můžete vložit do jakéhokoli projektu.

## Požadavky

- Python 3.8+ nainstalován  
- balíček `aspose-cells` (`pip install aspose-cells`)  
- Základní znalost Python funkcí a modulu datetime  

Žádné další knihovny nejsou potřeba; Aspose.Cells zpracovává všechny operace s Excelem.

## Krok 1: Vytvořte sešit a přistupte k prvnímu listu

Prvním krokem je **create excel workbook python** objekty a získat výchozí list. To vám poskytne čisté plátno pro další stylování.

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

*Proč je to důležité:* `Workbook()` vytváří Excel soubor v paměti. Přístup k `worksheets[0]` zabraňuje pevně zakódovaným názvům listů a funguje i když se výchozí název změní.

## Krok 2: Pomocná funkce pro přidání podmíněného formátu TIME_PERIOD

Aby byl kód přehledný, zabalíme vytvoření podmíněného formátu do pomocné funkce. Přijímá rozsah buněk, barvu pozadí a požadované pravidlo časového období.

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

*Proč je to důležité:* Pomocná funkce abstrahuje opakující se kroky při vytváření podmíněného formátu, což usnadňuje opětovné použití pro další pravidla založená na datech, jako je „Today“ nebo „Last Week“.

## Krok 3: Použijte pravidlo „Yesterday“ na rozsah

Nyní použijeme pomocnou funkci k zvýraznění buněk, které obsahují včerejší datum. Rozsah `I19:K20` se změní na **medium sea green**, když je podmínka splněna.

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*Proč je to důležité:* `TimePeriodType.YESTERDAY` je součástí vestavěné výčtové hodnoty Aspose.Cells, takže nemusíte počítat data ručně. Knihovna vyhodnocuje pravidlo při každém otevření sešitu.

## Krok 4: Naplňte rozsah ukázkovými daty

Aby bylo vidět pravidlo v akci, zapíšeme dvě data — jedno, které odpovídá „Yesterday“, a druhé, které ne. Styl `number` `30` odpovídá vestavěnému formátu data.

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

*Proč je to důležité:* Vložení konkrétních dat vám umožní ověřit, že podmíněné formátování funguje, aniž byste museli soubor otevřít konkrétní den.

## Krok 5: Přidejte popisný štítek a automaticky přizpůsobte sloupec

Malý štítek objasňuje účel formátovaného rozsahu a `auto_fit_column` učiní list čitelným.

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## Krok 6: Uložte sešit

Nakonec zapíšete sešit na disk. Volání `os.makedirs` zajistí, že cílová složka existuje.

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Když otevřete *TimePeriodDemo.xlsx*, uvidíte:

- Buňka **I19** je vybarvena **medium sea green**, protože její hodnota odpovídá pravidlu „Yesterday“.
- Buňka **K20** si ponechává výchozí pozadí, protože její datum nesplňuje podmínku.

Toto demonstruje **format cells by date** pomocí jediného řádku Python kódu.

## Kompletní, spustitelný příklad

Spojením všech částí dohromady je zde kompletní skript, který můžete zkopírovat a spustit:

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

Spusťte skript, otevřete vzniklý soubor a uvidíte podmíněné formátování v akci.

## Běžné varianty a okrajové případy

| Variace | Jak implementovat | Kdy použít |
|-----------|------------------|-------------|
| **Highlight “Today”** | Nahraďte `TimePeriodType.YESTERDAY` za `TimePeriodType.TODAY` | Real‑time dashboardy |
| **Multiple ranges** | Zavolejte `add_time_period` pro každý rozsah s různými barvami | Složité reporty |
| **Dynamic date range** | Použijte `TimePeriodType.LAST_7_DAYS` nebo `TimePeriodType.NEXT_MONTH` | Průběžné reporty |
| **Custom color** | Použijte `Color.from_argb(255, r, g, b)` k vytvoření libovolného odstínu | Stylování v souladu se značkou |

**Pro tip:** Vždy nastavte `condition.style.pattern = BackgroundType.SOLID`, když chcete plnou výplň; jinak může Excel zobrazit gradient, který vypadá nekonzistentně napříč verzemi.

## Závěr

Nyní víte, jak vytvořit **create Excel workbook python** skripty, které **set cell background color**, aplikují **excel conditional formatting python** a **format cells by date** pomocí Aspose.Cells. Příklad pokrývá scénář **date based conditional formatting**, ale stejný vzor funguje pro jakékoli pravidlo časového období.

Dále můžete zkoumat:

- Přidání datových pruhů nebo ikonových sad (`FormatConditionType.DATA_BAR`)  
- Kombinování více podmíněných pravidel na stejném rozsahu  
- Export sešitu do PDF (`SaveFormat.PDF`) pro reportování  

Neváhejte experimentovat s různými barvami, rozsahy a typy časových období, aby vyhovovaly vašim konkrétním potřebám reportování. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Mistrovství v formátování buněk Excel a správě sešitů s Aspose.Cells pro .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Automatizace Excelu s Aspose.Cells .NET: Vytvoření sešitu a nastavení externích odkazů](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Jak vytvořit pojmenované rozsahy omezené na sešit v Excelu pomocí Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}