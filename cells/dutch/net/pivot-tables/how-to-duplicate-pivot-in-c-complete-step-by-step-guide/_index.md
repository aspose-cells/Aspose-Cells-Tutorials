---
category: general
date: 2026-03-22
description: Leer hoe je een draaitabel dupliceert in C# met Aspose.Cells. Deze gids
  laat ook zien hoe je rijen kopieert en een Excel-werkmap laadt in C# voor naadloze
  Excel-automatisering en het kopiëren van rijen.
draft: false
keywords:
- how to duplicate pivot
- how to copy rows
- load excel workbook c#
- excel automation copy rows
language: nl
og_description: Hoe dupliceer je een pivot in C#? Volg deze beknopte tutorial om een
  Excel-werkboek te laden in C#, rijen te kopiëren en de master Excel-automatisering
  voor het kopiëren van rijen te beheersen.
og_title: Hoe een Pivot te dupliceren in C# – Complete gids
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Hoe een Pivot te dupliceren in C# – Complete stapsgewijze handleiding
url: /nl/net/pivot-tables/how-to-duplicate-pivot-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een draaitabel te dupliceren in C# – Complete stapsgewijze gids

Heb je je ooit afgevraagd **hoe je een draaitabel** programmatically kunt dupliceren zonder ze handmatig te slepen in Excel? Je bent niet de enige. In veel rapportage‑pipelines is dezelfde draaitabel‑lay‑out nodig op een nieuwe set rijen, en dit handmatig doen is tijdverspilling.  

Het goede nieuws? Met een paar regels C# kun je een Excel‑werkmap laden, het gebied definiëren dat de draaitabel bevat, en **hoe je rijen kopieert** zodat de draaitabel op een nieuwe locatie verschijnt – allemaal in één geautomatiseerde run. In deze tutorial behandelen we ook de basis van **load excel workbook c#** en geven we je een solide basis voor **excel automation copy rows** taken.

> **Wat je zult leren**  
> • Een volledig, uitvoerbaar voorbeeld dat een draaitabel dupliceert.  
> • Een uitleg waarom elke regel belangrijk is.  
> • Tips voor het omgaan met randgevallen zoals verborgen werkbladen of meerdere draaitabellen.

---

## Vereisten

Voordat we beginnen, zorg dat je het volgende hebt:

- **.NET 6.0** (of een recente .NET‑versie) geïnstalleerd.  
- **Aspose.Cells for .NET** – de bibliotheek die we gebruiken om Excel‑bestanden te manipuleren. Je kunt deze via NuGet ophalen:  

```bash
dotnet add package Aspose.Cells
```  

- Een bron‑werkmap (`Source.xlsx`) die al een draaitabel bevat in het bereik **A1:J20** (het bereik dat we gaan dupliceren).  
- Basiskennis van C#‑syntaxis – niets bijzonders, alleen de gebruikelijke `using`‑statements en de `Main`‑methode.

Als een van deze onderdelen onbekend is, pauzeer even en installeer het pakket; de rest van de gids gaat ervan uit dat de bibliotheek klaar is voor gebruik.

---

