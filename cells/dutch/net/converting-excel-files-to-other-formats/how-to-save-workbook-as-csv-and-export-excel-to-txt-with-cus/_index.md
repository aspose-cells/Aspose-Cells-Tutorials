---
category: general
date: 2026-09-15
description: Leer hoe je een werkmap opslaat als CSV, Excel exporteert naar TXT, en
  een aangepast getalformaat toepast terwijl je celwaarden naar hoofdletters converteert
  in C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as csv
- apply custom number format
- export excel to txt
- uppercase cell values
- export worksheet as text
language: nl
lastmod: 2026-09-15
og_description: Sla werkmap op als CSV, exporteer Excel naar TXT en pas een aangepast
  getalformaat toe terwijl je celwaarden omzet naar hoofdletters met Aspose.Cells
  in C#.
og_image_alt: Screenshot showing workbook saved as CSV using C# code
og_title: Werkmap opslaan als CSV en Excel exporteren naar TXT met aangepaste opmaak
  in C#
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to save workbook as CSV, export Excel to TXT, and apply custom
    number format while converting cell values to uppercase in C#.
  headline: How to save workbook as CSV and export Excel to TXT with custom formatting
    in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hoe een werkmap opslaan als CSV en Excel exporteren naar TXT met aangepaste
  opmaak in C#
url: /nl/net/converting-excel-files-to-other-formats/how-to-save-workbook-as-csv-and-export-excel-to-txt-with-cus/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een werkmap op te slaan als CSV en Excel te exporteren naar TXT met aangepaste opmaak in C#

Als je **werkmap opslaan als CSV** moet doen terwijl je ook een werkblad exporteert als platte‑tekst en een aangepast getalformaat toepast, laat deze gids je een complete, kant‑klaar oplossing zien. Je ziet hoe je numerieke precisie behoudt, elke celwaarde naar hoofdletters converteert en Japanse‑éra datums verwerkt — allemaal met Aspose.Cells voor .NET.

Gegevens exporteren uit Excel betekent vaak dat je met verschillende formaten moet omgaan: CSV voor gegevensuitwisseling, TXT voor legacy‑systemen en aangepaste getalformaten voor locale‑specifieke rapportage. Deze tutorial loopt stap‑voor‑stap door elke vereiste, zodat je de code direct in je project kunt kopiëren.

In de volgende secties leer je hoe je:

* **werkmap opslaan als csv** met een gedefinieerd aantal significante cijfers  
* **excel exporteren naar txt** terwijl **hoofdlettercelwaarden** worden afgedwongen  
* **aangepast getalformaat toepassen** voor Japanse‑éra datums en het opgemaakte resultaat lezen  

Er zijn geen externe tools nodig — alleen de Aspose.Cells‑bibliotheek en een .NET‑ontwikkelomgeving.

## Vereisten

* .NET 6.0 of later (de code werkt ook met .NET Framework 4.8)  
* Aspose.Cells voor .NET (NuGet‑pakket `Aspose.Cells`)  
* Basiskennis van C# en Excel‑concepten  

---

## Stap 1: Werkmap opslaan als CSV met gecontroleerde precisie

Wanneer je **werkmap opslaan als CSV**, worden numerieke waarden weggeschreven met de standaard tekenreeksrepresentatie, waardoor precisie kan verloren gaan. Door `CsvSaveOptions.SignificantDigits` te configureren, geef je Aspose.Cells aan hoeveel significante cijfers behouden moeten blijven.

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (or load an existing one)
Workbook workbook = new Workbook();               // you can also use new Workbook("input.xlsx");

// Configure CSV options to keep up to 4 significant digits
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    SignificantDigits = 4   // ensures numbers like 123.4567 stay precise
};

// Save the workbook as CSV
string csvPath = @"C:\Temp\Digits.csv";
workbook.Save(csvPath, csvOptions);

