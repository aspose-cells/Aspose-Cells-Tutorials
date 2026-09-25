---
category: general
date: 2026-05-04
description: Exporteer werkbladbereik met C# en aangepaste opmaak. Leer hoe je een
  Excel‑bereik exporteert en hoe je celexport kunt aanpassen in een paar eenvoudige
  stappen.
draft: false
keywords:
- export worksheet range
- how to export excel range
- how to customize cell export
- C# Excel export
- worksheet export options
language: nl
og_description: Werkbladbereik exporteren met C#. Deze gids laat zien hoe je een Excel‑bereik
  exporteert en celexport snel en betrouwbaar kunt aanpassen.
og_title: Werkbladbereik exporteren in C# – Complete programmeergids
tags:
- C#
- Excel
- Data Export
title: Werkbladbereik exporteren in C# – Complete programmeergids
url: /nl/net/excel-data-export-retrieval/export-worksheet-range-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Werkbladbereik exporteren in C# – Complete Programming Guide

Heb je ooit **werkbladbereik moeten exporteren** maar was de standaardoutput niet wat je wilde? Je bent niet de enige—veel ontwikkelaars lopen tegen die muur aan wanneer ze een blok cellen naar een CSV‑ of JSON‑bestand proberen te halen. Het goede nieuws? Met een paar regels C# kun je niet alleen **excel‑bereik exporteren** maar ook **cel‑export aanpassen** zodat het past bij elk downstream‑formaat.

In deze tutorial lopen we een real‑world scenario door: cellen *A1:D10* uit een Excel‑werkmap nemen, elke waarde omzetten naar een haakjes‑string, en het resultaat naar een bestand schrijven. Aan het einde weet je precies **hoe je werkbladbereik exporteert** met volledige controle over de weergave van elke cel, plus een reeks tips voor randgevallen waar je later tegenaan kunt lopen.

## Wat je nodig hebt

- .NET 6 of later (de code werkt ook met .NET Framework 4.7+)  
- Het **GemBox.Spreadsheet** NuGet‑pakket (of elke bibliotheek die `ExportTableOptions` biedt; de getoonde API is van GemBox)  
- Een basisbegrip van C#‑syntaxis – niets bijzonders, alleen de gebruikelijke `using`‑statements en objectcreatie  

Als je dit hebt, kun je meteen beginnen.

## Stap 1: De exportopties instellen – Primair controlepunt  

Het eerste wat je doet is een `ExportTableOptions`‑instantie maken en aangeven dat elke cel als string behandeld moet worden. Dit is de basis voor **hoe je excel‑bereik exporteert** terwijl het gegevenstype consistent blijft.

```csharp
using GemBox.Spreadsheet;

public class WorksheetExporter
{
    public void ExportRange(string sourcePath, string destinationPath)
    {
        // Load the workbook.
        var workbook = ExcelFile.Load(sourcePath);
        var worksheet = workbook.Worksheets[0]; // assume first sheet

        // Step 1: Create export options and enable string export.
        var exportOptions = new ExportTableOptions
        {
            ExportAsString = true // forces every cell to be exported as text
        };
```

*Waarom string‑export forceren?*  
Wanneer je later elke cel aanpast, voeg je haakjes en mogelijk andere symbolen toe. Alles als string houden voorkomt verrassingen bij type‑conversie (bijv. datums die veranderen in seriële getallen).

## Stap 2: De CellExport‑event afvangen – Elke cel aanpassen  

Nu komt het leuke deel: **hoe je cel‑export aanpast**. GemBox heft een `CellExport`‑event op voor elke cel die geschreven gaat worden. Door dit te behandelen kun je de waarde in haakjes plaatsen, een prefix toevoegen, of zelfs een cel volledig overslaan.

```csharp
        // Step 2: Customize each cell's exported value.
        exportOptions.CellExport += (sender, e) =>
        {
            // e.Value holds the original cell content.
            // We'll wrap it in square brackets.
            e.Value = $"[{e.Value}]";
        };
```

*Pro tip:* Als je alleen numerieke cellen wilt aanpassen, controleer dan `e.Value.GetType()` voordat je de haakjes toevoegt. Die kleine guard kan je redden van onbedoeld beschadigde header‑tekst.

## Stap 3: Het gewenste bereik exporteren – De kernactie  

