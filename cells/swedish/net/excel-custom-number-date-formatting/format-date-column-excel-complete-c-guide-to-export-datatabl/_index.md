---
category: general
date: 2026-07-13
description: Formatera datumkolumn i Excel när du exporterar en DataTable från C#.
  Lär dig exportera DataTable till Excel i C# och importera DataTable till Excel med
  formatering på några minuter.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- format date column excel
- excel export datatable c#
- import datatable to excel
language: sv
lastmod: 2026-07-13
og_description: Formatera datumkolumn i Excel enkelt. Den här guiden visar hur du
  exporterar en datatabell till Excel med C# och importerar en datatabell till Excel
  med anpassade stilar.
og_image_alt: Screenshot showing a formatted date column in an Excel sheet generated
  from C#
og_title: Formatera datumkolumn i Excel – Steg‑för‑steg C#‑exporthandledning
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  headline: Format Date Column Excel – Complete C# Guide to Export DataTable
  type: TechArticle
- description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  name: Format Date Column Excel – Complete C# Guide to Export DataTable
  steps:
  - name: What if My DataTable Has More Than Three Columns?
    text: Just extend the `columnStyles` array. For any column you don’t explicitly
      style, leave the entry `null`; Excel will apply the default General format.
  - name: How to Apply a Custom Date Format (e.g., “dd‑MMM‑yyyy”)?
    text: 'Replace the built‑in number with a custom string:'
  - name: Can I Use This Approach with EPPlus or ClosedXML?
    text: 'Yes, the concept is identical: create a style object, assign it to a column,
      then load the `DataTable`. The API differs, but the **excel export datatable
      c#** pattern remains the same.'
  - name: What About Large DataSets (100k+ rows)?
    text: '`ImportDataTable` is optimized for bulk writes, but you might hit memory
      limits. In that case, consider streaming rows with `Cells.ImportDataTable` in
      chunks, or use `Worksheet.Cells["A1"].PutValue` in a loop while reusing the
      style objects.'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Export
title: Formatera datumkolumn i Excel – Komplett C#-guide för att exportera DataTable
url: /sv/net/excel-custom-number-date-formatting/format-date-column-excel-complete-c-guide-to-export-datatabl/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formatera datumkolumn Excel – Komplett C#‑guide för att exportera DataTable

Har du någonsin behövt **format date column Excel** när du hämtar data från en databas, men cellerna fortsatte visa råa tidsstämplar? Du är inte ensam. I många affärsprogram dumpas standardexporten ett `DateTime`‑värde som `2024‑03‑15 00:00:00` och ingen vill ha den röran.  

Den goda nyheten är att du kan styra exakt hur varje kolumn ser ut direkt från C#. I den här handledningen går vi igenom en end‑to‑end‑lösning som **excel export datatable c#**, applicerar ett datumformat på den första kolumnen, ett valutastil på den andra, och slutligen **import datatable to excel** med nollbesvärsstyling.

När du är klar har du en återanvändbar metod som du kan slänga in i vilket .NET‑projekt som helst, oavsett om du använder .NET 6, .NET Framework 4.8 eller en senare version.

---

## Vad du behöver

- **Aspose.Cells for .NET** (eller vilket bibliotek som helst som erbjuder `CreateStyle` och `ImportDataTable`). Kodsnuttarna använder Aspose eftersom dess API är rent och allmänt använt.
- En **DataTable** som du redan fyller på från SQL, CSV eller någon annan källa.
- Visual Studio (eller din föredragna IDE).  
- .NET‑runtime 5.0+ (exemplet riktar sig mot .NET 6, men äldre ramverk fungerar på samma sätt).

Om du ännu inte har Aspose.Cells, skaffa en gratis provversion från den officiella webbplatsen—ingen kreditkort krävs.

---

## Steg 1: Hämta källdata som en DataTable

Först och främst behöver du en `DataTable`. I verkliga scenarier kommer den vanligtvis från `SqlDataAdapter.Fill`, men för tydlighetens skull kommer vi att mocka en enkel tabell:

```csharp
using System;
using System.Data;

DataTable GetSampleData()
{
    var dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("TotalAmount", typeof(decimal));
    dt.Columns.Add("Customer", typeof(string));

    dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
    dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
    dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");

    return dt;
}
```

> **Proffstips:** När du hämtar data direkt från en lagrad procedur, se till att kolumntyperna matchar de avsedda Excel‑formaten. En `datetime`‑kolumn kommer senare att vara målet för vårt **format date column excel**‑format.

---

## Steg 2: Skapa en Excel‑arbetsbok och definiera kolumnstilar

Nu skapar vi en ny arbetsbok. Knepet för **format date column excel** ligger i att skapa ett `Style`‑objekt, sätta dess `Number`‑egenskap till det inbyggda Excel‑datumformatet (kod 14), och tilldela den stilen till rätt kolumnindex.

```csharp
using Aspose.Cells;

Workbook wb = new Workbook();               // creates a blank workbook
Worksheet sheet = wb.Worksheets[0];        // we’ll work with the first sheet

// Prepare a style array – one entry per DataTable column
Style[] columnStyles = new Style[dt.Columns.Count];

// Column 0 – format as a short date (e.g., 03/15/2024)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Excel built‑in date format

// Column 1 – format as currency (e.g., $1,245.67)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].Number = 2;                // Built‑in currency format

// Column 2 – no special formatting; leave null or default
columnStyles[2] = null;
```

Varför `Number = 14`? Excel lagrar datum som serienummer; format 14 instruerar programmet att rendera dessa siffror med lokala korta datumformatet. Om du behöver ett eget mönster (t.ex. `dd‑MMM‑yyyy`), kan du istället sätta `columnStyles[0].Custom = "dd-MMM-yyyy"`.

---

## Steg 3: Importera DataTable till kalkylbladet med stilar

Med stil‑arrayen klar är import‑anropet en enda rad. Detta är kärnan i **excel export datatable c#** och också platsen där vi **import datatable to excel** samtidigt som vi bevarar vår formatering.

```csharp
// Import the DataTable, include column headers, start at cell A1 (row 0, column 0)
sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
```

`ImportDataTable`‑överladdningen vi använder accepterar stil‑arrayen och applicerar varje stil på motsvarande kolumn när data skrivs. Ingen efterbearbetningsloop behövs—din datumkolumn är redan snyggt formaterad.

---

## Steg 4: Spara arbetsboken (eller strömma den direkt till webbläsaren)

Beroende på ditt scenario kan du spara till disk, ett minnesström, eller returnera filen som ett HTTP‑svar. Här är tre vanliga mönster:

```csharp
// 1️⃣ Save to a physical file
wb.Save("ExportedReport.xlsx");

// 2️⃣ Save to a MemoryStream (useful for ASP.NET Core)
using var ms = new MemoryStream();
wb.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // rewind for downstream consumers

// 3️⃣ Return as a file download in ASP.NET MVC
public IActionResult DownloadReport()
{
    var dt = GetSampleData();
    var wb = BuildWorkbook(dt); // encapsulate steps 2‑3 in a method
    using var ms = new MemoryStream();
    wb.Save(ms, SaveFormat.Xlsx);
    return File(ms.ToArray(), 
                "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
                "Report.xlsx");
}
```

> **Se upp för:** Om du använder `FileResult` i ASP.NET Core, se till att sätta `Response.Headers["Cache-Control"] = "no-cache"` när filen genereras i farten. Det förhindrar att webbläsaren levererar en föråldrad version.

---

## Steg 5: Verifiera resultatet – Så ser Excel‑arket ut

Efter att ha kört koden, öppna `ExportedReport.xlsx`. Du bör se:

| OrderDate (formaterad) | TotalAmount (valuta) | Customer |
|-----------------------|------------------------|----------|
| 03/13/2024            | $1,245.67              | Acme Corp|
| 03/14/2024            | $980.00                | Beta Ltd |
| 03/15/2024            | $1,500.25              | Gamma Inc|

