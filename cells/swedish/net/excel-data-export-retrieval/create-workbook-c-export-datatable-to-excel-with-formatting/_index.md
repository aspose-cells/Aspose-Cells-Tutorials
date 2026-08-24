---
category: general
date: 2026-02-15
description: Skapa en arbetsbok i C# och exportera en DataTable till Excel med radformatering,
  sätt radbakgrund och automatisera Excel‑uppgifter på några minuter.
draft: false
keywords:
- create workbook c#
- excel export formatting
- export datatable excel
- set row background
- excel automation c#
language: sv
og_description: Skapa arbetsbok i C# snabbt, applicera radstilar och automatisera
  Excel‑export med kompletta kodexempel och bästa praxis‑tips.
og_title: Skapa arbetsbok i C# – Exportera DataTable till Excel med formatering
tags:
- C#
- Excel
- DataExport
title: Skapa arbetsbok C# – Exportera DataTable till Excel med formatering
url: /sv/net/excel-data-export-retrieval/create-workbook-c-export-datatable-to-excel-with-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa arbetsbok C# – Exportera DataTable till Excel med formatering

Har du någonsin behövt **create workbook C#** och dumpa en `DataTable` till Excel med anpassad styling? Du är inte ensam. I många affärsapplikationer är kravet att leverera ett snyggt formaterat kalkylblad som en icke‑teknisk användare kan öppna och förstå omedelbart.  

I den här guiden går vi igenom en komplett, färdig‑att‑köra lösning som visar dig **how to create workbook C#**, applicera **excel export formatting**, sätta en **row background**, och utnyttja **excel automation c#** för att producera en polerad fil. Inga vaga “se dokumentationen”-genvägar—bara hela koden, förklaringar till varför varje rad är viktig, och tips du faktiskt kommer att använda imorgon.

---

## Förutsättningar

- .NET 6 (eller .NET Framework 4.6+).  
- Visual Studio 2022 eller någon C#‑kompatibel IDE.  
- **Aspose.Cells for .NET** NuGet‑paketet (eller något bibliotek som exponerar `Workbook`, `Worksheet`, `Style`).  
- Grundläggande kunskap om `DataTable`.  

Om du ännu inte har Aspose.Cells, kör:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Den kostnadsfria provversionen fungerar för de flesta utvecklingsscenarier; kom bara ihåg att byta licensnyckeln innan du levererar.

![Exempel på create workbook C# som visar stylade rader i Excel]( "Exempel på create workbook C# med radbakgrundsfärger")

---

## Steg 1: Initiera arbetsboken och kalkylbladet (Create Workbook C#)

Det första du måste göra är att instansiera en `Workbook`. Tänk på det som att öppna en helt ny Excel‑fil i minnet.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // Create a new workbook – this is the core of create workbook C#
        var workbook = new Workbook();

        // Grab the first worksheet (index 0) – it's already there by default
        var worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this worksheet with data and styling
        ExportDataTableWithStyling(workbook, worksheet);
    }
}
```

**Varför?**  
`Workbook` innehåller hela Excel‑dokumentet, medan `Worksheet` representerar en enskild flik. Att börja med en ren arbetsbok säkerställer att du kontrollerar varje aspekt av utdata—inga dolda standardstilar som smyger in.

---

## Steg 2: Förbered ett exempel‑DataTable (Export DataTable Excel)

I ett riktigt projekt skulle du hämta data från en databas, men för illustration bygger vi ett litet `DataTable` i farten.

```csharp
private static DataTable GetSampleData()
{
    var dt = new DataTable("Employees");
    dt.Columns.Add("Id", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
    dt.Rows.Add(2, "Bob Smith", "IT", 68000);
    dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
    dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);

    return dt;
}
```

**Varför är detta viktigt:**  
Att exportera ett `DataTable` är det vanligaste sättet att flytta tabulär data från en applikation till Excel. Metoden ovan är helt självständig, så du kan kopiera‑klistra in den i vilket projekt som helst och den kommer att fungera.

---

## Steg 3: Skapa en stil per rad (Excel Export Formatting)

För att ge varje rad sin egen bakgrundsfärg genererar vi ett `Style`‑objekt för varje rad i `DataTable`. Det är här **excel export formatting** glänser.

```csharp
private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
{
    var styles = new Style[rowCount];

    // Define a palette of background colors – feel free to extend
    var colors = new[] { System.Drawing.Color.LightYellow,
                         System.Drawing.Color.LightCyan,
                         System.Drawing.Color.LightGreen,
                         System.Drawing.Color.LightPink };

    for (int i = 0; i < rowCount; i++)
    {
        // Create a fresh style instance
        var style = workbook.CreateStyle();

        // Cycle through our color array so rows get alternating shades
        style.ForegroundColor = colors[i % colors.Length];
        style.Pattern = BackgroundType.Solid;

        // Optional: make the font a little bolder for readability
        style.Font.IsBold = true;

        styles[i] = style;
    }

    return styles;
}
```

**Varför stil per rad?**  
Om du behöver markera specifika poster (t.ex. förfallna fakturor) kan du ersätta den enkla färgcykeln med villkorslogik—sätt bara `style.ForegroundColor` baserat på radens data.

---

## Steg 4: Importera DataTable med radstilar (Set Row Background)

Nu samlar vi allt: data, arbetsboken och stilarna.

```csharp
private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
{
    // 1️⃣ Get the data
    DataTable dt = GetSampleData();

    // 2️⃣ Build a style for each row
    Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

    // 3️⃣ Import the DataTable starting at cell A1.
    //    The `true` flag tells Aspose.Cells to include column headers.
    worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

    // 4️⃣ Save the workbook to disk
    string outputPath = "EmployeesReport.xlsx";
    workbook.Save(outputPath);
    Console.WriteLine($"Workbook saved to {outputPath}");
}
```

**Vad du kommer att se:**  
När du öppnar `EmployeesReport.xlsx` visas en rubrikrad med standardformatering, följt av fyra datarader var och en med en ljus bakgrundsfärg. Resultatet ser ut som en handgjord rapport, inte en tråkig dump.

---

## Steg 5: Avancerade Excel Automation C#‑tips (Excel Automation C#)

Nedan följer några snabba knep du kan lägga ovanpå grundexemplet:

| Tips | Kodsnutt | När att använda |
|-----|--------------|-------------|
| **Auto‑Fit Columns** | `worksheet.AutoFitColumns();` | Efter att ha importerat data för att undvika avklippt text. |
| **Freeze Header Row** | `worksheet.WindowPane.SplitRows = 1;` | När tabellen kan rulla bortom skärmen. |
| **Conditional Formatting** | <details><summary>Visa</summary>```csharp\nvar cf = worksheet.ConditionalFormattings[0];\ncf.AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");\ncf.Style.ForegroundColor = System.Drawing.Color.LightSalmon;\ncf.Style.Pattern = BackgroundType.Solid;\n```</details> | Markera löner över en tröskel. |
| **Protect Sheet** | `worksheet.Protect(ProtectionType.All, "myPassword");` | När du behöver rapporter i skrivskyddat läge. |

