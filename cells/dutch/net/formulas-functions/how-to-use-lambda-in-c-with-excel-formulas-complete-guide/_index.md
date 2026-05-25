---
category: general
date: 2026-03-22
description: Hoe lambda te gebruiken in C# om met Excel‑formules te werken. Leer een
  formule naar een cel te schrijven, een bereik naar een array te converteren, de
  array in de console weer te geven en de cotangens in Excel te berekenen.
draft: false
keywords:
- how to use lambda
- display array in console
- convert range to array
- write formula to cell
- calculate cotangent in excel
language: nl
og_description: Hoe lambda te gebruiken in C# om Excel‑formules te manipuleren, een
  bereik naar een array te converteren, een formule naar een cel te schrijven, een
  array in de console weer te geven en cotangens te berekenen in Excel.
og_title: Hoe Lambda te gebruiken in C# met Excel‑formules – Stap voor stap
tags:
- C#
- Aspose.Cells
- Excel Automation
- Lambda Expressions
title: Hoe Lambda in C# te gebruiken met Excel‑formules – Complete gids
url: /nl/net/formulas-functions/how-to-use-lambda-in-c-with-excel-formulas-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Lambda te Gebruiken in C# met Excel‑formules – Complete Gids

Heb je je ooit afgevraagd **hoe je lambda kunt gebruiken** wanneer je Excel automatiseert vanuit C#? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze de kracht van Excel’s nieuwe dynamische matrixfuncties moeten combineren met de `LAMBDA`‑mogelijkheid van C#. Het goede nieuws? Het is eigenlijk best eenvoudig zodra je ziet hoe de onderdelen in elkaar passen.

In deze tutorial lopen we door **een formule naar een cel schrijven**, **een bereik omzetten naar een array**, **die array in de console weergeven**, en zelfs **cotangens berekenen in Excel** — allemaal terwijl we je **laten zien hoe je lambda kunt gebruiken** binnen een `REDUCE`‑aanroep. Aan het einde heb je een uitvoerbare snippet die je in elk .NET‑project kunt plaatsen dat Aspose.Cells (of een vergelijkbare bibliotheek) referereert.

---

## Wat je zult leren

- Hoe je **een formule naar een cel schrijft** met C#.
- Hoe je **een bereik omzet naar een array** met de `EXPAND`‑functie.
- Hoe je **een array in de console weergeeft** na berekening.
- Hoe je **cotangens berekent in Excel** met `COT` en `COTH`.
- De exacte syntaxis voor **hoe je lambda kunt gebruiken** binnen Excel’s `REDUCE`‑functie vanuit C#.

> **Prerequisite:** Je hebt een recente versie van .NET (Core 6+ of .NET Framework 4.7+) en de Aspose.Cells for .NET‑bibliotheek geïnstalleerd via NuGet nodig.

---

## Stap 1: Het Werkboek Instellen en Formule naar Cel Schrijven

Het eerste wat we doen is een nieuw werkboek aanmaken en het eerste werkblad ophalen. Vervolgens **schrijven we een formule naar een cel** – in dit geval zal `A1` het resultaat van een `EXPAND`‑aanroep bevatten.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write formula to A1 – we’ll expand B1:C2 into a 4‑by‑5 array later
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";
```

**Waarom dit belangrijk is:** De formule direct vanuit code schrijven betekent dat je complexe spreadsheets on‑the‑fly kunt genereren zonder Excel te openen. Het legt ook de basis voor de volgende stap waarin we **een bereik omzetten naar een array**.

---

## Stap 2: Bereik Omzetten naar Array met EXPAND

`EXPAND` is Excel’s manier om een klein bereik om te zetten in een grotere matrix. Door de formule in `A1` te plaatsen, zal Excel een 4 × 5‑blok laten “spillen” vanaf die cel. Vanuit C# hoeven we de waarden niet handmatig te kopiëren – de bibliotheek doet het zware werk wanneer we `Calculate` aanroepen.

```csharp
        // The EXPAND formula will spill into A1:E4 (4 rows × 5 columns)
        // No extra code needed – the workbook will handle the spill.
