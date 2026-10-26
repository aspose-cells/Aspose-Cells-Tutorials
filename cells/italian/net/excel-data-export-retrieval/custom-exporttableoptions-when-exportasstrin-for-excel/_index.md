---
category: general
date: 2026-10-26
description: Le opzioni personalizzate ExportTableOptions quando ExportAsStrin ti
  consentono di esportare i dati di Excel come stringhe in C#. Segui la guida passo‑passo
  per configurare ed eseguire l'esportazione.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: it
lastmod: 2026-10-26
og_description: ExportTableOptions personalizzate quando ExportAsStrin abilita l'esportazione
  Excel solo stringhe. Scopri i passaggi esatti per configurare ed eseguire l'esportazione
  in C#.
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: Opzioni ExportTable personalizzate quando ExportAsString – esporta Excel
  come stringa in C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Custom ExportTableOptions when ExportAsStrin lets you export Excel
    data as strings in C#. Follow the step‑by‑step guide to configure and run the
    export.
  headline: Custom ExportTableOptions when ExportAsStrin for Excel
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Opzioni personalizzate di ExportTable quando ExportAsStrin per Excel
url: /it/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Custom ExportTableOptions when ExportAsStrin – esporta Excel come stringa in C#

Se hai bisogno di **Custom ExportTableOptions when ExportAsStrin** per ottenere il valore di ogni cella come stringa semplice, questa guida ti mostra esattamente come farlo. Che tu stia costruendo una pipeline di importazione dati o abbia bisogno di un dump pronto per CSV pulito, vedrai perché configurare le opzioni in questo modo evita sorprese di conversione dei tipi.

In questo tutorial imparerai **come esportare excel come stringa** usando la libreria Aspose.Cells, vedrai il codice completo e eseguibile, e comprenderai la logica dietro ogni impostazione. Non è necessaria alcuna documentazione esterna – tutto ciò che ti serve è qui.

## Prerequisiti

* .NET 6.0 SDK o versioni successive installato  
* Visual Studio 2022 (o qualsiasi IDE che supporti .NET)  
* Pacchetto Aspose.Cells per .NET (installare via NuGet: `Install-Package Aspose.Cells`)  
* Un workbook Excel (`sample.xlsx`) posizionato nella cartella radice del progetto  

Questi elementi sono le uniche dipendenze; il codice funziona su Windows, Linux o macOS senza librerie aggiuntive.

## Passo 1: Carica il workbook che desideri esportare

La prima cosa da fare quando si utilizza **Custom ExportTableOptions when ExportAsStrin** è ottenere un oggetto `Worksheet` da un workbook caricato. Questo oggetto ti dà accesso a righe, colonne e all'API di esportazione.

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*Perché è importante:*  
`Workbook` legge il file una sola volta e mantiene tutte le informazioni di formattazione in memoria. Selezionando un `Worksheet` specifico, limiti l'ambito di esportazione ed eviti l'elaborazione non necessaria di fogli nascosti.

## Passo 2: Configura ExportTableOptions con ExportAsString = true

Il nucleo di **Custom ExportTableOptions when ExportAsStrin** è l'oggetto `ExportTableOptions`. Impostare `ExportAsString` costringe l'esportatore a trattare ogni cella come una stringa, indipendentemente dal tipo di dato originale (data, numero, booleano, ecc.). Abilitare `PreserveFormatting` mantiene lo stile visivo (ad esempio i simboli di valuta) nella stringa risultante.

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*Perché è importante:*  
Quando successivamente chiami `ExportDataTable`, la libreria normalmente tenta di inferire il tipo .NET di ogni colonna. Con `ExportAsString = true`, questo passaggio di inferenza viene saltato, evitando conversioni inattese di `DateTime` o `double` che potrebbero rompere i parser CSV a valle.

## Passo 3: Esporta un intervallo in un DataTable usando le opzioni personalizzate

Ora puoi esportare un intervallo rettangolare (righe 0‑9, colonne 0‑4) dal worksheet. Il metodo restituisce un `DataTable` dove ogni campo è una `string`.

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*Perché è importante:*  
`ExportDataTable` è il modo più comodo per trasferire i dati Excel in una struttura relazionale che molte API .NET già comprendono (ad esempio Entity Framework, Dapper). Passando le **Custom ExportTableOptions when ExportAsStrin**, garantisci che ogni `DataColumn.DataType` sarà `typeof(string)`.

## Passo 4: Verifica il risultato – tutti i valori sono stringhe

È buona pratica confermare che l'esportazione si sia comportata come previsto. Il ciclo seguente stampa ogni cella e il suo tipo a runtime.

```csharp
Console.WriteLine("Exported DataTable (all values as strings):");
foreach (DataRow row in dataTable.Rows)
{
    for (int i = 0; i < dataTable.Columns.Count; i++)
    {
        object value = row[i];
        Console.Write($"{value} ({value.GetType().Name})\t");
    }
    Console.WriteLine();
}
```

**Output previsto**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

Ogni cella mostra `String` come tipo, confermando che **Custom ExportTableOptions when ExportAsStrin** ha funzionato correttamente.

## Passo 5: Opzionale – scrivi il DataTable in CSV

Se il tuo obiettivo finale è un file di testo semplice, puoi facilmente serializzare il `DataTable` in CSV:



## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Esporta stringhe HTML da Excel a DataTable usando Aspose.Cells per .NET: Guida passo‑passo](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [Esporta proprietà personalizzate Excel PDF Aspose Cells Net](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java Filtri di caricamento personalizzati Esportazione Excel](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}