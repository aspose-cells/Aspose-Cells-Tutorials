---
category: general
date: 2026-03-18
description: Extrahera datum från Excel och skriv ut datum i formatet yyyy‑mm‑dd i
  ISO-format. Lär dig hur du läser japanska era‑datum, konverterar dem och visar ISO‑datum
  i C#.
draft: false
keywords:
- extract date from excel
- output date yyyy-mm-dd
- display date iso format
language: sv
og_description: Extrahera datum från Excel och skriv ut datum i formatet yyyy‑mm‑dd
  enligt ISO. Steg‑för‑steg C#‑handledning med fullständig kod och förklaringar.
og_title: Extrahera datum från Excel – Skriv ut datum yyyy‑mm‑dd i C#
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Extrahera datum från Excel och skriv ut datum yyyy‑mm‑dd – Komplett C#‑guide
url: /sv/net/data-loading-and-parsing/extract-date-from-excel-and-output-date-yyyy-mm-dd-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera datum från Excel – Hur man skriver ut datum yyyy‑mm‑dd i ISO-format

Har du någonsin behövt **extrahera datum från Excel** men varit osäker på hur du hanterar japanska era‑datum eller får en ren `yyyy‑mm‑dd`‑sträng? Du är inte ensam. I många datamigrationsprojekt lagras datum i källarboken med den japanska kejsarkalendern, och det nedströms systemet förväntar sig ett ISO‑kompatibelt datum som `2024-04-01`.  

I den här guiden går vi igenom en komplett, körbar lösning som läser en cell, tolkar den japanska eran och **skriver ut datumet yyyy‑mm‑dd**. När du är klar vet du exakt hur du **visar datum i ISO‑format** i vilken .NET‑app som helst, och du har ett återanvändbart kodsnutt som du kan klistra in i ditt eget projekt.

## Vad du behöver

- **.NET 6+** (eller .NET Framework 4.7.2+).  
- **Aspose.Cells for .NET** – biblioteket som låter oss ange en anpassad kalender när vi laddar en arbetsbok.  
- En Excel‑fil (`japan-date.xlsx`) som innehåller ett datum lagrat i en japansk era‑cell (t.ex. `令和3年4月1日`).  
- En favorit‑IDE – Visual Studio, Rider eller till och med VS Code räcker.

Inga extra NuGet‑paket krävs utöver Aspose.Cells, och koden fungerar på Windows, Linux eller macOS.

## Steg 1: Skapa projektet och installera Aspose.Cells

Börja med att skapa en konsolapp:

```bash
dotnet new console -n ExcelDateDemo
cd ExcelDateDemo
dotnet add package Aspose.Cells
```

> **Proffstips:** Om du kör på en CI‑server, spetsa paketversionen (`Aspose.Cells 23.12`) för att garantera reproducerbara byggen.

## Steg 2: Ladda arbetsboken med den japanska kejsarkalendern

Nyckeln till **extrahera datum från Excel** när källan använder en icke‑gregoriansk kalender är att tala om för Aspose.Cells vilken kalender som ska tillämpas vid inläsning. Det gör vi med `LoadOptions.Calendar`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create load options and set the Japanese Emperor calendar
        LoadOptions loadOptions = new LoadOptions
        {
            // This tells Aspose.Cells to interpret era dates correctly
            Calendar = new JapaneseEmperorCalendar()
        };

        // Step 3: Open the workbook that contains Japanese era dates
        // Replace the path with the actual location of your Excel file
        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);
```

**Varför detta är viktigt:** Utan den anpassade kalendern skulle Aspose.Cells behandla cellen som en vanlig sträng, och du skulle förlora era‑informationen. Genom att tilldela `JapaneseEmperorCalendar` konverterar biblioteket automatiskt `令和3年4月1日` till `2021‑04‑01` bakom kulisserna.

## Steg 3: Hämta datumet från en specifik cell

Nu när arbetsboken vet hur man tolkar eran kan vi läsa cellen som ett `DateTime`. Låt oss anta att datumet finns i det första kalkylbladet, cell **A1** (rad 0, kolumn 0).

```csharp
        // Step 4: Retrieve the date value from the first worksheet, first cell
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0]; // A1

        // GetDateTime() returns a System.DateTime object
        DateTime extractedDate = dateCell.GetDateTime();
```

Om cellen är tom eller innehåller ett icke‑datumvärde kommer `GetDateTime()` att kasta ett undantag. Ett defensivt tillvägagångssätt ser ut så här:

```csharp
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        DateTime extractedDate = dateCell.GetDateTime();
```

**Edge case:** Vissa äldre Excel‑filer lagrar datum som tal (seriedatum). Aspose.Cells hanterar dem automatiskt, men du bör ändå verifiera celltypen om du förväntar dig blandat innehåll.

## Steg 4: Skriv ut datum yyyy‑mm‑dd (ISO) och verifiera

Med `DateTime` i handen är formateringen till **output date yyyy‑mm‑dd** en enradare:

```csharp
        // Step 5: Output the date in ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

