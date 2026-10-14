---
category: general
date: 2026-03-29
description: Leer hoe je snel rijen in GridJs kunt invoegen. Deze gids behandelt ook
  hoe je rijen kunt toevoegen en meerdere rijen aan een raster kunt toevoegen met
  een batchbewerking.
draft: false
keywords:
- how to insert rows
- how to add rows
- add multiple rows grid
- batch row insertion
- large grid performance
language: nl
og_description: Leer hoe je snel rijen in GridJs kunt invoegen. Deze gids laat zien
  hoe je rijen toevoegt, meerdere rijen in de grid toevoegt en grote batchinvoegingen
  afhandelt.
og_title: Hoe rijen invoegen in GridJs – Voeg meerdere rijen efficiënt toe aan het
  raster
tags:
- GridJs
- C#
- data‑grid
title: Hoe rijen invoegen in GridJs – Voeg meerdere rijen efficiënt toe aan de grid
url: /nl/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-grid-efficien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe rijen in GridJs in te voegen – Meerdere rijen in een raster efficiënt toevoegen

Heb je je ooit afgevraagd **hoe je rijen kunt invoegen** in een enorme GridJs‑tabel zonder de UI te laten bevriezen? Misschien ben je tegen een muur aangelopen bij het proberen **rijen toe te voegen** één voor één en valt de prestaties gewoon uit elkaar. Het goede nieuws is dat GridJs een batch‑API biedt waarmee je **meerdere rijen in een raster kunt toevoegen** in één enkele oproep, waardoor alles snel blijft, zelfs wanneer je met miljoenen items werkt.

In deze tutorial lopen we een compleet, uitvoerbaar voorbeeld door dat precies laat zien **hoe je rijen kunt invoegen** met `InsertRowsBatch`. Je ziet waarom batchen belangrijk is, hoe je het resultaat verifieert, en waar je op moet letten wanneer de index die je target enorm is. Aan het einde kun je met vertrouwen duizend nieuwe records in elke GridJs‑instantie plaatsen.

## Vereisten

- .NET 6.0 of later (de code compileert met elke recente SDK)
- Een referentie naar het `GridJs` NuGet‑pakket (of de DLL als je een aangepaste build gebruikt)
- Basiskennis van C# – je hoeft geen guru te zijn, alleen vertrouwd met klassen en methoden
- Een IDE of editor naar keuze (Visual Studio, Rider, VS Code… alles werkt)

> **Pro tip:** Als je van plan bent om met echt enorme rasters te werken (tientallen miljoenen rijen), schakel `gridJs.EnableVirtualization = true;` in om de UI‑rendering lichtgewicht te houden.

## Stap 1: Maak en configureer de GridJs‑instantie

First things first: you need a live `GridJs` object. Think of it as the canvas on which you’ll paint rows.

```csharp
using System;
using GridJsLibrary;   // Assume this is the namespace for GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Initialize the grid
            GridJs gridJs = new GridJs();

            // Optional: turn on virtualization for huge data sets
            gridJs.EnableVirtualization = true;

            // Populate the grid with some dummy data so we can see the effect
            SeedInitialData(gridJs);

            // Now we’re ready to insert rows in bulk
            InsertRowsInBatch(gridJs);
        }

        // Helper: add 2 000 000 rows so our batch lands at index 2 000 001
        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }
```

> **Waarom deze stap belangrijk is:** Het initialiseren van het raster en eventueel vooraf vullen van data spiegelt een real‑world scenario waarin het raster al een grote hoeveelheid informatie bevat. De batch‑invoeging die we later uitvoeren moet rekening houden met de nul‑gebaseerde index, dus we vullen vooraf om het exacte invoegpunt te illustreren.

## Stap 2: Gebruik `InsertRowsBatch` om **Meerdere rijen in een raster toe te voegen**

Now the core of the tutorial – the call that actually **adds rows** in bulk. The method signature is `InsertRowsBatch(int startIndex, int count)`. In our example we’ll start at index 2 000 000 (which corresponds to the 2 000 001st row) and add ten rows.

```csharp
        // Step 2 – Insert a batch of rows
        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based, so this is row 2 000 001
            int rowsToAdd = 10;

            // The batch call creates placeholder rows; you can later populate them
            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Verify by reading back a few rows
            VerifyInsertion(grid, startIndex, rowsToAdd);
        }
```

