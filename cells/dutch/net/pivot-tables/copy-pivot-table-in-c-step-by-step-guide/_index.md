---
category: general
date: 2026-03-18
description: Kopieer draaitabel in C# met Aspose.Cells. Leer hoe je een Excel-bereik
  kopieert, een Excel-draaitabel dupliceert, een bereik naar een nieuw blad kopieert
  en een draaitabel naar een blad kopieert in enkele minuten.
draft: false
keywords:
- copy pivot table
- copy excel range
- duplicate excel pivot
- copy range to new
- copy pivot to sheet
language: nl
og_description: Kopieer draaitabel in C# met Aspose.Cells. Leer hoe je een Excel‑draaitabel
  dupliceert, een Excel‑bereik naar een nieuwe locatie kopieert en een draaitabel
  naar een blad kopieert, met volledige codevoorbeelden.
og_title: Draaitabel kopiëren in C# – Complete programmeergids
tags:
- Aspose.Cells
- C#
- Excel automation
title: Kopieer draaitabel in C# – Stapsgewijze handleiding
url: /nl/net/pivot-tables/copy-pivot-table-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Draaitabel kopiëren in C# – Complete Programmeergids

Heb je ooit een **draaitabel** moeten **kopiëren** van het ene deel van een werkmap naar het andere, maar wist je niet hoe je dat kon doen zonder de onderliggende gegevensverbindingen te verliezen? Je bent niet de enige. Veel ontwikkelaars lopen tegen dit probleem aan bij het automatiseren van Excel‑rapporten, vooral wanneer de draaitabel zich binnen een groter gegevensblok bevindt. Het goede nieuws? Met Aspose.Cells kun je de draaitabel **exact zoals deze verschijnt** kopiëren, en leer je ook hoe je **excelbereik kunt kopiëren**, **excel‑draaitabel kunt dupliceren**, en zelfs **draaitabel naar blad kunt kopiëren** met slechts een paar regels C#.

In deze tutorial lopen we door een real‑world scenario: een draaitabel die zich uitstrekt over *A1:J20* verplaatsen naar een nieuw gebied *M1:V20* in hetzelfde werkblad. Aan het einde heb je een uitvoerbaar programma, begrijp je waarom elke stap belangrijk is, en weet je hoe je de code kunt aanpassen voor andere bereiken of zelfs aparte werkbladen. Geen externe documentatie nodig—alles staat hier.

---

## Vereisten

Voordat we beginnen, zorg dat je het volgende hebt:

- **Aspose.Cells for .NET** (versie 23.9 of later). Je kunt het via NuGet ophalen: `Install-Package Aspose.Cells`.
- Een basis C# ontwikkelomgeving (Visual Studio 2022, Rider, of VS Code met de C# extensie).
- Een Excel‑bestand (`source.xlsx`) dat een draaitabel bevat binnen het bereik *A1:J20*.

Dat is alles. Als je comfortabel bent met het maken van een console‑applicatie, ben je klaar om te starten.

---

## Hoe een draaitabel kopiëren in Aspose.Cells

De kern van de oplossing is één enkele aanroep van `Worksheet.Cells.CopyRange`. Deze methode kopieert niet alleen ruwe celwaarden, maar behoudt ook draaitabellen, grafieken en andere rijke objecten automatisch. Laten we het stap voor stap bekijken.

### Stap 1: Laad de bronwerkmap

Eerst moeten we de werkmap in het geheugen laden.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Waarom dit belangrijk is:** Het laden van de werkmap creëert een in‑memory representatie die Aspose.Cells kan manipuleren zonder Excel te starten. Het is snel, thread‑safe en werkt op servers.

### Stap 2: Haal het eerste werkblad op

