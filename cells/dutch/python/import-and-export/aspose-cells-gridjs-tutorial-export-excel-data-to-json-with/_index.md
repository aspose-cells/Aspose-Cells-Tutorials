---
category: general
date: 2026-07-03
description: Aspose Cells GridJs‑tutorial die laat zien hoe je Excel‑gegevens naar
  JSON exporteert en een werkblad efficiënt naar JSON exporteert met lazy loading.
draft: false
keywords:
- aspose cells gridjs tutorial
- export excel data json
- export worksheet to json
language: nl
og_description: De Aspose Cells GridJs‑tutorial legt uit hoe u Excel‑gegevens naar
  JSON exporteert en een werkblad naar JSON exporteert met lazy loading voor grote
  spreadsheets.
og_title: Aspose Cells GridJs-tutorial – Exporteer Excel-gegevens naar JSON
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  headline: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  type: TechArticle
- description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  name: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed locally. - `asposecells` package (you can `pip
      install aspose-cells`). - A sizeable Excel file (e.g., `large-data.xlsx`) placed
      in a known directory. - Basic familiarity with Python and web development concepts.'
  - name: Exporting a specific worksheet
    text: 'The example above always uses the first worksheet (`Worksheets[0]`). To
      export a different sheet, simply change the index or use the sheet name:'
  - name: Changing the chunk size for massive files
    text: For files with millions of rows, a chunk size of 500 may still be too small,
      causing many round‑trips. You can increase it to 2000 or more, but remember
      that larger chunks consume more bandwidth per request.
  - name: Exporting to a stream instead of a file
    text: 'If your API returns the JSON directly, you don’t need to write to disk:'
  - name: Handling formulas and formatting
    text: 'By default, `ExportGridJsJson` includes the calculated values of formulas.
      If you need raw formulas instead, set:'
  type: HowTo
tags:
- Aspose.Cells
- Python
- GridJs
- JSON export
title: Aspose Cells GridJs-tutorial – Exporteer Excel-gegevens naar JSON met lazy
  loading
url: /nl/python/import-and-export/aspose-cells-gridjs-tutorial-export-excel-data-to-json-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Cells GridJs‑tutorial – Export Excel‑gegevens JSON met lazy loading

Heb je je ooit afgevraagd hoe je **Excel‑gegevens JSON** kunt exporteren vanuit een enorme spreadsheet zonder de browser te laten haperen? In deze Aspose Cells GridJs‑tutorial lopen we een complete, kant‑klaar oplossing door die je **werkblad naar JSON exporteert** met lazy loading, zodat alleen de rijen die je nodig hebt op aanvraag worden opgehaald.

Als je worstelt met enorme `.xlsx`‑bestanden en de client‑kant blijft bevriezen, ben je niet de enige. Het goede nieuws? De aanpak die we hier behandelen is zowel lichtgewicht als schaalbaar, en je kunt hem in elk Python‑project gebruiken dat al de Aspose.Cells‑bibliotheek gebruikt.

## Wat deze gids behandelt

In de komende paar minuten leer je hoe je:

1. Een groot werkboek laden met Aspose.Cells.
2. GridJs lazy loading inschakelen zodat de server rijen in delen streamt.
3. De GridJs‑configuratie exporteren naar een JSON‑bestand dat de front‑end kan gebruiken.
4. De chunk‑grootte aanpassen voor optimale prestaties.
5. De output verifiëren en integreren met een eenvoudige HTML‑pagina.

Geen externe services, geen verborgen magie—alleen pure Python en de Aspose.Cells‑API. Aan het einde heb je een **volledige export‑werkblad‑naar‑JSON**‑pipeline die je kunt aanpassen voor dashboards, rapportagetools of elk data‑grid‑component.

### Vereisten

- Python 3.8+ lokaal geïnstalleerd.
- `asposecells`‑pakket (je kunt `pip install aspose-cells`).
- Een omvangrijk Excel‑bestand (bijv. `large-data.xlsx`) geplaatst in een bekende map.
- Basiskennis van Python en webontwikkelingsconcepten.

Als een van deze je onbekend voorkomt, geen paniek—elke stap bevat een korte “waarom”‑uitleg zodat je de reden achter de code begrijpt.

---

