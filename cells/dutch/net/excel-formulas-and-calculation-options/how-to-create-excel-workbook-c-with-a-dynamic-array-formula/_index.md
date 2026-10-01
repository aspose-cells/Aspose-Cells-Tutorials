---
category: general
date: 2026-10-01
description: Maak snel een Excel-werkmap in C# en leer een voorbeeld van een dynamische
  arrayformule om Excel-formules in C# te schrijven met Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- dynamic array formula example
- write excel formula c#
language: nl
lastmod: 2026-10-01
og_description: Maak snel een Excel‑werkmap in C# en bekijk een voorbeeld van een
  dynamische array‑formule die laat zien hoe je een Excel‑formule in C# schrijft met
  Aspose.Cells. Volg de stapsgewijze handleiding om het bestand te genereren, te berekenen
  en op te slaan.
og_image_alt: Screenshot of C# code creating an Excel workbook and applying a SORT
  dynamic array formula
og_title: Maak Excel-werkmap C# met dynamische arrayformule
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create Excel workbook C# quickly and learn a dynamic array formula
    example to write Excel formula C# in Aspose.Cells.
  headline: How to create Excel workbook C# with a dynamic array formula
  type: TechArticle
- description: Create Excel workbook C# quickly and learn a dynamic array formula
    example to write Excel formula C# in Aspose.Cells.
  name: How to create Excel workbook C# with a dynamic array formula
  steps:
  - name: Verifying the result (expected output)
    text: 'You can print the spilled values to the console to confirm the calculation
      succeeded:'
  - name: What if I need to use a different dynamic array function?
    text: 'Replace the formula string with any other dynamic array function, such
      as `=FILTER(A2:A10, B2:B10>10)` or `=UNIQUE(A2:A10)`. The same **write Excel
      formula C#** pattern applies:'
  - name: How do I handle formulas that reference other worksheets?
    text: 'Reference another sheet by its name:'
  - name: Can I suppress automatic calculation and calculate later?
    text: 'Yes. Set the workbook’s calculation mode to manual:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hoe maak je een Excel‑werkmap in C# met een dynamische arrayformule
url: /nl/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een Excel-werkmap C# te maken met een dynamische arrayformule

Als je **create Excel workbook C#** programmatically moet maken, laat deze gids je precies zien hoe je dat doet met Aspose.Cells. Je krijgt ook een **dynamic array formula example** die laat zien hoe je **write Excel formula C#** voor moderne Excel-functies zoals `SORT` het beste kunt schrijven.

Een Excel‑bestand maken vanuit C# vereiste vroeger COM‑interop of handmatige XML‑generatie, beide zijn fragiel en moeilijk te onderhouden. Aan het einde van deze tutorial heb je een volledig functionele werkmap die automatisch een dynamische array berekent, en begrijp je waarom deze aanpak betrouwbaar is voor productie‑grade automatisering.

## Vereisten

