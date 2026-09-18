---
category: general
date: 2026-02-28
description: Lär dig hur du ställer in datumformat i Excel, läser datum och tid i
  Excel, extraherar datum från Excel och beräknar arbetsboksformler med Aspose.Cells
  i C#. Fullt körbart exempel.
draft: false
keywords:
- set excel date format
- read excel datetime
- extract date from excel
- calculate workbook formulas
- get datetime cell
language: sv
og_description: Mästra att ställa in Excel-datumformat, läsa Excel-datum/tid, extrahera
  datum och beräkna arbetsboksformler med ett komplett C#‑exempel.
og_title: Ställ in Excel‑datumformat i C# – Komplett steg‑för‑steg‑guide
tags:
- Aspose.Cells
- C#
- Excel automation
title: Ställ in Excel-datumformat i C# – Komplett steg‑för‑steg‑guide
url: /sv/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# sätt excel datumformat – Komplett C#‑guide

Har du någonsin haft problem med att **sätta excel datumformat** när du genererar kalkylblad i farten? Du är inte ensam. Många utvecklare stöter på hinder när cellen visar en rå sträng istället för ett riktigt datum, särskilt med japanska erasträngar eller anpassade lokala strängar.  

I den här handledningen går vi igenom ett verkligt exempel som **sätter Excel datumformat**, sedan **läser excel datum‑tid**, **extraherar datum från excel**, och till och med **beräknar arbetsboksformler** så att du slutligen kan **hämta datum‑tid‑celler** som inbyggda .NET `DateTime`‑objekt. Inga externa referenser, bara ett självständigt, körbart kodexempel som du kan klistra in i Visual Studio och se fungera direkt.

## Vad du behöver

- **Aspose.Cells for .NET** (valfri nyare version; API‑et som används här fungerar med 23.x och senare)  
- .NET 6 eller senare (koden kompileras även med .NET Framework 4.6+)  
- En grundläggande förståelse för C#‑syntax – om du kan skriva `Console.WriteLine` är du klar.

Det är allt. Inga extra NuGet‑paket utöver Aspose.Cells, ingen Excel‑installation krävs.

## Hur man sätter excel datumformat i C#  

Det första vi gör är att berätta för Excel att cellen innehåller ett datum, inte bara text. Aspose.Cells tillhandahåller ett inbyggt nummerformat‑ID (`14`) som motsvarar kortdatum‑mönstret för den aktuella lokalen.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Step 2: Write a Japanese era date string into cell A1
        sheet.Cells["A1"].PutValue("Reiwa 2-04-01");

        // Step 3: Apply the standard date number format (ID 14) to A1
        // This tells Excel to treat the cell as a date.
        sheet.Cells["A1"].Style.Number = 14;

        // Step 4: Force Excel to recalculate formulas so the value is parsed
        workbook.CalculateFormula();

        // Step 5: Retrieve the parsed value as a .NET DateTime
        DateTime parsedDate = sheet.Cells["A1"].GetDateTime();

        // Step 6: Show the result – should be 2020‑04‑01
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
    }
}
```

> **Proffstips:** Anropet `CalculateFormula()` är avgörande. Utan det behåller cellen den råa strängen, och `GetDateTime()` skulle kasta ett undantag. Den här raden tvingar Aspose.Cells att köra sin interna parser, vilket effektivt **beräknar arbetsboksformler** åt oss.

Utdata du ser när du kör programmet är:

```
Parsed DateTime: 2020-04-01
```

Det bekräftar att vi framgångsrikt **satte excel datumformat**, och att vi kunde **hämta datum‑tid‑cell** som ett korrekt `DateTime`.

## Läsa excel datum‑tid‑värden  

Nu när datumet är lagrat korrekt kanske du undrar hur du hämtar tillbaka det senare, kanske från en befintlig fil. Samma `GetDateTime()`‑metod fungerar på vilken cell som helst som redan har ett datumformat.

```csharp
// Assuming 'sheet' is already loaded from an existing workbook
DateTime existingDate = sheet.Cells["B5"].GetDateTime();
Console.WriteLine($"Cell B5 contains: {existingDate:d}");
```

Om cellen inte är formaterad som ett datum returnerar `GetDateTime()` `DateTime.MinValue`. Därför måste vi alltid **sätta excel datumformat** först.

## Extrahera datum från excel‑celler  

Ibland innehåller cellen en full tidsstämpel (datum + tid) men du behöver bara datumdelen. Du kan trunkera tidskomponenten genom att använda `.Date` på det returnerade `DateTime`.

```csharp
DateTime fullStamp = sheet.Cells["C3"].GetDateTime(); // e.g., 2023-07-15 14:30:00
DateTime onlyDate = fullStamp.Date;                  // 2023-07-15 00:00:00
Console.WriteLine($"Date only: {onlyDate:yyyy-MM-dd}");
```

Detta tillvägagångssätt fungerar oavsett det underliggande Excel‑nummerformatet, så länge cellen känns igen som ett datum.

## Beräkna arbetsboksformler  

Vad händer om datumet är resultatet av en formel, som `=TODAY()` eller `=DATE(2022,5,10)`? Aspose.Cells utvärderar formeln när du anropar `CalculateFormula()`. Efter det beter sig cellen exakt som ett manuellt inmatat datum.

```csharp
sheet.Cells["D2"].Formula = "=TODAY()";
workbook.CalculateFormula(); // Re‑evaluate the sheet
DateTime today = sheet.Cells["D2"].GetDateTime();
Console.WriteLine($"Today is: {today:yyyy-MM-dd}");
```

Observera att vi inte behövde ändra cellstilen; Excel behandlar redan formelresultat som datum när formeln returnerar ett serienummer som motsvarar ett datum.

## Hämta en datum‑tid‑cell från en befintlig arbetsbok  

När vi sätter ihop allt, här är en kompakt rutin som du kan slänga in i vilket projekt som helst för att öppna en Excel‑fil, säkerställa att alla datumceller tolkas korrekt, och returnera en lista med `DateTime`‑objekt.

```csharp
using System.Collections.Generic;
using Aspose.Cells;

