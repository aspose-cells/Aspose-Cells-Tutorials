---
category: general
date: 2026-10-10
description: Skapa en Excel-arbetsbok i C# och sätt cellvärdet till ett datum i japansk
  era, applicera sedan ett anpassat format och läs datumcellen med Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set cell value
- apply custom format
- read date cell
- excel date parsing
language: sv
lastmod: 2026-10-10
og_description: Skapa en Excel‑arbetsbok i C# och tolka japanska era‑datum. Lär dig
  att ange cellvärde, tillämpa anpassat format och läsa datumceller med Aspose.Cells.
og_image_alt: Screenshot showing a C# program that creates an Excel workbook and parses
  a Japanese era date
og_title: Skapa Excel-arbetsbok i C# – fullständig guide till datumparsning
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and set cell value with a Japanese era
    date, then apply custom format and read date cell using Aspose.Cells.
  headline: How to create Excel workbook and parse Japanese dates in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: Hur man skapar en Excel-arbetsbok och parsar japanska datum i C#
url: /sv/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar Excel-arbetsbok och parsar japanska datum i C#

Om du behöver **create Excel workbook** från början, visar den här guiden exakt hur. Du kommer att lära dig att **set cell value** med en japansk era‑datumsträng, **apply custom format** som förstår eran, och slutligen **read date cell** för att få en .NET `DateTime`. Det kompletta exemplet fungerar med den senaste Aspose.Cells för .NET, så du kan kopiera‑klistra in koden i vilket C#‑projekt som helst.

Att arbeta med datum som inkluderar japanska eror kan vara knepigt eftersom standard‑Excel‑parsern inte känner igen erasymbolerna. Genom att använda ett anpassat talformat (`[ja-JP-Era]`) talar du om för Excel hur strängen ska tolkas, vilket möjliggör pålitlig **excel date parsing**. Stegen nedan täcker hela arbetsflödet, från arbetsboks‑skapande till datumextraktion.

## Förutsättningar

- .NET 6.0 eller senare (koden körs också på .NET Framework 4.7+)
- Aspose.Cells för .NET (NuGet‑paketet `Aspose.Cells`)
- Grundläggande kunskap om C# och Visual Studio eller någon annan IDE du föredrar

## Steg 1: Skapa Excel-arbetsbok och lägg till ett kalkylblad

Den första operationen är att **create Excel workbook** i minnet. Aspose.Cells skapar automatiskt ett standardkalkylblad, men du kan lägga till fler om det behövs.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Optional: rename the default worksheet for clarity
        workbook.Worksheets[0].Name = "Dates";
```

Att skapa arbetsboken allokerar de interna strukturerna som senare håller celler, stilar och formler. Ingen fil skrivs på detta stadium, vilket gör operationen snabb och testbar.

## Steg 2: Sätt cellvärde med en japansk era-datumsträng

Nästa steg, **set cell value** till den japanska era-representationen "R5-04-01" (Reiwa 5, april 1). Strängen följer mönstret `EraYear-MM-DD`.

```csharp
        // Step 2: Reference cell A1 on the first worksheet
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Put the Japanese era date string into the cell
        dateCell.PutValue("R5-04-01");
```

Genom att använda `PutValue` lagras den råa texten. Excel kommer att behandla den som en sträng tills ett talformat säger något annat. Detta tillvägagångssätt fungerar för alla anpassade kalendrar, inte bara japanska eror.

## Steg 3: Applicera ett anpassat talformat som förstår den japanska eran

Nu **apply custom format** så att Excel kan översätta era-strängen till ett faktiskt serienummer för datum. Formatet `[ja-JP-Era]yyyy/MM/dd` instruerar motorn att tolka den inledande era‑karaktären (`R` för Reiwa) och beräkna det gregorianska datumet.

```csharp
        // Step 3: Apply a custom number format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";
