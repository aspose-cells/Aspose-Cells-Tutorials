---
category: general
date: 2026-06-30
description: Aggiungi un menu contestuale personalizzato a una griglia Excel in Python
  e scrivi un valore nella cella Excel durante il salvataggio del file aggiornato.
  Impara a creare un menu con clic destro e aggiornare il valore della cella in stile
  Python.
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: it
og_description: Aggiungi un menu contestuale personalizzato in Python per scrivere
  un valore in una cella Excel e salvare il file Excel aggiornato. Questa guida ti
  guida nella creazione di un menu con clic destro usando GridJs.
og_title: Aggiungi un menu contestuale personalizzato in Python – Tutorial passo passo
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
title: Aggiungi un menu contestuale personalizzato in Python – Guida completa
url: /it/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungi un menu contestuale personalizzato in Python – Guida completa

Ti sei mai chiesto come **aggiungere voci di menu contestuale personalizzate** a una griglia di foglio di calcolo che servi da Python? Forse ti serve un rapido pulsante “Mark as Reviewed” che appare quando un utente fa clic con il tasto destro su una cella, scrive un valore nella cella Excel e poi salva la cartella di lavoro aggiornata—tutto senza uscire dall'interfaccia web.  

In questo tutorial costruiremo esattamente questo: un **menu contestuale personalizzato** alimentato da GridJs, un gestore lato server che **scrive valore nella cella Excel**, e un passaggio finale che **salva il file Excel aggiornato** su disco. Alla fine avrai un modello riutilizzabile da inserire in qualsiasi progetto Flask, FastAPI o Django.

> **Perché importa?**  
> Aggiungere un menu contestuale personalizzato semplifica i flussi di lavoro di revisione dei dati, riduce il copia‑incolla manuale e offre agli utenti finali un'esperienza nativa direttamente nella griglia. Inoltre, vedrai come **aggiornare il valore di una cella in stile python**, che è una competenza fondamentale per qualsiasi attività di automazione Excel.

## Prerequisiti

- Python 3.9+ (il codice funziona anche su 3.10)  
- `openpyxl` per la gestione dei file Excel  
- `gridjs` wrapper Python (o la libreria JS se preferisci il front‑end)  
- Un framework web di base (esempio Flask mostrato)  
- Un file di cartella di lavoro chiamato `sample.xlsx` nella cartella del progetto  

Se ti manca qualcuno di questi, esegui:

```bash
pip install openpyxl flask gridjs
```

Ora immergiamoci.

---

## Passo 1 – Aggiungi un menu contestuale personalizzato: Inizializza GridJs e collega il foglio di lavoro

La prima cosa da fare è avviare un'istanza `GridJs` e puntarla al foglio di lavoro con cui intendi lavorare. È qui che la frase **add custom context menu** appare per la prima volta nel nostro codice, e prepara il terreno per tutto il resto.

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

**Cosa sta succedendo?**  
`grid.set_worksheet(ws)` indica a GridJs di usare i dati di `ws` come sua fonte dati. Da ora in poi, qualsiasi modifica al menu contestuale che aggiungiamo punterà automaticamente allo stesso foglio di lavoro, mantenendo l'interfaccia UI e il file sincronizzati.

> **Consiglio professionale:** Mantieni il tuo workbook aperto in modalità lettura/scrittura una sola volta. Aprirlo ripetutamente all'interno di un gestore di richieste può causare problemi di blocco file su Windows.

## Passo 2 – Scrivi valore nella cella Excel: Definisci l'azione per l'elemento del menu

Ora che la griglia è pronta, dobbiamo **scrivere valore nella cella Excel** quando l'utente seleziona il nostro comando personalizzato. Aggiungeremo una voce di menu chiamata “Mark as Reviewed” e le assegneremo un identificatore `markReviewed`. L'identificatore è ciò che il JavaScript lato client invierà al server.

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**Perché usare un identificatore personalizzato?**  
L'identificatore separa il testo dell'interfaccia utente dalla logica del server, permettendoti di cambiare l'etichetta senza modificare il codice backend. Inoltre rende l'operazione **create right‑click menu** esplicita e riutilizzabile.

