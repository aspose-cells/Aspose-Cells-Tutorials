---
category: general
date: 2026-10-07
description: Vytvořte Excel sešit v Pythonu, nastavte barvu pozadí buňky, automaticky
  přizpůsobte šířku sloupců a vyplňte datumy v Excelu pomocí stručného příkladu kódu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: cs
lastmod: 2026-10-07
og_description: Vytvořte Excel sešit v Pythonu, poté nastavte barvu pozadí buňky,
  automaticky přizpůsobte sloupce a vyplňte data v Excelu. Postupujte podle tohoto
  krok‑za‑krokem návodu a vytvořte soubor TimePeriodDemo.xlsx.
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: Vytvořte Excel sešit v Pythonu – nastavte pozadí a automatické přizpůsobení
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  headline: Create Excel workbook in Python and set cell background
  type: TechArticle
- description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  name: Create Excel workbook in Python and set cell background
  steps:
  - name: Import required namespaces and define a helper function
    text: '```python # Step 1: Import Aspose.Cells classes and supporting modules
      from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType,
      SaveFormat from aspose.pydrawing import Color from datetime import datetime
      import os ```'
  - name: Create the workbook and get the first worksheet
    text: '```python def create_workbook(): # Step 2: Instantiate a new workbook (empty
      Excel file) book = Workbook() # Aspose.Cells creates a default worksheet; we
      retrieve it for further work sheet = book.worksheets[0] return book, sheet ```'
  - name: Set cell background color with a conditional format
    text: '```python def add_yesterday_rule(sheet): # Define a conditional format
      for the range I19:K20 (Yesterday) conds = sheet.get_range("I19:K20").format_conditions
      idx = conds.add_condition(FormatConditionType.TIME_PERIOD) cond = conds[idx]'
  - name: Populate dates in Excel
    text: '```python def populate_sample_dates(sheet): # Insert a date that falls
      on yesterday relative to the demo data cell = sheet.cells.get("I19") cell.put_value(datetime(2008,
      7, 30)) # sample date cell.style.number = 30 # Excel’s date format ID cell.set_style(cell.style)'
  - name: Auto‑fit Excel columns for better visibility
    text: '```python def auto_fit_columns(sheet): # Auto‑fit column L (index 12) so
      the content is fully visible sheet.auto_fit_column(12) # <-- auto fit excel
      columns ```'
  - name: Save the workbook
    text: '```python def save_workbook(book, filename="TimePeriodDemo.xlsx"): out_path
      = os.path.join("YOUR_DIRECTORY", filename) os.makedirs(os.path.dirname(out_path),
      exist_ok=True) book.save(out_path, SaveFormat.XLSX) print(f"Workbook saved to:
      {out_path}") ```'
  - name: Full script – putting it all together
    text: '```python def main(): # Create workbook and obtain the first worksheet
      book, sheet = create_workbook()'
  type: HowTo
tags:
- Excel
- Python
- Aspose.Cells
title: Vytvořte Excel sešit v Pythonu a nastavte pozadí buňky
url: /cs/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření Excel sešitu v Pythonu a nastavení pozadí buňky

Vytvořte Excel sešit v Pythonu a aplikujte podmíněné formátování pomocí jen několika řádků kódu. Tento tutoriál vám ukáže **jak vytvořit excel** soubory programově, nastavit barvu pozadí buňky, automaticky přizpůsobit šířku sloupců v Excelu a naplnit data v Excelu pomocí knihovny Aspose.Cells.

Dozvíte se, jak:
* Inicializovat sešit a získat první list.  
* Definovat podmíněný formát, který zvýrazní data „Včera“.  
* Vložit ukázková data do konkrétních buněk.  
* Automaticky přizpůsobit sloupce, aby byla data dobře viditelná.  
* Uložit sešit do zvoleného adresáře.

Jedinou podmínkou je fungující prostředí Python 3 s nainstalovanými balíčky `aspose-cells` a `aspose-pydrawing`:

```bash
pip install aspose-cells aspose-pydrawing
```

---

## Vytvoření Excel sešitu v Pythonu – krok za krokem

Následující sekce rozdělují proces na zvládnutelné kroky. Každý krok obsahuje požadovaný kód, vysvětlení **proč** je důležitý, a tip, jak se vyhnout běžným úskalím.

### Krok 1: Import požadovaných jmenných prostorů a definice pomocné funkce

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*Proč je to důležité*: Import správných tříd vám poskytuje přístup k tvorbě sešitu, podmíněnému formátování a manipulaci s barvami.  
**Pro tip**: Udržujte importy na začátku souboru; usnadní to čitelnost skriptu a zabrání chybám typu circular‑import.

### Krok 2: Vytvoření sešitu a získání prvního listu

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

Konstruktor `Workbook()` vytvoří prázdný Excel sešit v paměti.  
**Proč**: Začátek s čistým sešitem zajišťuje, že nebudou přítomny žádné zbylé formátování z předchozích běhů.

### Krok 3: Nastavení barvy pozadí buňky pomocí podmíněného formátu

```python
def add_yesterday_rule(sheet):
    # Define a conditional format for the range I19:K20 (Yesterday)
    conds = sheet.get_range("I19:K20").format_conditions
    idx = conds.add_condition(FormatConditionType.TIME_PERIOD)
    cond = conds[idx]

    # Apply visual style – this is where we set the cell background color
    cond.style.background_color = Color.pink          # <-- set cell background color
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

*Proč*: Použití podmínky **time period** automaticky zvýrazní každou buňku, která obsahuje datum včerejška, čímž eliminuje ruční kontrolu dat.  
**Tip**: `Color.pink` je jen příklad; můžete použít libovolný objekt `Color` (`Color.yellow`, `Color.light_green` atd.).

### Krok 4: Naplnění dat v Excelu

```python
def populate_sample_dates(sheet):
    # Insert a date that falls on yesterday relative to the demo data
    cell = sheet.cells.get("I19")
    cell.put_value(datetime(2008, 7, 30))   # sample date
    cell.style.number = 30                 # Excel’s date format ID
    cell.set_style(cell.style)

    # Insert another date outside the “Yesterday” range
    cell = sheet.cells.get("K20")
    cell.put_value(datetime(2008, 8, 3))
    cell.style.number = 30
    cell.set_style(cell.style)

    # Add a label for the rule
    sheet.cells.get("I20").put_value("Yesterday")
```

Zde **naplňujeme data v Excelu** v buňkách `I19` a `K20`. První datum spustí podmíněné formátování, zatímco druhé ne.  
**Proč je to důležité**: Ukázka jak shodných, tak neshodných hodnot vám pomůže ověřit, že pravidlo funguje podle očekávání.

### Krok 5: Automatické přizpůsobení šířky sloupců v Excelu pro lepší čitelnost

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

`auto_fit_column` upravuje šířku sloupce podle nejdelší hodnoty buňky.  
**Tip**: Zavolejte tuto metodu po zápisu všech dat; jinak může být šířka vypočtena na základě neúplného obsahu.

### Krok 6: Uložení sešitu

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

Uložení souboru zapíše sešit z paměti na disk ve moderním formátu XLSX.

### Úplný skript – spojení všeho dohromady

```python
def main():
    # Create workbook and obtain the first worksheet
    book, sheet = create_workbook()

    # Apply conditional formatting (set cell background color)
    add_yesterday_rule(sheet)

    # Populate the demo dates (populate dates in excel)
    populate_sample_dates(sheet)

    # Auto‑fit the relevant column (auto fit excel columns)
    auto_fit_columns(sheet)

    # Persist the file
    save_workbook(book)

if __name__ == "__main__":
    main()
```

**Očekávaný výstup**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Otevřete vygenerovaný soubor v Excelu – buňky `I19:K20` zobrazí růžové pozadí pro datum, které spadá do „Včerejška“, a sloupec L bude dostatečně široký, aby zobrazil popisek bez oříznutí.

---

## Proč tento přístup funguje nejlépe

* **Single‑pass workflow** – Všechny operace probíhají na stejném objektu `Workbook`, čímž se vyhýbá zbytečnému I/O.  
* **Conditional formatting** – Použití `FormatConditionType.TIME_PERIOD` nechává Excel řešit logiku dat, což je spolehlivější než psaní vlastních kontrol v Pythonu.  
* **Explicit styling** – Nastavení `background_color` a `pattern` zaručuje vizuální výsledek napříč verzemi Excelu.  
* **Auto‑fit after data**

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními krok za krokem, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Vytvoření Excel sešitu v Pythonu – Kompletní průvodce](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Vytvoření Excel sešitu v Pythonu – Kompletní krok‑za‑krokem průvodce](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Vytvoření Excel sešitu v Pythonu – Kompletní průvodce s Lambdou](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}