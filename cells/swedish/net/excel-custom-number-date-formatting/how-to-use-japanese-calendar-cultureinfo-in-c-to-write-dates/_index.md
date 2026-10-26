---
category: general
date: 2026-10-26
description: Lär dig hur du använder japansk kalender CultureInfo i C# när du parsar
  era‑datum och infogar dem i ett Excel‑ark med NPOI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: sv
lastmod: 2026-10-26
og_description: Använd den japanska kalendern CultureInfo i C# för att tolka datum
  i Reiwa‑eran och skriva dem till ett Excel‑ark. Komplett, körbar kod med förklaringar.
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: Använd japansk kalender CultureInfo i C# – fullständigt Excel‑exempel
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
    dates and inserting them into an Excel worksheet with NPOI.
  headline: How to use Japanese calendar CultureInfo in C# to write dates to Excel
  type: TechArticle
tags:
- C#
- CultureInfo
- Excel
- NPOI
- Internationalization
title: Hur man använder japansk kalender CultureInfo i C# för att skriva datum till
  Excel
url: /sv/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder japansk kalender CultureInfo i C# för att skriva datum till Excel

Om du behöver **använda japansk kalender CultureInfo** när du arbetar med datum i C#, visar den här guiden exakt hur. Du kommer att lära dig att tolka en datumsträng som innehåller ett japanskt era‑namn (till exempel *Reiwa 2/5/1*) och sedan skriva det resulterande `DateTime` i den första cellen i ett Excel‑arbetsblad med hjälp av NPOI‑biblioteket.

Att tolka era‑baserade datum utan korrekt `CultureInfo` leder till `FormatException` eller felaktiga månad/dag‑värden. Genom att konfigurera `CultureInfo` till den japanska kalendern säkerställer du att .NET‑runtime tolkar eran korrekt och att värdet du sparar i Excel matchar den ursprungliga japanska notationen.

I den här handledningen kommer du att:

* Skapa ett `CultureInfo`‑objekt som använder den japanska kalendern.
* Tolka en japansk era‑datumsträng med `DateTime.Parse`.
* Infoga det tolkade `DateTime` i en NPOI‑arbetsbladscell.
* Se det kompletta, körbara programmet och förväntad output.

> **Förutsättningar** – .NET 6.0+ (eller .NET Core 3.1+), **NPOI**‑NuGet‑paketet, och en grundläggande förståelse för C# och hantering av Excel‑filer.

---

## Vad du behöver

| Item | Reason |
|------|--------|
| **.NET SDK** (6.0 or later) | Tillhandahåller runtime och bibliotek för `CultureInfo`. |
| **NPOI** (`NPOI` NuGet package) | Gör det möjligt att skapa och manipulera Excel‑filer utan att Office är installerat. |
| **Visual Studio Code**, **Visual Studio**, or any C# IDE | För att kompilera och köra exemplet. |
| **Japanese era date string** (e.g., `"Reiwa 2/5/1"`) | Visar hur den japanska kalendern används. |

## Steg 1: Installera NPOI

Öppna en terminal i din projektmapp och kör:

```bash
dotnet add package NPOI --version 2.6.1
```

Paketet tillhandahåller typerna `IWorkbook`, `ISheet` och `ICell` som används senare.

## Steg 2: Skapa ett CultureInfo som använder den japanska kalendern

Den japanska kalendern är en era‑baserad kalender. Du måste begära *Japanese*-varianten av `ja-JP`‑lokalen och explicit sätta kalendern till `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **Varför detta är viktigt** – Standard‑kulturen `ja-JP` använder den gregorianska kalendern. Genom att återtilldela `Calendar`‑egenskapen säkerställer du att eranamn som *Reiwa* känns igen vid tolkning.

## Steg 3: Tolka en japansk era‑datumsträng

Nu när `CultureInfo` är konfigurerad kan du säkert tolka en sträng som innehåller ett eranamn.

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**Resultat**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

`Parse`‑metoden tolkar *Reiwa 2* som det gregorianska året 2020, månad 5, dag 1.

### Kantfall: hantera ogiltiga eror

Om en användare anger en ej stödd era (t.ex. `"Heisei 31/4/30"` efter att Heisei‑eran avslutades), kastar `DateTime.Parse` ett `FormatException`. Omge anropet med ett try‑catch‑block för att ge ett vänligt felmeddelande:

```csharp
try
{
    DateTime parsed = DateTime.Parse(input, japaneseCulture);
}
catch (FormatException)
{
    Console.Error.WriteLine($"'{input}' is not a valid Japanese era date.");
}
```

## Steg 4: Skriv det tolkade DateTime‑värdet i ett Excel‑arbetsblad

När `DateTime`‑objektet är klart kan du lagra det i en Excel‑cell. NPOI formaterar automatiskt `DateTime`‑värden som Excel‑datum.

```csharp
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;
using System.IO;

// Create a new workbook and a sheet.
IWorkbook workbook = new XSSFWorkbook();
ISheet sheet = workbook.CreateSheet("Japanese Dates");

