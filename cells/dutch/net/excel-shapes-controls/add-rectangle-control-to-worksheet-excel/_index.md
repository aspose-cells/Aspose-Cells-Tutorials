---
title: Rechthoekbesturingselement toevoegen aan werkblad in Excel
linktitle: Rechthoekbesturingselement toevoegen aan werkblad in Excel
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Ontdek hoe u een rechthoekbesturingselement toevoegt aan een Excel-werkblad met Aspose.Cells voor .NET met een gedetailleerde, stapsgewijze handleiding.
weight: 25
url: /nl/net/excel-shapes-controls/add-rectangle-control-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rechthoekbesturingselement toevoegen aan werkblad in Excel

## Invoering
Als het gaat om het automatiseren van Excel-taken, is Aspose.Cells voor .NET een krachtige tool die u kan helpen bij het bereiken van verschillende doelen, waaronder het toevoegen van vormen zoals rechthoeken aan uw werkbladen. In deze gids onderzoeken we hoe u een rechthoekbesturingselement toevoegt aan een Excel-werkblad met behulp van Aspose.Cells voor .NET. Aan het einde kunt u een werkblad maken, aanpassen en opslaan met een rechthoekbesturingselement erin ingebed.
Maar voordat we beginnen, bespreken we eerst de vereisten.
## Vereisten
Om deze tutorial te kunnen volgen, moet u aan de volgende vereisten voldoen:
1.  Aspose.Cells voor .NET-bibliotheek: Als u dat nog niet hebt gedaan,[download de bibliotheek](https://releases.aspose.com/cells/net/) of installeer het met behulp van NuGet in Visual Studio.
2. .NET Framework: U moet de .NET-ontwikkelomgeving op uw computer hebben ingesteld.
3. Basiskennis van C#: Hoewel we u stap voor stap begeleiden, is basiskennis van C# en objectgeoriënteerd programmeren nuttig.
4.  Licentie: Aspose.Cells gebruiken in de evaluatiemodus werkt prima voor basistaken, maar voor volledige functionaliteit kunt u overwegen om een[tijdelijke licentie](https://purchase.aspose.com/temporary-license/)of er een kopen bij[hier](https://purchase.aspose.com/buy).
Laten we nu in de code duiken!
## Pakketten importeren
Om aan de slag te gaan met Aspose.Cells, moet u ervoor zorgen dat u de benodigde namespaces in uw project hebt geïmporteerd. Deze imports bieden toegang tot verschillende klassen en methoden die u nodig hebt om met Excel-bestanden te communiceren.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Deze regels zorgen ervoor dat uw project kan communiceren met bestandsmappen (`System.IO`), Excel-werkmappen (`Aspose.Cells`), en vormtekenen (`Aspose.Cells.Drawing`).
Laten we het proces nu opsplitsen in eenvoudige stappen, zodat u het gemakkelijk kunt volgen en toepassen in uw eigen projecten.
## Stap 1: Het directorypad instellen
Het eerste wat u moet doen is de directory definiëren waar uw Excel-bestand wordt opgeslagen. Deze stap zorgt ervoor dat uw project weet waar het uitvoerbestand moet worden gemaakt en opgeslagen.
### De gegevensdirectory definiëren
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
```
 Hier geeft u het directorypad op waar het Excel-bestand wordt opgeslagen. U kunt vervangen`"Your Document Directory"` met het werkelijke pad op uw computer, of maak dynamisch een map aan als deze nog niet bestaat.
### De directory controleren en aanmaken
```csharp
// Maak een map aan als deze nog niet bestaat.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Dit blok controleert of de directory bestaat. Als dat niet zo is, maakt het er een. Zie het als het gereed hebben van uw archiefkast voordat u documenten opslaat.
## Stap 2: Een nieuwe werkmap instantiëren
 In deze stap maakt u een nieuwe Excel-werkmap met behulp van de`Aspose.Cells.Workbook` klasse. Dit zal dienen als de container voor uw werkblad en vormen.
```csharp
// Een nieuwe werkmap maken.
Workbook excelbook = new Workbook();
```
 Door de`Workbook` constructor, dan hebt u nu een lege Excel-werkmap die u kunt aanpassen.
## Stap 3: Een rechthoekbesturingselement toevoegen
Hier gebeurt de magie. Je voegt een rechthoekige vorm toe aan het eerste werkblad van je werkboek.
```csharp
// Voeg een rechthoekig besturingselement toe.
Aspose.Cells.Drawing.RectangleShape rectangle = excelbook.Worksheets[0].Shapes.AddRectangle(3, 0, 2, 0, 70, 130);
```
Laten we dit eens nader bekijken:
- `excelbook.Worksheets[0]`: Hiermee krijgt u toegang tot het eerste werkblad in uw werkmap.
- `.Shapes.AddRectangle(3, 0, 2, 0, 70, 130)`: Dit voegt een rechthoekige vorm toe aan het werkblad. De parameters hier definiëren de positie (rij en kolom), evenals de breedte en hoogte van de rechthoek.
## Stap 4: De rechthoek aanpassen
Alleen een rechthoek toevoegen is niet genoeg: u wilt het aanpassen. In deze stap stellen we de plaatsing, lijndikte en streepjesstijl van de rechthoek in.
### De plaatsing instellen
```csharp
// Bepaal de plaatsing van de rechthoek.
rectangle.Placement = PlacementType.FreeFloating;
```
Hiermee wordt aangegeven dat de rechthoek vrij zwevend is, wat betekent dat deze niet wordt begrensd door celafmetingen.
### De lijndikte instellen
```csharp
// Stel de lijndikte in.
rectangle.Line.Weight = 4;
```
Hier stellen we de lijndikte van de rechthoek in op 4 punten. Hoe hoger het getal, hoe dikker de lijn.
### De streepjesstijl instellen
```csharp
// Stel de streepjesstijl van de rechthoek in.
rectangle.Line.DashStyle = MsoLineDashStyle.Solid;
```
 Deze lijn stelt de streepjesstijl van de rand van de rechthoek in op effen. U kunt experimenteren met verschillende stijlen, zoals`Dash` of`Dot` afhankelijk van uw wensen.
## Stap 5: De werkmap opslaan
Nadat u de rechthoek hebt toegevoegd en aangepast, is de laatste stap het opslaan van de werkmap in de opgegeven map.
```csharp
// Sla het Excel-bestand op.
excelbook.Save(dataDir + "book1.out.xls");
```
 Hiermee wordt de werkmap opgeslagen als een`.xls` bestand in de map die u eerder hebt gedefinieerd. U kunt het bestandsformaat wijzigen door de extensie te wijzigen, zoals`.xlsx` als u de nieuwere Excel-indeling prefereert.
## Conclusie
En daar heb je het! Een rechthoekbesturingselement toevoegen aan een Excel-werkblad met Aspose.Cells voor .NET is een eenvoudig proces als je het stap voor stap opsplitst. Of je nu vormen wilt toevoegen voor visuele aantrekkingskracht, secties van je gegevens wilt markeren of je rapporten wilt aanpassen, Aspose.Cells geeft je de flexibiliteit om dit programmatisch te doen.
Deze gids zou u moeten hebben voorzien van alle kennis die u nodig hebt om vormen zoals rechthoeken toe te voegen aan uw Excel-sheets met Aspose.Cells. Nu is het tijd om te experimenteren en te zien wat u nog meer kunt bereiken met deze krachtige bibliotheek!
## Veelgestelde vragen
### Kan ik andere vormen, zoals cirkels of lijnen, toevoegen met Aspose.Cells voor .NET?  
Ja, met Aspose.Cells kunt u verschillende vormen toevoegen, waaronder cirkels, lijnen, pijlen en meer.
### Welke andere eigenschappen kan ik instellen voor het rechthoekbesturingselement?  
U kunt de opvulkleur, lijnkleur en transparantie aanpassen en zelfs tekst toevoegen binnen de rechthoek.
### Is Aspose.Cells compatibel met .NET Core?  
Ja, Aspose.Cells ondersteunt .NET Core, evenals .NET Framework en andere .NET-gebaseerde platforms.
### Kan ik de rechthoek ten opzichte van een specifieke cel positioneren?  
 Ja, u kunt de rechthoek binnen specifieke rijen en kolommen plaatsen, of de`PlacementType` om te bepalen hoe het verankerd is.
### Is er een gratis proefversie beschikbaar voor Aspose.Cells?  
 Ja, je kunt een[gratis proefperiode](https://releases.aspose.com/) vanaf de website om de functies van de bibliotheek te testen voordat u tot aankoop overgaat.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
