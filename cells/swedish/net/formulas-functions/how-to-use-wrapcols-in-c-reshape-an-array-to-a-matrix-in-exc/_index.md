---
category: general
date: 2026-06-17
description: Hur man använder WRAPCOLS i C# för att omvandla en array till en matris,
  skriva en arrayformel till en cell och läsa in befintliga Excel‑filer med Aspose.Cells.
draft: false
keywords:
- how to use wrapcols
- reshape array to matrix
- write array formula
- write formula to cell
- load existing excel
language: sv
og_description: Hur man använder WRAPCOLS i C# för att snabbt omforma en array till
  en matris, skriva en arrayformel till en cell och arbeta med befintliga Excel-filer.
og_title: Hur man använder WRAPCOLS i C# – Omforma en array till en matris
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: How to use WRAPCOLS in C# to reshape an array to a matrix, write array
    formula to a cell, and load existing Excel files with Aspose.Cells.
  headline: How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel
  type: TechArticle
- description: How to use WRAPCOLS in C# to reshape an array to a matrix, write array
    formula to a cell, and load existing Excel files with Aspose.Cells.
  name: How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel
  steps:
  - name: 'Optional: Write a Dynamic Array Reference'
    text: 'If you prefer to reference a range instead of a hard‑coded list, you can
      use:'
  - name: 1. What if I need a different number of rows?
    text: '`WRAPCOLS` only takes the column count; the row count is inferred. To force
      a specific row count, you can combine it with `WRAPROWS` or pad the source array
      with empty strings.'
  - name: 2. Does WRAPCOLS work with text values?
    text: 'Absolutely. Replace the numbers with quoted strings:'
  - name: 3. Can I apply formatting to the generated matrix?
    text: 'After calculation, you can style the range programmatically:'
  - name: 4. How do I handle very large arrays?
    text: Aspose.Cells can process tens of thousands of elements, but keep an eye
      on memory. If you hit limits, consider writing the data in chunks or using `Workbook.Settings.MemorySetting
      = MemorySetting.MemoryPreference;`.
  type: HowTo
tags:
- excel
- csharp
- aspose.cells
title: Hur man använder WRAPCOLS i C# – Omforma en array till en matris i Excel
url: /sv/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder WRAPCOLS i C# – Omforma en array till en matris i Excel

Har du någonsin undrat **hur man använder WRAPCOLS** för att omvandla en platt lista med siffror till en prydlig tabell i Excel? Du är inte ensam. Oavsett om du bygger ett rapporteringsverktyg eller bara leker med data, kan omformning av en array till en matris spara dig massor av manuellt kopierande‑och‑klistra.

I den här handledningen går vi igenom ett komplett, körbart exempel som visar dig hur du **skriver en array‑formel till en cell**, beräknar resultatet och till och med **laddar en befintlig Excel**‑arbetsbok om du behöver. När du är klar har du ett robust, kopiera‑och‑klistra‑klart kodsnutt som fungerar med den senaste Aspose.Cells för .NET.

## Vad du kommer att lära dig

- Syftet med `WRAPCOLS`‑funktionen och när den glänser.  
- Hur du **omformar en array till en matris** med en enda formel.  
- Steg‑för‑steg‑kod för att **skriva en formel till en cell** och tvinga beräkning.  
- Valfria tekniker för **laddning av en befintlig Excel**‑fil innan formeln appliceras.  
- Vanliga fallgropar och tips för att utöka metoden till större datamängder.

Ingen extern dokumentation behövs – allt du behöver finns här.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar också på .NET Framework 4.7+).  
- Aspose.Cells för .NET installerat (`dotnet add package Aspose.Cells`).  
- Grundläggande förståelse för C#‑syntax; om du kan skapa en konsolapp är du redo att köra.

> **Pro tip:** Om du använder Visual Studio, aktivera *nullable reference types* (`<Nullable>enable</Nullable>`) för att fånga potentiella null‑buggar tidigt.

## Steg 1: Ställ in projektet och importera namnrymder

Först, skapa ett nytt konsolprojekt (eller klistra in koden i ett befintligt). Lägg sedan till de nödvändiga `using`‑direktiven så kompilatorn vet var `Workbook` och `Worksheet` finns.

```csharp
using System;
using Aspose.Cells;   // Main library for Excel manipulation

namespace WrapColsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill in the logic in the next steps
        }
    }
}
```

> **Why this matters:** Importing `Aspose.Cells` gives you access to the high‑performance Excel engine that evaluates `WRAPCOLS` without needing Excel installed on the machine.

## Steg 2: Skapa eller ladda en arbetsbok

Du kan börja från början eller öppna en befintlig fil. Följande kodsnutt visar båda alternativen; kommentera bara den du inte behöver.

```csharp
// Option A – Create a brand‑new workbook
Workbook workbook = new Workbook();   // starts with a single empty worksheet

// Option B – Load an existing Excel file (useful when you have templates)
// string inputPath = @"C:\Data\input.xlsx";
// Workbook workbook = new Workbook(inputPath);
```

> **Edge case:** If the file you’re loading is password‑protected, pass the password as the second argument: `new Workbook(path, "password")`.

## Steg 3: Hämta målbladet

För det mesta är det första bladet (`Worksheets[0]`) det du vill ha, men du kan också referera till ett blad med namn.

```csharp
Worksheet sheet = workbook.Worksheets[0];               // by index
// Worksheet sheet = workbook.Worksheets["DataSheet"]; // by name (if it exists)
```

## Steg 4: Skriv WRAPCOLS‑formeln till en cell

