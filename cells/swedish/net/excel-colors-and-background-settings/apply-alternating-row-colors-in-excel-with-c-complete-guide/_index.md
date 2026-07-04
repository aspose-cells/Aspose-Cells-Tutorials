---
category: general
date: 2026-07-03
description: Applicera alternerande radfärger när du importerar en datatabell till
  Excel med C#. Lär dig hur du exporterar en C#‑datatabell till Excel, sparar en stiliserad
  Excel‑tabell och behåller arbetsbokens formatering.
draft: false
keywords:
- apply alternating row colors
- import datatable to excel
- export c# datatable to excel
- save styled table excel
- save workbook with formatting
language: sv
og_description: Tillämpa alternerande radfärger i Excel med C#. Den här handledningen
  visar hur du importerar en datatabell till Excel, exporterar en C#‑datatabell till
  Excel och sparar arbetsboken med formatering.
og_title: Applicera alternerande radfärger i Excel med C# – Komplett guide
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  headline: Apply Alternating Row Colors in Excel with C# – Complete Guide
  type: TechArticle
- description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  name: Apply Alternating Row Colors in Excel with C# – Complete Guide
  steps:
  - name: Expected Output
    text: '| ID | Name | Department | HireDate | |----|---------|------------|------------|
      | 1 | Alice | Finance | 15‑01‑2020 | | 2 | Bob | HR | 23‑06‑2019 | | 3 | Charlie
      | IT | 10‑03‑2021 | | 4 | Diana | Marketing | 05‑11‑2018 |'
  - name: What if my DataTable has thousands of rows?
    text: The `ImportDataTable` method streams data efficiently, but you might hit
      memory limits on very large tables. In such cases, consider splitting the export
      into multiple worksheets or using the `ImportDataTable` overload that lets you
      specify a start row and column.
  - name: Can I use custom colors instead of the built‑in ones?
    text: Absolutely. Just replace the `ForegroundColor` assignments in `styleWhite`
      and `styleGray` with any `System.Drawing.Color` you prefer—think pastel blues
      or corporate brand colors.
  - name: How do I ensure the alternating style works when the user adds rows later?
    text: If users edit the file manually, the original style array won’t automatically
      extend. A quick workaround is to convert the range into an Excel Table (`ListObject`)
      after import; Excel then repeats the pattern for new rows.
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataExport
title: Applicera alternerande radfärger i Excel med C# – Komplett guide
url: /sv/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Applicera alternerande radfärger i Excel med C# – Komplett guide

Har du någonsin behövt **apply alternating row colors** när du exporterar en C# `DataTable` till Excel? Du är inte ensam—utvecklare frågar ständigt hur man får kalkylbladen att se polerade ut utan att manuellt pilla i Excel i efterhand. Den goda nyheten? Du kan göra det programatiskt på bara några rader kod.

I den här handledningen går vi igenom **import datatable to excel**, visar hur du **export c# datatable to excel** med ett stylat bord, och slutligen **save styled table excel** samtidigt som formateringen bevaras. I slutet kommer du kunna **save workbook with formatting** som ser klar ut för ett kundmöte.

## Förutsättningar

- .NET 6.0 eller senare (exemplet använder .NET 6, men alla nyare versioner fungerar)
- Aspose.Cells för .NET (gratis provversion eller licensierad version) – detta bibliotek gör styling enkelt
- En `DataTable`-källa (kan komma från en databas, CSV eller en minnesbaserad samling)

> **Pro tip:** Om du ännu inte har Aspose.Cells kan du hämta det från NuGet med `dotnet add package Aspose.Cells`.

## Steg 1: Ställ in projektet och ladda dina data

Först, skapa en konsolapp (eller vilket C#-projekt som helst) och lägg till de nödvändiga `using`-satserna. Hämta sedan data till en `DataTable`. För illustration kommer vi att generera ett enkelt bord i farten.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Retrieve the source data as a DataTable
        DataTable sourceTable = GetSampleData();

        // The rest of the steps follow...
    }

    // Helper that creates a dummy DataTable
    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

**Why this matters:** Att ha en `DataTable` redo betyder att du kan **import datatable to excel** i ett enda anrop, vilket eliminerar behovet av manuell cell‑för‑cell‑insättning.

## Steg 2: Skapa en arbetsbok och definiera de alternerande radstilarna

Nu kommer vi att instansiera en ny `Workbook`. Tricket för att **apply alternating row colors** ligger i `ImportTableOptions.StyleArray`. Vi kommer att använda de två första inbyggda stilarna (vanligtvis vit och ljusgrå) men du kan anpassa dem senare.

```csharp
// Step 2: Create a new workbook
Workbook workbook = new Workbook();

// Define two simple styles: white (default) and light gray
Style styleWhite = workbook.Styles[workbook.Styles.Add()];
styleWhite.ForegroundColor = System.Drawing.Color.White;
styleWhite.Pattern = BackgroundType.Solid;

Style styleGray = workbook.Styles[workbook.Styles.Add()];
styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242); // light gray
styleGray.Pattern = BackgroundType.Solid;

// Step 3: Set up ImportTableOptions with the alternating styles
ImportTableOptions importOptions = new ImportTableOptions
{
    // The array alternates between the two styles for each row
    StyleArray = new Style[] { styleWhite, styleGray }
};
```

**Explanation:** `ImportTableOptions` talar om för Aspose.Cells hur varje rad ska behandlas under importen. Genom att tillhandahålla en `StyleArray` med två poster målar biblioteket automatiskt varje udda rad med den första stilen och varje jämn rad med den andra—precis vad du behöver för att **apply alternating row colors**.

## Steg 3: Hämta DataTable till kalkylbladet (inklusive rubriker)

