---
category: general
date: 2026-03-01
description: Hoe je een pivot snel en betrouwbaar opslaat. Leer hoe je een pivot exporteert,
  een pivot‑afbeelding exporteert en een bereik naar afbeelding converteert in slechts
  een paar regels C#.
draft: false
keywords:
- how to save pivot
- how to export pivot
- export pivot image
- convert range to image
language: nl
og_description: Hoe je een pivot in C# in seconden opslaat. Volg deze gids om een
  pivot te exporteren, een pivot‑afbeelding te exporteren en een bereik naar een afbeelding
  te converteren met nette code.
og_title: Hoe een Pivot opslaan als afbeelding – Snelle C#‑tutorial
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Hoe een draaitabel opslaan als afbeelding – Stapsgewijze handleiding
url: /nl/net/image-and-chart-operations/how-to-save-pivot-as-an-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een draaitabel opslaan als afbeelding – Complete C# Tutorial

Heb je je ooit afgevraagd **how to save pivot** direct vanuit een Excel-werkblad op te slaan zonder het bestand handmatig te openen? Je bent niet de enige. In veel rapportage‑pipelines is de draaitabel het uiteindelijke beeld, en de volgende stap — deze in een PDF insluiten, e‑mailen, of op een dashboard plaatsen — vereist een statische afbeelding. Het goede nieuws? Met slechts een paar API‑aanroepen kun je **how to save pivot** uitvoeren zonder enige UI‑interactie.

In deze tutorial lopen we stap voor stap door de exacte code die je nodig hebt om **how to export pivot** uit te voeren, die export om te zetten in een **export pivot image**, en zelfs **convert range to image** voor elk aangepast gebied dat je wilt. Aan het einde heb je een herbruikbare methode die je in elk .NET‑project kunt gebruiken.

> **Snelle opmerking:** De voorbeelden gebruiken de populaire Aspose.Cells for .NET‑bibliotheek, maar de concepten zijn toepasbaar op elke bibliotheek die `PivotTable`, `Range` en afbeeldings‑exportfunctionaliteit biedt.

## Vereisten – Wat je nodig hebt voordat je begint

- **.NET 6+** (of .NET Framework 4.7.2+) geïnstalleerd op je machine.  
- **Aspose.Cells for .NET** (gratis proefversie of gelicentieerde versie). Je kunt het toevoegen via NuGet:  

  ```bash
  dotnet add package Aspose.Cells
  ```
- Een basisbegrip van C# en Excel‑concepten. Geen diepgaande interne kennis vereist.  
- Een bestaand Excel‑bestand (`sample.xlsx`) dat minstens één draaitabel bevat.

Als een van deze onbekend klinkt, pauzeer dan en installeer eerst het pakket — het heeft geen zin om dieper te duiken voordat de bibliotheek klaar is.

## Hoe een draaitabel opslaan als afbeelding – De kernmethode

