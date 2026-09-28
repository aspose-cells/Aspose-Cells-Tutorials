---
category: general
date: 2026-09-27
description: Lär dig hur du tar bort rader från en Excel‑tabell i C# med en steg‑för‑steg‑guide
  som också visar hur du snabbt laddar en Excel‑arbetsbok i C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: sv
lastmod: 2026-09-27
og_description: Ta bort rader från en Excel‑tabell i C# med ett tydligt exempel. Denna
  handledning täcker också hur du laddar en Excel‑arbetsbok i C# och hanterar vanliga
  edge‑cases.
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: Ta bort rader från Excel‑tabell i C# – komplett kodguide
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
title: Hur man tar bort rader från en Excel‑tabell med C#
url: /sv/net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ta bort rader från Excel‑tabell i C# – komplett programmeringsguide

Om du behöver **ta bort rader från Excel‑tabell** i en .xlsx‑fil, visar den här handledningen exakt hur du gör det med C#. Du får se ett kort, körbart exempel som laddar en Excel‑arbetsbok, tar bort specifika rader från den första tabellen och sparar resultatet. Metoden fungerar med det populära Aspose.Cells‑biblioteket och kan anpassas till andra .NET‑Excel‑API:er.

Att ta bort rader från en tabell är en vanlig uppgift när man rensar importerad data, kortar ner rapportsektioner eller automatiserar kalkylbladsuppdateringar. I slutet av den här guiden kommer du att kunna **ladda Excel‑arbetsbok C#**, hitta en tabell (ListObject), ta bort valfria rader och skriva den modifierade filen tillbaka till disk.

## Förutsättningar

* .NET 6.0 eller senare installerat (koden fungerar också med .NET Framework 4.7+).
* En referens till **Aspose.Cells**‑NuGet‑paketet (eller något kompatibelt bibliotek som exponerar typerna `Workbook`, `Worksheet` och `ListObject`).
* En indatafil med namnet `input.xlsx` placerad i en mapp du kan referera till från ditt projekt.
* Grundläggande kunskap om C#‑syntax och Visual Studio (eller din föredragna IDE).

> **Proffstips:** Om du föredrar ett öppen‑källkods‑alternativ kan samma logik tillämpas med **ClosedXML** – byt bara ut de Aspose‑specifika klasserna mot `XLWorkbook`, `IXLWorksheet` och `IXLTable`.

## Steg 1: Ladda Excel‑arbetsboken i C#

Den första operationen är att läsa källfilen till minnet. Att ladda arbetsboken är snabbt för vanliga kalkylbladsstorlekar och ger dig full åtkomst till arbetsblad, tabeller och cellvärden.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*Varför detta är viktigt:* `Workbook` parsar Open XML‑strukturen i .xlsx‑filen och exponerar en samling `Worksheet`‑objekt. Om filen inte kan hittas kastar Aspose ett `FileNotFoundException`, så se till att sökvägen är korrekt.

## Steg 2: Åtkomst till mål‑arbetsbladet

De flesta kalkylblad innehåller flera blad; du måste välja det som innehåller tabellen du vill ändra. Här använder vi det första bladet (`Worksheets[0]`), vilket är ett säkert standardval för enkla filer.

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*Varför detta är viktigt:* `Worksheet` är behållaren för tabeller (`ListObjects`). Att komma åt rätt blad förhindrar oavsiktliga ändringar i orelaterad data.

## Steg 3: Ta bort rader från Excel‑tabell

Excel‑tabeller representeras av `ListObject`‑objekt. Den första tabellen på bladet är `ListObjects[0]`. Metoden `DeleteRows(startIndex, rowCount)` tar bort rader **relativt tabellens dataområde**, inte arbetsbladets absoluta radnummer.  

I detta exempel tar vi bort den andra och tredje raden i tabellen (rubriken är rad 0, så vi börjar på index 1).

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### Vad händer om tabellen har ett annat namn eller en annan position?

* **Namngiven tabell:** Använd `ws.ListObjects["MyTableName"]` istället för indexet.
* **Flera tabeller:** Loopa igenom `ws.ListObjects` och välj den som matchar ett villkor (t.ex. kolumnrubriknamn).
* **Dynamiskt radantal:** Du kan beräkna `rowCount` vid körning genom att inspektera `ws.ListObjects[0].DataRange.RowCount`.

