---
category: general
date: 2026-10-01
description: Lägg till diagram i Word med Aspose på bara några minuter. Lär dig att
  bädda in Excel‑diagram i Word, exportera diagram från Excel till Word, skapa Word‑dokument
  med Aspose och spara diagram i Word‑dokument.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add chart to word
- embed excel chart word
- export chart excel word
- create word document aspose
- save chart word document
language: sv
lastmod: 2026-10-01
og_description: Lägg till diagram i Word med Aspose på några minuter. Den här guiden
  visar hur du bäddar in ett Excel‑diagram i Word, exporterar diagram från Excel till
  Word, skapar ett Word‑dokument med Aspose och sparar diagrammet i Word‑dokumentet.
og_image_alt: Screenshot illustrating how to add chart to Word using Aspose
og_title: Lägg till diagram i Word med Aspose – bädda in Excel-diagram
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  headline: How to add chart to Word with Aspose – embed Excel chart
  type: TechArticle
- description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  name: How to add chart to Word with Aspose – embed Excel chart
  steps:
  - name: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
    text: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
  - name: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
    text: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
  - name: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
    text: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
  - name: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
    text: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
  - name: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
    text: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
  type: HowTo
tags:
- Aspose
- C#
- Word automation
title: Hur man lägger till diagram i Word med Aspose – bädda in Excel-diagram
url: /sv/net/chart-rendering-and-conversion/how-to-add-chart-to-word-with-aspose-embed-excel-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så lägger du till diagram i Word med Aspose – bädda in Excel‑diagram

Om du snabbt behöver **add chart to Word**, ger den här handledningen dig en komplett, färdig‑körbar lösning. Du kommer att se hur du bäddar in ett Excel‑diagram i en Word‑fil, exporterar diagrammet från Excel till Word, och slutligen **save chart Word document** med bara några rader C#.

Att bädda in diagram är ett vanligt krav när du genererar rapporter, fakturor eller instrumentpaneler programatiskt. I slutet av den här guiden kommer du att kunna **create Word document Aspose** som innehåller vilket diagram som helst från en Excel‑arbetsbok, utan manuell copy‑paste.

## Prerequisites

- .NET 6.0 eller senare (koden fungerar också med .NET Framework 4.7+)
- Aspose.Cells- och Aspose.Words‑paket från NuGet (installera via `dotnet add package Aspose.Cells` och `dotnet add package Aspose.Words`)
- En befintlig Excel‑fil (`Chart.xlsx`) som innehåller minst ett diagram
- En utvecklingsmiljö såsom Visual Studio 2022 eller VS Code

## Lägg till diagram i Word med Aspose

Nedan är det fullständiga, fristående programmet. Kopiera det till ett nytt konsolprojekt, återställ paketen och kör det. Programmet läser in Excel‑arbetsboken, skapar ett Word‑dokument, infogar det första diagrammet och sparar resultatet.

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

namespace AddChartToWordDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the Excel workbook that contains the chart
            var workbookPath = @"YOUR_DIRECTORY\Chart.xlsx";
            var workbook = new Workbook(workbookPath);

            // Step 2: Create a new Word document that will receive the chart
            var wordDoc = new Document();

            // Step 3: Initialise a DocumentBuilder for the Word document
            var builder = new DocumentBuilder(wordDoc);

            // Step 4: Insert the first chart from the first worksheet into the Word document
            // This uses Aspose.Words' InsertChart overload that accepts an Aspose.Cells chart object
            builder.InsertChart(workbook.Worksheets[0].Charts[0]);

            // Step 5: Save the resulting Word document
            var outputPath = @"YOUR_DIRECTORY\Chart.docx";
            wordDoc.Save(outputPath);

            Console.WriteLine($"Chart successfully added and saved to '{outputPath}'.");
        }
    }
}
```

### Varför varje rad är viktig

1. **Loading the workbook** – `Workbook` läser in Excel‑filen och ger dig programmatisk åtkomst till dess arbetsblad och diagram.  
2. **Creating the Word document** – `Document` är Aspose.Words ingångspunkt för alla Word‑behandlingsuppgifter.  
3. **DocumentBuilder** – Denna hjälparklass låter dig infoga innehåll (text, bilder, diagram) vid den aktuella markörpositionen.  
4. **InsertChart** – Överlagringen som accepterar ett `Aspose.Cells.Chart`‑objekt kopierar diagrammets data, formatering och serier direkt in i Word‑filen. Ingen mellanliggande bildkonvertering krävs, vilket bevarar vektor­kvaliteten.  
5. **Save** – `Save` skriver .docx‑paketet till disk och slutför steget **save chart word document**.

#### Förväntat resultat

Efter att ha kört programmet, öppna `Chart.docx`. Du kommer att se exakt det diagram som lagrades i `Chart.xlsx`, placerat där byggaren placerades (i början av dokumentet). Diagrammet förblir fullt redigerbart i Word (du kan ändra storlek, färger eller modifiera datakällan).

## Bädda in Excel‑diagram i Word

Om du behöver bädda in mer än ett diagram, upprepa `InsertChart`‑anropet för varje diagramobjekt. Till exempel, för att bädda in alla diagram från det första arbetsbladet:

```csharp
var sheet = workbook.Worksheets[0];
foreach (Chart chart in sheet.Charts)
{
    builder.InsertChart(chart);
    builder.Writeln(); // add a line break between charts
}
```

**Pro tip:** Använd `builder.Writeln()` för att infoga ett styckebrott, så att varje diagram börjar på en ny rad.

## Exportera diagram Excel Word – hantera flera arbetsblad

När diagram är spridda över flera arbetsblad, iterera genom arbetsbokens `Worksheets`‑samling:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    foreach (Chart chart in ws.Charts)
    {
        builder.InsertChart(chart);
        builder.Writeln();
    }
}
```

