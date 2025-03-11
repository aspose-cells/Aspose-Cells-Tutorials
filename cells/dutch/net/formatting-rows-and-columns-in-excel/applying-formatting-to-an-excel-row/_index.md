---
title: Opmaak op een Excel-rij programmatisch toepassen
linktitle: Opmaak op een Excel-rij programmatisch toepassen
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u opmaak programmatisch toepast op een Excel-rij met Aspose.Cells voor .NET. Deze gedetailleerde, stapsgewijze handleiding behandelt alles van uitlijning tot randen.
weight: 11
url: /nl/net/formatting-rows-and-columns-in-excel/applying-formatting-to-an-excel-row/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Opmaak op een Excel-rij programmatisch toepassen

## Invoering
In deze tutorial laten we zien hoe je opmaak op een Excel-rij programmatisch toepast met Aspose.Cells voor .NET. We behandelen alles van het instellen van de omgeving tot het toepassen van verschillende opmaakopties zoals lettertypekleur, uitlijning en randen, terwijl we het simpel en boeiend houden. Laten we beginnen!
## Vereisten
Voordat we beginnen, zorgen we ervoor dat je alles hebt wat je nodig hebt om deze tutorial te volgen. Dit heb je nodig:
1.  Aspose.Cells voor .NET-bibliotheek – U kunt het downloaden van de[Aspose.Cells voor .NET downloadpagina](https://releases.aspose.com/cells/net/).
2. IDE – Elke .NET-ontwikkelomgeving, zoals Visual Studio.
3. Basiskennis van C# – U moet bekend zijn met de programmeertaal C# en met het werken met .NET-toepassingen.
Zorg ervoor dat u ook de nieuwste versie van Aspose.Cells installeert. U kunt deze rechtstreeks downloaden of via NuGet Package Manager in Visual Studio.
## Pakketten importeren
Zorg er allereerst voor dat u de benodigde pakketten importeert. Dit is essentieel om toegang te krijgen tot de functionaliteit die nodig is voor het werken met Excel-bestanden en het programmatisch toepassen van stijlen.
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Nu de instellingen zijn voltooid, kunnen we beginnen met het spannende gedeelte: het opmaken van rijen!
In deze sectie zullen we elke stap van het proces uiteenzetten. Elke stap wordt vergezeld door codefragmenten en een gedetailleerde uitleg, dus zelfs als u nieuw bent met Aspose.Cells, kunt u het gemakkelijk volgen.
## Stap 1: Werkmap en werkblad instellen
Voordat u opmaak toepast, moet u een exemplaar van de werkmap maken en het eerste werkblad openen. Dit is alsof u een leeg canvas opent voordat u begint met schilderen.
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
// Maak een map aan als deze nog niet bestaat.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Een werkmapobject instantiëren
Workbook workbook = new Workbook();
// De referentie van het eerste (standaard) werkblad verkrijgen door de index van het werkblad door te geven
Worksheet worksheet = workbook.Worksheets[0];
```
Hier maken we een nieuw werkmapobject en halen het eerste werkblad op. Dit is het werkblad waarop we onze opmaak toepassen.
## Stap 2: Een stijl maken en aanpassen
Nu u uw werkblad gereed hebt, is de volgende stap het definiëren van de stijlen die u op de rij wilt toepassen. We beginnen met het maken van een nieuwe stijl en het instellen van eigenschappen zoals lettertypekleur, uitlijning en randen.
```csharp
// Een nieuwe stijl toevoegen aan de stijlen
Style style = workbook.CreateStyle();
// De verticale uitlijning van de tekst in cel "A1" instellen
style.VerticalAlignment = TextAlignmentType.Center;
// De horizontale uitlijning van de tekst in cel "A1" instellen
style.HorizontalAlignment = TextAlignmentType.Center;
// De letterkleur van de tekst in cel "A1" instellen
style.Font.Color = Color.Green;
```
In dit onderdeel stellen we de uitlijning van de tekst in de rij in (zowel verticaal als horizontaal) en specificeren we de letterkleur. Dit is waar u begint met het definiëren hoe de inhoud visueel in uw Excel-sheet zal verschijnen.
## Stap 3: Krimpen om te passen toepassen
Soms kan de tekst in een cel te lang zijn, waardoor deze overloopt. Een handige truc is om de tekst te verkleinen zodat deze in de cel past en leesbaar blijft.
```csharp
// De tekst verkleinen zodat deze in de cel past
style.ShrinkToFit = true;
```
 Met`ShrinkToFit`zorgt u ervoor dat lange tekst wordt aangepast aan de celgrenzen, waardoor uw Excel-werkblad er overzichtelijker uitziet.
## Stap 4: Randen voor de rij instellen
Om uw rijen te laten opvallen, is het toepassen van randen een geweldige optie. In dit voorbeeld passen we de onderste rand aan, door de kleur op rood en de stijl op medium te zetten.
```csharp
// De onderste randkleur van de cel instellen op rood
style.Borders[BorderType.BottomBorder].Color = Color.Red;
// Het type onderste rand van de cel instellen op medium
style.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Medium;
```
Met randen kunt u inhoud visueel scheiden, waardoor uw gegevens beter leesbaar en aantrekkelijker worden.
## Stap 5: Een StyleFlag-object maken
 De`StyleFlag`object vertelt Aspose.Cells welke aspecten van de stijl moeten worden toegepast. Dit geeft u nauwkeurige controle over wat wordt toegepast en zorgt ervoor dat alleen de beoogde opmaak wordt ingesteld.
```csharp
// Stijlvlag maken
StyleFlag styleFlag = new StyleFlag();
styleFlag.HorizontalAlignment = true;
styleFlag.VerticalAlignment = true;
styleFlag.ShrinkToFit = true;
styleFlag.Borders = true;
styleFlag.FontColor = true;
```
In dit geval geven we aan dat horizontale en verticale uitlijning, tekstkleur, tekstverkleining en randen allemaal moeten worden toegepast.
## Stap 6: Ga naar de gewenste rij
Zodra de stijl is gemaakt, is de volgende stap om toegang te krijgen tot de rij waar we de opmaak willen toepassen. In dit voorbeeld formatteren we de eerste rij (rij-index 0).
```csharp
// Toegang krijgen tot een rij uit de verzameling Rijen
Row row = worksheet.Cells.Rows[0];
```
Hier halen we de eerste rij van het werkblad op. U kunt de index wijzigen om elke andere rij op te maken.
## Stap 7: Pas de stijl toe op de rij
 Ten slotte is het tijd om de stijl op de rij toe te passen! We gebruiken de`ApplyStyle` Methode om de gedefinieerde stijl toe te passen op de geselecteerde rij.
```csharp
// Het Style-object toewijzen aan de Style-eigenschap van de rij
row.ApplyStyle(style, styleFlag);
```
De stijl wordt nu op de hele rij toegepast, waardoor uw gegevens er precies zo uitzien als u voor ogen had.
## Stap 8: Sla de werkmap op
Zodra u klaar bent met het toepassen van de opmaak, moet u de werkmap opslaan in een Excel-bestand. Dit is hetzelfde als op 'Opslaan' klikken in Excel nadat u uw wijzigingen hebt aangebracht.
```csharp
// Het Excel-bestand opslaan
workbook.Save(dataDir + "book1.out.xls");
```
U hebt nu een volledig opgemaakt Excel-bestand opgeslagen in de door u opgegeven map!
## Conclusie
Dat is alles! In slechts een paar eenvoudige stappen hebt u geleerd hoe u opmaak op een Excel-rij programmatisch kunt toepassen met Aspose.Cells voor .NET. Van het instellen van tekstuitlijning tot het aanpassen van randen, deze tutorial behandelde de basisprincipes die u zullen helpen om professionele en visueel aantrekkelijke Excel-rapporten programmatisch te maken. 
Aspose.Cells biedt een breed scala aan mogelijkheden en de hier getoonde methoden kunnen eenvoudig worden uitgebreid om complexere stijlen en opmaak toe te passen op uw Excel-bestanden. Dus waarom zou u het niet eens proberen en uw gegevens laten opvallen?
## Veelgestelde vragen
### Kan ik verschillende stijlen toepassen op afzonderlijke cellen in een rij?  
Ja, u kunt verschillende stijlen op afzonderlijke cellen toepassen door er rechtstreeks via de`Cells` verzameling in plaats van de stijl op de hele rij toe te passen.
### Is het mogelijk om voorwaardelijke opmaak toe te passen met Aspose.Cells?  
Absoluut! Aspose.Cells ondersteunt voorwaardelijke opmaak, zodat u regels kunt definiëren op basis van celwaarden.
### Hoe kan ik opmaak toepassen op meerdere rijen?  
 U kunt door meerdere rijen heen lussen met behulp van een`for` herhalen en dezelfde stijl op elke rij afzonderlijk toepassen.
### Ondersteunt Aspose.Cells het toepassen van stijlen op hele kolommen?  
 Ja, net als bij rijen kunt u kolommen openen met behulp van de`Columns` verzamelen en er stijlen op toepassen.
### Kan ik Aspose.Cells gebruiken met .NET Core-toepassingen?  
Ja, Aspose.Cells is volledig compatibel met .NET Core, zodat u het op verschillende platforms kunt gebruiken.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
