---
category: general
date: 2026-11-22
description: Scopri come servire Excel in un'app web usando Flask. Questa guida mostra
  come caricare una cartella di lavoro Excel e visualizzare Excel sul web con GridJs.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to serve excel
- load excel workbook
- display excel web
language: it
lastmod: 2026-11-22
og_description: Come servire file Excel usando Flask e GridJs. Segui questo tutorial
  completo per caricare una cartella di lavoro Excel e visualizzarla sul web.
og_image_alt: Screenshot of a Flask‑powered GridJs table showing Excel data
og_title: Come servire Excel con Flask – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to serve Excel in a web app using Flask. This guide shows
    how to load Excel workbook and display Excel on the web with GridJs.
  headline: How to serve Excel files with Flask and GridJs
  type: TechArticle
- description: Learn how to serve Excel in a web app using Flask. This guide shows
    how to load Excel workbook and display Excel on the web with GridJs.
  name: How to serve Excel files with Flask and GridJs
  steps:
  - name: Load the Excel workbook
    text: '```python # Step 1: Load the workbook you want to expose via GridJs import
      cells'
  - name: Create a GridJs server‑side handler
    text: '```python # Step 2: Create a GridJs server‑side handler for the workbook
      grid_handler = cells.GridJsHandler(workbook) ```'
  - name: Enable optional features (lazy loading)
    text: '```python # Step 3: Enable optional features (e.g., lazy loading for large
      sheets) grid_handler.settings.lazy_load = True ```'
  - name: Set up a minimal Flask application
    text: '```python # Step 4: Set up a minimal Flask application to serve the GridJs
      UI from flask import Flask, request, jsonify'
  - name: Define the GridJs endpoint
    text: '```python # Step 5: Define an endpoint that returns the current view state
      # and applies any client‑side edits sent as JSON @app.route("/gridjs", methods=["GET",
      "POST"]) def gridjs(): if request.method == "POST": # Apply edits sent from
      the GridJs UI grid_handler.apply_changes(request.json) # Retur'
  - name: Run the Flask server
    text: '```python # Step 6: Run the Flask server (default port 5000) if __name__
      == "__main__": # Debug mode is off for production; enable it only during development.
      app.run(port=5000, debug=False) ```'
  type: HowTo
tags:
- Flask
- Python
- Excel
title: Come servire file Excel con Flask e GridJs
url: /it/python/integration-and-interoperability/how-to-serve-excel-files-with-flask-and-gridjs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come servire file Excel con Flask e GridJs

Se hai bisogno di **how to serve excel** in una applicazione web Python, questo tutorial mostra una soluzione completa. Imparerai come **load excel workbook** con la libreria `cells`, esporla tramite un endpoint Flask e consentire agli utenti di **display excel web** usando GridJs.

Passeremo in rassegna ogni riga di codice, spiegheremo perché ogni parte è importante e ti forniremo un esempio pronto all'uso. Alla fine della guida potrai incorporare qualsiasi file `.xlsx` in una griglia reattiva lato client senza scrivere parser JavaScript personalizzati per i dati.

## Prerequisiti

- Python 3.9+ installato  
- pacchetti `flask` e `cells` (`pip install flask cells`)  
- Un file Excel di esempio (ad es., `sample.xlsx`) in una directory nota  

Non è necessario alcun framework front‑end aggiuntivo; GridJs gestisce l'interfaccia utente automaticamente.

## Panoramica della soluzione

La idea centrale è semplice:

1. **Load** il workbook Excel sul server.  
2. **Create** un `GridJsHandler` che traduce i dati del foglio di lavoro nel formato JSON che GridJs si aspetta.  
3. **Expose** una route Flask che restituisce la vista JSON e accetta modifiche dal client.  
4. **Run** il server Flask così il browser può recuperare i dati e renderizzare la griglia.

Ora implementiamo ogni passaggio.

## Come servire Excel con Flask e GridJs

### Passo 1: Caricare il workbook Excel

```python
# Step 1: Load the workbook you want to expose via GridJs
import cells

workbook_path = "YOUR_DIRECTORY/sample.xlsx"
workbook = cells.Workbook(workbook_path)
```

**Perché è importante:**  
`cells.Workbook` analizza il file `.xlsx` in una rappresentazione in memoria. Caricare il workbook una sola volta all'avvio mantiene il server veloce perché le richieste successive riutilizzano lo stesso oggetto invece di accedere ripetutamente al file system.

### Passo 2: Creare un handler server‑side per GridJs

```python
# Step 2: Create a GridJs server‑side handler for the workbook
grid_handler = cells.GridJsHandler(workbook)
```

**Perché è importante:**  
`GridJsHandler` astrae la conversione da righe/colonne Excel allo schema JSON consumato da GridJs. Tiene anche traccia delle modifiche lato client, consentendoti di persistere le modifiche al workbook in seguito, se necessario.

### Passo 3: Abilitare funzionalità opzionali (lazy loading)

```python
# Step 3: Enable optional features (e.g., lazy loading for large sheets)
grid_handler.settings.lazy_load = True
```

**Perché è importante:**  
Quando un foglio di lavoro contiene migliaia di righe, inviare l'intero dataset in una volta può sovraccaricare il browser. Il lazy loading trasmette i dati pagina per pagina, migliorando le prestazioni per lo scenario **display excel web**.

### Passo 4: Configurare un'app Flask minimale

```python
# Step 4: Set up a minimal Flask application to serve the GridJs UI
from flask import Flask, request, jsonify