```

**Hoe je lambda gebruikt:** Nog niet, maar blijf kijken. Eerst hebben we de data in het blad nodig, daarna reduceren we het met een lambda.

---

## Stap 3: LAMBDA Binnen REDUCE Gebruiken – De Kern van “Hoe Lambda te Gebruiken”

Excel 365 introduceerde `REDUCE`, dat een **beginwaarde**, een **bereik**, en een **LAMBDA** accepteert die bepaalt hoe elk element gecombineerd wordt. Vanuit C# wijzen we simpelweg de formule‑string toe; de lambda zit in de Excel‑formule, niet in de C#‑code.

```csharp
        // Reduce the spilled array by summing all its values.
        // This demonstrates how to use lambda inside REDUCE.
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";
```

**Uitleg:**  
- `0` is de start‑accumulator (`acc`).  
- `A1:D4` is het bereik dat we willen verwerken (de eerste vier kolommen van de spill).  
- `LAMBDA(acc, x, acc + x)` vertelt Excel elk cel‑waarde (`x`) bij de accumulator op te tellen.  

Dat is de essentie van **hoe je lambda kunt gebruiken** voor aggregatie in een spreadsheet‑context.

---

## Stap 4: Cotangens Berekenen in Excel – Van Graden naar Hyperbolisch

Als je trigonometrische resultaten nodig hebt, zijn Excel’s `COT`‑ en `COTH`‑functies een makkie. We plaatsen ze respectievelijk in `G1` en `G2`.

```csharp
        // Demonstrate trigonometric functions – cotangent and hyperbolic cotangent
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected result: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";      // Hyperbolic cotangent of 1
```

**Waarom dit handig is:** Weten **hoe je cotangens berekent in Excel** kan je veel eigen wiskundige code besparen, vooral wanneer het werkboek gedeeld wordt met niet‑ontwikkelaars.

---

## Stap 5: Berekening Forceren en de Uitgebreide Array Ophalen

Nu laten we het werkboek alle formules evalueren en halen we de gespilde array uit `A1`. Dit is het moment waarop we **de array in de console weergeven**.

```csharp
        // Force calculation of all formulas
        workbook.Calculate();

        // Retrieve the spilled array from A1 as a 2‑D object
        var expanded = worksheet.Cells["A1"].Value;

        // Pretty‑print the 2‑D array to the console
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show the result of the REDUCE lambda
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Wat je zult zien:**  
- Een netjes geformatteerde 4 × 5‑matrix, regel voor regel afgedrukt.  
- De som berekend door de `REDUCE`‑lambda.  
- De twee cotangens‑waarden.

Dat voltooit de stroom van **formule naar cel schrijven** tot **array in de console weergeven**.

---

## Volledig Werkend Voorbeeld (Klaar om te Kopiëren)

Hieronder staat het volledige programma dat je in een console‑app kunt plakken. Vergeet niet eerst het `Aspose.Cells`‑NuGet‑pakket toe te voegen (`dotnet add package Aspose.Cells`).

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write EXPAND formula (convert range to array)
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";

        // Step 3: Use REDUCE with LAMBDA (how to use lambda)
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";

        // Step 4: Calculate cotangent values (calculate cotangent in excel)
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";

        // Step 5: Force calculation
        workbook.Calculate();

        // Step 6: Retrieve and display the expanded array (display array in console)
        var expanded = worksheet.Cells["A1"].Value;
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show REDUCE result
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Verwachte console‑output (waarden kunnen variëren afhankelijk van de standaardinhoud van B1:C2, die standaard 0 is):**

```
Expanded array from A1 (4×5):
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0

Sum of A1:D4 (via REDUCE lambda): 0
Cotangent of π/4: 1
Hyperbolic cotangent of 1: 1.31303528549933
```

Voel je vrij om `B1:C2` te vullen met je eigen getallen vóór je het programma draait – de matrix zal die waarden weerspiegelen.

---

## Pro‑tips & Veelvoorkomende Valkuilen

- **Pro tip:** Als je wilt dat het gespilde bereik ergens anders begint, wijzig dan simpelweg de doelcel (`A1`). De `EXPAND`‑functie houdt rekening met de ankerpositie.  
- **Let op:** Lege cellen in het bronbereik worden `0` in de gespilde array, wat je `REDUCE`‑som kan beïnvloeden.  
- **Randgeval:** Wanneer het werkboek formules bevat die afhankelijk zijn van vluchtige functies (bijv. `NOW()`), roep dan `workbook.Calculate()` aan nadat alle formules zijn ingesteld om alles up‑to‑date te houden.  
- **Prestatie‑opmerking:** Voor enorme spills, overweeg de grootte in de `EXPAND`‑aanroep te beperken; anders kun je meer geheugen reserveren dan nodig is.  
- **Compatibiliteit:** The `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}