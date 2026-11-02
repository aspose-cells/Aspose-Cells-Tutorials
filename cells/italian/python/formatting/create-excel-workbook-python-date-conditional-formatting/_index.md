---
category: general
date: 2026-08-08
description: Crea un workbook Excel in Python e aggiungi una formattazione condizionale
  basata sulla data. Guida passo‑passo con Aspose.Cells per evidenziare le celle di
  ieri.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: it
lastmod: 2026-08-08
og_description: Crea una cartella di lavoro Excel in Python con Aspose.Cells e applica
  la formattazione condizionale basata sulla data per fogli di calcolo dinamici.
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: Crea cartella di lavoro Excel con Python – formattazione condizionale per
  data
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Create Excel workbook Python and add conditional formatting based on
    date. Step‑by‑step guide using Aspose.Cells to highlight yesterday’s cells.
  headline: Create Excel workbook Python date conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Crea una cartella di lavoro Excel con formattazione condizionale di data in
  Python
url: /it/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea un workbook Excel con Python e formattazione condizionale basata sulla data

Se hai bisogno di **creare un workbook Excel con Python** e evidenziare automaticamente le celle che corrispondono a una data specifica, questo tutorial ti mostra esattamente come fare. Imparerai ad applicare **formattazione condizionale basata sulla data** in modo che le date di ieri vengano evidenziate in rosa, utilizzando la libreria Aspose.Cells.

La guida percorre ogni passaggio — dall'installazione dell'SDK al salvataggio del file .xlsx finale — così potrai copiare‑incollare un esempio funzionante nel tuo progetto. Non è necessaria alcuna documentazione esterna; tutto il codice e le spiegazioni sono auto‑contenuti.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* Python 3.8 o versioni successive installate.  
* Pacchetto `aspose-cells` (il wrapper Python per Aspose.Cells). Installalo con:
  ```bash
  pip install aspose-cells
  ```
* Familiarità di base con Python e i concetti di Excel come fogli di lavoro e stili di cella.

> **Suggerimento:** Aspose.Cells funziona senza la necessità di avere Microsoft Excel installato, rendendolo ideale per l'automazione lato server.

## Passo 1: Crea il workbook Excel in Python

Il primo compito è istanziare un nuovo workbook e ottenere il foglio di lavoro predefinito. Questo oggetto rappresenta l'intero file Excel e fornisce l'accesso a righe, colonne e API di formattazione.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

Creare il workbook è la base per qualsiasi ulteriore manipolazione, sia che tu stia aggiungendo dati, formule o regole di formattazione.

## Passo 2: Definisci una formattazione condizionale basata sulla data

Ora aggiungiamo **formattazione condizionale basata sulla data**. L'enumerazione `FormatConditionType.TIME_PERIOD` ci consente di specificare periodi di tempo predefiniti come Yesterday, Today o LastWeek.

```python
from aspose.cells import FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color

# Target range I19:K20 – three columns by two rows
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions

# Add a new time‑period condition (e.g., Yesterday)
condition_index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[condition_index]

# Set the visual style: pink solid background
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Specify that the condition should trigger for "Yesterday"
condition.time_period = TimePeriodType.YESTERDAY
```

Perché questo passaggio è importante: Excel valuta la condizione per ogni cella nell'intervallo. Quando il valore di una cella ricade nel periodo definito (ieri), lo stile che abbiamo assegnato viene applicato automaticamente.

## Passo 3: Popola l'intervallo con date di esempio

Per vedere la regola in azione, scriviamo un paio di oggetti `datetime` nelle celle target. Uno di essi è deliberatamente impostato alla data di ieri rispetto al sistema di data interno del workbook.

