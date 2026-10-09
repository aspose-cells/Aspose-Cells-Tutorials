---
category: general
date: 2026-03-29
description: Leer hoe je Excel‑tabellen exporteert naar platte tekst, een string naar
  een bestand schrijft en een Excel‑tabel converteert naar CSV of TXT met C#. Inclusief
  volledige code en tips.
draft: false
keywords:
- how to export excel
- write string to file
- convert excel table
- export table as csv
- save txt file c#
language: nl
og_description: Hoe Excel‑tabellen exporteren naar tekstbestanden in C#. Ontvang de
  volledige oplossing, code en best practices voor het converteren van Excel‑tabellen
  en het opslaan van TXT‑bestanden.
og_title: Hoe Excel-gegevens te exporteren – Complete C#-tutorial
tags:
- C#
- Excel
- File I/O
title: Hoe Excel-gegevens te exporteren – Stap‑voor‑stap C#‑gids
url: /nl/net/excel-data-export-retrieval/how-to-export-excel-data-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Excel-gegevens exporteren – Complete C#‑gids

Heb je je ooit afgevraagd **how to export Excel** gegevens zonder de spreadsheet handmatig te openen? Misschien moet je een tabel dumpen naar een simpel tekstbestand voor een legacy‑systeem, of wil je snel een CSV‑export voor data‑analyse‑pijplijnen. In deze tutorial lopen we een praktische, end‑to‑end‑oplossing door die **writes a string to file** en laat je precies zien hoe je **convert Excel table** gegevens omzet naar een gescheiden tekstformaat met C#.

We behandelen alles, van het laden van de werkmap, het kiezen van de juiste tabel, het configureren van exportopties, tot het uiteindelijk opslaan van het resultaat als een `.txt`‑bestand. Aan het einde kun je **export table as CSV** (of elke delimiter die je kiest) en zie je een paar handige trucjes voor **saving txt file C#** projecten. Geen externe tools nodig—alleen een paar NuGet‑pakketten en een beetje code.

---

## Wat je nodig hebt

- **.NET 6.0+** (of .NET Framework 4.7.2 als je de klassieke versie prefereert)
- **Syncfusion.XlsIO** NuGet‑package (de `ExportTableOptions`‑klasse bevindt zich hier)
- Een basis C#‑IDE (Visual Studio, VS Code, Rider—elk werkt)
- Een Excel‑werkmap die minstens één tabel bevat (we gebruiken `ws.Tables[0]` in het voorbeeld)

> Pro tip: Als je de Syncfusion‑bibliotheek nog niet hebt, voer dan  
> `dotnet add package Syncfusion.XlsIO.Net.Core` uit vanaf de commandoregel.

---

## Stap 1 – Open de werkmap en haal de eerste tabel op  

Het eerste is het laden van het Excel‑bestand en een referentie krijgen naar het werkblad dat de tabel bevat. Deze stap is cruciaal omdat de **convert excel table**‑bewerking werkt op een `ITable`‑object, niet op ruwe celbereiken.

```csharp
using Syncfusion.XlsIO;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        // Load the workbook (replace with your actual file path)
        using (ExcelEngine excelEngine = new ExcelEngine())
        {
            IApplication application = excelEngine.Excel;
            application.DefaultVersion = ExcelVersion.Xlsx;

            // Open the file
            FileStream stream = new FileStream(@"C:\Data\Sample.xlsx", FileMode.Open, FileAccess.Read);
            IWorkbook workbook = application.Workbooks.Open(stream);
            IWorksheet ws = workbook.Worksheets[0];   // First worksheet
```

*Waarom dit belangrijk is:* Het openen van de werkmap met `using` zorgt ervoor dat alle unmanaged resources worden vrijgegeven, waardoor later geen bestands‑lock‑problemen ontstaan wanneer je **write string to file** probeert.

---

## Stap 2 – Configureer exportopties (platte tekst, geen kopteksten, puntkomma‑delimiter)  

Nu vertellen we Syncfusion hoe we de tabel willen serialiseren. Met `ExportTableOptions` kun je de opname van kopteksten in- of uitschakelen, een delimiter kiezen en bepalen of je een string of een byte‑array wilt ontvangen.

```csharp
            // Step 2: Configure export options – plain text, omit headers, ';' delimiter
            var exportOptions = new ExportTableOptions
            {
                ExportAsString = true,      // Returns a string we can write directly
                IncludeHeaders = false,     // Skip column headers if you don’t need them
                Delimiter = ";"             // Change to ',' for classic CSV
            };
```

*Waarom dit belangrijk is:* `IncludeHeaders = false` komt vaak overeen met de verwachtingen van downstream‑systemen die de kolomvolgorde al kennen. Het wijzigen van de delimiter is hoe je **export table as CSV** doet met een aangepaste scheidingsteken.

---

## Stap 3 – Exporteer de tabel naar een string  

Met de opties klaar, roepen we `ExportToString` aan. Deze methode haalt de volledige tabel (inclusief alle rijen) op en retourneert een enkele string die klaar is voor bestandsoutput.

```csharp
            // Step 3: Export the first table to a string using the configured options
            ITable firstTable = ws.Tables[0];               // Access the first table
            string tableText = firstTable.ExportToString(exportOptions);
```

*Waarom dit belangrijk is:* De `ExportToString`‑aanroep doet het zware werk van het omzetten van het Excel‑rooster naar een gescheiden formaat. Het respecteert de `Delimiter` die je hebt ingesteld, zodat je een nette **export table as csv**‑resultaat krijgt zonder extra verwerking.

---

## Stap 4 – Schrijf de geëxporteerde tekst naar een bestand  

