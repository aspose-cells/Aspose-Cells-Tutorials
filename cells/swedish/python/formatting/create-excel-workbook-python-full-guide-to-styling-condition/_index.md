---
category: general
date: 2026-07-06
description: Skapa Excel-arbetsbok i Python med kod för att sätta cellbakgrundsfärg,
  sätta cellstil programatiskt och lägga till villkorsstyrd formatering i Python för
  att markera dagens datum.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- set cell style programmatically
- highlight today date excel
- add conditional formatting python
language: sv
lastmod: 2026-07-06
og_description: Skapa Excel-arbetsbok med Python direkt. Lär dig hur du sätter cellbakgrundsfärg,
  ställer in cellstil programatiskt och lägger till villkorsstyrd formatering i Python
  för att markera dagens datum.
og_image_alt: Screenshot of an Excel workbook created with Python showing colored
  cells and today’s date highlighted
og_title: Skapa Excel‑arbetsbok med Python – Formatera celler och markera idag
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
title: Skapa Excel-arbetsbok i Python – Fullständig guide till styling och villkorsstyrd
  formatering
url: /sv/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel-arbetsbok med Python – Fullständig guide till formatering och villkorsstyrd formatering

Har du någonsin undrat hur man **skapar Excel-arbetsbok med Python** från grunden utan att öppna Excel själv? Du är inte ensam. Många utvecklare behöver generera rapporter, instrumentpaneler eller till och med enkla dataloggar i farten, och att göra det programatiskt sparar timmar av manuellt arbete.

I den här handledningen går vi igenom hela processen: från att skapa en helt ny arbetsbok, till att **ange cellbakgrundsfärg**, till att **ange cellstil programatiskt**, och slutligen att **markera dagens datum i Excel** med hjälp av **lägg till villkorsstyrd formatering i Python**. I slutet har du ett färdigt skript som producerar en polerad .xlsx-fil på några sekunder.

---

## Vad du kommer att bygga

- En ny Excel-fil med några ifyllda celler.
- Celler färgade med en anpassad bakgrund.
- Numeriska och datumvärden formaterade med en specifik talstil.
- En villkorsregel som automatiskt markerar cellen som innehåller dagens datum.

Ingen extern Excel-installation krävs—Aspose.Cells för Python via .NET sköter allt det tunga arbetet.

---

## Förutsättningar

| Krav | Varför det är viktigt |
|------|-----------------------|
| Python 3.8+ | Modern syntax och typindikeringar |
| `aspose-cells` package | Kärnbibliotek för arbetsboksmanipulation |
| `aspose-pydrawing` (installed with Aspose.Cells) | Tillhandahåller `Color`-klassen |
| Basic familiarity with Excel concepts (cells, ranges, formatting) | Gör handledningen smidigare |

Install the library with:

```bash
pip install aspose-cells
```

---

## Steg 1: Initiera arbetsboken och kalkylbladet

Det första du gör när du **skapar Excel-arbetsbok med Python** är att instansiera ett `Workbook`-objekt och hämta standardkalkylbladet. Tänk på arbetsboken som hela Excel-filen, medan kalkylbladet är en enskild flik i den.

```python
from aspose.cells import Workbook

# Create a new workbook – this is our empty Excel file
book = Workbook()

# Grab the first (default) worksheet
sheet = book.worksheets[0]
```

> **Proffstips:** Om du behöver flera blad, använd `book.worksheets.add("MySheet")` för att lägga till fler flikar.

---

## Steg 2: Hjälparklass för formatering & villkorsstyrd formatering

Nedan är en kompakt men komplett `ConditionalFormatting`-klass. Den kapslar in de repetitiva uppgifterna:

1. Konvertera ett område som `"A1:C3"` till ett `CellArea`.
2. Fyll varje cell i det området med ett sekventiellt nummer (endast för demonstrationsändamål).
3. Applicera en solid **ange cellbakgrundsfärg**.
4. Lägg till en villkorsregel som **markerar dagens datum i Excel**.

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

### Varför en hjälparklass?

- **Återanvändbarhet:** Du kan anropa `add_time_period_1()` för vilket kalkylblad som helst utan att skriva om logiken.
- **Tydlighet:** Varje metod gör en sak – ett kännetecken för ren kod.
- **Utbyggbarhet:** Vill du lägga till fler regler? Lägg bara till en annan metod enligt samma mönster.

---

## Steg 3: Applicera formateringen och spara filen

Nu knyter vi ihop allt: instansiera hjälparen, kör formateringsrutinen och skriv slutligen arbetsboken till disk.

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

När du öppnar *styled_workbook.xlsx* bör du se:

- Celler **A1:C3** numrerade 0‑8 med en ljus himmelsblå fyllning.
- Cell **I1** visar dagens datum med rosa bakgrund (tack vare den villkorsstyrda regeln).
- Cell **K2** visar det statiska datumet *2008‑07‑30* för jämförelse.
- Cell **I2** innehåller texten “Today”.

Den visuella indikationen är exakt vad **markerar dagens datum i Excel**-kravet efterfrågar.

---

## Steg 4: Gräv djupare – Anpassa stilar

Om du behöver justera teckensnitt, kanter eller talformat kan du utöka `fill_cell`-metoden eller skapa en ny hjälparklass:

```python
def apply_custom_style(cell, font_name="Calibri", font_size=11, bold=False):
    style = cell.get_style()
    style.font.name = font_name
    style.font.size = font_size
    style.font.bold = bold
    cell.set_style(style)
```

Du kan då anropa `apply_custom_style(cell, bold=True)` i loopen för att **ange cellstil programatiskt** för varje cell i ett område.

---

## Vanliga fallgropar & hur man undviker dem

| Symptom | Trolig orsak | Lösning |
|---------|--------------|---------|
| Celler förblir vita trots `Color.light_sky_blue` | Stilen applicerades inte efter att `foreground_color` satts | Anropa alltid `cell.set_style(style)` efter att stilobjektet har modifierats. |
| Villkorsregeln aktiveras aldrig | `style.number` är inte satt för datumceller, så Excel behandlar värdet som en sträng | Sätt `style.number = 30` (eller något datumformat) innan `cell.put_value(datetime…)`. |
| Arbetsboken sparas som .xls trots `SaveFormat.XLSX` | Äldre Aspose-version som standardar till legacy-format | Uppgradera till den senaste `aspose-cells`-paketet. |
| Område som `"A1"` ger ett indexfel | Använder `cells.get("A1")` på ett blad som inte har initierats | Säkerställ att kalkylbladet finns (det gör det direkt efter `Workbook()`), eller använd `cells.get(row, col)` med nollbaserade index. |

---

## Fullt skript för kopiera‑och‑klistra

Nedan är det **fullständiga** skriptet som du kan klistra in i en fil med namnet `create_excel.py` och köra omedelbart.

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


## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Excel‑automatisering med Aspose.Cells .NET: Skapa arbetsbok & ange externa länkar](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Behärska Excel‑cellformatering och arbetsbokshantering med Aspose.Cells för .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel‑automatisering: Skapa en arbetsbok och lägg till en ListBox med Aspose.Cells för .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}