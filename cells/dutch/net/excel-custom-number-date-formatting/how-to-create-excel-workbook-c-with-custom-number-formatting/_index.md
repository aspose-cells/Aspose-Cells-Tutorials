---
category: general
date: 2026-10-01
description: Leer hoe je een Excel-werkmap maakt in C# en een aangepast getalformaat
  toepast, het aantal decimalen van een cel instelt, en de werkmap opslaat als XLSX
  in een volledige stapsgewijze handleiding.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: nl
lastmod: 2026-10-01
og_description: Maak een Excel-werkboek in C# met een aangepast getalformaat, stel
  het aantal decimalen van de cel in en sla het werkboek op als XLSX. Volg deze volledige
  handleiding voor nauwkeurige numerieke output.
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: Excel-werkmap maken C# – aangepast getalformaat & XLSX-export
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  headline: How to create Excel workbook C# with custom number formatting
  type: TechArticle
- description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  name: How to create Excel workbook C# with custom number formatting
  steps:
  - name: Run the program (`dotnet run`).
    text: Run the program (`dotnet run`).
  - name: Open `SigDigits.xlsx`.
    text: Open `SigDigits.xlsx`.
  - name: Confirm that **A1** reads `123.5`.
    text: Confirm that **A1** reads `123.5`.
  - name: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
    text: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Hoe een Excel-werkboek te maken in C# met aangepaste getalopmaak
url: /nl/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een Excel-werkmap C# te maken met aangepaste getalopmaak

Als je een **excel workbook c#** moet maken die getallen precies weergeeft zoals je wilt, laat deze gids je zien hoe je dat in een paar duidelijke stappen doet. Je leert een aangepaste getalopmaak toe te passen, het aantal decimalen van een cel in te stellen, en uiteindelijk **workbook opslaan als xlsx** voor downstream gebruik.

Werken met numerieke data betekent vaak een balans vinden tussen precisie en leesbaarheid. Aan het einde van deze tutorial heb je een herbruikbaar patroon dat het aantal weergegeven cijfers beperkt tot een specifiek aantal significante cijfers, terwijl de oorspronkelijke waarde in het bestand behouden blijft. Er zijn geen externe scripts nodig—alleen C# en de Aspose.Cells‑bibliotheek.

## Vereisten

