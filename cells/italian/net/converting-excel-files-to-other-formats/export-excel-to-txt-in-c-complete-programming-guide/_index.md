---
category: general
date: 2026-08-11
description: Esporta Excel in txt in C# con una guida passo‑passo. Scopri come convertire
  xlsx in testo semplice usando Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- convert xlsx to plain text
- how to export excel worksheet as text
- export worksheet as text file
language: it
lastmod: 2026-08-11
og_description: Esporta Excel in txt in C# rapidamente. Questo tutorial mostra come
  convertire xlsx in testo semplice, configurare i formati e gestire fogli di lavoro
  di grandi dimensioni.
og_image_alt: Code snippet that exports an Excel worksheet to a plain text file using
  C#
og_title: Esporta Excel in TXT in C# – guida passo‑passo per sviluppatori
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  headline: Export excel to txt in C# – complete programming guide
  type: TechArticle
- description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  name: Export excel to txt in C# – complete programming guide
  steps:
  - name: – load the workbook
    text: '```csharp using Aspose.Cells;'
  - name: – get the first worksheet
    text: '```csharp Worksheet sheet = workbook.Worksheets[0]; ```'
  - name: – define export options for text conversion
    text: '```csharp ExportTableOptions exportOptions = new ExportTableOptions { ExportAsString
      = true, // Export all values as text DateTimeFormat = "yyyy-MM-dd", // Desired
      date format NumberFormat = "#,##0.00" // Desired numeric format }; ```'
  - name: – export worksheet as text file
    text: '```csharp // Apply the options to the worksheet sheet.ExportTableOptions
      = exportOptions;'
  type: HowTo
tags:
- excel
- csharp
- text export
- aspose.cells
title: Esporta Excel in TXT in C# – guida completa alla programmazione
url: /it/net/converting-excel-files-to-other-formats/export-excel-to-txt-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esportare Excel in TXT con C# – guida completa alla programmazione

Se hai bisogno di **esportare excel in txt** puoi ottenere il risultato con poche righe di codice C#. Questa guida mostra come convertire una cartella di lavoro `.xlsx` in un file di testo semplice mantenendo il formato dei dati che definisci.

Esportare i fogli di lavoro come file di testo è una necessità comune quando i sistemi a valle accettano solo dati delimitati o quando è necessario verificare i valori grezzi delle celle. Nelle sezioni seguenti imparerai a configurare i formati data e numero, gestire fogli di grandi dimensioni e evitare le insidie più tipiche.

## Prerequisiti per convertire xlsx in testo semplice

Prima di iniziare, assicurati di avere:

* .NET 6.0 (o successivo) installato – il codice punta a .NET Standard 2.0, quindi funziona anche con .NET Framework 4.6+.
* Una licenza per **Aspose.Cells** (la valutazione gratuita è sufficiente per i test).
* Un IDE come Visual Studio 2022 o Visual Studio Code.
* Un file Excel chiamato `input.xlsx` collocato in una cartella a cui il tuo progetto può fare riferimento.

Questi elementi sono gli unici requisiti esterni; il tutorial non dipende da altri pacchetti NuGet.

## Come esportare excel in txt usando Aspose.Cells

Aspose.Cells fornisce la classe `ExportTableOptions` che ti permette di controllare come i valori delle celle vengono renderizzati come stringhe. Impostando `ExportAsString` a `true` forzi ogni cella a essere scritta come testo, cosa essenziale quando desideri un output di testo deterministico.

### Passo 1 – caricare la cartella di lavoro

```csharp
using Aspose.Cells;

string inputPath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(inputPath);
```

*Il costruttore `Workbook` legge il file Excel in memoria. Se il file non esiste, viene sollevata un'eccezione, quindi potresti voler avvolgere questa chiamata in un blocco try‑catch per il codice di produzione.*

### Passo 2 – ottenere il primo foglio di lavoro

```csharp
Worksheet sheet = workbook.Worksheets[0];
```

*I fogli di lavoro sono indicizzati a partire da zero, quindi l'indice 0 si riferisce alla prima scheda. Puoi sostituire l'indice con il nome del foglio (`workbook.Worksheets["Sheet1"]`) quando devi puntare a una scheda specifica.*

### Passo 3 – definire le opzioni di esportazione per la conversione in testo

```csharp
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,               // Export all values as text
    DateTimeFormat = "yyyy-MM-dd",       // Desired date format
    NumberFormat   = "#,##0.00"          // Desired numeric format
};
```

*`ExportAsString` garantisce che ogni cella, indipendentemente dal tipo originale, diventi una stringa nel file di output. Le proprietà `DateTimeFormat` e `NumberFormat` ti consentono di controllare come appaiono date e numeri, il che è cruciale quando **converti xlsx in testo semplice** per sistemi che si aspettano un pattern specifico.*

### Passo 4 – esportare il foglio di lavoro come file di testo

```csharp
// Apply the options to the worksheet
sheet.ExportTableOptions = exportOptions;

// Export the data to a tab‑delimited text file
string outputPath = @"YOUR_DIRECTORY\Exported.txt";
sheet.ExportDataTable(outputPath);
```

