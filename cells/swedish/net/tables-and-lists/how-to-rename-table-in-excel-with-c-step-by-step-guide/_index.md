---
category: general
date: 2026-08-11
description: Hur man byter namn på en tabell i Excel med C# och Aspose.Cells. Lär
  dig att skapa en Excel-arbetsbok, lägga till ett namngivet område och undvika namnbytningskonflikter.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rename table
- create excel workbook
- add named range
- how to add range
- rename excel table
language: sv
lastmod: 2026-08-11
og_description: Hur man byter namn på en tabell i Excel med C# och Aspose.Cells. Den
  här guiden visar hur du skapar en Excel-arbetsbok, lägger till ett namngivet område
  och säkert byter namn på en Excel-tabell.
og_image_alt: Screenshot of C# code that renames an Excel table
og_title: Hur man byter namn på en tabell i Excel med C# – komplett programmeringshandledning
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
title: Hur du byter namn på en tabell i Excel med C# – steg‑för‑steg‑guide
url: /sv/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man byter namn på en tabell i Excel med C# – steg‑för‑steg‑guide

Om du behöver **byta namn på en tabell** i en Excel‑fil programatiskt, visar den här handledningen den exakta metoden med Aspose.Cells för .NET. Du får se hur du **skapar en Excel‑arbetsbok**, definierar ett **namngivet område** och byter namn på en befintlig Excel‑tabell utan att orsaka en namnkonflikt.

Lösningen fungerar för alla .NET‑projekt som riktar sig mot .NET 6 eller senare och kräver endast Aspose.Cells‑NuGet‑paketet. I slutet av guiden kan du säkert byta namn på en Excel‑tabell och förstå varför en konflikt kan uppstå när ett tabellnamn matchar ett definierat område.

## Förutsättningar

- .NET 6 SDK eller nyare installerat  
- Visual Studio 2022 (eller någon C#‑IDE)  
- Aspose.Cells för .NET‑paketet (`dotnet add package Aspose.Cells`)  

Inga ytterligare Excel‑interop‑assemblys behövs eftersom Aspose.Cells arbetar helt i minnet.

## Översikt av lösningen

1. **Skapa Excel‑arbetsbok** – instansiera ett `Workbook` och lägg till lite exempeldata.  
2. **Lägg till ett namngivet område** – använd `Worksheets.Names.Add` för att skapa ett område som heter `MyRange`.  
3. **Skapa en Excel‑tabell (ListObject)** – konvertera data till en tabell så att vi har något att byta namn på.  
4. **Byt namn på tabellen** – försök att sätta tabellens `Name`‑egenskap till samma identifierare som det namngivna området.  
5. **Hantera namnkonflikter** – fånga undantaget, förklara varför det uppstår och visa en säker namnbytesstrategi.

Varje steg förklaras i detalj nedan.

## Steg 1: Hur man skapar Excel‑arbetsbok och fyller i data

Att skapa en arbetsbok är grunden för alla Excel‑automatiseringsuppgifter. Klassen `Workbook` representerar hela filen i minnet.

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

**Varför detta är viktigt:** Arbetsboken måste innehålla data innan du kan skapa en tabell. Aspose.Cells lagrar data i en noll‑baserad samling, så `Worksheets[0]` refererar alltid till det första bladet.

## Steg 2: Hur man lägger till ett namngivet område i kalkylbladet

Ett **namngivet område** låter dig referera till en specifik cell eller ett område med en vänlig identifierare. Att lägga till ett område är enkelt:

```csharp
        // 2️⃣ Define a named range called "MyRange" that points to cell A1
        // The range string follows Excel notation: SheetName!$A$1
        workbook.Worksheets.Names.Add("MyRange", "Sheet1!$A$1");
```

**Varför detta är viktigt:** Namngivna områden lagras i arbetsbokens globala namn‑samling. Om en tabell senare får samma namn, kastar Aspose.Cells ett `CellException` eftersom Excel inte tillåter duplicerade namn.

## Steg 3: Hur man lägger till en Excel‑tabell (ListObject)

En tabell ger strukturerad datahantering, filtrering och formatering. I Aspose.Cells kallas den för en **ListObject**.

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

**Varför detta är viktigt:** Tabellen finns nu med namnet `InitialTable`. Att byta namn på den demonstrerar processen **hur man byter namn på en tabell**.

## Steg 4: Hur man byter namn på en Excel‑tabell och hanterar konflikter

Att försöka byta namn på tabellen till `MyRange` kommer att kollidera med det namngivna området vi skapade tidigare. Följande kod visar det korrekta mönstret för att upptäcka och lösa konflikten.

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

### Vad koden gör

| Steg | Åtgärd | Orsak |
|------|--------|--------|
| **Försök byta namn** | `table.Name = "MyRange"` | Demonstrerar konflikt‑scenariot. |
| **Fånga undantag** | Skriver ut konfliktmeddelandet. | Ger dig omedelbar återkoppling om problemet. |
| **Generera säkert namn** | `GetUniqueTableName` lägger till ett numeriskt suffix tills namnet är fritt. | Säkerställer att det nya tabellnamnet **inte** kolliderar med något befintligt namngivet område eller tabell. |
| **Spara arbetsbok** | `workbook.Save("RenamedTable.xlsx")` | Sparar ändringarna så att du kan öppna filen i Excel och verifiera resultatet. |

**Förväntat resultat** när du kör programmet:

```
Name conflict detected: A name with the same text already exists.
Table renamed to safe identifier: MyRange_1
```

När du öppnar `RenamedTable.xlsx` visas en tabell med namnet `MyRange_1` och ett separat namngivet område `MyRange` som pekar på cell A1.

## Varför konflikten uppstår och bästa praxis för att byta namn på en Excel‑tabell

- Excel lagrar **namngivna områden** och **tabellnamn** i samma namnrymd.  
- När du försöker tilldela ett tabellnamn som redan finns som ett område, kastar Aspose.Cells ett `CellException`.  
- Den rekommenderade metoden är att **kontrollera befintliga namn först** (som visas i `NameExists`) eller att använda en namnkonvention som garanterar unikhet (t.ex. prefixa tabeller med `tbl_`).  

Genom att följa detta mönster undviker du körningsfel och gör din automatisering robust.

## Ytterligare tips för att arbeta med Aspose.Cells

- **Proffstips:** Använd `Workbook.Worksheets.Names.Remove("MyRange")` om du avsiktligt vill ersätta området med ett tabellnamn.  
- **Var uppmärksam på skiftlägeskänslighet:** Excel behandlar namn skiftläges‑okänsligt; hjälpfunktionerna använder `OrdinalIgnoreCase` för att efterlikna Excels beteende.  
- **Prestanda:** Om du bearbetar många kalkylblad, cachea namn‑samlingen istället för att iterera upprepade gånger.

## Fullständigt exempel i ett block

Nedan är hela programmet som du kan kopiera‑klistra in i ett konsolprojekt. Det inkluderar alla steg från att skapa arbetsboken till att säkert byta namn på tabellen.

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


## Vad du bör lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man skapar arbetsboks‑omfattande namngivna områden i Excel med Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [Hur man implementerar formler med namngivna områden i .NET med Aspose.Cells för Excel‑automatisering](/cells/english/net/formulas-functions/implement-named-range-formulas-net-aspose-cells/)
- [Hur man lägger till slicers i Excel‑tabeller med Aspose.Cells för .NET: En omfattande guide](/cells/english/net/advanced-features/add-slicers-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}