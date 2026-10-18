---
category: general
date: 2026-07-06
description: Crea un workbook Excel in Python con codice per impostare il colore di
  sfondo delle celle, impostare lo stile delle celle programmaticamente e aggiungere
  la formattazione condizionale in Python per evidenziare la data odierna.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- set cell style programmatically
- highlight today date excel
- add conditional formatting python
language: it
lastmod: 2026-07-06
og_description: Crea un workbook Excel con Python all'istante. Scopri come impostare
  il colore di sfondo delle celle, definire lo stile delle celle programmaticamente
  e aggiungere la formattazione condizionale in Python per evidenziare la data odierna.
og_image_alt: Screenshot of an Excel workbook created with Python showing colored
  cells and today’s date highlighted
og_title: Crea cartella di lavoro Excel con Python – Stile celle e evidenzia oggi
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  headline: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  type: TechArticle
- description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  name: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  steps:
  - name: Converting a range like `"A1:C3"` into a `CellArea`.
    text: Converting a range like `"A1:C3"` into a `CellArea`.
  - name: Filling every cell in that area with a sequential number (just for demo
      purposes).
    text: Filling every cell in that area with a sequential number (just for demo
      purposes).
  - name: Applying a solid **set cell background color**.
    text: Applying a solid **set cell background color**.
  - name: Adding a conditional rule that **highlight today date excel**.
    text: Adding a conditional rule that **highlight today date excel**.
  type: HowTo
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Crea cartella di lavoro Excel con Python – Guida completa a stile e formattazione
  condizionale
url: /it/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea Excel Workbook Python – Guida Completa a Styling & Conditional Formatting

Ti sei mai chiesto come **create Excel workbook Python** da zero senza aprire Excel manualmente? Non sei l'unico. Molti sviluppatori hanno bisogno di generare report, dashboard o anche semplici registri di dati al volo, e farlo programmaticamente fa risparmiare ore di lavoro manuale.

In questo tutorial percorreremo l'intero processo: dalla creazione di una cartella di lavoro nuovissima, a **set cell background color**, a **set cell style programmatically**, e infine a **highlight today date excel** usando **add conditional formatting python**. Alla fine avrai uno script pronto all'uso che produce un file .xlsx rifinito in pochi secondi.

---

## Cosa Costruirai

- Un nuovo file Excel con alcune celle popolate.
- Celle colorate con uno sfondo personalizzato.
- Valori numerici e di data formattati con uno stile numerico specifico.
- Una regola condizionale che evidenzia automaticamente la cella contenente la data odierna.

Non è necessaria alcuna installazione esterna di Excel—Aspose.Cells per Python via .NET gestisce tutto il lavoro pesante.

---

## Prerequisiti

| Requisito | Perché è importante |
|-------------|----------------|
| Python 3.8+ | Sintassi moderna e type hints |
| `aspose-cells` package | Libreria core per la manipolazione della cartella di lavoro |
| `aspose-pydrawing` (installed with Aspose.Cells) | Fornisce la classe `Color` |
| Familiarità di base con i concetti di Excel (celle, intervalli, formattazione) | Rende il tutorial più fluido |

Installa la libreria con:

```bash
pip install aspose-cells
```

---

## Passo 1: Inizializza la Cartella di Lavoro e il Foglio di Lavoro

La prima cosa da fare quando **create excel workbook python** è istanziare un oggetto `Workbook` e ottenere il foglio di lavoro predefinito. Pensa alla cartella di lavoro come all'intero file Excel, mentre il foglio di lavoro è una singola scheda al suo interno.

```python
from aspose.cells import Workbook

# Create a new workbook – this is our empty Excel file
book = Workbook()

# Grab the first (default) worksheet
sheet = book.worksheets[0]
```

> **Pro tip:** Se ti servono più fogli, usa `book.worksheets.add("MySheet")` per aggiungere altre schede.

---

## Passo 2: Classe di Supporto per Stile e Formattazione Condizionale

Sotto trovi una classe `ConditionalFormatting` compatta ma completa. Avvolge le attività ripetitive di:

1. Convertire un intervallo come `"A1:C3"` in un `CellArea`.
2. Riempire ogni cella in quell'area con un numero sequenziale (solo a scopo dimostrativo).
3. Applicare un solido **set cell background color**.
4. Aggiungere una regola condizionale che **highlight today date excel**.