Console.WriteLine($"Workbook saved as CSV to {csvPath}");
```

**Waarom dit belangrijk is:**  
Het instellen van `SignificantDigits` voorkomt afrondingsfouten die vaak optreden wanneer grote datasets worden uitgewisseld met downstream‑systemen (bijv. data‑warehouses). Het `CsvSaveOptions`‑object laat je ook delimiters, codering en andere CSV‑specifieke instellingen beheren indien nodig.

---

## Stap 2: Een werkblad exporteren als platte tekst terwijl waarden naar hoofdletters worden geconverteerd

Een blad exporteren naar een eenvoudig `.txt`‑bestand is handig voor legacy‑importroutines die gegevens verwachten die door witruimte zijn gescheiden. Door `ExportTableOptions.ExportAsString` in te schakelen en een `CustomExport`‑delegate te leveren, kun je **excel exporteren naar txt** en tegelijkertijd **hoofdlettercelwaarden** afdwingen.

```csharp
// Prepare export options for plain‑text output
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true, // forces every cell to be treated as a string
    // CustomExport receives the cell and its current string value,
    // allowing you to modify it before it is written.
    CustomExport = (cell, value) =>
    {
        // Convert the cell value to an upper‑case string
        return value?.ToString().ToUpperInvariant();
    }
};

// Define the output path for the text file
string txtPath = @"C:\Temp\Table.txt";

// Export the first worksheet (index 0) as a tab‑delimited text file
workbook.Worksheets[0].ExportTable(txtPath, tableOptions);

Console.WriteLine($"Worksheet exported as text to {txtPath}");
```

**Waarom dit belangrijk is:**  
Veel integratiepunten (bijv. mainframe‑batchtaken) verwachten hoofdletter‑identifiers. De `CustomExport`‑callback geeft je volledige controle over de weergave van elke cel, zodat je transformaties zoals trimmen, opvullen of locale‑specifieke opmaak kunt injecteren zonder nabewerking van het bestand.

---

## Stap 3: Een aangepast getalformaat toepassen en het opgemaakte resultaat lezen

De ingebouwde getalformaten van Excel dekken de meeste gevallen, maar soms moet je datums weergeven in een specifiek kalendersysteem — zoals de Japanse era. De volgende code laat zien hoe je **aangepast getalformaat toepast** op een cel en vervolgens de opgemaakte tekenreeks leest die rekening houdt met de locale van de werkmap.

```csharp
// Create a new workbook for the era example
Workbook eraWorkbook = new Workbook();

// Access the first worksheet and target cell A1
Worksheet sheet = eraWorkbook.Worksheets[0];
Cell dateCell = sheet.Cells["A1"];

// Insert a Japanese‑era date string (Reiwa 3 = 2021)
dateCell.PutValue("Reiwa 3/04/01");

// Apply a built‑in date number format (14 = mm-dd-yy)
// You could also assign a custom format string, e.g., "[$-ja-JP]ggge年m月d日"
Style style = eraWorkbook.CreateStyle();
style.Number = 14; // standard short date format
dateCell.SetStyle(style);

// Force formula calculation (necessary if the cell contains a formula)
eraWorkbook.CalculateFormula();

