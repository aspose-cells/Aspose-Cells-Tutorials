---
category: general
date: 2026-11-25
description: Leer hoe je rijen uit een Excel‑tabel in C# kunt verwijderen en ook meerdere
  rijen efficiënt uit een Excel‑werkblad kunt verwijderen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from excel table
- delete multiple rows from excel sheet
language: nl
lastmod: 2026-11-25
og_description: Verwijder rijen uit een Excel‑tabel in C# en leer hoe je meerdere
  rijen uit een Excel‑werkblad kunt verwijderen met schone code.
og_image_alt: Screenshot of C# code deleting rows from an Excel table
og_title: Rijen verwijderen uit Excel‑tabel in C# – complete gids
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  headline: How to delete rows from Excel table with C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  name: How to delete rows from Excel table with C#
  steps:
  - name: Add Aspose.Cells to your project
    text: 'Open the **Package Manager Console** and run:'
  - name: Load the workbook and locate the table
    text: '```csharp using Aspose.Cells;'
  - name: Delete the desired data rows
    text: The `DeleteRows` method expects a **zero‑based** row index relative to the
      table, **including** the header row. Because the header cannot be removed, you
      must start at index 1 for the first data row.
  - name: Save the modified workbook
    text: '```csharp // Save the workbook to a new file to preserve the original workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
      } } ```'
  - name: Full working example
    text: '```csharp using Aspose.Cells;'
  - name: Edge cases and best practices
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Deleting rows beyond the last row | Check `worksheet.Rows.Count` before calling
      `RemoveAt`. | | Removing all rows except the header | Delete data rows in a
      loop or use `DeleteRows(1, table.DataRa'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
- data manipulation
title: Hoe rijen uit een Excel‑tabel te verwijderen met C#
url: /nl/net/row-and-column-management/how-to-delete-rows-from-excel-table-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe rijen uit een Excel‑tabel te verwijderen met C#

Als je rijen uit een Excel‑tabel moet verwijderen met C#, laat deze gids je precies zien hoe je dat doet. Je zult ook zien hoe je meerdere rijen uit een Excel‑werkblad kunt verwijderen zonder andere gegevens te beïnvloeden.

Werken met Excel via code vereist vaak het verwijderen van verouderde of ongeldige records. Rijen direct in een werkblad verwijderen kan riskant zijn omdat de koprij van een gestructureerde tabel intact moet blijven. Deze tutorial leidt je door een veilige aanpak die de tabel‑kop respecteert en je in één oproep een willekeurig aantal gegevensrijen kunt verwijderen.

## Vereisten

* .NET 6.0 of later geïnstalleerd  
* Visual Studio 2022 (of een andere compatibele IDE)  
* Het **Aspose.Cells** NuGet‑pakket (versie 23.10 of nieuwer) – deze bibliotheek levert de `Workbook`, `Worksheet` en `ListObject` klassen die in de voorbeelden worden gebruikt  

Je hebt Microsoft Office niet nodig op de ontwikkelmachine, omdat Aspose.Cells direct met het bestandsformaat werkt.

## Rijen uit een Excel‑tabel verwijderen – stap voor stap

De volgende secties beschrijven elke stap die nodig is om rijen uit een Excel‑tabel veilig te verwijderen. Het primaire zoekwoord staat in deze kop om te voldoen aan SEO‑vereisten.

### Stap 1: Voeg Aspose.Cells toe aan je project

Open de **Package Manager Console** en voer uit:

```powershell
Install-Package Aspose.Cells
```

Het pakket voegt de benodigde assemblies toe en lost de `Workbook`, `Worksheet` en `ListObject` types op.

### Stap 2: Laad de werkmap en lokaliseer de tabel

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Load the workbook that contains the table
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // Access the first worksheet (index 0)
        var worksheet = workbook.Worksheets[0];

        // Retrieve the first ListObject (structured table) on the sheet
        var table = worksheet.ListObjects[0];
```

*Waarom dit belangrijk is*: De `ListObject` vertegenwoordigt een echte Excel‑tabel, die zijn eigen koprij behoudt. Door met de `ListObject` te werken, vermijd je per ongeluk het verwijderen van de koprij.

### Stap 3: Verwijder de gewenste gegevensrijen

De `DeleteRows`‑methode verwacht een **nul‑gebaseerde** rij‑index ten opzichte van de tabel, **inclusief** de koprij. Omdat de koprij niet kan worden verwijderd, moet je bij index 1 beginnen voor de eerste gegevensrij.

```csharp
        // Delete two data rows starting after the header (index 1)
        // Parameters: startRow (relative to the table), numberOfRows
        table.DeleteRows(1, 2);
```

Als je `table.DeleteRows(0, 2)` probeert, zal Aspose.Cells een uitzondering gooien omdat de koprij (index 0) beschermd is. Beginnen bij index 1 zorgt ervoor dat alleen gegevensrijen worden verwijderd.

### Stap 4: Sla de gewijzigde werkmap op

