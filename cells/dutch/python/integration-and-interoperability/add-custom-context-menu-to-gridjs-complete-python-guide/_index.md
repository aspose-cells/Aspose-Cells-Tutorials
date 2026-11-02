---
category: general
date: 2026-06-30
description: Voeg een aangepast contextmenu toe in GridJs en leer hoe je een Excel-werkmap
  laadt, een celwaarde bijwerkt, spellingcontrole inschakelt en een aangepast commando
  registreert.
draft: false
keywords:
- add custom context menu
- update cell value
- enable spell checking
- load excel workbook
- register custom command
language: nl
og_description: Voeg een aangepast contextmenu toe in GridJs terwijl je leert hoe
  je een Excel-werkmap laadt, een celwaarde bijwerkt, spellingcontrole inschakelt
  en een aangepast commando registreert.
og_title: Voeg aangepast contextmenu toe aan GridJs – Stapsgewijze Python‑tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu in GridJs and learn how to load Excel workbook,
    update cell value, enable spell checking, and register custom command.
  headline: Add Custom Context Menu to GridJs – Complete Python Guide
  type: TechArticle
tags:
- GridJs
- Python
- Excel Automation
title: Voeg aangepast contextmenu toe aan GridJs – Complete Python-gids
url: /nl/python/integration-and-interoperability/add-custom-context-menu-to-gridjs-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aangepast contextmenu toevoegen aan GridJs – Complete Python‑handleiding

Heb je je ooit afgevraagd hoe je **aangepaste contextmenu**‑items kunt toevoegen aan een GridJs‑tabel die wordt gevoed door een Excel‑werkmap? Je bent niet de enige. In veel data‑intensieve apps heb je dat rechtermuisklikmenu nodig om gebruikers rijen te laten markeren, items als beoordeeld te markeren, of een server‑side actie te starten—zonder de grid te verlaten.  

In deze tutorial lopen we stap voor stap door het laden van een Excel‑werkmap, het koppelen van een aangepast contextmenu‑item, het bijwerken van een celwaarde, het inschakelen van spellingscontrole, en het registreren van een aangepast commando dat wijzigingen terug naar het bestand schrijft. Aan het einde heb je een volledig functionerende GridJs‑instantie die natuurlijk aanvoelt voor je gebruikers en direct terugschrijft naar de bron‑spreadsheet.

## Vereisten

- Python 3.9+ (de code gebruikt type‑hints maar draait op elke recente versie)  
- `cells`‑bibliotheek (of een andere Excel‑verwerkingswrapper die `Workbook`‑ en `Worksheet`‑objecten biedt)  
- `gridjs` Python‑binding (het objectmodel spiegelt de JavaScript‑API)  
- Een basisbegrip van lambda‑functies en JSON‑structuren  

Als je die hebt, laten we erin duiken.

## Stap 1: Excel‑werkmap laden en een werkblad selecteren

Het eerste wat je moet doen is **een Excel‑werkmap laden** zodat GridJs data heeft om weer te geven. De `cells.Workbook`‑klasse abstraheert de bestands‑IO en geeft je directe toegang tot rijen, kolommen en individuele cellen.

```python
# Step 1: Load the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]          # Grab the first sheet – change index if needed
```

> **Waarom dit belangrijk is:** Het vooraf laden van de werkmap betekent dat de grid data op aanvraag kan ophalen, en eventuele bewerkingen die je later maakt (zoals **celwaarde bijwerken**) worden bewaard in hetzelfde bestand.

## Stap 2: GridJs‑instantie maken en koppelen aan het werkblad

