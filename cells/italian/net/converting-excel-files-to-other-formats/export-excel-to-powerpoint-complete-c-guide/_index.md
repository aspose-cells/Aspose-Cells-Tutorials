---
category: general
date: 2026-03-22
description: Scopri come esportare Excel in PowerPoint, impostare l'area di stampa
  in Excel e salvare Excel come PPTX con grafici modificabili e oggetti OLE in pochi
  passaggi.
draft: false
keywords:
- export excel to powerpoint
- set print area excel
- save excel as pptx
- editable charts PowerPoint
- OLE objects export
language: it
og_description: Esporta Excel in PowerPoint rapidamente. Questo tutorial mostra come
  impostare l'area di stampa di Excel e salvare Excel come PPTX con grafici modificabili
  e oggetti OLE.
og_title: Esporta Excel in PowerPoint – Guida completa C#
tags:
- Aspose.Cells
- C#
- Office Automation
title: Esporta Excel in PowerPoint – Guida completa C#
url: /it/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esporta Excel in PowerPoint – Guida Completa C#

Hai bisogno di **esportare Excel in PowerPoint**? Sei nel posto giusto. Che tu stia creando una presentazione settimanale delle vendite o automatizzando una pipeline di report, trasformare un foglio di lavoro Excel in una presentazione PowerPoint può farti risparmiare ore di lavoro di copia‑incolla.  

In questo tutorial seguirai un esempio pratico che non solo **esporta excel in powerpoint**, ma mostra anche come **impostare l'area di stampa in Excel** e **salvare excel come pptx** così le diapositive risultanti mantengono i grafici e gli oggetti OLE completamente modificabili. Alla fine avrai un programma C# pronto all'uso che produce un file `.pptx` dall'aspetto professionale senza alcuna manipolazione manuale.

## Di cosa avrai bisogno

