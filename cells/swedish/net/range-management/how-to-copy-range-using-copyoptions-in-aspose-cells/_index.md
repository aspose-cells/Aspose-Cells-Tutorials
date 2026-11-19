---
category: general
date: 2026-11-19
description: Lär dig hur du kopierar ett område med CopyOptions i Aspose.Cells, bevarar
  formatering och pivottabeller när du kopierar ett Excel‑område med formatering.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: sv
lastmod: 2026-11-19
og_description: Att kopiera ett område med CopyOptions i Aspose.Cells låter dig duplicera
  Excel‑data med full formatering och pivottabeller bevarade, vilket möjliggör pålitlig
  arbetsbokshantering.
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: Kopiera område med CopyOptions i Aspose.Cells – steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hur man kopierar ett område med CopyOptions i Aspose.Cells
url: /sv/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man kopierar område med CopyOptions i Aspose.Cells

Om du behöver **copy range using CopyOptions** i Aspose.Cells, visar den här guiden exakt hur du duplicerar ett block med celler samtidigt som all formatering och inbäddade pivottabeller behålls. Många utvecklare har problem med att bevara stil när data flyttas mellan kalkylblad, och `CopyOptions`‑klassen löser det utan extra manuella steg.

I den här handledningen kommer du att lära dig att:

* Definiera käll‑ och målområden i en Excel‑arbetsbok.  
* Använda `CopyOptions` för att behålla cellformatering, kolumnbredder och pivottabeller.  
* Spara resultatet till en ny fil som är klar för vidare bearbetning.

Exemplet fungerar med vilken `.xlsx`‑fil som helst och kräver endast Aspose.Cells för .NET‑biblioteket.

## Förutsättningar

Innan du börjar, se till att du har:

* .NET 6.0 eller senare installerat.  
* En giltig Aspose.Cells för .NET‑licens (eller en gratis utvärderingsnyckel).  
* Visual Studio 2022 eller någon annan C#‑IDE du föredrar.  

Inga ytterligare NuGet‑paket behövs utöver `Aspose.Cells`.

## Steg 1: Skapa projektet och importera namnrymder

Skapa en ny konsolapplikation och lägg till referensen till Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

Direktivet `using Aspose.Cells;` ger dig åtkomst till `Workbook`, `CellArea` och `CopyOptions`.

## Steg 2: Ladda arbetsboken du vill ändra

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`Workbook` representerar hela Excel‑filen. Ersätt `YOUR_DIRECTORY` med den mapp som innehåller din källfil.

## Steg 3: Definiera käll‑ och målområdena

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

`CellArea.CreateCellArea` bygger ett rektangulärt område baserat på den övre‑vänstra och nedre‑högra celladressen. Du kan justera koordinaterna så att de matchar storleken på det block du vill kopiera.

## Steg 4: Kopiera området samtidigt som formatering och pivottabeller bevaras

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

`CopyOptions`‑objektet talar om för Aspose.Cells exakt vad som ska behållas. Att sätta `CopyPivotTables = true` är nyckeln till **copy range using CopyOptions** när din källa innehåller pivottabeller. De andra flaggorna säkerställer att **copy excel range with formatting** uppnås automatiskt – ingen extra kod behövs för att återapplicera stilar efter kopieringen.

### Varför `CopyOptions` är viktigt

* **Prestanda** – Biblioteket utför en enda intern operation istället för att kopiera celler en efter en.  
* **Noggrannhet** – Alla visuella aspekter (typsnitt, färger, kantlinjer) överlever flytten, vilket eliminerar visuell drift i genererade rapporter.  
* **Tillförlitlighet** – Pivottabeller förblir funktionella eftersom deras cache och källreferenser dupliceras.

## Steg 5: Spara den ändrade arbetsboken

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

Efter att ha anropat `Save` innehåller filen `output.xlsx` de ursprungliga data plus det duplicerade blocket på målplatsen, komplett med formatering och pivottabeller.

## Fullständig källkod för referens

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

När du kör programmet skrivs följande ut:

```
Range copied successfully. Output saved to output.xlsx
```

Öppna `output.xlsx` i Excel – du kommer att se blocket A1:H30 duplicerat till A35:H64, med alla cellfärger, kantlinjer, talformat och eventuella pivottabeller intakta.

## Vanliga frågor och hantering av kantfall

### Vad händer om målområdet överlappar källområdet?

Aspose.Cells kastar ett `ArgumentException`. För att undvika detta, beräkna ett mål som inte skär källområdet, eller kopiera till ett annat kalkylblad:

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### Hur kopierar man mellan olika arbetsböcker?

Skapa en andra `Workbook`‑instans för målfilen och använd samma `CopyOptions`‑objekt:

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### Kopierar `CopyOptions` även sammanslagna celler?

Ja. Flaggan `CopyStyle` inkluderar information om sammanslagna celler. Om du behöver finare kontroll, sätt `options.CopyMergedCells = true` (tillgängligt i nyare versioner).

### Vad händer med stora områden (tusentals rader)?

Operationen är minnes‑effektiv, men du kan vilja öka `WorkbookSettings`‑`MemorySetting` till `MemorySetting.MemoryPreference` för mycket stora filer.

## Pro‑tips

* **Återanvänd samma `CopyOptions`**‑instans för flera kopieringsoperationer – det minskar overhead för objektallokering.  
* **Validera områden** innan du kopierar: `if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` hjälper dig att fånga fel relaterade till felaktiga koordinater tidigt.  
* **Stäng av beräkning** (`workbook.Settings.CalcMode = CalculationMode.Manual`) medan du kopierar stora datamängder för att snabba upp processen, och anropa sedan `workbook.CalculateFormula()` efter kopieringen om du behöver uppdaterade resultat.

## Slutsats

Du vet nu hur du **copy range using CopyOptions** i Aspose.Cells, och uppnår en full **copy excel range with formatting** samtidigt som pivottabeller och andra avancerade funktioner bevaras. Detta tillvägagångssätt eliminerar manuell återapplicering av stil och säkerställer att din Excel‑automatisering förblir robust och underhållbar.

Nästa steg du kan utforska:

* Använd `CopyOptions` för att duplicera hela kalkylblad.  
* Kombinera kopieringsoperationen med `WorksheetCollection.AddCopy` för mall‑baserad rapportgenerering.  
* Integrera koden i ett ASP.NET Core‑API för att erbjuda Excel‑transformeringar i realtid.

Känn dig fri att experimentera med olika käll‑/målkoordinater och dela dina resultat i kommentarerna!

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}