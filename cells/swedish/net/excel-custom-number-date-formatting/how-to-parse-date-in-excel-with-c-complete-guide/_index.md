---
category: general
date: 2026-05-23
description: Hur man parsar datum från en Excel-cell med C#. Lär dig anpassade talformat,
  Excel-trick, läs datum från cellen och tillämpa anpassat format för korrekta resultat.
draft: false
keywords:
- how to parse date
- custom number format excel
- read date from cell
- format excel cell date
- apply custom format
language: sv
og_description: Hur man parsar datum från en Excel-cell med C#. Denna handledning
  visar hur man tillämpar anpassat talformat i Excel, läser datum från en cell och
  formaterar datum i en Excel-cell korrekt.
og_title: Hur man parsar datum i Excel med C# – Komplett guide
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to parse date from an Excel cell using C#. Learn custom number
    format Excel tricks, read date from cell, and apply custom format for accurate
    results.
  headline: How to Parse Date in Excel with C# – Complete Guide
  type: TechArticle
- description: How to parse date from an Excel cell using C#. Learn custom number
    format Excel tricks, read date from cell, and apply custom format for accurate
    results.
  name: How to Parse Date in Excel with C# – Complete Guide
  steps:
  - name: Why a Custom Format Works
    text: Excel stores dates as serial numbers internally. By applying a locale‑aware
      format, Excel attempts to *interpret* the underlying text according to the pattern.
      The `[$-ja-JP]` prefix forces the Japanese calendar rules, while the rest of
      the pattern maps the characters to year, month, and day.
  - name: 1. Parsing European Dates (e.g., “12/05/2021” in French)
    text: '```csharp firstCell.PutValue("12/05/2021"); // day/month/year Style frStyle
      = workbook.CreateStyle(); frStyle.Custom = "[$-fr-FR]dd/mm/yyyy"; firstCell.SetStyle(frStyle);
      DateTime frDate = firstCell.DateTimeValue; // 2021-05-12 ```'
  - name: 2. When the Cell Already Contains a Serial Date
    text: 'If the source Excel file already stores a true date value, you can skip
      the custom format entirely:'
  - name: 3. Fallback to Manual Parsing
    text: 'Sometimes data is messy (extra spaces, hidden characters). A safe fallback
      is:'
  type: HowTo
tags:
- Excel
- C#
- Date Parsing
title: Hur du parsar datum i Excel med C# – Komplett guide
url: /sv/net/excel-custom-number-date-formatting/how-to-parse-date-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man parsar datum i Excel med C# – Komplett guide

Har du någonsin undrat **hur man parsar datum** som lagras i ett Excel‑blad utan att manuellt trixa med strängkonverteringar? Du är inte ensam. Oavsett om du hämtar japanska räkenskapsdatum, europeiska månad‑dag‑kombinationer eller någon annan lokalanpassad sträng, kan det kännas som att jaga ett rörligt mål att få ett pålitligt `DateTime` i C#.

I den här handledningen går vi igenom ett konkret, end‑to‑end‑exempel som **tillämpa ett anpassat talformat i Excel** på en textcell, och sedan **läser datum från cellen** som ett korrekt `DateTime`. I slutet kommer du att veta exakt hur man **formaterar Excel‑cellens datum**, **tillämpa anpassat format**, och undviker de vanliga fallgroparna som får de flesta utvecklare att snubbla.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar med .NET Core, .NET Framework och .NET 5+)
- En referens till ett kalkylbladsbibliotek som stödjer stilmanipulation – exemplet använder **Aspose.Cells**, men koncepten kan överföras till EPPlus, ClosedXML eller NPOI.
- Grundläggande kunskaper i C# (du har det, eller hur?)

> **Proffstips:** Om du ännu inte har Aspose.Cells kan du hämta en gratis provversion från deras webbplats och lägga till den via NuGet: `dotnet add package Aspose.Cells`.

## Översikt av lösningen

1. **Skapa en arbetsbok** och rikta in dig på det första kalkylbladets första cell.  
2. **Infoga en lokalanpassad datumsträng** (japansk i vårt fall).  
3. **Tillämpa ett anpassat talformat** som får Excel att behandla strängen som ett datum.  
4. **Läs av cellvärdet** tillbaka som ett `DateTime`‑objekt.  

