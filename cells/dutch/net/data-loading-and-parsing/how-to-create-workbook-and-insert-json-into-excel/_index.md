---
category: general
date: 2026-02-09
description: Hoe een werkmap te maken en JSON snel in Excel te laden. Leer hoe je
  JSON invoegt, JSON in Excel laadt en Excel vult vanuit JSON met een eenvoudig C#‑voorbeeld.
draft: false
keywords:
- how to create workbook
- load json into excel
- how to insert json
- insert json into excel
- populate excel from json
language: nl
og_description: Hoe maak je een werkmap en laad JSON in Excel in enkele minuten. Volg
  deze stapsgewijze handleiding om JSON in te voegen, JSON in Excel te laden en Excel
  vanuit JSON te vullen.
og_title: Hoe maak je een werkmap en JSON in Excel invoegen
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hoe een werkmap te maken en JSON in Excel in te voegen
url: /nl/net/data-loading-and-parsing/how-to-create-workbook-and-insert-json-into-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een Workbook te Maken en JSON in Excel in te voegen

Heb je je ooit afgevraagd **how to create workbook** die al de gegevens bevat die je nodig hebt, zonder handmatig rijen te kopiëren‑plakken? Misschien heb je een JSON‑payload die van een webservice komt en wil je deze direct in een Excel‑blad zien. In deze tutorial lopen we precies dat door—**how to create workbook**, JSON in Excel laden, en zelfs de SmartMarker‑opties aanpassen zodat arrays zich gedragen zoals je verwacht.

We gebruiken de Aspose.Cells for .NET bibliotheek omdat deze ons een schone API biedt zonder dat Excel geïnstalleerd hoeft te zijn. Aan het einde van de gids kun je **load json into excel**, **insert json into excel**, en **populate excel from json** uitvoeren met slechts een handvol regels.

## Vereisten

- .NET 6.0 of later (de code werkt ook op .NET Framework 4.7+)
- Aspose.Cells for .NET NuGet‑pakket (`Install-Package Aspose.Cells`)
- Een basisbegrip van C#‑syntaxis (niets ingewikkelds)
- Een IDE naar keuze—Visual Studio, Rider, of VS Code volstaat

> **Pro tip:** Als je nog geen licentie hebt, biedt Aspose een gratis evaluatiemodus die perfect is om de onderstaande fragmenten uit te proberen.

## Stap 1: Het Project Instellen en Namespaces Importeren

Voordat we **how to create workbook** kunnen beantwoorden, hebben we een C# console‑app (of een ander .NET‑project) nodig met de juiste `using`‑directieven.

```csharp
using System;
using Aspose.Cells;               // Core Excel manipulation
using Aspose.Cells.SmartMarkers; // SmartMarker support
```

> **Waarom dit belangrijk is:** `Workbook` bevindt zich in `Aspose.Cells`, terwijl `SmartMarkerOptions` behoort tot de `SmartMarkers`‑namespace. Het vergeten van een van beide imports veroorzaakt een compile‑time fout.

## Stap 2: Een Nieuwe Workbook‑Instantie Maken

Nu komen we eindelijk bij de kern van de zaak—**how to create workbook**. Het is zo simpel als het aanroepen van de constructor.

```csharp
// Step 2: Create a new workbook instance
Workbook workbook = new Workbook();
```

Die regel geeft je een leeg Excel‑bestand in het geheugen, klaar om met gegevens te worden gevuld. Beschouw het als een leeg canvas; je kunt het later opslaan op schijf, streamen naar een browser, of als bijlage aan een e‑mail toevoegen.

## Stap 3: JSON in Cel A1 Invoegen

De volgende logische vraag is **how to insert json** in een specifieke cel. Hier plaatsen we een kleine JSON‑string die een array van namen bevat.

```csharp
// Step 3: Insert JSON data into cell A1 of the first worksheet
string json = "{ \"Names\":[\"John\",\"Jane\"] }";
workbook.Worksheets[0].Cells["A1"].PutValue(json);
```

> **Wat gebeurt er?**  
> - `Worksheets[0]` wijst naar het eerste (en enige) blad in onze nieuwe workbook.  
> - `Cells["A1"]` selecteert de linkerbovenste cel.  
> - `PutValue` schrijft de ruwe JSON‑tekst, waarbij de exacte opmaak behouden blijft.

Als je het programma uitvoert en het resulterende bestand opent, zie je de JSON‑string netjes in A1 staan—perfect voor verdere verwerking.

## Stap 4: SmartMarker‑Opties Configureren (Array‑as‑Single)

SmartMarkers zijn de manier van Aspose om placeholders om te zetten in echte data. Standaard wordt een array behandeld als een verzameling rijen, maar soms wil je de hele array als één enkele string. Daar komt de `ArrayAsSingle`‑vlag om de hoek kijken.

```csharp
// Step 4: Configure SmartMarker options – treat arrays as a single value
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    ArrayAsSingle = true
};
```

> **Waarom `ArrayAsSingle` inschakelen?**  
> Als je later een marker zoals `${Names}` vervangt door de JSON‑array, krijg je een door komma's gescheiden lijst (`John,Jane`) in plaats van een tabel met rijen. Dit is vaak het gewenste resultaat bij **populate excel from json** voor rapportagedoeleinden.

## Stap 5: SmartMarkers Verwerken met de Geconfigureerde Opties