Tot slot slaan we de string op schijf op. `File.WriteAllText` is de eenvoudigste manier om **save txt file C#** uit te voeren; het maakt het bestand automatisch aan als het niet bestaat en overschrijft het anders.

```csharp
            // Step 4: Write the exported text to a file
            string outputPath = @"C:\Data\ExportedTable.txt";
            File.WriteAllText(outputPath, tableText);
            System.Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

*Waarom dit belangrijk is:* Door de string direct te schrijven, vermijd je een extra conversiestap. Het bestand bevat nu rijen zoals `Value1;Value2;Value3`, klaar voor elke downstream‑parser.

---

## Volledig werkend voorbeeld (alle stappen op één plek)  

Hieronder vind je het complete, kant‑klaar‑te‑kopiëren programma dat alles combineert wat we hebben besproken. Het bevat foutafhandeling en commentaar voor duidelijkheid.

```csharp
using Syncfusion.XlsIO;
using System;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load workbook and get first worksheet
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication app = excelEngine.Excel;
                app.DefaultVersion = ExcelVersion.Xlsx;

                string sourcePath = @"C:\Data\Sample.xlsx";
                using (FileStream fs = new FileStream(sourcePath, FileMode.Open, FileAccess.Read))
                {
                    IWorkbook wb = app.Workbooks.Open(fs);
                    IWorksheet ws = wb.Worksheets[0]; // first sheet

                    // 2️⃣ Set export options (plain text, no headers, ';' delimiter)
                    var opts = new ExportTableOptions
                    {
                        ExportAsString = true,
                        IncludeHeaders = false,
                        Delimiter = ";"
                    };

                    // 3️⃣ Export the first table to a string
                    ITable table = ws.Tables[0];
                    string csvText = table.ExportToString(opts);

                    // 4️⃣ Save the string to a .txt file
                    string destPath = @"C:\Data\ExportedTable.txt";
                    File.WriteAllText(destPath, csvText);

                    Console.WriteLine($"✅ Export complete! File saved at: {destPath}");
                }
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

**Verwachte output** (de inhoud van `ExportedTable.txt`):

```
John;Doe;35
Jane;Smith;28
Bob;Brown;42
```

Elke regel komt overeen met een rij uit de oorspronkelijke Excel‑tabel, met waarden gescheiden door puntkomma’s. Als je `Delimiter = ","` verandert, krijg je in plaats daarvan een klassiek CSV‑bestand.

---

## Veelgestelde vragen & randgevallen  

### Wat als mijn werkmap meerdere tabellen bevat?  
Je kunt simpelweg `ws.Tables[0]` vervangen door de juiste index, of door `ws.Tables` te itereren:

```csharp
foreach (var tbl in ws.Tables)
{
    string txt = tbl.ExportToString(opts);
    // Save each table to a separate file or concatenate as needed
}
```

### Hoe neem ik kolomkoppen op?  
Stel `IncludeHeaders = true` in `ExportTableOptions`. Handig wanneer het downstream‑systeem een header‑rij verwacht.

### Kan ik dynamisch naar een andere map exporteren?  
Zeker. Gebruik `Path.Combine` met `Environment.GetFolderPath(Environment.SpecialFolder.Desktop)` of een door de gebruiker opgegeven pad om de oplossing flexibeler te maken.

### Hoe zit het met grote bestanden?  
Voor enorme tabellen kun je overwegen de output te streamen in plaats van de volledige string in het geheugen te laden:

```csharp
using (StreamWriter writer = new StreamWriter(outputPath))
{
    writer.Write(table.ExportToString(opts));
}
```

### Werkt dit op .NET Core?  
Ja—Syncfusion.XlsIO ondersteunt .NET 5/6/7. Verwijs gewoon naar het juiste NuGet‑package en je bent klaar om te gaan.

---

## Pro‑tips voor betrouwbare exports  

- **Validate the file path** voordat je schrijft. Een ontbrekende map veroorzaakt een `DirectoryNotFoundException`.  
- **Check `ExportAsString`** alleen wanneer de tabel comfortabel in het geheugen past; gebruik anders `ExportToStream` voor enorme datasets.  
- **Mind the culture**: als je gegevens komma’s bevatten als decimale scheidingstekens, kies dan een puntkomma (`;`) of tab (`\t`) als delimiter om CSV‑parsing‑fouten te voorkomen.  
- **Version lock**: Syncfusion wijzigt af en toe API‑handtekeningen. Pin de NuGet‑versie (`<PackageReference Include="Syncfusion.XlsIO.Net.Core" Version="21.2.0.44" />`) om je build reproduceerbaar te houden.

---

## Conclusie  

In deze gids hebben we laten zien **how to export Excel** tabellen naar platte‑tekstbestanden met C#. Door de werkmap te laden, `ExportTableOptions` te configureren, de tabel naar een string te exporteren en tenslotte **writes the string to file**, heb je nu een robuust patroon voor **convert excel table**‑data, **export table as csv**, en **save txt file C#**‑taken.  

Voel je vrij om te experimenteren—verander de delimiter, neem kopteksten op, of loop over meerdere tabellen. dezelfde aanpak werkt voor het genereren van CSV‑rapporten, het voeden van data naar legacy‑parsers, of simpelweg het archiveren van spreadsheet‑inhoud als lichte tekstbestanden.

Heb je meer scenario’s die je wilt aanpakken? Misschien moet je **write string to file** asynchroon doen, of wil je de output on‑the‑fly zippen. Bekijk onze volgende tutorials over *asynchronous file I/O in C#* en *zipping files with .NET* om de voortgang vast te houden.

Veel plezier met coderen! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}