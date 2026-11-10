---
category: general
date: 2026-09-27
description: Scopri come copiare una tabella pivot in C# usando Aspose.Cells. Include
  la copia delle righe con formattazione, la copia della tabella pivot in un altro
  foglio e l'esportazione della tabella pivot in una nuova cartella di lavoro.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: it
lastmod: 2026-09-27
og_description: Come copiare una tabella pivot in C# usando Aspose.Cells. Segui la
  guida passo‑passo per copiare le righe con la formattazione, spostare una tabella
  pivot su un altro foglio e esportarla in una nuova cartella di lavoro.
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: Come copiare una tabella pivot in C# – guida completa ad Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: Come copiare una tabella pivot in C# con Aspose.Cells
url: /it/net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come copiare una tabella pivot in C# con Aspose.Cells

Se hai bisogno di **copiare una tabella pivot** da un foglio di lavoro a un altro, imparare **come copiare una tabella pivot** in C# con Aspose.Cells può farti risparmiare ore di lavoro manuale. L'approccio ti consente anche di **copiare righe con formattazione**, mantenere intatto il cache della pivot e persino **esportare la tabella pivot in una nuova cartella di lavoro** quando ti serve un file autonomo.

Questo tutorial ti guida attraverso l'intero flusso di lavoro:

* creare una cartella di lavoro,  
* copiare l'intervallo della tabella pivot mantenendo la formattazione,  
* posizionare i dati copiati su un nuovo foglio, e  
* salvare il risultato come file separato.

Vedrai perché il metodo integrato `CopyRows` è il modo più affidabile per **copiare una tabella pivot su un altro foglio**, e otterrai consigli su come gestire casi particolari come righe nascoste o fonti di dati esterne.

## Prerequisiti

Prima di iniziare, assicurati di avere:

