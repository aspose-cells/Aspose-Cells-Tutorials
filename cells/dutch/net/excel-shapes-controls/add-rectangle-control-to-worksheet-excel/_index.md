---
"description": "Ontdek hoe u een rechthoekbesturingselement toevoegt aan een Excel-werkblad met Aspose.Cells voor .NET met een gedetailleerde, stapsgewijze handleiding."
"linktitle": "Rechthoekbesturingselement toevoegen aan werkblad in Excel"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Rechthoekbesturingselement toevoegen aan werkblad in Excel"
"url": "/nl/net/excel-shapes-controls/add-rectangle-control-to-worksheet-excel/"
"weight": 25
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Rechthoekbesturingselement toevoegen aan werkblad in Excel

## Invoering
Aspose.Cells voor .NET is een krachtige tool voor het automatiseren van Excel-taken. Hiermee kunt u diverse doelen bereiken, waaronder het toevoegen van vormen zoals rechthoeken aan uw werkbladen. In deze handleiding leggen we uit hoe u een rechthoekbesturingselement aan een Excel-werkblad kunt toevoegen met Aspose.Cells voor .NET. Uiteindelijk kunt u een werkblad met een rechthoekbesturingselement maken, aanpassen en opslaan.
Maar voordat we daarin duiken, moeten we het even over de vereisten hebben.
## Vereisten
Om deze tutorial te kunnen volgen, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:
1. Aspose.Cells voor .NET-bibliotheek: Als u dat nog niet hebt gedaan, [download de bibliotheek](https://releases.aspose.com/cells/net/) of installeer het via NuGet in Visual Studio.
2. .NET Framework: De .NET-ontwikkelomgeving moet op uw computer zijn ingesteld.
3. Basiskennis van C#: Hoewel we u stap voor stap begeleiden, is basiskennis van C# en objectgeoriënteerd programmeren nuttig.
4. Licentie: Het gebruik van Aspose.Cells in de evaluatiemodus werkt prima voor basistaken, maar voor volledige functionaliteit kunt u overwegen een [tijdelijke licentie](https://purchase.aspose.com/temporary-license/) of er een kopen bij [hier](https://purchase.aspose.com/buy).
Laten we nu in de code duiken!
## Pakketten importeren
Om aan de slag te gaan met Aspose.Cells, moet u ervoor zorgen dat u de benodigde naamruimten in uw project hebt geïmporteerd. Deze imports geven toegang tot verschillende klassen en methoden die u nodig hebt om met Excel-bestanden te werken.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Deze regels zorgen ervoor dat uw project kan communiceren met bestandsmappen (`System.IO`), Excel-werkmappen (`Aspose.Cells`), en vormtekenen (`Aspose.Cells.Drawing`).
Laten we het proces nu opsplitsen in eenvoudige stappen, zodat u het gemakkelijk kunt volgen en toepassen in uw eigen projecten.
## Stap 1: Het directorypad instellen
Het eerste wat u moet doen, is de map definiëren waar uw Excel-bestand wordt opgeslagen. Deze stap zorgt ervoor dat uw project weet waar het uitvoerbestand moet worden gemaakt en opgeslagen.
### De gegevensdirectory definiëren
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
```
Hier geeft u het pad op waar het Excel-bestand wordt opgeslagen. U kunt dit vervangen door `"Your Document Directory"` met het werkelijke pad op uw computer, of dynamisch een map aanmaken als deze niet bestaat.
### De directory controleren en aanmaken
```csharp
// Maak een map aan als deze nog niet bestaat.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Dit blok controleert of de map bestaat. Zo niet, dan maakt het er een aan. Zie het als het gereedmaken van uw archiefkast voordat u documenten opslaat.
## Stap 2: Een nieuwe werkmap instantiëren
In deze stap maakt u een nieuwe Excel-werkmap met behulp van de `Aspose.Cells.Workbook` klasse. Dit dient als container voor uw werkblad en vormen.
```csharp
// Een nieuwe werkmap instantiëren.
Workbook excelbook = new Workbook();
```
Door de `Workbook` constructor, dan hebt u nu een lege Excel-werkmap die u kunt aanpassen.
## Stap 3: Een rechthoekbesturingselement toevoegen
Hier gebeurt de magie. Je voegt een rechthoekige vorm toe aan het eerste werkblad van je werkmap.
```csharp
// Voeg een rechthoekig besturingselement toe.
Aspose.Cells.Drawing.RectangleShape rectangle = excelbook.Worksheets[0].Shapes.AddRectangle(3, 0, 2, 0, 70, 130);
```
Laten we dit eens verder uitdiepen:
- `excelbook.Worksheets[0]`Hiermee krijgt u toegang tot het eerste werkblad in uw werkmap.
- `.Shapes.AddRectangle(3, 0, 2, 0, 70, 130)`: Hiermee voegt u een rechthoek toe aan het werkblad. De parameters hier definiëren de positie (rij en kolom), evenals de breedte en hoogte van de rechthoek.
## Stap 4: De rechthoek aanpassen
Alleen een rechthoek toevoegen is niet voldoende: je moet hem ook aanpassen. In deze stap stellen we de plaatsing, lijndikte en streepjesstijl van de rechthoek in.
### De plaatsing instellen
```csharp
// Bepaal de plaatsing van de rechthoek.
rectangle.Placement = PlacementType.FreeFloating;
```
Hiermee wordt aangegeven dat de rechthoek vrij zwevend is, wat betekent dat deze niet wordt beperkt door celafmetingen.
### De lijndikte instellen
```csharp
// Lijndikte instellen.
rectangle.Line.Weight = 4;
```
Hier stellen we de lijndikte van de rechthoek in op 4 punten. Hoe hoger het getal, hoe dikker de lijn.
### De streepjesstijl instellen
```csharp
// Stel de streepjesstijl van de rechthoek in.
rectangle.Line.DashStyle = MsoLineDashStyle.Solid;
```
Met deze lijn wordt de streepjesstijl van de rand van de rechthoek vastgezet. Je kunt experimenteren met verschillende stijlen, zoals `Dash` of `Dot` afhankelijk van uw wensen.
## Stap 5: De werkmap opslaan
Nadat u de rechthoek hebt toegevoegd en aangepast, slaat u de werkmap als laatste op in de opgegeven map.
```csharp
// Sla het Excel-bestand op.
excelbook.Save(dataDir + "book1.out.xls");
```
Hiermee wordt de werkmap opgeslagen als een `.xls` bestand in de map die u eerder hebt gedefinieerd. U kunt de bestandsindeling wijzigen door de extensie te wijzigen, zoals `.xlsx` als u de nieuwere Excel-indeling prefereert.
## Conclusie
En voilà! Het toevoegen van een rechthoekbesturingselement aan een Excel-werkblad met Aspose.Cells voor .NET is een eenvoudig proces als je het stap voor stap uitlegt. Of je nu vormen wilt toevoegen voor een aantrekkelijkere weergave, delen van je gegevens wilt markeren of je rapporten wilt aanpassen, Aspose.Cells biedt je de flexibiliteit om dit programmatisch te doen.
Deze handleiding zou je alle kennis moeten hebben gegeven die je nodig hebt om vormen zoals rechthoeken toe te voegen aan je Excel-sheets met Aspose.Cells. Nu is het tijd om te experimenteren en te zien wat je nog meer kunt bereiken met deze krachtige bibliotheek!
## Veelgestelde vragen
### Kan ik andere vormen zoals cirkels of lijnen toevoegen met Aspose.Cells voor .NET?  
Ja, met Aspose.Cells kunt u verschillende vormen toevoegen, waaronder cirkels, lijnen, pijlen en meer.
### Welke andere eigenschappen kan ik instellen voor het rechthoekbesturingselement?  
U kunt de opvulkleur, lijnkleur en transparantie aanpassen en zelfs tekst binnen de rechthoek toevoegen.
### Is Aspose.Cells compatibel met .NET Core?  
Ja, Aspose.Cells ondersteunt .NET Core, evenals .NET Framework en andere .NET-gebaseerde platforms.
### Kan ik de rechthoek ten opzichte van een specifieke cel positioneren?  
Ja, u kunt de rechthoek binnen specifieke rijen en kolommen plaatsen, of de `PlacementType` om te bepalen hoe het verankerd wordt.
### Is er een gratis proefversie beschikbaar voor Aspose.Cells?  
Ja, je kunt een [gratis proefperiode](https://releases.aspose.com/) vanaf de website om de functies van de bibliotheek te testen voordat u tot aankoop overgaat.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}