```python
from datetime import datetime

# Cell I19 – yesterday’s date (will be highlighted)
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # This date matches the "Yesterday" rule
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel’s built‑in date format
cell_i19.set_style(style_i19)

# Cell K20 – a random later date (no highlight)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Not yesterday, so no formatting
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

La riga `number = 30` indica a Excel di visualizzare il valore usando il suo formato data breve standard. Puoi cambiare questo indice con qualsiasi formato numerico predefinito se preferisci una presentazione diversa.

## Passo 4: Regola la larghezza della colonna per una migliore leggibilità

L'adattamento automatico della colonna che contiene le date rende l'output più facile da leggere, soprattutto quando il workbook viene aperto in Excel o in un visualizzatore.

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## Passo 5: Salva il workbook su disco

Infine, salva il workbook come file .xlsx. Sostituisci `"YOUR_DIRECTORY"` con un percorso reale sulla tua macchina.

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Quando apri `TimePeriodDemo.out.xlsx` in Excel, la cella **I19** apparirà con uno sfondo rosa perché il suo valore corrisponde alla regola “Yesterday”, mentre **K20** rimarrà invariata.

### Output previsto

| I19 (data) | I20 (etichetta) | J19 | J20 | K19 | K20 (data) |
|------------|-----------------|-----|-----|-----|------------|
| *2008‑07‑30* (sfondo rosa) | Yesterday | – | – | – | *2008‑08‑03* (nessuna formattazione) |

L'ombreggiatura rosa conferma che **la formattazione condizionale basata sulla data** funziona come previsto.

## Varianti comuni e casi limite

| Situazione | Come adattare il codice |
|------------|--------------------------|
| **Evidenziare “Today” invece di “Yesterday”** | Cambia `condition.time_period = TimePeriodType.TODAY` |
| **Applicare la regola a un'intera colonna** | Usa `worksheet.get_range("A:A").format_conditions` |
| **Usare un intervallo di date personalizzato (es. ultimi 7 giorni)** | Sostituisci la condizione di periodo di tempo con una condizione di formula: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **Colori di sfondo diversi** | Imposta `condition.style.background_color = Color.light_green` (o qualsiasi `Color` preferisci) |
| **Esecuzione su Linux senza display** | Aspose.Cells è completamente headless; non è necessaria alcuna configurazione aggiuntiva. |

## Esempio completo, eseguibile

Di seguito trovi lo script completo che puoi eseguire così com'è (dopo aver aggiornato la directory di output). Sono inclusi tutti gli import, i commenti e le basi della gestione degli errori.

```python
# -*- coding: utf-8 -*-
"""
Create Excel workbook Python with date conditional formatting.
Demonstrates how to highlight yesterday’s dates using Aspose.Cells.
"""

import os
from datetime import datetime
from aspose.cells import (
    Workbook, SaveFormat,
    FormatConditionType, BackgroundType,
    TimePeriodType
)
from aspose.pydrawing import Color

# ----------------------------------------------------------------------
# 1️⃣ Initialize workbook
# ----------------------------------------------------------------------
workbook = Workbook()
worksheet = workbook.worksheets[0]

# ----------------------------------------------------------------------
# 2️⃣ Add conditional formatting for "Yesterday"
# ----------------------------------------------------------------------
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions
cond_idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[cond_idx]

# Visual style: pink solid fill
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
condition.time_period = TimePeriodType.YESTERDAY

# ----------------------------------------------------------------------
# 3️⃣ Populate sample dates
# ----------------------------------------------------------------------
# Cell that should match the condition
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Yesterday relative to demo data
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel short‑date format
cell_i19.set_style(style_i19)

# Cell that does NOT match
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label
worksheet.cells.get("I20").put_value("Yesterday")

# ----------------------------------------------------------------------
# 4️⃣ Auto‑fit column for better visibility
# ----------------------------------------------------------------------
worksheet.auto_fit_column(12)   # Column L (0‑based index)

# ----------------------------------------------------------------------
# 5️⃣ Save workbook
# ----------------------------------------------------------------------
output_dir = "YOUR_DIRECTORY"   # <-- replace with a real folder
os.makedirs(output_dir, exist_ok=True)
output_path = os.path.join(output_dir, "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Eseguendo lo script si genera un file Excel in cui la cella “Yesterday” viene evidenziata automaticamente, dimostrando **creare un workbook Excel con Python** combinato con **formattazione condizionale basata sulla data**.

## Conclusione

Ora sai come **creare oggetti workbook Excel con Python**, definire una **formattazione condizionale basata sulla data** e salvare il risultato.

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Create Excel Workbook with Charts Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}