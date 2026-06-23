---
category: general
date: 2026-06-17
description: Ställ in datumformat i Excel med C# och sätt även cellbakgrund, applicera
  förgrundsfärg och färga Excel‑kolumnen vid import. Lär dig steg för steg.
draft: false
keywords:
- set date format
- set cell background
- apply foreground color
- color excel column
- excel import formatting
language: sv
og_description: Ställ in datumformat i Excel med C# samtidigt som du sätter cellbakgrund,
  applicerar förgrundsfärg och färgar Excel‑kolumnen vid import. Fullständig handledning.
og_title: Ställ in datumformat i Excel med C# – Komplett guide
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  headline: Set date format in Excel with C# – Full Import Formatting Guide
  type: TechArticle
- description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  name: Set date format in Excel with C# – Full Import Formatting Guide
  steps:
  - name: 2.1 Set Date Format for the First Column
    text: The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses
      the built‑in number format index 14 for the short date, but you can also supply
      a custom format string if you prefer.
  - name: 2.2 Set Cell Background for the Second Column
    text: Let’s give the `CustomerName` column a light blue background. This is where
      **set cell background** comes into play.
  - name: 2.3 Apply Foreground (Text) Color – Optional Extra
    text: 'If you also want the text itself to be a contrasting color, you can tweak
      the same style:'
  - name: 3.1 Save the Workbook
    text: '```csharp // Save to a file – change path as needed wb.Save("FormattedReport.xlsx",
      SaveFormat.Xlsx); Console.WriteLine("Excel file created with date format and
      colors."); ```'
  - name: What if I have more than two columns?
    text: Just expand the `columnStyles` array and assign a `Style` to each index
      you care about. Unassigned indexes will fall back to the default style, which
      is perfectly fine.
  - name: How do I format a column as currency?
    text: '```csharp columnStyles[3] = wb.CreateStyle(); columnStyles[3].Number =
      164; // Built‑in currency format (e.g., $#,##0.00) ```'
  - name: Can I change the header row style separately?
    text: 'Yes. After the import, you can grab the first row and apply a distinct
      style:'
  - name: What if the DataTable contains null dates?
    text: 'Aspose will leave those cells blank. If you prefer a placeholder like “N/A”,
      you can preprocess the table:'
  type: HowTo
tags:
- excel
- csharp
- aspnet
- data-import
title: Ställ in datumformat i Excel med C# – Fullständig guide för importformatering
url: /sv/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ställ in datumformat i Excel med C# – Fullständig guide för importformatering

Har du någonsin behövt **set date format** i ett Excel‑blad som genererats från C#‑kod, men också vilja att kolumnen ska ha en anpassad bakgrund eller textfärg? Du är inte ensam. I många rapporteringsscenarier hämtar du en `DataTable` från en databas, lägger den i ett kalkylblad och kämpar sedan för att få datumen att se rätt ut och kolumnerna att sticka ut med rätt färger.  

I den här handledningen går vi igenom en ren, end‑to‑end‑lösning som **sets date format**, **sets cell background**, **applies foreground color**, och till och med **colors an Excel column** medan du importerar data. I slutet har du ett återanvändbart mönster som hanterar **excel import formatting** utan den vanliga trial‑and‑error.

> **What you’ll need**  
> * .NET 6+ (or .NET Framework 4.7+)  
> * Aspose.Cells for .NET (free trial works for testing)  
> * A `DataTable` source – any ADO.NET query will do  
> * Visual Studio or your favorite IDE  

Låt oss sätta igång.

---

## Översikt av lösningen

Vi delar upp problemet i tre logiska delar:

1. **Retrieve the source data** – en `DataTable` med rader du vill exportera.  
2. **Create column‑specific styles** – en stil för datumkolumnen, en annan för en textkolumn, plus eventuell extra styling du önskar.  
3. **Import the table with styles** – använd `Worksheet.Cells.ImportDataTable` så varje kolumn ärver den stil du förberett.

Varför detta tillvägagångssätt? Eftersom Aspose.Cells låter dig bifoga en `Style`‑array direkt till `ImportDataTable`‑anropet, vilket betyder att du inte behöver ett andra pass för att återapplicera formatering. Det är snabbare, mindre felbenäget och håller din kod prydlig.

## Steg 1: Hämta data för export

Först och främst – du behöver en `DataTable`. I ett riktigt projekt skulle du förmodligen anropa en lagrad procedur eller använda Entity Framework för att fylla den, men för illustration skapar vi en enkel tabell med en datum‑ och en textkolumn.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("OrderDate", typeof(DateTime));
    table.Columns.Add("CustomerName", typeof(string));

    // Sample rows – replace with your DB call
    table.Rows.Add(DateTime.Today.AddDays(-2), "Acme Corp");
    table.Rows.Add(DateTime.Today.AddDays(-1), "Globex Inc");
    table.Rows.Add(DateTime.Today, "Soylent Co");

    return table;
}
```

> **Pro tip:** Om din källa använder nullable datum, se till att kolumntypen är `typeof(DateTime?)` – Aspose kommer fortfarande att respektera formatet du tilldelar senare.

## Steg 2: Förbered en array av stilar – en per kolumn

Nu skapar vi en `Style[]` vars längd matchar antalet kolumner i `DataTable`. Varje element kommer att innehålla formateringen för respektive kolumn.

```csharp
// Create a new workbook and get the first worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Pull the data
DataTable dataTable = GetData();

// Allocate the style array
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

### 2.1 Ställ in datumformat för den första kolumnen

Den första kolumnen (`OrderDate`) bör visas som “MM/dd/yyyy”. Aspose använder det inbyggda talformatindexet 14 för kort datum, men du kan också ange en anpassad formatsträng om du föredrar.

