---
category: general
date: 2026-09-15
description: Naučte se, jak použít podmíněné formátování časových období a uložit
  sešit jako XLSX pomocí Aspose.Cells v Pythonu. Obsahuje krok‑za‑krokem kód.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: cs
lastmod: 2026-09-15
og_description: Použijte podmíněné formátování časových období v Excelu pomocí Pythonu
  a uložte sešit jako XLSX. Postupujte podle tohoto kompletního průvodce pro Aspose.Cells.
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: Použijte podmíněné formátování časových období v Excelu pomocí Pythonu
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  headline: How to apply time period conditional formatting in Excel using Python
  type: TechArticle
- description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  name: How to apply time period conditional formatting in Excel using Python
  steps:
  - name: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
    text: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
  - name: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
    text: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
  - name: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
    text: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
  - name: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
    text: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
  - name: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
    text: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
  - name: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
    text: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
  - name: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
    text: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
  - name: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
    text: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
  - name: The cell `I20` shows the text “Yesterday”.
    text: The cell `I20` shows the text “Yesterday”.
  - name: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
    text: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Jak v Excelu použít podmíněné formátování časových období pomocí Pythonu
url: /cs/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít podmíněné formátování časového období v Excelu pomocí Pythonu

Pokud potřebujete **podmíněné formátování časového období** v souboru Excel, tento tutoriál vám přesně ukáže, jak to provést pomocí Pythonu. Uvidíte kompletní, spustitelný příklad, který vytvoří sešit, zvýrazní včerejší data a **uloží sešit jako XLSX** během několika řádků kódu.

Podmíněné formátování je výkonný způsob, jak upoutat pozornost na data splňující konkrétní pravidlo. V tomto průvodci se zaměříme na časové období „Yesterday“, ale stejný vzor funguje i pro další vestavěná období, jako je Today, LastWeek a NextMonth. Na konci tutoriálu budete schopni **jak vytvořit excel workbook python**‑stylové skripty připravené pro produkci.

## Prerekvizity

- Python 3.8+ nainstalovaný  
- Balíčky `aspose-cells` a `aspose-pydrawing` (`pip install aspose-cells aspose-pydrawing`)  
- Základní znalost syntaxe Pythonu  

Další instalace Office není vyžadována, protože Aspose.Cells interně generuje soubor.

## Podmíněné formátování časového období s Aspose.Cells v Pythonu

Tato sekce prochází každým řádkem kódu potřebným pro hlavní úkol. Níže uvedený kódový blok je kompletní skript; komentáře vysvětlují účel jednotlivých kroků.

