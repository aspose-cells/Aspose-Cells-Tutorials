---
category: general
date: 2026-02-26
description: Skapa en ny arbetsbok i C# och lär dig hur du laddar Excel‑filer, ställer
  in kalendern på japanska och extraherar datum från Excel utan ansträngning.
draft: false
keywords:
- create new workbook
- how to load excel
- how to set calendar
- extract date from excel
- read japanese dates
language: sv
og_description: Skapa en ny arbetsbok i C# och lär dig snabbt hur du laddar Excel,
  ställer in en japansk kalender och extraherar datum från Excel‑filer.
og_title: Skapa ny arbetsbok i C# – Ladda Excel med japansk kalender
tags:
- C#
- Excel
- Aspose.Cells
- DateTime
title: Skapa ny arbetsbok i C# – Ladda Excel med japansk kalender
url: /sv/net/loading-and-saving-excel-files-with-options/create-new-workbook-in-c-load-excel-with-japanese-calendar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa ny arbetsbok i C# – Ladda Excel med japansk kalender

Har du någonsin behövt **create new workbook** i C# men varit osäker på hur du får Excel att respektera den japanska kalendern? Du är inte ensam. I många företagsmiljöer får du kalkylblad som lagrar datum i det japanska era‑systemet, och att extrahera dessa datum korrekt kan kännas som att avkoda ett hemligt språk.

Här är grejen: du kan **create new workbook**, tala om för laddaren att tolka datum med den japanska kalendern, och sedan **extract date from excel** med bara några rader kod. I den här guiden går vi igenom *how to load excel*, *how to set calendar* för japanska datum, och slutligen *read Japanese dates* från en cell. Inga onödiga detaljer—bara ett komplett, körbart exempel som du kan kopiera‑klistra in i ditt projekt.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar även på .NET Framework 4.6+)  
- **Aspose.Cells**‑biblioteket (gratis provversion eller licensierad version). Installera det via NuGet:

```bash
dotnet add package Aspose.Cells
```

- En Excel‑fil (`JapanDates.xlsx`) som innehåller japanska era‑datum i cell A1.

Det är allt. Om du har dessa kan vi hoppa rakt in.

---

## Skapa ny arbetsbok och ställ in japansk kalender

Det första steget är att **create new workbook**‑objektet och konfigurera `LoadOptions` så att parsern vet vilken kalender som ska användas.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Step 2: Set load options to interpret dates using the Japanese calendar
        workbook.LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese };

        // Step 3: Load the workbook from a file
        workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");

        // Step 4: Access cell A1 – it now contains a proper DateTime value
        var cellA1 = workbook.Worksheets[0].Cells["A1"];
        DateTime dateValue = cellA1.GetDateTime();

        Console.WriteLine($"The Japanese date in A1 is: {dateValue:yyyy-MM-dd}");
    }
}
```

> **Pro tip:** `LoadOptions.Calendar`‑egenskapen accepterar flera enum‑värden (`Gregorian`, `Japanese`, `Hijri`, etc.). Att välja rätt säkerställer att biblioteket översätter era‑texten (t.ex. “令和3年”) till en .NET `DateTime`.

![skärmdump av exempel på ny arbetsbok](image-url.png "Skärmdump som visar en ny arbetsbokinstans med japanska kalenderinställningar"){: .align-center alt="skärmdump av exempel på ny arbetsbok"}

### Varför detta fungerar

- **Workbook creation**: `new Workbook()` ger dig en ren start—inga dolda arbetsblad, ingen standarddata.
- **LoadOptions**: Genom att tilldela `CalendarType.Japanese` *innan* du anropar `Load` behandlar parsern alla era‑baserade strängar som datum snarare än vanlig text.
- **GetDateTime()**: Efter inläsning returnerar `cellA1.GetDateTime()` ett riktigt `DateTime`‑objekt, vilket låter dig utföra aritmetik, formatering eller databasinsättningar utan extra konverteringssteg.

---

## Hur du laddar Excel‑fil korrekt

Du kanske undrar, “Finns det ett speciellt sätt att **how to load excel** när man hanterar icke‑gregorianska kalendrar?” Svaret är ja—ställ alltid in `LoadOptions` *innan* du anropar `Load`. Om du laddar först och sedan ändrar kalendern har datumen redan parsats felaktigt.

```csharp
// Example of a wrong order – will treat Japanese dates as plain strings
Workbook badWorkbook = new Workbook();
badWorkbook.Load("JapanDates.xlsx");          // Loads with default Gregorian calendar
badWorkbook.LoadOptions.Calendar = CalendarType.Japanese; // Too late!
```

Kodsnutten ovan visar ett vanligt fallgropar. Den korrekta ordningen (som visas i föregående avsnitt) garanterar att motorn tolkar cellerna *som datum* redan från början.

---

## Hur du ställer in kalender för japanska datum

Om du behöver byta kalender i farten—t.ex. bearbeta en batch av filer som använder olika erasystem—kan du återanvända samma `Workbook`‑objekt med nya `LoadOptions` varje gång.

```csharp
void LoadWithCalendar(string filePath, CalendarType calendar)
{
    Workbook wb = new Workbook
    {
        LoadOptions = new LoadOptions { Calendar = calendar }
    };
    wb.Load(filePath);
    // Now you can read dates according to the chosen calendar
}
```

Att anropa `LoadWithCalendar("JapanDates.xlsx", CalendarType.Japanese)` ger samma resultat som vårt huvudexempel, medan `CalendarType.Gregorian` skulle behandla samma cell som en vanlig sträng (eller kasta ett undantag om formatet är oigenkännligt).

---

## Extrahera datum från Excel – Läsa japanska datum

Nu när arbetsboken är laddad med rätt kalender är det enkelt att hämta datumet. Metoden `Cell.GetDateTime()` returnerar ett `DateTime`‑objekt som respekterar era‑konverteringen.

```csharp
DateTime ExtractJapaneseDate(Workbook wb, string address)
{
    var cell = wb.Worksheets[0].Cells[address];
    return cell.GetDateTime(); // Returns a .NET DateTime
}

