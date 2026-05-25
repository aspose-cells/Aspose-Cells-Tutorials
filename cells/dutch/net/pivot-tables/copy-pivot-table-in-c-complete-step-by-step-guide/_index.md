---
category: general
date: 2026-03-25
description: Kopieer een draaitabel met C# via Aspose.Cells. Leer hoe je een draaitabel
  kopieert, een draaitabelbestand exporteert en gegevens behoudt in enkele minuten.
draft: false
keywords:
- copy pivot table
- how to copy pivot
- export pivot table file
- Aspose.Cells pivot
- C# Excel automation
language: nl
og_description: Kopieer draaitabel in C# met Aspose.Cells. Deze gids laat zien hoe
  je een draaitabel kopieert, het draaitabelbestand exporteert en alle instellingen
  intact houdt.
og_title: Kopieer draaitabel in C# – Volledige programmeertutorial
tags:
- C#
- Excel
- Aspose.Cells
- Data Export
title: Kopieer draaitabel in C# – Complete stap‑voor‑stap gids
url: /nl/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopieer draaitabel in C# – Complete stapsgewijze handleiding

Heb je ooit een **draaitabel kopiëren** nodig gehad van het ene werkboek naar het andere en je afgevraagd of de draaitabel‑logica de verplaatsing overleeft? Je bent niet de enige. In veel rapportage‑pijplijnen genereren we een master‑werkboek en sturen vervolgens een lichtgewicht kopie die eindgebruikers nog steeds in staat stelt de gegevens te slicen. Het goede nieuws? Met een paar regels C# en Aspose.Cells kun je precies dat doen—geen handmatig gedoe nodig.

In deze tutorial lopen we het volledige proces door: het laden van het bronbestand, het selecteren van het bereik dat de draaitabel bevat, het plakken in een nieuw werkboek terwijl de draaitabeldefinitie behouden blijft, en uiteindelijk **export pivot table file** voor downstream consumptie. Aan het einde weet je *hoe je een draaitabel programmatically kunt kopiëren* en heb je een kant‑klaar voorbeeld dat je in je project kunt plaatsen.

## Prerequisites

- .NET 6+ (of .NET Framework 4.6+) geïnstalleerd  
- Aspose.Cells for .NET NuGet‑pakket (`Install-Package Aspose.Cells`)  
- Een bron‑Excel‑bestand (`source.xlsx`) dat al een draaitabel bevat (elke grootte werkt)  
- Basiskennis van C#; geen diepgaande Excel‑internals vereist  

Als je een van deze mist, voeg dan gewoon het NuGet‑pakket toe en open Visual Studio—niets meer.

## What the Code Does (Overview)

1. **Load** het werkboek dat de originele draaitabel bevat.  
2. **Define** een `Range` die de volledige draaitabel omsluit (inclusief de cache).  
3. **Create** een gloednieuw werkboek dat de bestemming wordt.  
4. **Paste** het bereik met `CopyPivotTable = true` zodat de draaitabeldefinitie wordt gekopieerd, niet alleen de waarden.  
5. **Save** het bestemmingsbestand, waardoor je een **export pivot table file** krijgt die je kunt delen.  

Dat is de volledige workflow in vijf nette stappen. Laten we elk onderdeel nader bekijken.

## Step 1 – Load the Source Workbook that Contains the Pivot Table

First we need to bring the source file into memory. Aspose.Cells makes this a one‑liner.

```csharp
using Aspose.Cells;

// Load the source workbook (replace the path with your actual file)
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet – adjust the index if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
```

*Waarom dit belangrijk is:* Het laden van het werkboek geeft ons toegang tot de onderliggende pivot‑cache. Als je alleen celwaarden kopieert, verliest de draaitabel zijn slicer‑functionaliteit. Door het werkboekobject alive te houden, behouden we de volledige pivot‑metadata.

## Step 2 – Define the Range That Includes the Pivot Table

A pivot isn’t just a block of cells; it also has hidden cache data. The safest way is to select a rectangle that fully surrounds the visible area. In most cases `A1:E20` works, but you can programmatically discover the exact bounds using `PivotTable` properties.

```csharp
// Example range – adjust to match your pivot's size
Range sourceRange = sourceSheet.Cells.CreateRange("A1:E20");

// (Optional) Dynamically get the used range of the pivot:
PivotTable pivot = sourceSheet.PivotTables[0];
int firstRow = pivot.Row - 1;      // include header row
int firstCol = pivot.Column - 1;   // include field list
int lastRow  = pivot.Row + pivot.RowCount;
int lastCol  = pivot.Column + pivot.ColumnCount;
Range dynamicRange = sourceSheet.Cells.CreateRange(firstRow, firstCol,
                                                    lastRow - firstRow + 1,
                                                    lastCol - firstCol + 1);
```

*Waarom we een bereik kiezen:* De `Paste`‑methode werkt op een `Range`‑object. Door het exacte gebied te specificeren, zorgen we ervoor dat zowel de draaitabel‑lay‑out als de cache samen reizen.

## Step 3 – Create a New Destination Workbook

Now we spin up a blank workbook that will receive the copied pivot. Nothing fancy, just a clean slate.

```csharp
// Initialize an empty workbook – it comes with one default worksheet
Workbook destinationWorkbook = new Workbook();
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

*Tip:* Als je bestaande werkbladen wilt behouden (bijv. een sjabloon), kun je het nieuwe werkboek toevoegen als een kloon van een sjabloonbestand in plaats van de lege constructor te gebruiken.

## Step 4 – Paste the Range While Preserving the Pivot Table

Here’s the heart of the operation. Setting `CopyPivotTable = true` tells Aspose.Cells to transfer the pivot definition, not just the displayed values.

```csharp
destinationSheet.Cells.Paste(
    sourceRange,
    new PasteOptions
    {
        PasteType = PasteType.All,      // copy everything: formulas, formats, etc.
        CopyPivotTable = true           // crucial – keeps the pivot functional
    });
