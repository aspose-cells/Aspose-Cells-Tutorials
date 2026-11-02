---
category: general
date: 2026-05-23
description: Generera Excel från JSON i C# snabbt. Lär dig hur du laddar JSON i Excel,
  skapar en Excel-arbetsbok programatiskt och sparar arbetsboken till en fil.
draft: false
keywords:
- generate excel from json
- load json into excel
- save workbook to file
- create excel workbook programmatically
language: sv
og_description: Generera Excel från JSON med C#. Den här guiden visar hur du laddar
  JSON i Excel, skapar en Excel‑arbetsbok programatiskt och sparar arbetsboken till
  en fil.
og_title: Generera Excel från JSON med C# – Fullständig programmeringshandledning
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Generate Excel from JSON in C# quickly. Learn how to load JSON into
    Excel, create Excel workbook programmatically, and save workbook to file.
  headline: Generate Excel from JSON with C# – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- JSON
- Excel Automation
title: Generera Excel från JSON med C# – Komplett steg‑för‑steg‑guide
url: /sv/net/data-loading-and-parsing/generate-excel-from-json-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Generera Excel från JSON med C# – Komplett steg‑för‑steg‑guide

Har du någonsin undrat hur man **genererar Excel från JSON** utan att öppna Excel manuellt? Du är inte ensam. Många utvecklare behöver omvandla API‑svar, konfigurationsfiler eller enkla datautskrifter till färdiga kalkylblad—snabbt, pålitligt och utan användarinteraktion.  

I den här handledningen går vi igenom en ren, end‑to‑end‑lösning som **läser in JSON i Excel**, bygger arbetsboken helt i kod och slutligen **sparar arbetsboken till fil**. När du är klar har du ett återanvändbart kodsnutt som du kan lägga in i vilket .NET‑projekt som helst.

> **Proffstips:** Metoden fungerar med vilken JSON‑struktur som helst som kan mappas till en platt tabell. För nästlade objekt kommer vi att diskutera en snabb lösning senare.

## Vad du behöver

- **.NET 6+** (eller .NET Framework 4.6+).  
- **Aspose.Cells for .NET** – biblioteket som driver Smart Marker‑motorn vi kommer att använda.  
- En JSON‑payload (exemplet använder en liten orderlista).  
- Din favorit‑IDE (Visual Studio, Rider eller VS Code).  

Inga andra tredjepartsverktyg behövs; allt körs i minnet.

## Steg 1 – Skapa en Excel‑arbetsbok programatiskt

Det första som alla Excel‑automatiseringar gör är att skapa ett arbetsboks‑objekt. Tänk på det som en tom duk som du kan måla på.

```csharp
using Aspose.Cells;          // Excel manipulation
using Aspose.Cells.Tables;   // Smart Marker support
using System;

class ExcelFromJsonDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook in memory
        Workbook workbook = new Workbook();
```

Varför skapa arbetsboken i kod? Det garanterar att filen **skapas programatiskt**, undviker filsystem‑race‑conditions och låter dig köra hela pipeline:n på en server utan UI.

## Steg 2 – Infoga en Smart Marker‑platshållare

Smart Markers är Asposes svar på kopplad utskrift för kalkylblad. Genom att placera en enda platshållare som `${Orders:ArrayAsSingle}` i en cell vet biblioteket att automatiskt expandera JSON‑arrayen till rader.

```csharp
        // Step 2: Put a Smart Marker into cell A1 (first worksheet, first cell)
        workbook.Worksheets[0].Cells[0, 0].PutValue("${Orders:ArrayAsSingle}");
```

Om du är ny på Smart Markers, föreställ dig att skriva `${Orders:ArrayAsSingle}` som en malltagg som säger “när du ser detta, skriv ut varje objekt i *Orders*-samlingen som en separat rad”.

## Steg 3 – Anslut SmartMarkerProcessor

Processorn är motorn som läser platshållaren, parsar JSON‑en och fyller i bladet.

```csharp
        // Step 3: Initialise the processor with the workbook we just prepared
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

Varför anropa `Workbook.Save` direkt? För att datan ännu inte finns. Processorn bygger bron mellan rå JSON och Excel‑layouten.

## Steg 4 – Definiera JSON‑data att läsa in

Här är en liten JSON‑array som representerar två order. I ett riktigt scenario kan du hämta detta från ett REST‑API, läsa en fil eller bygga det i farten.

```csharp
        // Step 4: JSON that will populate the Smart Marker
        string jsonData = "[{\"Id\":1,\"Total\":99.9},{\"Id\":2,\"Total\":45.0}]";
```

Observera att vi håller JSON‑en **platt**—varje objekt innehåller bara primitiva fält. Detta matchar “ladda JSON i Excel”-mönstret på det renaste sättet. Om du har nästlade objekt måste du först platta till dem (se *Avancerat tips* i slutet).

## Steg 5 – Applicera JSON på arbetsboken

Nu händer magin. Processorn läser JSON‑en, expanderar Smart Marker och skriver rader för varje objekt.

```csharp
        // Step 5: Apply JSON – the Smart Marker expands automatically
        processor.ApplyJson(jsonData);
