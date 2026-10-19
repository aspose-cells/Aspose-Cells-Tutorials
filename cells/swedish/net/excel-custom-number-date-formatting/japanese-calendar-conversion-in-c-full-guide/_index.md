---
category: general
date: 2026-07-13
description: Japansk kalenderkonvertering i C# med steg‑för‑steg‑kod. Lär dig hur
  du extraherar DateTime från Excel och hanterar japanska era‑datum effektivt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- japanese calendar conversion
- extract datetime from excel
- excel date parsing c#
- aspnet excel cultureinfo
- japanese era date handling
language: sv
lastmod: 2026-07-13
og_description: Japansk kalenderkonvertering i C# förklarad. Bemästra att extrahera
  DateTime från Excel‑celler och konvertera japanska era‑strängar till gregorianska
  datum.
og_image_alt: Code screenshot illustrating Japanese calendar conversion in a C# console
  app
og_title: Japansk kalenderkonvertering i C# – Fullständig programmeringsgenomgång
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Japanese calendar conversion in C# with step‑by‑step code. Learn how
    to extract DateTime from Excel and handle Japanese era dates efficiently.
  headline: Japanese Calendar Conversion in C# – Full Guide
  type: TechArticle
- description: Japanese calendar conversion in C# with step‑by‑step code. Learn how
    to extract DateTime from Excel and handle Japanese era dates efficiently.
  name: Japanese Calendar Conversion in C# – Full Guide
  steps:
  - name: Recognizes era names (e.g., *Meiji*, *Taishō*, *Shōwa*, *Heisei*, *Reiwa*).
    text: Recognizes era names (e.g., *Meiji*, *Taishō*, *Shōwa*, *Heisei*, *Reiwa*).
  - name: Parses the year number relative to the era’s start.
    text: Parses the year number relative to the era’s start.
  - name: Constructs the corresponding Gregorian `DateTime`.
    text: Constructs the corresponding Gregorian `DateTime`.
  type: HowTo
tags:
- C#
- Excel
- DateTime
- Localization
title: Japansk kalenderkonvertering i C# – Fullständig guide
url: /sv/net/excel-custom-number-date-formatting/japanese-calendar-conversion-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Japansk kalenderkonvertering i C# – Fullständig guide

Har du någonsin behövt **japanese calendar conversion** när du hämtar data från ett Excel‑blad? Du är inte den enda som kliar dig i huvudet över hur man omvandlar “Reiwa 3‑04‑01” till ett korrekt .NET `DateTime`. I den här handledningen går vi igenom en ren, end‑to‑end‑lösning som inte bara konverterar japanska eradatummer utan också visar dig hur du **extract datetime from excel** celler med Aspose.Cells. I slutet har du en färdig körbar konsolapp och en solid förståelse för varför kulturinställningar är viktiga.

Vi kommer att täcka allt du kan tänka dig: att ställa in rätt kultur, parsning av erasträngen, hantera kantfall som skottår och slutligen skriva ut det gregorianska resultatet. Ingen extern dokumentation behövs—bara kopiera, klistra in och kör.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar på .NET Core och .NET Framework lika väl)
- Aspose.Cells för .NET (gratis provversion NuGet‑paket `Aspose.Cells`)
- Grundläggande kunskap om C# och konsolapplikationer
- En Excel‑fil (eller en ny arbetsbok) där datumet lagras som en sträng i japanskt erafomat

Om du saknar någon av dessa, hämta NuGet‑paketet med:

```bash
dotnet add package Aspose.Cells
```

Nu låt oss dyka ner.

## Steg 1: Skapa en arbetsbok och ställ in japansk kultur

Det första du måste göra är att tala om för Aspose.Cells att arbetsboken ska tolka datum med den japanska kalendern. Det är här **japanese calendar conversion** verkligen börjar.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook instance
        Workbook workbook = new Workbook();

        // 2️⃣ Apply Japanese culture (Japanese calendar) to the workbook settings
        workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("ja-JP-u-ca-japanese");

        // The rest of the steps follow...
