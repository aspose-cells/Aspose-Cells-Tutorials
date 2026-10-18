---
category: general
date: 2026-09-15
description: Scopri come applicare la formattazione condizionale per intervalli di
  tempo e salvare la cartella di lavoro come XLSX con Aspose.Cells in Python. Include
  codice passo‑passo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: it
lastmod: 2026-09-15
og_description: Applica la formattazione condizionale per periodi di tempo in Excel
  usando Python e salva la cartella di lavoro come XLSX. Segui questa guida completa
  per Aspose.Cells.
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: Applica la formattazione condizionale per periodi di tempo in Excel con
  Python
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  headline: How to apply time period conditional formatting in Excel using Python
  type: TechArticle
- description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  name: How to apply time period conditional formatting in Excel using Python
  steps:
  - name: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
    text: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
  - name: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
    text: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
  - name: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
    text: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
  - name: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
    text: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
  - name: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
    text: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
  - name: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
    text: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
  - name: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
    text: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
  - name: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
    text: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
  - name: The cell `I20` shows the text “Yesterday”.
    text: The cell `I20` shows the text “Yesterday”.
  - name: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
    text: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Come applicare la formattazione condizionale per periodi di tempo in Excel
  usando Python
url: /it/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come applicare la formattazione condizionale per periodo di tempo in Excel usando Python

Se hai bisogno di **formattazione condizionale per periodo di tempo** in un file Excel, questo tutorial ti mostra esattamente come farlo con Python. Vedrai un esempio completo e eseguibile che crea una cartella di lavoro, evidenzia le date di ieri e **salva la cartella di lavoro come XLSX** in poche righe di codice.

La formattazione condizionale è un modo potente per attirare l'attenzione sui dati che soddisfano una regola specifica. In questa guida ci concentriamo sul periodo di tempo “Yesterday”, ma lo stesso schema funziona per altri periodi predefiniti come Today, LastWeek e NextMonth. Alla fine del tutorial sarai in grado di creare script **how to create excel workbook python**‑style pronti per la produzione.

## Prerequisiti

- Python 3.8+ installato  
- pacchetti `aspose-cells` e `aspose-pydrawing` (`pip install aspose-cells aspose-pydrawing`)  
- Familiarità di base con la sintassi di Python  

Non è necessaria alcuna installazione aggiuntiva di Office perché Aspose.Cells gestisce internamente la generazione del file.

## Formattazione condizionale per periodo di tempo con Aspose.Cells in Python

Questa sezione analizza ogni riga di codice necessaria per l'attività principale. Il blocco di codice qui sotto è lo script completo; i commenti spiegano lo scopo di ogni passaggio.

