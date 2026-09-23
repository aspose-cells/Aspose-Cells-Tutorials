---
category: general
date: 2026-01-14
description: Exporteer tabel naar CSV in C# en leer hoe je een aangepast getalformaat
  instelt, CSV naar een bestand schrijft en automatische berekening inschakelt — allemaal
  in één tutorial.
draft: false
keywords:
- export table to csv
- set custom number format
- write csv to file
- enable automatic calculation
- how to format numbers
language: nl
og_description: Exporteer tabel naar CSV met aangepaste getalformaten, schrijf CSV
  naar bestand en schakel automatische berekening in met Aspose.Cells in C#.
og_title: Tabel exporteren naar CSV – Volledige C# walkthrough
tags:
- Aspose.Cells
- C#
- CSV export
- Excel automation
title: Tabel exporteren naar CSV – Complete C#‑gids met aangepaste getalformaten
url: /nl/net/csv-file-handling/export-table-to-csv-complete-c-guide-with-custom-number-form/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Table to CSV – Complete C# Guide with Custom Number Formats

Heb je ooit moeten **export table to CSV** maar wist je niet hoe je je getallen er netjes uit kunt laten zien? Je bent niet de enige. In veel data‑exportscenario's wil je de getallen mooi opgemaakt, de CSV naar schijf geschreven, en de werkmap gesynchroniseerd blijven met eventuele formules. Deze tutorial laat je precies zien **how to export table to CSV**, hoe je **set custom number format**, hoe je **write CSV to file**, en hoe je **enable automatic calculation** zodat alles up-to-date blijft.

We lopen door een real‑world voorbeeld met Aspose.Cells voor .NET. Aan het einde van deze gids heb je een enkel, uitvoerbaar C#‑programma dat:

* Formatteert een cel met een aangepast numeriek patroon (het “how to format numbers” gedeelte).
* Exporteert de eerste werkbladtabel naar een CSV‑string met een door jou gekozen scheidingsteken.
* Slaat die CSV‑string op naar een bestand op schijf.
* Parseert een Japanse‑era datum en schrijft deze terug naar het blad.
* Schakelt automatische berekening in zodat dynamische‑array formules altijd opnieuw berekenen.

Geen externe referenties nodig—kopieer, plak en voer uit.

![Export table to CSV illustration](export-table-to-csv.png "Export table to CSV diagram"){: alt="Export table to CSV diagram toont werkmap, tabel en CSV-uitvoer"}

---

## Wat je nodig hebt

* **Aspose.Cells for .NET** (NuGet package `Aspose.Cells`). De code werkt met versie 23.9 of later.
* Een .NET‑ontwikkelomgeving (Visual Studio, Rider, of `dotnet CLI`).
* Basiskennis van C#‑syntaxis—niets fancy, gewoon de gebruikelijke `using`‑statements en `Main`‑methode.

---

## Stap 1 – Aangepast getalformaat instellen (How to Format Numbers)

Voordat we iets exporteren, laten we ervoor zorgen dat getallen verschijnen zoals we willen. De `Custom`‑eigenschap op een `Style`‑object laat je een patroon definiëren zoals `"0.####"` om tot vier decimalen weer te geven terwijl achterliggende nullen worden weggelaten.

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Put a raw double value into cell A1
        worksheet.Cells[0, 0].PutValue(123.456789);

        // 3️⃣ Define a custom number format – this is the “how to format numbers” piece
        Style numberStyle = workbook.CreateStyle();
        numberStyle.Custom = "0.####"; // up to 4 significant digits
        worksheet.Cells[0, 0].SetStyle(numberStyle);
