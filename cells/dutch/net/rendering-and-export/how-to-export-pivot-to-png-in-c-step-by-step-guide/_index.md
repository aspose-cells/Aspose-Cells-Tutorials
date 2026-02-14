---
category: general
date: 2026-02-14
description: hoe je een draaitabel uit een Excel-werkmap exporteert naar PNG met Aspose.Cells.
  Leer hoe je een Excel-werkmap laadt, een draaitabel rendert naar een afbeelding
  en de afbeelding van de draaitabel moeiteloos opslaat.
draft: false
keywords:
- how to export pivot
- export excel pivot
- load excel workbook
- pivot table to png
- save pivot image
language: nl
og_description: hoe je een draaitabel vanuit Excel naar PNG exporteert in C#. Deze
  gids laat zien hoe je een Excel‑werkmap laadt, een draaitabel rendert naar PNG en
  de draaitabelafbeelding opslaat.
og_title: hoe pivot exporteren naar png in C# – volledige tutorial
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hoe je een pivot exporteert naar PNG in C# – Stapsgewijze handleiding
url: /nl/net/rendering-and-export/how-to-export-pivot-to-png-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hoe pivot exporteren naar PNG in C# – Complete Tutorial

Heb je je ooit afgevraagd **how to export pivot** uit een Excel‑sheet als een scherpe PNG‑file? Je bent niet de enige—developers hebben vaak een snelle visual van een pivot‑tabel nodig voor rapporten, dashboards of e‑mailbijlagen. Het goede nieuws? Met Aspose.Cells kun je de Excel‑workbook laden, de eerste pivot‑tabel pakken, omzetten naar een afbeelding, en **save pivot image** in slechts een paar regels C#.

In deze tutorial lopen we alles door wat je nodig hebt: van de basis van **load excel workbook**, tot het renderen van een **pivot table to png**, en uiteindelijk het bestand op schijf opslaan. Aan het einde heb je een zelf‑containend, uitvoerbaar programma dat je in elk .NET‑project kunt plaatsen.

---

## Wat je nodig hebt

- **.NET 6 of later** (de code werkt ook op .NET Framework 4.7+)
- **Aspose.Cells for .NET** NuGet‑pakket (versie 23.12 op het moment van schrijven)
- Een Excel‑bestand (`input.xlsx`) dat minstens één draaitabel bevat
- Een Visual Studio‑ of VS Code‑omgeving waar je je prettig in voelt

Geen extra bibliotheken, geen COM‑interop en geen Excel‑installatie vereist—Aspose.Cells regelt alles in het geheugen.

---

## Stap 1 – Laad de Excel‑werkmap

Het eerste is om de werkmap in het geheugen te laden. Hier komt het **load excel workbook**‑trefwoord van pas.

```csharp
using System.Drawing;
using Aspose.Cells;

class PivotExport
{
    static void Main()
    {
        // Step 1: Load the workbook from disk
        // Adjust the path to where your input.xlsx lives
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // Grab the first worksheet (you can also select by name)
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Waarom dit belangrijk is:**  
> Het één keer laden van de werkmap houdt de bewerking snel en voorkomt dat het bronbestand wordt vergrendeld. Aspose.Cells leest het bestand in een beheerde stream, zodat je later zelfs kunt laden vanuit een byte‑array of een netwerklocatie.

---

## Stap 2 – Render de Pivot Table naar een afbeelding

Nu de werkmap in het geheugen staat, kunnen we de draaitabellen benaderen. De API biedt een handige `ToImage()`‑methode die een `System.Drawing.Image` retourneert.

```csharp
        // Step 2: Find the first pivot table on the worksheet
        if (worksheet.PivotTables.Count == 0)
        {
            System.Console.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }

        // Export the first pivot table as an image
        Image pivotImage = worksheet.PivotTables[0].ToImage();

        // Optional: tweak image quality or size here
        // pivotImage.SetResolution(300, 300);
