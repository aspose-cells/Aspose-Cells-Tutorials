---
category: general
date: 2026-08-01
description: Maak een Excel-werkmap in Python met Aspose.Cells – leer kolommen automatisch
  aanpassen, cellen op datum formatteren, datumopmaak voor cellen instellen en voorwaardelijke
  opmaak toepassen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- auto fit excel column
- format cells by date
- set cell date format
- aspose cells conditional formatting
language: nl
lastmod: 2026-08-01
og_description: Maak direct een Excel-werkmap met Python. Volg deze gids om kolommen
  automatisch aan te passen, cellen op datum te formatteren, datumopmaak voor cellen
  in te stellen en de voorwaardelijke opmaak van Aspose Cells onder de knie te krijgen.
og_image_alt: Screenshot showing a Python script that creates an Excel workbook using
  Aspose.Cells
og_title: Maak Excel‑werkmap met Python – Stap‑voor‑stap met Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-01'
  description: Create Excel workbook python using Aspose.Cells – learn auto fit excel
    column, format cells by date, set cell date format and apply conditional formatting.
  headline: Create Excel Workbook Python – Full Guide with Aspose.Cells
  type: TechArticle
tags:
- Aspose Cells
- Python
- Excel automation
- Conditional Formatting
- Date handling
title: Excel-werkboek maken met Python – Volledige gids met Aspose.Cells
url: /nl/python/formatting/create-excel-workbook-python-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-werkmap maken met Python – Volledige gids met Aspose.Cells

Heb je je ooit afgevraagd hoe je **create Excel workbook python**‑scripts kunt maken die er professioneel uitzien zonder Excel handmatig te openen? Je bent niet de enige. Of je nu een rapportagedashboard bouwt of dagelijkse data‑dumps automatiseert, de mogelijkheid om een Excel‑bestand vanuit Python te genereren is een echte game‑changer.

In deze tutorial lopen we stap voor stap door een compleet, uitvoerbaar voorbeeld dat niet alleen een werkmap maakt, maar ook **auto fit excel column**, **format cells by date**, **set cell date format** demonstreert, en **aspose cells conditional formatting** toepast. Aan het einde heb je een zelfstandige script die je in elk project kunt gebruiken.

> **Pro tip:** Aspose.Cells for Python via .NET laat je werken met Excel‑bestanden zonder een COM‑afhankelijkheid, waardoor het perfect is voor Linux‑containers of CI‑pipelines.

## Wat je nodig hebt

- **Python 3.8+** (de code werkt op elke recente versie)  
- **Aspose.Cells for Python via .NET** – installeer met `pip install aspose-cells`  
- Een map waarin je kunt schrijven (we noemen deze `YOUR_DIRECTORY`)  
- Een basisbegrip van Python‑functies en objecten (geen diepgaande Excel‑kennis vereist)  

Als je dit al hebt, geweldig—laten we beginnen.

## Stap 1: Create Excel Workbook Python – Initialiseer de werkmap

Het eerste wat we doen is een nieuw workbook‑object aanmaken. Beschouw het als een leeg canvas waarop elke latere bewerking een nieuw element schildert.

```python
from aspose.cells import Workbook, SaveFormat, FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color
from datetime import datetime
import os

# Create a new workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

> **Waarom dit belangrijk is:** `Workbook()` creëert een in‑memory representatie van een `.xlsx`‑bestand. Door `worksheets[0]` te benaderen krijgen we het standaardblad, klaar voor data en opmaak.

## Stap 2: Definieer het doelbereik en basiskleur – Voorbereiden voor voorwaardelijke opmaak

Voordat we enige voorwaardelijke logica toevoegen, hebben we een bereik nodig dat de regel zal bevatten. Het bereik `I19:K20` is willekeurig maar groot genoeg om meerdere cellen te demonstreren.

```python
# Add a conditional formatting collection to the range and set a base colour
conds = worksheet.conditional_formattings.add("I19:K20", Color.medium_sea_green)
```

De `add`‑methode maakt zowel het opmaakobject als een standaardachtergrond, waardoor de latere regel eruit springt.

## Stap 3: Aspose Cells Conditional Formatting – Pas een TIME_PERIOD‑regel toe voor YESTERDAY

Nu komen we bij het hart van de demo: een **TIME_PERIOD**‑conditie die cellen markeert met de datum van gisteren.

```python
# Insert a TIME_PERIOD condition for YESTERDAY
condition_index = conds.add_condition(FormatConditionType.TIME_PERIOD)
condition = conds[condition_index]

# Configure the rule – yesterday, pink background, solid fill
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

> **Uitleg:** `FormatConditionType.TIME_PERIOD` vertelt Aspose dat we te maken hebben met een datum‑gebaseerde regel. Door `time_period` op `YESTERDAY` te zetten, evalueert de engine automatisch de waarde van elke cel ten opzichte van de vorige kalenderdag.

## Stap 4: Voorbeelddata invullen – Stel cel‑datumnotatie in en controleer de regel

Om de regel in actie te zien hebben we echte datums nodig. We **set cell date format** ook zodat de waarden als leesbare datums verschijnen.

