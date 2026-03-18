---
category: general
date: 2026-03-18
description: Estrai la data da Excel e restituisci la data nel formato ISO yyyy‑mm‑dd.
  Scopri come leggere le date dell'era giapponese, convertirle e visualizzare le date
  ISO in C#.
draft: false
keywords:
- extract date from excel
- output date yyyy-mm-dd
- display date iso format
language: it
og_description: Estrai la data da Excel e restituisci la data nel formato ISO yyyy‑mm‑dd.
  Tutorial passo‑passo in C# con codice completo e spiegazioni.
og_title: Estrai data da Excel – Output data yyyy‑mm‑dd in C#
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Estrai la data da Excel e visualizza la data yyyy‑mm‑dd – Guida completa a
  C#
url: /it/net/data-loading-and-parsing/extract-date-from-excel-and-output-date-yyyy-mm-dd-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai data da Excel – Come ottenere la data yyyy‑mm‑dd in formato ISO

Hai mai avuto bisogno di **estrarre data da Excel** ma non sapevi come gestire le date dell'era giapponese o ottenere una stringa pulita `yyyy‑mm‑dd`? Non sei solo. In molti progetti di migrazione dati il workbook di origine memorizza le date usando il calendario dell'Imperatore giapponese, e il sistema a valle si aspetta una data conforme a ISO come `2024-04-01`.  

In questa guida percorreremo una soluzione completa e eseguibile che legge una cella, interpreta l'era giapponese e **genera la data yyyy‑mm‑dd**. Alla fine saprai esattamente come **visualizzare la data in formato ISO** in qualsiasi app .NET, e avrai uno snippet di codice riutilizzabile da inserire nel tuo progetto.

## Cosa ti serve

- **.NET 6+** (o .NET Framework 4.7.2+).  
- **Aspose.Cells for .NET** – la libreria che ci permette di impostare un calendario personalizzato durante il caricamento di un workbook.  
- Un file Excel (`japan-date.xlsx`) che contiene una data memorizzata in una cella con era giapponese (ad es. `令和3年4月1日`).  
- Un IDE preferito – Visual Studio, Rider, o anche VS Code vanno bene.

Non sono richiesti pacchetti NuGet aggiuntivi oltre a Aspose.Cells, e il codice funziona su Windows, Linux o macOS.

## Passo 1: Configura il progetto e installa Aspose.Cells

```bash
dotnet new console -n ExcelDateDemo
cd ExcelDateDemo
dotnet add package Aspose.Cells
```

> **Suggerimento:** Se sei su un server CI, fissa la versione del pacchetto (`Aspose.Cells 23.12`) per garantire build riproducibili.

## Passo 2: Carica il workbook con il calendario dell'Imperatore giapponese

La chiave per **estrarre data da Excel** quando la sorgente usa un calendario non gregoriano è indicare ad Aspose.Cells quale calendario applicare durante il caricamento. Lo facciamo con `LoadOptions.Calendar`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create load options and set the Japanese Emperor calendar
        LoadOptions loadOptions = new LoadOptions
        {
            // This tells Aspose.Cells to interpret era dates correctly
            Calendar = new JapaneseEmperorCalendar()
        };

        // Step 3: Open the workbook that contains Japanese era dates
        // Replace the path with the actual location of your Excel file
        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);
```

**Perché è importante:** Senza il calendario personalizzato, Aspose.Cells tratterebbe la cella come una semplice stringa e perderesti l'informazione sull'era. Assegnando `JapaneseEmperorCalendar`, la libreria converte automaticamente `令和3年4月1日` in `2021‑04‑01` dietro le quinte.

## Passo 3: Recupera la data da una cella specifica

Ora che il workbook sa come interpretare l'era, possiamo leggere la cella come un `DateTime`. Supponiamo che la data sia nella prima scheda, cella **A1** (riga 0, colonna 0).

```csharp
        // Step 4: Retrieve the date value from the first worksheet, first cell
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0]; // A1

        // GetDateTime() returns a System.DateTime object
        DateTime extractedDate = dateCell.GetDateTime();
```

Se la cella è vuota o contiene un valore non data, `GetDateTime()` lancerà un'eccezione. Un approccio difensivo appare così:

```csharp
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        DateTime extractedDate = dateCell.GetDateTime();
```

**Caso limite:** Alcuni file Excel più vecchi memorizzano le date come numeri (date seriali). Aspose.Cells le gestisce automaticamente, ma dovresti comunque verificare il tipo di cella se ti aspetti contenuti misti.

## Passo 4: Genera la data yyyy‑mm‑dd (ISO) e verifica

Con il `DateTime` a disposizione, formattarlo come **output date yyyy‑mm‑dd** è una singola riga:

```csharp
        // Step 5: Output the date in ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