## Stap 1: Installeer en importeer Aspose.Cells

Allereerst hebben we de Aspose.Cells‑bibliotheek nodig. Het is een commercieel product, maar een gratis proefversie werkt voor ontwikkeling.

```bash
pip install aspose-cells
```

Importeer nu de benodigde klassen in je script.

```python
# Step 1: Import the Aspose.Cells workbook class
import asposecells
from asposecells import Workbook
```

> **Waarom dit belangrijk is:** Het importeren van `Workbook` geeft je toegang tot de high‑performance engine die Excel‑bestanden direct in het geheugen leest, waardoor de tragere `openpyxl`‑methode wordt omzeild.

## Stap 2: Laad het werkboek met de grote dataset

Met de bibliotheek klaar, wijs je deze op je Excel‑bestand. Het pad kan absoluut of relatief zijn; zorg er gewoon voor dat het bestand bestaat.

```python
# Step 2: Load the workbook that contains a large data set
workbook = Workbook("YOUR_DIRECTORY/large-data.xlsx")
```

> **Pro tip:** Als je werkboek groter is dan enkele honderden megabytes, overweeg dan het geheugenlimiet van het Python‑proces te verhogen of een 64‑bit interpreter te gebruiken om `MemoryError` te voorkomen.

## Stap 3: Schakel GridJs lazy loading in

GridJs is Aspose’s JavaScript‑grid‑component. Lazy loading vertelt de server om alleen een deel van de rijen te sturen—perfect voor enorme bladen.

```python
# Step 3: Enable lazy loading so the client fetches rows on demand
grid_options = workbook.Worksheets[0].Cells.GridJsOptions
grid_options.LazyLoading = True                 # fetch rows/columns only when needed
grid_options.LazyLoadingChunkSize = 500         # rows per server request
```

> **Waarom lazy loading?** Zonder dit zou het volledige werkblad in één keer naar JSON worden geserialiseerd, wat gemakkelijk de geheugenlimieten van de browser kan overschrijden. Door `LazyLoadingChunkSize` op 500 te zetten, bevat elk verzoek een hanteerbare payload.

## Stap 4: Exporteer de GridJs‑configuratie naar JSON

Nu vragen we Aspose om de JSON te produceren die de front‑end GridJs‑component verwacht. Dit is de kern van de **export excel data json**‑operatie.

```python
# Step 4: Export the GridJs configuration to a JSON file for the client side
grid_json = workbook.Worksheets[0].Cells.ExportGridJsJson()
```

De `ExportGridJsJson`‑methode retourneert een `bytes`‑object dat de JSON‑representatie van het werkblad bevat, klaar om te worden opgeslagen of gestreamd.

## Stap 5: Schrijf de JSON naar een bestand (of stream het)

Voor een snelle test, schrijf de JSON naar schijf. In een productie‑API zou je deze direct teruggeven vanuit een Flask/Django‑endpoint.

```python
# Step 5: Persist the JSON to a file
output_path = "YOUR_DIRECTORY/lazygrid.json"
with open(output_path, "wb") as f:
    f.write(grid_json)

print(f"✅ GridJs JSON exported successfully to {output_path}")
```

> **Wat je zult zien:** Het openen van `lazygrid.json` onthult een structuur met `columns`, `rows` en paginering‑metadata. De `rows`‑array zal aanvankelijk leeg zijn; GridJs zal het eerste chunk opvragen wanneer de pagina laadt.

## Stap 6: Koppel de JSON aan een eenvoudige HTML‑pagina (optioneel)

Als je het raster in actie wilt zien, maak dan een klein HTML‑bestand dat GridJs van een CDN laadt en erop wijst naar de gegenereerde JSON.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Lazy‑Loaded GridJs Demo</title>
    <link href="https://unpkg.com/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
    <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
</head>
<body>
    <div id="wrapper"></div>
    <script>
        // Fetch the lazy‑loaded JSON and initialize GridJs
        fetch('lazygrid.json')
            .then(r => r.json())
            .then(config => {
                new gridjs.Grid({
                    ...config,
                    server: {
                        url: 'lazygrid.json',
                        then: data => data
                    }
                }).render(document.getElementById('wrapper'));
            });
    </script>