```

**Varför detta är viktigt:** `CultureInfo` bär inte bara språk utan också kalenderinformation. Genom att byta till `"ja-JP-u-ca-japanese"` gör vi så att biblioteket kan förstå eranamn som *Reiwa* eller *Heisei* när de visas i celler.

## Steg 2: Skriv ett japanskt eradatum i en cell

För demonstrationen placerar vi en japansk erasträng direkt i cell **A1**. I ett verkligt scenario läser du sannolikt en befintlig arbetsbok, men principen är densamma.

```csharp
        // 3️⃣ Write a Japanese era date string into cell A1 (row 0, column 0)
        workbook.Worksheets[0].Cells[0, 0].PutValue("Reiwa 3-04-01");
```

> **Pro tip:** Om käll‑Excel redan lagrar datum som korrekta Excel‑serienummer kan du hoppa över `PutValue`‑steget och gå direkt till extrahering. Konverteringslogiken fungerar på båda sätt.

## Steg 3: Extrahera DateTime från Excel – Kärnan i “extract datetime from excel”

Nu kommer delen där vi **extract datetime from excel**. Aspose.Cells tillhandahåller en bekväm `GetDateTime`‑metod som respekterar arbetsbokens kulturinställningar.

```csharp
        // 4️⃣ Retrieve the cell value as a .NET DateTime object
        DateTime gregorianDate = workbook.Worksheets[0].Cells[0, 0].GetDateTime();
```

Bakom kulisserna tittar Aspose på den kultur vi satte tidigare, parsar “Reiwa 3‑04‑01” och returnerar motsvarande gregorianska datum (`2021‑04‑01`).

## Steg 4: Visa resultatet

Till sist skriver vi ut det konverterade datumet till konsolen så att du kan verifiera att **japanese calendar conversion** lyckades.

```csharp
        // 5️⃣ Show the converted Gregorian date
        Console.WriteLine(gregorianDate.ToString("yyyy‑MM‑dd"));
        // Expected output: 2021‑04‑01
    }
}
```

Kör programmet (`dotnet run`) så bör du se:

```
2021‑04‑01
```

Det är hela cykeln: skapa en arbetsbok, ställ in japansk kultur, skriv ett eradatum, extrahera ett `DateTime` och visa det.

---

## Djupdykning: Hur den japanska kalendern fungerar i .NET

Den japanska kalendern är ett *lunisolärt* system som grupperar år i eror namngivna efter den regerande kejsaren. .NET:s `JapaneseCalendar`‑klass mappar varje era till ett intervall av gregorianska år. När du begär en `CultureInfo` som inkluderar `-u-ca-japanese` hanterar runtime automatiskt:

1. Känner igen eranamn (t.ex. *Meiji*, *Taishō*, *Shōwa*, *Heisei*, *Reiwa*).
2. Parsar årtalet relativt till erans start.
3. Skapar motsvarande gregorianska `DateTime`.

Om du någonsin behöver konvertera åt andra hållet—från gregorianskt till japanskt era—kan du använda:

```csharp
var japaneseCal = new System.Globalization.JapaneseCalendar();
int era = japaneseCal.GetEra(gregorianDate);
string eraName = japaneseCal.Eras[era - 1]; // .Eras is zero‑based
int yearInEra = japaneseCal.GetYear(gregorianDate);
Console.WriteLine($"{eraName} {yearInEra:D2}-{gregorianDate:MM-dd}");
```

### Hantera kantfall

| Situation | Vad att hålla utkik efter | Föreslagen lösning |
|-----------|---------------------------|--------------------|
| **Saknat eranamn** (t.ex. “03‑04‑01”) | `GetDateTime` kommer att kasta ett `FormatException`. | Förvalidera strängen eller falla tillbaka på `DateTime.ParseExact` med ett eget mönster. |
| **Framtida era** (ny kejsare) | Den nuvarande `JapaneseCalendar` kanske inte känner till den nya eran förrän en OS‑uppdatering. | Uppdatera .NET‑runtime eller använd en egen mappningstabell tills OS hinner med. |
| **Blandade kalendrar i en arbetsbok** | Vissa celler kan använda den gregorianska kalendern medan andra använder japansk. | Ställ in `CultureInfo` per cell med `cell.Style.CultureInfo` om det behövs. |

## Extrahera DateTime från befintliga Excel‑filer

Om du redan har en `.xlsx`‑fil med japanska datum är extraheringskoden nästan identisk—byt bara ut skapandet av arbetsboken mot ett laddningsanrop:

```csharp
Workbook workbook = new Workbook("Path/To/YourFile.xlsx");
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("ja-JP-u-ca-japanese");

