---
category: general
date: 2026-03-18
description: Haal datum uit Excel op en geef de datum yyyy‑mm‑dd in ISO‑formaat weer.
  Leer hoe je Japanse era‑datums kunt lezen, ze kunt converteren en ISO‑datums kunt
  weergeven in C#.
draft: false
keywords:
- extract date from excel
- output date yyyy-mm-dd
- display date iso format
language: nl
og_description: Haal datum uit Excel en geef datum yyyy‑mm‑dd in ISO‑formaat weer.
  Stapsgewijze C#‑tutorial met volledige code en uitleg.
og_title: Datum uit Excel extraheren – Output datum yyyy‑mm‑dd in C#
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Datum extraheren uit Excel en datum weergeven yyyy‑mm‑dd – Complete C#‑gids
url: /nl/net/data-loading-and-parsing/extract-date-from-excel-and-output-date-yyyy-mm-dd-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Datum uit Excel extraheren – Hoe een datum yyyy‑mm‑dd in ISO-formaat weergeven

Ever needed to **extract date from Excel** but weren’t sure how to handle Japanese era dates or get a clean `yyyy‑mm‑dd` string? You're not alone. In many data‑migration projects the source workbook stores dates using the Japanese Emperor calendar, and the downstream system expects an ISO‑compliant date like `2024-04-01`.  

In this guide we’ll walk through a complete, runnable solution that reads a cell, interprets the Japanese era, and **outputs the date yyyy‑mm‑dd**. By the end you’ll know exactly how to **display date ISO format** in any .NET app, and you’ll have a reusable code snippet you can drop into your own project.

## Wat je nodig hebt

- **.NET 6+** (of .NET Framework 4.7.2+).  
- **Aspose.Cells for .NET** – de bibliotheek die ons toestaat een aangepaste kalender in te stellen bij het laden van een werkmap.  
- Een Excel‑bestand (`japan-date.xlsx`) dat een datum bevat die is opgeslagen in een Japanse jaartelling‑cel (bijv. `令和3年4月1日`).  
- Een favoriete IDE – Visual Studio, Rider, of zelfs VS Code volstaat.

Er zijn geen extra NuGet‑pakketten nodig naast Aspose.Cells, en de code werkt op Windows, Linux of macOS.

## Stap 1: Het project opzetten en Aspose.Cells installeren

```bash
dotnet new console -n ExcelDateDemo
cd ExcelDateDemo
dotnet add package Aspose.Cells
```

> **Pro tip:** Als je op een CI‑server werkt, pin dan de pakketversie (`Aspose.Cells 23.12`) om reproduceerbare builds te garanderen.

## Stap 2: Laad de werkmap met de Japanse keizerkalender

De sleutel om **extract date from Excel** te doen wanneer de bron een niet‑Gregoriaanse kalender gebruikt, is om Aspose.Cells te vertellen welke kalender moet worden toegepast tijdens het laden. We doen dat met `LoadOptions.Calendar`.

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

**Why this matters:** Zonder de aangepaste kalender zou Aspose.Cells de cel behandelen als een gewone string, en zou je de jaartelling‑informatie verliezen. Door `JapaneseEmperorCalendar` toe te wijzen, converteert de bibliotheek automatisch `令和3年4月1日` naar `2021‑04‑01` op de achtergrond.

## Stap 3: Haal de datum op uit een specifieke cel

Nu de werkmap weet hoe de jaartelling te interpreteren, kunnen we de cel lezen als een `DateTime`. Laten we aannemen dat de datum zich bevindt in het eerste werkblad, cel **A1** (rij 0, kolom 0).

```csharp
        // Step 4: Retrieve the date value from the first worksheet, first cell
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0]; // A1

        // GetDateTime() returns a System.DateTime object
        DateTime extractedDate = dateCell.GetDateTime();
```

Als de cel leeg is of een niet‑datumelement bevat, zal `GetDateTime()` een uitzondering werpen. Een defensieve aanpak ziet er als volgt uit:

```csharp
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        DateTime extractedDate = dateCell.GetDateTime();
```

