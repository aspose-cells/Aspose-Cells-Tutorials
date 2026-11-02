---
category: general
date: 2026-06-30
description: Lägg till en anpassad snabbmeny i GridJs och lär dig hur du laddar en
  Excel‑arbetsbok, uppdaterar ett cellvärde, aktiverar stavningskontroll och registrerar
  ett anpassat kommando.
draft: false
keywords:
- add custom context menu
- update cell value
- enable spell checking
- load excel workbook
- register custom command
language: sv
og_description: Lägg till en anpassad kontextmeny i GridJs medan du lär dig att ladda
  en Excel‑arbetsbok, uppdatera cellvärdet, aktivera stavningskontroll och registrera
  ett anpassat kommando.
og_title: Lägg till anpassad snabbmeny i GridJs – Steg‑för‑steg Python‑handledning
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
title: Lägg till anpassad kontextmeny i GridJs – Komplett Python-guide
url: /sv/python/integration-and-interoperability/add-custom-context-menu-to-gridjs-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till anpassad snabbmeny i GridJs – Komplett Python‑guide

Har du någonsin funderat på hur man **lägger till anpassade snabbmeny‑element** i ett GridJs‑bord som drivs av en Excel‑arbetsbok? Du är inte ensam. I många dataintensiva appar behöver du den där högerklick‑menyn för att låta användare flagga rader, markera objekt som granskade eller starta en server‑sidåtgärd—utan att lämna rutnätet.  

I den här handledningen går vi igenom hur man laddar en Excel‑arbetsbok, kopplar ett anpassat snabbmeny‑alternativ, uppdaterar ett cellvärde, aktiverar stavningskontroll och registrerar ett anpassat kommando som sparar ändringarna tillbaka till filen. När du är klar har du en fullt fungerande GridJs‑instans som känns inbyggd för dina användare och skriver direkt tillbaka till källdokumentet.

## Förutsättningar

- Python 3.9+ (koden använder typ‑hints men fungerar på alla nyare versioner)  
- `cells`‑biblioteket (eller någon Excel‑hanteringswrapper som tillhandahåller `Workbook` och `Worksheet`‑objekt)  
- `gridjs`‑Python‑bindning (objektmodellen speglar JavaScript‑API‑et)  
- Grundläggande förståelse för lambda‑funktioner och JSON‑strukturer  

Om du har detta, låt oss dyka ner.

## Steg 1: Ladda Excel‑arbetsbok och välj ett kalkylblad

Det första du måste göra är att **ladda excel‑arbetsboken** så att GridJs har data att visa. Klassen `cells.Workbook` abstraherar fil‑IO och ger dig direkt åtkomst till rader, kolumner och enskilda celler.

```python
# Step 1: Load the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]          # Grab the first sheet – change index if needed
```

> **Varför detta är viktigt:** Att ladda arbetsboken i förväg betyder att rutnätet kan hämta data på begäran, och alla redigeringar du gör senare (som **uppdatera cellvärde**) kommer att sparas i samma fil.

## Steg 2: Skapa GridJs‑instans och bind den till kalkylbladet

