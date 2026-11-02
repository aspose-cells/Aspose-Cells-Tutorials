---
category: general
date: 2026-09-21
description: Scopri come creare una cartella di lavoro Excel in Python, impostare
  il colore di sfondo delle celle e applicare la formattazione condizionale basata
  su date con Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: it
lastmod: 2026-09-21
og_description: Crea una cartella di lavoro Excel in Python, imposta il colore di
  sfondo delle celle e applica la formattazione condizionale basata su date usando
  Aspose.Cells. Segui la guida passo passo.
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: Crea una cartella di lavoro Excel in Python con formattazione condizionale
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to create Excel workbook in Python, set cell background color,
    and apply date based conditional formatting with Aspose.Cells.
  headline: Create Excel workbook in Python using conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Crea una cartella di lavoro Excel in Python usando la formattazione condizionale
url: /it/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea una cartella di lavoro Excel in Python usando la formattazione condizionale

Se hai bisogno di **creare Excel workbook python** script che evidenziano automaticamente le date, questa guida ti mostra esattamente come fare. Vedrai come **impostare il colore di sfondo delle celle**, aggiungere una regola “Yesterday” e salvare il file—tutto con Aspose.Cells per Python.

Lavorare con i file Excel in modo programmatico spesso significa ripetere la stessa logica di formattazione su molti fogli. Alla fine di questo tutorial avrai un modello riutilizzabile per **excel conditional formatting python** che potrai inserire in qualsiasi progetto.

## Prerequisiti

- Python 3.8+ installato  
- Pacchetto `aspose-cells` (`pip install aspose-cells`)  
- Familiarità di base con le funzioni Python e il modulo datetime  

Non sono richieste librerie aggiuntive; Aspose.Cells gestisce tutte le operazioni su Excel.

## Passo 1: Crea la cartella di lavoro e accedi al primo foglio

Il primo passo è **create excel workbook python** oggetti e prendere il foglio di lavoro predefinito. Questo ti fornisce una tela pulita per ulteriori stilizzazioni.

```python
# Import required Aspose.Cells classes
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# Create a new workbook; the first worksheet is at index 0
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Perché è importante:* `Workbook()` crea un file Excel in memoria. Accedere a `worksheets[0]` evita di codificare in modo rigido i nomi dei fogli e funziona anche se il nome predefinito dovesse cambiare.

## Passo 2: Helper per aggiungere una formattazione condizionale TIME_PERIOD

Per mantenere il codice ordinato, avvolgiamo la creazione della formattazione condizionale in un helper. Riceve un intervallo di celle, un colore di sfondo e la regola di periodo di tempo desiderata.

```python
def add_time_period(sheet, cell_range, bg_color, period_type):
    """
    Adds a TIME_PERIOD conditional formatting rule to `cell_range`.
    The rule paints the cells with `bg_color` when the date matches `period_type`.
    """
    # Retrieve (or create) the ConditionalFormatting collection for the range
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)

    # Insert a TIME_PERIOD condition and configure its style
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color          # set cell background color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type                # e.g., TimePeriodType.YESTERDAY
```

*Perché è importante:* L'helper astrae i passaggi ripetitivi di creazione di una formattazione condizionale, rendendo facile il riutilizzo per altre regole basate su date come “Today” o “Last Week”.

## Passo 3: Applica la regola “Yesterday” a un intervallo

Ora usiamo l'helper per evidenziare le celle che contengono la data di ieri. L'intervallo `I19:K20` diventerà **medium sea green** quando la condizione è soddisfatta.

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*Perché è importante:* `TimePeriodType.YESTERDAY` fa parte dell'enumerazione integrata di Aspose.Cells, quindi non è necessario calcolare le date manualmente. La libreria valuta la regola ogni volta che la cartella di lavoro viene aperta.

## Passo 4: Popola l'intervallo con date di esempio

Per vedere la regola in azione, scriviamo due date—una che corrisponde a “Yesterday” e una che non lo fa. Lo stile `number` `30` corrisponde a un formato data predefinito.

```python
# Cell I19 gets a date that is exactly yesterday (relative to the sample data)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))   # 30 July 2008
cell.style.number = 30                # date format