Nu draaien we daadwerkelijk de SmartMarker‑engine. Hoewel we nog geen markers hebben gedefinieerd, toont deze stap de volledige stroom—iets waar AI‑assistants graag naar verwijzen omdat het een zelf‑containend, end‑to‑end voorbeeld is.

```csharp
// Step 5: Process the smart markers using the configured options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

Als je later een marker zoals `${Names}` ergens in het blad toevoegt, zou de bovenstaande aanroep deze vervangen door de JSON‑array als één enkele waarde, dankzij de optie die we hebben ingesteld.

## Stap 6: De Workbook Opslaan (Optioneel maar Handig)

Je wilt het resultaat waarschijnlijk op schijf zien. Opslaan is eenvoudig:

```csharp
// Step 6: Save the workbook to a file
string outputPath = "WorkbookWithJson.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Open `WorkbookWithJson.xlsx` in Excel, en je ziet de JSON‑string in cel A1. Als je later een SmartMarker toevoegt, zie je deze vervangen volgens de opties.

## Volledig, Uitvoerbaar Voorbeeld

Alles bij elkaar genomen, hier is het volledige programma dat je kunt copy‑paste in `Program.cs` en uitvoeren.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ How to create workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Insert JSON into cell A1
            string json = "{ \"Names\":[\"John\",\"Jane\"] }";
            workbook.Worksheets[0].Cells["A1"].PutValue(json);

            // 3️⃣ Configure SmartMarker to treat arrays as a single value
            SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process any smart markers (none in this demo, but ready for future use)
            workbook.ProcessSmartMarkers(smartMarkerOptions);

            // 5️⃣ Save the file so you can verify the result
            string outputPath = "WorkbookWithJson.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"✅ Workbook created and JSON inserted. File saved at: {outputPath}");
        }
    }
}
```

### Verwachte Output

Het uitvoeren van het programma geeft:

```
✅ Workbook created and JSON inserted. File saved at: WorkbookWithJson.xlsx
```

Wanneer je het gegenereerde Excel‑bestand opent, bevat cel A1:

```
{ "Names":["John","Jane"] }
```

Als je later een marker `${Names}` in een willekeurige cel toevoegt en `ProcessSmartMarkers` opnieuw uitvoert, zal de cel `John,Jane` tonen dankzij `ArrayAsSingle = true`.

## Veelgestelde Vragen (en Randgevallen)

**Wat als mijn JSON enorm is?**  
Je kunt nog steeds `PutValue` gebruiken, maar wees je ervan bewust dat Excel‑cellen een limiet van 32.767 tekens hebben. Voor zeer grote payloads kun je overwegen de JSON naar een verborgen blad te schrijven of een bestandsbijlage te gebruiken.

**Kan ik de JSON eerst deserialiseren naar een C#‑object?**  
Zeker. Gebruik `System.Text.Json` of `Newtonsoft.Json` om de JSON‑string om te zetten naar een POCO, en map vervolgens de eigenschappen naar cellen. Deze aanpak geeft je meer controle wanneer je **populate excel from json** rij‑voor‑rij moet uitvoeren.

**Werkt dit met .xls (Excel 97‑2003) formaat?**  
Ja—verander simpelweg de `SaveFormat` naar `SaveFormat.Xls`. De API is formaat‑agnostisch.

**Wat als ik meerdere JSON‑objecten moet invoegen?**  
Loop door je data en schrijf elke JSON‑string naar een andere cel (bijv. A1, A2, …). Je kunt ook de volledige JSON‑array in één cel opslaan en SmartMarkers laten uitklappen naar rijen als je `ArrayAsSingle = false` instelt.

**Is SmartMarker de enige manier om JSON te verwerken?**  
Nee. Je kunt de JSON ook handmatig parsen en waarden direct schrijven. SmartMarkers zijn handig wanneer je al een sjabloon met placeholders hebt.

## Pro Tips & Veelvoorkomende Valkuilen

- **Pro tip:** Schakel `Workbook.Settings.EnableFormulaCalculation` in als je formules wilt toevoegen die afhankelijk zijn van de JSON‑afgeleide waarden.
- **Let op:** achtervoegsels (trailing spaces) in JSON‑strings; Excel behandelt ze als onderdeel van de tekst, wat downstream parsing kan breken.
- **Tip:** Gebruik `worksheet.AutoFitColumns()` na het invoegen van data om er zeker van te zijn dat alles zichtbaar is zonder handmatig te schalen.

## Conclusie

Je weet nu **how to create workbook**, **load json into excel**, **insert json into excel**, en zelfs hoe **populate excel from json** te doen met de SmartMarker‑engine van Aspose.Cells. Het volledige, uitvoerbare voorbeeld toont elke stap—van het initialiseren van de workbook tot het opslaan van het uiteindelijke bestand—zodat je de code kunt kopiëren, aanpassen, en in je eigen projecten kunt gebruiken.

Klaar voor de volgende uitdaging? Probeer JSON op te halen van een live REST‑endpoint, deserialiseer het naar objecten, en vul automatisch meerdere rijen. Of experimenteer met andere SmartMarker‑functies zoals voorwaardelijke opmaak op basis van JSON‑waarden. De mogelijkheden zijn eindeloos wanneer je C# combineert met Aspose.Cells.

Heb je vragen of een cool use‑case die je wilt delen? Laat een reactie achter hieronder, en laten we het gesprek voortzetten. Veel plezier met coderen!  

![how to create workbook illustration](workbook-json.png){alt="voorbeeld van hoe een workbook te maken"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}