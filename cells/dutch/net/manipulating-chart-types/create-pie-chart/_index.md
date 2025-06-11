---
"description": "Leer hoe je een cirkeldiagram maakt in Excel met Aspose.Cells voor .NET met deze stapsgewijze handleiding. Visualiseer je gegevens moeiteloos."
"linktitle": "Cirkeldiagram maken"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Cirkeldiagram maken"
"url": "/nl/net/manipulating-chart-types/create-pie-chart/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cirkeldiagram maken

## Invoering

Het maken van grafieken is essentieel voor de visuele weergave van gegevens, en cirkeldiagrammen zijn een van de populairste manieren om te illustreren hoe onderdelen een geheel vormen. Met Aspose.Cells voor .NET kunt u het genereren van cirkeldiagrammen in Excel-bestanden eenvoudig automatiseren. In deze tutorial duiken we in hoe u een cirkeldiagram helemaal zelf kunt maken met Aspose.Cells voor .NET, met een stapsgewijze handleiding om het proces soepel en eenvoudig te laten verlopen. Of u nu nieuw bent met de tool of uw Excel-automatiseringsvaardigheden wilt verbeteren, deze handleiding helpt u verder!

## Vereisten

Voordat u in de code duikt, moet u ervoor zorgen dat u het volgende hebt ingesteld:

1. Aspose.Cells voor .NET-bibliotheek: Zorg ervoor dat Aspose.Cells in uw project is geïnstalleerd. Als u het nog niet hebt geïnstalleerd, kunt u het downloaden van [hier](https://releases.aspose.com/cells/net/).
2. .NET-ontwikkelomgeving: zorg ervoor dat uw project is ingesteld voor gebruik met .NET Framework of .NET Core.
3. Basiskennis van C#: U moet vertrouwd zijn met C#-programmering, met name objectgeoriënteerd programmeren (OOP).

Voor gevorderde gebruikers is een tijdelijke licentie beschikbaar waarmee alle functies van Aspose.Cells ontgrendeld kunnen worden. U kunt deze aanvragen bij [hier](https://purchase.aspose.com/temporary-license/).

## Pakketten importeren

Importeer om te beginnen de benodigde naamruimten en pakketten voor deze tutorial. Deze omvatten basis-I/O-bewerkingen en het Aspose.Cells-pakket.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## Stap 1: Een nieuwe werkmap maken

Eerst moeten we een instantie van de `Workbook` klasse, die het Excel-bestand vertegenwoordigt. Een werkmap bevat meerdere werkbladen, en in ons voorbeeld werken we met twee werkbladen: één voor de gegevens en één voor het cirkeldiagram.

```csharp
Workbook workbook = new Workbook();
```

Hiermee wordt een nieuwe Excel-werkmap geïnitialiseerd. Maar waar gaan de gegevens naartoe? Dat gaan we in de volgende stap regelen.

## Stap 2: Gegevens toevoegen aan het werkblad

Zodra de werkmap is aangemaakt, moeten we het eerste werkblad openen en een naam geven. Hier voeren we de gegevens in die nodig zijn voor het cirkeldiagram.

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

Hier voegen we twee kolommen toe: één voor regio's en één voor verkoopcijfers. Deze gegevens worden weergegeven in het cirkeldiagram.

## Stap 3: Voeg een grafiekblad toe

Laten we vervolgens een apart werkblad toevoegen voor het cirkeldiagram.

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

Dit nieuwe werkblad zal het cirkeldiagram bevatten. Door het een naam te geven zoals 'Grafiek', weten gebruikers wat ze kunnen verwachten wanneer ze het bestand openen.

## Stap 4: Maak het cirkeldiagram

Nu is het tijd om de grafiek zelf te maken. We geven aan dat we een cirkeldiagram willen en bepalen de positie ervan op het werkblad.

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

De methode `Add()` accepteert parameters voor het grafiektype (in dit geval, `ChartType.Pie`) en de locatie ervan op het werkblad. De getallen geven de rij- en kolomposities aan.

## Stap 5: Pas het uiterlijk van de grafiek aan

Een cirkeldiagram is niet compleet zonder wat aanpassingen! Laten we het diagram visueel aantrekkelijker maken door de kleuren, labels en titel aan te passen.

### Grafiektitel instellen
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

We stellen de kleurverloopvulling in voor het tekengebied en verbergen de rand voor een nettere weergave.

## Stap 6: Grafiekgegevens definiëren

Het is tijd om de grafiek aan onze gegevens te koppelen. `NSeries` Eigenschap van het diagram koppelt de verkoopcijfers en regio's aan het cirkeldiagram.

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

De eerste regel geeft aan dat we de verkoopgegevens uit de cellen gebruiken `B2:B8`We vertellen de grafiek ook om de regionamen van `A2:A8` als categorielabels.

## Stap 7: Gegevenslabels toevoegen

Door labels rechtstreeks aan de diagramsegmenten toe te voegen, wordt het gemakkelijker te begrijpen. Laten we de regionamen en verkoopwaarden opnemen in de segmenten van het cirkeldiagram.

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

Laten we tot slot het grafiekgedeelte en de legenda de laatste hand leggen. Dit verbetert de algehele presentatie van de grafiek.

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

Ten slotte slaan we de werkmap op in een Excel-bestand. U kunt de uitvoermap en bestandsnaam naar wens opgeven.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## Conclusie

Het maken van een cirkeldiagram met Aspose.Cells voor .NET is een eenvoudig en aanpasbaar proces. Door deze handleiding te volgen, kunt u in slechts een paar stappen een professioneel ogende grafiek genereren die waardevolle inzichten biedt. Of het nu voor zakelijke rapportages of educatieve doeleinden is, het beheersen van het maken van grafieken zal uw Excel-automatiseringsvaardigheden verbeteren. Onthoud dat Aspose.Cells de flexibiliteit biedt die u nodig hebt om moeiteloos verbluffende, datagestuurde Excel-bestanden te maken.

## Veelgestelde vragen

### Kan ik andere typen grafieken maken met Aspose.Cells voor .NET?
Ja! Aspose.Cells ondersteunt verschillende grafiektypen, waaronder staafdiagrammen, lijndiagrammen en spreidingsdiagrammen.

### Heb ik een betaalde licentie nodig om Aspose.Cells voor .NET te gebruiken?
Je kunt de gratis versie gebruiken met enkele beperkingen. Voor alle functies heb je een licentie nodig, die je kunt kopen. [hier](https://purchase.aspose.com/buy).

### Kan ik de grafiek exporteren naar formaten zoals PDF of afbeeldingen?
Absoluut! Met Aspose.Cells kun je grafieken exporteren naar verschillende formaten, waaronder PDF en PNG.

### Is het mogelijk om elke taartpunt met verschillende kleuren te stylen?
Ja, u kunt verschillende kleuren op elk segment toepassen door de `IsColorVaried` eigendom van `true`, zoals getoond in de tutorial.

### Kan ik het genereren van meerdere grafieken in één werkmap automatiseren?
Ja, u kunt zoveel grafieken maken en aanpassen als u nodig hebt in één Excel-bestand.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}