* .NET 6.0 SDK of later geïnstalleerd  
* Visual Studio 2022 (of een andere C# IDE)  
* Het **Aspose.Cells for .NET** NuGet‑pakket (`Install-Package Aspose.Cells`) – deze bibliotheek levert de `Workbook`, `Worksheet` en `ExportTableOptions` klassen die in de voorbeelden worden gebruikt.  

Deze vereisten zijn minimaal; dezelfde code werkt in .NET Core, .NET Framework en zelfs in Azure Functions.

## Stap 1: Excel workbook C# maken – het bestand initialiseren

De eerste handeling is het instantiëren van een nieuw `Workbook`‑object. Dit object vertegenwoordigt het volledige Excel‑bestand in het geheugen en bevat automatisch een standaard werkblad.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // creates an empty .xlsx container
            Worksheet sheet = workbook.Worksheets[0];         // reference to the default sheet
```

**Waarom dit belangrijk is:**  
Het vooraf aanmaken van de werkmap geeft je een schoon canvas. Het standaard werkblad (`Worksheets[0]`) is klaar voor gegevensinvoer, dus je hoeft geen nieuw blad toe te voegen tenzij je scenario meerdere tabbladen vereist.

## Stap 2: Een numerieke waarde naar een cel schrijven

Plaats nu een voorbeeldgetal in cel **A1**. De waarde die we gebruiken (`123.456789`) bevat meer decimalen dan we uiteindelijk willen weergeven, waardoor we later afronding kunnen demonstreren.

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**Tip:** `PutValue` detecteert automatisch het gegevenstype, zodat je het getal niet naar een string hoeft te converteren.

## Stap 3: Aangepaste getalopmaak toepassen – zichtbare decimalen beperken

Om te bepalen hoe Excel het getal weergeeft, maken we een `Style` met een **aangepaste getalopmaak**. Het patroon `"0.######"` vertelt Excel om tot zes decimalen weer te geven maar achterliggende nullen weg te laten.

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**Hoe dit werkt:**  
De opmaakstring volgt de aangepaste‑opmaaksyntaxis van Excel. `0` dwingt een cijfer af, terwijl `#` een cijfer alleen weergeeft als het significant is. Door ze te combineren krijg je een flexibele weergave die nog steeds de oorspronkelijke precisie respecteert.

## Stap 4: Celdecimalen instellen – met ExportTableOptions

Als je **celdecimalen moet instellen** voor geëxporteerde data (bijv. bij conversie naar een DataTable), laat Aspose.Cells je het aantal **significante cijfers** opgeven. Deze stap zorgt ervoor dat de geëxporteerde CSV of DataTable dezelfde afrondingsregels respecteert als in de werkmap toegepast.

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**Waarom `SignificantDigits` gebruiken?**  
In tegenstelling tot een vast aantal decimalen behouden significante cijfers de grootte van het getal terwijl ze de precisie beperken, wat vaak is wat analisten verwachten bij het samenvatten van data.

## Stap 5: De werkbladdata exporteren en **workbook opslaan als xlsx**

Tot slot exporteer je de data (als je een DataTable nodig hebt) en sla je de werkmap op schijf op. De `ExportDataTable`‑aanroep respecteert de `ExportTableOptions` die we hebben geconfigureerd, en `workbook.Save` schrijft een standaard XLSX‑bestand.

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**Verwacht resultaat:**  
Wanneer je *SigDigits.xlsx* in Excel opent, toont cel **A1** `123.5`. De onderliggende waarde blijft `123.456789`, maar het weergegeven getal respecteert de 4‑significante‑cijfer‑regel. Als je het blad exporteert naar een DataTable, wordt de waarde in de tabel ook afgerond naar `123.5`.

---

## Aangepaste getalopmaak toepassen op extra cellen

Als je een bereik in plaats van één cel wilt opmaken, hergebruik dan het `Style`‑object:

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**Pro tip:** Het hergebruiken van een style‑object vermindert het geheugenverbruik en garandeert consistente opmaak over het hele blad.

## Hoe getallen opmaken in Excel met C# – veelvoorkomende variaties

| Scenario | Format string | Result |
|----------|---------------|--------|
| Vaste twee decimalen | `"0.00"` | `123.46` |
| Valuta (VS) | `"$#,##0.00"` | `$123.46` |
| Percentage met één decimaal | `"0.0%"` | `12,346.0%` |
| Wetenschappelijke notatie | `"0.00E+00"` | `1.23E+02` |

Kies het patroon dat past bij je rapportage‑eisen. Alle patronen zijn compatibel met de eerder getoonde `Style.Custom`‑eigenschap.

## Celdecimalen dynamisch instellen op basis van gebruikersinvoer

Soms is de vereiste precisie niet bekend tijdens het compileren. Je kunt de opmaakstring tijdens runtime samenstellen:

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**Randgeval:** Als `decimals` nul is, wordt de opmaak `"0"` (geheel getal). Valideer altijd de gebruikersinvoer om misvormde opmaakstrings te voorkomen.

## Werkmap opslaan als XLSX – best practices

* **Gebruik absolute paden** bij het schrijven naar een bekende map (`Path.Combine(Environment.CurrentDirectory, "output.xlsx")`).  
* **Dispose** de `Workbook` als je deze in een `using`‑statement wikkelt om onbeheerste resources direct vrij te geven:

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **Versie‑compatibiliteit:** Aspose.Cells schrijft bestanden die compatibel zijn met Excel 2010‑2023, zodat downstream‑gebruikers geen opmaakproblemen ondervinden.

---

## Volledig werkend voorbeeld

Hieronder staat het volledige programma dat je direct kunt kopiëren, plakken en uitvoeren. Het bevat alle benodigde `using`‑directieven, commentaren en foutafhandeling.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Create workbook and get the first worksheet
                Workbook workbook = new Workbook();
                Worksheet sheet = workbook.Worksheets[0];

                // 2️⃣ Write a high‑precision number to A1
                sheet.Cells[0, 0].PutValue(123.456789);

                // 3️⃣ Apply a custom number format (up to 6 decimals)
                Style customStyle = workbook.CreateStyle();
                customStyle.Custom = "0.######";
                sheet.Cells[0, 0].SetStyle(customStyle);

                // 4️⃣ Configure export options for 4 significant digits
                ExportTableOptions exportOptions = new ExportTableOptions
                {
                    SignificantDigits = 4
                };

                // 5️⃣ Export data (optional) and save the workbook as XLSX
                sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
                string outputPath = Path.Combine(Environment.CurrentDirectory, "SigDigits.xlsx");
                workbook.Save(outputPath);

                Console.WriteLine($"Workbook saved successfully at: {outputPath}");
                Console.WriteLine("Cell A1 displays: " + sheet.Cells["A1"].StringValue);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error creating workbook: {ex.Message}");
            }
        }
    }
}
```

**Verificatiestappen**

1. Voer het programma uit (`dotnet run`).  
2. Open `SigDigits.xlsx`.  
3. Controleer dat **A1** `123.5` weergeeft.  
4. Als je de XML van het bestand opent (`.xlsx` is een zip‑archief), zie je de aangepaste opmaak `"0.######"` opgeslagen in het `s`‑attribuut van het `<c>`‑element.

## Conclusie

In deze tutorial heb je geleerd hoe je **excel workbook c#** maakt, **aangepaste getalopmaak toepast**, **celdecimalen instelt**, en **workbook opslaat als xlsx** met Aspose.Cells. De oplossing toont zowel visuele opmaak binnen Excel als data‑exportafronding via `ExportTableOptions`.  

Vanaf hier kun je:

* De aanpak uitbreiden naar volledige bereiken of tabellen.  
* Meerdere stijlen (lettertypen, randen) combineren met `StyleFlag`.  
* Rapportgeneratie automatiseren door over gegevensbronnen te itereren en dezelfde opmaaklogica toe te passen.

Voel je vrij om te experimenteren met verschillende opmaakstrings, decimalen of exportopties om aan je specifieke rapportagebehoeften te voldoen. Veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Excel-werkmap maken C# – Valuta‑opmaak toepassen en DataTable importeren](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Excel-werkmap maken C# – Stapsgewijze gids met voorwaardelijke opmaak](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [Excel-werkmap maken C# – Opmerking toevoegen & opslaan als XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}