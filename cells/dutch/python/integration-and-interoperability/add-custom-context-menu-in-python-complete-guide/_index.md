---
category: general
date: 2026-06-30
description: Voeg een aangepast contextmenu toe aan een Python‑Excel‑rooster en schrijf
  een waarde naar een Excel‑cel terwijl je het bijgewerkte bestand opslaat. Leer hoe
  je een rechtermuisklik‑menu maakt en de celwaarde bijwerkt in Python‑stijl.
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: nl
og_description: Voeg een aangepast contextmenu toe in Python om een waarde naar een
  Excel-cel te schrijven en het bijgewerkte Excel‑bestand op te slaan. Deze gids leidt
  je door het maken van een rechtermuisklikmenu met GridJs.
og_title: Aangepaste contextmenu toevoegen in Python – Stapsgewijze tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu to a Python Excel grid and write value to excel
    cell while saving the updated file. Learn to create right‑click menu and update
    cell value python style.
  headline: Add Custom Context Menu in Python – Complete Guide
  type: TechArticle
tags:
- Python
- Excel Automation
- GridJs
- Context Menu
title: Aangepast contextmenu toevoegen in Python – Complete gids
url: /nl/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Voeg Aangepast Contextmenu toe in Python – Complete Gids

Heb je je ooit afgevraagd hoe je **aangepast contextmenu toevoegen** items kunt toevoegen aan een spreadsheet‑rooster dat je vanuit Python serveert? Misschien heb je een snelle “Mark as Reviewed”‑knop nodig die verschijnt wanneer een gebruiker met de rechtermuisknop op een cel klikt, een waarde naar de Excel‑cel schrijft, en vervolgens de bijgewerkte werkmap opslaat—alles zonder de web‑UI te verlaten.  

In deze tutorial bouwen we precies dat: een **aangepast rechtermuisklikmenu** aangedreven door GridJs, een server‑side handler die **waarde naar excel‑cel schrijft**, en een laatste stap die **bijgewerkt excel‑bestand opslaat** op schijf. Aan het einde heb je een herbruikbaar patroon dat je in elk Flask-, FastAPI- of Django‑project kunt gebruiken.

> **Waarom zou je dit willen?**  
> Het toevoegen van een aangepast contextmenu stroomlijnt data‑review‑workflows, vermindert handmatig copy‑pasten, en geeft eindgebruikers een native‑gevoel ervaring direct binnen het rooster. Bovendien zie je hoe je **celwaarde python‑stijl bijwerkt**, wat een essentiële vaardigheid is voor elke Excel‑automatiseringstaak.

## Vereisten

- Python 3.9+ (de code werkt ook op 3.10)  
- `openpyxl` voor Excel‑bestandsafhandeling  
- `gridjs` Python‑wrapper (of de JS‑bibliotheek als je de front‑end verkiest)  
- Een basis web‑framework (Flask‑voorbeeld getoond)  
- Een werkmap‑bestand genaamd `sample.xlsx` in je projectmap  

Als je een van deze mist, voer dan uit:

```bash
pip install openpyxl flask gridjs
```

Laten we nu duiken.

---

## Stap 1 – Voeg Aangepast Contextmenu toe: Initialiseer GridJs en Koppel Werkblad

Het eerste wat je moet doen is een `GridJs`‑instance opzetten en deze wijzen op het werkblad waarmee je wilt werken. Hier verschijnt voor het eerst de **add custom context menu**‑zin in onze code, en het zet de basis voor alles wat volgt.

```python
# step_1_initialize.py
import openpyxl
from gridjs import GridJs

# Load the workbook – this could be any .xlsx file you own
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]                     # Grab the sheet you’ll display

# Create the GridJs object and bind it to the worksheet
grid = GridJs()
grid.set_worksheet(ws)                # <-- add custom context menu works on this sheet
```

**Wat gebeurt er?**  
`grid.set_worksheet(ws)` vertelt GridJs om de data van `ws` als gegevensbron te gebruiken. Vanaf nu zullen alle context‑menu‑aanpassingen die we toevoegen automatisch hetzelfde werkblad targeten, waardoor de UI en het bestand gesynchroniseerd blijven.

> **Pro tip:** Houd je werkmap slechts één keer open in lees‑/schrijvingsmodus. Het herhaaldelijk openen binnen een request‑handler kan bestandsvergrendelingsproblemen veroorzaken op Windows.

## Stap 2 – Schrijf Waarde naar Excel‑Cel: Definieer de Actie voor het Menu‑Item

Nu het rooster klaar is, moeten we **write value to excel cell** uitvoeren wanneer de gebruiker ons aangepaste commando selecteert. We voegen een menu‑item toe genaamd “Mark as Reviewed” en geven het een identifier `markReviewed`. De identifier is wat de client‑side JavaScript terugstuurt naar de server.

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**Waarom een aangepaste identifier gebruiken?**  
De identifier ontkoppelt UI‑tekst van serverlogica, waardoor je het label kunt wijzigen zonder de backend‑code aan te passen. Het maakt ook de **create right‑click menu**‑operatie expliciet en herbruikbaar.

## Stap 3 – Maak Rechtermuisklikmenu: Registreer de Server‑Side Handler

Met het menu‑item op zijn plaats moeten we GridJs vertellen wat te doen wanneer de gebruiker erop klikt. Hier implementeren we de **create right‑click menu**‑functionaliteit die daadwerkelijk een request terugstuurt naar Python.