Här är kärnan i handledningen. `WRAPCOLS` tar en array och ett kolumnantal, och sprider sedan värdena radvis. Vi placerar formeln i **A1** så att matrisen börjar i övre‑vänstra hörnet.

```csharp
// Write the WRAPCOLS formula that turns {1,2,3,4,5,6} into 2 rows × 3 columns
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

> **What’s happening?**  
> - The curly‑brace syntax `{1,2,3,4,5,6}` creates an inline array constant.  
> - The second argument (`3`) tells Excel to create three columns, automatically wrapping the remaining items into new rows.  
> - Because we’re using Aspose.Cells, the formula is stored exactly as you’d type it in Excel, and the engine will evaluate it on demand.

### Valfritt: Skriv en dynamisk array‑referens

Om du föredrar att referera till ett område istället för en hårdkodad lista kan du använda:

```csharp
// Assume B1:B6 already contains numbers you want to reshape
sheet.Cells["A1"].Formula = "=WRAPCOLS(B1:B6,3)";
```

På så sätt uppdateras matrisen automatiskt när källområdet ändras.

## Steg 5: Tvinga beräkning och spara resultatet

Aspose.Cells beräknar inte formler förrän du säger åt den. Genom att anropa `Calculate()` materialiseras resultatet och formelns utdata blir faktiska cellvärden.

```csharp
// Force calculation so the WRAPCOLS output appears in the sheet
workbook.Calculate();

// Save the workbook – adjust the path as needed
string outputPath = @"C:\Data\output.xlsx";
workbook.Save(outputPath);
```

När du öppnar `output.xlsx` i Excel ser du:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

Det är **omformnings‑effekten från array till matris** du efterfrågade.

## Fullt fungerande exempel

Sätter vi ihop alla bitar får du ett färdigt program:

```csharp
using System;
using Aspose.Cells;

namespace WrapColsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a new workbook (or load an existing one)
            Workbook workbook = new Workbook(); // new Workbook(@"C:\Data\input.xlsx");

            // 2️⃣ Get the first worksheet
            Worksheet sheet = workbook.Worksheets[0];

            // 3️⃣ Write the WRAPCOLS formula – reshape {1..6} into 2×3
            sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

            // 4️⃣ Force calculation so the matrix is materialized
            workbook.Calculate();

            // 5️⃣ Save the result
            string outputPath = @"C:\Data\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Kör programmet, öppna `output.xlsx`, och du ser matrisen exakt som ovan.

## Vanliga frågor & fallgropar

### 1. Vad händer om jag behöver ett annat antal rader?

`WRAPCOLS` tar bara kolumnantalet; antalet rader härleds automatiskt. För att tvinga ett specifikt radantal kan du kombinera med `WRAPROWS` eller fylla på källarrayen med tomma strängar.

```csharp
// Example: Force 3 rows, 2 columns (will add blanks if needed)
sheet.Cells["A1"].Formula = "=WRAPROWS({1,2,3,4,5,6},3)";
```

### 2. Fungerar WRAPCOLS med textvärden?

Absolut. Byt ut siffrorna mot strängar inom citationstecken:

```csharp
sheet.Cells["A1"].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",\"Apr\",\"May\",\"Jun\"},3)";
```

### 3. Kan jag applicera formatering på den genererade matrisen?

Efter beräkning kan du programatiskt formatera området:

```csharp
Range matrix = sheet.Cells.CreateRange("A1:C2");
Style style = workbook.CreateStyle();
style.Font.Color = System.Drawing.Color.Blue;
style.Font.IsBold = true;
matrix.ApplyStyle(style, new StyleFlag() { Font = true });
```

### 4. Hur hanterar jag mycket stora arrayer?

Aspose.Cells kan bearbeta tiotusentals element, men håll koll på minnet. Om du når gränserna, överväg att skriva data i delar eller använda `Workbook.Settings.MemorySetting = MemorySetting.MemoryPreference;`.

## Pro‑tips för produktionskod

- **Cache the worksheet reference** if you’re writing many formulas in a loop; it reduces lookup overhead.  
- **Disable automatic calculation** (`workbook.Settings.CalculateFormulaOnOpen = false;`) when you plan to batch‑write dozens of formulas, then call `Calculate()` once at the end.  
- **Wrap the file I/O in try/catch** to surface permission errors early:

```csharp
try
{
    workbook.Save(outputPath);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

- **Validate input** before building the formula string—especially if you concatenate user‑provided values—to avoid malformed formulas.

## Visuell sammanfattning

![Hur man använder WRAPCOLS resultatmatris i Excel](wrapcols-output.png "Hur man använder WRAPCOLS i C# för att omforma en array till en matris")

*Skärmdumpen visar den 2 × 3‑matris som produceras av WRAPCOLS‑formeln.*

## Slutsats

Vi har gått igenom **hur man använder WRAPCOLS** i C# från början till slut: skapa eller ladda en arbetsbok, skriva en array‑formel till en cell, tvinga beräkning och spara resultatet. Du vet nu hur du **omformar en array till en matris**, **skriver en array‑formel** och **laddar befintliga Excel**‑filer – allt med några få rader ren, underhållbar kod.

Nästa steg, du kanske vill utforska:

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationssätt i dina egna projekt.

- [Hur man laddar Excel-filer effektivt med Aspose.Cells i .NET](/cells/english/net/workbook-operations/efficient-excel-load-aspose-cells-net/)
- [Hur man laddar och ändrar Excel-filer med Aspose.Cells för .NET: En omfattande guide](/cells/english/net/workbook-operations/load-modify-excel-aspose-cells-net/)
- [Hur man ställer in språk i Excel-filer med Aspose.Cells .NET för flerspråkigt stöd](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}