---
category: general
date: 2026-02-28
description: Skapa master‑detail‑rapport i C# och lär dig hur du fyller i en Excel‑mall,
  slår samman data i Excel och laddar en Excel‑arbetsbok i C# på bara några steg.
draft: false
keywords:
- create master detail report
- populate excel template
- merge data into excel
- load excel workbook c#
- how to create master detail
language: sv
og_description: Skapa master‑detail‑rapport i C# med Aspose.Cells SmartMarker. Lär
  dig att ladda Excel‑arbetsbok i C#, slå samman data i Excel och fylla i en Excel‑mall.
og_title: Skapa master‑detailrapport i C# – Fyll i Excel‑mall
tags:
- C#
- Aspose.Cells
- Excel automation
- SmartMarker
title: Skapa master‑detail‑rapport i C# – Populera Excel‑mall med SmartMarker
url: /sv/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa master‑detail‑rapport i C# – Fyll i Excel‑mall med SmartMarker

Har du någonsin behövt **create master detail report** i C# men varit osäker på hur du får data in i en Excel‑fil? Du är inte ensam. I den här guiden går vi igenom de exakta stegen för att **populate Excel template**, **merge data into Excel**, och **load Excel workbook C#**‑style så att du får en polerad master‑detail‑rapport klar för distribution.

Vi kommer att använda Aspose.Cells SmartMarker, en kraftfull motor som förstår master‑detail‑relationer direkt. I slutet av handledningen har du ett komplett, körbart exempel som du kan lägga in i vilket .NET‑projekt som helst. Inga vaga “see the docs”-genvägar—bara en självständig lösning som du kan kopiera‑klistra in och köra.

## Vad du kommer att lära dig

- Hur du **create master detail** datastrukturer i C# som mappar direkt till en Excel‑mall.
- Det exakta sättet att **load Excel workbook C#** kod som öppnar en `.xlsx`‑fil som innehåller SmartMarker‑taggar.
- Processen för att **populate Excel template** genom att köra `SmartMarkerProcessor`.
- Tips för att hantera edge cases, såsom saknade taggar eller stora datamängder.
- Hur du verifierar resultatet och hur den slutgiltiga **master detail report** ser ut.

### Förutsättningar

- .NET 6.0 eller senare (koden fungerar också på .NET Framework 4.8).
- Aspose.Cells för .NET (du kan hämta ett gratis prov‑NuGet‑paket: `Install-Package Aspose.Cells`).
- En grundläggande Excel‑fil (`template.xlsx`) som innehåller SmartMarker‑taggar (vi visar den minsta markup du behöver).

Om du har detta klart, låt oss dyka ner.

## Steg 1 – Skapa master‑detail‑datakällan *(how to create master detail)*

Det första du behöver är ett C#‑objekt som representerar master‑raderna (orders) och deras underordnade rader (order items). SmartMarker läser automatiskt denna hierarki när `MasterDetail` är satt till `true`.

```csharp
using System;

// Step 1: Build the master‑detail data object
var orderData = new
{
    // Master collection – each order is a row in the master table
    Orders = new[]
    {
        new
        {
            Id = 1,
            // Detail collection – items belonging to order 1
            Items = new[] { new { Sku = 101, Qty = 2 }, new { Sku = 102, Qty = 1 } }
        },
        new
        {
            Id = 2,
            Items = new[] { new { Sku = 202, Qty = 1 } }
        }
    }
};
```

**Varför detta är viktigt:**  
SmartMarker letar efter en egenskap som heter `Orders` (master) och sedan för varje order söker den efter en samling som heter `Items`. Genom att matcha dessa namn får du automatiskt en **master‑detail report** utan att skriva några loopar själv.

> **Pro tip:** Håll egenskapsnamnen korta och meningsfulla; de blir platshållarna i din Excel‑mall.

## Steg 2 – Konfigurera SmartMarker‑alternativ för master‑detail‑bearbetning

Berätta för motorn att du hanterar ett master‑detail‑scenario och ge den namnet på detaljbladet som ska ta emot underordnade rader.

```csharp
using Aspose.Cells;

// Step 2: Set up SmartMarker options
SmartMarkerOptions options = new SmartMarkerOptions
{
    // Enables master‑detail processing
    MasterDetail = true,
    // The sheet in the template that holds the detail rows
    DetailSheetName = "OrderDetail"
};
```

**Varför detta är viktigt:**  
Om du utelämnar `MasterDetail = true` kommer SmartMarker att behandla data som en platt lista och detaljraderna kommer aldrig att visas. `DetailSheetName` måste matcha bladnamnet du skapade i mallen (skiftlägeskänsligt).

## Steg 3 – Ladda Excel‑arbetsboken C#‑stil

Nu öppnar vi mallen som innehåller SmartMarker‑taggarna. Detta är steget **load Excel workbook C#** som många utvecklare snubblar på eftersom de glömmer att använda rätt filsökväg eller att korrekt disponera arbetsboken.

