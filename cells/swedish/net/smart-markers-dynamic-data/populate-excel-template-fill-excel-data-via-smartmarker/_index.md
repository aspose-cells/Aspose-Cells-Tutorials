---
category: general
date: 2026-05-30
description: Fyll i Excel-mallen snabbt och lär dig hur du fyller Excel med data med
  Aspose.Cells SmartMarker. Komplett C#‑guide med körbar kod.
draft: false
keywords:
- populate excel template
- fill excel with data
- Aspose.Cells SmartMarker
- automate Excel reporting
- C# Excel automation
language: sv
og_description: Fyll i Excel‑mallen och fyll Excel med data med Aspose.Cells SmartMarker.
  Följ den här steg‑för‑steg C#‑handledningen för omedelbara resultat.
og_title: Fyll i Excel‑mall – Fyll Excel‑data via SmartMarker
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  headline: Populate Excel Template – Fill Excel Data via SmartMarker
  type: TechArticle
- description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  name: Populate Excel Template – Fill Excel Data via SmartMarker
  steps:
  - name: Empty Collections
    text: 'If `Items` is empty, SmartMarker will leave the table header intact but
      won’t insert any rows. To avoid a blank space, you can add a conditional block:'
  - name: Custom Number Formats
    text: 'Sometimes you need currency symbols or thousands separators. After processing,
      you can apply a style programmatically:'
  - name: Large Data Sets
    text: 'For thousands of rows, enable the `UseFastMode` option to improve performance:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Fyll i Excel‑mallen – Fyll Excel‑data via SmartMarker
url: /sv/net/smart-markers-dynamic-data/populate-excel-template-fill-excel-data-via-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Fyll i Excel‑mall – Fyll Excel‑data via SmartMarker

Har du någonsin behövt **fylla i en Excel‑mall** men varit osäker på hur du automatiserar processen? I den här handledningen visar vi hur du **fyller Excel med data** med hjälp av Aspose.Cells SmartMarker – ett verktyg som förvandlar en statisk arbetsbok till en dynamisk rapportgenerator.

Föreställ dig att du har ett fördesignat fakturablad, en försäljningsdashboard eller något återanvändbart formulär. Istället för att manuellt skriva in värden kan du mata in ett C#‑objekt och låta SmartMarker göra det tunga arbetet. I slutet av guiden har du ett fullt körbart projekt som tar en mall, injicerar rader, totaler och till och med villkorsstyrd formatering – utan att röra UI‑en.

## Vad du kommer att lära dig

- Hur du förbereder en datakälla som matchar markörerna i din Excel‑mall.  
- Hur du instansierar **SmartMarkerProcessor** och aktiverar stöd för områden.  
- Hur du **fyller i Excel‑mallen** med nästlade samlingar, såsom orderrader.  
- Tips för att hantera kantfall som tomma samlingar eller anpassade talformat.  

Inga externa tjänster, inga VBA‑makron – bara ren C# och Aspose.Cells. Allt du behöver är .NET 6 (eller senare) och Aspose.Cells NuGet‑paketet.

## Förutsättningar

- Visual Studio 2022 (eller någon IDE du föredrar).  
- .NET 6 SDK installerat.  
- Aspose.Cells för .NET (du kan hämta en gratis provversion från Aspose‑webbplatsen).  
- En grundläggande Excel‑mall med SmartMarker‑taggar (vi skapar en om ett ögonblick).

Om någon av dessa känns obekant, panik inte; stegen nedan guidar dig genom varje krav.

## Steg 1: Designa Excel‑mallen med SmartMarker‑taggar

Först öppnar du en ny arbetsbok och lägger ut de statiska delarna – företagslogotyp, rubriker osv. Sedan infogar du SmartMarker‑platshållare där dynamisk data ska visas.

| Cell | Content |
|------|---------|
| A1   | **Faktura** |
| A3   | `{{CompanyName}}` |
| A5   | **Orderdetaljer** |
| A7   | `{{Orders.Items.Name}}` |
| B7   | `{{Orders.Items.Qty}}` |
| C7   | `{{Orders.Items.Price}}` |
| D7   | `{{Orders.Items.Price * Orders.Items.Qty}}` |

**Varför detta är viktigt:** SmartMarker läser de dubbla klammerparenteserna och mappar dem till egenskaper på det objekt du skickar senare. `Orders.Items`‑samlingen talar om för motorn att upprepa raden för varje post i listan.

> **Pro tip:** Använd `RangeSmartMarker`‑alternativet (vi aktiverar det senare) när du behöver att motorn automatiskt expanderar området – perfekt för tabeller som växer eller krymper.

Spara filen som `InvoiceTemplate.xlsx` i ditt projekts `Resources`‑mapp.

## Steg 2: Förbered datakällan som matchar mallens markörer

