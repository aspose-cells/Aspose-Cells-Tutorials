---
title: OLE-object in Excel invoegen
linktitle: OLE-object in Excel invoegen
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u OLE-objecten in Excel-bestanden invoegt met Aspose.Cells voor .NET in deze uitgebreide handleiding met stapsgewijze instructies.
weight: 11
url: /nl/net/excel-ole-picture-objects/insert-ole-object-into-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OLE-object in Excel invoegen

## Invoering
Of u nu afbeeldingen, grafieken of andere bestanden insluit, Aspose.Cells voor .NET biedt een eenvoudige manier om dit te bereiken. In deze handleiding verkennen we de stappen die nodig zijn om een OLE-object in een Excel-sheet in te voegen. Aan het einde kunt u uw Excel-werkmappen verbeteren met gepersonaliseerde insluitingen die indruk kunnen maken op uw publiek of die aan verschillende professionele behoeften voldoen. 
## Vereisten
Voordat we in de details van de code duiken, zijn er een paar dingen die u bij de hand moet hebben:
1. Visual Studio: Idealiter zou u moeten werken in een omgeving die .NET ondersteunt, zoals Visual Studio. Deze IDE maakt het eenvoudig om uw applicaties te schrijven, testen en debuggen.
2. Aspose.Cells-bibliotheek: U moet de Aspose.Cells-bibliotheek geïnstalleerd hebben. U kunt deze verkrijgen via NuGet-pakketbeheerder of rechtstreeks downloaden van de[Aspose-website](https://releases.aspose.com/cells/net/).
3.  Voorbeeld bestanden: Zorg ervoor dat u voor demonstratiedoeleinden een afbeelding hebt (zoals`logo.jpg`) en een Excel-bestand (`book1.xls`) om mee te werken. Deze worden in de code vermeld.
4. Basiskennis van C#: Kennis van C# helpt u de betrokken stappen te begrijpen en indien nodig aanpassingen door te voeren.
Zodra u alles op zijn plaats hebt, is het tijd om de mouwen op te stropen en aan de slag te gaan met het invoegen van OLE-objecten in Excel!
## Pakketten importeren
Om Excel-bestanden te manipuleren met Aspose.Cells, moet u eerst de vereiste pakketten importeren. Voeg de volgende naamruimten toe bovenaan uw C#-bestand:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Met deze basisinstelling kunt u werken met de werkmap, werkbladen en andere essentiële onderdelen die u voor uw taak nodig hebt.
Laten we het opsplitsen in gemakkelijk te verteren stappen.
## Stap 1: Stel uw documentenmap in
De eerste stap is om vast te stellen waar uw documenten worden opgeslagen. Dit is vrij eenvoudig.
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
```
 Zorg ervoor dat u vervangt`"Your Document Directory"` met een daadwerkelijk pad naar de map op uw systeem waar u uw bestanden wilt opslaan.
## Stap 2: Maak de directory aan als deze nog niet bestaat
Vervolgens willen we ervoor zorgen dat deze directory bestaat. Als dat niet zo is, moeten we hem aanmaken.
```csharp
// Maak een map aan als deze nog niet bestaat.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Met deze eenvoudige controle voorkomt u dat uw programma onnodige fouten veroorzaakt.
## Stap 3: Een nieuwe werkmap instantiëren
Laten we nu een nieuwe werkmap maken waarin we met onze OLE-objecten gaan werken.
```csharp
// Een nieuwe werkmap maken.
Workbook workbook = new Workbook();
```
Deze nieuwe werkmap fungeert als canvas voor het OLE-object dat u wilt invoegen.
## Stap 4: Ontvang het eerste werkblad
Nadat we ons werkboek hebben, moeten we het eerste werkblad pakken. Dit is doorgaans waar je het meest actief mee bezig bent.
```csharp
// Pak het eerste werkblad.
Worksheet sheet = workbook.Worksheets[0];
```
Mooi en simpel! We zijn klaar om inhoud toe te voegen aan dit werkblad.
## Stap 5: Definieer het pad voor de afbeelding
Nu gaan we een pad instellen voor de afbeelding die u in uw Excel-bestand wilt insluiten.
```csharp
//Definieer een tekenreeksvariabele om het afbeeldingspad op te slaan.
string ImageUrl = dataDir + "logo.jpg";
```
 Zorg ervoor dat dit pad correct weergeeft waar uw`logo.jpg` bestand is opgeslagen.
## Stap 6: Laad de afbeelding in een byte-array
We moeten de afbeelding in een formaat lezen waarmee we kunnen werken. Om dit te doen, openen we de bestandsstroom en lezen de gegevens in een byte-array.
```csharp
// Breng de afbeelding in de streams.
FileStream fs = File.OpenRead(ImageUrl);
// Definieer een byte-array.
byte[] imageData = new Byte[fs.Length];
// Verkrijg een afbeelding van de byte-array uit de streams.
fs.Read(imageData, 0, imageData.Length);
// Sluit de stroom.
fs.Close();
```
Door de afbeelding in een byte-array te lezen, bereiden we deze voor op invoeging in het Excel-werkblad.
## Stap 7: Het pad naar het Excel-bestand ophalen
Laten we nu definiëren waar uw Excel-bestand zich bevindt.
```csharp
// Haal het pad van een Excel-bestand op in een variabele.
string path = dataDir + "book1.xls";
```
Controleer nogmaals of het pad correct is en naar het juiste bestand verwijst.
## Stap 8: Laad het Excel-bestand in een byte-array
Net zoals we met de afbeelding hebben gedaan, moeten we het Excel-bestand zelf in een byte-array laden.
```csharp
// Plaats het bestand in de streams.
fs = File.OpenRead(path);
//Definieer een byte-array.
byte[] objectData = new Byte[fs.Length];
// Sla het bestand op vanuit streams.
fs.Read(objectData, 0, objectData.Length);
// Sluit de stroom.
fs.Close();
```
Hiermee wordt het Excel-bestand voorbereid voor het insluiten van onze OLE-objecten.
## Stap 9: Voeg het OLE-object toe aan het werkblad
Nu onze gegevens gereed zijn, kunnen we het OLE-object in het werkblad invoegen.
```csharp
// Voeg een OLE-object toe aan het werkblad met de afbeelding.
sheet.OleObjects.Add(14, 3, 200, 220, imageData);
// Ingesloten OLE-objectgegevens instellen.
sheet.OleObjects[0].ObjectData = objectData;
```
 Deze regel maakt een ingesloten object in het Excel-document. De parameters`(14, 3, 200, 220)` specificeer de locatie en grootte van het ingebedde object. Pas deze waarden indien nodig aan voor uw specifieke use case.
## Stap 10: Sla het Excel-bestand op
Ten slotte is het tijd om uw wijzigingen in het Excel-bestand op te slaan.
```csharp
// Sla het Excel-bestand op
workbook.Save(dataDir + "output.out.xls");
```
Deze regel slaat de werkmap op met het ingevoegde OLE-object. Zorg ervoor dat u een naam gebruikt die logisch is!
## Conclusie
Het invoegen van OLE-objecten in Excel-bestanden met Aspose.Cells voor .NET is niet alleen nuttig, maar ook eenvoudig als u het opsplitst in beheersbare stappen. Met deze krachtige tool kunt u uw Excel-documenten verbeteren, waardoor ze interactief en visueel aantrekkelijk worden. Of u nu een ontwikkelaar bent die rapporten wil automatiseren of een analist die graag gegevens effectief wil presenteren, het beheersen van OLE-embedding kan een belangrijke troef zijn in uw toolkit.
## Veelgestelde vragen
### Wat is een OLE-object?
Een OLE-object is een bestand dat in een document kan worden ingebed, waardoor verschillende applicaties met elkaar kunnen worden geïntegreerd. Voorbeelden hiervan zijn afbeeldingen, Word-documenten en presentaties.
### Kan ik Aspose.Cells gratis gebruiken?
 U kunt Aspose.Cells gratis uitproberen door een proefversie te downloaden die beschikbaar is op hun website.[website](https://releases.aspose.com/).
### Welke bestandsindelingen kan ik gebruiken met OLE-objecten?
U kunt verschillende formaten gebruiken, waaronder afbeeldingen (JPEG, PNG), Word-documenten, PDF's en meer, afhankelijk van uw toepassing.
### Wordt Aspose.Cells op alle platforms ondersteund?
Aspose.Cells voor .NET is primair ontworpen voor het .NET-platform. De functionaliteit kan echter variëren in verschillende Windows-, Mac- of cloudomgevingen.
### Hoe kan ik hulp krijgen als ik problemen ondervind?
 U kunt ondersteuning krijgen via de[Aspose-forum](https://forum.aspose.com/c/cells/9) waar ontwikkelaars inzichten en oplossingen delen.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
