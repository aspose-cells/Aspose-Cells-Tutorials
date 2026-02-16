---
category: general
date: 2026-02-15
description: Skapa en ny arbetsbok i C# och kopiera en pivottabell utan att förlora
  dess definition. Lär dig hur du kopierar rader, bevarar pivottabellen och duplicerar
  pivottabellen enkelt.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- duplicate pivot table
language: sv
og_description: Skapa en ny arbetsbok i C# och kopiera en pivottabell samtidigt som
  du bevarar dess definition. Steg‑för‑steg‑guide för utvecklare.
og_title: Skapa ny arbetsbok i C# – bevara pivottabell
tags:
- Aspose.Cells
- C#
- Excel automation
title: Skapa ny arbetsbok i C# – Bevara pivottabell
url: /sv/net/pivot-tables/create-new-workbook-in-c-preserve-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa ny arbetsbok i C# – Bevara pivottabell

Har du någonsin behövt **create new workbook** i C# som innehåller en exakt kopia av en pivottabell från en annan fil? Du är inte ensam. I många rapporteringspipelines är pivottabellen hjärtat i analysen, och att förlora dess definition när du flyttar data är en mardröm.

Den goda nyheten? Med några rader Aspose.Cells‑kod kan du kopiera rader—inklusive pivottabellen—till en ny arbetsbok och behålla allt intakt. Nedan ser du **how to copy rows**, **preserve pivot table**‑inställningar, och till och med **duplicate pivot table** över filer utan att bryta formler eller cache.

## Vad den här handledningen täcker

I den här guiden går vi igenom:

1. Laddar in källarbetsboken som redan har en pivottabell.  
2. **Create new workbook**‑objekt för destinationen.  
3. Använder `CopyRows` för att överföra området som innehåller pivottabellen.  
4. Sparar resultatet samtidigt som pivottabellen förblir funktionell.  

Ingen extern dokumentation behövs—bara koden, förklaringen, och ett antal praktiska tips som du kan klistra in direkt i ditt projekt.

> **Pro tip:** Aspose.Cells fungerar med .NET Core, .NET Framework och även Xamarin, så samma kodsnutt körs var du än behöver den.

![Skapa ny arbetsbok med kopierad pivottabell](/images/create-new-workbook-pivot.png "skapa ny arbetsbok med kopierad pivottabell")

## Steg 1 – Skapa ny arbetsbok och ladda källfilen

Det första vi gör är **create new workbook**‑objekt. Ett innehåller den ursprungliga datan, det andra kommer att ta emot det kopierade området.

```csharp
using Aspose.Cells;

// Load the source workbook that already contains a pivot table
var sourceWorkbook = new Workbook(@"C:\Data\source.xlsx");

// Create an empty workbook that will become the destination
var destinationWorkbook = new Workbook();
```

*Varför detta är viktigt:*  
`Workbook` är startpunkten för all Excel‑manipulation i Aspose.Cells. Genom att instansiera en ny arbetsbok garanterar vi en ren start—inga dolda stilar eller lösa kalkylblad som kan störa senare.

## Steg 2 – Hur man kopierar rader inklusive en pivottabell

Nu kommer kärnan i problemet: **how to copy rows** som omsluter pivottabellen utan att platta till den. Metoden `CopyRows` gör exakt det.

```csharp
// Copy the first 20 rows (adjust as needed) from the source to the destination
// Parameters: startRow, totalRows, targetCells, targetStartRow
sourceWorkbook.Worksheets[0].Cells.CopyRows(
    startRow: 0,
    totalRows: 20,
    targetCells: destinationWorkbook.Worksheets[0].Cells,
    targetStartRow: 0);
```

Några saker att notera:

* `startRow` och `totalRows` definierar blocket som innehåller pivottabellen.  
* Metoden kopierar **both** rådata och pivottabellens cache, så destinationens arbetsbok vet hur den ska bygga om pivottabellen i farten.  
* Om din pivottabell börjar längre ner i bladet, ändra bara indexen—ingen annan API‑anrop behövs.

> **Common question:** *Kommer den kopierade pivottabellen att förlora sin källdatareferens?*  
> Nej. Aspose.Cells bäddar in cachen direkt i kalkylbladet, så pivottabellen blir självständig i den nya filen.

## Steg 3 – Bevara pivottabell vid sparande av destinationen