```python
# -*- coding: utf-8 -*-
"""
Apply time period conditional formatting to highlight yesterday's dates
and save the workbook as XLSX using Aspose.Cells for Python.
"""

from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the range that will receive the conditional formatting rule
cell_range = "I19:K20"
cond_format = worksheet.conditional_formattings.add(cell_range)

# Step 3: Add a TIME_PERIOD condition for “Yesterday” and style it
condition_index = cond_format.add_condition(FormatConditionType.TIME_PERIOD)
condition = cond_format[condition_index]
condition.style.background_color = Color.pink          # Highlight colour
condition.style.pattern = BackgroundType.SOLID        # Solid fill
condition.time_period = TimePeriodType.YESTERDAY      # Built‑in “Yesterday” period

# Step 4: Populate the range with sample dates (Excel number format 30 = short date)
date_cells = ["I19", "K20"]                           # Cells that will contain dates
sample_dates = [datetime(2008, 7, 30), datetime(2008, 8, 3)]
for cell_ref, date_val in zip(date_cells, sample_dates):
    cell = worksheet.cells.get(cell_ref)
    cell.put_value(date_val)                         # Write the Python datetime
    style = cell.get_style()
    style.number = 30                                 # Excel short date format
    cell.set_style(style)

# Step 5: Add a label so the user knows what the rule represents
worksheet.cells.get("I20").put_value("Yesterday")

# Step 6: Auto‑fit the column for better readability (column L is index 12)
worksheet.auto_fit_column(12)

# Step 7: Save the workbook – this demonstrates “save workbook as xlsx”
output_path = "TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

### Perché ogni passaggio è importante

1. **Creating the workbook** ti fornisce un file Excel in memoria che puoi manipolare senza aprire Excel.  
2. **Defining the range** (`I19:K20`) indica ad Aspose.Cells dove si applica la regola, mantenendo la logica isolata.  
3. **Adding a TIME_PERIOD condition** utilizza l'enumerazione integrata di Aspose `TimePeriodType.YESTERDAY`. Questo evita calcoli manuali delle date e si aggiorna automaticamente quando il file viene aperto in un giorno diverso.  
4. **Setting the style** (`background_color` e `pattern`) determina come appaiono le celle evidenziate. Usare `Color.pink` rende la regola facile da individuare.  
5. **Writing sample dates** con il formato numerico 30 garantisce che Excel le mostri come date brevi anziché numeri seriali.  
6. **Auto‑fitting the column** migliora la leggibilità per chiunque apra il file in seguito.  
7. **Saving as XLSX** produce un file ampiamente compatibile che può essere aperto in Excel, Google Sheets o qualsiasi programma di fogli di calcolo moderno.

## Come creare una cartella di lavoro Excel in stile Python con Aspose.Cells

Lo script sopra dimostra già i passaggi minimi per **how to create excel workbook python**. In pratica potresti voler:

- Aggiungere più fogli di lavoro (`workbook.worksheets.add("Report")`).  
- Popolare grandi tabelle di dati con loop o pandas DataFrames (`worksheet.cells.import_data_table`).  
- Applicare formattazioni aggiuntive (font, bordi) usando `cell.get_style()`.

Tutte queste azioni seguono lo stesso schema: ottenere l'oggetto, modificare le sue proprietà e chiamare `set_style` o `save`.

## Aggiungere formattazione condizionale Python – altri modelli utili

Oltre all'esempio “Yesterday”, Aspose.Cells supporta diversi tipi di formattazione condizionale:

| FormatConditionType | Caso d'uso tipico |
|---------------------|-------------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | Formule personalizzate (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | Confronti semplici (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | Scale di colore a gradiente |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | Visualizzazione a barra nella cella |

Per **add conditional formatting python** per una soglia numerica, dovresti sostituire `FormatConditionType.TIME_PERIOD` con `FormatConditionType.CELL_VALUE` e impostare `condition.operator_type` e `condition.formula1`.

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## Salva la cartella di lavoro come XLSX – migliori pratiche

Quando **save workbook as xlsx**, considera:

- **Specifying the correct `SaveFormat`** (`SaveFormat.XLSX`) per evitare formati legacy.  
- **Using a deterministic file name** se lo script viene eseguito in un ciclo (`f"report_{datetime.now():%Y%m%d}.xlsx"`).  
- **Closing resources** (`workbook.dispose()`) nei servizi a lunga esecuzione per liberare memoria nativa.  

L'esempio utilizza già `SaveFormat.XLSX`, che produce una cartella di lavoro moderna basata su zip che conserva tutte le regole di formattazione condizionale.

## Evidenziare ieri in Excel – passaggi di verifica

Dopo aver eseguito lo script, apri `TimePeriodExample.xlsx`:

1. Le celle `I19` e `K20` contengono le date `30‑07‑2008` e `03‑08‑2008`.  
2. La cella `I20` mostra il testo “Yesterday”.  
3. Se cambi la data di sistema al **30 luglio 2008** e riapri il file, le celle con date corrispondenti vengono riempite automaticamente di rosa.  
4. Cambiando la data di sistema a qualsiasi altro giorno, il riempimento rosa scompare, confermando che la regola reagisce alla logica della **time period conditional formatting**.

## Errori comuni e come evitarli

- **Missing `aspose-pydrawing`** – la classe `Color` si trova in questo pacchetto; dimenticare di installarlo genera un `ImportError`.  
- **Incorrect number format** – usare il formato predefinito General mostra numeri seriali (es., 39822). Imposta sempre `style.number = 30` per date brevi.  
- **Range mismatch** – l'intervallo di formattazione condizionale deve includere le celle che intendi evidenziare; altrimenti la regola non ha effetto.

## Consiglio professionale: riutilizzare la routine di formattazione

Se ti serve la stessa regola “Yesterday” in più cartelle di lavoro, avvolgi la logica in una funzione di supporto:

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

Chiama `apply_yesterday_highlight(worksheet, "A1:A10")` dove necessario.

## Conclusione

Questa guida ti ha mostrato come implementare la **time period conditional formatting** in Excel usando Python, come **save workbook as XLSX**, e come **highlight yesterday in Excel** con uno script unico e riutilizzabile. Ora hai una solida base per aggiungere codice **add conditional formatting python** a qualsiasi progetto di automazione, sia che tu stia generando report giornalieri, costruendo dashboard o preparando esportazioni di dati.

**Passi successivi**

- Esplora altri valori `TimePeriodType` come `TODAY` o `LAST_WEEK`.  
- Combina più regole condizionali sullo stesso intervallo per indicazioni visive più ricche.  
- Integra la generazione della cartella di lavoro in un servizio web o in un job programmato.

Buona programmazione e goditi la chiarezza visiva che la formattazione condizionale porta alla tua automazione Excel!

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Guida completa alla formattazione condizionale in Excel con Aspose.Cells .NET : A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Master Aspose.Cells .NET : Applicare la formattazione condizionale a righe alternate in Excel](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [Master Conditional Formatting con caratteri personalizzati in Excel usando Aspose.Cells per .NET e C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}