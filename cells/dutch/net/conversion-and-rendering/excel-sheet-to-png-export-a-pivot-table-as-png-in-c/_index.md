---
category: general
date: 2026-03-18
description: excel-werkblad‑naar‑png‑tutorial die laat zien hoe je een draaitabel
  exporteert, het afdrukgebied van de draaitabel instelt en een Excel‑bereikafbeelding
  exporteert met Aspose.Cells.
draft: false
keywords:
- excel sheet to png
- how to export pivot
- set print area pivot
- export excel range image
- export worksheet to image
language: nl
og_description: Excel-naar-PNG tutorial die je begeleidt bij het exporteren van draaitabellen,
  het instellen van het afdrukgebied voor draaitabellen en het exporteren van een
  Excel-bereikafbeelding met C#.
og_title: Excel-werkblad naar PNG – Complete gids voor het exporteren van draaitabellen
tags:
- Aspose.Cells
- C#
- Excel automation
title: Excel-werkblad naar PNG – Exporteer een draaitabel als PNG in C#
url: /nl/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excel sheet to png – Exporteer een draaitabel als PNG in C#

Heb je ooit een **excel sheet to png** moeten maken maar wist je niet hoe je alleen de draaitabel kunt vastleggen? Je bent niet de enige. In veel rapportage‑pipelines is de visualisatie van een draaitabel de ster, en door deze als PNG te exporteren kun je deze in e‑mails, dashboards of documentatie insluiten zonder de hele werkmap mee te nemen.

In deze gids laten we je zien **how to export pivot** data, **set print area pivot**, en uiteindelijk **export excel range image**, zodat je eindigt met een schoon **export worksheet to image**‑bestand. Geen mysterieuze links naar externe documenten—alleen een volledige, uitvoerbare code‑fragment en de redenering achter elke regel.

## Wat je nodig hebt

- **Aspose.Cells for .NET** (het NuGet‑pakket `Aspose.Cells` – versie 23.12 of nieuwer).  
- Een .NET‑ontwikkelomgeving (Visual Studio, Rider, of de `dotnet` CLI).  
- Een Excel‑bestand (`input.xlsx`) dat minstens één draaitabel bevat.

Dat is alles. Als je die hebt, laten we erin duiken.

## Stap 1 – Laad de werkmap en haal het eerste werkblad op

Voordat we de draaitabel kunnen benaderen, moeten we de werkmap in het geheugen laden.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");

            // Get the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];
```

*Waarom dit belangrijk is:* Het laden van het bestand geeft ons toegang tot alle objecten (tabellen, grafieken, draaitabellen). Het gebruiken van het eerste werkblad is een eenvoudige standaard; je kunt `0` vervangen door de werkelijke blad‑index of -naam indien nodig.

## Stap 2 – Haal het bereik van de draaitabel op

Een draaitabel bevindt zich binnen een celblok. We hebben dat blok nodig zodat we Excel kunnen vertellen wat er moet worden afgedrukt.

```csharp
            // Assume the first pivot table on the sheet
            PivotTable pivot = worksheet.PivotTables[0];

            // The range that the pivot occupies (e.g., A1:D20)
            CellArea pivotRange = pivot.PivotTableRange;
```

*Waarom we dit doen:* De `PivotTableRange` geeft ons de exacte begin‑ en eindrijen/kolommen. Zonder dit zou de export het hele blad omvatten, wat het doel van **set print area pivot** ondermijnt.

## Stap 3 – Definieer het afdrukgebied zodat alleen de draaitabel wordt gerenderd

De afdrukengine van Excel respecteert de eigenschap `PrintArea`. Door deze te beperken tot de draaitabel vermijden we vreemde data of lege cellen.

```csharp
            // Build the address string: "StartRow,StartColumn:EndRow,EndColumn"
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";

            worksheet.PageSetup.PrintArea = printArea;
```

*Pro tip:* Als je meerdere draaitabellen op hetzelfde blad hebt, kun je hun bereiken combineren met een door komma's gescheiden lijst (`"0,0:10,5,12,0:22,5"`). Dat is de **export excel range image**‑techniek voor meerdere blokken.

## Stap 4 – Stel de afbeeldings‑exportopties in (PNG‑formaat)

Aspose.Cells stelt je in staat de output fijn af te stemmen. PNG is verliesvrij, perfect voor scherpe draaitabel‑visualisaties.

```csharp
            // Configure image export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: increase resolution for sharper output
                HorizontalResolution = 300,
                VerticalResolution = 300
            };
