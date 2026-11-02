---
category: general
date: 2026-10-04
description: Creare un workbook Excel in Python usando Aspose.Cells. Impara la formattazione
  condizionale di Excel in Python, il colore di sfondo delle celle in Python e la
  formattazione delle date delle celle in Python in un esempio completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: it
lastmod: 2026-10-04
og_description: Crea un workbook Excel in Python con Aspose.Cells. Questo tutorial
  mostra la formattazione condizionale di Excel in Python, il colore di sfondo delle
  celle in Python e la formattazione delle date delle celle in Python passo dopo passo.
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: Crea un workbook Excel con Python – guida completa con formattazione condizionale
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  headline: Create Excel workbook python with conditional formatting and cell background
    color
  type: TechArticle
- description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  name: Create Excel workbook python with conditional formatting and cell background
    color
  steps:
  - name: '**create Excel workbook python** using the Aspose.Cells library.'
    text: '**create Excel workbook python** using the Aspose.Cells library.'
  - name: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
    text: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
  - name: Set the **cell background color python** to pink (or any color you prefer).
    text: Set the **cell background color python** to pink (or any color you prefer).
  - name: '**format cells date python** so the dates appear in the standard Excel
      date style.'
    text: '**format cells date python** so the dates appear in the standard Excel
      date style.'
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Crea una cartella di lavoro Excel in Python con formattazione condizionale
  e colore di sfondo delle celle
url: /it/python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea cartella di lavoro Excel python con formattazione condizionale e colore di sfondo della cella

Se hai bisogno di **create Excel workbook python** rapidamente, questa guida ti mostra esattamente come. Vedrai un esempio completo e eseguibile che aggiunge **excel conditional formatting python**, cambia il **cell background color python**, e **format cells date python** per un evidenziazione “Yesterday”.  

In molti scenari di reporting, l'indicatore visivo di una cella colorata rende i dati immediatamente comprensibili. Questo tutorial ti guida attraverso ogni riga di codice, spiega perché ogni passaggio è importante e ti fornisce uno script pronto‑da‑eseguire che puoi adattare ai tuoi progetti.

## Cosa otterrai

1. **create Excel workbook python** utilizzando la libreria Aspose.Cells.  
2. Applica **excel conditional formatting python** che evidenzia automaticamente le date che corrispondono a “Yesterday”.  
3. Imposta il **cell background color python** su rosa (o qualsiasi altro colore tu preferisca).  
4. **format cells date python** in modo che le date appaiano nello stile data standard di Excel.  

Non è necessaria alcuna esperienza pregressa con Aspose.Cells—basta un ambiente Python 3 funzionante e l'accesso a pip.

## Prerequisiti

- Python 3.8 o versioni successive installato.  
- `aspose-cells` e `aspose-pydrawing` pacchetti installati tramite `pip install aspose-cells aspose-pydrawing`.  
- Familiarità di base con la sintassi Python e i concetti di Excel (cartelle di lavoro, fogli di lavoro, celle).  

> **Pro tip:** Se esegui lo script in un ambiente virtuale, eviti conflitti di versione con altri progetti.

## Passo 1: Configura il progetto e importa le classi necessarie

Il primo passo quando **create Excel workbook python** è importare le classi Aspose.Cells di cui avrai bisogno. Queste classi ti danno accesso diretto alla creazione di cartelle di lavoro, alla formattazione condizionale e allo styling.

```python
# Import Aspose.Cells core classes
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)

# Import Aspose.PyDrawing for color handling
from aspose.pydrawing import Color

# Standard library for date values
from datetime import datetime
```

*Perché è importante:* Importare solo i simboli necessari mantiene pulito lo spazio dei nomi e rende lo script più leggibile. `Workbook` è il punto di ingresso per **create Excel workbook python**, mentre `FormatConditionType` e `TimePeriodType` sono essenziali per **excel conditional formatting python**.

## Passo 2: Crea una nuova cartella di lavoro e ottieni il primo foglio di lavoro

Ora creiamo effettivamente **create Excel workbook python**. Il costruttore `Workbook()` ti fornisce un file Excel vuoto con un foglio di lavoro predefinito.

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Spiegazione:* Ogni file Excel inizia con almeno un foglio di lavoro. Per impostazione predefinita Aspose.Cells lo chiama “Sheet1”. Puoi aggiungere altri fogli in seguito, ma per questa dimostrazione un unico foglio mantiene l'esempio focalizzato.

## Passo 3: Definisci l'intervallo di destinazione per la formattazione condizionale

La formattazione condizionale funziona su un intervallo rettangolare. Qui scegliamo l'intervallo `I19:K20`, che ci fornisce tre colonne e due righe su cui operare.

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*Perché lo facciamo:* Il metodo `get` restituisce un oggetto `ConditionalFormatting` collegato all'intervallo specificato. Se l'intervallo non ha ancora alcuna formattazione, Aspose.Cells crea automaticamente una nuova collezione.

