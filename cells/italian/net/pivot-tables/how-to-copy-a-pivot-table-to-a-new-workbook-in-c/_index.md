---
category: general
date: 2026-11-16
description: Come copiare una tabella pivot da un file Excel a una nuova cartella
  di lavoro usando C#. Impara a caricare la cartella di lavoro, copiare l’intervallo
  e preservare le tabelle pivot.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new workbook
- load excel workbook c#
- Aspose.Cells copy pivot
- preserve pivot table C#
- Excel automation C#
language: it
lastmod: 2026-11-16
og_description: Come copiare una tabella pivot da una cartella di lavoro esistente
  a una nuova cartella di lavoro usando C#. Segui questa guida completa per caricare
  la cartella di lavoro Excel, copiare l’intervallo e mantenere intatta la pivot.
og_image_alt: how to copy pivot table example in C#
og_title: Come copiare una tabella pivot in una nuova cartella di lavoro in C# – guida
  passo‑passo
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  headline: How to copy a pivot table to a new workbook in C#
  type: TechArticle
- description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  name: How to copy a pivot table to a new workbook in C#
  steps:
  - name: Expected output
    text: 'Running the program produces `CopyWithPivot.xlsx`. Opening the file in
      Excel shows:'
  - name: Copying multiple pivot tables
    text: If your source sheet contains several pivots, expand the `CellArea` to cover
      the union of all ranges, or repeat the copy step for each distinct area.
  - name: Preserving styles and conditional formatting
    text: '`CopyRows` copies cell styles automatically. If you need to preserve workbook‑wide
      named styles or custom number formats, call `destWorkbook.Worksheets[0].CopyStyle`
      before saving.'
  - name: Working with large workbooks
    text: For files larger than 100 MB, consider using `Workbook.LoadOptions` with
      the `MemorySetting` set to `MemorySetting.MemoryPreference` to reduce memory
      pressure.
  - name: Next steps
    text: '* Explore **Aspose.Cells** features such as refreshing pivots programmatically.
      * Combine this approach with **ExcelPackage** (EPPlus) if you need an open‑source
      alternative. * Automate copying across multiple sheets by looping through `srcWorkbook.Worksheets`.'
  type: HowTo
- questions:
  - answer: Aspose.Cells can read macro‑enabled files (`.xlsm`), but the macro code
      isn’t copied. The pivot table itself is preserved because it’s part of the worksheet
      XML.
    question: Does this work with macros or VBA‑enabled workbooks?
  - answer: The copy operation includes the cached data only. If the destination workbook
      needs to refresh from the original source, you’ll have to re‑configure the data
      connection manually.
    question: What if the pivot uses an external data source?
  - answer: 'No. A pivot table needs its cache. The most reliable way is to copy the
      rows that contain the cache, as demonstrated. You can later hide those rows
      if you don’t want them visible. ## Conclusion You now know **how to copy pivot
      table** from one Excel file to another using C#. The tutorial covered **l'
    question: Can I copy the pivot without the underlying data rows?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Come copiare una tabella pivot in una nuova cartella di lavoro in C#
url: /it/net/pivot-tables/how-to-copy-a-pivot-table-to-a-new-workbook-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come copiare una tabella pivot in una nuova cartella di lavoro in C#

Se hai bisogno di **come copiare tabella pivot** da un file Excel a una nuova cartella di lavoro, questa guida mostra i passaggi esatti. Imparerai come **load excel workbook c#**, definire l’intervallo di origine e **copy range to new workbook** mantenendo intatta la pivot.

Copiare una tabella pivot è una necessità comune quando vuoi riutilizzare un modello di report, migrare dati tra progetti o generare un file leggero per la distribuzione. Il campione di codice qui sotto utilizza Aspose.Cells, una libreria .NET completamente gestita che funziona senza Microsoft Office installato. Alla fine di questo tutorial avrai un programma eseguibile che crea una nuova cartella di lavoro contenente la tabella pivot originale, pronta per ulteriori elaborazioni o condivisioni.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* .NET 6.0 SDK o successivo (l’esempio funziona con .NET Core e .NET Framework)
* Visual Studio 2022 o qualsiasi editor C# tu preferisca
* Una licenza Aspose.Cells per .NET (la versione di prova gratuita è valida per la valutazione)
* Un file Excel di origine (`Source.xlsx`) che contenga almeno una tabella pivot