```python
from aspose.cells import (
    CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """
    Utility class that demonstrates how to:
    • set cell background color
    • set cell style programmatically
    • add conditional formatting python
    """
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        """
        Creates a conditional formatting object for the given range
        and fills the range with a background color.
        """
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]

        # Convert "A1:C3" → CellArea object
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)

        # Paint the whole area with the supplied color
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        """
        Populates each cell in the range with an incrementing integer
        and applies the supplied background color.
        """
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)

                # Apply background only if a real color is supplied
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)

                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name: str) -> CellArea:
        """
        Parses an Excel‑style address (e.g. "B2:D4") into a CellArea.
        """
        area = CellArea()
        parts = name.replace("$", "").split(':')

        start_row, start_col = CellsHelper.cell_name_to_index(parts[0])
        area.start_row = start_row
        area.start_column = start_col

        if len(parts) == 2:
            end_row, end_col = CellsHelper.cell_name_to_index(parts[1])
            area.end_row = end_row
            area.end_column = end_col
        else:
            area.end_row = start_row
            area.end_column = start_col
        return area

    # -----------------------------------------------------------------
    # Step 2: Add conditional formatting for TODAY
    # -----------------------------------------------------------------
    def add_time_period_1(self):
        """
        Demonstrates add conditional formatting python that highlights
        cells containing today’s date.
        """
        # 1️⃣ Create a formatting range and give it a neutral background
        cf = self.get_format_condition("I1:K2", Color.light_slate_gray)

        # 2️⃣ Add a TIME_PERIOD condition (Today)
        idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
        cond = cf[idx]
        cond.time_period = TimePeriodType.TODAY
        cond.style.background_color = Color.pink
        cond.style.pattern = BackgroundType.SOLID

        # 3️⃣ Populate the cells with date values
        # Cell I1 – today’s date, formatted as a date
        cell = self._sheet.cells.get("I1")
        style = cell.get_style()
        style.number = 30               # 30 = “mm-dd-yy” style in Aspose
        cell.set_style(style)
        cell.put_value(datetime.today())

        # Cell K2 – an arbitrary past date for contrast
        self._sheet.cells.get("K2").put_value(datetime(2008, 7, 30))

        # Cell I2 – a label so the reader knows what’s being highlighted
        self._sheet.cells.get("I2").put_value("Today")
```

### Perché una Classe di Supporto?

- **Reusability:** Puoi chiamare `add_time_period_1()` per qualsiasi foglio di lavoro senza riscrivere la logica.
- **Clarity:** Ogni metodo fa una cosa – un segno distintivo del codice pulito.
- **Extensibility:** Vuoi aggiungere altre regole? Basta aggiungere un altro metodo seguendo lo stesso schema.

---

## Passo 3: Applica la Formattazione e Salva il File

Now we tie everything together: instantiate the helper, run the formatting routine, and finally write the workbook to disk.

```python
# Instantiate the helper with our worksheet
formatter = ConditionalFormatting(sheet)

# Fill a demo range with numbers and a light blue background
formatter.get_format_condition("A1:C3", Color.light_sky_blue)

# Add the “today” conditional rule
formatter.add_time_period_1()

# Save the workbook – choose any location you like
output_path = "styled_workbook.xlsx"
book.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

When you open *styled_workbook.xlsx* you should see:

- Celle **A1:C3** numerate da 0‑8 con un riempimento light‑sky‑blue.
- Cella **I1** che mostra la data odierna con sfondo rosa (grazie alla regola condizionale).
- Cella **K2** che visualizza la data statica *2008‑07‑30* per confronto.
- Cella **I2** contenente il testo “Today”.

Quel segnale visivo è esattamente ciò che richiede il requisito **highlight today date excel**.

---

## Passo 4: Approfondisci – Personalizzare gli Stili

Se hai bisogno di modificare caratteri, bordi o formati numerici, puoi estendere il metodo `fill_cell` o creare un nuovo helper:

```python
def apply_custom_style(cell, font_name="Calibri", font_size=11, bold=False):
    style = cell.get_style()
    style.font.name = font_name
    style.font.size = font_size
    style.font.bold = bold
    cell.set_style(style)
```

Puoi quindi chiamare `apply_custom_style(cell, bold=True)` all'interno del ciclo per **set cell style programmatically** per ogni cella in un intervallo.

---

## Problemi Comuni & Come Evitarli

| Sintomo | Causa Probabile | Risoluzione |
|---------|----------------|-------------|
| Le celle rimangono bianche nonostante `Color.light_sky_blue` | Lo stile non è stato applicato dopo aver impostato `foreground_color` | Chiama sempre `cell.set_style(style)` dopo aver modificato l'oggetto stile. |
| La regola condizionale non si attiva mai | `style.number` non impostato per le celle data, quindi Excel tratta il valore come stringa | Imposta `style.number = 30` (o qualsiasi formato data) prima di `cell.put_value(datetime…)`. |
| La cartella di lavoro si salva come .xls nonostante `SaveFormat.XLSX` | Versione Aspose più vecchia che usa il formato legacy per impostazione predefinita | Aggiorna all'ultima versione del pacchetto `aspose-cells`. |
| Intervallo come `"A1"` genera un errore di indice | Uso di `cells.get("A1")` su un foglio non ancora inizializzato | Assicurati che il foglio di lavoro esista (esiste subito dopo `Workbook()`), oppure usa `cells.get(row, col)` con indici a base zero. |

---

## Script Completo per Copia‑Incolla

Di seguito trovi lo script **intero** che puoi inserire in un file chiamato `create_excel.py` ed eseguire immediatamente.

```python
# create_excel.py
from aspose.cells import (
    Workbook, CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """Utility for styling cells and adding conditional formatting."""
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)
                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name:


## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Excel Automation with Aspose.Cells .NET: Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}