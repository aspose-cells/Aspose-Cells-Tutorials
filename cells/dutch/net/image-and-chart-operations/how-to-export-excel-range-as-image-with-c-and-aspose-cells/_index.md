---
category: general
date: 2026-09-24
description: Excel‑bereik exporteren als afbeelding in C# met Aspose.Cells – stapsgewijze
  handleiding om een werkbladgebied op te slaan als PNG of JPEG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- Aspose.Cells export range
- C# Excel to PNG
- ImageOrPrintOptions usage
- export pivot table as image
language: nl
lastmod: 2026-09-24
og_description: Exporteer een Excel-bereik als afbeelding in C# met Aspose.Cells.
  Leer hoe je elk werkbladgebied, inclusief draaitabellen, binnen enkele minuten naar
  PNG of JPEG kunt converteren.
og_image_alt: Screenshot of a C# program exporting an Excel range to a PNG image
og_title: Excel-bereik exporteren als afbeelding met C# – volledige Aspose.Cells-gids
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  headline: How to export excel range as image with C# and Aspose.Cells
  type: TechArticle
- description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  name: How to export excel range as image with C# and Aspose.Cells
  steps:
  - name: '**Load** the workbook from disk.'
    text: '**Load** the workbook from disk.'
  - name: '**Define** the cell area that will become the image (the *print area*).'
    text: '**Define** the cell area that will become the image (the *print area*).'
  - name: '**Export** the area using `ImageOrPrintOptions` and write the file.'
    text: '**Export** the area using `ImageOrPrintOptions` and write the file.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Image export
title: Hoe een Excel‑bereik exporteren als afbeelding met C# en Aspose.Cells
url: /nl/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een Excel‑bereik exporteren als afbeelding met C# en Aspose.Cells

Als je **excel range als afbeelding wilt exporteren** in een .NET‑applicatie, laat deze gids je een complete, kant‑klaar oplossing zien. Of je nu een dashboard publiceert, een draaitabel in een webpagina embedt, of een miniatuur van een rapport genereert, je kunt elk werkbladgebied omzetten naar een PNG (of JPEG) met slechts een paar regels C#‑code.

In deze tutorial leer je hoe je:

* Een bestaande werkmap laden (`Workbook`‑klasse)  
* Het exacte celbereik dat je wilt vastleggen definiëren (`PrintArea`)  
* Afbeeldings‑exportopties configureren (`ImageOrPrintOptions`)  
* De resulterende afbeelding naar schijf opslaat  

Alle vereisten, randgevallen en veelvoorkomende valkuilen worden behandeld zodat je de code zonder verrassingen kunt aanpassen aan je eigen projecten.

## Vereisten

| Vereiste | Reden |
|----------|-------|
| **Aspose.Cells for .NET** (latest version) | Biedt de `Workbook`, `Worksheet` en `ImageOrPrintOptions` API's die in het voorbeeld worden gebruikt. |
| **.NET 6.0 or later** | Het voorbeeld richt zich op .NET 6, maar elke .NET Core/Framework‑versie die Aspose.Cells ondersteunt werkt. |
| **A valid Excel file** (e.g., `input.xlsx`) | De werkmap die je wilt converteren. |
| **Write permission to the output folder** | Vereist om `Save` te laten slagen. |

Je kunt Aspose.Cells installeren via NuGet:

```bash
dotnet add package Aspose.Cells
```

## Export excel range als afbeelding – overzicht van het proces

De bewerking bestaat uit drie logische fasen:

1. **Load** de werkmap van de schijf.  
2. **Define** het celgebied dat de afbeelding wordt (de *print area*).  
3. **Export** het gebied met `ImageOrPrintOptions` en schrijf het bestand.

Elke fase wordt hieronder opgesplitst in een specifieke stap met volledige broncode en uitleg.

## Stap 1: Werkmap laden

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Path to the source Excel file
string inputPath = @"YOUR_DIRECTORY\input.xlsx";

// Create a Workbook object – this reads the file into memory
Workbook workbook = new Workbook(inputPath);
```

**Waarom dit belangrijk is:**  
`Workbook` is het toegangspunt voor alle Excel‑bewerkingen. Het bestand één keer laden houdt het geheugenverbruik laag en stelt je in staat later elk werkblad te benaderen.

## Stap 2: Toegang tot het doel‑werkblad

```csharp
// Get the first worksheet (index 0). Change the index or use the sheet name as needed.
Worksheet sheet = workbook.Worksheets[0];
```

**Tip:** Als je een specifiek blad op naam nodig hebt, vervang dan de index door `workbook.Worksheets["SheetName"]`. Dit voorkomt fouten wanneer de lay-out van de werkmap verandert.

## Stap 3: Definieer het bereik dat je wilt exporteren

```csharp
// Define the cell range that will be exported.
// Example: A1:G20 captures a typical pivot‑table area.
sheet.PageSetup.PrintArea = "A1:G20";
```

**Waarom `PrintArea` instellen?**  
Aspose.Cells rendert de *print area* bij het maken van een afbeelding. Door het te beperken tot het exacte bereik, vermijd je extra witruimte en verbeter je de prestaties.

### Alternatief: Het volledige blad exporteren

Als je het hele werkblad wilt, laat dan simpelweg de `PrintArea`‑toewijzing weg. Aspose.Cells gebruikt standaard het gebruikte bereik van het blad.

## Stap 4: Configureren van afbeeldings‑exportopties

```csharp
// Create an ImageOrPrintOptions object to control the output format.
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    // Choose PNG for lossless quality; change to Jpeg for smaller files.
    ImageFormat = ImageFormat.Png,

    // Optional: set the resolution (DPI). Higher DPI yields sharper images.
    HorizontalResolution = 300,
    VerticalResolution = 300,

    // Optional: set the page orientation if the range is wide.
    PageOrientation = PageOrientationType.Landscape
};
```

**Uitleg van belangrijke eigenschappen:**

* `ImageFormat` – Bepaalt het bestandstype (`Png`, `Jpeg`, `Bmp`, etc.). PNG is ideaal voor grafieken en tekst omdat het scherpe randen behoudt.
* `HorizontalResolution` / `VerticalResolution` – Regelen de pixel‑dichtheid. Voor web‑miniaturen is 96 DPI voldoende; voor afdruk‑gereed grafisch werk wordt 300 DPI aanbevolen.
* `PageOrientation` – Helpt wanneer het geselecteerde bereik breder is dan hoog.

## Stap 5: Het bereik exporteren naar een afbeeldingsbestand

```csharp
// Define the output path for the image
string outputPath = @"YOUR_DIRECTORY\range.png";

