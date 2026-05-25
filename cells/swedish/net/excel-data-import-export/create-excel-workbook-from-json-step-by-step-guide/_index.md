---
category: general
date: 2026-03-25
description: Skapa en Excel-arbetsbok från JSON och spara arbetsboken som xlsx. Lär
  dig hur du exporterar JSON till xlsx, genererar Excel från JSON och fyller i Excel
  från JSON på några minuter.
draft: false
keywords:
- create excel workbook
- export json to xlsx
- generate excel from json
- populate excel from json
- save workbook as xlsx
language: sv
og_description: Skapa Excel-arbetsbok från JSON omedelbart. Denna guide visar hur
  du exporterar JSON till XLSX, genererar Excel från JSON och fyller i Excel från
  JSON med Aspose.Cells.
og_title: Skapa Excel-arbetsbok från JSON – Komplett C#-handledning
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Skapa Excel-arbetsbok från JSON – Steg‑för‑steg‑guide
url: /sv/net/excel-data-import-export/create-excel-workbook-from-json-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel-arbetsbok från JSON – Komplett C#-handledning

Har du någonsin behövt **create excel workbook** från en JSON‑payload men varit osäker på var du ska börja? Du är inte ensam; många utvecklare stöter på samma problem när de försöker omvandla API‑data till ett snyggt kalkylblad. Den goda nyheten? Med några rader C# och Aspose.Cells kan du **export json to xlsx**, **generate excel from json**, och **populate excel from json** utan att jonglera med tredjeparts‑konverterare.

I den här guiden går vi igenom hela processen – från en rå JSON‑sträng, till att släppa den i en SmartMarker, och slutligen **save workbook as xlsx** på disk. När du är klar har du en färdig‑att‑använda Excel‑fil som ser ut så här:

| Name | Score |
|------|-------|
| John | 90    |
| Anna | 85    |

> **Pro tip:** Om du redan använder Aspose.Cells någon annanstans i ditt projekt kan du återanvända samma `Workbook`‑instans för flera JSON‑importer – perfekt för batch‑bearbetning.

## Vad du behöver