```csharp
// Style for the date column (index 0)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Built‑in short date format
// Or a custom pattern:
// columnStyles[0].Custom = "mm/dd/yyyy";
```

**Varför detta är viktigt:** Excel lagrar datum som serienummer. Genom att tilldela ett talformat säger du åt Excel att rendera dessa serienummer som mänskligt läsbara datum istället för råa siffror.

### 2.2 Ställ in cellbakgrund för den andra kolumnen

Låt oss ge `CustomerName`‑kolumnen en ljusblå bakgrund. Det är här **set cell background** kommer in i bilden.

```csharp
// Style for the text column (index 1)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightBlue;
columnStyles[1].Pattern = BackgroundType.Solid; // Needed to show the color
```

> **Obs:** Utan att sätta `Pattern` till `Solid` kommer förgrundsfärgen inte att visas eftersom standardmönstret är “None”.

### 2.3 Applicera förgrund (text) färg – valfritt extra

Om du också vill att själva texten ska ha en kontrasterande färg kan du justera samma stil:

```csharp
columnStyles[1].Font.Color = System.Drawing.Color.DarkBlue; // apply foreground color
```

Det uppfyller kravet **apply foreground color** samtidigt som kolumnens bakgrund förblir intakt.

## Steg 3: Importera DataTable med de definierade stilarna

Med stilarna klara är sista steget en enda rad som importerar data och applicerar stilarna kolumn för kolumn.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// includeColumnNames = true to add a header row
ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Hur det fungerar:** Aspose läser `columnStyles`‑arrayen och mappar varje `Style` till motsvarande kolumnindex. Rubrikraden ärver standardstilen om du inte anger en separat stil för rad 0.

### 3.1 Spara arbetsboken

```csharp
// Save to a file – change path as needed
wb.Save("FormattedReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Excel file created with date format and colors.");
```

Kör programmet, öppna *FormattedReport.xlsx*, och du bör se:

- **OrderDate**‑kolumnen visas som datum (t.ex. `06/15/2026`).  
- **CustomerName**‑kolumnen med en ljusblå fyllning och mörkblå text.  

Det är hela **excel import formatting**‑arbetsflödet på under 30 rader C#.

## Steg‑för‑steg‑sammanfattning (med varför)

| Steg | Vad du gör | Varför det är viktigt |
|------|------------|-----------------------|
| **Hämta data** | Call `GetData()` to fill a `DataTable`. | Provides a structured source that Aspose can ingest directly. |
| **Skapa stilarray** | Allocate `Style[]` matching column count. | Allows per‑column styling in a single import call. |
| **Ställ in datumformat** | `columnStyles[0].Number = 14;` | Ensures dates render correctly in Excel. |
| **Ställ in bakgrundsfärg** | `ForegroundColor = LightBlue; Pattern = Solid;` | Highlights the column, satisfying **set cell background**. |
| **Applicera förgrundsfärg** | `Font.Color = DarkBlue;` | Improves readability and meets **apply foreground color**. |
| **Importera med stilar** | `ImportDataTable(..., columnStyles);` | One‑pass import that respects all formatting. |
| **Spara arbetsbok** | `wb.Save(...);` | Persists the result for downstream users. |

## Hantera kantfall & vanliga frågor

### Vad händer om jag har mer än två kolumner?

Utöka helt enkelt `columnStyles`‑arrayen och tilldela en `Style` till varje index du bryr dig om. Omtalade index kommer att falla tillbaka på standardstilen, vilket är helt okej.

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].Number = 0; // General format for numeric columns
```

### Hur formaterar jag en kolumn som valuta?

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 164; // Built‑in currency format (e.g., $#,##0.00)
```

### Kan jag ändra rubrikradens stil separat?

Ja. Efter importen kan du hämta den första raden och applicera en separat stil:

```csharp
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = System.Drawing.Color.Gold;
headerStyle.Pattern = BackgroundType.Solid;

ws.Cells.Rows[0].ApplyStyle(headerStyle, new StyleFlag { All = true });
```

### Vad händer om DataTable innehåller null‑datum?

Aspose lämnar dessa celler tomma. Om du föredrar en platshållare som “N/A” kan du förbehandla tabellen:

```csharp
foreach (DataRow row in dataTable.Rows)
{
    if (row.IsNull("OrderDate"))
        row["OrderDate"] = DateTime.MinValue; // or any sentinel
}
```

Justera sedan stilen för att visa ett anpassat format som visar “N/A” för sentinel‑värdet.

## Fullt fungerande exempel

Nedan är det kompletta, kopiera‑och‑klistra‑klara programmet. Kör det som en konsolapp, så får du en snyggt formaterad Excel‑fil.

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelExportDemo
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook & style array
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 2a️⃣ Date column – set date format
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date (MM/dd/yyyy)

        // 2b️⃣ Text column – set background & foreground colors
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].ForegroundColor = Color.LightBlue;
        columnStyles[1].Pattern = BackgroundType.Solid;
        columnStyles[1].Font.Color = Color.DarkBlue; // apply foreground color

        // 3️⃣ Import with formatting
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Optional: style header row
        Style headerStyle = wb.CreateStyle();
        headerStyle.Font.IsBold = true;
        headerStyle.ForegroundColor = Color.Gold;
        headerStyle.Pattern = BackgroundType.Solid;
        ws.Cells


## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Set Font Color in Excel Cells using Aspose.Cells for .NET](/cells/english/net/formatting/setting-font-color/)
- [Set Font Color in .NET Excel with Aspose.Cells](/cells/english/net/formatting/set-font-color-net-excel-aspose-cells/)
- [Set Excel Column Widths in Pixels Using Aspose.Cells for .NET | Step-by-Step Guide](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}