Nu maken we een `gridjs.GridJs`‑object aan en geven we aan welk werkblad het moet renderen. Beschouw dit als het geven van een live gegevensbron aan GridJs die het kan raadplegen wanneer het een pagina of een lazy‑geladen deel moet weergeven.

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)
```

> **Pro‑tip:** Als je met meerdere bladen werkt, roep dan later gewoon `grid.set_worksheet(other_ws)` aan—geen noodzaak om de grid opnieuw te maken.

## Stap 3: Spellingscontrole inschakelen (en andere handige functies)

De meeste zakelijke apps laten gebruikers vrije notities typen. Het inschakelen van **spellingscontrole** vermindert typefouten en verbetert de datakwaliteit. GridJs biedt een eenvoudige vlag hiervoor.

```python
# Step 3: Turn on spell checking (and keep other helpers enabled)
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True          # optional but handy
grid.settings.formula_explanation.enabled = True   # if you support formulas
```

> **Waarom spellingscontrole inschakelen?** Het draait client‑side en geeft directe feedback zonder extra server‑aanvragen—perfect voor grootschalige sheets.

## Stap 4: Een aangepast contextmenu‑item toevoegen

Dit is het hart van de tutorial: **aangepaste contextmenu**‑items toevoegen. We maken een “Mark as Reviewed”‑optie die, bij klikken, een server‑side commando uitvoert dat we daarna definiëren.

```python
# Step 4: Add a custom context‑menu item
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",   # What the user sees
    "action": "markReviewed"      # Identifier used in the command registration
})
```

> **Image illustration**  
> ![Schermafbeelding van aangepast contextmenu die rechtermuisklikopties toont](/images/add-custom-context-menu.png "Voorbeeld van aangepast contextmenu")

De alt‑tekst hierboven bevat het primaire zoekwoord, wat voldoet aan de SEO‑vereisten.

## Stap 5: Aangepast commando registreren om de celwaarde bij te werken

Wanneer de gebruiker “Mark as Reviewed” selecteert, moeten we een **aangepast commando registreren** dat de onderliggende Excel‑cel bijwerkt en het bestand opslaat. De `grid.register_custom_command`‑methode bindt een Python‑callable aan de actie‑identifier die we eerder hebben ingesteld.

```python
# Step 5: Register the server‑side command that updates a cell value
def mark_reviewed_handler(req):
    """
    req is a dict containing at least:
        - 'cell': Excel address like "B5"
    This function writes "Reviewed" into the target cell and saves the workbook.
    """
    # Update the cell value
    ws.get_range(req["cell"]).put_value("Reviewed")
    
    # Persist changes back to disk
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    
    # Return a simple JSON response the client can interpret
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)
```

> **Waarom dit werkt:** De handler ontvangt de celreferentie van de client, gebruikt de `Worksheet`‑API om **celwaarde bij te werken**, en schrijft vervolgens de volledige werkmap terug naar de schijf. Het antwoord laat de front‑end weten dat de bewerking geslaagd is.

### Rand‑geval afhandeling

- **Ontbrekende celreferentie:** Als `req` geen `"cell"` bevat, gooi een duidelijke fout zodat de UI een toast kan tonen.  
- **Gelijktijdige bewerkingen:** Voor scenario's met veel verkeer, overweeg het vergrendelen van de werkmap of het gebruik van een versie‑stempel om race‑condities te voorkomen.

## Stap 6: Lazy loading inschakelen voor grote sheets

Als je te maken hebt met duizenden rijen, houdt lazy loading de UI responsief. Stel de paginagrootte in op een redelijk deel—500 rijen werkt goed voor de meeste browsers.

```python
# Step 6: Activate lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500
```

> **Wat als je 10 000 rijen hebt?** De grid vraagt data pagina‑voor‑pagina op, waardoor de geheugenbelasting op zowel client als server wordt verminderd.

## Stap 7: (Optioneel) Een aangepast modalvenster toevoegen voor rij‑bewerking

Soms heb je een rijkere UI nodig dan een inline editor. GridJs laat je een modaal venster openen dat je overal kunt hosten—bijvoorbeeld een React‑component of een simpel HTML‑formulier.

```python
# Step 7: Configure a custom modal window for row editing
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"   # Serve this URL from your Flask/Django app
```

> **Waarom een modal gebruiken?** Het isoleert complexe validatielogica en geeft je volledige controle over de lay-out, terwijl het nog steeds vanuit de grid wordt geactiveerd.

## Stap 8: De client‑side configuratie‑JSON ophalen

Tot slot moet je de configuratie naar de browser sturen. De `get_client_config`‑methode serialiseert alles naar een JSON‑blob die de front‑end GridJs‑bibliotheek kan gebruiken.

```python
# Step 8: Get the JSON configuration for the front‑end
client_config = grid.get_client_config()

