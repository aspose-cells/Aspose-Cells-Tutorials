---
title: Groepeer rijen en kolommen in Excel met Aspose.Cells
linktitle: Groepeer rijen en kolommen in Excel met Aspose.Cells
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u rijen en kolommen in Excel kunt degroeperen met Aspose.Cells voor .NET met deze uitgebreide gids. Vereenvoudig uw Excel-gegevensmanipulatie.
weight: 15
url: /nl/net/row-and-column-management/ungrouping-rows-and-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Groepeer rijen en kolommen in Excel met Aspose.Cells

## Invoering
Als het gaat om het verwerken van Excel-bestanden, kunt u in situaties terechtkomen waarin u rijen en kolommen moet degroeperen. Of u nu een spreadsheet opschoont of gegevens opnieuw formatteert voor een betere presentatie, Aspose.Cells voor .NET is een fantastische tool die het proces vereenvoudigt. In deze tutorial begeleid ik u door de stappen om rijen en kolommen in Excel te degroeperen met behulp van Aspose.Cells. Aan het einde hebt u een goed begrip van hoe u programmatisch met Excel-bestanden kunt werken.
## Vereisten
Voordat we in de code duiken, moeten we ervoor zorgen dat alles is ingesteld. Dit is wat je nodig hebt:
1.  Visual Studio: U zou een werkende versie van Visual Studio op uw machine moeten hebben geïnstalleerd. Als u deze nog niet hebt, kunt u deze downloaden van[De site van Visual Studio](https://visualstudio.microsoft.com/).
2. Aspose.Cells voor .NET: U moet de Aspose.Cells-bibliotheek downloaden. U kunt deze ophalen van de[Aspose Releases-pagina](https://releases.aspose.com/cells/net/) Zorg ervoor dat u over de benodigde licenties beschikt, die u kunt aanschaffen of verkrijgen via een[tijdelijke licentie](https://purchase.aspose.com/temporary-license/).
3. Basiskennis van C#: Een basiskennis van C#-programmering helpt u de cursus beter te volgen.
Zodra je alles klaar hebt, kunnen we beginnen met het leukste gedeelte: de code!
## Pakketten importeren
Om te beginnen moet u de benodigde pakketten importeren in uw C#-project. Dit is hoe u dat doet:
1. Open uw project in Visual Studio.
2. Voeg een referentie toe aan de Aspose.Cells-bibliotheek. U kunt dit doen door met de rechtermuisknop op de referenties in uw project te klikken en Add Reference te selecteren. Blader naar de locatie waar u de Aspose.Cells DLL hebt opgeslagen.
3. Voeg bovenaan uw C#-bestand het volgende toe met behulp van richtlijnen:
```csharp
using System.IO;
using Aspose.Cells;
```
Nu alles is ingesteld, doorlopen we de stappen om rijen en kolommen in uw Excel-werkblad te degroeperen. 
## Stap 1: Definieer de documentdirectory
Eerst moet u de directory opgeven waar uw Excel-bestand zich bevindt. U kunt dit als volgt instellen:
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
```
 Vervangen`"Your Document Directory"` met het daadwerkelijke pad op uw computer waar het Excel-bestand is opgeslagen. 
## Stap 2: Een bestandsstroom maken
Vervolgens moet u een bestandsstroom maken om het Excel-bestand te openen. Dit is hoe u dat kunt doen:
```csharp
// Een bestandsstroom maken met het te openen Excel-bestand
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
 Hier opent u het bestand met de naam`book1.xls`Zorg ervoor dat dit bestand in de opgegeven directory staat, anders krijg je de foutmelding dat het bestand niet is gevonden.
## Stap 3: Een werkmapobject instantiëren
Laten we nu het Excel-bestand in een Workbook-object laden. Hiermee kunt u de werkmap programmatisch manipuleren:
```csharp
// Een werkmapobject instantiëren
// Het Excel-bestand openen via de bestandsstroom
Workbook workbook = new Workbook(fstream);
```
Met deze coderegel hebt u het Excel-bestand succesvol in het geheugen geladen en kunt u ermee aan de slag.
## Stap 4: Toegang tot het werkblad
Nadat u de werkmap hebt, is de volgende stap om toegang te krijgen tot het specifieke werkblad waar u rijen en kolommen wilt degroeperen. Dit is hoe u dat doet:
```csharp
// Toegang krijgen tot het eerste werkblad in het Excel-bestand
Worksheet worksheet = workbook.Worksheets[0];
```
In dit geval benaderen we het eerste werkblad. Als uw gegevens op een ander werkblad staan, kunt u de index dienovereenkomstig wijzigen.
## Stap 5: Rijen degroeperen
Nu komt het spannende gedeelte! Laten we de eerste zes rijen (van rij 0 tot rij 5) degroeperen. Gebruik de volgende code:
```csharp
// Groepering van de eerste zes rijen ongedaan maken (van 0 tot 5)
worksheet.Cells.UngroupRows(0, 5);
```
Deze methode verwijdert alle groeperingen die zijn toegepast op de opgegeven rijen. Zo eenvoudig is het!
## Stap 6: Kolommen degroeperen
Net als rijen kunt u ook kolommen degroeperen. Zo degroepeert u de eerste drie kolommen (van kolom 0 tot kolom 2):
```csharp
// Groepering van de eerste drie kolommen ongedaan maken (van 0 tot 2)
worksheet.Cells.UngroupColumns(0, 2);
```
## Stap 7: Sla het gewijzigde Excel-bestand op
 Nadat u de rijen en kolommen hebt gedegroepeerd, is de volgende stap om de wijzigingen op te slaan in een Excel-bestand. U kunt dit doen met behulp van de`Save` methode:
```csharp
// Het gewijzigde Excel-bestand opslaan
workbook.Save(dataDir + "output.xls");
```
 In dit voorbeeld slaan we het gewijzigde bestand op als`output.xls`U kunt de bestandsnaam naar wens wijzigen.
## Stap 8: Sluit de bestandsstroom
Om bronnen vrij te maken, moet u ten slotte de bestandsstroom sluiten:
```csharp
// De bestandsstroom sluiten om alle bronnen vrij te maken
fstream.Close();
```
Dit is een goede gewoonte om ervoor te zorgen dat uw toepassing bestands-handles niet langer vasthoudt dan nodig is.
## Conclusie
En daar heb je het! Je hebt succesvol geleerd hoe je rijen en kolommen in een Excel-bestand kunt degroeperen met Aspose.Cells voor .NET. Met slechts een paar regels code kun je programmatisch belangrijke wijzigingen aanbrengen in je Excel-bestanden. Of je nu rapporten automatiseert of gegevens voorbereidt voor analyse, het onder de knie krijgen van deze technieken kan je een hoop tijd besparen.
## Veelgestelde vragen
### Wat is Aspose.Cells?
Aspose.Cells is een krachtige bibliotheek voor het werken met Excel-bestanden in .NET-toepassingen, waarmee u eenvoudig spreadsheets kunt bewerken, converteren en maken.
### Kan ik rijen en kolommen in Excel degroeperen met behulp van andere bibliotheken?
Ja, er zijn andere bibliotheken beschikbaar voor Excel-bewerking in .NET, maar Aspose.Cells biedt uitgebreide functies en gebruiksgemak.
### Is er een manier om wijzigingen ongedaan te maken nadat ik ze heb opgeslagen?
Zodra u een Excel-bestand opslaat, kunt u de vorige status niet meer herstellen, tenzij u een back-up van het oorspronkelijke bestand hebt.
### Hoe krijg ik ondersteuning voor Aspose.Cells?
 U kunt ondersteuning vinden door de[Aspose Ondersteuningsforum](https://forum.aspose.com/c/cells/9), waar u vragen kunt stellen en oplossingen kunt vinden.
### Kan ik Aspose.Cells gebruiken zonder licentie?
Ja, u kunt Aspose.Cells gratis gebruiken met bepaalde beperkingen, en u kunt beginnen met een[tijdelijke licentie](https://purchase.aspose.com/temporary-license/) voor volledige functionaliteit.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
