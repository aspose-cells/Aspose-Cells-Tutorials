---
category: general
date: 2026-08-11
description: Hoe een tabel in Excel te hernoemen met C# en Aspose.Cells. Leer een
  Excel-werkmap te maken, een benoemd bereik toe te voegen en hernoemconflicten te
  vermijden.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rename table
- create excel workbook
- add named range
- how to add range
- rename excel table
language: nl
lastmod: 2026-08-11
og_description: Hoe een tabel in Excel te hernoemen met C# en Aspose.Cells. Deze gids
  laat zien hoe je een Excel-werkmap maakt, een benoemd bereik toevoegt en veilig
  een Excel-tabel hernoemt.
og_image_alt: Screenshot of C# code that renames an Excel table
og_title: Hoe een tabel in Excel te hernoemen met C# – volledige programmeertutorial
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: How to rename table in Excel with C# using Aspose.Cells. Learn to create
    Excel workbook, add named range, and avoid rename conflicts.
  headline: How to rename table in Excel with C# – step‑by‑step guide
  type: TechArticle
- description: How to rename table in Excel with C# using Aspose.Cells. Learn to create
    Excel workbook, add named range, and avoid rename conflicts.
  name: How to rename table in Excel with C# – step‑by‑step guide
  steps:
  - name: '**Create Excel workbook** – instantiate a `Workbook` and add some sample
      data.'
    text: '**Create Excel workbook** – instantiate a `Workbook` and add some sample
      data.'
  - name: '**Add a named range** – use `Worksheets.Names.Add` to create a range called
      `MyRange`.'
    text: '**Add a named range** – use `Worksheets.Names.Add` to create a range called
      `MyRange`.'
  - name: '**Create an Excel table (ListObject)** – convert the data into a table
      so we have something to rename.'
    text: '**Create an Excel table (ListObject)** – convert the data into a table
      so we have something to rename.'
  - name: '**Rename the table** – attempt to set the table’s `Name` property to the
      same identifier as the named range.'
    text: '**Rename the table** – attempt to set the table’s `Name` property to the
      same identifier as the named range.'
  - name: '**Handle name conflicts** – catch the exception, explain why it occurs,
      and show a safe rename strategy.'
    text: '**Handle name conflicts** – catch the exception, explain why it occurs,
      and show a safe rename strategy.'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: Hoe een tabel in Excel te hernoemen met C# – stapsgewijze handleiding
url: /nl/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een tabel in Excel te hernoemen met C# – stapsgewijze gids

Als je **how to rename table** in een Excel‑bestand programmatisch moet uitvoeren, laat deze tutorial je de exacte aanpak zien met Aspose.Cells voor .NET. Je ziet hoe je een **create Excel workbook** maakt, een **named range** definieert en een bestaande Excel‑tabel hernoemt zonder een naamconflict te veroorzaken.

De oplossing werkt voor elk .NET‑project dat .NET 6 of hoger target en vereist alleen het Aspose.Cells NuGet‑pakket. Aan het einde van de gids kun je een Excel‑tabel veilig hernoemen en begrijp je waarom een conflict kan ontstaan wanneer een tabelnaam overeenkomt met een gedefinieerde range.

## Voorvereisten

