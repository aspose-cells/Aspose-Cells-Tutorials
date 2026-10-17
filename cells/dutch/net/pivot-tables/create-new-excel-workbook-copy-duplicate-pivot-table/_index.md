---
category: general
date: 2026-02-09
description: Maak een nieuw Excel‑werkboek en leer hoe je draaitabellen moeiteloos
  kunt kopiëren. Deze gids laat zien hoe je een draaitabel dupliceert en het werkboek
  als nieuw opslaat.
draft: false
keywords:
- create new excel workbook
- how to copy pivot
- duplicate pivot table
- save workbook as new
- how to copy worksheet
language: nl
og_description: Maak een nieuwe Excel-werkmap in C# en kopieer direct een draaitabel.
  Leer hoe je een draaitabel dupliceert en de werkmap opslaat als nieuw, met een volledig
  codevoorbeeld.
og_title: Nieuw Excel‑werkboek maken – Stapsgewijze draaitabelkopie
tags:
- excel
- csharp
- aspose.cells
- automation
title: Nieuw Excel-werkboek maken – Kopiëren & dupliceren draaitabel
url: /nl/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak nieuw Excel-werkboek – Kopiëren & dupliceren draaitabel

Heb je ooit moeten **create new Excel workbook** die een complexe draaitabel van een bestaand bestand overneemt? Je bent niet de enige—veel ontwikkelaars lopen tegen dit obstakel aan bij het automatiseren van rapportage‑pijplijnen. Het goede nieuws is dat je met een paar regels C# en de Aspose.Cells‑bibliotheek snel **how to copy pivot** kunt uitvoeren, een **duplicate pivot table** kunt maken, en **save workbook as new** kunt opslaan zonder Excel handmatig te openen.

In deze gids lopen we het volledige proces door, van het laden van het bron‑werkboek tot het opslaan van de gedupliceerde versie. Aan het einde heb je een kant‑klaar snippet dat je in elk .NET‑project kunt plaatsen. Geen poespas, alleen een praktische oplossing die je vandaag nog kunt testen.

## Wat deze tutorial behandelt

* **Prerequisites** – .NET 6+ (of .NET Framework 4.6+), Visual Studio, en het Aspose.Cells for .NET NuGet‑pakket.
* Stapsgewijze code die **creates new Excel workbook**, de draaitabel kopieert en het resultaat naar schijf schrijft.
* Uitleg over **why** elke regel belangrijk is, niet alleen **what** het doet.
* Tips voor het omgaan met randgevallen zoals verborgen werkbladen of grote gegevensbereiken.
* Een snelle blik op **how to copy worksheet** voor het geval je ooit het volledige blad nodig hebt in plaats van alleen de draaitabel.

Klaar? Laten we beginnen.

![illustratie van nieuw Excel-werkboek](image.png "Diagram dat bron‑werkboek, draaitabelkopie en bestemmings‑werkboek toont")

## Stap 1: Het project opzetten en Aspose.Cells installeren

Voordat we **create new Excel workbook** kunnen maken, hebben we een project nodig dat naar de juiste bibliotheek verwijst.

```csharp
// Install the Aspose.Cells package via NuGet:
//   dotnet add package Aspose.Cells
using Aspose.Cells;   // Provides Workbook, Worksheet, Range, etc.
using System;        // For basic .NET types
```

*Why this matters:* Aspose.Cells werkt volledig in het geheugen, zodat je Excel nooit op de server hoeft te starten. Het behoudt ook de draaitabel‑cache‑informatie, wat essentieel is voor een echte **duplicate pivot table**.

> **Pro tip:** Als je .NET Core targett, zorg er dan voor dat de runtime‑identifier (RID) van je project overeenkomt met het platform waarop je gaat implementeren; anders kun je native bibliotheek‑laadfouten tegenkomen.

## Stap 2: Laad het bron‑werkboek dat de draaitabel bevat

Nu gaan we **how to copy pivot** van een bestaand bestand. Het bron‑werkboek kan overal op schijf staan, een stream zijn, of zelfs een byte‑array.

```csharp
// Step 2: Load the source workbook that contains the pivot table
string sourcePath = @"C:\Reports\source.xlsx";
Workbook sourceWorkbook = new Workbook(sourcePath);

// Grab the first worksheet (adjust the index if your pivot lives elsewhere)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that encloses the pivot table – A1:D20 in this example
Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");
```

*Why we pick a range:* Een draaitabel bevindt zich binnen een regulier celbereik, maar heeft ook verborgen cache‑data gekoppeld aan het blad. Door het bereik **including the pivot** te kopiëren, zorgt Aspose.Cells ervoor dat de cache meereist, waardoor je een functionele **duplicate pivot table** in het bestemmingsbestand krijgt.

## Stap 3: Maak een nieuw Excel‑werkboek om de gekopieerde gegevens te ontvangen

Hier maken we daadwerkelijk **create new Excel workbook** dat de gedupliceerde draaitabel zal bevatten.

```csharp
// Step 3: Create a fresh workbook (empty) for the destination
Workbook destinationWorkbook = new Workbook(); // Starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

// Destination starts at A1 – you could offset if you need space for other data
Range destinationRange = destinationSheet.Cells.CreateRange("A1");
```