De meeste voorbeelden gebruiken het eerste blad, maar je kunt elk index of naam targeten.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = sourceWorkbook.Worksheets[0];
```

> **Tip:** Als je **draaitabel naar blad** wilt kopiëren in plaats van naar hetzelfde blad, wijzig dan simpelweg de `worksheet`‑referentie naar een ander `Worksheet`‑object.

### Stap 3: Definieer de bron‑ en doelbereiken

We gebruiken `CellArea`‑structuren om de blokken die we verplaatsen te beschrijven.

```csharp
        // Define the source range (A1:J20) that contains the pivot table
        CellArea sourceRange = new CellArea(0, 0, 19, 9);   // rows 0‑19, columns 0‑9

        // Define the target range (M1:V20) where the data will be copied
        CellArea targetRange = new CellArea(0, 12, 19, 21); // rows 0‑19, columns 12‑21
```

> **Uitleg:** Rij‑ en kolomindices zijn nul‑gebaseerd. Kolom 0 = **A**, kolom 12 = **M**, enzovoort. Pas deze getallen aan als je draaitabel zich elders bevindt.

### Stap 4: Voer de kopieerbewerking uit

Nu gebeurt de magie. Het instellen van de laatste boolean‑parameter op `true` vertelt Aspose.Cells om alle objecten te kopiëren — inclusief de draaitabel.

```csharp
        // Copy the source range to the target range; pivot tables are copied automatically
        worksheet.Cells.CopyRange(
            sourceRange.StartRow, sourceRange.StartColumn,
            sourceRange.EndRow, sourceRange.EndColumn,
            targetRange.StartRow, targetRange.StartColumn,
            true);
```

> **Waarom `true`?** De vlag geeft aan “kopieer alle objecten”. Als je `false` instelt, worden alleen platte celwaarden verplaatst en gaat de draaitabel verloren.

### Stap 5: Sla de werkmap op

Tot slot schrijven we de gewijzigde werkmap terug naar schijf.

```csharp
        // Save the workbook with the copied range
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copy-pivot.xlsx");
    }
}
```

> **Resultaat:** `copy-pivot.xlsx` bevat nu de originele draaitabel op *A1:J20* **en** een identieke kopie op *M1:V20*. Open het bestand in Excel om te verifiëren dat beide draaitabellen functioneel zijn en hun gegevensverbindingen behouden.

---

## Excel‑bereik naar een nieuwe locatie kopiëren – een snelle variatie

Soms hoef je alleen **excelbereik** te **kopiëren** zonder je zorgen te maken over draaitabellen. Dezelfde `CopyRange`‑methode doet het werk; stel gewoon het laatste argument in op `false`.

```csharp
worksheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    false); // plain values only
```

> **Wanneer te gebruiken:** Als je ruwe data verplaatst naar een tijdelijk berekeningsblad, bespaart het uitschakelen van objectkopie geheugen en versnelt het de bewerking.

---

## Excel‑draaitabel dupliceren over meerdere bladen

Wat als je een **excel‑draaitabel** wilt **dupliceren** op een ander werkblad? Het patroon blijft hetzelfde; je verwijst alleen naar een ander `Worksheet` voor de bestemming.

```csharp
// Assume we have a second sheet already created
Worksheet destSheet = sourceWorkbook.Worksheets.Add("PivotCopy");

// Copy the pivot (and its data source) to the new sheet starting at A1
destSheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    0, 0, // destination at A1
    true);
