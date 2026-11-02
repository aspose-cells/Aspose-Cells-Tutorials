---
category: general
date: 2026-10-04
description: Vytvořte Excel sešit v Pythonu pomocí Aspose.Cells. Naučte se podmíněné
  formátování v Excelu v Pythonu, nastavení barvy pozadí buňky v Pythonu a formátování
  dat v buňkách v Pythonu v kompletním příkladu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: cs
lastmod: 2026-10-04
og_description: Vytvořte Excel sešit v Pythonu s Aspose.Cells. Tento tutoriál ukazuje
  podmíněné formátování v Excelu v Pythonu, barvu pozadí buňky v Pythonu a formátování
  data v buňkách v Pythonu krok za krokem.
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: Vytvořte Excel sešit v Pythonu – kompletní průvodce s podmíněným formátováním
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
title: Vytvořit Excel sešit v Pythonu s podmíněným formátováním a barvou pozadí buňky
url: /cs/python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořit Excel workbook python s podmíněným formátováním a barvou pozadí buňky

Pokud potřebujete rychle **create Excel workbook python**, tento průvodce vám přesně ukáže, jak na to. Uvidíte kompletní, spustitelný příklad, který přidává **excel conditional formatting python**, mění **cell background color python** a **format cells date python** pro zvýraznění „Yesterday“.

V mnoha scénářích reportování vizuální náznak barevné buňky umožňuje okamžitě pochopit data. Tento tutoriál vás provede každým řádkem kódu, vysvětlí, proč je každý krok důležitý, a poskytne vám připravený skript, který můžete přizpůsobit svým projektům.

## Co dosáhnete

1. **create Excel workbook python** pomocí knihovny Aspose.Cells.  
2. Použít **excel conditional formatting python**, který automaticky zvýrazní data spadající na „Yesterday“.  
3. Nastavit **cell background color python** na růžovou (nebo jakoukoli jinou barvu, kterou preferujete).  
4. **format cells date python**, aby se data zobrazovala ve standardním stylu data v Excelu.  

Žádná předchozí zkušenost s Aspose.Cells není vyžadována – stačí funkční prostředí Python 3 a přístup k pip.

## Požadavky

- Python 3.8 nebo novější nainstalovaný.  
- Balíčky `aspose-cells` a `aspose-pydrawing` nainstalované pomocí `pip install aspose-cells aspose-pydrawing`.  
- Základní znalost syntaxe Pythonu a konceptů Excelu (sešity, listy, buňky).  

> **Pro tip:** Pokud spustíte skript ve virtuálním prostředí, vyhnete se konfliktům verzí s ostatními projekty.

## Krok 1: Nastavení projektu a import potřebných tříd

Prvním krokem, když **create Excel workbook python**, je importovat třídy Aspose.Cells, které budete potřebovat. Tyto třídy vám poskytují přímý přístup k vytváření sešitu, podmíněnému formátování a stylování.

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

*Proč je to důležité:* Importování pouze potřebných symbolů udržuje jmenný prostor přehledný a usnadňuje čtení skriptu. `Workbook` je vstupní bod pro **create Excel workbook python**, zatímco `FormatConditionType` a `TimePeriodType` jsou nezbytné pro **excel conditional formatting python**.

## Krok 2: Vytvoření nového sešitu a získání první listu

Nyní skutečně **create Excel workbook python**. Konstruktor `Workbook()` vám poskytne prázdný Excel soubor s výchozím listem.

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Vysvětlení:* Každý Excel soubor začíná alespoň jedním listem. Ve výchozím nastavení ho Aspose.Cells pojmenuje „Sheet1“. Později můžete přidat další listy, ale pro tuto ukázku stačí jeden list, aby byl příklad soustředěný.

## Krok 3: Definování cílového rozsahu pro podmíněné formátování