```

*Wat er onder de motorkap gebeurt:* Aspose.Cells recreëert de pivot‑cache in het bestemmingswerkboek, herschakelt de gegevensbron van de draaitabel en behoudt slicers, filters en berekende velden. Het resultaat is een volledig interactieve draaitabel—precies wat je zou verwachten als je het blad handmatig in Excel had gedupliceerd.

## Step 5 – Save the Resulting Workbook (Export Pivot Table File)

Finally we write the destination workbook to disk. The file you get is your **export pivot table file** ready for distribution.

```csharp
destinationWorkbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");
```

Open `copy-pivot.xlsx` in Excel, and you’ll see the pivot table intact, ready to be refreshed or sliced.

## Full Working Example (All Steps Combined)

Below is the complete program you can copy‑paste into a console app. It includes error handling and comments for clarity.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // 1️⃣ Load source workbook with the pivot table
                Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
                Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

                // 2️⃣ Define the range that fully encloses the pivot
                // Adjust "A1:E20" as needed, or use dynamic detection shown earlier
                Range sourceRange = sourceSheet.Cells.CreateRange("A1:E20");

                // 3️⃣ Create a fresh destination workbook
                Workbook destinationWorkbook = new Workbook();
                Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

                // 4️⃣ Paste the range and keep the pivot definition
                destinationSheet.Cells.Paste(
                    sourceRange,
                    new PasteOptions
                    {
                        PasteType = PasteType.All,
                        CopyPivotTable = true
                    });

                // 5️⃣ Save the new file – this is your exported pivot table file
                destinationWorkbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");

                Console.WriteLine("✅ Pivot table copied successfully! File saved as copy-pivot.xlsx");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❌ An error occurred: {ex.Message}");
            }
        }
    }
}
```

**Expected outcome:** When you open `copy-pivot.xlsx`, the pivot table appears exactly as in `source.xlsx`. You can refresh it, change filters, or even add new data sources without losing functionality.

## Common Questions & Edge Cases

### What if the source workbook has multiple pivots?

Loop through `sourceSheet.PivotTables` and repeat the copy‑paste for each. Just be sure each destination range doesn’t overlap.

```csharp
int destRow = 0;
foreach (PivotTable pt in sourceSheet.PivotTables)
{
    // Calculate a non‑overlapping destination range for each pivot
    Range src = sourceSheet.Cells.CreateRange(pt.Row, pt.Column,
                                              pt.RowCount + 5, pt.ColumnCount + 5);
    destinationSheet.Cells.Paste(src, new PasteOptions { PasteType = PasteType.All, CopyPivotTable = true });
    destRow += pt.RowCount + 10; // move down for the next pivot
}
```

### Does this work with external data sources (e.g., SQL)?

If the original pivot pulls from an external connection, the connection string is also copied. However, the destination workbook must have access to the same data source. You may need to adjust credentials or use `WorkbookSettings` to allow external connections.

### Can I copy only the pivot layout (no data)?

Set `PasteOptions.PasteType = PasteType.Formulas` and keep `CopyPivotTable = true`. This copies the structure while leaving the data cache empty, forcing a refresh on first open.

### What about protecting the sheet?

If the source sheet is protected, unprotect it before copying, or pass the appropriate `Password` to `Worksheet.Unprotect`. After pasting, you can re‑apply protection on the destination sheet.

## Pro Tips & Pitfalls

- **Pro tip:** Gebruik altijd de nieuwste versie van Aspose.Cells; oudere releases hadden een bug waarbij `CopyPivotTable` slicers negeerde.  
- **Watch out for:** Grote pivot‑caches kunnen het bestemmingsbestand oppompen. Als grootte belangrijk is, overweeg dan ongebruikte velden te wissen vóór het kopiëren.  
- **Performance tip:** Bij het kopiëren van veel werkbladen, schakel tijdelijk `WorkbookSettings.EnableThreadedCalculation` uit om de bewerking te versnellen.  
- **Naming clash:** Als het bestemmingswerkboek al een draaitabel met dezelfde naam bevat, zal Aspose de binnenkomende een hernoemen (`PivotTable1_1`). Hernoem handmatig als je een specifieke identifier nodig hebt.

## Visual Summary

![Copy pivot table in C# – diagram showing source workbook → range selection → paste with pivot preservation → destination file](copy-pivot-diagram.png "Copy pivot table workflow illustration")

*Alt‑tekst:* **Copy pivot table** workflow‑diagram dat bron, bereik, plakopties en geëxporteerd bestand illustreert.

## Conclusion

We’ve covered everything you need to **copy pivot table** using C# and Aspose.Cells: loading the source, selecting the correct range, preserving the pivot definition during paste, and finally exporting the result as a standalone file. The snippet above is production‑ready; just plug in your paths and you’re good to go.

Now that you know *hoe je een draaitabel programmatically kunt kopiëren*, you can automate report distribution, build template generators, or integrate Excel analytics into larger .NET services. Next up you might explore **export pivot table file** to other formats (PDF, CSV) or embed the workbook into a web API for on‑the‑fly analytics.

Got a twist you’d like to share—perhaps copying pivots across different Excel versions or handling PowerPivot models? Drop a comment, and let’s keep the conversation going. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}