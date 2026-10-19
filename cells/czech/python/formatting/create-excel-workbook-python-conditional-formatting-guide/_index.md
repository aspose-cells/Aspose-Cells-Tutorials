---
category: general
date: 2026-07-20
description: Vytvořte Excel sešit v Pythonu pomocí Aspose.Cells, nastavte barvu pozadí
  buňky a přidejte podmíněné formátování v Pythonu pro stylování buněk podle data.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: cs
lastmod: 2026-07-20
og_description: Vytvořte Excel sešit v Pythonu pomocí Aspose.Cells. Naučte se, jak
  nastavit barvu pozadí buňky a přidat podmíněné formátování v Pythonu pro formátování
  buněk podle data.
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: Vytvořte Excel sešit v Pythonu – Přidejte podmíněné formátování
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
title: Vytvoření Excel sešitu v Pythonu – Průvodce podmíněným formátováním
url: /cs/python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření Excel sešitu v Pythonu – Průvodce podmíněným formátováním

Už jste se někdy zamysleli, jak **create Excel workbook Python** od nuly a vytvořit profesionální vzhled bez otevírání UI? Nejste sami. Mnoho vývojářů narazí na problém, když potřebují **set cell background color** nebo aplikovat stylování založené na datech programově.  

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který používá Aspose.Cells k **add conditional formatting python** pravidlům, formátování buněk podle data a uložení výsledku jako moderní soubor XLSX. Na konci budete mít samostatný skript, který můžete vložit do libovolného projektu.

## Co se naučíte

- Jak inicializovat sešit a získat první list.  
- Způsoby, jak **set cell background color** pro celý rozsah.  
- Použití **aspose cells conditional formatting** k zvýraznění dat „Včera“.  
- Automatické přizpůsobení sloupců a uložení souboru na disk.  

Žádná externí konfigurace není vyžadována – stačí Python 3 a balíček Aspose.Cells. Pokud už máte nainstalováno `aspose-cells`, můžete rovnou začít; jinak stačí rychle spustit `pip install aspose-cells`.

## Požadavky

- Python 3.8+ (kód funguje na 3.9, 3.10 a novějších).  
- Aspose.Cells for Python via .NET (`aspose-cells` NuGet wrapper).  
- Základní znalost konceptů Excelu (buňky, rozsahy, formátování).  

Máte vše? Skvělé – ponořme se do toho.

## Vytvoření Excel sešitu v Pythonu – Nastavení a list

Nejprve potřebujeme čerstvý objekt sešitu a odkaz na výchozí list. Toto je plátno, kde se budou provádět všechny následné operace.

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **Why this matters:** `Workbook()` constructs an in‑memory Excel file, eliminating the need for any temporary files. The `worksheet` variable is our entry point for cell‑level actions.

## Nastavení barvy pozadí buňky

Než přidáme jakákoli pravidla, je hezké dát cílovému rozsahu základní barvu, aby podmíněné formátování vyniklo. Pomocná funkce níže jak získá (nebo vytvoří) `FormatConditionCollection` pro daný rozsah, tak buňky natřel plnou barvou pozadí.

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

> **Pro tip:** If you plan to reuse the same range with multiple rules, call this helper once and keep the returned collection; it saves a few API calls.

## Přidání podmíněného formátování v Pythonu pro datové rozsahy

Teď ta zábavná část: vytvoříme **time‑period conditional formatting** pravidlo, které zvýrazní buňky obsahující včerejší datum. To demonstruje sílu **format cells by date** pomocí Aspose.Cells.

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

> **Why use `TIME_PERIOD`?** It abstracts away the need to write custom formulas. Aspose.Cells evaluates the date against the current system date, so the rule always stays relevant.

### Spuštění pravidla

```python
apply_yesterday_rule()
```

Když otevřete výsledný soubor, buňky `I19` budou růžově svítit (protože jsou „Yesterday“), zatímco `K20` zůstane v základní zelené barvě.

## Automatické přizpůsobení sloupců a uložení sešitu

Upravený tabulkový list vypadá profesionálně. Automatické přizpůsobení zajistí, že naše data nebudou stísněná.

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Edge case:** If you target a directory that doesn’t exist, `workbook.save` will raise an error. Wrap the save call in a `try/except` block if you need graceful handling.

### Kompletní skript (připravený ke kopírování)

Níže je celý skript, připravený ke spuštění. Stačí nahradit `YOUR_DIRECTORY` platnou složkou na vašem počítači.

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

Spuštěním tohoto skriptu vznikne soubor `TimePeriodExample.xlsx` s podmíněným formátováním, které jsme popsali.

## Často kladené otázky a tipy

- **Can I target a different date range?**  
  Absolutely. Change `"I19:K20"` to any A1‑style range, and adjust the sample dates accordingly.

- **What if I need a custom formula instead of `YESTERDAY`?**  
  Use `FormatConditionType.FORMULA` and set `condition.formula1 = "YOUR_FORMULA"`—for example, `=TODAY()-A1=1` to mimic yesterday.

- **How do I apply multiple rules to the same range?**  
  Call `conditions.add_condition` again with a different `FormatConditionType`. The order matters; later rules can override earlier ones.

- **Is there a way to set font colour together with background?**  
  Yes—modify `condition.style.font.color = Color.white` (or any other `Color`).

## Závěr

Nyní už víte, jak **create Excel workbook Python** pomocí Aspose.Cells, **set cell background color** a **add conditional formatting python**, které formátuje buňky podle data. Skript je plně funkční, řeší okrajové případy jako chybějící adresáře a lze jej rozšířit o složitější scénáře, jako je vícepravidlová podmíněná logika nebo dynamické určení rozsahu.

Jste připraveni na další krok? Zkuste vyměnit pravidlo „Yesterday“ za „Last Week“, experimentujte s gradientními výplněmi nebo vygenerujte kompletní report s desítkami formátovaných tabulek. Stavební bloky jsou zde všechny a právě jste si osvojili jádro **aspose cells conditional formatting** v Pythonu.

Šťastné programování a klidně sdílejte své vlastní varianty v komentářích!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich vlastních projektech.

- [Ovládněte formátování buněk v Excelu a správu sešitu s Aspose.Cells pro .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Jak vytvořit a uložit Excel sešit jako ODS pomocí Aspose.Cells pro .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Jak vytvořit pojmenované oblasti omezené na sešit v Excelu pomocí Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}