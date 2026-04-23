---
category: general
date: 2026-03-18
description: Leer hoe je Excel genereert vanuit JSON met C#, dubbele werkbladnamen
  toestaat, een detailblad maakt en een werkmap opslaat met C# in enkele minuten.
draft: false
keywords:
- generate excel from json
- allow duplicate sheet names
- how to create detail sheet
- save workbook c#
- smartmarker options
- aspnet cells integration
language: nl
og_description: Genereer Excel vanuit JSON met C#. Deze gids laat zien hoe je dubbele
  bladnamen toestaat, een detailblad maakt en een werkmap opslaat in C# met Aspose.Cells.
og_title: Genereer Excel vanuit JSON in C# – Complete tutorial
tags:
- C#
- Excel automation
- JSON
- Aspose.Cells
title: Genereer Excel vanuit JSON in C# – Stapsgewijze handleiding
url: /nl/net/excel-data-import-export/generate-excel-from-json-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel genereren vanuit JSON in C# – Stapsgewijze handleiding

Heb je ooit **Excel genereren vanuit JSON** moeten doen, maar wist je niet welke bibliotheek het zware werk kon doen? Je bent niet de enige. In veel enterprise‑applicaties ontvangen we payloads als JSON en moeten we die gegevens in mooi opgemaakte spreadsheets stoppen — denk aan verkooprapporten, voorraaddump's of audit‑logboeken. Het goede nieuws? Met de SmartMarker‑engine van Aspose.Cells kun je een JSON‑string omzetten in een volledig Excel‑bestand in slechts een handvol regels.

In deze tutorial lopen we het volledige proces door: van het voorbereiden van de JSON‑payload, het configureren van SmartMarker om **duplicate sheet names toe te staan**, het maken van een **detail sheet**, en uiteindelijk **het opslaan van de workbook C#** stijl. Aan het einde heb je een herbruikbare code‑fragment die je in elk .NET‑project kunt gebruiken.

> **Snelle samenvatting:**  
> • Primair doel – Excel genereren vanuit JSON.  
> • Secundaire doelen – duplicate sheet names toestaan, detail sheet maken, workbook C# opslaan.  

## Prerequisites

- .NET 6.0 SDK (of een recente .NET‑versie).  
- Visual Studio 2022 of VS Code met de C#‑extensie.  
- Een actieve licentie of een gratis proefversie van **Aspose.Cells for .NET** (het NuGet‑pakket is `Aspose.Cells`).  
- Een sjabloon‑Excel‑bestand (`template.xlsx`) dat al SmartMarker‑tags bevat zoals `&=Name` en een placeholder voor een detailtabel.  

Als een van deze je onbekend voorkomt, geen paniek—het installeren van het NuGet‑pakket is één commando, en het sjabloon kan een simpel werkboek zijn met een paar placeholder‑cellen.

## Overview of the Solution

Op een hoog niveau zullen we:

1. Definieer een JSON‑string die de gegevens weerspiegelt die we in het blad willen hebben.  
2. Stel `SmartMarkerOptions` in zodat duplicate sheet names zijn toegestaan en een **detail sheet** een voorspelbare naam krijgt.  
3. Laad het Excel‑sjabloon dat de SmartMarker‑tags bevat.  
4. Voer de SmartMarker‑processor uit om de JSON‑gegevens te combineren met het werkboek.  
5. Sla het uiteindelijke bestand op met `workbook.Save(...)`.  

Elke stap wordt hieronder uitgelegd, met volledige code‑fragmenten en waarom de stap belangrijk is.

---

## Stap 1 – Bereid de JSON‑payload voor die je gaat samenvoegen

Het eerste wat je nodig hebt is een JSON‑document dat overeenkomt met de SmartMarker‑tags in je sjabloon. Beschouw de JSON als de bron van waarheid; elke sleutel wordt een placeholder in het Excel‑bestand.

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

**Waarom dit belangrijk is:**  
SmartMarker leest de JSON‑hiërarchie en breidt automatisch tabellen uit voor collecties zoals `Orders`. Als je JSON‑structuur niet overeenkomt met de tags, zal de samenvoeging stilletjes lege rijen opleveren — een veelvoorkomende valkuil.

---

## Stap 2 – Configureer SmartMarker om duplicate sheet names toe te staan en benoem de detail sheet

Standaard verbiedt Aspose.Cells duplicate sheet names, wat een belemmering kan zijn wanneer je een detail sheet genereert voor elk master‑record. De `SmartMarkerOptions`‑klasse laat je die regel versoepelen en tevens een naamgevingspatroon opgeven voor nieuw aangemaakte detail sheets.

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

**Waarom dit belangrijk is:**  
Als je over meerdere klanten iterereert en elke iteratie een nieuw blad maakt, zou de engine normaal een uitzondering werpen. Door `AllowDuplicateSheetNames` op `true` te zetten, vertelt je Aspose.Cells om automatisch een numeriek achtervoegsel toe te voegen, waardoor het proces soepel verloopt.

---

## Stap 3 – Laad het Excel‑sjabloon dat SmartMarker‑tags bevat

Je sjabloon is het canvas waarop SmartMarker de gegevens zal schilderen. Het kan elke opmaak bevatten — kleuren, formules, grafieken — zodat je die logica niet programmatically hoeft te recreëren.

```csharp
// Step 3: Load the workbook that contains SmartMarker tags
using var workbook = new Aspose.Cells.Workbook(@"C:\MyProjects\ExcelDemo\template.xlsx");
```

