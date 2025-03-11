---
title: Pijlpunt toevoegen aan vorm in Excel
linktitle: Pijlpunt toevoegen aan vorm in Excel
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u pijlpunten toevoegt aan vormen in Excel met Aspose.Cells voor .NET. Verbeter uw spreadsheets met deze stapsgewijze handleiding.
weight: 10
url: /nl/net/excel-shapes-controls/add-arrow-head-to-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pijlpunt toevoegen aan vorm in Excel

## Invoering
Het maken van visueel aantrekkelijke Excel-spreadsheets is cruciaal, vooral wanneer u gegevens op een duidelijke en informatieve manier presenteert. Een manier om dergelijke presentaties te verbeteren, is door vormen toe te voegen, zoals lijnen met pijlpunten. Deze gids leidt u door het toevoegen van pijlpunten aan vormen in een Excel-werkmap met behulp van Aspose.Cells voor .NET. Of u nu een ontwikkelaar bent die rapporten wil automatiseren of gewoon iemand die geïnteresseerd is in het verbeteren van uw Excel-spreadsheets, dit artikel biedt u de inzichten die u nodig hebt.
## Vereisten
Voordat we in de tutorial duiken, zorgen we ervoor dat je alles klaar hebt staan. Dit is wat je nodig hebt:
1. Basiskennis van C# en .NET: Als u de basisbeginselen van programmeren in C# begrijpt, kunt u soepeler door de codevoorbeelden navigeren.
2.  Aspose.Cells voor .NET-bibliotheek: Zorg ervoor dat u de Aspose.Cells-bibliotheek hebt geïnstalleerd. U kunt deze ophalen via de[downloadpagina](https://releases.aspose.com/cells/net/).
3. Ontwikkelomgeving: Een IDE zoals Visual Studio om uw .NET-toepassingen uit te voeren en te testen.
4.  Een gratis proefversie of een licentie: Als u dat nog niet hebt gedaan, overweeg dan om een gratis proefversie of licentie te downloaden.[gratis proefperiode](https://releases.aspose.com/) of het verwerven van een[tijdelijke licentie](https://purchase.aspose.com/temporary-license/) voor Aspose.Cells.
5. Kennis van Excel: Als u weet hoe u door Excel kunt navigeren, begrijpt u beter hoe de vormen en lijnen interacteren met uw gegevens.
## Pakketten importeren
Om Aspose.Cells te gebruiken, moet u de benodigde namespaces importeren in uw C#-project. U kunt dit doen door de volgende regel bovenaan uw codebestand toe te voegen:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Deze naamruimten bieden toegang tot de essentiële klassen en methoden die nodig zijn om Excel-bestanden te bewerken en vormen te maken. 

Laten we het proces nu opsplitsen in eenvoudige, beheersbare stappen. 
## Stap 1: Stel uw projectomgeving in
Open eerst uw IDE (zoals Visual Studio) en maak een nieuw C#-project. U kunt een Console Application kiezen, omdat we hiermee de code rechtstreeks vanuit de terminal kunnen uitvoeren.

Zorg er vervolgens voor dat Aspose.Cells wordt gerefereerd in uw project. Als u NuGet gebruikt, kunt u het eenvoudig toevoegen via de Package Manager Console met de volgende opdracht:
```bash
Install-Package Aspose.Cells
```
## Stap 2: Definieer de documentdirectory
Nu is het tijd om te definiëren waar uw documenten worden opgeslagen. U wilt een directory maken om uw werkmap in te bewaren. Dit is hoe u dit in code kunt doen:
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
// Maak een map aan als deze nog niet bestaat.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
```
 Zorg ervoor dat je verandert`"Your Document Directory"` naar een geschikt pad op uw systeem waar u schrijfrechten hebt.
## Stap 3: Maak de werkmap en het werkblad
### Een nieuwe werkmap instantiëren
Vervolgens moet u een werkboek maken en er een werkblad aan toevoegen. Dit is zo eenvoudig als:
```csharp
// Een nieuwe werkmap maken.
Workbook workbook = new Workbook();
```
### Toegang tot het eerste werkblad
Laten we nu het eerste werkblad pakken, waar we onze vormen aan gaan toevoegen.
```csharp
// Pak het eerste werkblad uit het boek.
Worksheet worksheet = workbook.Worksheets[0];
```
## Stap 4: Voeg een lijnvorm toe
Laten we nu een regel aan ons werkblad toevoegen:
```csharp
// Voeg een regel toe aan het werkblad
Aspose.Cells.Drawing.LineShape line2 = worksheet.Shapes.AddLine(7, 0, 1, 0, 85, 250);
```
In dit voorbeeld maken we een lijnvorm die begint bij de coördinaten (7, 0) en eindigt bij (85, 250). U kunt deze getallen aanpassen om de grootte en positie van uw lijn naar wens aan te passen.
## Stap 5: Pas de lijn aan
U kunt de lijn visueel aantrekkelijker maken door de kleur en het gewicht te veranderen. Dit doet u als volgt:
```csharp
// Stel de lijnkleur in
line2.Line.FillType = FillType.Solid;
line2.Line.SolidFill.Color = Color.Blue;
// Stel de dikte van de lijn in.
line2.Line.Weight = 3;
```
In dit geval stellen we de lijn in op een effen blauwe vulling en een dikte van 3. Experimenteer met verschillende kleuren en diktes om te ontdekken wat voor jou werkt!
## Stap 6: Wijzig de plaatsing van de lijn
Vervolgens moet u instellen hoe de lijn in het werkblad wordt geplaatst. Voor dit voorbeeld maken we het vrij zwevend:
```csharp
// Plaatsing instellen.
line2.Placement = PlacementType.FreeFloating;
```
## Stap 7: Pijlpunten toevoegen
Hier is het spannende gedeelte! Laten we pijlpunten toevoegen aan beide uiteinden van onze lijn:
```csharp
// Stel de lijnpijlen in.
line2.Line.EndArrowheadWidth = MsoArrowheadWidth.Medium;
line2.Line.EndArrowheadStyle = MsoArrowheadStyle.Arrow;
line2.Line.EndArrowheadLength = MsoArrowheadLength.Medium;
line2.Line.BeginArrowheadStyle = MsoArrowheadStyle.ArrowDiamond;
line2.Line.BeginArrowheadLength = MsoArrowheadLength.Medium;
```
Deze code stelt het einde van de regel in op een pijl van gemiddelde breedte, terwijl het begin een pijl in ruitvorm krijgt. U kunt deze eigenschappen aanpassen op basis van uw ontwerpvoorkeuren.
## Stap 8: Maak rasterlijnen onzichtbaar
Soms kunnen rasterlijnen de visuele aantrekkingskracht van een grafiek of vorm belemmeren. Om ze uit te schakelen, gebruikt u de volgende regel:
```csharp
// Maak de rasterlijnen in het eerste werkblad onzichtbaar.
workbook.Worksheets[0].IsGridlinesVisible = false;
```
## Stap 9: Sla het Excel-bestand op
Eindelijk is het tijd om uw werk op te slaan:
```csharp
// Sla het Excel-bestand op.
workbook.Save(dataDir + "book1.out.xlsx");
```
 Zorg ervoor dat de bestandsnaam eindigt met de juiste Excel-bestandsextensie, zoals`.xlsx` in dit geval. 

## Conclusie
Het toevoegen van pijlpunten aan vormen in Excel met Aspose.Cells voor .NET kan de visuele aantrekkingskracht van uw spreadsheets aanzienlijk verbeteren. Met slechts een paar regels code kunt u professioneel ogende diagrammen maken die informatie duidelijk communiceren. Of u nu rapporten automatiseert of gewoon visuele hulpmiddelen maakt, het beheersen van deze technieken zal uw presentaties ongetwijfeld laten opvallen.
## Veelgestelde vragen
### Kan ik de kleur van de pijlpunten veranderen?
Ja, u kunt de kleur van de lijnen en vormen, inclusief de pijlpunten, aanpassen door de`SolidFill.Color` eigendom.
### Is Aspose.Cells gratis te gebruiken?
 Aspose.Cells is een betaald product, maar biedt een[gratis proefperiode](https://releases.aspose.com/) die u kunt gebruiken om de functies ervan te testen.
### Moet ik nog andere bibliotheken installeren?
Nee, Aspose.Cells is een standalone bibliotheek. Zorg ervoor dat u er correct naar verwijst in uw project.
### Kan ik naast lijnen ook andere vormen maken?
Absoluut! Aspose.Cells ondersteunt verschillende vormen, waaronder rechthoeken, ellipsen en meer.
### Waar kan ik aanvullende documentatie vinden?
 U kunt uitgebreide documentatie vinden over het gebruik van Aspose.Cells voor .NET[hier](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