![Illustratie van hoe je een draaitabel dupliceert in C# met Aspose.Cells](https://example.com/duplicate-pivot.png "illustratie van hoe je een draaitabel dupliceert in C#")

*Afbeeldings‑alt‑tekst: "voorbeeld van hoe je een draaitabel dupliceert in C# met bron‑ en gedupliceerde draaitabel‑rijen".*

---

## Stap 1: Load Excel Workbook C# – Het bestand openen

Het allereerste wat je moet doen wanneer je **load excel workbook c#** wilt, is een `Workbook`‑instance maken die naar je bestand wijst. Dit object geeft je toegang tot elk werkblad, elke cel en elke draaitabel in het bestand.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Load the source workbook
        string sourcePath = @"C:\Data\Source.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // From here on we can work with worksheets, ranges, and pivots.
```

**Waarom dit belangrijk is:**  
`Workbook` abstraheert het volledige Excel‑bestand naar een in‑memory model. Zonder het eerst te laden kun je de locatie van de draaitabel niet inspecteren of rijen kopiëren. Bovendien detecteert de constructor automatisch het bestandsformaat (XLS, XLSX, CSV, enz.), zodat je geen extra code nodig hebt voor formatdetectie.

---

## Stap 2: How to Copy Rows – Het draaitabel‑gebied definiëren

Nu de werkmap in het geheugen staat, moeten we Aspose.Cells vertellen welke rijen de draaitabel bevatten. In ons voorbeeld bevindt de draaitabel zich in **A1:J20**, wat overeenkomt met rijen **0‑19** (nul‑gebaseerde indexering). We verpakken dat in een `CellArea`‑structuur.

```csharp
        // Step 2: Define the cell area that contains the pivot table (A1:J20)
        // Row indices are zero‑based, column indices are also zero‑based.
        CellArea copyRange = new CellArea(startRow: 0, startColumn: 0, endRow: 19, endColumn: 9);
```

**Waarom we `CellArea` gebruiken:**  
Het is een lichte manier om een rechthoekig blok te beschrijven. Wanneer je later `CopyRows` aanroept, leest de methode dit object om precies te weten welke rijen moeten worden gedupliceerd. Als je ooit het bereik moet aanpassen (bijvoorbeeld als de draaitabel groeit naar kolom K), wijzig je alleen de `endColumn`‑waarde.

---

## Stap 3: Toegang tot het doel‑werkblad

De meeste werkmappen hebben één blad, maar de API werkt hetzelfde voor meerdere bladen. Haal het eerste werkblad op (index 0) – daar bevindt zich de originele draaitabel.

```csharp
        // Step 3: Get the first worksheet from the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Pro‑tip:**  
Als je werkbladen namen heeft, kun je ze ook op naam ophalen: `workbook.Worksheets["Sheet1"]`. Dit helpt hard‑codering van indices te vermijden wanneer de structuur van de werkmap verandert.

---

## Stap 4: How to Copy Rows – De draaitabel dupliceren

Hier is het hart van **how to duplicate pivot**: we kopiëren de rijen die de draaitabel bevatten naar een nieuwe locatie. In ons geval beginnen we bij rij 31 (nul‑gebaseerde index 30). De `CopyRows`‑methode kopieert *zowel* de data als de onderliggende draaitabel‑cache, zodat de nieuwe rijen zich exact hetzelfde gedragen als de originele.

```csharp
        // Step 4: Copy the rows of the defined range to a new location (starting at row 31)
        // The third argument is the destination start row (zero‑based).
        worksheet.Cells.CopyRows(copyRange.StartRow, copyRange.EndRow, destinationRow: 30);
```

**Wat er onder de motorkap gebeurt:**  
`CopyRows` kloont elke rij, waarbij formules, stijlen en draaitabeldefinities behouden blijven. Omdat de cache van de draaitabel op werkmapniveau leeft, verwijst de gedupliceerde draaitabel automatisch naar dezelfde gegevensbron – geen extra configuratie nodig.

**Randgeval – verborgen rijen:**  
Als een van de rijen in het bronbereik verborgen is, blijven ze verborgen na het kopiëren. Wil je ze zichtbaar maken, roep dan `worksheet.Rows[destRow].IsHidden = false` aan na de kopie.

---

## Stap 5: Werkmap opslaan – Het duplicaat verifiëren

Tot slot schrijf je de wijzigingen terug naar schijf. Je kunt het originele bestand overschrijven of, veiliger, opslaan onder een nieuwe naam zodat je het voor‑ en na‑resultaat kunt vergelijken.

```csharp
        // Step 5: Save the workbook – the pivot table is now duplicated in the new rows
        string outputPath = @"C:\Data\CopyWithPivot.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine("Pivot duplicated successfully! Check " + outputPath);
    }
}
```

**Resultaat dat je moet zien:**  
Open `CopyWithPivot.xlsx`. Je vindt de originele draaitabel in **A1:J20** en een identieke kopie beginnend bij **A31:J50**. Beide draaitabellen kunnen onafhankelijk worden vernieuwd, en eventuele slicers die aan de originele zijn gekoppeld, werken nog steeds voor de kopie omdat ze dezelfde cache delen.

---

## Veelgestelde vragen & Variaties

### Kan ik meerdere draaitabellen tegelijk dupliceren?

Zeker. Loop door alle draaitabellen (`worksheet.PivotTables`) en kopieer elk bereik naar een andere bestemming. Zorg er alleen voor dat de bestemmingsbereiken elkaar niet overlappen.

### Wat als de bron‑werkmap met een wachtwoord is beveiligd?

Aspose.Cells laat je een beveiligd bestand openen door het wachtwoord mee te geven aan de `Workbook`‑constructor:

```csharp
Workbook workbook = new Workbook(sourcePath, new LoadOptions { Password = "mySecret" });
```

### Hoe kopieer ik rijen zonder formules te beïnvloeden?

Als je alleen de *waarden* nodig hebt (geen formules), gebruik dan `CopyRows` met de `CopyOptions`‑vlag:

```csharp
worksheet.Cells.CopyRows(sourceStart, sourceEnd, destStart, new CopyOptions { CopyValues = true });
```

### Is er een manier om rijen naar een *ander* werkmap te kopiëren?

Ja. Na het kopiëren van rijen in het bronblad kun je het werkblad klonen naar een andere `Workbook`‑instance via `targetWorkbook.Worksheets.AddCopy(worksheet)`.

---

## Pro‑tips voor betrouwbare Excel‑automatisering Copy Rows

- **Valideer het bereik** vóór het kopiëren. Een snelle `if (copyRange.EndRow >= worksheet.Cells.MaxDataRow)` voorkomt out‑of‑range‑fouten.  
- **Schakel berekeningen uit** tijdens het kopiëren van grote bereiken: `workbook.Settings.CalcMode = CalcMode.Manual;` – dit versnelt de operatie aanzienlijk.  
- **Dispose objecten** (`workbook.Dispose()`) als je veel bestanden in een lus verwerkt om native resources vrij te maken.  
- **Log de operatie** – vooral in productiepijplijnen – zodat je kunt traceren welke bestanden zijn verwerkt en fouten vroegtijdig kunt opvangen.

---

## Conclusie

Je weet nu **hoe je een draaitabel** dupliceert in C# met Aspose.Cells, en je hebt de volledige workflow gezien van **load excel workbook c#** tot **excel automation copy rows** en uiteindelijk het opslaan van het resultaat. Het voorbeeld is zelf‑voorzienend, werkt direct uit de doos, en kan worden uitgebreid om meerdere draaitabellen, beveiligde bestanden of cross‑workbook‑kopieën te behandelen.

Volgende stappen? Probeer het script aan te passen om:

- De gedupliceerde draaitabel programmatically te vernieuwen (`pivotTable.RefreshData();`).  
- Het gedupliceerde gebied naar een CSV te exporteren voor downstream verwerking.  
- De code te integreren in een ASP.NET Core API zodat gebruikers een bestand kunnen uploaden en direct een versie met gedupliceerde draaitabel ontvangen.

Happy coding, en moge je Excel‑automatisering altijd soepel verlopen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}