# Example: you might embed this in a template
print(client_config)   # For debugging – remove in production
```

De output ziet er ongeveer zo uit (ingekort voor beknoptheid):

```json
{
  "worksheet": "example.xlsx",
  "settings": {
    "spell_check": {"enabled": true},
    "context_menu": {
      "custom_items": [
        {"text": "Mark as Reviewed", "action": "markReviewed"}
      ]
    },
    "lazy_load": {"enabled": true, "page_size": 500},
    "custom_modal": {
      "enabled": true,
      "title": "Edit Row Details",
      "url": "/row-editor.html"
    }
  }
}
```

### Verwacht resultaat

- Met rechtermuisklik op een cel wordt een menu geopend met **Mark as Reviewed**.  
- Het selecteren stuurt een verzoek naar de server, die de **celwaarde bijwerkt** naar “Reviewed” en `example‑updated.xlsx` opslaat.  
- Spellingscontrole markeert verkeerd gespelde woorden terwijl de gebruiker typt.  

Dit alles gebeurt zonder een volledige paginavernieuwing, dankzij lazy loading en de lichte JSON‑payload.

## Veelgestelde vragen & Pro‑tips

| Vraag | Antwoord |
|-------|----------|
| *Wat als de werkmap alleen‑lezen is?* | Zorg ervoor dat de bestandsrechten schrijfrechten toestaan, of open de werkmap met `mode="rw"` als de bibliotheek dat ondersteunt. |
| *Kan ik meer dan één aangepast menu‑item toevoegen?* | Zeker—voeg gewoon extra dicts toe aan `grid.settings.context_menu.custom_items`. |
| *Moet ik de grid opnieuw laden na een cel‑update?* | GridJs ververst automatisch de betreffende rij als je `{status:"ok"}` retourneert; anders roep `grid.refresh()` aan vanuit de client. |
| *Hoe maak ik spellingscontrole taalspecifiek?* | Stel `grid.settings.spell_check.language = "en-US"` in (of een andere ondersteunde locale). |
| *Is lazy loading compatibel met server‑side filtering?* | Ja—combineer `grid.settings.filter.enabled = True` en implementeer de filterlogica in je aangepaste commando. |

## Volledig werkend voorbeeld (Alle stappen gecombineerd)

Hieronder staat een enkel script dat je in een Flask‑route kunt plaatsen of als een zelfstandig proces kunt uitvoeren. Vervang `YOUR_DIRECTORY` door het daadwerkelijke pad op je server.

```python
import cells
import gridjs
from flask import Flask, request, jsonify, render_template_string

app = Flask(__name__)

# ---------- Initialization ----------
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]

grid = gridjs.GridJs()
grid.set_worksheet(ws)

# Enable helpers
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True
grid.settings.formula_explanation.enabled = True

# Lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500

# Custom context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed"
})

# Custom command implementation
def mark_reviewed_handler(req):
    cell_addr = req.get("cell")
    if not cell_addr:
        return {"status": "error", "message": "Cell address missing"}
    ws.get_range(cell_addr).put_value("Reviewed")
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)

# Optional modal
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"

client_config = grid.get_client_config()

# ---------- Flask Routes ----------
@app.route("/")
def index():
    # Simple page that injects the config into a <script> tag
    html = f"""
    <!doctype html>
    <html>
    <head>
        <title>GridJs Demo</title>
        <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
    </head>
    <body>
        <div id="grid"></div>
        <script>
            const config = {client_config};
            new gridjs.Grid(config).render(document.getElementById("grid"));
        </script>
    </body>
    </html>
    """
    return render_template_string(html)

@app.route("/command/<name>", methods=["POST"])
def command(name):


## Wat kun je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Aangepaste contenttype‑eigenschappen toevoegen aan Excel‑werkboeken met Aspose.Cells Java](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [Aangepaste XML‑onderdelen met ID toevoegen aan werkmap](/cells/english/net/workbook-operations/add-custom-xml-parts-with-id/)
- [Aspose Cells Java aangepaste laadfilters Excel‑export](/cells/hindi/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}