> **Suggerimento:** Se utilizzi la versione di prova gratuita, imposta la licenza nel codice per evitare filigrane di valutazione.

## Passo 1: Caricare la cartella di lavoro di origine (load excel workbook c#)

La prima azione è aprire la cartella di lavoro che contiene la tabella pivot. Aspose.Cells legge il file in memoria, fornendoti pieno accesso a fogli, celle e oggetti pivot.

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Load the source workbook that contains the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");
```

*Perché è importante*: Caricare la cartella di lavoro è la base per qualsiasi automazione Excel. Senza un oggetto `Workbook` valido non puoi ispezionare la pivot né copiare i suoi dati.

## Passo 2: Definire l’area di celle che racchiude la tabella pivot (copy range to new workbook)

Una tabella pivot vive all’interno di un blocco rettangolare di celle. Devi specificare quel blocco affinché l’operazione di copia sappia cosa spostare. Il costruttore `CellArea` utilizza indici a base zero: `StartRow, StartColumn, EndRow, EndColumn`.

```csharp
        // Define the cell range that encloses the pivot table, e.g., A1:K21
        // Row and column indexes start at 0, so A1 = (0,0)
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21
```

*Perché è importante*: Impostando esplicitamente l’intervallo eviti di copiare dati non correlati e garantisci che la cache della pivot sia inclusa. L’intervallo può essere calcolato dinamicamente se devi gestire dimensioni di pivot variabili.

## Passo 3: Creare una nuova cartella di lavoro e ottenere il suo primo foglio

Ora crea la cartella di lavoro di destinazione che riceverà le righe copiate. Aspose.Cells aggiunge automaticamente un foglio di lavoro predefinito, che utilizzeremo come destinazione.

```csharp
        // Create a new workbook that will receive the copied range
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Perché è importante*: Partire da una cartella di lavoro pulita garantisce che solo la tabella pivot (e le righe di supporto) finiscano nel file, mantenendo l’output leggero.

## Passo 4: Copiare le righe dall’intervallo di origine al foglio di destinazione (how to copy pivot table)

Il metodo `CopyRows` copia intere righe, preservando formule, formattazione e—soprattutto—tabelle pivot. I parametri del metodo sono: riga di inizio, riga di fine, collezione di celle di destinazione e l’indice di riga nella destinazione dove inizia la copia (qui `0` per partire dalla prima riga).

```csharp
        // Copy the rows that contain the pivot table.
        // Pivot tables inside the range are preserved automatically.
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);
```

*Perché è importante*: Usare `CopyRows` invece di copiare celle singole assicura che la cache della pivot rimanga collegata ai dati copiati. Aspose.Cells gestisce le strutture XML sottostanti, così non è necessario ricostruire manualmente la pivot.

## Passo 5: Salvare la cartella di lavoro risultante (copy range to new workbook)

Infine, scrivi il nuovo file su disco. La cartella di lavoro di destinazione ora contiene una tabella pivot identica che funziona indipendentemente dal file di origine.

```csharp
        // Save the new workbook with the copied pivot table
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        // Optional: inform the user
        System.Console.WriteLine("Pivot table copied successfully!");
    }
}
```

### Output previsto

L’esecuzione del programma produce `CopyWithPivot.xlsx`. Aprendo il file in Excel si osserva:

* Lo stesso layout della tabella pivot di `Source.xlsx`
* Tutte le righe di dati di origine che facevano parte della cache della pivot
* Nessun riferimento alla cartella di lavoro originale (la pivot funziona offline)

## Gestione delle variazioni comuni

### Copiare più tabelle pivot

Se il foglio di origine contiene diverse pivot, espandi il `CellArea` per coprire l’unione di tutti gli intervalli, oppure ripeti il passaggio di copia per ciascuna area distinta.

