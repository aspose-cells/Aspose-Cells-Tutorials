---
category: general
date: 2026-06-08
description: Voeg een aangepast contextmenu toe aan GridJs en exporteer het raster
  naar CSV met een download‑CSV‑bestand‑blob. Volg deze stap‑voor‑stap‑tutorial voor
  een volledig werkend voorbeeld.
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: nl
og_description: Voeg een aangepast contextmenu toe aan GridJs en exporteer het raster
  naar CSV met een downloadbare CSV‑bestandblob. Leer de volledige implementatie in
  minder dan 10 minuten.
og_title: Aangepaste contextmenu toevoegen aan GridJs – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add custom context menu to GridJs and export grid to CSV with a download
    CSV file blob. Follow this step‑by‑step tutorial for a fully working example.
  headline: Add Custom Context Menu to GridJs – Complete Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- Python
- Flask
title: Voeg aangepast contextmenu toe aan GridJs – Complete gids
url: /nl/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aangepast contextmenu toevoegen aan GridJs – Complete gids

Wil je **een aangepast contextmenu** toevoegen aan een GridJs‑component? In deze tutorial lopen we je precies dat stap voor stap na, en laten we je zien hoe je **export grid to CSV** met een **download CSV file blob**. Of je nu een snel admin‑paneel bouwt of een volledige rapportagedashboard, een rechtermuisklik‑menu dat gebruikers in staat stelt gegevens als CSV te halen, kan een echte productiviteitsboost zijn.

We behandelen alles wat je nodig hebt: de Python‑kant met Flask, de JavaScript‑handler die de Blob maakt, en de HTML/JS die GridJs genereert. Aan het einde heb je een zelfstandige voorbeeld die je in elk project kunt gebruiken.

---

## Wat je nodig hebt

Before we dive in, make sure you have:

- **Python 3.9+** en **Flask** geïnstalleerd (`pip install flask`).
- De **gridjs** Python‑wrapper (of de JavaScript‑bibliotheek direct) – voor deze gids gaan we uit van een dunne Python‑wrapper die de JavaScript‑API weerspiegelt.
- Een basisbegrip van **async JavaScript** (`fetch`, `Promise`) – maar maak je geen zorgen, we leggen elke regel uit.
- Een editor die je prettig vindt (VS Code, PyCharm, of zelfs een eenvoudige teksteditor volstaat).

Dat is alles. Geen extra front‑end build‑tools, geen Node‑npm gedoe. Gewoon eenvoudige Flask die de HTML serveert die GridJs genereert.

---

## Aangepast contextmenu toevoegen aan GridJs

Het eerste dat je moet doen is GridJs laten weten dat je een aangepast rechtermuisklik‑menu wilt. Standaard wordt GridJs geleverd met een minimale set (kopiëren, plakken, enz.), maar je kunt die volledig vervangen.

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**Waarom dit belangrijk is:**  
Het instellen van `CustomContextMenu` vervangt de standaardlijst door de lijst die je opgeeft. De string `"Export CSV"` is slechts een label – het echte werk gebeurt wanneer de gebruiker erop klikt, wat we in de volgende stap zullen koppelen.

> *Pro tip:* Houd de lijst kort. Een rommelig contextmenu ondermijnt het doel van snelle acties.

---

## Grid exporteren naar CSV met een Blob‑download

Nu het menu‑item bestaat, hebben we een JavaScript‑handler nodig die met de server communiceert, de CSV ophaalt, deze omzet in een **Blob**, en een download afdwingt. Dit is waar de uitdrukking **download CSV file blob** voorkomt.

```python
# Step 4: Attach a JavaScript handler that runs when "Export CSV" is chosen.
#         The handler sends an AJAX request to a server endpoint,
#         receives the CSV file as a Blob, and triggers a download.
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""
```

### Handler stap voor stap analyseren

