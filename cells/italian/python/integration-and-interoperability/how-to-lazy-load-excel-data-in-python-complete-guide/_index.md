---
category: general
date: 2026-06-30
description: Come caricare pigramente i dati Excel in Python usando GridJs. Scopri
  come collegare il foglio di lavoro, limitare le colonne e ottenere la configurazione
  per una gestione efficiente dei dati.
draft: false
keywords:
- how to lazy load
- how to limit columns
- how to bind worksheet
- how to get config
- load excel workbook python
language: it
og_description: Come caricare pigramente i dati Excel in Python con GridJs. Padroneggia
  il binding dei fogli di lavoro, limita le colonne e recupera la configurazione per
  un caricamento rapido e su richiesta.
og_title: Come caricare pigramente i dati Excel in Python – Passo dopo passo
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to lazy load Excel data in Python using GridJs. Learn how to bind
    worksheet, limit columns, and get config for efficient data handling.
  headline: How to Lazy Load Excel Data in Python – Complete Guide
  type: TechArticle
- description: How to lazy load Excel data in Python using GridJs. Learn how to bind
    worksheet, limit columns, and get config for efficient data handling.
  name: How to Lazy Load Excel Data in Python – Complete Guide
  steps:
  - name: What if my workbook has multiple sheets?
    text: You can call `grid.set_worksheet(ws, name="MySheet")` for each sheet you
      want to expose. Then, when you **how to get config**, the JSON will contain
      a `worksheet` field you can switch on the client side.
  - name: How does GridJs handle empty rows?
    text: Lazy loading skips rows that are completely empty by default. If you need
      to keep them (e.g., for preserving line numbers), set `grid.settings.lazy_load.include_empty
      = True`.
  - name: Can I change the column order?
    text: 'Absolutely. Replace the `columns` list with the exact order you want: `["D",
      "B", "A", "C"]`. The client will receive cells in that sequence.'
  - name: Is it safe to expose the endpoint publicly?
    text: 'Treat the endpoint like any other API: add authentication middleware, rate
      limiting, or IP whitelisting if the data is sensitive. The lazy‑load mechanism
      itself doesn’t add security concerns.'
  type: HowTo
tags:
- python
- excel
- gridjs
- data‑visualization
title: Come caricare pigramente i dati Excel in Python – Guida completa
url: /it/python/integration-and-interoperability/how-to-lazy-load-excel-data-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come Caricare Pigramente Dati Excel in Python – Guida Completa

Caricare pigramente grandi cartelle di lavoro Excel in Python è una sfida comune per chiunque gestisca gigabyte di righe. Hai mai aperto un foglio di calcolo e visto il tuo script fermarsi? In questo tutorial scoprirai **come caricare pigramente** i dati in modo efficiente, **come collegare il foglio di lavoro** agli oggetti, **come limitare le colonne**, e **come ottenere la configurazione** per il componente GridJs lato client—tutto usando il semplice flusso di lavoro `load excel workbook python`.

Ti guideremo passo passo, dall’apertura del workbook alla stampa della configurazione JSON che alimenta l’endpoint REST a caricamento pigro. Alla fine avrai uno script pronto all’uso che può servire blocchi da 500 righe su richiesta, mantenendo basso l’utilizzo di memoria e alta la reattività dell’interfaccia. Niente fronzoli, solo codice pratico e la logica dietro ogni riga.

---

## What You’ll Need

- Python 3.9+ (l'ultima versione stabile è la migliore)
- Il pacchetto `cells` (o qualsiasi libreria che espone una classe `Workbook` compatibile con GridJs)
- `gridjs` binding per Python (installati tramite `pip install gridjs`)
- Un file Excel (`big-data.xlsx`) di almeno qualche megabyte
- Un editor di testo o IDE con cui ti trovi a tuo agio (VS Code, PyCharm, o anche un buon notebook)

Se li hai già, ottimo—tuffiamoci. Altrimenti, procurali subito; la configurazione richiede solo un paio di minuti.

---

## Step 1: Load Excel Workbook in Python

Prima di tutto: devi **load excel workbook python** nello stile corretto. Il costruttore `cells.Workbook` legge il file e ti dà accesso ai fogli di lavoro come oggetti simili a liste.

```python
# Step 1: Open the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/big-data.xlsx")
ws = wb.worksheets[0]  # Grab the first sheet; adjust index if needed
```

> **Why this matters:** Caricare l’intero workbook in memoria può essere costoso. Prelevando solo il riferimento al foglio di lavoro, mantieni l’oggetto leggero finché GridJs non richiede i dati. Questa è la base per **how to lazy load** in seguito.

---

## Step 2: Bind the Worksheet to GridJs

Ora rispondiamo alla domanda **how to bind worksheet** a un’istanza GridJs. Il binding indica a GridJs da dove estrarre le righe quando il front‑end richiede una pagina.

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)   # This links the worksheet to the grid
```

