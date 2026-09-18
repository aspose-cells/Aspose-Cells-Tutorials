---
category: general
date: 2026-02-23
description: Namnge Excel‑ark automatiskt och lär dig hur du genererar ark automatiskt
  med SmartMarkers. Steg‑för‑steg C#‑guide för dynamiska arbetsböcker.
draft: false
keywords:
- auto name excel sheets
- how to generate sheets
- Aspose.Cells SmartMarkers
- dynamic worksheet naming
- C# Excel automation
language: sv
og_description: Namnge Excel‑ark automatiskt på direkten. Lär dig hur du genererar
  ark med SmartMarkers i C# – komplett, körbart exempel.
og_title: Automatiskt namnge Excel‑ark – Snabb C#‑handledning
tags:
- C#
- Excel
- Aspose.Cells
title: Auto namnge Excel‑ark – Enkelt sätt att skapa ark
url: /sv/net/smart-markers-dynamic-data/auto-name-excel-sheets-easy-way-to-generate-sheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Automatiskt namnge Excel-blad – Komplett C#-handledning

Har du någonsin undrat hur man **automatiskt namnge Excel-blad** utan att skriva en loop som manuellt byter namn på varje flik? Du är inte ensam. I många rapporteringsprojekt ökar antalet blad vid körning, och att hålla namnen prydliga blir ett problem. De goda nyheterna? Med Aspose.Cells’ **SmartMarkers** kan du låta biblioteket hantera namngivningen åt dig, och det låter dig dessutom **hur man genererar blad** i realtid.

I den här guiden går vi igenom ett verkligt scenario: skapa en arbetsbok, konfigurera SmartMarker-alternativ så att detaljbladen automatiskt namnges *Detail*, *Detail1*, *Detail2*, …, och sedan verifiera att bladen visas som förväntat. I slutet har du en självständig, kopiera‑och‑klistra‑klar lösning som du kan anpassa till vilket projekt som helst som behöver dynamisk kalkylblads‑skapning.

---

## Vad du behöver

- **.NET 6+** (eller .NET Framework 4.6.2+). Koden fungerar på alla moderna runtime-miljöer.
- **Aspose.Cells for .NET** NuGet‑paket – `Install-Package Aspose.Cells`.
- Ett grundläggande C#‑projekt (Konsolapp, WinForms eller ASP.NET – samma kod fungerar överallt).
- Visual Studio, VS Code eller din favoriteditor.

Ingen extra Excel‑interop, ingen COM, bara ren hanterad kod.

---

## Steg 1: Automatiskt namnge Excel-blad med SmartMarkers

Det första du måste göra är att tala om för Aspose.Cells vilket basnamn du vill ha för de automatiskt skapade detaljbladen. Detta görs via klassen `SmartMarkerOptions`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;   // for SmartMarkers
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook that will hold the master sheet.
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Master";

        // -----------------------------------------------------------
        // Step 1: Configure SmartMarker options – set the base name
        // -----------------------------------------------------------
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // This tells SmartMarkers to create sheets named Detail, Detail1, Detail2, …
            DetailSheetNewName = "Detail"
        };
```

**Varför detta är viktigt:** Genom att sätta `DetailSheetNewName` överlämnar du namngivningslogiken till biblioteket. Du behöver inte skriva en `for`‑loop som kontrollerar befintliga bladnamn och ökar en räknare – API‑et gör det åt dig och garanterar unika namn även när datakällan innehåller dussintals rader.

---

## Steg 2: Förbered datakällan

SmartMarkers fungerar med vilken `IEnumerable`‑samling som helst, en `DataTable` eller till och med en enkel lista med objekt. För den här demonstrationen använder vi en enkel lista med objekt som representerar orderdetaljer.

```csharp
        // -----------------------------------------------------------
        // Step 2: Build a sample data source
        // -----------------------------------------------------------
        var orders = new[]
        {
            new { OrderId = 1001, Product = "Laptop", Qty = 2, Price = 1200.00 },
            new { OrderId = 1002, Product = "Mouse",   Qty = 5, Price =  25.99 },
            new { OrderId = 1003, Product = "Keyboard",Qty = 3, Price =  45.50 }
        };
