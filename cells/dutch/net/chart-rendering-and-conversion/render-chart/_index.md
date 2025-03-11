---
title: Grafiek weergeven
linktitle: Grafiek weergeven
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Ontdek hoe u grafieken in .NET kunt renderen met Aspose.Cells. Volg onze stapsgewijze tutorial om moeiteloos verbluffende visuals te maken.
weight: 10
url: /nl/net/chart-rendering-and-conversion/render-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Grafiek weergeven

## Invoering

Grafieken zijn een essentieel element in datapresentatie en -analyse, waardoor complexe informatie gemakkelijk te verteren is. Als u met .NET werkt en grafieken programmatisch moet genereren, is Aspose.Cells een krachtige bibliotheek die intuïtieve en geavanceerde functies biedt voor het verwerken van Excel-bestanden en grafieken. In deze gids doorlopen we het proces van het renderen van een grafiek met Aspose.Cells voor .NET. Maak je klaar om in deze gedetailleerde tutorial te duiken, die is ontworpen om boeiend en gemakkelijk te volgen te zijn!

## Vereisten

Voordat we in de code duiken, zorgen we ervoor dat je alles klaar hebt. Dit is wat je nodig hebt:

1. .NET-omgeving: Zorg ervoor dat u een .NET-ontwikkelomgeving hebt ingesteld. U kunt Visual Studio of een andere IDE gebruiken die .NET ondersteunt.
2.  Aspose.Cells voor .NET: U moet de Aspose.Cells-bibliotheek geïnstalleerd hebben. U kunt deze downloaden van[Aspose's releasepagina](https://releases.aspose.com/cells/net/).
3. Basiskennis van C#: Als u bekend bent met C#-programmering, begrijpt u de voorbeelden beter. Maar maak u geen zorgen als u nieuw bent: in deze gids wordt alles stap voor stap uitgelegd!

## Pakketten importeren

De eerste stap in uw codeerreis is het importeren van de benodigde pakketten. Open uw project in uw IDE en voeg de volgende naamruimte toe:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
```

Met deze naamruimten krijgt u toegang tot de functionaliteit van de Aspose.Cells-bibliotheek, zodat u naadloos grafieken kunt maken en bewerken.


Nu we de vereisten en imports hebben besproken, duiken we in de details van het renderen van een grafiek! We splitsen het op in duidelijke, beheersbare stappen.

## Stap 1: Stel uw uitvoermap in

Voordat we onze werkmap en grafiek maken, moeten we bepalen waar onze outputs worden opgeslagen. Op deze manier weet u precies waar u onze grafiek kunt vinden wanneer deze wordt gegenereerd.

```csharp
string outputDir = "Your Output Directory"; // Geef hier de uitvoermap op.
```

Zorg ervoor dat u 'Uw uitvoermap' vervangt door het pad waar u uw grafiekafbeeldingen wilt opslaan.

## Stap 2: Maak een werkmap

Vervolgens maken we een nieuwe werkmap. Dit is waar alle magie gebeurt!

```csharp
Workbook workbook = new Workbook();
```

 Deze regel creëert een nieuw exemplaar van de`Workbook` klasse, waarmee we met bladen en grafieken kunnen werken.

## Stap 3: Een nieuw werkblad toevoegen

Nu we onze werkmap hebben, is het tijd om een nieuw werkblad toe te voegen. Beschouw werkbladen als verschillende pagina's in een notitieboek, waar u uw gegevens georganiseerd kunt houden.

```csharp
int sheetIndex = workbook.Worksheets.Add();
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```

Hier voegen we een nieuw werkblad toe en verkrijgen we een referentie ernaar. U zult met dit werkblad werken om uw gegevens en grafieken in te voeren.

## Stap 4: Voorbeeldwaarden invoeren

Nu ons werkblad is gemaakt, voegen we wat voorbeeldgegevens toe aan de cellen. Deze gegevens zijn de basis voor uw grafiek, dus kies waarden die logisch zijn voor uw grafiektype!

```csharp
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```

In dit fragment vullen we cellen "A1" tot "A3" met wat numerieke waarden en cellen "B1" tot "B3" met een andere set waarden. Voel je vrij om deze getallen aan te passen aan jouw behoeften!

## Stap 5: Maak een grafiek

Nu is het tijd om uw grafiek te maken. We voegen een kolomdiagram toe, wat geweldig is voor het vergelijken van waarden.

```csharp
int chartIndex = worksheet.Charts.Add(ChartType.Column, 5, 0, 15, 5);
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

Hier voegen we een grafiek toe op de opgegeven locatie door de lay-out ervan te definiëren: de eerste reeks getallen geeft de positie van de grafiek op het raster weer.

## Stap 6: Gegevensreeksen toevoegen aan de grafiek

Nu we de grafiek hebben gemaakt, moeten we deze koppelen aan de gegevens die we in de vorige stappen hebben ingevoerd.

```csharp
chart.NSeries.Add("A1:B3", true);
```

Deze lijn verbindt de gegevensreeksen van de grafiek met de waarden in cellen "A1" tot en met "B3". Dit betekent dat uw grafiek de gegevens visueel weergeeft zoals bedoeld.

## Stap 7: Sla de grafiek op als afbeelding

Laten we ons diagram nu omzetten naar een afbeeldingsformaat, zodat u het eenvoudig kunt delen en bekijken.

```csharp
chart.ToImage(outputDir + "outputChartRendering.emf", System.Drawing.Imaging.ImageFormat.Emf);
```

In deze stap slaan we de grafiek op als een EMF (Enhanced Metafile) afbeelding in de opgegeven output directory. U kunt het ook opslaan in verschillende formaten zoals BMP of PNG.

## Stap 8: Converteer grafiek naar bitmap

Als u liever met bitmaps werkt, kunt u uw grafiek als volgt naar een bitmapformaat converteren.

```csharp
System.Drawing.Bitmap bitmap = chart.ToImage();
bitmap.Save(outputDir + "outputChartRendering.bmp", System.Drawing.Imaging.ImageFormat.Bmp);
```

Dit slaat uw grafiek op als een BMP-afbeelding. Vergeet niet dat BMP-bestanden over het algemeen groter zijn, maar van ongelooflijk hoge kwaliteit!

## Stap 9: Renderen met geavanceerde opties

We kunnen de grafiek ook renderen met een aantal geavanceerde afbeeldingsopties voor een betere kwaliteit en resolutie. Laten we een paar opties instellen:

```csharp
ImageOrPrintOptions options = new ImageOrPrintOptions()
{
    VerticalResolution = 300,
    HorizontalResolution = 300,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.AntiAlias
};
```

Met deze opties verbetert u de visuele kwaliteit van de afbeelding die u genereert. Dit is vooral handig voor presentaties of publicaties.

## Stap 10: Converteer grafiek naar afbeelding met geavanceerde opties

Laten we nu de grafiek converteren met behulp van de geavanceerde opties die we zojuist hebben ingesteld.

```csharp
chart.ToImage(outputDir + "outputChartRendering.png", options);
```

Hiermee wordt uw grafiek opgeslagen als een PNG-bestand met verbeterde kwaliteitsinstellingen.

## Stap 11: De grafiek exporteren naar PDF

Als u ten slotte een verzorgd, eenvoudig te delen document wilt, kunt u uw grafiek rechtstreeks naar een PDF-formaat exporteren.

```csharp
chart.ToPdf(outputDir + "outputChartRendering.pdf");
```

Met deze stap wordt een PDF-bestand gemaakt dat uw grafiek bevat, waardoor deze perfect is voor digitale rapporten of om te delen met collega's.

## Conclusie 

Gefeliciteerd! U hebt met succes een grafiek gerenderd met Aspose.Cells voor .NET. Deze krachtige bibliotheek vereenvoudigt het maken en bewerken van Excel-bestanden en grafieken, waardoor uw gegevens veel toegankelijker en visueel aantrekkelijker worden. Of u nu rapporten, analyses of presentaties voorbereidt, grafieken hebben een aanzienlijke impact en met Aspose kunt u ze eenvoudig programmatisch maken.

## Veelgestelde vragen

### Welke soorten grafieken kan ik maken met Aspose.Cells voor .NET?
U kunt verschillende grafieken maken, waaronder kolom-, lijn-, cirkel- en staafdiagrammen.

### Kan ik het uiterlijk van de grafieken aanpassen?
Ja, Aspose.Cells biedt uitgebreide aanpassingsmogelijkheden, waaronder kleuren, stijlen en grafiekelementen.

### Is er een gratis proefversie beschikbaar?
Absoluut! U kunt een gratis proefversie downloaden van[hier](https://releases.aspose.com/).

### Waar kan ik ondersteuning krijgen voor Aspose.Cells?
 U kunt ondersteuning en middelen van de gemeenschap vinden op de[Aspose Ondersteuningsforum](https://forum.aspose.com/c/cells/9).

### Heb ik een licentie nodig om Aspose.Cells te gebruiken?
 Ja, voor voortgezet gebruik na de proefperiode is een licentie vereist, maar u kunt een tijdelijke licentie aanvragen[hier](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
