---
category: general
date: 2026-10-26
description: Lär dig hur du skapar en Excel-arbetsbok och infogar data i Excel med
  smarta markörer för att bygga en dynamisk Excel-rapport i C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- insert data into excel
- dynamic excel report
language: sv
lastmod: 2026-10-26
og_description: Skapa en Excel-arbetsbok och infoga data i Excel med C#-smartmarkörer.
  Följ den här guiden för att snabbt generera en dynamisk Excel-rapport.
og_image_alt: Screenshot showing a created excel workbook with populated data
og_title: Skapa Excel-arbetsbok med smarta markörer – steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to create excel workbook and insert data into excel using
    smart markers to build a dynamic excel report in C#.
  headline: How to create excel workbook with smart markers for a dynamic excel report
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Hur man skapar en Excel-arbetsbok med smarta markörer för en dynamisk Excel-rapport
url: /sv/net/smart-markers-dynamic-data/how-to-create-excel-workbook-with-smart-markers-for-a-dynami/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar excel-arbetsbok med smarta markörer för en dynamisk excel-rapport

Om du behöver **skapa excel-arbetsbok** programatiskt, visar den här guiden exakt hur. Genom att använda smarta markörer kan du **infoga data i excel** utan att skriva kod cell‑för‑cell, vilket gör att generera en **dynamisk excel-rapport** blir snabbt och underhållbart.

Du kommer att gå igenom varje steg—från att initiera arbetsboken till att bearbeta markörerna—så att du kan kopiera det kompletta, körbara exemplet till ditt eget projekt. Ingen extern dokumentation krävs; all kod och alla förklaringar finns nedan.

## Förutsättningar

* .NET 6.0 eller senare (exemplet fungerar även med .NET Framework 4.7+)
* En referens till **Aspose.Cells**-biblioteket (tillgängligt via NuGet `Install-Package Aspose.Cells`)
* Grundläggande kunskap om C# anonyma typer och LINQ
* En IDE såsom Visual Studio eller VS Code

> **Proffstips:** Använd den kostnadsfria Aspose.Cells-utvärderingslicensen för testning; ersätt den med en full licens innan produktion.

## Steg 1: Skapa excel-arbetsbok och få åtkomst till det första kalkylbladet

Den första operationen är att instansiera ett `Workbook`-objekt. Detta objekt representerar hela Excel-filen i minnet och ger dig direkt åtkomst till dess kalkylblad.

```csharp
using Aspose.Cells;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new workbook – this is the core object for any Excel manipulation
            Workbook wb = new Workbook();

            // The workbook always contains at least one worksheet; we work with the first one
            Worksheet ws = wb.Worksheets[0];
```

Att skapa arbetsboken är grunden för alla **dynamiska excel-rapporter**. Utan detta objekt kan du inte placera smarta markörer eller senare spara filen.

## Steg 2: Placera smarta markörtaggar där data ska infogas

Smarta markörer är speciella platshållare som Aspose.Cells ersätter med data vid körning. De följer syntaxen `${Object.Property}` och kan representera enskilda rader, tabeller eller hierarkisk data.

```csharp
            // Insert a smart marker for the master (header) section
            ws.Cells[0, 0].PutValue("${Orders.Master}");

            // Insert a smart marker for the detail (row) section
            ws.Cells[1, 0].PutValue("${Orders.Detail}");
```

* Cellen `[0,0]` (A1) blir rubrikraden.
* Cellen `[1,0]` (A2) kommer att expandera till så många rader som det finns objekt i `Orders.Detail`.

Att placera markörer direkt i kalkylbladet betyder att du senare **infogar data i excel** automatiskt, vilket eliminerar manuella loopar.

## Steg 3: Förbered datakällan som matchar de smarta markörerna

Smarta markörer kräver en datakälla vars struktur speglar markörhierarkin. Här använder vi ett anonymt objekt som innehåller en samling av beställningar. Varje beställning inkluderar en huvudrad och en samling av detaljrader.

```csharp
            // Build the data that matches the markers
            var data = new
            {
                Orders = GetOrders()
            };
```

`GetOrders`-metoden (visas nedan) returnerar en lista med `OrderInfo`-objekt. Varje `OrderInfo` innehåller ett `Master`-objekt för rubriken och en `Detail`-lista för raderna.

```csharp
        // Sample data generator – replace with your real data source (e.g., database, API)
        static List<OrderInfo> GetOrders()
        {
            return new List<OrderInfo>
            {
                new OrderInfo
                {
                    Master = new { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today },
                    Detail = new[]
                    {
                        new { Product = "Widget A", Qty = 10, Price = 9.99 },
                        new { Product = "Widget B", Qty = 5,  Price = 19.99 }
                    }
                },
                new OrderInfo
                {
                    Master = new { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1) },
                    Detail = new[]
                    {
                        new { Product = "Gadget X", Qty = 2, Price = 99.99 },
                        new { Product = "Gadget Y", Qty = 1, Price = 149.99 }
                    }
                }
            };
        }

        // Helper class to keep master/detail together
        class OrderInfo
        {
            public object Master { get; set; }
            public object[] Detail { get; set; }
        }
```

