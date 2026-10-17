---
category: general
date: 2026-05-04
description: Esporta l'intervallo del foglio di lavoro usando C# con formattazione
  personalizzata. Scopri come esportare un intervallo Excel e come personalizzare
  l'esportazione delle celle in pochi semplici passaggi.
draft: false
keywords:
- export worksheet range
- how to export excel range
- how to customize cell export
- C# Excel export
- worksheet export options
language: it
og_description: Esporta l'intervallo del foglio di lavoro con C#. Questa guida mostra
  come esportare un intervallo Excel e personalizzare l'esportazione delle celle in
  modo rapido e affidabile.
og_title: Esporta l'intervallo di foglio di lavoro in C# – Guida completa alla programmazione
tags:
- C#
- Excel
- Data Export
title: Esporta l’intervallo del foglio di lavoro in C# – Guida completa alla programmazione
url: /it/net/excel-data-export-retrieval/export-worksheet-range-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esporta intervallo di foglio di lavoro in C# – Guida completa di programmazione

Hai mai avuto bisogno di **export worksheet range** ma l'output predefinito non era quello che desideravi? Non sei l'unico—molti sviluppatori incontrano lo stesso ostacolo quando cercano di estrarre un blocco di celle in un file CSV o JSON. La buona notizia? Con poche righe di C# puoi non solo **export excel range** ma anche **customize cell export** per adattarlo a qualsiasi formato successivo.

In questo tutorial percorreremo uno scenario reale: prendere le celle *A1:D10* da una cartella di lavoro Excel, trasformare ogni valore in una stringa tra parentesi quadre e scrivere il risultato in un file. Alla fine saprai esattamente **how to export worksheet range** con pieno controllo sulla rappresentazione di ogni cella, oltre a una serie di consigli per i casi limite che potresti incontrare in seguito.

## Di cosa avrai bisogno

