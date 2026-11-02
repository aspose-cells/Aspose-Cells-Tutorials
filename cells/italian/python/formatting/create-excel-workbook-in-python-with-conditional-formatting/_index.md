---
category: general
date: 2026-09-05
description: Crea una cartella di lavoro Excel in Python e aggiungi una formattazione
  condizionale per evidenziare le celle di ieri. Scopri il codice completo e perché
  ogni passaggio è importante.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: it
lastmod: 2026-09-05
og_description: Crea una cartella di lavoro Excel in Python e aggiungi una formattazione
  condizionale per evidenziare le celle di ieri. Segui questa guida passo‑passo per
  una soluzione completa.
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: Crea una cartella di lavoro Excel in Python – aggiungi formattazione condizionale
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create Excel workbook in Python and add conditional formatting to highlight
    yesterday cells. Learn the full code and why each step matters.
  headline: Create Excel workbook in Python with conditional formatting
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Crea una cartella di lavoro Excel in Python con formattazione condizionale
url: /it/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea una cartella di lavoro Excel in Python con formattazione condizionale

Se hai bisogno di **create Excel workbook python** per un compito di reporting, questa guida ti mostra come generare una cartella di lavoro e applicare una regola di formattazione condizionale che evidenzia le date di ieri. Vedrai il codice esatto, perché esiste ogni riga e come adattare la soluzione ad altri intervalli di date.

La formattazione condizionale è un modo potente per attirare l'attenzione sui dati che soddisfano una condizione specifica. In questo tutorial utilizziamo la libreria Aspose.Cells per Python via .NET, che fornisce il supporto completo alle funzionalità di Excel senza richiedere Microsoft Office. Alla fine della guida avrai un file in cui le celle dell'intervallo *I19:K20* diventano rosa quando contengono la data di ieri.

## Prerequisiti

* Python 3.9+ installato
* Pacchetto `aspose-cells` (installare con `pip install aspose-cells`)
* Familiarità di base con la sintassi Python
* Permesso di scrittura nella directory in cui verrà salvata la cartella di lavoro

Il codice funziona su Windows, macOS e Linux purché il runtime .NET sia disponibile.

## Crea una cartella di lavoro Excel in Python

Il primo passo è istanziare un oggetto `Workbook` e ottenere il foglio di lavoro predefinito. Questo oggetto rappresenta l'intero file Excel in memoria.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Perché è importante*: `Workbook()` crea una cartella di lavoro vuota con un singolo foglio. Accedere a `worksheets[0]` ti fornisce un riferimento per aggiungere dati, stili e formattazione in seguito.

## Aggiungi l'intervallo di formattazione condizionale

Successivamente definiamo l'area che sarà valutata dalla regola condizionale. L'intervallo `I19:K20` copre sei celle su due righe.

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*Perché è importante*: Aggiungere una collezione di formattazione condizionale a uno specifico intervallo isola la regola, impedendone l'applicazione a celle non correlate. Questo soddisfa il requisito **add conditional formatting range**.

## Definisci la regola: evidenzia le celle in base alla data

Ora creiamo una condizione di tipo `TIME_PERIOD`. Questo indica a Excel di confrontare il valore di ogni cella con una finestra temporale predefinita.

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*Perché è importante*: `TIME_PERIOD` è l'unico tipo incorporato che supporta direttamente “Yesterday”, “Today”, “Last Week”, ecc. Impostando `condition.time_period` su `YESTERDAY`, la regola valuta automaticamente il valore di data di ogni cella rispetto al giorno precedente alla data corrente.

## Stile delle celle che soddisfano la condizione

La formattazione condizionale richiede anche uno stile visivo. Qui scegliamo un riempimento solido rosa per far risaltare le celle corrispondenti.

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*Perché è importante*: L'oggetto stile definisce come Excel renderà le celle che soddisfano la condizione. Usare un riempimento solido rosa soddisfa il requisito **highlight cells based on date** e rende il risultato facile da verificare.

## Popola date di esempio per la valutazione

Per vedere la regola in azione inseriamo due date — una che corrisponde alla data di ieri e una che non lo è. Il formato `number` `30` corrisponde al formato data incorporato `mm-dd-yy`.

```python
from datetime import datetime

# Cell I19: a date that matches “Yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Example date; adjust as needed
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

# Cell K20: a date outside the “Yesterday” period
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Example date; adjust as needed
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Optional label for the range
worksheet.cells.get("I20").put_value("Yesterday")
```

*Perché è importante*: Fornire sia una data corrispondente sia una non corrispondente ti permette di verificare che la formattazione condizionale funzioni correttamente. Regola le date al mese corrente quando esegui lo script, o sostituiscile con valori dinamici.

## Salva la cartella di lavoro

Infine scriviamo il file su disco. La costante `SaveFormat.XLSX` garantisce che l'output sia un file Excel moderno.

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*Perché è importante*: Persistere la cartella di lavoro ti consente di aprirla in Excel, LibreOffice o qualsiasi visualizzatore che supporti XLSX. Il percorso stampato conferma dove è stato scritto il file.

## Script completo

Mettendo insieme tutti i pezzi, lo script completo e eseguibile è il seguente:

```python
# -*- coding: utf-8 -*-
"""
Create an Excel workbook in Python, add a conditional formatting rule,
and highlight yesterday's cells.
"""

from aspose.cells import (
    Workbook, SaveFormat, FormatConditionType,
    BackgroundType, TimePeriodType
)
from aspose.pydrawing import Color as DrawingColor
from datetime import datetime

# Step 1: Create a new workbook and access the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Add a conditional formatting rule for the range I19:K20
condition_collection = worksheet.conditional_formattings.add("I19:K20")
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Step 3: Define the visual style for cells that meet the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID

# Step 4: Set the time‑period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Step 5: Populate sample dates for evaluation
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # yesterday relative to the example
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # outside the period
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Step 6: Add a label for the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Output previsto

Quando apri `TimePeriodExample.xlsx`:

* La cella **I19** appare con uno sfondo rosa perché il suo valore corrisponde a ieri.
* La cella **K20** mantiene lo sfondo predefinito perché la sua data è fuori dal periodo.
* L'etichetta **“Yesterday”** è nella cella I20 per chiarezza.

## Variazioni comuni e casi limite

| Situazione | Adeguamento |
|-----------|------------|
| **Highlight today instead of yesterday** | Cambia `condition.time_period = TimePeriodType.TODAY`. |
| **Apply the rule to a larger area** | Aggiorna la stringa dell'intervallo in `add("I19:K20")` a qualcosa come `"A1:Z100"`. |
| **Use a different fill color** | Sostituisci `DrawingColor.pink` con qualsiasi altro `DrawingColor` (es., `DrawingColor.light_green`). |
| **Work with dynamic dates** | Calcola `datetime.now() - timedelta(days=1)` per ieri e scrivi quel valore nelle celle prima di applicare la regola. |

**Suggerimento professionale:** Quando generi la cartella di lavoro programmaticamente per molti utenti, mantieni la definizione della formattazione condizionale separata dall'inserimento dei dati. In questo modo puoi riutilizzare lo stesso stile su più fogli senza duplicare il codice.

## Verifica il risultato programmaticamente (opzionale)

Se vuoi confermare la formattazione senza aprire Excel, puoi ispezionare lo stile di una cella dopo il salvataggio:



## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Excel Automation&#58; Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Create Excel Workbook and Add Labels with Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}