---
category: general
date: 2026-02-15
description: Hur man skapar en arbetsbok, konverterar en sträng till datum och formaterar
  en cell som datum med Aspose.Cells. Lär dig att ställa in cellens talformat och
  enkelt läsa Excel‑datum.
draft: false
keywords:
- how to create workbook
- convert string to date
- format cell as date
- set cell number format
- read excel date
language: sv
og_description: Hur man skapar en arbetsbok, konverterar en sträng till datum och
  formaterar cellen som ett datum. Komplett steg‑för‑steg‑guide för att läsa Excel‑datum.
og_title: Hur man skapar en arbetsbok och konverterar en sträng till datum i C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Hur man skapar en arbetsbok och konverterar sträng till datum i C#
url: /sv/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar en arbetsbok och konverterar sträng till datum i C#

Har du någonsin undrat **hur man skapar en arbetsbok** som omvandlar en vanlig text som `"R3-04-01"` till ett riktigt `DateTime`‑värde? Du är inte ensam—många utvecklare stöter på detta problem när de hämtar data från äldre system eller användarinmatning. Den goda nyheten? Med några rader C# och Aspose.Cells kan du göra det på ett ögonblick, utan manuell parsning.

I den här handledningen går vi igenom hela processen: skapa en arbetsbok, infoga en datumsträng, tillämpa en korrekt **format cell as date**, tvinga motorn att **set cell number format**, och slutligen **read excel date** tillbaka som ett `DateTime`. I slutet har du ett körbart kodexempel som du kan lägga in i vilket .NET‑projekt som helst.

## Förutsättningar

- .NET 6+ (eller .NET Framework 4.7.2+)
- **Aspose.Cells for .NET** NuGet‑paket (`Install-Package Aspose.Cells`)
- En grundläggande förståelse för C#‑syntax
- En IDE som Visual Studio eller VS Code (vilken som helst fungerar)

Ingen extra konfiguration behövs—Aspose.Cells hanterar allt tungt arbete internt.

## Steg 1: Hur man skapar en arbetsbok – initiera Excel‑filen

Först behöver vi ett nytt arbetsboksobjekt. Tänk på det som en tom anteckningsbok där varje arbetsblad är en sida.

```csharp
using Aspose.Cells;

 // Step 1: Create a new workbook
 var workbook = new Workbook();          // Empty workbook with one default sheet
```

*Varför detta är viktigt:* Att skapa arbetsboken ger oss en behållare för celler, stilar och formler. Utan den finns det ingenstans att placera datumsträngen.

## Steg 2: Konvertera sträng till datum – infoga den råa texten

Nu placerar vi den råa datumsträngen i cell **A1** på det första arbetsbladet. Strängen använder ett anpassat format (`R3-04-01`) som Excel inte känner igen direkt.

```csharp
 // Step 2: Insert a date string into cell A1 of the first worksheet
 var targetCell = workbook.Worksheets[0].Cells["A1"];
 targetCell.PutValue("R3-04-01");        // Raw text, not yet a date
```

*Varför vi gör detta:* `PutValue` lagrar den bokstavliga texten. Om vi försökte sätta ett `DateTime` direkt, skulle det anpassade formatet gå förlorat. Genom att behålla det som text kan vi senare tillämpa ett **set cell number format** som talar om för Excel hur det ska tolkas.

## Steg 3: Formatera cell som datum – tillämpa stil nummer 14

Excels inbyggda datumstil 14 motsvarar `mm-dd-yy`. Genom att tilldela denna stil säger vi till motorn: ”Behandla innehållet i den här cellen som ett datum.”

```csharp
 // Step 3: Apply a date number format (style number 14) to the cell
 targetCell.SetStyle(new Style { Number = 14 });
```

*Vad som händer under huven:* `Number`‑egenskapen mappar till Excels interna nummer‑format‑ID:n. När arbetsboken omräknas kommer Excel att försöka omvandla texten till ett serienummer för datum med det angivna formatet.

## Steg 4: Ställ in cellens nummerformat – tvinga omräkning

Excel konverterar inte magiskt texten förrän vi ber den utvärdera formler (eller i detta fall omtolka cellen). Att anropa `CalculateFormula` utlöser den konverteringen.

```csharp
 // Step 4: Recalculate any formulas so the cell value is interpreted as a date
 workbook.CalculateFormula();
```

