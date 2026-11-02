---
category: general
date: 2026-06-08
description: Maak stap‑voor‑stap een Excel‑werkmap in C# en leer hoe je de EXPAND‑functie
  in Excel gebruikt voor dynamische bereiken. Perfect voor .NET‑ontwikkelaars.
draft: false
keywords:
- create excel workbook c#
- use expand function in excel
language: nl
og_description: Maak een Excel-werkmap in C# met een duidelijk voorbeeld en ontdek
  hoe je de EXPAND-functie in Excel kunt gebruiken om dynamische arrays te genereren.
og_title: Maak Excel-werkmap C# – Complete programmeergids
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  headline: Create Excel Workbook C# – Full Guide with Expand Function
  type: TechArticle
- description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  name: Create Excel Workbook C# – Full Guide with Expand Function
  steps:
  - name: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
    text: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
  - name: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
    text: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
  - name: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
    text: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
  - name: '**Creates an Excel workbook C#** using Aspose.Cells.'
    text: '**Creates an Excel workbook C#** using Aspose.Cells.'
  - name: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
    text: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
  - name: Adds a cotangent formula (`COT(PI()/4)`).
    text: Adds a cotangent formula (`COT(PI()/4)`).
  - name: Saves the file and optionally auto‑fits columns.
    text: Saves the file and optionally auto‑fits columns.
  type: HowTo
- questions:
  - answer: Absolutely. Aspose.Cells targets .NET Standard 2.0, which is compatible
      with both .NET Core and the classic Framework.
    question: Does this work with .NET Framework 4.8?
  - answer: Use `ws.Protect(ProtectionType.All, "yourPassword");` before saving.
    question: What if I need to protect the sheet?
  - answer: 'Yes—`workbook.Save(stream, SaveFormat.Xlsx);` is handy for web APIs that
      return the file as a download. --- ## TL;DR We built a **complete C# console
      app** that: 1. **Creates an Excel workbook C#** using Aspose.Cells. 2. **Uses
      the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5 block.'
    question: Can I write the workbook directly to a `MemoryStream`?
  type: FAQPage
tags:
- csharp
- excel
- aspose-cells
- .net
title: Excel-werkboek maken C# – Volledige gids met uitbreidingsfunctie
url: /nl/net/excel-workbook/create-excel-workbook-c-full-guide-with-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak Excel-werkmap C# – Volledige gids met de EXPAND-functie

Ever wondered how to **create Excel workbook C#** without wrestling with COM interop or fiddling with XML? You're not the only one. In many .NET projects we need to spit out a spreadsheet, fill it with formulas, and hand it off to non‑technical users. The good news? With a modern library like **Aspose.Cells** the whole process is a piece of cake.

In this tutorial we'll walk through a complete, runnable example that **creates an Excel workbook C#**, drops a couple of formulas—including how to **use expand function in Excel**—and saves the file so you can open it in Excel instantly. By the end you’ll know not only *what* to type, but *why* each line matters, and you’ll have a template you can copy into any project.

## Vereisten

- .NET 6 SDK (of een recente .NET‑versie) geïnstalleerd.
- Een NuGet‑compatibele IDE (Visual Studio, VS Code, Rider, enz.).
- Het **Aspose.Cells** NuGet‑pakket – het levert de `Workbook` en `Worksheet`‑klassen die in de code worden gebruikt.
- Basiskennis van C#; geen Excel‑specifieke ervaring vereist.

Got all that? Great—let’s get started.

## Stap 1: Het project opzetten en Aspose.Cells toevoegen

First, spin up a console app and pull in the library.

```bash
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

> **Pro tip:** Als je op een bedrijfsnetwerk zit, moet je mogelijk een NuGet‑proxy configureren. Het Aspose.Cells‑pakket is lichtgewicht, dus de installatie voltooit zich binnen enkele seconden.

Now open `Program.cs`. You’ll see the default `Main` method—replace it with the skeleton below.

```csharp
using System;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // All of our Excel logic will go here.
        }
    }
}
```

The `using Aspose.Cells;` line brings the spreadsheet classes into scope. If you forget it, the compiler will complain that `Workbook` is undefined—something we’ll avoid later.

## Stap 2: Excel Workbook C# maken en toegang krijgen tot het eerste werkblad

With the project ready, we can finally **create Excel workbook C#**. The `Workbook` constructor gives us a fresh, empty workbook, and the `Worksheets[0]` index returns the default sheet (named “Sheet1”).

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty .xlsx file in memory
Worksheet ws = workbook.Worksheets[0];            // reference to the first (default) sheet
```

Why do we grab the first worksheet explicitly? Because many downstream APIs (like setting formulas) require a `Worksheet` object, not just the `Workbook`. This also makes the code clearer for anyone reading it later.

## Stap 3: Expand-functie in Excel gebruiken om een dynamisch bereik te vullen

Now comes the star of the show: **use expand function in Excel**. The `EXPAND` function (available from Excel 365 onward) takes a source array and pads it to a desired size. In our example we’ll start with a 3‑row vertical array generated by `SEQUENCE(3)` and expand it into a 5 × 5 block.

```csharp
// Step 3: Insert the EXPAND formula into cell A1
ws.Cells["A1"].Formula = "EXPAND(SEQUENCE(3),5,5)";
```

What actually happens?