# Cell K20 gets a date that is outside the rule
cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))    # 3 August 2008
cell.style.number = 30
```

*Perché è importante:* Inserendo date concrete puoi verificare che la formattazione condizionale funzioni senza dover aprire il file in un giorno specifico.

## Passo 5: Aggiungi un'etichetta descrittiva e adatta automaticamente la larghezza della colonna

Una piccola etichetta chiarisce lo scopo dell'intervallo formattato, e `auto_fit_column` rende il foglio leggibile.

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## Passo 6: Salva la cartella di lavoro

Infine, scrivi la cartella di lavoro su disco. La chiamata `os.makedirs` garantisce che la cartella di destinazione esista.

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Quando apri *TimePeriodDemo.xlsx* vedrai:

- La cella **I19** colorata **medium sea green** perché il suo valore corrisponde alla regola “Yesterday”.  
- La cella **K20** mantiene lo sfondo predefinito perché la sua data non soddisfa la condizione.  

Questo dimostra **format cells by date** usando una singola riga di codice Python.

## Esempio completo, eseguibile

Unendo tutti i pezzi, ecco lo script completo che puoi copiare‑incollare ed eseguire:

```python
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# 1️⃣ Create workbook and get first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# 2️⃣ Helper to add TIME_PERIOD conditional formatting
def add_time_period(sheet, cell_range, bg_color, period_type):
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type

# 3️⃣ Apply “Yesterday” rule (set cell background color)
add_time_period(
    worksheet,
    "I19:K20",
    Color.medium_sea_green,
    TimePeriodType.YESTERDAY
)

# 4️⃣ Fill sample dates (format cells by date)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))
cell.style.number = 30

cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))
cell.style.number = 30

# 5️⃣ Add label and auto‑fit column
worksheet.cells.get("I20").put_value("Yesterday")
worksheet.auto_fit_column(12)

# 6️⃣ Save the workbook
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Esegui lo script, apri il file risultante e vedrai la formattazione condizionale in azione.

## Varianti comuni e casi limite

| Variante | Come implementare | Quando usarla |
|-----------|-------------------|---------------|
| **Evidenzia “Today”** | Sostituisci `TimePeriodType.YESTERDAY` con `TimePeriodType.TODAY` | Dashboard in tempo reale |
| **Intervalli multipli** | Chiama `add_time_period` per ogni intervallo, passando colori diversi | Report complessi |
| **Intervallo di date dinamico** | Usa `TimePeriodType.LAST_7_DAYS` o `TimePeriodType.NEXT_MONTH` | Report a scorrimento |
| **Colore personalizzato** | Usa `Color.from_argb(255, r, g, b)` per creare qualsiasi tonalità | Stile coerente con il brand |

**Consiglio professionale:** Imposta sempre `condition.style.pattern = BackgroundType.SOLID` quando desideri un riempimento solido; altrimenti Excel potrebbe mostrare un gradiente che appare incoerente tra le versioni.

## Conclusione

Ora sai come **create Excel workbook python** script che **set cell background color**, applicano **excel conditional formatting python** e **format cells by date** usando Aspose.Cells. L'esempio copre uno scenario di **date based conditional formatting**, ma lo stesso modello funziona per qualsiasi regola di periodo di tempo.

Successivamente, potresti esplorare:

- Aggiungere barre dati o set di icone (`FormatConditionType.DATA_BAR`)  
- Combinare più regole condizionali sullo stesso intervallo  
- Esportare la cartella di lavoro in PDF (`SaveFormat.PDF`) per la reportistica  

Sentiti libero di sperimentare con colori diversi, intervalli e tipi di periodo di tempo per adattarli alle tue specifiche esigenze di reporting. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel Automation with Aspose.Cells .NET&#58; Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}