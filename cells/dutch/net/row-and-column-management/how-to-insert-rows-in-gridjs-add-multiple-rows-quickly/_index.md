---
category: general
date: 2026-03-01
description: Hoe rijen in GridJs invoegen eenvoudig gemaakt—leer hoe je 100 rijen
  toevoegt, lege rijen maakt en het totale aantal rijen controleert in slechts een
  paar regels C#.
draft: false
keywords:
- how to insert rows
- add multiple rows
- add 100 rows
- create empty rows
- check total rows
language: nl
og_description: Hoe voeg je snel rijen toe in GridJs. Deze gids laat je zien hoe je
  meerdere rijen toevoegt, lege rijen maakt en het totale aantal rijen controleert
  met nette C#-code.
og_title: Hoe rijen invoegen in GridJs – Snelle gids
tags:
- C#
- GridJs
- data‑grid
title: Hoe rijen invoegen in GridJs – Voeg snel meerdere rijen toe
url: /nl/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe rijen in te voegen in GridJs – Voeg meerdere rijen snel toe

Heb je je ooit afgevraagd **hoe je rijen kunt invoegen** in een GridJs data‑grid zonder een eindeloze lus te schrijven? Je bent niet de enige. In veel enterprise‑applicaties kom je op een moment waar je ruimte moet maken voor een bulk‑import, een sjabloon, of gewoon een tijdelijke aanduiding voor toekomstige gegevens. Het goede nieuws? GridJs biedt je één methode die het zware werk voor je doet.

In deze tutorial lopen we een volledig, uitvoerbaar voorbeeld door dat laat zien hoe je **100 rijen kunt toevoegen**, **lege rijen kunt maken**, en **het totale aantal rijen kunt controleren** na de bewerking. Aan het einde heb je een solide patroon dat je in elk C#‑project dat GridJs gebruikt kunt gebruiken.

## Vereisten

- .NET 6.0 of later (de API werkt hetzelfde op .NET Framework 4.8, maar de nieuwere SDK biedt prettigere tooling).
- Een referentie naar het `GridJs` NuGet‑pakket of de gecompileerde DLL die de `GridJs`‑klasse bevat.
- Basiskennis van C#‑syntaxis—niets exotisch, alleen standaard `using`‑statements en object‑georiënteerde basisprincipes.

Als een van deze punten een rode vlag oplevert, pauzeer dan een minuut en los het op. De stappen die volgen gaan ervan uit dat het grid‑object al is geïnstantieerd en klaar is om rijen te ontvangen.

![illustratie hoe rijen in te voegen](gridjs-insert-rows.png)

## Stap 1: Maak de Grid‑instantie aan

Allereerst heb je een `GridJs`‑object nodig. In een echte applicatie zou dit waarschijnlijk afkomstig zijn van een servicelaag of via dependency injection worden geïnjecteerd, maar voor de duidelijkheid maken we het lokaal aan.

```csharp
using System;
using GridJsLibrary;   // <-- replace with the actual namespace of GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create or obtain the grid you want to modify
            GridJs gridJs = new GridJs();   // replace with your actual grid initialization
```

> **Waarom dit belangrijk is:** Het instantieren van het grid geeft je een schone lei, waardoor de rij‑invoeglogica niet botst met overgebleven staat van eerdere runs.

## Stap 2: Voeg 100 rijen toe op een specifieke index

Nu volgt de kern van **hoe je rijen kunt invoegen**. De `InsertRows`‑methode neemt twee argumenten: de nul‑gebaseerde startindex en het aantal rijen dat je wilt toevoegen. Laten we 100 rijen invoegen beginnend bij rij 5.

```csharp
            // Step 2: Insert 100 rows starting at row index 5 (zero‑based)
            // This pushes existing rows down and creates space for new data.
            gridJs.InsertRows(5, 100);
```

> **Pro tip:** Als je rijen aan het einde van het grid wilt toevoegen, kun je `gridJs.RowCount` gebruiken als startindex. Op die manier voeg je effectief toe (“append”) in plaats van in te voegen.

### Wat gebeurt er onder de motorkap?

- **Geheugenallocatie:** `InsertRows` reserveert intern een blok lege rij‑objecten, zodat je niet elke afzonderlijke rij handmatig hoeft te instantieren.
- **Indexverschuiving:** Alle rijen die zich op index 5 of later bevonden, verschuiven 100 posities naar beneden, waarbij hun oorspronkelijke gegevens behouden blijven.
- **Prestaties:** Omdat de bewerking in één enkele oproep wordt uitgevoerd, is deze meestal sneller dan 100 keer `InsertRow` in een lus aanroepen.

## Stap 3: Verifieer de invoeging (Controleer het totale aantal rijen)

Nadat je rijen hebt toegevoegd, is het een goede gewoonte om **het totale aantal rijen te controleren** om te bevestigen dat de bewerking geslaagd is. De `RowCount`‑eigenschap geeft je het huidige aantal rijen in het grid.

```csharp
            // Step 3: (Optional) Verify the insertion or continue processing
            int newRowCount = gridJs.RowCount; // example property to check total rows
            Console.WriteLine($"Grid now contains {newRowCount} rows.");
```

Als je begon met bijvoorbeeld 20 rijen, zou je `120` in de console moeten zien verschijnen. Deze eenvoudige verificatiestap kan je later uren aan debugging besparen.

