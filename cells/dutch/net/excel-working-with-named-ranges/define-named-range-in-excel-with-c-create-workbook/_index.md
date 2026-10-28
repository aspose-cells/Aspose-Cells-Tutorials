---
category: general
date: 2026-08-07
description: Definieer een benoemd bereik in Excel met C# en leer hoe je een tabel
  aan een werkblad toevoegt, waarna je het werkboek programmatisch opslaat als bestand.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define named range excel
- save workbook to file
- add named range excel
- add table to worksheet
- create excel workbook programmatically
language: nl
lastmod: 2026-08-07
og_description: Definieer een benoemd bereik in Excel met C# en zie hoe je een tabel
  kunt toevoegen, een werkmap programmatically kunt maken en de werkmap in één stroom
  naar een bestand kunt opslaan.
og_image_alt: Screenshot of C# code that creates an Excel workbook, adds a table,
  defines a named range, and saves the file
og_title: Definieer een naamgebied in Excel met C# – volledige werkboekhandleiding
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Define named range in Excel with C# and learn how to add a table to
    a worksheet, then save workbook to file programmatically.
  headline: Define named range in Excel with C# – create workbook
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- named range
- programmatic Excel
title: Definieer een benoemd bereik in Excel met C# – werkmap maken
url: /nl/net/excel-working-with-named-ranges/define-named-range-in-excel-with-c-create-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definieer een named range in Excel met C# – werkmap maken

Als je een **named range in Excel** vanuit C#-code moet definiëren, laat deze tutorial je precies zien hoe je dat doet. Je ziet ook hoe je een **tabel aan een werkblad toevoegt**, de werkmap **programmatically** maakt, en uiteindelijk de **save workbook to file** opslaat zonder de IDE te verlaten.

Werken met Excel‑bestanden programmatically bespaart tijd, elimineert handmatige fouten en maakt geautomatiseerde rapportage‑pijplijnen mogelijk. In deze gids leer je:

* Een nieuwe Excel‑werkmap vanaf nul maken.  
* Een tabel toevoegen die een specifiek celbereik beslaat.  
* Een named range definiëren en naamconflicten afhandelen.  
* De werkmap op schijf opslaan.

Alle stappen gebruiken de **Aspose.Cells for .NET**‑bibliotheek, die werkt met .NET 6+ en .NET Framework 4.6+. Er is geen extra COM‑interop of Office‑installatie vereist.

## Vereisten

* .NET 6 SDK (of .NET Framework 4.6+).  
* Visual Studio 2022 of een andere C#‑compatibele IDE.  
* Aspose.Cells for .NET NuGet‑pakket (`Install-Package Aspose.Cells`).  

> **Pro tip:** Gebruik de gratis evaluatielicentie tijdens het testen; vervang deze door een productielicentie vóór de uitrol.

## Stap 1: Excel‑werkmap programmatically maken

De eerste handeling is het instantieren van een `Workbook`‑object. Dit object vertegenwoordigt het volledige Excel‑bestand in het geheugen.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook in memory
        Workbook workbook = new Workbook();               // create an empty workbook
        Worksheet worksheet = workbook.Worksheets[0];    // get the first (default) worksheet
```

*Waarom dit belangrijk is*: Het maken van de werkmap in code geeft je volledige controle over bladen, stijlen en data voordat er een bestand naar de schijf wordt geschreven.

## Stap 2: Tabel aan werkblad toevoegen

Een tabel (ook wel ListObject genoemd) biedt ingebouwde filter‑, sorteer‑ en stijlfuncties. Hier maken we een tabel die de cellen **A1:B5** bestrijkt en geven we deze de naam **SalesData**.

```csharp
        // Step 2: Define a range and convert it into a table
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Populate the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");
        worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");
        worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries");
        worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");
        worksheet.Cells["B5"].PutValue(30);
