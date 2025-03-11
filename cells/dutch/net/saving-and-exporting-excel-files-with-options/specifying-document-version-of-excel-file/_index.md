---
title: Documentversie van Excel-bestand programmatisch specificeren in .NET
linktitle: Documentversie van Excel-bestand programmatisch specificeren in .NET
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u documenteigenschappen zoals versie, auteur en titel programmatisch kunt opgeven in een Excel-bestand met behulp van Aspose.Cells voor .NET, met stapsgewijze instructies.
weight: 12
url: /nl/net/saving-and-exporting-excel-files-with-options/specifying-document-version-of-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Documentversie van Excel-bestand programmatisch specificeren in .NET

## Invoering
Aspose.Cells voor .NET is een krachtige bibliotheek waarmee ontwikkelaars eenvoudig Excel-bestanden programmatisch kunnen manipuleren. Of u nu Excel-bestanden vanaf nul wilt maken of bestaande bestanden wilt wijzigen, Aspose.Cells biedt een uitgebreide API om uw doelen te bereiken. Een van die functies is het specificeren van documenteigenschappen zoals versie, auteur of titel. Deze tutorial leidt u door het programmatisch specificeren van de documentversie van een Excel-bestand met behulp van Aspose.Cells voor .NET.
## Vereisten
Voordat we in de details duiken, willen we ervoor zorgen dat je alles hebt wat je nodig hebt om deze tutorial te volgen:
1. Aspose.Cells voor .NET: U kunt de nieuwste versie downloaden[hier](https://releases.aspose.com/cells/net/) Als u nog geen licentie hebt gekocht, kunt u kiezen voor een[tijdelijke licentie](https://purchase.aspose.com/temporary-license/) om de functies te verkennen.
2. .NET-ontwikkelomgeving: u kunt Visual Studio of een andere .NET-compatibele IDE gebruiken.
3. Basiskennis van C#: Als u de C#-programmering begrijpt, is het gemakkelijker om de cursus te volgen.
## Pakketten importeren
Voordat u kunt beginnen met coderen, moet u de benodigde naamruimten importeren uit de Aspose.Cells-bibliotheek. Dit geeft u toegang tot de klassen en methoden die nodig zijn voor Excel-bestandsmanipulatie.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Deze twee naamruimten zijn essentieel voor de interactie met de werkmap en de ingebouwde documenteigenschappen.
Laten we nu het proces van het specificeren van documenteigenschappen in een Excel-bestand, waaronder de versie, titel en auteur, eens nader bekijken.
## Stap 1: Initialiseer het werkmapobject
 De eerste stap is het maken van een nieuw exemplaar van de`Workbook` object. Dit object vertegenwoordigt het volledige Excel-bestand waarmee u gaat werken.
```csharp
Workbook wb = new Workbook();
```
 De`Workbook`klasse biedt een representatie van een Excel-bestand. Door het te instantiëren, maken we een lege Excel-werkmap die we kunnen manipuleren.
## Stap 2: Toegang tot ingebouwde documenteigenschappen
 Aspose.Cells biedt ingebouwde documenteigenschappen, waaronder velden zoals titel, auteur en documentversie. U kunt deze eigenschappen openen via de`BuiltInDocumentProperties`verzameling.
```csharp
Aspose.Cells.Properties.BuiltInDocumentPropertyCollection bdpc = wb.BuiltInDocumentProperties;
```
 De`BuiltInDocumentPropertyCollection` klasse biedt toegang tot een verzameling ingebouwde documenteigenschappen, zoals de titel, auteur en andere metagegevens die doorgaans aan het document worden gekoppeld.
## Stap 3: Stel de titel van het Excel-document in
Vervolgens stellen we de titel van het Excel-document in. Deze metadata helpt bij het identificeren en beheren van het bestand later.
```csharp
bdpc.Title = "Aspose File Format APIs";
```
Het instellen van de titel is belangrijk voor de organisatie van het document. Deze metadata is te zien in bestandseigenschappen en kan door externe systemen worden gebruikt om het document effectiever te catalogiseren of identificeren.
## Stap 4: Geef de auteur op
U kunt ook de auteur van het document opgeven, zodat duidelijk is wie het bestand heeft gemaakt of gewijzigd.
```csharp
bdpc.Author = "Aspose APIs Developers";
```
Met deze stap kunt u het document toewijzen aan de maker en aanvullende metagegevens verstrekken voor documentbeheer of samenwerkingsscenario's.
## Stap 5: Geef de documentversie op
Een van de meest cruciale eigenschappen die we in deze tutorial behandelen, is de documentversie. Met deze stap kunt u de versie van het document opgeven, wat handig is wanneer u werkt in omgevingen die versiebeheer vereisen.
```csharp
bdpc.DocumentVersion = "Aspose.Cells Version - 18.3";
```
Het instellen van de documentversie biedt duidelijkheid over welke versie van het document of de bibliotheek is gebruikt om het bestand te maken. Dit is met name belangrijk in omgevingen die bestandsrevisies of compatibiliteit met verschillende bibliotheekversies moeten bijhouden.
## Stap 6: Sla het Excel-bestand op
 Ten slotte kunt u het Excel-bestand opslaan met alle eigenschappen die u zojuist hebt ingesteld. Met Aspose.Cells kunt u het bestand in verschillende formaten opslaan, maar voor dit voorbeeld houden we het bij de`.xlsx` formaat.
```csharp
wb.Save("outputSpecifyDocumentVersionOfExcelFile.xlsx", SaveFormat.Xlsx);
```
 De`Save` methode wordt gebruikt om het bestand op te slaan in de door u opgegeven directory. Hier slaan we het op als een Excel-bestand in de`.xlsx`formaat. Indien nodig ondersteunt Aspose.Cells ook formaten zoals`.xls`, `.csv` , En`.pdf`, wat flexibiliteit biedt op basis van uw projectbehoeften.
## Conclusie
In deze tutorial hebben we uitgelegd hoe u documenteigenschappen, met name de documentversie, in een Excel-bestand kunt opgeven met Aspose.Cells voor .NET. Aspose.Cells is een uiterst flexibele en krachtige tool waarmee u Excel-bestanden programmatisch kunt bewerken. Dit is een geweldige aanwinst voor elke .NET-ontwikkelaar die met spreadsheets werkt.
## Veelgestelde vragen
### Kan ik andere ingebouwde eigenschappen wijzigen met Aspose.Cells?  
Ja, u kunt andere ingebouwde eigenschappen wijzigen, zoals het onderwerp, trefwoorden en opmerkingen.
### Welke bestandsformaten worden ondersteund door Aspose.Cells?  
 Aspose.Cells ondersteunt een breed scala aan formaten, waaronder`.xls`, `.xlsx`, `.csv`, `.pdf`, en meer.
### Heb ik een licentie nodig om Aspose.Cells voor .NET te gebruiken?  
 Je kunt Aspose.Cells verkennen met een[gratis proefperiode](https://releases.aspose.com/) of een aanvraag indienen voor een[tijdelijke licentie](https://purchase.aspose.com/temporary-license/) voor uitgebreide tests.
### Kan ik Aspose.Cells gebruiken in een webapplicatie?  
Ja, Aspose.Cells kan worden gebruikt in zowel desktop- als webapplicaties. Het is zeer veelzijdig en integreert goed met .NET webframeworks.
### Waar kan ik ondersteuning krijgen voor Aspose.Cells?  
 U kunt toegang krijgen tot de community en ondersteuning via de[Aspose.Cells ondersteuningsforum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