| Line | What It Does |
|------|--------------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | Roept een Flask‑route (`/export/csv`) aan en geeft de bladnaam door als query‑string. |
| `.then(r => r.blob())` | Zet de HTTP‑respons om naar een **Blob** – in wezen een binaire container voor de CSV‑gegevens. |
| `URL.createObjectURL(b)` | Genereert een tijdelijke URL die de browser als een bestand kan behandelen. |
| `a.download = cell.sheetName + ".csv"` | Stelt de bestandsnaam in die de gebruiker ziet in het download‑dialoogvenster. |
| `a.click()` | Klikt programmatically op de verborgen anchor, waardoor de browser de Blob downloadt. |

> **Waarom een Blob gebruiken?**  
> Browsers kunnen ruwe tekst die door `fetch` wordt geretourneerd niet direct downloaden zonder deze om te zetten in iets dat op een bestand lijkt. De Blob‑URL‑truc is de meest betrouwbare, cross‑browser manier om een **download CSV file blob** te activeren zonder de pagina te vernieuwen.

---

## Flask‑backend opzetten

De front‑end handler verwacht een endpoint op `/export/csv`. Hier is een minimale Flask‑view die de bladnaam neemt, gegevens uit de werkmap haalt, en een CSV terugstuurt.

```python
from flask import Flask, request, Response
import csv
import io

app = Flask(__name__)

# Assume `workbook` is a global object we created earlier
# (in a real app you’d probably fetch it from a database or session)
@app.route('/export/csv')
def export_csv():
    sheet_name = request.args.get('sheet', 'default')
    # Retrieve the sheet data – this is pseudo‑code; replace with your actual API
    sheet = workbook.get_sheet(sheet_name)

    # Convert rows to CSV in memory
    output = io.StringIO()
    writer = csv.writer(output)
    writer.writerow(sheet.headers)          # Header row
    writer.writerows(sheet.rows)            # Data rows

    # Create a Flask response with the correct MIME type
    csv_bytes = output.getvalue().encode('utf-8')
    return Response(
        csv_bytes,
        mimetype='text/csv',
        headers={'Content-Disposition': f'attachment;filename={sheet_name}.csv'}
    )
```

### Belangrijke punten

- **`io.StringIO`** stelt ons in staat de CSV in het geheugen te bouwen zonder het bestandssysteem aan te raken.
- **`Content‑Disposition`** vertelt de browser dat het bestand een bijlage is en stelt een bestandsnaam voor. Hoewel de front‑end ook `a.download` instelt, biedt het op de server‑kant een fallback voor niet‑JS‑clients.
- De route is opzettelijk eenvoudig; je kunt later authenticatie, permissiecontroles of streaming voor enorme datasets toevoegen.

---

## Het raster renderen aan de clientzijde

Met het contextmenu en de backend klaar, is het laatste onderdeel het renderen van de GridJs‑component en het leveren van de HTML/JS aan de browser.

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

In een Flask‑view zou je meestal doen:

```python
@app.route('/')
def index():
    html_output = grid_js.Render()
    return f"""
    <!doctype html>
    <html>
    <head>
        <title>Grid with Custom Context Menu</title>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
    </head>
    <body>
        {html_output}
    </body>
    </html>
    """
```

Wanneer de pagina laadt, bouwt GridJs de tabel, injecteert het aangepaste contextmenu, en de JavaScript‑handler die we eerder hebben gedefinieerd is klaar om te activeren. Klik met de rechtermuisknop op een willekeurige cel, kies **Export CSV**, en zie de browser een bestand downloaden met de naam van het blad.

---

## Volledig werkend voorbeeld (Alle bestanden)

Hieronder staat de volledige, uitvoerbare code die je kunt kopiëren‑plakken in een nieuwe map. Installeer Flask (`pip install flask`) en voer `python app.py` uit.

**`app.py`**



## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Load Csv Files Custom Parsers Aspose Cells Java](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [Csv Export Java Code](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [Export Excel Csv Blank Rows Aspose Cells Net](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}