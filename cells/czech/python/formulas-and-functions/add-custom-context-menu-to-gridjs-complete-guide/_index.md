---
category: general
date: 2026-06-08
description: Přidejte vlastní kontextové menu do GridJs a exportujte mřížku do CSV
  s blobem souboru ke stažení. Postupujte podle tohoto krok‑za‑krokem tutoriálu pro
  plně funkční příklad.
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: cs
og_description: Přidejte vlastní kontextové menu do GridJs a exportujte mřížku do
  CSV pomocí blobu ke stažení souboru CSV. Naučte se kompletní implementaci za méně
  než 10 minut.
og_title: Přidejte vlastní kontextové menu do GridJs – kompletní průvodce
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
title: Přidání vlastního kontextového menu do GridJs – kompletní průvodce
url: /cs/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidání vlastního kontextového menu do GridJs – Kompletní průvodce

Chcete **přidat vlastní kontextové menu** do komponenty GridJs? V tomto tutoriálu vás provedeme přesně tímto krokem a ukážeme, jak **exportovat grid do CSV** pomocí **stahování CSV souboru jako Blob**. Ať už vytváříte rychlý admin panel nebo plnohodnotný reportingový dashboard, menu po kliknutí pravým tlačítkem, které uživatelům umožní stáhnout data jako CSV, může výrazně zvýšit produktivitu.

Probereme vše, co potřebujete: Python část s Flask, JavaScriptový handler, který vytváří Blob, a HTML/JS, které GridJs generuje. Na konci budete mít samostatný příklad, který můžete vložit do libovolného projektu.

---

## Co budete potřebovat

- **Python 3.9+** a **Flask** nainstalované (`pip install flask`).
- **gridjs** Python wrapper (nebo přímo JavaScriptová knihovna) – v tomto průvodci předpokládáme tenký Python wrapper, který odráží JavaScript API.
- Základní pochopení **async JavaScript** (`fetch`, `Promise`) – ale nebojte se, každou řádku vysvětlíme.
- Editor dle vašeho výběru (VS Code, PyCharm nebo i jednoduchý textový editor).

To je vše. Žádné další front‑end build nástroje, žádný Node npm tanec. Pouze čistý Flask, který servíruje HTML generované GridJs.

---

## Přidání vlastního kontextového menu do GridJs

První věc, kterou musíte udělat, je říct GridJs, že chcete vlastní menu po kliknutí pravým tlačítkem. Ve výchozím nastavení GridJs poskytuje minimální sadu (copy, paste, atd.), ale můžete ji kompletně nahradit.

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**Proč je to důležité:**  
Nastavením `CustomContextMenu` nahradíte výchozí seznam tím, který poskytnete vy. Řetězec `"Export CSV"` je jen popisek – skutečná práce se spustí, když uživatel na něj klikne, což provedeme v dalším kroku.

> *Pro tip:* Udržujte seznam krátký. Přetížené kontextové menu ruší smysl rychlých akcí.

---

## Export gridu do CSV pomocí Blob stahování

Nyní, když položka menu existuje, potřebujeme JavaScriptový handler, který komunikuje se serverem, načte CSV, převede ho na **Blob** a vynutí stažení. Právě zde se objevuje fráze **download CSV file blob**.

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

### Rozbor handleru

| Řádek | Co dělá |
|------|----------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | Volá Flask routu (`/export/csv`) a předává název listu jako dotazový řetězec. |
| `.then(r => r.blob())` | Převádí HTTP odpověď na **Blob** – v podstatě binární kontejner pro CSV data. |
| `URL.createObjectURL(b)` | Vytvoří dočasnou URL, kterou může prohlížeč zacházet jako se souborem. |
| `a.download = cell.sheetName + ".csv"` | Nastaví název souboru, který uživatel uvidí v dialogu pro stažení. |
| `a.click()` | Programově klikne na skrytý odkaz, čímž spustí stažení Blobu. |

**Proč použít Blob?**  
Prohlížeče nemohou přímo stáhnout surový text vrácený z `fetch` bez jeho převodu na něco podobného souboru. Trik s Blob‑URL je nejspolehlivější, cross‑browser způsob, jak spustit **download CSV file blob** bez obnovení stránky.

---

## Nastavení Flask backendu

Front‑end handler očekává endpoint na `/export/csv`. Zde je minimální Flask view, který přijme název listu, získá data z workbooku a pošle zpět CSV.

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

### Klíčové body

- `io.StringIO` nám umožňuje vytvořit CSV v paměti, aniž bychom se dotýkali souborového systému.
- `Content‑Disposition` říká prohlížeči, že soubor je příloha a navrhuje název souboru. I když front‑end také nastavuje `a.download`, mít to na straně serveru poskytuje záložní řešení pro ne‑JS klienty.
- Routa je záměrně jednoduchá; později můžete přidat autentizaci, kontrolu oprávnění nebo streamování pro obrovské datové sady.

---

## Renderování gridu na klientovi

S připraveným kontextovým menu a backendem je posledním krokem vykreslit komponentu GridJs a poslat HTML/JS do prohlížeče.

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

V Flask view byste typicky udělali:

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

Když se stránka načte, GridJs vytvoří tabulku, vloží vlastní kontextové menu a JavaScriptový handler, který jsme definovali dříve, je připravený k aktivaci. Klikněte pravým tlačítkem na libovolnou buňku, vyberte **Export CSV** a sledujte, jak prohlížeč stáhne soubor pojmenovaný podle listu.

---

## Kompletní funkční příklad (všechny soubory)

Níže je kompletní, spustitelný kód, který můžete zkopírovat do nového adresáře. Nainstalujte Flask (`pip install flask`) a spusťte `python app.py`.

**`app.py`**



## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční kódové příklady s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vlastních projektech.

- [Načtení CSV souborů s vlastními parsery Aspose Cells Java](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [Export CSV v Javě – kód](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [Export Excel CSV prázdné řádky Aspose Cells .NET](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}