```

> **Pro tip:** Als je werkmap meerdere draaitabellen bevat, loop dan eenvoudig over `worksheet.PivotTables` en exporteer elke tabel. De `ToImage()`‑aanroep respecteert de huidige weergave (filters, slicers, enz.), zodat je precies krijgt wat de gebruiker ziet.

---

## Stap 3 – Sla het gegenereerde PNG‑bestand op

Tot slot slaan we de bitmap op schijf op. De `Save`‑overload kiest automatisch het formaat op basis van de bestandsextensie.

```csharp
        // Step 3: Save the image as PNG
        var outputPath = @"YOUR_DIRECTORY\pivot.png";
        pivotImage.Save(outputPath, System.Drawing.Imaging.ImageFormat.Png);

        System.Console.WriteLine($"Pivot table exported successfully to {outputPath}");
    }
}
```

Het uitvoeren van het programma genereert een `pivot.png` die er precies uitziet als de draaitabel in Excel. Open het met een willekeurige afbeeldingsviewer en je ziet rijen, kolommen en totalen pixel‑perfect gerenderd.

---

## Veelvoorkomende randgevallen behandelen

### Meerdere werkbladen of draaitabellen

Als je werkmap de draaitabel op een ander blad opslaat, wijzig dan de werkblad‑index of gebruik de bladnaam:

```csharp
Worksheet ws = workbook.Worksheets["SalesData"];
```

Vervolgens loop:

```csharp
foreach (PivotTable pt in ws.PivotTables)
{
    Image img = pt.ToImage();
    img.Save($"pivot_{pt.Name}.png", ImageFormat.Png);
}
```

### Grote draaitabellen

Voor zeer grote draaitabellen kan de standaardafbeeldingsgrootte enorm zijn. Je kunt de rendergrootte regelen door de zoomfactor van het werkblad aan te passen vóór het aanroepen van `ToImage()`:

```csharp
worksheet.PageSetup.Zoom = 75; // renders at 75 % of original size
```

### Geheugenbeheer

`System.Drawing.Image` implementeert `IDisposable`. In productiecodel moet je de afbeelding in een `using`‑blok plaatsen om native resources tijdig vrij te geven:

```csharp
using (Image pivotImage = worksheet.PivotTables[0].ToImage())
{
    pivotImage.Save(outputPath, ImageFormat.Png);
}
```

---

## Volledig werkend voorbeeld

Hieronder staat het volledige, kant‑klaar programma. Plak het in een nieuw console‑project, pas de bestands‑paden aan, en druk op **F5**.

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;

namespace PivotExportDemo
{
    class Program
    {
        static void Main()
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook (load excel workbook)
            // -----------------------------------------------------------------
            string inputFile = @"YOUR_DIRECTORY\input.xlsx";
            Workbook wb = new Workbook(inputFile);
            Worksheet ws = wb.Worksheets[0]; // first worksheet

            // -----------------------------------------------------------------
            // 2️⃣ Ensure a pivot table exists and export it (how to export pivot)
            // -----------------------------------------------------------------
            if (ws.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found. Exiting.");
                return;
            }

            // Export the first pivot table as a PNG image (pivot table to png)
            using (Image img = ws.PivotTables[0].ToImage())
            {
                // -----------------------------------------------------------------
                // 3️⃣ Save the pivot image to disk (save pivot image)
                // -----------------------------------------------------------------
                string outputFile = @"YOUR_DIRECTORY\pivot.png";
                img.Save(outputFile, ImageFormat.Png);
                Console.WriteLine($"Pivot exported successfully → {outputFile}");
            }
        }
    }
}
```

**Verwachte output:**  
```
Pivot exported successfully → YOUR_DIRECTORY\pivot.png
```

En het bestand `pivot.png` zal een visuele replica van de oorspronkelijke draaitabel bevatten.

---

## Veelgestelde vragen

- **Werkt dit met .xlsx‑bestanden die grafieken bevatten?**  
  Ja. De `ToImage()`‑methode houdt alleen rekening met de lay‑out van de draaitabel; grafieken blijven onaangetast.

- **Kan ik exporteren naar JPEG of BMP in plaats van PNG?**  
  Absoluut—verander gewoon het `ImageFormat`‑argument in `Save`. PNG is verliesloos, daarom raden we het aan voor scherpe data.

- **Wat als de werkmap met een wachtwoord is beveiligd?**  
  Laad deze met de wachtwoord‑overload:  
  `Workbook wb = new Workbook(inputFile, new LoadOptions { Password = "mySecret" });`

---

## Afronding

We hebben zojuist **how to export pivot** vanuit een Excel‑bestand naar een PNG‑afbeelding met Aspose.Cells behandeld. De stappen—**load excel workbook**, locate the **pivot table to png**, en **save pivot image**—zijn eenvoudig, maar krachtig genoeg voor real‑world rapportage‑pijplijnen. 

Vervolgens kun je verkennen:

- Het automatiseren van de export voor alle draaitabellen in een map (export excel pivot in bulk)  
- Het insluiten van de PNG in een PDF of HTML‑e‑mail (combineer met iTextSharp of Razor)  
- Het toevoegen van watermerken of aangepaste styling aan de geëxporteerde afbeelding  

Probeer het eens en laat de afbeeldingen spreken in je volgende dashboard.

---

![voorbeeldoutput van hoe pivot exporteren](assets/pivot-export-example.png "voorbeeldoutput van hoe pivot exporteren")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}