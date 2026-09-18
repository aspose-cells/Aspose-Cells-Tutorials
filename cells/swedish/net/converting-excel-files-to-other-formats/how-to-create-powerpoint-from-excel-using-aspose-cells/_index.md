---
category: general
date: 2026-09-18
description: Skapa PowerPoint från Excel med Aspose.Cells – kopiera pivottabeller,
  exportera områden och spara som PPTX med några få rader C#‑kod.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: sv
lastmod: 2026-09-18
og_description: Skapa PowerPoint från Excel snabbt. Lär dig hur du kopierar pivottabeller,
  exporterar områden och sparar en arbetsbok som PPTX med Aspose.Cells.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: Skapa PowerPoint från Excel med Aspose.Cells – steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  headline: How to create PowerPoint from Excel using Aspose.Cells
  type: TechArticle
- description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  name: How to create PowerPoint from Excel using Aspose.Cells
  steps:
  - name: Load the source workbook and define the range
    text: You must load the workbook that holds the source data and the pivot table.
      Selecting a precise range ensures that only the needed cells are transferred,
      which keeps the resulting slide lightweight.
  - name: Prepare the destination workbook
    text: Aspose.Cells treats a PowerPoint slide as a workbook when you save it in
      PPTX format. Creating a fresh workbook gives you a clean canvas for the copied
      range.
  - name: Copy the range while preserving the pivot table
    text: The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables
      = true` tells Aspose.Cells to keep the pivot table structure intact, not just
      the rendered values.
  - name: Save the workbook as a PowerPoint file
    text: Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag
      tells Aspose.Cells to write the worksheet as a PowerPoint slide.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel to PowerPoint
title: Hur man skapar PowerPoint från Excel med Aspose.Cells
url: /sv/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa PowerPoint från Excel med Aspose.Cells

Om du behöver skapa PowerPoint från Excel visar den här guiden en kortfattad, end‑to‑end‑lösning. Du får se hur du kopierar en pivottabell, exporterar ett markerat område och sparar resultatet som en PPTX‑fil med bara några rader C#.

Att generera en bildspel direkt från kalkylbladsdata tar bort det manuella kopiera‑och‑klistra‑steget som bromsar rapporteringsarbetsflöden. Handledningen täcker allt du behöver, från projektuppsättning till den färdiga PPTX‑filen, och den fungerar med den senaste versionen av Aspose.Cells för .NET.

## Förutsättningar

Innan du börjar, se till att du har:

* **Aspose.Cells för .NET** (version 23.12 eller nyare). Installera via NuGet: `Install-Package Aspose.Cells`.
* En **.NET 6+**‑utvecklingsmiljö (Visual Studio 2022 eller VS Code fungerar).
* En Excel‑arbetsbok (`Source.xlsx`) som innehåller data och pivottabellen du vill återanvända.
* Skrivbehörighet till mål‑mappen.

Inga ytterligare tredjepartsbibliotek krävs.

## Skapa PowerPoint från Excel – steg för steg

Processen består av fyra logiska steg som motsvarar kodexemplet du kommer att se senare.

### Steg 1: Läs in källarbetsboken och definiera området

Du måste läsa in arbetsboken som innehåller källdata och pivottabellen. Att välja ett exakt område säkerställer att endast de nödvändiga cellerna överförs, vilket håller den resulterande bilden lätt.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// Select the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that contains the pivot table and surrounding data
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

**Varför detta är viktigt:**  
`CreateRange` skapar ett `Range`‑objekt som kan kopieras som helhet. Genom att begränsa området till `A1:G20` undviker du att orelaterade celler tas med, vilket annars skulle göra PowerPoint‑filen onödigt stor.

### Steg 2: Förbered mål‑arbetsboken

Aspose.Cells behandlar en PowerPoint‑bild som en arbetsbok när du sparar den i PPTX‑format. Att skapa en ny arbetsbok ger dig en ren canvas för det kopierade området.

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**Tips:** Om du behöver flera bilder kan du lägga till ytterligare kalkylblad och senare spara varje som en separat PPTX‑fil.

### Steg 3: Kopiera området samtidigt som pivottabellen bevaras

`CopyRange`‑metoden accepterar ett `PasteOptions`‑objekt. Genom att sätta `CopyPivotTables = true` instrueras Aspose.Cells att behålla pivottabellens struktur, inte bara de renderade värdena.

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**Hur det fungerar:**  
När `CopyPivotTables` är true får destinationsbladet både källdata och pivot‑cachen. Detta innebär att pivottabellen förblir fullt funktionell och kan uppdateras senare om källdata ändras.

### Steg 4: Spara arbetsboken som en PowerPoint‑fil

Till sist exporteras arbetsboken till PPTX‑format. Flaggan `SaveFormat.Pptx` talar om för Aspose.Cells att skriva kalkylbladet som en PowerPoint‑bild.

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**Resultat:**  
`CopyWithPivot.pptx` öppnas i Microsoft PowerPoint (eller någon kompatibel visare) med en enda bild som visar det kopierade området, inklusive en levande pivottabell som kan interageras med i PowerPoint.

## Fullt körbart exempel

Nedan är hela programmet som du kan klistra in i ett nytt konsolprojekt och köra direkt.

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook and select the range containing the pivot table
            Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
            Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

            // 2️⃣ Create a fresh workbook that will become the PowerPoint slide
            Workbook destinationWorkbook = new Workbook();
            Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

            // 3️⃣ Copy the range, preserving the pivot table definition
            destinationSheet.Cells.CopyRange(
                sourceRange,
                new PasteOptions { CopyPivotTables = true });

            // 4️⃣ Export the workbook as a PPTX file
            destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);

            Console.WriteLine("PowerPoint file created successfully.");
        }
    }
}
```

