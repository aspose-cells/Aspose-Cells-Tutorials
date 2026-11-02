---
category: general
date: 2026-08-17
description: Spara Excel som PowerPoint med C# – steg‑för‑steg‑guide för att konvertera
  XLSX‑filer, göra textrutor redigerbara och generera PPTX‑utdata.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- how to convert xlsx
- make textbox editable
- how to edit textboxes
language: sv
lastmod: 2026-08-17
og_description: Spara Excel som PowerPoint i C# med ett komplett kodexempel. Lär dig
  hur du konverterar XLSX, gör textrutor redigerbara och exporterar till PPTX.
og_image_alt: Screenshot showing Excel data saved as a PowerPoint slide
og_title: Spara Excel som PowerPoint i C# – komplett konverteringsguide
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Save Excel as PowerPoint with C# – step‑by‑step guide to convert XLSX
    files, make textboxes editable, and generate PPTX output.
  headline: How to save Excel as PowerPoint using C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel-to-PowerPoint
title: Hur man sparar Excel som PowerPoint med C# och Aspose.Cells
url: /sv/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man sparar Excel som PowerPoint med C# och Aspose.Cells

Om du behöver **spara Excel som PowerPoint** i ett .NET‑projekt, visar den här guiden en komplett, färdig‑att‑köra‑lösning. Du kommer att se hur du laddar en XLSX‑arbetsbok, gör varje textruta på bladet redigerbar och exporterar resultatet till en PPTX‑fil — allt med bara några rader C#.

Att konvertera Excel till PowerPoint är ett vanligt krav för rapport‑dashboards, bildspel eller automatiserad presentationsgenerering. Denna handledning täcker också **hur man redigerar textrutor** programatiskt, så att du kan anpassa bildens innehåll innan du sparar.

## Förutsättningar

* .NET 6.0 (eller senare) SDK installerat  
* En utvecklingsmiljö såsom Visual Studio 2022 eller VS Code  
* En Aspose.Cells för .NET-licens (eller en gratis utvärderingsnyckel) – ladda ner från [Aspose website](https://products.aspose.com/cells/net/)  
* `input.xlsx`‑filen du vill konvertera  

> **Proffstips:** Om du använder den gratis utvärderingsversionen kommer den exporterade PPTX‑filen att innehålla ett vattenmärke. En licensierad version tar bort det.

## Steg 1: Installera Aspose.Cells NuGet‑paketet

Öppna en terminal i din projektmapp och kör:

```bash
dotnet add package Aspose.Cells
```

Detta lägger till `Aspose.Cells`‑assemblyn, som tillhandahåller klasserna `Workbook`, `Worksheet` och `Shape` som behövs för konverteringen.

## Steg 2: Skapa ett konsolapplikations‑skelett

Skapa ett nytt konsolprojekt (om du inte redan har ett):

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
```

Ersätt den genererade `Program.cs` med koden som visas i nästa steg.

## Steg 3: Ladda arbetsboken och välj det första kalkylbladet

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Load the workbook from a file – adjust the path to your environment
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Varför detta är viktigt:**  
`Workbook` läser in Excel‑filen i minnet, medan `Worksheet` ger dig åtkomst till bladets celler, diagram och former. Det första kalkylbladet är ofta den standardrapport du vill presentera.

## Steg 4: Gör varje textruta på bladet redigerbar

```csharp
        // Iterate through all shapes on the worksheet
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            // Check if the shape is a textbox (ShapeType.TextBox)
            if (shapeItem.Type == ShapeType.TextBox)
            {
                // The IsEditable property was added in Aspose.Cells 25.11
                shapeItem.TextBox.IsEditable = true;
            }
        }
```

**Varför du behöver detta:**  
Som standard är textrutor som importeras från Excel skrivskyddade när de visas i PowerPoint. Genom att sätta `IsEditable = true` möjliggör du att du (eller senare PowerPoint‑användare) kan ändra texten direkt på bilden.

## Steg 5: Spara arbetsboken som en PowerPoint‑presentation

```csharp
        // Define the output path for the PPTX file
        string outputPath = @"YOUR_DIRECTORY\output.pptx";

        // Save the workbook as a PowerPoint presentation
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

