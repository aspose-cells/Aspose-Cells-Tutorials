---
category: general
date: 2026-03-30
description: Skapa en Excel-arbetsbok i C# med Aspose.Cells. Lär dig att använda lambda‑funktionen
  i Excel, sekvensfunktionen i Excel, expandera array i Excel och spara arbetsboken
  som xlsx.
draft: false
keywords:
- create excel workbook c#
- lambda function excel
- save workbook as xlsx
- sequence function excel
- expand array excel
language: sv
og_description: Skapa en Excel‑arbetsbok i C# snabbt. Den här guiden visar hur du
  använder lambda‑funktionen i Excel, sekvens‑funktionen i Excel, expanderar en array
  i Excel och sparar arbetsboken som xlsx.
og_title: Skapa Excel-arbetsbok C# – Lambda, SEQUENCE & EXPAND-guide
tags:
- Aspose.Cells
- C#
- Excel automation
title: Skapa Excel-arbetsbok C# – Lambda, SEQUENCE & EXPAND-guide
url: /sv/net/formulas-functions/create-excel-workbook-c-lambda-sequence-expand-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel-arbetsbok C# – Lambda, SEQUENCE & EXPAND‑guide

Har du någonsin behövt **skapa Excel-arbetsbok C#** för en automatiserad rapport, men varit osäker på vilka API‑anrop du ska använda? Du är inte ensam—många utvecklare stöter på samma hinder när de först dyker in i programmatisk Excel‑generering. I den här guiden får du ett komplett, körbart exempel som täcker allt från den nya **SEQUENCE‑funktionen i Excel** till den kraftfulla **LAMBDA‑funktionen i Excel**, och även hur du **expanderar array‑resultat i Excel**.  

Vi visar också exakt hur du **sparar arbetsboken som xlsx** så att du kan överlämna filen till vem som helst som använder Excel. I slutet av tutorialen har du ett stabilt, produktionsklart kodsnutt som du kan klistra in i vilket .NET‑projekt som helst. Inga vaga “se dokumentationen”-länkar—bara kod som fungerar idag.

## Vad du behöver

- **.NET 6.0 eller senare** – exemplet riktar sig mot .NET 6, men vilken recent version som helst fungerar.  
- **Aspose.Cells för .NET** – installera via NuGet (`Install-Package Aspose.Cells`).  
- Grundläggande förståelse för C#‑syntax (variabler, objekt och lambda‑uttryck).  
- En IDE du är bekväm med (Visual Studio, Rider eller VS Code).  

Det är allt. Ingen extra COM‑interop, ingen Office‑installation på servern—Aspose.Cells hanterar allt i minnet.

## Skapa Excel-arbetsbok C# – Steg‑för‑steg‑implementation

Nedan delar vi upp processen i lagom stora steg. Varje steg har en tydlig rubrik, ett kort kodexempel och en förklaring av **varför** vi gör det. Kopiera gärna hela blocket i slutet och kör det som en konsolapp.

### Steg 1 – Initiera en ny arbetsbok

