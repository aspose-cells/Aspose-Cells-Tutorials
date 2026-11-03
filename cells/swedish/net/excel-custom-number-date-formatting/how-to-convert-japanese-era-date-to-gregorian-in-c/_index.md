---
category: general
date: 2026-10-01
description: Konvertera japanskt era‑datum till ett gregorianskt DateTime med Aspose.Cells
  i C#. Lär dig hur du snabbt konverterar den japanska kalendern.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert japanese era date
- how to convert japanese calendar
language: sv
lastmod: 2026-10-01
og_description: Konvertera japanskt era‑datum till ett gregorianskt DateTime i C#.
  Denna handledning förklarar hur du konverterar den japanska kalendern exakt med
  Aspose.Cells.
og_image_alt: Code example converting a Japanese era date string to a Gregorian DateTime
  in a C# console app
og_title: Konvertera japanskt era‑datum till gregorianskt i C# – steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  headline: How to convert Japanese era date to Gregorian in C#
  type: TechArticle
- description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  name: How to convert Japanese era date to Gregorian in C#
  steps:
  - name: Why each step matters
    text: '| Step | Purpose | How it helps the conversion | |------|---------|-----------------------------|
      | **Create workbook** | Provides a container that understands Excel formulas
      and date systems. | The library’s internal date engine is activated only inside
      a workbook. | | **Insert era string** | Suppl'
  - name: Handling invalid or ambiguous strings
    text: '* **Invalid era name** – Aspose.Cells throws a `FormatException`. Wrap
      the conversion in `try/catch` to provide a friendly error message. * **Missing
      year/month/day** – The library expects a full “Era Year/Month/Day” pattern.
      If you receive partial data, prepend missing parts or reject the input ear'
  - name: Next steps
    text: '* Explore **formatting options** to write the Gregorian date back into
      the worksheet with a custom number format. * Combine this conversion with **data
      import pipelines** (e.g., reading CSV files that contain era dates). * Review
      other Aspose.Cells features such as **date arithmetic** and **regional'
  type: HowTo
tags:
- Aspose.Cells
- C#
- date conversion
title: Hur man konverterar japanskt era‑datum till gregorianskt i C#
url: /sv/net/excel-custom-number-date-formatting/how-to-convert-japanese-era-date-to-gregorian-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så konverterar du japanska era‑datum till gregorianskt i C#

Om du behöver **konvertera japanska era‑datum**‑strängar till gregorianska datum i C#, visar den här guiden exakt hur du gör. Oavsett om du bearbetar äldre data, läser användarinmatning eller genererar rapporter, gör Aspose.Cells‑biblioteket konverteringen enkel. Dessutom kommer du att upptäcka det bästa sättet att **konvertera japanska kalendervärden** när du arbetar med kalkylblad.

Handledningen täcker varje steg—från att skapa en arbetsbok till att hämta ett `DateTime`‑värde—så att du kan kopiera‑klistra in ett komplett, körbart program. Ingen extern dokumentation behövs; följ bara koden och förklaringarna nedan.

## Förutsättningar

Innan du börjar, se till att du har:

* .NET 6.0 eller senare (koden fungerar även med .NET Framework 4.6+)
* En licens för **Aspose.Cells** (gratis provversion fungerar för testning)
* En utvecklingsmiljö som Visual Studio 2022 eller VS Code
* Grundläggande kunskap om C#‑konsolapplikationer

## Konvertera japanska era‑datum med Aspose.Cells

