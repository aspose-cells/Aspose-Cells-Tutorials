---
category: general
date: 2026-07-06
description: Maak een Excel-werkboek in Python met code om de achtergrondkleur van
  een cel in te stellen, de celstijl programmatisch in te stellen en voorwaardelijke
  opmaak toe te voegen in Python om de datum van vandaag te markeren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- set cell style programmatically
- highlight today date excel
- add conditional formatting python
language: nl
lastmod: 2026-07-06
og_description: Maak direct een Excel-werkmap met Python. Leer hoe je de achtergrondkleur
  van een cel instelt, de celstijl programmeermatig aanpast en voorwaardelijke opmaak
  in Python toevoegt om de datum van vandaag te markeren.
og_image_alt: Screenshot of an Excel workbook created with Python showing colored
  cells and today’s date highlighted
og_title: Excel-werkboek maken met Python – Cellen opmaken & Vandaag markeren
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  headline: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  type: TechArticle
- description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  name: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  steps:
  - name: Converting a range like `"A1:C3"` into a `CellArea`.
    text: Converting a range like `"A1:C3"` into a `CellArea`.
  - name: Filling every cell in that area with a sequential number (just for demo
      purposes).
    text: Filling every cell in that area with a sequential number (just for demo
      purposes).
  - name: Applying a solid **set cell background color**.
    text: Applying a solid **set cell background color**.
  - name: Adding a conditional rule that **highlight today date excel**.
    text: Adding a conditional rule that **highlight today date excel**.
  type: HowTo
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Excel-werkmap maken met Python – Volledige gids voor styling en voorwaardelijke
  opmaak
url: /nl/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-werkboek maken met Python – Volledige gids voor styling & voorwaardelijke opmaak

Heb je je ooit afgevraagd hoe je **Excel-werkboek met Python** vanaf nul kunt maken zonder Excel zelf te openen? Je bent niet de enige. Veel ontwikkelaars moeten rapporten, dashboards of zelfs eenvoudige gegevenslogboeken on‑the‑fly genereren, en dit programmatisch doen bespaart uren handmatig werk.

In deze tutorial lopen we het volledige proces door: van het aanmaken van een gloednieuw werkboek, tot **set cell background color**, tot **set cell style programmatically**, en uiteindelijk **highlight today date excel** met **add conditional formatting python**. Aan het einde heb je een kant‑klaar script dat in enkele seconden een gepolijst .xlsx‑bestand produceert.

---

## Wat je gaat bouwen

- Een nieuw Excel‑bestand met een paar ingevulde cellen.
- Cellen gekleurd met een aangepaste achtergrond.
- Numerieke en datumwaarden opgemaakt met een specifieke getalstijl.
- Een voorwaardelijke regel die automatisch de cel met de datum van vandaag markeert.

Er is geen externe Excel‑installatie vereist—Aspose.Cells voor Python via .NET doet al het zware werk.

---

## Vereisten

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| Python 3.8+ | Moderne syntaxis en type‑hints |
| `aspose-cells` package | Kernbibliotheek voor werkboekmanipulatie |
| `aspose-pydrawing` (geïnstalleerd met Aspose.Cells) | Biedt de `Color`‑klasse |
| Basiskennis van Excel‑concepten (cellen, bereiken, opmaak) | Zorgt voor een soepelere tutorial |

Installeer de bibliotheek met:

```bash
pip install aspose-cells
```

---

## Stap 1: Werkboek en werkblad initialiseren

Het eerste wat je doet wanneer je **create excel workbook python** is een `Workbook`‑object instantieren en het standaard werkblad ophalen. Beschouw het werkboek als het volledige Excel‑bestand, terwijl het werkblad een enkele tabblad daarin is.

```python
from aspose.cells import Workbook

# Create a new workbook – this is our empty Excel file
book = Workbook()

# Grab the first (default) worksheet
sheet = book.worksheets[0]
```

> **Pro tip:** Als je meerdere bladen nodig hebt, gebruik dan `book.worksheets.add("MySheet")` om extra tabbladen toe te voegen.

---

## Stap 2: Helper‑klasse voor styling & voorwaardelijke opmaak

Hieronder staat een compacte maar volledige `ConditionalFormatting`‑klasse. Deze omvat de repetitieve taken van:

1. Een bereik zoals "A1:C3" omzetten naar een `CellArea`.
2. Elke cel in dat gebied vullen met een opeenvolgend getal (alleen voor demonstratiedoeleinden).
3. Een solide **set cell background color** toepassen.
4. Een voorwaardelijke regel toevoegen die **highlight today date excel**.

