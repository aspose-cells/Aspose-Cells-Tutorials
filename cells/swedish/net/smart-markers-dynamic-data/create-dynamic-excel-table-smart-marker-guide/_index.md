---
category: general
date: 2026-05-23
description: Skapa dynamisk Excel-tabell med en mall och JSON‑data. Lär dig hur du
  laddar Excel‑mallen, automatiserar Excel‑rapporten och snabbt fyller i Excel från
  JSON.
draft: false
keywords:
- create dynamic excel table
- load excel template
- automate excel report
- populate excel from json
- generate excel report json
language: sv
og_description: Skapa dynamisk Excel-tabell på några minuter med en mall och JSON.
  Den här handledningen visar hur du laddar en Excel-mall, automatiserar Excel-rapporten
  och fyller i Excel från JSON.
og_title: Skapa dynamisk Excel‑tabell – Smart Marker‑guide
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create dynamic excel table using a template and JSON data. Learn how
    to load excel template, automate excel report, and populate excel from json quickly.
  headline: Create Dynamic Excel Table – Smart Marker Guide
  type: TechArticle
tags:
- Excel
- Smart Markers
- JSON
- .NET
title: Skapa dynamisk Excel‑tabell – Smart Marker‑guide
url: /sv/net/smart-markers-dynamic-data/create-dynamic-excel-table-smart-marker-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa dynamisk Excel-tabell – Smart Marker-guide

Har du någonsin behövt **create dynamic excel table** som expanderar automatiskt för varje post i din datamängd? Du är inte ensam. Oavsett om du bygger en månatlig försäljningsdashboard eller ett kund‑specifikt fakturapaket, kan förmågan att **populate excel from json** utan att skriva ändlösa loopar spara timmar.

I den här handledningen går vi igenom en komplett, praktisk lösning som visar dig hur du **load excel template**, bäddar in en Smart Marker, matar den med JSON, och slutligen **automate excel report**-generering. I slutet har du ett färdigt .NET-projekt som producerar en polerad Excel-arbetsbok från en enda JSON-payload.

---

## Vad du behöver