Med arbetsboken och stilarna klara, **import datatable to excel** nu. Metoden `ImportDataTable` gör det tunga arbetet: den skriver kolumnrubrikerna, respekterar stilarrayen och placerar data med start i cell A1.

```csharp
// Step 4: Import the DataTable into the first worksheet (include column headers)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells.ImportDataTable(sourceTable, true, importOptions);
```

**Why we include `true` for the second argument:** Det talar om för metoden att skriva kolumnnamnen som den första raden, vilket är avgörande för en professionellt‑utseende rapport.

## Steg 4: Finjustera tabellen (valfritt men praktiskt)

Om du vill att tabellen automatiskt ska anpassa kolumner eller lägga till en filterrad, gör ett par extra rader den glänsande.

```csharp
// Auto‑fit all columns for readability
sheet.AutoFitColumns();

// Add a filter to the header row
sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";
```

Dessa justeringar påverkar inte de alternerande färgerna men förbättrar den övergripande användarupplevelsen av **save styled table excel**‑filen.

## Steg 5: Spara arbetsboken medan all formatering behålls

Till sist skriver vi filen till disk. Metoden `Save` bevarar varje stil vi har satt, vilket säkerställer att de alternerande raderna förblir intakta.

```csharp
// Step 5: Save the workbook with the styled table
string outputPath = @"C:\Temp\StyledEmployees.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

När du öppnar `StyledEmployees.xlsx` kommer du att se en ren tabell där raderna alternerar mellan vit och ljusgrå—precis den visuella ledtråden som många användare förlitar sig på för läsbarhet.

### Förväntad utdata

| ID | Name    | Department | HireDate   |
|----|---------|------------|------------|
| 1  | Alice   | Finance    | 15‑01‑2020 |
| 2  | Bob     | HR         | 23‑06‑2019 |
| 3  | Charlie | IT         | 10‑03‑2021 |
| 4  | Diana   | Marketing  | 05‑11‑2018 |

- Rad 1, 3 … → vit bakgrund  
- Rad 2, 4 … → ljus‑grå bakgrund  

Det är hela processen för **save workbook with formatting**.

## Vanliga frågor & specialfall

### Vad händer om min DataTable har tusentals rader?

`ImportDataTable`‑metoden strömmar data effektivt, men du kan stöta på minnesgränser på mycket stora tabeller. I sådana fall, överväg att dela upp exporten i flera kalkylblad eller använda `ImportDataTable`‑överladdningen som låter dig ange startrad och -kolumn.

### Kan jag använda egna färger istället för de inbyggda?

Absolut. Byt bara ut `ForegroundColor`‑tilldelningarna i `styleWhite` och `styleGray` mot någon `System.Drawing.Color` du föredrar—tänk pastellblått eller företagets varumärkesfärger.

```csharp
styleWhite.ForegroundColor = System.Drawing.Color.LightBlue;
styleGray.ForegroundColor = System.Drawing.Color.LightCyan;
```

### Hur säkerställer jag att den alternerande stilen fungerar när användaren lägger till rader senare?

Om användare redigerar filen manuellt kommer den ursprungliga stilarrayen inte att automatiskt utökas. En snabb lösning är att konvertera området till en Excel‑tabell (`ListObject`) efter import; Excel upprepar då mönstret för nya rader.

```csharp
int lastRow = sheet.Cells.MaxDataRow;
int lastCol = sheet.Cells.MaxDataColumn;
string tableRange = $"A1:{CellsHelper.ColumnIndexToName(lastCol)}{lastRow + 1}";
ListObject table = sheet.ListObjects[sheet.ListObjects.Add(tableRange, true)];
```

Nu ärver varje ny rad de alternerande färgerna.

## Fullt fungerande exempel (alla steg på ett ställe)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve source data
        DataTable sourceTable = GetSampleData();

        // 2️⃣ Create workbook and define alternating styles
        Workbook workbook = new Workbook();

        Style styleWhite = workbook.Styles[workbook.Styles.Add()];
        styleWhite.ForegroundColor = System.Drawing.Color.White;
        styleWhite.Pattern = BackgroundType.Solid;

        Style styleGray = workbook.Styles[workbook.Styles.Add()];
        styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242);
        styleGray.Pattern = BackgroundType.Solid;

        ImportTableOptions importOptions = new ImportTableOptions
        {
            StyleArray = new Style[] { styleWhite, styleGray }
        };

        // 3️⃣ Import DataTable (including headers)
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(sourceTable, true, importOptions);

        // 4️⃣ Optional polish
        sheet.AutoFitColumns();
        sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";

        // 5️⃣ Save the styled workbook
        string outputPath = @"C:\Temp\StyledEmployees.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

Kör programmet, öppna den genererade filen, och du kommer omedelbart att se de alternerande färgerna tillämpade—ingen manuell formatering krävs.

## Slutsats

Vi har just demonstrerat hur man **apply alternating row colors** när du **import datatable to excel** med C#. Processen täcker allt du behöver för att **export c# datatable to excel**, **save styled table excel**, och **save workbook with formatting** som ser professionell ut direkt ur lådan.

Nästa steg? Prova att byta de två stilarna mot ett eget tema, eller gör om området till en Excel‑tabell så att användare kan sortera och filtrera samtidigt som färgmönstret behålls. Du kan också utforska villkorlig formatering via `ConditionalFormattingCollection` för mer dynamiska visuella ledtrådar.

Har du en twist

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man importerar DataTable till Excel med Aspose.Cells för .NET (Steg‑för‑steg‑guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Applicera färger och bakgrunder i Excel med Aspose.Cells för .NET](/cells/english/net/formatting/colors-and-background/)
- [Automatisera Excel‑temafärger med Aspose.Cells .NET för effektiv formatering](/cells/english/net/formatting/automate-excel-theme-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}