```csharp
using System.IO;

// Step 3: Load the workbook that holds the SmartMarker tags
string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
Workbook workbook = new Workbook(templatePath);
```

**Varför detta är viktigt:**  
Aspose.Cells läser in hela arbetsboken i minnet, så filen kan ligga på disk, vara inbäddad som en resurs eller till och med strömmas från en webbtjänst. Se bara till att sökvägen pekar på en giltig `.xlsx`‑fil som innehåller de taggar vi kommer att diskutera härnäst.

## Steg 4 – Infoga SmartMarker‑taggar i mallen (populate Excel template)

Om du öppnar `template.xlsx` nu kommer du att se två blad:

- **Orders** – master‑bladet med en rad som `&=Orders.Id`.
- **OrderDetail** – detaljbladet med rader som `&=Items.Sku` och `&=Items.Qty`.

Här är en minimal vy av markupen:

| Blad | Cell A1 | Cell B1 |
|-------|---------|---------|
| Orders | `&=Orders.Id` | *(empty)* |
| OrderDetail | `&=Items.Sku` | `&=Items.Qty` |

Du behöver inte skriva någon kod för taggarna—de finns i Excel‑filen. Steget **populate Excel template** är helt enkelt att anropa processorn:

```csharp
// Step 4: Run SmartMarker to merge data into Excel
new SmartMarkerProcessor().Process(workbook, orderData, options);
```

**Varför detta är viktigt:**  
Processorn skannar varje blad, ersätter `&=`‑platshållarna med faktiska värden och expanderar rader för varje master‑ och detaljpost. Eftersom `MasterDetail` är aktiverat skapas automatiskt en ny rad för varje objekt under den aktuella ordern.

## Steg 5 – Spara master‑detail‑rapporten

Till sist skriver du den fyllda arbetsboken till disk. Detta är ögonblicket då du får en färdig **master detail report** att dela.

```csharp
// Step 5: Save the populated workbook
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);

// Optional: open the file automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Förväntat resultat:**  

- **Orders**‑bladet visar två rader: `1` och `2` (order‑ID:n).  
- **OrderDetail**‑bladet visar tre rader:  
  - SKU 101 Qty 2  
  - SKU 102 Qty 1  
  - SKU 202 Qty 1  

Det är en fullt funktionell **create master detail report** som du kan e‑mailla, skriva ut eller mata in i ett annat system.

## Edge cases & vanliga frågor

### Vad händer om mallen saknar en tagg?
SmartMarker ignorerar tyst okända taggar, men du får tomma celler. Dubbelkolla tagg‑stavningen och se till att egenskapsnamnen i ditt C#‑objekt matchar exakt.

### Hur hanterar den stora datamängder?
Processorn strömmar rader, så även tusentals detaljposter tar inte upp för mycket minne. För extremt stora filer kan du dock vilja öka `MemorySetting` i `LoadOptions`.

```csharp
var loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeWorkbook = new Workbook(templatePath, loadOptions);
```

### Kan jag använda ett annat bladnamn för master?
Ja—byt bara namn på bladet i mallen och justera `DetailSheetName` om du har ett detaljblad. Master‑bladets namn härleds från platshållaren (`&=Orders.Id`).

### Vad händer om jag behöver lägga till en totalsrad?
Lägg till en vanlig Excel‑formel i mallen (t.ex. `=SUM(B2:B{#})`). SmartMarker bevarar formeln efter datainmatning.

## Fullt körbart exempel

Nedan är det kompletta programmet som du kan kopiera‑klistra in i en konsolapp. Det inkluderar alla `using`‑direktiv, datamodellen, alternativ och filhantering.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace MasterDetailReportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Create master‑detail data ----------
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Sku = 101, Qty = 2 },
                            new { Sku = 102, Qty = 1 }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Sku = 202, Qty = 1 }
                        }
                    }
                }
            };

            // ---------- Step 2: SmartMarker options ----------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                MasterDetail = true,
                DetailSheetName = "OrderDetail"
            };

            // ---------- Step 3: Load the template ----------
            string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
            Workbook workbook = new Workbook(templatePath);

            // ---------- Step 4: Process the template ----------
            new SmartMarkerProcessor().Process(workbook, orderData, options);

            // ---------- Step 5: Save the result ----------
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);

            Console.WriteLine($"Master detail report generated at: {outputPath}");
        }
    }
}
```

Kör programmet, öppna `output.xlsx`, och du kommer att se master‑detail‑data vackert fyllda.

## Visuell referens

![Skärmdump av skapad master detail‑rapport](https://example.com/images/master-detail-report.png "Exempel på master detail‑rapport")

*Bilden visar Orders‑bladet med ID:n 1 och 2, samt OrderDetail‑bladet med de tre SKU‑Qty‑raderna.*

## Slutsats

Du vet nu **how to create master detail report** i C# med Aspose.Cells SmartMarker, från att bygga datakällan till **loading Excel workbook C#**, **populating Excel template**, och slutligen

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}