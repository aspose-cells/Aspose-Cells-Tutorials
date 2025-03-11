---
title: Pagina-afmetingen van werkblad ophalen
linktitle: Pagina-afmetingen van werkblad ophalen
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u pagina-afmetingen in een Excel-werkblad kunt krijgen met Aspose.Cells voor .NET. Een stapsgewijze handleiding om A2-, A3-, A4- en Letter-papierformaten aan te passen.
weight: 13
url: /nl/net/worksheet-page-setup-features/get-page-dimensions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pagina-afmetingen van werkblad ophalen

## Invoering
Als u programmatisch met Excel-bestanden werkt met Aspose.Cells voor .NET, kan het voorkomen dat u pagina-afmetingen van een werkblad moet openen en instellen. Het kennen van de afmetingen kan helpen bij lay-outs, afdrukken en het aanpassen van Excel-bladen voor specifieke doeleinden. In dit artikel onderzoeken we hoe u verschillende pagina-afmetingen in Excel kunt ophalen en weergeven met Aspose.Cells voor .NET. We doorlopen een stapsgewijze zelfstudie om ervoor te zorgen dat u alle details hebt om vol vertrouwen aan de slag te gaan.
## Vereisten
Voordat we beginnen, controleren we of je alles bij de hand hebt om deze tutorial te volgen.
1.  Aspose.Cells voor .NET: Zorg ervoor dat u Aspose.Cells voor .NET hebt geïnstalleerd. U kunt[download hier de bibliotheek](https://releases.aspose.com/cells/net/) of installeer het via NuGet in uw .NET-project.
2. .NET-omgeving: een compatibele .NET-ontwikkelomgeving (bijvoorbeeld Visual Studio).
3.  Licentie-instelling: Voor de volledige functionaliteit van Aspose.Cells, past u een licentie toe. U kunt[Vraag een gratis tijdelijke licentie aan](https://purchase.aspose.com/temporary-license/) voor evaluatiedoeleinden.
Begin met de gratis proefversie van Aspose.Cells als u het voor het eerst uitprobeert.
## Pakketten importeren
Voordat we met de code beginnen, moet u de Aspose.Cells-naamruimte in uw project importeren om toegang te krijgen tot alle benodigde klassen en methoden.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Laten we het proces opsplitsen in eenvoudige stappen. Hier zullen we verschillende papierformaten benaderen, ze toepassen op een werkblad en de afmetingen voor elk afdrukken.
## Stap 1: Maak een werkboekinstantie
 De eerste stap is het maken van een exemplaar van de`Workbook` klasse. Dit object zal fungeren als onze hoofdwerkmap met werkbladen die we kunnen manipuleren.
```csharp
Workbook book = new Workbook();
```
 Denk aan`Workbook` als de hoofdcontainer voor uw Excel-bestand. We hebben het nodig om toegang te krijgen tot individuele werkbladen en deze te beheren.
## Stap 2: Toegang tot het eerste werkblad
 Laten we nu het eerste werkblad in de werkmap openen. Standaard wordt een nieuwe werkmap geleverd met één werkblad, dus we kunnen er direct naar verwijzen met behulp van een index van`0`.
```csharp
Worksheet sheet = book.Worksheets[0];
```
 De`Worksheets` verzameling in`Workbook` geeft ons toegang tot elk werkblad via index. Hier pakken we het eerste werkblad om te beginnen met het instellen van pagina-afmetingen.
## Stap 3: Stel het papierformaat in op A2 en geef de afmetingen weer
Nu we toegang hebben tot ons werkblad, stellen we het papierformaat in op A2. Het instellen van het papierformaat is handig voor het formatteren van de pagina voordat u deze afdrukt of exporteert. Zodra we het papierformaat hebben ingesteld, drukken we de pagina-afmetingen af in inches.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
 Hier veranderen we de`PaperSize` eigendom van`PaperA2` Nadat u de grootte hebt ingesteld,`PageSetup.PaperWidth` En`PageSetup.PaperHeight` de breedte en hoogte van het vel in inches ophalen. Dit geeft ons een snel overzicht van de pagina-afmetingen.
## Stap 4: Stel het papierformaat in op A3 en geef de afmetingen weer
Volg dezelfde stappen als hierboven en pas de pagina-afmetingen aan naar A3-formaat. Deze wijziging is handig voor iets grotere afdrukken of om meer content op één pagina te passen.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
A3-formaat is twee keer zo groot als A4, wat het een goede keuze maakt voor grote tabellen of gedetailleerde grafieken. Door het papierformaat te wijzigen, kunt u de werkbladindeling hierop aanpassen.
## Stap 5: Stel het papierformaat in op A4 en geef de afmetingen weer
Laten we nu het papierformaat instellen op A4. Dit is het meest gebruikte paginaformaat voor het afdrukken van documenten. We zullen de bijgewerkte afmetingen later weergeven.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Als uw doel een standaard documentformaat is, is A4 doorgaans het meest geschikte formaat. De afmetingen kennen kan helpen bij het aanpassen van de inhoudsindeling om afdrukproblemen te voorkomen.
## Stap 6: Stel het papierformaat in op Letter en geef de afmetingen weer
Tot slot stellen we het papierformaat in op het Letter-formaat, dat veel wordt gebruikt in Noord-Amerika. Laten we de afmetingen nog een laatste keer afdrukken.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Het formaat Letter wordt veel gebruikt voor documenten in Noord-Amerika. Het instellen van dit formaat is handig bij samenwerking met teams of klanten die daar gevestigd zijn.
## Conclusie
In deze tutorial hebben we uitgelegd hoe u pagina-afmetingen voor verschillende papierformaten instelt en ophaalt met Aspose.Cells voor .NET. Door paginaformaten als A2, A3, A4 en Letter te configureren, kunt u Excel-werkbladen opmaken om te voldoen aan specifieke afdruk- en lay-outbehoeften. Deze controle over pagina-afmetingen is vooral waardevol voor professionele rapportage en presentatie, omdat het ervoor zorgt dat uw content perfect op elk paginaformaat past.
## Veelgestelde vragen
### Hoe kan ik de oriëntatie van de pagina in Aspose.Cells wijzigen?  
 U kunt de oriëntatie wijzigen met behulp van de`PageSetup.Orientation` eigenschap, door deze in te stellen op`PageOrientationType.Portrait` of`PageOrientationType.Landscape`.
### Kan ik aangepaste pagina-afmetingen instellen in Aspose.Cells?  
 Ja, u kunt aangepaste pagina-afmetingen instellen door de marges en schaalopties onder aan te passen`PageSetup` voor meer controle.
### Wat is het standaardpapierformaat in Aspose.Cells?  
Het standaard papierformaat is doorgaans A4. Dit kan echter afhankelijk zijn van regionale instellingen en kan indien nodig worden aangepast.
### Is het mogelijk om een voorbeeld van pagina-indelingen te bekijken in Aspose.Cells?  
Hoewel Aspose.Cells geen grafische voorvertoning biedt, kunt u in Excel wel programmatisch lay-outs instellen en afdrukvoorbeelden gebruiken.
### Hoe installeer ik Aspose.Cells voor .NET?  
 U kunt Aspose.Cells installeren met NuGet Package Manager in Visual Studio of de DLL downloaden van de[Aspose.Cells downloadpagina](https://releases.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
