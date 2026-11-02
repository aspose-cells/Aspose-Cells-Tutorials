---
category: general
date: 2026-09-05
description: Vytvořte sešit Excel v Pythonu a přidejte podmíněné formátování pro zvýraznění
  buněk ze včerejška. Naučte se celý kód a proč je každý krok důležitý.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: cs
lastmod: 2026-09-05
og_description: Vytvořte Excel sešit v Pythonu a přidejte podmíněné formátování pro
  zvýraznění buněk ze včerejška. Postupujte podle tohoto průvodce krok za krokem pro
  kompletní řešení.
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: Vytvořte Excel sešit v Pythonu – přidejte podmíněné formátování
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create Excel workbook in Python and add conditional formatting to highlight
    yesterday cells. Learn the full code and why each step matters.
  headline: Create Excel workbook in Python with conditional formatting
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Vytvořte Excel sešit v Pythonu s podmíněným formátováním
url: /cs/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření sešitu Excel v Pythonu s podmíněným formátováním

Pokud potřebujete **create Excel workbook python** pro úkol reportování, tento průvodce vám ukáže, jak vygenerovat sešit a použít pravidlo podmíněného formátování, které zvýrazní včerejší data. Uvidíte přesný kód, proč každá řádka existuje, a jak přizpůsobit řešení pro jiné časové intervaly.

Podmíněné formátování je výkonný způsob, jak upoutat pozornost na data, která splňují konkrétní podmínku. V tomto tutoriálu používáme knihovnu Aspose.Cells pro Python via .NET, která poskytuje plnou podporu funkcí Excelu bez nutnosti Microsoft Office. Na konci průvodce budete mít soubor, kde buňky v rozsahu *I19:K20* se zbarví růžově, pokud obsahují včerejší datum.

## Požadavky

* Nainstalovaný Python 3.9+
* Balíček `aspose-cells` (nainstalujte pomocí `pip install aspose-cells`)
* Základní znalost syntaxe Pythonu
* Oprávnění k zápisu do adresáře, kde bude sešit uložen

Kód funguje na Windows, macOS i Linuxu, pokud je k dispozici .NET runtime.

## Vytvoření sešitu Excel v Pythonu

Prvním krokem je vytvořit objekt `Workbook` a získat výchozí list. Tento objekt představuje celý soubor Excel v paměti.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Proč je to důležité*: `Workbook()` vytvoří prázdný sešit s jedním listem. Přístup k `worksheets[0]` vám poskytne referenci pro pozdější přidání dat, stylů a formátování.

## Přidání rozsahu podmíněného formátování

Dále definujeme oblast, která bude vyhodnocena podmíněným pravidlem. Rozsah `I19:K20` zahrnuje šest buněk ve dvou řádcích.

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*Proč je to důležité*: Přidání kolekce podmíněného formátování k určitému rozsahu izoluje pravidlo a zabraňuje jeho vlivu na nesouvisející buňky. Tím se splňuje požadavek **add conditional formatting range**.

## Definice pravidla: zvýraznění buněk na základě data

Nyní vytvoříme podmínku typu `TIME_PERIOD`. To říká Excelu, aby porovnával hodnotu každé buňky s předdefinovaným časovým oknem.

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*Proč je to důležité*: `TIME_PERIOD` je jediný vestavěný typ, který přímo podporuje „Yesterday“, „Today“, „Last Week“ atd. Nastavením `condition.time_period` na `YESTERDAY` pravidlo automaticky vyhodnocuje datum v buňce vůči dni před aktuálním datem.

## Stylování buněk, které splňují podmínku

Podmíněné formátování také vyžaduje vizuální styl. Zde volíme růžové plné vyplnění, aby se odpovídající buňky vynikly.

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*Proč je to důležité*: Objekt stylu určuje, jak Excel vykreslí buňky, které splňují podmínku. Použití plného růžového vyplnění splňuje požadavek **highlight cells based on date** a usnadňuje ověření výsledku.