*Tips:* Om du arbetar med många celler kan du anropa `CalculateFormula` en gång efter att du har avslutat all formatering—det sparar några millisekunder.

## Steg 5: Läs Excel‑datum – hämta DateTime‑värdet

Slutligen hämtar vi `DateTime`‑representationen från cellen. Aspose.Cells exponerar den via `DateTimeValue`.

```csharp
 // Step 5: Retrieve the DateTime representation and display it
 Console.WriteLine(targetCell.DateTimeValue);
```

**Förväntat utdata (förutsatt standard Gregorianska kalendern):**

```
2023-04-01 00:00:00
```

Observera hur prefixet `"R3-"` ignoreras eftersom Excels datumparser fokuserar på den numeriska delen när stilen är ett datum. Om dina strängar innehåller andra prefix kan du behöva förbehandla dem, men för många äldre format fungerar detta tillvägagångssätt perfekt.

## Fullständigt fungerande exempel

När vi sätter ihop allt, här är det kompletta, körklara programmet:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook
        var workbook = new Workbook();

        // Step 2: Insert a date string into cell A1 of the first worksheet
        var targetCell = workbook.Worksheets[0].Cells["A1"];
        targetCell.PutValue("R3-04-01");

        // Step 3: Apply a date number format (style number 14) to the cell
        targetCell.SetStyle(new Style { Number = 14 });

        // Step 4: Recalculate any formulas so the cell value is interpreted as a date
        workbook.CalculateFormula();

        // Step 5: Retrieve the DateTime representation and display it
        Console.WriteLine(targetCell.DateTimeValue);
    }
}
```

Spara detta som `Program.cs`, återställ Aspose.Cells‑paketet och kör `dotnet run`. Du bör se det formaterade `DateTime`‑värdet skrivet till konsolen.

## Vanliga variationer & kantfall

### Olika datumsträngar

Om dina källdata ser ut som `"2023/04/01"` eller `"01‑Apr‑2023"` kan du fortfarande använda samma arbetsflöde—byt bara **Number**‑egenskapen till ett format som matchar mönstret (t.ex. `Number = 15` för `d-mmm-yy`).  

### Lokalspecifika format

Excel respekterar arbetsbokens lokala inställningar. För att tvinga US‑stil parsning, sätt arbetsbokens kultur:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");
```

### När strängen inte känns igen

Ibland kan Excel inte härleda ett datum (t.ex. `"R3-13-40"`). I sådana fall, förbehandla strängen:

```csharp
string raw = "R3-04-01";
string cleaned = raw.Replace("R3-", "");   // Remove the prefix
targetCell.PutValue(cleaned);
```

Applicera sedan samma nummerformat.

## Pro‑tips & fallgropar

- **Pro‑tips:** Använd `StyleFlag` för att bara ändra nummerformatet, och lämna andra stilattribut orörda.  
  ```csharp
  var style = targetCell.GetStyle();
  style.Number = 14;
  var flag = new StyleFlag { Number = true };
  targetCell.SetStyle(style, flag);
  ```
- **Se upp för:** Att skriva över befintliga stilar på en cell som redan har kanter eller teckensnitt. `StyleFlag`‑metoden förhindrar detta.
- **Prestanda‑notering:** Om du bearbetar tusentals rader, batcha `CalculateFormula`‑anropet efter att du har avslutat alla uppdateringar; att anropa det per rad ger onödig overhead.

## Slutsats

Du vet nu **hur man skapar en arbetsbok**, **konverterar sträng till datum**, **formaterar cell som datum**, **ställer in cellens nummerformat**, och slutligen **läser excel‑datum** tillbaka till ett `DateTime`. Mönstret är enkelt: infoga råtext, tillämpa ett datumformat, tvinga omräkning, och sedan läsa värdet.

Härifrån kan du utöka logiken till hela kolumner, importera CSV‑data, eller till och med generera rapporter som automatiskt översätter äldre datumsträngar till korrekta Excel‑datum.

Redo att ta nästa steg? Prova att tillämpa ett anpassat nummerformat (`Number = 22`) för att visa datum som `yyyy-mm-dd`, eller utforska Aspose.Cells `DateTimeConversion`‑verktyg för mer komplexa scenarier.

Lycka till med kodandet! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}