1. `SEQUENCE(3)` produceert een verticale array `{1;2;3}`.
2. `EXPAND(...,5,5)` vertelt Excel om die array uit te breiden tot 5 rijen en 5 kolommen.
3. Het resultaat is een 5 × 5‑rooster waarbij de eerste drie rijen de getallen 1‑3 bevatten die over de kolommen worden herhaald, en de resterende twee rijen leeg zijn.

Because we’re writing the formula as a string, Excel evaluates it *when the file is opened*, not at runtime. That means the workbook stays lightweight, and any changes to the source array will automatically ripple through.

> **Edge case:** Als een gebruiker de werkmap opent in een oudere versie van Excel die `EXPAND` niet ondersteunt, zal de cel `#NAME?` weergeven. Om dat te voorkomen kun je de formule omhullen met `IFERROR`, maar voor moderne omgevingen is het veilig om op de functie te vertrouwen.

## Stap 4: Een cotangens‑formule toevoegen voor de volledigheid

Let’s sprinkle in another formula to showcase how simple it is to add mathematical expressions. We’ll calculate the cotangent of π/4, which is exactly `1`.

```csharp
// Step 4: Insert a cotangent calculation in cell B1
ws.Cells["B1"].Formula = "COT(PI()/4)";
```

Excel’s `COT` function isn’t as commonly used as `SIN` or `COS`, yet it’s perfect for trigonometric workflows. When you open the workbook, cell **B1** will display `1`.

## Stap 5: De werkmap opslaan en het resultaat verifiëren

All that work would be pointless if we didn’t persist the file. The `Save` method writes the in‑memory workbook to disk. Choose a folder you have write access to, and give the file a friendly name.

```csharp
// Step 5: Save the workbook to the output folder
string outputPath = @"./output.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Run the program:

```bash
dotnet run
```

You should see the console message confirming the save. Open `output.xlsx` in Excel, and you’ll notice:

- Cellen **A1:E5** gevuld met de uitgebreide reeks (1,2,3 in de eerste drie rijen, lege cellen in rijen 4‑5).
- Cel **B1** toont de waarde `1` van de cotangens‑formule.

That’s the full cycle: **create excel workbook c#**, embed formulas, and produce a usable spreadsheet.

![Schermafbeelding van de gegenereerde Excel-werkmap die de uitgebreide array en cotangensresultaat toont](/images/create-excel-workbook-csharp.png "create excel workbook c# voorbeeld")

*Afbeeldings‑alt‑tekst: create excel workbook c# – weergave van de gevulde spreadsheet.*

## Stap 6: Optioneel – Kolommen automatisch aanpassen voor een gepolijste uitstraling

If you plan to distribute the file to end‑users, a quick auto‑fit makes it look professional.

```csharp
// Optional: Auto‑fit all columns in the used range
ws.AutoFitColumns(0, ws.Cells.MaxColumn);
```

This line loops through every column that contains data and adjusts its width to the longest entry. It’s a tiny touch, but it prevents the dreaded “…###” overflow when numbers are wider than the default column width.

## Stap 7: Afronding en volgende stappen

Congratulations—you’ve just mastered how to **create excel workbook c#** from scratch and learned how to **use expand function in excel** to generate dynamic arrays. The code is deliberately minimal so you can copy‑paste it into any project, but the concepts scale:

- **Dynamische gegevensbronnen:** Vervang `SEQUENCE(3)` door een verwijzing naar een ander bereik of een benoemde tabel.
- **Voorwaardelijke opmaak:** Gebruik `ws.Cells["A1:E5"].Style` om kleuren toe te voegen op basis van waarden.
- **Grafieken en afbeeldingen:** Aspose.Cells kan grafieken, afbeeldingen en zelfs draaitabellen insluiten.

Feel free to experiment—swap the `EXPAND` dimensions, try `FILTER` or `SORT`, or chain multiple formulas together. The library handles all of it without you ever touching the low‑level OpenXML format.

---

### Veelgestelde vragen

**Q: Werkt dit met .NET Framework 4.8?**  
A: Absoluut. Aspose.Cells richt zich op .NET Standard 2.0, wat compatibel is met zowel .NET Core als het klassieke Framework.

**Q: Wat als ik het blad moet beveiligen?**  
A: Gebruik `ws.Protect(ProtectionType.All, "yourPassword");` vóór het opslaan.

**Q: Kan ik de werkmap direct naar een `MemoryStream` schrijven?**  
A: Ja—`workbook.Save(stream, SaveFormat.Xlsx);` is handig voor web‑API’s die het bestand als download retourneren.

## TL;DR

We built a **complete C# console app** that:

1. **Creates an Excel workbook C#** using Aspose.Cells.
2. **Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5 block.
3. Adds a cotangent formula (`COT(PI()/4)`).
4. Slaat het bestand op en past optioneel kolommen automatisch aan.

You now have a solid foundation for any automation task that involves generating Excel files from .NET. Happy coding, and may your spreadsheets always stay error‑free!

## Wat moet je hierna leren?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Hoe maak je werkmap‑gescopeerde benoemde bereiken in Excel met Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [Hoe maak en gebruik je unie‑bereiken in Excel met Aspose.Cells .NET (C#‑gids)](/cells/english/net/range-management/excel-union-range-aspose-cells-net/)
- [Excel-werkmap maken met grafieken met Aspose.Cells .NET | Stapsgewijze gids](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}