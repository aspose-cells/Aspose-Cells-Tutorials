---
category: general
date: 2026-02-23
description: Hoe een werkmap te maken met Aspose.Cells en markers toe te voegen met
  een JSON‑array. Leer hoe je markers toevoegt, een JSON‑array gebruikt en slimme
  markers in Aspose.Cells in enkele minuten.
draft: false
keywords:
- how to create workbook
- how to add markers
- use json array
- smart markers aspose.cells
language: nl
og_description: Hoe maak je een werkmap met Aspose.Cells, voeg je markeringen toe
  en gebruik je een JSON‑array. Deze stapsgewijze gids laat je alles zien wat je nodig
  hebt.
og_title: Hoe een werkmap te maken met slimme markers – Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Hoe een werkmap te maken met slimme markers – Aspose.Cells-gids
url: /nl/net/smart-markers-dynamic-data/how-to-create-workbook-with-smart-markers-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een Workbook te Maken met Smart Markers – Aspose.Cells Gids

Heb je je ooit afgevraagd **hoe je een workbook** automatisch kunt vullen met gegevens uit een JSON‑bron? Je bent niet de enige—ontwikkelaars vragen voortdurend hoe ze markers kunnen toevoegen die waarden uit arrays halen, vooral bij het werken met Aspose.Cells. Het goede nieuws? Het is best eenvoudig zodra je het smart‑marker‑concept begrijpt. In deze tutorial lopen we stap voor stap door het maken van een workbook, het toevoegen van markers, het gebruiken van een JSON‑array, en het configureren van smart markers in Aspose.Cells zodat je Excel‑bestanden on‑the‑fly kunt genereren.

We behandelen alles wat je moet weten: het initialiseren van de workbook, het bouwen van een `MarkerCollection`, het voeden van een JSON‑array, het schakelen van de “ArrayAsSingle”‑vlag, en uiteindelijk het toepassen van de markers. Aan het einde heb je een volledig functioneel C#‑programma dat een Excel‑bestand produceert met de waarden **A**, **B** en **C** automatisch ingevuld. Geen externe services, alleen pure Aspose.Cells‑magie.

## Prerequisites

- .NET 6.0 of later (de code werkt ook met .NET Framework 4.6+)
- Aspose.Cells for .NET NuGet‑package (`Install-Package Aspose.Cells`)
- Een basisbegrip van C#‑syntaxis (als je helemaal nieuw bent, zijn de fragmenten uitgebreid gecommentarieerd)
- Visual Studio of een IDE naar keuze

Als je dit al hebt, geweldig—laten we beginnen.

## Stap 1: Hoe een Workbook te Maken (Initialiseer het Excel‑bestand)

Het eerste wat je nodig hebt is een leeg workbook‑object. Beschouw het als een blanco canvas dat Aspose.Cells later zal vullen met data.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // reference to the default sheet
```

> **Waarom dit belangrijk is:** `Workbook` is het startpunt voor elke Excel‑bewerking. Zonder dit kun je geen smart markers toevoegen of het bestand opslaan. Het eerst aanmaken van de workbook zorgt bovendien voor een schone omgeving voor de volgende stappen.

## Stap 2: Hoe Markers Toevoegen – Initialiseert een Marker Collection

Smart markers bevinden zich binnen een `MarkerCollection`. In deze collectie definieer je placeholders (de markers) en de data die ze zullen vervangen.

```csharp
        // Step 2: Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();
```

> **Pro tip:** Je kunt dezelfde `MarkerCollection` hergebruiken voor meerdere werkbladen, maar één per blad maakt debuggen makkelijker.

## Stap 3: JSON‑Array Gebruiken – Voeg een Marker toe met JSON‑Data

Nu voegen we daadwerkelijk een marker toe. De placeholder `{SmartMarker}` wordt vervangen door de JSON‑array die we leveren. De JSON moet een stringified array zijn, bijvoorbeeld `["A","B","C"]`.

```csharp
        // Step 3: Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");
```

> **Uitleg:** De `Add`‑methode neemt twee argumenten: de marker‑tekst en de gegevensbron. Hier is de gegevensbron een JSON‑array, die Aspose.Cells automatisch kan parseren. Dit is de kern van **use json array** met smart markers.

## Stap 4: De Marker Configureren – De Array als Eén Waarde Behandelen

Standaard breidt Aspose.Cells een JSON‑array uit naar afzonderlijke rijen. Als je de hele array als één celwaarde wilt behandelen (handig voor dropdown‑lijsten of samengevoegde strings), zet je de `ArrayAsSingle`‑vlag.

```csharp
        // Step 4: Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;
