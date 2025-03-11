---
title: Boog toevoegen aan werkblad in Excel
linktitle: Boog toevoegen aan werkblad in Excel
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u bogen toevoegt aan Excel-werkbladen met Aspose.Cells voor .NET. Volg onze stapsgewijze handleiding om uw spreadsheetontwerpen te verbeteren.
weight: 16
url: /nl/net/excel-shapes-controls/add-arc-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Boog toevoegen aan werkblad in Excel

## Invoering
Het maken van visueel aantrekkelijke Excel-spreadsheets is cruciaal voor de presentatie van gegevens en de Aspose.Cells-bibliotheek biedt ontwikkelaars robuuste tools om deze taak uit te voeren. Een interessante functie die u wellicht in uw Excel-documenten wilt opnemen, is de mogelijkheid om vormen toe te voegen, zoals bogen. In deze tutorial laten we stap voor stap zien hoe u bogen toevoegt aan een Excel-werkblad met Aspose.Cells voor .NET. Aan het einde van dit artikel leert u niet alleen hoe u bogen toevoegt, maar krijgt u ook inzicht in het beheren van vormen in het algemeen.
## Vereisten
Voordat we ingaan op de complexiteit van het toevoegen van bogen aan uw werkblad, is het essentieel om ervoor te zorgen dat u een aantal dingen op orde hebt. Dit zijn de vereisten die u nodig hebt om te beginnen:
1. Visual Studio: Visual Studio moet op uw computer geïnstalleerd zijn, omdat we C# als programmeertaal gebruiken.
2. .NET Framework: Zorg ervoor dat u .NET Framework of .NET Core hebt geïnstalleerd. Aspose.Cells ondersteunt beide.
3. Aspose.Cells voor .NET: U moet de Aspose.Cells-bibliotheek hebben. U kunt deze downloaden van de[Aspose.Cellen Downloads](https://releases.aspose.com/cells/net/) pagina.
4. Basiskennis van C#: Als u bekend bent met C#, kunt u de codefragmenten zonder al te veel gedoe volgen.
## Pakketten importeren
Om te beginnen met Aspose.Cells in uw project, moet u de benodigde pakketten importeren. Dit is hoe u dat doet:
### Een nieuw project maken
- Open Visual Studio.
- Kies 'Een nieuw project maken'.
- Selecteer een sjabloon die werkt met .NET (zoals Console Application).
  
### Voeg Aspose.Cells-verwijzingen toe
- Klik met de rechtermuisknop op uw project in de Solution Explorer.
- Selecteer 'NuGet-pakketten beheren'.
- Zoek naar “Aspose.Cells” en installeer het.
Nu bent u klaar om te beginnen met het coderen van de boogtoevoeging.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Hieronder vindt u een stapsgewijze uitleg van de code die laat zien hoe u bogen toevoegt aan een werkblad in Excel.
## Stap 1: De directory instellen
De eerste stap is om een directory in te stellen waar u uw Excel-bestand opslaat. Dit helpt bij het eenvoudig beheren van uw uitvoerbestanden.
```csharp
string dataDir = "Your Document Directory";
// Maak een map aan als deze nog niet bestaat.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
In dit codefragment specificeren we het pad naar de documentdirectory. We controleren ook of de directory bestaat; als dat niet zo is, maken we hem aan. Dit vormt de basis voor onze output.
## Stap 2: Een werkmap instantiëren
Laten we nu een nieuwe werkmapinstantie maken.
```csharp
// Een nieuwe werkmap maken.
Workbook excelbook = new Workbook();
```
Deze regel creëert een nieuwe Excel-werkmap. Zie dit als een leeg canvas waar we vormen, gegevens en meer aan kunnen toevoegen.
## Stap 3: Voeg de eerste boogvorm toe
Laten we nu onze eerste boogvorm aan het werkblad toevoegen.
```csharp
// Voeg een boogvorm toe.
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
 Hier voegen we een boog toe aan het eerste werkblad. De parameters definiëren de positie en grootte van de boog:`(left, top, width, height, startAngle, endAngle)`Het is alsof je een cirkelsegment tekent!
## Stap 4: Pas de eerste boog aan
Nadat u de boog hebt toegevoegd, wilt u mogelijk het uiterlijk ervan aanpassen.
```csharp
// Stel de kleur van de opvulvorm in
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
// Bepaal de plaatsing van de boog.
arc1.Placement = PlacementType.FreeFloating;           
// Stel de lijndikte in.
arc1.Line.Weight = 1;      
// Stel de streepjesstijl van de boog in.
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
In deze sectie passen we de boog aan. We stellen het opvultype in op effen kleur (in dit geval blauw), definiëren hoe het wordt geplaatst, bepalen de lijndikte en kiezen een streepjesstijl. Eigenlijk kleden we onze boog aan om hem visueel aantrekkelijk te maken!
## Stap 5: Voeg een tweede boogvorm toe
Laten we nog een boogvorm toevoegen om meer context te bieden.
```csharp
// Voeg nog een boogvorm toe.
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Vergelijkbaar met de eerste boog, voegen we een tweede boog toe op hetzelfde werkblad. De coördinaten zijn hier een beetje verschoven om het anders te positioneren.
## Stap 6: Pas de tweede boog aan
Net als bij de eerste boog gaan we de tweede ook aanpassen.
```csharp
// Stel de lijnkleur in
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
// Bepaal de plaatsing van de boog.
arc2.Placement = PlacementType.FreeFloating;          
// Stel de lijndikte in.
arc2.Line.Weight = 1;           
// Stel de streepjesstijl van de boog in.
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Hier geven we de tweede boog dezelfde styling als de eerste. U kunt de kleur of styling naar wens wijzigen voor uniciteit of thematische doeleinden.
## Stap 7: Sla de werkmap op
Ten slotte is het tijd om uw nieuwe werkmap met de bogen op te slaan.
```csharp
// Sla het Excel-bestand op.
excelbook.Save(dataDir + "book1.out.xls");
```
Deze regel werkt alsof je op de opslaan-knop drukt. We slaan ons werk op de opgegeven locatie op met een aangewezen bestandsnaam. Controleer je directory om je meesterwerk in Excel-formaat te zien!
## Conclusie
In deze tutorial hebben we het proces van het toevoegen van boogvormen aan een Excel-werkblad met Aspose.Cells voor .NET onderzocht. Via een eenvoudige stapsgewijze handleiding hebt u geleerd hoe u een nieuwe werkmap maakt, bogen toevoegt, hun uiterlijk aanpast en uw document opslaat. Deze mogelijkheid verbetert niet alleen de visuele aantrekkingskracht van uw spreadsheets, maar maakt uw gegevenspresentaties ook informatiever. Of u nu grafieken of rapporten maakt of gewoon experimenteert, het gebruik van vormen zoals bogen kan een creatieve draai geven aan uw projecten.
## Veelgestelde vragen
### Wat is Aspose.Cells?
Aspose.Cells is een krachtige bibliotheek waarmee ontwikkelaars programmatisch Excel-bestanden kunnen maken, bewerken en converteren zonder dat ze Microsoft Excel nodig hebben.
### Moet ik Microsoft Excel installeren om Aspose.Cells te gebruiken?
Nee, Aspose.Cells is volledig onafhankelijk en vereist geen installatie van Microsoft Excel.
### Kan ik Aspose.Cells gratis uitproberen?
 Ja, u kunt Aspose.Cells uitproberen met behulp van hun[Gratis proefperiode](https://releases.aspose.com/).
### Welke programmeertalen ondersteunt Aspose.Cells?
Aspose.Cells ondersteunt meerdere talen, waaronder C#, VB.NET en meer.
### Waar kan ik ondersteuning krijgen voor Aspose.Cells?
 U kunt ondersteuning krijgen via de[Aspose-forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
