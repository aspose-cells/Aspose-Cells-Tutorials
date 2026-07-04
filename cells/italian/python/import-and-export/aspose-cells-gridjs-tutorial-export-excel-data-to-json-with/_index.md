---
category: general
date: 2026-07-03
description: Tutorial Aspose Cells GridJs che mostra come esportare i dati di Excel
  in JSON ed esportare il foglio di lavoro in JSON in modo efficiente usando il lazy
  loading.
draft: false
keywords:
- aspose cells gridjs tutorial
- export excel data json
- export worksheet to json
language: it
og_description: Il tutorial GridJs di Aspose Cells spiega come esportare i dati di
  Excel in JSON e come esportare il foglio di lavoro in JSON con caricamento lazy
  per fogli di calcolo di grandi dimensioni.
og_title: Tutorial GridJs di Aspose Cells – Esporta i dati di Excel in JSON
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  headline: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  type: TechArticle
- description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  name: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed locally. - `asposecells` package (you can `pip
      install aspose-cells`). - A sizeable Excel file (e.g., `large-data.xlsx`) placed
      in a known directory. - Basic familiarity with Python and web development concepts.'
  - name: Exporting a specific worksheet
    text: 'The example above always uses the first worksheet (`Worksheets[0]`). To
      export a different sheet, simply change the index or use the sheet name:'
  - name: Changing the chunk size for massive files
    text: For files with millions of rows, a chunk size of 500 may still be too small,
      causing many round‑trips. You can increase it to 2000 or more, but remember
      that larger chunks consume more bandwidth per request.
  - name: Exporting to a stream instead of a file
    text: 'If your API returns the JSON directly, you don’t need to write to disk:'
  - name: Handling formulas and formatting
    text: 'By default, `ExportGridJsJson` includes the calculated values of formulas.
      If you need raw formulas instead, set:'
  type: HowTo
tags:
- Aspose.Cells
- Python
- GridJs
- JSON export
title: Tutorial Aspose Cells GridJs – Esporta dati Excel in JSON con caricamento differito
url: /it/python/import-and-export/aspose-cells-gridjs-tutorial-export-excel-data-to-json-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutorial Aspose Cells GridJs – Esporta dati Excel in JSON con caricamento lazy

Ti sei mai chiesto come **esportare dati Excel in JSON** da un foglio di calcolo enorme senza bloccare il browser? In questo tutorial Aspose Cells GridJs ti guideremo attraverso una soluzione completa, pronta all'uso, che ti permette di **esportare il foglio di lavoro in JSON** usando il caricamento lazy, così solo le righe di cui hai bisogno vengono recuperate su richiesta.

Se hai lottato con file `.xlsx` di grandi dimensioni e il lato client continua a bloccarsi, non sei solo. La buona notizia? L'approccio che descriviamo è leggero e scalabile, e puoi inserirlo in qualsiasi progetto Python che utilizza già la libreria Aspose.Cells.

## Cosa copre questa guida

Nei prossimi minuti imparerai a:

1. Caricare una cartella di lavoro grande con Aspose.Cells.  
2. Attivare il caricamento lazy di GridJs così il server trasmette le righe a blocchi.  
3. Esportare la configurazione GridJs in un file JSON che il front‑end può consumare.  
4. Regolare la dimensione del blocco per prestazioni ottimali.  
5. Verificare l'output e integrarlo con una semplice pagina HTML.

Nessun servizio esterno, nessuna magia nascosta—solo puro Python e l'API Aspose.Cells. Alla fine avrai una pipeline **completa di esportazione del foglio di lavoro in JSON** che potrai adattare a dashboard, strumenti di reporting o qualsiasi componente di griglia dati.

### Prerequisiti

- Python 3.8+ installato localmente.  
- Pacchetto `asposecells` (puoi eseguire `pip install aspose-cells`).  
- Un file Excel di dimensioni considerevoli (ad esempio `large-data.xlsx`) posizionato in una directory nota.  
- Familiarità di base con Python e i concetti di sviluppo web.

