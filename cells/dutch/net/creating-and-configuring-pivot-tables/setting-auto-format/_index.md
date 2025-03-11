---
title: Automatische opmaak van draaitabel programmatisch instellen in .NET
linktitle: Automatische opmaak van draaitabel programmatisch instellen in .NET
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u automatische opmaak voor draaitabellen in Excel programmatisch instelt met Aspose.Cells voor .NET in deze gedetailleerde stapsgewijze zelfstudie.
weight: 18
url: /nl/net/creating-and-configuring-pivot-tables/setting-auto-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Automatische opmaak van draaitabel programmatisch instellen in .NET

## Invoering
Als het aankomt op het analyseren van data, kunnen draaitabellen in Excel een game-changer zijn. Ze stellen u in staat om data dynamisch samen te vatten en te analyseren, waardoor u inzichten kunt vergaren die bijna onmogelijk handmatig te extraheren zijn. Maar wat als u het proces van het formatteren van uw draaitabellen in .NET wilt automatiseren? Hier laat ik u zien hoe u de automatische opmaak van een draaitabel programmatisch instelt met behulp van de krachtige Aspose.Cells-bibliotheek voor .NET.
In deze gids verkennen we de basis, doorlopen we de vereisten, importeren we de benodigde pakketten en duiken we vervolgens in een stapsgewijze tutorial om u te helpen draaitabellen te formatteren als een pro. Klinkt goed? Laten we er meteen induiken!
## Vereisten
Voordat we beginnen, controleren we of u alles heeft wat u nodig hebt om te beginnen:
1. Een .NET-ontwikkelomgeving: zorg ervoor dat u een werkend exemplaar van Visual Studio hebt (of een .NET-ondersteunende IDE).
2.  Aspose.Cells-bibliotheek: Om soepel met Excel-bestanden te werken, moet u de Aspose.Cells-bibliotheek installeren. Als u dat nog niet hebt gedaan, kunt u deze downloaden van de[downloadpagina](https://releases.aspose.com/cells/net/).
3. Basiskennis van C#: Kennis van C#-programmering helpt u de stappen beter te begrijpen.
4.  Excel-bestand (sjabloon): U hebt om te beginnen een Excel-sjabloonbestand nodig, dat in ons voorbeeld wordt verwerkt. Voor de eenvoud kunt u een voorbeeldbestand maken met de naam`Book1.xls`.
## Pakketten importeren
Om aan de slag te gaan met Aspose.Cells in uw project, moet u de benodigde pakketten importeren. Zo kunt u dat instellen in uw .NET-project:
### Een nieuw project maken
Begin met het maken van een nieuw .NET-project in uw favoriete IDE. 
### Referenties toevoegen
Zorg ervoor dat u een verwijzing naar de Aspose.Cells-bibliotheek toevoegt. Als u de bibliotheek hebt gedownload, voegt u de DLL's van de extractie toe. Als u NuGet gebruikt, kunt u gewoon het volgende uitvoeren:
```bash
Install-Package Aspose.Cells
```
### Naamruimten importeren
Nu moet u in uw codebestand de Aspose.Cells-naamruimte importeren. U kunt dit doen door de volgende regel bovenaan uw C#-bestand toe te voegen:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Nu u deze stappen hebt voltooid, bent u klaar om code te schrijven!
Laten we de code die u hebt verstrekt nu opsplitsen in gedetailleerde stappen met uitleg over wat elk onderdeel doet. 
## Stap 1: Definieer uw documentendirectory
Om te beginnen moet u het pad naar uw documentenmap instellen waar uw Excel-bestanden zich bevinden. In ons voorbeeld definiëren we het als volgt:
```csharp
string dataDir = "Your Document Directory";  // Indien nodig aanpassen
```
 Deze regel maakt een tekenreeksvariabele`dataDir`die het bestandspad naar uw documenten bevat. Zorg ervoor dat u vervangt`"Your Document Directory"` met het werkelijke pad op uw systeem.
## Stap 2: Laad het sjabloonbestand
Vervolgens wilt u een bestaande werkmap laden die uw draaitabel bevat:
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
 Deze regel initialiseert een nieuwe`Workbook` object door het opgegeven Excel-bestand te laden. Het bestand moet ten minste één draaitabel bevatten om de volgende stappen effectief te laten zijn.
## Stap 3: Ga naar het gewenste werkblad
Bepaal welk werkblad u moet gebruiken om toegang te krijgen tot de draaitabel. In dit geval pakken we gewoon de eerste:
```csharp
int pivotIndex = 0;  // Index van de draaitabel
Worksheet worksheet = workbook.Worksheets[0];
```
 Hier,`worksheet` haalt het eerste werkblad op uit de werkmap. De draaitabelindex is ingesteld op`0`, wat betekent dat we toegang hebben tot de eerste draaitabel in dat werkblad.
## Stap 4: Zoek de draaitabel
Nu het werkblad klaar is, is het tijd om uw draaitabel te openen:
```csharp
PivotTable pivotTable = worksheet.PivotTables[pivotIndex];
```
 Hiermee wordt een nieuwe geïnitialiseerd`PivotTable` object door de draaitabel op de opgegeven index uit het werkblad te halen.
## Stap 5: Stel de eigenschap Automatische opmaak in
En nu het sappigste gedeelte: het instellen van de opties voor automatische opmaak voor uw draaitabel.
```csharp
pivotTable.IsAutoFormat = true; // Automatisch opmaken inschakelen
```
 Deze regel schakelt de functie voor automatisch opmaken voor de draaitabel in. Wanneer ingesteld op`true`, wordt de draaitabel automatisch opgemaakt op basis van vooraf gedefinieerde stijlen.
## Stap 6: Kies een specifiek type automatische opmaak
We willen ook specificeren welke automatische opmaakstijl de draaitabel moet aannemen. Aspose.Cells heeft verschillende formaten waaruit we kunnen kiezen. Dit is hoe je het instelt:
```csharp
pivotTable.AutoFormatType = Aspose.Cells.Pivot.PivotTableAutoFormatType.Report5;
```
 Met deze regel wijzen we een specifiek automatisch opmaaktype toe aan de draaitabel.`Report5` is slechts een voorbeeld van één stijl; u kunt kiezen uit verschillende opties, afhankelijk van uw behoeften. 
## Stap 7: Sla de werkmap op
Vergeet ten slotte niet om uw werkmap op te slaan nadat u alle wijzigingen hebt aangebracht:
```csharp
workbook.Save(dataDir + "output.xls");
```
 Deze regel code slaat de gewijzigde werkmap op in een nieuw bestand met de naam`output.xls` in de opgegeven directory. Controleer dit bestand om uw prachtig geformatteerde draaitabel te zien!
## Conclusie
Gefeliciteerd! U hebt zojuist een Excel-draaitabel geprogrammeerd om automatisch op te maken met Aspose.Cells in .NET. Dit proces bespaart u niet alleen tijd bij het voorbereiden van rapporten, maar zorgt er ook voor dat uw gegevens er bij elke run consistent uitzien. Met slechts een paar regels code kunt u uw Excel-bestanden aanzienlijk verbeteren, net als een digitale goochelaar.
## Veelgestelde vragen
### Wat is Aspose.Cells?
Aspose.Cells is een krachtige .NET-bibliotheek voor het verwerken van Excel-bestanden zonder dat Microsoft Excel geïnstalleerd hoeft te zijn.
### Kan ik meerdere draaitabellen in een werkmap opmaken?
Ja, u kunt meerdere draaitabelobjecten in uw werkmap doorlopen om ze één voor één op te maken.
### Is er een gratis proefversie beschikbaar voor Aspose.Cells?
 Absoluut! U kunt beginnen met een gratis proefversie die beschikbaar is[hier](https://releases.aspose.com/).
### Wat moet ik doen als mijn draaitabel niet correct wordt opgemaakt?
Zorg ervoor dat er correct naar de draaitabel wordt verwezen en dat het type automatische opmaak aanwezig is. Anders worden de standaardinstellingen mogelijk teruggezet.
### Kan ik dit proces automatiseren met geplande taken?
Jazeker! Door deze code in een geplande taak op te nemen, kunt u het genereren en opmaken van rapporten regelmatig automatiseren.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
