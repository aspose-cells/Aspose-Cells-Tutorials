---
category: general
date: 2026-09-27
description: Leer hoe je rijen uit een Excel‑tabel verwijdert in C# met een stapsgewijze
  handleiding die ook laat zien hoe je snel een Excel‑werkmap laadt in C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: nl
lastmod: 2026-09-27
og_description: Verwijder rijen uit een Excel‑tabel in C# met een duidelijk voorbeeld.
  Deze tutorial behandelt ook hoe je een Excel‑werkmap laadt in C# en veelvoorkomende
  randgevallen afhandelt.
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: Rijen verwijderen uit Excel‑tabel in C# – volledige codegids
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  headline: How to delete rows from Excel table using C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  name: How to delete rows from Excel table using C#
  steps:
  - name: What if the table has a different name or position?
    text: '* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
      * **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches
      a condition (e.g., column header names). * **Dynamic row count:** You can compute
      `rowCount` at runtime by inspecting `ws.ListObjects[0].Dat'
  - name: Edge‑case handling
    text: '| Situation | Recommended code change | |----------------------------------------|--------------------------------------------------------------|
      | Table is empty or has fewer rows | Check `ws.ListObjects[0].DataRange.RowCount`
      before deleting. | | Rows to delete exceed table size | Clamp `rowCount`'
  - name: How do I delete rows from **all** tables in a workbook?
    text: '```csharp foreach (Worksheet sheet in workbook.Worksheets) { foreach (ListObject
      tbl in sheet.ListObjects) { // Example: delete the first data row of each table
      if (tbl.DataRange.RowCount > 1) tbl.DeleteRows(1, 1); } } ```'
  - name: Can I delete rows based on a **cell value**?
    text: 'Yes. Scan the `DataRange` for matching cells, collect their zero‑based
      indices, then delete in descending order:'
  - name: What if I need to **preserve formatting**?
    text: '`DeleteRows` removes the entire row from the table but retains the table’s
      style for remaining rows. If you need to keep specific formatting on a row you’re
      deleting, copy the style to another row before deletion.'
  - name: Does this work with **.xls** (Excel 97‑2003) files?
    text: Yes. Aspose.Cells automatically detects the file format, so the same code
      works with `.xls`. Just change the file extension in the `Workbook` constructor.
  - name: Next steps
    text: '* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source
      stack. * Combine row deletion with **data validation** to clean spreadsheets
      before importing into a database. * Automate the process for a folder of workbooks
      using `Directory.GetFiles` and a loop.'
  type: HowTo
tags:
- Excel
- C#
- .NET
title: Hoe rijen uit een Excel‑tabel te verwijderen met C#
url: /nl/net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rijen verwijderen uit Excel-tabel in C# – volledige programmeergids

Als je **rijen uit een Excel-tabel** moet verwijderen in een .xlsx‑bestand, laat deze tutorial je precies zien hoe je dat doet met C#. Je ziet een beknopt, uitvoerbaar voorbeeld dat een Excel‑werkmap laadt, specifieke rijen uit de eerste tabel verwijdert en het resultaat opslaat. De aanpak werkt met de populaire Aspose.Cells‑bibliotheek en kan worden aangepast aan andere .NET Excel‑API's.

Rijen uit een tabel verwijderen is een veelvoorkomende taak bij het opschonen van geïmporteerde gegevens, het inkorten van rapportsecties of het automatiseren van spreadsheet‑updates. Aan het einde van deze gids kun je **Excel-werkmap laden C#**, een tabel (ListObject) vinden, willekeurige rijen verwijderen en het gewijzigde bestand terug naar schijf schrijven.

## Vereisten

* .NET 6.0 of later geïnstalleerd (de code werkt ook met .NET Framework 4.7+).
* Een referentie naar het **Aspose.Cells** NuGet‑pakket (of een compatibele bibliotheek die de typen `Workbook`, `Worksheet` en `ListObject` beschikbaar maakt).
* Een invoerbestand met de naam `input.xlsx` geplaatst in een map die je vanuit je project kunt refereren.
* Basiskennis van C#‑syntaxis en Visual Studio (of je favoriete IDE).

> **Pro tip:** Als je de voorkeur geeft aan een open‑source alternatief, kan dezelfde logica worden toegepast met **ClosedXML** – vervang gewoon de Aspose‑specifieke klassen door `XLWorkbook`, `IXLWorksheet` en `IXLTable`.

## Stap 1: Laad de Excel-werkmap in C#

De eerste bewerking is het lezen van het bronbestand in het geheugen. Het laden van de werkmap is goedkoop voor typische spreadsheet‑groottes en geeft je volledige toegang tot werkbladen, tabellen en celwaarden.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*Waarom dit belangrijk is:* `Workbook` parseert de Open XML‑structuur van het .xlsx‑bestand en maakt een collectie van `Worksheet`‑objecten beschikbaar. Als het bestand niet gevonden kan worden, gooit Aspose een `FileNotFoundException`, zorg er dus voor dat het pad correct is.

## Stap 2: Toegang tot het doel‑werkblad

De meeste spreadsheets bevatten meerdere bladen; je moet het blad kiezen dat de tabel bevat die je wilt aanpassen. Hier gebruiken we het eerste blad (`Worksheets[0]`), wat een veilige standaard is voor eenvoudige bestanden.

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*Waarom dit belangrijk is:* `Worksheet` is de container voor tabellen (`ListObjects`). Het openen van het juiste blad voorkomt per ongeluk wijzigingen in niet‑gerelateerde gegevens.

## Stap 3: Rijen verwijderen uit Excel‑tabel

Excel‑tabellen worden weergegeven door `ListObject`‑objecten. De eerste tabel op het blad is `ListObjects[0]`. De methode `DeleteRows(startIndex, rowCount)` verwijdert rijen **relatief ten opzichte van het gegevensgebied van de tabel**, niet ten opzichte van de absolute rijnummers van het werkblad.  

In dit voorbeeld verwijderen we de tweede en derde rij van de tabel (de kop is rij 0, dus we beginnen bij index 1).

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### Wat als de tabel een andere naam of positie heeft?

* **Naamgegeven tabel:** Gebruik `ws.ListObjects["MyTableName"]` in plaats van de index.
* **Meerdere tabellen:** Loop door `ws.ListObjects` en kies degene die aan een voorwaarde voldoet (bijv. kolomkop‑namen).
* **Dynamisch aantal rijen:** Je kunt `rowCount` berekenen tijdens runtime door `ws.ListObjects[0].DataRange.RowCount` te inspecteren.

### Afhandeling van randgevallen

| Situatie                              | Aanbevolen code‑wijziging                                      |
|----------------------------------------|--------------------------------------------------------------|
| Tabel is leeg of heeft minder rijen      | Controleer `ws.ListObjects[0].DataRange.RowCount` vóór het verwijderen. |
| Rijen die moeten worden verwijderd overschrijden de tabelgrootte       | Beperk `rowCount` tot `DataRange.RowCount - startIndex`.       |
| Rijen moeten worden verwijderd op basis van een voorwaarde (bijv. waarde in kolom C) | Loop door `DataRange.Rows` en verzamel overeenkomende indices, verwijder vervolgens in omgekeerde volgorde om indices stabiel te houden. |

## Stap 4: Sla de gewijzigde werkmap op

Na het verwijderen, schrijf je de werkmap terug naar een nieuw bestand (of overschrijf het origineel als je dat wilt). Opslaan maakt een nieuw .xlsx‑bestand aan dat de bijgewerkte tabel weergeeft.

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*Waarom dit belangrijk is:* `Save` serialiseert de in‑memory representatie naar schijf. Als je het originele bestand wilt behouden, schrijf dan altijd naar een ander pad.

## Volledig, uitvoerbaar voorbeeld

Alle stappen samenvoegen levert een zelfstandige applicatie op die je kunt kopiëren, plakken en uitvoeren.

```csharp
using System;
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Adjust the folder path as needed
        const string folder = @"YOUR_DIRECTORY";

        // Load the workbook (load Excel workbook C#)
        Workbook workbook = new Workbook($"{folder}\\input.xlsx");

        // Access the first worksheet
        Worksheet ws = workbook.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (ws.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Delete rows 1 and 2 from the first table (skip header)
        ListObject table = ws.ListObjects[0];
        int rowsToDelete = Math.Min(2, table.DataRange.RowCount - 1); // guard against short tables
        if (rowsToDelete > 0)
        {
            table.DeleteRows(1, rowsToDelete);
            Console.WriteLine($"Deleted {rowsToDelete} row(s) from table \"{table.Name}\".");
        }
        else
        {
            Console.WriteLine("Table does not have enough rows to delete.");
        }

        // Save the result
        workbook.Save($"{folder}\\output.xlsx");
        Console.WriteLine("Workbook saved as output.xlsx");
    }
}
```

**Verwachte output** (console):

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

Open `output.xlsx` – de eerste tabel mist nu de rijen die je hebt verwijderd, terwijl de koprij intact blijft.

## Veelgestelde vragen en variaties

### Hoe verwijder ik rijen uit **alle** tabellen in een werkmap?

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (ListObject tbl in sheet.ListObjects)
    {
        // Example: delete the first data row of each table
        if (tbl.DataRange.RowCount > 1)
            tbl.DeleteRows(1, 1);
    }
}
```