```

**Varför detta är viktigt:** Datakällan styr hur många detaljblad som kommer att genereras. Varje element i samlingen skapar ett nytt blad baserat på SmartMarker‑mallen som vi lägger till härnäst.

---

## Steg 3: Infoga en SmartMarker‑mall i huvudbladet

En SmartMarker‑mall är bara en cell (eller ett område) som innehåller platshållare. När `Apply`‑metoden körs ersätts platshållarna med faktiska data, och för varje rad skapas ett nytt blad.

```csharp
        // -----------------------------------------------------------
        // Step 3: Add a SmartMarker template to the master sheet
        // -----------------------------------------------------------
        // Put a header row
        ws.Cells["A1"].PutValue("Order ID");
        ws.Cells["B1"].PutValue("Product");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["D1"].PutValue("Unit Price");

        // Insert SmartMarker placeholders starting at row 2
        ws.Cells["A2"].PutValue("&=orders.OrderId");
        ws.Cells["B2"].PutValue("&=orders.Product");
        ws.Cells["C2"].PutValue("&=orders.Qty");
        ws.Cells["D2"].PutValue("&=orders.Price");
```

**Varför detta är viktigt:** Syntaxen `&=` talar om för SmartMarkers att “ta värdet från datakällan”. När `Apply` körs kommer Aspose.Cells att kopiera den här raden till ett nytt blad för varje objekt i `orders`, och automatiskt namnge bladet baserat på alternativet vi satte tidigare.

---

## Steg 4: Använd SmartMarker‑alternativ – Här namnges bladen automatiskt

Nu kommer ögonblicket då biblioteket gör det tunga arbetet. `Apply`‑anropet läser mallen, skapar detaljbladen och namnger dem enligt `DetailSheetNewName`.

```csharp
        // -----------------------------------------------------------
        // Step 4: Apply SmartMarker – auto name excel sheets happens here
        // -----------------------------------------------------------
        ws.SmartMarkers.Apply(smartMarkerOptions, new { orders });

        // Save the workbook to verify the result
        wb.Save("AutoNamedSheets.xlsx");
        Console.WriteLine("Workbook saved. Open AutoNamedSheets.xlsx to see the result.");
    }
}
```

**Varför detta är viktigt:** `Apply`‑metoden fyller inte bara i data utan respekterar också det namnmönster vi angav. Om du öppnar *AutoNamedSheets.xlsx* kommer du att se:

- **Detail** – innehåller den första ordern.
- **Detail1** – andra ordern.
- **Detail2** – tredje ordern.

Ingen manuell namnändring krävs.

---

## Steg 5: Verifiera resultatet – Hur man genererar blad korrekt

Efter att ha kört programmet, öppna den genererade filen. Du bör se tre nya kalkylblad med exakt de namn som beskrivits ovan. Detta bevisar att du framgångsrikt har lärt dig **hur man genererar blad** automatiskt.

> **Proffstips:** Om du behöver ett eget suffix (t.ex. “_Report”), sätt bara `DetailSheetNewName = "Detail_Report"` så kommer biblioteket att lägga till siffror efter bassträngen.

---

## Kantfall & Vanliga frågor

### Vad händer om basnamnet redan finns?

Aspose.Cells kontrollerar befintliga bladnamn och lägger till ett inkrementellt nummer tills ett unikt namn hittas. Så även om ett blad med namnet *Detail* redan finns i arbetsboken, blir nästa genererade blad *Detail1*.

### Kan jag styra ordningen på de genererade bladen?

Ja. Ordningen följer sekvensen i datakällan. Om du behöver en specifik ordning, sortera samlingen innan du skickar den till `Apply`.

### Är det möjligt att generera blad i en annan arbetsbok?

Absolut. Skapa en andra `Workbook`‑instans, lägg till ett platshållarblad och anropa `Apply` på det bladet. Samma namngivningslogik gäller.

### Hur fungerar detta med stora datamängder?

SmartMarkers är optimerade för prestanda. Även med tusentals rader strömmar biblioteket data effektivt. Se bara till att du har tillräckligt med minne för den slutliga arbetsbokens storlek.

---

## Komplett fungerande exempel (Kopiera‑och‑klistra‑klart)

Nedan är hela programmet som du kan klistra in i ett nytt konsolprojekt. Inga delar saknas – allt från `using`‑direktiv till det sista `Save`‑anropet är med.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System;

class AutoNameExcelSheetsDemo
{
    static void Main()
    {
        // 1️⃣ Create workbook and master worksheet
        Workbook workbook = new Workbook();
        Worksheet master = workbook.Worksheets[0];
        master.Name = "Master";

        // 2️⃣ Set up SmartMarker options – this is the key to auto‑naming
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"   // base name for generated sheets
        };

        // 3️⃣ Sample data source – each element will become a new sheet
        var orders = new[]
        {
            new { OrderId = 1001, Product = "Laptop",   Qty = 2, Price = 1200.00 },
            new { OrderId = 1002, Product = "Mouse",    Qty = 5, Price =  25.99 },
            new { OrderId = 1003, Product = "Keyboard", Qty = 3, Price =  45.50 }
        };

        // 4️⃣ Build a simple template on the master sheet
        master.Cells["A1"].PutValue("Order ID");
        master.Cells["B1"].PutValue("Product");
        master.Cells["C1"].PutValue("Quantity");
        master.Cells["D1"].PutValue("Unit Price");

        master.Cells["A2"].PutValue("&=orders.OrderId");
        master.Cells["B2"].PutValue("&=orders.Product");
        master.Cells["C2"].PutValue("&=orders.Qty");
        master.Cells["D2"].PutValue("&=orders.Price");

        // 5️⃣ Apply SmartMarkers – this auto‑creates and auto‑names the sheets
        master.SmartMarkers.Apply(options, new { orders });

        // 6️⃣ Save and inform the user
        workbook.Save("AutoNamedSheets.xlsx");
        Console.WriteLine("Done! Open AutoNamedSheets.xlsx – you’ll see Detail, Detail1, Detail2 …");
    }
}
```