- **.NET 6+** (qualsiasi runtime .NET recente funziona; il codice utilizza la sintassi C# 10)
- **Aspose.Cells for .NET** – la libreria che gestisce l'esportazione. Puoi ottenerla da NuGet (`Install-Package Aspose.Cells`).
- Una cartella di lavoro Excel che contiene almeno un grafico e/o un oggetto OLE (il file di esempio `ChartAndOle.xlsx` è usato nel codice).
- Un IDE preferito (Visual Studio, Rider o VS Code – quello che preferisci).

È tutto. Nessun interop COM, nessuna installazione di Office necessaria.  

> **Perché usare una libreria?**  
> L'Interop Office integrato è fragile, richiede Office sul server e spesso produce immagini rasterizzate quando si desiderano forme vettoriali e modificabili. Aspose.Cells gestisce il lavoro pesante e mantiene tutto modificabile in PowerPoint.

## Passo 1: Carica la cartella di lavoro Excel  

Per prima cosa carichiamo il file sorgente in memoria. La classe `Workbook` astrae l'intero file Excel, fornendoci l'accesso a fogli di lavoro, grafici e oggetti OLE.

```csharp
using Aspose.Cells;

try
{
    // Load the Excel file that contains the chart and OLE object.
    // Adjust the path to point to your own workbook.
    Workbook workbook = new Workbook(@"C:\MyProjects\ChartAndOle.xlsx");
}
catch (Exception ex)
{
    Console.WriteLine($"Failed to load workbook: {ex.Message}");
    return;
}
```

**Perché è importante:** Caricare la cartella di lavoro è la base. Se il percorso è errato o il file è corrotto, il resto della pipeline non verrà mai eseguito. Il blocco `try…catch` fornisce un errore amichevole invece di un arresto anomalo.

## Passo 2: Imposta l'area di stampa in Excel  

Prima di esportare, di solito vuoi limitare l'output a un intervallo specifico. È qui che entra in gioco **set print area excel**. Definendo un'area di stampa, indichi ad Aspose.Cells esattamente quali celle (e gli oggetti associati) devono apparire nella diapositiva.

```csharp
// Assuming we want to export only the range A1:H30 on the first worksheet.
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:H30";
```

> **Consiglio professionale:** Se hai più fogli di lavoro, ripeti l'assegnazione `PrintArea` per ciascuno che intendi esportare. Lasciare l'area di stampa non impostata esporterà l'intero foglio, il che può gonfiare il file PowerPoint.

## Passo 3: Configura le opzioni di esportazione – Mantieni grafici e OLE modificabili  

Aspose.Cells offre un ricco oggetto `ImageOrPrintOptions`. Attivando `ExportChartObjects` e `ExportOleObjects` preserviamo la natura vettoriale dei grafici e la modificabilità in tempo reale degli oggetti OLE (come documenti Word o PDF incorporati).

```csharp
ImageOrPrintOptions pptExportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,   // We want a PPTX, not a PNG or PDF.
    ExportChartObjects = true,      // Charts stay editable in PowerPoint.
    ExportOleObjects = true         // OLE objects remain live (you can double‑click to edit).
};
```

**Cosa succede dietro le quinte?**  
Quando `ExportChartObjects` è `true`, Aspose converte il grafico in una forma grafico nativa di PowerPoint, preservando serie, assi e formattazione. Con `ExportOleObjects` abilitato, gli oggetti incorporati vengono inseriti come frame OLE, così un doppio clic in PowerPoint apre l'applicazione originale (Word, Excel, ecc.) per la modifica.

## Passo 4: Salva il foglio di lavoro come file PowerPoint modificabile  

Ora uniamo tutto. Il metodo `Save` scrive il file `.pptx` usando le opzioni configurate. Il risultato è una presentazione in cui ogni foglio di lavoro diventa una diapositiva (o una serie di diapositive se l'area di stampa copre più pagine).

```csharp
// Save the first worksheet as an editable PowerPoint presentation.
workbook.Save(@"C:\MyProjects\EditableChartOle.pptx", pptExportOptions);
Console.WriteLine("Export completed! Check EditableChartOle.pptx.");
```

### Risultato atteso

- **Posizione del file:** `C:\MyProjects\EditableChartOle.pptx`
- **Contenuto:**  
  - Una diapositiva che mostra l'intervallo `A1:H30` esattamente come appare in Excel.  
  - Tutti i grafici sono oggetti grafico PowerPoint—clicca su una barra e modifica i dati.  
  - Gli oggetti OLE (ad esempio, un documento Word incorporato) possono essere aperti e modificati direttamente dalla diapositiva.

Se apri il PPTX in PowerPoint, dovresti vedere una diapositiva pulita con componenti completamente modificabili—nessuno screenshot rasterizzato.

## Casi limite e variazioni  

### Più fogli di lavoro → Più diapositive  
Se vuoi che ogni foglio di lavoro diventi una propria diapositiva, basta iterare su `workbook.Worksheets` e chiamare `Save` con un `SheetToImageOptions` che punta a un indice di foglio specifico. Aspose genererà automaticamente una nuova diapositiva per ogni iterazione.

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    ImageOrPrintOptions opts = new ImageOrPrintOptions
    {
        SaveFormat = SaveFormat.Pptx,
        ExportChartObjects = true,
        ExportOleObjects = true,
        OnePagePerSheet = true   // Ensures each sheet starts on a new slide.
    };
    workbook.Save($"Sheet{i + 1}.pptx", opts);
}
```

### Intervalli grandi e prestazioni  
Esportare un'area di stampa enorme (ad es., `A1:Z1000`) può aumentare l'uso della memoria. Per mitigare, considera:
- Suddividere l'intervallo in blocchi più piccoli ed esportarli come diapositive separate.  
- Usare `WorkbookSettings` per aumentare il `MemorySetting` se incontri `OutOfMemoryException`.

### Problemi di compatibilità  
Il PPTX generato funziona con PowerPoint 2016 e versioni successive. Le versioni più vecchie possono comunque aprire il file ma potrebbero perdere alcune funzionalità avanzate dei grafici. Testa sempre sulla versione di Office di destinazione se distribuisci la presentazione su larga scala.

## Esempio completo funzionante (pronto per copia‑incolla)

```csharp
// ---------------------------------------------------------------
// Export Excel to PowerPoint – Complete C# Example
// ---------------------------------------------------------------

using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook.
            string excelPath = @"C:\MyProjects\ChartAndOle.xlsx";
            Workbook workbook;
            try
            {
                workbook = new Workbook(excelPath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error loading Excel file: {ex.Message}");
                return;
            }

            // 2️⃣ Set the print area (set print area excel).
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:H30";

            // 3️⃣ Configure export options – keep charts & OLE objects editable.
            ImageOrPrintOptions pptExportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportChartObjects = true,
                ExportOleObjects = true
            };

            // 4️⃣ Save as PPTX (save excel as pptx).
            string pptxPath = @"C:\MyProjects\EditableChartOle.pptx";
            try
            {
                workbook.Save(pptxPath, pptExportOptions);
                Console.WriteLine($"Success! PPTX created at: {pptxPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Failed to save PPTX: {ex.Message}");
            }
        }
    }
}
```

> **Suggerimento:** Sostituisci i percorsi codificati con valori di configurazione o argomenti da riga di comando per uno strumento più flessibile.

## Domande frequenti  

**D: Posso esportare solo un grafico senza le celle circostanti?**  
R: Sì. Usa solo `ExportChartObjects` e imposta l'area di stampa sull'intervallo che delimita il grafico. Il grafico apparirà centrato nella diapositiva.

**D: E se il mio workbook contiene macro?**  
R: Aspose.Cells ignora le macro VBA durante l'esportazione. Se ti serve la funzionalità macro in PowerPoint, dovrai ricrearla usando VBA di PowerPoint o componenti aggiuntivi.

**D: Funziona su Linux/macOS?**  
R: Assolutamente. Aspose.Cells è una libreria .NET pura; finché hai il runtime .NET, il codice funziona su più piattaforme.

## Conclusione  

Hai appena imparato come **esportare Excel in PowerPoint** impostando con precisione **set print area excel** e **save excel as pptx** con grafici e oggetti OLE completamente modificabili. I passaggi chiave sono caricare la cartella di lavoro, definire l'area di stampa, configurare `ImageOrPrintOptions` e infine salvare il PPTX.  

Da qui puoi esplorare:
- Esportare più fogli di lavoro in un'unica presentazione.  
- Aggiungere titoli di diapositiva o note personalizzate programmaticamente.  
- Convertire il PPTX in PDF per la distribuzione (usa `SaveFormat.Pdf`).  

Prova il codice, modifica l'area di stampa e guarda i tuoi dati Excel apparire magicamente in PowerPoint—senza necessità di copia‑incolla manuale. Se incontri problemi, consulta la documentazione di Aspose.Cells o lascia un commento qui sotto. Buona programmazione!  

![Diagram showing export excel to powerpoint workflow](/images/export-excel-to-powerpoint.png "export excel to powerpoint workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}