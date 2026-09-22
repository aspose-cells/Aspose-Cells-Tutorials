---
category: general
date: 2026-03-18
description: Lär dig hur du genererar Excel från JSON med C#, tillåter dubblettbladnamn,
  skapar detaljblad och sparar arbetsboken i C# på några minuter.
draft: false
keywords:
- generate excel from json
- allow duplicate sheet names
- how to create detail sheet
- save workbook c#
- smartmarker options
- aspnet cells integration
language: sv
og_description: Generera Excel från JSON med C#. Den här guiden visar hur du tillåter
  dubbla bladnamn, skapar ett detaljblad och sparar arbetsboken i C# med Aspose.Cells.
og_title: Generera Excel från JSON i C# – Komplett handledning
tags:
- C#
- Excel automation
- JSON
- Aspose.Cells
title: Generera Excel från JSON i C# – Steg‑för‑steg guide
url: /sv/net/excel-data-import-export/generate-excel-from-json-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Generera Excel från JSON i C# – Steg‑för‑steg‑guide

Har du någonsin behövt **generera Excel från JSON** men varit osäker på vilket bibliotek som klarar jobbet? Du är inte ensam. I många företagsapplikationer får vi payloads som JSON och måste föra in den datan i snyggt formaterade kalkylblad – tänk försäljningsrapporter, lagerutdrag eller revisionsloggar. Den goda nyheten? Med Aspose.Cells SmartMarker‑motor kan du omvandla en JSON‑sträng till en fullfjädrad Excel‑fil på bara några rader kod.

I den här handledningen går vi igenom hela processen: från att förbereda JSON‑payloaden, konfigurera SmartMarker för att **tillåta dubblettbladnamn**, skapa ett **detaljblad**, och slutligen **spara arbetsboken C#‑stil**. När du är klar har du ett återanvändbart kodexempel som du kan slänga in i vilket .NET‑projekt som helst.

> **Snabb sammanfattning:**  
> • Huvudmål – generera Excel från JSON.  
> • Delmål – tillåta dubblettbladnamn, skapa detaljblad, spara arbetsbok C#.  

## Förutsättningar

Innan vi dyker ner, se till att du har:

- .NET 6.0 SDK (eller någon nyare .NET‑version).  
- Visual Studio 2022 eller VS Code med C#‑tillägget.  
- En aktiv licens eller en gratis provversion av **Aspose.Cells for .NET** (NuGet‑paketet heter `Aspose.Cells`).  
- En mall‑Excel‑fil (`template.xlsx`) som redan innehåller SmartMarker‑taggar som `&=Name` och en platshållartabell för detaljer.

Om något av detta känns främmande, panik inte – att installera NuGet‑paketet är ett enda kommando, och mallen kan vara en enkel arbetsbok med några platshållarceller.

## Översikt av lösningen

På en hög nivå kommer vi att:

1. Definiera en JSON‑sträng som speglar den data vi vill ha i bladet.  
2. Ställa in `SmartMarkerOptions` så att dubblettbladnamn tillåts och ett **detaljblad** får ett förutsägbart namn.  
3. Ladda Excel‑mallen som innehåller SmartMarker‑taggarna.  
4. Köra SmartMarker‑processorn för att slå ihop JSON‑datan med arbetsboken.  
5. Spara den färdiga filen med `workbook.Save(...)`.

Varje steg förklaras nedan, med kompletta kodsnuttar och varför steget är viktigt.

---

## Steg 1 – Förbered JSON‑payloaden du ska slå ihop

Det första du behöver är ett JSON‑dokument som matchar SmartMarker‑taggarna i din mall. Tänk på JSON som sanningskällan; varje nyckel blir en platshållare i Excel‑filen.

```csharp
// Step 1: Define the JSON data that will be merged into the worksheet
string jsonData = @"{
    ""Name"": ""John"",
    ""Date"": ""2023-01-01"",
    ""Orders"": [
        { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
        { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
    ]
}";
```

