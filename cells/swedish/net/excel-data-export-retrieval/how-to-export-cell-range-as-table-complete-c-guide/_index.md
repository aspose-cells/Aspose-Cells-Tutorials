---
category: general
date: 2026-07-13
description: Hur man exporterar ett cellområde som tabell med C# och ExportTableOptions.
  Lär dig steg‑för‑steg arbetsboksinställning, formatering och tabellexport.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export cell range as table
- ExportTableOptions usage
- Workbook and Worksheet handling
- cell value formatting C#
- scientific notation export
language: sv
lastmod: 2026-07-13
og_description: Hur man exporterar ett cellområde som tabell i C# med ExportTableOptions.
  Följ den här guiden för att formatera celler, skapa en arbetsbok och exportera en
  tabell utan ansträngning.
og_image_alt: Diagram illustrating a C# code snippet that exports a single cell range
  as a formatted table
og_title: Hur man exporterar cellområde som tabell – Fullständig C#‑genomgång
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to export cell range as table using C# and ExportTableOptions.
    Learn step‑by‑step workbook setup, formatting, and table export.
  headline: How to Export Cell Range as Table – Complete C# Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
- data export
title: Hur man exporterar cellområde som tabell – Komplett C#-guide
url: /sv/net/excel-data-export-retrieval/how-to-export-cell-range-as-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man exporterar cellområde som tabell – Komplett C#‑guide

Har du någonsin undrat **hur man exporterar cellområde som tabell** utan att dra i håret över formateringsknep? Du är inte ensam. Oavsett om du matar data till en rapporteringspipeline eller bara behöver en snabb CSV‑liknande dump, kan behärskning av exportprocessen spara dig timmar av manuellt kopier‑och‑klistra.

I den här handledningen går vi igenom exakt vilka steg som krävs för att ta en numerisk cell, applicera vetenskaplig notation och exportera den som en tabell med **ExportTableOptions**. I slutet har du ett körbart kodexempel, förstår *varför* varje anrop behövs och vet hur du justerar koden för större områden eller andra format.

## Förutsättningar

- .NET 6 eller senare (API‑et fungerar likadant på .NET Framework 4.7+)
- Aspose.Cells för .NET installerat (`Install-Package Aspose.Cells`)
- Grundläggande kunskap om C#‑syntax; inga djupa Excel‑internkunskaper krävs

Har du allt? Bra—nu kör vi.

## Steg 1: Ställ in exportalternativ – Hur man exporterar cellområde som tabell

Det första du behöver är en **ExportTableOptions**‑instans som talar om för biblioteket hur cellinnehållet ska behandlas. Utan detta exporteras som standard råa numeriska värden, vilket kan bryta nedströms konsumenter som förväntar sig text.

```csharp
// Step 1: Define export options – export the cell value as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Return the cell content as text
    CustomFormat = "0.00E+00"       // Apply scientific notation format
};
```

**Varför det är viktigt:**  
- `ExportAsString = true` tvingar biblioteket att skriva cellens visade text, inte dess underliggande double.  
- `CustomFormat` låter dig påtvinga en **export i vetenskaplig notation**, användbart när du hanterar mycket stora eller mycket små tal.

> **Proffstips:** Om du behöver ett datum‑ eller valutformat, ersätt `"0.00E+00"` med `"yyyy‑MM‑dd"` respektive `"$#,##0.00"`.

## Steg 2: Skapa en arbetsbok och hämta det första kalkylbladet – Arbete med arbetsbok och kalkylblad

En **Workbook** representerar hela Excel‑filen, medan ett **Worksheet** är en enskild flik. För en enkel export använder vi det första bladet, som alltid finns på index 0.

