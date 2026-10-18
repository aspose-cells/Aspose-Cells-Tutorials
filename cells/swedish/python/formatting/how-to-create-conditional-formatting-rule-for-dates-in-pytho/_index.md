---
category: general
date: 2026-08-24
description: Create conditional formatting rule in Python using Aspose.Cells to highlight
  dates, with auto‑fit column and background color formatting.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting rule
- auto fit column
- conditional formatting by date
- background color conditional format
- date based conditional format
language: sv
lastmod: 2026-08-24
og_description: Create conditional formatting rule in Python with Aspose.Cells. Learn
  how to highlight dates, set background colors, and auto‑fit columns in just a few
  lines of code.
og_image_alt: Screenshot of an Excel sheet where yesterday's date cells are highlighted
  in pink
og_title: Create a conditional formatting rule for dates in Python – step‑by‑step
  guide
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
title: How to create conditional formatting rule for dates in Python
url: /sv/python/formatting/how-to-create-conditional-formatting-rule-for-dates-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar villkorsformatregel för datum i Python

Om du behöver **create conditional formatting rule** som reagerar på datum, visar den här guiden exakt hur du gör det med Aspose.Cells för Python. Oavsett om du bygger en rapporteringsdashboard eller ett automatiserat kalkylblad, kommer du att se hur du markerar gårdagens datum, applicerar en anpassad bakgrundsfärg och **auto fit column**‑bredder så att resultatet ser polerat ut.

I den här handledningen kommer vi att gå igenom **conditional formatting by date**, demonstrera ett **background color conditional format**, och avsluta med att spara arbetsboken som en XLSX‑fil. I slutet kommer du att ha en återanvändbar hjälpfunktion som du kan anpassa till vilken **date based conditional format** du än behöver.

## Vad du kommer att lära dig

* Skapa en arbetsbok och ett arbetsblad med Aspose.Cells.
* Skriv en hjälpfunktion som lägger till ett **date based conditional format** till ett valfritt cellområde.
* Fyll celler med exempeldatum så att regeln kan utvärderas.
* Applicera **auto fit column** för att göra innehållet läsbart.
* Spara arbetsboken och verifiera de markerade cellerna.

Det enda förutsättningen är en fungerande Python‑miljö med paketet `aspose-cells` installerat.

## Förutsättningar

| Krav | Detaljer |
|------|----------|
| Python | 3.8+ |
| Aspose.Cells for Python via Java | `pip install aspose-cells` |
| Grundläggande kunskap om Excel‑koncept | worksheets, cells, formatting |
| Valfritt: IDE (VS Code, PyCharm, etc.) | any editor that can run Python scripts |

## Steg 1: Skapa en arbetsbok och hämta det första arbetsbladet

Det första steget är att skapa objekt som är redo för **create conditional formatting rule**: en `Workbook` och dess standard `Worksheet`. Dessa objekt är ingångspunkten för alla efterföljande operationer.

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

*Varför detta är viktigt:* `Workbook` innehåller hela Excel‑filen, medan `Worksheet` är där du applicerar celler, stilar och **conditional formatting by date**. Utan dessa objekt har resten av koden ingen plats att verka på.

## Steg 2: Bygg en hjälpfunktion för att lägga till ett TIME_PERIOD villkorsformat

Istället för att upprepa samma boiler‑plate för varje område, kapslar vi in logiken i en hjälpfunktion. Denna funktion bifogar ett **background color conditional format** som färgar celler baserat på en `TimePeriodType` (t.ex. Yesterday, Today, LastWeek).

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

*Varför vi använder en hjälpfunktion:* Den isolerar logiken för **date based conditional format**, vilket gör koden enklare att läsa, testa och återanvända över flera blad eller projekt.

## Steg 3: Applicera villkorsformatregeln på ett specifikt område

Nu använder vi hjälpfunktionen för att markera celler som innehåller “Yesterday”. Detta är kärnan i vår **create conditional formatting rule**‑operation.

```python
# Step 3 – highlight cells I19:K20 that contain “Yesterday”
add_time_period_condition(
    cell_range="I19:K20",
    bg_color=Color.medium_sea_green,   # optional default background for the whole range
    period=TimePeriodType.YESTERDAY   # the date‑based trigger
)
```

