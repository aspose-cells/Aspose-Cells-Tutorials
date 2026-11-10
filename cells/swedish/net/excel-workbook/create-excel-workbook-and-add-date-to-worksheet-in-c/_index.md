---
category: general
date: 2026-10-13
description: Skapa en Excel-arbetsbok i C# och skriv datum till Excel med Aspose.Cells.
  Lär dig att spara Excel-filen som xlsx och lägga till datum i kalkylbladet med fullständig
  kod.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save excel file
- write date to excel
- save workbook as xlsx
- add date to worksheet
language: sv
lastmod: 2026-10-13
og_description: Skapa en Excel-arbetsbok i C# och skriv datum till Excel. Följ den
  här kompletta guiden för att spara Excel-filen som xlsx och lägga till datum i kalkylbladet
  med Aspose.Cells.
og_image_alt: Excel workbook screenshot showing a Japanese imperial date in cell A1
og_title: Skapa Excel-arbetsbok och lägg till datum i kalkylblad – C# steg för steg
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Create excel workbook in C# and write date to excel using Aspose.Cells.
    Learn to save excel file as xlsx and add date to worksheet with full code.
  headline: Create excel workbook and add date to worksheet in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Skapa Excel-arbetsbok och lägg till datum i kalkylblad i C#
url: /sv/net/excel-workbook/create-excel-workbook-and-add-date-to-worksheet-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel-arbetsbok och lägg till datum i kalkylblad i C#

Om du behöver **create excel workbook** programatiskt, visar den här guiden hur du **write date to excel** och **save excel file** som en *.xlsx* arbetsbok. Du får se ett komplett, körbart exempel som parsar en japansk kejserlig era‑sträng och lagrar det resulterande `DateTime` i cell A1.

Att arbeta med Excel från C# kräver ofta tre steg: skapa en instans av arbetsboken, lägga data på ett kalkylblad och slutligen spara filen. Denna handledning täcker varje steg, förklarar varför koden är skriven på detta sätt och lyfter fram vanliga fallgropar såsom kultur‑specifik parsning och fil‑systembehörigheter. I slutet kan du **add date to worksheet**, **save workbook as xlsx**, och anpassa mönstret för vilken datatyp som helst.

> **Förutsättning** – Exemplet använder **Aspose.Cells for .NET**‑biblioteket (version 23.10 eller senare). Installera det via NuGet:

```bash
dotnet add package Aspose.Cells
```

Du behöver också ett .NET 6+ SDK och en skrivbar katalog för utdatafilen.

---

## Skapa Excel-arbetsbok och konfigurera kalkylblad

Det första steget är att skapa en instans av en tom arbetsbok och hämta dess standardkalkylblad. Aspose.Cells skapar automatiskt en arbetsbok med ett blad som heter “Sheet1”.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

// Step 1: Create a new workbook
Workbook workbook = new Workbook();

// Step 2: Get the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];
```

**Varför detta är viktigt** – `Workbook` är ingångspunkten för alla Excel‑operationer. Genom att skapa den utan parametrar får du en ren arbetsbok som du senare kan **save excel file** i vilket format du önskar.

---

## Parsning av japanskt kejserligt datum

Japanska kejserliga datum använder en era‑symbol (t.ex. “R” för Reiwa) följt av ett tvåsiffrigt år. .NET `DateTime.ParseExact`‑metoden kan hantera detta format när du tillhandahåller ett anpassat `DateTimeParseOptions`‑objekt som instruerar parsern att använda den japanska kejsarkalendern.

```csharp
// Step 3: Define a date string in the Japanese imperial era
string imperialDate = "R3/04/01"; // Reiwa 3, April 1st

// Step 4: Configure parsing options for the Japanese Emperor calendar
var parseOptions = new DateTimeParseOptions
{
    Calendar = DateTimeParseOptions.CalendarType.JapaneseEmperor
};

// Step 5: Parse the string into a .NET DateTime
DateTime parsedDate = DateTime.ParseExact(
    imperialDate,
    "ggyy/MM/dd",
    CultureInfo.InvariantCulture,
    DateTimeStyles.None,
    parseOptions);
```

**Förklaring** –  
* `gg` läser era‑designatorn (`R` för Reiwa).  
* `yy` läser det tvåsiffriga året inom den eran.  
* `MM/dd` läser månad och dag.  

Om du utelämnar `parseOptions` antar parsern den gregorianska kalendern och kastar ett `FormatException`. Detta är ett vanligt kantfall när man arbetar med icke‑gregorianska kalendrar.

---

## Skriv datum till kalkylblad

Nu när du har ett `DateTime`‑värde kan du placera det i en cell. Aspose.Cells formaterar automatiskt cellen baserat på värdets typ.

```csharp
// Step 6: Write the parsed date into cell A1
sheet.Cells["A1"].PutValue(parsedDate);