**Varför detta är viktigt:**  
SmartMarker läser JSON‑hierarkin och expanderar automatiskt tabeller för samlingar som `Orders`. Om din JSON‑struktur inte stämmer överens med taggarna kommer sammanslagningen tyst att producera tomma rader – ett vanligt fallgropp.

---

## Steg 2 – Konfigurera SmartMarker för att tillåta dubblettbladnamn och namnge detaljbladet

Som standard förbjuder Aspose.Cells dubblettbladnamn, vilket kan bli ett hinder när du genererar ett detaljblad för varje huvudpost. Klassen `SmartMarkerOptions` låter dig släppa den regeln och även ange ett namnmönster för nysskapade detaljblad.

```csharp
// Step 2: Create SmartMarker options and allow duplicate base names for detail sheets
var smartMarkerOptions = new Aspose.Cells.SmartMarker.SmartMarkerOptions
{
    // When a detail sheet is generated, it will be named "Detail", "Detail (2)", etc.
    DetailSheetNewName = "Detail",

    // This flag tells the engine that duplicate sheet names are acceptable.
    // Useful when you generate multiple detail sheets from a loop.
    AllowDuplicateSheetNames = true
};
```

**Varför detta är viktigt:**  
Om du loopar över flera kunder och varje iteration skapar ett nytt blad, skulle motorn normalt kasta ett undantag. Genom att sätta `AllowDuplicateSheetNames` till `true` instruerar du Aspose.Cells att automatiskt lägga till ett numeriskt suffix, så processen flyter på.

---

## Steg 3 – Ladda Excel‑mallen som innehåller SmartMarker‑taggar

Din mall är duken där SmartMarker målar datan. Den kan innehålla vilken formatering som helst – färger, formler, diagram – så du slipper återskapa den logiken programatiskt.

```csharp
// Step 3: Load the workbook that contains SmartMarker tags
using var workbook = new Aspose.Cells.Workbook(@"C:\MyProjects\ExcelDemo\template.xlsx");
```

**Tips:**  
Placera mallen i en mapp som är en del av projektets output (t.ex. `Content\Templates`). På så sätt kan du referera till den med en relativ sökväg och undvika hårdkodade absoluta kataloger.

---

## Steg 4 – Kör SmartMarker‑processorn med JSON‑data och alternativ

Nu händer magin. `SmartMarkerProcessor` läser JSON‑en, respekterar de alternativ du ställt in och fyller i arbetsboken därefter.

```csharp
// Step 4: Process the SmartMarker tags using the JSON data and the configured options
workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);
```

**Vad händer under huven?**  
- Processorn skannar varje cell efter markörer som `&=Name` eller `&=Orders.Item`.  
- Den ersätter enkla markörer med skalära värden (`Name`, `Date`).  
- För samlingar (`Orders`) skapas ett nytt detaljblad (namngivet “Detail”) och en tabellrad fylls i för varje objekt.  
- Eftersom vi tillät dubblettbladnamn, om mallen redan hade ett blad som heter “Detail”, skapar motorn “Detail (2)”.

---

## Steg 5 – Spara den sammanslagna arbetsboken till disk

Till sist skriver du den fyllda arbetsboken till en fil. Du kan välja vilket format som helst som stöds av Aspose.Cells – XLSX, CSV, PDF, osv. Här håller vi oss till det moderna XLSX‑formatet.

```csharp
// Step 5: Save the workbook with the merged data
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

**Varför detta är viktigt:**  
Sparandet är där du faktiskt **sparar arbetsbok C#‑stil**. Om du behöver streama filen tillbaka till en webbklient kan du använda `workbook.Save(Stream, SaveFormat.Xlsx)` istället.

---

## Fullständigt fungerande exempel

Sätter vi ihop allt får vi en komplett, körklar konsolapp. Se till att du har installerat `Aspose.Cells`‑NuGet‑paketet (`dotnet add package Aspose.Cells`) innan du kompilerar.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace ExcelFromJsonDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Define the JSON payload
            string jsonData = @"{
                ""Name"": ""John"",
                ""Date"": ""2023-01-01"",
                ""Orders"": [
                    { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
                    { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
                ]
            }";

            // 2️⃣ Configure SmartMarker options – allow duplicate sheet names & set detail sheet name
            var smartMarkerOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail",
                AllowDuplicateSheetNames = true
            };

            // 3️⃣ Load the template workbook (ensure the path is correct)
            var workbookPath = @"C:\MyProjects\ExcelDemo\template.xlsx";
            using var workbook = new Workbook(workbookPath);

            // 4️⃣ Merge JSON data into the workbook
            workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);

            // 5️⃣ Save the result
            var outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Excel file generated successfully at: {outputPath}");
        }
    }
}
```