Det är hela flödet – ingen manuell parsning, ingen `DateTime.ParseExact`‑gymnastik. Låt oss dyka ner.

---

## Steg 1: Ställ in arbetsboken och målcell

Först skapar du en ny arbetsbok och hämtar cellen vi ska arbeta med. Detta speglar scenariot “ny arbetsbok” som de flesta batch‑processjobb startar från.

```csharp
using Aspose.Cells;

// Create a new workbook
Workbook workbook = new Workbook();

// Get the first worksheet's first cell (A1)
Cell firstCell = workbook.Worksheets[0].Cells[0, 0];
```

> **Varför detta är viktigt:** Att initiera arbetsboken programatiskt säkerställer att vi kontrollerar varje aspekt av filen – inga dolda formateringsöverraskningar. `Cell`‑objektet är vår ingångspunkt för både innehåll och stil.

---

## Steg 2: Infoga en japansk datumsträng

Excel får ofta datum som ren text, särskilt när data kommer från äldre system. Här simulerar vi det genom att lägga in ett japanskt era‑datum direkt i cellen.

```csharp
// Insert a Japanese date string (令和3年5月12日 = May 12, 2021)
firstCell.PutValue("令和3年5月12日");
```

> **Obs på kantfall:** Om cellen redan innehöll ett riktigt Excel‑datum (ett serienummer) kan du hoppa över steget med anpassat format. Denna guide fokuserar på *text‑till‑datum*-konverteringsvägen.

## Steg 3: Tillämpa ett anpassat talformat som tolkar texten som ett datum

Nu kommer magin: vi instruerar Excel att behandla strängen med ett **anpassat talformat i Excel**‑mönster som respekterar den japanska lokalen. Formatsträngen `[$-ja-JP]yyyy` extraherar årkomponenten, men du kan utöka den till månad och dag vid behov.

```csharp
// Define a style with a custom number format for Japanese locale
Style style = workbook.CreateStyle();
style.Custom = "[$-ja-JP]yyyy\"年\"m\"月\"d\"日\"";

// Apply the style to the cell
firstCell.SetStyle(style);
```

### Varför ett anpassat format fungerar

Excel lagrar datum internt som serienummer. Genom att tillämpa ett lokalanpassat format försöker Excel *tolka* den underliggande texten enligt mönstret. Prefixet `[$-ja-JP]` tvingar de japanska kalenderreglerna, medan resten av mönstret mappar tecknen till år, månad och dag.

> **Alternativ:** Om du behöver en mer generell metod kan du använda `[$-en-US]mm/dd/yyyy` för amerikanska datumformat, eller någon annan kulturkod som stöds av Windows.

## Steg 4: Hämta det parsade datumet som ett `DateTime`‑objekt

Slutligen ber vi cellen om dess `DateTimeValue`. Aspose.Cells konverterar automatiskt den formaterade texten till en korrekt `DateTime`‑instans.

```csharp
// Retrieve the cell value as a DateTime
DateTime parsedDate = firstCell.DateTimeValue;

// Output to console for verification
Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
```

**Förväntad konsolutskrift**

```
Parsed date: 2021-05-12
```

> **Vad händer om den returnerar `DateTime.MinValue`?** Det betyder vanligtvis att formatet inte matchade cellens innehåll. Dubbelkolla den anpassade formatsträngen och säkerställ att kulturkoden matchar källspråket.

## Bonus: Hantera andra lokaler och variationer i verkligheten

### 1. Parsning av europeiska datum (t.ex. “12/05/2021” på franska)

```csharp
firstCell.PutValue("12/05/2021"); // day/month/year
Style frStyle = workbook.CreateStyle();
frStyle.Custom = "[$-fr-FR]dd/mm/yyyy";
firstCell.SetStyle(frStyle);
DateTime frDate = firstCell.DateTimeValue; // 2021-05-12
```

### 2. När cellen redan innehåller ett serienummer‑datum

Om käll‑Excel‑filen redan lagrar ett riktigt datumvärde kan du hoppa över det anpassade formatet helt:

```csharp
DateTime existingDate = firstCell.DateTimeValue; // works out‑of‑the‑box
```

### 3. Fallback till manuell parsning

Ibland är data rörigt (extra mellanslag, dolda tecken). Ett säkert fallback‑alternativ är:

```csharp
string raw = firstCell.StringValue?.Trim();
if (DateTime.TryParseExact(raw, "yyyy/MM/dd", CultureInfo.InvariantCulture,
                           DateTimeStyles.None, out DateTime fallback))
{
    // use fallback
}
```

Men **tillämpa anpassat format**‑metoden är vanligtvis snabbare och mindre felbenägen eftersom den utnyttjar Excels egen parsning‑motor.

## Vanliga fallgropar och hur man undviker dem

| Fallgropar | Symptom | Åtgärd |
|------------|---------|--------|
| Fel kulturkod (`[$-ja-JP]` vs `[$-ja]`) | `DateTimeValue` förblir `1/1/1900` | Verifiera den exakta LCID‑strängen; använd `CultureInfo.GetCultureInfo("ja-JP").LCID` för att vara säker. |
| Saknade citattecken runt statisk text | Excel behandlar `"年"` som en format‑platshållare och misslyckas | Omge statiska tecken med dubbla citattecken, t.ex. `\"年\"`. |
| Cellen redan formaterad som *Text* | Anpassat format ignoreras | Rensa cellens `NumberFormat` först: `firstCell.SetStyle(workbook.CreateStyle());` |
| Använder ett bibliotek som inte stödjer `Custom`‑egenskapen | Kompileringsfel | Byt till ett bibliotek som exponerar anpassade talformat (Aspose.Cells, EPPlus, ClosedXML). |

## Fullständigt fungerande exempel (Klar att kopiera‑klistra in)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get target cell
        Workbook workbook = new Workbook();
        Cell firstCell = workbook.Worksheets[0].Cells[0, 0];

        // 2️⃣ Insert Japanese date string
        firstCell.PutValue("令和3年5月12日");

        // 3️⃣ Apply custom number format for Japanese locale
        Style style = workbook.CreateStyle();
        style.Custom = "[$-ja-JP]yyyy\"年\"m\"月\"d\"日\"";
        firstCell.SetStyle(style);

        // 4️⃣ Retrieve parsed DateTime
        DateTime parsedDate = firstCell.DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
        // Expected: Parsed date: 2021-05-12

        // Optional: Save the workbook to see the formatted cell in Excel
        workbook.Save("ParsedDateExample.xlsx");
    }
}
```

Kör programmet, öppna `ParsedDateExample.xlsx`, och du kommer att se cell **A1** som visar `2021年5月12日` medan det underliggande värdet är ett korrekt Excel‑datum.

## Slutsats

Vi har gått igenom **hur man parsar datum**‑strängar i Excel med C# genom att **tillämpa ett anpassat talformat i Excel** och sedan **läsa datum från cell** som ett inbyggt `DateTime`. De viktigaste slutsatserna:

- Använd ett lokalanpassat anpassat format (`[$-ja-JP]…`) för att låta Excel göra det tunga arbetet.  
- Åtkomst till `Cell.DateTimeValue` för att få ett rent `DateTime` utan manuell parsning.  
- Justera formatsträngen för andra kulturer, och verifiera alltid med en snabb konsolutskrift.  

Härifrån kan du **formatera Excel‑cellens datum** för rapporter, föra in `DateTime` i databaser, eller utföra beräkningar direkt i din C#‑app. Experimentera med olika lokaler, kombinera flera celler, eller till och med batch‑processa hela blad – samma principer gäller.

Har du ett knasigt datumformat du inte kan knäcka? Lämna en kommentar så felsöker vi tillsammans. Lycka till med kodandet!

## Relaterade handledningar

- [Excel Custom Number and Date Formatting](/cells/english/net/excel-custom-number-date-formatting/)
- [Mastering Data Presentation in Excel: Number and Custom Date Formatting with Aspose.Cells for Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Excel Custom Number Date Formatting](/cells/german/net/excel-custom-number-date-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}