---
category: general
date: 2026-10-07
description: Crea una cartella di lavoro Excel in Python, imposta il colore di sfondo
  delle celle, adatta automaticamente le colonne e inserisci le date in Excel con
  un esempio di codice conciso.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: it
lastmod: 2026-10-07
og_description: Crea una cartella di lavoro Excel in Python, quindi imposta il colore
  di sfondo delle celle, adatta automaticamente le colonne e inserisci le date in
  Excel. Segui questa guida passo passo per generare il file TimePeriodDemo.xlsx.
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: Crea cartella di lavoro Excel in Python – imposta lo sfondo e adatta automaticamente
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  headline: Create Excel workbook in Python and set cell background
  type: TechArticle
- description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  name: Create Excel workbook in Python and set cell background
  steps:
  - name: Import required namespaces and define a helper function
    text: '```python # Step 1: Import Aspose.Cells classes and supporting modules
      from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType,
      SaveFormat from aspose.pydrawing import Color from datetime import datetime
      import os ```'
  - name: Create the workbook and get the first worksheet
    text: '```python def create_workbook(): # Step 2: Instantiate a new workbook (empty
      Excel file) book = Workbook() # Aspose.Cells creates a default worksheet; we
      retrieve it for further work sheet = book.worksheets[0] return book, sheet ```'
  - name: Set cell background color with a conditional format
    text: '```python def add_yesterday_rule(sheet): # Define a conditional format
      for the range I19:K20 (Yesterday) conds = sheet.get_range("I19:K20").format_conditions
      idx = conds.add_condition(FormatConditionType.TIME_PERIOD) cond = conds[idx]'
  - name: Populate dates in Excel
    text: '```python def populate_sample_dates(sheet): # Insert a date that falls
      on yesterday relative to the demo data cell = sheet.cells.get("I19") cell.put_value(datetime(2008,
      7, 30)) # sample date cell.style.number = 30 # Excel’s date format ID cell.set_style(cell.style)'
  - name: Auto‑fit Excel columns for better visibility
    text: '```python def auto_fit_columns(sheet): # Auto‑fit column L (index 12) so
      the content is fully visible sheet.auto_fit_column(12) # <-- auto fit excel
      columns ```'
  - name: Save the workbook
    text: '```python def save_workbook(book, filename="TimePeriodDemo.xlsx"): out_path
      = os.path.join("YOUR_DIRECTORY", filename) os.makedirs(os.path.dirname(out_path),
      exist_ok=True) book.save(out_path, SaveFormat.XLSX) print(f"Workbook saved to:
      {out_path}") ```'
  - name: Full script – putting it all together
    text: '```python def main(): # Create workbook and obtain the first worksheet
      book, sheet = create_workbook()'
  type: HowTo
tags:
- Excel
- Python
- Aspose.Cells
title: Crea una cartella di lavoro Excel in Python e imposta lo sfondo della cella
url: /it/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea una cartella di lavoro Excel in Python e imposta lo sfondo della cella

Crea una cartella di lavoro Excel in Python e applica la formattazione condizionale con poche righe di codice. Questo tutorial ti mostra **come creare excel** programmaticamente, impostare il colore di sfondo della cella, adattare automaticamente le colonne di Excel e inserire date in Excel usando la libreria Aspose.Cells.

Imparerai a:
* Inizializzare una cartella di lavoro e ottenere il primo foglio di lavoro.  
* Definire una formattazione condizionale che evidenzia le date di “Yesterday”.  
* Inserire date di esempio in celle specifiche.  
* Adattare automaticamente le colonne affinché i dati siano chiaramente visibili.  
* Salvare la cartella di lavoro in una cartella scelta.

L'unico prerequisito è un ambiente Python 3 funzionante con i pacchetti `aspose-cells` e `aspose-pydrawing` installati:

```bash
pip install aspose-cells aspose-pydrawing
```

---

## Crea una cartella di lavoro Excel in Python – passo passo

Le sezioni seguenti suddividono il processo in passaggi gestibili. Ogni passaggio include il codice necessario, una spiegazione del **perché** è importante e un suggerimento per evitare errori comuni.

### Passo 1: Importa gli spazi dei nomi richiesti e definisci una funzione di supporto

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*Perché è importante*: Importare le classi corrette ti dà accesso alla creazione della cartella di lavoro, alla formattazione condizionale e alla gestione dei colori.  
**Suggerimento professionale**: Mantieni le importazioni in cima al file; rende lo script più facile da leggere e previene errori di importazione circolare.

### Passo 2: Crea la cartella di lavoro e ottieni il primo foglio di lavoro

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

Il costruttore `Workbook()` crea una cartella di lavoro Excel vuota in memoria.  
**Perché**: Iniziare con una cartella di lavoro nuova garantisce che non ci siano formattazioni residue da esecuzioni precedenti.

### Passo 3: Imposta il colore di sfondo della cella con una formattazione condizionale

```python
def add_yesterday_rule(sheet):
    # Define a conditional format for the range I19:K20 (Yesterday)
    conds = sheet.get_range("I19:K20").format_conditions
    idx = conds.add_condition(FormatConditionType.TIME_PERIOD)
    cond = conds[idx]

    # Apply visual style – this is where we set the cell background color
    cond.style.background_color = Color.pink          # <-- set cell background color
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

*Perché*: Usare una condizione di **time period** evidenzia automaticamente qualsiasi cella che contiene la data di ieri, eliminando i controlli manuali delle date.  
**Suggerimento**: `Color.pink` è solo un esempio; puoi usare qualsiasi oggetto `Color` (`Color.yellow`, `Color.light_green`, ecc.).

### Passo 4: Inserisci date in Excel

```python
def populate_sample_dates(sheet):
    # Insert a date that falls on yesterday relative to the demo data
    cell = sheet.cells.get("I19")
    cell.put_value(datetime(2008, 7, 30))   # sample date
    cell.style.number = 30                 # Excel’s date format ID
    cell.set_style(cell.style)

    # Insert another date outside the “Yesterday” range
    cell = sheet.cells.get("K20")
    cell.put_value(datetime(2008, 8, 3))
    cell.style.number = 30
    cell.set_style(cell.style)

    # Add a label for the rule
    sheet.cells.get("I20").put_value("Yesterday")
```

Qui **inseriamo date in Excel** nelle celle `I19` e `K20`. La prima data attiverà la formattazione condizionale, mentre la seconda no.  
**Perché è importante**: Dimostrare sia valori corrispondenti sia non corrispondenti ti aiuta a verificare che la regola funzioni come previsto.

### Passo 5: Adatta automaticamente le colonne di Excel per una migliore visibilità

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

`auto_fit_column` regola la larghezza della colonna in base al valore più lungo della cella.  
**Suggerimento**: Richiama questo metodo dopo aver scritto tutti i dati; altrimenti la larghezza potrebbe essere calcolata su contenuto incompleto.

### Passo 6: Salva la cartella di lavoro

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

Salvare il file scrive la cartella di lavoro in memoria su disco nel formato XLSX moderno.  

### Script completo – mettere tutto insieme

```python
def main():
    # Create workbook and obtain the first worksheet
    book, sheet = create_workbook()

    # Apply conditional formatting (set cell background color)
    add_yesterday_rule(sheet)

    # Populate the demo dates (populate dates in excel)
    populate_sample_dates(sheet)

    # Auto‑fit the relevant column (auto fit excel columns)
    auto_fit_columns(sheet)

    # Persist the file
    save_workbook(book)

if __name__ == "__main__":
    main()
```

**Expected output**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Apri il file generato in Excel – le celle `I19:K20` mostreranno uno sfondo rosa per la data che corrisponde a “Yesterday”, e la colonna L sarà sufficientemente larga da visualizzare l'etichetta senza tagli.

---

## Perché questo approccio funziona al meglio

* **Flusso di lavoro a singola passata** – Tutte le operazioni avvengono sulla stessa istanza `Workbook`, evitando I/O non necessario.  
* **Formattazione condizionale** – Usare `FormatConditionType.TIME_PERIOD` permette a Excel di gestire la logica delle date, più affidabile rispetto a scrivere controlli di data personalizzati in Python.  
* **Stile esplicito** – Impostare `background_color` e `pattern` garantisce il risultato visivo su tutte le versioni di Excel.  
* **Auto‑fit dopo i dati**

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea cartella di lavoro Excel Python – Guida completa](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Crea cartella di lavoro Excel Python – Guida completa passo‑passo](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Crea cartella di lavoro Excel Python – Guida completa con Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}