Denna metod **export chart Excel Word** för vilken arbetsboks­layout som helst, vilket gör lösningen robust för komplexa rapporter.

## Skapa Word‑dokument Aspose – anpassa utseende

Du kan kontrollera storlek och position för varje infogat diagram genom att modifiera `Shape` som returneras av `InsertChart`:

```csharp
Shape chartShape = builder.InsertChart(chart);
chartShape.Width = 500;   // width in points
chartShape.Height = 300;  // height in points
chartShape.WrapType = WrapType.Inline; // make the chart flow with text
```

Att justera `WrapType` till `Inline` säkerställer att diagrammet beter sig som ett vanligt stycke, vilket ofta är önskvärt för automatiserad dokumentgenerering.

## Spara diagram Word‑dokument – bästa praxis

- **Use a descriptive file name** (`Report_Q1_2026.docx`) för att göra versionshantering enklare.
- **Dispose objects** när du är klar, särskilt i stora batch‑processer:

```csharp
wordDoc.Dispose();
workbook.Dispose();
```

- **Validate the result** programatiskt om du genererar många filer:

```csharp
if (System.IO.File.Exists(outputPath))
{
    Console.WriteLine("File saved successfully.");
}
else
{
    Console.Error.WriteLine("Failed to save the document.");
}
```

## Vanliga frågor & kantfall

| Question | Answer |
|----------|--------|
| *Kan jag infoga ett diagram som inte är det första på bladet?* | Ja. Åtkomst via index: `sheet.Charts[2]` för det tredje diagrammet. |
| *Vad händer om Excel‑diagrammet använder en datakälla som inte finns i arbetsboken?* | Aspose.Cells bäddar in data direkt i diagramobjektet, så diagrammet förblir funktionellt även om källområdet tas bort. |
| *Behöver jag en licens för Aspose?* | En gratis utvärdering fungerar, men en licensierad version tar bort vattenstämpeln och låser upp alla funktioner. |
| *Kommer diagrammet att vara redigerbart i Word efter infogning?* | Diagrammet infogas som ett inbyggt Word‑diagram, så användare kan redigera serier, titlar och stilar via Word‑gränssnittet. |
| *Hur infogar man ett diagram som en bild istället för ett inbyggt diagram?* | Använd `builder.InsertImage(chart.ToImage())` för att bädda in en rasterbild. Detta är användbart när du vill bevara den exakta visuella återgivningen utan redigerbarhet på Word‑nivå. |

## Fullt fungerande exempel (kopiera‑klistra)

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

class AddChartToWord
{
    static void Main()
    {
        // Load Excel workbook
        var wb = new Workbook(@"C:\Data\Chart.xlsx");

        // Create Word document
        var doc = new Document();
        var builder = new DocumentBuilder(doc);

        // Insert every chart from every worksheet
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (Chart ch in ws.Charts)
            {
                Shape shape = builder.InsertChart(ch);
                shape.Width = 500;
                shape.Height = 300;
                builder.Writeln(); // separate charts
            }
        }

        // Save the document
        var outPath = @"C:\Data\ReportWithCharts.docx";
        doc.Save(outPath);
        Console.WriteLine($"Document saved to {outPath}");
    }
}
```

När koden körs skapas en Word‑fil (`ReportWithCharts.docx`) som innehåller **add chart to word**‑resultat för varje diagram i källarboken.

## Slutsats

Du vet nu hur du **add chart to Word** med Aspose.Cells och Aspose.Words, hur du **embed Excel chart word**, **export chart Excel Word**, **create Word document Aspose**, och slutligen **save chart word document**. Metoden fungerar för enkla diagram‑scenarier såväl som för komplexa arbetsböcker med många diagram över flera arbetsblad.

Nästa steg du kan utforska:

- Applicera anpassad styling på de infogade diagrammen (färger, typsnitt) via `Chart`‑API:et.
- Kombinera diagraminfogning med textgenerering för att producera helt automatiserade rapporter.
- Använd Aspose.Slides om du behöver

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man sparar DOCX från Excel – Komplett guide för att exportera diagram till Word](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-docx-from-excel-complete-guide-to-export-charts/)
- [Skapa Excel‑arbetsbok med cirkeldiagram med Aspose.Cells .NET – Omfattande guide](/cells/english/net/charts-graphs/create-excel-workbook-pie-chart-aspose-cells-net/)
- [Skapa ett bubbeldiagram i Excel med Aspose.Cells .NET&#58; En steg‑för‑steg‑guide](/cells/english/net/charts-graphs/create-bubble-chart-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}