```

**Waarom dit belangrijk is:**  
Wanneer je later de tabel exporteert naar CSV, zou de ruwe double `123.456789` verschijnen als `123.456789`. Met het aangepaste formaat zal de CSV `123.4568` bevatten (afgerond op vier decimalen) – precies wat de meeste rapportagetools verwachten.

---

## Stap 2 – Tabel exporteren naar CSV (Primair Doel)

Aspose.Cells behandelt een gegevensbereik als een `Table`. Zelfs als je er geen expliciet een hebt aangemaakt, bevat het eerste werkblad altijd een standaardtabel op index 0. Het exporteren van die tabel is een één‑regelcode zodra je je `ExportTableOptions` hebt ingesteld.

```csharp
        // 4️⃣ Grab the first table in the worksheet
        Table firstTable = worksheet.Tables[0];

        // 5️⃣ Configure export options – we want a CSV string, comma‑delimited
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            Delimiter = ","
        };

        // 6️⃣ Export to a CSV string
        string csvContent = firstTable.ExportToString(exportOptions);

        // Show what we got (optional debug output)
        Console.WriteLine("=== CSV CONTENT ===");
        Console.WriteLine(csvContent);
```

**Verwachte CSV‑output** (gezien het aangepaste formaat uit Stap 1):

```
123.4568
```

Let op hoe het getal het `"0.####"`‑patroon respecteert dat we eerder hebben ingesteld. Dat is de magie van **export table to csv** gecombineerd met een aangepast numeriek stijl.

---

## Stap 3 – CSV naar bestand schrijven (Gegevens behouden)

Nu we een CSV‑string hebben, moeten we deze bewaren. De `File.WriteAllText`‑methode doet het werk, en we kunnen het bestand plaatsen waar we willen—vervang simpelweg `"YOUR_DIRECTORY"` door een echt pad.

```csharp
        // 7️⃣ Define where to save the CSV file
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "table.csv");

        // 8️⃣ Write the CSV string to disk – this is the “write csv to file” step
        File.WriteAllText(outputPath, csvContent);
        Console.WriteLine($"CSV file written to: {outputPath}");
```

**Tip:** Als je een ander scheidingsteken nodig hebt (puntkomma, tab, pipe), wijzig dan simpelweg `Delimiter` in `ExportTableOptions`. De rest van de code blijft hetzelfde, waardoor het eenvoudig aan te passen is.

---

## Stap 4 – Japanse‑era datum parseren (Extra plezier)

Vaak moet je omgaan met locale‑specifieke datums. Aspose.Cells wordt geleverd met een `DateTimeParser` die Japanse era‑strings begrijpt zoals `"R02/04/01"` (Reiwa 2 = 2020). Laten we die datum in de volgende rij plaatsen.

```csharp
        // 9️⃣ Set up a parser for Japanese‑era dates
        DateTimeParser eraParser = new DateTimeParser { Calendar = CalendarType.JapaneseEra };
        DateTime reiwaDate = eraParser.Parse("R02/04/01"); // 2020‑04‑01

        // 10️⃣ Write the parsed date into cell A2
        worksheet.Cells[1, 0].PutValue(reiwaDate);