```

*Waarom dit belangrijk is*: Het vroegtijdig toevoegen van een tabel stelt je in staat later te refereren aan de data met een **named range**, en de gestructureerde referentie van de tabel kan in formules worden gebruikt.

## Stap 3: Named range excel definiëren – conflicten afhandelen

Een **named range** is een identifier die naar een cel of bereik wijst, waardoor formules makkelijker leesbaar worden. Als een naam al bestaat (bijvoorbeeld de tabelnaam **SalesData**), geeft Excel een conflict. De onderstaande code laat zien hoe je die uitzondering opvangt en veilig doorgaat.

```csharp
        // Step 3: Attempt to define a named range with the same identifier as the table
        try
        {
            // This will raise an exception because "SalesData" is already used by the table
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Step 4: Add a different named range – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";
```

*Waarom dit belangrijk is*: Het afhandelen van naamconflicten voorkomt runtime‑crashes in geautomatiseerde taken. De tweede named range **SalesTotal** toont hoe je de kolom van de tabel in een formule kunt refereren.

## Stap 4: Werkmap opslaan naar bestand

Na alle aanpassingen de werkmap naar schijf persisteren. De `Save`‑methode ondersteunt vele formaten; hier gebruiken we de standaard `.xlsx`.

```csharp
        // Step 5: Save the workbook to the file system
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

*Waarom dit belangrijk is*: Het programmatically **save workbook to file** maakt batch‑verwerking, geplande rapportgeneratie en integratie met web‑API’s mogelijk.

## Volledige broncode in één weergave

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Add a table covering A1:B5 and name it "SalesData"
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Fill the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");   worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");  worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries"); worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");    worksheet.Cells["B5"].PutValue(30);

        // Try to create a defined name with the same identifier – handle the conflict
        try
        {
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Add a different defined name – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";

        // Save the workbook
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

### Verwacht resultaat

* Een Excel‑bestand met de naam **NameConflictHandled.xlsx** verschijnt in `C:\Temp`.  
* Blad 1 bevat een opgemaakte tabel **SalesData** met product‑eenheid‑rijen.  
* Cel **B6** toont de som van de kolom **Units**, berekend via de named range **SalesTotal**.  
* De console geeft een bericht over het naamconflict (indien aanwezig) en bevestigt de bestandslocatie.

## Veelgestelde vragen & randgevallen

| Vraag | Antwoord |
|----------|--------|
| **Kan ik een named range definiëren die zich over meerdere werkbladen uitstrekt?** | Ja. Gebruik `worksheet.Names.Add("GlobalRange", "'Sheet1'!A1:B5")` en refereer er vanaf elk blad naar. |
| **Wat als ik een bestaand bestand moet overschrijven?** | Roep `workbook.Save(path, SaveFormat.Xlsx, new SaveOptions { Overwrite = true })` aan. |
| **Hoe voeg ik een named range toe zonder conflict wanneer de naam al bestaat?** | Gebruik `worksheet.Names.Remove("ExistingName")` vóór het toevoegen, of genereer een unieke identifier (bijv. `Guid.NewGuid().ToString("N")`). |
| **Is er een manier om automatisch een stijl op de tabel toe te passen?** | Stel `table.Style = workbook.Styles[BuiltInStyleId.TableStyleMedium9];` in na het aanmaken van de tabel. |
| **Werkt dit op .NET Core?** | Aspose.Cells ondersteunt .NET Core, .NET 5/6/7, en .NET Framework. Verwijs gewoon naar hetzelfde NuGet‑pakket. |

## Conclusie

Je weet nu hoe je een **named range in Excel** kunt definiëren met C#, een **tabel aan een werkblad** kunt toevoegen, en een **workbook to file** programmatically kunt opslaan. Het volledige voorbeeld toont het maken van een Excel‑werkmap vanaf nul, het afhandelen van naamconflicten, en het genereren van een bruikbaar rapportbestand in één herhaalbare workflow.

Verken vervolgens gerelateerde onderwerpen zoals **grafieken aan een werkblad toevoegen**, **exporteren naar PDF**, of **bestaande werkmappen lezen**. Elk van deze bouwt voort op dezelfde basisprincipes die hier behandeld zijn, zodat je klaar bent om de oplossing uit te breiden naar complexere automatiseringsscenario's. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Maak een benoemd bereik van cellen in Excel](/cells/english/net/excel-creating-formatting-named-ranges/create-named-range-of-cells/)
- [Hoe Named Range‑formules te implementeren in .NET met Aspose.Cells voor Excel‑automatisering](/cells/english/net/formulas-functions/implement-named-range-formulas-net-aspose-cells/)
- [Hoe Workbook‑scoped Named Ranges te maken in Excel met Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}