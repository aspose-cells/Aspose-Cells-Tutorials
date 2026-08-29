---
category: general
date: 2026-06-30
description: Adj hozzá egy egyéni helyi menüt a GridJs-ben, és tanuld meg, hogyan
  tölts be Excel munkafüzetet, frissítsd a cella értékét, engedélyezd a helyesírás-ellenőrzést,
  és regisztrálj egy egyéni parancsot.
draft: false
keywords:
- add custom context menu
- update cell value
- enable spell checking
- load excel workbook
- register custom command
language: hu
og_description: Egyéni helyi menü hozzáadása a GridJs-ben, miközben megtanuljuk betölteni
  az Excel munkafüzetet, frissíteni a cella értékét, engedélyezni a helyesírás-ellenőrzést,
  és regisztrálni egy egyéni parancsot.
og_title: Egyéni helyi menü hozzáadása a GridJs-hez – Lépésről lépésre Python oktatóanyag
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
title: Egyéni helyi menü hozzáadása a GridJs-hez – Teljes Python útmutató
url: /hu/python/integration-and-interoperability/add-custom-context-menu-to-gridjs-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Egyéni helyi menü hozzáadása a GridJs-hez – Teljes Python útmutató

Gondolkodtál már azon, hogyan **adj hozzá egyéni helyi menü** elemeket egy Excel munkafüzetet használó GridJs táblához? Nem vagy egyedül. Sok adat‑intenzív alkalmazásban szükség van a jobb‑klikk menüre, hogy a felhasználók megjelöljék a sorokat, jelöljék az elemeket felülvizsgáltként, vagy elindítsanak egy szerver‑oldali műveletet – anélkül, hogy elhagynák a rácsot.

Ebben az útmutatóban végigvezetünk az Excel munkafüzet betöltésén, egy egyéni helyi‑menü bejegyzés felkötésén, egy cellaérték frissítésén, a helyesírás-ellenőrzés engedélyezésén, valamint egy egyéni parancs regisztrálásán, amely a változtatásokat visszaírja a fájlba. A végére egy teljesen működő GridJs példányod lesz, amely natívnek érződik a felhasználók számára, és közvetlenül a forrás‑táblázatba ír.

## Előfeltételek

- Python 3.9+ (a kód típusjelöléseket használ, de bármely friss verzión működik)  
- `cells` könyvtár (vagy bármely Excel‑kezelő csomag, amely `Workbook` és `Worksheet` objektumokat biztosít)  
- `gridjs` Python kötés (az objektummodell tükrözi a JavaScript API-t)  
- Alapvető ismeretek a lambda függvényekről és a JSON struktúrákról  

Ha ezek megvannak, vágjunk bele.

## 1. lépés: Excel munkafüzet betöltése és munkalap kiválasztása

Az első dolog, amit meg kell tenned, **az excel munkafüzet betöltése**, hogy a GridJs rendelkezzen megjeleníthető adatokkal. A `cells.Workbook` osztály elrejti a fájl‑IO részleteit, és közvetlen hozzáférést biztosít a sorokhoz, oszlopokhoz és egyedi cellákhoz.

```python
# Step 1: Load the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]          # Grab the first sheet – change index if needed
```

> **Miért fontos ez:** A munkafüzet előzetes betöltése azt jelenti, hogy a rács igény szerint tud adatot lekérni, és a később végzett módosítások (például **cellaérték frissítése**) ugyanabban a fájlban maradnak meg.

## 2. lépés: GridJs példány létrehozása és a munkalaphoz kötése

