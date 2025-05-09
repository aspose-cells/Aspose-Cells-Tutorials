---
"description": "Leer hoe je bogen toevoegt aan Excel-werkbladen met Aspose.Cells voor .NET. Volg onze stapsgewijze handleiding om je spreadsheetontwerpen te verbeteren."
"linktitle": "Boog toevoegen aan werkblad in Excel"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Boog toevoegen aan werkblad in Excel"
"url": "/nl/net/excel-shapes-controls/add-arc-to-worksheet-excel/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Boog toevoegen aan werkblad in Excel

## Invoering
Het maken van visueel aantrekkelijke Excel-spreadsheets is cruciaal voor de presentatie van gegevens, en de Aspose.Cells-bibliotheek biedt ontwikkelaars robuuste tools om deze taak uit te voeren. Een interessante functie die u wellicht in uw Excel-documenten wilt opnemen, is de mogelijkheid om vormen, zoals bogen, toe te voegen. In deze tutorial laten we stap voor stap zien hoe u bogen toevoegt aan een Excel-werkblad met Aspose.Cells voor .NET. Aan het einde van dit artikel leert u niet alleen hoe u bogen toevoegt, maar krijgt u ook inzicht in het beheer van vormen in het algemeen.
## Vereisten
Voordat we ingaan op de fijne kneepjes van het toevoegen van bogen aan je werkblad, is het essentieel om ervoor te zorgen dat je een paar dingen op orde hebt. Dit zijn de vereisten om aan de slag te gaan:
1. Visual Studio: Je moet Visual Studio op je computer geïnstalleerd hebben, omdat we C# als programmeertaal gebruiken.
2. .NET Framework: Zorg ervoor dat u .NET Framework of .NET Core hebt geïnstalleerd. Aspose.Cells ondersteunt beide.
3. Aspose.Cells voor .NET: U moet de Aspose.Cells-bibliotheek hebben. U kunt deze downloaden van de [Aspose.Cells-downloads](https://releases.aspose.com/cells/net/) pagina.
4. Basiskennis van C#: Als u bekend bent met C#, kunt u de codefragmenten zonder al te veel gedoe volgen.
## Pakketten importeren
Om met Aspose.Cells in je project te kunnen werken, moet je de benodigde pakketten importeren. Zo doe je dat:
### Een nieuw project maken
- Visual Studio openen.
- Kies 'Een nieuw project maken'.
- Selecteer een sjabloon die met .NET werkt (bijvoorbeeld Console Application).
  
### Aspose.Cells-verwijzingen toevoegen
- Klik met de rechtermuisknop op uw project in Solution Explorer.
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
De eerste stap is het aanmaken van een map waar u uw Excel-bestand opslaat. Dit helpt u bij het eenvoudig beheren van uw uitvoerbestanden.
```csharp
string dataDir = "Your Document Directory";
// Maak een map aan als deze nog niet bestaat.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
In dit codefragment specificeren we het pad naar de documentmap. We controleren ook of de map bestaat; zo niet, dan maken we hem aan. Dit vormt de basis voor onze output.
## Stap 2: Een werkmap instantiëren
Laten we nu een nieuwe werkmapinstantie maken.
```csharp
// Een nieuwe werkmap instantiëren.
Workbook excelbook = new Workbook();
```
Met deze regel wordt een nieuwe Excel-werkmap aangemaakt. Zie dit als een leeg canvas waar we vormen, gegevens en meer kunnen toevoegen.
## Stap 3: Voeg de eerste boogvorm toe
Laten we nu onze eerste boogvorm aan het werkblad toevoegen.
```csharp
// Voeg een boogvorm toe.
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
Hier voegen we een boog toe aan het eerste werkblad. De parameters bepalen de positie en grootte van de boog: `(left, top, width, height, startAngle, endAngle)`Het is alsof je een cirkelsegment tekent!
## Stap 4: Pas de eerste boog aan
Nadat u de boog hebt toegevoegd, wilt u mogelijk het uiterlijk ervan aanpassen.
```csharp
// Stel de vulvormkleur in
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
// Stel de plaatsing van de boog in.
arc1.Placement = PlacementType.FreeFloating;           
// Lijndikte instellen.
arc1.Line.Weight = 1;      
// Stel de streepjesstijl van de boog in.
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
In deze sectie passen we de boog aan. We stellen het vultype in op een effen kleur (in dit geval blauw), definiëren de plaatsing, bepalen de lijndikte en kiezen een streepjesstijl. Kortom, we kleden onze boog aan om hem visueel aantrekkelijk te maken!
## Stap 5: Voeg een tweede boogvorm toe
Laten we nog een boogvorm toevoegen om meer context te bieden.
```csharp
// Voeg nog een boogvorm toe.
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Net als bij de eerste boog voegen we een tweede boog toe aan hetzelfde werkblad. De coördinaten zijn hier iets verschoven om hem anders te positioneren.
## Stap 6: Pas de tweede boog aan
Net als bij de eerste boog gaan we de tweede ook aanpassen.
```csharp
// Stel de lijnkleur in
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
// Stel de plaatsing van de boog in.
arc2.Placement = PlacementType.FreeFloating;          
// Lijndikte instellen.
arc2.Line.Weight = 1;           
// Stel de streepjesstijl van de boog in.
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Hier geven we de tweede boog dezelfde stijl als de eerste. Je kunt de kleur of stijl naar wens aanpassen voor een unieke of thematische look.
## Stap 7: Sla de werkmap op
Ten slotte is het tijd om uw nieuwe werkmap met de bogen op te slaan.
```csharp
// Sla het Excel-bestand op.
excelbook.Save(dataDir + "book1.out.xls");
```
Deze regel werkt alsof je op de knop 'Opslaan' drukt. We slaan ons werk op de opgegeven locatie op met een specifieke bestandsnaam. Controleer je map om je meesterwerk in Excel-formaat te bekijken!
## Conclusie
In deze tutorial hebben we het proces van het toevoegen van boogvormen aan een Excel-werkblad met Aspose.Cells voor .NET onderzocht. Met behulp van een eenvoudige stapsgewijze handleiding hebt u geleerd hoe u een nieuwe werkmap maakt, bogen toevoegt, hun weergave aanpast en uw document opslaat. Deze mogelijkheid verbetert niet alleen de visuele aantrekkingskracht van uw spreadsheets, maar maakt uw gegevenspresentaties ook informatiever. Of u nu grafieken of rapporten maakt of gewoon experimenteert, het gebruik van vormen zoals bogen kan een creatieve draai geven aan uw projecten.
## Veelgestelde vragen
### Wat is Aspose.Cells?
Aspose.Cells is een krachtige bibliotheek waarmee ontwikkelaars programmatisch Excel-bestanden kunnen maken, bewerken en converteren zonder dat ze Microsoft Excel nodig hebben.
### Moet ik Microsoft Excel installeren om Aspose.Cells te gebruiken?
Nee, Aspose.Cells is volledig onafhankelijk en vereist geen installatie van Microsoft Excel.
### Kan ik Aspose.Cells gratis uitproberen?
Ja, u kunt Aspose.Cells uitproberen met behulp van hun [Gratis proefperiode](https://releases.aspose.com/).
### Welke programmeertalen ondersteunt Aspose.Cells?
Aspose.Cells ondersteunt meerdere talen, waaronder C#, VB.NET en meer.
### Waar kan ik ondersteuning krijgen voor Aspose.Cells?
U kunt ondersteuning krijgen via de [Aspose Forum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}