---
title: Verbindingspunten van vorm in Excel verkrijgen
linktitle: Verbindingspunten van vorm in Excel verkrijgen
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u shape connection points in Excel kunt krijgen met Aspose.Cells voor .NET. Volg onze stapsgewijze handleiding om shape points eenvoudig programmatisch te extraheren en weer te geven.
weight: 11
url: /nl/net/excel-shapes-controls/get-connection-points-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Verbindingspunten van vorm in Excel verkrijgen

## Invoering
Wanneer we programmatisch met Excel-bestanden werken, moeten we vaak interacteren met vormen die in de sheets zijn ingebed. Een van de meer geavanceerde taken die u kunt uitvoeren, is het extraheren van verbindingspunten uit een vorm. Verbindingspunten worden gebruikt om vormen te koppelen aan connectoren en hun lay-out nauwkeuriger te beheren. Als u de verbindingspunten van een vorm in Excel wilt krijgen, is Aspose.Cells voor .NET de tool die u nodig hebt. In deze tutorial nemen we u mee door een stapsgewijs proces om dit te bereiken.
## Vereisten
Voordat u aan de slag gaat met de code, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:
- Aspose.Cells voor .NET: U moet Aspose.Cells in uw ontwikkelomgeving hebben geïnstalleerd. Als u het nog niet hebt, kunt u[Download hier de nieuwste versie](https://releases.aspose.com/cells/net/).
- Ontwikkelomgeving: Zorg ervoor dat u een werkende installatie van Visual Studio of een andere .NET-compatibele IDE hebt.
- Basiskennis van C#: in deze tutorial wordt ervan uitgegaan dat u een basiskennis hebt van C#-programmering en objectgeoriënteerde principes.
 U kunt zich ook aanmelden voor een[gratis proefversie van Aspose.Cells](https://releases.aspose.com/) als je dat nog niet hebt gedaan. Hiermee krijg je toegang tot alle functies die nodig zijn voor deze gids.

## Pakketten importeren
Om met Aspose.Cells in uw project te werken, moet u de benodigde naamruimten opnemen. De volgende import statements moeten bovenaan uw code worden geplaatst:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Met deze naamruimten krijgt u toegang tot de kernfunctionaliteit van Aspose.Cells en kunt u werkbladen en vormen bewerken.

## Stapsgewijze handleiding om verbindingspunten van een vorm te verkrijgen
In deze sectie laten we u zien hoe u de verbindingspunten van een vorm in een Excel-werkblad kunt extraheren. Volg elke stap zorgvuldig voor een duidelijk begrip.
## Stap 1: Een nieuwe werkmap instantiëren
 Allereerst moeten we een instantie van de maken`Workbook` class. Dit vertegenwoordigt een Excel-bestand in Aspose.Cells. Als u geen bestaand bestand hebt, is dat geen probleem: u kunt beginnen met een lege werkmap.
```csharp
// Een nieuwe werkmap instantiëren
Workbook workbook = new Workbook();
```
 In deze stap hebben we een lege Excel-werkmap gemaakt, maar u kunt ook een bestaande laden door het bestandspad door te geven aan de`Workbook` constructeur.
## Stap 2: Toegang tot het eerste werkblad
Vervolgens moeten we toegang krijgen tot het werkblad waar we met vormen willen werken. In dit geval gebruiken we het eerste werkblad van de werkmap.
```csharp
// Haal het eerste werkblad in de werkmap
Worksheet worksheet = workbook.Worksheets[0];
```
 Deze regel geeft toegang tot het eerste werkblad uit de verzameling werkbladen in de werkmap. Als u met een specifiek werkblad werkt, kunt u de index vervangen`0` met de gewenste index.
## Stap 3: Een nieuw tekstvak (vorm) toevoegen
Laten we nu een nieuwe vorm toevoegen aan het werkblad. We maken een tekstvak, wat een soort vorm is. Je kunt ook andere soorten vormen toevoegen, maar voor de eenvoud houden we het in deze tutorial bij een tekstvak.
```csharp
// Voeg een nieuw tekstvak toe aan de verzameling
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
Dit is wat we hebben gedaan:
-  Een tekstvak toegevoegd op rij`2` , kolom`1`.
-  Stel de afmetingen van het tekstvak in op`160` eenheden in breedte en`200` eenheden in hoogte.
## Stap 4: Toegang tot de vorm vanuit de vormenverzameling
 Zodra we het tekstvak hebben toegevoegd, wordt het onderdeel van de vormencollectie van het werkblad. Nu gaan we die vorm benaderen met behulp van de`Shapes`verzameling.
```csharp
// Toegang tot de vorm (tekstvak) vanuit de vormenverzameling
Shape shape = workbook.Worksheets[0].Shapes[0];
```
In deze stap halen we de eerste vorm (ons tekstvak) op uit de verzameling. Als u meerdere vormen hebt, kunt u de index opgeven of zelfs de vorm op naam zoeken.
## Stap 5: Verbindingspunten ophalen
Nu we onze vorm hebben, gaan we de verbindingspunten eruit halen. Deze punten worden gebruikt om connectoren aan de vorm te bevestigen. De`ConnectionPoints` De eigenschap van de vorm retourneert alle beschikbare verbindingspunten.
```csharp
// Krijg alle verbindingspunten in deze vorm
var connectionPoints = shape.ConnectionPoints;
```
Hiermee krijgen we een overzicht van alle verbindingspunten die beschikbaar zijn voor die vorm.
## Stap 6: Verbindingspunten weergeven
Ten slotte willen we de coördinaten van elk verbindingspunt weergeven. Dit is waar we door de verbindingspunten heen lopen en ze naar de console afdrukken.
```csharp
// Alle vormpunten weergeven
foreach (var pt in connectionPoints)
{
    System.Console.WriteLine(string.Format("X = {0}, Y = {1}", pt.X, pt.Y));
}
```
 Deze lus herhaalt elk verbindingspunt en drukt de`X` En`Y` coördinaten. Dit kan handig zijn voor het debuggen of visueel bevestigen van de verbindingspunten van een vorm.
## Stap 7: Uitvoeren en voltooien
Zodra u alle bovenstaande stappen hebt ingesteld, kunt u de code uitvoeren. Dit is de laatste regel die ervoor zorgt dat het proces succesvol wordt voltooid:
```csharp
System.Console.WriteLine("GetShapeConnectionPoints executed successfully.");
```
Deze regel registreert eenvoudigweg een bericht op de console dat het proces is voltooid.

## Conclusie
In deze tutorial hebben we behandeld hoe u verbindingspunten van een vorm in Excel kunt ophalen met Aspose.Cells voor .NET. Door de taak op te splitsen in kleine, verteerbare stappen, hebben we het proces van het maken van een werkmap, het toevoegen van een vorm en het extraheren van de verbindingspunten onderzocht.
Door te begrijpen hoe je vormen programmatisch kunt manipuleren, ontsluit je een wereld aan mogelijkheden voor het bouwen van dynamische en interactieve Excel-sheets. Of je nu rapporten bouwt, dashboards ontwerpt of diagrammen maakt, deze kennis komt goed van pas.
## Veelgestelde vragen
### Wat is een verbindingspunt in een vorm?
Een verbindingspunt is een specifiek punt op een vorm waar u connectoren aan kunt bevestigen of aan andere vormen kunt koppelen.
### Kan ik verbindingspunten voor alle vormen in een werkblad ophalen?
Ja, Aspose.Cells stelt u in staat om verbindingspunten op te halen voor elke vorm die deze ondersteunt. Loop gewoon door de vormenverzameling in het werkblad.
### Heb ik een licentie nodig om Aspose.Cells te gebruiken?
Ja, hoewel je het gratis kunt proberen, is er een licentie vereist voor volledige functies. Je kunt[Koop hier een licentie](https://purchase.aspose.com/buy)of krijg een[tijdelijke licentie](https://purchase.aspose.com/temporary-license/).
### Hoe kan ik verschillende soorten vormen toevoegen in Aspose.Cells?
 kunt de`Add` methode voor vormen zoals rechthoeken, ellipsen en meer. Elke vorm heeft specifieke parameters die u kunt aanpassen.
### Hoe laad ik een bestaand Excel-bestand in plaats van een nieuw bestand te maken?
 Om een bestaand bestand te laden, geeft u het bestandspad door aan de`Workbook` constructor, zoals dit:  
```csharp
Workbook workbook = new Workbook("path_to_file.xlsx");
```
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
