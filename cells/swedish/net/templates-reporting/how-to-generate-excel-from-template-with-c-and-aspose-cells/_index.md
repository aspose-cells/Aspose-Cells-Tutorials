---
category: general
date: 2026-11-19
description: Lär dig hur du snabbt genererar Excel från en mall i C#. Denna guide
  visar också hur du genererar Excel‑rapport i C# med hjälp av Smart Markers.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate excel from template
- generate excel report c#
- Aspose.Cells Smart Marker
- master‑detail Excel export
- C# Excel automation
language: sv
lastmod: 2026-11-19
og_description: Skapa Excel från mall i C# med Aspose.Cells. Följ den här handledningen
  för att generera en Excel‑rapport i C# med Smart Markers och master‑detail‑data.
og_image_alt: Screenshot showing C# code that generates Excel from a template file
og_title: Generera Excel från mall i C# – komplett steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to generate Excel from template in C# quickly. This guide
    also shows you how to generate Excel report C# using Smart Markers.
  headline: How to generate Excel from template with C# and Aspose.Cells
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Hur man genererar Excel från mall med C# och Aspose.Cells
url: /sv/net/templates-reporting/how-to-generate-excel-from-template-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Generera Excel från mall i C# – komplett steg‑för‑steg‑guide

Om du behöver **generera Excel från mall** i ett .NET‑projekt visar den här handledningen en färdig‑att‑köra‑lösning. Med Aspose.Cells Smart Markers kan du fylla en fördesignad arbetsbok med master‑detail‑data och skapa en polerad rapport utan att skriva några Excel‑specifika formler själv.

Du kommer också att se hur samma tillvägagångssätt låter dig **generera Excel‑rapport C#** för fakturor, ordersammanfattningar eller vilken hierarkisk datamängd som helst. I slutet av guiden har du en återanvändbar metod som omvandlar en mallfil till en fullt ifylld arbetsbok.

## Vad den här handledningen täcker

* Laddar en befintlig `.xlsx`‑mall som redan innehåller Smart Marker‑platshållare.  
* Förbereder ett master‑detail‑objekt som matchar mallens hierarki.  
* Konfigurerar `SmartMarkerProcessor` för att skapa ett separat detaljblad för nästlade samlingar.  
* Bearbetar kalkylbladet och sparar resultatet som en ny fil.  

Inga externa tjänster krävs—endast Aspose.Cells för .NET‑biblioteket (gratis provversion eller licensierad version) och ett .NET 6+‑projekt.

---

## Förutsättningar

| Krav | Varför det är viktigt |
|------|-----------------------|
| **Aspose.Cells for .NET** (NuGet package `Aspose.Cells`) | Tillhandahåller `SmartMarkerProcessor` och API:er för Excel‑manipulation. |
| **.NET 6 SDK** or later | Säkerställer moderna språkfunktioner och kompatibilitet med den senaste Aspose.Cells‑utgåvan. |
| **A template workbook** (`template.xlsx`) with Smart Markers placed in the first worksheet | Smart Markers styr databindningen; mallen definierar layout, stilar och statiskt innehåll. |
| Basic knowledge of C# collections and anonymous types | Datakällan byggs som ett anonymt objekt som speglar mallens struktur. |

Du kan skapa mallen i Excel genom att skriva `&=Orders.Id` för order‑ID‑kolumnen och `&=Orders.Items.Name` för de nästlade objekten. Prefixet `&=` talar om för Smart Markers att ersätta cellen med data vid körning.

---

## Steg 1: Ställ in C#‑projektet och lägg till Aspose.Cells

Skapa en konsolapplikation (eller integrera i en befintlig tjänst) och lägg till NuGet‑paketet:

```bash
dotnet new console -n ExcelTemplateDemo
cd ExcelTemplateDemo
dotnet add package Aspose.Cells
```

> **Proffstips:** Använd flaggan `--version` för att låsa till en känd stabil version, t.ex. `Aspose.Cells 23.12`.