**Vad som händer under huven:**  
`Workbook.Save` identifierar enum‑värdet `SaveFormat.Pptx` och översätter Excel‑bladets layout — inklusive rader, kolumner, diagram och de nu redigerbara textrutorna — till PowerPoint‑bildobjekt.

## Fullständig källkod (körbar)

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from a file
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Step 2: Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Make every textbox on the sheet editable (property added in version 25.11)
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            if (shapeItem.Type == ShapeType.TextBox)
            {
                shapeItem.TextBox.IsEditable = true;
            }
        }

        // Step 4: Save the workbook as a PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\output.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

### Förväntat resultat

När du kör programmet (`dotnet run`) bör du se:

```
Conversion complete. PPTX saved to: YOUR_DIRECTORY\output.pptx
```

När du öppnar `output.pptx` i Microsoft PowerPoint visas en bild som speglar det ursprungliga Excel‑bladet. Alla textrutor kan redigeras direkt genom att dubbelklicka på dem.

## Vanliga frågor och specialfall

| Question | Answer |
|----------|--------|
| **Kan jag konvertera ett specifikt kalkylblad istället för det första?** | Ja. Ersätt `workbook.Worksheets[0]` med `workbook.Worksheets["SheetName"]` eller vilket index du behöver. |
| **Vad händer om arbetsboken innehåller flera blad?** | Anropa `workbook.Save` en gång per kalkylblad och ange ett unikt PPTX‑filnamn för varje, eller kombinera dem till en enda presentation genom att använda `Presentation`‑objekt från Aspose.Slides. |
| **Kommer diagram att bevaras?** | Aspose.Cells konverterar Excel‑diagram till PowerPoint‑diagramobjekt automatiskt. Ingen extra kod behövs. |
| **Hur ändrar jag bildstorleken?** | Efter `workbook.Save` kan du ladda den genererade PPTX‑filen med Aspose.Slides och justera `Presentation.SlideSize`. |
| **Vad om jag behöver redigera textrutans text innan jag sparar?** | Åtkomst till `shapeItem.TextBox.Text` i loopen, ändra den och sätt sedan `IsEditable = true`. Exempel: `shapeItem.TextBox.Text = "New title";` |

## Felsökningstips

* **“ShapeType.TextBox” hittades inte** – Se till att du använder Aspose.Cells version 25.11 eller nyare; äldre versioner saknar egenskapen `IsEditable`.  
* **Fil‑inte‑hittad‑fel** – Verifiera att `YOUR_DIRECTORY` är en absolut sökväg eller att den relativa sökvägen pekar på rätt plats.  
* **Licens inte tillämpad** – Anropa `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` innan du laddar arbetsboken för att ta bort utvärderingsvattenmärken.

## Slutsats

Du vet nu hur du **sparar Excel som PowerPoint** med C# genom att ladda en XLSX‑arbetsbok, göra varje textruta redigerbar och exportera till PPTX. Denna metod hanterar diagram, bilder och cellformatering automatiskt, vilket ger dig en färdig presentation att använda.

Nästa steg, utforska relaterade ämnen såsom **konvertera Excel till PowerPoint med Aspose.Slides**, **hur man redigerar textrutor programatiskt efter konvertering**, eller **batch‑processa flera arbetsböcker**. Var och en av dessa bygger på de grundläggande stegen som täcks här och kan ytterligare automatisera ditt rapporteringsflöde.

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man konverterar Excel till PowerPoint med Aspose.Cells för .NET: En komplett guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Hur man kopierar pivottabell i C# – Konvertera Excel till PPTX, kopiera område & gör textruta](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Hur man sparar Excel‑filer i flera format med Aspose.Cells .NET (2023‑guide)](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}