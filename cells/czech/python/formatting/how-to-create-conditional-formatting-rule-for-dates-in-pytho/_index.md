---
category: general
date: 2026-08-24
description: Vytvořte pravidlo podmíněného formátování v Pythonu pomocí Aspose.Cells
  pro zvýraznění datumů, s automatickým přizpůsobením sloupce a formátováním barvy
  pozadí.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting rule
- auto fit column
- conditional formatting by date
- background color conditional format
- date based conditional format
language: cs
lastmod: 2026-08-24
og_description: Vytvořte pravidlo podmíněného formátování v Pythonu s Aspose.Cells.
  Naučte se, jak zvýraznit data, nastavit barvy pozadí a automaticky přizpůsobit šířku
  sloupců pomocí několika řádků kódu.
og_image_alt: Screenshot of an Excel sheet where yesterday's date cells are highlighted
  in pink
og_title: Vytvořte pravidlo podmíněného formátování pro data v Pythonu – průvodce
  krok za krokem
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
title: Jak vytvořit pravidlo podmíněného formátování pro data v Pythonu
url: /cs/python/formatting/how-to-create-conditional-formatting-rule-for-dates-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit pravidlo podmíněného formátování pro data v Pythonu

Pokud potřebujete **vytvořit pravidlo podmíněného formátování**, které reaguje na data, tento průvodce vám přesně ukáže, jak to provést pomocí Aspose.Cells pro Python. Ať už vytváříte reportingový dashboard nebo automatizovaný tabulkový list, uvidíte, jak zvýraznit včerejší data, použít vlastní barvu pozadí a **automaticky přizpůsobit šířku sloupce**, aby výsledek vypadal profesionálně.

V tomto tutoriálu se podíváme na **podmíněné formátování podle data**, ukážeme **podmíněný formát s barvou pozadí** a zakončíme uložením sešitu jako souboru XLSX. Na konci budete mít znovupoužitelnou pomocnou funkci, kterou můžete přizpůsobit libovolnému **podmíněnému formátu založenému na datu**, který potřebujete.

## Co se naučíte

* Nastavit sešit a list pomocí Aspose.Cells.
* Napsat pomocnou funkci, která přidá **podmíněný formát založený na datu** do libovolného rozsahu buněk.
* Naplnit buňky ukázkovými daty, aby se pravidlo mohlo vyhodnotit.
* Použít **automatické přizpůsobení šířky sloupce**, aby byl obsah čitelný.
* Uložit sešit a ověřit zvýrazněné buňky.

Jedinou podmínkou je fungující prostředí Pythonu s nainstalovaným balíčkem `aspose-cells`.

## Požadavky

| Požadavek | Detaily |
|-------------|---------|
| Python | 3.8+ |
| Aspose.Cells for Python via Java | `pip install aspose-cells` |
| Basic knowledge of Excel concepts | worksheets, cells, formatting |
| Optional: IDE (VS Code, PyCharm, etc.) | any editor that can run Python scripts |

## Krok 1: Vytvořte sešit a získejte první list

Prvním krokem je připravit objekty **vytvořit pravidlo podmíněného formátování**: `Workbook` a jeho výchozí `Worksheet`. Tyto objekty jsou vstupním bodem pro všechny následné operace.

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

*Proč je to důležité:* `Workbook` obsahuje celý soubor Excel, zatímco `Worksheet` je místo, kde aplikujete buňky, styly a **podmíněné formátování podle data**. Bez těchto objektů nemá zbytek kódu kam působit.

## Krok 2: Vytvořte pomocnou funkci pro přidání podmíněného formátu TIME_PERIOD

Místo opakování stejného boiler‑plate pro každý rozsah zapouzdříme logiku v pomocné funkci. Tato funkce přidá **podmíněný formát s barvou pozadí**, který barví buňky na základě `TimePeriodType` (např. Yesterday, Today, LastWeek).

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

*Proč používáme pomocnou funkci:* Izoluje logiku **podmíněného formátu založeného na datu**, což usnadňuje čtení, testování a opětovné použití kódu napříč více listy nebo projekty.

## Krok 3: Použijte pravidlo podmíněného formátování na konkrétní rozsah

Nyní použijeme pomocnou funkci k zvýraznění buněk, které obsahují „Yesterday“. Toto je jádro naší operace **vytvořit pravidlo podmíněného formátování**.

```python
# Step 3 – highlight cells I19:K20 that contain “Yesterday”
add_time_period_condition(
    cell_range="I19:K20",
    bg_color=Color.medium_sea_green,   # optional default background for the whole range
    period=TimePeriodType.YESTERDAY   # the date‑based trigger
)
```