**Edge case:** Sommige oudere Excel‑bestanden slaan datums op als getallen (seriële datums). Aspose.Cells verwerkt die automatisch, maar je moet nog steeds het celtype controleren als je gemengde inhoud verwacht.

## Stap 4: Datum yyyy‑mm‑dd (ISO) weergeven en verifiëren

Met de `DateTime` in de hand, kun je deze formatteren als **output date yyyy‑mm‑dd** met één regel code:

```csharp
        // Step 5: Output the date in ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

Het uitvoeren van het programma tegen een bestand dat `令和3年4月1日` bevat, zal afdrukken:

```
Extracted date (ISO): 2021-04-01
```

Dat is het exacte **display date iso format** dat veel API's vereisen.

## Volledig werkend voorbeeld

Door alle onderdelen samen te voegen, hier het volledige, kant‑klaar‑om‑te‑kopiëren‑en‑plakken programma:

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

> **Note:** Vervang `YOUR_DIRECTORY` door de daadwerkelijke map die `japan-date.xlsx` bevat. De code werkt met elk blad en elke cel – pas gewoon de indexen aan.

## Andere kalenders verwerken (optioneel)

Als je ooit **extract date from Excel** moet doen die de Thaise Boeddhistische kalender of de Hebreeuwse kalender gebruikt, verwissel dan simpelweg de kalender‑instantie:

```csharp
loadOptions.Calendar = new ThaiBuddhistCalendar();   // for Thai dates
// or
loadOptions.Calendar = new HebrewCalendar();         // for Hebrew dates
```

De rest van de logica blijft ongewijzigd, wat de flexibiliteit van de aanpak aantoont.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| `GetDateTime()` throws `InvalidCastException` | Cel is geen datum (mogelijk een string) | Controleer `Cell.Type` vóór het aanroepen, of gebruik `DateTime.TryParse` op `Cell.StringValue`. |
| Wrong year after conversion | Werkmap geladen zonder `Calendar` in te stellen | Maak altijd `LoadOptions` met de juiste kalender **voordat** je het bestand opent. |
| ISO output shows time part (`2021-04-01 00:00:00`) | `ToString()` gebruikt zonder opmaakstring | Gebruik `"yyyy-MM-dd"` format specifier to force **output date yyyy‑mm‑dd**. |
| File not found | Relatief pad wijst naar de verkeerde map | Gebruik `Path.Combine(Environment.CurrentDirectory, "japan-date.xlsx")` of geef een absoluut pad op. |

## Pro‑tips voor productie‑klare code

1. **Cache de werkmap** als je veel datums uit hetzelfde bestand moet lezen – het openen van een werkmap is relatief duur.  
2. **Wrap de extractielogica** in een herbruikbare methode:

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

3. **Log de originele jaartelling‑string** (`cell.StringValue`) naast de ISO‑output voor audit‑trails.  
4. **Unit‑test** de methode met een paar hard‑gecodeerde Excel‑bestanden die verschillende jaartellingen (Heisei, Reiwa) dekken om de juistheid te garanderen.

## Visueel overzicht

Hieronder staat een snel diagram dat de gegevensstroom illustreert — van Excel‑cel naar ISO‑string.  

![Extract date from Excel example showing Excel → LoadOptions → DateTime → ISO string]  

*Alt text: “extract date from excel” diagram die de conversiepijplijn weergeeft.*

## Conclusie

We hebben alles behandeld wat je nodig hebt om **extract date from Excel** uit te voeren, Japanse jaartelling‑waarden te verwerken, en **output date yyyy‑mm‑dd** zodat het voldoet aan het **display date iso format** dat moderne API's waarderen. De oplossing is zelfstandig, werkt met elke .NET‑versie die Aspose.Cells ondersteunt, en kan met één regel code naar andere kalenders worden uitgebreid.

Heb je een andere kalender in gedachten? Of haal je datums uit meerdere kolommen? Voel je vrij om de `ExtractIsoDate`‑helper aan te passen of een reactie achter te laten. Veel plezier met coderen, en moge je datums altijd perfect in ISO‑sync blijven!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}