### Hantering av kantfall

| Situation                              | Rekommenderad kodändring                                      |
|----------------------------------------|--------------------------------------------------------------|
| Tabellen är tom eller har färre rader  | Kontrollera `ws.ListObjects[0].DataRange.RowCount` innan du tar bort. |
| Rader att ta bort överstiger tabellens storlek | Begränsa `rowCount` till `DataRange.RowCount - startIndex`.       |
| Behöver ta bort rader baserat på ett villkor (t.ex. värde i kolumn C) | Iterera `DataRange.Rows` och samla matchande index, ta sedan bort i omvänd ordning för att hålla index stabila. |

## Steg 4: Spara den modifierade arbetsboken

Efter borttagningen, skriv arbetsboken tillbaka till en ny fil (eller skriv över originalet om du föredrar). Spara skapar en ny .xlsx som återspeglar den uppdaterade tabellen.

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*Varför detta är viktigt:* `Save` serialiserar den minnesbaserade representationen till disk. Om du behöver bevara originalfilen, skriv alltid till en annan sökväg.

## Fullständigt, körbart exempel

Genom att sätta ihop alla steg får du ett självständigt program som du kan kopiera, klistra in och köra.

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

**Förväntad output** (konsol):

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

Öppna `output.xlsx` – den första tabellen saknar nu de rader du tog bort, medan rubrikraden förblir intakt.

## Vanliga frågor och varianter

### Hur tar jag bort rader från **alla** tabeller i en arbetsbok?

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

### Kan jag ta bort rader baserat på ett **cellvärde**?

Ja. Skanna `DataRange` för matchande celler, samla deras noll‑baserade index och ta sedan bort i fallande ordning:

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

### Vad händer om jag behöver **bevara formatering**?

`DeleteRows` tar bort hela raden från tabellen men behåller tabellens stil för återstående rader. Om du behöver behålla specifik formatering på en rad du tar bort, kopiera stilen till en annan rad innan borttagning.

### Fungerar detta med **.xls** (Excel 97‑2003)‑filer?

Ja. Aspose.Cells upptäcker automatiskt filformatet, så samma kod fungerar med `.xls`. Ändra bara filändelsen i `Workbook`‑konstruktorn.

## Prestandatips

* **Batch‑borttagningar:** Att ta bort många rader en åt gången kan vara långsamt. Använd ett enda `DeleteRows(start, count)`‑anrop när det är möjligt.
* **Undvik UI‑trådblockering:** Om du integrerar detta i en skrivbordsapp, kör arbetsboksmanipuleringen på en bakgrundstråd för att hålla UI‑responsen.
* **Rensa korrekt:** Även om Aspose.Cells använder hanterat minne, omslut `Workbook` i ett `using`‑block om du arbetar med stora filer för att frigöra resurser snabbt.

## Slutsats

Du har nu ett komplett, produktionsklart exempel som **tar bort rader från Excel‑tabell** med C#. Guiden täckte hur du **laddar Excel‑arbetsbok C#**, hittar önskad `ListObject`, säkert tar bort rader och sparar den uppdaterade filen. Med hantering av kantfall och prestandatips kan du anpassa detta mönster till mer komplexa scenarier som villkorsstyrda borttagningar, flera tabeller eller alternativa .NET‑Excel‑bibliotek.

### Nästa steg

* Utforska **ClosedXML** eller **EPPlus** om du föredrar en helt öppen källkodstack.
* Kombinera radborttagning med **datavalidering** för att rensa kalkylblad innan import till en databas.
* Automatisera processen för en mapp med arbetsböcker med `Directory.GetFiles` och en loop.

Känn dig fri att experimentera med olika radintervall, tabellnamn och villkorslogik. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Ladda Excel‑fil C# – Hur man tar bort rader och tar bort specifika rader](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [Hur man infogar och tar bort rader i Excel med Aspose.Cells för .NET: En omfattande guide](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Hur man tar bort tomma rader i Excel med Aspose.Cells .NET för datarengöring](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}