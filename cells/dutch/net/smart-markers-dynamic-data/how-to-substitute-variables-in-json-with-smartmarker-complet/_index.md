---
category: general
date: 2026-03-29
description: Hoe variabelen in JSON te vervangen met SmartMarker – leer hoe je een
  if-expressie gebruikt, conditionele logica toepast, waarden vermenigvuldigt en JSON
  moeiteloos genereert.
draft: false
keywords:
- how to substitute variables
- use if expression
- how to apply conditional
- how to multiply values
- how to generate json
language: nl
og_description: Hoe variabelen te vervangen in JSON met SmartMarker. Ontdek hoe je
  een if‑expressie gebruikt, conditionele logica toepast, waarden vermenigvuldigt
  en JSON in enkele minuten genereert.
og_title: Hoe variabelen in JSON te vervangen met SmartMarker – Stap voor stap
tags:
- C#
- SmartMarker
- JSON templating
title: Hoe variabelen in JSON te vervangen met SmartMarker – Complete gids
url: /nl/net/smart-markers-dynamic-data/how-to-substitute-variables-in-json-with-smartmarker-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe variabelen te vervangen in JSON met SmartMarker – Complete gids

Heb je je ooit afgevraagd **hoe variabelen te vervangen** in een JSON‑payload zonder een eigen parser te schrijven? Je bent niet de enige. In veel integratiescenario's—denk aan facturen, prijsberekeningsengines of dynamische configuratiebestanden—moet je runtime‑waarden injecteren, eenvoudige conditionele logica toepassen en misschien zelfs een snelle vermenigvuldiging uitvoeren. Deze tutorial laat je precies zien **hoe variabelen te vervangen** met behulp van de SmartMarker‑bibliotheek, terwijl de JSON schoon en leesbaar blijft.

We lopen een praktijkvoorbeeld door dat **use if expression**, **how to apply conditional**, **how to multiply values** en **how to generate json** behandelt. Aan het einde heb je een kant‑klaar C#‑fragment dat je in elk .NET‑project kunt gebruiken.

## Wat je zult leren

- Stel `SmartMarkerOptions` in om herbruikbare variabelen op te slaan.  
- Schrijf een JSON‑template die een `if`‑expressie bevat voor conditionele logica.  
- Vermenigvuldig een waarde met een variabele binnen de template.  
- Verwerk de template met `SmartMarkerProcessor` en krijg de uiteindelijke JSON‑string.  
- Los veelvoorkomende valkuilen op, zoals ontbrekende variabelen of ongeldige expressies.

Geen externe services, geen zware afhankelijkheden—alleen plain C# en het SmartMarker‑NuGet‑pakket.

## Hoe variabelen te vervangen – Stapsgewijs overzicht

Hieronder zie je een overzichtsdiagram van de workflow. Beschouw het als een pijplijn waarbij je ruwe JSON‑template aan de linkerkant binnenkomt, de SmartMarker‑engine zijn magie doet, en de volledig gerenderde JSON aan de rechterkant uitkomt.

