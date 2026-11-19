---
category: general
date: 2026-11-19
description: Hur man använder wrapcols i C# för att radbryta data i Excel och snabbt
  beräkna Excel‑formler.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- calculate excel formulas
- wrap data in excel
- save excel file c#
- load excel workbook c#
language: sv
lastmod: 2026-11-19
og_description: Hur man använder wrapcols i C# för att bryta rader i Excel. Lär dig
  att beräkna Excel‑formler och spara arbetsboken programatiskt.
og_image_alt: Screenshot showing wrapped data in an Excel worksheet after applying
  WRAPCOLS
og_title: Hur man använder wrapcols i C# – wrapa data i Excel
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to use wrapcols in C# to wrap data in Excel and calculate Excel
    formulas quickly.
  headline: How to use wrapcols in C# to wrap data in Excel
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Data Wrapping
title: Hur man använder wrapcols i C# för att radbryta data i Excel
url: /sv/net/formatting-rows-and-columns-in-excel/how-to-use-wrapcols-in-c-to-wrap-data-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder wrapcols i C# för att radbryta data i Excel

Om du behöver **how to use wrapcols** för att omorganisera en vertikal lista till flera kolumner, visar den här guiden de exakta stegen. Du kommer också att lära dig hur du **calculate Excel formulas** så att resultatet lagras i filen du sparar.

Att arbeta med Excel från C# börjar ofta med att ladda en arbetsbok, applicera formler och slutligen spara ändringarna. Denna handledning täcker alla dessa steg samtidigt som koden är enkel att kopiera‑klistra in i ditt eget projekt.

## Vad du kommer att uppnå

