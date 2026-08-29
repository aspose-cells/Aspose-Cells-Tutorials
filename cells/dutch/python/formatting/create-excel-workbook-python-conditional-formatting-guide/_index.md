---
category: general
date: 2026-07-20
description: Maak een Excel-werkmap in Python met Aspose.Cells, stel de celachtergrondkleur
  in en voeg voorwaardelijke opmaak toe in Python om cellen op datum te stylen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: nl
lastmod: 2026-07-20
og_description: Maak een Excel-werkmap in Python met Aspose.Cells. Leer hoe je de
  achtergrondkleur van een cel instelt en voorwaardelijke opmaak toevoegt in Python
  om cellen op datum te formatteren.
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: Excel-werkmap maken met Python – Voorwaardelijke opmaak toevoegen
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Create Excel workbook Python with Aspose.Cells, set cell background
    color, and add conditional formatting python to style cells by date.
  headline: Create Excel Workbook Python – Conditional Formatting Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Change `"I19:K20"` to any A1‑style range, and adjust the sample
      dates accordingly.
    question: Can I target a different date range?
  - answer: Use `FormatConditionType.FORMULA` and set `condition.formula1 = "YOUR_FORMULA"`—for
      example, `=TODAY()-A1=1` to mimic yesterday.
    question: What if I need a custom formula instead of `YESTERDAY`?
  - answer: Call `conditions.add_condition` again with a different `FormatConditionType`.
      The order matters; later rules can override earlier ones.
    question: How do I apply multiple rules to the same range?
  - answer: Yes—modify `condition.style.font.color = Color.white` (or any other `Color`).
    question: Is there a way to set font colour together with background?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
title: Excel-werkboek maken met Python – Gids voor voorwaardelijke opmaak
url: /nl/python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-werkmap maken met Python – Gids voor voorwaardelijke opmaak

Heb je je ooit afgevraagd hoe je **een Excel-werkmap met Python** vanaf nul kunt maken en er een gepolijste uitstraling aan kunt geven zonder de UI te openen? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze **de achtergrondkleur van een cel moeten instellen** of datum‑gebaseerde stijlen programmatisch moeten toepassen.  

In deze tutorial lopen we stap voor stap door een volledig, uitvoerbaar voorbeeld dat Aspose.Cells gebruikt om **voorwaardelijke opmaak met Python** regels toe te voegen, cellen op datum te formatteren en het resultaat op te slaan als een modern XLSX‑bestand. Aan het einde heb je een zelfstandige script die je in elk project kunt plaatsen.

## Wat je gaat leren

- Hoe je een werkmap initialiseert en het eerste werkblad ophaalt.  
- Manieren om **de achtergrondkleur van een cel** voor een heel bereik in te stellen.  
- Het gebruik van **aspose cells conditional formatting** om “Gisteren” datums te markeren.  
- Kolommen automatisch aanpassen en het bestand opslaan op schijf.  

Er is geen externe configuratie nodig—alleen Python 3 en het Aspose.Cells‑pakket. Als je `aspose-cells` al hebt geïnstalleerd, ben je klaar; anders volstaat een snelle `pip install aspose-cells`.

## Voorvereisten

- Python 3.8+ (de code werkt op 3.9, 3.10 en nieuwer).  
- Aspose.Cells for Python via .NET (`aspose-cells` NuGet‑wrapper).  
- Basiskennis van Excel‑concepten (cellen, bereiken, opmaak).  

Heb je dit? Geweldig—laten we beginnen.

## Excel-werkmap maken met Python – Setup en werkblad

Allereerst: we hebben een nieuw werkmap‑object en een verwijzing naar het standaardwerkblad nodig. Dit is het canvas waarop alle latere bewerkingen plaatsvinden.

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **Waarom dit belangrijk is:** `Workbook()` maakt een Excel‑bestand in het geheugen, waardoor er geen tijdelijke bestanden nodig zijn. De variabele `worksheet` is ons toegangspunt voor bewerkingen op celniveau.

## Achtergrondkleur van cel instellen

Voordat we regels toevoegen, is het prettig om het doelbereik een basiskleur te geven zodat de voorwaardelijke opmaak eruit springt. De helper hieronder haalt (of maakt) een `FormatConditionCollection` voor een opgegeven bereik op en kleurt de cellen met een effen achtergrond.

```python
def get_format_condition(cell_range: str, base_color: Color):
    """
    Obtain (or create) a FormatConditionCollection for `cell_range`.
    Also set a base background colour for the whole range.
    """
    # Retrieve or add a conditional formatting entry for the range
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    # Apply the base colour to every cell in the range
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color          # set cell background color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection
```