- **.NET 6+** (eller någon recent .NET Framework som stödjer C# 10)
- **Aspose.Cells for .NET** – installera via NuGet: `dotnet add package Aspose.Cells`
- En grundläggande förståelse för C#‑syntax (ingen djup Excel‑kunskap krävs)

Det är allt. Inga externa tjänster, ingen COM‑interop, bara ren hanterad kod.

## Steg 1: Initiera en ny Excel‑arbetsbok

Det första vi gör är att skapa ett nytt workbook‑objekt. Tänk på det som att öppna en tom Excel‑fil där vi senare kommer att släppa våra data.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and grab the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

Varför börja med en ny arbetsbok? Det garanterar en ren start, förhindrar kvarvarande stilar från tidigare körningar och håller filstorleken minimal – perfekt för automatiserade pipelines.

## Steg 2: Förbered JSON‑data som du vill importera

För demonstration använder vi en liten JSON‑array, men du kan byta ut den mot vilken giltig JSON du får från en webbtjänst, en fil eller en databasfråga som helst.

```csharp
// Step 2: JSON string representing a simple collection of records
string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";
```

Observera de dubbelt escapade citationstecknen (`\"`) – det är bara C#‑strängliteral‑syntax. I ett verkligt scenario skulle du troligen läsa detta från en fil:

```csharp
// string jsonData = File.ReadAllText("data.json");
```

## Steg 3: Berätta för SmartMarker att behandla hela arrayen som ett enda rekord

Aspose.Cells SmartMarker‑motor kan iterera över samlingar automatiskt. Genom att aktivera **ArrayAsSingle** behandlar vi hela JSON‑arrayen som ett enda rekord, vilket är exakt vad vi behöver för en platt tabell.

```csharp
// Step 3: Configure SmartMarker options – array‑as‑single mode
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // This makes the whole JSON array behave like one record
};
```

Om du glömmer den här flaggan kommer SmartMarker att försöka skapa ett separat blad för varje element – definitivt inte vad du vill när du genererar en enkel tabell.

## Steg 4: Placera en SmartMarker‑token i kalkylbladet

SmartMarker‑tokens ser ut som `${jsonArray}`. När processorn körs ersätter den tokenen med data från JSON‑källan. Vi placerar tokenen i cell **A1** så att utskriften börjar i det övre vänstra hörnet.

```csharp
// Step 4: Insert the SmartMarker token into cell A1
worksheet.Cells["A1"].PutValue("${jsonArray}");
```

Du kan också förformatera rubrikraden innan bearbetning. Till exempel, sätt fet stil på den första raden:

```csharp
Cell headerCell = worksheet.Cells["A1"];
headerCell.Style.Font.IsBold = true;
```

## Steg 5: Kör SmartMarker‑processorn

Nu händer magin. Processorn läser JSON‑data, mappar varje egenskap till en kolumn och skriver raderna under tokenen.

```csharp
// Step 5: Process the SmartMarker with our JSON data and options
worksheet.SmartMarkerProcessor.Process(jsonData, options);
```

Bakom kulisserna gör Aspose.Cells:

1. Analyserar JSON‑en till ett .NET‑objekt.
2. Matchar egenskapsnamn (`Name`, `Score`) till kolumnrubriker.
3. Skriver varje array‑element som en ny rad.

Om din JSON innehåller nästlade objekt kan du referera till dem med punktnotation (`${parent.child}`) – en praktisk funktion för mer komplexa rapporter.

## Steg 6: Spara arbetsboken som en XLSX‑fil

Till sist sparar du arbetsboken till disk. Filändelsen `.xlsx` talar om för Excel (och de flesta andra kalkylprogram) att detta är en OpenXML‑arbetsbok.

```csharp
// Step 6: Save the workbook to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Du kan naturligtvis streama arbetsboken direkt till ett HTTP‑svar om du bygger ett webb‑API:

```csharp
// Example for ASP.NET Core
using (var stream = new MemoryStream())
{
    workbook.Save(stream, SaveFormat.Xlsx);
    stream.Position = 0;
    return File(stream, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "data.xlsx");
}
```

## Fullt fungerande exempel

Nedan är det kompletta, färdiga programmet som inkluderar alla steg ovan. Kopiera och klistra in det i ett nytt konsolprojekt och tryck **F5**.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ JSON data to be merged into the sheet
        string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";

        // 3️⃣ Enable array‑as‑single mode so the whole array is one record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Put a SmartMarker token in A1 that points to the JSON array
        worksheet.Cells["A1"].PutValue("${jsonArray}");

        // Optional: make the header bold for better readability
        worksheet.Cells["A1"].Style.Font.IsBold = true;

        // 5️⃣ Process the SmartMarker with the JSON payload
        worksheet.SmartMarkerProcessor.Process(jsonData, options);

        // 6️⃣ Save the result as an XLSX file
        string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"✅ Workbook created and saved to: {outputPath}");
    }
}
```

**Förväntat resultat:** När du öppnar `json-single.xlsx` visas två rader under den feta rubriken – `John` med poängen `90` och `Anna` med `85`. Kolumnnamnen härleds automatiskt från JSON‑egenskapsnamnen.

## Vanliga frågor & kantfall

### Vad händer om mina JSON‑nycklar innehåller mellanslag eller specialtecken?

SmartMarker förväntar sig giltiga identifierarnamn. Ersätt mellanslag med understreck eller använd en anpassad mappning:

```csharp
// Example JSON: {"First Name":"John"}
string jsonData = "[{\"First_Name\":\"John\",\"Score\":90}]";
// Token stays the same – Aspose.Cells will map "First_Name" to column header "First_Name"
```

### Hur exporterar jag en stor JSON‑array (tusentals rader)?

Processorn strömmar data internt, så minnesanvändningen förblir måttlig. Du kan dock vilja:

- Öka kalkylbladets `MaxRows`‑gräns (`worksheet.Cells.MaxRow = 1_048_576;` – Excels maximum).
- Stäng av rutnät för prestanda (`worksheet.IsGridlinesVisible = false;`).

### Kan jag lägga till flera JSON‑tabeller i samma arbetsbok?

Självklart. Placera bara olika SmartMarker‑tokens i separata områden (t.ex. `${orders}` i `A10`, `${customers}` i `D1`) och anropa `Process` en gång per token eller en gång med ett sammansatt JSON‑objekt som innehåller båda arrayerna.

## Bonus: Lägg till ett enkelt diagram (valfritt)

Om du vill visualisera poängen, lägg till ett snabbt stapeldiagram efter att datan har fyllts i:

```csharp
// Insert a column chart starting at cell E1
int chartIndex = worksheet.Charts.Add(ChartType.Column, 0, 4, 15, 10);
Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("B2:B3", true);
chart.NSeries[0].Name = "Score";
chart.Title.Text = "Scores by Name";
```

## Slutsats

Du vet nu **how to create excel workbook** från en JSON‑sträng, **export json to xlsx**, **generate excel from json**, och **populate excel from json** med Aspose.Cells SmartMarker‑funktion. Den kompletta lösningen – initiering av en arbetsbok, konfiguration av SmartMarker, bearbetning av JSON och sparande av filen – ryms i ett fåtal rader, men skalar till enorma datamängder.

Nästa steg? Prova att byta ut den statiska JSON‑en mot ett API‑anrop, lägg till villkorlig formatering baserat på poäng, eller generera flera blad för olika datadomäner. Samma mönster fungerar för CSV, XML eller till och med databassresultat – byt bara källsträngen och justera SmartMarker‑tokenen.

Lycka till med kodningen, och må dina kalkylblad alltid vara prydliga!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}