**Tip:**  
Bewaar het sjabloon in een map die deel uitmaakt van de output van je project (bijv. `Content\Templates`). Op die manier kun je er met een relatief pad naar verwijzen en vermijd je het hard‑coderen van absolute directories.

---

## Stap 4 – Voer de SmartMarker‑processor uit met de JSON en opties

Nu gebeurt de magie. De `SmartMarkerProcessor` leest de JSON, respecteert de ingestelde opties, en vult het werkboek dienovereenkomstig.

```csharp
// Step 4: Process the SmartMarker tags using the JSON data and the configured options
workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);
```

**Wat gebeurt er onder de motorkap?**  
- De processor scant elke cel op markers zoals `&=Name` of `&=Orders.Item`.  
- Hij vervangt eenvoudige markers door scalare waarden (`Name`, `Date`).  
- Voor collecties (`Orders`) maakt hij een nieuw detail sheet (genaamd “Detail”) en vult een tabelrij voor elk item.  
- Omdat we duplicate sheet names hebben toegestaan, zal de engine, als het sjabloon al een blad genaamd “Detail” had, “Detail (2)” aanmaken.

---

## Stap 5 – Sla het samengevoegde werkboek op naar schijf

Tot slot schrijf je het gevulde werkboek naar een bestand. Je kunt elk formaat kiezen dat door Aspose.Cells wordt ondersteund — XLSX, CSV, PDF, enz. Hier blijven we bij het moderne XLSX.

```csharp
// Step 5: Save the workbook with the merged data
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

**Waarom dit belangrijk is:**  
Opslaan is het moment waarop je daadwerkelijk **workbook C#** opslaat. Als je het bestand terug naar een webclient moet streamen, kun je in plaats daarvan `workbook.Save(Stream, SaveFormat.Xlsx)` gebruiken.

---

## Volledig werkend voorbeeld

Alles bij elkaar, hier is een volledige, kant‑klaar console‑applicatie. Zorg ervoor dat je het `Aspose.Cells` NuGet‑pakket (`dotnet add package Aspose.Cells`) hebt geïnstalleerd voordat je compileert.

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

### Verwacht resultaat

- **Sheet 1** (het master‑blad) toont “John” in de `Name`‑cel en “2023‑01‑01” in de `Date`‑cel.  
- Er verschijnt een nieuw **Detail**‑blad, met een tabel van twee rijen: één voor de Laptop‑order en één voor de Mouse‑order.  
- Als het sjabloon al een blad met de naam “Detail” had, zal het nieuwe blad “Detail (2)” heten, dankzij de `AllowDuplicateSheetNames`‑vlag.

![Excel‑output die het master‑blad toont met naam en datum, plus een Detail‑blad met orderrijen](excel-output.png "excel genereren vanuit json resultaat")

*Afbeeldings‑alt‑tekst:* **excel genereren vanuit json – voorbeeldwerkboek met master‑ en detail‑bladen**

---

## Veelgestelde vragen & randgevallen

### Wat als mijn JSON geneste collecties bevat?

SmartMarker kan geneste arrays aan, maar je moet extra detail sheets toevoegen of hiërarchische markers gebruiken. Bijvoorbeeld, `&=Orders.SubItems.Product` zou automatisch een blad van het derde niveau genereren.

### Hoe pas ik het naamgevingspatroon voor duplicate sheets aan?

In plaats van een statische `DetailSheetNewName` kun je een callback toewijzen via `smartMarkerOptions.DetailSheetNameGenerator`. Hiermee kun je tijdstempels of unieke ID's in de bladnaam opnemen.

```csharp
smartMarkerOptions.DetailSheetNameGenerator = (baseName, index) =>
    $"{baseName}_{DateTime.Now:yyyyMMdd}_{index}";
```

### Kan ik CSV genereren in plaats van XLSX?

Zeker. Vervang de laatste `Save`‑aanroep door:

```csharp
workbook.Save(outputPath, SaveFormat.Csv);
```

De rest van de pijplijn blijft identiek.

### Werkt dit in ASP.NET Core?

Ja. dezelfde code kan binnen een controller‑actie worden uitgevoerd. Stream gewoon het werkboek naar de response:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
ms.Position = 0;
return File(ms, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "report.xlsx");
```

---

## Pro‑tips & valkuilen

- **Pro‑tip:** Houd je SmartMarker‑tags op een apart “Template”‑blad. Zo kun je het blad beschermen tegen accidentele bewerkingen terwijl de processor het nog steeds kan lezen.  
- **Let op:** JSON‑sleutels die spaties of speciale tekens bevatten. Aspose.Cells verwacht geldige JavaScript‑identifiers; hernoem ze of gebruik het `JsonProperty`‑attribuut als je deserialiseert vanuit een POCO.  
- **Performance‑tip:** Als je duizenden rijen verwerkt, stel `smartMarkerOptions.EnableCache = true` in om gecompileerde markers te hergebruiken.  
- **Versie‑check:** De bovenstaande code richt zich op Aspose.Cells 23.9+. Oudere versies ondersteunen mogelijk `AllowDuplicateSheetNames` niet.

---

## Conclusie

Je hebt nu een volledige, end‑to‑end‑recept om **Excel genereren vanuit JSON** in C# te doen. Door `SmartMarkerOptions` te configureren hebben we laten zien hoe je **duplicate sheet names** kunt toestaan, de naamgeving van de **detail sheet** kunt beheersen, en uiteindelijk **workbook C#** kunt opslaan. De aanpak is volledig zelf‑voorzien — geen externe services, alleen één NuGet‑pakket.

Volgende stappen? Probeer de JSON‑bron te vervangen door een echte API

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}