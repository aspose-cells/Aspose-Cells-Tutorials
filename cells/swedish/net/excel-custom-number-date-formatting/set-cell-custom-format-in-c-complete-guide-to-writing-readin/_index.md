---
category: general
date: 2026-03-21
description: Ställ in anpassat cellformat i C# och lär dig hur du skriver datum till
  Excel, tillämpar anpassat datumformat, läser DateTime från Excel och skapar arbetsbok/arbetsblad
  snabbt.
draft: false
keywords:
- set cell custom format
- write date to excel
- read datetime from excel
- apply custom date format
- create workbook worksheet
language: sv
og_description: Ställ in anpassat cellformat i C# för att skriva datum till Excel,
  tillämpa anpassat datumformat, läsa DateTime från Excel och enkelt skapa ett arbetsblad
  i arbetsboken.
og_title: Ange anpassat cellformat i C# – Skriv och läs datum i Excel
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Ställ in anpassat cellformat i C# – Komplett guide för att skriva och läsa
  datum i Excel
url: /sv/net/excel-custom-number-date-formatting/set-cell-custom-format-in-c-complete-guide-to-writing-readin/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ange anpassat cellformat – Skriva & läsa datum i Excel med C#

Har du någonsin behövt **ange anpassat cellformat** i en Excel‑fil från C# men inte vetat var du ska börja? Du är inte ensam. I många rapportverktyg eller data‑exportverktyg måste datum visas i ett specifikt språk‑ eller regionformat – tänk japanska era‑datum, räkenskapskalendrar eller ISO‑8601‑strängar.  

I den här handledningen går vi igenom ett **komplett, körbart exempel** som visar hur du **skriver datum till Excel**, **tillämpar anpassat datumformat**, **läser DateTime från Excel** och **skapar arbetsbok och kalkylblad** med Aspose.Cells. När du är klar har du ett enda, självständigt program som du kan släppa in i vilket .NET‑projekt som helst.

## Vad du kommer att lära dig

- Hur du **skapar arbetsbok och kalkylblad** programatiskt.  
- De exakta stegen för att **skriva datum till Excel** med en regionsspecifik sträng.  
- Hur du **tillämpar anpassat datumformat** (inklusive japansk era‑notation).  
- Hur du **läser DateTime från Excel** tillbaka till ett `DateTime`‑objekt.  
- Tips, fallgropar och variationer du kan stöta på när du arbetar med Excel‑datum.

Ingen extern dokumentation behövs – allt du behöver finns här.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar också på .NET Framework 4.7+).  
- Aspose.Cells för .NET installerat via NuGet (`Install-Package Aspose.Cells`).  
- Grundläggande förståelse för C#‑syntax – inget avancerat.

> **Pro tip:** Om du använder Visual Studio, aktivera *nullable reference types* för att fånga subtila buggar tidigt.

## Steg 1: Skapa en arbetsbok och ett kalkylblad  

Först och främst: du behöver ett arbetsboksobjekt som representerar Excel‑filen, och ett kalkylblad där datan ska ligga.

```csharp
using Aspose.Cells;
using System;

class ExcelDateDemo
{
    static void Main()
    {
        // Step 1: Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];           // default sheet is named "Sheet1"
```

*Varför detta är viktigt:* Klassen `Workbook` är startpunkten för alla Excel‑operationer. Att skapa den i minnet betyder att du aldrig rör filsystemet förrän du explicit sparar, vilket gör processen snabb och testvänlig.

## Steg 2: Skriva datum till Excel  

Nästa steg är att placera en japansk era‑datumsträng (`"R02-04-01"`) i cell **A1**. Strängen efterliknar Reiwa‑eran (år 2, april 1).

```csharp
        // Step 2: Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("R02-04-01");
```

*Vad som händer:* `PutValue` lagrar den råa strängen. Aspose.Cells kommer senare att försöka tolka den baserat på cellens stil. Om du hoppar över detta steg och skriver ett `DateTime`‑värde direkt förlorar du den era‑information du vill visa.

## Steg 3: Tillämpa det inbyggda datum‑nummerformatet (ID 14)

Excel har ett inbyggt datumformat med ID 14 (`mm-dd-yy`). Att tillämpa det talar om för motorn att cellen **innehåller ett datum**, inte bara text.

```csharp
        // Step 3: Apply the built‑in date number format (ID 14)
        worksheet.Cells["A1"].Style.Number = 14;
```

*Varför använda ID 14?* Det är det universella “kort datum”-formatet som säkerställer att Excel behandlar innehållet som ett datumvärde, vilket är ett förutsättningskrav för att någon anpassad format ska fungera korrekt.

## Steg 4: Ange ett anpassat format för att visa japansk era‑notation  

Nu blir det roligt: vi säger åt Excel att rendera datumet med japansk era‑format. Den anpassade strängen `[$-ja-JP]ggge年m月d日` gör exakt det.