Dessa kodsnuttar demonstrerar bredden av **excel automation c#**—du kan fortsätta att utöka arbetsboken utan att skriva om den grundläggande importlogiken.

---

## Vanliga frågor & kantfall

**Vad händer om DataTable har tusentals rader?**  
Aspose.Cells strömmar data effektivt, men du kanske vill inaktivera stilskapande för varje rad för att spara minne. Applicera i stället en enda stil på ett område:

```csharp
var range = worksheet.Cells.CreateRange(1, dt.Rows.Count, 0, dt.Columns.Count);
range.SetStyle(rowStyles[0]); // reuse one style for the whole block
```

**Kan jag exportera till .csv istället för .xlsx?**  
Självklart—byt bara sparformatet:

```csharp
workbook.Save("EmployeesReport.csv", SaveFormat.Csv);
```

Stilinställningarna går förlorade (CSV har ingen styling), men dataexporten förblir densamma.

**Fungerar detta på .NET Core?**  
Ja. Aspose.Cells stödjer .NET Standard 2.0 och senare, så samma kod körs på .NET 6, .NET 7 eller .NET Framework.

---

## Fullt fungerande exempel (Klar‑för‑kopiering)

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // 1️⃣ Create a new workbook – core of create workbook C#
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // 2️⃣ Export DataTable with styling
        ExportDataTableWithStyling(workbook, worksheet);
    }

    private static DataTable GetSampleData()
    {
        var dt = new DataTable("Employees");
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Department", typeof(string));
        dt.Columns.Add("Salary", typeof(decimal));

        dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
        dt.Rows.Add(2, "Bob Smith", "IT", 68000);
        dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
        dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);
        return dt;
    }

    private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
    {
        var styles = new Style[rowCount];
        var colors = new[]
        {
            System.Drawing.Color.LightYellow,
            System.Drawing.Color.LightCyan,
            System.Drawing.Color.LightGreen,
            System.Drawing.Color.LightPink
        };

        for (int i = 0; i < rowCount; i++)
        {
            var style = workbook.CreateStyle();
            style.ForegroundColor = colors[i % colors.Length];
            style.Pattern = BackgroundType.Solid;
            style.Font.IsBold = true;
            styles[i] = style;
        }

        return styles;
    }

    private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
    {
        DataTable dt = GetSampleData();
        Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

        // Import with row styles – sets row background (set row background)
        worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

        // Optional polish
        worksheet.AutoFitColumns();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}