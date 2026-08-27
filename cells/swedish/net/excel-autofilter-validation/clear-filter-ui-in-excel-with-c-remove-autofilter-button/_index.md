---
category: general
date: 2026-02-09
description: Rensa filter‑gränssnittet i Excel med C# genom att ta bort AutoFilter‑knappen.
  Lär dig hur du döljer filterknappen, visar rubrikraden och håller dina blad prydliga.
draft: false
keywords:
- clear filter UI
- remove autofilter excel
- how to remove autofilter
- show header row
- hide filter button
language: sv
og_description: Rensa filter‑gränssnittet i Excel med C#. Denna guide visar hur du
  döljer filterknappen, visar rubrikraden och håller kalkylbladen rena.
og_title: Rensa filter‑gränssnitt i Excel med C# – Ta bort AutoFilter‑knappen
tags:
- excel
- csharp
- epplus
- automation
title: Rensa filter‑UI i Excel med C# – Ta bort AutoFilter‑knappen
url: /sv/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rensa filter‑UI i Excel med C# – Ta bort AutoFilter‑knappen

Har du någonsin behövt **rensa filter‑UI** i ett Excel‑ark men varit osäker på vilken kodrad som faktiskt döljer den lilla rullgardins‑pilen? Du är inte ensam. Filterknappen kan vara en ögonirritation när du levererar en rapport till slutanvändare som aldrig behöver ändra vyn.  

I den här handledningen går vi igenom ett komplett, körbart exempel som **tar bort AutoFilter‑knappen** från en tabell, ser till att rubrikraden förblir synlig och berör även hur man *döljer filterknappen* permanent. När du är klar vet du exakt **hur du tar bort AutoFilter** i C# och varför varje steg är viktigt.

## Vad du behöver

- .NET 6+ (eller .NET Framework 4.7.2+) – någon modern runtime fungerar.
- **EPPlus**‑paketet från NuGet (version 6.x eller senare) – det ger oss `ExcelWorksheet`, `ExcelTable` osv.
- En enkel Excel‑fil med en tabell som heter **SalesTable** (skapa gärna en på några klick).

Det är allt. Ingen COM‑interop, inga extra DLL‑filer, bara ett fåtal `using`‑satser och några rader kod.

## Rensa filter‑UI: Ta bort AutoFilter‑knappen

Kärnan i lösningen består av tre små satser. Låt oss gå igenom dem så att du förstår *varför* de behövs, inte bara *vad* de gör.

### Steg 1 – Hämta en referens till tabellen

```csharp
// Step 1: Get a reference to the "SalesTable" in the first worksheet
ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
```

Varför detta är viktigt: EPPlus arbetar med **tabeller** (`ExcelTable`), inte rena områden. Genom att hämta tabell‑objektet får vi åtkomst till egenskapen `AutoFilter`, som styr UI‑elementet du ser i bladet. Om du försöker manipulera arbetsbladet direkt påverkar du bara värden, inte filterknappen.

### Steg 2 – Ta bort raden med AutoFilter‑knappen

```csharp
// Step 2: Remove the AutoFilter button row (clears any applied filter UI)
salesTable.AutoFilter = null;
```

Genom att sätta `AutoFilter` till `null` säger du åt EPPlus att ta bort den underliggande filter‑raden. Detta är *rensa filter‑UI*-operationen som de flesta utvecklare letar efter när de frågar “**hur tar man bort autofilter**”. Det är ett rent en‑rad‑tillvägagångssätt som fungerar i alla Excel‑versioner som EPPlus stödjer.

### Steg 3 – Behåll rubrikraden synlig

```csharp
// Step 3: Ensure the header row remains visible after removing the filter
salesTable.ShowHeader = true;
```

När du tar bort filter‑UI kan Excel ibland dölja rubrikraden om tabellens `ShowHeader`‑flagga är falsk. Genom att explicit sätta den till `true` garanterar vi att kolumnrubrikerna förblir på skärmen – en subtil men viktig detalj för en polerad slutrapport.

### Fullt, körbart exempel

Nedan finns ett minimalt konsolprogram som öppnar en befintlig arbetsbok, utför de tre stegen och sparar resultatet. Kopiera‑klistra in, tryck **F5**, och se filterknappen försvinna.

```csharp
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

class Program
{
    static void Main()
    {
        // EPPlus requires a license context for non‑commercial use.
        ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

        // 1️⃣ Load the workbook (replace with your own path)
        var filePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        using var package = new ExcelPackage(new FileInfo(filePath));

        // 2️⃣ Get a reference to the table named "SalesTable"
        ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
        if (salesTable == null)
        {
            Console.WriteLine("Table 'SalesTable' not found in the first worksheet.");
            return;
        }

        // 3️⃣ Remove the AutoFilter button (clear filter UI)
        salesTable.AutoFilter = null;

        // 4️⃣ Ensure the header row stays visible (show header row)
        salesTable.ShowHeader = true;

        // 5️⃣ Save the changes to a new file so you don’t overwrite the original
        var outputPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
        package.SaveAs(new FileInfo(outputPath));

        Console.WriteLine($"Filter button removed. Saved to {outputPath}");
    }
}
```