Eseguendo il programma su un file che contiene `令和3年4月1日` verrà stampato:

```
Extracted date (ISO): 2021-04-01
```

Questo è l'esatto **display date iso format** richiesto da molte API.

## Esempio completo funzionante

Mettendo insieme tutti i pezzi, ecco il programma completo, pronto per il copia‑incolla:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook with Japanese era support
        LoadOptions loadOptions = new LoadOptions
        {
            Calendar = new JapaneseEmperorCalendar()
        };

        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);

        // Access the cell that holds the date (A1)
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0];

        // Validate the cell contains a date
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        // Extract the DateTime value
        DateTime extractedDate = dateCell.GetDateTime();

        // Convert to ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

> **Nota:** Sostituisci `YOUR_DIRECTORY` con la cartella reale che contiene `japan-date.xlsx`. Il codice funziona con qualsiasi foglio e qualsiasi cella – basta regolare gli indici.

## Gestione di altri calendari (Opzionale)

Se mai dovessi **estrarre data da Excel** che utilizza il calendario buddista tailandese o quello ebraico, basta sostituire l'istanza del calendario:

```csharp
loadOptions.Calendar = new ThaiBuddhistCalendar();   // for Thai dates
// or
loadOptions.Calendar = new HebrewCalendar();         // for Hebrew dates
```

Il resto della logica rimane invariato, il che dimostra la flessibilità dell'approccio.

## Problemi comuni e come evitarli

| Problema | Perché succede | Soluzione |
|----------|----------------|-----------|
| `GetDateTime()` lancia `InvalidCastException` | La cella non è una data (potrebbe essere una stringa) | Verifica `Cell.Type` prima di chiamare, oppure usa `DateTime.TryParse` su `Cell.StringValue`. |
| Anno errato dopo la conversione | Workbook caricato senza impostare `Calendar` | Crea sempre `LoadOptions` con il calendario appropriato **prima** di aprire il file. |
| L'output ISO mostra la parte temporale (`2021-04-01 00:00:00`) | Usato `ToString()` senza specificare un formato | Usa lo specificatore di formato `"yyyy-MM-dd"` per forzare **output date yyyy‑mm‑dd**. |
| File non trovato | Il percorso relativo punta alla cartella sbagliata | Usa `Path.Combine(Environment.CurrentDirectory, "japan-date.xlsx")` o fornisci un percorso assoluto. |

## Suggerimenti professionali per codice pronto alla produzione

1. **Cache il workbook** se devi leggere molte date dallo stesso file – aprire un workbook è relativamente costoso.  
2. **Avvolgi la logica di estrazione** in un metodo riutilizzabile:

   ```csharp
   static string ExtractIsoDate(string file, int sheetIdx, int row, int col)
   {
       var opts = new LoadOptions { Calendar = new JapaneseEmperorCalendar() };
       var wb = new Workbook(file, opts);
       var cell = wb.Worksheets[sheetIdx].Cells[row, col];
       if (cell.Type != CellValueType.IsDateTime) return null;
       return cell.GetDateTime().ToString("yyyy-MM-dd");
   }
   ```

3. **Registra la stringa originale dell'era** (`cell.StringValue`) insieme all'output ISO per tracciamenti di audit.  
4. **Test unitari** del metodo con alcuni file Excel hard‑coded che coprono diverse ere (Heisei, Reiwa) per garantire la correttezza.

## Panoramica visiva

Di seguito è riportato un diagramma rapido che illustra il flusso dei dati — dalla cella Excel alla stringa ISO.  

![Esempio di estrazione data da Excel che mostra Excel → LoadOptions → DateTime → stringa ISO]  

## Conclusione

Abbiamo coperto tutto ciò di cui hai bisogno per **estrarre data da Excel**, gestire i valori dell'era giapponese e **generare la data yyyy‑mm‑dd** in modo che sia conforme al **display date iso format** che le API moderne apprezzano. La soluzione è autonoma, funziona con qualsiasi versione .NET che supporta Aspose.Cells, e può essere estesa ad altri calendari con una singola riga di modifica.

Hai in mente un calendario diverso? O forse stai estraendo date da più colonne? Sentiti libero di modificare l'helper `ExtractIsoDate` o lasciare un commento qui sotto. Buona programmazione, e che le tue date rimangano sempre perfettamente sincronizzate in ISO!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}