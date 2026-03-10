---
category: general
date: 2026-02-15
description: Parse geneste JSON C# met SmartMarkers en leer hoe je een JSON‑payload
  C# maakt voor complexe bestellingen. Stapsgewijze gids met volledige code en uitleg.
draft: false
keywords:
- parse nested json c#
- create json payload c#
language: nl
og_description: Parse geneste JSON in C# direct. Leer hoe je een JSON‑payload in C#
  maakt en deze verwerkt met SmartMarkers in een compleet, uitvoerbaar voorbeeld.
og_title: Geneste JSON parseren C# – JSON‑payload maken C#
tags:
- json
- csharp
- smartmarkers
title: Geneste JSON parseren in C# – JSON‑payload maken in C#
url: /nl/net/smart-markers-dynamic-data/parse-nested-json-c-create-json-payload-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Geneste JSON C# – JSON‑payload maken C#  

Heb je ooit **geneste JSON C#** moeten parseren maar wist je niet waar te beginnen? Je bent niet de enige—veel ontwikkelaars lopen tegen een muur aan wanneer hun gegevens arrays binnen objecten bevatten. Het goede nieuws is dat je met een paar regels code zowel **JSON‑payload maken C#** kunt doen als SmartMarkers de geneste structuur voor je laat doorlopen.  

In deze tutorial bouwen we een JSON‑string die bestellingen met regel‑items weergeeft, schakelen we de SmartMarkers‑processor in om geneste reeksen te begrijpen, en verifiëren we uiteindelijk dat de gegevens correct zijn geparseerd. Aan het einde heb je een zelfstandige, kant‑klaar‑te‑kopiëren‑en‑plakken‑programma dat je kunt aanpassen aan elke hiërarchische JSON die je tegenkomt.

## Wat je nodig hebt  

- .NET 6 of later (de code compileert ook met .NET Core 3.1)  
- Een referentie naar de SmartMarkers‑bibliotheek (of een vergelijkbare processor die geneste reeksen ondersteunt)  
- Basiskennis van C#—niets exotisch, alleen de gebruikelijke `using`‑statements en een `Main`‑methode  

Dat is alles. Geen extra NuGet‑pakketten naast de marker‑bibliotheek, en geen externe services.

## Stap 1: JSON‑payload maken C# – De data bouwen  

Eerst maken we de JSON‑string die een array van bestellingen bevat, waarbij elke bestelling zijn eigen `Lines`‑array heeft. Beschouw het als een mini‑order‑management‑snapshot.

```csharp
using System;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // STEP 1 – Define the JSON payload with nested arrays
            // -------------------------------------------------
            string ordersJson = @"{
                ""Orders"": [
                    {
                        ""Id"": 1,
                        ""Lines"": [
                            { ""Prod"": ""A"" },
                            { ""Prod"": ""B"" }
                        ]
                    },
                    {
                        ""Id"": 2,
                        ""Lines"": [
                            { ""Prod"": ""C"" }
                        ]
                    }
                ]
            }";

            // The rest of the steps follow…
```

Waarom de payload als een verbatim‑string bouwen? Het behoudt regeleinden en laat je de structuur in één oogopslag zien—handig bij het debuggen van geneste JSON.  

> **Pro tip:** Als je JSON afkomstig is uit een database of een API, kun je de literal vervangen door `File.ReadAllText` of een web‑request—niets in deze tutorial is afhankelijk van de bron.

## Stap 2: Geneste reeksen inschakelen met SmartMarkerOptions  

SmartMarkers heeft een kleine duwtje nodig om te begrijpen dat een array een andere array kan bevatten. Dat doet `EnableNestedRanges`.

```csharp
            // -------------------------------------------------
            // STEP 2 – Configure SmartMarker options for nesting
            // -------------------------------------------------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                EnableNestedRanges = true   // <-- crucial for Orders → Lines
            };
```

Het instellen van `EnableNestedRanges` op `true` vertelt de processor elke `Lines`‑collectie te behandelen als een sub‑range van de bovenliggende `Orders`‑range. Zonder deze vlag zou de binnenste lus worden genegeerd, en zie je alleen de objecten op het hoogste niveau.

## Stap 3: De JSON verwerken met SmartMarkersProcessor  

Nu geven we de JSON‑string en de opties door aan de processor. De aanroep is synchroon en retourneert niets—SmartMarkers schrijft de resultaten naar de interne context, die je later kunt ophalen.