> **Pro tip:** Se hai più fogli, puoi chiamare `grid.set_worksheet(ws, name="Sheet2")` per mantenerli separati. Il binding è un’operazione una tantum; non dovrai ripeterla per ogni richiesta di caricamento pigro.

---

## Step 3: Enable Lazy‑Loading (The Core of How to Lazy Load)

Ecco il cuore di **how to lazy load**: attiva il flag lazy‑load e configura la dimensione della pagina. GridJs esporrà ora un endpoint REST che serve le righe su richiesta invece di scaricare l’intero foglio.

```python
# Step 3: Enable lazy‑loading to fetch data on demand
grid.settings.lazy_load.enabled = True
```

> **What’s happening under the hood?** Quando `enabled` è `True`, GridJs registra una rotta Flask (o FastAPI) che accetta i parametri `offset` e `limit`. Ogni richiesta preleva solo la fetta richiesta dal foglio di lavoro, riducendo drasticamente la pressione sulla memoria.

---

## Step 4: Define the Page Size

Scegliere il giusto `page_size` è parte di **how to lazy load** in modo efficiente. Troppo piccolo e inonderai il client di chiamate HTTP; troppo grande e vanificherai lo scopo del caricamento pigro.

```python
# Step 4: Define how many rows are returned per request (page size)
grid.settings.lazy_load.page_size = 500   # 500 rows per call
```

> **Typical values:** 200–1000 righe funzionano bene per la maggior parte dei browser. Se prevedi utenti mobile su connessioni lente, orientati verso il valore più basso.

---

## Step 5: Limit the Columns Sent to the Client (Answering How to Limit Columns)

Spesso non ti servono tutte le colonne—magari ti interessano solo ID, nomi e date. Qui entra in gioco **how to limit columns**.

```python
# Step 5 (optional): Limit the columns that will be sent to the client
grid.settings.lazy_load.columns = ["A", "B", "C", "D"]
```

> **Why limit columns?** Ridurre la dimensione del payload velocizza il rendering e riduce l’uso di banda. Le lettere delle colonne corrispondono all’indicizzazione basata su A di Excel; puoi anche passare indici numerici se la tua libreria li preferisce.

---

## Step 6: Retrieve the Client‑Side Configuration (How to Get Config)

Infine, rispondiamo a **how to get config**. Il JSON di configurazione contiene l’URL dell’endpoint REST, le impostazioni di lazy‑load e i metadati delle colonne—tutto ciò di cui il front‑end ha bisogno per iniziare a prelevare i dati.

```python
# Step 6: Retrieve the client‑side configuration (includes the REST endpoint)
config_json = grid.get_client_config()
print(config_json)
```

L’output appare più o meno così (formattato per leggibilità):

```json
{
  "endpoint": "/gridjs/data",
  "lazy_load": {
    "enabled": true,
    "page_size": 500,
    "columns": ["A", "B", "C", "D"]
  },
  "worksheet": "Sheet1"
}
```

> **How to use it:** Inserisci questo JSON nella tua inizializzazione JavaScript di GridJs. La libreria chiamerà automaticamente `/gridjs/data?offset=0&limit=500` e renderà la prima pagina.

---

## Full Working Example

Di seguito trovi lo script completo, eseguibile, che mette insieme tutti i pezzi. Copialo, aggiusta il percorso del file e avvia `python lazy_gridjs.py`.