Att tillhandahålla en välstrukturerad datakälla säkerställer att **dynamiska excel-rapporten** expanderar korrekt för vilket antal beställningar som helst.

## Steg 4: Bearbeta de smarta markörerna för att fylla i kalkylbladet

Nu när arbetsboken innehåller markörer och datakällan är klar, anropa `ProcessSmartMarkers`. Aspose.Cells skannar kalkylbladet, ersätter varje markör med lämpliga värden och expanderar automatiskt rader för samlingar.

```csharp
            // Populate the worksheet by processing the smart markers
            wb.ProcessSmartMarkers(data);
```

Under bearbetning:

* `${Orders.Master}` blir en enskild rad som innehåller huvudfälten (`OrderId`, `Customer`, `Date`).
* `${Orders.Detail}` expanderar till flera rader, en per detaljpost, och behåller kolumnjusteringen.

## Steg 5: Spara arbetsboken och verifiera resultatet

Slutligen skriver du arbetsboken till en fysisk fil. Du kan öppna resultatet i vilket Excel‑kompatibelt program som helst för att bekräfta att data har infogats korrekt.

```csharp
            // Save the populated workbook to disk
            string outputPath = "DynamicReport.xlsx";
            wb.Save(outputPath, SaveFormat.Xlsx);

            System.Console.WriteLine($"Report generated: {outputPath}");
        }
    }
}
```

**Förväntat resultat:** När du öppnar `DynamicReport.xlsx` kommer du att se en rubrikrad för varje beställning följt av dess detaljrader. Antalet rader anpassas automatiskt till storleken på `Detail`-samlingarna, vilket är kärnan i en **dynamisk excel-rapport**.

![Excel workbook created with smart markers](excel-workbook.png)

*Image alt text:* *skapa excel-arbetsbok med smarta markörer som visar ifylld data.*

## Vanliga variationer och kantfall

| Scenario | Vad som ska ändras | Varför det är viktigt |
|----------|--------------------|-----------------------|
| **Olika bladlayout** | Flytta de smarta markörerna till ett annat blad (`wb.Worksheets[1]`) | Gör att du kan hålla mallar separata från databladen |
| **Nästlade samlingar** | Använd `${Orders.SubOrders.Detail}` och lägg till en `SubOrders`-egenskap i `OrderInfo` | Stöder flernivå master/detail-rapporter |
| **Stora datamängder** | Anropa `wb.CalculateFormula()` efter bearbetning om du har formler som beror på infogad data | Säkerställer att beräknade fält är uppdaterade |
| **Anpassad formatering** | Applicera stilobjekt på `ws.Cells` före bearbetning (t.ex. `Style style = wb.CreateStyle();`) | Garantierar enhetligt utseende över genererade rader |
| **Minnesbegränsade miljöer** | Använd `WorkbookFactory.Create` med en ström och `Dispose` objekt omedelbart | Förhindrar minnesläckor när många rapporter genereras i en tjänst |

## Bästa praxis för att infoga data i excel med smarta markörer

* **Håll mallen ren:** Placera endast de markörer du behöver; extra celler kan orsaka oväntad dataplacering.
* **Matcha egenskapsnamn exakt:** Smarta markörer är skiftlägeskänsliga; ett stavfel resulterar i tomma celler utan fel.
* **Återanvänd samma dataobjekt:** Om du behöver generera flera blad från samma källa, anropa `ProcessSmartMarkers` upprepade gånger med samma `data`-instans.
* **Validera data före bearbetning:** Null‑referenser i datakällan kommer att producera tomma celler; skydda mot dem med `?.` eller standardvärden.

## Slutsats

Du vet nu hur du **skapar excel-arbetsbok**, använder smarta markörer för att **infoga data i excel**, och producerar en **dynamisk excel-rapport** som automatiskt skalar med dina data. Det kompletta kodexemplet kan kopieras in i vilket C#-projekt som helst, anpassas för dina egna datastrukturer och utökas med ytterligare formatering eller beräkningar.

### Nästa steg

* Utforska **infoga data i excel** med formler och diagram för att berika din rapport.
* Kombinera detta tillvägagångssätt med **dynamisk excel-rapport**-generering för flera kalkylblad (t.ex. ett blad per kund).
* Integrera lösningen i ett ASP.NET Core API för att leverera rapporter på begäran.

Lycka till med kodningen, och njut av att bygga flexibel Excel‑automatisering med Aspose.Cells!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Skapa Excel-arbetsbok programatiskt med Smart Markers](/cells/english/net/smart-markers-dynamic-data/create-excel-workbook-programmatically-using-smart-markers/)
- [Skapa Excel-arbetsbok C# – Fullständig guide för att infoga arrayer i celler](/cells/english/net/smart-markers-dynamic-data/create-excel-workbook-c-full-guide-to-inserting-arrays-into/)
- [Skapa Excel-arbetsbok och skriv data i C# – Fullständig steg‑för‑steg‑guide](/cells/english/net/excel-workbook/create-excel-workbook-and-write-data-in-c-full-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}