- .NET 6 SDK of nieuwer geïnstalleerd  
- Visual Studio 2022 (of een andere C#‑IDE)  
- Aspose.Cells for .NET‑pakket (`dotnet add package Aspose.Cells`)  

Er zijn geen extra Excel‑interop‑assemblies nodig omdat Aspose.Cells volledig in het geheugen werkt.

## Overzicht van de oplossing

1. **Create Excel workbook** – instantiate een `Workbook` en voeg wat voorbeeldgegevens toe.  
2. **Add a named range** – gebruik `Worksheets.Names.Add` om een range genaamd `MyRange` te maken.  
3. **Create an Excel table (ListObject)** – zet de gegevens om in een tabel zodat we iets hebben om te hernoemen.  
4. **Rename the table** – probeer de `Name`‑eigenschap van de tabel in te stellen op dezelfde identifier als de named range.  
5. **Handle name conflicts** – vang de uitzondering op, leg uit waarom deze optreedt en toon een veilige hernoemstrategie.

Elke stap wordt hieronder in detail uitgelegd.

## Stap 1: Hoe een Excel‑workbook te maken en gegevens te vullen

Een workbook maken is de basis voor elke Excel‑automatiseringstaak. De `Workbook`‑klasse vertegenwoordigt het volledige bestand in het geheugen.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Fill some sample data in cells A1:C4
        sheet.Cells["A1"].PutValue("ID");
        sheet.Cells["B1"].PutValue("Name");
        sheet.Cells["C1"].PutValue("Score");

        sheet.Cells["A2"].PutValue(1);
        sheet.Cells["B2"].PutValue("Alice");
        sheet.Cells["C2"].PutValue(85);

        sheet.Cells["A3"].PutValue(2);
        sheet.Cells["B3"].PutValue("Bob");
        sheet.Cells["C3"].PutValue(92);

        sheet.Cells["A4"].PutValue(3);
        sheet.Cells["B4"].PutValue("Carol");
        sheet.Cells["C4"].PutValue(78);
```

**Waarom dit belangrijk is:** Het workbook moet gegevens bevatten voordat je een tabel kunt maken. Aspose.Cells slaat gegevens op in een nul‑gebaseerde collectie, dus `Worksheets[0]` verwijst altijd naar het eerste blad.

## Stap 2: Hoe een named range toe te voegen aan het werkblad

Een **named range** stelt je in staat om naar een specifieke cel of range te verwijzen met een vriendelijke identifier. Een range toevoegen is eenvoudig:

```csharp
        // 2️⃣ Define a named range called "MyRange" that points to cell A1
        // The range string follows Excel notation: SheetName!$A$1
        workbook.Worksheets.Names.Add("MyRange", "Sheet1!$A$1");
```

**Waarom dit belangrijk is:** Named ranges worden opgeslagen in de globale naamcollectie van het workbook. Als later een tabel dezelfde naam krijgt, gooit Aspose.Cells een `CellException` omdat Excel geen dubbele namen toestaat.

## Stap 3: Hoe een Excel‑tabel (ListObject) toe te voegen

Een tabel biedt gestructureerde gegevensverwerking, filteren en opmaken. In Aspose.Cells heet dit een **ListObject**.

```csharp
        // 3️⃣ Convert the data range A1:C4 into an Excel table
        // The range string includes the header row.
        int firstRow = 0;   // zero‑based index for row 1
        int firstCol = 0;   // column A
        int totalRows = 4;  // rows 1‑4
        int totalCols = 3;  // columns A‑C

        // Create the ListObject (table) and give it an initial name
        ListObject table = sheet.ListObjects[sheet.ListObjects.Add(firstRow, firstCol, totalRows, totalCols, true)];
        table.Name = "InitialTable";
```

**Waarom dit belangrijk is:** De tabel bestaat nu met de naam `InitialTable`. Het hernoemen ervan demonstreert het **how to rename table**‑proces.

## Stap 4: Hoe een Excel‑tabel te hernoemen en conflicten af te handelen

Proberen de tabel te hernoemen naar `MyRange` botst met de eerder gemaakte named range. De onderstaande code toont het juiste patroon om het conflict te detecteren en op te lossen.

```csharp
        // 4️⃣ Try to rename the table to "MyRange"
        try
        {
            table.Name = "MyRange";   // This will raise an exception
            Console.WriteLine("Table renamed successfully.");
        }
        catch (Exception ex)
        {
            // 5️⃣ Handle the name conflict gracefully
            Console.WriteLine("Name conflict detected: " + ex.Message);

            // Resolve by choosing a unique name
            string safeName = GetUniqueTableName(workbook, "MyRange");
            table.Name = safeName;
            Console.WriteLine($"Table renamed to safe identifier: {safeName}");
        }

        // Save the workbook to verify the result
        workbook.Save("RenamedTable.xlsx");
    }

    /// <summary>
    /// Generates a unique table name that does not exist as a named range or another table.
    /// </summary>
    static string GetUniqueTableName(Workbook wb, string baseName)
    {
        int counter = 1;
        string candidate = baseName + "_" + counter;

        // Check against workbook names and existing table names
        while (NameExists(wb, candidate))
        {
            counter++;
            candidate = baseName + "_" + counter;
        }
        return candidate;
    }

    /// <summary>
    /// Returns true if the identifier is already used as a named range or table name.
    /// </summary>
    static bool NameExists(Workbook wb, string name)
    {
        // Check named ranges
        foreach (Name n in wb.Worksheets.Names)
        {
            if (string.Equals(n.TextToRefer, name, StringComparison.OrdinalIgnoreCase))
                return true;
        }

        // Check existing tables
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (ListObject lo in ws.ListObjects)
            {
                if (string.Equals(lo.Name, name, StringComparison.OrdinalIgnoreCase))
                    return true;
            }
        }
        return false;
    }
}
```

### Wat de code doet

| Stap | Actie | Reden |
|------|-------|-------|
| **Probeer hernoemen** | `table.Name = "MyRange"` | Demonstreert het conflictscenario. |
| **Vang uitzondering** | Print het conflictbericht. | Geeft je directe feedback over het probleem. |
| **Genereer veilige naam** | `GetUniqueTableName` voegt een numeriek achtervoegsel toe totdat de naam vrij is. | Garandeert dat de nieuwe tabelnaam **niet** botst met een bestaande named range of tabel. |
| **Sla workbook op** | `workbook.Save("RenamedTable.xlsx")` | Slaat de wijzigingen op zodat je het bestand in Excel kunt openen en het resultaat kunt verifiëren. |

**Verwachte output** wanneer je het programma uitvoert:

```
Name conflict detected: A name with the same text already exists.
Table renamed to safe identifier: MyRange_1
```

Het openen van `RenamedTable.xlsx` toont een tabel met de naam `MyRange_1` en een aparte named range `MyRange` die naar cel A1 wijst.

## Waarom het conflict ontstaat en beste praktijken voor het hernoemen van een Excel‑tabel

- Excel slaat **named ranges** en **tabelnamen** op in dezelfde namespace.  
- Wanneer je een tabelnaam probeert toe te wijzen die al bestaat als range, gooit Aspose.Cells een `CellException`.  
- De aanbevolen aanpak is om **eerst te controleren op bestaande namen** (zoals getoond in `NameExists`) of een naamgevingsconventie te gebruiken die uniekheid garandeert (bijv. tabellen laten beginnen met `tbl_`).  

Door dit patroon toe te passen voorkom je runtime‑fouten en maak je je automatisering robuust.

## Extra tips voor het werken met Aspose.Cells

- **Pro tip:** Gebruik `Workbook.Worksheets.Names.Remove("MyRange")` als je de range bewust wilt vervangen door een tabelnaam.  
- **Let op hoofdlettergevoeligheid:** Excel behandelt namen hoofdletter‑onafhankelijk; de hulpfuncties gebruiken `OrdinalIgnoreCase` om het gedrag van Excel te emuleren.  
- **Prestaties:** Als je veel werkbladen verwerkt, cache dan de naamcollectie in plaats van herhaaldelijk te itereren.

## Volledig voorbeeld in één blok

Hieronder staat het volledige programma dat je kunt copy‑pasten in een console‑project. Het bevat alle stappen van het maken van het workbook tot het veilig hernoemen van de tabel.

```csharp
using System;
using Aspose.Cells;

