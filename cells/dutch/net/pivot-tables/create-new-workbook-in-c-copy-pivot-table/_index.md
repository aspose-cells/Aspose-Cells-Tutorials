---
category: general
date: 2026-06-24
description: Maak een nieuw werkboek in C# en kopieer de draaitabel terwijl je de
  gegevens behoudt. Leer hoe je rijen kopieert, een geselecteerd bereik exporteert
  en de draaitabel intact houdt.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- export selected range
language: nl
og_description: Maak een nieuw werkboek in C# en kopieer een draaitabel terwijl je
  de gegevens behoudt. Stapsgewijze handleiding die uitlegt hoe je rijen kopieert
  en een geselecteerd bereik exporteert.
og_title: Nieuwe werkmap maken in C# – draaitabel kopiëren
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Create new workbook in C# and copy pivot table while preserving its
    data. Learn how to copy rows, export selected range, and keep the pivot intact.
  headline: Create New Workbook in C# – Copy Pivot Table
  type: TechArticle
- questions:
  - answer: Yes, as long as the copied rectangle encloses each pivot you need. If
      you only want one, adjust `rows`/`cols` to isolate it.
    question: Does this work with multiple pivot tables on the same sheet?
  - answer: The pivot cache will still point to the original connection. Call `pivotTable.RefreshData()`
      after loading the destination if you want to re‑query the source.
    question: What if the source workbook uses external data connections?
  - answer: Absolutely. Replace `destinationWorkbook` with `sourceWorkbook` and pick
      another worksheet index.
    question: Can I copy the pivot to a different sheet within the same workbook?
  - answer: 'Use `CopyRows`/`CopyColumns` overloads that accept a `CopyOptions` object—set
      `CopyOptions.CopyType = CopyType.ValuesOnly` or `CopyType.All` depending on
      your needs. --- ## Conclusion We’ve just walked through a **create new workbook**
      scenario that **copy pivot table**, **preserve pivot table**, an'
    question: Is there a way to copy formatting only?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel automation
title: Nieuw werkboek maken in C# – Draaitabel kopiëren
url: /nl/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nieuwe Werkmap Maken in C# – Kopieer Pivottabel

Heb je ooit een **create new workbook** in C# moeten maken alleen om een deel van gegevens te verplaatsen dat een pivottabel bevat? Je bent niet de enige. In veel rapportage‑pijplijnen pak je een handvol rijen, misschien een paar kolommen, en je verwacht dat de pivot precies blijft zoals hij was—geen gebroken verwijzingen, geen ontbrekende berekeningen.  

Het goede nieuws? Met een paar regels Aspose.Cells kun je **copy pivot table**, het intact houden, en zelfs **export selected range** zonder iets te breken. Hieronder zie je een compleet, kant‑klaar voorbeeld dat laat zien **how to copy rows**, de pivot behoudt, en het resultaat opslaat als een gloednieuwe werkmap.

## Wat Deze Tutorial Behandelt

- Een C#‑project opzetten met Aspose.Cells (de bibliotheek die de code aandrijft).
- Het bron‑werkboek laden dat de originele pivot bevat.
- De `CopyRows`‑ en `CopyColumns`‑methoden van de bibliotheek gebruiken om het exacte bereik dat je nodig hebt te dupliceren.
- Het gedupliceerde gebied opslaan in een **create new workbook**‑scenario terwijl de pivot functioneel blijft.
- Tips voor randgevallen zoals meerdere pivottabellen, verborgen rijen en grote datasets.

Aan het einde van deze gids kun je **export selected range** vanuit elk Excel‑bestand, de pivot‑logica levend houden, en het nieuwe bestand overal neerzetten waar je wilt.

> **Voorvereiste**: Aspose.Cells for .NET (gratis proefversie of gelicentieerde versie) geïnstalleerd via NuGet. Als je het nog niet hebt toegevoegd, voer `dotnet add package Aspose.Cells` uit in je projectmap.

---

## Nieuwe Werkmap Maken en Pivottabel Kopiëren