Hieronder vind je een **complete, uitvoerbare** snippet die de volledige flow demonstreert. Het bevat imports, foutafhandeling en commentaar zodat je het direct kunt copy‑pasten in een console‑applicatie.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;   // Needed for Image handling
using System.Drawing;        // System.Drawing.Image

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the workbook that holds the pivot table
            string workbookPath = @"C:\Temp\sample.xlsx";

            // Destination folder for the exported image
            string outputFolder = @"C:\Temp\Images";

            try
            {
                // Ensure output directory exists
                System.IO.Directory.CreateDirectory(outputFolder);

                // Call the helper that does the actual work
                SavePivotAsImage(workbookPath, outputFolder, "pivot.png");
                Console.WriteLine("Pivot saved successfully!");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }

        /// <summary>
        /// Saves the first pivot table in the given workbook as an image file.
        /// This method shows exactly **how to export pivot** and **convert range to image**.
        /// </summary>
        /// <param name="workbookPath">Full path to the source .xlsx file.</param>
        /// <param name="outputFolder">Folder where the image will be written.</param>
        /// <param name="fileName">Desired image file name (e.g., pivot.png).</param>
        public static void SavePivotAsImage(string workbookPath, string outputFolder, string fileName)
        {
            // Load the workbook
            Workbook wb = new Workbook(workbookPath);

            // --------------------------------------------------------------
            // Step 1: Get the first pivot table from the first worksheet
            // --------------------------------------------------------------
            Worksheet ws = wb.Worksheets[0];
            if (ws.PivotTables.Count == 0)
                throw new InvalidOperationException("No pivot tables found in the worksheet.");

            // This is the object we will eventually export.
            PivotTable pivot = ws.PivotTables[0];

            // --------------------------------------------------------------
            // Step 2: Create a range that covers the entire pivot table
            // --------------------------------------------------------------
            // The CreateRange method returns a Range object that precisely
            // matches the pivot's visual bounds.
            Range pivotRange = pivot.CreateRange();

            // --------------------------------------------------------------
            // Step 3: Convert the range to an image (the **export pivot image** step)
            // --------------------------------------------------------------
            // ToImage returns a System.Drawing.Image instance.
            Image pivotImg = pivotRange.ToImage();

            // --------------------------------------------------------------
            // Step 4: Save the image to a file
            // --------------------------------------------------------------
            string fullPath = System.IO.Path.Combine(outputFolder, fileName);
            pivotImg.Save(fullPath, System.Drawing.Imaging.ImageFormat.Png);
        }
    }
}
```

### Waarom dit werkt

- **Toegang tot de draaitabel:** `ws.PivotTables[0]` pakt de eerste draaitabel, die vaak degene is die je wilt exporteren. Als je meerdere draaitabellen hebt, wijzig dan simpelweg de index of loop door de collectie.
- **Het bereik maken:** `pivot.CreateRange()` geeft je een `Range`‑object dat exact overeenkomt met de cellen die op het scherm worden weergegeven. Dit is de cruciale stap die je **convert range to image** laat uitvoeren zonder handmatig adressen te berekenen.
- **Het bereik omzetten naar een afbeelding:** `pivotRange.ToImage()` rastert intern de cellen, behoudt opmaak, kleuren en randen — precies wat je in Excel ziet.
- **De PNG opslaan:** De laatste `Save`‑aanroep schrijft een draagbaar PNG‑bestand, waardoor de **export pivot image** klaar is voor elke downstream‑procedure (PDF, e‑mail, web).

## Hoe een draaitabel exporteren – Variaties die je nodig kunt hebben

### Meerdere draaitabellen exporteren van hetzelfde blad

Als je werkmap meerdere draaitabellen bevat, kun je er doorheen loopen:

```csharp
foreach (PivotTable pt in ws.PivotTables)
{
    Range r = pt.CreateRange();
    Image img = r.ToImage();
    string name = $"pivot_{pt.Index}.png";
    img.Save(System.IO.Path.Combine(outputFolder, name), ImageFormat.Png);
}
```

### Exporteren naar andere formaten (JPEG, BMP, GIF)

De `Image.Save`‑methode accepteert elk `ImageFormat`. Vervang simpelweg `ImageFormat.Png` door `ImageFormat.Jpeg` of `ImageFormat.Bmp`:

```csharp
pivotImg.Save(fullPath, System.Drawing.Imaging.ImageFormat.Jpeg);
```

### Afbeeldingsresolutie aanpassen

Soms heb je een screenshot met hogere resolutie nodig voor afdrukken. Gebruik de overload die `ImageOrPrintOptions` accepteert:

```csharp
ImageOrPrintOptions opts = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300   // DPI
};
Image highRes = pivotRange.ToImage(opts);
highRes.Save(fullPath, ImageFormat.Png);
```

## Bereik omzetten naar afbeelding – Buiten draaitabellen

De `ToImage`‑methode is niet beperkt tot draaitabellen. Wil je een diagram, een datatabel of een aangepast celblok vastleggen? Geef gewoon een `Range` door:

```csharp
// Capture cells B2:E20 as an image
Range customRange = ws.Cells.CreateRange("B2", "E20");
Image rangeImg = customRange.ToImage();
rangeImg.Save(@"C:\Temp\custom_range.png", ImageFormat.Png);
```

Dat is de essentie van **convert range to image** — dezelfde API die je voor de draaitabel gebruikte werkt voor elk rechthoekig blok.

## Veelvoorkomende valkuilen & pro‑tips

- **Draaitabel vernieuwen:** Als je brongegevens wijzigen, roep dan `pivot.RefreshData()` aan vóór het maken van het bereik. Het overslaan van deze stap kan een verouderde weergave opleveren.
- **Verborgen rijen/kolommen:** Standaard worden verborgen rijen/kolommen genegeerd. Als je ze zichtbaar wilt, stel `pivot.ShowHiddenData = true` in vóór `CreateRange()`.
- **Geheugenbeheer:** `Image` implementeert `IDisposable`. In productiecodel moet je de afbeelding in een `using`‑blok plaatsen of `Dispose()` aanroepen na het opslaan om geheugenlekken te voorkomen.
- **Thread‑veiligheid:** Aspose.Cells‑objecten zijn niet thread‑safe. Als je draaitabellen vanuit meerdere threads exporteert, maak dan per thread een aparte `Workbook`‑instantie.

## Volledig werkend voorbeeld – Eén‑bestand oplossing

Voor wie van copy‑paste houdt, hier is het volledige programma samengevoegd tot één enkel bestand. Plaats het in een nieuw console‑project, werk de paden bij en voer het uit.

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using System.IO;
using Aspose.Cells;

namespace PivotExportDemo
{
    class Program
    {
        static void Main()
        {
            string src = @"C:\Temp\sample.xlsx";
            string outDir = @"C:\Temp\Images";

            Directory.CreateDirectory(outDir);
            SaveFirstPivotAsPng(src, outDir, "pivot.png");
        }

        static void SaveFirstPivotAsPng(string workbookPath, string folder, string fileName)
        {
            Workbook wb = new Workbook(workbookPath);
            Worksheet ws = wb.Worksheets[0];

            if (ws.PivotTables.Count == 0)
                throw new Exception("Worksheet contains no pivots.");

            PivotTable pt = ws.PivotTables[0];
            Range r = pt.CreateRange();

            using (Image img = r.ToImage())
            {
                string full = Path.Combine(folder, fileName);
                img.Save(full, ImageFormat.Png);
            }
        }
    }
}
```

Het uitvoeren hiervan print “Pivot saved successfully!” en laat een `pivot.png` achter op de opgegeven locatie.

## Conclusie

We hebben **how to save pivot** in C# van begin tot eind behandeld, je **how to export pivot** voor meerdere scenario's laten zien, een **export pivot image** met verschillende formaten gedemonstreerd, en de onderliggende **convert range to image**‑mechanica uitgelegd. Gewapend met deze snippets kun je rapportgeneratie automatiseren, afbeeldingen in PDF's invoegen, of simpelweg je analytics‑dashboards archiveren zonder ooit Excel handmatig te openen.

Volgende stappen? Probeer de gegenereerde PNG in een PDF te embedden met Aspose.PDF, of duw het naar een Azure Blob voor webgebruik. Je kunt ook verkennen hoe je diagrammen op dezelfde manier exporteert — vervang gewoon de `PivotTable` door een `Chart`‑object en roep `ToImage()` aan.

Heb je vragen over randgevallen, licenties of prestaties? Laat een reactie achter hieronder, en happy coding! 

![hoe draaitabel opslaan](/images/pivot-save-example.png "hoe draaitabel opslaan")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}