```python
#!/usr/bin/env python3
# lazy_gridjs.py – Demonstrates how to lazy load Excel data with GridJs

import cells          # Assumes 'cells' library is installed
import gridjs         # GridJs Python bindings

def main():
    # 1️⃣ Load the workbook (load excel workbook python)
    wb = cells.Workbook("YOUR_DIRECTORY/big-data.xlsx")
    ws = wb.worksheets[0]          # Grab the first sheet

    # 2️⃣ Bind the worksheet (how to bind worksheet)
    grid = gridjs.GridJs()
    grid.set_worksheet(ws)

    # 3️⃣ Turn on lazy loading (how to lazy load)
    grid.settings.lazy_load.enabled = True

    # 4️⃣ Set page size – tweak as needed
    grid.settings.lazy_load.page_size = 500

    # 5️⃣ Optional: limit columns (how to limit columns)
    grid.settings.lazy_load.columns = ["A", "B", "C", "D"]

    # 6️⃣ Pull the client config (how to get config)
    config_json = grid.get_client_config()
    print("=== GridJs Client Configuration ===")
    print(config_json)

    # Optional: start a simple server if you want to test the endpoint
    # grid.run_server(host="127.0.0.1", port=8000)  # Uncomment to launch

if __name__ == "__main__":
    main()
```

**Running the script** stampa il JSON di configurazione e, se decommenti `grid.run_server(...)`, avrai un piccolo server HTTP pronto a servire blocchi caricati pigramente. Apri il browser, punta GridJs all’endpoint stampato e osserva i dati apparire pagina per pagina.

---

## Common Questions & Edge Cases

### Cosa succede se il mio workbook ha più fogli?

Puoi chiamare `grid.set_worksheet(ws, name="MySheet")` per ogni foglio che vuoi esporre. Poi, quando **how to get config**, il JSON conterrà un campo `worksheet` che potrai cambiare lato client.

### Come gestisce GridJs le righe vuote?

Il caricamento pigro salta le righe completamente vuote per impostazione predefinita. Se devi mantenerle (ad esempio per preservare i numeri di riga), imposta `grid.settings.lazy_load.include_empty = True`.

### Posso cambiare l'ordine delle colonne?

Assolutamente. Sostituisci la lista `columns` con l’ordine esatto che desideri: `["D", "B", "A", "C"]`. Il client riceverà le celle in quella sequenza.

### È sicuro esporre l'endpoint pubblicamente?

Tratta l’endpoint come qualsiasi altra API: aggiungi middleware di autenticazione, limitazione di velocità o whitelist IP se i dati sono sensibili. Il meccanismo di lazy‑load di per sé non introduce problemi di sicurezza.

---

## Performance Tips (Pro Tips)

- **Cache del foglio di lavoro**: Se stai servendo molti utenti concorrenti, mantieni l'oggetto `Workbook` in memoria invece di ricaricarlo per ogni richiesta.
- **Regola `page_size` in base alla latenza**: Prova sia 200 che 1000 righe; scegli il punto ottimale dove l'interfaccia risponde rapidamente.
- **Comprimi il JSON**: Abilita gzip sul tuo server; un payload di 500 righe si comprime a pochi kilobyte.
- **Monitora la memoria**: Usa `tracemalloc` o strumenti simili per assicurarti che il lazy loader non carichi involontariamente l'intero foglio in RAM.

---

## Conclusion

Ora sai **how to lazy load** dati Excel in Python, **how to bind worksheet** agli oggetti GridJs, **how to limit columns**, e **how to get config** per un’integrazione front‑end senza intoppi. Seguendo i passaggi sopra, trasformerai un enorme file `big-data.xlsx` in una griglia reattiva, on‑demand, che scala con eleganza.

Cosa fare dopo? Prova a sostituire l’endpoint REST con un wrapper GraphQL, sperimenta valori diversi di `page_size`, o aggiungi formattazione delle colonne (date, valute) prima di inviare i dati al client. Lo stesso schema funziona per file CSV, Google Sheets o persino tabelle di database—

## What Should You Learn Next?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come Caricare File Excel Efficientemente Usando Aspose.Cells in .NET](/cells/english/net/workbook-operations/efficient-excel-load-aspose-cells-net/)
- [Come Caricare File Excel senza Grafici Usando Aspose.Cells per Java: Guida Completa](/cells/english/java/workbook-operations/efficient-excel-loading-aspose-cells-java/)
- [Come Caricare e Modificare File Excel Usando Aspose.Cells per .NET: Guida Completa](/cells/english/net/workbook-operations/load-modify-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}