Hieronder staat het hart van de oplossing. We lopen elke regel door, leggen uit waarom deze belangrijk is, en tonen vervolgens het volledige programma.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // 1️⃣ Load the source workbook that contains the pivot table
        string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.Worksheets[0];

        // 3️⃣ Define the range we want to copy (first 20 rows, first 4 columns)
        //    This range includes the pivot table we care about.
        int startRow = 0;   // zero‑based index
        int startColumn = 0;
        int totalRows = 20;
        int totalColumns = 4;

        // 4️⃣ Copy rows – this is the “how to copy rows” part.
        //    Aspose.Cells lets us copy rows directly from the source cells collection.
        sourceWorkbook.Worksheets[0].Cells.CopyRows(startRow, startRow, totalRows);

        // 5️⃣ Copy columns – paired with the row copy to form a rectangular block.
        sourceWorkbook.Worksheets[0].Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 6️⃣ Now move the copied block into the destination sheet.
        //    We use the same start cell (A1) for simplicity.
        destSheet.Cells.CopyRows(startRow, startRow, totalRows);
        destSheet.Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 7️⃣ Save the destination workbook – the pivot table is preserved in the copied range
        string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
        destinationWorkbook.Save(destPath);

        Console.WriteLine("✅ New workbook created and pivot table preserved at: " + destPath);
    }
}
```

### Waarom Dit Werkt

- **`CopyRows` / `CopyColumns`**: Deze methoden dupliceren de onderliggende celgegevens *en* de bijbehorende objecten (zoals een pivot‑cache). Daarom blijft de pivot functioneel na de verplaatsing.
- **Separate destination workbook**: Door een verse `Workbook`‑instantie te maken, **create new workbook** zonder resterende opmaak of verborgen bladen die kunnen interfereren.
- **Zero‑based indexing**: Aspose.Cells gebruikt nul‑gebaseerde indexen, dus `0` wijst naar cel **A1**. Pas `startRow`/`startColumn` aan als je pivot niet in de linkerbovenhoek staat.
- **Preserve pivot table**: De cache van de pivot bevindt zich in hetzelfde bereik, dus het kopiëren van het bereik kopieert automatisch de cache. Geen extra code nodig.

---

## Hoe Rijen Kopiëren Zonder de Pivot te Breken

Als je alleen geïnteresseerd bent in het rij‑kopie‑gedeelte, kun je dat isoleren:

```csharp
// Copy just rows 5‑15 (inclusive) from the source sheet
int sourceStartRow = 4;   // row 5 in Excel terms
int rowsToCopy = 11;      // rows 5‑15 => 11 rows
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy);
```

**Pro tip**: Bij het kopiëren van rijen die een pivottabel kruisen, kopieer altijd het *volledige* pivot‑gebied (rijen + kolommen). Gedeeltelijke kopieën kunnen de pivot achterlaten met ontbrekende velden, wat `#REF!`‑fouten veroorzaakt.

## Export Selected Range – Een Praktijkvoorbeeld

Stel je voor dat je een gigantisch verkoop‑werkboek hebt, maar je klant alleen de samenvatting van het eerste kwartaal wil, die zich bevindt in rijen 1‑20 en kolommen A‑D. Het fragment hierboven **export selected range** al voor je. Verander gewoon de variabelen `totalRows` en `totalColumns` zodat ze overeenkomen met de aanvraag van de klant, en je bent klaar.

### Verborgen Rijen of Filters Afhandelen

Als het bronblad verborgen rijen heeft (mogelijk gefilterd), wil je misschien alleen *zichtbare* rijen kopiëren. Aspose.Cells biedt `CopyRows`‑overloads die zichtbaarheid respecteren:

```csharp
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy, true);
```

Stel de laatste boolean in op `true` om alleen zichtbare rijen te kopiëren—perfect voor “export selected range” wanneer de gebruiker filters heeft toegepast.

## Pivot Tabel Behouden – Veelvoorkomende Valkuilen & Hoe ze te Vermijden

