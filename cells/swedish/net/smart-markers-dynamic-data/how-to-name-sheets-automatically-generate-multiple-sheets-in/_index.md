---
category: general
date: 2026-02-09
description: Hur man namnger blad i C# med SmartMarker – lär dig att generera flera
  blad och automatisera bladnamngivning på bara några rader kod.
draft: false
keywords:
- how to name sheets
- generate multiple sheets
- automate sheet naming
- SmartMarker sheet naming
- workbook automation
language: sv
og_description: Hur du namnger blad i C# med SmartMarker-alternativ. Denna guide visar
  hur du genererar flera blad och automatiskt namnger dem utan ansträngning.
og_title: Hur man namnger blad automatiskt – Snabb C#-guide
tags:
- C#
- Aspose.Cells
- Excel automation
title: Hur du namnger blad automatiskt – Generera flera blad i C#
url: /sv/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man namnger blad automatiskt – Generera flera blad i C#

Har du någonsin undrat **hur man namnger blad** i en Excel-arbetsbok utan att manuellt klicka på “Rename” varje gång? Du är inte ensam. I många rapporteringsscenario slutar du med dussintals detaljblad som behöver systematiska namn, och att göra det för hand är en mardröm.  

Den goda nyheten är att med några rader C# kan du **generera flera blad** och **automatisera bladnamngivning** så att varje nytt detaljblad följer ett förutsägbart mönster. I den här handledningen går vi igenom den kompletta lösningen, förklarar varför varje del är viktig, och ger dig ett färdigt kodexempel att köra.

## Vad den här guiden täcker

* Att skapa en arbetsbok som innehåller SmartMarkers.
* Att konfigurera `SmartMarkerOptions` för att styra grundnamnet på genererade blad.
* Att köra `ProcessSmartMarkers` så att biblioteket skapar `Detail`, `Detail_1`, `Detail_2`, … automatiskt.
* Tips för att hantera kantfall såsom befintliga bladnamn eller anpassade namngivningskonventioner.
* Ett komplett, körbart exempel som du kan klistra in i Visual Studio och se resultatet omedelbart.

Ingen tidigare erfarenhet av Aspose.Cells krävs – bara en grundläggande C#-miljö och en IDE du föredrar.

## Förutsättningar

| Krav | Varför det är viktigt |
|-------------|----------------|
| .NET 6.0 eller senare | Moderna språkfunktioner och bibliotekskompatibilitet |
| Aspose.Cells for .NET (NuGet-paket) | Tillhandahåller `SmartMarker`-bearbetning och bladskapande |
| Ett tomt konsolprojekt (eller någon .NET-app) | Ger oss en plats att köra koden |

Installera biblioteket med:

```bash
dotnet add package Aspose.Cells
```

Nu när vi har grunderna på plats, låt oss dyka ner i den faktiska implementeringen.

## Steg 1: Skapa en arbetsbok med SmartMarkers

Först behöver vi en arbetsbok som innehåller en SmartMarker‑platshållare. Tänk på en SmartMarker som en malltagg som talar om för motorn var data ska injiceras och, i vårt fall, när ett nytt blad ska skapas.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣  Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // 2️⃣  Insert a SmartMarker that will trigger sheet creation
        // The marker {{detail}} tells Aspose.Cells to repeat the row for each item in the "detail" collection.
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // 3️⃣  Prepare sample data for the SmartMarker
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };
```

> **Proffstips:** Håll mallbladet lättviktigt. Endast de rader som behöver dupliceras bör innehålla SmartMarkers; allt annat förblir statiskt.

## Steg 2: Konfigurera SmartMarker‑alternativ – Kärnan i bladnamngivning

Nu kommer magin. Genom att sätta `DetailSheetNewName` talar vi om för motorn vilket grundnamn som ska användas för varje genererat blad. Biblioteket kommer att lägga till “_1”, “_2” osv. när grundnamnet redan finns.

```csharp
        // 4️⃣  Define naming options – this is where we answer “how to name sheets”
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // Primary keyword appears here: how to name sheets
            DetailSheetNewName = "Detail"   // Base name for all generated sheets
        };
