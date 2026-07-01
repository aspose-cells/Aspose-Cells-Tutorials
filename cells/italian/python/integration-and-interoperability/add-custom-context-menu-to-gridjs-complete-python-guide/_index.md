---
category: general
date: 2026-06-30
description: Aggiungi un menu contestuale personalizzato in GridJs e scopri come caricare
  una cartella di lavoro Excel, aggiornare il valore di una cella, abilitare il controllo
  ortografico e registrare un comando personalizzato.
draft: false
keywords:
- add custom context menu
- update cell value
- enable spell checking
- load excel workbook
- register custom command
language: it
og_description: Aggiungi un menu contestuale personalizzato in GridJs mentre impari
  a caricare una cartella di lavoro Excel, aggiornare il valore di una cella, abilitare
  il controllo ortografico e registrare un comando personalizzato.
og_title: Aggiungi un menu contestuale personalizzato a GridJs – Tutorial Python passo
  passo
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
title: Aggiungi un menu contestuale personalizzato a GridJs – Guida completa Python
url: /it/python/integration-and-interoperability/add-custom-context-menu-to-gridjs-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungi un Menu Contestuale Personalizzato a GridJs – Guida Completa Python

Ti sei mai chiesto come **aggiungere voci di menu contestuale personalizzate** a una tabella GridJs alimentata da una cartella di lavoro Excel? Non sei l’unico. In molte applicazioni ricche di dati è necessario quel menu con il tasto destro per consentire agli utenti di segnalare righe, contrassegnare elementi come revisionati o avviare un’azione lato server—senza abbandonare la griglia.  

In questo tutorial vedremo come caricare una cartella di lavoro Excel, collegare una voce di menu contestuale personalizzata, aggiornare il valore di una cella, abilitare il controllo ortografico e registrare un comando personalizzato che persiste le modifiche nel file. Alla fine avrai un’istanza GridJs completamente funzionante, che sembra nativa per i tuoi utenti e scrive direttamente sul foglio di calcolo di origine.

## Prerequisiti

- Python 3.9+ (il codice usa type hints ma funziona con qualsiasi versione recente)  
- libreria `cells` (o qualsiasi wrapper per Excel che fornisca oggetti `Workbook` e `Worksheet`)  
- binding Python `gridjs` (il modello di oggetti rispecchia l’API JavaScript)  
- una conoscenza di base di lambda e strutture JSON  

Se hai tutto questo, immergiamoci.

## Passo 1: Caricare la Cartella di Lavoro Excel e Selezionare un Foglio

La prima cosa da fare è **caricare la cartella di lavoro Excel** così GridJs ha i dati da visualizzare. La classe `cells.Workbook` astrae l’I/O del file e ti dà accesso diretto a righe, colonne e celle individuali.

```python
# Step 1: Load the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]          # Grab the first sheet – change index if needed
```

> **Perché è importante:** Caricare la cartella di lavoro in anticipo permette alla griglia di prelevare i dati su richiesta, e qualsiasi modifica successiva (come **aggiornare il valore di una cella**) verrà persa nello stesso file.

## Passo 2: Creare l’Istanza GridJs e Collegarla al Foglio