- **Aspose.Cells for .NET** (eller något bibliotek som stödjer Smart Markers). Exemplet använder version 24.5, men vilken recent version som helst fungerar.
- Visual Studio 2022 (eller din favoritä IDE för C#).
- En enkel Excel‑mallfil (`template.xlsx`) placerad i en mapp du kontrollerar.
- En JSON‑sträng som innehåller en samling med namnet `Customers`.

Det är allt—inga extra tjänster, inga databasanslutningar, bara ren kod.

---

## Steg 1: Skapa en mallarbok – Load Excel Template

Det första vi gör är att **load excel template** i minnet. Tänk på mallen som en duk där en speciell platshållare talar om för processorn var rader ska upprepas.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook (make sure the path is correct)
Workbook workbook = new Workbook(@"C:\Reports\template.xlsx");

// Grab the first worksheet – this is where our Smart Marker lives
Worksheet worksheet = workbook.Worksheets[0];
```

> **Varför detta är viktigt:** Att ladda mallen en gång håller fil‑I/O till ett minimum och låter dig återanvända samma layout för många rapporter. Det isolerar också Smart Marker‑logiken från resten av din kod, vilket är en ren separation av ansvarsområden.

---

## Steg 2: Infoga en Smart Marker – Create Dynamic Excel Table

Nu bäddar vi in en **Smart Marker** som kommer att upprepa en tabell för varje post i `Customers`‑samlingen. Syntaxen `${Customers.RepeatWorksheet}` talar om för Aspose.Cells att klona hela arbetsbladet för varje kund.

```csharp
// Place the Smart Marker in cell A1 (top‑left corner)
worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");
```

> **Proffstips:** Om du bara behöver upprepa rader istället för hela arbetsblad, använd `${Customers.Repeat}` på den första raden i tabellen. Upprepning på arbetsbladsnivå är praktisk när varje kund får sin egen flik.

---

## Steg 3: Förbered SmartMarkerProcessor – Automate Excel Report

Med markören på plats skapar vi en `SmartMarkerProcessor`. Detta objekt orkestrerar databindningen mellan JSON och Excel‑mallen.

```csharp
// Initialize the processor with the workbook that contains the marker
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

Processorn är lättviktig; du kan återanvända den för flera JSON‑payloads om du vill.

---

## Steg 4: Mata in JSON‑data – Populate Excel from JSON

Här sker magin. Vi matar in en JSON‑sträng som innehåller en array av kunder. Varje kund kan ha fält som `Name`, `Email` och `Total`.

```csharp
// Sample JSON data – in a real scenario you might read this from a file or API
string customersJson = @"
{
  ""Customers"": [
    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
  ]
}";

// Apply the JSON to the processor – this populates the workbook
processor.ApplyJson(customersJson);
```

> **Varför JSON?** JSON är språk‑oberoende och lätt att generera från API:er, databaser eller till och med manuella inmatningar. Att använda `ApplyJson` betyder att du inte behöver mappa objekt manuellt; processorn gör det tunga arbetet.

---

## Steg 5: Spara resultatet – Generate Excel Report JSON

Till sist skriver vi den fyllda arbetsboken till disk. Utdatafilen innehåller nu ett separat arbetsblad för varje kund, var och en fylld med data från vår JSON.

```csharp
// Save the filled workbook – choose a path that makes sense for your app
workbook.Save(@"C:\Reports\output.xlsx");
```

### Förväntad output

- **output.xlsx** kommer att ha tre arbetsblad namngivna `Sheet1`, `Sheet2`, `Sheet3` (eller vilken namngivningskonvention din mall använder).
- Varje blad kommer att visa `Name`, `Email` och `Total`‑värdena för en enskild kund.
- Layouten du designade i `template.xlsx` (rubriker, styling, formler) bevaras i alla genererade blad.

---

## Fullt fungerande exempel

Nedan är det kompletta, färdiga programmet. Kopiera‑klistra in det i en konsolapp, justera filsökvägarna och tryck **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace DynamicExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template workbook
            string templatePath = @"C:\Reports\template.xlsx";
            Workbook workbook = new Workbook(templatePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Insert the Smart Marker that repeats the worksheet per customer
            worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");

            // 3️⃣ Create the SmartMarkerProcessor
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

            // 4️⃣ JSON data containing a collection of customers
            string customersJson = @"
            {
                ""Customers"": [
                    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
                    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
                    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
                ]
            }";

            // Apply the JSON – this populates the workbook dynamically
            processor.ApplyJson(customersJson);

            // 5️⃣ Save the generated report
            string outputPath = @"C:\Reports\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Dynamic Excel report generated at: {outputPath}");
        }
    }
}
```

Kör programmet, öppna `output.xlsx`, och du kommer att se en **create dynamic excel table** i aktion—varje kund får sitt eget blad, fullt formaterat enligt din design.

---

## Vanliga frågor & kantfall

| Question | Answer |
|----------|--------|
| *Vad händer om min JSON har nästlade objekt?* | Smart Markers stödjer punktnotation (`${Customers.Address.City}`) så länge JSON‑hierarkin matchar. |
| *Kan jag namnge de genererade arbetsbladen efter kunden?* | Ja—lägg till en markör som `${Customers.Name}` i cellen för arbetsbladsnamnet eller använd `processor.ApplyJson(customersJson, \"Customers\")` med ett namngivningsmönster. |
| *Vad händer med stora datamängder (10 k+ rader)?* | Processorn strömmar data effektivt, men håll ett öga på minnet. Överväg att dela upp rapporten i flera filer om du når prestandagränser. |
| *Behöver jag en licens för Aspose.Cells?* | En gratis utvärdering fungerar för testning, men en licensierad version tar bort vattenstämplar och ger full funktionalitet. |
| *Kan jag använda detta tillvägagångssätt med .NET Core?* | Absolut—Aspose.Cells stödjer .NET 6/7/8. Referera bara NuGet‑paketet så förblir koden densamma. |

---

## Tips för produktionsklara implementationer

- **Validate JSON** innan du matar in den i `ApplyJson`. En felaktig payload kommer att kasta ett `JsonParseException`.
- **Cache the template** om du genererar många rapporter på kort tid; att ladda från disk upprepade gånger är onödig I/O.
- **Lock the workbook** under bearbetning om du kör detta i en flertrådad webbtjänst för att undvika race‑conditions.
- **Add error handling** runt `workbook.Save` för att smidigt hantera behörighetsproblem eller låsta filer.
- **Customize styling** i mallen (villkorsstyrd formatering, formler) så att de genererade bladen behåller affärslogik utan extra kod.

---

## Slutsats

Du har nu ett robust, end‑to‑end‑mönster för hur du **create dynamic excel table** med en mall, Smart Markers och JSON‑data. Genom att **load excel template**, infoga en repeat‑markör och **populate excel from json**, kan du **automate excel report**‑generering med bara några rader C#.

Nästa steg? Prova att lägga till diagram som refererar till de dynamiska tabellerna, eller exportera samma JSON till en PDF med Aspose.Words. Du kan också experimentera med **generate excel report json** från en databasfråga för att slutföra loopen

## Relaterade handledningar

- [Create a Pivot Table in Excel Using Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [Create Dynamic Line Charts in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [How to Create Checkboxes in Excel using Aspose.Cells for .NET | Data Validation Tutorial](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}