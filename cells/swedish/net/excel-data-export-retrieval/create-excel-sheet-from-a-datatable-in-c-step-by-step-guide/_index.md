---
category: general
date: 2026-08-11
description: Skapa ett Excel‑ark från en DataTable i C# och exportera datatabellen
  till Excel med automatisk bladnamngivning. Lär dig hur du lägger till rader i datatabellen
  och sparar arbetsboken som xlsx.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel sheet
- export datatable to excel
- add rows to datatable
- create multiple excel sheets
- save workbook as xlsx
language: sv
lastmod: 2026-08-11
og_description: Skapa ett Excel‑ark från en DataTable i C#. Den här handledningen
  visar hur man exporterar en DataTable till Excel, lägger till rader i DataTable,
  genererar flera Excel‑ark och sparar arbetsboken som xlsx.
og_image_alt: Screenshot of an Excel workbook created from a DataTable with automatically
  renamed sheets
og_title: Skapa Excel‑ark från en DataTable i C# – komplett programmeringsguide
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel sheet from a DataTable in C# and export datatable to excel
    with automatic sheet naming. Learn how to add rows to datatable and save workbook
    as xlsx.
  headline: Create excel sheet from a DataTable in C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Skapa Excel‑ark från en DataTable i C# – steg‑för‑steg‑guide
url: /sv/net/excel-data-export-retrieval/create-excel-sheet-from-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa excel sheet från en DataTable i C# – steg‑för‑steg‑guide

Om du behöver **create excel sheet** från en `DataTable` i C#, visar den här guiden exakt hur du gör det. Du kommer att se hur du **export datatable to excel**, lägger till rader, hanterar duplicerade bladnamn och slutligen **save workbook as xlsx**.

Exemplet använder Aspose.Cells, ett allmänt använt .NET‑bibliotek för Excel‑automatisering. Samma koncept gäller för andra bibliotek som stödjer SmartMarker‑stil bearbetning, men koden nedan fungerar direkt med Aspose.Cells 22.12 eller senare.

## Förutsättningar

* .NET 6.0 SDK eller senare installerat  
* En referens till NuGet‑paketet **Aspose.Cells** (`Install-Package Aspose.Cells`)  
* Grundläggande kunskap om `DataTable` och C#‑konsolapplikationer  

Dessa krav gör att handledningen är självständig och undviker externa verktyg.

## Steg 1: Skapa en DataTable som ska exporteras till Excel

Det första steget är att bygga en `DataTable` som speglar de data du vill ha i kalkylbladet. Här skapar vi en tabell med namnet **Sheet1**, lägger till en `Id`‑kolumn och infogar två rader.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a DataTable named "Sheet1"
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // 2️⃣ Add rows to the DataTable
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);

        // Subsequent steps are called from here
        ProcessAndSaveWorkbook(dataTable);
    }
```

**Varför detta är viktigt:**  
`DataTable` är en bekväm in‑memory‑representation av tabulära data. Att namnge tabellen `"Sheet1"` talar om för Aspose.Cells vilket blad som ska riktas mot när SmartMarkers bearbetas.

## Steg 2: Lägg till rader i DataTable (valfri utökning)

Om dina källdata är dynamiska, kommer du ofta behöva lägga till rader i en loop. Följande kodsnutt demonstrerar ett typiskt mönster:

```csharp
        // Example: add rows from a collection
        int[] ids = { 3, 4, 5 };
        foreach (int id in ids)
        {
            dataTable.Rows.Add(id);
        }
```

**Tips:** När du lägger till många rader, överväg att inaktivera begränsningar (`dataTable.Constraints.Clear()`) för att förbättra prestanda.

## Steg 3: Konfigurera SmartMarker‑alternativ för att automatiskt skapa flera excel‑blad

SmartMarker‑alternativ låter dig styra hur duplicerade bladnamn hanteras. Genom att sätta `DetailSheetNewName` till `"Sheet1_{0}"` instruerar du Aspose.Cells att byta namn på efterföljande blad till `Sheet1_1`, `Sheet1_2` och så vidare.

```csharp
    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // 3️⃣ Set SmartMarker options for automatic sheet renaming
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // New sheets will be named Sheet1_1, Sheet1_2, etc.
            DetailSheetNewName = "Sheet1_{0}"
        };
