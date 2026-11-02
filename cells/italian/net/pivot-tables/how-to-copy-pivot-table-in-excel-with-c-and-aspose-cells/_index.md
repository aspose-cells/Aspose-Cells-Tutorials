---
category: general
date: 2026-10-04
description: Scopri come copiare una tabella pivot da una cartella di lavoro all'altra
  usando C#. Questa guida copre anche come copiare righe, duplicare la tabella pivot
  e copiare l’intervallo Excel in modo efficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- how to copy rows
- duplicate pivot table
language: it
lastmod: 2026-10-04
og_description: Copia la tabella pivot in Excel usando C#. Segui questo tutorial completo
  per duplicare le tabelle pivot, copiare le righe e copiare l'intervallo di Excel
  con Aspose.Cells.
og_image_alt: Screenshot showing a duplicated pivot table in an Excel worksheet after
  using C# code
og_title: Copia tabella pivot in Excel con C# – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to copy pivot table from one workbook to another using C#.
    This guide also covers how to copy rows, duplicate pivot table, and copy Excel
    range efficiently.
  headline: How to copy pivot table in Excel with C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Come copiare una tabella pivot in Excel con C# e Aspose.Cells
url: /it/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come copiare una tabella pivot in Excel con C# e Aspose.Cells

Se hai bisogno di **copiare una tabella pivot** da una cartella di lavoro a un'altra, questo tutorial ti mostra una soluzione completa e eseguibile. Vedrai esattamente come caricare un file di origine, definire l'intervallo che contiene la pivot, copiare le righe (inclusa la definizione della pivot) e salvare il risultato. Che tu stia automatizzando una pipeline di reporting o costruendo uno strumento di migrazione, i passaggi seguenti ti consentono di duplicare una tabella pivot con poche righe di C#.

Copiare una tabella pivot è più che copiare i valori delle celle; la cache sottostante e le impostazioni dei campi devono viaggiare insieme. L'esempio utilizza la libreria **Aspose.Cells** perché gestisce automaticamente i metadati della pivot, così non devi ricostruire la cache manualmente. Alla fine di questa guida sarai in grado di **come copiare una pivot**, **copiare intervallo Excel**, e **come copiare righe** in modo sicuro.

## Prerequisiti

- .NET 6.0 o versioni successive installato (il codice funziona anche con .NET Framework 4.7+).
- Una licenza valida di Aspose.Cells per .NET o una licenza di valutazione temporanea.
- Due file Excel: `Source.xlsx` contenente la tabella pivot che desideri duplicare e una cartella vuota dove verrà scritto `CopyWithPivot.xlsx`.
- Visual Studio 2022 (o qualsiasi IDE che supporti C#).

## Passo 1: Configurare il progetto e aggiungere Aspose.Cells

Crea un nuovo progetto console e aggiungi il pacchetto NuGet Aspose.Cells:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
dotnet add package Aspose.Cells
```

Il pacchetto fornisce le classi `Workbook`, `Worksheet` e `CellArea` utilizzate nel codice qui sotto.

## Passo 2: Caricare la cartella di lavoro di origine che contiene la tabella pivot

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the source workbook that holds the pivot you want to duplicate
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");
```

> **Perché è importante:** Caricare la cartella di lavoro crea una rappresentazione in memoria di tutti i fogli, incluse eventuali cache pivot nascoste. Senza caricare il file, non è possibile fare riferimento all'intervallo della pivot.

## Passo 3: Definire l'area di celle che copre la tabella pivot

Devi indicare ad Aspose.Cells quali righe e colonne appartengono alla pivot. La struttura `CellArea` ti consente di specificare un blocco rettangolare.

```csharp
        // Define the rectangle that encloses the pivot table (adjust as needed)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,      // first row (zero‑based)
            StartColumn = 0,   // first column
            EndRow = 30,       // last row of the pivot
            EndColumn = 10     // last column of the pivot
        };
```

> **Suggerimento:** Se non sei sicuro delle dimensioni esatte, apri il file di origine in Excel, seleziona la pivot e annota l'intervallo mostrato nella casella del nome (ad es., `A1:K31`). Converti le coordinate di Excel in indici basati su zero per il codice.

## Passo 4: Creare una nuova cartella di lavoro di destinazione e ottenere il suo primo foglio

```csharp
        // Create an empty workbook that will receive the copied pivot
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

> **Perché questo passaggio è necessario:** La cartella di lavoro di destinazione deve esistere prima di poter copiare le righe. Aspose.Cells crea automaticamente un foglio di lavoro predefinito, che useremo come destinazione.

## Passo 5: Copiare le righe (inclusa la tabella pivot) dall'origine alla destinazione

Il metodo `CopyRows` copia sia i valori delle celle sia la cache pivot sottostante.

```csharp
        // Copy rows from source to destination, preserving the pivot definition
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,      // source cells
            sourceRange.StartRow,                 // first row to copy
            sourceRange.EndRow - sourceRange.StartRow + 1, // number of rows
            destWorksheet.Cells,                  // target cells
            sourceRange.StartRow);                // target start row
