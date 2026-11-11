---
category: general
date: 2026-10-26
description: Scopri come usare WRAPCOLS in C# per suddividere un intervallo in colonne,
  applicare WRAPROWS per le righe e salvare il workbook come XLSX in modo programmatico.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split range into rows
- excel wrapcols example
- save workbook as xlsx
- create excel workbook programmatically
language: it
lastmod: 2026-10-26
og_description: Come utilizzare WRAPCOLS in C# per suddividere i dati in colonne,
  usare WRAPROWS per le righe e salvare la cartella di lavoro come XLSX. Segui la
  guida completa passo passo.
og_image_alt: Screenshot illustrating how to use WRAPCOLS to split a range into columns
  in Excel
og_title: Come usare WRAPCOLS in C# – suddividere gli intervalli e salvare come XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  headline: How to use WRAPCOLS in C# and save workbook as XLSX
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  name: How to use WRAPCOLS in C# and save workbook as XLSX
  steps:
  - name: What the saved file looks like
    text: 'When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:'
  - name: Changing the number of columns or rows
    text: '* **More columns:** Increase the second argument of `WRAPCOLS`. Example:
      `=WRAPCOLS(A1:A10,5)` creates five columns, leaving empty cells where data runs
      out. * **Dynamic column count:** Use a cell reference instead of a hard‑coded
      number. `=WRAPCOLS(A1:A10, G1)` where `G1` holds the desired column c'
  - name: Handling empty or non‑numeric cells
    text: WRAPCOLS and WRAPROWS ignore empty cells by default, but they preserve the
      order of non‑empty values. If you need to preserve blanks, wrap the source range
      with `IFERROR` or `TEXT` functions before applying WRAPCOLS.
  - name: Saving to other formats
    text: 'While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells
      supports many formats (`.xls`, `.csv`, `.pdf`, etc.):'
  - name: What’s next?
    text: '* Explore **conditional formatting** to highlight the spilled data. * Combine
      **WRAPCOLS** with **SORT** or **FILTER** for dynamic dashboards. * Use Aspose.Cells’
      **charting API** to visualize the rearranged data directly from code.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Come usare WRAPCOLS in C# e salvare la cartella di lavoro come XLSX
url: /it/net/row-and-column-management/how-to-use-wrapcols-in-c-and-save-workbook-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare WRAPCOLS in C# e salvare la cartella di lavoro come XLSX

Se hai bisogno di **come usare WRAPCOLS** per riorganizzare i dati in un file Excel, questa guida ti mostra una soluzione completa e funzionante. Vedrai un **esempio di excel wrapcols**, imparerai a **dividere un intervallo in righe** con WRAPROWS e terminerai con **salvare la cartella di lavoro come XLSX**—tutto eseguito **programmaticamente**.

Lavorare con Excel da C# spesso significa creare una cartella di lavoro, applicare formule e persistere il file. Il codice qui sotto utilizza la libreria Aspose.Cells, che consente di manipolare i file Excel senza la necessità di avere Microsoft Office installato. Alla fine di questo tutorial sarai in grado di **creare excel workbook programmatically**, dividere i dati sia orizzontalmente che verticalmente e produrre un file `.xlsx` pulito pronto per l'elaborazione successiva.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* .NET 6.0 o successivo (il codice funziona anche con .NET Framework 4.7+)
* Un riferimento al pacchetto NuGet **Aspose.Cells**  
  ```bash
  dotnet add package Aspose.Cells
  ```
* Familiarità di base con C# e le formule di Excel

## Passo 1: Come usare WRAPCOLS per dividere un intervallo in colonne

La funzione **WRAPCOLS** prende un intervallo monodimensionale e distribuisce i suoi valori nel numero specificato di colonne. In questo esempio partiamo da valori in `A1:A10` e chiediamo a WRAPCOLS di creare tre colonne.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is the “create excel workbook programmatically” step
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Populate source data for demonstration
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 0].PutValue($"Item {i + 1}");
        }

        // Apply WRAPCOLS: split A1:A10 into 3 columns starting at C1
        // The formula is entered in cell C1 (row 0, column 2)
        ws.Cells[0, 2].Formula = "=WRAPCOLS(A1:A10,3)";

        // -------------------------------------------------
        // Why this works:
        // -------------------------------------------------
        // * WRAPCOLS reads the source range (A1:A10) vertically.
        // * The second argument (3) tells Excel to create three columns.
        // * The function returns a 2‑dimensional array that Excel spills into the
        //   surrounding cells automatically.
        // -------------------------------------------------