*`ExportDataTable` scrive il contenuto del foglio di lavoro in un file di testo semplice usando le opzioni fornite. Il delimitatore predefinito è il carattere tab (`\t`). Se ti serve un delimitatore diverso, puoi usare la sovraccarico che accetta un'istanza di `ExportTableOptions` e specificare `ExportTableOptions.Separator`. Il file risultante può essere aperto in qualsiasi editor di testo o importato in un database.*

#### Output previsto

Supponiamo che `input.xlsx` contenga:

| A            | B       | C          |
|--------------|---------|------------|
| 2023‑05‑01   | 1234.5  | Sample text|

Con le opzioni sopra il file `Exported.txt` conterrà:

```
2023-05-01	1,234.50	Sample text
```

Ogni colonna è separata da un tab, le date seguono il formato `yyyy‑MM‑dd` e i numeri usano la virgola come separatore delle migliaia e due cifre decimali.

## Problemi comuni quando esporti un foglio di lavoro come file di testo

| Problema | Perché accade | Come evitarlo |
|----------|---------------|---------------|
| Formattazione numerica dipendente dalla locale | Il formato predefinito rispetta la cultura del sistema operativo, il che può produrre virgole o punti in modo incoerente. | Imposta esplicitamente `NumberFormat` in `ExportTableOptions`. |
| Righe o colonne nascoste appaiono nell'output | Aspose.Cells esporta l'intero intervallo usato, comprese le righe nascoste. | Imposta `ExportTableOptions.ExportHiddenRows = false` e `ExportHiddenColumns = false` se vuoi saltarle. |
| Fogli di lavoro molto grandi causano pressione sulla memoria | L'intera cartella di lavoro viene caricata in memoria prima dell'esportazione. | Usa `Workbook.LoadOptions` con `LoadDataOnly = true` per ridurre l'uso di memoria, oppure elabora il file a blocchi. |
| Celle data memorizzate come testo nel file sorgente | Se una cella contiene già una stringa formattata, l'esportatore la tratta come testo e ignora `DateTimeFormat`. | Assicurati che la cartella di lavoro sorgente memorizzi le date come veri tipi data di Excel. |

Affrontare questi problemi rende il processo **come esportare un foglio di lavoro Excel come testo** affidabile in diversi ambienti.

## Estendere la soluzione – delimitatori personalizzati e esportazione in streaming

Se ti serve un file CSV (valori separati da virgola) invece di un file delimitato da tab, modifica le opzioni:

```csharp
exportOptions.Separator = ',';
exportOptions.ExportHiddenRows = false;   // optional
exportOptions.ExportHiddenColumns = false; // optional
sheet.ExportTableOptions = exportOptions;
sheet.ExportDataTable(@"YOUR_DIRECTORY\Exported.csv");
```

Per file più grandi di 500 MB, lo streaming dell'output impedisce all'applicazione di esaurire la RAM:

```csharp
using (FileStream stream = new FileStream(@"YOUR_DIRECTORY\LargeExport.txt",
                                          FileMode.Create,
                                          FileAccess.Write,
                                          FileShare.None,
                                          bufferSize: 81920,
                                          useAsync: true))
{
    sheet.ExportDataTable(stream, exportOptions);
}
```

La sovraccarico che accetta uno `Stream` scrive le righe in modo incrementale, ideale per job batch o servizi web che restituiscono direttamente il file di testo al client.

## Verifica del risultato programmaticamente

Dopo che l'esportazione è terminata puoi leggere la prima riga in memoria per confermare il formato:

```csharp
string firstLine = File.ReadLines(outputPath).First();
Console.WriteLine($"First line: {firstLine}");
```

Eseguendo questo snippet dovrebbe stampare la stessa riga mostrata nella sezione *Output previsto*, dandoti la certezza che la conversione è avvenuta con successo.

## Riepilogo del codice completo

Unendo tutti i pezzi ottieni un programma autonomo che puoi copiare in un'applicazione console:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputPath  = @"YOUR_DIRECTORY\input.xlsx";
        string outputPath = @"YOUR_DIRECTORY\Exported.txt";

        // Load workbook
        Workbook workbook = new Workbook(inputPath);
        Worksheet sheet = workbook.Worksheets[0];

        // Configure export options
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            DateTimeFormat = "yyyy-MM-dd",
            NumberFormat   = "#,##0.00",
            Separator      = '\t' // tab delimiter
        };

        // Apply options and export
        sheet.ExportTableOptions = exportOptions;
        sheet.ExportDataTable(outputPath);

        // Simple verification
        string firstLine = File.ReadLines(outputPath).First();
        Console.WriteLine($"Export completed. First line: {firstLine}");
    }
}
```

Compila ed esegui il programma; il file `Exported.txt` apparirà nella stessa directory della cartella di lavoro sorgente.

## Prossimi passi e argomenti correlati

* **Export worksheet as text file** – sperimenta con diversi delimitatori, codifiche (UTF‑8 vs. ASCII) e stili di terminazione di riga per la compatibilità cross‑platform.
* **Bulk conversion** – itera su `workbook.Worksheets` per generare un file di testo separato per ogni scheda.
* **Integration with databases** – indirizza il testo generato direttamente in un'operazione di bulk‑insert per SQL Server o PostgreSQL.
* 

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Export Excel Files in .NET Using Aspose.Cells&#58; A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Export Visible Excel Rows Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}