---
category: general
date: 2026-06-30
description: Přidejte vlastní kontextové menu do Python Excel mřížky a při ukládání
  aktualizovaného souboru zapište hodnotu do buňky Excelu. Naučte se vytvořit menu
  po kliknutí pravým tlačítkem a aktualizovat hodnotu buňky v pythonovém stylu.
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: cs
og_description: Přidejte vlastní kontextové menu v Pythonu, které zapíše hodnotu do
  buňky Excelu a uloží aktualizovaný soubor Excel. Tento průvodce vás provede vytvořením
  pravým tlačítkem myši menu pomocí GridJs.
og_title: Přidání vlastního kontextového menu v Pythonu – návod krok za krokem
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
title: Přidání vlastního kontextového menu v Pythonu – kompletní průvodce
url: /cs/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidání vlastního kontextového menu v Pythonu – Kompletní průvodce

Už jste se někdy zamysleli, jak **přidat vlastní kontextové menu** položky do mřížky tabulky, kterou poskytujete z Pythonu? Možná potřebujete rychlé tlačítko „Mark as Reviewed“, které se objeví, když uživatel pravým tlačítkem klikne na buňku, zapíše hodnotu do buňky Excelu a poté uloží aktualizovaný sešit – vše bez opuštění webového rozhraní.  

V tomto tutoriálu postavíme přesně to: **vlastní pravé‑klikové menu** poháněné GridJs, server‑side handler, který **zapíše hodnotu do buňky Excelu**, a poslední krok, který **uloží aktualizovaný soubor Excel** na disk. Na konci budete mít znovupoužitelný vzor, který můžete vložit do jakéhokoli projektu Flask, FastAPI nebo Django.

> **Proč na tom záleží?**  
> Přidání vlastního kontextového menu zjednodušuje pracovní postupy revize dat, snižuje potřebu ručního kopírování a vkládání a poskytuje koncovým uživatelům zážitek s nativním pocitem přímo v mřížce. Navíc uvidíte, jak **aktualizovat hodnotu buňky v pythonu**‑stylu, což je základní dovednost pro jakýkoli úkol automatizace Excelu.

## Požadavky

- Python 3.9+ (kód funguje také na 3.10)  
- `openpyxl` pro práci se soubory Excel  
- `gridjs` Python wrapper (nebo JS knihovna, pokud dáváte přednost front‑endu)  
- Základní webový framework (ukázka pro Flask)  
- Soubor sešitu pojmenovaný `sample.xlsx` ve složce projektu  

Pokud vám něco chybí, spusťte:

```bash
pip install openpyxl flask gridjs
```

Pojďme na to.

---

## Krok 1 – Přidání vlastního kontextového menu: Inicializace GridJs a navázání listu

První věc, kterou musíte udělat, je vytvořit instanci `GridJs` a nasměrovat ji na list, se kterým chcete pracovat. Zde se v našem kódu poprvé objevuje fráze **add custom context menu**, a nastavuje scénu pro vše ostatní.

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

**Co se děje?**  
`grid.set_worksheet(ws)` říká GridJs, aby použil data z `ws` jako svůj zdroj dat. Od této chvíle budou všechny úpravy kontext‑menu, které přidáme, automaticky cílit na stejný list, čímž se UI a soubor udrží v synchronizaci.

> **Tip:** Udržujte svůj sešit otevřený v režimu čtení/zápisu jen jednou. Opakované otevírání uvnitř handleru požadavku může způsobit problémy se zamykáním souborů ve Windows.

---

## Krok 2 – Zapsání hodnoty do buňky Excelu: Definice akce pro položku menu

Nyní, když je mřížka připravená, potřebujeme **zapsat hodnotu do buňky Excelu**, když uživatel vybere náš vlastní příkaz. Přidáme položku menu nazvanou „Mark as Reviewed“ a přiřadíme jí identifikátor `markReviewed`. Identifikátor je to, co klient‑side JavaScript pošle zpět na server.

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**Proč používat vlastní identifikátor?**  
Identifikátor odděluje text UI od logiky serveru, což vám umožní změnit popisek, aniž byste zasahovali do backendového kódu. Také činí operaci **create right‑click menu** explicitní a znovupoužitelnou.