Nu skapar vi ett C#‑anonymous‑object (eller en starkt typad klass) vars egenskapsnamn stämmer överens med markörerna. Nyckeln är att spegla hierarkin exakt.

```csharp
// Step 2: Prepare the data source that matches the template markers
var data = new
{
    CompanyName = "Acme Corp.",
    Orders = new[]
    {
        new
        {
            Items = new[]
            {
                new { Name = "Pen",   Qty = 2, Price = 1.5m },
                new { Name = "Notebook", Qty = 1, Price = 3.75m },
                new { Name = "Stapler",  Qty = 1, Price = 5.0m }
            }
        }
    }
};
```

**Varför detta är viktigt:** `Orders`‑arrayen innehåller en enda order, och varje order har en `Items`‑array. SmartMarker itererar över `Items`, klonar raden för varje element. Om du senare behöver flera order, lägg bara till fler objekt i `Orders`‑arrayen – inga kodändringar behövs.

## Steg 3: Ladda mallen och skapa en SmartMarkerProcessor‑instans

Med datan redo laddar vi arbetsboken, skapar processorn och talar om att den ska respektera områdes‑markörer.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook
Workbook workbook = new Workbook("Resources/InvoiceTemplate.xlsx");

// Get the first worksheet (where our markers live)
Worksheet ws = workbook.Worksheets[0];

// Step 3: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

**Varför detta är viktigt:** `SmartMarkerProcessor` är motorn som parsar markörerna, expanderar områden och skriver värden. Genom att separera processorn från arbetsboken håller du koden ren och återanvändbar.

## Steg 4: Bearbeta kalkylbladet med RangeSmartMarker aktiverat

Magin händer när vi anropar `Process`. Genom att sätta `RangeSmartMarker = true` talar vi om för SmartMarker att behandla hela radområdet som ett upprepningsbart block, och automatiskt infoga eller ta bort rader efter behov.

```csharp
// Step 4: Process the worksheet using SmartMarker with range support enabled
processor.Process(ws, data, new SmartMarkerOptions { RangeSmartMarker = true });
```

Vid denna punkt har motorn:

1. Skannat kalkylbladet efter `{{...}}`‑taggar.  
2. Mappat varje tagg till en egenskap på `data`.  
3. Detekterat tabellområdet (A7:D7) och duplicerat det tre gånger – en gång per post.  
4. Beräknat uttrycket `Price * Qty` för total‑kolumnen.

## Steg 5: Spara den resulterande arbetsboken

Slutligen skriver vi den ifyllda arbetsboken till disk (eller strömmar tillbaka den till en webbklient).

```csharp
// Step 5: Save the populated workbook
workbook.Save("Output/InvoicePopulated.xlsx");
```

Öppna `InvoicePopulated.xlsx` så ser du en prydligt ifylld tabell:

| Namn      | Antal | Pris | Summa |
|-----------|-------|------|-------|
| Pen       | 2     | 1.5  | 3.00 |
| Notebook  | 1     | 3.75 | 3.75 |
| Stapler   | 1     | 5.00 | 5.00 |

Steget **fylla i Excel‑mall** är nu slutfört, och du har framgångsrikt **fyllt Excel med data** för ett godtyckligt antal rader.

## Hantera vanliga kantfall

### Tomma samlingar

Om `Items` är tomt lämnar SmartMarker tabellrubriken intakt men infogar inga rader. För att undvika ett tomt utrymme kan du lägga till ett villkorsblock:

```csharp
{{#if Orders.Items.Length > 0}}
    ... table rows ...
{{else}}
    No items were ordered.
{{/if}}
```

### Anpassade talformat

Ibland behöver du valutasymboler eller tusentalsavgränsare. Efter bearbetning kan du programatiskt applicera en stil:

```csharp
Style style = workbook.CreateStyle();
style.Number = 164; // Built‑in currency format
StyleFlag flag = new StyleFlag { NumberFormat = true };

foreach (Cell cell in ws.Cells["C8:D12"])
{
    cell.SetStyle(style, flag);
}
```

### Stora datamängder

För tusentals rader, aktivera `UseFastMode`‑alternativet för att förbättra prestandan:

```csharp
processor.Process(ws, data, new SmartMarkerOptions { 
    RangeSmartMarker = true,
    UseFastMode = true
});
```

## Fullt fungerande exempel

Nedan är det kompletta, självständiga programmet som du kan kopiera och klistra in i en konsolapp. Det inkluderar alla using‑direktiv, databeredning, bearbetning och sparande.



## Vad bör du lära dig härnäst?

- [Fyll Excel med data med Aspose.Cells och Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [Hur du fyller Excel‑celler med Aspose.Cells för .NET: En steg‑för‑steg‑guide](/cells/english/net/cell-operations/aspose-cells-dotnet-populate-excel-data/)
- [Automatisera Excel‑dataexport med Aspose.Cells för .NET: En steg‑för‑steg‑guide](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}