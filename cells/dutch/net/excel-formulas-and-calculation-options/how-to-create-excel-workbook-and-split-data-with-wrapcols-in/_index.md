---
category: general
date: 2026-10-10
description: Maak een Excel‑werkmap in C# en gebruik de WRAPCOLS‑functie om array‑gegevens
  in kolommen te splitsen. Volg een volledige stap‑voor‑stap‑handleiding met uitvoerbare
  code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: nl
lastmod: 2026-10-10
og_description: Maak een Excel-werkmap in C# en pas de WRAPCOLS-functie toe om arraygegevens
  over kolommen te verdelen. Deze gids toont de volledige code en legt elke stap uit.
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: Maak een Excel-werkmap en splits gegevens met WRAPCOLS in C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  headline: How to create Excel workbook and split data with WRAPCOLS in C#
  type: TechArticle
- description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  name: How to create Excel workbook and split data with WRAPCOLS in C#
  steps:
  - name: Using the function with different data types
    text: 'The `WRAPCOLS` function is not limited to numbers. You can split text values,
      dates, or mixed types:'
  - name: Variable column count at runtime
    text: 'Often the number of columns you need depends on user input. You can build
      the formula string dynamically:'
  - name: Large arrays and performance
    text: '`WRAPCOLS` can handle thousands of elements, but evaluating extremely large
      arrays in a single cell may increase calculation time. If you notice slowdown:'
  - name: Handling empty cells
    text: If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS`
      inserts blank cells, preserving the column layout. This behavior is useful when
      you need placeholder columns for later data entry.
  - name: Using named ranges instead of literals
    text: 'For maintainability, define a named range that holds the source data, then
      reference it:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hoe een Excel-werkmap te maken en gegevens te splitsen met WRAPCOLS in C#
url: /nl/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een Excel‑werkmap te maken en gegevens te splitsen met WRAPCOLS in C#

Als je **een Excel‑werkmap** programmatisch wilt **maken**, laat deze gids je precies zien hoe je dat doet en hoe je **array‑gegevens** over kolommen kunt **splitsen** met de `WRAPCOLS`‑functie. Je krijgt een volledig, uitvoerbaar voorbeeld dat een `.xlsx`‑bestand produceert met de gegevens verdeeld over drie kolommen.

De tutorial behandelt alles wat je nodig hebt: vereiste NuGet‑pakketten, elke regel code, waarom de `WRAPCOLS`‑formule werkt, en hoe je de oplossing kunt aanpassen voor verschillende array‑groottes of kolomaantallen. Aan het einde kun je de **use wrapcols function**‑techniek in elk C#‑project dat Excel‑bestanden genereert, integreren.

## Vereisten

Voordat je begint, zorg dat je het volgende hebt:

* .NET 6.0 SDK of later geïnstalleerd  
* Een C#‑IDE (Visual Studio, VS Code, Rider, etc.)  
* Het **Aspose.Cells for .NET** NuGet‑pakket – de bibliotheek die de `Workbook`‑klasse levert die in de voorbeelden wordt gebruikt  

Je hebt geen Office‑installatie nodig; Aspose.Cells schrijft het `.xlsx`‑bestand direct.

## Stap 1 – Excel‑werkmap maken

De eerste taak is om een nieuw workbook‑object te instantieren en een referentie naar het eerste werkblad te verkrijgen. Deze stap vormt de basis voor elke verdere manipulatie.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();                // creates an empty Excel file in memory
        Worksheet ws = wb.Worksheets[0];             // the default worksheet is at index 0
```

`Workbook` vertegenwoordigt het volledige bestand, terwijl `Worksheet` een enkel blad vertegenwoordigt. Door het workbook in het geheugen te maken, vermijd je schijf‑I/O totdat je het expliciet opslaat.

## Stap 2 – WRAPCOLS toepassen om array‑kolommen te splitsen

Nu plaats je een formule in cel **A1** die `WRAPCOLS` gebruikt. De functie ontvangt twee argumenten: de bron‑array en het aantal kolommen waarin je de array wilt laten wikkelen.

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**Waarom dit werkt:** `WRAPCOLS` neemt de platte array `{1,2,3,4,5,6}` en vult het werkblad rij‑voor‑rij, waarbij drie kolommen per rij worden aangemaakt. Het eerste argument kan elke Excel‑array‑literal, een benoemd bereik of een dynamische array‑formule zijn. Het tweede argument (`3`) vertelt Excel hoeveel kolommen er moeten worden gegenereerd voordat naar de volgende rij wordt gegaan.

### De functie gebruiken met verschillende gegevenstypen

De `WRAPCOLS`‑functie is niet beperkt tot getallen. Je kunt tekstwaarden, datums of gemengde typen splitsen:

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

Wanneer de bron‑array strings bevat, behandelt Excel het resultaat automatisch als tekstcellen. Deze flexibiliteit stelt je in staat **excel formula split data** te gebruiken voor rapportages, dashboards of data‑migratietaken.

## Stap 3 – Formules berekenen zodat het werkblad wordt gevuld