Först och främst: vi behöver ett tomt arbetsboksobjekt som representerar Excel‑filen i minnet.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // empty workbook
Worksheet sheet = workbook.Worksheets[0];         // default first sheet
```

*Varför detta är viktigt:* `Workbook` är startpunkten för alla Aspose.Cells‑operationer. Genom att hämta den första `Worksheet` får vi en canvas där vi kan skriva formler, värden eller formatering.  

> **Proffstips:** Om du behöver flera blad, anropa bara `workbook.Worksheets.Add()` och behåll en referens till varje.

### Steg 2 – Använd SEQUENCE‑funktionen i Excel för att generera data

Den **sequence function excel** skapar en dynamisk array av tal utan någon VBA. Vi placerar den i cell `A1` och låter Excel expandera den automatiskt.

```csharp
// Step 2: Generate a 5‑row, 1‑column array from a SEQUENCE
sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)"; // 1..3 padded with blanks
```

*Varför detta är viktigt:* `SEQUENCE(3)` ger `[1,2,3]`. Genom att omsluta den med `EXPAND` tvingas resultatet in i ett 5‑radigt område, där de extra raderna fylls med tomma celler. Detta demonstrerar både **sequence function excel** och **expand array excel** i ett svep.

### Steg 3 – Aggregera tal med LAMBDA‑funktionen i Excel

Nu visar vi **lambda function excel**‑kapaciteten. Vi summerar talen 1‑5 med den nya `REDUCE`‑funktionen, som internt använder en lambda.

```csharp
// Step 3: Aggregate a sequence (sum 1..5) using REDUCE/LAMBDA
sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))"; // result = 15
```

*Varför detta är viktigt:* `REDUCE` itererar över arrayen som produceras av `SEQUENCE(5)`, och matar varje element (`b`) in i lambda‑uttrycket tillsammans med ackumulatorn (`a`). Lambdan `a+b` adderar dem, vilket lämnar `15` i `B1`. Detta är ett rent, formel‑endast sätt att utföra reduceringar utan loopar i C#.

### Steg 4 – Applicera trigonometriska funktioner direkt i celler

Excels inbyggda matematiska funktioner är praktiska för snabba beräkningar. Vi placerar en kotangens och en hyperbolisk kotangens i intilliggande celler.

```csharp
// Step 4: Trigonometric functions directly in Excel cells
sheet["C1"].Formula = "COT(PI()/4)";   // evaluates to 1
sheet["D1"].Formula = "COTH(1)";      // hyperbolic cotangent of 1
```

*Varför detta är viktigt:* Visar att du kan blanda klassiska matematiska funktioner med de nyare dynamiska array‑formlerna. Ingen anledning att beräkna dessa värden i C# om du inte har ett specifikt prestandaskäl.

### Steg 5 – Beräkna alla formler

Aspose.Cells utvärderar inte automatiskt formler när du sätter dem. Du måste be den att beräkna.

```csharp
// Step 5: Force calculation so that cells store the results
workbook.CalculateFormula();
```

*Varför detta är viktigt:* Efter detta anrop innehåller varje cells `Value`‑egenskap det utvärderade resultatet, redo att sparas eller läsas tillbaka.

### Steg 6 – Spara arbetsboken som Xlsx

Till sist persisterar vi arbetsboken till disk med **save workbook as xlsx**‑mönstret.

```csharp
// Step 6: Save the workbook to an Excel file (XLSX format)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "NewFunctions.xlsx");

workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

*Varför detta är viktigt:* `Save`‑metoden upptäcker automatiskt filändelsen. Genom att använda “.xlsx” säkerställer vi att filen är kompatibel med moderna Excel‑versioner. Sökvägen pekar på skrivbordet för enkel åtkomst under testning.

### Fullt fungerande exempel

Nedan är hela programmet som du kan klistra in i ett nytt konsolprojekt. Det innehåller alla stegen ovan, plus ett litet verifieringsblock som skriver ut de beräknade värdena till konsolen.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Initialize workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // SEQUENCE + EXPAND
        sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)";

        // REDUCE with LAMBDA
        sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))";

        // Trig functions
        sheet["C1"].Formula = "COT(PI()/4)";
        sheet["D1"].Formula = "COTH(1)";

        // Calculate formulas
        workbook.CalculateFormula();

        // Verify results (optional)
        Console.WriteLine("A1‑A5 (expanded SEQUENCE):");
        for (int i = 0; i < 5; i++)
        {
            Console.WriteLine($"  Row {i + 1}: {sheet.Cells[i, 0].Value ?? "blank"}");
        }
        Console.WriteLine($"B1 (sum 1‑5): {sheet["B1"].Value}");
        Console.WriteLine($"C1 (cot(π/4)): {sheet["C1"].Value}");
        Console.WriteLine($"D1 (coth(1)): {sheet["D1"].Value}");

        // Save workbook
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "NewFunctions.xlsx");
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

**Förväntad utskrift i konsolen**

```
A1‑A5 (expanded SEQUENCE):
  Row 1: 1
  Row 2: 2
  Row 3: 3
  Row 4: blank
  Row 5: blank
B1 (sum 1‑5): 15
C1 (cot(π/4)): 1
D1 (coth(1)): 1.31303528549933
Workbook saved to: C:\Users\YourName\Desktop\NewFunctions.xlsx
```

Och när du öppnar *NewFunctions.xlsx* ser du samma siffror placerade i de fyra första kolumnerna.

![skärmdump av den resulterande kalkylbladet](/images/create-excel-workbook-csharp.png)

## Edge Cases, Tips och Vanliga Frågor

- **Vad händer om jag behöver mer än ett blad?**  
  Anropa bara `workbook.Worksheets.Add()` och upprepa formel‑tilldelningarna på varje nytt `Worksheet`‑objekt.  

- **Kan jag använda äldre Excel‑versioner?**  
  De dynamiska array‑funktionerna (`SEQUENCE`, `EXPAND`, `REDUCE`) kräver Excel 365 eller Excel 2021+. Om du riktar dig mot äldre versioner, håll dig till klassiska formler eller beräkna värdena i C# innan du skriver dem.  

- **Prestanda‑bekymmer?**  
  För tusentals rader är det vanligtvis snabbare att sätta formler på ett område och sedan anropa `CalculateFormula` än att loopa och tilldela värden en‑och‑en.  

- **Spara till en ström istället för en fil?**  
  `work

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}