```

Det anpassade formatet lagras i cellens stilobjekt. Aspose.Cells respekterar detta format både vid rendering och värdeomvandling, vilket möjliggör pålitlig **excel date parsing** senare i kedjan.

## Steg 4: Hämta det parsade DateTime‑värdet från cellen

Slutligen, **read date cell** för att få en .NET `DateTime`. `DateTimeValue`‑egenskapen returnerar det konverterade värdet baserat på det anpassade format som applicerades tidigare.

```csharp
        // Step 4: Retrieve the parsed DateTime value
        DateTime parsedDate = dateCell.DateTimeValue;

        // Output the result to the console for verification
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
```

När programmet körs skriver konsolen ut:

```
Parsed Gregorian date: 2023-04-01
```

Utdatan bekräftar att den japanska era‑strängen "R5-04-01" tolkades korrekt som 1 april 2023.

## Fullt, körbart exempel

Genom att sätta ihop delarna får du ett självständigt program som du kan kompilera och köra omedelbart.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Reference cell A1
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Insert Japanese era date string
        dateCell.PutValue("R5-04-01");

        // Apply custom format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";

        // Retrieve the parsed DateTime
        DateTime parsedDate = dateCell.DateTimeValue;

        // Show the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");

        // (Optional) Save the workbook to verify the visual format
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

När programmet körs skapas `JapaneseEraDate.xlsx` med cell A1 som visar `2023/04/01` medan konsolen visar samma gregorianska datum. Filen kan öppnas i Excel för att se det formaterade värdet.

## Varför detta tillvägagångssätt fungerar

- **create excel workbook** – Att instansiera `Workbook` bygger hela Excel‑filstrukturen i minnet utan att röra disken.
- **set cell value** – `PutValue` lagrar råtext, vilket är nödvändigt innan ett kulturspecifikt format appliceras.
- **apply custom format** – `[ja-JP-Era]`‑tokenen överbryggar klyftan mellan era‑notation och Excels interna serienumrering för datum.
- **read date cell** – `DateTimeValue` använder automatiskt cellens stil för att utföra konverteringen, vilket ger dig ett inbyggt `DateTime`.
- **excel date parsing** – Genom att delegera parsning till cellens stil undviker du manuell strängmanipulation, vilket minskar buggar och förbättrar stöd för lokaler.

## Kantfall och praktiska tips

- **Different eras** – Använd `S` för Showa, `H` för Heisei, `R` för Reiwa. Samma formatsträng fungerar för alla eror.
- **Invalid strings** – Om cellen innehåller ett felaktigt era‑datum, returnerar `DateTimeValue` `DateTime.MinValue`. Kontrollera `dateCell.IsDate` innan du läser.
- **Multiple cells** – Applicera det anpassade formatet på ett helt område (`range.ApplyStyle(style)`) när du behöver parsra många datum.
- **Performance** – Att sätta stil en gång per kolumn är snabbare än per cell för stora blad.
- **Saving options** – Aspose.Cells kan exportera till XLSX, XLS, CSV eller PDF. Välj det format som matchar efterföljande bearbetning.

## Vanliga frågor

**Kan jag använda den inbyggda .NET‑kulturen istället för ett anpassat format?**  
.NET‑klassen `CultureInfo` förstår inte japanska era‑symboler på samma sätt som Excel. Att använda ett anpassat talformat är den mest pålitliga metoden för **excel date parsing** av era‑strängar.

**Vad händer om jag behöver skriva tillbaka datumet till Excel i era‑format?**  
Sätt cellens värde till ett `DateTime` och applicera samma anpassade format. Excel visar automatiskt erat.

**Fungerar detta i äldre versioner av Excel?**  
`[ja-JP-Era]`‑tokenen stöds av Excel 2010 och senare. Aspose.Cells emulerar beteendet, så arbetsboken visas korrekt även när den öppnas i äldre Excel‑versioner som saknar inbyggt stöd för eror.

## Slutsats

Du vet nu hur du **create Excel workbook**, **set cell value** med en japansk era‑sträng, **apply custom format**, och **read date cell** för att få ett `DateTime`. Detta mönster ger robust **excel date parsing** utan manuell stränghantering, vilket gör din C#‑automatiseringskod både kortfattad och pålitlig.

Nästa steg är att utforska relaterade ämnen som **formatting multiple date columns**, **working with other cultural calendars**, eller **exporting the workbook to PDF**. Varje utökning bygger på samma principer som behandlats här, så du kan anpassa lösningen till ett brett spektrum av lokalanpassningsscenarier. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa Excel-arbetsbok i C# – Applicera anpassat talformat](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/)
- [Skapa Excel-arbetsbok med anpassat format – C#‑guide](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-custom-format-c-guide/)
- [Excel‑automatisering med Aspose.Cells .NET: Skapa arbetsbok & sätt externa länkar](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}