---
category: general
date: 2026-03-30
description: Maak een Excel-werkmap in C# met Aspose.Cells. Leer hoe je de lambda-functie
  in Excel toepast, de sequence-functie in Excel gebruikt, een array in Excel uitbreidt,
  en de werkmap opslaat als xlsx.
draft: false
keywords:
- create excel workbook c#
- lambda function excel
- save workbook as xlsx
- sequence function excel
- expand array excel
language: nl
og_description: Maak snel een Excel-werkmap in C#. Deze gids laat zien hoe je de lambda‑functie
  in Excel, de sequentiefunctie in Excel, de array‑uitbreiding in Excel kunt gebruiken
  en de werkmap als xlsx opslaat.
og_title: Maak Excel-werkmap C# – Lambda, SEQUENCE & EXPAND gids
tags:
- Aspose.Cells
- C#
- Excel automation
title: Excel-werkmap maken in C# – Lambda, SEQUENCE & EXPAND‑gids
url: /nl/net/formulas-functions/create-excel-workbook-c-lambda-sequence-expand-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-werkmap maken C# – Lambda, SEQUENCE & EXPAND gids

Heb je ooit een **Excel-werkmap C#** moeten maken voor een geautomatiseerd rapport, maar wist je niet welke API‑aanroepen je moest gebruiken? Je bent niet de enige—veel ontwikkelaars lopen tegen dezelfde muur aan wanneer ze voor het eerst programmatiche Excel‑generatie proberen. In deze gids zie je een volledig, uitvoerbaar voorbeeld dat alles behandelt, van de nieuwe **SEQUENCE‑functie Excel** tot de krachtige **LAMBDA‑functie Excel**, en zelfs hoe je **array‑resultaten Excel uitbreidt**.  

We laten je ook precies zien hoe je de **werkmap opslaat als xlsx** zodat je het bestand kunt doorgeven aan iedereen die Excel gebruikt. Aan het einde van deze tutorial heb je een solide, productie‑klare snippet die je in elk .NET‑project kunt plaatsen. Geen vage “zie de docs”‑links—alleen code die vandaag werkt.

## Wat je nodig hebt

- **.NET 6.0 of later** – het voorbeeld richt zich op .NET 6, maar elke recente versie werkt.  
- **Aspose.Cells for .NET** – installeer via NuGet (`Install-Package Aspose.Cells`).  
- Een basisbegrip van C#‑syntaxis (variabelen, objecten en lambda‑expressies).  
- Een IDE waar je je prettig bij voelt (Visual Studio, Rider of VS Code).  

Dat is alles. Geen extra COM‑interop, geen Office geïnstalleerd op de server—Aspose.Cells regelt alles in het geheugen.

## Excel-werkmap maken C# – Stapsgewijze implementatie

Hieronder splitsen we het proces op in hapklare stappen. Elke stap heeft een duidelijke kop, een kort code‑fragment en een uitleg **waarom** we het doen. Voel je vrij om het volledige blok aan het einde te kopiëren en als console‑app uit te voeren.

### Stap 1 – Een nieuwe werkmap initialiseren