```

Om du någonsin behöver ett annat konvention (t.ex. “Report_2023”), ändra bara strängen. Motorn hanterar kollisioner automatiskt, vilket är anledningen till att detta tillvägagångssätt **automatiserar bladnamngivning** utan extra kod.

## Steg 3: Bearbeta SmartMarkers och generera bladen

Med arbetsboken, data och alternativ redo utför ett enda metodanrop det tunga arbetet.

```csharp
        // 5️⃣  Run the SmartMarker processor – this will create Detail, Detail_1, Detail_2…
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // 6️⃣  Save the result so you can open it in Excel
        wb.Save("GeneratedSheets.xlsx");

        // 7️⃣  Let the user know we’re done
        System.Console.WriteLine("Workbook created – check GeneratedSheets.xlsx");
    }
}
```

### Förväntat resultat

När du öppnar *GeneratedSheets.xlsx* kommer du att se:

| Bladnamn | Innehåll |
|------------|---------|
| Template   | Den ursprungliga markeringslayouten (behållen för referens) |
| Detail     | Första uppsättningen rader (Apple, Banana, Cherry) |
| Detail_1   | Andra kopian – identisk data (användbart när du har flera samlingar) |
| Detail_2   | …och så vidare, beroende på hur många distinkta SmartMarker‑grupper du har |

Namnmönstret (`Detail`, `Detail_1`, `Detail_2`) demonstrerar **hur man namnger blad** programatiskt samtidigt som det **genererar flera blad** vid behov.

## Kantfall & Variationer

### 1. Befintliga bladnamn

Om din arbetsbok redan innehåller ett blad med namnet “Detail”, kommer motorn att börja med “Detail_1”. Detta förhindrar oavsiktliga överskrivningar.

### 2. Anpassade inkrementformat

Vill du ha “Detail‑A”, “Detail‑B” istället för numeriska suffix? Du kan efterbehandla namnen efter `ProcessSmartMarkers`:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet sh = wb.Worksheets[i];
    if (sh.Name.StartsWith("Detail_"))
    {
        string suffix = ((char)('A' + i - 1)).ToString(); // A, B, C…
        sh.Name = $"Detail-{suffix}";
    }
}
```

### 3. Flera SmartMarker‑grupper

Om din arbetsbok innehåller mer än en SmartMarker‑grupp (t.ex. `{{invoice}}` och `{{detail}}`), kommer varje grupp att generera sin egen uppsättning blad baserat på samma `DetailSheetNewName`. För att ge varje grupp ett distinkt prefix, skapa separata `SmartMarkerOptions`‑instanser och anropa `ProcessSmartMarkers` för varje samling.

## Praktiska tips från fältet

* **Proffstips:** Stäng av `AllowDuplicateNames` i `WorkbookSettings` om du vill att biblioteket ska kasta ett undantag istället för att tyst byta namn på blad. Detta hjälper till att fånga fel i namngivningslogik tidigt.
* **Se upp för:** Mycket långa grundnamn. Excel begränsar bladnamn till 31 tecken; biblioteket trunkerar automatiskt, men du kan sluta med tvetydiga namn.
* **Prestanda‑notering:** Att generera hundratals blad kan förbruka minne. Disposera arbetsboken (`wb.Dispose()`) så snart du är klar om du kör i en långlivad tjänst.

## Visuell översikt

![hur man namnger blad diagram](image.png "Diagram som visar flödet från SmartMarker‑mall till genererade blad – hur man namnger blad")

*Alt‑texten innehåller huvudnyckelordet för att uppfylla SEO.*

## Fullständig källkod (Klar‑för‑kopiering)

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and template sheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // SmartMarker layout
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // Sample data
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };

        // Configure naming – this answers how to name sheets
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"
        };

        // Process markers → generates Detail, Detail_1, Detail_2 …
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // Save and finish
        wb.Save("GeneratedSheets.xlsx");
        System.Console.WriteLine("Workbook created – open GeneratedSheets.xlsx to see the result.");
    }
}
```

Kör programmet, öppna den genererade filen, och du kommer att se bladen automatiskt namngivna enligt det mönster vi definierade.

## Slutsats

Du vet nu **hur man namnger blad** i en C#‑arbetsbok, hur man **genererar flera blad** med SmartMarker, och hur man **automatiserar bladnamngivning** så att du aldrig behöver byta namn på något för hand igen. Tillvägagångssättet skalar från ett fåtal detaljsidor till hundratals, och samma mönster fungerar för vilken samling du än matar in i `ProcessSmartMarkers`.

Vad är nästa steg? Prova att byta datakälla till en databasfråga, experimentera med anpassade suffixformat, eller kedja flera SmartMarker‑grupper för en fullfjädrad rapporteringsmotor. Himlen är gränsen när du låter biblioteket sköta det repetitiva namngivningsarbetet.

Om du tyckte att den här guiden var hjälpsam, ge den en stjärna på GitHub, dela den med kollegor, eller lämna en kommentar nedan med dina egna namngivningstrick. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}