Kör programmet mot en fil som innehåller `令和3年4月1日` så skrivs följande ut:

```
Extracted date (ISO): 2021-04-01
```

Det är exakt **display date iso format** som många API:er kräver.

## Fullt fungerande exempel

När vi sätter ihop alla bitar får vi det kompletta, kopiera‑och‑klistra‑klara programmet:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook with Japanese era support
        LoadOptions loadOptions = new LoadOptions
        {
            Calendar = new JapaneseEmperorCalendar()
        };

        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);

        // Access the cell that holds the date (A1)
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0];

        // Validate the cell contains a date
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        // Extract the DateTime value
        DateTime extractedDate = dateCell.GetDateTime();

        // Convert to ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

> **Obs:** Ersätt `YOUR_DIRECTORY` med den faktiska mappen som innehåller `japan-date.xlsx`. Koden fungerar med vilket blad och vilken cell som helst – justera bara indexen.

## Hantera andra kalendrar (valfritt)

Om du någonsin behöver **extrahera datum från Excel** som använder den thailändska buddhistkalendern eller den hebreiska kalendern, byt helt enkelt kalenderinstansen:

```csharp
loadOptions.Calendar = new ThaiBuddhistCalendar();   // for Thai dates
// or
loadOptions.Calendar = new HebrewCalendar();         // for Hebrew dates
```

Resten av logiken förblir oförändrad, vilket visar metodens flexibilitet.

## Vanliga fallgropar och hur du undviker dem

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| `GetDateTime()` kastar `InvalidCastException` | Cellen är inte ett datum (kanske en sträng) | Kontrollera `Cell.Type` innan du anropar, eller använd `DateTime.TryParse` på `Cell.StringValue`. |
| Fel årtal efter konvertering | Arbetsboken laddades utan att sätta `Calendar` | Skapa alltid `LoadOptions` med rätt kalender **innan** du öppnar filen. |
| ISO‑utdata visar tid (`2021-04-01 00:00:00`) | Använde `ToString()` utan formatsträng | Använd formatsträngen `"yyyy-MM-dd"` för att tvinga **output date yyyy‑mm‑dd**. |
| Filen hittas inte | Relativ sökväg pekar på fel mapp | Använd `Path.Combine(Environment.CurrentDirectory, "japan-date.xlsx")` eller ange en absolut sökväg. |

## Proffstips för produktionsklar kod

1. **Cacha arbetsboken** om du behöver läsa många datum från samma fil – att öppna en arbetsbok är relativt dyrt.  
2. **Packa in extraktionslogiken** i en återanvändbar metod:

   ```csharp
   static string ExtractIsoDate(string file, int sheetIdx, int row, int col)
   {
       var opts = new LoadOptions { Calendar = new JapaneseEmperorCalendar() };
       var wb = new Workbook(file, opts);
       var cell = wb.Worksheets[sheetIdx].Cells[row, col];
       if (cell.Type != CellValueType.IsDateTime) return null;
       return cell.GetDateTime().ToString("yyyy-MM-dd");
   }
   ```

3. **Logga den ursprungliga era‑strängen** (`cell.StringValue`) tillsammans med ISO‑utdata för revisionsspår.  
4. **Enhetstesta** metoden med några hårdkodade Excel‑filer som täcker olika eror (Heisei, Reiwa) för att garantera korrekthet.

## Visuell översikt

Nedan är ett snabbt diagram som illustrerar dataflödet – från Excel‑cell till ISO‑sträng.  

![Extract date from Excel example showing Excel → LoadOptions → DateTime → ISO string]  

*Alt‑text: “extract date from excel” diagram som visar konverteringspipeline.*

## Slutsats

Vi har gått igenom allt du behöver för att **extrahera datum från Excel**, hantera japanska era‑värden och **skriva ut datum yyyy‑mm‑dd** så att det följer **display date iso format** som moderna API:er älskar. Lösningen är fristående, fungerar med alla .NET‑versioner som stöder Aspose.Cells, och kan utökas till andra kalendrar med en enda rad förändring.

Har du en annan kalender i åtanke? Eller kanske drar du datum från flera kolumner? Känn dig fri att justera `ExtractIsoDate`‑hjälparen eller lämna en kommentar nedan. Lycka till med kodningen, och må dina datum alltid hålla sig i perfekt ISO‑synk!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}