---
category: general
date: 2026-07-14
description: Crea codice Python per un workbook Excel che imposta il colore di sfondo
  delle celle, evidenzia le celle in base all’intervallo di date e salva il workbook
  come XLSX in pochi minuti.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- save workbook as xlsx
- highlight cells based on date range
- conditional formatting based on date
language: it
lastmod: 2026-07-14
og_description: Crea un workbook Excel in Python istantaneamente. Impara a impostare
  il colore di sfondo delle celle, evidenziare le celle in base all'intervallo di
  date e salvare il workbook come XLSX con Aspose.Cells.
og_image_alt: Screenshot showing an Excel sheet created with Python highlighting yesterday's
  dates
og_title: Crea una cartella di lavoro Excel con Python – Formattazione condizionale
  passo passo
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Create Excel workbook Python code that sets cell background color,
    highlights cells based on date range, and saves workbook as XLSX in minutes.
  headline: Create Excel Workbook Python – Full Guide with Conditional Formatting
  type: TechArticle
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Crea cartella di lavoro Excel con Python – Guida completa con formattazione
  condizionale
url: /it/python/formatting/create-excel-workbook-python-full-guide-with-conditional-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea un Excel Workbook con Python – Guida Completa con Formattazione Condizionale

Ti sei mai chiesto come creare script **create excel workbook python** dall'aspetto professionale senza aprire Excel manualmente? Non sei l'unico. In molti progetti basati sui dati dobbiamo generare fogli di calcolo, colorare le celle e persino evidenziare date che rientrano in un intervallo specifico, tutto da puro codice Python.

In questo tutorial percorreremo un esempio completo, pronto‑all'uso, che **creates an Excel workbook python** usando la libreria Aspose.Cells, **sets cell background color**, applica **conditional formatting based on date** e infine **saves workbook as xlsx**. Alla fine avrai uno snippet riutilizzabile da inserire in qualsiasi pipeline di automazione.

## Cosa Imparerai

- Come inizializzare un workbook e accedere al primo foglio di lavoro.  
- Una funzione di supporto che aggiunge una collezione di conditional‑formatting per qualsiasi intervallo di celle.  
- Utilizzare **conditional formatting based on date** per evidenziare le voci di ieri.  
- Regolare la larghezza delle colonne per un layout ordinato.  
- Persistire il risultato con **save workbook as xlsx**.  

Non è necessaria alcuna installazione di Excel esterna—Aspose.Cells gestisce tutto in memoria.

## Prerequisiti

- Python 3.8+ installato.  
- `aspose-cells` package (`pip install aspose-cells`).  
- Familiarità di base con le funzioni Python e gli oggetti datetime.  

Se non hai mai usato Aspose.Cells, pensalo come una potente API pure‑Python che imita il modello a oggetti di Excel. È perfetta per la generazione lato server dove la suite Office non è disponibile.

## Passo 1: Inizializza il Workbook (Create Excel Workbook Python)

Prima di tutto: dobbiamo **create excel workbook python** in stile. Questo passo crea un oggetto workbook vuoto e ci punta al foglio di lavoro predefinito.

```python
# Step 1 – create a fresh workbook and get the first sheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, Color, SaveFormat
from datetime import datetime

workbook = Workbook()                     # <-- creates a new Excel file in memory
worksheet = workbook.worksheets[0]        # the default (first) sheet
```

> **Perché è importante:** La classe `Workbook` è il punto di ingresso per ogni operazione Excel. Creandola programmaticamente evitiamo qualsiasi gestione manuale dei file.

## Passo 2: Helper per Aggiungere una Collezione di Conditional‑Formatting (Set Cell Background Color)

Il conditional formatting vive all'interno di una *collezione* collegata a un intervallo. Avvolgiamo quel boilerplate in un piccolo helper che ci permette anche di **set cell background color** per l'intero intervallo.

```python
def add_time_period_condition(cell_range: str, highlight_color: Color):
    """
    Adds a conditional‑formatting collection to `cell_range` and
    applies `highlight_color` as the base fill.
    """
    worksheet.conditional_formattings.add(cell_range)   # attach to the range
    cf = worksheet.conditional_formattings[-1]           # grab the newly added collection
    cf.style.background_color = highlight_color
    cf.style.pattern = BackgroundType.SOLID
    return cf
```

> **Consiglio:** Usare un helper mantiene il flusso principale pulito e rende facile riutilizzare la stessa logica per più intervalli.

## Passo 3: Applica Conditional Formatting Based on Date (Evidenzia Celle in Base a Intervallo di Date)

Ora effettueremo realmente **highlight cells based on date range**. L'esempio si concentra su “yesterday” ma puoi sostituire `TimePeriodType.YESTERDAY` con `TODAY`, `LAST_WEEK`, ecc.