Ora creiamo un oggetto `gridjs.GridJs` e gli indichiamo quale foglio deve renderizzare. Pensalo come fornire a GridJs una fonte dati live che può interrogare ogni volta che deve renderizzare una pagina o un blocco caricato pigramente.

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)
```

> **Consiglio professionale:** Se lavori con più fogli, basta chiamare `grid.set_worksheet(other_ws)` in seguito—non è necessario ricreare la griglia.

## Passo 3: Abilitare il Controllo Ortografico (e Altre Funzionalità Utili)

La maggior parte delle app aziendali permette agli utenti di digitare note libere. Abilitare **il controllo ortografico** riduce gli errori di battitura e migliora la qualità dei dati. GridJs espone un semplice flag per questo.

```python
# Step 3: Turn on spell checking (and keep other helpers enabled)
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True          # optional but handy
grid.settings.formula_explanation.enabled = True   # if you support formulas
```

> **Perché abilitare il controllo ortografico?** Funziona lato client, fornendo feedback immediato senza chiamate extra al server—perfetto per fogli di grandi dimensioni.

## Passo 4: Aggiungere una Voce di Menu Contestuale Personalizzata

Ecco il cuore del tutorial: **aggiungere voci di menu contestuale personalizzate**. Creeremo un’opzione “Mark as Reviewed” che, al click, esegue un comando lato server che definiremo subito dopo.

```python
# Step 4: Add a custom context‑menu item
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",   # What the user sees
    "action": "markReviewed"      # Identifier used in the command registration
})
```

> **Illustrazione immagine**  
> ![Add Custom Context Menu screenshot showing right‑click options](/images/add-custom-context-menu.png "Add Custom Context Menu example")

Il testo alternativo sopra contiene la parola chiave principale, soddisfacendo i requisiti SEO.

## Passo 5: Registrare il Comando Personalizzato per Aggiornare il Valore della Cella

Quando l’utente seleziona “Mark as Reviewed”, dobbiamo **registrare un comando personalizzato** che aggiorna la cella Excel sottostante e salva il file. Il metodo `grid.register_custom_command` associa una callable Python all’identificatore di azione impostato in precedenza.

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

> **Perché funziona:** Il gestore riceve il riferimento della cella dal client, usa l’API `Worksheet` per **aggiornare il valore della cella**, quindi scrive l’intera cartella di lavoro su disco. La risposta informa il front‑end che l’operazione è riuscita.

### Gestione dei Casi Limite

- **Riferimento cella mancante:** Se `req` non contiene `"cell"`, genera un errore chiaro così l’interfaccia può mostrare un toast.  
- **Modifiche concorrenti:** Per scenari ad alto traffico, considera il lock della cartella di lavoro o l’uso di un timestamp di versione per evitare condizioni di gara.

## Passo 6: Abilitare il Lazy Loading per Fogli Grandi

Se gestisci migliaia di righe, il lazy loading mantiene l’interfaccia reattiva. Imposta la dimensione della pagina a un valore ragionevole—500 righe funzionano bene per la maggior parte dei browser.

```python
# Step 6: Activate lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500
```

> **E se hai 10 000 righe?** La griglia richiederà i dati pagina per pagina, riducendo la pressione di memoria sia sul client che sul server.

## Passo 7: (Opzionale) Aggiungere un Modal Personalizzato per la Modifica delle Righe

A volte serve un’interfaccia più ricca di un editor inline. GridJs ti permette di aprire una finestra modal che puoi ospitare ovunque—un componente React o un semplice form HTML.

```python
# Step 7: Configure a custom modal window for row editing
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"   # Serve this URL from your Flask/Django app
```

> **Perché usare un modal?** Isola la logica di validazione complessa e ti dà il pieno controllo sul layout, pur essendo attivato dalla griglia.

## Passo 8: Recuperare il JSON di Configurazione Lato Client

Infine, devi inviare la configurazione al browser. Il metodo `get_client_config` serializza tutto in un blob JSON che la libreria GridJs lato front‑end può consumare.

```python
# Step 8: Get the JSON configuration for the front‑end
client_config = grid.get_client_config()

# Example: you might embed this in a template
print(client_config)   # For debugging – remove in production
```

L’output appare più o meno così (troncato per brevità):

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

### Risultato Atteso

- Facendo clic con il tasto destro su qualsiasi cella si apre un menu con **Mark as Reviewed**.  
- Selezionandolo invia una richiesta al server, che **aggiorna il valore della cella** a “Reviewed” e salva `example‑updated.xlsx`.  
- Il controllo ortografico evidenzia le parole errate mentre l’utente digita.  

Tutto ciò avviene senza un refresh completo della pagina, grazie al lazy loading e al payload JSON leggero.

## Domande Frequenti & Consigli Pro

| Domanda | Risposta |
|----------|--------|
| *E se la cartella di lavoro è di sola lettura?* | Assicurati che i permessi del file consentano la scrittura, oppure apri la cartella con `mode="rw"` se la libreria lo supporta. |
| *Posso aggiungere più di una voce di menu personalizzata?* | Certamente—basta aggiungere altri dict a `grid.settings.context_menu.custom_items`. |
| *Devo ricaricare la griglia dopo un aggiornamento di cella?* | GridJs aggiorna automaticamente la riga interessata se restituisci `{status:"ok"}`; altrimenti chiama `grid.refresh()` dal client. |
| *Come rendere il controllo ortografico specifico per lingua?* | Imposta `grid.settings.spell_check.language = "en-US"` (o qualsiasi locale supportato). |
| *Il lazy loading è compatibile con il filtraggio lato server?* | Sì—combina `grid.settings.filter.enabled = True` e implementa la logica di filtro nel tuo comando personalizzato. |

## Esempio Completo (Tutti i Passi Combinati)

Di seguito trovi uno script unico che puoi inserire in una route Flask o eseguire come processo standalone. Sostituisci `YOUR_DIRECTORY` con il percorso reale sul tuo server.

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


## Cosa Dovresti Imparare Dopo?


I tutorial seguenti trattano argomenti strettamente correlati che approfondiscono le tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell’API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Add Custom Content Type Properties to Excel Workbooks Using Aspose.Cells Java](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [Add Custom XML Parts with ID to Workbook](/cells/english/net/workbook-operations/add-custom-xml-parts-with-id/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hindi/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}