app = Flask(__name__)
```

**Perché è importante:**  
Flask fornisce un server HTTP leggero che può servire endpoint JSON e file statici. Mantenere l'app Flask minimale riduce la superficie di attacco e rende l'esempio facile da adattare.

### Passo 5: Definire l'endpoint GridJs

```python
# Step 5: Define an endpoint that returns the current view state
#         and applies any client‑side edits sent as JSON
@app.route("/gridjs", methods=["GET", "POST"])
def gridjs():
    if request.method == "POST":
        # Apply edits sent from the GridJs UI
        grid_handler.apply_changes(request.json)
    # Return the JSON view expected by GridJs
    return jsonify(grid_handler.get_view())
```

**Perché è importante:**  

- **GET** – Il browser recupera la vista iniziale del foglio di lavoro.  
- **POST** – Quando un utente modifica una cella, GridJs invia un payload JSON; `apply_changes` unisce quelle modifiche allo stato interno dell'handler.  

Restituire `grid_handler.get_view()` garantisce che il client riceva sempre i dati più recenti, il che è essenziale per un'esperienza fluida di **display excel web**.

### Passo 6: Avviare il server Flask

```python
# Step 6: Run the Flask server (default port 5000)
if __name__ == "__main__":
    # Debug mode is off for production; enable it only during development.
    app.run(port=5000, debug=False)
```

**Perché è importante:**  
Eseguire sulla porta 5000 è il valore predefinito di Flask, rendendo facile testare localmente (`http://localhost:5000/gridjs`). In produzione si dovrebbe posizionare Flask dietro un server WSGI (ad es., Gunicorn) e possibilmente abilitare HTTPS.

## Output JSON previsto

Quando navighi a `http://localhost:5000/gridjs` con una richiesta GET, la risposta appare così:

```json
{
  "columns": ["A", "B", "C"],
  "data": [
    ["Header1", "Header2", "Header3"],
    ["Row1Col1", "Row1Col2", "Row1Col3"],
    ["Row2Col1", "Row2Col2", "Row2Col3"]
  ],
  "settings": {
    "lazy_load": true
  }
}
```

## Esempio completo eseguibile

Di seguito lo script completo che puoi copiare in `app.py` ed eseguire:

```python
import cells
from flask import Flask, request, jsonify

# -------------------------------------------------
# 1. Load the Excel workbook
# -------------------------------------------------
workbook_path = "YOUR_DIRECTORY/sample.xlsx"
workbook = cells.Workbook(workbook_path)

# -------------------------------------------------
# 2. Create the GridJs handler
# -------------------------------------------------
grid_handler = cells.GridJsHandler(workbook)

# -------------------------------------------------
# 3. Enable lazy loading (optional but recommended)
# -------------------------------------------------
grid_handler.settings.lazy_load = True

# -------------------------------------------------
# 4. Initialize Flask
# -------------------------------------------------
app = Flask(__name__)

# -------------------------------------------------
# 5. Define the GridJs endpoint
# -------------------------------------------------
@app.route("/gridjs", methods=["GET", "POST"])
def gridjs():
    if request.method == "POST":
        # Apply client‑side edits
        grid_handler.apply_changes(request.json)
    # Return current view as JSON
    return jsonify(grid_handler.get_view())

# -------------------------------------------------
# 6. Run the server
# -------------------------------------------------
if __name__ == "__main__":
    app.run(port=5000, debug=False)
```

Esegui lo script con:

```bash
python app.py
```

Apri un browser e puntalo a una semplice pagina HTML che carica GridJs (vedi la documentazione di GridJs per il tag `<script>`). La griglia mostrerà il contenuto di Excel istantaneamente.

## Varianti comuni e casi limite

| Situazione | Come adattare |
|-----------|--------------|
| **Multiple worksheets** | Create a separate `GridJsHandler` for each sheet and expose distinct endpoints (`/gridjs/sheet1`, `/gridjs/sheet2`). |
| **Large files (>10 MB)** | Increase Flask’s request size limit (`app.config['MAX_CONTENT_LENGTH']`) and keep `lazy_load` enabled. |
| **Persisting edits back to the file** | After `apply_changes`, call `workbook.save("output.xlsx")` to write changes to disk. |
| **Authentication** | Wrap the endpoint with Flask‑Login or an API token check before returning data. |
| **CORS for external front‑ends** | Add `from flask_cors import CORS; CORS(app)` to allow cross‑origin requests. |

Queste modifiche ti permettono di scalare il processo **load excel workbook** per carichi di lavoro in produzione.

## Consigli professionali

- **Cache the JSON view** se il workbook cambia raramente; usa `functools.lru_cache` attorno a `grid_handler.get_view()` per ridurre l'overhead di serializzazione.  
- **Validate incoming edits** (`request.json`) per prevenire dati malformati che potrebbero corrompere il workbook.  
- Quando si serve tramite HTTPS, imposta `app.run(ssl_context=('cert.pem', 'key.pem'))` per criptare il traffico.

## Conclusione

Ora sai **how to serve excel** file usando Flask e GridJs, dal caricamento del workbook alla restituzione di una vista JSON che il browser può renderizzare. L'esempio copre l'intero ciclo di vita: **load excel workbook**, abilita il lazy loading, espone un endpoint REST e avvia un server pronto per la produzione.

Successivamente, esplora argomenti correlati come **display excel web** in un front‑end React, o estendi l'handler per **load excel workbook** da storage cloud (ad es., AWS S3). Sperimenta con lo styling delle colonne GridJs, aggiungendo paginazione, o persistere le modifiche degli utenti nel foglio di calcolo originale.

Buon coding e divertiti a trasformare file Excel statici in tabelle web interattive!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come caricare e modificare file Excel usando Aspose.Cells per .NET: Guida completa](/cells/english/net/workbook-operations/load-modify-excel-aspose-cells-net/)
- [Come creare ed esportare Excel in HTML usando Aspose.Cells Java | Guida alle operazioni del workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}