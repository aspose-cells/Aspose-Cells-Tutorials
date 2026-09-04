---
category: general
date: 2026-02-09
description: Hur man skapar en arbetsbok i C# med en ljusblå bakgrund och importerar
  data med rubriker. Lär dig att lägga till en ljusblå bakgrund, använda Excels standardstil
  och importera en datatabell.
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: sv
og_description: Hur man skapar en arbetsbok i C# med ljusblå bakgrund, importerar
  data med rubriker och tillämpar standardformat i Excel – allt i en kortfattad guide.
og_title: Hur man skapar arbetsbok – Ljusblå bakgrund, dataimport
tags:
- C#
- Excel
- Aspose.Cells
title: Hur man skapar arbetsbok – ljusblå bakgrund, dataimport
url: /sv/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så skapar du en arbetsbok – ljusblå bakgrund, dataimport

Har du någonsin funderat **hur man skapar en arbetsbok** i C# som ser lite snyggare ut direkt ur lådan? Kanske har du hämtat en `DataTable` från en databas och är trött på de tråkiga, standardvita cellerna. I den här handledningen går vi igenom hur du skapar en ny arbetsbok, lägger till en ljusblå bakgrund på en kolumn och importerar data med rubriker – allt med den standardstil som Excel levererar.

Vi kommer också att strö in några “vad‑om”-scenarier, som att hantera null‑värden eller anpassa fler än en kolumn. När du är klar har du en fullt stylad Excel‑fil som du kan skicka till intressenter utan någon efterbearbetning.

## Förutsättningar

Innan vi dyker ner, se till att du har:

* **.NET 6+** (koden fungerar även på .NET Framework 4.6+)  
* **Aspose.Cells for .NET** – biblioteket som driver `Workbook`, `Style` och `ImportDataTable`‑anropen. Installera det via NuGet:  

  ```bash
  dotnet add package Aspose.Cells
  ```

* En `DataTable`‑källa – vi fejkar en i exemplet, men du kan ersätta den med vilken ADO.NET‑fråga som helst.

Har du allt? Bra, låt oss komma igång.

## Steg 1: Initiera en ny arbetsbok (Primärt nyckelord)

Det första du behöver göra är **hur man skapar en arbetsbok** – bokstavligen. Klassen `Workbook` representerar hela Excel‑filen, och dess konstruktor ger dig en ren start.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **Varför detta är viktigt:** Att börja med en ny `Workbook` säkerställer att du har full kontroll över varje stil från början. Om du öppnade en befintlig fil skulle du ärva de stilar som den ursprungliga författaren lämnade, vilket kan leda till inkonsekvent formatering.

## Steg 2: Förbered den DataTable du ska importera

För illustrationens skull skapar vi en enkel `DataTable`. I verkliga scenarier skulle du förmodligen anropa en lagrad procedur eller en ORM‑metod.

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **Tips:** Om du behöver bevara kolumnordningen exakt som den visas i databasen, sätt `ImportDataTable`‑parametern `importColumnNames` till `true`. Detta instruerar Aspose.Cells att skriva kolumnrubrikerna åt dig.

## Steg 3: Definiera kolumnstilar – standard + ljusblå bakgrund

Nu svarar vi på **add light blue background**‑delen av pusslet. Aspose.Cells låter dig skicka en array av `Style`‑objekt som motsvarar varje kolumn du importerar. Det första elementet är stilen för kolumn 0, det andra för kolumn 1, och så vidare. Om du har färre stilar än kolumner faller de återstående kolumnerna tillbaka på standardstilen.

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **Varför bara två stilar?** I vårt exempel har vi fyra kolumner, men vi vill bara att den andra kolumnen (Name) ska sticka ut. Array‑längden behöver inte matcha antalet kolumner; alla saknade poster ärver automatiskt arbetsbokens standardstil.

## Steg 4: Importera DataTable med rubriker och stilar

Här samlar vi **excel import datatable c#** och **import data with headers**. Metoden `ImportDataTable` gör det tunga arbetet: den skriver kolumnnamnen, raderna och applicerar stil‑arrayen vi just byggde.

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### Förväntat resultat

Efter att programmet har körts kommer `workbook` att innehålla ett enda kalkylblad som ser ut så här:

| **ID** | **Name** (light‑blue) | **HireDate** | **Salary** |
|-------|------------------------|--------------|------------|
| 1     | Alice Johnson          | 5/12/2020    | 72000      |
| 2     | Bob Smith              | 3/4/2019     | 68000      |
| 3     | Carol White            | *(blank)*    | 75000      |

* **Name**‑kolumnen har en ljusblå bakgrund, vilket bevisar att stil‑arrayen fungerar.
* Kolumnrubrikerna genereras automatiskt eftersom vi skickade `true` för `importColumnNames`.
* Null‑värden visas som tomma celler, vilket är standardbeteendet i Aspose.Cells.

## Steg 5: Spara arbetsboken (Valfritt men användbart)

Du kommer förmodligen vilja skriva filen till disk eller strömma tillbaka den till en webbklient. Att spara är enkelt:

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **Pro‑tips:** Om du riktar dig mot äldre Excel‑versioner, ändra `SaveFormat.Xlsx` till `SaveFormat.Xls`. API:t sköter konverteringen åt dig.

## Kantfall & variationer

### Flera stylade kolumner

Om du behöver fler än en stylad kolumn, utöka helt enkelt `columnStyles`‑arrayen:

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

Nu kommer både **Name** och **Salary** att vara ljusblå.

### Villkorsstyrd formatering istället för fasta stilar

Ibland vill du att en kolumn ska bli röd när ett värde överstiger ett tröskelvärde. Det är där **use default style excel** möter villkorsstyrd formatering:

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### Import utan rubriker

Om ditt downstream‑system redan levererar egna rubriker, skicka bara `false` för argumentet `importColumnNames`. Datan börjar då på `A1` och du kan skriva egna rubriker efteråt.

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## Fullt fungerande exempel (All

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}