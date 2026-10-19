---
category: general
date: 2026-08-11
description: Exportera Excel till txt i C# med en steg‑för‑steg‑guide. Lär dig hur
  du konverterar xlsx till vanlig text med Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- convert xlsx to plain text
- how to export excel worksheet as text
- export worksheet as text file
language: sv
lastmod: 2026-08-11
og_description: Exportera Excel till txt i C# snabbt. Denna handledning visar hur
  man konverterar xlsx till vanlig text, konfigurerar format och hanterar stora kalkylblad.
og_image_alt: Code snippet that exports an Excel worksheet to a plain text file using
  C#
og_title: Exportera Excel till txt i C# – steg‑för‑steg guide för utvecklare
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  headline: Export excel to txt in C# – complete programming guide
  type: TechArticle
- description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  name: Export excel to txt in C# – complete programming guide
  steps:
  - name: – load the workbook
    text: '```csharp using Aspose.Cells;'
  - name: – get the first worksheet
    text: '```csharp Worksheet sheet = workbook.Worksheets[0]; ```'
  - name: – define export options for text conversion
    text: '```csharp ExportTableOptions exportOptions = new ExportTableOptions { ExportAsString
      = true, // Export all values as text DateTimeFormat = "yyyy-MM-dd", // Desired
      date format NumberFormat = "#,##0.00" // Desired numeric format }; ```'
  - name: – export worksheet as text file
    text: '```csharp // Apply the options to the worksheet sheet.ExportTableOptions
      = exportOptions;'
  type: HowTo
tags:
- excel
- csharp
- text export
- aspose.cells
title: Exportera Excel till txt i C# – komplett programmeringsguide
url: /sv/net/converting-excel-files-to-other-formats/export-excel-to-txt-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportera Excel till txt i C# – komplett programmeringsguide

Om du behöver **exportera excel till txt** kan du uppnå resultatet med några rader C#‑kod. Denna guide visar hur du konverterar en `.xlsx`‑arbetsbok till en ren‑textfil samtidigt som du bevarar det dataformat du definierar.

Att exportera kalkylblad som textfiler är ett vanligt krav när efterföljande system endast accepterar avgränsad data eller när du behöver granska råa cellvärden. I följande avsnitt kommer du att lära dig hur du konfigurerar datum- och talformat, hanterar stora blad och undviker vanliga fallgropar.

## Förutsättningar för att konvertera xlsx till ren text

* .NET 6.0 (eller senare) installerat – koden riktar sig mot .NET Standard 2.0, så den fungerar även med .NET Framework 4.6+.
* En licens för **Aspose.Cells** (den kostnadsfria utvärderingen fungerar för testning).
* En IDE som Visual Studio 2022 eller Visual Studio Code.
* En Excel‑fil med namnet `input.xlsx` placerad i en mapp som du kan referera till från ditt projekt.

Dessa objekt är de enda externa kraven; handledningen är inte beroende av ytterligare NuGet‑paket.

## Så exporterar du excel till txt med Aspose.Cells

Aspose.Cells tillhandahåller klassen `ExportTableOptions` som låter dig styra hur cellvärden renderas som strängar. Genom att sätta `ExportAsString` till `true` tvingar du varje cell att skrivas som text, vilket är avgörande när du vill ha en deterministisk ren‑text‑utdata.

### Steg 1 – ladda arbetsboken

```csharp
using Aspose.Cells;

string inputPath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(inputPath);
```

*`Workbook`‑konstruktorn läser Excel‑filen till minnet. Om filen inte finns kastas ett undantag, så du kanske vill omsluta detta anrop i ett try‑catch‑block för produktionskod.*

### Steg 2 – hämta det första kalkylbladet

```csharp
Worksheet sheet = workbook.Worksheets[0];
```

*Kalkylblad är noll‑baserade, så index 0 refererar till den första fliken. Du kan ersätta indexet med ett bladnamn (`workbook.Worksheets["Sheet1"]`) när du behöver rikta in dig på ett specifikt blad.*

### Steg 3 – definiera exportalternativ för textkonvertering

```csharp
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,               // Export all values as text
    DateTimeFormat = "yyyy-MM-dd",       // Desired date format
    NumberFormat   = "#,##0.00"          // Desired numeric format
};
```

*`ExportAsString` garanterar att varje cell, oavsett ursprunglig typ, blir en sträng i utdatafilen. Egenskaperna `DateTimeFormat` och `NumberFormat` låter dig styra hur datum och tal visas, vilket är avgörande när du **konverterar xlsx till ren text** för system som förväntar ett specifikt mönster.*

### Steg 4 – exportera kalkylbladet som textfil

```csharp
// Apply the options to the worksheet
sheet.ExportTableOptions = exportOptions;

// Export the data to a tab‑delimited text file
string outputPath = @"YOUR_DIRECTORY\Exported.txt";
sheet.ExportDataTable(outputPath);
```

*`ExportDataTable` skriver kalkylbladets innehåll till en ren‑textfil med de alternativ du angav. Standardavgränsaren är ett tab‑tecken (`\t`). Om du behöver en annan avgränsare kan du använda överlagringen som accepterar en `ExportTableOptions`‑instans och specificera `ExportTableOptions.Separator`. Den resulterande filen kan öppnas i vilken textredigerare som helst eller importeras till en databas.*

