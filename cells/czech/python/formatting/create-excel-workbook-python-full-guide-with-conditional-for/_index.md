---
category: general
date: 2026-07-14
description: Vytvořte Python kód pro Excel sešit, který nastaví barvu pozadí buňky,
  zvýrazní buňky podle časového rozmezí a během několika minut uloží sešit jako XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- save workbook as xlsx
- highlight cells based on date range
- conditional formatting based on date
language: cs
lastmod: 2026-07-14
og_description: Okamžitě vytvořte Excel sešit v Pythonu. Naučte se nastavit barvu
  pozadí buňky, zvýraznit buňky podle časového rozmezí a uložit sešit jako XLSX pomocí
  Aspose.Cells.
og_image_alt: Screenshot showing an Excel sheet created with Python highlighting yesterday's
  dates
og_title: Vytvořte Excel sešit v Pythonu – Krok za krokem podmíněné formátování
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
title: Vytvoření Excel sešitu v Pythonu – Kompletní průvodce s podmíněným formátováním
url: /cs/python/formatting/create-excel-workbook-python-full-guide-with-conditional-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření Excel sešitu v Pythonu – Kompletní průvodce s podmíněným formátováním

Už jste se někdy zamysleli, jak **create excel workbook python** skripty, které vypadají profesionálně, aniž byste museli ručně otevírat Excel? Nejste v tom sami. V mnoha projektech založených na datech potřebujeme generovat tabulky, barvit buňky a dokonce označovat data, která spadají do konkrétního rozsahu – vše z čistého Python kódu.

V tomto tutoriálu projdeme kompletním, připraveným k běhu příkladem, který **creates an Excel workbook python** pomocí knihovny Aspose.Cells, **sets cell background color**, použije **conditional formatting based on date** a nakonec **saves workbook as xlsx**. Na konci budete mít znovupoužitelný úryvek, který můžete vložit do jakéhokoli automatizačního pipeline.

## Co se naučíte

- Jak inicializovat sešit a získat první list.  
- Pomocná funkce, která přidá kolekci podmíněného formátování pro libovolný rozsah buněk.  
- Použití **conditional formatting based on date** k zvýraznění včerejších záznamů.  
- Úprava šířky sloupců pro úhledné rozvržení.  
- Uložení výsledku pomocí **save workbook as xlsx**.  

Není vyžadována žádná externí instalace Excelu – Aspose.Cells vše zpracuje v paměti.

## Požadavky

- Python 3.8+ nainstalován.  
- `aspose-cells` balíček (`pip install aspose-cells`).  
- Základní znalost Python funkcí a objektů datetime.  

Pokud jste ještě nikdy nepoužili Aspose.Cells, představte si jej jako výkonné, čistě Python API, které napodobuje objektový model Excelu. Je ideální pro generování na serveru, kde není k dispozici balík Office.

## Krok 1: Inicializace sešitu (Create Excel Workbook Python)

Nejprve potřebujeme **create excel workbook python** styl. Tento krok vytvoří prázdný objekt sešitu a nasměruje nás na výchozí list.

```python
# Step 1 – create a fresh workbook and get the first sheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, Color, SaveFormat
from datetime import datetime

workbook = Workbook()                     # <-- creates a new Excel file in memory
worksheet = workbook.worksheets[0]        # the default (first) sheet
```

> **Proč je to důležité:** Třída `Workbook` je vstupním bodem pro každou operaci s Excelem. Vytvořením programově se vyhneme jakémukoli ručnímu zpracování souborů.

## Krok 2: Pomocná funkce pro přidání kolekce podmíněného formátování (Set Cell Background Color)

Podmíněné formátování žije uvnitř *kolekce* připojené k rozsahu. Zabalme tento boilerplate do malé pomocné funkce, která nám také umožní **set cell background color** pro celý rozsah.

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

> **Tip:** Použití pomocné funkce udržuje hlavní tok čistý a usnadňuje opakované použití stejné logiky pro více rozsahů.

## Krok 3: Použití podmíněného formátování na základě data (Highlight Cells Based on Date Range)

Nyní skutečně **highlight cells based on date range**. Příklad se zaměřuje na „včerejší“ den, ale můžete vyměnit `TimePeriodType.YESTERDAY` za `TODAY`, `LAST_WEEK` atd.

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

