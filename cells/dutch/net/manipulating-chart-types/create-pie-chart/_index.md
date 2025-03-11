---
title: Cirkeldiagram maken
linktitle: Cirkeldiagram maken
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u een cirkeldiagram in Excel maakt met Aspose.Cells voor .NET met deze stapsgewijze handleiding. Visualiseer uw gegevens moeiteloos.
weight: 12
url: /nl/net/manipulating-chart-types/create-pie-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cirkeldiagram maken

## Invoering

Het maken van diagrammen is essentieel voor het visueel weergeven van gegevens, en cirkeldiagrammen zijn een van de populairste manieren om te illustreren hoe delen een geheel vormen. Met Aspose.Cells voor .NET kunt u eenvoudig de generatie van cirkeldiagrammen in Excel-bestanden automatiseren. In deze tutorial duiken we in hoe u een cirkeldiagram vanaf nul kunt maken met Aspose.Cells voor .NET, met een stapsgewijze handleiding om het proces soepel en eenvoudig te maken. Of u nu nieuw bent met de tool of uw Excel-automatiseringsvaardigheden wilt verbeteren, deze handleiding heeft u gedekt!

## Vereisten

Voordat u in de code duikt, moet u ervoor zorgen dat u het volgende hebt ingesteld:

1.  Aspose.Cells voor .NET-bibliotheek: zorg ervoor dat u Aspose.Cells in uw project hebt geïnstalleerd. Als u het nog niet hebt geïnstalleerd, kunt u het downloaden van[hier](https://releases.aspose.com/cells/net/).
2. .NET-ontwikkelomgeving: zorg ervoor dat uw project is ingesteld voor gebruik met .NET Framework of .NET Core.
3. Basiskennis van C#: U moet vertrouwd zijn met C#-programmering, met name objectgeoriënteerd programmeren (OOP).

 Voor gevorderde gebruikers kan een tijdelijke licentie worden toegepast om alle functies van Aspose.Cells te ontgrendelen. U kunt er een aanvragen bij[hier](https://purchase.aspose.com/temporary-license/).

## Pakketten importeren

Om te beginnen importeert u de benodigde namespaces en packages die vereist zijn voor deze tutorial. Deze omvatten basis I/O-bewerkingen en het Aspose.Cells-pakket.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## Stap 1: Maak een nieuwe werkmap

 Eerst moeten we een instantie van de maken`Workbook` klasse, die het Excel-bestand vertegenwoordigt. Een werkmap bevat meerdere bladen en voor ons voorbeeld werken we met twee bladen: één voor gegevens en één voor het cirkeldiagram.

```csharp
Workbook workbook = new Workbook();
```

Dit initialiseert een nieuwe Excel-werkmap. Maar waar gaan de gegevens naartoe? Dat gaan we in de volgende stap regelen.

## Stap 2: Gegevens toevoegen aan het werkblad

Zodra de werkmap is gemaakt, moeten we het eerste werkblad openen en een naam geven. Hier voeren we de gegevens in die nodig zijn voor het cirkeldiagram.

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

Nu kunnen we een aantal dummy-verkoopgegevens invoeren die verschillende regio's vertegenwoordigen:

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

Hier voegen we twee kolommen toe: een voor regio's en een andere voor verkoopcijfers. Deze gegevens worden weergegeven in het cirkeldiagram.

## Stap 3: Voeg een grafiekblad toe

Laten we nu een apart werkblad toevoegen voor het cirkeldiagram.

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

Dit nieuwe blad zal het cirkeldiagram hosten. Door het een naam te geven zoals "Grafiek" weet u zeker dat gebruikers weten wat ze kunnen verwachten als ze het bestand openen.

## Stap 4: Maak het cirkeldiagram

Nu is het tijd om de eigenlijke grafiek te maken. We specificeren dat we een cirkeldiagram willen en we definiëren de positie ervan op het blad.

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

 De methode`Add()`accepteert parameters voor het grafiektype (in dit geval,`ChartType.Pie`), en de locatie ervan op het werkblad. De getallen geven rij- en kolomposities weer.

## Stap 5: Pas het uiterlijk van de grafiek aan

Een cirkeldiagram zou niet compleet zijn zonder enige aanpassing! Laten we ons diagram visueel aantrekkelijk maken door de kleuren, labels en titel aan te passen.

### Stel grafiektitel in
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### Perceeloppervlak aanpassen
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

We stellen de verloopvulling voor het tekengebied in en verbergen de rand voor een strakkere weergave.

## Stap 6: Definieer grafiekgegevens

 Het is tijd om de grafiek aan onze data te koppelen.`NSeries` De eigenschap van de grafiek koppelt de verkoopcijfers en regio's aan het cirkeldiagram.

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

 De eerste regel geeft aan dat we de verkoopgegevens uit de cellen gebruiken`B2:B8` . We vertellen de grafiek ook om de regionamen van`A2:A8` als categorie-labels.

## Stap 7: Gegevenslabels toevoegen

Labels direct aan de diagramsegmenten toevoegen kan het makkelijker maken om te begrijpen. Laten we de regionamen en verkoopwaarden opnemen in de cirkeldiagramsegmenten.

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## Stap 8: Pas het grafiekgebied en de legenda aan

Laten we als laatste het grafiekgebied en de legenda wat finishing touches geven. Dit verbetert de algehele presentatie van de grafiek.

### Grafiekgebied
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### Legende
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## Stap 9: Sla de werkmap op

Tot slot slaan we de werkmap op in een Excel-bestand. U kunt de uitvoermap en bestandsnaam naar wens opgeven.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## Conclusie

Het maken van een cirkeldiagram met Aspose.Cells voor .NET is een eenvoudig en aanpasbaar proces. Door deze handleiding te volgen, kunt u in slechts een paar stappen een professioneel ogende grafiek genereren die waardevolle inzichten biedt. Of het nu voor zakelijke rapportage of educatieve doeleinden is, het beheersen van het maken van grafieken zal uw Excel-automatiseringsvaardigheden verbeteren. Vergeet niet dat Aspose.Cells de flexibiliteit biedt die u nodig hebt om moeiteloos verbluffende, datagestuurde Excel-bestanden te maken.

## Veelgestelde vragen

### Kan ik andere typen grafieken maken met Aspose.Cells voor .NET?
Ja! Aspose.Cells ondersteunt verschillende grafiektypen, waaronder staafdiagrammen, lijndiagrammen en spreidingsdiagrammen.

### Heb ik een betaalde licentie nodig om Aspose.Cells voor .NET te gebruiken?
 kunt de gratis versie gebruiken met enkele beperkingen. Voor volledige functies hebt u een licentie nodig, die u kunt kopen[hier](https://purchase.aspose.com/buy).

### Kan ik de grafiek exporteren naar formaten zoals PDF of afbeeldingen?
Absoluut! Met Aspose.Cells kunt u grafieken exporteren naar verschillende formaten, waaronder PDF en PNG.

### Is het mogelijk om elke taartpunt met verschillende kleuren te stylen?
 Ja, u kunt verschillende kleuren op elk segment toepassen door de`IsColorVaried` eigendom van`true`, zoals getoond in de tutorial.

### Kan ik het genereren van meerdere grafieken in één werkmap automatiseren?
Ja, u kunt zoveel grafieken maken en aanpassen als u wilt in één Excel-bestand.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
