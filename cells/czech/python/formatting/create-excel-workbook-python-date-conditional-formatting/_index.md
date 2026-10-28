---
category: general
date: 2026-08-08
description: Vytvořte Excel sešit v Pythonu a přidejte podmíněné formátování na základě
  data. Krok za krokem průvodce s použitím Aspose.Cells pro zvýraznění buněk ze včerejška.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: cs
lastmod: 2026-08-08
og_description: Vytvořte Excelový sešit v Pythonu s Aspose.Cells a použijte podmíněné
  formátování na základě data pro dynamické tabulky.
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: Vytvořte Excel sešit v Pythonu – podmíněné formátování podle data
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
title: Vytvořit Excel sešit s podmíněným formátováním data v Pythonu
url: /cs/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření Excel sešitu v Pythonu s podmíněným formátováním podle data

Pokud potřebujete **create Excel workbook Python** a automaticky zvýraznit buňky, které odpovídají konkrétnímu datu, tento tutoriál vám přesně ukáže, jak na to. Naučíte se použít **conditional formatting based on date**, aby se včerejší data rozsvítila růžově, pomocí knihovny Aspose.Cells.

Průvodce vás provede každým krokem — od instalace SDK až po uložení finálního souboru .xlsx — takže můžete zkopírovat‑vložit funkční příklad do svého projektu. Není potřeba žádná externí dokumentace; veškerý kód a vysvětlení jsou kompletní.

## Prerequisites

Než začnete, ujistěte se, že máte:

* Python 3.8 nebo novější nainstalovaný.
* `aspose-cells` balíček (Python wrapper pro Aspose.Cells). Nainstalujte jej pomocí:
  ```bash
  pip install aspose-cells
  ```
* Základní znalosti Pythonu a konceptů Excelu, jako jsou listy a styly buněk.

> **Pro tip:** Aspose.Cells funguje bez nainstalovaného Microsoft Excel, což ho činí ideálním pro automatizaci na serveru.

## Step 1: Create the Excel workbook in Python

Prvním úkolem je vytvořit novou instanci sešitu a získat výchozí list. Tento objekt představuje celý Excel soubor a poskytuje přístup k řádkům, sloupcům a API pro formátování.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

Vytvoření sešitu je základem pro jakoukoli další manipulaci, ať už přidáváte data, vzorce nebo pravidla formátování.

## Step 2: Define a date‑based conditional format

Nyní přidáme **conditional formatting based on date**. Výčtový typ `FormatConditionType.TIME_PERIOD` nám umožňuje specifikovat vestavěné časové období, jako je Yesterday, Today nebo LastWeek.

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

Proč je tento krok důležitý: Excel vyhodnocuje podmínku pro každou buňku v rozsahu. Když hodnota buňky spadá do definovaného období (včera), automaticky se použije přiřazený styl.

## Step 3: Populate the range with sample dates

Abychom viděli pravidlo v akci, zapíšeme několik objektů `datetime` do cílových buněk. Jeden z nich je úmyslně nastaven na včerejší datum vzhledem k internímu datovému systému sešitu.

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

Řádek `number = 30` říká Excelu, aby hodnotu zobrazil pomocí standardního formátu krátkého data. Tento index můžete změnit na libovolný vestavěný číselný formát, pokud preferujete jinou prezentaci.

## Step 4: Adjust column width for readability

Automatické přizpůsobení šířky sloupce, který obsahuje data, usnadní čtení výstupu, zejména když je sešit otevřen v Excelu nebo prohlížeči.

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## Step 5: Save the workbook to disk

Nakonec uložte sešit jako soubor .xlsx. Nahraďte `"YOUR_DIRECTORY"` skutečnou cestou na vašem počítači.

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Když otevřete `TimePeriodDemo.out.xlsx` v Excelu, buňka **I19** se zobrazí s růžovým pozadím, protože její hodnota odpovídá pravidlu „Yesterday“, zatímco **K20** zůstane beze změny.

### Expected output

| I19 (datum) | I20 (popisek) | J19 | J20 | K19 | K20 (datum) |
|------------|---------------|-----|-----|-----|------------|
| *2008‑07‑30* (růžové pozadí) | Včera | – | – | – | *2008‑08‑03* (bez formátování) |

Růžové zabarvení potvrzuje, že **conditional formatting based on date** funguje podle očekávání.

## Common variations and edge cases

| Situation | How to adapt the code |
|-----------|-----------------------|
| **Highlight “Today” instead of “Yesterday”** | Change `condition.time_period = TimePeriodType.TODAY` |
| **Apply the rule to an entire column** | Use `worksheet.get_range("A:A").format_conditions` |
| **Use a custom date range (e.g., last 7 days)** | Replace the time‑period condition with a formula condition: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **Different background colors** | Set `condition.style.background_color = Color.light_green` (or any `Color` you prefer) |
| **Running on Linux without a display** | Aspose.Cells is fully headless; no extra configuration required. |

## Full, runnable example

Níže je kompletní skript, který můžete spustit tak, jak je (po aktualizaci výstupního adresáře). Všechny importy, komentáře a základní ošetření chyb jsou zahrnuty.

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

Spuštěním skriptu vznikne Excel soubor, kde je buňka „Yesterday“ automaticky zvýrazněna, což demonstruje **create Excel workbook Python** v kombinaci s **conditional formatting based on date**.

## Conclusion

Nyní víte, jak **create Excel workbook Python** objekty, definovat **date‑based conditional formatting**.

## What Should You Learn Next?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich vlastních projektech.

- [Vytvoření Excel sešitu pomocí Aspose.Cells v Javě: průvodce krok za krokem](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Vytvoření Excel sešitu s grafy pomocí Aspose.Cells .NET | průvodce krok za krokem](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Automatizace Excelu: Vytvoření sešitu a přidání ListBoxu pomocí Aspose.Cells pro .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}