| Requisito | Perché è importante |
|-------------|----------------|
| .NET 6.0 o successivo | Aspose.Cells supporta .NET 6+ e offre le migliori prestazioni. |
| Visual Studio 2022 (o qualsiasi IDE C#) | Hai bisogno di un editor che possa ripristinare i pacchetti NuGet. |
| Aspose.Cells per .NET (pacchetto NuGet `Aspose.Cells`) | Questa libreria fornisce l'API `CopyRows` usata nell'esempio. |
| Un file Excel di origine (`source.xlsx`) che contiene una tabella pivot nell'intervallo `A1:G20` | Il codice copia questo intervallo specifico; regola l'intervallo se la tua tabella pivot è più grande. |

Installa la libreria con la CLI di NuGet o la Console di Package Manager:

```bash
dotnet add package Aspose.Cells
```

## Passo 1: Carica la cartella di lavoro che contiene la tabella pivot

La prima riga crea un oggetto `Workbook` che rappresenta l'intero file Excel. Caricare il file una volta ti dà accesso in lettura/scrittura a tutti i fogli di lavoro.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Perché questo passo è importante** – Senza caricare la cartella di lavoro, nessuna delle successive chiamate `CopyRows` può fare riferimento ai dati di origine o al cache della pivot.

## Passo 2: Prepara i fogli di lavoro di origine e destinazione

Hai bisogno di un foglio di destinazione dove vivrà la tabella pivot copiata. Il codice qui sotto recupera il primo foglio di lavoro (dove risiede la tabella pivot originale) e aggiunge un nuovo foglio chiamato **Copy**.

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **Consiglio professionale:** Se il foglio di destinazione esiste già, chiama prima `Worksheets.RemoveAt(index)` per evitare nomi duplicati.

## Passo 3: Definisci l'area di celle che racchiude la tabella pivot

Un oggetto `CellArea` descrive le celle in alto‑sinistra e in basso‑destra dell'intervallo che desideri spostare. In questo esempio la tabella pivot occupa `A1:G20`. Regola le coordinate per tabelle più grandi.

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## Passo 4: Copia le righe con formattazione e preserva il cache della pivot

Il metodo `CopyRows` copia **righe** dal foglio di origine al foglio di destinazione. Passando `CopyOptions.CopyAll` garantisci che valori, formattazione, grafici e oggetti incorporati—tutti elementi di una tabella pivot—vengano trasferiti.

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### Perché `CopyRows` funziona meglio di `Copy` per le tabelle pivot

* `CopyRows` rispetta il cache interno della pivot, quindi la tabella pivot copiata rimane funzionale.
* Preserva **copiare righe con formattazione** esattamente come appaiono nel foglio originale.
* A differenza di un semplice `Copy` di un intervallo, sposta anche le righe nascoste e eventuali slicer associati.

## Passo 5: Salva la cartella di lavoro con la tabella pivot copiata

Infine, scrivi la cartella di lavoro modificata su disco. Il nuovo file contiene il foglio originale più un foglio **Copy** che contiene un duplicato completamente funzionale della tabella pivot originale.

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### Risultato atteso

Quando apri `pivot_copied.xlsx`:

* Il foglio **Sheet1** contiene ancora i dati e la tabella pivot originali.
* Il foglio **Copy** mostra una tabella pivot identica con lo stesso layout, filtri e formattazione.
* Tutte le formule e le connessioni dati rimangono intatte perché il cache della pivot è stato copiato insieme alle righe.

## Come copiare una tabella pivot su un altro foglio nella stessa cartella di lavoro

Se ti serve la tabella pivot in un altro foglio esistente (ad es., “Report”), sostituisci il passo di creazione della destinazione con un riferimento al foglio di destinazione:

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

Questo frammento dimostra **copiare la tabella pivot su un altro foglio** senza creare un nuovo foglio di lavoro.

## Esporta la tabella pivot in una nuova cartella di lavoro

A volte vuoi la tabella pivot in un file completamente separato. Dopo l'operazione di copia, puoi rimuovere tutti i fogli di lavoro tranne quello che contiene la tabella pivot copiata e poi salvare:

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

Ora `pivot_only.xlsx` contiene un unico foglio con la tabella pivot duplicata, soddisfacendo il requisito di **esportare la tabella pivot in una nuova cartella di lavoro**.

## Come copiare righe Excel senza perdere la formattazione

La stessa chiamata `CopyRows` funziona per qualsiasi intervallo, non solo per le tabelle pivot. Se hai bisogno di **copiare righe Excel** che includono formattazione condizionale, convalida dati o celle unite, usa lo stesso metodo:

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

Poiché `CopyOptions.CopyAll` trasferisce tutto, le righe di destinazione appaiono esattamente come le righe di origine.

## Problemi comuni e come evitarli

| Problema | Sintomo | Soluzione |
|---------|---------|-----|
| L'intervallo di origine non include l'intera tabella pivot | La tabella pivot copiata appare troncata. | Verifica che il `CellArea` copra tutte le righe/colonne della tabella pivot. |
| Il foglio di destinazione contiene già dati | Le righe sovrascritte causano perdita di dati. | Scegli un foglio nuovo o inizia a copiare a un indice di riga più alto. |
| La tabella pivot utilizza una fonte dati esterna | La copia perde la connessione. | Dopo la copia, chiama `pivotTable.RefreshData()` per ristabilire il collegamento. |
| Le righe nascoste vengono omesse | Alcune righe scompaiono nella copia. | `CopyRows` copia automaticamente le righe nascoste; assicurati di non usare `CopyOptions.CopyValuesOnly`. |

## Esempio completo e eseguibile

Di seguito trovi un programma autonomo che puoi incollare in un nuovo progetto console. Dimostra ogni passo discusso sopra.

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**Eseguendo il programma** crea `pivot_copied.xlsx` con un duplicato della tabella pivot originale su un nuovo foglio chiamato **Copy**.

## Conclusione

Ora sai **come copiare una tabella pivot** in C# usando

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea nuova cartella di lavoro – Come copiare un foglio di lavoro con una tabella pivot](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copia tabella pivot in C# – Guida completa passo‑passo](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Come copiare un intervallo con tabelle pivot in C# – Guida completa](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}