> **Why a fresh workbook?** Beginnen met een schone lei garandeert dat geen resterende opmaak of verborgen objecten interfereren met de gekopieerde draaitabel. Het maakt het resulterende bestand ook kleiner, wat handig is voor geautomatiseerde e‑mailbijlagen.

## Stap 4: Kopieer het draaitabel‑bereik naar het nieuwe werkboek

Nu voeren we de daadwerkelijke **how to copy pivot**‑bewerking uit.

```csharp
// Step 4: Copy the range (including the pivot) from source to destination
sourceRange.Copy(destinationRange);
```

Die ene regel doet het zware werk:

* De celwaarden, formules en opmaak worden overgebracht.
* De draaitabel‑cache wordt gedupliceerd, zodat de nieuwe draaitabel volledig functioneel blijft.
* Alle relatieve verwijzingen binnen de draaitabel passen zich automatisch aan de nieuwe locatie aan.

### Randgevallen afhandelen

* **Hidden worksheets:** Als het bronblad verborgen is, kopieert de draaitabel nog steeds goed, maar je wilt misschien het bestemmingsblad zichtbaar maken voor de gebruiker:
  ```csharp
  destinationSheet.IsVisible = true;
  ```
* **Large data sets:** Voor bereiken groter dan enkele duizenden rijen, overweeg `CopyTo` met `CopyOptions` te gebruiken om de bewerking te streamen en geheugenbelasting te verminderen.

## Stap 5: Sla het bestemmings‑werkboek op als een nieuw bestand

Tot slot **save workbook as new** en verifiëren we het resultaat.

```csharp
// Step 5: Save the destination workbook with the duplicated pivot table
string destPath = @"C:\Reports\copied.xlsx";
destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

// Quick verification – open the file manually or read a cell value
Console.WriteLine($"Workbook saved to {destPath}");
```

Als je `copied.xlsx` opent, zie je een exacte replica van de oorspronkelijke draaitabel, klaar voor verdere manipulatie of distributie.

### Optioneel: How to Copy Worksheet in plaats van alleen de draaitabel

Soms wil je het volledige blad, niet alleen de draaitabel. Dezelfde API maakt dit triviaal:

```csharp
// Copy the whole worksheet (including all charts, tables, etc.)
sourceSheet.CopyTo(destinationWorkbook, 0); // Inserts at index 0
destinationWorkbook.Save(@"C:\Reports\full_copy.xlsx");
```

Dit beantwoordt de **how to copy worksheet**‑vraag en kan handig zijn wanneer je extra blad‑niveau instellingen moet behouden.

## Volledig werkend voorbeeld

Alles bij elkaar genomen, hier is een zelfstandige console‑app die je kunt compileren en uitvoeren:

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load source workbook
        string sourcePath = @"C:\Reports\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");

        // 2️⃣ Create destination workbook
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
        Range destinationRange = destinationSheet.Cells.CreateRange("A1");

        // 3️⃣ Copy the pivot (range)
        sourceRange.Copy(destinationRange);

        // 4️⃣ Save as new file
        string destPath = @"C:\Reports\copied.xlsx";
        destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Successfully created new Excel workbook with duplicated pivot table at {destPath}");
    }
}
```

**Expected output:** De console toont een succesbericht, en `copied.xlsx` verschijnt in `C:\Reports` met een functionele draaitabel die identiek is aan die in `source.xlsx`.

## Veelgestelde vragen & valkuilen

* **Will formulas inside the pivot break?** Nee—omdat de pivot cache meereist met het bereik, blijven alle berekende velden intact.
* **What if the source pivot uses external data connections?** Die verbindingen worden *niet* gekopieerd. Je moet ze opnieuw tot stand brengen in het bestemmings‑werkboek of de draaitabel eerst omzetten naar een statische tabel.
* **Can I copy multiple pivots at once?** Absoluut—definieer gewoon een groter bereik dat alle draaitabellen omvat, of loop door elk `PivotTable`‑object in `sourceSheet.PivotTables` en kopieer ze afzonderlijk.
* **Do I need to dispose of the `Workbook` objects?** Ze implementeren `IDisposable`, dus het omhullen met `using`‑statements is een goede gewoonte, vooral in services met hoge doorvoersnelheid.

## Conclusie

Je weet nu **how to create new Excel workbook**, een draaitabel kopiëren, **duplicate pivot table**, en **save workbook as new** met C# en Aspose.Cells. De stappen zijn eenvoudig: laden, maken, kopiëren en opslaan. Met de optionele **how to copy worksheet**‑snippet heb je ook een alternatief voor volledige blad‑duplicatie.

Vervolgens kun je onderzoeken:

* Het toevoegen van aangepaste opmaak aan de gedupliceerde draaitabel.
* Het programmatically vernieuwen van de draaitabel‑cache na gegevenswijzigingen.
* Het exporteren van het werkboek naar PDF of CSV voor downstream‑systemen.

Probeer het, pas het bereik aan, en laat de automatisering het zware werk uit je rapportage‑workflow halen. Veel plezier met coderen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}