Se qualcuno di questi punti ti è sconosciuto, non farti prendere dal panico—ogni passaggio include una breve spiegazione del “perché”, così comprenderai la logica dietro il codice.

---

## Passo 1: Installa e importa Aspose.Cells

Prima di tutto, abbiamo bisogno della libreria Aspose.Cells. È un prodotto commerciale, ma una versione di prova gratuita è sufficiente per lo sviluppo.

```bash
pip install aspose-cells
```

Ora importa le classi necessarie nel tuo script.

```python
# Step 1: Import the Aspose.Cells workbook class
import asposecells
from asposecells import Workbook
```

> **Perché è importante:** Importare `Workbook` ti dà accesso al motore ad alte prestazioni che legge i file Excel direttamente in memoria, evitando l'approccio più lento di `openpyxl`.

## Passo 2: Carica la cartella di lavoro contenente il grande dataset

Con la libreria pronta, puntala al tuo file Excel. Il percorso può essere assoluto o relativo; assicurati solo che il file esista.

```python
# Step 2: Load the workbook that contains a large data set
workbook = Workbook("YOUR_DIRECTORY/large-data.xlsx")
```

> **Consiglio professionale:** Se la tua cartella di lavoro supera qualche centinaio di megabyte, considera di aumentare il limite di memoria del processo Python o di usare un interprete a 64 bit per evitare `MemoryError`.

## Passo 3: Abilita il caricamento lazy di GridJs

GridJs è il componente grid JavaScript di Aspose. Il caricamento lazy indica al server di inviare solo un sottoinsieme di righe—perfetto per fogli enormi.

```python
# Step 3: Enable lazy loading so the client fetches rows on demand
grid_options = workbook.Worksheets[0].Cells.GridJsOptions
grid_options.LazyLoading = True                 # fetch rows/columns only when needed
grid_options.LazyLoadingChunkSize = 500         # rows per server request
```

> **Perché il caricamento lazy?** Senza di esso, l'intero foglio di lavoro verrebbe serializzato in JSON in un'unica operazione, superando facilmente i limiti di memoria del browser. Impostando `LazyLoadingChunkSize` a 500, ogni richiesta trasporta un payload gestibile.

## Passo 4: Esporta la configurazione GridJs in JSON

Ora chiediamo ad Aspose di produrre il JSON che il componente GridJs del front‑end si aspetta. Questa è la parte centrale dell'operazione **export excel data json**.

```python
# Step 4: Export the GridJs configuration to a JSON file for the client side
grid_json = workbook.Worksheets[0].Cells.ExportGridJsJson()
```

Il metodo `ExportGridJsJson` restituisce un oggetto `bytes` contenente la rappresentazione JSON del foglio di lavoro, pronto per essere salvato o trasmesso.

## Passo 5: Scrivi il JSON su file (o trasmettilo)

Per un test rapido, scrivi il JSON su disco. In un'API di produzione lo restituiresti direttamente da un endpoint Flask/Django.

```python
# Step 5: Persist the JSON to a file
output_path = "YOUR_DIRECTORY/lazygrid.json"
with open(output_path, "wb") as f:
    f.write(grid_json)

print(f"✅ GridJs JSON exported successfully to {output_path}")
```

> **Cosa vedrai:** Aprendo `lazygrid.json` scoprirai una struttura con `columns`, `rows` e metadati di paginazione. L'array `rows` sarà inizialmente vuoto; GridJs richiederà il primo blocco al caricamento della pagina.

## Passo 6: Integra il JSON in una semplice pagina HTML (opzionale)

Se vuoi vedere la griglia in azione, crea un piccolo file HTML che carica GridJs da un CDN e lo punta al JSON generato.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Lazy‑Loaded GridJs Demo</title>
    <link href="https://unpkg.com/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
    <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
</head>
<body>
    <div id="wrapper"></div>
    <script>
        // Fetch the lazy‑loaded JSON and initialize GridJs
        fetch('lazygrid.json')
            .then(r => r.json())
            .then(config => {
                new gridjs.Grid({
                    ...config,
                    server: {
                        url: 'lazygrid.json',
                        then: data => data
                    }
                }).render(document.getElementById('wrapper'));
            });
    </script>
