---
category: general
date: 2026-07-20
description: Crea un workbook Excel in Python con Aspose.Cells, imposta il colore
  di sfondo della cella e aggiungi la formattazione condizionale in Python per stilizzare
  le celle in base alla data.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: it
lastmod: 2026-07-20
og_description: Crea un workbook Excel in Python usando Aspose.Cells. Scopri come
  impostare il colore di sfondo delle celle e aggiungere la formattazione condizionale
  in Python per formattare le celle in base alla data.
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: Crea cartella di lavoro Excel con Python – Aggiungi formattazione condizionale
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Create Excel workbook Python with Aspose.Cells, set cell background
    color, and add conditional formatting python to style cells by date.
  headline: Create Excel Workbook Python – Conditional Formatting Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Change `"I19:K20"` to any A1‑style range, and adjust the sample
      dates accordingly.
    question: Can I target a different date range?
  - answer: Use `FormatConditionType.FORMULA` and set `condition.formula1 = "YOUR_FORMULA"`—for
      example, `=TODAY()-A1=1` to mimic yesterday.
    question: What if I need a custom formula instead of `YESTERDAY`?
  - answer: Call `conditions.add_condition` again with a different `FormatConditionType`.
      The order matters; later rules can override earlier ones.
    question: How do I apply multiple rules to the same range?
  - answer: Yes—modify `condition.style.font.color = Color.white` (or any other `Color`).
    question: Is there a way to set font colour together with background?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
title: Creare una cartella di lavoro Excel con Python – Guida alla formattazione condizionale
url: /it/python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea Cartella di Lavoro Excel con Python – Guida alla Formattazione Condizionale

Ti sei mai chiesto come **create Excel workbook Python** da zero e farlo apparire curato senza aprire l'interfaccia? Non sei solo. Molti sviluppatori incontrano difficoltà quando devono **set cell background color** o applicare stili basati su date in modo programmatico.  

In questo tutorial percorreremo un esempio completo e eseguibile che utilizza Aspose.Cells per **add conditional formatting python** regole, formattare le celle per data e salvare il risultato come file XLSX moderno. Alla fine avrai uno script autonomo che potrai inserire in qualsiasi progetto.

## Cosa Imparerai

- Come inizializzare una cartella di lavoro e ottenere il primo foglio di lavoro.  
- Modi per **set cell background color** per un intero intervallo.  
- Utilizzare **aspose cells conditional formatting** per evidenziare le date “Yesterday”.  
- Auto‑fit delle colonne e salvataggio del file su disco.  

Nessuna configurazione esterna è necessaria—basta Python 3 e il pacchetto Aspose.Cells. Se hai già installato `aspose-cells`, sei pronto; altrimenti un rapido `pip install aspose-cells` farà al caso tuo.

## Prerequisiti

- Python 3.8+ (il codice funziona su 3.9, 3.10 e versioni successive).  
- Aspose.Cells per Python via .NET (`aspose-cells` NuGet wrapper).  
- Familiarità di base con i concetti di Excel (celle, intervalli, formattazione).  

Li hai? Ottimo—tuffiamoci.

## Crea Cartella di Lavoro Excel con Python – Configurazione e Foglio di Lavoro

Prima di tutto: abbiamo bisogno di un nuovo oggetto workbook e di un riferimento al foglio di lavoro predefinito. Questa è la tela su cui avverranno tutte le operazioni successive.

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **Perché è importante:** `Workbook()` costruisce un file Excel in memoria, eliminando la necessità di file temporanei. La variabile `worksheet` è il nostro punto di ingresso per le azioni a livello di cella.

## Imposta il Colore di Sfondo della Cella

Prima di aggiungere regole, è utile dare all'intervallo target un colore di base in modo che la formattazione condizionale risalti. L'helper qui sotto recupera (o crea) una `FormatConditionCollection` per un dato intervallo e colora le celle con uno sfondo solido.

```python
def get_format_condition(cell_range: str, base_color: Color):
    """
    Obtain (or create) a FormatConditionCollection for `cell_range`.
    Also set a base background colour for the whole range.
    """
    # Retrieve or add a conditional formatting entry for the range
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    # Apply the base colour to every cell in the range
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color          # set cell background color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection
```

> **Suggerimento:** Se prevedi di riutilizzare lo stesso intervallo con più regole, chiama questo helper una sola volta e conserva la collezione restituita; risparmia alcune chiamate API.

