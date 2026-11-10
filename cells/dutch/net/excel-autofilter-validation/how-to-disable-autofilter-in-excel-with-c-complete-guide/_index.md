---
category: general
date: 2026-10-26
description: autofilter uitschakelen in Excel met C#. Deze tutorial laat zien hoe
  je autofilter van een Excel‑tabel programmeermatig verwijdert en bevat een volledig
  werkend voorbeeld.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- disable autofilter in excel
- remove autofilter from excel table
- Excel automation C#
- Aspose.Cells filter handling
- programmatic Excel editing
language: nl
lastmod: 2026-10-26
og_description: Schakel autofilter in Excel snel uit. Volg deze gids om autofilter
  uit een Excel-tabel te verwijderen met C# en Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet where the autofilter has been disabled
og_title: Uitschakelen van autofilter in Excel met C# – stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  headline: How to disable autofilter in Excel with C# – complete guide
  type: TechArticle
- description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  name: How to disable autofilter in Excel with C# – complete guide
  steps:
  - name: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
    text: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
  - name: Click any column header – you should **not** see the drop‑down filter arrow.
    text: Click any column header – you should **not** see the drop‑down filter arrow.
  - name: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
    text: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Hoe het autofilter in Excel uitschakelen met C# – volledige gids
url: /nl/net/excel-autofilter-validation/how-to-disable-autofilter-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe autofilter in Excel uitschakelen met C# – volledige gids

Als je **autofilter in Excel** moet **uitschakelen**, laat deze gids je precies zien hoe je dat vanuit C# doet. Of je nu een rapport opschoont vóór publicatie of een data‑export‑pipeline automatiseert, het verwijderen van de filter zorgt ervoor dat het werkblad elke rij weergeeft. Je leert ook hoe je **autofilter van een Excel‑tabel** in één enkele, betrouwbare aanroep **verwijdert**.

We gebruiken de populaire **Aspose.Cells for .NET** bibliotheek omdat deze werkt zonder dat Excel op de server geïnstalleerd hoeft te zijn. Aan het einde van deze tutorial heb je een zelfstandige console‑applicatie die een werkmap laadt, de eerste tabel vindt en de autofilter uitschakelt. De oplossing werkt met .xlsx‑bestanden die zijn gemaakt met Excel 2007 of nieuwer.

## Wat je nodig hebt

