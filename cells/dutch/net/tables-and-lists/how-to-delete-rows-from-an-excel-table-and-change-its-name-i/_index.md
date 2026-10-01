---
category: general
date: 2026-10-01
description: Leer hoe je rijen uit een Excel‑tabel verwijdert en de naam van de Excel‑tabel
  wijzigt met C#. Stapsgewijze handleiding met volledige code en best practices.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows excel table
- change excel table name
- load excel workbook c#
- remove rows from excel table
- update excel table name
language: nl
lastmod: 2026-10-01
og_description: Verwijder rijen uit een Excel‑tabel en wijzig de naam van de Excel‑tabel
  in C#. Volg deze volledige tutorial om een werkmap te laden, de tabel te bewerken
  en het resultaat op te slaan.
og_image_alt: Screenshot showing C# code that deletes rows from an Excel table and
  updates the table name
og_title: Rijen verwijderen uit een Excel‑tabel en de naam wijzigen in C# – volledige
  gids
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn to delete rows from an Excel table and change the Excel table
    name using C#. Step‑by‑step guide with full code and best practices.
  headline: How to delete rows from an Excel table and change its name in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: Hoe rijen uit een Excel‑tabel te verwijderen en de naam ervan te wijzigen in
  C#
url: /nl/net/tables-and-lists/how-to-delete-rows-from-an-excel-table-and-change-its-name-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe rijen uit een Excel-tabel te verwijderen en de naam te wijzigen in C#

Als je **rijen uit een Excel-tabel** moet verwijderen tijdens het werken met C#, laat deze gids de exacte stappen zien die nodig zijn. Je zult zien hoe je **een Excel-werkmap in C# laadt**, specifieke rijen uit een tabel verwijdert, en vervolgens **de naam van de Excel-tabel bijwerkt** zodat het bestand consistent blijft.

De tutorial behandelt alles wat je moet weten: vereiste NuGet‑pakketten, volledige uitvoerbare code, en veelvoorkomende valkuilen zoals schendingen van de tabelstructuur. Aan het einde van het artikel kun je elke Excel-tabel programmatisch wijzigen zonder handmatige tussenkomst.

## Vereisten

