---
category: general
date: 2026-05-30
description: Aktivera tolkning av japanska era i C# med Aspose.Cells. Lär dig att
  ställa in arbetsbokens kultur, tolka era‑datum och hantera den japanska kalendern
  i Excel‑ark.
draft: false
keywords:
- enable japanese era parsing
- Aspose.Cells Japanese era
- set workbook culture
- parse era dates
- c# excel date parsing
language: sv
og_description: Aktivera tolkning av japanska era i C# med Aspose.Cells. Denna guide
  visar hur du ställer in arbetsbokens kultur, aktiverar stöd för era och arbetar
  med japanska datum.
og_title: Aktivera japansk era‑parsing i C# – Komplett guide
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Enable Japanese era parsing in C# using Aspose.Cells. Learn to set
    workbook culture, parse era dates, and handle Japanese calendar in Excel worksheets.
  headline: Enable Japanese Era Parsing in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Aktivera parsning av japansk era i C# med Aspose.Cells
url: /sv/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aktivera japansk era‑parsing i C# med Aspose.Cells

Har du någonsin behövt **enable japanese era parsing** när du genererar Excel‑filer för en japansk kund? Du är inte ensam—många utvecklare stöter på problem när den äldre japanska kalendern (令和, 平成, osv.) dyker upp i data. Den goda nyheten är att Aspose.Cells gör det enkelt att känna igen dessa era‑datum och omvandla dem till vanliga gregorianska värden.

I den här handledningen går vi igenom de exakta stegen för att **enable japanese era parsing** med Aspose.Cells, sätta arbetsbokens kultur till japanska och infoga ett era‑formaterat datum i en cell. I slutet har du ett körbart C#‑exempel som parsar “令和3年5月1日” till det korrekta `2021‑05‑01` datumobjektet. Ingen extern dokumentation behövs—bara kopiera, klistra in och kör.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar med .NET Core, .NET Framework och .NET 5+)
- Aspose.Cells för .NET (NuGet‑paketet `Aspose.Cells`)
- Grundläggande C#‑kunskaper—om du kan skriva en `Console.WriteLine` är du klar
- En IDE efter eget val (Visual Studio, VS Code, Rider…)

> **Pro tip:** Håll din Aspose.Cells‑version uppdaterad; version 24.10+ innehåller de senaste definitionerna för japanska eraer.

## Varför aktivera japansk era‑parsing?

Japanska kalendrar använder era som är knutna till kejsarens regeringstid. För de flesta moderna applikationer vill du lagra datum i det välbekanta gregorianska formatet, men källdata kan fortfarande komma som “令和3年5月1日”. Om du hoppar över **enable japanese era parsing** kommer strängen att behandlas som vanlig text, vilket bryter beräkningar, sortering och diagram. Genom att slå på era‑stöd konverterar Aspose.Cells automatiskt dessa strängar till korrekta `DateTime`‑värden, vilket bevarar både läsbarhet för japanska användare och numerisk korrekthet för efterföljande bearbetning.

## Steg 1: Ställ in arbetsbokens kultur till japanska

Det första du måste göra är att tala om för Aspose.Cells att arbetsbokens standard‑locale är japanska (`ja-JP`). Detta säkerställer att all kultur‑specifik parsning (inklusive era‑namn) följer japanska regler.

```csharp
using Aspose.Cells;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Set the workbook culture to Japanese (ja-JP)
        workbook.Settings.Culture = new CultureInfo("ja-JP");
```

> **Why this matters:** `CultureInfo`‑objektet styr talformat, datumseparatorer och, viktigast för oss, kalendersystemet som används när strängar parsas.

## Steg 2: Aktivera japansk era‑parsing

Nu när kulturen är inställd måste du slå på flaggan som talar om för Aspose.Cells att känna igen era‑datum. Detta är kärnan i **enable japanese era parsing**.

```csharp
        // Enable parsing of Japanese era dates (令和, 平成, 昭和, etc.)
        workbook.Settings.UseJapaneseEra = true;
```

> **Common pitfall:** Att glömma denna flagga betyder att “令和3年5月1日” förblir en bokstavlig sträng. När den är på mappar Aspose.Cells automatiskt era‑namnet till rätt gregorianskt år.

## Steg 3: Infoga ett era‑formaterat datum i en cell

Med kulturen och era‑stödet på plats är det enkelt att infoga en japansk era‑sträng. Biblioteket kommer att parsra den och lagra ett riktigt `DateTime`‑värde.

```csharp
        // Grab the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Insert a Japanese era date string into cell A1
        // The string "令和3年5月1日" becomes 2021‑05‑01 internally
        sheet.Cells["A1"].PutValue("令和3年5月1日");

        // Save the workbook to verify the result
        workbook.Save("JapaneseEraDemo.xlsx");
    }
}
```