| Prerequisite | Why it matters |
|--------------|----------------|
| .NET 6.0 or later | Levert de runtime voor de C#‑code. |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Biedt programmatische toegang tot werkbladen, tabellen en autofilters. |
| A sample Excel file (`Sample.xlsx`) that contains at least one table with an autofilter applied | Een voorbeeld‑Excel‑bestand (`Sample.xlsx`) dat minstens één tabel bevat met een toegepaste autofilter. |
| Visual Studio 2022 (or any C# IDE) | Maakt het bouwen en debuggen van de console‑applicatie eenvoudig. |

> **Pro tip:** Als je een gratis alternatief verkiest, kun je de code aanpassen om **ClosedXML** of **EPPlus** te gebruiken; het kernidee—het instellen van de `AutoFilter`‑eigenschap van de tabel op `null`—blijft hetzelfde.

## Stap 1: Maak een nieuw console‑project

Open een terminal of de Visual Studio‑opdrachtprompt en voer uit:

```bash
dotnet new console -n ExcelFilterDemo
cd ExcelFilterDemo
dotnet add package Aspose.Cells
```

## Stap 2: Laad de werkmap en vind het eerste werkblad

De eerste logische handeling is het openen van het werkmap‑bestand. Aspose.Cells leest het bestand in een `Workbook`‑object dat je directe toegang geeft tot werkbladen en tabellen.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the Excel file you want to modify
        const string inputPath = "Sample.xlsx";

        // Load the workbook into memory
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **Waarom deze stap?** Het laden van de werkmap is vereist voordat je Excel‑objecten kunt manipuleren. Het gebruiken van het eerste werkblad (`Worksheets[0]`) weerspiegelt het typische scenario waarin de primaire gegevens zich op het eerste blad bevinden.

## Stap 3: Haal de eerste tabel op die op het werkblad is gedefinieerd

Excel‑tabellen (ook wel ListObjects genoemd) zijn de containers die gestructureerde gegevens bevatten. Elke tabel kan zijn eigen autofilter hebben. Om de filter te verwijderen hebben we eerst een referentie naar het tabelobject nodig.

```csharp
        // Get the first table on the worksheet.
        // If the worksheet has no tables, this will throw an IndexOutOfRangeException.
        Table table = worksheet.Tables[0];
```

> **Randgeval:** Als de werkmap mogelijk werkbladen zonder tabellen bevat, wikkel de toegang dan in een `if (worksheet.Tables.Count > 0)`‑controle. Dit voorkomt runtime‑fouten en maakt de oplossing robuust.

## Stap 4: Schakel de autofilter voor de tabel uit

Het daadwerkelijke uitschakelen is één regel: wijs `null` toe aan de `AutoFilter`‑eigenschap van het `Table`‑object. Dit wist alle filtercriteria en verwijdert de vervolgkeuzepijlen uit de koprij.

```csharp
        // Disable the autofilter – this clears any applied filter.
        table.AutoFilter = null;
```

Nadat deze regel is uitgevoerd, gedraagt de tabel zich als een normaal bereik zonder filter‑UI.

## Stap 5: Sla de gewijzigde werkmap op

Schrijf tenslotte de wijzigingen terug naar de schijf. Je kunt het oorspronkelijke bestand overschrijven of een nieuw bestand maken om de bron ongewijzigd te houden.

```csharp
        // Save the workbook. Use a new file name to avoid overwriting the original.
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

### Volledige broncode

Als we alle onderdelen samenvoegen, ziet het volledige programma er als volgt uit:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the original Excel file
        const string inputPath = "Sample.xlsx";

        // Load the workbook
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (worksheet.Tables.Count == 0)
        {
            System.Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Get the first table
        Table table = worksheet.Tables[0];

        // Disable the autofilter – clears any applied filter
        table.AutoFilter = null;

        // Save the modified workbook
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

Voer het programma uit met `dotnet run`. Na uitvoering, open `Sample_NoFilter.xlsx` in Excel; je zult zien dat de filterpijlen verdwenen zijn en alle rijen zichtbaar zijn.

## Verifieer dat de autofilter echt verdwenen is

1. Open het opgeslagen bestand (`Sample_NoFilter.xlsx`) in Microsoft Excel.  
2. Klik op een kolomkop – je zou **niet** de vervolgkeuzefilter‑pijl moeten zien.  
3. Als je nog steeds pijlen ziet, controleer dan of de tabel die je hebt geselecteerd inderdaad de tabel met de filter is. Je kunt alle tabellen weergeven met:

```csharp
foreach (var tbl in worksheet.Tables)
{
    System.Console.WriteLine($"Table name: {tbl.Name}, Has AutoFilter: {tbl.AutoFilter != null}");
}
```

De console‑output zou `Has AutoFilter: False` moeten rapporteren voor de tabel die je hebt aangepast.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| `IndexOutOfRangeException` at `worksheet.Tables[0]` | Het werkblad heeft geen tabellen. | Voeg een guard toe `if (worksheet.Tables.Count == 0)` vóór het benaderen. |
| Saved file still shows filters | Je hebt het verkeerde werkblad of de verkeerde tabel bewerkt. | Gebruik `wb.Worksheets["SheetName"]` of doorloop `wb.Worksheets` om de juiste tabel te vinden. |
| The program crashes on older .NET versions | Het programma crasht op oudere .NET‑versies. | Upgrade het target‑framework in het `.csproj`‑bestand. |
| NullReferenceException when `table.AutoFilter` is already null | Je hebt de code twee keer op hetzelfde bestand aangeroepen zonder opnieuw te laden. | Laad de werkmap opnieuw of controleer `if (table.AutoFilter != null)` vóór het toewijzen. |

## De oplossing uitbreiden

Nu je weet hoe je **autofilter in Excel** kunt **uitschakelen**, wil je misschien:

* **Remove autofilter from Excel table** alleen wanneer aan een specifieke voorwaarde wordt voldaan (bijv. wanneer een gebruikersvlag is ingesteld). Voeg een `if`‑statement toe rond `table.AutoFilter = null;`.
* **Apply a new filter** programmatisch na het wissen van de oude, met gebruik van `table.AutoFilter.Range` en `table.AutoFilter.AddFilterColumn(...)`.
* **Process multiple tables** in dezelfde werkmap door te itereren over `worksheet.Tables` en elke filter uit te schakelen.

Deze uitbreidingen volgen hetzelfde patroon dat hierboven is gedemonstreerd en houden de codebasis schoon.

## Conclusie

Je hebt nu een beknopte, productie‑klare methode om **autofilter in Excel** uit te schakelen met C#. Door de werkmap te laden, de eerste tabel te benaderen en `table.AutoFilter = null` in te stellen, verwijder je effectief **autofilter van een Excel‑tabel** zonder handmatige interactie. Het volledige voorbeeld compileert, draait en produceert een schoon bestand dat klaar is voor verdere automatisering of distributie.

Voel je vrij om te experimenteren met extra tabellen, conditionele logica of alternatieve bibliotheken. Als je tegen randgevallen aanloopt, raadpleeg dan de probleemoplossingssectie of verken de uitgebreide documentatie van Aspose.Cells voor geavanceerde filterafhandeling. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe autofilter van Excel‑tabellen te verwijderen met C#](/cells/english/net/excel-autofilter-validation/how-to-remove-autofilter-from-excel-tables-using-c/)
- [Filter‑UI in Excel wissen met C# – Verwijder AutoFilter‑knop](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [Hoe AutoFilter te gebruiken in C# Excel‑automatisering – Volledige stap‑voor‑stap gids](/cells/english/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}