```

> **Risultato:** Le celle `C1:E4` ora contengono i dieci elementi originali disposti in tre colonne (l'ultima colonna contiene gli elementi rimanenti).

![Screenshot che illustra come usare WRAPCOLS per dividere un intervallo in colonne in Excel](image-url.png)

## Passo 2: Dividere l'intervallo in righe con WRAPROWS

Mentre **WRAPCOLS** opera orizzontalmente, **WRAPROWS** fa l'opposto: distribuisce un intervallo su un dato numero di righe. Qui prendiamo i valori da `B1:B10` e li disponiamo in due righe a partire da `F1`.

```csharp
        // Populate a second source column for WRAPROWS
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 1].PutValue($"Value {i + 1}");
        }

        // Apply WRAPROWS: split B1:B10 into 2 rows starting at F1
        ws.Cells[0, 5].Formula = "=WRAPROWS(B1:B10,2)";

        // -------------------------------------------------
        // Why WRAPROWS is useful:
        // -------------------------------------------------
        // * It converts a vertical list into a matrix with the specified row count.
        // * Handy when you need to prepare data for pivot tables, charts, or
        //   reporting layouts that expect a horizontal orientation.
        // -------------------------------------------------
```

> **Risultato:** La formula riempie le celle `F1:K2` con i dieci valori distribuiti su due righe.

## Passo 3: Salvare la cartella di lavoro come XLSX

Dopo aver applicato le formule, l'ultimo passo è persistere il file. L'operazione **save workbook as xlsx** scrive la cartella di lavoro in memoria su disco nel moderno formato OpenXML.

```csharp
        // Save the workbook – this completes the “save workbook as xlsx” step
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "wrapcols_wraprows_output.xlsx");

        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Come appare il file salvato

Quando apri `wrapcols_wraprows_output.xlsx` in Excel vedrai:

| C | D | E |
|---|---|---|
| Item 1 | Item 4 | Item 7 |
| Item 2 | Item 5 | Item 8 |
| Item 3 | Item 6 | Item 9 |
|        |        | Item 10 |

e

| F | G | H | I | J | K |
|---|---|---|---|---|---|
| Value 1 | Value 3 | Value 5 | Value 7 | Value 9 | |
| Value 2 | Value 4 | Value 6 | Value 8 | Value 10 | |

Le formule rimangono nelle celle, quindi eventuali modifiche successive agli intervalli di origine vengono riflesse automaticamente.

## Passo 4: Varianti comuni e casi limite

### Modificare il numero di colonne o righe

* **Più colonne:** Incrementa il secondo argomento di `WRAPCOLS`.  
  Esempio: `=WRAPCOLS(A1:A10,5)` crea cinque colonne, lasciando celle vuote dove i dati finiscono.
* **Conteggio colonne dinamico:** Usa un riferimento di cella invece di un numero fisso.  
  `=WRAPCOLS(A1:A10, G1)` dove `G1` contiene il numero di colonne desiderato.

### Gestire celle vuote o non numeriche

WRAPCOLS e WRAPROWS ignorano le celle vuote per impostazione predefinita, ma preservano l'ordine dei valori non vuoti. Se devi mantenere gli spazi vuoti, avvolgi l'intervallo di origine con le funzioni `IFERROR` o `TEXT` prima di applicare WRAPCOLS.

### Salvataggio in altri formati

Mentre questo tutorial si concentra su **save workbook as xlsx**, Aspose.Cells supporta molti formati (`.xls`, `.csv`, `.pdf`, ecc.):

```csharp
workbook.Save("output.pdf", SaveFormat.Pdf);   // Export to PDF
workbook.Save("output.csv", SaveFormat.Csv);   // Export to CSV
```

## Consigli professionali e insidie

* **Consiglio pro:** Imposta `Workbook.Settings.CalcEngineEnabled = true` se prevedi di valutare le formule subito dopo il salvataggio.
* **Attenzione a:** Intervalli di origine molto grandi possono generare aree di spill molto ampie, influenzando le prestazioni. Limita la dimensione dell'intervallo o suddividi l'operazione in più fogli di lavoro.
* **Sicurezza dei thread:** Gli oggetti Aspose.Cells **non** sono thread‑safe. Crea un'istanza `Workbook` separata per ogni thread se elabori file in parallelo.

## Conclusione

Ora sai **come usare WRAPCOLS** per dividere un intervallo verticale in più colonne, **come dividere l'intervallo in righe** con WRAPROWS, e **come salvare la cartella di lavoro come XLSX** dopo aver effettuato queste trasformazioni. Seguendo i passaggi sopra potrai **creare excel workbook programmatically**, applicare potenti formule di spill e generare file Excel pronti da condividere senza intervento manuale.

### Cosa fare dopo?

* Esplora **conditional formatting** per evidenziare i dati spillati.
* Combina **WRAPCOLS** con **SORT** o **FILTER** per dashboard dinamici.
* Usa l'**API di charting** di Aspose.Cells per visualizzare i dati riorganizzati direttamente dal codice.

Buona programmazione e buona automazione dei tuoi flussi di lavoro Excel!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [come usare wrapcols in C# – Guida completa con Excel WRAPROWS & Ricalcolo formule](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [Come usare WRAPCOLS in C# – Rimodellare un array in una matrice in Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)
- [Come usare WRAPCOLS – Guida completa per l'automazione Excel in C#](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}