Formules worden opgeslagen als strings totdat je het workbook vraagt ze te evalueren. Het aanroepen van `CalculateFormula` dwingt de evaluatie af en schrijft de resultaten in de cellen.

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

Zonder deze aanroep zou het opgeslagen bestand alleen de formule‑tekst bevatten, niet de berekende waarden. De methode werkt over het hele workbook, zodat je extra formules elders kunt plaatsen en ze allemaal met één aanroep worden opgelost.

## Stap 4 – Het workbook opslaan om het resultaat te zien

Schrijf tenslotte het workbook naar schijf. Kies een map waarin je schrijfrechten hebt, en geef het bestand een duidelijke naam.

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

Wanneer je `output.xlsx` opent in Excel (of een compatibele viewer), zie je:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

Als je het voorbeeld met gemengde typen hebt gebruikt, zouden rijen 3‑4 respectievelijk de tekst en cijfers bevatten.

## Geavanceerde variaties en afhandeling van randgevallen

### Variabel aantal kolommen tijdens runtime

Vaak hangt het aantal benodigde kolommen af van gebruikersinvoer. Je kunt de formule‑string dynamisch opbouwen:

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### Grote arrays en prestaties

`WRAPCOLS` kan duizenden elementen aan, maar het evalueren van extreem grote arrays in één cel kan de rekentijd verhogen. Als je een vertraging merkt:

* Splits de bron‑array in kleinere delen en schrijf elk deel naar een aparte startcel.  
* Gebruik `WorkbookSettings` om multithreaded berekening in te schakelen:

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### Lege cellen afhandelen

Als de bron‑array lege strings (`""`) of `NULL`‑waarden bevat, voegt `WRAPCOLS` lege cellen in, waardoor de kolomlay-out behouden blijft. Dit gedrag is handig wanneer je placeholder‑kolommen nodig hebt voor latere gegevensinvoer.

### Benoemde bereiken gebruiken in plaats van literals

Voor onderhoudbaarheid kun je een benoemd bereik definiëren dat de bron‑data bevat, en dat vervolgens refereren:

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

Nu leest de formule data uit het werkblad zelf, waardoor **how to use wrapcols** in dynamische rapportagescenario's mogelijk wordt.

## Veelvoorkomende valkuilen en pro‑tips

* **Laat het tweede argument niet weg.** `WRAPCOLS(array)` zonder kolomaantal geeft één kolom terug, waardoor het doel van het splitsen van gegevens teniet wordt gedaan.  
* **Vermijd het mengen van array‑dimensies.** De bron‑array moet één‑dimensioneel zijn; een twee‑dimensionele array (bijv. `{ {1,2},{3,4} }`) veroorzaakt een `#VALUE!`‑fout.  
* **Sla op na berekening.** Als je `wb.Save` aanroept vóór `CalculateFormula`, bevat het bestand alleen de formule‑tekst.  
* **Controleer bestandsrechten.** Wanneer je in een beperkte omgeving draait (bijv. ASP.NET), zorg dan dat de proces‑identiteit naar de doelmap kan schrijven.  

## Volledig werkend voorbeeld

Hieronder staat het complete programma dat je kunt kopiëren, plakken en uitvoeren. Het bevat alle imports, foutafhandeling en commentaar.

```csharp
using System;
using Aspose.Cells;

class ExcelWrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Split a numeric array into 3 columns
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

        // Split a mixed array (text + numbers) into 3 columns, starting at row 3
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";

        // Dynamically build a formula with a variable column count
        int columnCount = 4;
        string sourceArray = "{10,20,30,40,50,60,70,80}";
        ws.Cells[5, 0].Formula = $"=WRAPCOLS({sourceArray},{columnCount})";

        // Evaluate all formulas
        wb.CalculateFormula();

        // Save the workbook
        string outputPath = "output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Het uitvoeren van het programma produceert `output.xlsx` met drie afzonderlijke gebieden die **excel formula split data** demonstreren met de `WRAPCOLS`‑functie.

## Conclusie

Je weet nu hoe je **Excel‑werkmap**‑bestanden in C# kunt **maken** en hoe je de **use wrapcols function** kunt **gebruiken om array‑kolommen** efficiënt te **splitsen**. De belangrijkste stappen — het instantieren van `Workbook`, het invoegen van de `WRAPCOLS`‑formule, berekenen en opslaan — vormen een herbruikbaar patroon voor elke automatiseringstaak die gegevens over kolommen moet verdelen.

Vanaf hier kun je:

* `WRAPCOLS` combineren met andere dynamische‑array‑functies zoals `FILTER` of `SORT`.  
* Grote datasets uit databases exporteren en Excel de lay‑out automatisch laten afhandelen.  
* Gebruikersgestuurde rapporten bouwen waarbij het aantal kolommen wordt gekozen via een UI‑controle.

Experimenteer met verschillende array‑bronnen, kolomaantallen en extra formules om deze basis uit te breiden. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Create Excel Workbook – Convert Array to Matrix with WRAPCOLS](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [Create Excel Workbook C# – Step‑by‑Step Guide](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}