## Stap 4: Vul de nieuw aangemaakte lege rijen (optioneel)

Vaak wil je die vers aangemaakte rijen vullen met placeholder‑gegevens of standaardobjecten. Aangezien `InsertRows` je een blok lege rijen geeft, kun je over het bereik itereren en waarden toewijzen.

```csharp
            // Optional: Fill the newly created rows with default values
            for (int i = 5; i < 5 + 100; i++)
            {
                var row = gridJs.GetRow(i); // assume GetRow returns a mutable row object
                row["Name"] = $"Placeholder {i - 4}";
                row["CreatedOn"] = DateTime.UtcNow;
            }

            // Verify a sample row
            var sample = gridJs.GetRow(5);
            Console.WriteLine($"First inserted row name: {sample["Name"]}");
        }
    }
}
```

> **Waarom je dit zou doen:** Het aanmaken van lege rijen is handig wanneer je een sjabloon nodig hebt voor gebruikersinvoer, een batch‑upload placeholder, of simpelweg ruimte wilt reserveren voor toekomstige berekeningen.

## Veelvoorkomende variaties & randgevallen

### Minder dan 100 rijen toevoegen

Als je alleen **meerdere rijen wilt toevoegen**—bijvoorbeeld 10 of 25—werkt dezelfde `InsertRows`‑aanroep; vervang gewoon `100` door het gewenste aantal.

```csharp
gridJs.InsertRows(startIndex, 25); // adds 25 rows
```

### Invoegen aan de bovenkant van het grid

Wil je rijen vooraan toevoegen? Gebruik `0` als startindex:

```csharp
gridJs.InsertRows(0, 5); // adds 5 rows at the very beginning
```

### Omgaan met out‑of‑range indexen

Een index groter dan `RowCount` doorgeven veroorzaakt een `ArgumentOutOfRangeException`. Bescherm hiertegen:

```csharp
int safeIndex = Math.Min(requestedIndex, gridJs.RowCount);
gridJs.InsertRows(safeIndex, 100);
```

### Omgaan met alleen‑lezen grids

Sommige GridJs‑configuraties bieden een alleen‑lezen weergave. In dat scenario moet je overschakelen naar een schrijfbare instantie of tijdelijk de alleen‑lezen‑vlag uitschakelen voordat je `InsertRows` aanroept.

## Prestatie‑tips

- **Batch‑operaties:** Als je rijen herhaaldelijk in een lus invoegt, bundel ze dan in één `InsertRows`‑aanroep waar mogelijk. Dit vermindert interne lijst‑herallocaties.
- **Vermijd UI‑verversingen:** In UI‑gebonden grids, schort de weergave (`gridJs.BeginUpdate()`) vóór het invoegen van rijen en hervat (`gridJs.EndUpdate()`) daarna om flikkering te voorkomen.
- **Geheugenprofilering:** Grote invoegingen (bijv. >10.000 rijen) kunnen het geheugenverbruik laten pieken. Overweeg paginering of streaming van gegevens in plaats van één enorme invoeging.

## Volledige werkende voorbeeld‑overzicht

Alles samenvoegend, hier is het volledige, kant‑klaar‑te‑kopiëren‑en‑plakken programma:

```csharp
using System;
using GridJsLibrary;   // replace with the actual namespace

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create the grid instance
            GridJs gridJs = new GridJs();

            // Insert 100 rows starting at index 5
            gridJs.InsertRows(5, 100);

            // Verify insertion
            int newRowCount = gridJs.RowCount;
            Console.WriteLine($"Grid now contains {newRowCount} rows.");

            // Optional: Fill new rows with placeholder data
            for (int i = 5; i < 5 + 100; i++)
            {
                var row = gridJs.GetRow(i);
                row["Name"] = $"Placeholder {i - 4}";
                row["CreatedOn"] = DateTime.UtcNow;
            }

            // Show a sample row
            var sample = gridJs.GetRow(5);
            Console.WriteLine($"First inserted row name: {sample["Name"]}");
        }
    }
}
```

Voer dit programma uit, en je ziet de console‑output die het aantal rijen bevestigt en de naam van de eerste placeholder‑rij. Dat is het volledige antwoord op **hoe je rijen kunt invoegen** in GridJs, compleet met verificatie en optionele gegevenspopulatie.

## Conclusie

We hebben een duidelijke, end‑to‑end‑oplossing doorlopen voor **hoe je rijen kunt invoegen** in GridJs, waarbij we hebben behandeld hoe je **100 rijen kunt toevoegen**, **lege rijen kunt maken**, en **het totale aantal rijen kunt controleren** na de bewerking. Het patroon schaalt—pas gewoon de startindex en het aantal aan om **meerdere rijen toe te voegen** waar je ze nodig hebt.  

Volgende stappen? Probeer deze techniek te combineren met bulk‑data‑importen vanuit CSV‑bestanden, of experimenteer met conditionele rij‑creatie op basis van gebruikersinvoer. Als je nieuwsgierig bent naar het verwijderen van rijen, sorteren, of het toepassen van conditionele opmaak, zijn dat natuurlijke uitbreidingen van dezelfde API‑surface.

Veel plezier met coderen, en moge je grids altijd perfect van grootte blijven!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}