## Passo 4: Aggiungi una condizione TIME_PERIOD e imposta il colore di sfondo

Questo è il nucleo di **excel conditional formatting python**. Aggiungiamo una regola `TIME_PERIOD` che evidenzia le celle contenenti date corrispondenti a “Yesterday”.

```python
# Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Access the newly created condition
condition = conditional_formatting[condition_index]

# Configure the condition to target “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Set the cell background color – this is the cell background color python part
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

*Approfondimento:*  
- `FormatConditionType.TIME_PERIOD` indica a Excel di valutare le date rispetto alla data corrente.  
- `TimePeriodType.YESTERDAY` è un enum integrato che si aggiorna automaticamente ogni giorno, così la cartella di lavoro evidenzia sempre il più recente “Yesterday”.  
- Impostando `background_color` su `Color.pink` e il pattern su `SOLID`, otteniamo l'effetto **cell background color python** senza codice VBA aggiuntivo.

## Passo 5: Popola l'intervallo con date di esempio e applica la formattazione delle date

Per vedere la formattazione condizionale in azione, abbiamo bisogno di valori data reali. Abbiamo anche bisogno di **format cells date python** affinché Excel li tratti come date anziché semplici numeri.

```python
# Helper function to set a cell's date style and value
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    # Excel’s built‑in date format code 30 = "m/d/yy"
    style.number = 30
    cell.set_style(style)
    cell.put_value(date_value)

# Populate I19 with a date that is “yesterday” relative to the sample data
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”

# Populate K20 with another arbitrary date
set_date("K20", datetime(2008, 8, 3))    # Not “yesterday”
```

*Spiegazione:*  
- La riga `style.number = 30` è il passaggio **format cells date python**. Il codice di formato 30 corrisponde al formato data breve (`m/d/yy`).  
- L'uso di una funzione di supporto mantiene il codice DRY (Don’t Repeat Yourself) e facilita l'aggiunta di altre date in seguito.

## Passo 6: Aggiungi un'etichetta descrittiva

Una piccola etichetta aiuta chiunque apra la cartella di lavoro a capire perché le celle sono colorate.

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## Passo 7: Salva la cartella di lavoro su disco

Infine, **create Excel workbook python** su disco chiamando `save`. La costante `SaveFormat.XLSX` garantisce che il file sia nel moderno formato Office Open XML.

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Quando apri `TimePeriodDemo.xlsx` in Excel, vedrai:

- Le celle `I19` e `K20` contengono date.  
- La cella che corrisponde a “Yesterday” (in questo esempio statico, `I19`) è evidenziata in rosa.  
- L'etichetta “Yesterday” appare in `I20`.  

> **Suggerimento:** Se esegui lo script in un giorno diverso, la formattazione condizionale evidenzia comunque la cella la cui data è esattamente un giorno prima della data di sistema corrente—non sono necessarie modifiche al codice.

## Script completo – pronto da copiare ed eseguire

Di seguito trovi il programma completo e autonomo che incorpora tutti i passaggi sopra. Copialo in un file chiamato `conditional_format_demo.py`, regola `YOUR_DIRECTORY` ed esegui con `python conditional_format_demo.py`.

```python
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the cell range that will receive the conditional format
target_range = "I19:K20"
conditional_formatting = worksheet.conditional_formattings.get(target_range)

# Step 3: Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Step 4: Configure the condition to highlight “Yesterday” dates
condition = conditional_formatting[condition_index]
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Helper to set date value and style
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    style.number = 30          # Excel date format code 30 = short date
    cell.set_style(style)
    cell.put_value(date_value)

# Step 5: Populate the range with sample dates (excel conditional formatting python)
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”
set_date("K20", datetime(2008, 8, 3))    # Another sample date

# Step 6: Add a label describing the condition
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Output previsto

L'esecuzione dello script stampa una riga di conferma:

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

L'apertura del file generato mostra lo sfondo rosa sulla cella che corrisponde alla regola “Yesterday”, confermando che **excel conditional formatting python** e **cell background color python** funzionano insieme.

## Varianti comuni e casi limite

| Situazione | Come adattare il codice |
|------------|--------------------------|
| **Different highlight color** | Modifica `Color.pink` in qualsiasi altra costante `Color`, ad esempio `Color.light_green`. |
| **Highlight “Today” instead of “Yesterday”** | Imposta `condition.time_period = TimePeriodType.TODAY`. |
| **Apply formatting to an entire column** | Usa un intervallo come `"A:A"` e regola di conseguenza la variabile `target_range`. |
| **Use a custom date format** | Sostituisci `style.number = 30` con `style.custom = "dd-mmm-yyyy"` per un formato più leggibile. |
| **Multiple conditions on the same range** |  |

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea cartella di lavoro Excel Python – Guida completa con Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [Crea e salva cartella di lavoro Excel come PDF in ASP.NET usando Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Come creare e salvare una cartella di lavoro Excel come ODS usando Aspose.Cells per .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}