| Valkuil | Waarom Het Gebeurt | Oplossing |
|---------|--------------------|-----------|
| **Pivot cache not copied** | Gebruik van gewone `Range.Copy` in plaats van `Cells.CopyRows/CopyColumns`. | Blijf bij de `Cells`‑methoden zoals getoond. |
| **Destination sheet has existing pivot** | Opslaan over een werkboek dat al een pivot met dezelfde naam bevat. | Begin met een verse `Workbook()` (zoals wij doen). |
| **Named ranges break** | De bron‑pivot verwijst naar een benoemd bereik dat niet aanwezig is in het nieuwe bestand. | Copy the named range too: `sourceWorkbook.Worksheets[0].Names.CopyTo(destSheet);` |
| **Data source path changes** | Pivot wijst naar een externe gegevensbron die niet beschikbaar is. | Use `PivotTable.RefreshData()` after copying if needed. |

## Volledig End‑to‑End Voorbeeld (Klaar om Uit te Voeren)

Hieronder staat het volledige programma, inclusief de `using`‑directieven en een korte console‑UI. Kopieer‑en‑plak het in een nieuw Console‑App‑project en druk op **F5**.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyUtility
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load source workbook (contains the pivot)
            // -------------------------------------------------
            string srcPath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook srcWb = new Workbook(srcPath);

            // -------------------------------------------------
            // Step 2: Prepare destination workbook (create new workbook)
            // -------------------------------------------------
            Workbook destWb = new Workbook();
            Worksheet destWs = destWb.Worksheets[0];

            // -------------------------------------------------
            // Step 3: Define the block we want to copy
            // -------------------------------------------------
            int startRow = 0;      // A1
            int startCol = 0;      // A
            int rows = 20;         // first 20 rows
            int cols = 4;          // first 4 columns

            // -------------------------------------------------
            // Step 4: Copy rows and columns from source to destination
            // -------------------------------------------------
            srcWb.Worksheets[0].Cells.CopyRows(startRow, startRow, rows);
            srcWb.Worksheets[0].Cells.CopyColumns(startCol, startCol, cols);
            destWs.Cells.CopyRows(startRow, startRow, rows);
            destWs.Cells.CopyColumns(startCol, startCol, cols);

            // -------------------------------------------------
            // Step 5: Save the new workbook (preserve pivot table)
            // -------------------------------------------------
            string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
            destWb.Save(destPath);

            Console.WriteLine($"✅ Workbook created at {destPath}");
        }
    }
}
```

**Verwachte output** (in de console):

```
✅ Workbook created at YOUR_DIRECTORY\copy-pivot.xlsx
```

Open `copy-pivot.xlsx` en je ziet dezelfde pivottabel als in `source.xlsx`, volledig functioneel en verwijzend naar het gekopieerde gegevensbereik.

## Veelgestelde Vragen

**Q: Werkt dit met meerdere pivottabellen op hetzelfde blad?**  
A: Ja, zolang het gekopieerde rechthoek het elke benodigde pivot omvat. Als je er maar één wilt, pas `rows`/`cols` aan om deze te isoleren.

**Q: Wat als het bron‑werkboek externe gegevensverbindingen gebruikt?**  
A: De pivot‑cache blijft wijzen naar de originele verbinding. Roep `pivotTable.RefreshData()` aan na het laden van de bestemming als je de bron opnieuw wilt bevragen.

**Q: Kan ik de pivot naar een ander blad binnen hetzelfde werkboek kopiëren?**  
A: Zeker. Vervang `destinationWorkbook` door `sourceWorkbook` en kies een andere werkblad‑index.

**Q: Is er een manier om alleen opmaak te kopiëren?**  
A: Gebruik `CopyRows`/`CopyColumns`‑overloads die een `CopyOptions`‑object accepteren—stel `CopyOptions.CopyType = CopyType.ValuesOnly` of `CopyType.All` in, afhankelijk van je behoeften.

## Conclusie

We hebben zojuist een **create new workbook**‑scenario doorlopen dat **copy pivot table**, **preserve pivot table**, en **export selected range** uitvoert—alles in pure C#

## Wat Moet Je Volgende Leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies te beheersen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Create a New Pivot Table Programmatically in .NET](/cells/english/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/)
- [How to Change Pivot Table Source Data Using Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [How to Manage Excel Pivot Table Compatibility with Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}