Efter att raderna har kopierats lever pivottabellen i destinationsarbetsboken exakt som i källan. Att spara filen är enkelt.

```csharp
// Save the destination workbook; the pivot table remains functional
destinationWorkbook.Save(@"C:\Data\destination.xlsx");
```

När du öppnar `destination.xlsx` i Excel ser du pivottabellen redo att uppdateras. Beteendet **preserve pivot table** är automatiskt eftersom cachen följde med raderna.

### Verifiera resultatet

Öppna filen och:

1. Klicka på pivottabellen.  
2. Lägg märke till att fältlistan visas—det betyder att cachen är intakt.  
3. Försök med en uppdatering; datan uppdateras utan fel.

Om du stöter på ett *#REF!*‑fel, dubbelkolla att det kopierade området inkluderar de dolda cache‑raderna (vanligtvis precis efter den synliga datan).

## Steg 4 – Duplicera pivottabell till flera arbetsböcker (valfritt)

Ibland behöver du samma pivottabell i flera rapporter. Mönstret vi just använde skalar bra—upprepa bara kopieringen för varje ny arbetsbok.

```csharp
string[] targets = {
    @"C:\Reports\Q1.xlsx",
    @"C:\Reports\Q2.xlsx",
    @"C:\Reports\Q3.xlsx"
};

foreach (var path in targets)
{
    var wb = new Workbook(); // fresh workbook each loop
    sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 20, wb.Worksheets[0].Cells, 0);
    wb.Save(path);
}
```

Detta kodsnutt **duplicates pivot table** tre gånger med en enda loop. Anpassa `targets`‑arrayen så att den matchar ditt rapporteringsschema.

### Särskilda fall att tänka på

| Situation | Vad du bör hålla utkik efter | Lösning |
|-----------|-----------------------------|---------|
| Pivottabell använder extern datakälla | Cachen kan referera till en anslutning som inte finns på den nya maskinen | Bädda in datakällan eller återskapa anslutningen i destinationsarbetsboken |
| Mycket stor pivottabell ( > 100 k rader ) | `CopyRows` kan vara minnesintensiv | Använd `CopyRows` i delar eller överväg `Copy` med `PasteOptions` för att begränsa minnesanvändning |
| Arbetsbladet har dolda rader/kolumner | Dolda cache‑rader kan hoppas över om du bara kopierar synliga rader | Kopiera alltid exakt det radområde som innehåller cachen, inte bara det synliga området |

## Fullt fungerande exempel

Sätter vi ihop allt, här är ett självständigt program som du kan klistra in i en konsolapp.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook (contains the original pivot)
            var sourcePath = @"C:\Data\source.xlsx";
            var sourceWorkbook = new Workbook(sourcePath);

            // 2️⃣ Prepare destination workbook
            var destinationWorkbook = new Workbook();

            // 3️⃣ Copy rows that include the pivot (adjust range as needed)
            sourceWorkbook.Worksheets[0].Cells.CopyRows(
                startRow: 0,
                totalRows: 20,
                targetCells: destinationWorkbook.Worksheets[0].Cells,
                targetStartRow: 0);

            // 4️⃣ Save – the pivot table is preserved
            var destPath = @"C:\Data\destination.xlsx";
            destinationWorkbook.Save(destPath);

            Console.WriteLine("Pivot table successfully copied!");
        }
    }
}
```

Kör programmet, öppna `destination.xlsx`, och du kommer att se samma pivottabell redo att skära och analysera din data. Ingen manuell återuppbyggnad behövs.

---

## Slutsats

Vi har just visat hur man **create new workbook** i C# och **copy pivot table** samtidigt som alla inställningar behålls. Genom att använda `CopyRows` får du ett pålitligt sätt att **preserve pivot table**‑funktionalitet, svara på den gamla frågan “**how to copy rows**”, och till och med **duplicate pivot table** över flera rapporter med minimal kod.

Nästa steg? Prova att ändra det kopierade området så att det inkluderar diagram som refererar till samma pivottabell, eller experimentera med `PasteOptions` för att behålla formatering exakt. Samma mönster fungerar för andra Aspose.Cells‑objekt som tabeller och namngivna områden, så känn dig fri att utöka det.

Har du en variant du kämpar med—kanske en pivottabell som hämtar data från en extern DB, eller en arbetsbok som ligger i molnet? Lämna en kommentar nedan, så tar vi itu med den tillsammans. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}