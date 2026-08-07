---
category: general
date: 2026-06-30
description: Lägg till en anpassad snabbmeny i ett Python‑Excel‑rutnät och skriv ett
  värde till en Excel‑cell samtidigt som du sparar den uppdaterade filen. Lär dig
  att skapa en högerklicksmeny och uppdatera cellvärdet i Python‑stil.
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: sv
og_description: Lägg till en anpassad kontextmeny i Python för att skriva ett värde
  till en Excel-cell och spara den uppdaterade Excel-filen. Den här guiden visar hur
  du skapar en högerklicksmeny med GridJs.
og_title: Lägg till anpassad kontextmeny i Python – Steg‑för‑steg‑handledning
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
title: Lägg till anpassad kontextmeny i Python – Komplett guide
url: /sv/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till anpassad snabbmeny i Python – Komplett guide

Har du någonsin undrat hur man **add custom context menu**-element till ett kalkylblads‑rutnät som du serverar från Python? Kanske du behöver en snabb “Mark as Reviewed”-knapp som dyker upp när en användare högerklickar på en cell, skriver ett värde till Excel‑cellen och sedan sparar den uppdaterade arbetsboken—utan att lämna webb‑UI:n.  

I den här handledningen kommer vi att bygga precis det: en **custom right‑click menu** driven av GridJs, en server‑side‑hanterare som **write(s) value to excel cell**, och ett sista steg som **save(s) updated excel file** på disk. I slutet har du ett återanvändbart mönster som du kan släppa in i vilket Flask-, FastAPI- eller Django‑projekt som helst.

> **Varför bry sig?**  
> Att lägga till en anpassad snabbmeny effektiviserar arbetsflöden för datagranskning, minskar manuellt kopierande och klistra in, och ger slutanvändare en native‑känsla direkt i rutnätet. Dessutom får du se hur man **update cell value python**‑style, vilket är en grundläggande färdighet för alla Excel‑automatiseringsuppgifter.

## Förutsättningar

- Python 3.9+ (koden fungerar även på 3.10)  
- `openpyxl` för Excel‑filhantering  
- `gridjs` Python‑wrapper (eller JS‑biblioteket om du föredrar front‑end)  
- Ett grundläggande webb‑ramverk (Flask‑exempel visas)  
- En arbetsbokfil med namnet `sample.xlsx` i din projektmapp  

Om du saknar någon av dessa, kör:

```bash
pip install openpyxl flask gridjs
```

Nu dyker vi ner.

---

## Steg 1 – Lägg till anpassad snabbmeny: Initiera GridJs och bind worksheet

Det allra första du behöver göra är att starta en `GridJs`‑instans och peka den mot det kalkylblad du planerar att arbeta med. Det är här frasen **add custom context menu** först dyker upp i vår kod, och den lägger grunden för allt annat.

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

**What’s happening?**  
`grid.set_worksheet(ws)` talar om för GridJs att använda data från `ws` som datakälla. Härifrån kommer alla kontext‑meny‑modifieringar vi lägger till automatiskt att rikta sig mot samma kalkylblad, vilket håller UI‑et och filen i synk.

> **Pro tip:** Håll din arbetsbok öppen i läs/skriv‑läge bara en gång. Att öppna den upprepade gånger i en request‑handler kan orsaka fil‑lås‑problem på Windows.

---

## Steg 2 – Skriv värde till Excel‑cell: Definiera åtgärden för menyalternativet

Nu när rutnätet är klart, måste vi **write value to excel cell** när användaren väljer vårt anpassade kommando. Vi kommer att lägga till ett menyalternativ som heter “Mark as Reviewed” och ge det en identifierare `markReviewed`. Identifieraren är vad klient‑side JavaScript kommer att skicka tillbaka till servern.

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**Why use a custom identifier?**  
Identifieraren kopplar loss UI‑texten från serverlogiken, vilket låter dig ändra etiketten utan att röra backend‑koden. Den gör också **create right‑click menu**‑operationen explicit och återanvändbar.

---