Když se sešit otevře, každá buňka v `I19:K20`, jejíž datum se rovná včerejšímu datu, se zobrazí s růžovým výplní (styl, který jsme nastavili v pomocné funkci). Argument `bg_color` ukazuje, jak můžete případně vrstvit výchozí pozadí za podmíněnou barvu.

## Krok 4: Naplňte rozsah ukázkovými daty

Podmíněné pravidlo se zobrazí až poté, co list obsahuje data, která podmínku splňují. Vložíme dva datumy: jeden, který odpovídá „Yesterday“, a druhý, který spadá mimo období.

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

*Proč je to důležité:* Používáním objektů `datetime` zajistíme, že Excel hodnoty interpretuje jako skutečná data, což je nutné pro správnou funkci **podmíněného formátování podle data**. Číselný formát (`30`) zaručuje, že buňky zobrazí rozpoznatelná data.

## Krok 5: Automaticky přizpůsobte šířku sloupce a uložte sešit

Po vložení dat a formátování je posledním vylepšením **automatické přizpůsobení šířky sloupce**, aby byla data plně viditelná. Poté soubor zapíšeme na disk.

```python
# Step 5 – adjust column width and save the file

# Auto‑fit column 12 (the column that contains our sample data)
worksheet.auto_fit_column(12)

# Save the workbook as an XLSX file
output_path = "YOUR_DIRECTORY/TimePeriodDemo.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

Volání `auto_fit_column` prozkoumá nejdelší obsah ve sloupci 12 (což odpovídá sloupci **L** v Excelu) a podle toho rozšíří šířku. Tento malý krok zabraňuje oříznutým datumům a zajišťuje, že **podmíněný formát s barvou pozadí** je jasně viditelný.

### Očekávaný výsledek

Když otevřete `TimePeriodDemo.out.xlsx`:

| I19 (datum) | I20 (popisek) | K20 (datum) |
|------------|------------|------------|
| 30‑Jul‑2008 (zvýrazněno růžově) | Yesterday | 03‑Aug‑2008 (bez zvýraznění) |

* Buňka s včerejším datem má růžové pozadí, protože **vytvořené pravidlo podmíněného formátování** odpovídalo období `YESTERDAY`.
* Všechny ostatní buňky si zachovají výchozí pozadí (nebo volitelný `medium_sea_green`, který jste zadali).
* Sloupec L je automaticky rozšířen, takže data jsou plně čitelná.

## Běžné varianty a okrajové případy

| Situace | Jak upravit kód |
|-----------|-----------------------|
| **Zvýraznit „Today“ místo „Yesterday“** | Replace `TimePeriodType.YESTERDAY` with `TimePeriodType.TODAY`. |
| **Použít jinou barvu pozadí** | Change `condition.style.background_color = Color.pink` to any other `Color` (e.g., `Color.light_sky_blue`). |
| **Použít pravidlo na nesouvislý rozsah** | Call `add_time_period_condition` multiple times with different `cell_range` strings (e.g., `"A1:A10", "C1:C10"`). |
| **Pracovat s již existujícím sešitem** | Load the file with `Workbook("myfile.xlsx")` instead of creating a new one. |
| **Více podmínek založených na datu ve stejném rozsahu** | After the first `add_time_period_condition` call, add another condition with `conditions.add_condition(FormatConditionType.TIME_PERIOD)` and set a different `time_period`. |

## Závěr

Nyní víte, jak **vytvořit pravidlo podmíněného formátování**, které reaguje na data, použít **podmíněný formát s barvou pozadí** a **automaticky přizpůsobit šířku sloupce** pomocí Aspose.Cells pro Python. Pomocná funkce abstrahuje logiku, což vám umožní znovu použít stejný vzor pro jakýkoli scénář **podmíněného formátování podle data** – ať už jde o „Yesterday“, „LastWeek“ nebo vlastní rozsah.

Další kroky, které můžete prozkoumat:

* Přidání **sady ikon** nebo **datových pruhů** vedle pravidel pro data.
* Generování dynamických reportů, které získávají data z databáze.
* Kombinování více **podmíněných formátů založených na datu** na jednom listu.

Neváhejte experimentovat s různými barvami, obdobími a rozsahy, aby vyhovovaly potřebám vašeho projektu. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Master Conditional Formatting in Excel Using Aspose.Cells .NET: A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [How to Extract Conditional Formatting Colors Using Aspose.Cells for .NET](/cells/english/net/formatting/extract-conditional-formatting-colors-aspose-cells-net/)
- [Master Conditional Formatting with Custom Fonts in Excel using Aspose.Cells for .NET and C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}