> **Co se děje?**  
> 1. Nejprve dáme celému rozsahu neutrální zelené pozadí.  
> 2. Pak přidáme podmínku `TIME_PERIOD`, která přepíše výplň na růžovou **pouze** když datum buňky odpovídá včerejšímu dni.  
> 3. Výčet `TimePeriodType` abstrahuje výpočet data, takže nemusíte psát vlastní logiku.

## Krok 4: Naplnění ukázkových dat (So the Rule Can Be Evaluated)

Abychom viděli pravidlo v akci, vložíme do listu několik dat. Jedno spadá do okna „včerejšího“ dne, druhé ne.

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

> **Poznámka k okrajovým případům:** Pokud bude váš sešit otevírán v různých locale, zvažte použití `date_style.custom = "dd‑mm‑yyyy"` pro vynucení jednotného zobrazení.

## Krok 5: Úprava rozvržení (Auto‑Fit Columns)

Stísněná tabulka vypadá neprofesionálně. Pojďme **adjust column width for a tidy output**.

```python
# Auto‑fit column L (index 12) to show the full content without truncation
worksheet.auto_fit_column(12)
```

> **Proč auto‑fit?** Zajišťuje, že jakékoli dlouhé popisky nebo data jsou plně viditelné, což je zvláště důležité při sdílení souboru s netechnickými zainteresovanými stranami.

## Krok 6: Uložení sešitu (Save Workbook As XLSX)

Nakonec **save workbook as xlsx** na vámi zvolené místo. Konstantní `SaveFormat.XLSX` říká Aspose.Cells, aby zapsal moderní formát OpenXML.

```python
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Výsledek, který byste měli vidět:**  
> - Buňky I19 a K20 obsahují data.  
> - I19 (včera) je zvýrazněna růžově, zatímco K20 zůstává zelená.  
> - Sloupec L se automaticky rozšíří, aby pojmul popisek „Yesterday“.  

Pokud otevřete `TimePeriodDemo.xlsx` v Excelu, podmíněné formátování bude již aplikováno – není potřeba žádné další kroky.

![Excel list zobrazující zvýrazněné datum včerejška](https://example.com/images/excel-demo.png "Snímek obrazovky vygenerovaného Excel souboru se zvýrazněnými buňkami")

*Obrázek výše ilustruje finální sešit; všimněte si růžového zvýraznění buňky obsahující včerejší datum.*

## Shrnutí: Co jsme dosáhli

- **Created an Excel workbook python** od začátku pomocí Aspose.Cells.  
- **Set cell background color** pro celý rozsah, aby list získal vizuální vodítko.  
- Aplikováno **conditional formatting based on date** pro automatické označení včerejších záznamů.  
- **Saved workbook as xlsx**, připravený k distribuci nebo dalšímu zpracování.  

Vše bylo provedeno v méně než 60 řádcích Pythonu a kód funguje na jakékoli platformě, která podporuje runtime Aspose.Cells.

## Další kroky a související témata

Pokud se vám to hodilo, můžete také prozkoumat:

- **set cell background color** pro celé řádky na základě hodnot statusu (např. „Completed“, „Pending“).  
- Použití **highlight cells based on date range** k vytvoření posuvných oken (posledních 7 dní, aktuální měsíc).  
- Export do dalších formátů jako **CSV** nebo **PDF** s `SaveFormat.CSV` nebo `SaveFormat.PDF`.  
- Přidání **charts** programově pro vizualizaci dat, která jste právě naformátovali.  

Neváhejte upravit logiku data, změnit barevnou paletu nebo rozšířit rozsah tak, aby pokrýval celé sloupce. Vzor zůstává stejný: vytvořit sešit, připojit kolekci podmíněného formátování, definovat pravidlo a uložit.

Máte otázky ohledně konkrétního případu použití? Zanechte komentář níže a šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Automatizace Excelu s Aspose.Cells .NET: Vytvoření sešitu a nastavení externích odkazů](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Vytvoření a uložení Excel sešitu Aspose Cells Java](/cells/hongkong/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Vytvoření a uložení Excel sešitu Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}