```

*Waarom PNG?* In tegenstelling tot JPEG behoudt PNG de scherpte van tekst en transparante achtergronden, waardoor het de standaard is voor **excel sheet to png**‑scenario's.

## Stap 5 – Exporteer het werkblad (draaibereik) naar een PNG‑bestand

Nu gebeurt de magie—render het gedefinieerde afdrukgebied naar een afbeelding.

```csharp
            // Export the first page (index 0) of the worksheet to an image
            // The page corresponds to the print area we set earlier
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            // Inform the user
            System.Console.WriteLine("Pivot exported to PNG successfully!");
        }
    }
}
```

*Wat je zult zien:* Een bestand `pivot.png` dat alleen de draaitabel bevat, zonder extra rijen of kolommen. Open het in een willekeurige afbeeldingsviewer en je hebt een kant‑klare visual om te delen.

---

## Veelgestelde vragen & randgevallen

### Wat als de werkmap **meerdere draaitabellen** bevat?

Haal voor elke draaitabel de `PivotTableRange` op, voeg de bereiken samen en wijs de gecombineerde string toe aan `PrintArea`. Voorbeeld:

```csharp
string combinedArea = "";
foreach (PivotTable pt in worksheet.PivotTables)
{
    CellArea ca = pt.PivotTableRange;
    combinedArea += $"{ca.StartRow},{ca.StartColumn}:{ca.EndRow},{ca.EndColumn},";
}
combinedArea = combinedArea.TrimEnd(','); // Remove trailing comma
worksheet.PageSetup.PrintArea = combinedArea;
```

### Kan ik exporteren naar **andere afbeeldingsformaten**?

Zeker. Verander `imgOptions.ImageFormat = ImageFormat.Jpeg;` (of `Bmp`, `Gif`, `Tiff`). Houd er wel rekening mee dat JPEG compressie‑artefacten introduceert—meestal niet ideaal voor tekst‑zware draaitabellen.

### Hoe ga ik om met **grote draaitabellen** die over meerdere pagina's lopen?

Stel `imgOptions.OnePagePerSheet = false;` in om multi‑pagina rendering toe te staan, en loop vervolgens door de pagina's:

```csharp
int pageCount = worksheet.PageCount;
for (int i = 0; i < pageCount; i++)
{
    worksheet.ToImage(i, imgOptions).Save($@"C:\Data\pivot_page{i + 1}.png");
}
```

### Hoe zit het met **verborgen rijen/kolommen**?

Aspose respecteert de zichtbaarheidinstellingen van het werkblad. Als je verborgen elementen wilt negeren, maak ze tijdelijk zichtbaar vóór het exporteren of pas de `PrintArea` handmatig aan.

---

## Volledig werkend voorbeeld (klaar om te kopiëren‑en‑plakken)

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook & select sheet
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Get the first pivot table's range
            PivotTable pivot = worksheet.PivotTables[0];
            CellArea pivotRange = pivot.PivotTableRange;

            // 3️⃣ Set print area to the pivot only
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";
            worksheet.PageSetup.PrintArea = printArea;

            // 4️⃣ Prepare PNG export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // 5️⃣ Export to PNG
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            System.Console.WriteLine("✅ Pivot exported to PNG at C:\\Data\\pivot.png");
        }
    }
}
```

Voer het programma uit, en je vindt `pivot.png` precies op de opgegeven locatie. Open het bestand—je zou een scherpe weergave van alleen de draaitabel moeten zien, niets anders.

---

## Conclusie

Je hebt nu een **volledige, end‑to‑end oplossing** voor het omzetten van een **excel sheet to png** die zich uitsluitend richt op een draaitabel. Door **setting the print area pivot** toe te passen, **image export options** te configureren, en de `ToImage`‑methode van Aspose.Cells te gebruiken, kun je rapportgeneratie automatiseren, visualisaties in webpagina's insluiten, of eenvoudig analytische momentopnames archiveren.

Wat is het volgende? Probeer de PNG te vervangen door een hoge‑resolutie PDF (`ImageFormat.Pdf`), experimenteer met meerdere draaitabellen op één blad, of combineer deze aanpak met grafiek‑exports voor een volledig uitgeruste dashboard‑exportpipeline.

Heb je een eigen twist die je wilt delen? Laat een reactie achter, of start de volgende tutorial waarin we **export worksheet to image** verkennen voor volledige blad‑snapshots, inclusief grafieken en voorwaardelijke opmaak. Veel plezier met coderen!  

<img src="pivot.png" alt="excel sheet to png example of pivot table export">

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}