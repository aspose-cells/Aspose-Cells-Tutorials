---
category: general
date: 2026-02-21
description: Upprepa data i Excel snabbt med SmartMarker — lär dig hur du fyller i
  en Excel‑mall och enkelt upprepar rader.
draft: false
keywords:
- repeat data in excel
- populate excel template
- how to repeat rows
- repeat rows in excel
- populate excel from data
language: sv
og_description: Upprepa data i Excel med SmartMarker. Lär dig hur du fyller i en Excel-mall,
  upprepar rader och automatiserar dina kalkylblad.
og_title: Upprepa data i Excel – Populera mall med SmartMarker
tags:
- excel
- csharp
- smartmarker
- automation
title: Upprepa data i Excel – Fyll i mall med SmartMarker
url: /sv/net/smart-markers-dynamic-data/repeat-data-in-excel-populate-template-with-smartmarker/
---

ar behövs."

Next horizontal line.

## Conclusion -> "## Slutsats"

Paragraph translate.

At end: "and generally **" seems cut off. Keep as is.

Then closing shortcodes.

Make sure to preserve all shortcodes and code block placeholders.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# upprepa data i excel – Fyll i mall med SmartMarker

Har du någonsin behövt **upprepa data i Excel** men var osäker på hur du undviker manuellt copy‑pasting? Du är inte ensam. I många rapporteringsscenario har du en lista med objekt som måste expandera till rader automatiskt, och att göra det för hand är en recept på fel.

Här är grejen—genom att använda `SmartMarkerProcessor` från **GemBox.Spreadsheet**‑biblioteket kan du **populate an Excel template** med en enda rad C# och låta rader upprepas för varje objekt i din samling. I den här guiden går vi igenom de exakta stegen, visar dig den kompletta koden och förklarar varför varje del är viktig, så att du tryggt kan **repeat rows in Excel** utan att svettas.

## Vad du kommer att lära dig

* Hur du definierar datastrukturen som driver upprepningsoperationen.  
* Hur du kopplar en `SmartMarkerProcessor` till en arbetsbok som innehåller ett dolt mallark.  
* Hur markören `${Repeat:Item}` expanderar till flera rader automatiskt.  
* Tips för att hantera kantfall som tomma samlingar eller anpassad formatering.  

När du är klar med den här tutorialen kommer du att kunna **populate excel from data** på ett sätt som skalar, är lätt att underhålla och fungerar med alla .NET‑projekt.

---

## Förutsättningar

