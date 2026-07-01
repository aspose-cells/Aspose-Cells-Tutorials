---
category: general
date: 2026-06-30
description: Adj hozzá egy egyéni helyi menüt egy Python Excel rácshoz, és írj értéket
  az Excel cellába, miközben mented a frissített fájlt. Tanulj meg jobb‑kattintásos
  menüt létrehozni és a cella értékét Python‑stílusban frissíteni.
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: hu
og_description: Adj hozzá egy egyéni helyi menüt Pythonban, amely értéket ír az Excel
  cellába, és elmenti a frissített Excel fájlt. Ez az útmutató végigvezet a jobb‑kattintásos
  menü létrehozásán a GridJs segítségével.
og_title: Egyéni kontextus menü hozzáadása Pythonban – Lépésről lépésre útmutató
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
title: Egyedi helyi menü hozzáadása Pythonban – Teljes útmutató
url: /hu/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Egyéni helyi menü hozzáadása Pythonban – Teljes útmutató

Gondolkodtál már azon, hogyan **adj hozzá egyéni helyi menüt** a Pythonból kiszolgált táblázat‑rácshoz? Lehet, hogy szükséged van egy gyors „Mark as Reviewed” (Megjelölés felülvizsgáltként) gombra, amely megjelenik, amikor a felhasználó jobb‑kattint egy cellára, beír egy értéket az Excel‑cellába, majd elmenti a frissített munkafüzetet – mindezt anélkül, hogy elhagynád a webes felületet.  

Ebben az útmutatóban pontosan ezt fogjuk megépíteni: egy **egyéni jobb‑kattintás menüt** a GridJs által, egy szerver‑oldali kezelőt, amely **értéket ír az excel cellába**, és egy végső lépést, amely **elmenti a frissített excel fájlt** a lemezen. A végére egy újrahasználható mintát kapsz, amelyet bármely Flask, FastAPI vagy Django projektbe beilleszthetsz.

> **Miért fontos?**  
> Egy egyéni helyi menü hozzáadása egyszerűsíti az adat‑felülvizsgálati munkafolyamatokat, csökkenti a kézi másolás‑beillesztés szükségességét, és natív érzetű élményt nyújt a végfelhasználóknak közvetlenül a rácson belül. Emellett megmutatjuk, hogyan **frissíts cellaértéket python**‑stílusban, ami alapvető készség minden Excel‑automatizálási feladathoz.

## Előkövetelmények

- Python 3.9+ (a kód 3.10‑en is működik)  
- `openpyxl` az Excel‑fájlok kezeléséhez  
- `gridjs` Python csomag (vagy a JS könyvtár, ha a front‑endet részesíted előnyben)  
- Egy alap webkeretrendszer (Flask példa megjelenítve)  
- Egy `sample.xlsx` nevű munkafüzet a projekt mappádban  

Ha valamelyik hiányzik, futtasd:

```bash
pip install openpyxl flask gridjs
```

Most merüljünk el benne.

---

## 1. lépés – Egyéni helyi menü hozzáadása: GridJs inicializálása és munkalap kötése

Az első dolog, amit tenned kell, egy `GridJs` példány létrehozása, és a használni kívánt munkalapra mutatása. Itt jelenik meg először a **add custom context menu** kifejezés a kódban, és ez állítja be a színpadot a többi számára.

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

**Mi történik?**  
`grid.set_worksheet(ws)` azt mondja a GridJs‑nek, hogy a `ws` adatait használja adatforrásként. Ettől kezdve minden általunk hozzáadott helyi‑menü módosítás automatikusan ugyanarra a munkalapra irányul, így a felhasználói felület és a fájl szinkronban marad.

> **Pro tipp:** Tartsd a munkafüzetet csak egyszer nyitva olvasás/írás módban. Ha egy kéréskezelőben többször nyitod meg, fájl‑zárolási problémákat okozhat Windows-on.

---

## 2. lépés – Érték írása Excel‑cellába: A menüpont műveletének meghatározása

Most, hogy a rács készen áll, **értéket kell írni az excel cellába**, amikor a felhasználó kiválasztja az egyéni parancsunkat. Hozzáadunk egy „Mark as Reviewed” nevű menüelemet, és egy `markReviewed` azonosítót adunk neki. Az azonosító az, amit a kliens‑oldali JavaScript visszaküld a szervernek.

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**Miért használjunk egyedi azonosítót?**  
Az azonosító leválasztja a UI szöveget a szerver logikától, lehetővé téve a címke módosítását a backend kód érintése nélkül. Emellett a **create right‑click menu** műveletet egyértelművé és újrahasználhatóvá teszi.

---

