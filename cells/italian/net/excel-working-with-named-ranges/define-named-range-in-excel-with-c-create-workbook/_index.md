---
category: general
date: 2026-08-07
description: Definisci un intervallo denominato in Excel con C# e impara come aggiungere
  una tabella a un foglio di lavoro, quindi salva la cartella di lavoro su file in
  modo programmatico.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define named range excel
- save workbook to file
- add named range excel
- add table to worksheet
- create excel workbook programmatically
language: it
lastmod: 2026-08-07
og_description: Definisci un intervallo denominato in Excel con C# e scopri come aggiungere
  una tabella, creare una cartella di lavoro programmaticamente e salvare la cartella
  di lavoro su file in un unico flusso.
og_image_alt: Screenshot of C# code that creates an Excel workbook, adds a table,
  defines a named range, and saves the file
og_title: Definisci un intervallo con nome in Excel con C# – tutorial completo della
  cartella di lavoro
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Define named range in Excel with C# and learn how to add a table to
    a worksheet, then save workbook to file programmatically.
  headline: Define named range in Excel with C# – create workbook
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- named range
- programmatic Excel
title: Definisci un intervallo denominato in Excel con C# – crea una cartella di lavoro
url: /it/net/excel-working-with-named-ranges/define-named-range-in-excel-with-c-create-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definire un intervallo denominato in Excel con C# – creare cartella di lavoro

Se hai bisogno di **definire un intervallo denominato in Excel** dal codice C#, questo tutorial ti mostra esattamente come farlo. Vedrai anche come **aggiungere una tabella a un foglio di lavoro**, creare la cartella di lavoro **programmaticamente** e infine **salvare la cartella di lavoro su file** senza uscire dall'IDE.

Lavorare con i file Excel in modo programmatico fa risparmiare tempo, elimina errori manuali e consente pipeline di reporting automatizzate. In questa guida tu:

* Creare una nuova cartella di lavoro Excel da zero.  
* Aggiungere una tabella che copre un intervallo di celle specifico.  
* Definire un intervallo denominato e gestire i conflitti di denominazione.  
* Persistire la cartella di lavoro su disco.

Tutti i passaggi utilizzano la libreria **Aspose.Cells for .NET**, che funziona con .NET 6+ e .NET Framework 4.6+. Non è necessario alcun interop COM aggiuntivo o installazione di Office.

## Prerequisiti

* .NET 6 SDK (o .NET Framework 4.6+).  
* Visual Studio 2022 o qualsiasi IDE compatibile con C#.  
* Pacchetto NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`).  

> **Suggerimento professionale:** Usa la licenza di valutazione gratuita durante i test; sostituiscila con una licenza di produzione prima del deployment.

## Passo 1: Creare una cartella di lavoro Excel programmaticamente

La prima operazione è istanziare un oggetto `Workbook`. Questo oggetto rappresenta l'intero file Excel in memoria.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook in memory
        Workbook workbook = new Workbook();               // create an empty workbook
        Worksheet worksheet = workbook.Worksheets[0];    // get the first (default) worksheet
```

*Perché è importante*: Creare la cartella di lavoro in codice ti dà il pieno controllo su fogli, stili e dati prima che qualsiasi file tocchi il disco.

## Passo 2: Aggiungere una tabella al foglio di lavoro

Una tabella (nota anche come ListObject) fornisce filtraggio, ordinamento e formattazione integrati. Qui creiamo una tabella che copre le celle **A1:B5** e le diamo il nome **SalesData**.

```csharp
        // Step 2: Define a range and convert it into a table
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Populate the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");
        worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");
        worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries");
        worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");
        worksheet.Cells["B5"].PutValue(30);
```

*Perché è importante*: Aggiungere una tabella in anticipo ti consente di fare riferimento ai dati in seguito con un **intervallo denominato**, e il riferimento strutturato della tabella può essere usato nelle formule.

## Passo 3: Definire un intervallo denominato in Excel – gestire i conflitti