// Write the DateTime into cell A1 (row 0, column 0).
IRow row = sheet.CreateRow(0);
ICell cell = row.CreateCell(0);
cell.SetCellValue(reiwaDate);

// Optionally apply a date style that shows the era (Excel does not have a built‑in era format,
// so we keep the Gregorian representation).
ICellStyle dateStyle = workbook.CreateCellStyle();
short dateFormatId = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
dateStyle.DataFormat = dateFormatId;
cell.CellStyle = dateStyle;

// Save the workbook to a file.
using (FileStream fs = new FileStream("JapaneseEraDate.xlsx", FileMode.Create, FileAccess.Write))
{
    workbook.Write(fs);
}
Console.WriteLine("Excel file 'JapaneseEraDate.xlsx' created successfully.");
```

**Resultat** – När du öppnar *JapaneseEraDate.xlsx* visas datumet **2020‑05‑01** i cell A1.

### Varför använda NPOI?

*Fungerar på alla plattformar* (Windows, Linux, macOS) och kräver **inte** Microsoft Office. Detta gör lösningen lämplig för CI‑pipelines, Docker‑behållare eller server‑sidig bearbetning.

## Steg 5: Fullständigt, körbart program

När allt sätts ihop, här är ett komplett konsolprogram som demonstrerar hela flödet:

```csharp
// File: Program.cs
using System;
using System.Globalization;
using System.IO;
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure CultureInfo for the Japanese calendar.
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // 2️⃣ Parse a Japanese era date string.
        string eraDate = "Reiwa 2/5/1";
        DateTime reiwaDate;
        try
        {
            reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
            Console.WriteLine($"Parsed DateTime: {reiwaDate:u}");
        }
        catch (FormatException)
        {
            Console.Error.WriteLine($"'{eraDate}' is not a valid Japanese era date.");
            return;
        }

        // 3️⃣ Create an Excel workbook and write the date.
        IWorkbook workbook = new XSSFWorkbook();
        ISheet sheet = workbook.CreateSheet("Japanese Dates");
        IRow row = sheet.CreateRow(0);
        ICell cell = row.CreateCell(0);
        cell.SetCellValue(reiwaDate);

        // Apply a simple Gregorian date format.
        ICellStyle style = workbook.CreateCellStyle();
        short fmt = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
        style.DataFormat = fmt;
        cell.CellStyle = style;

        // 4️⃣ Save the workbook.
        const string fileName = "JapaneseEraDate.xlsx";
        using (FileStream fs = new FileStream(fileName, FileMode.Create, FileAccess.Write))
        {
            workbook.Write(fs);
        }

        Console.WriteLine($"Excel file '{fileName}' created successfully.");
    }
}
```

**Hur du kör**

```bash
dotnet run
```

Efter körning hittar du `JapaneseEraDate.xlsx` i projektmappen med det korrekt tolkade datumet.

## Vanliga fallgropar och bästa praxis‑tips

| Fallgrop | Lösning / Rekommendation |
|---------|----------------------|
| Glömmer att sätta `japaneseCulture.DateTimeFormat.Calendar` | Tilldela alltid en `JapaneseCalendar`‑instans; annars känns eranamnet inte igen. |
| Använder `DateTime.TryParse` utan den anpassade `CultureInfo` | Skicka samma `japaneseCulture` till `TryParse` för att behålla samma beteende. |
| Förväntar sig att Excel visar eranamnet | Excels inbyggda datumformat är endast gregorianska. Om du behöver visa eran, lagra den ursprungliga strängen i en separat kolumn eller skapa ett eget textformat. |
| Inte disponerar `FileStream` | Använd ett `using`‑block (som visas) för att säkerställa att filhandtaget frigörs omedelbart. |
| Blandar `CultureInfo`‑objekt över trådar | `CultureInfo` är trådsäker för skriv‑skyddade operationer, men undvik att ändra dess `Calendar`‑egenskap efter initial konfiguration. |

## Slutsats

Du vet nu hur du **använder japansk kalender CultureInfo** i C# för att exakt tolka japanska era‑datum och skriva det resulterande `DateTime` i ett Excel‑arbetsblad med NPOI. Det kompletta exemplet täcker konfiguration, tolkning, felhantering och Excel‑output, vilket ger dig en solid grund för alla internationaliserade rapporterings‑ eller datautbytes‑scenarier.

Nästa steg kan du utforska:

* **Formatera datum med anpassad text** för att behålla eranamnet i Excel.
* **Läsa datum från Excel** med `cell.DateCellValue` samtidigt som du respekterar den japanska kalendern.
* **Applicera samma teknik** för andra era‑baserade kalendrar (t.ex. thailändsk buddhistisk kalender) genom att byta `JapaneseCalendar` mot lämplig `Calendar`‑subklass.

Känn dig fri att experimentera med olika erasträngar, större datamängder, eller integrera denna logik i ASP.NET Core‑API:er som genererar Excel‑rapporter i realtid. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa Excel‑arbetsbok med japanska kalenderdatum – Fullständig guide](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Tolka japanska era‑datum i Excel – Full guide för C#‑utvecklare](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [Hur man skapar Excel‑arbetsbok och tolkar japanska datum i C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}