## Passo 3 – Crea il menu contestuale: Registra il gestore lato server

Con l'elemento di menu in posizione, dobbiamo dire a GridJs cosa fare quando l'utente ci clicca sopra. È qui che implementiamo la funzionalità **create right‑click menu** che effettivamente invia una richiesta a Python.

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

Alcune cose da notare:

1. **`ws[cell_address] = "Reviewed"`** è il modo più diretto per **update cell value python**. In pratica, `openpyxl` traduce l'indirizzo in stile A1 in indici di riga/colonna.
2. Il gestore restituisce un piccolo payload JSON. GridJs si aspetta un indicatore di stato; potresti espanderlo per includere messaggi di errore se necessario.

Ora colleghiamo l'identificatore al gestore:

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**E se la cella è vuota o protetta?**  
- Le celle vuote vanno bene—`openpyxl` le creerà al volo.  
- Per fogli protetti, dovrai prima rimuovere la protezione (`ws.protection.sheet = False`) o gestire un `PermissionError`.

## Passo 4 – Aggiorna valore cella Python: Persisti la modifica salvando la cartella di lavoro

Scrivere un valore è solo metà della storia; devi **save updated excel file** affinché la modifica sopravviva oltre la sessione corrente. È qui che completiamo il ciclo dall'interfaccia UI al disco.

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**Perché una cartella separata?**  
Salvare in una directory `output/` mantiene intatto il modello originale, utile per le tracce di audit. Regola il percorso per adattarlo al tuo ambiente di distribuzione.

> **Attenzione:** Se servi molti utenti concorrenti, considera l'uso di un lock thread‑safe (`threading.Lock`) attorno a `wb.save()` per evitare condizioni di gara.

## Passo 5 – Genera il JSON di configurazione client e collega tutto insieme

Infine, dobbiamo generare il JSON che l'istanza GridJs del front‑end consumerà. Questo JSON contiene i dati del foglio di lavoro **e** la definizione del menu personalizzato.

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

Quando inserisci `config_json` nella tua pagina HTML, GridJs renderizzerà la griglia con la voce “Mark as Reviewed” cliccabile con il tasto destro su ogni cella.

### Esempio Flask completo

Di seguito trovi una minimal Flask app che mette insieme tutti i componenti. Eseguila, apri `http://localhost:5000` e fai clic con il tasto destro su qualsiasi cella per vedere il menu personalizzato in azione.

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

**Risultato atteso:**  
- Fai clic con il tasto destro su qualsiasi cella → appare “Mark as Reviewed”.  
- Cliccaci sopra → il contenuto della cella cambia in “Reviewed”.  
- La cartella di lavoro `output/sample-updated.xlsx` ora contiene il nuovo valore.

## Domande comuni e casi limite

| Question | Answer |
|----------|--------|
| *E se ho bisogno di più azioni personalizzate?* | Basta aggiungere più oggetti a `grid.settings.context_menu.custom_items` e registrare ciascuno con il proprio identificatore. |
| *Posso passare dati extra (ad esempio, ID riga) al gestore?* | Sì. Includi chiavi extra nel payload JSON lato client, poi leggile da `request` in `on_custom_command`. |
| *Questo approccio è compatibile con framework asincroni?* | Assolutamente—basta rendere `on_custom_command` una funzione async e usare `await wb.save(...)` se passi a `aiofiles` o simili. |
| *Come posso stilizzare l'icona del menu?* | Fornisci qualsiasi nome di Material‑Icons (`"icon": "edit"`). Il front‑end carica automaticamente il font delle icone. |
| *E i file Excel di grandi dimensioni?* | Carica solo il foglio necessario e considera lo streaming delle righe con `openpyxl.iter_rows()` per mantenere basso l'uso di memoria |

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Preserve Single Quote Prefix of Cell Value or Range in Excel](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}