</body>
</html>
```

> **Waarom dit opnemen?** Het toont de volledige round‑trip: Python maakt de JSON, de browser haalt deze op, en GridJs rendert de data chunk‑voor‑chunk. Je kunt nu experimenteren met verschillende `LazyLoadingChunkSize`‑waarden om de optimale instelling voor je netwerk te vinden.

## Stap 7: Verifiëren en problemen oplossen

Voer het Python‑script uit:

```bash
python export_lazy_grid.py
```

Je zou het succesbericht en een `lazygrid.json`‑bestand moeten zien. Open het HTML‑bestand in een browser; het raster zou de eerste 500 rijen direct moeten weergeven, met paginering‑besturingselementen om meer te laden.

Als het raster leeg lijkt:

- **Controleer de grootte van het JSON‑bestand** – een bestand van nul bytes betekent meestal dat het pad naar het werkboek onjuist was.
- **Bevestig dat lazy loading is ingeschakeld** – de `LazyLoading`‑vlag moet `True` zijn.
- **Inspecteer de browser‑console** – eventuele CORS‑ of 404‑fouten geven aan dat de JSON niet correct wordt geserveerd.

---

## Veelvoorkomende variaties en randgevallen

### Een specifiek werkblad exporteren

Het voorbeeld hierboven gebruikt altijd het eerste werkblad (`Worksheets[0]`). Om een ander blad te exporteren, wijzig je eenvoudig de index of gebruik je de bladnaam:

```python
sheet = workbook.Worksheets["DataSheet"]   # by name
grid_options = sheet.Cells.GridJsOptions
grid_json = sheet.Cells.ExportGridJsJson()
```

### De chunk‑grootte aanpassen voor enorme bestanden

Voor bestanden met miljoenen rijen kan een chunk‑grootte van 500 nog steeds te klein zijn, waardoor er veel round‑trips ontstaan. Je kunt deze verhogen naar 2000 of meer, maar onthoud dat grotere chunks meer bandbreedte per verzoek verbruiken.

```python
grid_options.LazyLoadingChunkSize = 2000
```

### Exporteren naar een stream in plaats van een bestand

Als je API de JSON direct retourneert, hoef je deze niet naar schijf te schrijven:

```python
from flask import Flask, Response
app = Flask(__name__)

@app.route("/api/gridjson")
def gridjson():
    json_bytes = workbook.Worksheets[0].Cells.ExportGridJsJson()
    return Response(json_bytes, mimetype="application/json")
```

### Formules en opmaak verwerken

Standaard bevat `ExportGridJsJson` de berekende waarden van formules. Als je in plaats daarvan de ruwe formules nodig hebt, stel dan:

```python
grid_options.ExportFormulas = True
```

## Conclusie

In deze **Aspose Cells GridJs‑tutorial** hebben we alles behandeld wat je nodig hebt om **Excel‑gegevens JSON te exporteren** en **werkblad naar JSON te exporteren** met lazy loading. Van het installeren van Aspose.Cells, het inschakelen van lazy loading, het genereren van de JSON, tot het koppelen aan een eenvoudige HTML‑pagina, je hebt nu een full‑stack patroon dat elegant schaalt met enorme spreadsheets.

Probeer het uit—pas de chunk‑grootte aan, wijs naar verschillende werkbladen, of integreer de endpoint in een Flask‑ of Django‑app. De mogelijkheden zijn eindeloos, en de prestatieverbeteringen zijn direct.

Klaar voor de volgende stap? Probeer kolomsortering, aangepaste cel‑renderers, of zelfs server‑side filtering toe te voegen om je GridJs‑grid echt interactief te maken. Als je tegen een probleem aanloopt, laat dan een reactie achter; happy coding!

## Wat je hierna kunt leren

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [JSON-gegevens importeren in Excel met Aspose.Cells Java&#58; Een uitgebreide gids](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [CSV laden & exporteren naar JSON met Aspose.Cells voor .NET&#58; Een uitgebreide gids](/cells/english/net/import-export/load-csv-export-json-aspose-cells-dotnet/)
- [Excel‑gegevens exporteren met Aspose.Cells .NET&#58; Een complete gids voor naadloze gegevens‑export](/cells/english/net/import-export/export-excel-data-aspose-cells-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}