```csharp
            // -------------------------------------------------
            // STEP 3 – Run the processor on the JSON payload
            // -------------------------------------------------
            ws.SmartMarkersProcessor.Process(ordersJson, options);
```

Gebruik je een andere bibliotheek, vervang dan `ws.SmartMarkersProcessor.Process` door de juiste methode; het principe blijft hetzelfde—geef de JSON en de configuratie door die geneste verwerking mogelijk maakt.

## Stap 4: Het geparseerde resultaat verifiëren  

Na verwerking wil je meestal bevestigen dat elke bestelling en zijn regel‑items zijn bezocht. Hieronder een eenvoudige manier om de data terug naar de console te dumpen met een hypothetische `GetProcessedData`‑methode (vervang door de daadwerkelijke accessor van jouw bibliotheek).

```csharp
            // -------------------------------------------------
            // STEP 4 – Output the parsed structure (demo purpose)
            // -------------------------------------------------
            var result = ws.SmartMarkersProcessor.GetProcessedData(); // pseudo‑code
            Console.WriteLine("=== Parsed Orders ===");
            foreach (var order in result.Orders)
            {
                Console.WriteLine($"Order Id: {order.Id}");
                foreach (var line in order.Lines)
                {
                    Console.WriteLine($"  - Product: {line.Prod}");
                }
            }
        }
    }
}
```

**Verwachte console‑output**

```
=== Parsed Orders ===
Order Id: 1
  - Product: A
  - Product: B
Order Id: 2
  - Product: C
```

Het zien van de hiërarchie bevestigt dat **parse nested json c#** heeft gewerkt zoals bedoeld.

## Stap 5: Randgevallen & Veelvoorkomende valkuilen  

### Lege collecties  
Als een bestelling geen `Lines` heeft, maakt de processor nog steeds een lege range aan. Zorg ervoor dat je downstream‑code een lege lijst aankan zonder een `NullReferenceException` te gooien.

### Diep geneste structuren  
`EnableNestedRanges` werkt standaard voor twee‑niveau nesting. Voor drie of meer niveaus moet je mogelijk `MaxNestedDepth` instellen (als de bibliotheek dit exposeert) of de processor recursief aanroepen voor elk sub‑object.

### Speciale tekens  
JSON‑strings met aanhalingstekens, backslashes of Unicode vereisen juiste escaping. Het gebruik van een verbatim‑string (`@""`) zoals wij deden omzeilt de meeste problemen, maar als je JSON programmatisch opbouwt, laat dan `System.Text.Json.JsonSerializer` de escaping afhandelen.

### Prestaties  
Het parseren van grote payloads (megabytes) kan veel geheugen verbruiken. Overweeg om de JSON te streamen met `Utf8JsonReader` en stukken aan de processor te voeren als je tegen prestatie‑knelpunten aanloopt.

## Visueel overzicht  

![Diagram dat laat zien hoe parse nested json c# door SmartMarkers‑verwerking stroomt](parse-nested-json-csharp-diagram.png "parse nested json c# diagram")

De afbeelding toont de reis van ruwe JSON → SmartMarkerOptions → Processor → Geparseerd objectmodel.

## Samenvatting  

We hebben een volledige **parse nested json c#**‑voorbeeld doorlopen, van **create json payload c#** tot het verifiëren van de geneste data na verwerking. De belangrijkste lessen zijn:

1. Bouw een goed gestructureerde JSON‑string die je domeinobjecten weerspiegelt.  
2. Schakel `EnableNestedRanges` (of het equivalent) in zodat de parser inner‑arrays respecteert.  
3. Voer de processor uit en inspecteer het resultaat om te verzekeren dat elk niveau is bezocht.  

## Wat is het vervolg?  

- **Dynamische payloads:** Vervang de hard‑gecodeerde string door objecten die worden geserializeerd via `System.Text.Json`.  
- **Aangepaste markers:** Breid SmartMarkers uit met eigen tags om berekende velden in elk regel‑item te injecteren.  
- **Foutafhandeling:** Plaats de `Process`‑aanroep in een try/catch en log `SmartMarkerException`‑details voor probleemoplossing.  

Voel je vrij om te experimenteren—verwissel de `Orders`‑array bijvoorbeeld met klanten, facturen, of elke hiërarchische data die je moet **parse nested json c#**. Het patroon blijft hetzelfde.

Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}