## Naplnění ukázkových dat pro vyhodnocení

Abychom viděli pravidlo v akci, vložíme dva data – jedno, které odpovídá včerejšímu datu, a druhé, které ne. Formát `number` `30` odpovídá vestavěnému formátu data `mm-dd-yy`.

```python
from datetime import datetime

# Cell I19: a date that matches “Yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Example date; adjust as needed
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

# Cell K20: a date outside the “Yesterday” period
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Example date; adjust as needed
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Optional label for the range
worksheet.cells.get("I20").put_value("Yesterday")
```

*Proč je to důležité*: Poskytnutí jak odpovídajícího, tak neodpovídajícího data vám umožní ověřit, že podmíněné formátování funguje správně. Přizpůsobte data aktuálnímu měsíci při spuštění skriptu nebo je nahraďte dynamickými hodnotami.

## Uložení sešitu

Nakonec soubor zapíšeme na disk. Konstantní `SaveFormat.XLSX` zajišťuje, že výstup je moderní soubor Excel.

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*Proč je to důležité*: Uložení sešitu vám umožní otevřít jej v Excelu, LibreOffice nebo jakémkoli prohlížeči podporujícím XLSX. Vytisknutá cesta potvrzuje, kam byl soubor zapsán.

## Kompletní skript

Spojením všech částí dohromady vypadá kompletní spustitelný skript takto:

```python
# -*- coding: utf-8 -*-
"""
Create an Excel workbook in Python, add a conditional formatting rule,
and highlight yesterday's cells.
"""

from aspose.cells import (
    Workbook, SaveFormat, FormatConditionType,
    BackgroundType, TimePeriodType
)
from aspose.pydrawing import Color as DrawingColor
from datetime import datetime

# Step 1: Create a new workbook and access the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Add a conditional formatting rule for the range I19:K20
condition_collection = worksheet.conditional_formattings.add("I19:K20")
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Step 3: Define the visual style for cells that meet the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID

# Step 4: Set the time‑period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Step 5: Populate sample dates for evaluation
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # yesterday relative to the example
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # outside the period
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Step 6: Add a label for the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Očekávaný výstup

Když otevřete `TimePeriodExample.xlsx`:

* Buňka **I19** se zobrazí s růžovým pozadím, protože její hodnota odpovídá včerejšímu datu.
* Buňka **K20** si ponechá výchozí pozadí, protože její datum spadá mimo období.
* Štítek **„Yesterday“** je umístěn v buňce I20 pro přehlednost.

## Běžné varianty a okrajové případy

| Situace | Úprava |
|-----------|------------|
| **Zvýraznit dnešek místo včerejška** | Změňte `condition.time_period = TimePeriodType.TODAY`. |
| **Použít pravidlo na větší oblast** | Aktualizujte řetězec rozsahu v `add("I19:K20")` na něco jako `"A1:Z100"`. |
| **Použít jinou barvu výplně** | Nahraďte `DrawingColor.pink` libovolnou jinou `DrawingColor` (např. `DrawingColor.light_green`). |
| **Pracovat s dynamickými daty** | Vypočítejte `datetime.now() - timedelta(days=1)` pro včerejší datum a zapište tuto hodnotu do buněk před aplikací pravidla. |

**Tip:** Když generujete sešit programově pro mnoho uživatelů, udržujte definici podmíněného formátování oddělenou od vkládání dat. Tím můžete znovu použít stejný styl napříč více listy bez duplicitního kódu.

## Ověření výsledku programově (volitelné)

Pokud chcete potvrdit formátování bez otevření Excelu, můžete po uložení zkontrolovat styl buňky:



## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Excel Automation&#58; Vytvoření sešitu a přidání ListBoxu pomocí Aspose.Cells pro .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Vytvoření sešitu Excel a přidání popisků pomocí Aspose.Cells pro Java](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Excel Automation: Vytvoření sešitu a přidání ListBoxu pomocí Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}