---
category: general
date: 2026-02-21
description: Maak snel een celstijl in C#. Leer hoe je een stijl op een cel toepast,
  tekst in een cel centreert, de uitlijning van een cel instelt en celopmaak onder
  de knie krijgt.
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: nl
og_description: Maak een celstijl in C# en leer hoe je een stijl op een cel toepast,
  tekst in een cel centreert en de celuitlijning instelt met een duidelijke stap‑voor‑stap‑gids.
og_title: Maak celstijl in C# – Pas stijl toe op een cel en centreer tekst
tags:
- C#
- Aspose.Cells
- Excel automation
title: Celstijl maken in C# – Hoe een stijl toepassen op een cel en tekst centreren
url: /nl/net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Celstijl maken in C# – Complete gids voor het toepassen van stijlen en het centreren van tekst

Heb je ooit moeten **create cell style** in een Excel-werkblad, maar wist je niet waar te beginnen? Je bent niet de enige. In veel automatiseringsprojecten is de mogelijkheid om **apply style to cell** objecten te gebruiken het verschil tussen een saai spreadsheet en een gepolijst rapport.  

In deze tutorial lopen we een volledig, uitvoerbaar voorbeeld door dat je laat zien **how to center text** binnen een cel, de uitlijning instelt en een dunne rand toevoegt — allemaal in slechts een paar regels C#. Aan het einde weet je precies waarom elk onderdeel belangrijk is en hoe je het kunt aanpassen voor je eigen scenario's.

## Wat je zult meenemen

- Een duidelijk begrip van de **create cell style** workflow met Aspose.Cells (of een vergelijkbare bibliotheek).
- De exacte code die je kunt copy‑paste in een console‑app om **apply style to cell**.
- Inzicht in **center text in cell**, **set cell alignment**, en het omgaan met randgevallen zoals samengevoegde cellen of aangepaste getalformaten.
- Tips om de stijl uit te breiden—verschillende lettertypen, achtergrondkleuren of voorwaardelijke opmaak.

> **Voorvereiste:** Visual Studio 2022 (of een andere C# IDE) en het Aspose.Cells for .NET NuGet‑pakket. Geen andere afhankelijkheden zijn vereist.

---

## Stap 1: Stel je project in en importeer namespaces

Voordat we **create cell style** kunnen uitvoeren, hebben we een project nodig dat naar de Excel‑bibliotheek verwijst.

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*Waarom dit belangrijk is:* Het importeren van `Aspose.Cells` geeft ons toegang tot de `Workbook`, `Worksheet`, `Style` en `Border` klassen. Als je een andere bibliotheek gebruikt (bijv. EPPlus), veranderen de klassennamen, maar het concept blijft hetzelfde.

---

## Stap 2: Maak een werkmap en pak de eerste cel

Nu **create cell style** we door eerst een referentie naar de cel te krijgen die we willen opmaken.

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

Let op dat we `Cell` gebruiken in plaats van het generieke `var` — expliciete typisering maakt de code duidelijker voor beginners. De aanroep van `PutValue` schrijft een string zodat we later het stijl‑effect kunnen zien.

---

## Stap 3: Definieer de stijl – tekst centreren, een dunne rand toevoegen

Hier is het hart van de **create cell style** operatie. We stellen horizontale uitlijning, een dunne rand en een paar optionele extra’s in.

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*Waarom we dit doen:*  
- **HorizontalAlignment** en **VerticalAlignment** samen beantwoorden de vraag “**how to center text** in a cell?”.  
- Het toevoegen van alle vier de randen zorgt ervoor dat de cel eruitziet als een ingekaderd label, wat handig is voor koppen.  
- De achtergrondkleur is niet vereist, maar laat zien hoe je de stijl later kunt uitbreiden.

---

## Stap 4: Pas de gedefinieerde stijl toe op de geselecteerde cel

Nu de stijl bestaat, **apply style to cell** we met één methode‑aanroep.

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

Dat is alles — Aspose.Cells zorgt voor het kopiëren van de stijl naar de interne stijlcollectie van de cel. Als je dezelfde opmaak op een bereik nodig hebt, kun je `ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });` gebruiken.

---

## Stap 5: Sla de werkmap op en controleer het resultaat

Een snelle save laat je het bestand in Excel openen en bevestigen dat de tekst echt gecentreerd is en de rand verschijnt.

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*Verwacht resultaat:* Wanneer je **StyledCell.xlsx** opent, bevat cel **A1** “Hello, styled world!” gecentreerd zowel horizontaal als verticaal, omgeven door een dunne grijze rand, en geplaatst op een lichtgrijze achtergrond.

---

## Veelvoorkomende variaties & randgevallen

### 1. Tekst centreren in een samengevoegd gebied

Als je cellen **A1:C1** samenvoegt en de tekst nog steeds gecentreerd wilt, moet je de stijl toepassen op de linkerboven‑cel **na** het samenvoegen:

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. Een numeriek formaat gebruiken

Soms moet je **set cell alignment** *en* getallen weergeven met een specifiek formaat:

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

De uitlijning blijft gecentreerd terwijl het getal verschijnt als `12,345.68`.

### 3. Stijlen efficiënt hergebruiken

Het maken van een nieuwe `Style` voor elke cel kan de prestaties aantasten. Maak in plaats daarvan één stijlobject en hergebruik dit over vele cellen of bereiken. De `StyleFlag`‑klasse laat je alleen de delen toepassen die je nodig hebt, waardoor geheugen wordt bespaard.

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

---

## Pro‑tips & valkuilen om op te letten

- **Vergeet verticale uitlijning niet** – alleen horizontaal centreren ziet er vaak vreemd uit, vooral bij hogere rijen.  
- **Randtypen**: `CellBorderType.Thin` werkt voor de meeste rapporten, maar je kunt overschakelen naar `Medium` of `Dashed` voor visuele hiërarchie.  
- **Kleurafhandeling**: Bij .NET Core gebruik je `System.Drawing.Color` uit het `System.Drawing.Common`‑pakket; anders krijg je een runtime‑fout.  
- **Opslagformaat**: Als je compatibiliteit met oudere Excel‑versies nodig hebt, wijzig `SaveFormat.Xlsx` naar `SaveFormat.Xls`.

---

![Create cell style example](https://example.com/images/create-cell-style.png "Create cell style in C#")
*Alt‑tekst: screenshot die een cel toont met gecentreerde tekst en een dunne rand, gemaakt door de create cell style‑tutorial.*

---

## Volledig werkend voorbeeld (klaar om te copy‑pasten)

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

Voer dit programma uit, open **StyledCell.xlsx**, en je ziet exact het eerder beschreven resultaat. Voel je vrij om de tekst, randstijl of achtergrondkleur aan te passen aan je eigen huisstijl.

---

## Conclusie

We hebben zojuist **created cell style** vanaf nul, **applied style to cell**, en laten zien **how to center text** zowel horizontaal als verticaal. Door deze bouwstenen te beheersen kun je nu koppen opmaken, totalen markeren, of volledige rapporttemplates bouwen zonder ooit C# te verlaten.  

Als je nieuwsgierig bent naar de volgende stappen, probeer dan:

- **Dezelfde stijl toepassen op een hele rij** (`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`).  
- **Voorwaardelijke opmaak toevoegen** om de achtergrond te wijzigen op basis van celwaarden.  
- **Exporteren naar PDF** terwijl de stijl behouden blijft.

Onthoud, stijlen gaat net zo veel over leesbaarheid als over esthetiek. Experimenteer, itereer, en al snel zien je spreadsheets er net zo professioneel uit als je code.

*Veel plezier met coderen!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}