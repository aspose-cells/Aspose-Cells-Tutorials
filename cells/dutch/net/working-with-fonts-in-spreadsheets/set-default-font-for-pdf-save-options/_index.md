---
title: Standaardlettertype instellen voor PDF-opslagopties
linktitle: Standaardlettertype instellen voor PDF-opslagopties
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u standaardlettertypen voor PDF-opslagopties instelt met Aspose.Cells voor .NET, zodat uw documenten er altijd perfect uitzien.
weight: 11
url: /nl/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Standaardlettertype instellen voor PDF-opslagopties

## Invoering
Als het gaat om het genereren van rapporten, facturen of andere documenten in PDF-formaat, is het van het grootste belang dat uw inhoud er precies goed uitziet. Lettertypen spelen een essentiële rol bij het behouden van de visuele aantrekkingskracht en leesbaarheid van uw documenten. Maar wat gebeurt er als het lettertype dat u in uw Excel-bestand hebt gebruikt, niet beschikbaar is op het systeem waarop u uw PDF genereert? Dan komt Aspose.Cells voor .NET goed van pas. Met deze krachtige bibliotheek kunt u standaardlettertypen instellen voor uw PDF-opslagopties, zodat uw documenten er professioneel en consistent uitzien, ongeacht waar ze worden geopend.
## Vereisten
Voordat we beginnen, zorg ervoor dat u het volgende heeft:
1. Visual Studio: U hebt een ontwikkelomgeving zoals Visual Studio nodig om uw code te schrijven en uit te voeren.
2.  Aspose.Cells voor .NET: U kunt de nieuwste versie downloaden van[deze link](https://releases.aspose.com/cells/net/)U kunt het ook installeren via NuGet Package Manager in Visual Studio.
3. Basiskennis van C#: Als u de basisprincipes van C# begrijpt, kunt u de codevoorbeelden beter volgen.
4. Voorbeeld Excel-bestand: Zorg dat u een voorbeeld Excel-bestand gereed hebt om te testen. U kunt er een maken met verschillende lettertypen en stijlen om te zien hoe Aspose.Cells omgaat met ontbrekende lettertypen.
## Pakketten importeren
Voordat u Aspose.Cells in uw project kunt gebruiken, moet u de benodigde pakketten importeren. Dit is hoe u dat doet:
1. Open uw project: start Visual Studio en open uw bestaande project of maak een nieuw project.
2. Verwijzingen toevoegen: Klik met de rechtermuisknop op uw project in Solution Explorer en selecteer 'NuGet-pakketten beheren'.
3. Installeer Aspose.Cells: Zoek naar "Aspose.Cells" en klik op de knop "Installeren".
4. Voeg richtlijnen toe: neem bovenaan uw C#-bestand de volgende naamruimten op:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## Stap 1: Stel uw mappen in
Voordat u met bestanden gaat werken, is het belangrijk om de bron- en uitvoermappen te definiëren. Dit maakt het gemakkelijker om uw invoer-Excel-bestand te vinden en de gegenereerde uitvoerbestanden op te slaan.
```csharp
// Bron directory
string sourceDir = "Your Document Directory";
// Uitvoermap
string outputDir = "Your Document Directory";
```
 Vervangen`"Your Document Directory"` met het daadwerkelijke pad naar uw mappen.
## Stap 2: Open het Excel-bestand
 Nu we onze mappen hebben ingesteld, openen we het Excel-bestand waarmee u wilt werken.`Workbook` klasse in Aspose.Cells wordt gebruikt om het Excel-document te laden.
```csharp
// Open een Excel-bestand
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
Zorg ervoor dat u de bestandsnaam vervangt door de daadwerkelijke bestandsnaam.
## Stap 3: Stel opties voor het renderen van afbeeldingen in
Vervolgens moeten we de renderingopties configureren om ons Excel-blad te converteren naar een afbeeldingsformaat. We maken een instantie van`ImageOrPrintOptions`, waarbij u het afbeeldingstype en het standaardlettertype opgeeft.
```csharp
// Renderen naar PNG-bestandsformaat
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
 In dit codefragment stellen we de`CheckWorkbookDefaultFont` eigendom van`false`, wat betekent dat als er lettertypen ontbreken, het opgegeven standaardlettertype (“Times New Roman”) wordt gebruikt.
## Stap 4: Render het werkblad als een afbeelding
 Laten we nu het eerste blad van de werkmap renderen als een PNG-afbeelding. We gebruiken de`SheetRender` klasse om dit te bereiken.
```csharp
// Render het eerste werkblad naar een afbeelding
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## Stap 5: Wijzig het afbeeldingstype en render naar TIFF
 Als u hetzelfde werkblad naar een ander afbeeldingsformaat wilt renderen, zoals TIFF, kunt u eenvoudig de`ImageType` eigenschap en herhaal het renderingproces.
```csharp
// Instellen op TIFF-indeling
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## Stap 6: PDF-opslagopties configureren
 Vervolgens gaan we de PDF-opslagopties instellen. We maken een instantie van`PdfSaveOptions`stel het standaardlettertype in en geef aan dat we willen controleren op ontbrekende lettertypen.
```csharp
// Opties voor het opslaan van PDF's configureren
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## Stap 7: Sla de werkmap op als PDF
Nu de opslagopties zijn geconfigureerd, is het tijd om onze Excel-werkmap op te slaan als een PDF-bestand. 
```csharp
// Sla de werkmap op als PDF
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## Stap 8: Bevestig de uitvoering
Ten slotte is het een goede gewoonte om de gebruiker te laten weten dat het proces succesvol is voltooid. U kunt dit bereiken door een eenvoudig consolebericht te gebruiken.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## Conclusie
Aspose.Cells biedt een flexibele en robuuste manier om Excel-bestandsmanipulaties te verwerken, waardoor het voor ontwikkelaars eenvoudiger wordt om visueel aantrekkelijke documenten te maken die hun opmaak behouden. Of u nu werkt aan rapporten, financiële documenten of een andere vorm van gegevenspresentatie, controle hebben over de weergave van lettertypen kan de kwaliteit van uw uitvoer aanzienlijk verbeteren.
## Veelgestelde vragen
### Wat is Aspose.Cells?
Aspose.Cells is een krachtige .NET-bibliotheek waarmee ontwikkelaars Excel-bestanden kunnen bewerken zonder dat Microsoft Excel geïnstalleerd hoeft te zijn. Het ondersteunt verschillende bestandsformaten en biedt uitgebreide functies voor het werken met spreadsheets.
### Hoe kan ik een standaardlettertype voor mijn Excel-bestanden instellen?
 U kunt een standaardlettertype instellen met behulp van de`PdfSaveOptions` class en geef de gewenste lettertypenaam op. Dit zorgt ervoor dat zelfs als er een lettertype ontbreekt, uw document het standaardlettertype gebruikt dat u hebt opgegeven.
### Kan ik Excel-bestanden converteren naar andere formaten dan PDF?
Absoluut! Met Aspose.Cells kunt u Excel-bestanden converteren naar verschillende formaten, waaronder afbeeldingen (PNG, TIFF), HTML, CSV en meer.
### Is Aspose.Cells gratis te gebruiken?
Aspose.Cells is een commercieel product, maar u kunt het gratis uitproberen met een beperkte proefversie. Voor volledige functionaliteit moet u een licentie aanschaffen.
### Waar kan ik ondersteuning vinden voor Aspose.Cells?
 Ondersteuning voor Aspose.Cells vindt u op de website[Aspose-forum](https://forum.aspose.com/c/cells/9), waar u vragen kunt stellen en inzichten kunt delen met andere gebruikers en ontwikkelaars.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
