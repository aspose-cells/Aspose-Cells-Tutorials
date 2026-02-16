---
category: general
date: 2026-02-15
description: Maak een nieuw werkboek in C# en kopieer een draaitabel zonder de definitie
  te verliezen. Leer hoe je rijen kunt kopiëren, de draaitabel behoudt en een draaitabel
  eenvoudig dupliceert.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- duplicate pivot table
language: nl
og_description: Maak een nieuwe werkmap in C# en kopieer een draaitabel terwijl je
  de definitie behoudt. Stapsgewijze handleiding voor ontwikkelaars.
og_title: Nieuw werkboek maken in C# – Draaitabel behouden
tags:
- Aspose.Cells
- C#
- Excel automation
title: Maak een nieuw werkboek in C# – Behoud draaitabel
url: /nl/net/pivot-tables/create-new-workbook-in-c-preserve-pivot-table/
---

-button >}}

Make sure we keep them.

Now ensure we didn't miss any markdown formatting.

Check bullet lists: we used "*Why this matters:*" originally "*Why this matters:*". Should translate "*Waarom dit belangrijk is:*". Keep same bullet formatting.

Make sure we keep code block placeholders unchanged.

Now produce final output with all translated content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nieuwe Werkmap Maken in C# – Pivot‑tabel Behouden

Heb je ooit moeten **create new workbook** in C# die een exacte kopie van een pivot‑tabel uit een ander bestand bevat? Je bent niet de enige. In veel rapportage‑pijplijnen is de pivot‑tabel het hart van de analyse, en het verliezen van de definitie ervan wanneer je data verplaatst is een nachtmerrie.

Het goede nieuws? Met een paar regels Aspose.Cells‑code kun je rijen—incl. de pivot‑tabel—kopiëren naar een nieuwe werkmap en alles intact houden. Hieronder zie je **how to copy rows**, **preserve pivot table** instellingen, en zelfs **duplicate pivot table** over bestanden heen zonder formules of cache te breken.

## Wat Deze Tutorial Behandelt

In deze gids lopen we door:

1. Het laden van de bron‑werkmap die al een pivot‑tabel bevat.  
2. **Create new workbook** objecten voor de bestemming.  
3. Het gebruiken van `CopyRows` om het bereik dat de pivot‑tabel bevat over te dragen.  
4. Het opslaan van het resultaat terwijl je ervoor zorgt dat de pivot‑tabel functioneel blijft.  

Geen externe documentatie nodig—alleen de code, de reden, en een handvol praktische tips die je rechtstreeks in je project kunt plakken.

> **Pro tip:** Aspose.Cells werkt met .NET Core, .NET Framework en zelfs Xamarin, dus dezelfde snippet draait waar je hem ook nodig hebt.

![Nieuwe werkmap maken met gekopieerde pivot‑tabel](/images/create-new-workbook-pivot.png "nieuwe werkmap maken met gekopieerde pivot‑tabel")

## Stap 1 – Nieuwe Werkmap Maken en het Bronbestand Laden

Het eerste wat we doen is **create new workbook** objecten maken. Eén bevat de oorspronkelijke data, de andere ontvangt het gekopieerde bereik.

```csharp
using Aspose.Cells;

// Load the source workbook that already contains a pivot table
var sourceWorkbook = new Workbook(@"C:\Data\source.xlsx");

// Create an empty workbook that will become the destination
var destinationWorkbook = new Workbook();
```

*Waarom dit belangrijk is:*  
`Workbook` is het toegangspunt voor elke Excel‑manipulatie in Aspose.Cells. Door een nieuwe werkmap te instantieren garanderen we een schone lei—geen verborgen stijlen of vreemde werkbladen die later kunnen interfereren.

## Stap 2 – Rijen Kopiëren Inclusief een Pivot‑tabel

Nu komt de kern van het probleem: **how to copy rows** die de pivot‑tabel omvatten zonder deze plat te maken. De `CopyRows`‑methode doet precies dat.

```csharp
// Copy the first 20 rows (adjust as needed) from the source to the destination
// Parameters: startRow, totalRows, targetCells, targetStartRow
sourceWorkbook.Worksheets[0].Cells.CopyRows(
    startRow: 0,
    totalRows: 20,
    targetCells: destinationWorkbook.Worksheets[0].Cells,
    targetStartRow: 0);
```

Een paar dingen om op te merken:

* `startRow` en `totalRows` definiëren het blok dat de pivot‑tabel bevat.  
* De methode kopieert **both** ruwe data en de pivot‑cache, zodat de bestemmings‑werkmap weet hoe de pivot‑tabel on‑the‑fly opnieuw opgebouwd moet worden.  
* Als je pivot dieper in het blad begint, wijzig dan gewoon de indices—geen andere API‑aanroep nodig.