class RenameTableDemo
{
    static void Main()
    {
        // Create workbook and populate data
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        sheet.Cells["A1"].PutValue("ID");
        sheet.Cells["B1"].PutValue("Name");
        sheet.Cells["C1"].PutValue("Score");

        sheet.Cells["A2"].PutValue(1);
        sheet.Cells["B2"].PutValue("Alice");
        sheet.Cells["C2"].PutValue(85);

        sheet.Cells["A3"].PutValue(2);
        sheet.Cells["B3"].PutValue("Bob");
        sheet.Cells["C3"].PutValue(92);

        sheet.Cells["A4"].PutValue(3);
        sheet.Cells["B4"].PutValue("Carol");
        sheet.Cells["C4"].PutValue(78);

        // Add named range "MyRange" pointing to A1
        workbook.Worksheets.Names.Add("MyRange", "Sheet1!$A$1");

        // Convert the data range into a table named "InitialTable"
        ListObject table = sheet.ListObjects[sheet.ListObjects.Add(0, 0, 4, 3, true)];
        table.Name = "InitialTable";

        // Attempt to rename the table to "MyRange" – this will conflict
        try
        {
            table.Name = "MyRange";
            Console


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [How to Implement Named Range Formulas in .NET using Aspose.Cells for Excel Automation](/cells/english/net/formulas-functions/implement-named-range-formulas-net-aspose-cells/)
- [How to Add Slicers to Excel Tables Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/advanced-features/add-slicers-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}