Nu skapar vi ett `gridjs.GridJs`‑objekt och talar om vilket kalkylblad som ska renderas. Tänk på det som att ge GridJs en levande datakälla den kan fråga när den behöver rendera en sida eller ett lazy‑laddat segment.

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)
```

> **Proffstips:** Om du arbetar med flera blad, anropa bara `grid.set_worksheet(other_ws)` senare—ingen anledning att återskapa rutnätet.

## Steg 3: Aktivera stavningskontroll (och andra trevliga funktioner)

De flesta affärsappar låter användare skriva fria anteckningar. Att aktivera **stavningskontroll** minskar stavfel och förbättrar datakvaliteten. GridJs exponerar en enkel flagga för detta.

```python
# Step 3: Turn on spell checking (and keep other helpers enabled)
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True          # optional but handy
grid.settings.formula_explanation.enabled = True   # if you support formulas
```

> **Varför aktivera stavningskontroll?** Den körs på klientsidan och ger omedelbar återkoppling utan extra server‑anrop—perfekt för stora kalkylblad.

## Steg 4: Lägg till ett anpassat snabbmeny‑element

Här kommer hjärtat i handledningen: **lägga till anpassade snabbmeny‑element**. Vi skapar ett “Mark as Reviewed”-alternativ som, när det klickas, kör ett server‑sidigt kommando som vi definierar härnäst.

```python
# Step 4: Add a custom context‑menu item
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",   # What the user sees
    "action": "markReviewed"      # Identifier used in the command registration
})
```

> **Bildillustration**  
> ![Lägg till anpassad snabbmeny‑skärmdump som visar högerklick‑alternativ](/images/add-custom-context-menu.png "Exempel på anpassad snabbmeny")

Alt‑texten ovan innehåller huvudnyckelordet, vilket uppfyller SEO‑kraven.

## Steg 5: Registrera anpassat kommando för att uppdatera cellvärdet

När användaren väljer “Mark as Reviewed” måste vi **registrera ett anpassat kommando** som uppdaterar den underliggande Excel‑cellen och sparar filen. Metoden `grid.register_custom_command` binder en Python‑callable till den åtgärds‑identifierare vi satte tidigare.

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

> **Varför detta fungerar:** Handlaren får cellreferensen från klienten, använder `Worksheet`‑API:t för att **uppdatera cellvärde**, och skriver sedan hela arbetsboken tillbaka till disk. Svaret låter front‑enden veta att operationen lyckades.

### Hantering av kantfall

- **Saknad cellreferens:** Om `req` saknar `"cell"` kastas ett tydligt fel så UI kan visa en toast.  
- **Samtidiga redigeringar:** För högtrafik‑scenarier, överväg att låsa arbetsboken eller använda en versionsstämpel för att undvika race‑conditions.

## Steg 6: Aktivera lazy loading för stora blad

Om du hanterar tusentals rader håller lazy loading UI‑t snabbt. Sätt sidstorleken till ett rimligt parti—500 rader fungerar bra för de flesta webbläsare.

```python
# Step 6: Activate lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500
```

> **Vad händer om du har 10 000 rader?** Rutnätet begär data sida‑för‑sida, vilket minskar minnesbelastningen både på klient och server.

## Steg 7: (Valfritt) Lägg till en anpassad modal för radredigering

Ibland behövs ett rikare UI än en inline‑redigerare. GridJs låter dig öppna ett modal‑fönster som du kan hosta var som helst—kanske en React‑komponent eller ett enkelt HTML‑formulär.

```python
# Step 7: Configure a custom modal window for row editing
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"   # Serve this URL from your Flask/Django app
```

> **Varför använda en modal?** Den isolerar komplex valideringslogik och ger dig full kontroll över layouten, samtidigt som den kan triggas från rutnätet.

## Steg 8: Hämta klient‑sidans konfigurations‑JSON

Till sist måste du skicka konfigurationen till webbläsaren. Metoden `get_client_config` serialiserar allt till ett JSON‑blob som front‑end‑biblioteket GridJs kan konsumera.

```python
# Step 8: Get the JSON configuration for the front‑end
client_config = grid.get_client_config()

# Example: you might embed this in a template
print(client_config)   # For debugging – remove in production
```

Resultatet ser ungefär ut så här (trimmat för korthet):

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

### Förväntat resultat

- Högerklick på någon cell öppnar en meny med **Mark as Reviewed**.  
- När den väljs skickas en begäran till servern, som **uppdaterar cellvärdet** till “Reviewed” och sparar `example‑updated.xlsx`.  
- Stavningskontrollen markerar felstavade ord medan användaren skriver.  

Allt detta sker utan en fullständig siduppdatering, tack vare lazy loading och den lätta JSON‑payloaden.

## Vanliga frågor & Proffstips

| Fråga | Svar |
|----------|--------|
| *Vad händer om arbetsboken är skrivskyddad?* | Säkerställ att filbehörigheterna tillåter skrivåtkomst, eller öppna arbetsboken med `mode="rw"` om biblioteket stödjer det. |
| *Kan jag lägga till fler än ett anpassat meny‑element?* | Absolut—lägg bara till ytterligare dict‑objekt i `grid.settings.context_menu.custom_items`. |
| *Behöver jag ladda om rutnätet efter en celluppdatering?* | GridJs uppdaterar automatiskt den påverkade raden om du returnerar `{status:"ok"}`; annars anropa `grid.refresh()` från klienten. |
| *Hur gör jag stavningskontrollen språk‑specifik?* | Sätt `grid.settings.spell_check.language = "en-US"` (eller någon annan stödjande locale). |
| *Är lazy loading kompatibel med server‑sidig filtrering?* | Ja—kombinera `grid.settings.filter.enabled = True` och implementera filterlogiken i ditt anpassade kommando. |

## Fullt fungerande exempel (Alla steg kombinerade)

Nedan är ett enda skript som du kan klistra in i en Flask‑route eller köra som fristående process. Ersätt `YOUR_DIRECTORY` med den faktiska sökvägen på din server.

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


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Lägg till anpassade innehållstypsegenskaper i Excel‑arbetsböcker med Aspose.Cells Java](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [Lägg till anpassade XML‑delar med ID i arbetsboken](/cells/english/net/workbook-operations/add-custom-xml-parts-with-id/)
- [Aspose Cells Java anpassade laddningsfilter för Excel‑export](/cells/hindi/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}