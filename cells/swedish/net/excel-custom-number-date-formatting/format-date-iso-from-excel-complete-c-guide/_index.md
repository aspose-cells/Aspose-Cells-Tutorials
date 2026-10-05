---
category: general
date: 2026-03-30
description: Lär dig hur du formaterar datum i ISO när du läser Excel-datumvärden
  och extraherar datum‑ och tidsdata från Excel med Aspose.Cells i C#.
draft: false
keywords:
- format date iso
- read excel datetime
- extract datetime excel
- Aspose.Cells date parsing
- Japanese era dates
language: sv
og_description: formatera datum i ISO från Excel-data med Aspose.Cells. Denna guide
  visar hur du läser Excel-datum/tid, extraherar datum/tid‑värden från Excel och skriver
  ut ISO‑datum.
og_title: formatera datum ISO från Excel – Steg‑för‑steg C#‑handledning
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Formatera datum i ISO-format från Excel – Komplett C#‑guide
url: /sv/net/excel-custom-number-date-formatting/format-date-iso-from-excel-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# formatera datum iso från Excel – Komplett C#‑guide

Har du någonsin behövt **format date iso** när du hämtar datum från ett Excel‑ark? Kanske jonglerar du med japanska era‑datum, eller så vill du bara ha en ren `yyyy‑MM‑dd`‑sträng för en API‑payload. I den här handledningen kommer du att se exakt hur du **read Excel datetime**‑celler, **extract datetime Excel**‑värden, och omvandlar dem till ISO‑8601‑format—utan gissningar.

Vi går igenom ett verkligt exempel som använder Aspose.Cells, förklarar varför varje rad är viktig, och visar dig den slutgiltiga utskriften som du kan kopiera‑klistra in i ditt projekt. När du är klar kan du hantera knasiga era‑strängar som “令和3年5月1日” och producera ett standard‑ISO‑datum, redo för databaser, JSON eller var du än behöver det.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar även med .NET Framework)
- Aspose.Cells för .NET (gratis provversion eller licensierad version)
- Grundläggande kunskap om C# och Excel‑koncept
- Visual Studio eller någon annan C#‑redigerare du föredrar

Inga ytterligare NuGet‑paket krävs utöver Aspose.Cells, så installationen är ganska enkel.

---

## Steg 1: Skapa en arbetsbok och rikta in dig på det första kalkylbladet

Det första du gör är att skapa ett nytt `Workbook`‑objekt. Detta ger dig en minnes‑representation av en Excel‑fil, som du sedan kan manipulera eller läsa från.

```csharp
using Aspose.Cells;
using System.Globalization;

// Step 1: Initialize a new workbook and grab the first worksheet
Workbook workbook = new Workbook();                 // creates an empty .xlsx
Worksheet worksheet = workbook.Worksheets[0];      // the default sheet is "Sheet1"
```

*Why this matters:*  
Creating the workbook programmatically lets you avoid dealing with physical files during testing. It also ensures the worksheet reference is always valid—no null‑reference surprises later when you try to **read Excel datetime** values.

---

## Steg 2: Skriv en japansk era‑datumsträng i en cell

Vårt mål är att demonstrera parsning av ett icke‑gregorianskt datum. Vi placerar era‑strängen direkt i cell **A1**.

```csharp
// Step 2: Insert a Japanese era date string into cell A1
worksheet.Cells["A1"].PutValue("令和3年5月1日");
```

*Pro tip:* If you’re pulling data from an existing workbook, you’d skip the `PutValue` call and just reference the cell that already contains the date. The key is that the cell holds a **string** that represents a date in the Japanese lunisolar calendar.

---

## Steg 3: Konfigurera en kultur som förstår den japanska lunisolära kalendern

.NET:s `CultureInfo`‑klass låter dig ange hur datum ska tolkas. Genom att byta ut den standard‑gregorianska kalendern mot `JapaneseLunisolarCalendar` ger du parsern den kontext den behöver.

```csharp
// Step 3: Set up a culture using the Japanese lunisolar calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();
```

*Why we do this:*  
If you tried to parse “令和3年5月1日” with the default culture, .NET would throw a `FormatException`. Swapping in the lunisolar calendar tells the runtime exactly how to map “令和3年” (the 3rd year of the Reiwa era) to the Gregorian year 2021.

---

## Steg 4: Parsa cellvärdet som ett `DateTime` med den konfigurerade kulturen

Nu kommer hjärtat i operationen—att omvandla den era‑strängen till ett riktigt `DateTime`‑objekt. Aspose.Cells erbjuder en bekväm `GetDateTime`‑overload som accepterar en `CultureInfo`.