```python
# Cell I19 – a date that falls on “yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))          # July 30, 2008 is “yesterday” for demo purposes
style_i19 = cell_i19.get_style()
style_i19.number = 30          # 30 = built‑in Excel date format (e.g., mm/dd/yyyy)
cell_i19.set_style(style_i19)

# Cell K20 – a date outside the period (no formatting applied)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)
```

Let op dat we hetzelfde **format cells by date**‑nummer (`30`) voor beide cellen gebruiken. Dit zorgt ervoor dat de datums consistent worden weergegeven, ongeacht de systeem‑locale.

## Stap 5: Voeg een beschrijvend label toe – Maak het blad zelf‑verklarend

Een klein label helpt iedereen die het bestand opent te begrijpen wat de gekleurde cellen betekenen.

```python
worksheet.cells.get("I20").put_value("Yesterday")
```

## Stap 6: Auto Fit Excel Column – Pas kolombreedtes automatisch aan

Wanneer je data programmatisch genereert, blijven kolombreedtes vaak op de standaard smalle grootte. De **auto fit excel column**‑methode vergroot ze net genoeg om de inhoud weer te geven.

```python
# Auto‑fit the 12th column (which corresponds to column L) so the label is fully visible
worksheet.auto_fit_column(12)
```

> **Waarom kolom 12?** In nul‑gebaseerde indexering correspondeert kolom `12` met de Excel‑kolom `L`. Pas de index aan als je de lay‑out wijzigt.

## Stap 7: Sla de werkmap op – Exporteer naar een echt bestand

Tot slot schrijven we alles naar schijf. De `SaveFormat.XLSX`‑vlag zorgt voor een modern, zip‑gebaseerd werkboek.

```python
output_file = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_file, SaveFormat.XLSX)
print(f"Workbook saved to {output_file}")
```

### Verwacht resultaat

Open `TimePeriodDemo.out.xlsx` in Excel (of een andere viewer) en je zou moeten zien:

- Cel **I19** gemarkeerd in **roze** omdat de datum overeenkomt met “gisteren”.  
- Cel **K20** ongewijzigd, wat aantoont dat de voorwaardelijke regel correct datums buiten de periode negeert.  
- Kolom **L** automatisch aangepast zodat het label “Yesterday” niet wordt afgekapt.

![Create Excel workbook python example](/images/create_excel_workbook_python.png){: .center-image alt="Voorbeeld van create Excel workbook python met voorwaardelijke opmaak voor de datum van gisteren"}

## Veelvoorkomende variaties & randgevallen

| Situatie | Hoe aan te passen |
|-----------|-------------------|
| **Andere datumbereik** | Verander `condition.time_period` naar `TimePeriodType.TODAY`, `TimePeriodType.LAST_7_DAYS`, enz. |
| **Meerdere voorwaarden** | Roep opnieuw `conds.add_condition()` aan en configureer een nieuw `FormatConditionType` (bijv. `FORMAT_CONDITION_TYPE.EXPRESSION`). |
| **Aangepaste datumnotatie** | Gebruik `style_i19.number = 14` voor `mm-dd-yy` of wijs een aangepaste notatie toe via `style_i19.custom = "dd-mmm-yyyy"`. |
| **Grote werkbladen** | Plaats de `auto_fit_column`‑aanroep in een try/except‑blok om prestatie‑problemen bij enorme bestanden te vermijden. |
| **Uitvoeren in headless CI** | Er is geen UI nodig; Aspose werkt volledig in het geheugen, zodat je het bestand in een Docker‑container kunt genereren zonder Excel geïnstalleerd. |

## Samenvatting – Wat we hebben behandeld

- **Create Excel workbook python** vanaf nul met Aspose.Cells.  
- **Auto fit excel column** om je output netjes te houden.  
- **Format cells by date** en **set cell date format** voor consistente weergave.  
- Toepassen van **aspose cells conditional formatting** met het `TIME_PERIOD`‑type.

Dit alles past in één eenvoudig uit te voeren script dat je kunt aanpassen voor facturen, dagelijkse logs, of elke situatie waarin datums visuele aanwijzingen sturen.

## Volgende stappen

Als je de basis onder de knie hebt, overweeg dan om te verkennen:

- **Data bars, color scales, and icon sets** voor rijkere voorwaardelijke styling.  
- **PivotTable‑generatie** via `worksheet.pivot_tables.add()`.  
- **Exporteren naar PDF** met `workbook.save("report.pdf", SaveFormat.PDF)`.  

Elk van deze onderwerpen bouwt voort op dezelfde fundamentele concepten die we hier hebben gebruikt, dus je voelt je meteen thuis.

---

*Happy coding! Als je ergens vastloopt, laat dan een reactie achter of raadpleeg de Aspose.Cells for Python‑documentatie voor diepere duiken.*

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementaties in je eigen projecten te verkennen.

- [Auto-Fit Rows & Columns in Excel using Aspose.Cells Java for Seamless Workbook Management](/cells/english/java/range-management/aspose-cells-java-auto-fit-rows-columns/)
- [Create an Excel Workbook using Aspose.Cells in Java&#58; A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Automate Excel Column Widths&#58; Auto-Fit Columns using Aspose.Cells for .NET](/cells/english/net/range-management/excel-automation-auto-fit-columns-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}