static List<DateTime> ExtractAllDates(string filePath)
{
    Workbook wb = new Workbook(filePath);
    Worksheet ws = wb.Worksheets[0];
    wb.CalculateFormula(); // Make sure formulas are evaluated

    var dates = new List<DateTime>();
    foreach (Cell cell in ws.Cells)
    {
        // Check if the cell has a date number format (ID 14‑22 are common date formats)
        if (cell.GetStyle().Number >= 14 && cell.GetStyle().Number <= 22)
        {
            dates.Add(cell.GetDateTime());
        }
    }
    return dates;
}
```

Att köra `ExtractAllDates("Sample.xlsx")` ger dig varje datum som **sattes excel datumformat** korrekt i det första bladet.

## Vanliga fallgropar & hur du undviker dem  

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| `GetDateTime()` kastar `ArgumentException` | Cellen känns inte igen som ett datum (saknar nummerformat) | Applicera `Style.Number = 14` **innan** du anropar `CalculateFormula()` |
| Datum visas som `1900‑01‑00` | Excels serienummer 0 tolkas som epoken | Säkerställ att cellen faktiskt innehåller ett giltigt serienummer (>0) |
| Japanska erasträngar parsas inte | Aspose.Cells parsar bara erasträngar efter `CalculateFormula()` | Behåll den råa strängen, sätt ett datumformat, och anropa sedan `CalculateFormula()` |
| Tidszonsförskjutningar | `DateTime` lagras utan zoninformation, men din app kan visa i en annan lokal | Använd `DateTimeKind.Utc` eller konvertera explicit vid behov |

## Bild – Visuell sammanfattning  

![set excel date format example](excel-date-format.png "set excel date format example")

Diagrammet illustrerar flödet: **skriv sträng → applicera nummerformat → omberäkna → hämta DateTime**.

## Avslutning  

Vi har gått igenom allt du behöver för att **sätta excel datumformat**, **läsa excel datum‑tid**, **extrahera datum från excel**, **beräkna arbetsboksformler**, och slutligen **hämta datum‑tid‑celler** som inbyggda .NET‑objekt. Den kompletta, körbara koden är klar för kopiering och inklistring, och förklaringarna ger dig “varför” bakom varje steg, så att du kan anpassa mönstret till mer komplexa scenarier.

### Vad blir nästa steg?

- **Massimport/-export:** Använd `ExtractAllDates`‑hjälpen för att batch‑processa stora rapporter.  
- **Anpassade datumformat:** Byt ut `Style.Number = 14` mot `Style.Custom = "yyyy/mm/dd"` för lokaloberoende formatering.  
- **Tidszonsmedvetna datum:** Kombinera `DateTimeOffset` med Excels serienummer för globala applikationer.

Känn dig fri att experimentera, lägga till villkorlig formatering, eller föra in datumen i en databas. Om du stöter på problem, lämna en kommentar – lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}