#### Förväntat resultat

Anta att `input.xlsx` innehåller:

| A            | B       | C          |
|--------------|---------|------------|
| 2023‑05‑01   | 1234.5  | Exempeltext|

Med alternativen ovan kommer filen `Exported.txt` att innehålla:

```
2023-05-01	1,234.50	Sample text
```

Varje kolumn separeras med ett tab‑tecken, datum följer formatet `yyyy‑MM‑dd` och tal använder komma som tusentalsavgränsare samt två decimaler.

## Vanliga fallgropar när du exporterar kalkylblad som textfil

| Problem | Varför det händer | Hur man undviker det |
|---------|-------------------|----------------------|
| Språköberoende talformat | Standardformatet följer OS‑kulturen, vilket kan producera kommatecken eller punkter inkonsekvent. | Ställ explicit in `NumberFormat` i `ExportTableOptions`. |
| Dolda rader eller kolumner visas i utdata | Aspose.Cells exporterar hela det använda området, inklusive dolda rader. | Sätt `ExportTableOptions.ExportHiddenRows = false` och `ExportHiddenColumns = false` om du vill hoppa över dem. |
| Stora kalkylblad orsakar minnesbelastning | Hela arbetsboken laddas in i minnet innan export. | Använd `Workbook.LoadOptions` med `LoadDataOnly = true` för att minska minnesanvändning, eller bearbeta filen i delar. |
| Datumceller lagrade som text i källfilen | Om en cell redan innehåller en formaterad sträng behandlar exportören den som text och ignorerar `DateTimeFormat`. | Säkerställ att källarbetsboken lagrar datum som korrekta Excel‑datatyper. |

Att åtgärda dessa problem gör processen **hur man exporterar Excel‑kalkylblad som text** pålitlig i olika miljöer.

## Utöka lösningen – anpassade avgränsare och strömexport

Om du behöver en kommaseparerad värdefil (CSV) istället för en tab‑avgränsad fil, ändra alternativen:

```csharp
exportOptions.Separator = ',';
exportOptions.ExportHiddenRows = false;   // optional
exportOptions.ExportHiddenColumns = false; // optional
sheet.ExportTableOptions = exportOptions;
sheet.ExportDataTable(@"YOUR_DIRECTORY\Exported.csv");
```

För filer större än 500 MB förhindrar strömning av utdata att applikationen tar slut på RAM:

```csharp
using (FileStream stream = new FileStream(@"YOUR_DIRECTORY\LargeExport.txt",
                                          FileMode.Create,
                                          FileAccess.Write,
                                          FileShare.None,
                                          bufferSize: 81920,
                                          useAsync: true))
{
    sheet.ExportDataTable(stream, exportOptions);
}
```

Överlagringen som accepterar en `Stream` skriver rader inkrementellt, vilket är idealiskt för batch‑jobb eller webbtjänster som returnerar textfilen direkt till en klient.

## Verifiera resultatet programatiskt

När exporten är klar kan du läsa den första raden tillbaka till minnet för att bekräfta formatet:

```csharp
string firstLine = File.ReadLines(outputPath).First();
Console.WriteLine($"First line: {firstLine}");
```

Att köra detta kodsnutt bör skriva ut samma rad som visas i avsnittet *Förväntat resultat*, vilket ger dig förtroende för att konverteringen lyckades.

## Sammanfattning av den kompletta koden

Genom att sätta ihop alla delar får du ett självständigt program som du kan kopiera in i en konsolapplikation:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputPath  = @"YOUR_DIRECTORY\input.xlsx";
        string outputPath = @"YOUR_DIRECTORY\Exported.txt";

        // Load workbook
        Workbook workbook = new Workbook(inputPath);
        Worksheet sheet = workbook.Worksheets[0];

        // Configure export options
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            DateTimeFormat = "yyyy-MM-dd",
            NumberFormat   = "#,##0.00",
            Separator      = '\t' // tab delimiter
        };

        // Apply options and export
        sheet.ExportTableOptions = exportOptions;
        sheet.ExportDataTable(outputPath);

        // Simple verification
        string firstLine = File.ReadLines(outputPath).First();
        Console.WriteLine($"Export completed. First line: {firstLine}");
    }
}
```

Kompilera och kör programmet; filen `Exported.txt` visas i samma katalog som källarbetsboken.

## Nästa steg och relaterade ämnen

* **Exportera kalkylblad som textfil** – experimentera med olika avgränsare, kodningar (UTF‑8 vs. ASCII) och radslutstilar för plattformsoberoende kompatibilitet.
* **Masskonvertering** – loopa igenom `workbook.Worksheets` för att generera en separat textfil för varje flik.
* **Integration med databaser** – skicka den genererade texten direkt till en bulk‑insert‑operation för SQL Server eller PostgreSQL.
* **

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig behärska ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man exporterar Excel‑filer i .NET med Aspose.Cells: En omfattande guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [Hur man exporterar synliga Excel‑rader med Aspose.Cells för .NET: En steg‑för‑steg‑guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [Hur man exporterar Excel‑diagram till PDF med Aspose.Cells för .NET: En steg‑för‑steg‑guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}