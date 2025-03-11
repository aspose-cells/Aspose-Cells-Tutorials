---
title: Draaitabel in ODS-formaat programmatisch opslaan in .NET
linktitle: Draaitabel in ODS-formaat programmatisch opslaan in .NET
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u draaitabellen in ODS-formaat opslaat met Aspose.Cells voor .NET met deze stapsgewijze handleiding.
weight: 25
url: /nl/net/creating-and-configuring-pivot-tables/saving-in-ods-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Draaitabel in ODS-formaat programmatisch opslaan in .NET

## Invoering
Als het aankomt op het beheren van data in spreadsheets, is er niets dat kan tippen aan de kracht van draaitabellen. Ze zijn een go-to tool voor het samenvatten, analyseren en presenteren van complexe datasets. Vandaag duiken we in het gebruik van Aspose.Cells voor .NET om een draaitabel op te slaan in ODS-formaat. Of u nu een doorgewinterde ontwikkelaar bent of net begint met .NET, u zult deze gids eenvoudig vinden. 
Laten we beginnen!
## Vereisten
Voordat we met de code beginnen, zijn er een paar essentiële zaken die je nodig hebt:
### 1. Basiskennis van .NET
Als u een basiskennis hebt van .NET en de bijbehorende programmeerconcepten, kunt u de cursus gemakkelijk volgen.
### 2. Aspose.Cells voor .NET
 U moet Aspose.Cells voor .NET geïnstalleerd hebben. U kunt het downloaden van de[Aspose releases pagina](https://releases.aspose.com/cells/net/) . Er is ook een proefversie beschikbaar[hier](https://releases.aspose.com/).
### 3. Ontwikkelomgeving
Zorg ervoor dat u een IDE zoals Visual Studio hebt waar u uw .NET-code kunt schrijven en testen.
### 4. Een beetje geduld
Zoals bij elke coderingsinspanning is geduld de sleutel. Maak je geen zorgen als dingen niet meteen perfect werken; debuggen is onderdeel van het proces.
## Pakketten importeren
Om met Aspose.Cells te werken, moet u de benodigde naamruimten importeren. Voeg de volgende using-richtlijn toe aan het begin van uw codebestand:
```csharp
using System;
using Aspose.Cells.Pivot;
```
Met deze regel krijgt u toegang tot alle functionaliteiten in de Aspose.Cells-bibliotheek, waardoor uw coderingsproces een fluitje van een cent wordt.
Laten we het proces nu opdelen in beheersbare stappen.
## Stap 1: Stel uw uitvoermap in
Eerst moet u definiëren waar u uw ODS-bestand wilt opslaan. Dit is een eenvoudige toewijzing van een directorypad.
```csharp
string outputDir = "Your Document Directory";
```
 Vervang in deze regel`"Your Document Directory"` met het pad waar u het bestand wilt opslaan.
## Stap 2: Maak een nieuwe werkmap
Vervolgens maakt u een nieuw werkmapobject aan, dat al uw gegevens en structuren bevat, inclusief de draaitabel.
```csharp
Workbook workbook = new Workbook();
```
Hier begin je in principe helemaal opnieuw: zie het als een leeg canvas waarop je je meesterwerk creëert.
## Stap 3: Toegang tot het werkblad
Nu we onze werkmap hebben, moeten we aan de slag met ons werkblad. Met Aspose.Cells kunt u eenvoudig toegang krijgen tot het eerste beschikbare werkblad.
```csharp
Worksheet sheet = workbook.Worksheets[0];
```
Met deze regel komen we bij het allereerste werkblad, klaar voor gegevensinvoer.
## Stap 4: Cellen vullen met gegevens
Het is tijd om ons werkblad te vullen met wat data. We gaan een eenvoudig voorbeeld van sportverkoopdata gebruiken. 
Zo kunt u waarden in verschillende cellen instellen:
```csharp
Cells cells = sheet.Cells;
cells["A1"].PutValue("Sport");
cells["B1"].PutValue("Quarter");
cells["C1"].PutValue("Sales");
cells["A2"].PutValue("Golf");
cells["A3"].PutValue("Golf");
cells["A4"].PutValue("Tennis");
cells["A5"].PutValue("Tennis");
cells["A6"].PutValue("Tennis");
cells["A7"].PutValue("Tennis");
cells["A8"].PutValue("Golf");
cells["B2"].PutValue("Qtr3");
cells["B3"].PutValue("Qtr4");
cells["B4"].PutValue("Qtr3");
cells["B5"].PutValue("Qtr4");
cells["B6"].PutValue("Qtr3");
cells["B7"].PutValue("Qtr4");
cells["B8"].PutValue("Qtr3");
cells["C2"].PutValue(1500);
cells["C3"].PutValue(2000);
cells["C4"].PutValue(600);
cells["C5"].PutValue(1500);
cells["C6"].PutValue(4070);
cells["C7"].PutValue(5000);
cells["C8"].PutValue(6430);
```
In deze regels definiëren we de koppen en vullen we de verkoopgegevens. Zie deze stap als het vullen van uw voorraadkast voordat u een maaltijd kookt; hoe beter uw ingrediënten (gegevens), hoe beter uw maaltijd (analyse).
## Stap 5: Een draaitabel maken
Nu komt het leuke gedeelte: de draaitabel maken! Zo voegt u deze toe aan uw werkblad:
```csharp
PivotTableCollection pivotTables = sheet.PivotTables;
// Een draaitabel toevoegen aan het werkblad
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```
 In dit fragment specificeren we het gegevensbereik voor de draaitabel en waar we het op het werkblad moeten plaatsen. Het gegevensbereik`=A1:C8` bestrijkt het gebied waar onze gegevens zich bevinden.
## Stap 6: Pas uw draaitabel aan
Vervolgens wilt u uw draaitabel aanpassen aan uw behoeften. Dit houdt in dat u bepaalt wat er wordt weergegeven, hoe het wordt gecategoriseerd en hoe het gegevens berekent.
```csharp
PivotTable pivotTable = pivotTables[index];
// Totalen voor rijen niet meer weergeven.
pivotTable.RowGrand = false;
// Het eerste veld naar het rijgebied slepen.
pivotTable.AddFieldToArea(PivotFieldType.Row, 0);
// Het tweede veld naar het kolomgebied slepen.
pivotTable.AddFieldToArea(PivotFieldType.Column, 1);
// Het derde veld naar het gegevensgebied slepen.
pivotTable.AddFieldToArea(PivotFieldType.Data, 2);
pivotTable.CalculateData();
```
Hier beslist u welke gegevensvelden u wilt samenvatten en hoe ze moeten worden weergegeven. Het is alsof u de tafel dekt voor uw etentje; u beslist wat het beste past en hoe u het presenteert.
## Stap 7: Sla uw werkmap op
Ten slotte bent u klaar om uw werk op te slaan in het gewenste ODS-formaat. Dit is hoe u dat doet:
```csharp
workbook.Save(outputDir + "PivotTableSaveInODS_out.ods");
```
Met deze stap rondt u uw project af en bewaart u het in de door u gekozen map. Een bevredigend resultaat!
## Stap 8: Controleer uw uitvoer
Ten slotte is het altijd een goed idee om te controleren of het proces succesvol is voltooid. U kunt een eenvoudig consolebericht toevoegen:
```csharp
Console.WriteLine("PivotTableSaveInODS executed successfully.");
```
Dit bericht verschijnt in uw console om te bevestigen dat alles zonder problemen is verlopen. Net als een chef die controleert of alles perfect is gekookt voordat hij het serveert!
## Conclusie 
En daar heb je het! Je hebt niet alleen een draaitabel gemaakt met Aspose.Cells, maar je hebt het ook opgeslagen in ODS-formaat. Deze gids heeft je door elke stap geleid, zodat je bent gewapend met de kennis en het vertrouwen om soortgelijke taken in de toekomst aan te pakken.
## Veelgestelde vragen
### Wat is Aspose.Cells?
Aspose.Cells is een geavanceerde bibliotheek waarmee u Excel-bestanden in .NET-toepassingen kunt maken en bewerken.
### Kan ik Aspose.Cells gratis gebruiken?
 Ja, u kunt een gratis proefversie downloaden van de[Aspose-website](https://releases.aspose.com/).
### Welke formaten ondersteunt Aspose.Cells?
Het ondersteunt talloze formaten, waaronder XLSX, XLS, ODS, PDF en vele andere.
### Hoe krijg ik ondersteuning voor Aspose.Cells?
 U kunt hulp vinden op de[Aspose Ondersteuningsforum](https://forum.aspose.com/c/cells/9).
### Is er een tijdelijke licentie beschikbaar?
 Ja, u kunt via de Aspose-site een tijdelijke licentie aanvragen[hier](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
