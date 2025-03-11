---
title: Groepeer rijen en kolommen in Excel met Aspose.Cells
linktitle: Groepeer rijen en kolommen in Excel met Aspose.Cells
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u rijen en kolommen in Excel kunt groeperen met Aspose.Cells voor .NET met deze stapsgewijze handleiding.
weight: 12
url: /nl/net/row-and-column-management/grouping-rows-and-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Groepeer rijen en kolommen in Excel met Aspose.Cells

## Invoering
Als u met grote Excel-sheets werkt, weet u hoe belangrijk het is om alles overzichtelijk en gebruiksvriendelijk te houden. Door rijen en kolommen te groeperen, kunt u secties maken, waardoor gegevensnavigatie veel soepeler verloopt. Met Aspose.Cells voor .NET kunt u rijen en kolommen in Excel eenvoudig programmatisch groeperen, waardoor u volledige controle hebt over de lay-out van uw bestanden.
In deze tutorial doorlopen we alles wat u moet weten om rijen en kolommen in een Excel-sheet in te stellen, te groeperen en te verbergen met Aspose.Cells voor .NET. Aan het einde kunt u Excel-bestanden als een professional manipuleren zonder Excel zelf te openen. Klaar om erin te duiken?
## Vereisten
Voordat we met de code aan de slag gaan, controleren we of alles klaar is en gereed is:
1.  Aspose.Cells voor .NET-bibliotheek: u hebt deze bibliotheek nodig om met Excel-bestanden te werken. U kunt deze downloaden[hier](https://releases.aspose.com/cells/net/).
2. Visual Studio: in deze zelfstudie wordt Visual Studio gebruikt voor codevoorbeelden.
3. Basiskennis van C#: Kennis van C# en .NET is nuttig.
4. Aspose-licentie: Een betaalde of tijdelijke licentie is vereist om evaluatiebeperkingen te vermijden. Verkrijg een tijdelijke licentie[hier](https://purchase.aspose.com/temporary-license/).
## Pakketten importeren
Om te beginnen importeert u de benodigde Aspose.Cells-naamruimte, samen met essentiële .NET-bibliotheken voor bestandsverwerking. 
```csharp
using System.IO;
using Aspose.Cells;
```
Laten we elk onderdeel van de code eens nader bekijken, zodat u het gemakkelijker kunt volgen en begrijpen.
## Stap 1: Stel uw gegevensdirectory in
Allereerst moeten we het pad naar het Excel-bestand definiëren waarmee we gaan werken. Dit is meestal een lokaal pad, maar het kan ook een pad op een netwerk zijn.
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
```
 Hier, vervang`"Your Document Directory"` met het daadwerkelijke pad naar uw Excel-bestanden. Deze instelling helpt uw code de bestanden te vinden die het nodig heeft om aan te werken.
## Stap 2: Maak een bestandsstroom om toegang te krijgen tot het Excel-bestand
Aspose.Cells vereist dat u het bestand opent via een bestandsstroom. Deze stroom leest en laadt de inhoud van het bestand voor verwerking.
```csharp
// Een bestandsstroom maken met het te openen Excel-bestand
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
 De bovenstaande code opent`book1.xls` vanuit de door u opgegeven directory. Als het bestand niet bestaat, zorg er dan voor dat u het aanmaakt of de bestandsnaam wijzigt.
## Stap 3: Laad de werkmap met Aspose.Cells
Laten we nu de werkmap initialiseren via Aspose.Cells. Deze stap geeft ons toegang tot het Excel-bestand, wat eenvoudige manipulatie mogelijk maakt.
```csharp
// Het Excel-bestand openen via de bestandsstroom
Workbook workbook = new Workbook(fstream);
```
 Na deze regel komt de`workbook` object bevat alle gegevens en structuur uit uw Excel-bestand. Zie het alsof u de hele spreadsheet in het geheugen laadt.
## Stap 4: Ga naar het werkblad dat u wilt wijzigen
Aspose.Cells slaat elk werkblad in de werkmap op als een apart object. Hier selecteren we het eerste werkblad.
```csharp
// Toegang krijgen tot het eerste werkblad in het Excel-bestand
Worksheet worksheet = workbook.Worksheets[0];
```
Als u een specifiek werkblad nodig hebt, kunt u deze regel aanpassen, zodat u het werkblad via de naam of index kunt openen.
## Stap 5: Groepeer rijen in het werkblad
Nu is het tijd voor het leukste gedeelte: rijen groeperen! Laten we de eerste zes rijen groeperen en verbergen.
```csharp
// Groepeer de eerste zes rijen (van 0 tot 5) en maak ze verborgen door true door te geven
worksheet.Cells.GroupRows(0, 5, true);
```
Dit is wat elke parameter doet:
- 0, 5: De begin- en eindindexen voor de rijen die u wilt groeperen. In Excel begint rijindexering bij 0.
- true: Als u dit op true instelt, worden de gegroepeerde rijen verborgen.
Nadat de opdracht is uitgevoerd, worden de rijen van 0 tot en met 5 gegroepeerd en verborgen.
## Stap 6: Kolommen groeperen in het werkblad
Net als bij rijen kunt u kolommen groeperen om een schonere, meer georganiseerde lay-out te creëren. Hier ziet u hoe u de eerste drie kolommen groepeert.
```csharp
// Groepeer de eerste drie kolommen (van 0 tot 2) en maak ze verborgen door true door te geven
worksheet.Cells.GroupColumns(0, 2, true);
```
Parameters voor deze functie zijn:
- 0, 2: Het bereik van de kolommen die gegroepeerd moeten worden, waarbij de indexering begint bij 0.
- true: Deze parameter verbergt de gegroepeerde kolommen.
De geselecteerde kolommen (0 tot en met 2) worden nu gegroepeerd en verborgen weergegeven in het Excel-bestand.
## Stap 7: Sla het gewijzigde Excel-bestand op
Nadat u de wijzigingen hebt aangebracht, slaat u het bestand op onder een nieuwe naam. Zo voorkomt u dat u het origineel overschrijft.
```csharp
// Het gewijzigde Excel-bestand opslaan
workbook.Save(dataDir + "output.xls");
```
 U hebt nu met succes uw gegroepeerde rijen en kolommen opgeslagen in`output.xls`U kunt de bestandsnaam indien nodig aanpassen.
## Stap 8: Sluit de bestandsstroom naar vrije bronnen
Sluit ten slotte de bestandsstroom om alle resources vrij te geven. Als u dit niet doet, kan dit problemen veroorzaken als u het bestand opnieuw moet openen of wijzigen.
```csharp
// De bestandsstroom sluiten om alle bronnen vrij te maken
fstream.Close();
```
En dat is alles! U hebt nu rijen en kolommen in een Excel-bestand gegroepeerd met Aspose.Cells voor .NET.
## Conclusie
Rijen en kolommen groeperen in Excel met Aspose.Cells voor .NET is een eenvoudig proces dat uw spreadsheets veel gebruiksvriendelijker en georganiseerder kan maken. Met slechts een paar regels code hebt u een krachtige functie onder de knie die meer stappen zou kosten als u het handmatig in Excel zou doen. Bovendien kunt u dit proces automatiseren voor meerdere bestanden, wat tijd bespaart en fouten vermindert. Deze gids heeft u alle stappen laten zien die u nodig hebt om uw Excel-bestanden programmatisch onder controle te krijgen.
## Veelgestelde vragen
### Kan ik rijen en kolommen groeperen zonder ze te verbergen?  
 Ja! Gewoon passeren`false` als derde parameter in de`GroupRows` of`GroupColumns` methode.
### Wat moet ik doen als ik rijen of kolommen wil degroeperen?  
 Gebruik`worksheet.Cells.UngroupRows(startRow, endRow)` of`worksheet.Cells.UngroupColumns(startColumn, endColumn)` om ze te degroeperen.
### Kan ik meerdere bereiken binnen hetzelfde werkblad groeperen?  
 Absoluut. Bel de`GroupRows` of`GroupColumns`methode voor elk bereik dat u wilt groeperen.
### Heb ik een licentie nodig om Aspose.Cells voor .NET te gebruiken?  
 Ja, hoewel er een proefversie beschikbaar is, heb je een licentie nodig om de volledige functionaliteit te ontgrendelen. Je kunt een tijdelijke licentie krijgen[hier](https://purchase.aspose.com/temporary-license/).
### Kan ik rijen en kolommen groeperen met voorwaardelijke logica?  
Ja! U kunt voorwaardelijke groepering maken door logica in uw code op te nemen vóór het groeperen, afhankelijk van de gegevens in elke rij of kolom.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
