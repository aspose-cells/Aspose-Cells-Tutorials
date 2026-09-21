---
category: general
date: 2026-03-22
description: Lär dig hur du formaterar datum/tid till ISO när du extraherar datum
  från Excel och visar ISO‑datum med Aspose.Cells i C#.
draft: false
keywords:
- format datetime to iso
- extract date from excel
- display iso date
- Aspose.Cells date parsing
- Japanese era dates
language: sv
og_description: Formatera datum och tid till ISO gjort enkelt. Denna guide visar hur
  du extraherar datum från Excel och visar ISO-datum med Aspose.Cells.
og_title: Formatera datum/tid till ISO i C# – Steg‑för‑steg‑handledning
tags:
- C#
- Aspose.Cells
- DateTime
- Excel
- ISO 8601
title: Formatera datum/tid till ISO i C# – Komplett guide
url: /sv/net/number-and-display-formats-in-excel/format-datetime-to-iso-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# format datetime to iso i C# – Komplett guide

Har du någonsin behövt **format datetime to iso** men källan finns i en Excel‑arbetsbok? Kanske innehåller cellen en japansk era som “令和3年5月1日” och du kliar dig i huvudet och undrar hur du omvandlar det till en ren `2021‑05‑01`‑sträng. Du är inte ensam. I den här handledningen kommer vi att **extract date from excel**, parsar den japanska eran och sedan **display iso date** i konsolen—allt med några rader C# och Aspose.Cells.

Vi går igenom allt du behöver: det nödvändiga NuGet‑paketet, den exakta koden du kan kopiera‑klistra, varför varje rad är viktig, och ett antal edge‑case‑tips. I slutet har du ett återanvändbart snippet som formaterar datetime to iso oavsett hur knasigt det ursprungliga Excel‑värdet ser ut.

## Vad du behöver

- .NET 6.0 eller senare (koden kompileras även på .NET Framework 4.6+)
- Visual Studio 2022 (eller någon annan editor du föredrar)
- **Aspose.Cells for .NET** NuGet‑paket – `Install-Package Aspose.Cells`
- En Excel‑fil (eller en ny arbetsbok) som innehåller ett datum i japansk era‑format

Det är allt. Inga extra bibliotek, ingen COM‑interop, bara en enda, väl‑dokumenterad metod.

## Steg 1: Skapa en arbetsbok och skriv ett datum i japansk era  

Först behöver vi en arbetsbok att arbeta med. Om du redan har en Excel‑fil kan du ladda den med `new Workbook("path")`. I det här exemplet skapar vi en ny arbetsbok i minnet och placerar en japansk era‑sträng i cell **A1**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date (Reiwa 3 = 2021) into A1
        sheet.Cells["A1"].PutValue("令和3年5月1日");
```

> **Varför vi gör detta:** Aspose.Cells behandlar cellvärden som strängar som standard. Genom att infoga den råa era‑texten simulerar vi ett verkligt scenario där en japansk kund har angett datum i sin inhemska kalender.

## Steg 2: Aktivera parsning av japansk era och extrahera datumet  

Aspose.Cells kan automatiskt översätta japanska era‑strängar till .NET `DateTime`‑objekt—förutsatt att du talar om för det. Flaggan `DateTimeParseOptions.EnableJapaneseEra` gör det tunga arbetet.

```csharp
        // 3️⃣ Retrieve the cell value while enabling Japanese era parsing
        CellValue parsed = sheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

> **Pro‑tips:** Om du glömmer `EnableJapaneseEra`‑alternativet kommer biblioteket att returnera den ursprungliga strängen, och din efterföljande konvertering kommer att misslyckas. Verifiera alltid `parsed.Type` om du hanterar blandat innehåll.

## Steg 3: Konvertera den parsade DateTime till ISO 8601  

Nu när vi har ett riktigt `DateTime` är det en barnlek att göra om det till en ISO‑formaterad sträng. Mönstret `"yyyy-MM-dd"` följer ISO 8601‑datumsdelen, vilket är vad de flesta API:er förväntar sig.