### Kan ik rijen verwijderen op basis van een **celwaarde**?

Ja. Scan de `DataRange` op overeenkomende cellen, verzamel hun nul‑gebaseerde indices en verwijder vervolgens in aflopende volgorde:

```csharp
var rowsToRemove = new List<int>();
for (int i = 0; i < table.DataRange.RowCount; i++)
{
    var cell = table.DataRange[i, 2]; // column C (zero‑based)
    if (cell.StringValue == "Obsolete")
        rowsToRemove.Add(i);
}

// Delete rows from bottom to top to keep indices valid
rowsToRemove.Sort((a, b) => b.CompareTo(a));
foreach (int rowIdx in rowsToRemove)
    table.DeleteRows(rowIdx, 1);
```

### Wat als ik de **opmaak moet behouden**?

`DeleteRows` verwijdert de volledige rij uit de tabel maar behoudt de tabel‑stijl voor de resterende rijen. Als je specifieke opmaak op een te verwijderen rij wilt behouden, kopieer dan de stijl naar een andere rij vóór het verwijderen.

### Werkt dit met **.xls** (Excel 97‑2003) bestanden?

Ja. Aspose.Cells detecteert automatisch het bestandsformaat, dus dezelfde code werkt met `.xls`. Verander gewoon de bestandsextensie in de `Workbook`‑constructor.

