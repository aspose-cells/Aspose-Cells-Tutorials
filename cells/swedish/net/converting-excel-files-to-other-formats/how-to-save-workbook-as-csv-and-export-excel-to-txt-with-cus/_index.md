---
category: general
date: 2026-09-15
description: Lär dig hur du sparar arbetsboken som CSV, exporterar Excel till TXT
  och tillämpar anpassat talformat samtidigt som du konverterar cellvärden till versaler
  i C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as csv
- apply custom number format
- export excel to txt
- uppercase cell values
- export worksheet as text
language: sv
lastmod: 2026-09-15
og_description: Spara arbetsbok som CSV, exportera Excel till TXT och tillämpa anpassat
  talformat samtidigt som du konverterar cellvärden till versaler med Aspose.Cells
  i C#.
og_image_alt: Screenshot showing workbook saved as CSV using C# code
og_title: Spara arbetsbok som CSV och exportera Excel till TXT med anpassad formatering
  i C#
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to save workbook as CSV, export Excel to TXT, and apply custom
    number format while converting cell values to uppercase in C#.
  headline: How to save workbook as CSV and export Excel to TXT with custom formatting
    in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hur man sparar arbetsbok som CSV och exporterar Excel till TXT med anpassad
  formatering i C#
url: /sv/net/converting-excel-files-to-other-formats/how-to-save-workbook-as-csv-and-export-excel-to-txt-with-cus/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man sparar arbetsbok som CSV och exporterar Excel till TXT med anpassad formatering i C#

Om du behöver **spara arbetsbok som CSV** samtidigt som du exporterar ett kalkylblad som ren text och använder ett eget talformat, visar den här guiden en komplett, färdigkörbar lösning. Du får se hur du behåller numerisk precision, konverterar varje cellvärde till versaler och hanterar datum i japansk era – allt med Aspose.Cells för .NET.

Att exportera data från Excel innebär ofta att man jonglerar flera format: CSV för datautbyte, TXT för äldre system och anpassade talformat för lokalspecifik rapportering. Denna handledning går igenom varje krav steg för steg, så att du kan kopiera koden direkt in i ditt projekt.

I avsnitten nedan lär du dig hur du:

* **sparar arbetsbok som csv** med ett definierat antal signifikanta siffror  
* **exporterar excel till txt** samtidigt som du tvingar **versala cellvärden**  
* **tillämpar anpassat talformat** för datum i japansk era och läser det formaterade resultatet  

Inga externa verktyg krävs – bara Aspose.Cells‑biblioteket och en .NET‑utvecklingsmiljö.

## Förutsättningar

* .NET 6.0 eller senare (koden fungerar också med .NET Framework 4.8)  
* Aspose.Cells för .NET (NuGet‑paket `Aspose.Cells`)  
* Grundläggande kunskap om C# och Excel‑koncept  

---

## Steg 1: Spara arbetsboken som CSV med kontrollerad precision

När du **sparar arbetsbok som CSV** skrivs numeriska värden med standard‑strängrepresentation, vilket kan förlora precision. Genom att konfigurera `CsvSaveOptions.SignificantDigits` talar du om för Aspose.Cells hur många signifikanta siffror som ska behållas.

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (or load an existing one)
Workbook workbook = new Workbook();               // you can also use new Workbook("input.xlsx");

// Configure CSV options to keep up to 4 significant digits
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    SignificantDigits = 4   // ensures numbers like 123.4567 stay precise
};

// Save the workbook as CSV
string csvPath = @"C:\Temp\Digits.csv";
workbook.Save(csvPath, csvOptions);