- .NET 6 o versioni successive (il codice funziona anche con .NET Framework 4.7+)  
- Il pacchetto NuGet **GemBox.Spreadsheet** (o qualsiasi libreria che offra `ExportTableOptions`; l'API mostrata è di GemBox)  
- Una comprensione di base della sintassi C# – niente di complicato, solo le consuete istruzioni `using` e la creazione di oggetti  

Se li hai, sei pronto per immergerti.

## Passo 1: Configura le opzioni di esportazione – Punto di controllo principale  

La prima cosa da fare è creare un'istanza di `ExportTableOptions` e indicare di trattare ogni cella come una stringa. Questa è la base per **how to export excel range** mantenendo coerente il tipo di dato.

```csharp
using GemBox.Spreadsheet;

public class WorksheetExporter
{
    public void ExportRange(string sourcePath, string destinationPath)
    {
        // Load the workbook.
        var workbook = ExcelFile.Load(sourcePath);
        var worksheet = workbook.Worksheets[0]; // assume first sheet

        // Step 1: Create export options and enable string export.
        var exportOptions = new ExportTableOptions
        {
            ExportAsString = true // forces every cell to be exported as text
        };
```

*Perché forzare l'esportazione come stringa?*  
Quando in seguito personalizzi ogni cella, inserirai parentesi e possibilmente altri simboli. Mantenere tutto come stringa evita sorprese di conversione di tipo (ad esempio, date che diventano numeri seriali).

## Passo 2: Collegati all'evento CellExport – Personalizzare ogni cella  

Ora arriva la parte divertente: **how to customize cell export**. GemBox genera un evento `CellExport` per ogni cella che sta per essere scritta. Gestendolo puoi avvolgere il valore tra parentesi, aggiungere un prefisso o addirittura saltare completamente una cella.

```csharp
        // Step 2: Customize each cell's exported value.
        exportOptions.CellExport += (sender, e) =>
        {
            // e.Value holds the original cell content.
            // We'll wrap it in square brackets.
            e.Value = $"[{e.Value}]";
        };
```

*Consiglio professionale:* Se vuoi modificare solo le celle numeriche, controlla `e.Value.GetType()` prima di applicare le parentesi. Questa piccola verifica può salvarti dal corrompere involontariamente il testo dell'intestazione.

## Passo 3: Esporta l'intervallo desiderato – L'azione principale  

Con le opzioni pronte, chiami `ExportTable`. Il metodo prende la cartella di lavoro caricata, l'indirizzo dell'intervallo desiderato e le opzioni appena configurate.

```csharp
        // Step 3: Export the range A1:D10 using the configured options.
        worksheet.ExportTable(workbook, "A1:D10", exportOptions, destinationPath);
    }
}
```

Il sovraccarico che abbiamo usato scrive direttamente su un file (CSV per impostazione predefinita). Se preferisci una stringa in memoria, sostituisci l'ultimo argomento con un `StringWriter` e leggi il risultato successivamente.

### Esempio completo funzionante

Di seguito trovi un'app console autonoma che puoi incollare in un nuovo progetto ed eseguire immediatamente (basta sostituire i percorsi dei file).

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License key (free version works with limited rows/columns).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        var exporter = new WorksheetExporter();
        exporter.ExportRange(
            sourcePath: @"C:\Temp\Sample.xlsx",
            destinationPath: @"C:\Temp\ExportedRange.csv");

        Console.WriteLine("Export completed. Check C:\\Temp\\ExportedRange.csv");
    }
}
```

**Output previsto (snippet CSV):**

```
[Header1],[Header2],[Header3],[Header4]
[123],[456],[789],[012]
[ABC],[DEF],[GHI],[JKL]
...
```

Ogni cella da *A1* a *D10* è ora avvolta tra parentesi quadre, esattamente come abbiamo definito nel gestore `CellExport`.

## Gestione dei casi limite comuni  

### 1. Celle vuote  

Se una cella è vuota, `e.Value` sarà `null`. Tentare di formattarla con l'interpolazione di stringa genera un'eccezione. Proteggiti da questo:

```csharp
exportOptions.CellExport += (s, e) =>
{
    var raw = e.Value?.ToString() ?? string.Empty;
    e.Value = $"[{raw}]";
};
```

### 2. Intervalli di grandi dimensioni  

Esportare milioni di righe può superare i limiti di memoria. In questo caso, trasmetti l'output invece di caricare l'intera cartella di lavoro in memoria:

```csharp
using (var writer = new StreamWriter(destinationPath))
{
    worksheet.ExportTable(workbook, "A1:D1000000", exportOptions, writer);
}
```

### 3. Delimitatori diversi  

CSV non è l'unico formato di cui potresti aver bisogno. Cambia il delimitatore modificando `ExportTableOptions.CsvSeparator`:

```csharp
exportOptions.CsvSeparator = '\t'; // Tab‑delimited
```

## Domande frequenti  

**D: Questo funziona con file .xlsx creati da Excel 365?**  
Assolutamente. GemBox legge il moderno formato OpenXML senza configurazioni aggiuntive.

**D: Posso esportare più intervalli non contigui contemporaneamente?**  
Non direttamente con una singola chiamata `ExportTable`. Esegui un ciclo su ogni stringa di intervallo (`"A1:D10"`, `"F1:H5"` ecc.) e concatena i risultati manualmente.

**D: E se devo applicare formattazioni diverse per colonna?**  
All'interno del gestore `CellExport` hai accesso a `e.ColumnIndex`. Usa una dichiarazione `switch` per applicare una logica specifica per colonna.

## Conclusione  

Abbiamo coperto **how to export worksheet range** con pieno controllo sull'aspetto di ogni cella, dimostrato **how to export excel range** usando `ExportTableOptions`, e mostrato **how to customize cell export** tramite l'evento `CellExport`. La soluzione completa è contenuta in poche decine di righe di C#, ma è sufficientemente flessibile per scenari di livello produttivo.

Prossimi passi? Prova a sostituire il wrapper a parentesi con un formato compatibile JSON, o sperimenta una logica condizionale che salta le righe nascoste. Potresti anche esplorare l'esportazione diretta in un `MemoryStream` per risposte di web‑API—senza file temporanei.

Se hai seguito il tutorial, ora disponi di un modello solido e riutilizzabile per esportare qualsiasi intervallo di foglio di lavoro esattamente come ti serve. Buon coding, e sentiti libero di lasciare un commento se incontri difficoltà!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}