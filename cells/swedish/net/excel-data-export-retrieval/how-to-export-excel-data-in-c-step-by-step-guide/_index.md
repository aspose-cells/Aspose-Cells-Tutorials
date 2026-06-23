---
category: general
date: 2026-03-21
description: Hur man exporterar Excel-data med kolumnnamn, bevarar talformat och läser
  specifika rader med Aspose.Cells i C#. Lär dig att läsa Excel-ark och exportera
  specifika rader effektivt.
draft: false
keywords:
- how to export excel
- preserve number format
- export with column names
- read excel worksheet
- export specific rows
language: sv
og_description: Hur man exporterar Excel-data med kolumnnamn, bevarar talformat och
  läser specifika rader med Aspose.Cells. Ett komplett, körbart exempel för C#‑utvecklare.
og_title: Hur man exporterar Excel-data i C# – Komplett programmeringsguide
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Hur man exporterar Excel‑data i C# – Steg‑för‑steg‑guide
url: /sv/net/excel-data-export-retrieval/how-to-export-excel-data-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man exporterar Excel-data i C# – Komplett programmeringsguide

Har du någonsin funderat **hur man exporterar excel** data utan att förlora den ursprungliga formateringen? Kanske har du provat en snabb kopiera‑klistra och slutade med datum som ser ut som “44728” eller saknade kolumnrubriker. Det är frustrerande, eller hur? I den här handledningen får du se ett rent, end‑to‑end‑sätt att läsa ett Excel‑arbetsblad, bevara talformat, exportera med kolumnnamn och till och med välja bara de rader du behöver.

Vi kommer att använda Aspose.Cells‑biblioteket eftersom det ger dig fin‑granulär kontroll över exportalternativ. I slutet av den här guiden har du ett återanvändbart kodsnutt som kan läggas in i vilket .NET‑projekt som helst, och du kommer att förstå varför varje alternativ är viktigt. Inga externa dokument behövs – allt du behöver finns här.

---

## Vad du kommer att lära dig

- **Read Excel worksheet** till minnet med Aspose.Cells.
- **Export specific rows** (t.ex. rader 0‑49) medan kolumnnamnen behålls.
- **Preserve number format** så att valuta, datum och procenttal förblir intakta.
- Hur man **export with column names** och inkluderar cellkommentarer om du behöver dem.
- Ett komplett, färdigt‑att‑köra C#‑exempel plus tips för vanliga fallgropar.

### Förutsättningar

- .NET 6.0 eller senare (koden fungerar även med .NET Framework 4.6+).
- Aspose.Cells för .NET installerat via NuGet (`Install-Package Aspose.Cells`).
- En Excel‑fil (`input.xlsx`) placerad i en mapp du kan referera till.

> **Pro tip:** Om du kör i en CI‑pipeline, överväg att hämta NuGet‑paketet från ett privat flöde för att undvika licensöverraskningar.

## Steg 1 – Installera Aspose.Cells och lägg till namnrymder

Först, se till att Aspose.Cells‑paketet finns i ditt projekt. Öppna Package Manager Console och kör:

```powershell
Install-Package Aspose.Cells
```

Lägg sedan till de nödvändiga `using`‑direktiven högst upp i din C#‑fil:

```csharp
using Aspose.Cells;
using System.Data;
using System;
```

Dessa importeringar ger dig åtkomst till `Workbook`, `Worksheet`, `ExportTableOptions` och `DataTable` – de centrala delarna för **reading an Excel worksheet** och export av data.

## Steg 2 – Ladda arbetsboken (Läs Excel‑filen)

Nu läser vi faktiskt **read the Excel worksheet**. `Workbook`‑konstruktorn tar en sökväg till filen, och Aspose.Cells hanterar både `.xlsx`‑ och äldre `.xls`‑format.

```csharp
// Step 2: Load the workbook containing the data
string filePath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(filePath);
```

> **Why this matters:** Att ladda arbetsboken en gång och återanvända samma `Worksheet`‑objekt är mycket mer effektivt än att öppna filen upprepade gånger, särskilt för stora kalkylblad.

## Steg 3 – Konfigurera exportalternativ (Bevara talformat & kolumnnamn)

Här är vi där vi talar om för Aspose.Cells *hur* man ska exportera. `ExportTableOptions`‑klassen låter oss finjustera utskriften. Vi kommer att aktivera tre flaggor:

1. `ExportAsString = true` – tvingar varje cell att bli en sträng, vilket garanterar att siffror behåller sin visuella representation.
2. `IncludeCellComments = true` – kopierar eventuella kommentarer som är bifogade celler (praktiskt för dokumentation).
3. `PreserveNumberFormat = true` – behåller det ursprungliga talformatet (valutasymboler, datumformat osv.).

```csharp
// Step 3: Configure export options to control how the table is exported
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export all values as strings
    IncludeCellComments = true,     // Preserve any cell comments
    PreserveNumberFormat = true     // Keep the original number formatting
};
```

> **Edge case:** Om du sätter `ExportAsString` till `false` men fortfarande vill behålla talformat, kan du sluta med råa numeriska värden (t.ex. 44728 för ett datum). Att ha båda flaggorna på undviker den överraskningen.

## Steg 4 – Hämta det första arbetsbladet (Read Excel Worksheet)

De flesta enkla filer har den data du behöver på det första bladet, så vi hämtar det via index. Om du behöver ett annat blad, ersätt bara `0` med rätt noll‑baserade index eller använd `workbook.Worksheets["SheetName"]`.