Observera hur **format date column excel** visar ett rent kort datum, medan valutakolumnen automatiskt anpassas efter dina regionala inställningar. Ingen manuell cell‑för‑cell‑formatering behövs.

![format date column excel exempel](/images/format-date-column-excel.png)

*Bildtext: format date column excel – en skärmdump av Excel‑arket med en korrekt formaterad datumkolumn.*

---

## Vanliga frågor & kantfall

### Vad händer om min DataTable har fler än tre kolumner?

Bara utöka `columnStyles`‑arrayen. För varje kolumn du inte explicit formaterar, lämna posten `null`; Excel kommer då att använda standardformatet General.

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 10; // Percent format, for example
```

### Hur applicerar man ett eget datumformat (t.ex. “dd‑MMM‑yyyy”)?

Byt ut det inbyggda numret mot en egen sträng:

```csharp
columnStyles[0].Custom = "dd-MMM-yyyy";
```

### Kan jag använda detta tillvägagångssätt med EPPlus eller ClosedXML?

Ja, konceptet är identiskt: skapa ett stil‑objekt, tilldela det till en kolumn, och ladda sedan `DataTable`. API‑et skiljer sig, men mönstret **excel export datatable c#** förblir detsamma.

### Vad gäller stora dataset (100 k+ rader)?

`ImportDataTable` är optimerad för massinmatning, men du kan stöta på minnesgränser. I så fall, överväg att strömma rader med `Cells.ImportDataTable` i delar, eller använd `Worksheet.Cells["A1"].PutValue` i en loop medan du återanvänder stil‑objekten.

---

## Fullständigt fungerande exempel (alla steg i en metod)

Nedan är en självständig metod som du kan kopiera‑klistra in i vilken konsolapp eller ASP.NET‑controller som helst. Den demonstrerar hela flödet—från datainhämtning till stylad Excel‑export.

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;

public class ExcelExporter
{
    // Entry point for demonstration
    public static void Main()
    {
        DataTable dt = GetSampleData();
        Workbook wb = BuildWorkbook(dt);
        wb.Save("StyledExport.xlsx");
        Console.WriteLine("Excel file created – check StyledExport.xlsx");
    }

    // Generates the sample DataTable (Step 1)
    private static DataTable GetSampleData()
    {
        var dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("TotalAmount", typeof(decimal));
        dt.Columns.Add("Customer", typeof(string));

        dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
        dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
        dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");
        return dt;
    }

    // Builds the workbook with styled columns (Steps 2‑3)
    private static Workbook BuildWorkbook(DataTable dt)
    {
        var wb = new Workbook();
        var sheet = wb.Worksheets[0];

        // Allocate style array
        Style[] columnStyles = new Style[dt.Columns.Count];

        // Format column 0 as short date
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date

        // Format column 1 as currency
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].Number = 2; // currency

        // No style for column 2 (Customer name)
        columnStyles[2] = null;

        // Import with headers, start at A1
        sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
        return wb;
    }
}
```

Kör programmet, öppna `StyledExport.xlsx`, och du kommer att se **format date column excel** tillämpat perfekt.

---

## Sammanfattning & nästa steg

Vi har just gått igenom hur man **format date column excel** när man utför en **excel export datatable c#**, och hur man **import datatable to excel** med kolumn‑specifik styling i ett enda anrop. De viktigaste slutsatserna:

1. Skapa ett `Style` för varje kolumn du vill formatera.  
2. Använd `Number = 14` för datum, `Number = 2` för valuta, eller vilket eget format du behöver.  
3. Skicka stil‑arrayen till `ImportDataTable`—biblioteket gör det tunga arbetet.

Vad kan du utforska härnäst?

- **Conditional formatting** för att markera försenade datum.  
- **

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man importerar DataTable till Excel med Aspose.Cells för .NET (Steg‑för‑steg‑guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Exportera Excel‑data till DataTable med Aspose.Cells för .NET&#58; En komplett guide](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [Exportera HTML‑strängar från Excel till DataTable med Aspose.Cells för .NET&#58; En steg‑för‑steg‑guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}