---

## Steg 2: Definiera master‑detail‑datakällan

Datakällan måste spegla den hierarki som används i mallen. I det här exemplet har vi beställningar (master) som var och en innehåller en samling artiklar (detail).

```csharp
using System;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2: Create the data source with master‑detail information
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Name = "A" },
                            new { Name = "B" }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Name = "C" }
                        }
                    }
                }
            };
```

**Varför detta fungerar:**  
*Den anonyma typen* låter dig bygga en snabb in‑memory‑representation utan att definiera explicita POCO‑klasser. Varje `Order` har ett `Id` och en `Items`‑array, vilket matchar markörerna `&=Orders.Id` och `&=Orders.Items.Name` i mallen.

---

## Steg 3: Ladda Excel‑mallen som innehåller Smart Markers

```csharp
            // Step 3: Load the Excel template that contains Smart Markers
            string templatePath = @"YOUR_DIRECTORY\template.xlsx";
            Workbook workbook = new Workbook(templatePath);
```

**Förklaring:**  
`Workbook` läser `.xlsx`‑filen till minnet. Mallen bör redan ha Smart Marker‑syntaxen (`&=Orders.Id`, `&=Orders.Items.Name` osv.) placerad där du vill att data ska visas.

---

## Steg 4: Hämta kalkylbladet där Smart Markers är placerade

```csharp
            // Step 4: Get the worksheet where the Smart Markers are placed
            Worksheet worksheet = workbook.Worksheets[0];   // first sheet (index 0)
```

**Varför det första bladet?**  
De flesta mallar har master‑tabellen på det första bladet, men du kan referera till vilket blad som helst med namn (`workbook.Worksheets["SheetName"]`) om din design skiljer sig.

---

## Steg 5: Konfigurera SmartMarker‑processorn

`SmartMarkerProcessor` hanterar det tunga lyftet. Genom att sätta `DetailSheetNewName` instruerar vi Aspose.Cells att skapa ett nytt blad för varje nästlad samling.

```csharp
            // Step 5: Set up the SmartMarker processor and configure options
            SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
            smartMarkerProcessor.Options.DetailSheetNewName = "OrderDetails";
```

**Vad detta gör:**  
När processorn stöter på en samling inuti en samling (`Items`‑arrayen) skapar den ett nytt kalkylblad med namnet `OrderDetails` och fyller det med de relaterade raderna. Detta håller master‑bladet prydligt och speglar en typisk master‑detail‑rapportlayout.

---

## Steg 6: Bearbeta kalkylbladet med datakällan

```csharp
            // Step 6: Process the worksheet using the data source
            smartMarkerProcessor.Process(worksheet, orderData);
```

`Process`‑metoden ersätter varje Smart Marker med motsvarande värde från `orderData`. Den expanderar också rader vid behov, så du behöver inte förallokera utrymme i mallen.

---

## Steg 7: Spara den ifyllda arbetsboken

```csharp
            // Step 7: Save the populated workbook
            string outputPath = @"YOUR_DIRECTORY\masterDetail.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Resultat:**  
- `masterDetail.xlsx` innehåller ett master‑blad med order‑ID:n.  
- Ett nytt blad `OrderDetails` innehåller artikelnamnen för varje order.  
- All formatering (typsnitt, kantlinjer, kolumnbredder) från mallen bevaras.

Du kan öppna filen i Excel för att verifiera att datan matchar källobjektet.

---

## Fullständig källkod (klar att kopiera och klistra in)

```csharp
using System;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create the data source with master‑detail information
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Name = "A" },
                            new { Name = "B" }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Name = "C" }
                        }
                    }
                }
            };

            // Step 2: Load the Excel template that contains Smart Markers
            string templatePath = @"YOUR_DIRECTORY\template.xlsx";
            Workbook workbook = new Workbook(templatePath);

            // Step 3: Get the worksheet where the Smart Markers are placed
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 4: Set up the SmartMarker processor and configure options
            SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
            smartMarkerProcessor.Options.DetailSheetNewName = "OrderDetails";

            // Step 5: Process the worksheet using the data source
            smartMarkerProcessor.Process(worksheet, orderData);

            // Step 6: Save the populated workbook
            string outputPath = @"YOUR_DIRECTORY\masterDetail.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Förväntad utskrift i Excel**