## Aggiungi Formattazione Condizionale Python per Intervalli di Data

Ora la parte divertente: creeremo una regola di **time‑period conditional formatting** che evidenzia le celle contenenti la data di ieri. Questo dimostra la potenza di **format cells by date** usando Aspose.Cells.

```python
def apply_yesterday_rule():
    """
    Apply a “Yesterday” conditional formatting rule to the range I19:K20.
    Cells that match will turn pink; others stay with the base colour.
    """
    # Obtain the condition collection for the target range
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)

    # Create a TIME_PERIOD condition (this is the aspose cells conditional formatting type we need)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]

    # Define the appearance for cells that meet the condition
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Set the time period to “Yesterday”
    condition.time_period = TimePeriodType.YESTERDAY

    # Populate sample dates to demonstrate the rule
    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))   # matches “Yesterday”
    cell_i19.style.number = 30                 # Excel number format for dates
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))    # does NOT match
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    # Add a label for clarity
    worksheet.cells.get("I20").put_value("Yesterday")
```

> **Perché usare `TIME_PERIOD`?** Astrae la necessità di scrivere formule personalizzate. Aspose.Cells valuta la data rispetto alla data di sistema corrente, quindi la regola rimane sempre pertinente.

### Esecuzione della Regola

```python
apply_yesterday_rule()
```

Quando apri il file risultante, le celle `I19` brilleranno di rosa (perché sono “Yesterday”), mentre `K20` manterrà il colore verde di base.

## Auto‑Fit delle Colonne e Salva la Cartella di Lavoro

Un foglio di calcolo ordinato appare professionale. L'auto‑fit garantisce che i dati non siano stipati.

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Caso limite:** Se punti a una directory che non esiste, `workbook.save` genererà un errore. Avvolgi la chiamata di salvataggio in un blocco `try/except` se hai bisogno di una gestione delicata.

### Script Completo (Pronto per Copia‑Incolla)

Sotto trovi l'intero script, pronto per l'esecuzione. Sostituisci semplicemente `YOUR_DIRECTORY` con una cartella valida sul tuo computer.

```python
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create the workbook and worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

def get_format_condition(cell_range: str, base_color: Color):
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection

def apply_yesterday_rule():
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = TimePeriodType.YESTERDAY

    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))
    cell_i19.style.number = 30
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    worksheet.cells.get("I20").put_value("Yesterday")

apply_yesterday_rule()
worksheet.auto_fit_column(12)

output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Eseguendo questo script otterrai `TimePeriodExample.xlsx` con la formattazione condizionale descritta.

## Domande Frequenti e Suggerimenti

- **Posso mirare a un intervallo di date diverso?**  
  Assolutamente. Cambia `"I19:K20"` con qualsiasi intervallo in stile A1 e regola le date di esempio di conseguenza.

- **E se ho bisogno di una formula personalizzata invece di `YESTERDAY`?**  
  Usa `FormatConditionType.FORMULA` e imposta `condition.formula1 = "YOUR_FORMULA"`—ad esempio, `=TODAY()-A1=1` per simulare ieri.

- **Come applicare più regole allo stesso intervallo?**  
  Chiama nuovamente `conditions.add_condition` con un diverso `FormatConditionType`. L'ordine è importante; le regole successive possono sovrascrivere quelle precedenti.

- **C'è un modo per impostare il colore del carattere insieme allo sfondo?**  
  Sì—modifica `condition.style.font.color = Color.white` (o qualsiasi altro `Color`).

## Conclusione

Ora sai come **create Excel workbook Python** usando Aspose.Cells, **set cell background color**, e **add conditional formatting python** che formatta le celle per data. Lo script è pienamente funzionale, gestisce casi limite come directory mancanti, e può essere esteso a scenari più sofisticati come logica condizionale a più regole o rilevamento dinamico degli intervalli.

Pronto per il passo successivo? Prova a sostituire la regola “Yesterday” con “Last Week”, sperimenta riempimenti a gradiente, o genera un report completo con decine di tabelle formattate. I mattoni fondamentali sono tutti qui, e hai appena padroneggiato il nucleo di **aspose cells conditional formatting** in Python.

Buon coding, e sentiti libero di condividere le tue varianti nei commenti!

## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}