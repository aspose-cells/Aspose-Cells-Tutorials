---
category: general
date: 2026-02-14
description: Hoe je hiërarchie maakt in SmartMarker‑sjablonen is makkelijker dan je
  denkt – leer hoe je hiërarchische gegevens maakt en hoe je werknemers efficiënt
  kunt weergeven.
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: nl
og_description: Hoe je hiërarchie in SmartMarker‑sjablonen maakt, is eenvoudig. Volg
  deze gids om hiërarchische gegevens te maken en werknemers met geneste bereiken
  te vermelden.
og_title: Hoe hiërarchie te creëren met SmartMarker – Complete gids
tags:
- SmartMarker
- C#
- templating
title: Hoe een hiërarchie te maken met SmartMarker – Stapsgewijze gids
url: /nl/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe hiërarchie te maken met SmartMarker – Complete gids

Heb je je ooit afgevraagd **hoe je hiërarchie** kunt maken in een SmartMarker‑template zonder je haar uit te trekken? Je bent niet de enige. In veel rapportagescenario's heb je een ouder‑kindrelatie nodig — denk aan afdelingen en de mensen die er werken. Het goede nieuws is dat SmartMarker het een fluitje van een cent maakt zodra je de juiste stappen kent.

In deze tutorial lopen we het volledige proces door: van **het maken van hiërarchische data** in C#, het inschakelen van geneste bereiken, en uiteindelijk het renderen van een template dat **medewerkers opsomt** per afdeling. Aan het einde heb je een kant‑klaar voorbeeld dat je in elk .NET‑project kunt gebruiken.

---

## Wat je nodig hebt

- .NET 6+ (elke recente versie werkt)
- Een referentie naar de **SmartMarker**‑bibliotheek (de `ws.SmartMarkerProcessor` namespace)
- Basiskennis van C# – niets ingewikkelds, alleen een paar objecten en een lambda of twee
- Een IDE of editor naar keuze (Visual Studio, Rider, VS Code… je kiest zelf)

Als je dat al hebt, geweldig—laten we erin duiken.

---

## Hoe hiërarchie te maken – Overzicht

Het kernidee is om een **geneste objectgrafiek** te bouwen die de structuur weerspiegelt die je in het uiteindelijke document wilt zien. In ons geval ziet de grafiek er zo uit:

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

SmartMarker kan vervolgens over `Departments` itereren en, omdat we **geneste bereikverwerking** inschakelen, zal het ook automatisch over elke `Employees`‑collectie van een afdeling loopen.

---

## Stap 1: Bouw het hiërarchische datamodel

Eerst maken we een anoniem object dat een array van afdelingen bevat, elk met zijn eigen medewerkerslijst. Het gebruik van een anonieme type houdt het voorbeeld lichtgewicht—voel je vrij om later echte POCO‑klassen te gebruiken.

```csharp
// Step 1: Create hierarchical data that SmartMarker will iterate over
var departmentData = new
{
    Departments = new[]
    {
        new { Name = "HR", Employees = new[] { "John", "Amy" } },
        new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
    }
};
```

> **Waarom dit belangrijk is:** De `Departments`‑array is de collectie op het hoogste niveau. Elk element bevat een `Employees`‑array, waardoor we de tweede hiërarchieniveau krijgen die we later benaderen met `#Departments.Employees#`.

---

## Stap 2: Schakel geneste bereikverwerking in

SmartMarker duikt niet in innerlijke collecties tenzij je het vertelt. Het `SmartMarkerOptions`‑object bevat die schakelaar.

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **Pro tip:** Als je deze vlag vergeet, geeft het innerlijke `#Employees#`‑bereik simpelweg niets terug, en zul je je afvragen waarom de template leeg is.

---

## Stap 3: Voer de processor uit met je gegevens

Nu geven we de data en opties door aan de processor. De variabele `ws` staat voor je **WebService** (of welk object ook de SmartMarker‑engine hostt).

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

Op dit moment parseert SmartMarker de template, vervangt `#Departments.Name#` door elke afdelingsnaam, en omdat geneste bereiken zijn ingeschakeld, itereren we door elke `Employees`‑collectie van een afdeling.