```

Bakom kulisserna skapar Aspose en temporär datatabell, mappar varje egenskap (`Id`, `Total`) till en kolumn och infogar raderna precis under platshållaren. Inga loopar, ingen manuell celladressning—bara deklarativ transformation.

## Steg 6 – Spara arbetsboken till fil

Till sist sparar vi den fyllda arbetsboken till disk.

```csharp
        // Step 6: Save the populated workbook to a physical file
        string outputPath = @"C:\Temp\OrdersReport.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Steget **spara arbetsbok till fil** är den sista pusselbiten. Aspose skriver den slutgiltiga `.xlsx` med Open XML under huven, så filen är fullt kompatibel med Excel, Google Sheets och LibreOffice.

## Fullt fungerande exempel (alla steg kombinerade)

Nedan är det kompletta programmet som du kan kopiera‑klistra in och köra. Se till att Aspose.Cells‑NuGet‑paketet är installerat (`dotnet add package Aspose.Cells`).

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System;

class ExcelFromJsonDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Insert Smart Marker placeholder in cell A1
        workbook.Worksheets[0].Cells[0, 0].PutValue("${Orders:ArrayAsSingle}");

        // 3️⃣ Initialise SmartMarkerProcessor
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

        // 4️⃣ JSON data (could come from a file, API, etc.)
        string jsonData = "[{\"Id\":1,\"Total\":99.9},{\"Id\":2,\"Total\":45.0}]";

        // 5️⃣ Apply JSON – Smart Marker expands automatically
        processor.ApplyJson(jsonData);

        // 6️⃣ Save the workbook to disk
        string outputPath = @"C:\Temp\OrdersReport.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Förväntat resultat

När du öppnar `OrdersReport.xlsx` kommer du att se:

| Id | Total |
|----|-------|
| 1  | 99.9  |
| 2  | 45.0  |

Kolumnrubrikerna genereras automatiskt från JSON‑egenskapsnamnen, och varje array‑element blir en ny rad. Ingen manuell celladressning krävs.

## Avancerat tips – Hantera större eller nästlad JSON

Om din JSON innehåller **nästlade objekt** (t.ex. en `Order` med ett `Customer`‑subobjekt), kan Smart Markers fortfarande hjälpa till men du måste först platta till strukturen:

```csharp
// Example flattening using Newtonsoft.Json.Linq
var jArray = JArray.Parse(jsonData);
var flatList = jArray.Select(item => new {
    Id = (int)item["Id"],
    Total = (decimal)item["Total"],
    CustomerName = (string)item["Customer"]["Name"]
}).ToList();
string flatJson = JsonConvert.SerializeObject(flatList);
processor.ApplyJson(flatJson);
```

Detta tillvägagångssätt håller flödet **ladda json i excel** smidigt, även för komplex data.

## Vanliga fallgropar & hur man undviker dem

| Problem | Varför det händer | Lösning |
|---------|-------------------|---------|
| **Saknad Aspose.Cells‑licens** | Gratisversionen lägger till ett vattenstämpel. | Skaffa en licensfil och registrera den via `License license = new License(); license.SetLicense("Aspose.Cells.lic");` |
| **Fel i platshållare** | Smart Marker‑taggar är skiftlägeskänsliga. | Dubbelkolla stavningen och hakparenteserna i `${Orders:ArrayAsSingle}`. |
| **Stor JSON orsakar minnespress** | Hela JSON‑en laddas in i RAM. | Strömma JSON‑en eller bearbeta i batchar, och slå sedan ihop arbetsblad. |
| **Datumformatet stämmer inte** | JSON‑datum visas som råa ticks. | Använd `JsonSerializerSettings` för att formatera datum, eller lägg till ett anpassat kolumnformat efter bearbetning. |

## Varför denna metod slår manuell loopning

- **Deklarativ**: Du beskriver *vad* du vill ha (en tabell) snarare än *hur* du ska iterera rader.  
- **Prestanda**: Smart Markers använder optimerade interna buffertar, ofta snabbare än naiva `for`‑loopar.  
- **Underhållbarhet**: Att byta datakälla (CSV, DB, API) kräver bara att du byter JSON‑strängen—inga kodändringar i Excel‑logiken.  
- **Skalbarhet**: Samma mall kan återanvändas för dussintals rapporter med olika datastrukturer.

## Slutsats

Vi har just demonstrerat hur man **genererar Excel från JSON** i C# genom att **ladda JSON i Excel**, **skapa en Excel‑arbetsbok programatiskt** och slutligen **spara arbetsboken till fil**. Hela pipeline:n körs i minnet, kräver bara några få kodrader och producerar ett rent, färdigt kalkylblad att dela.

Vill du gå längre? Prova att lägga till villkorsstyrd formatering, infoga diagram eller exportera direkt till PDF—allt är möjligt med samma `Workbook`‑objekt. Huvudpoängen: Smart Markers omvandlar JSON till Excel‑tabeller med nästan ingen boilerplate.

Har du frågor om hur du hanterar specifika JSON‑strukturer eller justerar utdataformatet? Lämna en kommentar eller skriv i diskussionen nedan. Lycka till med kodandet!

![Generera Excel från JSON med C# – skärmbild av den resulterande OrdersReport.xlsx](/images/generate-excel-from-json.png "generera excel från json")

*Bildtext:* generera excel från json – visuell resultat av handledningen.

## Relaterade handledningar

- [Hur man skapar och sparar en Excel‑arbetsbok som ODS med Aspose.Cells för .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Skapa och spara Excel‑arbetsbok som PDF i ASP.NET med Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Importera JSON‑data till Excel med Aspose.Cells Java: En omfattande guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}