### Förväntat resultat

- **Cell A1** i den genererade `JapaneseEraDemo.xlsx` kommer att visa **2021‑05‑01** (eller det lokalanpassade japanska datumformatet om du öppnar den i Excel med japansk locale).
- Det underliggande värdet är ett riktigt `DateTime`, så du kan säkert använda det i formler, pivottabeller eller vidare C#‑beräkningar.

## Steg 4: Verifiera det parsade datumet programatiskt (valfritt)

Om du vill dubbelkolla att parsningen lyckades innan du sparar kan du läsa tillbaka cellen:

```csharp
        // Retrieve the value as a DateTime
        DateTime parsedDate = sheet.Cells["A1"].GetDateTime();

        Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
        // Output: Parsed date: 2021-05-01
```

Detta lilla verifieringssteg är praktiskt i enhetstester eller när du bearbetar användargenererade Excel‑filer.

## Kantfall & variationer

| Scenario | Vad du ska göra |
|----------|-------------------|
| **Multiple eras in one workbook** | Behåll `UseJapaneseEra = true`; Aspose.Cells kommer att känna igen alla stödda eraer (令和, 平成, 昭和, 大正, 明治). |
| **Mixed Gregorian and era strings** | Parsern skiljer automatiskt åt; gregorianska strängar förblir oförändrade. |
| **Custom calendar requirements** | Du kan fortfarande sätta `Workbook.Settings.Calendar` till en specifik `Calendar`‑instans om du behöver mer kontroll. |
| **Older .NET versions** | Samma kod fungerar på .NET Framework 4.6+; se bara till att `System.Globalization.CultureInfo`‑konstruktorn är tillgänglig. |

## Praktiska tips för verkliga projekt

- **Cache the CultureInfo** om du skapar många arbetsböcker i en loop; att konstruera den upprepade gånger ger extra overhead.
- **Validate input** innan du anropar `PutValue`; felaktiga era‑strängar kommer att kasta ett undantag.
- **Turn off era parsing** (`UseJapaneseEra = false`) när du är säker på att data aldrig innehåller era‑datum—detta kan förbättra prestandan något.
- **Use `Workbook.SaveOptions`** för att styra utdataformatet (XLSX, XLS, CSV) samtidigt som det parsade datumet bevaras.

## Fullt fungerande exempel (klar att kopiera‑klistra in)

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class EnableJapaneseEraParsingDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Set workbook culture to Japanese (ja-JP)
        workbook.Settings.Culture = new CultureInfo("ja-JP");

        // 3️⃣ Enable Japanese era parsing
        workbook.Settings.UseJapaneseEra = true;

        // 4️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 5️⃣ Insert an era‑formatted date
        sheet.Cells["A1"].PutValue("令和3年5月1日");

        // Optional: read back the parsed value
        DateTime dt = sheet.Cells["A1"].GetDateTime();
        Console.WriteLine($"Parsed date: {dt:yyyy-MM-dd}");

        // Save the workbook
        workbook.Save("EnableJapaneseEraParsing.xlsx");
    }
}
```

Kör programmet, öppna den genererade filen, och du kommer att se **2021‑05‑01** i cell A1—bevis på att vi framgångsrikt **enable japanese era parsing**.

## Slutsats

Vi har just demonstrerat hur man **enable japanese era parsing** i C# med Aspose.Cells, sätter arbetsbokens kultur och sömlöst konverterar era‑datum som “令和3年5月1日” till standard gregorianska värden. Stegen är få, koden är självständig och resultatet fungerar felfritt i Excel.

Redo för nästa utmaning? Prova att kombinera **set workbook culture** med talformat för japanska yen, eller generera en flik‑rapport som blandar gregorianska och era‑datum. Du har nu grunden för att hantera alla japanska kalendrar quirks i dina .NET Excel‑automatiseringsprojekt.

---

*Om den här guiden hjälpte dig, överväg att ge ett stjärnmärke till Aspose.Cells GitHub‑repo eller dela dina egna tips i kommentarerna. Lycka till med kodningen!*

## Vad bör du lära dig härnäst?

- [Ladda Excel‑arbetsböcker med kultur‑specifika datum med Aspose.Cells för .NET](/cells/english/net/formatting/load-workbook-culture-specific-dates-aspose-cells-net/)
- [Hur man ställer in språk i Excel‑filer med Aspose.Cells .NET för flerspråkigt stöd](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [Ladda arbetsbok med kultur‑specifika datum Aspose Cells Net](/cells/chinese/net/formatting/load-workbook-culture-specific-dates-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}