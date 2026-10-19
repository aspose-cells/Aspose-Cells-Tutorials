---
category: general
date: 2026-08-24
description: Maak een voorwaardelijke opmaakregel in Python met Aspose.Cells om datums
  te markeren, met automatisch aanpassen van de kolom en achtergrondkleuropmaak.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting rule
- auto fit column
- conditional formatting by date
- background color conditional format
- date based conditional format
language: nl
lastmod: 2026-08-24
og_description: Maak een voorwaardelijke opmaakregel in Python met Aspose.Cells. Leer
  hoe je datums markeert, achtergrondkleuren instelt en kolommen automatisch aanpast
  in slechts een paar regels code.
og_image_alt: Screenshot of an Excel sheet where yesterday's date cells are highlighted
  in pink
og_title: Maak een voorwaardelijke opmaakregel voor datums in Python – stapsgewijze
  handleiding
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
title: Hoe maak je een voorwaardelijke opmaakregel voor datums in Python
url: /nl/python/formatting/how-to-create-conditional-formatting-rule-for-dates-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe maak je een voorwaardelijke opmaakregel voor datums in Python

Als je een **create conditional formatting rule** wilt maken die reageert op datums, laat deze gids je precies zien hoe je dit doet met Aspose.Cells voor Python. Of je nu een rapportagedashboard of een geautomatiseerde spreadsheet bouwt, je ziet hoe je de datums van gisteren kunt markeren, een aangepaste achtergrondkleur kunt toepassen, en **auto fit column** breedtes kunt aanpassen zodat het resultaat er gepolijst uitziet.

In deze tutorial behandelen we **conditional formatting by date**, demonstreren we een **background color conditional format**, en sluiten we af met het opslaan van de werkmap als een XLSX‑bestand. Aan het einde heb je een herbruikbare helper die je kunt aanpassen aan elke **date based conditional format** die je nodig hebt.

## Wat je zult leren

* Een werkmap en werkblad instellen met Aspose.Cells.
* Een helper‑functie schrijven die een **date based conditional format** toevoegt aan elk celbereik.
* Cellen vullen met voorbeelddatums zodat de regel kan worden geëvalueerd.
* **auto fit column** toepassen om de inhoud leesbaar te maken.
* De werkmap opslaan en de gemarkeerde cellen verifiëren.

De enige vereiste is een werkende Python‑omgeving met het `aspose-cells`‑pakket geïnstalleerd.

## Vereisten

| Vereiste | Details |
|----------|---------|
| Python | 3.8+ |
| Aspose.Cells for Python via Java | `pip install aspose-cells` |
| Basiskennis van Excel‑concepten | worksheets, cells, formatting |
| Optioneel: IDE (VS Code, PyCharm, etc.) | any editor that can run Python scripts |

## Stap 1: Maak een werkmap en haal het eerste werkblad op

De eerste stap is om **create conditional formatting rule**‑gereed objecten te maken: een `Workbook` en het standaard `Worksheet`. Deze objecten vormen het toegangspunt voor alle volgende bewerkingen.

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

*Waarom dit belangrijk is:* De `Workbook` bevat het volledige Excel‑bestand, terwijl het `Worksheet` de plaats is waar je cellen, stijlen en **conditional formatting by date** toepast. Zonder deze objecten heeft de rest van de code nergens om te werken.

## Stap 2: Bouw een helper om een TIME_PERIOD voorwaardelijke opmaak toe te voegen

In plaats van dezelfde boiler‑plate voor elk bereik te herhalen, kapselen we de logica in een helper‑functie. Deze functie voegt een **background color conditional format** toe die cellen kleurt op basis van een `TimePeriodType` (bijv. Yesterday, Today, LastWeek).

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

*Waarom we een helper gebruiken:* Het isoleert de **date based conditional format**‑logica, waardoor de code makkelijker leesbaar, testbaar en herbruikbaar is over meerdere bladen of projecten.

## Stap 3: Pas de voorwaardelijke opmaakregel toe op een specifiek bereik

Nu gebruiken we de helper om cellen die “Yesterday” bevatten te markeren. Dit is de kern van onze **create conditional formatting rule**‑operatie.

```python
# Step 3 – highlight cells I19:K20 that contain “Yesterday”
add_time_period_condition(
    cell_range="I19:K20",
    bg_color=Color.medium_sea_green,   # optional default background for the whole range
    period=TimePeriodType.YESTERDAY   # the date‑based trigger
)
```

Wanneer de werkmap wordt geopend, zal elke cel in `I19:K20` waarvan de datum gelijk is aan de datum van gisteren, verschijnen met een roze vulling (de stijl die we in de helper hebben ingesteld). Het `bg_color`‑argument laat zien hoe je een standaard achtergrond kunt plaatsen achter de voorwaardelijke kleur indien gewenst.