</body>
</html>
```

> **Perché includerlo?** Dimostra il ciclo completo: Python crea il JSON, il browser lo recupera e GridJs rende i dati blocco per blocco. Ora puoi sperimentare con valori diversi di `LazyLoadingChunkSize` per trovare il punto ottimale per la tua rete.

## Passo 7: Verifica e risolvi i problemi

Esegui lo script Python:

```bash
python export_lazy_grid.py
```

Dovresti vedere il messaggio di successo e un file `lazygrid.json`. Apri il file HTML in un browser; la griglia dovrebbe mostrare immediatamente le prime 500 righe, con controlli di paginazione per caricare altre.

Se la griglia appare vuota:

- **Controlla la dimensione del file JSON** – un file di zero byte di solito indica che il percorso del workbook era errato.  
- **Verifica che il caricamento lazy sia abilitato** – il flag `LazyLoading` deve essere `True`.  
- **Ispeziona la console del browser** – eventuali errori CORS o 404 indicano che il JSON non è servito correttamente.

---

## Variazioni comuni e casi limite

### Esportare un foglio di lavoro specifico

L'esempio sopra usa sempre il primo foglio (`Worksheets[0]`). Per esportare un foglio diverso, cambia semplicemente l'indice o usa il nome del foglio:

```python
sheet = workbook.Worksheets["DataSheet"]   # by name
grid_options = sheet.Cells.GridJsOptions
grid_json = sheet.Cells.ExportGridJsJson()
```

### Modificare la dimensione del blocco per file massivi

Per file con milioni di righe, una dimensione di blocco di 500 potrebbe ancora essere troppo piccola, provocando numerosi round‑trip. Puoi aumentarla a 2000 o più, ma ricorda che blocchi più grandi consumano più larghezza di banda per richiesta.

```python
grid_options.LazyLoadingChunkSize = 2000
```

### Esportare su uno stream invece che su file

Se la tua API restituisce direttamente il JSON, non è necessario scriverlo su disco:

```python
from flask import Flask, Response
app = Flask(__name__)

@app.route("/api/gridjson")
def gridjson():
    json_bytes = workbook.Worksheets[0].Cells.ExportGridJsJson()
    return Response(json_bytes, mimetype="application/json")
```

### Gestire formule e formattazione

Per impostazione predefinita, `ExportGridJsJson` include i valori calcolati delle formule. Se ti servono le formule grezze, imposta:

```python
grid_options.ExportFormulas = True
```

---

## Conclusione

In questo **tutorial Aspose Cells GridJs** abbiamo coperto tutto ciò che ti serve per **esportare dati Excel in JSON** e **esportare il foglio di lavoro in JSON** con caricamento lazy. Dall'installazione di Aspose.Cells, all'abilitazione del lazy loading, alla generazione del JSON, fino all'integrazione con una semplice pagina HTML, ora disponi di un modello full‑stack che scala agevolmente con fogli di calcolo enormi.

Provalo—regola la dimensione del blocco, punta a fogli diversi o integra l'endpoint in un'app Flask o Django. Le possibilità sono infinite e i guadagni di performance sono immediati.

Pronto per il passo successivo? Prova ad aggiungere l'ordinamento delle colonne, renderer personalizzati per le celle o persino filtri lato server per rendere la tua griglia GridJs davvero interattiva. Se incontri difficoltà, lascia un commento qui sotto; buona programmazione!

## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Import JSON Data into Excel Using Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Load CSV & Export to JSON Using Aspose.Cells for .NET&#58; A Comprehensive Guide](/cells/english/net/import-export/load-csv-export-json-aspose-cells-dotnet/)
- [Export Excel Data Using Aspose.Cells .NET&#58; A Complete Guide for Seamless Data Export](/cells/english/net/import-export/export-excel-data-aspose-cells-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}