```

> **Wanneer te gebruiken:** Als je de array in één cel wilt zien (bijv. `"A,B,C"`), schakel je deze vlag in. Anders schrijft Aspose.Cells elk element in een eigen rij.

## Stap 5: Markers Aan het Werkblad Koppelen en Toepassen

Tot slot bind je de marker‑collectie aan het werkblad en vertel je Aspose.Cells de placeholders te vervangen door de daadwerkelijke data.

```csharp
        // Step 5: Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Optional: write the placeholder into a cell so you can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook to disk
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

> **Resultaat:** Na het uitvoeren van het programma bevat `SmartMarkerResult.xlsx` de waarde **A** (of de hele array als `ArrayAsSingle` true is) in cel `A1`. Open het bestand om te verifiëren.

### Verwachte Output

| A |
|---|
| A |   *(als `ArrayAsSingle` false is, vult het eerste element de cel)*

Als je `ArrayAsSingle = true` zet, bevat cel `A1` de string `["A","B","C"]`.

## Stap 6: Hoe Markers Toevoegen – Geavanceerde Scenario's (Optioneel)

Je vraagt je misschien af, *wat als ik meer dan één marker nodig heb?* Het antwoord is simpel: roep gewoon opnieuw `Add` aan.

```csharp
        smartMarkerCollection.Add("{SecondMarker}", "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]");
        // You can also control each marker individually:
        smartMarkerCollection["SecondMarker"] = false; // expand into rows
```

> **Waarom dit werkt:** Elke marker werkt onafhankelijk, zodat je “array as single” en “expand into rows” binnen hetzelfde werkblad kunt mixen. Deze flexibiliteit is een kenmerk van **smart markers aspose.cells**.

## Veelvoorkomende Valkuilen & Hoe ze te Vermijden

| Probleem | Waarom Het Gebeurt | Oplossing |
|----------|--------------------|-----------|
| Marker wordt niet vervangen | Placeholder‑tekst ontbreekt of typfout | Zorg dat de cel exact de marker‑string bevat (`{SmartMarker}`) |
| JSON wordt niet geparseerd | Ongeldige JSON‑syntaxis (ontbrekende aanhalingstekens) | Gebruik een JSON‑validator of escape aanhalingstekens dubbel in C#‑strings |
| Array wordt onverwacht uitgebreid | `ArrayAsSingle` blijft op standaard `false` | Zet `["ArrayAsSingle"] = true` voor de specifieke marker |
| Workbook wordt leeg opgeslagen | `Apply()` niet aangeroepen vóór `Save()` | Roep altijd `worksheet.SmartMarkers.Apply()` aan vóór het opslaan |

## Volledig Werkend Voorbeeld (Klaar om te Kopiëren‑Plakken)

Hieronder staat het complete programma dat je in een console‑app kunt plakken. Er zijn geen extra bestanden nodig.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();

        // Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");

        // Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;

        // Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Place the marker in a cell so we can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

Voer het programma uit, open `SmartMarkerResult.xlsx`, en je ziet de JSON‑array (of het eerste element) keurig geplaatst in cel **A1**.

## Volgende Stappen: De Oplossing Uitbreiden

Nu je weet **hoe je een workbook** maakt, **hoe je markers toevoegt**, en **json array** gebruikt met Aspose.Cells, overweeg dan deze vervolgidées:

1. **Meerdere Werkbladen** – Loop door een lijst van werkbladen en koppel verschillende marker‑collecties aan elk.
2. **Dynamische JSON** – Haal JSON op van een web‑API (`HttpClient`) en voer het direct in `smartMarkerCollection.Add` in.
3. **Styling van Output** – Na het toepassen van markers, formatteer cellen (lettertypen, kleuren) om het rapport er gepolijst uit te laten zien.
4. **Exportformaten** – Sla de workbook op als PDF, CSV of HTML door `workbook.Save("file.pdf")` te wijzigen.

Elk van deze onderwerpen maakt vanzelfsprekend gebruik van **smart markers aspose.cells**, zodat je dezelfde kernconcepten uitbreidt die je net hebt geleerd.

## Conclusie

We hebben stap voor stap **hoe je een workbook** vanaf nul maakt, **hoe je markers toevoegt**, en hoe je **json array** gebruikt met Aspose.Cells smart markers. Het volledige, uitvoerbare voorbeeld laat de volledige workflow zien, van het initialiseren van de `Workbook` tot het opslaan van het eindbestand. Door de `ArrayAsSingle`‑vlag te schakelen, krijg je fijne controle over hoe JSON‑data in Excel verschijnt, waardoor de oplossing aanpasbaar is voor een breed scala aan rapportagescenario's.

Probeer de code, pas de JSON aan, en experimenteer met extra markers. Zodra je deze bouwstenen onder de knie hebt, wordt het genereren van geavanceerde Excel‑rapporten een eitje. Vragen of een cool use‑case om te delen? Laat een reactie achter—happy coding!

![Diagram showing how to create workbook with smart markers in Aspose.Cells](https://example.com/images/create-workbook-smart-markers.png "how to create workbook with Aspose.Cells smart markers")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}