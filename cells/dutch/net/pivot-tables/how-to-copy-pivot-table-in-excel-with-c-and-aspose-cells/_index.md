---
category: general
date: 2026-10-04
description: Leer hoe je een draaitabel van de ene werkmap naar de andere kunt kopiëren
  met C#. Deze gids behandelt ook hoe je rijen kunt kopiëren, een draaitabel kunt
  dupliceren en een Excel-bereik efficiënt kunt kopiëren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- how to copy rows
- duplicate pivot table
language: nl
lastmod: 2026-10-04
og_description: Kopieer draaitabel in Excel met C#. Volg deze volledige tutorial om
  draaitabellen te dupliceren, rijen te kopiëren en een Excel-bereik te kopiëren met
  Aspose.Cells.
og_image_alt: Screenshot showing a duplicated pivot table in an Excel worksheet after
  using C# code
og_title: Kopieer draaitabel in Excel met C# – stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to copy pivot table from one workbook to another using C#.
    This guide also covers how to copy rows, duplicate pivot table, and copy Excel
    range efficiently.
  headline: How to copy pivot table in Excel with C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hoe een draaitabel in Excel te kopiëren met C# en Aspose.Cells
url: /nl/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een draaitabel te kopiëren in Excel met C# en Aspose.Cells

Als je een **copy pivot table** van het ene werkboek naar het andere moet kopiëren, laat deze tutorial je een volledige, uitvoerbare oplossing zien. Je ziet precies hoe je een bronbestand laadt, het bereik definieert dat de draaitabel bevat, de rijen (inclusief de draaitabeldefinitie) kopieert en het resultaat opslaat. Of je nu een rapportage‑pipeline automatiseert of een migratietool bouwt, de onderstaande stappen laten je een draaitabel dupliceren met slechts een paar regels C#.

Een draaitabel kopiëren is meer dan alleen celwaarden kopiëren; de onderliggende cache en veldinstellingen moeten samen reizen. Het voorbeeld maakt gebruik van de **Aspose.Cells**‑bibliotheek omdat deze draaitabel‑metadata automatisch afhandelt, zodat je de cache niet handmatig hoeft te herbouwen. Aan het einde van deze gids kun je **how to copy pivot**, **copy excel range** en **how to copy rows** veilig uitvoeren.

## Voorvereisten

Voordat je begint, zorg dat je het volgende hebt:

- .NET 6.0 of later geïnstalleerd (de code werkt ook met .NET Framework 4.7+).
- Een geldige Aspose.Cells for .NET‑licentie of een tijdelijke evaluatielicentie.
- Twee Excel‑bestanden: `Source.xlsx` met de draaitabel die je wilt dupliceren, en een lege map waar `CopyWithPivot.xlsx` wordt weggeschreven.
- Visual Studio 2022 (of een andere IDE die C# ondersteunt).

## Stap 1: Het project opzetten en Aspose.Cells toevoegen

Maak een nieuw console‑project aan en voeg het Aspose.Cells‑NuGet‑pakket toe:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
dotnet add package Aspose.Cells
```

Het pakket levert de klassen `Workbook`, `Worksheet` en `CellArea` die in de onderstaande code worden gebruikt.

## Stap 2: Het bron‑werkboek laden dat de draaitabel bevat

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the source workbook that holds the pivot you want to duplicate
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");
```

> **Waarom dit belangrijk is:** Het laden van het werkboek creëert een in‑memory‑representatie van alle werkbladen, inclusief eventuele verborgen draaitabel‑caches. Zonder het bestand te laden kun je niet naar het bereik van de draaitabel verwijzen.

## Stap 3: Het celgebied definiëren dat de draaitabel omvat

Je moet Aspose.Cells vertellen welke rijen en kolommen tot de draaitabel behoren. De `CellArea`‑structuur laat je een rechthoekig blok specificeren.

```csharp
        // Define the rectangle that encloses the pivot table (adjust as needed)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,      // first row (zero‑based)
            StartColumn = 0,   // first column
            EndRow = 30,       // last row of the pivot
            EndColumn = 10     // last column of the pivot
        };
```

> **Tip:** Als je niet zeker bent van de exacte grootte, open dan het bronbestand in Excel, selecteer de draaitabel en noteer het bereik dat in het Naamvak wordt weergegeven (bijv. `A1:K31`). Zet de Excel‑coördinaten om naar nul‑gebaseerde indexen voor de code.

## Stap 4: Een nieuw bestemmings‑werkboek maken en het eerste werkblad ophalen

```csharp
        // Create an empty workbook that will receive the copied pivot
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

> **Waarom deze stap vereist is:** Het bestemmings‑werkboek moet bestaan voordat je rijen kunt kopiëren. Aspose.Cells maakt automatisch een standaardwerkblad aan, dat we als doel gebruiken.

## Stap 5: De rijen (inclusief de draaitabel) van bron naar bestemming kopiëren

De `CopyRows`‑methode kopieert zowel celwaarden als de onderliggende draaitabel‑cache.

```csharp
        // Copy rows from source to destination, preserving the pivot definition
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,      // source cells
            sourceRange.StartRow,                 // first row to copy
            sourceRange.EndRow - sourceRange.StartRow + 1, // number of rows
            destWorksheet.Cells,                  // target cells
            sourceRange.StartRow);                // target start row