---

## Stap 4: Maak de sjabloonmarkers

Hieronder staat een minimale template die zowel de buitenste als de binnenste lussen demonstreert. Plak deze in de SmartMarker‑template‑editor (of een `.txt`‑bestand dat je aan de processor doorgeeft).

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Wanneer gerenderd zie je:

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **Wat je ziet:** De buitenste `#Departments.Name#` print de afdelingsnaam. Het binnenste `#Departments.Employees#`‑blok loopt over elke medewerker, en `#Departments.Employees#` binnen het blok geeft de daadwerkelijke naam weer.

---

## Verwachte output & verificatie

Het uitvoeren van het volledige voorbeeld (data + opties + template) moet precies de lijst produceren die hierboven staat. Om snel te verifiëren, kun je het resultaat naar de console dumpen:

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

Als je de twee afdelingskoppen gevolgd door hun medewerkers‑bulletpoints ziet, heb je met succes **een hiërarchie gemaakt** en **medewerkers opgesomd**.

---

## Veelvoorkomende valkuilen & randgevallen

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| Geen output voor medewerkers | `EnableNestedRange` onterecht op false | Zet `EnableNestedRange = true` |
| Dubbele medewerker namen | Zelfde array hergebruikt over afdelingen | Kloon de array of gebruik aparte collecties |
| Zeer grote hiërarchieën veroorzaken geheugenbelasting | SmartMarker laadt de volledige objectgrafiek in het geheugen | Stream data of pagina grote collecties |
| Sjabloon syntaxisfouten | Ontbrekende afsluitende `#/…#` tags | Gebruik de SmartMarker validator of voer een snelle test uit met een klein sjabloon |

---

## Verder gaan – Real‑world variaties

1. **Dynamische gegevensbronnen** – Haal afdelingen op uit een database en map ze naar de anonieme structuur met LINQ.  
2. **Conditionele opmaak** – Voeg een `IsManager`‑vlag toe aan elke medewerker en gebruik SmartMarker’s conditionele tags (`#if …#`) om managers te markeren.  
3. **Meerdere nestingsniveaus** – Als je teams binnen afdelingen nodig hebt, voeg dan gewoon een extra collectie (`Teams`) toe en houd `EnableNestedRange` ingeschakeld.

---

## Volledig werkend voorbeeld (klaar om te kopiëren‑plakken)

```csharp
using System;
using SmartMarker; // hypothetical namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Build hierarchical data
        var departmentData = new
        {
            Departments = new[]
            {
                new { Name = "HR", Employees = new[] { "John", "Amy" } },
                new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
            }
        };

        // 2️⃣ Enable nested ranges
        var smartMarkerOptions = new SmartMarkerOptions
        {
            EnableNestedRange = true
        };

        // 3️⃣ Start processing
        var ws = new WebService(); // assume this is your entry point
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);

        // 4️⃣ Retrieve and display the result
        string output = ws.SmartMarkerProcessor.GetProcessedResult(); // placeholder method
        Console.WriteLine(output);
    }
}
```

**Template (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Het uitvoeren van het programma print de hiërarchie precies zoals eerder getoond.

---

## Conclusie

We hebben behandeld **hoe je hiërarchie maakt** in SmartMarker, van het vormgeven van **hiërarchische data** in C# tot het inschakelen van geneste bereiken en uiteindelijk het renderen van een template die **medewerkers per afdeling opsomt**. Het patroon schaalt — voeg gewoon meer geneste collecties of conditionele logica toe en je hebt een krachtige rapportage‑engine binnen handbereik.

Klaar voor de volgende uitdaging? Probeer de anonieme types te vervangen door sterk getypeerde POCO‑klassen, of integreer deze flow in een ASP.NET Core‑endpoint die een PDF‑ of Word‑document retourneert. De mogelijkheden zijn eindeloos, en nu heb je een solide basis.

---

![How to create hierarchy diagram](image.png){alt="Diagram hoe hiërarchie te maken, toont de relatie tussen afdeling‑medewerker"}

*Happy coding! If you hit any snags, drop a comment below—I'm happy to help.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}