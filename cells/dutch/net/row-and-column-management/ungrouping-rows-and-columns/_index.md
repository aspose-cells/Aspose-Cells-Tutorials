---
"description": "Leer hoe u rijen en kolommen in Excel kunt degroeperen met Aspose.Cells voor .NET met deze uitgebreide handleiding. Vereenvoudig uw Excel-gegevensmanipulatie."
"linktitle": "Rijen en kolommen in Excel degroeperen met Aspose.Cells"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Rijen en kolommen in Excel degroeperen met Aspose.Cells"
"url": "/nl/net/row-and-column-management/ungrouping-rows-and-columns/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Rijen en kolommen in Excel degroeperen met Aspose.Cells

## Invoering
Bij het werken met Excel-bestanden kom je soms situaties tegen waarin je rijen en kolommen moet degroeperen. Of je nu een spreadsheet wilt opschonen of gegevens wilt herformatteren voor een betere presentatie, Aspose.Cells voor .NET is een fantastische tool die het proces vereenvoudigt. In deze tutorial begeleid ik je door de stappen om rijen en kolommen in Excel te degroeperen met behulp van Aspose.Cells. Aan het einde heb je een gedegen begrip van hoe je programmatisch met Excel-bestanden kunt werken.
## Vereisten
Voordat we de code induiken, zorgen we ervoor dat alles klaar staat. Dit heb je nodig:
1. Visual Studio: Er zou een werkende versie van Visual Studio op uw computer geïnstalleerd moeten zijn. Als u deze nog niet hebt, kunt u deze downloaden van [De site van Visual Studio](https://visualstudio.microsoft.com/).
2. Aspose.Cells voor .NET: Je moet de Aspose.Cells-bibliotheek downloaden. Je kunt deze vinden op de [Aspose Releases-pagina](https://releases.aspose.com/cells/net/)Zorg ervoor dat u over de benodigde licenties beschikt, die u kunt aanschaffen of verkrijgen via een [tijdelijke licentie](https://purchase.aspose.com/temporary-license/).
3. Basiskennis van C#: Met een basiskennis van C#-programmering kunt u de cursus gemakkelijker volgen.
Zodra je alles klaar hebt, kunnen we beginnen met het leukste gedeelte: de code!
## Pakketten importeren
Om te beginnen moet je de benodigde pakketten in je C#-project importeren. Zo doe je dat:
1. Open uw project in Visual Studio.
2. Voeg een verwijzing toe aan de Aspose.Cells-bibliotheek. U kunt dit doen door met de rechtermuisknop op de verwijzingen in uw project te klikken en 'Verwijzing toevoegen' te selecteren. Blader naar de locatie waar u de Aspose.Cells-DLL hebt opgeslagen.
3. Voeg bovenaan uw C#-bestand het volgende toe met behulp van richtlijnen:
```csharp
using System.IO;
using Aspose.Cells;
```
Nu alles is ingesteld, doorlopen we de stappen om rijen en kolommen in uw Excel-werkblad te degroeperen. 
## Stap 1: Definieer de documentmap
Eerst moet u de map opgeven waar uw Excel-bestand zich bevindt. U kunt dit als volgt instellen:
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
```
Vervangen `"Your Document Directory"` met het werkelijke pad op uw computer waar het Excel-bestand is opgeslagen. 
## Stap 2: Een bestandsstroom maken
Vervolgens moet je een bestandsstroom aanmaken om het Excel-bestand te openen. Zo doe je dat:
```csharp
// Een bestandsstroom maken met het te openen Excel-bestand
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
Hier opent u het bestand met de naam `book1.xls`Zorg ervoor dat dit bestand in de opgegeven directory staat, anders krijg je de foutmelding dat het bestand niet is gevonden.
## Stap 3: Een werkmapobject instantiëren
Laten we nu het Excel-bestand in een werkmapobject laden. Dit stelt je in staat om de werkmap programmatisch te bewerken:
```csharp
// Een werkmapobject instantiëren
// Het Excel-bestand openen via de bestandsstroom
Workbook workbook = new Workbook(fstream);
```
Met deze coderegel hebt u het Excel-bestand succesvol in het geheugen geladen en kunt u ermee aan de slag.
## Stap 4: Toegang tot het werkblad
Nadat je de werkmap hebt, is de volgende stap het openen van het specifieke werkblad waarvan je de rijen en kolommen wilt degroeperen. Zo doe je dat:
```csharp
// Toegang krijgen tot het eerste werkblad in het Excel-bestand
Worksheet worksheet = workbook.Worksheets[0];
```
In dit geval gebruiken we het eerste werkblad. Als uw gegevens zich op een ander werkblad bevinden, kunt u de index dienovereenkomstig wijzigen.
## Stap 5: Rijen degroeperen
Nu komt het spannende gedeelte! Laten we de eerste zes rijen (van rij 0 tot rij 5) degroeperen. Gebruik de volgende code:
```csharp
// Groepering van de eerste zes rijen opheffen (van 0 tot 5)
worksheet.Cells.UngroupRows(0, 5);
```
Deze methode verwijdert alle groeperingen die op de opgegeven rijen zijn toegepast. Zo eenvoudig is het!
## Stap 6: Kolommen degroeperen
Net als bij rijen kun je ook kolommen degroeperen. Zo degroepeer je de eerste drie kolommen (van kolom 0 tot kolom 2):
```csharp
// Groepering van de eerste drie kolommen opheffen (van 0 naar 2)
worksheet.Cells.UngroupColumns(0, 2);
```
## Stap 7: Sla het gewijzigde Excel-bestand op
Nadat u de rijen en kolommen hebt gedegroepeerd, is de volgende stap het opslaan van de wijzigingen in een Excel-bestand. U kunt dit doen met behulp van de `Save` methode:
```csharp
// Het gewijzigde Excel-bestand opslaan
workbook.Save(dataDir + "output.xls");
```
In dit voorbeeld slaan we het gewijzigde bestand op als `output.xls`U kunt de bestandsnaam naar wens wijzigen.
## Stap 8: Sluit de bestandsstroom
Om bronnen vrij te maken, moet u ten slotte de bestandsstroom sluiten:
```csharp
// De bestandsstroom sluiten om alle bronnen vrij te maken
fstream.Close();
```
Dit is een goede gewoonte om ervoor te zorgen dat uw toepassing bestands-handles niet langer vasthoudt dan nodig is.
## Conclusie
En voilà! Je hebt met succes geleerd hoe je rijen en kolommen in een Excel-bestand kunt degroeperen met Aspose.Cells voor .NET. Met slechts een paar regels code kun je programmatisch belangrijke wijzigingen in je Excel-bestanden aanbrengen. Of je nu rapporten automatiseert of gegevens voorbereidt voor analyse, het beheersen van deze technieken kan je veel tijd besparen.
## Veelgestelde vragen
### Wat is Aspose.Cells?
Aspose.Cells is een krachtige bibliotheek voor het werken met Excel-bestanden in .NET-toepassingen, waarmee u eenvoudig spreadsheets kunt bewerken, converteren en maken.
### Kan ik rijen en kolommen in Excel degroeperen met behulp van andere bibliotheken?
Ja, er zijn andere bibliotheken beschikbaar voor Excel-manipulatie in .NET, maar Aspose.Cells biedt uitgebreide functies en gebruiksgemak.
### Is er een manier om wijzigingen ongedaan te maken nadat ik ze heb opgeslagen?
Zodra u een Excel-bestand opslaat, kunt u de vorige status niet meer herstellen, tenzij u een back-up van het oorspronkelijke bestand hebt.
### Hoe krijg ik ondersteuning voor Aspose.Cells?
U kunt ondersteuning vinden door de [Aspose Supportforum](https://forum.aspose.com/c/cells/9), waar u vragen kunt stellen en oplossingen kunt vinden.
### Kan ik Aspose.Cells gebruiken zonder licentie?
Ja, u kunt Aspose.Cells gratis gebruiken met bepaalde beperkingen, en u kunt beginnen met een [tijdelijke licentie](https://purchase.aspose.com/temporary-license/) voor volledige functionaliteit.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}