* Ladda en befintlig `.xlsx`-fil från disk (**load excel workbook c#**).
* Applicera `WRAPCOLS`-funktionen på ett område, vilket effektivt **wrap data in Excel**.
* Tvinga motorn att utvärdera formeln (**calculate Excel formulas**).
* Spara den modifierade arbetsboken (**save Excel file c#**).

Det enda förutsättningen är en referens till **Aspose.Cells for .NET** (eller något bibliotek som stödjer `WRAPCOLS`-funktionen). Koden fungerar med .NET 6+ och Visual Studio 2022, men vilken C#‑IDE som helst räcker.

## Så använder du wrapcols med Aspose.Cells

`WRAPCOLS`‑arbetsbladsfunktionen tar ett endimensionellt område och returnerar en tvådimensionell array som fyller det angivna antalet kolumner. Aspose.Cells utvärderar funktionen precis som Excel gör, så du kan använda den direkt i en cellformel.

```csharp
using System;
using Aspose.Cells;          // Install-Package Aspose.Cells via NuGet

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook and get the first worksheet
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(workbookPath);
        Worksheet ws = wb.Worksheets[0];

        // Step 2: Write the WRAPCOLS formula into a cell
        // This wraps the values from A2:A10 into 3 columns, starting at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";

        // Step 3: Force calculation so the result becomes a static range
        wb.CalculateFormula();

        // Step 4: Save the workbook so you can open it in Excel
        var outputPath = @"YOUR_DIRECTORY\output.xlsx";
        wb.Save(outputPath);

        Console.WriteLine("Workbook saved to " + outputPath);
    }
}
```

### Varför varje rad är viktig

* **Loading the workbook** ger dig en levande objektmodell som speglar Excel‑filen på disken.  
* **Assigning the formula** till `A1` talar om för Excel (eller Aspose.Cells) att behandla området som en dynamisk array.  
* **`CalculateFormula()`** triggar beräkningsmotorn; utan den skulle formeln förbli oberäknad tills filen öppnas i Excel.  
* **Saving** skriver de beräknade värdena tillbaka till en ny fil, vilket gör den radbrutna datan synlig för alla som öppnar arbetsboken.

## Beräkna Excel‑formler programatiskt

Att anropa `Workbook.CalculateFormula()` är det rekommenderade sättet att **calculate Excel formulas** när du behöver resultaten omedelbart. Metoden respekterar alla inbyggda funktioner, anpassade användardefinierade funktioner och eventuella externa referenser som redan har lösts.

Om du har flera arbetsblad som är beroende av varandra kan du också skicka ett `CalculationOptions`‑objekt för att kontrollera itereringsgränser eller aktivera flertrådad beräkning:

```csharp
var options = new CalculationOptions
{
    // Enable iterative calculation for circular references
    IterativeCalculation = true,
    MaxIterations = 100,
    // Use all available CPU cores
    EnableMultiThreadedCalculation = true
};

wb.CalculateFormula(options);
```

Detta extra steg är valfritt för det enkla `WRAPCOLS`‑exemplet, men blir nödvändigt i större arbetsböcker där prestanda spelar roll.

## Spara Excel‑fil C# efter att ha radbutit data

Anropet till `Workbook.Save()` skriver hela arbetsboken, inklusive den nymaterialiserade arrayen som produceras av `WRAPCOLS`. Du kan välja något av de stödjade formaten (`.xlsx`, `.xls`, `.csv`, etc.):

```csharp
// Save as a standard XLSX file (default)
wb.Save(@"YOUR_DIRECTORY\wrapped.xlsx");

// Save as CSV – only the active sheet is exported
wb.Save(@"YOUR_DIRECTORY\wrapped.csv", SaveFormat.Csv);
```

Steget **save Excel file c#** garanterar att den radbrutna datan sparas, så nästa gång någon öppnar filen ser de en statisk tabell istället för en formel.

## Ladda Excel‑arbetsbok C# och förbered arbetsblad

Om din källfil ännu inte innehåller den data du vill radbryta, kan du skapa den i farten:

```csharp
// Create a new workbook with a single worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Populate column A with sample values
for (int i = 0; i < 9; i++)
{
    ws.Cells[i + 2, 0].PutValue($"Item {i + 1}");
}
```

Detta kodsnutt demonstrerar **load excel workbook c#** i den meningen att du kan börja med en tom arbetsbok, fylla den och sedan applicera `WRAPCOLS`. Samma mönster fungerar när du behöver importera data från en databas eller en CSV‑fil innan radbrytning.

## Proffstips: verifiera resultatet utan att öppna Excel

Efter sparning kan du programatiskt läsa tillbaka det radbrutna området för att bekräfta att operationen lyckades:

```csharp
// Reload the saved file
Workbook checkWb = new Workbook(@"YOUR_DIRECTORY\output.xlsx");
Worksheet checkWs = checkWb.Worksheets[0];

// Print the first three rows of the wrapped area
for (int row = 0; row < 3; row++)
{
    for (int col = 0; col < 3; col++)
    {
        Console.Write($"{checkWs.Cells[row, col].StringValue}\t");
    }
    Console.WriteLine();
}
```

Konsolen bör visa den ursprungliga listan uppdelad i tre kolumner, vilket bekräftar att **wrap data in excel** fungerade som förväntat.

## Vanliga frågor och edge cases

| Fråga | Svar |
|----------|--------|
| *Vad händer om källområdet har fler rader än `WRAPCOLS` kan fylla?* | Funktionen fortsätter att skapa nya rader vid behov. Antalet kolumner förblir fast. |
| *Kan jag radbryta till ett annat antal kolumner?* | Ja—ändra det andra argumentet, t.ex. `=WRAPCOLS(A2:A10,5)` för fem kolumner. |
| *Behöver jag rensa formeln efter beräkning?* | Nej om du anropar `CalculateFormula()`. Funktionen returnerar en statisk array, men formeln kvarstår i cellen. Om du vill ha ett rent värde, kopiera området och klistra in‑värden över det. |
| *Fungerar detta med äldre `.xls`‑filer?* | `WRAPCOLS` är en dynamisk‑array‑funktion som introducerades i Excel 365. Äldre filformat som inte stödjer dynamiska arrayer kommer att lagra formeln men kanske inte visar det radbrutna resultatet korrekt. Använd `.xlsx` för pålitligt beteende. |

## Slutsats

Du vet nu **how to use wrapcols** i C# för att **wrap data in Excel**, hur du **calculate Excel formulas** i farten, och hur du **save Excel file C#** efter transformationen. Det kompletta exemplet demonstrerar hur man laddar en arbetsbok, applicerar `WRAPCOLS`‑funktionen, tvingar beräkning och sparar resultatet.

### Nästa steg

* Utforska andra dynamiska‑array‑funktioner som `UNWRAPCOLS` eller `SEQUENCE`.  
* Använd **Aspose.Cells** för att importera data från en databas och sedan radbryta dem automatiskt.  
* Kombinera `WRAPCOLS` med villkorsstyrd formatering för att markera specifika rader efter radbrytning.

Känn dig fri att experimentera med olika källområden, antal kolumner och utdataformat. Om du stöter på problem löser du dem oftast genom att gå tillbaka till steget **calculate Excel formulas** eller kontrollera arbetsbokens beräkningsinställningar.

--- 

*Image: ![Screenshot of wrapped data in Excel](/images/wrapcols-example.png){.align-center alt="Skärmbild som visar radbruten data i ett Excel‑arbetsblad efter att ha applicerat WRAPCOLS"}*


## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man använder WRAPCOLS i C# för Excel‑arrayer och sparande av arbetsbok](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-in-c-for-excel-arrays-and-workbook-savin/)
- [Hur man skapar Excel‑arbetsbok och delar data med WRAPCOLS i C#](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}