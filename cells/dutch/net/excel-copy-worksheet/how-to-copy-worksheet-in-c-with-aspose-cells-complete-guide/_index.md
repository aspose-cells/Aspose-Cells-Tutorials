---
category: general
date: 2026-03-30
description: Hoe een werkblad te kopiëren in C# met Aspose.Cells – stapsgewijze handleiding
  die het kopiëren van een celbereik, het kopiëren van kolommen tussen bladen, het
  kopiëren van een draaitabel in een werkblad en het toevoegen van een nieuw werkblad
  behandelt.
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: nl
og_description: Leer hoe je een werkblad kopieert in C# met Aspose.Cells. Deze gids
  toont het kopiëren van een celbereik, het behouden van draaitabellen, het kopiëren
  van kolommen tussen bladen en het toevoegen van code voor een nieuw werkblad.
og_title: Hoe een werkblad te kopiëren in C# – Volledige Aspose.Cells‑tutorial
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Hoe een werkblad te kopiëren in C# met Aspose.Cells – Complete gids
url: /nl/net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een werkblad te kopiëren in C# met Aspose.Cells – Complete gids

Heb je je ooit afgevraagd **how to copy worksheet** in C# zonder een enkele draaitabel of formule te verliezen? Je bent niet de enige—veel ontwikkelaars lopen tegen een muur aan wanneer ze een blad moeten dupliceren terwijl ze alle functionaliteit behouden. In deze tutorial lopen we een praktische, end‑to‑end oplossing door die niet alleen de gegevens kopieert maar ook de **copy worksheet pivot table** behoudt, **copy cell range** afhandelt, en de **add new worksheet code** toont die je nodig hebt.

We behandelen alles van het laden van de bron‑workbook tot het opslaan van het bestemmingsbestand, zodat je kolommen tussen bladen kunt kopiëren, objecten kunt behouden en je code schoon houdt. Geen vage verwijzingen, alleen een compleet, uitvoerbaar voorbeeld dat je vandaag nog in je project kunt plaatsen.

## Wat deze tutorial behandelt

- Een bestaand Excel‑bestand laden met Aspose.Cells  
- **add new worksheet code** gebruiken om een doelfblad te maken  
- Een **copy cell range** definiëren die een draaitabel bevat  
- **CopyOptions** instellen om grafieken, formules en draaitabellen intact te houden  
- **copy columns between sheets** uitvoeren met rij‑gewijze precisie  
- Het resultaat opslaan en verifiëren dat het werkblad correct is gekopieerd  

Aan het einde van deze gids kun je de vraag “how to copy worksheet” vol vertrouwen beantwoorden, of je nu rapporten automatiseert of een spreadsheet‑gedreven UI bouwt.

## Hoe een werkblad te kopiëren – Overzicht

Voordat we in de code duiken, schetsen we de high‑level flow. Beschouw het als een recept:

1. **Load** het bron‑workbook (`Source.xlsx`).  
2. **Add** een nieuw werkblad om de kopie in te plaatsen (`add new worksheet code`).  
3. **Define** het gebied dat je wilt dupliceren (`copy cell range`).  
4. **Configure** kopieeropties zodat de draaitabel overleeft (`copy worksheet pivot table`).  
5. **Copy** rijen en kolommen (`copy columns between sheets`).  
6. **Save** het nieuwe workbook (`Destination.xlsx`).  

Dat is alles—zes stappen, geen magie. Elke stap wordt hieronder uitgelegd met code‑fragmenten en de reden erachter.

## Stap 1 – Laad het bron‑workbook

Allereerst: je hebt een `Workbook`‑instantie nodig die naar het bestand wijst dat je wilt dupliceren. Deze stap is essentieel omdat Aspose.Cells direct met het bestandssysteem werkt, niet met de Office‑UI.

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*Waarom dit belangrijk is:* Het laden van het bestand creëert een in‑memory representatie van elk blad, elke cel en elk object. Zonder dit is er niets om te kopiëren, en elke poging om later `add new worksheet code` uit te voeren zou mislukken omdat de brongegevens niet aanwezig zijn.

## Stap 2 – Voeg een nieuw werkblad toe (add new worksheet code)

