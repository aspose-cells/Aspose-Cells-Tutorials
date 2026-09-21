---
category: general
date: 2026-03-01
description: Il tutorial Read write Excel C# mostra come leggere il valore di una
  cella Excel e scrivere una data/ora in Excel usando C# e Aspose.Cells in pochi semplici
  passaggi.
draft: false
keywords:
- read write excel c#
- read excel cell value
- write datetime to excel
- c# excel interop
- aspnet excel automation
language: it
og_description: Il tutorial Read write Excel C# spiega come leggere il valore di una
  cella Excel e scrivere una data/ora in Excel con esempi di codice chiari e le migliori
  pratiche.
og_title: Leggi e scrivi Excel C# – Guida passo passo
tags:
- C#
- Excel
- Aspose.Cells
title: Lettura e Scrittura di Excel C# – Guida Completa alla Lettura e Scrittura delle
  Celle Excel
url: /it/net/cell-operations/read-write-excel-c-complete-guide-to-reading-and-writing-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Read Write Excel C# – Guida Completa alla Lettura e Scrittura di Celle Excel

Hai mai provato a **read write Excel C#** e ti sei ritrovato con un'eccezione criptica o una data non corrispondente? Non sei solo. Molti sviluppatori inciampano quando devono estrarre una data dell'era giapponese da un foglio di lavoro e poi memorizzare un corretto `DateTime` nella stessa cella.  

In questa guida vedremo passo passo come **read excel cell value** e **write datetime to excel** usando C# e la potente libreria Aspose.Cells. Alla fine avrai un esempio autonomo e eseguibile che potrai inserire in qualsiasi progetto .NET.

## Cosa Imparerai

- Come installare e referenziare Aspose.Cells in un progetto .NET 6+.
- Il codice esatto necessario per recuperare una cella che contiene una stringa dell'era giapponese come `"R3/5/12"`.
- Come analizzare quella stringa in un `DateTime` usando la cultura `"ja-JP"`.
- I passaggi per inserire il `DateTime` risultante nella stessa cella del foglio di lavoro.
- Suggerimenti per gestire casi limite come celle vuote o formati di era inaspettati.  

Non è necessaria alcuna esperienza pregressa con l'interoperabilità Excel—basta una comprensione di base di C# e .NET. Iniziamo.