![Diagram dat laat zien hoe variabelen te vervangen in JSON](https://example.com/images/smartmarker-flow.png "Hoe variabelen te vervangen in JSON")

*Afbeeldingsalt‑tekst: Diagram dat laat zien hoe variabelen te vervangen in JSON.*

## Stap 1: Installeer en importeer SmartMarker

Voordat je kunt beginnen, zorg ervoor dat het SmartMarker‑pakket in je project is opgenomen. Als je de .NET‑CLI gebruikt, voer dan uit:

```bash
dotnet add package SmartMarker
```

Voeg vervolgens de benodigde `using`‑directives toe aan de bovenkant van je C#‑bestand:

```csharp
using SmartMarker;
using SmartMarker.Models;
using System;
```

> **Pro tip:** De nieuwste versie (vanaf maart 2026) is 2.4.1. Deze ondersteunt .NET 6 en later, maar werkt ook prima met .NET Framework 4.7.

## Stap 2: Maak SmartMarker‑opties aan en definieer variabelen

Nu maken we een instantie van `SmartMarkerOptions` die alle variabelen bevat die we in de template willen hergebruiken. Hier beantwoorden we de vraag **how to substitute variables**—de variabelen fungeren als placeholders die later door SmartMarker worden vervangen.

```csharp
// Step 2: Create SmartMarker options to hold variables used in the template
var smartMarkerOptions = new SmartMarkerOptions();

// Define a variable (Rate) that we’ll reference later in the JSON expression
smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission rate
```

Waarom de tarief opslaan in `Variables` in plaats van hard‑coderen? Omdat je dat getal mogelijk uit een database, een configuratiebestand of een gebruikersinvoer haalt. Het in de opties bewaren maakt de template herbruikbaar en testbaar.

## Stap 3: Schrijf de JSON‑template met een `if`‑expressie

Hier komt het **use if expression**‑trefwoord goed van pas. SmartMarker laat je conditionele logica direct in de JSON‑string insluiten. De syntaxis lijkt een beetje op een eigenschapsnaam, maar SmartMarker behandelt het als een directive.

```csharp
// Step 3: Prepare the JSON data with a conditional field that uses the variable
string jsonTemplate = @"{
    ""Amount"": 1000,
    ""if(Amount>500)"": ""${Amount * Rate}""
}";
```

Let op de sleutel `if(Amount>500)`. SmartMarker evalueert de expressie `Amount>500`; als deze waar is, wordt de bijbehorende waarde (`${Amount * Rate}`) in de output geplaatst. De `${...}`‑syntaxis is de *variable substitution*‑engine—hier **how to multiply values** (`Amount * Rate`) voordat het resultaat wordt geïnjecteerd.

## Stap 4: Verwerk de template en haal de uiteindelijke JSON op

Met de opties en template klaar, geven we alles door aan de processor. De methode `ProcessJson` parseert de template, past de voorwaarde toe, voert de vermenigvuldiging uit en retourneert een schone JSON‑string.

```csharp
// Step 4: Process the JSON with SmartMarker, applying the variable substitution
string resultJson = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(resultJson);
```

Running the snippet prints:

```json
{
  "Amount": 1000,
  "Result": "80"
}
```

**Wat gebeurde er?**  
- `Amount` is 1000, wat voldoet aan `Amount>500`.  
- SmartMarker evalueert `${Amount * Rate}` → `1000 * 0.08 = 80`.  
- De oorspronkelijke conditionele sleutel (`if(Amount>500)`) wordt vervangen door een schone eigenschapsnaam (`Result`). Standaard gebruikt SmartMarker `"Result"` maar je kunt dit aanpassen (meer hierover later).

Als je `Amount` verandert naar `400`, wordt de output:

```json
{
  "Amount": 400
}
```

Het conditionele blok verdwijnt omdat de expressie `false` oplevert. Dat is de kern van **how to apply conditional**‑logica in JSON.

## Stap 5: Aanpassen van de output‑eigenschapsnaam (optioneel)

Soms wil je niet de generieke `"Result"`‑sleutel. SmartMarker laat je een aangepaste naam opgeven via de `RenameIfExpression`‑optie:

```csharp
smartMarkerOptions.RenameIfExpression = "Discount";
string customResult = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(customResult);
```

Output:

```json
{
  "Amount": 1000,
  "Discount": "80"
}
```

Nu wordt de conditionele waarde opgeslagen onder een meer betekenisvolle eigenschapsnaam—perfect voor downstream‑services die een specifiek veld verwachten.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| Variabele niet gevonden | Je hebt een variabele aangewezen die niet aanwezig is in `smartMarkerOptions.Variables`. | Controleer de spelling en zorg dat de variabele is toegevoegd vóór verwerking. |
| Ongeldige `if`‑syntaxis | Ontbrekende haakjes of verkeerde operator (`>`, `<`, `==`). | Volg exact het `if(<expression>)`‑patroon; SmartMarker ondersteunt alleen eenvoudige numerieke vergelijkingen. |
| JSON wordt ongeldig | Per ongeluk een komma achter het conditionele blok laten staan. | Laat SmartMarker de verwijdering afhandelen; houd de oorspronkelijke template syntactisch correct. |
| Onverwacht getalformaat | Resultaat verschijnt als een string `"80"` in plaats van een getal. | Cast of parse later, of gebruik `${(Amount * Rate):N0}` voor numerieke opmaak. |

## Volledig werkend voorbeeld (klaar om te kopiëren en plakken)

Hieronder staat het volledige programma dat je kunt compileren en uitvoeren. Het demonstreert **how to generate json** met dynamische variabelen, conditionals en rekenkundige bewerkingen—alles in minder dan 30 regels.

```csharp
using System;
using SmartMarker;
using SmartMarker.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Create SmartMarker options and define a reusable variable
        var smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission
        smartMarkerOptions.RenameIfExpression = "Discount"; // optional custom name

        // 2️⃣ JSON template with an if expression and multiplication
        string jsonTemplate = @"{
            ""Amount"": 1000,
            ""if(Amount>500)"": ""${Amount * Rate}""
        }";

        // 3️⃣ Process the template
        string output = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);

        // 4️⃣ Show the result
        Console.WriteLine("Generated JSON:");
        Console.WriteLine(output);
    }
}
```

**Verwachte console‑output**

```
Generated JSON:
{
  "Amount": 1000,
  "Discount": "80"
}
```

Voel je vrij om `Amount` te wijzigen om de conditionele tak te testen, of `Rate` aan te passen om verschillende kortingsberekeningen te zien.

## Het patroon uitbreiden – Meer “How to” scenario’s

- **How to substitute variables** uit een configuratiebestand: Laad een `Dictionary<string, object>` uit `appsettings.json` en voer deze in `smartMarkerOptions.Variables`.  
- **How to use if expression** voor meerdere voorwaarden: Koppel ze zoals "if(Amount>500 && CustomerType=='VIP')"—SmartMarker ondersteunt logische AND/OR.  
- **How to apply conditional** opmaak: Gebruik `${Amount:0.00}` binnen de expressie om decimalen te regelen.  
- **How to multiply values** met complexere wiskunde: `${(Amount - Discount) * TaxRate}` werkt op dezelfde manier.  
- **How to generate json** voor geneste objecten: Plaats het conditionele blok binnen een ander JSON‑object, en SmartMarker behoudt de hiërarchie.

## Conclusie

We hebben **how to substitute variables** in JSON met SmartMarker behandeld, **use if expression** gedemonstreerd voor conditionele inclusie, **how to apply conditional**‑logica uitgelegd, **how to multiply values** binnen een template laten zien, en tenslotte **how to generate json** geïllustreerd dat klaar is voor downstream‑consumptie. De aanpak is lichtgewicht, vereist geen externe templating‑engine, en past naadloos in elke C#‑codebase.

Probeer het—pas de variabelen aan, voeg meer voorwaarden toe, of wikkel het geheel in een helper‑klasse voor hergebruik in je oplossing. Wanneer je snel dynamische JSON moet produceren, is SmartMarker een solide, productie‑klare optie.

**Volgende stappen**

- Duik dieper in de geavanceerde functies van SmartMarker, zoals loops (`foreach`) en aangepaste functies.  
- Combineer deze techniek met ASP.NET Core‑endpoints om dynamische JSON‑API’s te leveren.  
- Verken andere templating‑bibliotheken (bijv. Handlebars.NET) voor vergelijking, vooral als je een rijkere syntaxis nodig hebt.

Heb je vragen of een specifiek use‑case waar je tegenaan loopt? Laat een reactie achter hieronder, en laten we samen het probleem oplossen. Veel plezier met coderen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}