Podmíněné formátování funguje na obdélníkovém rozsahu. Zde volíme rozsah `I19:K20`, který poskytuje tři sloupce a dva řádky k práci.

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*Proč to děláme:* Metoda `get` vrací objekt `ConditionalFormatting` svázaný se zadaným rozsahem. Pokud rozsah ještě nemá žádné formátování, Aspose.Cells automaticky vytvoří novou kolekci.

## Krok 4: Přidání podmínky TIME_PERIOD a nastavení barvy pozadí

Toto je jádro **excel conditional formatting python**. Přidáme pravidlo `TIME_PERIOD`, které zvýrazní buňky obsahující data spadající na „Yesterday“.

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

*Hlubší pohled:*  
- `FormatConditionType.TIME_PERIOD` říká Excelu, aby vyhodnocoval data relativně k aktuálnímu datu.  
- `TimePeriodType.YESTERDAY` je vestavěná výčtová hodnota, která se automaticky aktualizuje každý den, takže sešit vždy zvýrazní nejnovější „Yesterday“.  
- Nastavením `background_color` na `Color.pink` a vzoru na `SOLID` dosáhneme efektu **cell background color python** bez nutnosti dalšího VBA kódu.

## Krok 5: Naplnění rozsahu ukázkovými daty a aplikace formátování data

Aby podmíněné formátování fungovalo, potřebujeme skutečné datumové hodnoty. Také musíme **format cells date python**, aby Excel zacházel s nimi jako s daty, ne jako s čísly.

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

*Vysvětlení:*  
- Řádek `style.number = 30` představuje krok **format cells date python**. Kód formátu 30 odpovídá krátkému formátu data (`m/d/yy`).  
- Použití pomocné funkce udržuje kód DRY (Don’t Repeat Yourself) a usnadňuje přidání dalších dat později.

## Krok 6: Přidání popisného popisku

Malý popisek pomůže komukoli, kdo otevře sešit, pochopit, proč jsou buňky zbarvené.

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## Krok 7: Uložení sešitu na disk

Nakonec **create Excel workbook python** na disku voláním `save`. Konstantní `SaveFormat.XLSX` zajišťuje, že soubor bude ve formátu moderního Office Open XML.

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Když otevřete `TimePeriodDemo.xlsx` v Excelu, uvidíte:

- Buňky `I19` a `K20` obsahují data.  
- Buňka, která odpovídá „Yesterday“ (v tomto statickém příkladu `I19`), je zvýrazněna růžově.  
- Popisek „Yesterday“ se objeví v `I20`.  

> **Tip:** Pokud skript spustíte v jiný den, podmíněné formátování i nadále zvýrazní buňku, jejíž datum je přesně o jeden den starší než aktuální systémové datum – žádné změny kódu nejsou potřeba.

## Kompletní skript – připravený ke kopírování a spuštění

Níže je kompletní, samostatný program, který zahrnuje všechny výše uvedené kroky. Zkopírujte jej do souboru pojmenovaného `conditional_format_demo.py`, upravte `YOUR_DIRECTORY` a spusťte pomocí `python conditional_format_demo.py`.

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

### Očekávaný výstup

Spuštění skriptu vypíše potvrzovací řádek:

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Otevření vygenerovaného souboru ukazuje růžové pozadí v buňce, která odpovídá pravidlu „Yesterday“, což potvrzuje, že **excel conditional formatting python** a **cell background color python** spolupracují.

## Běžné varianty a okrajové případy

| Situace | Jak upravit kód |
|-----------|-----------------------|
| **Jiná barva zvýraznění** | Změňte `Color.pink` na libovolnou jinou konstantu `Color`, např. `Color.light_green`. |
| **Zvýraznit „Today“ místo „Yesterday“** | Nastavte `condition.time_period = TimePeriodType.TODAY`. |
| **Použít formátování na celý sloupec** | Použijte rozsah jako `"A:A"` a podle toho upravte proměnnou `target_range`. |
| **Použít vlastní formát data** | Nahraďte `style.number = 30` za `style.custom = "dd-mmm-yyyy"` pro čitelnější formát. |
| **Více podmínek ve stejném rozsahu** |  |

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}