Allereerst hebben we een lege workbook‑object nodig dat het Excel‑bestand in het geheugen vertegenwoordigt.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // empty workbook
Worksheet sheet = workbook.Worksheets[0];         // default first sheet
```

*Waarom dit belangrijk is:* `Workbook` is het toegangspunt voor alle Aspose.Cells‑bewerkingen. Door het eerste `Worksheet` te pakken, krijgen we een canvas waarop we formules, waarden of opmaak kunnen schrijven.  

> **Pro tip:** Als je meerdere bladen nodig hebt, roep dan gewoon `workbook.Worksheets.Add()` aan en houd een referentie naar elk blad.

### Stap 2 – De SEQUENCE‑functie Excel gebruiken om data te genereren

De **sequence‑function excel** maakt een dynamische array van getallen zonder enige VBA. We plaatsen deze in cel `A1` en laten Excel deze automatisch uitbreiden.

```csharp
// Step 2: Generate a 5‑row, 1‑column array from a SEQUENCE
sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)"; // 1..3 padded with blanks
```

*Waarom dit belangrijk is:* `SEQUENCE(3)` levert `[1,2,3]`. Door het te omhullen met `EXPAND` dwingen we het resultaat naar een bereik van 5 rijen, waarbij de extra rijen leeg blijven. Dit demonstreert zowel **sequence‑function excel** als **expand‑array excel** in één stap.

### Stap 3 – Getallen aggregeren met de LAMBDA‑functie Excel

Laten we nu de mogelijkheden van de **lambda‑function excel** laten zien. We sommeren de getallen 1‑5 met de nieuwe `REDUCE`‑functie, die intern een lambda gebruikt.

```csharp
// Step 3: Aggregate a sequence (sum 1..5) using REDUCE/LAMBDA
sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))"; // result = 15
```

*Waarom dit belangrijk is:* `REDUCE` iterereert over de array die door `SEQUENCE(5)` wordt geproduceerd, en geeft elk element (`b`) samen met de accumulator (`a`) door aan de lambda. De lambda `a+b` telt ze op, waardoor `15` in `B1` terechtkomt. Dit is een nette, alleen‑formule‑manier om reducties uit te voeren zonder te loopen in C#.

### Stap 4 – Trigonometrische functies direct in cellen toepassen

De ingebouwde wiskundige functies van Excel zijn handig voor snelle berekeningen. We plaatsen een cotangens en een hyperbolische cotangens in aangrenzende cellen.

```csharp
// Step 4: Trigonometric functions directly in Excel cells
sheet["C1"].Formula = "COT(PI()/4)";   // evaluates to 1
sheet["D1"].Formula = "COTH(1)";      // hyperbolic cotangent of 1
```

*Waarom dit belangrijk is:* Laat zien dat je klassieke wiskundige functies kunt combineren met de nieuwere dynamische‑array‑formules. Geen noodzaak om deze waarden in C# te berekenen, tenzij je een specifieke prestatie‑reden hebt.

### Stap 5 – Alle formules berekenen

Aspose.Cells evalueert formules niet automatisch wanneer je ze instelt. Je moet het expliciet vragen om te berekenen.

```csharp
// Step 5: Force calculation so that cells store the results
workbook.CalculateFormula();
```

*Waarom dit belangrijk is:* Na deze aanroep bevat de `Value`‑eigenschap van elke cel het berekende resultaat, klaar om opgeslagen of opnieuw gelezen te worden.

### Stap 6 – De werkmap opslaan als Xlsx

Tot slot slaan we de werkmap op schijf op met het **save workbook as xlsx**‑patroon.

```csharp
// Step 6: Save the workbook to an Excel file (XLSX format)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "NewFunctions.xlsx");

workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

*Waarom dit belangrijk is:* De `Save`‑methode detecteert automatisch de bestandsextensie. Door “.xlsx” te gebruiken, zorgen we ervoor dat het bestand compatibel is met moderne Excel‑versies. Het pad wijst naar het bureaublad voor gemakkelijke toegang tijdens het testen.

### Volledig werkend voorbeeld

Hieronder staat het complete programma dat je in een nieuw console‑project kunt plakken. Het bevat alle bovenstaande stappen, plus een klein verificatie‑blok dat de berekende waarden naar de console schrijft.

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

**Verwachte uitvoer in de console**

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

En wanneer je *NewFunctions.xlsx* opent, zie je dezelfde cijfers in de eerste vier kolommen.

![screenshot van de resulterende spreadsheet van het maken van een Excel-werkmap c#](/images/create-excel-workbook-csharp.png)

## Randgevallen, tips en veelgestelde vragen

- **Wat als ik meer dan één blad nodig heb?**  
  Roep gewoon `workbook.Worksheets.Add()` aan en herhaal de formule‑toewijzingen op elk nieuw `Worksheet`‑object.  

- **Kan ik oudere Excel‑versies gebruiken?**  
  De dynamische‑array‑functies (`SEQUENCE`, `EXPAND`, `REDUCE`) vereisen Excel 365 of Excel 2021+. Als je oudere versies target, blijf dan bij klassieke formules of bereken de waarden in C# voordat je ze schrijft.  

- **Prestatiezorgen?**  
  Voor duizenden rijen is het meestal sneller om formules op een bereik in te stellen en vervolgens `CalculateFormula` aan te roepen dan om één‑voor‑één te loopen en waarden toe te wijzen.  

- **Opslaan naar een stream in plaats van een bestand?**  
  `work

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}