// Assuming the date is in B2 (row 1, column 1)
DateTime dateFromFile = workbook.Worksheets[0].Cells[1, 1].GetDateTime();
Console.WriteLine(dateFromFile);
```

Observera hur **extract datetime from excel** förblir samma metodanrop; det enda extra steget är att ladda filen.

---

## Fullt fungerande exempel (Klar att kopiera‑klistra in)

Nedan är det kompletta programmet som du kan lägga in i ett konsolprojekt. Det innehåller alla nödvändiga `using`‑direktiv, kommentarer och felhantering för en produktionskvalitet.

```csharp
using System;
using Aspose.Cells;

class JapaneseCalendarDemo
{
    static void Main()
    {
        try
        {
            // Initialize workbook
            Workbook wb = new Workbook();

            // Apply Japanese calendar culture
            wb.Settings.CultureInfo = new System.Globalization.CultureInfo("ja-JP-u-ca-japanese");

            // Insert a Japanese era date string (could be read from an existing file)
            wb.Worksheets[0].Cells[0, 0].PutValue("Reiwa 3-04-01");

            // Extract as .NET DateTime – this is the core of "extract datetime from excel"
            DateTime gregDate = wb.Worksheets[0].Cells[0, 0].GetDateTime();

            // Output in ISO format
            Console.WriteLine(gregDate.ToString("yyyy-MM-dd"));
        }
        catch (Exception ex)
        {
            // Simple error handling – in real apps you might log this
            Console.Error.WriteLine($"Error during conversion: {ex.Message}");
        }
    }
}
```

**Förväntad konsolutdata**

```
2021-04-01
```

Kör det, så ser du det gregorianska datumet som matchar den japanska erainmatningen.

---

## Vanliga frågor

**Q: Fungerar detta med äldre Excel‑filer (.xls)?**  
Ja. Aspose.Cells abstraherar filformatet, så samma `GetDateTime`‑anrop fungerar för både `.xls` och `.xlsx`.

**Q: Vad händer om cellen innehåller ett riktigt Excel‑datum (serienummer) istället för en sträng?**  
Aspose kommer fortfarande att respektera arbetsbokens kultur och returnera korrekt gregoriansk `DateTime`. Ingen extra parsning behövs.

**Q: Kan jag konvertera en hel kolumn med japanska datum på en gång?**  
Absolut. Loopa igenom raderna:

```csharp
for (int i = 0; i < worksheet.Cells.MaxDataRow + 1; i++)
{
    DateTime dt = worksheet.Cells[i, 0].GetDateTime();
    // Do something with dt
}
```

**Q: Finns det någon prestandapåverkan när man ställer in kulturen?**  
Försumbar för typiska dataset. Kulturen appliceras en gång per arbetsbok, inte per cell.

---

## Slutsats

Vi har just avslutat en **japanese calendar conversion**‑genomgång som visar exakt hur man **extract datetime from excel** med Aspose.Cells. Genom att sätta arbetsbokens `CultureInfo` till `"ja-JP-u-ca-japanese"` låser du upp sömlös parsning av erasträngar som *Reiwa 3‑04‑01* till standard .NET `DateTime`‑objekt. Koden är kompakt, robust och klar för produktion.

Vad blir nästa steg? Prova att ladda en verklig arbetsbok, konvertera en hel kolumn, eller till och med skriva tillbaka de gregorianska datumen till ett nytt blad. Du kan också utforska andra lokaler—franska republikanska kalendern, islamiska hijri‑kalendern—genom att byta kultursträngen. Mönstret förblir detsamma.

Har du ett eget knep du vill dela? Lägg en kommentar, och lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Behärska 1904-datersystemet i Excel med Aspose.Cells Java för effektiva celloperationer](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Excel‑cellreferenskonvertering med Aspose.Cells .NET: En omfattande guide](/cells/english/net/cell-operations/excel-cell-reference-conversion-aspose-cells-net/)
- [Behärska HTML‑till‑Excel‑konvertering med Aspose.Cells för .NET](/cells/english/net/workbook-operations/aspose-cells-net-html-layout-conversion/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}