Console.WriteLine($"Workbook saved as CSV to {csvPath}");
```

**Varför detta är viktigt:**  
Att sätta `SignificantDigits` förhindrar avrundningsfel som ofta uppstår när stora datamängder utbyts med efterföljande system (t.ex. datalager). Objektet `CsvSaveOptions` låter dig också styra avgränsare, kodning och andra CSV‑specifika inställningar om så behövs.

---

## Steg 2: Exportera ett kalkylblad som ren text samtidigt som du konverterar värden till versaler

Att exportera ett blad till en enkel `.txt`‑fil är användbart för äldre importrutiner som förväntar sig mellanslagsseparerade data. Genom att aktivera `ExportTableOptions.ExportAsString` och tillhandahålla en `CustomExport`‑delegat kan du **exportera excel till txt** och samtidigt verkställa **versala cellvärden**.

```csharp
// Prepare export options for plain‑text output
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true, // forces every cell to be treated as a string
    // CustomExport receives the cell and its current string value,
    // allowing you to modify it before it is written.
    CustomExport = (cell, value) =>
    {
        // Convert the cell value to an upper‑case string
        return value?.ToString().ToUpperInvariant();
    }
};

// Define the output path for the text file
string txtPath = @"C:\Temp\Table.txt";

// Export the first worksheet (index 0) as a tab‑delimited text file
workbook.Worksheets[0].ExportTable(txtPath, tableOptions);

Console.WriteLine($"Worksheet exported as text to {txtPath}");
```

**Varför detta är viktigt:**  
Många integrationspunkter (t.ex. mainframe‑batchjobb) förväntar sig versala identifierare. `CustomExport`‑callbacken ger dig full kontroll över varje cells representation, så att du kan injicera transformationer som trimning, utfyllnad eller lokalspecifik formatering utan efterbearbetning av filen.

---

## Steg 3: Tillämpa ett anpassat talformat och läsa det formaterade resultatet

Excels inbyggda talformat täcker de flesta fall, men ibland måste du visa datum i ett specifikt kalendersystem – exempelvis den japanska eran. Koden nedan demonstrerar hur du **tillämpa anpassat talformat** på en cell och sedan läsa den formaterade strängen som respekterar arbetsbokens språk.

```csharp
// Create a new workbook for the era example
Workbook eraWorkbook = new Workbook();

// Access the first worksheet and target cell A1
Worksheet sheet = eraWorkbook.Worksheets[0];
Cell dateCell = sheet.Cells["A1"];

// Insert a Japanese‑era date string (Reiwa 3 = 2021)
dateCell.PutValue("Reiwa 3/04/01");

// Apply a built‑in date number format (14 = mm-dd-yy)
// You could also assign a custom format string, e.g., "[$-ja-JP]ggge年m月d日"
Style style = eraWorkbook.CreateStyle();
style.Number = 14; // standard short date format
dateCell.SetStyle(style);

// Force formula calculation (necessary if the cell contains a formula)
eraWorkbook.CalculateFormula();