```csharp
        // Save the workbook to a new file to preserve the original
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

Het uitvoeren van het programma verwijdert de twee rijen direct onder de koprij, terwijl de tabelstructuur intact blijft.

### Volledig werkend voorbeeld

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // 1. Load workbook
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // 2. Access first worksheet
        var worksheet = workbook.Worksheets[0];

        // 3. Get the first table (ListObject)
        var table = worksheet.ListObjects[0];

        // 4. Delete two rows after the header (cannot delete header itself)
        table.DeleteRows(1, 2);

        // 5. Save the result
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

**Verwachte output**: Het bestand `table_with_header_modified.xlsx` bevat de oorspronkelijke tabel‑kop, gevolgd door alle rijen behalve de twee die zijn verwijderd. Geen andere werkbladen worden aangepast.

## Meerdere rijen uit een Excel‑werkblad verwijderen

Soms moet je rijen verwijderen die **niet** deel uitmaken van een gestructureerde tabel. Het secundaire zoekwoord staat in deze kop. De aanpak verschilt iets omdat je werkt met de `Rows`‑collectie van het werkblad in plaats van een `ListObject`.

```csharp
using Aspose.Cells;

class SheetRowDeletion
{
    static void Main()
    {
        var workbook = new Workbook(@"C:\Data\plain_sheet.xlsx");
        var worksheet = workbook.Worksheets[0];

        // Delete rows 5 through 9 (inclusive) – zero‑based index
        // The second argument is the count of rows to remove
        worksheet.Rows.RemoveAt(4, 5);

        workbook.Save(@"C:\Data\plain_sheet_modified.xlsx");
    }
}
```

**Waarom dit werkt**: `Rows.RemoveAt(startIndex, count)` verwijdert een aaneengesloten blok rijen direct uit het werkblad. Er is geen koprij‑bescherming, dus je kunt bij elke index beginnen. De methode is efficiënt omdat hij de interne datastructuren in één bewerking bijwerkt, wat ideaal is wanneer je meerdere rijen uit een Excel‑werkblad moet verwijderen.

### Randgevallen en best practices

| Situatie                               | Aanbevolen behandeling |
|----------------------------------------|------------------------|
| Rijen verwijderen voorbij de laatste rij      | Controleer `worksheet.Rows.Count` voordat je `RemoveAt` aanroept. |
| Alle rijen verwijderen behalve de koprij    | Verwijder gegevensrijen in een lus of gebruik `DeleteRows(1, table.DataRange.RowCount - 1)`. |
| Celopmaak behouden             | Verwijderen via `ListObject` verschuift automatisch de opmaak; voor ruwe werkbladen, kopieer de opmaak vóór verwijdering indien nodig. |
| Grote werkbladen ( > 10 000 rijen)      | Voer verwijderingen uit in aflopende volgorde om indexverschuiving te voorkomen, of gebruik `DeleteRows` op de tabel indien mogelijk. |

**Pro tip**: Wanneer je rijen moet verwijderen op basis van een voorwaarde (bijv. rijen waarvan een kolomwaarde leeg is), doorloop dan de `DataRange` van de tabel achterwaarts en roep `DeleteRows` aan voor elke overeenkomende rij. Achterwaarts verwijderen voorkomt index‑misalignatie.

## Veelgestelde vragen

*Werkt dit met .xlsx‑bestanden die zijn gemaakt door Excel 365?*  
Ja. Aspose.Cells ondersteunt de volledige Office Open XML‑specificatie, dus dezelfde code werkt voor elk modern `.xlsx`‑bestand.

*Wat als de werkmap meerdere tabellen bevat?*  
Haal de gewenste tabel op basis van naam op: `var table = worksheet.ListObjects["MyTable"];` en pas vervolgens `DeleteRows` toe zoals getoond.

*Kan ik rijen verwijderen zonder een externe bibliotheek te gebruiken?*  
Je zou de Microsoft.Office.Interop.Excel COM‑interop kunnen gebruiken, maar dat vereist dat Excel op de server is geïnstalleerd en brengt COM‑gerelateerde overhead met zich mee. Aspose.Cells biedt een lichtgewicht, server‑veilige alternatieve oplossing.

## Conclusie

Je weet nu hoe je rijen uit een Excel‑tabel veilig kunt verwijderen en hoe je meerdere rijen uit een Excel‑werkblad kunt verwijderen met C#. De primaire techniek maakt gebruik van de `ListObject.DeleteRows`‑methode, die de tabel‑kop respecteert, terwijl de secundaire techniek `Rows.RemoveAt` gebruikt voor gewone werkbladen. Pas deze patronen toe om data op te schonen, rapportgeneratie te automatiseren of bulk‑bewerkingsfuncties in je applicaties te implementeren.

**Volgende stappen**

* Verken andere Aspose.Cells‑functies zoals rijen invoegen, stijlen kopiëren of gegevens filteren.  
* Probeer dezelfde bewerkingen met **ClosedXML** als je de voorkeur geeft aan een open‑source bibliotheek; de API is vergelijkbaar maar gebruikt `IXLTable` en `IXLRows`.  
* Combineer rij‑verwijderlogica met LINQ‑queries om complexere data‑cleaning‑pijplijnen te bouwen.

Veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [how to delete rows in Excel with C# – protect table header](/cells/english/net/row-and-column-management/how-to-delete-rows-in-excel-with-c-protect-table-header/)
- [How to use Aspose.Cells to delete rows in an Excel table while keeping the](/cells/english/net/row-and-column-management/how-to-use-aspose-cells-to-delete-rows-in-an-excel-table-whi/)
- [Load Excel File C# – How to Delete Rows and Remove Specific Rows](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}