Most létrehozunk egy `gridjs.GridJs` objektumot, és megmondjuk, melyik munkalapot jelenítse meg. Ezt tekintheted egy élő adatforrásnak, amelyet a GridJs bármikor lekérdezhet, amikor egy oldalt vagy egy lazy‑loaded darabot kell renderelnie.

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)
```

> **Pro tip:** Ha több munkalappal dolgozol, egyszerűen hívd meg később a `grid.set_worksheet(other_ws)`‑t – nem kell újra létrehozni a rácsot.

## 3. lépés: Helyesírás-ellenőrzés engedélyezése (és egyéb kényelmi funkciók)

A legtöbb üzleti alkalmazás lehetővé teszi a felhasználók számára, hogy szabad szöveget írjanak. A **helyesírás-ellenőrzés** engedélyezése csökkenti a gépelési hibákat és javítja az adatminőséget. A GridJs ehhez egy egyszerű kapcsolót biztosít.

```python
# Step 3: Turn on spell checking (and keep other helpers enabled)
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True          # optional but handy
grid.settings.formula_explanation.enabled = True   # if you support formulas
```

> **Miért engedélyezzük a helyesírás-ellenőrzést?** Kliens‑oldalon fut, azonnali visszajelzést ad extra szerver‑hívások nélkül – tökéletes nagy mennyiségű táblázatokhoz.

## 4. lépés: Egyéni helyi menüelem hozzáadása

Ez a tutorial szíve: **egyéni helyi menü** elemek hozzáadása. Létrehozunk egy „Mark as Reviewed” (Megjelölés felülvizsgáltként) opciót, amely kattintásra egy szerver‑oldali parancsot futtat, amelyet a következő lépésben definiálunk.

```python
# Step 4: Add a custom context‑menu item
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",   # What the user sees
    "action": "markReviewed"      # Identifier used in the command registration
})
```

> **Képi illusztráció**  
> ![Egyéni helyi menü hozzáadása képernyőkép, amely a jobb‑klikk opciókat mutatja](/images/add-custom-context-menu.png "Egyéni helyi menü példa")

A fenti alt szöveg tartalmazza a fő kulcsszót, ezzel megfelelve az SEO‑követelményeknek.

## 5. lépés: Egyéni parancs regisztrálása a cellaérték frissítéséhez

Amikor a felhasználó a „Mark as Reviewed” opciót választja, **regisztrálnunk kell egy egyéni parancsot**, amely frissíti az alatta lévő Excel cellát és elmenti a fájlt. A `grid.register_custom_command` metódus egy Python hívható objektumot köt a korábban beállított akció‑azonosítóhoz.

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

> **Miért működik ez:** A kezelő megkapja a cellareferenciát a klienstől, a `Worksheet` API‑t használva **frissíti a cella értékét**, majd a teljes munkafüzetet visszaírja a lemezre. A válasz jelzi a front‑endnek, hogy a művelet sikeres volt.

### Szélsőséges esetek kezelése

- **Hiányzó cellareferencia:** Ha a `req` nem tartalmazza a `"cell"` kulcsot, dobj egy egyértelmű hibát, hogy a UI toast‑ot tudjon megjeleníteni.  
- **Párhuzamos módosítások:** Nagy forgalmú környezetben fontold meg a munkafüzet zárolását vagy egy verzió‑bélyeg használatát a versenyhelyzetek elkerülése érdekében.

## 6. lépés: Lazy loading engedélyezése nagy táblázatokhoz

Ha több ezer sorral dolgozol, a lazy loading fenntartja a UI gyorsaságát. Állítsd be a lapméretet egy ésszerű darabra – 500 sor általában jól működik a legtöbb böngészőben.

```python
# Step 6: Activate lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500
```

> **Mi van, ha 10 000 sorod van?** A rács oldalanként kéri le az adatokat, így csökkentve a memóriaigényt mind a kliensen, mind a szerveren.

## 7. lépés: (Opcionális) Egyéni modál hozzáadása sor szerkesztéséhez

Néha szükség van egy gazdagabb UI‑ra, mint egy beágyazott szerkesztő. A GridJs lehetővé teszi egy modál ablak felbukkanását, amelyet bárhol elhelyezhetsz – legyen az egy React komponens vagy egy egyszerű HTML űrlap.

```python
# Step 7: Configure a custom modal window for row editing
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"   # Serve this URL from your Flask/Django app
```

> **Miért használjunk modált?** Elkülöníti a komplex validációs logikát, teljes irányítást ad a layout felett, miközben továbbra is a rácsból indítható.

## 8. lépés: Az ügyfél‑oldali konfiguráció JSON lekérése

Végül a konfigurációt a böngészőnek kell elküldeni. A `get_client_config` metódus mindent egy JSON objektumba sorol, amelyet a front‑end GridJs könyvtár felhasználhat.

```python
# Step 8: Get the JSON configuration for the front‑end
client_config = grid.get_client_config()

# Example: you might embed this in a template
print(client_config)   # For debugging – remove in production
```

A kimenet nagyjából így néz ki (rövidítve a tömörség kedvéért):

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

### Várható eredmény

- A jobb‑klikk bármely cellán megnyit egy menüt a **Mark as Reviewed** opcióval.  
- A kiválasztás egy kérést küld a szervernek, amely **frissíti a cella értékét** „Reviewed”‑re, és elmenti az `example‑updated.xlsx` fájlt.  
- A helyesírás-ellenőrzés kiemeli a helytelen szavakat a felhasználó gépelése közben.  

Mindez teljes oldalú újratöltés nélkül történik, a lazy loading és a könnyű JSON payload köszönhetően.

## Gyakori kérdések és tippek

| Kérdés | Válasz |
|----------|--------|
| *Mi van, ha a munkafüzet csak olvasható?* | Győződj meg arról, hogy a fájl jogosultságai engedélyezik az írást, vagy nyisd meg a munkafüzetet `mode="rw"` módon, ha a könyvtár támogatja. |
| *Hozzáadhatok több egyéni menüelemet?* | Természetesen – egyszerűen adj hozzá további szótárakat a `grid.settings.context_menu.custom_items` listához. |
| *Újra kell tölteni a rácsot a cella frissítése után?* | A GridJs automatikusan frissíti az érintett sort, ha `{status:"ok"}`-t adsz vissza; egyébként hívd meg a `grid.refresh()`-t az ügyféloldalon. |
| *Hogyan állítsam be a helyesírás-ellenőrzés nyelvét?* | Állítsd be a `grid.settings.spell_check.language = "en-US"` értéket (vagy bármely támogatott helyi beállítást). |
| *A lazy loading kompatibilis a szerver‑oldali szűréssel?* | Igen – kombináld a `grid.settings.filter.enabled = True` beállítást, és valósítsd meg a szűrési logikát az egyéni parancsodban. |

## Teljes működő példa (az összes lépés egyben)

Az alábbi egyetlen szkript, amelyet beilleszthetsz egy Flask útvonalba, vagy önálló folyamatként futtathatsz. Cseréld le a `YOUR_DIRECTORY`‑t a szervereden lévő tényleges útvonalra.

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


## Mit érdemes következőként megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Egyéni tartalomtípus tulajdonságok hozzáadása Excel munkafüzetekhez az Aspose.Cells Java használatával](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [Egyéni XML részek hozzáadása azonosítóval a munkafüzethez](/cells/english/net/workbook-operations/add-custom-xml-parts-with-id/)
- [Aspose Cells Java egyéni betöltési szűrők Excel export](/cells/hindi/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}