```python
# Step 3 – create a TIME_PERIOD rule for I19:K20 (yesterday)
cf = add_time_period_condition("I19:K20", Color.medium_sea_green)

condition_index = cf.add_condition(FormatConditionType.TIME_PERIOD)
condition = cf[condition_index]

# Define the visual style for the matching cells
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# The actual rule: any cell whose date is yesterday gets the pink fill
condition.time_period = TimePeriodType.YESTERDAY
```

> **Cosa sta succedendo?**  
> 1. Prima di tutto diamo all'intero intervallo uno sfondo verde neutro.  
> 2. Poi aggiungiamo una condizione `TIME_PERIOD` che sovrascrive il riempimento con rosa **solo** quando la data della cella corrisponde a ieri.  
> 3. L'enumerazione `TimePeriodType` astrae il calcolo della data, così non è necessario scrivere logica personalizzata.

## Passo 4: Popola Date di Esempio (Affinché la Regola Venga Valutata)

Per vedere la regola in azione inseriremo un paio di date nel foglio. Una cade nella finestra “yesterday”, l'altra no.

```python
# Populate I19 with a date that is yesterday (relative to the hard‑coded date)
date_cell = worksheet.cells.get("I19")
date_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008
date_style = date_cell.get_style()
date_style.number = 30                     # Excel’s built‑in date format
date_cell.set_style(date_style)

# Populate K20 with a date that is NOT yesterday
date_cell = worksheet.cells.get("K20")
date_cell.put_value(datetime(2008, 8, 3))    # 03‑Aug‑2008
date_style = date_cell.get_style()
date_style.number = 30
date_cell.set_style(date_style)

# Add a label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

> **Nota su casi limite:** Se il tuo workbook verrà aperto in diverse impostazioni locali, considera di usare `date_style.custom = "dd‑mm‑yyyy"` per garantire una visualizzazione coerente.

## Passo 5: Sistemare il Layout (Auto‑Fit Columns)

Un foglio di calcolo stipato appare poco professionale. Facciamo **adjust column width for a tidy output**.

```python
# Auto‑fit column L (index 12) to show the full content without truncation
worksheet.auto_fit_column(12)
```

> **Perché auto‑fit?** Garantisce che etichette o date lunghe siano completamente visibili, cosa particolarmente importante quando condividi il file con stakeholder non tecnici.

## Passo 6: Salva il Workbook (Save Workbook As XLSX)

Infine, **save workbook as xlsx** in una posizione a tua scelta. La costante `SaveFormat.XLSX` indica ad Aspose.Cells di scrivere nel moderno formato OpenXML.

```python
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Risultato atteso:**  
> - Le celle I19 e K20 contengono date.  
> - I19 (yesterday) è evidenziata in rosa, mentre K20 rimane verde.  
> - La colonna L si espande automaticamente per contenere l'etichetta “Yesterday”.  

Se apri `TimePeriodDemo.xlsx` in Excel, la formattazione condizionale sarà già applicata—nessun passaggio aggiuntivo necessario.

---

![Foglio Excel che mostra la data di ieri evidenziata](https://example.com/images/excel-demo.png "Screenshot del file Excel generato con celle evidenziate")

*L'immagine sopra illustra il workbook finale; nota l'evidenziazione rosa sulla cella contenente la data di ieri.*

## Riepilogo: Cosa Abbiamo Realizzato

- **Created an Excel workbook python** da zero usando Aspose.Cells.  
- **Set cell background color** per un intero intervallo per dare al foglio un'indicazione visiva.  
- Applicato **conditional formatting based on date** per segnalare automaticamente le voci di ieri.  
- **Saved workbook as xlsx**, pronto per la distribuzione o ulteriori elaborazioni.  

Tutto questo è stato realizzato in meno di 60 righe di Python, e il codice funziona su qualsiasi piattaforma che supporta il runtime Aspose.Cells.

## Prossimi Passi e Argomenti Correlati

Se ti è stato utile, potresti anche voler esplorare:

- **set cell background color** per intere righe basate su valori di stato (es., “Completed”, “Pending”).  
- Usare **highlight cells based on date range** per creare finestre mobili (ultimi 7 giorni, mese corrente).  
- Esportare in altri formati come **CSV** o **PDF** con `SaveFormat.CSV` o `SaveFormat.PDF`.  
- Aggiungere **charts** programmaticamente per visualizzare i dati appena formattati.  

Sentiti libero di modificare la logica delle date, cambiare la palette di colori o espandere l'intervallo per coprire intere colonne. Il modello rimane lo stesso: crea un workbook, allega una collezione di conditional‑formatting, definisci la regola e salva.

Hai domande su un caso d'uso specifico? Lascia un commento qui sotto, e buona programmazione!

## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Automazione Excel con Aspose.Cells .NET: Crea Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Crea e Salva Excel Workbook Aspose Cells Java](/cells/hongkong/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Crea e Salva Excel Workbook Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}