**Förväntad utskrift:**  
När programmet körs skrivs “PowerPoint file created successfully.” och en fil med namnet `CopyWithPivot.pptx` skapas. När du öppnar filen i PowerPoint visas en enda bild där det kopierade Excel‑området visas exakt som i källarbetsbladet, med en aktiv pivottabell som kan uppdateras från PowerPoint.

## Vanliga variationer och kantfall

| Situation | Vad som ska ändras |
|-----------|--------------------|
| **Flera pivottabeller** | Definiera separata `Range`‑objekt för varje tabell och anropa `CopyRange` för var och en, eller kopiera hela bladet om de delar samma datakälla. |
| **Stora datamängder** | Utöka området (t.ex. `"A1:Z5000"`). Överväg att aktivera `PasteOptions.CompressData = true` för att minska PPTX‑storleken. |
| **Olika bildlayouter** | Efter sparning som PPTX, öppna filen i PowerPoint och applicera en anpassad layout eller tema; data förblir redigerbar. |
| **Spara till en ström** | Använd `destinationWorkbook.Save(stream, SaveFormat.Pptx)` när du behöver returnera PPTX via ett webb‑API. |
| **Bevara cellformatering** | Sätt `PasteOptions.PasteType = PasteType.All` för att behålla teckensnitt, färger och kantlinjer. |

**Proffstips:** Verifiera alltid att mål‑mappen finns innan du anropar `Save`. Om mappen saknas kastar `Save` ett `DirectoryNotFoundException`.

## Slutsats

Du vet nu hur du skapar PowerPoint från Excel, kopierar en pivottabell och exporterar resultatet som en PPTX‑fil med Aspose.Cells. Stegen – läsa in källarbetsboken, definiera ett område, kopiera med `CopyPivotTables` och spara som PPTX – täcker hela arbetsflödet på ett pålitligt, produktionsklart sätt.

Nästa steg är att utforska **hur du exporterar Excel till PPTX** för flera kalkylblad, eller lära dig **hur du kopierar område mellan arbetsböcker** när du behöver slå ihop data från flera källor innan du genererar bildspelet. Båda ämnena bygger på samma API‑yta och kan kombineras för att automatisera komplexa rapporteringspipelines.

Lycka till med kodningen, och njut av att förvandla dina kalkylblad till snygga presentationer!

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Create and Save Excel Files with Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}