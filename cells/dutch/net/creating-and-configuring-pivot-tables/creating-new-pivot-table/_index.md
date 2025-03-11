---
title: Een nieuwe draaitabel programmatisch maken in .NET
linktitle: Een nieuwe draaitabel programmatisch maken in .NET
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u programmatisch een draaitabel in .NET kunt maken met Aspose.Cells met onze stapsgewijze handleiding. Analyseer uw gegevens efficiënt.
weight: 13
url: /nl/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Een nieuwe draaitabel programmatisch maken in .NET

## Invoering
Het maken van een draaitabel kan een intimiderende taak lijken, vooral als u het programmatisch doet. Maar vrees niet! Met Aspose.Cells voor .NET is het samenstellen van een draaitabel niet alleen eenvoudig, maar ook behoorlijk krachtig voor gegevensanalyse. In deze tutorial begeleiden we u stapsgewijs bij het maken van een nieuwe draaitabel in een .NET-toepassing. Of u nu gegevens toevoegt voor verkoop, sport of een andere bedrijfsmetriek, deze gids helpt u om uw draaitabellen in een mum van tijd operationeel te krijgen.

## Vereisten
Voordat we erin duiken, zorgen we ervoor dat alles klaar is om te gaan. Dit is wat je moet doen:

1. Installeer .NET Framework: Zorg ervoor dat u het .NET Framework op uw machine hebt geïnstalleerd. Aspose.Cells ondersteunt verschillende versies, maar het is het beste om de nieuwste te gebruiken.
2.  Aspose.Cells-bibliotheek: U moet de Aspose.Cells-bibliotheek hebben. U kunt[download het hier](https://releases.aspose.com/cells/net/)of krijg een[tijdelijke licentie](https://purchase.aspose.com/temporary-license/) voor evaluatie.
3. IDE-installatie: Zorg dat u een C#-compatibele IDE bij de hand hebt, zoals Visual Studio, waar u een nieuw project kunt starten.
4. Basiskennis van C#: Kennis van C#-programmering helpt u de cursus te volgen zonder dat u te veel vastloopt.

Ben je helemaal klaar? Geweldig! Laten we beginnen met het importeren van de benodigde pakketten.

## Pakketten importeren
Allereerst moet u de vereiste namespaces importeren in uw C#-project. Open uw C#-bestand en voeg het volgende toe met behulp van richtlijnen:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Met deze naamruimten krijgt u toegang tot de werkmap-, werkblad- en draaitabelfunctionaliteiten die we in deze zelfstudie gebruiken.

## Stap 1: Een werkmapobject maken
Het maken van een werkboek is het begin van uw reis. Laten we beginnen met het instantiëren van een nieuw werkboek en het openen van het eerste werkblad.

```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
// Een werkmapobject instantiëren
Workbook workbook = new Workbook();

// De referentie van het nieuw toegevoegde werkblad verkrijgen
Worksheet sheet = workbook.Worksheets[0];
```

 In deze stap maken we een`Workbook`exemplaar dat ons Excel-bestand vertegenwoordigt en pak het allereerste werkblad, dat onze speeltuin voor de draaitabel zal zijn.

## Stap 2: Gegevens in cellen invoegen
Laten we vervolgens ons werkblad vullen met wat voorbeeldgegevens. We gaan rijen invoeren voor verschillende sporten, kwartalen en verkoopcijfers om onze draaitabel iets te geven om samen te vatten.

```csharp
Cells cells = sheet.Cells;

// De waarde instellen op de cellen
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

// Vullen van datacell = cellen["A2"];
cell.PutValue("Golf");
// ... Meer gegevensinvoeren
```

Hier definiëren we onze kolomkoppen en voegen we waarden toe onder elke kop. Deze gegevens fungeren als bron voor onze draaitabel, dus zorg ervoor dat deze georganiseerd is! Volg dit blok en je creëert een uitgebreide dataset.

## Stap 3: Een draaitabel toevoegen
Nu onze gegevens gereed zijn, is het tijd om de draaitabel te maken. We gebruiken de draaitabelcollectie van het werkblad om onze nieuwe draaitabel toe te voegen.

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// Een draaitabel toevoegen aan het werkblad
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

In dit fragment voegen we een draaitabel toe aan het werkblad die verwijst naar ons gegevensbereik (in dit geval cellen A1 tot en met C8). We plaatsen de draaitabel vanaf cel E3 en noemen deze "PivotTable2". Vrij eenvoudig, toch?

## Stap 4: Pas de draaitabel aan
Nu we onze draaitabel hebben, gaan we deze aanpassen om zinvolle samenvattingen te tonen. We kunnen bepalen wat er in de rijen, kolommen en gegevensgebieden van de draaitabel verschijnt.

```csharp
// Toegang krijgen tot het exemplaar van de nieuw toegevoegde draaitabel
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

// Totalen voor rijen niet meer weergeven.
pivotTable.RowGrand = false;

// Het eerste veld naar het rijgebied slepen.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

// Het tweede veld naar het kolomgebied slepen.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

// Het derde veld naar het gegevensgebied slepen.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

In deze stap vertellen we de draaitabel om de eindtotalen voor rijen te verbergen en specificeren we vervolgens welke velden in de rij-, kolom- en gegevensgebieden komen. De sportnamen vullen de rijen, de kwartalen vullen de kolommen en de verkoopcijfers leveren de samenvattingen.

## Stap 5: Sla de werkmap op
Tot slot willen we ons nieuwe werkboek opslaan, zodat we de vruchten van onze arbeid kunnen zien.

```csharp
// Het Excel-bestand opslaan
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

Geef gewoon een juist pad op, dan wordt de uitvoer van uw draaitabel opgeslagen in een Excel-bestand dat u kunt openen en bekijken.

## Conclusie
Het programmatisch maken van draaitabellen met Aspose.Cells voor .NET kan u aanzienlijk veel tijd besparen, vooral bij het werken met grote datasets. U hebt geleerd hoe u uw project instelt, benodigde pakketten importeert, gegevens vult en een aanpasbare draaitabel vanaf nul maakt. Dus de volgende keer dat u verdrinkt in cijfers, denk dan aan deze tutorial en laat Aspose.Cells het zware werk voor u doen.

## Veelgestelde vragen
### Wat is Aspose.Cells?
Aspose.Cells is een krachtige .NET-bibliotheek voor het programmatisch maken en beheren van Excel-spreadsheets.

### Is er een gratis proefversie voor Aspose.Cells?
 Ja, u kunt een gratis proefperiode krijgen[hier](https://releases.aspose.com/).

### Kan ik het uiterlijk van de draaitabel aanpassen?
Absoluut! U kunt de opmaak, lay-out en zelfs de stijlen van de draaitabel aanpassen aan uw behoeften.

### Waar kan ik meer voorbeelden en documentatie over Aspose.Cells vinden?
 U kunt de[documentatie](https://reference.aspose.com/cells/net/) voor uitgebreide handleidingen en voorbeelden.

### Hoe krijg ik ondersteuning voor Aspose.Cells?
 U kunt ondersteuning krijgen via de[Aspose-forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