När arbetsboken öppnas kommer varje cell i `I19:K20` vars datum är lika med gårdagens datum att visas med en rosa fyllning (stilen vi satte i hjälpfunktionen). `bg_color`‑argumentet visar hur du kan lägga ett standardbakgrund bakom den villkorliga färgen om så önskas.

## Steg 4: Fyll området med exempeldatum

En villkorsregel blir bara synlig efter att arbetsbladet innehåller data som uppfyller villkoret. Vi kommer att infoga två datum: ett som matchar “Yesterday” och ett annat som ligger utanför perioden.

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

*Varför detta är viktigt:* Genom att använda `datetime`‑objekt säkerställer vi att Excel behandlar värdena som riktiga datum, vilket krävs för att **conditional formatting by date** ska fungera korrekt. Det numeriska formatet (`30`) garanterar att cellerna visas som igenkännbara datum.

## Steg 5: Auto‑fit kolumnen och spara arbetsboken

När data och formatering är på plats är den sista finputsningen att **auto fit column**‑bredder så att datumen är helt synliga. Därefter skriver vi filen till disk.

```python
# Step 5 – adjust column width and save the file

# Auto‑fit column 12 (the column that contains our sample data)
worksheet.auto_fit_column(12)

# Save the workbook as an XLSX file
output_path = "YOUR_DIRECTORY/TimePeriodDemo.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

`auto_fit_column`‑anropet undersöker det längsta innehållet i kolumn 12 (som motsvarar kolumn **L** i Excel) och utökar bredden därefter. Detta lilla steg förhindrar avkortade datum och gör **background color conditional format** tydligt synligt.

### Förväntat resultat

När du öppnar `TimePeriodDemo.out.xlsx`:

| I19 (datum) | I20 (etikett) | K20 (datum) |
|------------|------------|------------|
| 30‑Jul‑2008 (markerad rosa) | Igår | 03‑Aug‑2008 (ingen markering) |

* Cellen med gårdagens datum visar en rosa bakgrund eftersom **create conditional formatting rule** matchade `YESTERDAY`‑perioden.  
* Alla andra celler behåller standardbakgrunden (eller den valfria `medium_sea_green` du angav).  
* Kolumn L breddas automatiskt, så datumen är helt läsbara.

## Vanliga variationer och kantfall

| Situation | Hur du anpassar koden |
|-----------|------------------------|
| **Markera “Today” istället för “Yesterday”** | Byt ut `TimePeriodType.YESTERDAY` mot `TimePeriodType.TODAY`. |
| **Använd en annan bakgrundsfärg** | Ändra `condition.style.background_color = Color.pink` till någon annan `Color` (t.ex. `Color.light_sky_blue`). |
| **Applicera regeln på ett icke‑sammanhängande område** | Anropa `add_time_period_condition` flera gånger med olika `cell_range`‑strängar (t.ex. `"A1:A10", "C1:C10"`). |
| **Arbeta med en befintlig arbetsbok** | Läs in filen med `Workbook("myfile.xlsx")` istället för att skapa en ny. |
| **Flera datum‑baserade villkor på samma område** | Efter det första anropet till `add_time_period_condition`, lägg till ett annat villkor med `conditions.add_condition(FormatConditionType.TIME_PERIOD)` och ange ett annat `time_period`. |

## Slutsats

Du vet nu hur du **create conditional formatting rule** som reagerar på datum, applicerar ett **background color conditional format**, och **auto fit column**‑bredder med Aspose.Cells för Python. Hjälpfunktionen abstraherar logiken, så att du kan återanvända samma mönster för vilket **conditional formatting by date**‑scenario som helst—oavsett om det är “Yesterday”, “LastWeek” eller ett anpassat område.

Nästa steg, du kan utforska:

* Lägga till **icon sets** eller **data bars** tillsammans med datumregler.  
* Generera dynamiska rapporter som hämtar datum från en databas.  
* Kombinera flera **date based conditional format**‑regler på ett enda blad.

Känn dig fri att experimentera med olika färger, perioder och områden för att passa ditt projekts behov. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Master Conditional Formatting in Excel Using Aspose.Cells .NET: A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [How to Extract Conditional Formatting Colors Using Aspose.Cells for .NET](/cells/english/net/formatting/extract-conditional-formatting-colors-aspose-cells-net/)
- [Master Conditional Formatting with Custom Fonts in Excel using Aspose.Cells for .NET and C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}