Kör programmet, öppna den resulterande *AutoNamedSheets.xlsx*, och du kommer att se funktionen **automatiskt namnge Excel-blad** i aktion.

---

## Vanligt förekommande uppföljningsfrågor

- **Kan jag använda detta med en befintlig mallfil?**  
  Ja. Ladda arbetsboken med `new Workbook("Template.xlsx")` och peka `master` på bladet som innehåller dina SmartMarker‑platshållare.

- **Vad händer om jag behöver olika namnkonventioner per bladtyp?**  
  Skapa flera `SmartMarkerOptions`‑objekt, var och en med sin egen `DetailSheetNewName`, och tillämpa dem på olika huvudblad.

- **Finns det ett sätt att dölja basbladet (det som innehåller mallen)?**  
  Efter `Apply` kan du helt enkelt ta bort huvudbladet: `workbook.Worksheets.RemoveAt(0);` – detaljbladen förblir orörda.

---

## Slutsats

Du vet nu **hur man automatiskt namnger Excel-blad** med Aspose.Cells SmartMarkers, och du har också sett ett robust mönster för **hur man genererar blad** dynamiskt i C#. Kärnidén är enkel: konfigurera `SmartMarkerOptions.DetailSheetNewName`, mata in en samling och låt biblioteket sköta resten. Detta tillvägagångssätt eliminerar onödiga loopar, garanterar unika namn och skalar smidigt.

Ready for the next step? Try swapping the data source for a `Data

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}