Met de opties klaar, roep je `ExportTable` aan. De methode neemt de werkmap die je geladen hebt, het adres van het bereik dat je wilt, en de opties die je zojuist geconfigureerd hebt.

```csharp
        // Step 3: Export the range A1:D10 using the configured options.
        worksheet.ExportTable(workbook, "A1:D10", exportOptions, destinationPath);
    }
}
```

De overload die we gebruiken schrijft direct naar een bestand (standaard CSV). Als je een string in het geheugen wilt, vervang dan het laatste argument door een `StringWriter` en lees het resultaat daarna.

### Volledig werkend voorbeeld

Hieronder vind je een zelfstandige console‑app die je in een nieuw project kunt plakken en direct kunt uitvoeren (vervang alleen de bestands‑paden).

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License key (free version works with limited rows/columns).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        var exporter = new WorksheetExporter();
        exporter.ExportRange(
            sourcePath: @"C:\Temp\Sample.xlsx",
            destinationPath: @"C:\Temp\ExportedRange.csv");

        Console.WriteLine("Export completed. Check C:\\Temp\\ExportedRange.csv");
    }
}
```

**Verwachte output (CSV‑fragment):**

```
[Header1],[Header2],[Header3],[Header4]
[123],[456],[789],[012]
[ABC],[DEF],[GHI],[JKL]
...
```

Elke cel van *A1* tot en met *D10* staat nu tussen vierkante haakjes, precies zoals we gedefinieerd hebben in de `CellExport`‑handler.

## Veelvoorkomende randgevallen afhandelen  

### 1. Lege cellen  
Als een cel leeg is, is `e.Value` `null`. Proberen het te formatteren met string‑interpolatie veroorzaakt een uitzondering. Bescherm hiertegen:

```csharp
exportOptions.CellExport += (s, e) =>
{
    var raw = e.Value?.ToString() ?? string.Empty;
    e.Value = $"[{raw}]";
};
```

### 2. Grote bereiken  
Het exporteren van miljoenen rijen kan geheugenlimieten raken. In dat geval stream je de output in plaats van de hele werkmap in het geheugen te laden:

```csharp
using (var writer = new StreamWriter(destinationPath))
{
    worksheet.ExportTable(workbook, "A1:D1000000", exportOptions, writer);
}
```

### 3. Verschillende delimiters  
CSV is niet het enige formaat dat je nodig kunt hebben. Verander de delimiter door `ExportTableOptions.CsvSeparator` aan te passen:

```csharp
exportOptions.CsvSeparator = '\t'; // Tab‑delimited
```

## Veelgestelde vragen  

**Q: Werkt dit met .xlsx‑bestanden die zijn aangemaakt door Excel 365?**  
Absoluut. GemBox leest het moderne OpenXML‑formaat zonder extra configuratie.

**Q: Kan ik meerdere niet‑aaneengesloten bereiken tegelijk exporteren?**  
Niet direct via één `ExportTable`‑aanroep. Loop over elke bereik‑string (`"A1:D10"`, `"F1:H5"` etc.) en concateneer de outputs zelf.

**Q: Wat als ik per kolom verschillende opmaak moet toepassen?**  
In de `CellExport`‑handler heb je toegang tot `e.ColumnIndex`. Gebruik een `switch`‑statement om kolomspecifieke logica toe te passen.

## Afsluiting  

We hebben behandeld **hoe je werkbladbereik exporteert** met volledige controle over de weergave van elke cel, laten zien **hoe je excel‑bereik exporteert** met `ExportTableOptions`, en demonstreren **hoe je cel‑export aanpast** via het `CellExport`‑event. De complete oplossing bestaat uit een paar dozijn regels C#, maar is flexibel genoeg voor productie‑scenario's.

Volgende stappen? Vervang de haakjes‑wrapper door een JSON‑vriendelijk formaat, of experimenteer met conditionele logica die verborgen rijen overslaat. Je kunt ook onderzoeken hoe je direct naar een `MemoryStream` exporteert voor web‑API‑responses—geen tijdelijke bestanden nodig.

Als je dit hebt gevolgd, heb je nu een solide, herbruikbaar patroon om elk werkbladbereik exact op de gewenste manier te exporteren. Veel programmeerplezier, en laat gerust een reactie achter als je ergens vastloopt!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}