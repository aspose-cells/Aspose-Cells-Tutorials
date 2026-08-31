---
category: general
date: 2026-02-14
description: Skapa masterdataobjekt i C# och generera detaljblad utan ansträngning.
  Lär dig hela SmartMarker‑arbetsflödet med praktiska kodexempel.
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: sv
og_description: Skapa masterdataobjekt i C# och generera detaljblad med SmartMarker.
  Följ vår detaljerade handledning för en färdigkörbar lösning.
og_title: Skapa Master Data-objekt – Komplett guide
tags:
- C#
- SmartMarker
- Excel Automation
title: Skapa masterdataobjekt – Steg‑för‑steg guide för att generera detaljblad
url: /sv/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Master Data Object – Komplett handledning

Har du någonsin behövt **create master data object** för ett Excel-ark men varit osäker på hur du kopplar det till ett SmartMarker detail sheet? Du är inte ensam. I många rapporteringsscenarier styr master‑objektet ett dynamiskt detaljblad, och att få kopplingen rätt kan kännas som att lägga ett pussel utan bild.  

I den här guiden går vi igenom hela processen — att bygga master data‑objektet, konfigurera SmartMarker‑alternativen för att **generate detail sheet**, och slutligen köra processorn. I slutet har du ett körbart kodexempel som du kan klistra in i vilket .NET‑projekt som helst som använder GrapeCity Documents for Excel (GcExcel)-biblioteket.

## Vad du behöver

- .NET 6+ (eller .NET Framework 4.7.2) med en referens till `GcExcel.dll`
- Grundläggande C#‑kunskaper (variabler, anonyma typer, objektinitialiserare)
- En Excel‑arbetsbok som redan innehåller SmartMarker‑taggar som `{{OrderId}}` och en tabell för radposter
- Visual Studio, Rider eller någon annan editor du föredrar

Det är allt — inga extra NuGet‑paket utöver den grundläggande GcExcel‑distributionen.

## Steg 1: Skapa Master Data Object

Det första du måste göra är att **create master data object** som speglar den struktur som SmartMarker‑taggarna förväntar sig. Tänk på det som en liten rapportmodell i minnet.

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

Varför använda en anonym typ här? För att den låter dig definiera en lättviktig behållare utan att deklarera en fullständig klass — perfekt för snabba demonstrationer eller när strukturen sannolikt inte kommer att förändras. Om du senare behöver en återanvändbar modell, ersätt helt enkelt `var` med en korrekt POCO.

> **Pro tip:** Håll egenskapsnamnen (`OrderId`, `Product`, `Quantity`) identiska med platshållarna i ditt kalkylblad; SmartMarker matchar dem utan att ta hänsyn till versaler.

## Steg 2: Konfigurera SmartMarker‑alternativ för att generera ett detaljblad

Nu berättar vi för SmartMarker att vi vill ha ett separat kalkylblad för radpost‑tabellen. Här kommer nyckelordet **generate detail sheet** in i bilden.

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

`DetailSheetNewName`‑mönstret använder måsvinge‑platshållare som ersätts vid körning. I vårt exempel kommer bladet att heta `Order_1`. Om du senare loopar över flera ordrar får varje sin egen flik — precis vad de flesta revisorer förväntar sig.

## Steg 3: Kör SmartMarker‑processorn

När data och alternativ är klara är sista steget att anropa processorn på mål‑kalkylbladet.

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

Bakom kulisserna skannar SmartMarker kalkylbladet efter taggar, injicerar `orderData`‑värdena, och eftersom `DetailSheet` är `true` klonar den mallen till ett nytt blad med namnet `Order_1`. Alla radposter visas i detaljområdet och behåller all formatering du använde i mallen.

### Fullständigt fungerande exempel

Nedan är ett fristående konsolprogram som öppnar en mallarbetsbok (`Template.xlsx`), kör de tre stegen och sparar resultatet som `Result.xlsx`. Du kan kopiera‑klistra in detta i ett nytt konsolprojekt och trycka **F5**.

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### Förväntat resultat

- **Result.xlsx** innehåller ett blad som heter `Order_1`.
- Cellen `A1` (eller var du än placerade `{{OrderId}}`) visar nu `1`.
- En tabell som börjar vid SmartMarker‑blocket listar två rader:
  | Product | Quantity |
  |---------|----------|
  | A       | 2        |
  | B       | 5        |

Om du öppnar filen kommer du att se att formateringen från mallen är bevarad — kanter, typsnitt, villkorsstyrd formatering — allt intakt.

## Vanliga frågor & specialfall

### Vad händer om jag har flera ordrar?

Packa in master‑objektet i en samling och låt SmartMarker iterera automatiskt:

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

Varje order skapar sitt eget blad (`Order_1`, `Order_2`, …). Processorn behandlar den yttre arrayen som master‑samlingen.

### Hur styr jag bladets position?

Ange `smartMarkerOptions.DetailSheetInsertIndex = 2;` för att placera det nya bladet efter den andra fliken, eller använd `DetailSheetInsertAfter = "Summary"` för att infoga efter ett namngivet blad.

### Kan jag inaktivera detaljbladet för ett specifikt körning?

Växla helt enkelt `DetailSheet = false;`. SmartMarker kommer då att skriva radposterna i samma blad där master‑taggarna finns.

### Vad händer med stora datamängder?

SmartMarker strömmar data effektivt, men om du överskrider några hundratusen rader kan du nå Excels gräns på 1 048 576 rader. I så fall dela upp data i flera master‑poster eller överväg att exportera till CSV.

## Visuell översikt

![Diagram illustrating how to create master data object and generate detail sheet using SmartMarker](/images/smartmarker-flow.png)

*Illustrationen visar flödet från C#‑master‑objektet → SmartMarker‑alternativ → kalkylbladsbehandling → nytt detaljblad.*

## Slutsats

Du vet nu hur du **create master data object** i C# och konfigurerar SmartMarker för att automatiskt **generate detail sheet**. Det tre‑stegs mönstret — data, alternativ, processor — täcker de flesta Excel‑automatiseringsscenarier med GcExcel.  

Från här kan du utforska:

- Lägga till huvud-/fotdata på varje detaljblad
- Använda villkorsstyrd formatering baserat på orderstatus
- Exportera den genererade arbetsboken till PDF med `workbook.SaveAsPdf(...)`

Känn dig fri att experimentera, bryta saker och sedan sätta ihop dem igen. Det är det snabbaste sättet att bemästra kalkylbladsautomatisering. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}