- .NET 6.0 of later geïnstalleerd (de code werkt ook met .NET Core en .NET Framework)
- Een geldige Aspose.Cells‑licentie of een gratis evaluatiesleutel
- Visual Studio 2022 (of een IDE die C# ondersteunt)
- Basiskennis van C#‑syntaxis en Excel‑formules

Er zijn geen extra NuGet‑pakketten vereist naast `Aspose.Cells`, die je kunt toevoegen met:

```bash
dotnet add package Aspose.Cells
```

## Stap 1: Het C#‑project instellen en Aspose.Cells refereren

Maak een nieuwe console‑applicatie en voeg de Aspose.Cells‑referentie toe. Deze stap is essentieel omdat de bibliotheek de `Workbook`, `Worksheet` en reken‑engine levert die je nodig hebt om **write Excel formula C#** code te schrijven.

```csharp
// Program.cs
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // The rest of the tutorial code lives inside this method.
    }
}
```

> **Waarom dit belangrijk is:** Aspose.Cells abstraheert de low‑level OpenXML‑details, zodat je je kunt concentreren op de bedrijfslogica in plaats van op eigenaardigheden van het bestandsformaat.

## Stap 2: De Excel‑werkmap maken en het eerste werkblad verkrijgen

Nu **create Excel workbook C#** door een `Workbook`‑object te instantieren. De standaard werkmap bevat één werkblad, dat we ophalen voor verdere bewerkingen.

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates a blank .xlsx file in memory
Worksheet worksheet = workbook.Worksheets[0];    // first (and only) sheet by default
```

> **Pro tip:** Als je meerdere bladen nodig hebt, roep dan `workbook.Worksheets.Add()` aan voordat je ze benadert.

## Stap 3: Brongegevens voor de dynamische array vullen

Dynamische array‑functies zoals `SORT` vereisen een bronbereik. Laten we de cellen *A2:A10* vullen met onsorterde getallen zodat de `SORT`‑formule zijn gedrag kan demonstreren.

```csharp
// Step 3: Fill A2:A10 with sample data
int[] numbers = { 42, 7, 19, 33, 5, 27, 14, 8, 21 };
for (int i = 0; i < numbers.Length; i++)
{
    worksheet.Cells[i + 1, 0].PutValue(numbers[i]); // Row i+2, Column A (0‑based index)
}
```

> **Waarom we dit doen:** Het leveren van concrete gegevens laat je de **dynamic array formula example** in actie zien zonder externe invoerbestanden nodig te hebben.

## Stap 4: De dynamische array‑formule in cel A1 schrijven

Hier is de kern van het **write Excel formula C#**‑gedeelte. We wijzen een `SORT`‑formule toe aan cel *A1*. Omdat `SORT` een dynamische array‑functie is, zal Excel automatisch de gesorteerde resultaten naar de onderliggende cellen laten uitvloeien.

```csharp
// Step 4: Insert a dynamic array formula (SORT) into cell A1
worksheet.Cells[0, 0].Formula = "=SORT(A2:A10)";
```

> **Uitleg:**  
> - `worksheet.Cells[0, 0]` richt zich op cel **A1** (rij 0, kolom 0).  
> - De string `=SORT(A2:A10)` is een standaard Excel‑formule. Aspose.Cells parseert deze op dezelfde manier als Excel, waardoor volledige ondersteuning voor moderne dynamische array‑functies mogelijk is.

## Stap 5: De werkmap opnieuw berekenen zodat de formule automatisch wordt ingevuld

Aspose.Cells berekent formules niet automatisch bij het schrijven. Je moet expliciet de berekening activeren om de uitgevloeide resultaten te zien.

```csharp
// Step 5: Recalculate the workbook so the formula evaluates
workbook.Calculate();   // runs the calculation engine once
```

Na deze oproep zullen cellen **A1:A9** de gesorteerde lijst bevatten: 5, 7, 8, 14, 19, 21, 27, 33, 42.

### Het resultaat verifiëren (verwachte output)

Je kunt de uitgevloeide waarden naar de console afdrukken om te bevestigen dat de berekening geslaagd is:

```csharp
Console.WriteLine("Sorted values from A1 down:");
for (int row = 0; row < 9; row++)
{
    Console.WriteLine(worksheet.Cells[row, 0].StringValue);
}
```

**Verwachte console‑output**

```
Sorted values from A1 down:
5
7
8
14
19
21
27
33
42
```

> **Opmerking voor randgevallen:** Als het bronbereik niet‑numerieke gegevens bevat, zal `SORT` lexicografisch sorteren. Valideer altijd datatypes voordat je alleen‑numerieke functies toepast.

## Stap 6: De werkmap opslaan op schijf (optioneel)

Het opslaan van het bestand stelt je in staat het in Excel te openen en de dynamische array visueel te zien. Deze stap is niet vereist voor de berekening zelf, maar is nuttig voor debugging en distributie.

```csharp
// Step 6: Save the workbook as an .xlsx file
string outputPath = "SortedNumbers.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Wanneer je *SortedNumbers.xlsx* opent in Excel 365 of later, zie je de gesorteerde lijst automatisch uitvloeien vanaf **A1** naar beneden — precies wat de **dynamic array formula example** uit C# heeft geproduceerd.

## Volledig werkend voorbeeld

Alle onderdelen samenvoegend, hier is het volledige, uitvoerbare programma:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1. Create workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2. Fill source data (A2:A10)
        int[] numbers = { 42, 7, 19, 33, 5, 27, 14, 8, 21 };
        for (int i = 0; i < numbers.Length; i++)
        {
            worksheet.Cells[i + 1, 0].PutValue(numbers[i]); // A2:A10
        }

        // 3. Write dynamic array formula (SORT) into A1
        worksheet.Cells[0, 0].Formula = "=SORT(A2:A10)";

        // 4. Force calculation so the array spills
        workbook.Calculate();

        // 5. Display the spilled values in the console
        Console.WriteLine("Sorted values from A1 down:");
        for (int row = 0; row < 9; row++)
        {
            Console.WriteLine(worksheet.Cells[row, 0].StringValue);
        }

        // 6. Save the workbook (optional)
        string outputPath = "SortedNumbers.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Voer het programma uit (`dotnet run`) en je ziet de gesorteerde getallen afgedrukt, gevolgd door een bevestiging dat het bestand is opgeslagen.

## Veelgestelde vragen en variaties

### Wat als ik een andere dynamische array‑functie moet gebruiken?

Vervang de formule‑string door een andere dynamische array‑functie, zoals `=FILTER(A2:A10, B2:B10>10)` of `=UNIQUE(A2:A10)`. Hetzelfde **write Excel formula C#**‑patroon is van toepassing:

```csharp
worksheet.Cells[0, 0].Formula = "=UNIQUE(A2:A10)";
```

### Hoe ga ik om met formules die naar andere werkbladen verwijzen?

Verwijs naar een ander blad via de naam:

```csharp
worksheet.Cells[0, 0].Formula = "=SORT('Sheet2'!A2:A10)";
```

Aspose.Cells lostt kruis‑blad‑referenties automatisch op tijdens `workbook.Calculate()`.

### Kan ik automatische berekening onderdrukken en later berekenen?

Ja. Stel de berekeningsmodus van de werkmap in op handmatig:

```csharp
workbook.Settings.CalcMode = CalcMode.Manual;
// ... make many changes ...
workbook.Calculate(); // call once when ready
```

Dit verbetert de prestaties wanneer je duizenden cellen bijwerkt vóór een definitieve berekening.

## Conclusie

Je weet nu hoe je **create Excel workbook C#** kunt gebruiken met Aspose.Cells, een **dynamic array formula example** kunt invoegen, en **write Excel formula C#** kunt schrijven die automatisch resultaten uitvloeit. De volledige oplossing omvat projectconfiguratie, gegevensvoorbereiding, formule‑invoeging, geforceerde berekening, verificatie en optioneel opslaan van het bestand.

Vanaf hier kun je meer geavanceerde scenario's verkennen: meerdere dynamische array‑functies combineren, aangepaste getalformaten toepassen, of de werkmapgeneratie integreren in een web‑API. Vergeet niet altijd invoergegevens te valideren voordat je formules toepast, en maak gebruik van de rijke reken‑engine van Aspose.Cells voor betrouwbare server‑side Excel‑verwerking. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Create New Workbook in C# – Add Formula and Save Excel File](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Excel Automation with Aspose.Cells .NET: Mastering Workbook & Formula Calculations](/cells/english/net/formulas-functions/excel-automation-aspose-cells-net-workbook-formulas/)
- [Create Excel Workbook C# – Complete Guide with Aspose.Cells](/cells/english/net/excel-workbook/create-excel-workbook-c-complete-guide-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}