// Save the first picture on the worksheet as an image.
// The Pictures collection is automatically populated after setting PrintArea.
sheet.Pictures[0].Save(outputPath, imgOptions);
```

**Wat er achter de schermen gebeurt:**  
Wanneer `PrintArea` is ingesteld, genereert Aspose.Cells een tijdelijke afbeelding die dat gebied vertegenwoordigt. Het `Pictures[0]`‑object wordt vervolgens opgeslagen met de door jou opgegeven opties.

### Omgaan met werkbladen zonder afbeeldingen

Als het werkblad nog geen afbeelding bevat (bijv. een gloednieuwe file), kun je er één on‑the‑fly maken:

```csharp
// Create a picture from the defined range and add it to the sheet
Picture pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
pic.Save(outputPath, imgOptions);
```

## Volledig, uitvoerbaar voorbeeld

Alles bij elkaar genomen, hier is een zelfstandige console‑applicatie die je kunt kopiëren, plakken en uitvoeren:

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // 2️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Define the range to export (e.g., a pivot table)
        sheet.PageSetup.PrintArea = "A1:G20";

        // 4️⃣ Set image export options (PNG, 300 DPI, landscape)
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300,
            PageOrientation = PageOrientationType.Landscape
        };

        // 5️⃣ Save the picture as an image file
        string outputPath = @"YOUR_DIRECTORY\range.png";

        // Ensure a picture exists; create one if necessary
        Picture pic;
        if (sheet.Pictures.Count == 0)
        {
            pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
        }
        else
        {
            pic = sheet.Pictures[0];
        }

        pic.Save(outputPath, imgOptions);

        System.Console.WriteLine($"Export completed: {outputPath}");
    }
}
```

**Verwachte output:**  
Er verschijnt een bestand met de naam `range.png` in `YOUR_DIRECTORY`. Bij het openen zie je de exacte cellen van **A1 tot G20** weergegeven als een scherpe PNG‑afbeelding.

## Veelvoorkomende variaties en afhandeling van randgevallen

| Scenario | Aanpassing |
|----------|------------|
| **Export naar JPEG** | Wijzig `ImageFormat = ImageFormat.Jpeg` en stel eventueel `Quality = 90` in (bereik 0‑100). |
| **Meerdere bereiken** | Roep `sheet.Pictures.Add` aan voor elk bereik en sla elke afbeelding op met een unieke bestandsnaam. |
| **Grote werkbladen** | Verhoog `HorizontalResolution`/`VerticalResolution` alleen voor het benodigde bereik om geheugenpieken te voorkomen. |
| **Geen afbeelding gegenereerd** | Controleer of `PrintArea` correct is geformatteerd (`"A1:G20"`). Een ongeldige adres leidt tot een lege `Pictures`‑collectie. |
| **Opslaan naar een stream** | Gebruik `pic.Save(Stream, imgOptions)` wanneer je de afbeelding in het geheugen nodig hebt (bijv. voor een ASP.NET‑respons). |

## Pro‑tips voor betrouwbare afbeeldingsexport

* **Validate the print area** – Gebruik `CellArea`‑parsing (`CellArea area = CellArea.CreateCellArea("A1", "G20")`) om programmatisch bereiken op te bouwen en typefouten te vermijden.  
* **Dispose of resources** – Plaats `Workbook` in een `using`‑blok als je veel bestanden verwerkt om native resources snel vrij te geven.  
* **Batch processing** – Bij het exporteren van tientallen bereiken, hergebruik een enkele `ImageOrPrintOptions`‑instantie om de overhead van objectallocatie te verminderen.  
* **Thread safety** – Aspose.Cells‑objecten zijn **niet** thread‑veilig. Maak een aparte `Workbook` per thread of synchroniseer de toegang.

## Conclusie

Je hebt nu een complete, productie‑klare methode om **excel range als afbeelding te exporteren** met C# en Aspose.Cells. De stappen — het laden van de werkmap, het instellen van de print area, het configureren van `ImageOrPrintOptions` en het opslaan van de afbeelding — behandelen zowel het “hoe” als het “waarom”, zodat je de code kunt aanpassen aan draaitabellen, grafieken of elk aangepast celblok.

Vervolgens kun je verkennen:

* **Export excel range as image** in andere formaten (SVG, BMP) – een ander secundair trefwoord om te proberen.  
* **Embedding the PNG in a PDF** met Aspose.PDF voor end‑to‑end rapportgeneratie.  
* **Automating batch exports** over meerdere werkmappen met een eenvoudige console‑lus.

Voel je vrij om te experimenteren met verschillende resoluties, oriëntaties en uitvoermap‑locaties. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Excel-cellen exporteren naar afbeelding met Aspose.Cells .NET: Een stapsgewijze gids](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [Excel-werkmap exporteren als afbeelding met Aspose.Cells voor Java](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Hoe een Excel-werkblad exporteren naar PNG met Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}