```csharp
        // 4️⃣ Convert to ISO 8601 (yyyy‑MM‑dd) and display it
        string isoDate = parsed.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

När programmet körs skrivs ut:

```
ISO date: 2021-05-01
```

Det är den **display iso date** du var ute efter.

## Fullt, körbart exempel  

Nedan är hela kodblocket som du kan kopiera rakt in i ett konsolprojekt. Inga dolda beroenden, ingen extra konfiguration.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a Japanese era date into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // Retrieve the cell value with Japanese era parsing enabled
        CellValue parsedValue = worksheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);

        // Convert the DateTime to ISO 8601 format and output it
        string isoDate = parsedValue.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

> **Förväntad output:** `ISO date: 2021-05-01`

## Steg‑för‑steg‑genomgång (Varför varje del är viktig)

| Steg | Vad händer | Varför det är viktigt |
|------|------------|-----------------------|
| **Create workbook** | Initierar en Excel‑behållare i minnet. | Ger dig en sandlåda för testning utan att röra filsystemet. |
| **PutValue** | Lagrar den råa japanska era‑strängen i **A1**. | Efterliknar verklig datainmatning; säkerställer att parsern ser exakt texten. |
| **GetValue with `EnableJapaneseEra`** | Omvandlar era‑strängen till ett .NET `DateTime`. | Hanterar kalenderomvandlingen automatiskt—inga manuella uppslagstabeller behövs. |
| **`ToString("yyyy-MM-dd")`** | Formaterar `DateTime` till ISO 8601. | Garantiar en kultur‑invariant, sorteringsbar datumsträng som accepteras av REST‑API:er, databaser osv. |
| **Console.WriteLine** | Visar det slutgiltiga ISO‑datumet. | Bekräftar att hela pipeline:n fungerar från början till slut. |

## Hantera vanliga variationer  

### 1. Olika cellpositioner  

Om ditt datum finns i **B2** eller ett namngivet område, ersätt helt enkelt `"A1"` med den aktuella adressen:

```csharp
worksheet.Cells["B2"].PutValue("令和2年12月31日");
var value = worksheet.Cells["B2"]
    .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

### 2. Flera datum i en kolumn  

När du behöver **extract date from excel** för många rader, loopa igenom det använda området:

```csharp
int lastRow = worksheet.Cells.MaxDataRow;
for (int i = 0; i <= lastRow; i++)
{
    var cell = worksheet.Cells[i, 0]; // column A
    var cv = cell.GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
    string iso = cv.DateTimeValue.ToString("yyyy-MM-dd");
    Console.WriteLine($"Row {i + 1}: {iso}");
}
```

### 3. Fallback för icke‑era datum  

Om en cell redan innehåller en standard datumsträng fungerar parsern fortfarande, men du kanske vill ha ett skyddsnät:

```csharp
CellValue cv = cell.GetValue(CellValueType.DateTime,
    DateTimeParseOptions.EnableJapaneseEra | DateTimeParseOptions.TryParse);
```

Flaggan `TryParse` förhindrar undantag och returnerar det ursprungliga värdet om konverteringen misslyckas.

### 4. Tidskomponent  

Om du även behöver tidsdelen, använd `"yyyy-MM-ddTHH:mm:ss"`:

```csharp
string isoDateTime = parsedValue.DateTimeValue.ToString("yyyy-MM-ddTHH:mm:ss");
```

Det ger en fullständig ISO 8601‑tidsstämpel (`2021-05-01T00:00:00`).

## Visuell hjälp  

![exempel på format datetime to iso](image.png "Ett exempel på format datetime to iso i C#")

*Alt‑text:* *exempel på format datetime to iso som visar konsolutdata*

## Vanliga frågor  

- **Kan jag använda detta med .xls‑filer?**  
  Ja. Aspose.Cells stödjer `.xls`, `.xlsx`, `.csv` och många andra format direkt ur lådan.

- **Vad händer om arbetsboken är lösenordsskyddad?**  
  Ladda den med `new Workbook("file.xlsx", new LoadOptions { Password = "secret" })`.

- **Är ISO‑formatet lokalt beroende?**  
  Nej. Mönstret `"yyyy-MM-dd"` är kultur‑invariant och garanterar samma sträng på vilken maskin som helst.

- **Fungerar detta på .NET Core?**  
  Absolut—Aspose.Cells är kompatibel med .NET Standard 2.0.

## Sammanfattning  

Vi har gått igenom hur man **format datetime to iso** genom att **extract date from excel**, parsar japanska era‑strängar och slutligen **display iso date** i konsolen. De grundläggande stegen—skapa en arbetsbok, skriv eller läs in era‑texten, aktivera japansk era‑parsning och formatera med `ToString("yyyy-MM-dd")`—är allt du behöver för de flesta scenarier.

Nästa steg kan vara att:

- Skriva tillbaka ISO‑datumen till en annan kolumn för vidare bearbetning.  
- Exportera den transformerade arbetsboken till CSV för massimport.  
- Kombinera denna logik med ett web‑API som accepterar Excel‑uppladdningar och returnerar JSON‑kodade ISO‑datum.

Känn dig fri att experimentera med olika datumformat, tidszoner eller till och med anpassade kalendrar. Flexibiliteten i Aspose.Cells innebär att du sällan stöter på en vägg.

Lycka till med kodandet, och må alla dina datum vara perfekt ISO‑kompatibla!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}