// Retrieve the formatted string as it would appear in Excel
string formattedDate = dateCell.StringValue;
Console.WriteLine($"Formatted date (locale aware): {formattedDate}");
```

**Varför detta är viktigt:**  
Genom att använda `SetStyle` med ett talformat säkerställer du att cellens visning följer regionala inställningar, vilket är kritiskt för rapporter som distribueras över olika språk. När du senare läser `StringValue` får du exakt den sträng som en användare skulle se i Excel‑gränssnittet, vilket eliminerar behovet av manuell parsning.

---

## Fullt, körbart exempel

Nedan finns ett enda program som kombinerar de tre stegen. Klistra in det i ett nytt Console‑App‑projekt, lägg till Aspose.Cells‑NuGet‑paketet och kör.

```csharp
using Aspose.Cells;
using System;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Save workbook as CSV ----------
            Workbook workbook = new Workbook(); // start with a fresh workbook
            // (Optionally load an existing file: new Workbook("input.xlsx"))

            // Populate some sample data
            workbook.Worksheets[0].Cells["A1"].PutValue(123.456789);
            workbook.Worksheets[0].Cells["B1"].PutValue("Sample Text");

            CsvSaveOptions csvOptions = new CsvSaveOptions
            {
                SignificantDigits = 4
            };
            string csvPath = @"C:\Temp\Digits.csv";
            workbook.Save(csvPath, csvOptions);
            Console.WriteLine($"Saved CSV to {csvPath}");

            // ---------- Step 2: Export worksheet as text with uppercase ----------
            ExportTableOptions tableOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, value) => value?.ToString().ToUpperInvariant()
            };
            string txtPath = @"C:\Temp\Table.txt";
            workbook.Worksheets[0].ExportTable(txtPath, tableOptions);
            Console.WriteLine($"Exported TXT to {txtPath}");

            // ---------- Step 3: Apply custom number format ----------
            Workbook eraWorkbook = new Workbook();
            Cell dateCell = eraWorkbook.Worksheets[0].Cells["A1"];
            dateCell.PutValue("Reiwa 3/04/01");

            Style eraStyle = eraWorkbook.CreateStyle();
            eraStyle.Number = 14; // short date format; replace with custom if needed
            dateCell.SetStyle(eraStyle);
            eraWorkbook.CalculateFormula();

            Console.WriteLine($"Japanese era date formatted: {dateCell.StringValue}");
        }
    }
}
```

**Förväntad utskrift**

```
Saved CSV to C:\Temp\Digits.csv
Exported TXT to C:\Temp\Table.txt
Japanese era date formatted: 4/1/2021
```

(Det exakta datumformatet kan variera beroende på ditt systems språk‑ och regioninställningar.)

---

## Vanliga frågor och hantering av kantfall

| Fråga | Svar |
|----------|--------|
| *Vad gör jag om jag behöver en annan avgränsare i CSV‑filen?* | Sätt `csvOptions.Separator` till `','`, `'\t'` eller någon annan tecken innan du anropar `Save`. |
| *Kan jag behålla den ursprungliga numeriska precisionen istället för att avrunda?* | Använd `SignificantDigits = 0` för att skriva hela double‑precision‑värdet, eller sätt `NumberDecimalSeparator` för språk‑specifika decimaltecken. |
| *Hur exporterar jag bara ett specifikt område istället för hela bladet?* | Anropa `ExportTable(string fileName, ExportTableOptions options, CellArea area)` och skicka in ett `CellArea` som definierar området. |
| *Vad händer om arbetsboken innehåller formler som refererar till andra blad?* | Se till att anropa `workbook.CalculateFormula()` innan export; annars får du de cachade värdena. |
| *Finns det ett sätt att behålla originalcellens formatering (typsnitt, färger) i TXT‑filen?* | Ren‑text‑format kan inte behålla visuell styling. Om du behöver rik formatering, överväg att exportera till HTML (`HtmlSaveOptions`) istället. |

---

## Slutsats

Du vet nu hur du **sparar arbetsbok som CSV** med kontrollerad precision, **exporterar excel till TXT** samtidigt som du tvingar **versala cellvärden**, och **tillämpa anpassat talformat** för lokalanpassad datumvisning. Varje kodsnutt är fristående, körs direkt och följer bästa praxis för både prestanda och underhållbarhet.

Nästa steg kan vara att utforska:

* Använda `HtmlSaveOptions` för att behålla styling vid export till webbvänliga format.  
* Utnyttja `CsvSaveOptions.Encoding` för UTF‑8 eller andra teckenkodningar när du hanterar flerspråkig data.  
* Automatisera batch‑behandling av flera kalkylblad genom att loopa över `workbook.Worksheets`.

Känn dig fri att anpassa koden till dina egna datapipelines, och låt Aspose.Cells‑flexibiliteten sköta det tunga arbetet.

---


## Vad bör du lära dig härnäst?


De följande handledningarna täcker närliggande ämnen som bygger vidare på teknikerna som demonstrerats i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Save Workbook To Text Csv Format](/cells/german/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)
- [Save Workbook To Text Csv Format](/cells/french/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)
- [Save Workbook To Text Csv Format](/cells/spanish/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}