---

## Krok 3 – Vytvoření pravého‑klikového menu: Registrace server‑side handleru

S položkou menu na místě musíme GridJs říct, co má dělat, když na ni uživatel klikne. Zde je místo, kde **create right‑click menu** funkčnost skutečně odešle požadavek zpět do Pythonu.

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

Par pár věcí k poznámce:

1. **`ws[cell_address] = "Reviewed"`** je nejužitečnější způsob, jak **update cell value python**. Pod kapotou `openpyxl` převádí adresu ve stylu A1 na indexy řádku/sloupce.
2. Handler vrací malý JSON payload. GridJs očekává indikátor stavu; můžete jej rozšířit o chybové zprávy, pokud bude potřeba.

Nyní navážeme identifikátor na handler:

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**Co když je buňka prázdná nebo chráněná?**  
- Prázdné buňky jsou v pořádku—`openpyxl` je vytvoří za běhu.  
- Pro chráněné listy budete muset nejprve odemknout (`ws.protection.sheet = False`) nebo zachytit `PermissionError`.

---

## Krok 4 – Aktualizace hodnoty buňky v Pythonu: Uložení změny uložením sešitu

Zapsání hodnoty je jen polovina příběhu; musíte **save updated excel file**, aby změna přežila mimo aktuální relaci. Zde dokončujeme celý cyklus od UI k disku.

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**Proč samostatná složka?**  
Ukládání do adresáře `output/` ponechává původní šablonu nedotčenou, což je užitečné pro auditní stopy. Přizpůsobte cestu tak, aby odpovídala vašemu nasazovacímu prostředí.

> **Pozor:** Pokud obsluhujete mnoho souběžných uživatelů, zvažte použití vlákny‑bezpečného zámku (`threading.Lock`) kolem `wb.save()`, aby se předešlo závodním podmínkám.

---

## Krok 5 – Generování konfiguračního JSON pro klienta a propojení všeho dohromady

Nakonec musíme vytvořit JSON, který bude konzumovat front‑endová instance GridJs. Tento JSON obsahuje data listu **a** definici vlastního menu.

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

Když vložíte `config_json` do své HTML stránky, GridJs vykreslí mřížku s položkou „Mark as Reviewed“, která bude pravým kliknutím dostupná na každé buňce.

### Kompletní Flask příklad

Níže je minimální Flask aplikace, která spojuje všechny části. Spusťte ji, otevřete `http://localhost:5000` a pravým kliknutím na libovolnou buňku uvidíte vlastní menu v akci.

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

**Očekávaný výsledek:**  
- Pravým kliknutím na libovolnou buňku → objeví se „Mark as Reviewed“.  
- Klikněte na ni → obsah buňky se změní na „Reviewed“.  
- Sešit `output/sample-updated.xlsx` nyní obsahuje novou hodnotu.

---

## Časté otázky a okrajové případy

| Question | Answer |
|----------|--------|
| *Co když potřebuji více vlastních akcí?* | Stačí přidat více objektů do `grid.settings.context_menu.custom_items` a zaregistrovat každý s vlastním identifikátorem. |
| *Mohu předat handleru další data (např. ID řádku)?* | Ano. Přidejte další klíče do JSON payload na straně klienta a poté je načtěte z `request` v `on_custom_command`. |
| *Je tento přístup kompatibilní s async frameworky?* | Rozhodně—stačí udělat `on_custom_command` asynchronní funkcí a použít `await wb.save(...)`, pokud přejdete na `aiofiles` nebo podobné. |
| *Jak stylovat ikonu menu?* | Poskytněte libovolný název z Material‑Icons (`"icon": "edit"`). Front‑end automaticky načte font ikon. |
| *Co s velkými sešity?* | Načtěte jen požadovaný list a zvažte streamování řádků pomocí `openpyxl.iter_rows()`, aby se snížila spotřeba paměti. |

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Preserve Single Quote Prefix of Cell Value or Range in Excel](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}