// Retrieve the formatted string as it would appear in Excel
string formattedDate = dateCell.StringValue;
Console.WriteLine($"Formatted date (locale aware): {formattedDate}");
```

**Waarom dit belangrijk is:**  
Het gebruik van `SetStyle` met een getalformaat zorgt ervoor dat de weergave van de cel de regionale instellingen respecteert, wat cruciaal is voor rapporten die over verschillende locales worden verspreid. Wanneer je later `StringValue` leest, krijg je exact de tekenreeks die een gebruiker in de Excel‑UI zou zien, waardoor handmatige parsing overbodig wordt.

---

## Volledig, uitvoerbaar voorbeeld

Hieronder staat een enkel programma dat de drie stappen combineert. Plak het in een nieuw Console‑App‑project, voeg het Aspose.Cells‑NuGet‑pakket toe en voer het uit.

```csharp
using Aspose.Cells;
using System;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Save workbook as CSV ----------
            Workbook workbook = new Workbook(); // start with a fresh workbook
            // (Optionally load an existing file: new Workbook("input.xlsx"))

            // Populate some sample data
            workbook.Worksheets[0].Cells["A1"].PutValue(123.456789);
            workbook.Worksheets[0].Cells["B1"].PutValue("Sample Text");

            CsvSaveOptions csvOptions = new CsvSaveOptions
            {
                SignificantDigits = 4
            };
            string csvPath = @"C:\Temp\Digits.csv";
            workbook.Save(csvPath, csvOptions);
            Console.WriteLine($"Saved CSV to {csvPath}");

            // ---------- Step 2: Export worksheet as text with uppercase ----------
            ExportTableOptions tableOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, value) => value?.ToString().ToUpperInvariant()
            };
            string txtPath = @"C:\Temp\Table.txt";
            workbook.Worksheets[0].ExportTable(txtPath, tableOptions);
            Console.WriteLine($"Exported TXT to {txtPath}");

            // ---------- Step 3: Apply custom number format ----------
            Workbook eraWorkbook = new Workbook();
            Cell dateCell = eraWorkbook.Worksheets[0].Cells["A1"];
            dateCell.PutValue("Reiwa 3/04/01");

            Style eraStyle = eraWorkbook.CreateStyle();
            eraStyle.Number = 14; // short date format; replace with custom if needed
            dateCell.SetStyle(eraStyle);
            eraWorkbook.CalculateFormula();

            Console.WriteLine($"Japanese era date formatted: {dateCell.StringValue}");
        }
    }
}
```

**Verwachte output**

```
Saved CSV to C:\Temp\Digits.csv
Exported TXT to C:\Temp\Table.txt
Japanese era date formatted: 4/1/2021
```

(Het exacte datumformaat kan variëren afhankelijk van de locale‑instellingen van je systeem.)

---

## Veelgestelde vragen en afhandeling van randgevallen

| Vraag | Antwoord |
|----------|--------|
| *Wat als ik een andere scheidingsteken in de CSV nodig heb?* | Stel `csvOptions.Separator` in op `','`, `'\t'` of elk aangepast teken voordat je `Save` aanroept. |
| *Kan ik de oorspronkelijke numerieke precisie behouden in plaats van afronden?* | Gebruik `SignificantDigits = 0` om de volledige double‑precisiewaarde te schrijven, of stel `NumberDecimalSeparator` in voor locale‑specifieke decimale symbolen. |
| *Hoe exporteer ik alleen een specifiek bereik in plaats van het hele blad?* | Roep `ExportTable(string fileName, ExportTableOptions options, CellArea area)` aan en geef een `CellArea` door die het bereik definieert. |
| *Wat als de werkmap formules bevat die naar andere bladen verwijzen?* | Zorg ervoor dat je `workbook.CalculateFormula()` aanroept vóór het exporteren; anders krijg je de gecachte waarden. |
| *Is er een manier om de oorspronkelijke celopmaak (lettertypen, kleuren) te behouden in het TXT‑bestand?* | Platte‑tekstformaten kunnen visuele styling niet behouden. Als je rijke opmaak nodig hebt, overweeg dan export naar HTML (`HtmlSaveOptions`). |

---

## Conclusie

Je weet nu hoe je **werkmap opslaan als CSV** met gecontroleerde precisie, **excel exporteren naar TXT** terwijl je **hoofdlettercelwaarden** afdwingt, en **aangepast getalformaat** toepast voor locale‑bewuste datumweergave. Elk fragment staat op zichzelf, werkt direct uit de doos en volgt best practices voor zowel prestaties als onderhoudbaarheid.

Vervolgens kun je verkennen:

* Het gebruik van `HtmlSaveOptions` om styling te behouden bij export naar web‑vriendelijke formaten.  
* Het benutten van `CsvSaveOptions.Encoding` voor UTF‑8 of andere tekensets bij het werken met meertalige gegevens.  
* Het automatiseren van batch‑verwerking van meerdere werkbladen door te itereren over `workbook.Worksheets`.

Voel je vrij de code aan te passen aan je eigen datastromen, en laat de flexibiliteit van Aspose.Cells het zware werk doen.

---


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Save Workbook To Text Csv Format](/cells/german/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)
- [Save Workbook To Text Csv Format](/cells/french/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)
- [Save Workbook To Text Csv Format](/cells/spanish/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}