> **Hoe het werkt:** `InsertRowsBatch` reserveert intern het opgegeven aantal rijen en verschuift bestaande rijen naar beneden. Omdat de operatie in één enkele transactie wordt uitgevoerd, wordt de UI slechts één keer ververst, wat de reden is dat deze methode de aanbevolen manier is om **hoe je rijen efficiënt kunt toevoegen**.

## Stap 3: Verifieer de invoeging – Zijn de rijen terechtgekomen waar verwacht?

After the batch operation you’ll want to be sure the rows are where you think they are. The following helper reads the first and last rows of the newly added block and prints them to the console.

```csharp
        // Step 3 – Simple verification
        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

**Verwachte output**

```
Initial seed completed – 2 000 000 rows present.
Inserted 10 rows starting at index 2000001.
Verifying inserted rows:
Row 2000001: , 
Row 2000002: , 
...
Row 2000010: , 
```

De lege cellen geven aan dat de rijen placeholders zijn die wachten op data. Je kunt ze nu individueel vullen of een andere batch‑update uitvoeren.

> **Edge case note:** If `startIndex` exceeds the current row count, GridJs will automatically append the new rows at the end. Conversely, a negative index throws an `ArgumentOutOfRangeException`, so always validate user‑supplied indices.

## Stap 4: Vul de nieuwe rijen (optioneel maar gebruikelijk)

Often you don’t just want empty rows; you need to fill them with meaningful values. You can loop over the newly created range and call `SetCell` or a similar API.

```csharp
        // Optional: fill the newly added rows with sample data
        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }
```

You could call `PopulateNewRows(gridJs, startIndex, rowsToAdd);` right after the batch insert if you need the rows ready for display immediately.

## Stap 5: Prestatietips voor zeer grote rasters

When you’re dealing with **add multiple rows grid** in the millions, keep these tricks in mind:

1. **Batch‑grootte is belangrijk** – Het invoegen van 10 000 rijen in één keer kan sneller zijn dan tien afzonderlijke batches van 1 000 rijen, omdat elke batch één UI‑verversing veroorzaakt.
2. **Schakel UI‑updates uit** – Sommige GridJs‑versies bieden `grid.SuspendLayout()` / `grid.ResumeLayout()`. Wikkel je batch in deze calls als je vertraging opmerkt.
3. **Gebruik virtualisatie** – Zoals eerder getoond, vermindert `EnableVirtualization` de geheugengebruik en render‑tijd drastisch.
4. **Vermijd diepe kopieën** – Geef eenvoudige waarde‑types of lichtgewicht objecten aan het raster; zware objecten dwingen het raster om data te klonen, wat de prestaties schaadt.

## Volledig werkend voorbeeld

Putting everything together, here’s the complete program you can copy‑paste into a new console project:

```csharp
using System;
using GridJsLibrary;   // Replace with the actual namespace of your GridJs library

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            GridJs gridJs = new GridJs
            {
                EnableVirtualization = true
            };

            SeedInitialData(gridJs);
            InsertRowsInBatch(gridJs);
        }

        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }

        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based index for row 2 000 001
            int rowsToAdd = 10;

            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Optional: fill them with data
            PopulateNewRows(grid, startIndex, rowsToAdd);

            VerifyInsertion(grid, startIndex, rowsToAdd);
        }

        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }

        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

Run the program, and you’ll see the console output confirming that the ten rows were inserted at the correct location and then populated.

## Conclusie

We’ve covered **how to insert rows** in GridJs using the batch API, demonstrated **how to add rows** efficiently, and explored ways to **add multiple rows grid** without choking the UI. The key takeaways are:

- Gebruik `InsertRowsBatch(startIndex, count)` voor elke bulk‑operatie.
- Valideer indices en overweeg virtualisatie voor enorme datasets.
- Vul rijen na de batch in als je directe inhoud nodig hebt.

Next, you might want to explore **how to delete rows**, implement **undo/redo** for batch edits, or integrate GridJs with a back‑end service that streams data on demand. All of those topics build directly on the concepts you’ve just learned.

Feel free to experiment—change the batch size, try inserting at the very beginning of the grid, or combine multiple batches in a single transaction. The more you play, the more comfortable you’ll become with large

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}