```python
from aspose.cells import (
    CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """
    Utility class that demonstrates how to:
    • set cell background color
    • set cell style programmatically
    • add conditional formatting python
    """
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        """
        Creates a conditional formatting object for the given range
        and fills the range with a background color.
        """
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]

        # Convert "A1:C3" → CellArea object
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)

        # Paint the whole area with the supplied color
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        """
        Populates each cell in the range with an incrementing integer
        and applies the supplied background color.
        """
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)

                # Apply background only if a real color is supplied
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)

                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name: str) -> CellArea:
        """
        Parses an Excel‑style address (e.g. "B2:D4") into a CellArea.
        """
        area = CellArea()
        parts = name.replace("$", "").split(':')

        start_row, start_col = CellsHelper.cell_name_to_index(parts[0])
        area.start_row = start_row
        area.start_column = start_col

        if len(parts) == 2:
            end_row, end_col = CellsHelper.cell_name_to_index(parts[1])
            area.end_row = end_row
            area.end_column = end_col
        else:
            area.end_row = start_row
            area.end_column = start_col
        return area

    # -----------------------------------------------------------------
    # Step 2: Add conditional formatting for TODAY
    # -----------------------------------------------------------------
    def add_time_period_1(self):
        """
        Demonstrates add conditional formatting python that highlights
        cells containing today’s date.
        """
        # 1️⃣ Create a formatting range and give it a neutral background
        cf = self.get_format_condition("I1:K2", Color.light_slate_gray)

        # 2️⃣ Add a TIME_PERIOD condition (Today)
        idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
        cond = cf[idx]
        cond.time_period = TimePeriodType.TODAY
        cond.style.background_color = Color.pink
        cond.style.pattern = BackgroundType.SOLID

        # 3️⃣ Populate the cells with date values
        # Cell I1 – today’s date, formatted as a date
        cell = self._sheet.cells.get("I1")
        style = cell.get_style()
        style.number = 30               # 30 = “mm-dd-yy” style in Aspose
        cell.set_style(style)
        cell.put_value(datetime.today())

        # Cell K2 – an arbitrary past date for contrast
        self._sheet.cells.get("K2").put_value(datetime(2008, 7, 30))

        # Cell I2 – a label so the reader knows what’s being highlighted
        self._sheet.cells.get("I2").put_value("Today")
```

### Waarom een helper‑klasse?

- **Herbruikbaarheid:** Je kunt `add_time_period_1()` aanroepen voor elk werkblad zonder de logica opnieuw te schrijven.
- **Duidelijkheid:** Elke methode doet één ding – een kenmerk van schone code.
- **Uitbreidbaarheid:** Wil je meer regels toevoegen? Voeg gewoon een andere methode toe volgens hetzelfde patroon.

---

## Stap 3: De opmaak toepassen en het bestand opslaan

Nu verbinden we alles: de helper instantieren, de opmaakroutine uitvoeren, en tenslotte het werkboek naar schijf schrijven.

```python
# Instantiate the helper with our worksheet
formatter = ConditionalFormatting(sheet)

# Fill a demo range with numbers and a light blue background
formatter.get_format_condition("A1:C3", Color.light_sky_blue)

# Add the “today” conditional rule
formatter.add_time_period_1()

# Save the workbook – choose any location you like
output_path = "styled_workbook.xlsx"
book.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

Wanneer je *styled_workbook.xlsx* opent, zou je moeten zien:

- Cellen **A1:C3** genummerd 0‑8 met een licht‑hemelsblauwe vulling.
- Cel **I1** toont de datum van vandaag met een roze achtergrond (dankzij de voorwaardelijke regel).
- Cel **K2** toont de statische datum *2008‑07‑30* ter vergelijking.
- Cel **I2** bevat de tekst “Today”.

Die visuele aanwijzing is precies wat de **highlight today date excel**‑vereiste vraagt.

---

## Stap 4: Dieper duiken – stijlen aanpassen

Als je lettertypen, randen of getalformaten wilt aanpassen, kun je de `fill_cell`‑methode uitbreiden of een nieuwe helper maken:

```python
def apply_custom_style(cell, font_name="Calibri", font_size=11, bold=False):
    style = cell.get_style()
    style.font.name = font_name
    style.font.size = font_size
    style.font.bold = bold
    cell.set_style(style)
```

Je zou vervolgens `apply_custom_style(cell, bold=True)` in de lus kunnen aanroepen om **set cell style programmatically** toe te passen op elke cel in een bereik.

---

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Symptoom | Waarschijnlijke oorzaak | Oplossing |
|----------|--------------------------|-----------|
| Cellbladen blijven wit ondanks `Color.light_sky_blue` | De stijl werd niet toegepast na het instellen van `foreground_color` | Roep altijd `cell.set_style(style)` aan na het wijzigen van het stijlobject. |
| Voorwaardelijke regel wordt nooit geactiveerd | `style.number` niet ingesteld voor datumcellen, waardoor Excel de waarde als een string behandelt | Stel `style.number = 30` (of een ander datumformaat) in vóór `cell.put_value(datetime…)`. |
| Werkboek wordt opgeslagen als .xls ondanks `SaveFormat.XLSX` | Oudere Aspose‑versie die standaard naar het legacy‑formaat gaat | Upgrade naar het nieuwste `aspose-cells`‑pakket. |
| Bereik zoals `"A1"` geeft een index‑fout | Gebruik van `cells.get("A1")` op een blad dat nog niet is geïnitialiseerd | Zorg ervoor dat het werkblad bestaat (het bestaat direct na `Workbook()`), of gebruik `cells.get(row, col)` met nul‑gebaseerde indexen. |

---

## Volledig script voor copy‑paste

Hieronder staat het **volledige** script dat je kunt plaatsen in een bestand genaamd `create_excel.py` en direct kunt uitvoeren.

```python
# create_excel.py
from aspose.cells import (
    Workbook, CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """Utility for styling cells and adding conditional formatting."""
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)
                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name:


## Wat je hierna moet leren

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Excel‑automatisering met Aspose.Cells .NET: Werkboek maken & externe koppelingen instellen](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Beheers Excel‑celopmaak en werkboekbeheer met Aspose.Cells voor .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel‑automatisering: Maak een werkboek en voeg een ListBox toe met Aspose.Cells voor .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}