* .NET 6.0 eller senare (koden använder moderna C#‑funktioner).  
* NuGet‑paketet **GemBox.Spreadsheet** (gratisversionen fungerar för upp till 150 rader).  
* En grundläggande Excel‑mallfil (`Template.xlsx`) med ett dolt ark som heter `HiddenTemplate`.  
* Bekantskap med C#‑objekt och LINQ är hjälpsamt men inte obligatoriskt.

---

## Steg 1 – Definiera upprepningsdatastrukturen

Först behöver du en datakälla som SmartMarker‑motorn kan iterera över. I de flesta verkliga appar kommer detta från en databas, ett API eller en CSV‑fil. För tydlighetens skull använder vi en anonym typ med en enda egenskap som heter `Item` och som innehåller en array av strängar.

```csharp
// Step 1: Define the data that will be repeated in the template
var repeatData = new { Item = new[] { "A", "B", "C" } };
```

> **Varför detta är viktigt:** Markören `${Repeat:Item}` i Excel‑mallen letar efter en egenskap som heter `Item`. Om du byter namn på egenskapen, uppdatera markören därefter. Denna täta koppling säkerställer att mallen hålls i synk med din kod, vilket gör det enklare att **populate excel template** utan att gissa kolumnnamn.

### Vanliga variationer

* **Komplexa objekt:** Istället för en enkel strängarray kan du leverera en lista med objekt (`new[] { new { Name = "A", Qty = 10 } }`). Markören kommer att upprepa rader och du kan referera till `${Item.Name}` och `${Item.Qty}` i arket.  
* **Tomma samlingar:** Om `Item` är tomt tar SmartMarker helt enkelt bort upprepningsblocket, vilket lämnar mallen orörd—perfekt för valfria sektioner.

---

## Steg 2 – Skapa SmartMarkerProcessor för det dolda mallarket

Läs in din arbetsbok och skapa en `SmartMarkerProcessor`. Peka den på arbetsboken som innehåller det dolda mallarket; SmartMarker kommer att kopiera det arket till ett synligt och expandera upprepningsmarkörerna.

```csharp
using GemBox.Spreadsheet;

// Load the workbook that holds the hidden template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Step 2: Create a SmartMarkerProcessor for the workbook that holds the hidden template sheet
var processor = new SmartMarkerProcessor(wb);
```

> **Pro tip:** Om du har flera mallar i samma fil kan du ange källarkets namn när du anropar `processor.Process`. Detta hjälper när du behöver **repeat rows in excel** för olika sektioner av en rapport.

### Hantering av kantfall

* **Saknat mallark:** Omge laddningen med try/catch och logga ett tydligt fel—detta förhindrar tysta fel när filvägen är fel.  
* **Stora dataset:** För tusentals rader, överväg att strömma utdata till en fil (`processor.Save`) istället för att hålla allt i minnet.

---

## Steg 3 – Tillämpa data och expandera markören `${Repeat:Item}`

Nu kommer den magiska raden som faktiskt upprepar raderna. Skicka objektet du skapade i Steg 1 till `processor.Process`. SmartMarker hittar varje `${Repeat:Item}`‑markör, duplicerar raden för varje element och ersätter platshållarna med de faktiska värdena.

```csharp
// Step 3: Apply the data to the template, expanding the ${Repeat:Item} marker
processor.Process(repeatData);

// Save the resulting workbook.
wb.Save("Result.xlsx");
```

### Vad du bör se

När du öppnar `Result.xlsx` har det dolda mallarket kopierats till ett nytt synligt ark (standardnamnet `Sheet1`). Raden som innehöll `${Repeat:Item}` visas nu tre gånger, med cellerna **A**, **B** och **C** respektive.

| Item |
|------|
| A    |
| B    |
| C    |

Om du lade till fler kolumner som `${Item.Price}` skulle de fyllas i automatiskt från datakällan.

---

## Hur man upprepar rader i Excel utan SmartMarker (snabb jämförelse)

| Metod                  | Kodkomplexitet | Underhåll | Prestanda |
|------------------------|----------------|-----------|-----------|
| Manual copy‑paste      | High           | Low       | Poor      |
| VBA macro              | Medium         | Medium    | Good      |
| **SmartMarkerProcessor**| Low          | High      | Excellent |

Som du kan se ger användning av SmartMarker för att **repeat data in excel** den renaste separationen mellan malldesign och affärslogik. Det är också språk‑oberoende—liknande koncept finns i Java, Python och JavaScript‑bibliotek.

---

## Avancerade tips & vanliga fallgropar

### 1. Formatera de upprepade raderna

SmartMarker kopierar hela raden—including cell styles, borders, and conditional formatting. Om du behöver en annan stil för den första eller sista raden, lägg till extra markörer som `${If:Item.IsFirst}` och använd villkorliga formler i Excel.

### 2. Hantera stora dataset

När du arbetar med > 10 000 rader, inaktivera Excels automatiska beräkning innan bearbetning:

```csharp
wb.WorkbookOptions = new WorkbookOptions { RecalculateAllFormulas = false };
```

Aktivera den igen efter sparning för att hålla prestandan snabb.

### 3. Fyll i Excel från data i en riktig databas

```csharp
var orders = dbContext.Orders
    .Where(o => o.Date >= start && o.Date <= end)
    .Select(o => new { o.OrderId, o.CustomerName, o.Total })
    .ToArray();

processor.Process(new { Order = orders });
```

Använd sedan `${Repeat:Order}` i mallen för att lista varje order. Detta mönster visar hur enkelt det är att **populate excel from data** direkt från Entity Framework.

### 4. Använda flera upprepningsblock

Du kan ha flera `${Repeat:...}`‑markörer på samma blad eller på olika blad. SmartMarker bearbetar dem sekventiellt, så ordningen spelar bara roll om ett block beror på resultatet från ett annat.

---

## Komplett körbart exempel

Nedan är en självständig konsolapplikation som du kan klistra in i Visual Studio och köra omedelbart. Den demonstrerar alla tre stegen samt sparar filen.

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License free version (up to 150 rows). For production use, set your license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Define the data to repeat.
        var repeatData = new { Item = new[] { "A", "B", "C" } };

        // 2️⃣ Load the template workbook (ensure Template.xlsx exists next to the exe).
        var wb = ExcelFile.Load("Template.xlsx");

        // Create processor bound to the workbook.
        var processor = new SmartMarkerProcessor(wb);

        // 3️⃣ Process the data – this expands the ${Repeat:Item} marker.
        processor.Process(repeatData);

        // Save the populated workbook.
        wb.Save("Result.xlsx");

        Console.WriteLine("Excel file generated successfully – check Result.xlsx");
    }
}
```

**Förväntad output:** `Result.xlsx` innehåller ett ark där raden med `${Repeat:Item}` visas tre gånger, med A, B och C. Inga manuella justeringar behövs.

---

## Slutsats

Du vet nu hur du **repeat data in excel** effektivt genom att utnyttja SmartMarkerProcessor. Genom att definiera ett enkelt dataobjekt, ladda en mallarbok och anropa `Process` kan du **populate excel template**, **repeat rows in excel**, och generellt **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}