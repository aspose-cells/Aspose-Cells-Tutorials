---
category: general
date: 2026-11-16
description: Maak voorwaardelijke opmaak in Excel met Python. Leer een bereik voor
  voorwaardelijke opmaak toe te voegen, datums te markeren en een werkmap programmatisch
  te bouwen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: nl
lastmod: 2026-11-16
og_description: Maak voorwaardelijke opmaak in Excel met Python. Deze tutorial laat
  zien hoe je een bereik voor voorwaardelijke opmaak toevoegt, datums markeert en
  een werkmap genereert.
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: Maak voorwaardelijke opmaak in Excel met Python – stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Hoe maak je voorwaardelijke opmaak in Excel met Python
url: /nl/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe maak je voorwaardelijke opmaak in Excel met Python

Als je **voorwaardelijke opmaak** in een Excel‑bestand moet maken terwijl je in Python werkt, laat deze gids je precies zien hoe je dat doet. Je leert **create excel workbook python**‑style, een opmaakbereik te definiëren en datums te markeren zonder de IDE te verlaten.

Voorwaardelijke opmaak stelt je in staat om cellen die aan specifieke criteria voldoen visueel te markeren — perfect voor dashboards, rapporten of gegevensvalidatie‑bladen. Aan het einde van deze tutorial heb je een volledig functionele werkmap die cellen met de datum “Yesterday” roze kleurt, terwijl de rest van het bereik groen blijft.

## Wat je zult bereiken

* Een nieuwe werkmap vanaf nul bouwen.  
* Een voorwaardelijke‑opmaakcollectie toevoegen voor een specifiek celblok.  
* Een **TIME_PERIOD**‑regel toepassen die datums markeert (het “how to highlight dates” scenario).  
* Het bestand opslaan als een XLSX‑werkmap klaar voor downstream verwerking.

**Vereisten**  
* Python 3.8+  
* `aspose-cells` Python‑pakket (`pip install aspose-cells`)  
* Basiskennis van Python’s `datetime`‑module  

---

## Hoe maak je voorwaardelijke opmaak in Python

De eerste stap is het opzetten van de werkmap en het werkblad dat de opmaakregels zal bevatten.

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**Waarom dit belangrijk is** – `Workbook` is het toegangspunt voor alle Excel‑bewerkingen. Het programmatically creëren van de werkmap vervangt de handmatige “File → New” stap, waardoor geautomatiseerde rapport‑pijplijnen mogelijk worden.

---

## De voorwaardelijke‑opmaakcollectie voorbereiden – bereik voor voorwaardelijke opmaak toevoegen

Vervolgens definiëren we het celblok dat de regel zal ontvangen. In dit voorbeeld is het bereik **I19:K20**.

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**Uitleg** – `conditional_formattings.add` registreert een nieuwe collectie gekoppeld aan de adres‑string. De eerste voorwaarde (`conds[0]`) fungeert als een “default” stijl; de latere regel zal deze overschrijven wanneer aan de criteria wordt voldaan.

---

## Een TIME_PERIOD‑voorwaarde toevoegen – hoe datums te markeren

Nu voegen we de daadwerkelijke logica toe die “Yesterday”‑datums identificeert en ze roze kleurt.

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**Waarom TIME_PERIOD gebruiken?** – Aspose.Cells biedt ingebouwde enumeraties zoals `YESTERDAY`, `TODAY` en `LAST_WEEK`. Ze evalueren de datumwaarde van de cel ten opzichte van de huidige systeemdatum, waardoor aangepaste formules overbodig zijn.

---

## Voorbeeldgegevens invoegen – de regel demonstreren

Om de opmaak in actie te zien, voegen we een datum in die aan de regel voldoet en een andere die dat niet doet.

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**Opmerking over randgeval** – De `TIME_PERIOD`‑regel werkt alleen met *echte* datums. Als een cel tekst bevat (bijv. “N/A”), wordt de regel genegeerd, waardoor onverwachte kleurveranderingen worden voorkomen.

---

## De werkmap opslaan – add conditional formatting python

Tot slot schrijf je de werkmap naar schijf. Het bestand kan in elk spreadsheet‑programma worden geopend om de kleuren te verifiëren.

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**Verwacht resultaat**  

| I19 (groen → roze) | J19 (groen) | K19 (groen) |
|--------------------|------------|------------|
| 7/30/2008 (gisteren) | – | – |
| **I20**: “Yesterday”‑label | – | – |
| I21‑K21 (groen)    | – | – |

De cel **I19** verschijnt met een roze achtergrond omdat de datum overeenkomt met de “Yesterday”‑periode, terwijl **K20** groen blijft.

---

## Veelgestelde vragen en praktische tips

* **Kan ik een aangepast datumbereik gebruiken in plaats van een ingebouwde periode?**  
  Ja. Vervang `condition.time_period` door `condition.formula1 = "TODAY()-1"` en stel `condition.type = FormatConditionType.FORMULA` in.

* **Wat als mijn werkmap al gegevens bevat?**  
  Gebruik `worksheet.cells.import_data` om gegevens in bulk te laden voordat je de voorwaardelijke opmaakcollectie toevoegt.

* **Prestaties bij grote bladen?**  
  Het toevoegen van veel voorwaarden kan het renderen vertragen. Groepeer cellen met dezelfde regel in één bereik (bijv. “A1:C1000”) om het aantal voorwaarden laag te houden.

* **Cross‑platform compatibiliteit?**  
  Het gegenereerde XLSX‑bestand volgt de Office Open XML‑standaard, dus het werkt op Windows, macOS en Linux spreadsheet‑applicaties.

---

## Conclusie

Je weet nu hoe je **voorwaardelijke opmaak** in een Excel‑werkmap kunt **creëren** met Python. De tutorial behandelde het maken van de werkmap, het definiëren van een **add conditional formatting range**, het toepassen van een **how to highlight dates**‑regel, en het opslaan van het bestand — alles met de **add conditional formatting python**‑aanpak die door Aspose.Cells wordt geleverd.

Van hieruit kun je:

* De regels uitbreiden met andere `TimePeriodType`‑waarden (bijv. `TODAY`, `LAST_MONTH`).  
* Meerdere voorwaarden combineren op hetzelfde bereik voor rijkere visuele aanwijzingen.  
* Deze workflow integreren in geautomatiseerde rapport‑pijplijnen of webservices.

Veel plezier met coderen, en voel je vrij om te experimenteren met verschillende kleuren, bereiken en datumlogica om aan je rapportagebehoeften te voldoen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Excel-werkmap maken Python datum voorwaardelijke opmaak](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [Hoe tijdsperiode voorwaardelijke opmaak toe te passen in Excel met Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Excel-werkmap maken Python – Volledige gids voor styling & voorwaardelijke opmaak](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}