![Screenshot dell'operazione read write Excel C# che mostra la cella B2 prima e dopo la conversione](read-write-excel-csharp.png "esempio read write excel c#")

## Passo 1: Configura il Progetto – Fondamenti di Read Write Excel C#

Prima di immergerci nel codice, abbiamo bisogno di una solida base.

1. **Create a new console app** (o qualsiasi progetto .NET) targeting .NET 6 o successivo:

   ```bash
   dotnet new console -n ExcelEraDemo
   cd ExcelEraDemo
   ```

2. **Add the Aspose.Cells NuGet package**. È una libreria completamente gestita che funziona senza interop COM:

   ```bash
   dotnet add package Aspose.Cells
   ```

3. **Copy an Excel file** (`EraDates.xlsx`) nella radice del progetto. Questo workbook dovrebbe contenere un foglio chiamato `"Sheet1"` con la cella **B2** contenente un valore come `"R3/5/12"` (Reiwa 3, maggio 12).

Questo è tutto lo scaffolding di cui hai bisogno. Il resto del tutorial si concentra sulla logica effettiva di **read excel cell value** e **write datetime to excel**.

## Passo 2: Leggi il Valore della Cella Excel con C#

Ora che il progetto è pronto, recuperiamo la stringa dal foglio di lavoro. Il frammento seguente dimostra la catena di chiamate esatta:

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load the workbook (adjust the path as needed)
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // assumes the sheet is named Sheet1

        // Step 2: Get the cell that holds the Japanese era date string
        // B2 contains something like "R3/5/12"
        Cell dateCell = ws.Cells["B2"];  

        // Step 3: Read the string representation from the cell
        string eraDateString = dateCell.StringValue;  

        Console.WriteLine($"Original cell value: {eraDateString}");
        // -------------------------------------------------
        // From here we’ll convert the era string to a DateTime.
        // -------------------------------------------------
    }
}
```

**Perché funziona:** `Cell.StringValue` restituisce sempre il testo visualizzato, indipendentemente dal formato numerico sottostante. Questo garantisce che lavoriamo con la stringa esatta "R3/5/12" che l'utente vede.

### Problemi Comuni

- **Empty cells** – `StringValue` restituisce una stringa vuota. Verifica prima di analizzare.  
- **Unexpected formats** – Se la cella contiene "2023/05/12" il parser dell'era genererà un'eccezione; potresti aver bisogno di un fallback.

## Passo 3: Scrivi DateTime in Excel con C#

Con la stringa dell'era a disposizione, ora la analizziamo usando `DateTime.ParseExact`. Il formato "ggyy/MM/dd" indica a .NET di aspettarsi un'era giapponese (`gg`), un anno a due cifre (`yy`) e i componenti mese/giorno.

```csharp
        // Step 4: Convert the era date string to a DateTime using the Japanese culture
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The cell value does not match the expected Japanese era format.");
            return;
        }

        Console.WriteLine($"Parsed DateTime (UTC): {parsedDate:u}");

        // Step 5: Store the resulting DateTime back into the same cell
        dateCell.PutValue(parsedDate);

        // Optional: Apply a standard date format so Excel shows it nicely
        dateCell.SetStyle(new Style { Number = 14 }); // 14 = "m/d/yyyy"

        // Save the workbook to a new file so we don’t overwrite the original
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Workbook saved as EraDates_Converted.xlsx");
```

**Perché usiamo `PutValue`**: Aspose.Cells rileva automaticamente il tipo .NET e scrive il tipo di cella Excel appropriato. Passare un `DateTime` produce una vera data Excel, che può essere formattata o usata in formule successive.

### Casi Limite e Suggerimenti

- **Time zones** – Gli oggetti `DateTime` sono memorizzati senza informazioni sul fuso. Se ti serve UTC, chiama `DateTime.SpecifyKind`.  
- **Culture fallback** – Se prevedi altre culture, avvolgi il parsing in un helper che provi più oggetti `CultureInfo`.  
- **Performance** – Quando elabori migliaia di righe, riutilizza una singola istanza di `CultureInfo` invece di crearne una nuova ad ogni ciclo.

## Passo 4: Esempio Completo Funzionante – Mettere Tutto Insieme

Di seguito il programma completo, pronto per l'esecuzione. Copialo e incollalo in `Program.cs`, assicurati che `EraDates.xlsx` sia accanto al binario compilato, ed esegui `dotnet run`.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load workbook
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // Change if your sheet has a different name

        // -------------------------------------------------
        // 1️⃣ Read the Japanese era string from B2
        // -------------------------------------------------
        Cell dateCell = ws.Cells["B2"];
        string eraDateString = dateCell.StringValue?.Trim();

        if (string.IsNullOrEmpty(eraDateString))
        {
            Console.WriteLine("Cell B2 is empty. Nothing to convert.");
            return;
        }

        Console.WriteLine($"Original cell value: {eraDateString}");

        // -------------------------------------------------
        // 2️⃣ Parse the era string into a DateTime
        // -------------------------------------------------
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The value does not match the expected Japanese era format (ggyy/MM/dd).");
            return;
        }

        Console.WriteLine($"Parsed DateTime: {parsedDate:u}");

        // -------------------------------------------------
        // 3️⃣ Write the DateTime back into the same cell
        // -------------------------------------------------
        dateCell.PutValue(parsedDate);

        // Apply a friendly date format (e.g., 2023/05/12)
        Style style = wb.CreateStyle();
        style.Number = 14; // Built‑in date format
        dateCell.SetStyle(style);

        // Save the updated workbook
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Conversion complete – saved as EraDates_Converted.xlsx");
    }
}
```

**Output previsto**

```
Original cell value: R3/5/12
Parsed DateTime: 2021-05-12 00:00:00Z
Conversion complete – saved as EraDates_Converted.xlsx
```

Quando apri `EraDates_Converted.xlsx`, la cella **B2** ora mostra una data regolare (ad esempio `5/12/2021`) e può essere usata nei calcoli di Excel come qualsiasi altra data.

## Consigli Pro per Codice Read Write Excel C# Robusto

- **Validate before you write** – Usa `Cell.IsFormula` o `Cell.Type` per evitare di sovrascrivere formule involontariamente.  
- **Batch processing** – Se devi convertire un'intera colonna, itera su `ws.Cells.Columns[1]` (colonna B) e applica la stessa logica.  
- **Thread safety** – Gli oggetti Aspose.Cells non sono thread‑safe; crea istanze separate di `Workbook` per **thread** quando parallelizzi.  
- **Logging** – Per script di **produzione**, sostituisci `Console.WriteLine` con un logger appropriato (ad es., **Serilog**) per catturare i fallimenti di **parse**.  
- **Testing** – Scrivi test unitari che forniscano stringhe di era note a un metodo helper e verifichino i valori `DateTime` risultanti.

## Conclusione

Hai appena padroneggiato **read write Excel C#** imparando a **read excel cell value**, analizzare una stringa dell'era giapponese e **write datetime to excel** con sicurezza. L'esempio completo dimostra un flusso di lavoro pulito, end‑to‑end, che puoi adattare a operazioni di massa, culture diverse o persino a pipeline Excel‑to‑database.

Qual è il prossimo passo? Prova a estendere lo script per elaborare un'intera colonna di date dell'era, o esplora le ricche opzioni di formattazione di Aspose.Cells per stilizzare le celle di output. Potresti anche sperimentare con altre librerie come EPPlus o ClosedXML—la maggior parte della logica rimane la stessa, solo le chiamate API differiscono.

Hai domande o uno scenario Excel complesso? Lascia un commento qui sotto, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}