## Prestatietips

* **Batch‑verwijderingen:** Veel rijen één voor één verwijderen kan trager zijn. Gebruik een enkele `DeleteRows(start, count)`‑aanroep wanneer mogelijk.
* **Voorkom blokkering van de UI‑thread:** Als je dit in een desktop‑applicatie integreert, voer de werkmap‑manipulatie uit op een achtergrondthread om de UI responsief te houden.
* **Correct opruimen:** Hoewel Aspose.Cells beheerd geheugen gebruikt, wikkel de `Workbook` in een `using`‑blok als je met grote bestanden werkt om bronnen snel vrij te geven.

## Conclusie

Je hebt nu een compleet, productie‑klaar voorbeeld dat **rijen uit een Excel‑tabel** verwijdert met C#. De gids behandelde hoe je **Excel-werkmap laadt C#**, het gewenste `ListObject` vindt, veilig rijen verwijdert en het bijgewerkte bestand opslaat. Met de opgenomen afhandeling van randgevallen en prestatie‑adviezen kun je dit patroon aanpassen aan complexere scenario's zoals voorwaardelijke verwijderingen, meerdere tabellen of alternatieve .NET Excel‑bibliotheken.

### Volgende stappen

* Verken **ClosedXML** of **EPPlus** als je de voorkeur geeft aan een volledig open‑source stack.
* Combineer rijenverwijdering met **datavalidatie** om spreadsheets op te schonen voordat je ze in een database importeert.
* Automatiseer het proces voor een map met werkmappen met behulp van `Directory.GetFiles` en een lus.

Voel je vrij om te experimenteren met verschillende rijenbereiken, tabelnamen en voorwaardelijke logica. Veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Load Excel File C# – How to Delete Rows and Remove Specific Rows](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [How to Insert and Delete Rows in Excel with Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [How to Delete Blank Rows in Excel Using Aspose.Cells .NET for Data Cleanup](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}