```csharp
// Step 4: Retrieve the cell value as a DateTime, respecting the Japanese culture
DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);
```

*What’s happening under the hood:*  
`GetDateTime` reads the raw string, applies the supplied culture’s calendar rules, and returns a `DateTime` that represents the same moment in the Gregorian calendar. This is the moment where you **extract datetime Excel** data in a form you can work with in .NET.

---

## Steg 5: Skriv ut det parsade datumet i ISO 8601‑format

Till sist formaterar vi `DateTime` som en ISO‑sträng—`yyyy‑MM‑dd`—som är universellt accepterad av API:er, databaser och front‑end‑ramverk.

```csharp
// Step 5: Print the date in ISO format (e.g., 2021-05-01)
Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // Output: 2021-05-01
```

*Why ISO?*  
ISO 8601 eliminates ambiguity. “05/01/2021” could be May 1st or January 5th depending on locale. `2021-05-01` is crystal clear, which is why we **format date iso** in almost every integration scenario.

---

## Fullt fungerande exempel

Nedan är det kompletta, körklara programmet. Kopiera det till ett konsol‑app‑projekt, lägg till Aspose.Cells‑referensen, och tryck **F5**.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and select the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // 3️⃣ Set up Japanese lunisolar culture
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();

        // 4️⃣ Parse the cell value as DateTime using the culture
        DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);

        // 5️⃣ Output the date in ISO format
        Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // 2021-05-01
    }
}
```

**Förväntad utskrift**

```
2021-05-01
```

Kör det en gång, så ser du det ISO‑formaterade datumet skrivet till konsolen. Det är hela kedjan från **read Excel datetime** till **format date iso**.

---

## Hantera vanliga edge‑fall

### 1. Celler som innehåller riktiga Excel‑datumnummer

Ibland lagrar Excel datum som serienummer (t.ex. `44204`). I så fall behöver du ingen kultur; anropa bara `GetDateTime()` utan parametrar:

```csharp
DateTime serialDate = worksheet.Cells["B2"].GetDateTime(); // B2 holds a numeric date
Console.WriteLine(serialDate.ToString("yyyy-MM-dd"));
```

### 2. Tomma eller ogiltiga celler

Om en cell är tom eller innehåller en oparsbar sträng, kommer `GetDateTime` att kasta ett undantag. Omge anropet med en `try/catch` eller kontrollera `IsDateTime` först:

```csharp
if (worksheet.Cells["C3"].Type == CellValueType.IsDateTime)
{
    DateTime safeDate = worksheet.Cells["C3"].GetDateTime();
    Console.WriteLine(safeDate.ToString("yyyy-MM-dd"));
}
else
{
    Console.WriteLine("Cell C3 does not contain a valid date.");
}
```

### 3. Olika era‑format

Andra japanska epoker (Heisei, Showa) följer samma mönster. Samma `JapaneseLunisolarCalendar` hanterar dem automatiskt, så du behöver ingen extra logik—mata bara in strängen.

---

## Pro‑tips & fallgropar

- **Performance:** When processing large spreadsheets, reuse a single `CultureInfo` instance instead of creating a new one inside a loop.
- **Thread Safety:** `CultureInfo` objects are read‑only after you set the calendar, so they’re safe to share across threads.
- **Aspose.Cells Licensing:** If you’re using the free trial, remember that some features may be limited after the trial period expires. The date parsing shown here works fine in both trial and licensed modes.
- **Time Zones:** The `DateTime` you get is **unspecified** (no time zone). If you need UTC, call `DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc)` or convert using `TimeZoneInfo`.

---

## Slutsats

Vi har gått igenom allt du behöver för att **format date iso** från en Excel‑arbetsbok med C#. Utifrån en rå japansk era‑sträng **read Excel datetime**, ställer in rätt kultur, **extract datetime excel**‑data, och slutligen skriver ut en ren ISO‑8601‑sträng. Metoden fungerar för alla datumrepresentationer som Excel kan kasta på dig, oavsett om det är ett serienummer, en lokalanpassad sträng eller ett traditionellt era‑format.

Nästa steg? Prova att loopa över en hel kolumn med datum, skriv tillbaka ISO‑resultaten till ett nytt blad, eller skicka dem direkt i en JSON‑payload till en webbtjänst. Om du är nyfiken på andra kalendersystem (hebreiska, islamiska) gör Aspose.Cells och .NET:s `CultureInfo` dessa experiment lika enkla.

Har du frågor eller ett knepigt datumformat du inte kan knäcka? Lägg en kommentar nedan, och lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}