```

De cel bevat nu een echte `DateTime`‑waarde, die Excel (of elke viewer) zal weergeven volgens de regionale instellingen van de werkmap.

---

## Stap 5 – Automatische berekening inschakelen (Formules actueel houden)

Als je werkmap formules bevat—vooral dynamische‑array formules—wil je dat ze automatisch opnieuw berekenen nadat we gegevens hebben gewijzigd. Het schakelen van de berekeningsmodus is een enkele eigenschapswijziging.

```csharp
        // 11️⃣ Turn on automatic calculation so formulas stay up‑to‑date
        workbook.Settings.CalcMode = CalculationMode.Automatic;

        // 12️⃣ Force a calculation pass (optional but ensures everything is up‑to‑date now)
        workbook.CalculateFormula();

        // Cleanup: save the workbook if you want to inspect it later
        string xlsPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "demo.xlsx");
        workbook.Save(xlsPath);
        Console.WriteLine($"Workbook saved to: {xlsPath}");
    }
}
```

**Waarom automatische berekening inschakelen?**  
Wanneer je later `demo.xlsx` opent in Excel, zullen alle formules die verwijzen naar het aangepast‑geformatteerde getal of de Japanse‑era datum al de nieuwste waarden weergeven. Dit is het “enable automatic calculation” onderdeel van onze tutorial.

---

## Volledig werkend voorbeeld (Alle stappen samen)

Hieronder staat het volledige, kant‑klaar‑om‑te‑kopiëren‑en‑plakken programma. Er ontbreken geen onderdelen; voer het gewoon uit en zie de console‑output en bestanden verschijnen op je bureaublad.

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Set a number with a custom format (how to format numbers)
        worksheet.Cells[0, 0].PutValue(123.456789);
        Style numberStyle = workbook.CreateStyle();
        numberStyle.Custom = "0.####";
        worksheet.Cells[0, 0].SetStyle(numberStyle);

        // Export the first table to CSV (export table to csv)
        Table firstTable = worksheet.Tables[0];
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            Delimiter = ","
        };
        string csvContent = firstTable.ExportToString(exportOptions);
        Console.WriteLine("=== CSV CONTENT ===");
        Console.WriteLine(csvContent);

        // Write CSV to file (write csv to file)
        string csvPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "table.csv");
        File.WriteAllText(csvPath, csvContent);
        Console.WriteLine($"CSV file written to: {csvPath}");

        // Parse a Japanese‑era date and write it to the sheet
        DateTimeParser eraParser = new DateTimeParser { Calendar = CalendarType.JapaneseEra };
        DateTime reiwaDate = eraParser.Parse("R02/04/01");
        worksheet.Cells[1, 0].PutValue(reiwaDate);

        // Enable automatic calculation (enable automatic calculation)
        workbook.Settings.CalcMode = CalculationMode.Automatic;
        workbook.CalculateFormula();

        // Save the workbook for inspection
        string xlsPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "demo.xlsx");
        workbook.Save(xlsPath);
        Console.WriteLine($"Workbook saved to: {xlsPath}");
    }
}
```

**Resultaat checklist**

| ✅ | Wat je zou moeten zien |
|---|--------------------------|
| CSV‑bestand `table.csv` op je bureaublad met `123.4568` |
| Excel‑bestand `demo.xlsx` op je bureaublad met het aangepast‑geformatteerde getal in A1 en de Japanse‑era datum (2020‑04‑01) in A2 |
| Console‑output die elke stap bevestigt |

---

## Veelgestelde vragen & randgevallen

**V: Wat als mijn tabel kopteksten heeft?**  
A: `ExportTableOptions` respecteert de `ShowHeaders`‑eigenschap van de tabel. Stel `firstTable.ShowHeaders = true;` in vóór het exporteren, en de CSV zal automatisch de koprij bevatten.

**V: Kan ik meerdere tabellen tegelijk exporteren?**  
A: Zeker. Loop door `worksheet.Tables` en concateneer de CSV‑strings, of sla elke op in een apart bestand. Vergeet niet `Delimiter` aan te passen als je per bestand een ander scheidingsteken nodig hebt.

**V: Mijn getallen hebben een duizendtallen‑scheidingsteken nodig (bijv. `1,234.56`).**  
A: Verander het aangepaste formaat naar `"#,##0.##"` en de geëxporteerde CSV zal de komma's bevatten. Houd er rekening mee dat sommige CSV‑parsers komma's als scheidingsteken behandelen, dus je kunt overschakelen naar een puntkomma (`Delimiter = ";"`) om verwarring te voorkomen.

**V: Ik richt me op .NET 6—zijn er compatibiliteitsproblemen?**  
A: Nee. Aspose.Cells 23.9+ richt zich op .NET Standard 2.0+, dus het werkt prima met .NET 6, .NET 7, en zelfs .NET Framework 4.8.

---

## Samenvatting

We hebben behandeld hoe je **export table to csv** kunt uitvoeren terwijl je een **custom number format** behoudt, hoe je **write csv to file** kunt doen, en hoe je **enable automatic calculation** kunt inschakelen zodat je werkmap gesynchroniseerd blijft. We hebben ook een snelle demo toegevoegd van het parseren van een Japanse‑

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}