## Steg 3 – Skapa högerklick‑meny: Registrera server‑side‑hanteraren

Med menyalternativet på plats måste vi tala om för GridJs vad den ska göra när användaren klickar på det. Det är här vi **create right‑click menu**‑funktionaliteten som faktiskt skickar en förfrågan tillbaka till Python.

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

Några saker att notera:

1. **`ws[cell_address] = "Reviewed"`** är det mest enkla sättet att **update cell value python**. Under huven översätter `openpyxl` A1‑stil‑adressen till rad‑/kolumn‑index.
2. Hantern returnerar en liten JSON‑payload. GridJs förväntar sig en statusindikator; du kan expandera detta för att inkludera felmeddelanden om så behövs.

Nu binder vi identifieraren till hantern:

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**Vad händer om cellen är tom eller skyddad?**  
- Tomma celler är okej—`openpyxl` skapar dem automatiskt.  
- För skyddade blad måste du först avskydda (`ws.protection.sheet = False`) eller fånga ett `PermissionError`.

---

## Steg 4 – Uppdatera cellvärde i Python: Spara förändringen genom att spara arbetsboken

Att skriva ett värde är bara halva historien; du måste **save updated excel file** så att förändringen överlever bortom den aktuella sessionen. Det är här vi avslutar rundresan från UI till disk.

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**Varför en separat mapp?**  
Att spara i en `output/`‑katalog håller den ursprungliga mallen intakt, vilket är användbart för revisionsspår. Anpassa sökvägen så att den matchar din driftsmiljö.

> **Watch out:** Om du serverar många samtidiga användare, överväg att använda en trådsäker lås (`threading.Lock`) runt `wb.save()` för att undvika race‑conditions.

---

## Steg 5 – Generera klient‑konfigurations‑JSON och koppla ihop allt

Till sist måste vi producera JSON‑en som front‑end GridJs‑instansen kommer att konsumera. Denna JSON innehåller worksheet‑data **och** den anpassade menyddefinitionen.

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

När du bäddar in `config_json` i din HTML‑sida kommer GridJs att rendera rutnätet med “Mark as Reviewed”-alternativet högerklickbart på varje cell.

### Fullt Flask‑exempel

Nedan är en minimal Flask‑app som sätter ihop alla delarna. Kör den, öppna `http://localhost:5000` och högerklicka på någon cell för att se den anpassade menyn i aktion.

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

**Förväntat resultat:**  
- Högerklicka på någon cell → “Mark as Reviewed” visas.  
- Klicka på den → cellens innehåll ändras till “Reviewed”.  
- Arbetsboken `output/sample-updated.xlsx` innehåller nu det nya värdet.

---

## Vanliga frågor & edge‑cases

| Question | Answer |
|----------|--------|
| *Vad händer om jag behöver flera anpassade åtgärder?* | Lägg bara till fler objekt i `grid.settings.context_menu.custom_items` och registrera varje med sin egen identifierare. |
| *Kan jag skicka extra data (t.ex. rad‑ID) till hanteraren?* | Ja. Inkludera extra nycklar i JSON‑payloaden på klientsidan, och läs dem sedan från `request` i `on_custom_command`. |
| *Är detta tillvägagångssätt kompatibelt med async‑ramverk?* | Absolut—gör bara `on_custom_command` till en async‑funktion och använd `await wb.save(...)` om du byter till `aiofiles` eller liknande. |
| *Hur stylar jag menyikonen?* | Ange vilket Material‑Icons‑namn som helst (`"icon": "edit"`). Front‑end laddar automatiskt ikonteckensnittet. |
| *Vad händer med stora arbetsböcker?* | Läs bara in det blad som behövs, och överväg att strömma rader med `openpyxl.iter_rows()` för att hålla minnesanvändningen låg. |

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Bevara enkelfnutt‑prefix för cellvärde eller område i Excel](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Bevara enkelfnutt‑prefix för cellvärde eller område i Excel](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Bevara enkelfnutt‑prefix för cellvärde eller område i Excel](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}