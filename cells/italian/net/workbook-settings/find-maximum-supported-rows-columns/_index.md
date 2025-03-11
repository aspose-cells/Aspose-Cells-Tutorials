---
title: Trova il numero massimo di righe e colonne supportate dai formati XLS e XLSX
linktitle: Trova il numero massimo di righe e colonne supportate dai formati XLS e XLSX
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri il numero massimo di righe e colonne supportate dai formati XLS e XLSX utilizzando Aspose.Cells per .NET. Ottimizza la gestione dei dati Excel con questo tutorial completo.
weight: 11
url: /it/net/workbook-settings/find-maximum-supported-rows-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trova il numero massimo di righe e colonne supportate dai formati XLS e XLSX

## Introduzione
Nel mondo di Excel, gestire grandi set di dati può essere un compito arduo, soprattutto quando si tratta di gestire il numero massimo di righe e colonne supportate da diversi formati di file. Questo tutorial ti guiderà attraverso il processo di ricerca del numero massimo di righe e colonne supportate dai formati XLS e XLSX utilizzando la libreria Aspose.Cells per .NET. Alla fine di questo articolo, avrai una comprensione completa di come utilizzare questo potente strumento per gestire in modo efficiente le tue attività relative a Excel.
## Prerequisiti
Prima di immergerci nel tutorial, assicurati di avere i seguenti prerequisiti:
1. [Quadro .NET](https://dotnet.microsoft.com/en-us/download) O[.NET Core](https://dotnet.microsoft.com/en-us/download) installato sul tuo sistema.
2. [Aspose.Cells per .NET](https://releases.aspose.com/cells/net/) libreria scaricata e a cui si fa riferimento nel progetto.
 Se non lo hai già fatto, puoi scaricare la libreria Aspose.Cells per .NET da[sito web](https://releases.aspose.com/cells/net/) oppure installarlo tramite[NuGet](https://www.nuget.org/packages/Aspose.Cells/).
## Importa pacchetti
Per iniziare, dovrai importare i pacchetti necessari dalla libreria Aspose.Cells per .NET. Aggiungi le seguenti istruzioni using all'inizio del tuo file C#:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Passaggio 1: trovare il numero massimo di righe e colonne supportate dal formato XLS
Cominciamo esplorando il numero massimo di righe e colonne supportate dal formato XLS (Excel 97-2003).
```csharp
// Stampa un messaggio sul formato XLS.
Console.WriteLine("Maximum Rows and Columns supported by XLS format.");
// Crea una cartella di lavoro in formato XLS.
Workbook wb = new Workbook(FileFormatType.Excel97To2003);
// Stampa il numero massimo di righe e colonne supportate dal formato XLS.
int maxRows = wb.Settings.MaxRow + 1;
int maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
Console.WriteLine();
```
In questa fase:
1. Visualizza un messaggio per indicare che stiamo lavorando con il formato XLS.
2.  Crea un nuovo`Workbook` istanza utilizzando il`FileFormatType.Excel97To2003` enum, che rappresenta il formato XLS.
3.  Recupera il numero massimo di righe e colonne supportate dal formato XLS utilizzando`Workbook.Settings.MaxRow` E`Workbook.Settings.MaxColumn`proprietà, rispettivamente. Aggiungiamo 1 a questi valori per ottenere i numeri massimi effettivi di riga e colonna (poiché sono basati su zero).
4. Stampa il numero massimo di righe e colonne sulla console.
## Passaggio 2: trovare il numero massimo di righe e colonne supportate dal formato XLSX
Ora esamineremo il numero massimo di righe e colonne supportate dal formato XLSX (Excel 2007 e versioni successive).
```csharp
// Stampa un messaggio sul formato XLSX.
Console.WriteLine("Maximum Rows and Columns supported by XLSX format.");
// Crea cartella di lavoro in formato XLSX.
wb = new Workbook(FileFormatType.Xlsx);
// Stampa il numero massimo di righe e colonne supportate dal formato XLSX.
maxRows = wb.Settings.MaxRow + 1;
maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
```
In questa fase:
1. Visualizza un messaggio per indicare che stiamo lavorando con il formato XLSX.
2.  Crea un nuovo`Workbook` istanza utilizzando il`FileFormatType.Xlsx` enum, che rappresenta il formato XLSX.
3.  Recupera il numero massimo di righe e colonne supportate dal formato XLSX utilizzando`Workbook.Settings.MaxRow` E`Workbook.Settings.MaxColumn`proprietà, rispettivamente. Aggiungiamo 1 a questi valori per ottenere i numeri massimi effettivi di riga e colonna (poiché sono basati su zero).
4. Stampa il numero massimo di righe e colonne sulla console.
## Passaggio 3: visualizzare un messaggio di successo
Infine, visualizziamo un messaggio di successo per indicare che l'esempio "FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats" è stato eseguito correttamente.
```csharp
Console.WriteLine("FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats executed successfully.");
```
Questo passaggio stampa semplicemente un messaggio di successo sulla console.
## Conclusione
In questo tutorial, hai imparato come usare la libreria Aspose.Cells per .NET per trovare il numero massimo di righe e colonne supportate dai formati di file XLS e XLSX. Comprendendo le limitazioni di questi formati, puoi pianificare e gestire meglio i tuoi progetti basati su Excel, assicurandoti che i tuoi dati rientrino negli intervalli supportati.
## Domande frequenti
### Qual è il numero massimo di righe supportate dal formato XLS?
Il numero massimo di righe supportato dal formato XLS (Excel 97-2003) è 65.536.
### Qual è il numero massimo di colonne supportate dal formato XLS?
Il numero massimo di colonne supportato dal formato XLS (Excel 97-2003) è 256.
### Qual è il numero massimo di righe supportate dal formato XLSX?
Il numero massimo di righe supportato dal formato XLSX (Excel 2007 e versioni successive) è 1.048.576.
### Qual è il numero massimo di colonne supportate dal formato XLSX?
Il numero massimo di colonne supportato dal formato XLSX (Excel 2007 e versioni successive) è 16.384.
### Posso usare la libreria Aspose.Cells per .NET per lavorare con altri formati di file Excel?
 Sì, la libreria Aspose.Cells per .NET supporta un'ampia gamma di formati di file Excel, tra cui XLS, XLSX, ODS e altri. Puoi esplorare[documentazione](https://reference.aspose.com/cells/net/) per conoscere le caratteristiche e le funzionalità disponibili.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