```

**Varför detta är viktigt:**  
När du bearbetar flera `DataTable`‑objekt som har samma namn, skulle Excel normalt ge ett fel eftersom bladnamn måste vara unika. Mönstret `DetailSheetNewName` eliminerar den konflikten automatiskt.

## Steg 4: Bearbeta SmartMarkers och exportera datatable till excel

Nu skapar vi ett nytt `Workbook`, kör `ProcessSmartMarkers` och låter Aspose.Cells fylla i kalkylbladet/bladen baserat på `DataTable`.

```csharp
        // 4️⃣ Create a workbook and process SmartMarkers
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);
```

**Förklaring:**  
`ProcessSmartMarkers` skannar arbetsboken efter markörer som `&=Sheet1!A1` (ej visat här) och ersätter dem med data från `dataTable`. Eftersom vi började med en tom arbetsbok, skapar Aspose.Cells ett nytt blad som matchar tabellnamnet och fyller det med de rader vi lade till.

## Steg 5: Spara arbetsbok som xlsx

Till sist skriver du arbetsboken till disk med det moderna OpenXML‑formatet (`.xlsx`). Du kan ändra sökvägen så att den passar din miljö.

```csharp
        // 5️⃣ Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Resultat:**  
När programmet körs genereras en Excel‑fil som innehåller:

| Bladnamn | Rader |
|----------|-------|
| Sheet1   | 1, 2, 3, 4, 5 |
| Sheet1_1 | (om en annan DataTable med samma namn bearbetades) |

Logiken för bladnamnbyte säkerställer **create multiple excel sheets** utan manuell namnhantering.

## Vanliga variationer och kantfall

| Situation | Hur man hanterar det |
|-----------|----------------------|
| **Very large tables** (≥ 100 000 rows) | Använd `WorkbookSettings.MemorySetting = MemorySetting.MemoryOptimized` innan bearbetning för att hålla minnesanvändningen låg. |
| **Custom column order** | Omordna `DataColumn`‑objekt i `DataTable` innan du anropar `ProcessSmartMarkers`. |
| **Multiple DataTables with different names** | Anropa `ProcessSmartMarkers` för varje tabell; Aspose.Cells skapar automatiskt ett separat blad för varje namn. |
| **Need a header row with styling** | Efter bearbetning, nå `Worksheet.Cells["A1"]` och tillämpa `Style`‑egenskaper (font, bakgrund). |
| **Saving to a stream instead of a file** | Byt ut `workbook.Save(outputPath, SaveFormat.Xlsx)` mot `workbook.Save(stream, SaveFormat.Xlsx)`. |

**Pro tip:** Omslut alltid filsystemoperationer i `try…catch`‑block för att tidigt avslöja behörighetsproblem.

## Fullständig källkod (klar att kopiera)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create the DataTable that will be exported
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // Add rows – you can replace this with your own data source
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);
        int[] extraIds = { 3, 4, 5 };
        foreach (int id in extraIds)
        {
            dataTable.Rows.Add(id);
        }

        // Process SmartMarkers and save the workbook
        ProcessAndSaveWorkbook(dataTable);
    }

    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // Configure SmartMarkerOptions to rename duplicate sheets automatically
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Sheet1_{0}"
        };

        // Create a new workbook and populate it from the DataTable
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);

        // Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Förväntad output

Running the program prints:

```
Workbook saved to YOUR_DIRECTORY\DuplicateSheets.xlsx
```

När du öppnar `DuplicateSheets.xlsx` visas ett blad med namnet **Sheet1** där `Id`‑kolumnen innehåller värdena `1, 2, 3, 4, 5`. Om du senare bearbetar en annan `DataTable` med namnet `"Sheet1"` i samma arbetsbok, kommer Aspose.Cells automatiskt att skapa **Sheet1_1**, **Sheet1_2**, osv.

## Slutsats

Du vet nu hur du **create excel sheet** från en `DataTable` i C#, **export datatable to excel**, **add rows to datatable**, genererar **create multiple excel sheets** med automatisk namngivning, och **save workbook as xlsx**. Det kompletta, körbara exemplet demonstrerar hela arbetsflödet och ger praktiska tips för stora datamängder och anpassad formatering.

### Vad blir nästa steg?

* Utforska **cell formatting** (typsnitt, färger, kanter) genom att komma åt `Worksheet.Cells` efter `ProcessSmartMarkers`.  
* Använd **SmartMarker loops** för att generera master‑detail‑rapporter i en enda arbetsbok.  
* Byt till **CSV export** genom att ändra `SaveFormat.Csv` om du behöver en ren‑text‑representation.  

Känn dig fri att anpassa koden till dina egna datakällor—oavsett om det är en databasfråga, ett API‑svar eller en in‑memory‑samling. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}