| **Beställningar** (master sheet) |
|---|
| Id |
| 1 |
| 2 |

*OrderDetails* blad:

| **Artiklar** |
|---|
| Namn |
| A |
| B |
| C |

Rader läggs automatiskt till för att matcha antalet artiklar per order.

---

## Vanliga variationer och kantfall

| Situation | Hur du anpassar koden |
|-----------|-----------------------|
| **Flera detaljnivåer** (t.ex. Orders → Items → SubItems) | Lägg till en annan samlingsproperty (`SubItems`) och sätt `DetailSheetNewName` till ett annat värde för varje nivå. Aspose.Cells skapar automatiskt ytterligare blad. |
| **Anpassad bladnamngivning per master‑post** | Använd `smartMarkerProcessor.Options.DetailSheetNameFromData = true;` och inkludera ett `SheetName`‑fält i master‑samlingen. |
| **Stora datamängder (10 000+ rader)** | Anropa `workbook.Settings.MemorySetting = MemorySetting.MemoryOptimized;` innan du laddar mallen för att minska minnesförbrukningen. |
| **Mall utan detaljblad (platt rapport)** | Utelämna `DetailSheetNewName`; processorn skriver nästlad data direkt i master‑bladet och expanderar rader vid behov. |
| **Kör i ASP.NET Core** | Byt ut `Console.WriteLine` mot loggning (`ILogger`) och använd `Path.Combine` för att lösa filplatser relativt `wwwroot`. |

---

## Tips för pålitlig Excel‑generering

* **Behåll platshållare i en separat rad** – Smart Markers expanderar rader under markören; att placera dem i rubrikraden bevarar formateringen.  
* **Undvik att slå ihop celler i datasegmentet** – Sammanfogade celler kan orsaka oväntade radförskjutningar vid expansion.  
* **Testa först med en minimal datamängd**; när layouten fungerar, skala upp till riktig data.  
* **Version lås** – Registrera den Aspose.Cells‑version du använde (`Aspose.Cells 23.12`) för att undvika brytande förändringar vid uppgradering.

---

## Slutsats

Du vet nu hur du **genererar Excel från mall** i C# med Aspose.Cells Smart Markers, och du kan enkelt utöka samma mönster för att **generera Excel‑rapport C#** för vilket master‑detail‑scenario som helst. Tillvägagångssättet separerar layout (mallen) från data (C#‑objektet), vilket ger dig en underhållbar, återanvändbar rapporteringsmotor.

Nästa, utforska dessa relaterade ämnen:

* **Formatera celler programatiskt** – lär dig hur du applicerar villkorlig formatering efter att data har fyllts i.  
* **Exportera till PDF** – Aspose.Cells kan konvertera den genererade arbetsboken till en PDF med ett enda anrop.  
* **Integrera med ASP.NET Core** – strömma den genererade filen direkt till webbläsaren utan att skriva till disk.

Kör koden, ändra mallen så den matchar ditt varumärke, och låt de genererade Excel‑rapporterna bli en kärnkomponent i dina .NET‑applikationer. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man genererar Excel‑rapport genom att slå ihop en Excel‑mall med Smart Markers](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-by-merging-an-excel-template-wi/)
- [Hur man genererar Excel‑rapport i C# – Fullständig guide med SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)
- [Aspose Cells Smart Markers: Generera Excel från modell i C#](/cells/english/net/smart-markers-dynamic-data/aspose-cells-smart-markers-generate-excel-from-model-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}