```

> **Hoe dit werkt:**  
> - `CopyRows` neemt het bron‑werkblad, de start‑rij en het aantal rijen dat gekopieerd moet worden.  
> - Het ontvangt ook het bestemmings‑werkblad en de rij waar de kopie moet beginnen.  
> - Omdat het bron‑bereik de draaitabel bevat, draagt de methode de cache, veldlijst en lay‑out van de draaitabel intact over. Dit is de kern van **how to copy pivot** zonder functionaliteit te verliezen.

### Randgeval: een draaitabel die zich over meerdere werkbladen uitstrekt

Als de bron‑gegevens van de draaitabel zich op een ander blad bevinden dan de draaitabel zelf, volgt de cache nog steeds de kopie omdat Aspose.Cells de cache in het werkboek opslaat, niet op het blad. Je moet er echter wel voor zorgen dat het bestemmings‑werkboek hetzelfde bron‑gegevens‑bereik bevat; anders toont de draaitabel `#REF!`‑fouten. Kopieer in dat geval eerst het bron‑gegevens‑bereik en daarna de draaitabel‑rijen.

## Stap 6: Het werkboek opslaan dat nu de gekopieerde draaitabel bevat

```csharp
        // Persist the destination workbook to disk
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

Het uitvoeren van het programma levert `CopyWithPivot.xlsx` op met een exacte replica van de oorspronkelijke draaitabel, inclusief alle slicers, filters en berekende velden.

### Verwachte output

Wanneer je `CopyWithPivot.xlsx` opent:

- De draaitabel verschijnt op dezelfde positie (bijv. A1:K31) als in `Source.xlsx`.
- Alle rij‑ en kolomlabels, totalen en opmaak zijn behouden.
- Het vernieuwen van de draaitabel toont dezelfde gegevens als de bron, wat bevestigt dat de cache correct is gekopieerd.

## Hoe rijen te kopiëren zonder een draaitabel (copy excel range)

Als je alleen een **copy excel range** zonder draaitabel‑gegevens wilt kopiëren, kun je dezelfde `CopyRows`‑methode gebruiken maar wijzen naar een bereik dat geen draaitabel bevat. Bijvoorbeeld:

```csharp
// Copy a simple data table from rows 5‑15, columns A‑D
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    4,            // start at row 5 (zero‑based)
    11,           // copy 11 rows (5‑15 inclusive)
    destWorksheet.Cells,
    0);           // paste at the top of the destination sheet
```

Dit demonstreert **how to copy rows** voor generieke data, en onderstreept de veelzijdigheid van dezelfde API.

## Draaitabel dupliceren in hetzelfde werkboek (alternatieve aanpak)

Soms wil je een **duplicate pivot table** binnen hetzelfde werkboek maken in plaats van een nieuw bestand. Dit kun je bereiken door rijen naar een andere locatie te kopiëren:

```csharp
// Duplicate pivot table to start at row 40 in the same worksheet
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    sourceRange.StartRow,
    sourceRange.EndRow - sourceRange.StartRow + 1,
    destWorksheet.Cells,
    40); // destination start row (zero‑based)
```

Na het opslaan bevat het werkboek twee identieke draaitabellen — handig voor naast‑elkaar‑vergelijkingen of het maken van back‑upkopieën.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Valkuil | Waarom het gebeurt | Oplossing |
|---------|--------------------|-----------|
| Draaitabel toont `#REF!` na kopiëren | Bron‑gegevensbereik ontbreekt in bestemmings‑werkboek | Kopieer eerst het bron‑gegevens‑bereik, of gebruik `CopyRows` op het bron‑gegevensblad vóór het kopiëren van de draaitabel |
| Opmaak verloren | Alleen waarden werden gekopieerd (bijv. `Copy` in plaats van `CopyRows`) | Gebruik altijd `CopyRows`, dat stijl, opmaak en draaitabel‑metadata behoudt |
| Onverwachte rij‑offset | Start‑rij van bestemming komt niet overeen met start‑rij van bron | Controleer dat `destWorksheet.Cells` start‑rij overeenkomt met de beoogde locatie |
| Grote werkboeken veroorzaken geheugen‑druk | `CopyRows` laadt volledige werkbladen in het geheugen | Verwerk de kopie in delen of gebruik streaming‑API’s bij >100.000 rijen |

## Volledig, uitvoerbaar voorbeeld

Hieronder staat het complete programma dat je in `Program.cs` kunt plakken en direct kunt uitvoeren (vervang `YOUR_DIRECTORY` door een echt pad op jouw machine).

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook containing the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");

        // 2️⃣ Define the area that encloses the pivot (adjust to your sheet)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 30,
            EndColumn = 10
        };

        // 3️⃣ Create the destination workbook (empty) and get its first sheet
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // 4️⃣ Copy rows—including the pivot cache—into the destination
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,
            sourceRange.StartRow,
            sourceRange.EndRow - sourceRange.StartRow + 1,
            destWorksheet.Cells,
            sourceRange.StartRow);

        // 5️⃣ Save the result
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

Voer het programma uit met `dotnet run`. Na uitvoering open je `CopyWithPivot.xlsx` om te verifiëren dat de draaitabel exact verschijnt zoals in het bronbestand.

## Conclusie

Je weet nu hoe je een **copy pivot table** van het ene Excel‑werkboek naar het andere kunt uitvoeren met C# en Aspose.Cells. De gids besprak de volledige workflow — van het laden van het bronbestand, het definiëren van het celgebied van de draaitabel, het kopiëren van rijen, tot het opslaan van het bestemmings‑werkboek. Daarnaast heb je geleerd **how to copy rows**, **copy excel range** en **duplicate pivot table** binnen hetzelfde bestand, plus veelvoorkomende valkuilen en best‑practice‑tips.

Klaar voor de volgende stap? Probeer code toe te voegen die de gekopieerde draaitabel programmatisch vernieuwt, of verken het exporteren van de draaitabel naar PDF met Aspose.Cells. Experimenteer met verschillende bron‑bereiken, en je beheerst Excel‑automatisering in .NET snel.

---


## Wat moet je hierna leren?


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [copy rows excel – Preserve Pivot Table While Duplicating Rows](/cells/english/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}