### Förväntat resultat

- **Sheet 1** (huvudbladet) visar “John” i `Name`‑cellen och “2023‑01‑01” i `Date`‑cellen.  
- Ett nytt **Detail**‑blad visas, med en tabell som innehåller två rader: en för Laptop‑beställningen och en för Mus‑beställningen.  
- Om mallen redan hade ett blad med namnet “Detail”, blir det nya bladet “Detail (2)”, tack vare flaggan `AllowDuplicateSheetNames`.

![Excel‑utdata som visar huvudblad med namn och datum, samt ett Detail‑blad med orderrader](excel-output.png "generera excel från json‑resultat")

*Bildtext:* **generera excel från json – exempelarbetsbok med huvud‑ och detaljblad**

---

## Vanliga frågor & kantfall

### Vad händer om min JSON innehåller nästlade samlingar?

SmartMarker kan hantera nästlade arrayer, men du måste lägga till ytterligare detaljblad eller använda hierarkiska markörer. Till exempel, `&=Orders.SubItems.Product` skulle automatiskt generera ett tredje‑nivåblad.

### Hur anpassar jag namnmönstret för dubblettblad?

Istället för ett statiskt `DetailSheetNewName` kan du tilldela en callback via `smartMarkerOptions.DetailSheetNameGenerator`. Detta låter dig bädda in tidsstämplar eller unika ID:n i bladnamnet.

```csharp
smartMarkerOptions.DetailSheetNameGenerator = (baseName, index) =>
    $"{baseName}_{DateTime.Now:yyyyMMdd}_{index}";
```

### Kan jag generera CSV istället för XLSX?

Absolut. Byt ut den sista `Save`‑anropet mot:

```csharp
workbook.Save(outputPath, SaveFormat.Csv);
```

Resten av pipeline‑flödet förblir oförändrat.

### Fungerar detta i ASP.NET Core?

Ja. Samma kod kan köras i en controller‑action. Streama bara arbetsboken till svaret:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
ms.Position = 0;
return File(ms, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "report.xlsx");
```

---

## Pro‑tips & fallgropar

- **Pro‑tips:** Håll dina SmartMarker‑taggar i ett separat “Template”‑blad. På så sätt kan du skydda bladet mot oavsiktliga redigeringar samtidigt som processorn kan läsa det.  
- **Se upp för:** JSON‑nycklar som innehåller mellanslag eller specialtecken. Aspose.Cells förväntar sig giltiga JavaScript‑identifierare; byt namn på dem eller använd `JsonProperty`‑attributet om du deserialiserar från en POCO.  
- **Prestanda‑tips:** Om du bearbetar tusentals rader, sätt `smartMarkerOptions.EnableCache = true` för att återanvända kompilerade markörer.  
- **Versionskontroll:** Koden ovan riktar sig mot Aspose.Cells 23.9+. Äldre versioner kanske inte stödjer `AllowDuplicateSheetNames`.

---

## Slutsats

Du har nu ett komplett, end‑to‑end‑recept för att **generera Excel från JSON** i C#. Genom att konfigurera `SmartMarkerOptions` har vi visat hur du **tillåter dubblettbladnamn**, styr **detaljbladets** namn och slutligen **sparar arbetsbok C#‑stil**. Tillvägagångssättet är helt självständigt – inga externa tjänster, bara ett enda NuGet‑paket.

Nästa steg? Prova att byta ut JSON‑källan mot ett riktigt API

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}