```python
# step_3_handler.py
def on_custom_command(request):
    """
    Server‑side handler for the 'markReviewed' custom command.
    It receives a JSON payload like {"cell": "C12"}.
    """
    # Extract the cell address from the incoming request
    cell_address = request["cell"]           # e.g., "C12"

    # Write the word "Reviewed" into that cell
    ws[cell_address] = "Reviewed"            # <-- write value to excel cell

    # Persist the change to disk (see next step)
    # We'll return a simple JSON response to the client
    return {"status": "ok"}
```

Enkele zaken om op te merken:

1. **`ws[cell_address] = "Reviewed"`** is de meest eenvoudige manier om **update cell value python** uit te voeren. Onder de motorkap vertaalt `openpyxl` het A1‑style adres naar rij‑/kolom‑indices.
2. De handler retourneert een kleine JSON‑payload. GridJs verwacht een statusindicator; je kunt dit uitbreiden met foutmeldingen indien nodig.

Nu binden we de identifier aan de handler:

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**Wat als de cel leeg of beschermd is?**  
- Lege cellen zijn geen probleem—`openpyxl` maakt ze on-the-fly aan.  
- Voor beschermde bladen moet je eerst de bescherming opheffen (`ws.protection.sheet = False`) of een `PermissionError` afvangen.

## Stap 4 – Celwaarde Python Bijwerken: Sla de Wijziging Op door de Werkmap op te slaan

Een waarde schrijven is slechts de helft van het verhaal; je moet **save updated excel file** uitvoeren zodat de wijziging behouden blijft na de huidige sessie. Hier ronden we de reis van UI naar schijf af.

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**Waarom een aparte map?**  
Opslaan in een `output/`‑directory houdt de originele template onaangetast, wat nuttig is voor audit‑trails. Pas het pad aan om overeen te komen met je implementatie‑omgeving.

> **Let op:** Als je veel gelijktijdige gebruikers bedient, overweeg dan een thread‑safe lock (`threading.Lock`) rond `wb.save()` te gebruiken om race‑conditions te voorkomen.

## Stap 5 – Genereer Client‑Configuratie‑JSON en Koppel Alles Samen

Tot slot moeten we de JSON genereren die de front‑end GridJs‑instance zal gebruiken. Deze JSON bevat de werkblad‑data **en** de definitie van het aangepaste menu.

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

Wanneer je `config_json` in je HTML‑pagina opneemt, zal GridJs het rooster renderen met de “Mark as Reviewed”‑optie die rechts‑klikken op elke cel mogelijk maakt.

### Volledig Flask‑voorbeeld

Hieronder staat een minimale Flask‑app die alle onderdelen samenbrengt. Voer hem uit, open `http://localhost:5000` en klik met de rechtermuisknop op een willekeurige cel om het aangepaste menu in actie te zien.

```python
# app.py
from flask import Flask, request, jsonify, render_template_string
import openpyxl
from gridjs import GridJs

app = Flask(__name__)

# Load workbook once at startup
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]
grid = GridJs()
grid.set_worksheet(ws)

# ---- Add custom context menu item ----
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed",
    "icon": "check_circle"
})

# ---- Server‑side handler ----
def on_custom_command(req):
    cell = req["cell"]
    ws[cell] = "Reviewed"
    wb.save("output/sample-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", on_custom_command)

# ---- Routes ----
@app.route("/")
def index():
    config = grid.get_client_config()
    # Simple inline template; in production use a separate .html file
    html = f"""
    <!doctype html>
    <html>
      <head>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
      </head>
      <body>
        <div id="wrapper"></div>
        <script>
          const config = {config};
          new gridjs.Grid(config).render(document.getElementById("wrapper"));
        </script>
      </body>
    </html>
    """
    return render_template_string(html)

@app.route("/custom-command", methods=["POST"])
def custom_command():
    payload = request.get_json()
    result = on_custom_command(payload)
    return jsonify(result)

if __name__ == "__main__":
    app.run(debug=True)
```

**Verwacht resultaat:**  
- Klik met de rechtermuisknop op een cel → “Mark as Reviewed” verschijnt.  
- Klik erop → de celinhoud verandert naar “Reviewed”.  
- De werkmap `output/sample-updated.xlsx` bevat nu de nieuwe waarde.

## Veelgestelde Vragen & Randgevallen

| Vraag | Antwoord |
|----------|--------|
| *Wat als ik meerdere aangepaste acties nodig heb?* | Voeg gewoon meer objecten toe aan `grid.settings.context_menu.custom_items` en registreer elk met zijn eigen identifier. |
| *Kan ik extra data (bijv. rij‑ID) naar de handler doorgeven?* | Ja. Voeg extra sleutels toe aan de JSON‑payload aan de client‑kant, en lees ze vervolgens uit `request` in `on_custom_command`. |
| *Is deze aanpak compatibel met async‑frameworks?* | Zeker—maak `on_custom_command` gewoon een async‑functie en gebruik `await wb.save(...)` als je overschakelt naar `aiofiles` of iets dergelijks. |
| *Hoe style ik het menu‑icoon?* | Geef een Material‑Icons‑naam op (`"icon": "edit"`). De front‑end laadt automatisch het icoonlettertype. |
| *Wat te doen met grote werkmappen?* | Laad alleen het benodigde blad, en overweeg om rijen te streamen met `openpyxl.iter_rows()` om het geheugenverbruik te beperken. |

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Behoud Enkel Aanhalingsteken Prefix van Celwaarde of Bereik in Excel](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Behoud Enkel Aanhalingsteken Prefix van Celwaarde of Bereik in Excel](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Behoud Enkel Aanhalingsteken Prefix van Celwaarde of Bereik in Excel](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}