```

> **Randgeval:** Als de bron‑draaitabel een tabel gebruikt die op het oorspronkelijke blad staat, zal Aspose.Cells ook de onderliggende tabeldefinitie kopiëren, zodat de nieuwe draaitabel direct werkt.

---

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Valkuil | Waarom het gebeurt | Oplossing |
|---------|--------------------|-----------|
| **Draaitabel verliest zijn cache** | Gebruik van `CopyRange` met `false` of een aangepaste kopie‑routine die objecten negeert. | Geef altijd `true` door wanneer je de draaitabel zelf nodig hebt. |
| **Doelcellen bevatten al gegevens** | Overschrijft stilletjes, waardoor bestaande formules mogelijk corrupt raken. | Wis eerst het doelgebied: `worksheet.Cells.ClearRange(targetRange.StartRow, targetRange.StartColumn, targetRange.EndRow, targetRange.EndColumn, true);` |
| **Bronbereik omvat niet de volledige draaitabel** | Draaitabellen beslaan meer rijen/kolommen dan je verwacht (bijv. verborgen rijen). | Gebruik `worksheet.PivotTables[0].DataRange` om programmatically de exacte grenzen op te halen. |
| **Kopiëren tussen werkmappen** | `CopyRange` werkt alleen binnen dezelfde werkmap. | Gebruik `sourceWorksheet.Cells.CopyRange` naar een tijdelijk bereik, daarna `destWorkbook.Worksheets.AddCopy(sourceWorksheet);` |

---

## Verwachte output & verificatie

Na het uitvoeren van het programma:

1. Open `copy-pivot.xlsx`.
2. Je ziet twee identieke draaitabellen — één op **A1:J20**, een andere op **M1:V20**.
3. Vernieuw een willekeurige draaitabel; beide moeten dezelfde onderliggende data weergeven.
4. Als je naar een ander blad hebt gedupliceerd, bevat het nieuwe blad ook een functionele kopie.

Een snelle manier om via code te verifiëren:

```csharp
int pivotCount = worksheet.PivotTables.Count; // should be 2 after copy
Console.WriteLine($"Pivot tables on the sheet: {pivotCount}");
```

---

## Pro tip: Bereikdetectie automatiseren

Hard‑coderen van `CellArea` werkt voor statische rapporten, maar productcode moet vaak de draaitabel dynamisch lokaliseren.

```csharp
// Find the first pivot table on the sheet
PivotTable pt = worksheet.PivotTables[0];
CellArea ptRange = pt.DataRange;

// Use the detected range for copying
worksheet.Cells.CopyRange(
    ptRange.StartRow, ptRange.StartColumn,
    ptRange.EndRow, ptRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    true);
```

> **Waarom het de moeite waard is:** Dit maakt je oplossing bestand tegen lay‑out wijzigingen — geen “Oeps, de draaitabel is naar B2 verplaatst” meer.

---

![copy pivot table example](copy-pivot.png){alt="voorbeeld van gekopieerde draaitabel"}

*De screenshot (placeholder) toont de originele draaitabel links en de gedupliceerde rechts.*

---

## Samenvatting

We hebben net behandeld hoe je **draaitabel** kunt **kopiëren** in C# met Aspose.Cells, manieren onderzocht om **excelbereik** te **kopiëren**, **excel‑draaitabel** te **dupliceren**, en zelfs **draaitabel naar blad** te **kopiëren** over werkbladen. De belangrijkste punten zijn:

- Gebruik `Worksheet.Cells.CopyRange` met de `true`‑vlag om rijke objecten te behouden.
- Definieer bron‑ en doel‑`CellArea`‑objecten met nul‑gebaseerde indices.
- Pas het bestemmings‑werkblad aan als je **draaitabel naar blad** wilt kopiëren.
- Let op randgevallen zoals bestaande data, verborgen rijen en scenario’s waarbij je tussen werkmappen kopieert.

---

## Wat is het vervolg?

- **Dynamische draaitabeldetectie**: Bouw een helper die een werkmap scant op alle draaitabellen en ze automatisch repliceert.
- **Exporteren naar PDF/HTML**: Na het kopiëren wil je het blad misschien renderen naar een rapportformaat — Aspose.Cells ondersteunt dat ook.
- **Prestatie‑optimalisatie**: Voor enorme werkmappen kun je overwegen de berekening uit te schakelen vóór het kopiëren en daarna weer in te schakelen.

Voel je vrij om te experimenteren: wijzig de doelcoördinaten, kopieer naar een gloednieuwe werkmap, of loop over meerdere werkbladen om een geconsolideerd rapport te maken. De mogelijkheden zijn eindeloos, en met de basis die je nu hebt, kun je de code aanpassen aan vrijwel elke Excel‑automatiseringstaak.

Happy coding, en moge je draaitabellen altijd perfect gesynchroniseerd blijven!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}