```

> **Come funziona:**  
> - `CopyRows` prende il foglio di lavoro di origine, la riga di partenza e il numero di righe da copiare.  
> - Riceve anche il foglio di lavoro di destinazione e la riga in cui deve iniziare la copia.  
> - Poiché l'intervallo di origine include la tabella pivot, il metodo trasferisce la cache della pivot, l'elenco dei campi e il layout intatti. Questo è il fulcro di **come copiare una pivot** senza perdere funzionalità.

### Caso limite: copiare una pivot che si estende su più fogli

Se i dati di origine della pivot si trovano su un foglio diverso da quello della pivot stessa, la cache segue comunque la copia perché Aspose.Cells memorizza la cache nella cartella di lavoro, non nel foglio. Tuttavia, devi assicurarti che la cartella di lavoro di destinazione contenga lo stesso intervallo di dati di origine; altrimenti la pivot mostrerà errori `#REF!`. In questi casi, copia prima l'intervallo di dati di origine, poi le righe della pivot.

## Passo 6: Salvare la cartella di lavoro che ora contiene la tabella pivot copiata

```csharp
        // Persist the destination workbook to disk
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

Eseguendo il programma si genera `CopyWithPivot.xlsx` con una replica esatta della tabella pivot originale, inclusi tutti gli slicer, i filtri e i campi calcolati.

### Output previsto

Quando apri `CopyWithPivot.xlsx`:

- La tabella pivot appare nella stessa posizione (ad es., A1:K31) di `Source.xlsx`.
- Tutte le etichette di righe e colonne, i totali e la formattazione sono preservati.
- Aggiornare la pivot mostra gli stessi dati della sorgente, confermando che la cache è stata copiata correttamente.

## Come copiare righe senza una pivot (copiare intervallo Excel)

Se hai solo bisogno di **copiare intervallo Excel** senza alcun dato pivot, puoi usare lo stesso metodo `CopyRows` ma puntare a un intervallo che non contiene una pivot. Ad esempio:

```csharp
// Copy a simple data table from rows 5‑15, columns A‑D
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    4,            // start at row 5 (zero‑based)
    11,           // copy 11 rows (5‑15 inclusive)
    destWorksheet.Cells,
    0);           // paste at the top of the destination sheet
```

Questo dimostra **come copiare righe** per dati generici, rafforzando la versatilità della stessa API.

## Duplicare la tabella pivot nella stessa cartella di lavoro (approccio alternativo)

A volte vuoi **duplicare la tabella pivot** all'interno della stessa cartella di lavoro invece di creare un nuovo file. Puoi ottenere questo copiando le righe in una posizione diversa:

```csharp
// Duplicate pivot table to start at row 40 in the same worksheet
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    sourceRange.StartRow,
    sourceRange.EndRow - sourceRange.StartRow + 1,
    destWorksheet.Cells,
    40); // destination start row (zero‑based)
```

Dopo il salvataggio, la cartella di lavoro conterrà due pivot identiche—utile per confronti affiancati o per creare copie di backup.

## Problemi comuni e come evitarli

| Problema | Perché accade | Soluzione |
|----------|----------------|----------|
| La pivot mostra `#REF!` dopo la copia | L'intervallo di dati di origine non è presente nella cartella di lavoro di destinazione | Copia prima l'intervallo di dati di origine, oppure usa `CopyRows` sul foglio dei dati di origine prima di copiare la pivot |
| Formattazione persa | Sono stati copiati solo i valori (ad es., usando `Copy` invece di `CopyRows`) | Usa sempre `CopyRows` che preserva stile, formattazione e metadati della pivot |
| Scostamento di riga inatteso | La riga di inizio della destinazione non corrisponde a quella di origine | Verifica che la riga di inizio di `destWorksheet.Cells` corrisponda alla posizione desiderata |
| Cartelle di lavoro grandi causano pressione sulla memoria | `CopyRows` carica interi fogli di lavoro in memoria | Esegui la copia a blocchi o usa le API di streaming se lavori con più di 100.000 righe |

## Esempio completo, eseguibile

Di seguito trovi il programma completo che puoi incollare in `Program.cs` ed eseguire immediatamente (sostituisci `YOUR_DIRECTORY` con un percorso reale sul tuo computer).

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook containing the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");

        // 2️⃣ Define the area that encloses the pivot (adjust to your sheet)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 30,
            EndColumn = 10
        };

        // 3️⃣ Create the destination workbook (empty) and get its first sheet
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // 4️⃣ Copy rows—including the pivot cache—into the destination
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,
            sourceRange.StartRow,
            sourceRange.EndRow - sourceRange.StartRow + 1,
            destWorksheet.Cells,
            sourceRange.StartRow);

        // 5️⃣ Save the result
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

Esegui il programma con `dotnet run`. Dopo l'esecuzione, apri `CopyWithPivot.xlsx` per verificare che la tabella pivot appaia esattamente come nel file di origine.

## Conclusione

Ora sai come **copiare una tabella pivot** da una cartella di lavoro Excel a un'altra usando C# e Aspose.Cells. La guida ha coperto l'intero flusso di lavoro—dalla lettura del file di origine, alla definizione dell'area di celle della pivot, alla copia delle righe e al salvataggio della cartella di lavoro di destinazione. Hai anche imparato **come copiare righe**, **copiare intervallo Excel** e **duplicare la tabella pivot** nello stesso file, oltre ai problemi comuni e ai consigli di buona pratica.

Pronto per il passo successivo? Prova ad aggiungere del codice per aggiornare programmaticamente la pivot copiata, oppure esplora l'esportazione della pivot in PDF con Aspose.Cells. Sperimenta con diversi intervalli di origine e diventerai rapidamente esperto nell'automazione di Excel in .NET.

---

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Copiare la tabella pivot in C# – Guida completa passo‑per‑passo](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Creare una nuova cartella di lavoro Excel – Copia e duplica la tabella pivot](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [copiare righe Excel – Conservare la tabella pivot durante la duplicazione delle righe](/cells/english/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}