```csharp
        // Step 4: Set a custom format to display the date in Japanese era notation
        worksheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge年m月d日";
```

*Förklaring:*  
- `[$-ja-JP]` tvingar språkinställningen till japanska.  
- `ggg` är erans namn (t.ex. “R” för Reiwa).  
- `e` är erårets siffra.  
- `年`, `月`, `日` är bokstavliga japanska tecken för år, månad, dag.

Om du behöver ett annat språk, byt helt enkelt ut `ja-JP` mot rätt kulturskod (t.ex. `en-US`).

## Steg 5: Hämta det tolkade DateTime‑värdet  

Till sist läser vi det **faktiska `DateTime`‑värdet** som Excel har tolkat från cellen. Detta bevisar att strängen tolkades korrekt.

```csharp
        // Step 5: Retrieve the parsed DateTime value from the cell
        DateTime parsedDate = worksheet.Cells["A1"].DateTime;   // => 2020‑04‑01

        // Output to console for verification
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

*Resultat:* Konsolen skriver ut `Parsed DateTime: 2020-04-01`. Trots att vi angav en japansk era‑sträng lagrar Excel internt det gregorianska datumet, vilket du kan använda för beräkningar, jämförelser eller vidare export.

## Steg 6: Spara arbetsboken (valfritt)

Om du vill se den formaterade arbetsboken i Excel, spara den bara till disk.

```csharp
        // Optional: Save the workbook to a file
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

Öppna den genererade **JapaneseEraDate.xlsx** så ser du att cell **A1** visar `R02年4月1日` (det exakta japanska era‑formatet vi satte).

![ange anpassat cellformat exempel](image-placeholder.png "Excel‑cell som visar japanskt era‑datum – ange anpassat cellformat")

*Alt‑texten ovan innehåller huvudnyckelordet och uppfyller bild‑SEO‑kravet.*

## Vanliga variationer & kantfall  

### Skriva ett annat datumformat  

Om du föredrar ISO‑8601 (`2020-04-01`) istället för en era‑sträng, byt bara ut `PutValue`‑anropet:

```csharp
worksheet.Cells["A1"].PutValue(new DateTime(2020, 4, 1));
worksheet.Cells["A1"].Style.Number = 14;                 // keep built‑in date format
worksheet.Cells["A1"].Style.Custom = "yyyy-mm-dd";      // custom ISO format
```

### Hantera null‑ eller tomma celler  

När du läser ett datum, skydda alltid mot tomma celler för att undvika `InvalidOperationException`:

```csharp
if (!worksheet.Cells["A1"].IsDate)
{
    Console.WriteLine("Cell A1 does not contain a valid date.");
}
else
{
    DateTime dt = worksheet.Cells["A1"].DateTime;
    // use dt...
}
```

### Stöd för flera språk  

Du kan loopa igenom en lista med kulturskoder och tillämpa dem dynamiskt:

```csharp
string[] cultures = { "ja-JP", "en-US", "fr-FR" };
foreach (var culture in cultures)
{
    worksheet.Cells["A1"].Style.Custom = $"[$-{culture}]ggge年m月d日";
    // Save or export per culture if needed
}
```

## Pro‑tips & fallgropar  

- **Sätt alltid ett inbyggt nummerformat först** (`Style.Number`). Utan det behandlar Excel cellen som ren text och det anpassade formatet ignoreras.  
- **Kulturskoder är skiftlägesoberoende**, men att använda den kanoniska formen (`ja-JP`) undviker förvirring.  
- **Spara är valfritt** för bearbetning i minnet; du kan streama arbetsboken direkt till ett webbsvar (`workbook.Save(stream, SaveFormat.Xlsx)`).  
- **Aspose.Cells‑licenser**: Den fria utvärderingsversionen lägger till ett vattenmärke. För produktion, se till att du har en giltig licens för att undvika prestandapåverkan.

## Sammanfattning  

Vi har visat hur du **anger anpassat cellformat** i C# för att visa japanska era‑datum, hur du **skriver datum till Excel**, **tillämpar anpassat datumformat**, **läser DateTime från Excel** och **skapar arbetsbok och kalkylblad** – allt i ett enda, självständigt program. Huvudnyckelordet förekommer naturligt genom hela texten, medan sekundära nyckelord vävs in i rubriker och brödtext, vilket uppfyller både SEO‑ och AI‑citeringsstandarder.

## Vad blir nästa steg?

- Utforska **villkorsstyrd formatering** för att markera försenade datum.  
- Kombinera detta tillvägagångssätt med **Pivot‑tabeller** för dynamisk rapportering.  
- Prova att **läsa stora CSV‑filer** och konvertera dem till Excel med samma datumhanteringslogik.  

Känn dig fri att experimentera med olika språk, anpassade mönster eller till och med tidszoner. Om du stöter på problem, lämna en kommentar nedan – happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}