```python
# -*- coding: utf-8 -*-
"""
Apply time period conditional formatting to highlight yesterday's dates
and save the workbook as XLSX using Aspose.Cells for Python.
"""

from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the range that will receive the conditional formatting rule
cell_range = "I19:K20"
cond_format = worksheet.conditional_formattings.add(cell_range)

# Step 3: Add a TIME_PERIOD condition for “Yesterday” and style it
condition_index = cond_format.add_condition(FormatConditionType.TIME_PERIOD)
condition = cond_format[condition_index]
condition.style.background_color = Color.pink          # Highlight colour
condition.style.pattern = BackgroundType.SOLID        # Solid fill
condition.time_period = TimePeriodType.YESTERDAY      # Built‑in “Yesterday” period

# Step 4: Populate the range with sample dates (Excel number format 30 = short date)
date_cells = ["I19", "K20"]                           # Cells that will contain dates
sample_dates = [datetime(2008, 7, 30), datetime(2008, 8, 3)]
for cell_ref, date_val in zip(date_cells, sample_dates):
    cell = worksheet.cells.get(cell_ref)
    cell.put_value(date_val)                         # Write the Python datetime
    style = cell.get_style()
    style.number = 30                                 # Excel short date format
    cell.set_style(style)

# Step 5: Add a label so the user knows what the rule represents
worksheet.cells.get("I20").put_value("Yesterday")

# Step 6: Auto‑fit the column for better readability (column L is index 12)
worksheet.auto_fit_column(12)

# Step 7: Save the workbook – this demonstrates “save workbook as xlsx”
output_path = "TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

### Proč je každý krok důležitý

1. **Vytvoření sešitu** vám poskytne Excel soubor v paměti, který můžete upravovat bez otevření Excelu.  
2. **Definování rozsahu** (`I19:K20`) říká Aspose.Cells, kde se pravidlo použije, a udržuje logiku izolovanou.  
3. **Přidání podmínky TIME_PERIOD** používá vestavěnou enumeraci Aspose `TimePeriodType.YESTERDAY`. Tím se vyhnete ručním výpočtům dat a pravidlo se automaticky aktualizuje při otevření souboru v jiný den.  
4. **Nastavení stylu** (`background_color` a `pattern`) určuje, jak budou zvýrazněné buňky vypadat. Použití `Color.pink` usnadňuje pravidlo rozpoznat.  
5. **Zapsání ukázkových dat** s formátem čísla 30 zajišťuje, že Excel zobrazí data jako krátké datumy místo sériových čísel.  
6. **Automatické přizpůsobení šířky sloupce** zlepšuje čitelnost pro každého, kdo soubor později otevře.  
7. **Uložení jako XLSX** vytvoří široce kompatibilní soubor, který lze otevřít v Excelu, Google Sheets nebo jakémkoli moderním tabulkovém programu.

## Jak vytvořit Excel workbook Python‑style s Aspose.Cells

Výše uvedený skript již demonstruje minimální kroky k **jak vytvořit excel workbook python**. V praxi můžete chtít:

- Přidat více listů (`workbook.worksheets.add("Report")`).  
- Naplnit velké datové tabulky pomocí smyček nebo pandas DataFrames (`worksheet.cells.import_data_table`).  
- Použít další formátování (písma, okraje) pomocí `cell.get_style()`.

Všechny tyto akce následují stejný vzor: získat objekt, upravit jeho vlastnosti a zavolat `set_style` nebo `save`.

## Přidání podmíněného formátování v Pythonu – další užitečné vzory

Kromě příkladu „Yesterday“ podporuje Aspose.Cells několik typů podmíněného formátování:

| FormatConditionType | Typický případ použití |
|---------------------|-----------------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | Vlastní vzorce (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | Jednoduché porovnání (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | Gradientní barevné stupnice |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | Vizualizace pruhů v buňce |

Pro **add conditional formatting python** pro číselný práh byste nahradili `FormatConditionType.TIME_PERIOD` za `FormatConditionType.CELL_VALUE` a nastavili `condition.operator_type` a `condition.formula1`.

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## Uložení sešitu jako XLSX – osvědčené postupy

Když **save workbook as xlsx**, zvažte:

- **Specifikaci správného `SaveFormat`** (`SaveFormat.XLSX`) pro vyhnutí se starším formátům.  
- **Použití deterministického názvu souboru**, pokud skript běží ve smyčce (`f"report_{datetime.now():%Y%m%d}.xlsx"`).  
- **Uzavření zdrojů** (`workbook.dispose()`) v dlouho běžících službách pro uvolnění nativní paměti.

Příklad již používá `SaveFormat.XLSX`, což vytváří moderní, zip‑základní sešit, který zachovává všechna pravidla podmíněného formátování.

## Zvýraznění včerejška v Excelu – ověřovací kroky

Po spuštění skriptu otevřete `TimePeriodExample.xlsx`:

1. Buňky `I19` a `K20` obsahují data `30‑07‑2008` a `03‑08‑2008`.  
2. Buňka `I20` zobrazuje text „Yesterday“.  
3. Pokud změníte systémové datum na **30 července 2008** a soubor znovu otevřete, buňky s odpovídajícími daty se automaticky vyplní růžovou barvou.  
4. Změna systémového data na jakýkoli jiný den růžové vyplnění odstraní, což potvrzuje, že pravidlo reaguje na **time period conditional formatting** logiku.

## Časté úskalí a jak se jim vyhnout

- **Chybějící `aspose-pydrawing`** – třída `Color` je v tomto balíčku; zapomenutí instalace vyvolá `ImportError`.  
- **Nesprávný formát čísla** – použití výchozího formátu General zobrazí sériová čísla (např. 39822). Vždy nastavte `style.number = 30` pro krátké datumy.  
- **Neshoda rozsahu** – rozsah podmíněného formátování musí zahrnovat buňky, které chcete zvýraznit; jinak pravidlo nemá žádný efekt.

## Pro tip: znovupoužití formátovací rutiny

Pokud potřebujete stejný pravidlo „Yesterday“ v několika sešitech, zabalte logiku do pomocné funkce:

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

Zavolejte `apply_yesterday_highlight(worksheet, "A1:A10")` kdekoliv potřebujete.

## Závěr

Tento průvodce vám ukázal, jak implementovat **time period conditional formatting** v Excelu pomocí Pythonu, jak **save workbook as XLSX**, a jak **highlight yesterday in Excel** jedním znovupoužitelným skriptem. Nyní máte pevný základ pro **add conditional formatting python** kód v jakémkoli automatizačním projektu, ať už generujete denní reporty, budujete dashboardy nebo připravujete exporty dat.

**Další kroky**

- Prozkoumejte další hodnoty `TimePeriodType`, jako jsou `TODAY` nebo `LAST_WEEK`.  
- Kombinujte více podmíněných pravidel na stejném rozsahu pro bohatší vizuální nápovědy.  
- Integrovat generování sešitu do webové služby nebo naplánované úlohy.

Šťastné kódování a užijte si vizuální přehlednost, kterou podmíněné formátování přináší do vaší Excel automatizace!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Master Conditional Formatting in Excel Using Aspose.Cells .NET : A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Master Aspose.Cells .NET : Apply Conditional Formatting to Alternate Rows in Excel](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [Master Conditional Formatting with Custom Fonts in Excel using Aspose.Cells for .NET and C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}