```csharp
// Example: copy two separate ranges
CellArea firstPivot = new CellArea(0, 0, 20, 10);
CellArea secondPivot = new CellArea(25, 0, 45, 10);

destWorksheet.Cells.CopyRows(firstPivot.StartRow, firstPivot.EndRow, destWorksheet.Cells, 0);
destWorksheet.Cells.CopyRows(secondPivot.StartRow, secondPivot.EndRow, destWorksheet.Cells, 21); // start after first block
```

### Preservare stili e formattazione condizionale

`CopyRows` copia automaticamente gli stili delle celle. Se devi preservare stili nominati a livello di cartella di lavoro o formati numerici personalizzati, chiama `destWorkbook.Worksheets[0].CopyStyle` prima di salvare.

### Lavorare con cartelle di lavoro di grandi dimensioni

Per file superiori a 100 MB, considera l’uso di `Workbook.LoadOptions` con `MemorySetting` impostato a `MemorySetting.MemoryPreference` per ridurre la pressione sulla memoria.

```csharp
LoadOptions loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeSrc = new Workbook(@"bigfile.xlsx", loadOptions);
```

## Codice sorgente completo (pronto per l'esecuzione)

Di seguito trovi il programma completo, inclusi i `using` e i commenti. Copialo in un nuovo progetto console e sostituisci `YOUR_DIRECTORY` con il percorso reale della cartella.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source workbook (load excel workbook c#)
        // -------------------------------------------------
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");

        // -------------------------------------------------
        // Step 2: Define the area that contains the pivot table
        // -------------------------------------------------
        // Adjust the indices if your pivot occupies a different range.
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21

        // -------------------------------------------------
        // Step 3: Create the destination workbook
        // -------------------------------------------------
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // -------------------------------------------------
        // Step 4: Copy rows (how to copy pivot table)
        // -------------------------------------------------
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);

        // -------------------------------------------------
        // Step 5: Save the new file (copy range to new workbook)
        // -------------------------------------------------
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        Console.WriteLine("Pivot table copied successfully!");
    }
}
```

Esegui il programma (`dotnet run` o `Ctrl+F5` in Visual Studio). Dopo l’esecuzione, apri `CopyWithPivot.xlsx` per verificare che la pivot si comporti esattamente come l’originale.

## Domande frequenti

**D: Questo funziona con cartelle di lavoro macro‑abilitate o VBA?**  
R: Aspose.Cells può leggere file macro‑abilitati (`.xlsm`), ma il codice macro non viene copiato. La tabella pivot stessa è preservata perché fa parte dell’XML del foglio di lavoro.

**D: E se la pivot utilizza una fonte dati esterna?**  
R: L’operazione di copia include solo i dati nella cache. Se la cartella di lavoro di destinazione deve aggiornarsi dalla fonte originale, dovrai riconfigurare manualmente la connessione dati.

**D: Posso copiare la pivot senza le righe di dati sottostanti?**  
R: No. Una tabella pivot necessita della sua cache. Il modo più affidabile è copiare le righe che contengono la cache, come mostrato. Puoi nascondere successivamente quelle righe se non vuoi che siano visibili.

## Conclusione

Ora sai **come copiare tabella pivot** da un file Excel a un altro usando C#. Il tutorial ha coperto **load excel workbook c#**, ha definito **copy range to new workbook** e ha utilizzato il metodo `CopyRows` di Aspose.Cells per mantenere intatta la pivot. Con l’esempio completo e funzionante puoi integrare questo modello nei pipeline di reporting, negli strumenti di esportazione automatica o in qualsiasi scenario in cui una pivot deve viaggiare tra cartelle di lavoro.

### Passi successivi

* Esplora le funzionalità di **Aspose.Cells** come l’aggiornamento delle pivot programmaticamente.  
* Combina questo approccio con **ExcelPackage** (EPPlus) se ti serve un’alternativa open‑source.  
* Automatizza la copia su più fogli iterando su `srcWorkbook.Worksheets`.  

Sentiti libero di sperimentare con intervalli diversi, aggiungere stili personalizzati o incorporare la logica in un servizio più ampio di elaborazione dati. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell’API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)
- [How to copy pivot table in Excel with C# and Aspose.Cells](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/)
- [Copy pivot table to new workbook, export shape to PowerPoint](/cells/english/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}