**Förväntat resultat:** Öppna *SalesReport_NoFilter.xlsx* – filterpilarna är borta, men kolumnrubrikerna finns kvar. Ingen mer “klick‑för‑filter”-UI‑klotter.

> **Proffstips:** Om du har **flera tabeller** och vill dölja filterknappen för alla, loopa igenom `worksheet.Tables` och applicera samma tre rader inuti loopen.

## Hur man tar bort AutoFilter i Excel med C# – en djupare genomgång

Du kanske undrar: “Vad händer om arbetsboken redan har ett filter aktivt? Rensar `AutoFilter = null` också de filtrerade raderna?” Svaret är **ja**. EPPlus rensar både UI‑elementet och de underliggande filterkriterierna, så att datan återgår till sin ursprungliga ordning.  

Om du bara vill *dölja* knappen men behålla filtret aktivt kan du istället sätta egenskapen `AutoFilter` till ett **nytt tomt filter**:

```csharp
salesTable.AutoFilter = new ExcelAutoFilter(); // hides button, retains filter logic
```

Den varianten är praktisk när du vill *dölja filterknappen* för ett snyggt utseende men ändå låta avancerade användare växla filter via VBA eller menyfliksområdet.

### Edge case: Tabeller utan rubrikrad

Vissa äldre rapporter använder rena områden istället för tabeller. I det fallet exponerar inte EPPlus ett `ExcelTable`‑objekt, så koden ovan skulle kasta ett fel. Lösningen är att först **konvertera området till en tabell**:

```csharp
var range = worksheet.Cells["A1:D100"];
var table = worksheet.Tables.Add(range, "TempTable");
table.ShowHeader = true;    // ensure header is visible
table.AutoFilter = null;    // clear filter UI
```

Nu har du *removed autofilter excel*-stil UI även på ett område som ursprungligen saknade en formell tabell.

## Visa rubrikrad efter att ha dolt filterknappen – varför det är viktigt

Ett vanligt klagomål är att efter att du döljer filter‑UI kan rubrikraden ibland försvinna, särskilt när arbetsboken ursprungligen skapades med “Hide Header” aktiverat. Genom att explicit sätta `salesTable.ShowHeader = true;` undviker vi den överraskningen.  

Om du någonsin behöver **dölja filterknappen** men behålla rubriken dold (kanske du genererar en rå data‑dump), sätt helt enkelt `salesTable.ShowHeader = false;` efter att ha rensat filtret. Koden är symmetrisk, vilket gör det enkelt att växla baserat på en konfigurationsflagga.

## Dölja filterknappen – praktiska tips och fallgropar

- **Versionkompatibilitet:** EPPlus 6+ fungerar endast med `.xlsx`‑filer. Om du arbetar med det äldre `.xls`‑formatet behöver du ett annat bibliotek (t.ex. NPOI) eftersom *clear filter UI*-API:et inte finns där.
- **Prestanda:** Att ladda en enorm arbetsbok bara för att dölja en knapp kan vara långsamt. Överväg att använda `ExcelPackage.Load(stream, true)` för att öppna i **read‑only**‑läge, göra ändringen och sedan spara.
- **Testning:** Validera alltid den resulterande filen manuellt första gången. Automatiserade UI‑tester kan verifiera att filterpilarna verkligen är borta (`worksheet.Tables[0].AutoFilter == null`).
- **Licensiering:** EPPlus gick över till en dubbellicens i version 5. För kommersiella projekt behöver du en betald licens eller byta till ett alternativt bibliotek.

## Fullständig källfil för kopiera‑och‑klistra

Nedan är den exakta filen du kan släppa in i ett nytt konsolprojekt. Inga dolda beroenden, allt är självständigt.

```csharp
// File: Program.cs
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

namespace ExcelFilterCleaner
{
    class Program
    {
        static void Main()
        {
            // License context – required for EPPlus 5+
            ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

            // Path to the original workbook (adjust as needed)
            string sourcePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
            if (!File.Exists(sourcePath))
            {
                Console.WriteLine($"Source file not found: {sourcePath}");
                return;
            }

            // Load workbook
            using var package = new ExcelPackage(new FileInfo(sourcePath));

            // Assume the first worksheet contains the table
            var worksheet = package.Workbook.Worksheets[0];
            const string tableName = "SalesTable";

            // Grab the table; abort if missing
            var salesTable = worksheet.Tables[tableName];
            if (salesTable == null)
            {
                Console.WriteLine($"Table '{tableName}' not found.");
                return;
            }

            // ---- Clear filter UI ----
            salesTable.AutoFilter = null;   // removes the filter button row
            salesTable.ShowHeader = true;   // guarantees the header row stays visible

            // Save to a new file so the original stays untouched
            string destPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
            package.SaveAs(new FileInfo(destPath));

            Console.WriteLine($"Successfully cleared filter UI. Output: {destPath}");
        }
    }
}
```

Kör `dotnet add package EPPlus --version 6.0.8` (eller den senaste) innan du bygger, så har du ett rent blad redo för distribution.

## Slutsats

Vi har just visat dig **hur du tar bort AutoFilter** och **rensar filter‑UI** i en Excel‑arbetsbok med C#. Den tre‑radiga kärnan (`AutoFilter = null;`, `ShowHeader = true;`) gör det tunga arbetet, medan den omgivande boilerplate‑koden gör lösningen

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}