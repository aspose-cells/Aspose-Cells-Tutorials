---
category: general
date: 2026-03-22
description: Hur man använder lambda i C# för att arbeta med Excel‑formler. Lär dig
  att skriva formel till en cell, konvertera ett område till en array, visa arrayen
  i konsolen och beräkna cotangens i Excel.
draft: false
keywords:
- how to use lambda
- display array in console
- convert range to array
- write formula to cell
- calculate cotangent in excel
language: sv
og_description: Hur man använder lambda i C# för att manipulera Excel‑formler, konvertera
  område till array, skriva formel till cell, visa array i konsolen och beräkna cotangens
  i Excel.
og_title: Hur man använder Lambda i C# med Excel‑formler – Steg för steg
tags:
- C#
- Aspose.Cells
- Excel Automation
- Lambda Expressions
title: Hur man använder Lambda i C# med Excel‑formler – Komplett guide
url: /sv/net/formulas-functions/how-to-use-lambda-in-c-with-excel-formulas-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder Lambda i C# med Excel-formler – Komplett guide

Har du någonsin undrat **hur man använder lambda** när du automatiserar Excel från C#? Du är inte ensam. Många utvecklare stöter på problem när de måste kombinera kraften i Excels nya dynamiska matrisfunktioner med C#'s `LAMBDA`‑funktionalitet. Den goda nyheten? Det är faktiskt ganska enkelt när du ser hur delarna passar ihop.

I den här handledningen går vi igenom **att skriva en formel till en cell**, **att konvertera ett område till en matris**, **att visa den matrisen i konsolen**, och till och med **att beräkna cotangens i Excel**—allt medan vi visar dig **hur man använder lambda** inuti ett `REDUCE`‑anrop. I slutet har du ett körbart kodexempel som du kan klistra in i vilket .NET‑projekt som helst som refererar till Aspose.Cells (eller ett liknande bibliotek).

---

## Vad du kommer att lära dig

- Hur man **skriver en formel till en cell** med C#.
- Hur man **konverterar ett område till en matris** med `EXPAND`‑funktionen.
- Hur man **visar matrisen i konsolen** efter beräkning.
- Hur man **beräknar cotangens i Excel** med `COT` och `COTH`.
- Den exakta syntaxen för **hur man använder lambda** inuti Excels `REDUCE`‑funktion från C#.

> **Förutsättning:** Du behöver en recent version of .NET (Core 6+ eller .NET Framework 4.7+) och Aspose.Cells for .NET‑biblioteket installerat via NuGet.

## Steg 1: Skapa arbetsboken och skriv formel till cell

Det första vi gör är att skapa en ny arbetsbok och hämta det första kalkylbladet. Sedan **skriver vi en formel till en cell** – i det här fallet kommer `A1` att innehålla resultatet av ett `EXPAND`‑anrop.

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

**Varför detta är viktigt:** Att skriva formeln direkt från koden innebär att du kan generera komplexa kalkylblad på språng utan att någonsin öppna Excel. Det förbereder också nästa steg där vi **konverterar ett område till en matris**.

---

## Steg 2: Konvertera område till matris med EXPAND

`EXPAND` är Excels sätt att omvandla ett litet område till en större matris. Genom att placera formeln i `A1` kommer Excel att spilla ut ett 4 × 5‑block som börjar i den cellen. Från C# behöver vi inte manuellt kopiera värden – biblioteket sköter det tunga arbetet när vi anropar `Calculate`.

```csharp
        // The EXPAND formula will spill into A1:E4 (4 rows × 5 columns)
        // No extra code needed – the workbook will handle the spill.
```

**Hur man använder lambda:** Inte ännu, men håll utkik. Först behöver vi data i bladet, sedan kommer vi att reducera det med en lambda.

## Steg 3: Använd LAMBDA inuti REDUCE – Kärnan i “Hur man använder Lambda”

Excel 365 introducerade `REDUCE`, som accepterar ett **initialt värde**, ett **område** och en **LAMBDA** som talar om hur varje element ska kombineras. Från C# tilldelar vi helt enkelt formelsträngen; lambdan lever i Excel‑formeln, inte i C#‑koden.

```csharp
        // Reduce the spilled array by summing all its values.
        // This demonstrates how to use lambda inside REDUCE.
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";
```

**Förklaring:**  
- `0` är startackumulatorn (`acc`).  
- `A1:D4` är det område vi vill bearbeta (de första fyra kolumnerna av spillen).  
- `LAMBDA(acc, x, acc + x)` talar om för Excel att lägga till varje cell (`x`) till ackumulatorn.  

Det är essensen av **hur man använder lambda** för aggregering i ett kalkylblads‑sammanhang.

## Steg 4: Beräkna cotangens i Excel – Från grader till hyperbolisk

Om du behöver trigonometriska resultat är Excels funktioner `COT` och `COTH` enkla att använda. Vi placerar dem i `G1` respektive `G2`.

```csharp
        // Demonstrate trigonometric functions – cotangent and hyperbolic cotangent
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected result: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";      // Hyperbolic cotangent of 1
```

**Varför detta är praktiskt:** Att veta **hur man beräknar cotangens i Excel** kan spara dig från att skriva egen matematik‑kod, särskilt när arbetsboken ska delas med icke‑utvecklare.

## Steg 5: Tvinga beräkning och hämta den expanderade matrisen

Nu instruerar vi arbetsboken att utvärdera varje formel och sedan hämta den spillade matrisen från `A1`. Det är här vi **visar matrisen i konsolen**.

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

**Vad du kommer att se:**  
- En snyggt formaterad 4 × 5‑matris utskriven rad för rad.  
- Summan beräknad av `REDUCE`‑lambdan.  
- De två cotangensvärdena.

Det avslutar flödet från **skriva formel till cell** hela vägen till **visa matris i konsolen**.

## Fullt fungerande exempel (Klar att kopiera och klistra in)

Nedan är hela programmet som du kan klistra in i en konsolapp. Kom ihåg att först lägga till `Aspose.Cells`‑NuGet‑paketet (`dotnet add package Aspose.Cells`).

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

**Förväntad konsolutdata (värdena kan variera beroende på standardinnehållet i B1:C2, som är 0 som standard):**

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

Känn dig fri att fylla `B1:C2` med egna siffror innan du kör – matrisen kommer att spegla dessa värden.

## Proffstips & vanliga fallgropar

- **Proffstips:** Om du behöver att den spillade matrisen ska börja någon annanstans, ändra bara målcell (`A1`). `EXPAND`‑funktionen respekterar ankaret.
- **Se upp för:** Tomma celler i källområdet blir `0` i den spillade matrisen, vilket kan påverka din `REDUCE`‑summa.
- **Edge case:** När arbetsboken innehåller formler som beror på volatila funktioner (t.ex. `NOW()`), anropa `workbook.Calculate()` efter att alla formler har satts för att säkerställa att allt är uppdaterat.
- **Prestanda‑notering:** För enorma spill, överväg att begränsa storleken i `EXPAND`‑anropet; annars kan du allokera mer minne än nödvändigt.
- **Compatibility:** The `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}