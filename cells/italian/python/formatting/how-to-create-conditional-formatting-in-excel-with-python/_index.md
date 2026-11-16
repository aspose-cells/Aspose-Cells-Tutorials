---
category: general
date: 2026-11-16
description: Crea formattazione condizionale in Excel usando Python. Impara ad aggiungere
  un intervallo di formattazione condizionale, evidenziare le date e costruire una
  cartella di lavoro programmaticamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: it
lastmod: 2026-11-16
og_description: Crea formattazione condizionale in Excel con Python. Questo tutorial
  mostra come aggiungere un intervallo di formattazione condizionale, evidenziare
  le date e generare una cartella di lavoro.
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: Crea formattazione condizionale in Excel con Python – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Come creare la formattazione condizionale in Excel con Python
url: /it/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare formattazione condizionale in Excel con Python

Se hai bisogno di **creare formattazione condizionale** in un file Excel mentre lavori in Python, questa guida ti mostra esattamente come farlo. Imparerai a **create excel workbook python**‑style, a definire un intervallo di formattazione e a evidenziare le date senza uscire dall'IDE.

La formattazione condizionale ti consente di evidenziare visivamente le celle che soddisfano criteri specifici—perfetto per dashboard, report o fogli di convalida dei dati. Alla fine di questo tutorial avrai un workbook completamente funzionante che colora di rosa le celle con data “Yesterday” mentre il resto dell'intervallo rimane verde.

## Cosa otterrai

* Crea un nuovo workbook da zero.  
* Aggiungi una collezione di formattazione condizionale per un blocco di celle specifico.  
* Applica una regola **TIME_PERIOD** che evidenzia le date (lo scenario “how to highlight dates”).  
* Salva il file come workbook XLSX pronto per l'elaborazione successiva.

**Prerequisiti**  
* Python 3.8+  
* `aspose-cells` Python package (`pip install aspose-cells`)  
* Familiarità di base con il modulo `datetime` di Python  

---

## Come creare formattazione condizionale in Python

Il primo passo è configurare il workbook e il foglio di lavoro che ospiterà le regole di formattazione.

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**Perché è importante** – `Workbook` è il punto di ingresso per tutte le operazioni Excel. Creare il workbook programmaticamente sostituisce il passaggio manuale “File → New”, consentendo pipeline di report automatizzate.

---

## Preparare la collezione di formattazione condizionale – aggiungere l'intervallo di formattazione condizionale

Successivamente definiamo il blocco di celle che riceverà la regola. In questo esempio l'intervallo è **I19:K20**.

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**Spiegazione** – `conditional_formattings.add` registra una nuova collezione legata alla stringa di indirizzo. La prima condizione (`conds[0]`) funge da stile “predefinito”; la regola successiva lo sovrascriverà quando i suoi criteri saranno soddisfatti.

---

## Aggiungere una condizione TIME_PERIOD – come evidenziare le date

Ora aggiungiamo la logica effettiva che identifica le date “Yesterday” e le colora di rosa.

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**Perché usare TIME_PERIOD?** – Aspose.Cells fornisce enumerazioni integrate come `YESTERDAY`, `TODAY` e `LAST_WEEK`. Valutano il valore data della cella rispetto alla data di sistema corrente, eliminando la necessità di formule personalizzate.

---

## Popolare dati di esempio – dimostrare la regola

Per vedere la formattazione in azione inseriamo una data che corrisponde alla regola e un'altra che non lo fa.

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**Nota caso limite** – La regola `TIME_PERIOD` funziona solo con date *reali*. Se una cella contiene testo (ad esempio “N/A”), la regola viene ignorata, evitando cambi di colore inaspettati.

---

## Salvare il workbook – add conditional formatting python

Infine, scrivi il workbook su disco. Il file può essere aperto in qualsiasi programma di fogli di calcolo per verificare i colori.

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**Risultato atteso**  

| I19 (verde → rosa) | J19 (verde) | K19 (verde) |
|--------------------|------------|------------|
| 7/30/2008 (ieri) | – | – |
| **I20**: etichetta “Yesterday” | – | – |
| I21‑K21 (verde) | – | – |

La cella **I19** appare con uno sfondo rosa perché la sua data corrisponde al periodo “Yesterday”, mentre **K20** rimane verde.

---

## Domande comuni e consigli pratici

* **Posso usare un intervallo di date personalizzato invece di un periodo predefinito?**  
  Sì. Sostituisci `condition.time_period` con `condition.formula1 = "TODAY()-1"` e imposta `condition.type = FormatConditionType.FORMULA`.

* **E se il mio workbook contiene già dei dati?**  
  Usa `worksheet.cells.import_data` per caricare i dati in blocco prima di aggiungere la collezione di formattazione condizionale.

* **Prestazioni con fogli di grandi dimensioni?**  
  Aggiungere molte condizioni può rallentare il rendering. Raggruppa le celle con la stessa regola in un unico intervallo (ad esempio “A1:C1000”) per mantenere basso il numero di condizioni.

* **Compatibilità cross‑platform?**  
  Il file XLSX generato segue lo standard Office Open XML, quindi funziona su applicazioni di fogli di calcolo Windows, macOS e Linux.

---

## Conclusione

Ora sai come **creare formattazione condizionale** in un workbook Excel usando Python. Il tutorial ha coperto la creazione del workbook, la definizione di un **add conditional formatting range**, l'applicazione di una regola **how to highlight dates**, e il salvataggio del file—tutto con l'approccio **add conditional formatting python** fornito da Aspose.Cells.

Da qui puoi:

* Estendi il set di regole con altri valori `TimePeriodType` (ad esempio `TODAY`, `LAST_MONTH`).  
* Combina più condizioni sullo stesso intervallo per indicazioni visive più ricche.  
* Integra questo flusso di lavoro in pipeline di report automatizzate o servizi web.

Buon coding, e sentiti libero di sperimentare con colori, intervalli e logiche di data diversi per soddisfare le tue esigenze di reporting!

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea workbook Excel Python formattazione condizionale per data](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [Come applicare la formattazione condizionale per periodo di tempo in Excel usando Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Crea Excel Workbook Python – Guida completa a Styling & Formattazione Condizionale](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}