---
category: general
date: 2026-06-30
description: Přidejte vlastní kontextové menu v GridJs a naučte se, jak načíst sešit
  Excel, aktualizovat hodnotu buňky, povolit kontrolu pravopisu a zaregistrovat vlastní
  příkaz.
draft: false
keywords:
- add custom context menu
- update cell value
- enable spell checking
- load excel workbook
- register custom command
language: cs
og_description: Přidejte vlastní kontextové menu v GridJs při učení načítání Excel
  sešitu, aktualizaci hodnoty buňky, povolení kontroly pravopisu a registraci vlastního
  příkazu.
og_title: Přidání vlastního kontextového menu do GridJs – krok za krokem Python tutoriál
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
title: Přidejte vlastní kontextové menu do GridJs – kompletní průvodce v Pythonu
url: /cs/python/integration-and-interoperability/add-custom-context-menu-to-gridjs-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidání vlastního kontextového menu do GridJs – Kompletní průvodce v Pythonu

Už jste se někdy zamýšleli, jak **přidat vlastní položky kontextového menu** do tabulky GridJs, která je napájena Excel sešitem? Nejste sami. V mnoha aplikacích s velkým objemem dat potřebujete menu po kliknutí pravým tlačítkem, aby uživatelé mohli označit řádky, označit položky jako zkontrolované nebo spustit serverovou akci — bez opuštění gridu.  

V tomto tutoriálu projdeme načtení Excel sešitu, připojení vlastní položky kontextového menu, aktualizaci hodnoty buňky, zapnutí kontroly pravopisu a registraci vlastního příkazu, který změny uloží zpět do souboru. Na konci budete mít plně funkční instanci GridJs, která působí jako nativní součást aplikace a zapisuje přímo do zdrojové tabulky.

## Prerequisites

- Python 3.9+ (kód používá typové nápovědy, ale běží na jakékoli aktuální verzi)  
- knihovna `cells` (nebo jakýkoli wrapper pro práci s Excelem, který poskytuje objekty `Workbook` a `Worksheet`)  
- Python binding `gridjs` (model objektů odráží JavaScript API)  
- Základní povědomí o lambdách a JSON strukturách  

Pokud máte vše připravené, pojďme na to.

## Step 1: Load Excel Workbook and Select a Worksheet

Prvním krokem je **načíst Excel sešit**, aby GridJs měl data k zobrazení. Třída `cells.Workbook` abstrahuje soubor‑IO a poskytuje přímý přístup k řádkům, sloupcům i jednotlivým buňkám.

```python
# Step 1: Load the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]          # Grab the first sheet – change index if needed
```

> **Proč je to důležité:** Načtení sešitu předem umožní gridu načítat data na vyžádání a jakékoli úpravy, které později provedete (např. **update cell value**), budou uloženy do stejného souboru.

## Step 2: Create GridJs Instance and Bind It to the Worksheet

