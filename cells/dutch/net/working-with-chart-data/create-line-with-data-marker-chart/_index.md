---
"description": "Leer hoe je een lijndiagram met gegevensmarkeringen maakt in Excel met Aspose.Cells voor .NET. Volg deze stapsgewijze handleiding om eenvoudig diagrammen te genereren en aan te passen."
"linktitle": "Lijn maken met gegevensmarkeringsgrafiek"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Lijn maken met gegevensmarkeringsgrafiek"
"url": "/nl/net/working-with-chart-data/create-line-with-data-marker-chart/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Lijn maken met gegevensmarkeringsgrafiek

## Invoering

Heb je je ooit afgevraagd hoe je programmatisch prachtige grafieken in Excel kunt maken? Maak je klaar, want vandaag duiken we in het maken van een lijndiagram met gegevensmarkeringen met Aspose.Cells voor .NET. Deze tutorial begeleidt je door elke stap, zodat je een gedegen kennis hebt van het maken van grafieken, zelfs als je net begint met Aspose.Cells.

## Vereisten

Voordat we beginnen, zorg ervoor dat je alles klaar hebt om alles soepel te kunnen volgen.

1. Aspose.Cells voor .NET-bibliotheek – Deze moet je installeren. Je kunt hem hier downloaden. [hier](https://releases.aspose.com/cells/net/).
2. .NET Framework – Zorg ervoor dat uw ontwikkelomgeving is ingesteld met de nieuwste versie van .NET.
3. IDE (Integrated Development Environment) – Visual Studio wordt aanbevolen.
4. Een geldige Aspose.Cells-licentie – Als u deze niet hebt, kunt u een nieuwe aanvragen [tijdelijke licentie](https://purchase.aspose.com/temporary-license/) of bekijk hun [gratis proefperiode](https://releases.aspose.com/).

Klaar om te gaan? Laten we het eens bekijken!

## Noodzakelijke pakketten importeren

Zorg er allereerst voor dat u de volgende naamruimten in uw project importeert. Deze bieden de benodigde klassen en methoden om uw grafiek te maken.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Zodra je dat onder de knie hebt, kunnen we beginnen met coderen!

## Stap 1: Uw werkmap en werkblad instellen

Allereerst moet u een nieuwe werkmap maken en het eerste werkblad openen.

```csharp
//Uitvoermap
static string outputDir = "Your Document Directory";
		
// Een werkmap instantiëren
Workbook workbook = new Workbook();

// Toegang tot het eerste werkblad
Worksheet worksheet = workbook.Worksheets[0];
```

Beschouw de werkmap als uw Excel-bestand en het werkblad als het specifieke blad daarin. In dit geval werken we met het eerste blad.

## Stap 2: Vul het werkblad met gegevens

Nu we ons werkblad hebben, vullen we het met wat gegevens. We creëren willekeurige datapunten voor twee reeksen waarden.

```csharp
// Kolommentitel instellen
worksheet.Cells[0, 0].Value = "X";
worksheet.Cells[0, 1].Value = "Y";

// Willekeurige gegevens voor het genereren van de grafiek
Random R = new Random();

// Maak willekeurige gegevens en sla ze op in de cellen
for (int i = 1; i < 21; i++)
{
    worksheet.Cells[i, 0].Value = i;
    worksheet.Cells[i, 1].Value = 0.8;
}

for (int i = 21; i < 41; i++)
{
    worksheet.Cells[i, 0].Value = i - 20;
    worksheet.Cells[i, 1].Value = 0.9;
}
```

Hier gebruiken we willekeurige getallen om gegevens te simuleren, maar in de praktijk kunt u de gegevens vullen met werkelijke waarden uit uw dataset.

## Stap 3: Voeg de grafiek toe aan het werkblad

Vervolgens voegen we de grafiek toe aan het werkblad en kiezen we het type: in dit geval een lijngrafiek met gegevensmarkeringen.

```csharp
// Voeg een grafiek toe aan het werkblad
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

// Toegang tot de nieuw gemaakte grafiek
Chart chart = worksheet.Charts[idx];
```

Dit fragment voegt een lijndiagram met gegevensmarkeringen toe aan het werkblad en plaatst het in een specifiek bereik (1, 3 tot 20, 20). Vrij eenvoudig, toch?

## Stap 4: Pas het uiterlijk van de grafiek aan

Zodra de grafiek is gemaakt, kunt u deze naar wens stylen. Laten we de achtergrond, titel en grafiekstijl aanpassen.

```csharp
// Grafiekstijl instellen
chart.Style = 3;

// Stel de waarde voor automatisch schalen in op waar
chart.AutoScaling = true;

// Voorgrondkleur instellen op wit
chart.PlotArea.Area.ForegroundColor = Color.White;

// Eigenschappen van grafiektitel instellen
chart.Title.Text = "Sample Chart";

// Grafiektype instellen
chart.Type = ChartType.LineWithDataMarkers;
```

Hier geven we de grafiek een overzichtelijk uiterlijk door een witte achtergrond in te stellen, automatisch te schalen en een betekenisvolle titel te geven.

## Stap 5: Definieer series en zet datapunten uit

Nu ons diagram er goed uitziet, moeten we de gegevensreeksen definiëren die we willen uitzetten.

```csharp
// Eigenschappen van de categorie-astitel instellen
chart.CategoryAxis.Title.Text = "Units";

// Definieer twee reeksen voor de grafiek
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

Deze reeksen komen overeen met de bereiken van datapunten die we eerder hebben ingevuld.

## Stap 6: Kleuren toevoegen en seriemarkeringen aanpassen

Laten we deze grafiek nog aantrekkelijker maken door aangepaste kleuren toe te voegen aan onze gegevensmarkeringen.

```csharp
// Eerste serie aanpassen
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

// Pas de tweede serie aan
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

Door de kleuren aan te passen, maakt u de grafiek niet alleen functioneel, maar ook visueel aantrekkelijk!

## Stap 7: Stel X- en Y-waarden in voor elke reeks

Laten we ten slotte de X- en Y-waarden aan elk van onze reeksen toewijzen.

```csharp
// Stel X- en Y-waarden van de eerste reeks in
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

// Stel X- en Y-waarden van de tweede reeks in
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

De waarden zijn gebaseerd op de gegevens die we in stap 2 hebben ingevuld.

## Stap 8: Sla de werkmap op

Nu alles is ingesteld, slaan we de werkmap op, zodat we de grafiek in actie kunnen zien.

```csharp
// Sla de werkmap op
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

En klaar! Je hebt zojuist een lijndiagram met gegevensmarkeringen gemaakt met Aspose.Cells voor .NET.

## Conclusie

Het programmatisch maken van grafieken in Excel lijkt misschien een hele klus, maar met Aspose.Cells voor .NET is het net zo eenvoudig als het volgen van een stapsgewijs recept. Van het instellen van je werkmap tot het aanpassen van de weergave van de grafiek, deze krachtige bibliotheek regelt het allemaal. Of je nu rapporten, dashboards of datavisualisaties maakt, met Aspose.Cells doe je het in een handomdraai.

## Veelgestelde vragen

### Kan ik de grafiek verder aanpassen?  
Absoluut! Aspose.Cells biedt talloze aanpassingsmogelijkheden, van lettertypen tot rasterlijnen en meer.

### Heb ik een licentie nodig om Aspose.Cells te gebruiken?  
Ja, voor volledige functionaliteit is een licentie vereist. U kunt een [tijdelijke licentie](https://purchase.aspose.com/temporary-license/) of begin met een [gratis proefperiode](https://releases.aspose.com/).

### Hoe kan ik meer gegevensreeksen toevoegen?  
Voeg eenvoudig extra series toe met behulp van de `NSeries.Add` methode, waarbij de celbereiken voor de nieuwe gegevens worden opgegeven.

### Kan ik het diagram exporteren als afbeelding?  
Ja, u kunt grafieken rechtstreeks als afbeeldingen exporteren met behulp van de `Chart.ToImage` methode.

### Ondersteunt Aspose.Cells 3D-diagrammen?  
Ja, Aspose.Cells ondersteunt een breed scala aan grafiektypen, waaronder 3D-grafieken.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}