```csharp
// Step 2: Create a new workbook and access the first worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

**Varför det är viktigt:**  
Att skapa en ny `Workbook` ger en ren start—inga dolda stilar eller kvarvarande data som kan störa. Att nå `Worksheets[0]` är det snabbaste sättet att få tag på det aktiva bladet utan att behöva tänka på bladnamn.

## Steg 3: Fyll i mål‑cellen – Formatering av cellvärde i C#

Nu sätter vi in ett numeriskt värde i cell **A1** (rad 0, kolumn 0). Värdet vi väljer är avsiktligt med många decimaler så att du kan se den vetenskapliga notationen i aktion.

```csharp
// Step 3: Insert a numeric value into cell A1 (row 0, column 0)
sheet.Cells[0, 0].PutValue(12345.6789);
```

**Varför det är viktigt:**  
`PutValue` infererar automatiskt cellens datatyp. Eftersom vi senare exporterar som sträng konverteras den råa double‑värdet med det format vi angav tidigare, vilket ger ett snyggt `"1.23E+04"`‑utdata.

## Steg 4: Exportera det definierade cellområdet som en tabell – Export av cellområde som tabell

Med alternativen och datan på plats är sista steget att be Aspose.Cells skriva ut området. Metoden `ExportTable` förväntar sig startrad/kolumn, storleken på området och options‑objektet vi byggde.

```csharp
// Step 4: Export the defined cell range as a table using the options above
// Parameters: startRow, startColumn, totalRows, totalColumns, options
sheet.ExportTable(0, 0, 1, 1, exportOptions);
```

**Varför det är viktigt:**  
- `totalRows = 1` och `totalColumns = 1` begränsar exporten till en enda cell, men du kan öka dessa tal för att täcka större block (t.ex. `5, 3` för ett 5‑rad × 3‑kolumn‑område).  
- Metoden skriver data till en intern tabellstruktur som kan sparas som CSV, HTML eller till och med strömmas direkt till en klient.

### Spara resultatet (valfritt)

Om du vill spara den exporterade tabellen på disk kan du skriva den till en CSV‑fil:

```csharp
// Optional: Save the exported table as CSV for verification
using (var stream = new MemoryStream())
{
    sheet.ExportTableToCSV(stream, exportOptions);
    File.WriteAllBytes("ExportedTable.csv", stream.ToArray());
}
```

Kör du ovanstående kod genereras en fil som innehåller:

```
1.23E+04
```

## Edge Cases & Vanliga variationer

| Situation | Vad som ska ändras | Orsak |
|-----------|-------------------|-------|
| **Exportera flera rader** | Justera `totalRows` och loopa över rader om behövs | Möjliggör batch‑export utan att anropa `ExportTable` upprepade gånger |
| **Bevara formler** | Sätt `ExportAsString = false` | Behåller den ursprungliga formeln istället för det visade värdet |
| **Olika avgränsare** | Använd overloaden `ExportTableToCSV(..., ',', ...)` | Byter från kommatecken‑separerade till tab‑separerade eller pipe‑separerade värden |
| **Stora kalkylblad** | Strömma exporten för att undvika `OutOfMemoryException` | Fungerar bra för >10 000 rader |

## Fullt fungerande exempel

Nedan är det kompletta, kopiera‑och‑klistra‑klara programmet. Det kompileras i vilket .NET‑konsolprojekt som helst som refererar Aspose.Cells.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class ExportCellRangeDemo
{
    static void Main()
    {
        // 1️⃣ Define export options – how to export cell range as table
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            CustomFormat = "0.00E+00"
        };

        // 2️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Put a numeric value into A1
        sheet.Cells[0, 0].PutValue(12345.6789);

        // 4️⃣ Export the single‑cell range as a table
        sheet.ExportTable(0, 0, 1, 1, exportOptions);

        // Optional: write to CSV to see the result
        using (var ms = new MemoryStream())
        {
            sheet.ExportTableToCSV(ms, exportOptions);
            File.WriteAllBytes("ExportedTable.csv", ms.ToArray());
        }

        Console.WriteLine("Export complete! Check ExportedTable.csv");
    }
}
```

**Förväntad utdata:**  
En fil med namnet `ExportedTable.csv` som innehåller en enda rad:

```
1.23E+04
```

Om du öppnar CSV‑filen i en textredigerare ser du den vetenskapliga notationen exakt som definierad.

## Slutsats

Vi har gått igenom **hur man exporterar cellområde som tabell** från början till slut: konfigurera `ExportTableOptions`, skapa en `Workbook`, infoga data och slutligen anropa `ExportTable`. Genom att förstå varje del kan du nu skala metoden till större områden, andra format eller till och med integrera den i ett web‑API som levererar Excel‑baserad data i realtid.

Framöver kan du vilja utforska:

- **ExportTableToHTML** för web‑klara förhandsvisningar  
- **ExportTableToDataTable** för att mata direkt in i ADO.NET‑pipelines  
- Avancerade **anpassade format** för datum, valutor eller procenttal  

Prova dessa och du förvandlar en enkel cell‑export till en mångsidig data‑leveransmotor. Har du frågor eller ett udda användningsfall? lämna en kommentar nedan—lycka till med kodandet!

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närliggande ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra fler API‑funktioner och utforska alternativa implementationssätt i dina egna projekt.

- [How to Export Visible Excel Rows Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Export Excel Files in .NET Using Aspose.Cells&#58; A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Access an Excel Cell by Name Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/cell-operations/access-cell-by-name-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}