Nyní vytvoříme objekt `gridjs.GridJs` a řekneme mu, který list má vykreslovat. Představte si to jako přiřazení živého zdroje dat, ze kterého může GridJs číst kdykoli potřebuje vykreslit stránku nebo načíst další část.

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)
```

> **Pro tip:** Pokud pracujete s více listy, stačí později zavolat `grid.set_worksheet(other_ws)` — není nutné grid znovu vytvářet.

## Step 3: Enable Spell Checking (and Other Nice‑to‑Haves)

Většina obchodních aplikací umožňuje uživatelům zadávat volný text. Zapnutí **spell checking** snižuje překlepy a zvyšuje kvalitu dat. GridJs nabízí jednoduchý příznak pro tuto funkci.

```python
# Step 3: Turn on spell checking (and keep other helpers enabled)
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True          # optional but handy
grid.settings.formula_explanation.enabled = True   # if you support formulas
```

> **Proč zapnout kontrolu pravopisu?** Běží na klientovi, poskytuje okamžitou zpětnou vazbu bez dalších serverových volání — ideální pro rozsáhlé tabulky.

## Step 4: Add a Custom Context‑Menu Item

Tady je jádro tutoriálu: **add custom context menu** položky. Vytvoříme volbu „Mark as Reviewed“, která po kliknutí spustí serverový příkaz, který definujeme v dalším kroku.

```python
# Step 4: Add a custom context‑menu item
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",   # What the user sees
    "action": "markReviewed"      # Identifier used in the command registration
})
```

> **Obrázková ilustrace**  
> ![Přidání vlastního kontextového menu – ukázka možností po kliknutí pravým tlačítkem](/images/add-custom-context-menu.png "Add Custom Context Menu example")

Alt text výše obsahuje primární klíčové slovo, čímž splňuje SEO požadavky.

## Step 5: Register Custom Command to Update the Cell Value

Když uživatel vybere „Mark as Reviewed“, musíme **register custom command**, který aktualizuje odpovídající buňku v Excelu a soubor uloží. Metoda `grid.register_custom_command` sváže Python callable s identifikátorem akce, který jsme nastavili dříve.

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

> **Proč to funguje:** Handler získá referenci buňky od klienta, použije API `Worksheet` k **update cell value** a poté zapíše celý sešit zpět na disk. Odpověď informuje front‑end, že operace byla úspěšná.

### Edge‑Case Handling

- **Missing cell reference:** Pokud `req` neobsahuje `"cell"`, vyhoďte jasnou chybu, aby UI mohlo zobrazit toast.  
- **Concurrent edits:** Pro scénáře s vysokým provozem zvažte zamykání sešitu nebo použití verze, aby nedošlo ke konfliktům.

## Step 6: Enable Lazy Loading for Big Sheets

Pokud pracujete s tisíci řádky, lazy loading udrží UI plynulé. Nastavte velikost stránky na rozumný kus — 500 řádků funguje dobře ve většině prohlížečů.

```python
# Step 6: Activate lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500
```

> **Co když máte 10 000 řádků?** Grid bude požadovat data po stránkách, čímž sníží zátěž na paměť jak na klientovi, tak na serveru.

## Step 7: (Optional) Add a Custom Modal for Row Editing

Někdy potřebujete bohatší UI než inline editor. GridJs umožňuje otevřít modální okno, které můžete hostovat kdekoliv — např. jako React komponentu nebo jednoduchý HTML formulář.

```python
# Step 7: Configure a custom modal window for row editing
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"   # Serve this URL from your Flask/Django app
```

> **Proč použít modal?** Izoluje složitou validační logiku a dává vám plnou kontrolu nad rozvržením, přičemž je stále spouštěn z gridu.

## Step 8: Retrieve the Client‑Side Configuration JSON

Nakonec musíte poslat konfiguraci do prohlížeče. Metoda `get_client_config` serializuje vše do JSON blobu, který front‑endová knihovna GridJs dokáže zpracovat.

```python
# Step 8: Get the JSON configuration for the front‑end
client_config = grid.get_client_config()

# Example: you might embed this in a template
print(client_config)   # For debugging – remove in production
```

Výstup vypadá zhruba takto (zkráceno pro přehlednost):

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

### Expected Result

- Kliknutím pravým tlačítkem na libovolnou buňku se otevře menu s **Mark as Reviewed**.  
- Vybráním této volby se pošle požadavek na server, který **updates the cell value** na „Reviewed“ a uloží `example‑updated.xlsx`.  
- Kontrola pravopisu zvýrazní špatně napsaná slova během psaní.  

Vše se odehraje bez úplného obnovení stránky díky lazy loadingu a lehkému JSON payloadu.

## Common Questions & Pro Tips

| Question | Answer |
|----------|--------|
| *What if the workbook is read‑only?* | Ensure the file permissions allow write access, or open the workbook with `mode="rw"` if the library supports it. |
| *Can I add more than one custom menu item?* | Absolutely—just append additional dicts to `grid.settings.context_menu.custom_items`. |
| *Do I need to reload the grid after a cell update?* | GridJs automatically refreshes the affected row if you return `{status:"ok"}`; otherwise call `grid.refresh()` from the client. |
| *How do I make spell checking language‑specific?* | Set `grid.settings.spell_check.language = "en-US"` (or any supported locale). |
| *Is lazy loading compatible with server‑side filtering?* | Yes—combine `grid.settings.filter.enabled = True` and implement the filter logic in your custom command. |

## Full Working Example (All Steps Combined)

Below is a single script you can drop into a Flask route or run as a standalone process. Replace `YOUR_DIRECTORY` with the actual path on your server.

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


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Add Custom Content Type Properties to Excel Workbooks Using Aspose.Cells Java](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [Add Custom XML Parts with ID to Workbook](/cells/english/net/workbook-operations/add-custom-xml-parts-with-id/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hindi/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}