## 3. lépés – Jobb‑kattintás menü létrehozása: Szerver‑oldali kezelő regisztrálása

A menüpont elkészülte után meg kell mondanunk a GridJs‑nek, mit tegyen, amikor a felhasználó rákattint. Itt jön a **create right‑click menu** funkció, amely ténylegesen kérést küld vissza a Python felé.

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

Néhány fontos megjegyzés:

1. **`ws[cell_address] = "Reviewed"`** a legegyszerűbb módja a **update cell value python**-nak. A háttérben a `openpyxl` az A1‑stílusú címet sor/oszlop indexekre alakítja.
2. A kezelő egy kis JSON terhet ad vissza. A GridJs egy állapotjelzőt vár; szükség esetén kibővítheted hibajelzésekkel.

Most kötjük az azonosítót a kezelőhöz:

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**Mi van, ha a cella üres vagy védett?**  
- Az üres cellák rendben vannak – a `openpyxl` létrehozza őket futás közben.  
- Védett munkalapok esetén előbb fel kell oldani a védelmet (`ws.protection.sheet = False`), vagy el kell kapni egy `PermissionError`‑t.

---

## 4. lépés – Cellaváltozás mentése Pythonban: A módosítás mentése a munkafüzetben

Egy érték írása csak a történet felét jelenti; **save updated excel file**-t kell végrehajtani, hogy a változás a jelenlegi munkamenet után is megmaradjon. Itt fejezzük be a UI‑tól a lemezig tartó körutat.

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**Miért külön mappa?**  
Az `output/` könyvtárba mentés megőrzi az eredeti sablont érintetlenül, ami hasznos az audit nyomvonalakhoz. Állítsd be az útvonalat a telepítési környezetednek megfelelően.

> **Figyelem:** Ha sok egyidejű felhasználót szolgálsz ki, fontold meg egy szálbiztos zárolás (`threading.Lock`) használatát a `wb.save()` körül, hogy elkerüld a versenyhelyzeteket.

---

## 5. lépés – Kliens konfigurációs JSON generálása és az egész összekapcsolása

Végül elő kell állítanunk a JSON‑t, amelyet a front‑end GridJs példány felhasznál. Ez a JSON tartalmazza a munkalap adatokat **és** az egyéni menü definícióját.

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

Ha beágyazod a `config_json`‑t a HTML oldaladba, a GridJs megjeleníti a rácsot a „Mark as Reviewed” bejegyzéssel, amely minden cellán jobb‑kattintásra elérhető.

### Teljes Flask példa

Az alábbiakban egy minimális Flask alkalmazás látható, amely az összes részt összeilleszti. Futtasd, nyisd meg a `http://localhost:5000` címet, és jobb‑kattints bármely cellára, hogy lásd az egyéni menüt működés közben.

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

**Várható eredmény:**  
- Jobb‑kattintás bármely cellára → megjelenik a “Mark as Reviewed”.  
- Kattints rá → a cella tartalma „Reviewed” lesz.  
- A `output/sample-updated.xlsx` munkafüzet most már tartalmazza az új értéket.

---

## Gyakori kérdések és széljegyek

| Kérdés | Válasz |
|----------|--------|
| *Mi van, ha több egyéni műveletre van szükségem?* | Csak adj hozzá több objektumot a `grid.settings.context_menu.custom_items`-hez, és regisztráld mindegyiket a saját azonosítójával. |
| *Át tudok adni extra adatot (pl. sor ID) a kezelőnek?* | Igen. Adj hozzá extra kulcsokat a JSON terheléshez a kliens oldalon, majd olvasd őket a `request`‑ből az `on_custom_command`‑ban. |
| *Ez a megközelítés kompatibilis az aszinkron keretrendszerekkel?* | Teljesen – csak tedd az `on_custom_command`‑ot aszinkron függvénnyé, és használj `await wb.save(...)`-t, ha `aiofiles`-ra vagy hasonlóra váltasz. |
| *Hogyan formázhatom a menü ikont?* | Adj meg bármely Material‑Icons nevet (`"icon": "edit"`). A front‑end automatikusan betölti az ikon betűkészletet. |
| *Mi a helyzet a nagy munkafüzetekkel?* | Töltsd be csak a szükséges lapot, és fontold meg a sorok streamelését a `openpyxl.iter_rows()`‑szel a memóriahasználat csökkentése érdekében. |

## Mit érdemes legközelebb tanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Egysoros idézőjel előtag megőrzése a cellaérték vagy tartomány Excelben](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Egysoros idézőjel előtag megőrzése a cellaérték vagy tartomány Excelben (német)](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Egysoros idézőjel előtag megőrzése a cellaérték vagy tartomány Excelben (francia)](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}