Un **intervallo denominato** è un identificatore che punta a una cella o a un intervallo, rendendo le formule più facili da leggere. Se un nome esiste già (ad esempio, il nome della tabella **SalesData**), Excel genera un conflitto. Il codice qui sotto dimostra come intercettare quell'eccezione e continuare in modo sicuro.

```csharp
        // Step 3: Attempt to define a named range with the same identifier as the table
        try
        {
            // This will raise an exception because "SalesData" is already used by the table
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Step 4: Add a different named range – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";
```

*Perché è importante*: Gestire le collisioni di nomi previene crash a runtime nei lavori automatizzati. Il secondo intervallo denominato **SalesTotal** dimostra il riferimento alla colonna della tabella in una formula.

## Passo 4: Salvare la cartella di lavoro su file

Dopo tutte le modifiche, persisti la cartella di lavoro su disco. Il metodo `Save` supporta molti formati; qui usiamo il predefinito `.xlsx`.

```csharp
        // Step 5: Save the workbook to the file system
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

*Perché è importante*: Usare **save workbook to file** programmaticamente consente l'elaborazione batch, la generazione programmata di report e l'integrazione con API web.

## Codice sorgente completo in un'unica visualizzazione

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Add a table covering A1:B5 and name it "SalesData"
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Fill the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");   worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");  worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries"); worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");    worksheet.Cells["B5"].PutValue(30);

        // Try to create a defined name with the same identifier – handle the conflict
        try
        {
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Add a different defined name – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";

        // Save the workbook
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

### Risultato atteso

* Un file Excel chiamato **NameConflictHandled.xlsx** appare in `C:\Temp`.  
* Il Foglio 1 contiene una tabella formattata **SalesData** con righe prodotto‑unità.  
* La cella **B6** mostra la somma della colonna **Units**, calcolata tramite l'intervallo denominato **SalesTotal**.  
* La console stampa un messaggio sul conflitto di nome (se presente) e conferma la posizione del file.

## Domande comuni e casi limite

| Question | Answer |
|----------|--------|
| **Posso definire un intervallo denominato che si estende su più fogli di lavoro?** | Sì. Usa `worksheet.Names.Add("GlobalRange", "'Sheet1'!A1:B5")` e fai riferimento da qualsiasi foglio. |
| **Cosa succede se devo sovrascrivere un file esistente?** | Chiama `workbook.Save(path, SaveFormat.Xlsx, new SaveOptions { Overwrite = true })`. |
| **Come aggiungere un intervallo denominato senza conflitto quando il nome esiste già?** | Usa `worksheet.Names.Remove("ExistingName")` prima di aggiungere il nuovo, oppure genera un identificatore unico (ad esempio, `Guid.NewGuid().ToString("N")`). |
| **È possibile applicare automaticamente uno stile alla tabella?** | Imposta `table.Style = workbook.Styles[BuiltInStyleId.TableStyleMedium9];` dopo aver creato la tabella. |
| **Funziona su .NET Core?** | Aspose.Cells supporta .NET Core, .NET 5/6/7 e .NET Framework. Basta referenziare lo stesso pacchetto NuGet. |

## Conclusione

Ora sai come **definire un intervallo denominato in Excel** usando C#, **aggiungere una tabella a un foglio di lavoro** e **salvare la cartella di lavoro su file** programmaticamente. L'esempio completo dimostra come creare una cartella di lavoro Excel da zero, gestire i conflitti di denominazione e generare un file di report utilizzabile in un unico flusso ripetibile.

Successivamente, esplora argomenti correlati come **aggiungere grafici a un foglio di lavoro**, **esportare in PDF** o **leggere cartelle di lavoro esistenti**. Ognuno di questi si basa sugli stessi fondamenti trattati qui, così sarai pronto a estendere la soluzione a scenari di automazione più complessi. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Create Named Range of Cells in Excel](/cells/english/net/excel-creating-formatting-named-ranges/create-named-range-of-cells/)
- [How to Implement Named Range Formulas in .NET using Aspose.Cells for Excel Automation](/cells/english/net/formulas-functions/implement-named-range-formulas-net-aspose-cells/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}