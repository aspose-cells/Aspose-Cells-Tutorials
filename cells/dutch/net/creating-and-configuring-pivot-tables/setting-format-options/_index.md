---
title: Instellen van opmaakopties van draaitabellen in .NET
linktitle: Instellen van opmaakopties van draaitabellen in .NET
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u Aspose.Cells voor .NET kunt gebruiken om moeiteloos draaitabellen te formatteren. Ontdek stapsgewijze technieken om uw gegevenspresentatie te verbeteren.
weight: 20
url: /nl/net/creating-and-configuring-pivot-tables/setting-format-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Instellen van opmaakopties van draaitabellen in .NET

## Invoering
Hebt u zich ooit overweldigd gevoeld door de enorme hoeveelheid data die u tot uw beschikking had? Of vond u het lastig om deze data op een duidelijke en inzichtelijke manier te presenteren? Zo ja, welkom aan boord! Vandaag duiken we in de wonderlijke wereld van draaitabellen in Excel met behulp van de Aspose.Cells-bibliotheek voor .NET. Draaitabellen kunnen de superhelden van datapresentatie zijn, door stapels getallen om te zetten in gestructureerde, inzichtelijke rapporten die het nemen van beslissingen een fluitje van een cent maken. Is dat niet een game changer?
## Vereisten
Voordat we in de tutorial duiken, zorgen we ervoor dat je alles hebt wat je nodig hebt om te slagen. Dit zijn de vereisten:
1. Basiskennis van C#: U moet een fundamenteel begrip hebben van de programmeertaal C#. Als u vertrouwd bent met de basis, bent u klaar om dit aan te pakken!
2. Visual Studio of een C# IDE: U hebt een geïntegreerde ontwikkelomgeving (IDE) nodig, zoals Visual Studio. Dit is waar de magie gebeurt. 
3. Aspose.Cells Library: Om de kracht van Aspose.Cells te benutten, moet u dit pakket downloaden. U kunt het eenvoudig vinden op de[Aspose.Cells Downloadpagina](https://releases.aspose.com/cells/net/).
4. Excel-bestand: Een voorbeeld-Excel-bestand is vereist om de tutorial te oefenen. Voel je vrij om een eenvoudige dataset in een Excel-sheet te maken (zoals "Book1.xls") voor deze oefening.
5. .NET Framework: Zorg ervoor dat .NET Framework op uw computer is geïnstalleerd.
Heb je dat allemaal? Fantastisch! Laten we nu naar onze eerste stap gaan.
## Pakketten importeren
Om de Aspose.Cells-bibliotheek te kunnen gebruiken, moeten we eerst de benodigde pakketten importeren. Dit doet u als volgt:
### Open uw project
Open uw Visual Studio (of een andere C# IDE die u gebruikt) en maak een nieuw project. Kies een Console Application omdat u hiermee het script eenvoudig kunt uitvoeren.
### Voeg Aspose.Cells-referentie toe
1. Klik met de rechtermuisknop op uw project in de Solution Explorer.
2. Selecteer NuGet-pakketten beheren.
3.  Typ in het zoekvak`Aspose.Cells` en installeer het.
Nu bent u klaar om de bibliotheek te importeren. U moet de volgende using-richtlijn aan het begin van uw codebestand toevoegen:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Met deze regel krijgt u toegang tot alle klassen en methoden die beschikbaar zijn in de Aspose.Cells-bibliotheek.
Nu de grond gelegd is, gaan we stap voor stap door elk onderdeel van het proces. We zullen bespreken hoe u verschillende opmaakopties voor een draaitabel effectief kunt instellen.
## Stap 1: Definieer uw documentendirectory
Eerst moet u het pad van uw documentdirectory instellen waar uw invoer-Excel-bestand zich bevindt. Deze regel code specificeert waar uw bestanden zich bevinden.
```csharp
string dataDir = "Your Document Directory";
```
 Vervangen`"Your Document Directory"` met het werkelijke pad waar uw "Book1.xls" bestand is opgeslagen. Dit helpt het programma te weten waar het moet zoeken naar het invoerbestand.
## Stap 2: Laad het sjabloonbestand
 Vervolgens laden we het Excel-bestand dat we willen bewerken. Dit doen we met behulp van de`Workbook` klas.
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Deze opdracht vertelt uw programma in feite dat het bestand 'Book1.xls' moet openen, zodat we met de gegevens kunnen werken.
## Stap 3: Ontvang het eerste werkblad
Nu we de werkmap geopend hebben, gaan we naar het werkblad met onze gegevens. 
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Hier openen we het eerste werkblad van de werkmap (omdat indexering bij nul begint). Als uw gegevens zich op een ander werkblad bevinden, past u eenvoudig de index aan.
## Stap 4: Toegang krijgen tot de draaitabel
Draaitabellen zijn krachtig, maar eerst moeten we degene pakken waarmee we willen werken. Ervan uitgaande dat u de index van uw draaitabel kent, leest u hier hoe u deze kunt openen.
```csharp
int pivotindex = 0;
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
In dit geval openen we de eerste draaitabel (index 0) in het werkblad. 
## Stap 5: Stel de draaitabeltotalen voor rijen in
Laten we beginnen met formatteren! We kunnen configureren of we eindtotalen voor rijen in onze draaitabel willen weergeven.
```csharp
pivotTable.RowGrand = true;
```
 Deze eigenschap instellen op`true` geeft de eindtotalen weer onderaan elke rij in uw draaitabel. Het is een eenvoudige maar effectieve manier om samenvattingen te geven.
## Stap 6: Stel de draaitabeltotalen voor kolommen in
Net zoals we eindtotalen voor rijen instellen, kunnen we dit ook voor kolommen doen.
```csharp
pivotTable.ColumnGrand = true;
```
Als u dit inschakelt, worden de totalen aan de rechterkant van elke kolom weergegeven. Nu is uw draaitabel een kampioen in het samenvatten van gegevens in beide richtingen!
## Stap 7: Aangepaste tekenreeks weergeven voor null-waarden
Een vaak over het hoofd gezien detail is het verwerken van null-waarden. U wilt misschien dat een specifieke string verschijnt in cellen met null-waarden. 
```csharp
pivotTable.DisplayNullString = true;
pivotTable.NullString = "null";
```
Hiermee wordt de draaitabel zo ingesteld dat er 'null' wordt weergegeven wanneer er een lege cel wordt aangetroffen. Dit zorgt voor meer duidelijkheid en consistentie in uw rapporten.
## Stap 8: De draaitabelindeling instellen
Draaitabellen kunnen verschillende lay-outs hebben en we kunnen ze aanpassen op basis van onze vereisten. Laten we de lay-out instellen op "DownThenOver".
```csharp
pivotTable.PageFieldOrder = PrintOrderType.DownThenOver;
```
Met deze opdracht past u de volgorde aan waarin de velden in uw rapport worden weergegeven, waardoor het rapport beter leesbaar wordt. 
## Stap 9: Het Excel-bestand opslaan
Nadat u al deze mooie aanpassingen hebt gemaakt, moet u uw wijzigingen opslaan in een Excel-bestand. 
```csharp
workbook.Save(dataDir + "output.xls");
```
Deze regel slaat de gewijzigde werkmap op als “output.xls” in de door u opgegeven map. 
En zo hebt u uw draaitabel uitgebreid met fantastische opmaakopties!
## Conclusie
Wauw, we hebben samen een hele reis afgelegd, nietwaar? Door de mogelijkheden van de Aspose.Cells-bibliotheek voor .NET te benutten, kunt u moeiteloos transformeren hoe uw gegevens eruitzien en zich gedragen in Excel. We hebben behandeld hoe u een werkmap laadt, een draaitabel opent en opmaakt, en alles tot een hoogtepunt brengt door onze wijzigingen op te slaan. Gegevens hoeven niet saai en eentonig te zijn; met een paar aanpassingen kunnen ze schitterend schitteren.
## Veelgestelde vragen
### Wat is een draaitabel?
Draaitabellen zijn een Excel-functie waarmee u gegevens dynamisch kunt samenvatten en analyseren.
### Moet ik Excel geïnstalleerd hebben om Aspose.Cells te kunnen gebruiken?
Nee, Aspose.Cells is een zelfstandige bibliotheek waarvoor Excel niet geïnstalleerd hoeft te zijn.
### Kan ik draaitabellen maken met Aspose.Cells?
Ja, met Aspose.Cells kunt u draaitabellen maken, wijzigen en manipuleren.
### Is Aspose.Cells gratis?
Aspose.Cells is een betaalde bibliotheek, maar er is een gratis proefversie beschikbaar.
### Waar kan ik meer Aspose.Cells-documentatie vinden?
 Bekijk de[Aspose.Cells-documentatie](https://reference.aspose.com/cells/net/) voor uitgebreide handleidingen en voorbeelden.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