## Stap 4: Vul het bereik met voorbeelddatums

Een voorwaardelijke regel wordt pas zichtbaar nadat het werkblad gegevens bevat die aan de voorwaarde voldoen. We voegen twee datums in: één die overeenkomt met “Yesterday” en een andere die buiten de periode valt.

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

*Waarom dit belangrijk is:* Door `datetime`‑objecten te gebruiken, zorgen we ervoor dat Excel de waarden als echte datums behandelt, wat vereist is zodat **conditional formatting by date** correct werkt. Het numerieke formaat (`30`) garandeert dat de cellen worden weergegeven als herkenbare datums.

## Stap 5: Auto‑fit de kolom en sla de werkmap op

Nadat de gegevens en opmaak op hun plaats staan, is de laatste afwerking om **auto fit column** breedtes aan te passen zodat de datums volledig zichtbaar zijn. Vervolgens schrijven we het bestand naar schijf.

```python
# Step 5 – adjust column width and save the file

# Auto‑fit column 12 (the column that contains our sample data)
worksheet.auto_fit_column(12)

# Save the workbook as an XLSX file
output_path = "YOUR_DIRECTORY/TimePeriodDemo.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

De `auto_fit_column`‑aanroep onderzoekt de langste inhoud in kolom 12 (die overeenkomt met kolom **L** in Excel) en vergroot de breedte dienovereenkomstig. Deze kleine stap voorkomt afgekorte datums en maakt de **background color conditional format** duidelijk zichtbaar.

### Verwacht resultaat

Wanneer je `TimePeriodDemo.out.xlsx` opent:

| I19 (datum) | I20 (label) | K20 (datum) |
|------------|------------|------------|
| 30‑Jul‑2008 (gemarkeerd roze) | Gisteren | 03‑Aug‑2008 (geen markering) |

* De cel met de datum van gisteren toont een roze achtergrond omdat de **create conditional formatting rule** overeenkwam met de `YESTERDAY`‑periode.
* Alle andere cellen behouden de standaard achtergrond (of de optionele `medium_sea_green` die je hebt opgegeven).
* Kolom L wordt automatisch verbreed, zodat de datums volledig leesbaar zijn.

## Veelvoorkomende variaties en randgevallen

| Situatie | Hoe de code aan te passen |
|----------|---------------------------|
| **Markeer “Today” in plaats van “Yesterday”** | Vervang `TimePeriodType.YESTERDAY` door `TimePeriodType.TODAY`. |
| **Gebruik een andere achtergrondkleur** | Verander `condition.style.background_color = Color.pink` naar een andere `Color` (bijv. `Color.light_sky_blue`). |
| **Pas de regel toe op een niet‑aaneengesloten bereik** | Roep `add_time_period_condition` meerdere keren aan met verschillende `cell_range`‑strings (bijv. `"A1:A10", "C1:C10"`). |
| **Werken met een reeds bestaande werkmap** | Laad het bestand met `Workbook("myfile.xlsx")` in plaats van een nieuwe te maken. |
| **Meerdere datum‑gebaseerde voorwaarden op hetzelfde bereik** | Na de eerste `add_time_period_condition`‑aanroep, voeg een andere voorwaarde toe met `conditions.add_condition(FormatConditionType.TIME_PERIOD)` en stel een andere `time_period` in. |

## Conclusie

Je weet nu hoe je een **create conditional formatting rule** maakt die reageert op datums, een **background color conditional format** toepast, en **auto fit column** breedtes gebruikt met Aspose.Cells voor Python. De helper‑functie abstraheert de logica, zodat je hetzelfde patroon kunt hergebruiken voor elke **conditional formatting by date**‑situatie—of het nu “Yesterday”, “LastWeek” of een aangepast bereik is.

Vervolgens kun je verkennen:

* Het toevoegen van **icon sets** of **data bars** naast datumregels.
* Dynamische rapporten genereren die datums uit een database halen.
* Meerdere **date based conditional format**‑regels combineren op één blad.

Voel je vrij om te experimenteren met verschillende kleuren, periodes en bereiken om aan de behoeften van je project te voldoen. Veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Master Conditional Formatting in Excel Using Aspose.Cells .NET: A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [How to Extract Conditional Formatting Colors Using Aspose.Cells for .NET](/cells/english/net/formatting/extract-conditional-formatting-colors-aspose-cells-net/)
- [Master Conditional Formatting with Custom Fonts in Excel using Aspose.Cells for .NET and C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}