// Usage
DateTime japaneseDate = ExtractJapaneseDate(workbook, "A1");
Console.WriteLine($"Extracted date: {japaneseDate:d}");
```

### Kantfall & Vad‑om‑scenarier

| Situation                              | Vad att göra                                                                                               |
|----------------------------------------|------------------------------------------------------------------------------------------------------------|
| Cellen innehåller **text** istället för ett datum | Anropa `cell.GetString()` först, validera med `DateTime.TryParse`, eller upprätthåll datavalidering i Excel. |
| Flera arbetsblad behöver bearbetas    | Loopa igenom `workbook.Worksheets` och tillämpa samma extraktionslogik på varje blad.                     |
| Datum lagras som **nummer** (Excel‑serial) | `cell.GetDateTime()` fungerar fortfarande eftersom Aspose.Cells automatiskt konverterar serialnummer.      |
| Filen är **lösenordsskyddad**         | Använd `LoadOptions.Password = "yourPwd"` innan du anropar `Load`.                                       |

---

## Fullt fungerande exempel (klar att kopiera‑klistra in)

Nedan är det kompletta programmet som du kan klistra in i en konsolapp. Det inkluderar felhantering och demonstrerar alla fyra sekundära nyckelord i kontext.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // 1️⃣  Create new workbook and configure calendar (primary keyword)
        // --------------------------------------------------------------------
        Workbook workbook = new Workbook
        {
            LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese }
        };

        // --------------------------------------------------------------------
        // 2️⃣  How to load excel – correct order matters (secondary keyword)
        // --------------------------------------------------------------------
        try
        {
            workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load Excel file: {ex.Message}");
            return;
        }

        // --------------------------------------------------------------------
        // 3️⃣  How to set calendar – already done before loading (secondary)
        // --------------------------------------------------------------------
        // (If you need to change it later, see the LoadWithCalendar method above.)

        // --------------------------------------------------------------------
        // 4️⃣  Extract date from excel – read Japanese dates (secondary keywords)
        // --------------------------------------------------------------------
        try
        {
            var cell = workbook.Worksheets[0].Cells["A1"];
            DateTime japaneseDate = cell.GetDateTime(); // Proper DateTime thanks to the calendar setting
            Console.WriteLine($"Japanese date in A1 → {japaneseDate:yyyy-MM-dd}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error extracting date: {ex.Message}");
        }
    }
}
```

**Förväntad output** (förutsatt att A1 innehåller “令和3年5月12日”):

```
Japanese date in A1 → 2021-05-12
```

Om cellen innehåller ett gregorianskt datum som “2021‑05‑12”, fungerar samma kod fortfarande eftersom biblioteket smidigt faller tillbaka till den gregorianska tolkningen.

---

## Slutsats

Du vet nu hur du **create new workbook**, korrekt **how to load excel**, ställer in rätt **how to set calendar**, och slutligen **extract date from excel** medan du **read Japanese dates** utan någon manuell parsning. Det viktigaste är att kalendern måste definieras *innan* inläsning; när arbetsboken väl är i minnet har datumen redan materialiserats som riktiga `DateTime`‑objekt.

### Vad blir nästa?

- **Batch processing**: Loopa igenom en mapp med filer och anropa `LoadWithCalendar` för varje.
- **Export to other formats**: Använd `workbook.Save("output.csv")` efter konvertering.
- **Localization**: Kombinera `CultureInfo` med `DateTime.ToString` för att visa datum på användarens föredragna språk.

Känn dig fri att experimentera—byt `CalendarType.Japanese` mot `CalendarType.Hijri` eller `CalendarType.Gregorian` och se hur samma kod anpassar sig automatiskt. Om du stöter på problem, lämna en kommentar nedan eller kolla Aspose.Cells‑dokumentationen för djupare API‑insikter.

Lycka till med kodandet, och njut av att omvandla de mystiska japanska era‑datumen till rena .NET `DateTime`‑värden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}