* .NET 6.0 SDK of later geïnstalleerd.
* Visual Studio 2022 (of een andere C#‑IDE) geconfigureerd voor .NET‑ontwikkeling.
* De **Aspose.Cells for .NET**‑bibliotheek toegevoegd via NuGet (`Install-Package Aspose.Cells`).
* Een bestaande Excel-werkmap (`Table.xlsx`) die minstens één werkblad met een tabel bevat.

Deze items bieden de omgeving die nodig is om **Excel-werkmap c#** code te laden en de bewerkingen betrouwbaar uit te voeren.

## Stap 1: Laad de werkmap die de tabel bevat

De eerste bewerking is het openen van het werkmapbestand. Aspose.Cells leest de volledige werkmap in het geheugen, waardoor je volledige controle krijgt over werkbladen, tabellen en celgegevens.

```csharp
using Aspose.Cells;

string inputPath = @"C:\Data\Table.xlsx";

// Load the workbook from disk
Workbook workbook = new Workbook(inputPath);
```

*Waarom dit belangrijk is*: Het laden van de werkmap is de basis voor elke daaropvolgende tabelmanipulatie. Het `Workbook`‑object biedt de `Worksheets`‑collectie, die je zult gebruiken om de doel‑tabel te vinden.

## Stap 2: Toegang tot het eerste werkblad en de eerste tabel

De meeste Excel‑bestanden slaan tabellen op in het eerste werkblad, maar je kunt de index aanpassen indien nodig. De volgende code haalt het eerste `Table`‑object op.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Retrieve the first table on that worksheet
Table table = sheet.Tables[0];
```

Als het werkblad geen tabel bevat, zal `sheet.Tables.Count` nul zijn en moet je dat geval afhandelen. Proberen `sheet.Tables[0]` te benaderen wanneer er geen tabellen bestaan, veroorzaakt een uitzondering, daarom wordt een guard‑clausule aanbevolen in productiecodel.

## Stap 3: Rijen uit de Excel-tabel verwijderen

Om **rijen uit een Excel-tabel** te verwijderen, roep je `DeleteRows(startRow, totalRows)` aan. De parameter `startRow` is nul‑gebaseerd ten opzichte van de eerste gegevensrij van de tabel (de rij na de koptekst).

```csharp
// Delete two rows starting from the second data row (index 1)
int startRow = 1;   // second row within the table
int rowsToDelete = 2;

table.DeleteRows(startRow, rowsToDelete);
```

### Waarom `DeleteRows` gebruiken in plaats van werkblad‑rijen te verwijderen?

`DeleteRows` werkt het interne bereik van de tabel bij, waardoor formules, stijlen en gedefinieerde namen die bij de tabel horen behouden blijven. Directe verwijdering van werkblad‑rijen kan de tabelstructuur breken en een uitzondering veroorzaken.

**Randgeval**: Als de verwijdering de tabel zonder gegevensrijen zou achterlaten, gooit Aspose.Cells een `ArgumentException`. Bescherm hiertegen door `table.RowCount` te controleren vóór het verwijderen.

```csharp
if (table.RowCount - rowsToDelete < 1)
{
    throw new InvalidOperationException("Cannot delete all data rows from the table.");
}
```

## Stap 4: De naam van de Excel-tabel wijzigen

Nadat rijen zijn verwijderd, wil je de tabel misschien een meer beschrijvende identifier geven. De eigenschap `Name` stelt de gedefinieerde naam van de tabel in, die wordt gebruikt in formules en VBA.

```csharp
// Assign a new name to the table
string newTableName = "SalesData2026";

if (workbook.Worksheets.GetDefinedNames().Any(d => d.Text == newTableName))
{
    throw new InvalidOperationException($"The name '{newTableName}' already exists as a defined name.");
}

table.Name = newTableName;
```

*Waarom hernoemen?* Een duidelijke tabelnaam verbetert de leesbaarheid in formules (`=SUM(SalesData2026[Amount])`) en voorkomt naamconflicten wanneer meerdere tabellen vergelijkbare doeleinden hebben.

## Stap 5: De gewijzigde werkmap opslaan (optioneel)

Bewaar de wijzigingen door op te slaan naar een nieuw bestand of door het origineel te overschrijven. Opslaan naar een nieuwe locatie is veiliger tijdens de ontwikkeling.

```csharp
string outputPath = @"C:\Data\ModifiedTable.xlsx";
workbook.Save(outputPath);
```

De `Save`‑methode schrijft de bijgewerkte werkmap, inclusief het gewijzigde tabelbereik en de nieuwe tabelnaam, naar schijf.

## Volledig werkend voorbeeld

Alle stappen samenvoegen levert een zelfstandige applicatie op die je direct kunt uitvoeren.

```csharp
using System;
using System.Linq;
using Aspose.Cells;

class ExcelTableModifier
{
    static void Main()
    {
        // ----- Step 1: Load workbook -----
        string inputPath = @"C:\Data\Table.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // ----- Step 2: Access worksheet and table -----
        Worksheet sheet = workbook.Worksheets[0];
        if (sheet.Tables.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        Table table = sheet.Tables[0];

        // ----- Step 3: Delete rows -----
        int startRow = 1;      // second data row (zero‑based)
        int rowsToDelete = 2;

        if (table.RowCount - rowsToDelete < 1)
        {
            Console.WriteLine("Deletion would remove all data rows; operation aborted.");
            return;
        }

        table.DeleteRows(startRow, rowsToDelete);
        Console.WriteLine($"{rowsToDelete} rows removed starting at index {startRow}.");

        // ----- Step 4: Change table name -----
        string newTableName = "SalesData2026";

        bool nameExists = workbook.Worksheets.GetDefinedNames()
                               .Any(d => d.Text.Equals(newTableName, StringComparison.OrdinalIgnoreCase));

        if (nameExists)
        {
            Console.WriteLine($"The name '{newTableName}' already exists. Choose a different name.");
            return;
        }

        table.Name = newTableName;
        Console.WriteLine($"Table renamed to '{newTableName}'.");

        // ----- Step 5: Save workbook -----
        string outputPath = @"C:\Data\ModifiedTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to '{outputPath}'.");
    }
}
```

**Verwachte output** (ervan uitgaande dat het bestand en de tabel bestaan):

```
2 rows removed starting at index 1.
Table renamed to 'SalesData2026'.
Modified workbook saved to 'C:\Data\ModifiedTable.xlsx'.
```

Het uitvoeren van het programma werkt het Excel‑bestand precies zoals beschreven bij: rijen worden verwijderd, de tabelnaam verandert, en het resultaat wordt opgeslagen zonder handmatige bewerking.

## Veelgestelde vragen en probleemoplossing

| Vraag | Antwoord |
|----------|--------|
| *Wat gebeurt er als de tabel over samengevoegde cellen loopt?* | `DeleteRows` respecteert samengevoegde bereiken. Als een samengevoegde cel de verwijderingsgrens overschrijdt, past Aspose.Cells de samenvoeging automatisch aan. Controleer het resultaat visueel als je afhankelijk bent van complexe samenvoegingen. |
| *Kan ik rijen uit een tabel verwijderen die deel uitmaakt van een pivot‑cache?* | Het verwijderen van rijen uit een bron‑tabel die een draaitabel voedt, **ververst** de pivot‑cache niet automatisch. Roep `pivotTable.RefreshData()` aan na het wijzigen van de bron‑tabel. |
| *Is het mogelijk om rijen te verwijderen op basis van een voorwaarde (bijv. waarde < 0)?* | Ja. Iterate door `table.ListObjects` of `table.Rows` om overeenkomende rijen te vinden, verzamel vervolgens hun indices en roep `DeleteRows` aan voor elk bereik. |
| *Moet ik het `Workbook`‑object vrijgeven?* | `Workbook` implementeert `IDisposable`. Plaats het in een `using`‑blok voor deterministische vrijgave van bronnen, vooral bij het verwerken van grote bestanden. |
| *Hoe verschilt dit van het gebruik van EPPlus?* | EPPlus ondersteunt ook tabelmanipulatie maar gebruikt een andere API (`ExcelTable`). De concepten van het laden van een werkmap, rijen verwijderen en de tabel hernoemen zijn analoog. Kies de bibliotheek die past bij je licentie‑eisen. |

## Best practices bij het wijzigen van Excel‑tabellen in C#

* **Valideer indexen** – Tabel‑rij‑indexen zijn nul‑gebaseerd; off‑by‑one‑fouten veroorzaken onverwachte verwijderingen.
* **Controleer op naamconflicten** – Excel staat geen dubbele gedefinieerde namen toe; controleer altijd op uniciteit voordat je een nieuwe naam toewijst.
* **Maak een back‑up van originele bestanden** – Geautomatiseerde scripts kunnen data corrupt maken; bewaar een kopie van de bron‑werkmap.
* **Gebruik `using`‑statements** – Garandeert dat bestands‑handles tijdig worden vrijgegeven:

```csharp
using (Workbook wb = new Workbook(inputPath))
{
    // modify workbook
}
```

* **Test met randgevallen** – Tabellen met één gegevensrij, tabellen die het hele werkblad beslaan, en tabellen gekoppeld aan grafieken moeten na wijzigingen worden geverifieerd.

## Conclusie

Je weet nu hoe je **rijen uit een Excel-tabel** kunt verwijderen en **de naam van de Excel-tabel** kunt wijzigen met C#. De volledige oplossing laadt de werkmap, benadert de doel‑tabel, verwijdert de gewenste rijen, hernoemt de tabel en slaat het resultaat op. Pas deze technieken toe om rapportgeneratie, gegevensopschoning of elke workflow die programmatisch Excel‑tabelbeheer vereist, te automatiseren.

Vervolgens kun je gerelateerde onderwerpen verkennen, zoals **celwaarden bijwerken in een Excel-tabel**, **programmeer­matig nieuwe rijen toevoegen**, en **tabelgegevens exporteren naar CSV**. Het beheersen van deze bewerkingen geeft je volledige controle over Excel‑bestanden vanuit je C#‑applicaties.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe een tabel te hernoemen in Excel met C# – Stapsgewijze gids](/cells/english/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/)
- [Een Excel‑tabel maken in C# – Stapsgewijze gids](/cells/english/net/tables-and-lists/create-excel-table-in-c-step-by-step-guide/)
- [Eerste tabel uit een Excel‑werkmap halen in C# – Complete gids](/cells/english/net/excel-autofilter-validation/get-first-table-from-excel-workbook-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}