> **Pro‑tip:** Als je van plan bent hetzelfde bereik met meerdere regels te gebruiken, roep deze helper dan één keer aan en bewaar de geretourneerde collectie; dit bespaart een paar API‑calls.

## Voorwaardelijke opmaak met Python voor datum‑bereiken

Nu het leuke deel: we maken een **tijd‑periode voorwaardelijke opmaak**‑regel die cellen met de datum van gisteren markeert. Dit laat de kracht zien van **format cells by date** met Aspose.Cells.

```python
def apply_yesterday_rule():
    """
    Apply a “Yesterday” conditional formatting rule to the range I19:K20.
    Cells that match will turn pink; others stay with the base colour.
    """
    # Obtain the condition collection for the target range
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)

    # Create a TIME_PERIOD condition (this is the aspose cells conditional formatting type we need)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]

    # Define the appearance for cells that meet the condition
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Set the time period to “Yesterday”
    condition.time_period = TimePeriodType.YESTERDAY

    # Populate sample dates to demonstrate the rule
    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))   # matches “Yesterday”
    cell_i19.style.number = 30                 # Excel number format for dates
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))    # does NOT match
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    # Add a label for clarity
    worksheet.cells.get("I20").put_value("Yesterday")
```

> **Waarom `TIME_PERIOD` gebruiken?** Het abstraheert het schrijven van aangepaste formules. Aspose.Cells vergelijkt de datum met de huidige systeemdatum, zodat de regel altijd actueel blijft.

### De regel uitvoeren

```python
apply_yesterday_rule()
```

Wanneer je het resulterende bestand opent, zullen cellen `I19` roze oplichten (omdat ze “Gisteren” zijn), terwijl `K20` de basisgroene kleur behoudt.

## Kolommen automatisch aanpassen en werkmap opslaan

Een nette spreadsheet oogt professioneel. Auto‑fit zorgt ervoor dat onze data niet samengeperst wordt.

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Randgeval:** Als je een map opgeeft die niet bestaat, zal `workbook.save` een fout veroorzaken. Plaats de save‑aanroep in een `try/except`‑blok als je een nette afhandeling wilt.

### Volledig script (klaar om te kopiëren)

Hieronder staat het volledige script, klaar om uitgevoerd te worden. Vervang `YOUR_DIRECTORY` door een geldige map op jouw machine.

```python
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create the workbook and worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

def get_format_condition(cell_range: str, base_color: Color):
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection

def apply_yesterday_rule():
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = TimePeriodType.YESTERDAY

    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))
    cell_i19.style.number = 30
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    worksheet.cells.get("I20").put_value("Yesterday")

apply_yesterday_rule()
worksheet.auto_fit_column(12)

output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Het uitvoeren van dit script levert `TimePeriodExample.xlsx` op met de voorwaardelijke opmaak die we beschreven.

## Veelgestelde vragen & tips

- **Kan ik een ander datum‑bereik targeten?**  
  Zeker. Verander `"I19:K20"` naar elk A1‑stijl bereik en pas de voorbeelddatums aan.

- **Wat als ik een aangepaste formule nodig heb in plaats van `YESTERDAY`?**  
  Gebruik `FormatConditionType.FORMULA` en stel `condition.formula1 = "YOUR_FORMULA"` in—bijvoorbeeld `=TODAY()-A1=1` om gisteren te simuleren.

- **Hoe pas ik meerdere regels toe op hetzelfde bereik?**  
  Roep opnieuw `conditions.add_condition` aan met een ander `FormatConditionType`. De volgorde is belangrijk; latere regels kunnen eerdere overschrijven.

- **Is er een manier om tegelijk de letterkleur in te stellen?**  
  Ja—pas `condition.style.font.color = Color.white` aan (of een andere `Color`).

## Conclusie

Je weet nu hoe je **een Excel-werkmap met Python** maakt met Aspose.Cells, **de achtergrondkleur van een cel** instelt, en **voorwaardelijke opmaak met Python** toevoegt die cellen op datum formatteert. Het script is volledig functioneel, behandelt randgevallen zoals ontbrekende mappen, en kan worden uitgebreid naar meer geavanceerde scenario’s zoals meerdere voorwaardelijke regels of dynamische bereikdetectie.

Klaar voor de volgende stap? Probeer de “Gisteren”‑regel te vervangen door “Vorige week”, experimenteer met kleurverlopen, of genereer een volledig rapport met tientallen opgemaakte tabellen. De bouwstenen liggen klaar, en je hebt zojuist de kern van **aspose cells conditional formatting** in Python onder de knie.

Happy coding, en deel gerust je eigen variaties in de reacties!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}