// Optional: Apply a date format for better readability
Style style = workbook.CreateStyle();
style.Custom = "yyyy-mm-dd";
sheet.Cells["A1"].SetStyle(style);
```

**Varför ange en stil?** – Utan en stil kan Excel visa datumet med systemets standardformat, vilket kan vara förvirrande för användare i andra regioner. Att explicit definiera `"yyyy-mm-dd"` säkerställer ett enhetligt utseende.

---

## Spara Excel-fil som xlsx

Slutligen sparas arbetsboken till disk. `Save`‑metoden bestämmer utdataformatet från filändelsen, så att använda “.xlsx” automatiskt aktiverar Office Open XML‑formatet.

```csharp
// Step 7: Define the output path (adjust to your environment)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "JapaneseDate.xlsx");

// Step 8: Save the workbook
workbook.Save(outputPath, SaveFormat.Xlsx);
```

**Tips** – Om mål katalogen inte finns eller du saknar skrivrättigheter, kastar `Save` ett `IOException`. Verifiera alltid sökvägen innan du anropar `Save`.

---

## Fullständigt körbart exempel

Nedan är det fullständiga programmet som du kan kopiera, klistra in och köra. Det inkluderar alla `using`‑direktiv, felhantering och kommentarer som förklarar varje operation.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;
using System.IO;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Define the Japanese imperial date string
            string imperialDate = "R3/04/01"; // Reiwa 3, April 1st

            // 3️⃣ Set up parsing options for the Japanese Emperor calendar
            var parseOptions = new DateTimeParseOptions
            {
                Calendar = DateTimeParseOptions.CalendarType.JapaneseEmperor
            };

            // 4️⃣ Parse the string into a .NET DateTime
            DateTime parsedDate = DateTime.ParseExact(
                imperialDate,
                "ggyy/MM/dd",
                CultureInfo.InvariantCulture,
                DateTimeStyles.None,
                parseOptions);

            // 5️⃣ Write the date to cell A1
            sheet.Cells["A1"].PutValue(parsedDate);

            // Apply a consistent date format
            Style dateStyle = workbook.CreateStyle();
            dateStyle.Custom = "yyyy-mm-dd";
            sheet.Cells["A1"].SetStyle(dateStyle);

            // 6️⃣ Determine the output file location
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "JapaneseDate.xlsx");

            // 7️⃣ Save the workbook as an .xlsx file
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Workbook saved successfully to: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

**Förväntat resultat**

När du öppnar `JapaneseDate.xlsx` innehåller cell A1 datumet **2021‑04‑01** (det gregorianska motsvarande av Reiwa 3 / 04 / 01) visat i formatet `yyyy‑mm‑dd`.

![Excel workbook with date in cell A1](excel-date-screenshot.png){alt="Skärmdump av en Excel-arbetsbok som visar ett japanskt kejserligt datum i cell A1"}

---

## Vanliga frågor och kantfall

| Fråga | Svar |
|----------|--------|
| *Vad händer om eran ändras (t.ex. Heisei till Reiwa)?* | Den `JapaneseEmperor`‑kalendern mappar automatiskt era‑symboler (`H`, `R`, etc.) till rätt gregorianska intervall, så du behöver bara uppdatera inmatningssträngen. |
| *Kan jag skriva flera datum i en kolumn?* | Ja. Loopa över dina data och anropa `sheet.Cells[row, column].PutValue(dateValue)` för varje rad. |
| *Vad gör jag om jag behöver ett annat datumformat?* | Ändra `dateStyle.Custom` till någon Excel‑datumformatsträng, t.ex. `"dd-mmm-yyyy"` eller `"mm/dd/yyyy"`. |
| *Finns det ett sätt att skydda bladet efter att ha skrivit datumet?* | Använd `sheet.Protect(ProtectOptions.All, "password")` innan du sparar. |
| *Hur hanterar jag tidszoner?* | `DateTime` lagrar UTC eller lokal tid. Konvertera med `DateTime.SpecifyKind` eller `TimeZoneInfo.ConvertTime` innan du anropar `PutValue`. |

---

## Slutsats

Du vet nu hur du **create excel workbook**, **write date to excel**, **add date to worksheet**, och **save workbook as xlsx** med Aspose.Cells i C#. Det kompletta exemplet demonstrerar parsning av en japansk kejserlig kalendrarsträng, tillämpning av en enhetlig stil och hantering av fil‑systemaspekter.  

Från här kan du

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa Excel-arbetsbok C# – Lägg till kommentar och spara som XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [Skapa ny arbetsbok i C# – Lägg till formel och spara Excel-fil](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Skapa Excel-arbetsbok – Radbryt kolumner och spara som XLSX](/cells/english/net/formatting-rows-and-columns-in-excel/create-excel-workbook-wrap-columns-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}