> **Veelgestelde vraag:** *Verliest de gekopieerde pivot zijn bron‑dataverwijzing?*  
> Nee. Aspose.Cells embedde de cache direct in het werkblad, zodat de pivot zelf‑voorzienend wordt in het nieuwe bestand.

## Stap 3 – Pivot‑tabel Behouden bij het Opslaan van de Bestemming

Nadat de rijen zijn gekopieerd, leeft de pivot‑tabel in de bestemmings‑werkmap precies zoals in de bron. Het bestand opslaan is eenvoudig.

```csharp
// Save the destination workbook; the pivot table remains functional
destinationWorkbook.Save(@"C:\Data\destination.xlsx");
```

Wanneer je `destination.xlsx` in Excel opent, zie je de pivot‑tabel klaar om te verversen. Het **preserve pivot table** gedrag is automatisch omdat de cache met de rijen meereist.

### Het Resultaat Verifiëren

Open het bestand en:

1. Klik op de pivot‑tabel.  
2. Merk op dat de veldlijst verschijnt—dit betekent dat de cache intact is.  
3. Probeer een verversing; de data wordt bijgewerkt zonder fouten.

Als je een *#REF!*‑fout tegenkomt, controleer dan dubbel of het gekopieerde bereik de verborgen cache‑rijen bevat (meestal direct na de zichtbare data).

## Stap 4 – Pivot‑tabel Dupliceren naar Meerdere Werkmappen (Optioneel)

Soms heb je dezelfde pivot nodig in meerdere rapporten. Het patroon dat we net gebruikten schaalt goed—herhaal gewoon de kopie voor elke nieuwe werkmap.

```csharp
string[] targets = {
    @"C:\Reports\Q1.xlsx",
    @"C:\Reports\Q2.xlsx",
    @"C:\Reports\Q3.xlsx"
};

foreach (var path in targets)
{
    var wb = new Workbook(); // fresh workbook each loop
    sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 20, wb.Worksheets[0].Cells, 0);
    wb.Save(path);
}
```

Deze snippet **duplicates pivot table** drie keer met één lus. Pas de `targets`‑array aan om overeen te komen met je rapportageschema.

### Randgevallen om in Gedachten te Houden

| Situation | What to Watch For | Fix |
|-----------|-------------------|-----|
| Pivot uses external data source | Cache may reference a connection that doesn’t exist on the new machine | Embed the data source or recreate the connection in the destination workbook |
| Very large pivot ( > 100 k rows ) | `CopyRows` can be memory‑intensive | Use `CopyRows` in chunks or consider `Copy` with `PasteOptions` to limit memory usage |
| Worksheet has hidden rows/columns | Hidden cache rows might be skipped if you copy only visible rows | Always copy the exact row range that contains the cache, not just the visible area |

## Volledig Werkend Voorbeeld

Alles samengevoegd, hier is een zelf‑containend programma dat je in een console‑app kunt plaatsen.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook (contains the original pivot)
            var sourcePath = @"C:\Data\source.xlsx";
            var sourceWorkbook = new Workbook(sourcePath);

            // 2️⃣ Prepare destination workbook
            var destinationWorkbook = new Workbook();

            // 3️⃣ Copy rows that include the pivot (adjust range as needed)
            sourceWorkbook.Worksheets[0].Cells.CopyRows(
                startRow: 0,
                totalRows: 20,
                targetCells: destinationWorkbook.Worksheets[0].Cells,
                targetStartRow: 0);

            // 4️⃣ Save – the pivot table is preserved
            var destPath = @"C:\Data\destination.xlsx";
            destinationWorkbook.Save(destPath);

            Console.WriteLine("Pivot table successfully copied!");
        }
    }
}
```

Voer het programma uit, open `destination.xlsx`, en je ziet dezelfde pivot‑tabel klaar om je data te slicen en te dicing. Handmatige recreatie is niet nodig.

---

## Conclusie

We hebben zojuist laten zien hoe je **create new workbook** in C# kunt **copy pivot table** terwijl je elke instelling behoudt. Door `CopyRows` te gebruiken krijg je een betrouwbare manier om **preserve pivot table** functionaliteit te behouden, de eeuwenoude “**how to copy rows**” vraag te beantwoorden, en zelfs **duplicate pivot table** over meerdere rapporten te verspreiden met minimale code.

Volgende stappen? Probeer het gekopieerde bereik aan te passen zodat het grafieken omvat die naar dezelfde pivot verwijzen, of experimenteer met `PasteOptions` om opmaak exact te behouden. Hetzelfde patroon werkt voor andere Aspose.Cells‑objecten zoals tabellen en benoemde bereiken, dus voel je vrij om het uit te breiden.

Heb je een uitdaging waar je mee worstelt—misschien een pivot die data uit een externe DB haalt, of een werkmap die in de cloud staat? Laat een reactie achter hieronder, en we pakken het samen aan. Veel plezier met coderen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}