Nu hebben we een plek nodig om de gekopieerde gegevens te plakken. Hier komt de **add new worksheet code** van pas. Je kunt het blad elke naam geven die je wilt; hier noemen we het `"Copy"`.

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*Pro tip:* Als je van plan bent meerdere bladen te kopiëren, roep `Worksheets.Add` aan binnen een lus en geef elk blad een unieke naam. Zo vermijd je naamconflicten en houd je je workbook overzichtelijk.

## Stap 3 – Definieer het copy cell range

Een **copy cell range** vertelt Aspose.Cells precies welke rijen en kolommen moeten worden gedupliceerd. In veel real‑world scenario's omvat het bereik een draaitabel, dus moeten we nauwkeurig zijn.

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*Waarom we dit nodig hebben:* Door het bereik expliciet op te geven, vermijd je het kopiëren van het hele blad (wat verspilling kan zijn) en garandeer je dat de draaitabel binnen het gekopieerde gebied blijft. Dit is de kern van **how to copy worksheet** wanneer je slechts een deel van het blad nodig hebt.

## Stap 4 – Stel copy options in (preserve copy worksheet pivot table)

Aspose.Cells biedt een `CopyOptions`‑object dat bepaalt wat er wordt geplakt. Om de draaitabel, grafieken en formules te behouden, stellen we `PasteType.All` in en schakelen we `PasteSpecial` in.

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*Uitleg:* `PasteType.All` is de meest inclusieve optie, terwijl `PasteSpecial` de engine vertelt complexe objecten—zoals draaitabellen—correct te behandelen. Het overslaan van deze stap is een veelvoorkomende valkuil; het gekopieerde blad zou zijn interactieve functies verliezen.

## Stap 5 – Kopieer rijen en kolommen (copy columns between sheets)

Nu komt het zware werk: het daadwerkelijk verplaatsen van de gegevens. We gebruiken `CopyRows` en `CopyColumns` om **copy columns between sheets** af te handelen. Beide uitvoeren zorgt ervoor dat samengevoegde cellen en kolombreedtes behouden blijven.

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*Wat er gebeurt:* `CopyRows` verplaatst de gegevens rij voor rij, terwijl `CopyColumns` hetzelfde kolom voor kolom doet. Beide uitvoeren garandeert dat het volledige rechthoekige blok wordt gedupliceerd, wat essentieel is wanneer je **copy columns between sheets** moet uitvoeren die verschillende kolombreedtes of verborgen kolommen hebben.

## Stap 6 – Sla het workbook op

Tot slot schrijf je de wijzigingen terug naar de schijf. Deze stap voltooit het **how to copy worksheet** proces.

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*Verificatietip:* Open `Destination.xlsx` en controleer of het `"Copy"`‑blad er identiek uitziet als het origineel, de draaitabellen functioneel zijn en de kolombreedtes overeenkomen. Als er iets niet klopt, bekijk dan opnieuw de `CopyOptions`‑instellingen.

## Randgevallen & Veelvoorkomende variaties

### Meerdere werkbladen kopiëren

Als je meerdere bladen moet dupliceren, wikkel je de bovenstaande logica in een `foreach`‑lus:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### Formules behouden tussen verschillende workbooks

Wanneer de bron‑ en bestemmings‑workbooks verschillende benoemde bereiken hebben, stel je `copyOptions` in op `PasteType.Formulas` naast `All`:

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### Grote bereiken en prestaties

Voor enorme datasets (honderdduizenden rijen) kun je overwegen alleen `CopyRows` te gebruiken en `CopyColumns` over te slaan als kolombreedtes niet cruciaal zijn. Dit kan enkele seconden schelen.

## Volledig werkend voorbeeld

Hieronder staat het volledige, kant‑klaar programma dat alles omvat wat we hebben besproken. Plak het in een console‑app, pas de bestandspaden aan, en druk op **F5**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**Verwacht resultaat:** Het openen van `Destination.xlsx` toont een blad met de naam **Copy** dat een exacte kopie is van het eerste blad van `Source.xlsx`—inclusief eventuele draaitabellen, opmaak en kolombreedtes. Het originele bestand blijft onaangetast.

## Veelgestelde vragen

**Q: Werkt dit met .xlsx‑bestanden die zijn gemaakt door Excel 2019?**  
A: Absoluut. Aspose.Cells ondersteunt alle moderne Excel‑formaten, dus dezelfde code werkt voor `.xlsx`, `.xlsm` en zelfs oudere `.xls`‑bestanden

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}