```csharp
// Step 4: Get the first worksheet from the workbook
Worksheet firstWorksheet = workbook.Worksheets[0];
```

> **Why it’s useful:** Att direkt komma åt arbetsbladsobjektet ger dig full kontroll över dess `Cells`‑samling, vilket är avgörande för **export specific rows** senare.

## Steg 5 – Exportera ett cellområde (Export Specific Rows)

Nu är vi i hjärtat av handledningen: exportera rader 0‑49 och kolumner 0‑4 (dvs. de första 50 raderna och de fem första kolumnerna) till en `DataTable`. Vi kommer också be Aspose.Cells att inkludera kolumnnamn som den första raden i `DataTable`.

```csharp
// Step 5: Export a range of cells (rows 0‑49, columns 0‑4) to a DataTable using the options
DataTable exportedTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 50,
    totalColumns: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

### Vad detta gör

- **`startRow: 0`** – börjar högst upp på bladet.
- **`totalRows: 50`** – hämtar de första 50 raderna (dvs. **export specific rows**).
- **`totalColumns: 5`** – begränsar exporten till de fem första kolumnerna.
- **`includeColumnNames: true`** – säkerställer att `DataTable`‑kolumnrubrikerna matchar Excel‑rubrikraden, vilket uppfyller kravet **export with column names**.
- **`exportOptions`** – tillämpar inställningarna från Steg 3, så att dina numeriska värden ser ut som “$1,234.56” istället för “1234.56”.

## Steg 6 – Verifiera exporten (Hur resultatet ser ut)

Låt oss skriva ut de första raderna till konsolen så att du kan se att formateringen överlevde.

```csharp
// Step 6: Display a few rows to verify the export
Console.WriteLine("=== Exported DataTable Preview ===");
foreach (DataRow row in exportedTable.Rows)
{
    // Join each column with a tab for readability
    Console.WriteLine(string.Join("\t", row.ItemArray));
}
```

**Förväntad utskrift (exempel):**

```
=== Exported DataTable Preview ===
Date        Description    Amount   Tax   Total
01/02/2024  Widget A       $120.00  $12  $132.00
01/03/2024  Widget B       $200.00  $20  $220.00
...
```

Observera hur datumen visas i formatet `MM/dd/yyyy` och valutan behåller `$`‑symbolen – tack vare **preserve number format**.

## Vanliga fallgropar & hur man undviker dem

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| Dates turn into large numbers | `ExportAsString` left `false` | Keep `ExportAsString = true` or convert cells manually |
| Missing column headers | `includeColumnNames` set to `false` | Set it to `true` when you need **export with column names** |
| Comments disappear | `IncludeCellComments` not enabled | Turn on `IncludeCellComments` in `ExportTableOptions` |
| Exporting the wrong sheet | Using `Worksheets[0]` on a multi‑sheet file | Specify the sheet name: `workbook.Worksheets["Data"]` |
| Out‑of‑range exception | `totalRows` exceeds actual rows | Use `Math.Min(totalRows, worksheet.Cells.MaxDataRow + 1)` |

## Bonus: Exportera hela bladet samtidigt som formaten bevaras

Om du senare bestämmer dig för att du behöver hela bladet, byt bara ut `totalRows` och `totalColumns` mot bladets maximala dimensioner:

```csharp
int maxRows = firstWorksheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int maxCols = firstWorksheet.Cells.MaxDataColumn + 1;

DataTable fullTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: maxRows,
    totalColumns: maxCols,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

Nu har du en **read excel worksheet**‑rutin som fungerar för alla storlekar, samtidigt som du **preserving number format** och **exporting with column names**.

## Fullt fungerande exempel (Klar att kopiera‑klistra)

Nedan är det kompletta programmet som du kan släppa in i en konsolapp. Det innehåller alla stegen, importerna och en enkel verifieringsutskrift.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);

            // 2️⃣ Set export options (preserve number format, include comments, export as strings)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                IncludeCellComments = true,
                PreserveNumberFormat = true
            };

            // 3️⃣ Grab the first worksheet (read excel worksheet)
            Worksheet sheet = workbook.Worksheets[0];

            // 4️⃣ Export rows 0‑49, columns 0‑4 (export specific rows) with column headers
            DataTable table = sheet.Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: 50,
                totalColumns: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // 5️⃣ Show a preview
            Console.WriteLine("=== Exported DataTable Preview ===");
            foreach (DataRow row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.ItemArray));
            }

            // Keep console open
            Console.WriteLine("\nExport complete. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

Spara detta som `Program.cs`, kör `dotnet run`, och du bör se den formaterade förhandsvisningen i din terminal.

## Slutsats

Vi har precis gått igenom **how to export excel** data med Aspose.Cells, och täckt allt från att ladda arbetsboken till att bevara talformat, exportera med kolumnnamn och begränsa exporten till specifika rader. Koden är självständig, fullt körbar och innehåller praktiska skydd för de vanligaste kantfallen.

Redo för nästa utmaning? Försök att exportera direkt till en CSV samtidigt som du behåller den ursprungliga talformateringen, eller skjut `DataTable` in i en Entity Framework Core‑kontext för massinmatning i databasen. Båda scenarierna bygger på samma grunder som vi täckte här.

Om du fann den här guiden hjälpsam

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}