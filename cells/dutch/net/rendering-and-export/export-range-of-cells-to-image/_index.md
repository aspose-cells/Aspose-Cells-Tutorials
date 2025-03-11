---
title: Exporteer het celbereik naar een afbeelding met Aspose.Cells
linktitle: Exporteer het celbereik naar een afbeelding met Aspose.Cells
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Exporteer eenvoudig Excel-celbereiken naar afbeeldingen met Aspose.Cells voor .NET met deze stapsgewijze handleiding. Verbeter uw rapportage en presentaties.
weight: 14
url: /nl/net/rendering-and-export/export-range-of-cells-to-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exporteer het celbereik naar een afbeelding met Aspose.Cells

## Invoering
Wanneer u met Excel-bestanden werkt, kan de mogelijkheid om specifieke celbereiken naar afbeeldingen te converteren ongelooflijk nuttig zijn. Stelt u zich eens voor dat u een cruciaal onderdeel van uw spreadsheet moet delen zonder het hele document te verzenden: hier komt Aspose.Cells voor .NET om de hoek kijken! In deze gids leiden we u stap voor stap door het exporteren van een celbereik naar een afbeelding, zodat u elk onderdeel van het proces begrijpt zonder technische obstakels.
## Vereisten
Voordat u met de tutorial begint, zijn er een paar vereisten om ervoor te zorgen dat alles correct is ingesteld:
1. Visual Studio: Zorg ervoor dat Visual Studio op uw systeem is geïnstalleerd.
2.  Aspose.Cells voor .NET: Download deze bibliotheek van de[Aspose-site](https://releases.aspose.com/cells/net/)U kunt ook een gratis proefperiode starten als u de mogelijkheden ervan wilt verkennen voordat u zich vastlegt.
3. Basiskennis van C#: Kennis van C# en het .NET Framework helpt u de code beter te begrijpen.
4.  Een voorbeeld van een Excel-bestand: voor deze tutorial gebruiken we een bestand met de naam`sampleExportRangeOfCellsInWorksheetToImage.xlsx`U kunt een eenvoudig Excel-bestand maken voor testdoeleinden.
Nu we de vereisten hebben besproken, kunnen we meteen aan de slag met de code!
## Pakketten importeren
Om te beginnen moeten we de essentiële namespaces importeren. Dit is hoe je dat doet:
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
Met deze pakketten kunnen we werken met werkmappen en werkbladen en de weergave van onze celbereiken beheren.
## Stap 1: Stel uw directorypaden in
Het instellen van directories lijkt misschien saai, maar het is superbelangrijk. Deze stap zorgt ervoor dat uw programma weet waar de bestanden te vinden zijn en waar de geëxporteerde afbeeldingen opgeslagen moeten worden.
```csharp
// Bron directory
string sourceDir = "Your Document Directory";
// Uitvoermap
string outputDir = "Your Document Directory";
```
 Vervangen`"Your Document Directory"`met het daadwerkelijke pad waar uw bestanden zich bevinden. Dit kan een pad op uw lokale schijf of een netwerkdirectory zijn.
## Stap 2: Maak een werkmap van het bronbestand
 De volgende stap is het creëren van een`Workbook` object dat als toegangspunt tot het Excel-bestand dient.
```csharp
// Maak een werkmap van het bronbestand.
Workbook workbook = new Workbook(sourceDir + "sampleExportRangeOfCellsInWorksheetToImage.xlsx");
```
 Hier creëren we een nieuwe`Workbook` bijvoorbeeld, door het volledige pad van het Excel-bestand waarmee u wilt werken door te geven. Deze stap opent het bestand en bereidt het voor op manipulatie.
## Stap 3: Toegang tot het eerste werkblad
Zodra we de werkmap hebben, moeten we het werkblad openen met de gegevens die we willen exporteren.
```csharp
// Toegang tot het eerste werkblad
Worksheet worksheet = workbook.Worksheets[0];
```
 De`Worksheets` collectie is 0-geïndexeerd, wat betekent dat`Worksheets[0]` geeft ons het eerste blad. U kunt de index aanpassen als u een ander blad wilt.
## Stap 4: Stel het afdrukgebied in
Vervolgens moeten we het gebied definiëren dat we als afbeelding willen exporteren. Dit doen we door het afdrukgebied op het werkblad in te stellen.
```csharp
// Stel het afdrukgebied in met het door u gewenste bereik
worksheet.PageSetup.PrintArea = "D8:G16";
```
In dit geval geven we aan dat we de cellen van D8 naar G16 willen exporteren. Pas deze celverwijzingen aan op basis van de gegevens die u wilt vastleggen.
## Stap 5: Marges configureren
Laten we ervoor zorgen dat onze geëxporteerde afbeelding geen onnodige witruimte heeft. We zetten alle marges op nul.
```csharp
// Stel alle marges in op 0
worksheet.PageSetup.LeftMargin = 0;
worksheet.PageSetup.RightMargin = 0;
worksheet.PageSetup.TopMargin = 0;
worksheet.PageSetup.BottomMargin = 0;
```
Deze stap is cruciaal om ervoor te zorgen dat de uiteindelijke afbeelding perfect past, zonder rommel eromheen.
## Stap 6: Afbeeldingsopties instellen
Vervolgens stellen we de opties in voor hoe de afbeelding wordt gerenderd. Dit omvat het specificeren van de resolutie en het afbeeldingstype.
```csharp
// Stel de optie OnePagePerSheet in op true
ImageOrPrintOptions options = new ImageOrPrintOptions();
options.OnePagePerSheet = true;
options.ImageType = ImageType.Jpeg;
options.HorizontalResolution = 200;
options.VerticalResolution = 200;
```
Hier stellen we dat we willen dat de afbeelding in JPEG-formaat is met een resolutie van 200 DPI. U kunt de DPI naar eigen wens aanpassen.
## Stap 7: Render het werkblad naar een afbeelding
Nu komt het spannende gedeelte: het werkblad omzetten in een afbeelding!
```csharp
// Maak een afbeelding van je werkblad
SheetRender sr = new SheetRender(worksheet, options);
sr.ToImage(0, outputDir + "outputExportRangeOfCellsInWorksheetToImage.jpg");
```
 Wij creëren een`SheetRender` instantie en oproep`ToImage`om de afbeelding te genereren vanaf de eerste pagina van het opgegeven werkblad. De afbeelding wordt opgeslagen in de uitvoermap met de opgegeven bestandsnaam.
## Stap 8: Bevestig de uitvoering
Ten slotte is het altijd goed om feedback te geven nadat de bewerking is voltooid. Daarom sturen we een bericht naar de console.
```csharp
Console.WriteLine("ExportRangeOfCellsInWorksheetToImage executed successfully.\r\n");
```
Deze stap is cruciaal om het succes van de bewerking te bevestigen, vooral wanneer u de code in een consoletoepassing uitvoert.
## Conclusie
En daar heb je het: je stapsgewijze handleiding voor het exporteren van een cellenbereik naar een afbeelding met Aspose.Cells voor .NET! Met deze krachtige bibliotheek kun je Excel-bestanden naadloos bewerken en ermee werken, en nu weet je hoe je die belangrijke cellen als afbeeldingen kunt vastleggen. Of het nu gaat om rapportages, presentaties of het delen van specifieke gegevens, deze methode is ongelooflijk handig en efficiënt. 
## Veelgestelde vragen
### Kan ik het afbeeldingsformaat wijzigen?
 Ja! U kunt de`ImageType` eigenschap om andere formaten zoals PNG of BMP te ondersteunen.
### Wat als ik meerdere bereiken wil exporteren?
moet de renderingstappen herhalen voor elk bereik dat u wilt exporteren.
### Is er een limiet aan de grootte van het bereik dat ik kan exporteren?
Hoewel Aspose.Cells behoorlijk robuust is, kunnen extreem grote bereiken de prestaties beïnvloeden. Het is het beste om binnen redelijke grenzen te testen.
### Kan ik dit proces automatiseren?
Absoluut! U kunt deze code integreren in grotere applicaties of scripts om uw Excel-taken te automatiseren.
### Waar kan ik extra ondersteuning krijgen?
 Voor verdere assistentie, bezoek de[Aspose Ondersteuningsforum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