Kärnan i konverteringen finns i några enkla API‑anrop. Aspose.Cells tolkar automatiskt japanska era‑strängar (t.ex. “Reiwa 2/04/01”) och exponerar resultatet som ett `DateTime`‑objekt när kalkylbladet har beräknats om.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                // creates an empty Excel file in memory
        var worksheet = workbook.Worksheets[0];       // the default sheet is at index 0

        // Step 2: Insert a Japanese era date string into cell A1
        // The string follows the Japanese calendar format: Era Year/Month/Day
        worksheet.Cells[0, 0].PutValue("Reiwa 2/04/01");

        // Step 3: Apply a default style to the cell (required for proper calculation)
        // Without a style, Aspose.Cells may treat the content as plain text and skip conversion.
        worksheet.Cells[0, 0].SetStyle(workbook.CreateStyle());

        // Step 4: Recalculate the worksheet so the date string is converted to a Gregorian date
        // The Calculate method parses the era string and updates the cell's internal value.
        worksheet.Calculate();

        // Step 5: Retrieve and display the converted DateTime value (2020‑04‑01)
        DateTime gregorian = worksheet.Cells[0, 0].DateTimeValue;
        Console.WriteLine($"Gregorian date: {gregorian:yyyy-MM-dd}");
    }
}
```

### Varför varje steg är viktigt

| Steg | Syfte | Hur det hjälper konverteringen |
|------|-------|--------------------------------|
| **Skapa arbetsbok** | Tillhandahåller en behållare som förstår Excel‑formler och datumssystem. | Bibliotekets interna datum‑motor aktiveras endast inom en arbetsbok. |
| **Infoga era‑sträng** | Tillhandahåller den råa japanska kalendertexten du vill översätta. | Aspose.Cells känner igen eranamn som *Reiwa*, *Heisei*, *Showa* osv. |
| **Ange stil** | Tvingar cellen att behandlas som ett värde‑fält snarare än en bokstavlig sträng. | Utan en stil kan `Calculate`‑metoden ignorera cellen, vilket lämnar texten oförändrad. |
| **Beräkna** | Utlöser tolkning av era‑strängen och konvertering till det interna serienummer‑datumet. | Biblioteket konverterar “Reiwa 2/04/01” → serienummer → gregoriansk `DateTime`. |
| **Läs `DateTimeValue`** | Returnerar det konverterade .NET `DateTime`‑objektet. | Du har nu ett standard‑`DateTime` som du kan använda i alla .NET‑API. |

## Så konverterar du japansk kalender i andra scenarier

Samma metod fungerar för alla japanska eranamn som stöds av Aspose.Cells:

```csharp
// Example: converting a Heisei era date
worksheet.Cells[0, 0].PutValue("Heisei 30/12/31"); // corresponds to 2018‑12‑31
worksheet.Calculate();
Console.WriteLine(worksheet.Cells[0, 0].DateTimeValue); // 2018-12-31
```

### Hantera ogiltiga eller tvetydiga strängar

* **Invalid era name** – Aspose.Cells kastar ett `FormatException`. Omslut konverteringen i `try/catch` för att ge ett vänligt felmeddelande.
* **Missing year/month/day** – Biblioteket förväntar sig ett komplett “Era Year/Month/Day”‑mönster. Om du får partiella data, lägg till de saknade delarna eller avvisa inmatningen tidigt.
* **Different locale settings** – Konverteringen är **inte** beroende av den aktuella trådkulturen; den använder alltid den japanska erakartan som är inbyggd i Aspose.Cells. Detta gör metoden säker för server‑sidig bearbetning.

```csharp
try
{
    worksheet.Cells[0, 0].PutValue(userInput);
    worksheet.Calculate();
    DateTime result = worksheet.Cells[0, 0].DateTimeValue;
    // Use result...
}
catch (FormatException ex)
{
    Console.WriteLine($"Unable to parse Japanese era date: {ex.Message}");
}
```

## Praktiska tips och vanliga fallgropar

* **Always call `SetStyle`** before `Calculate`. Att hoppa över detta steg är en vanlig felkälla eftersom cellen förblir en ren text‑behållare.
* **Reuse the same workbook** if you need to convert many dates. Att skapa en ny arbetsbok för varje konvertering ger onödig overhead.
* **Batch conversion** – Fyll en kolumn med era‑strängar, anropa `worksheet.Calculate()` en gång och läs sedan hela kolumnen med `DateTimeValue`s. Detta är mycket effektivare än att beräkna per cell.
* **Version compatibility** – Logiken för era‑konvertering introducerades i Aspose.Cells 22.9. Säkerställ att du använder den versionen eller senare; äldre versioner behandlar strängen som ren text.

## Fullständigt fungerande exempel (konsolapp)

Nedan är ett självständigt program som du kan kompilera och köra omedelbart. Det demonstrerar både en Reiwa‑ och en Heisei‑konvertering samt hanterar fel på ett smidigt sätt.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConverter
{
    static void Main()
    {
        // Initialize workbook once
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        var style = workbook.CreateStyle();
        sheet.Cells[0, 0].SetStyle(style);
        sheet.Cells[1, 0].SetStyle(style);

        // Sample inputs
        string[] eraDates = { "Reiwa 2/04/01", "Heisei 30/12/31", "InvalidEra 1/01/01" };

        for (int i = 0; i < eraDates.Length; i++)
        {
            sheet.Cells[i, 0].PutValue(eraDates[i]);
        }

        // Perform conversion for all populated cells
        sheet.Calculate();

        // Output results
        for (int i = 0; i < eraDates.Length; i++)
        {
            try
            {
                DateTime dt = sheet.Cells[i, 0].DateTimeValue;
                Console.WriteLine($"{eraDates[i]} → {dt:yyyy-MM-dd}");
            }
            catch (Exception)
            {
                Console.WriteLine($"{eraDates[i]} → conversion failed");
            }
        }
    }
}
```

**Förväntad konsolutmatning**

```
Reiwa 2/04/01 → 2020-04-01
Heisei 30/12/31 → 2018-12-31
InvalidEra 1/01/01 → conversion failed
```

Att köra detta program bekräftar att biblioteket korrekt **konverterar japanska era‑datum**‑strängar och smidigt rapporterar ej stödda värden.

## Slutsats

Du vet nu hur du **konverterar japanska era‑datum**‑strängar till standard‑gregorianska `DateTime`‑objekt med Aspose.Cells i C#. Processen reduceras till att infoga era‑texten, applicera en stil, beräkna om kalkylbladet och läsa `DateTimeValue`. Genom att följa stegen ovan kan du också besvara den bredare frågan **hur man konverterar japansk kalender**‑data i bulk, hantera fel och optimera prestanda.

### Nästa steg

* Utforska **formatalternativ** för att skriva tillbaka det gregorianska datumet till kalkylbladet med ett anpassat talformat.
* Kombinera denna konvertering med **datainmatnings‑pipeline** (t.ex. läsa CSV‑filer som innehåller era‑datum).
* Granska andra Aspose.Cells‑funktioner såsom **datum‑aritmetik** och **regionala inställningar** för mer komplexa kalenderscenarier.

Lycka till med kodandet, och känn dig fri att anpassa exemplet till dina egna databehandlingsflöden!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig behärska ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Analysera japanska era‑datum i C# med Aspose.Cells – Fullständig guide](/cells/english/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/)
- [Aktivera japansk era‑parsing i C# med Aspose.Cells](/cells/english/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/)
- [Hur man skapar arbetsbok och konverterar sträng till datum i C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}