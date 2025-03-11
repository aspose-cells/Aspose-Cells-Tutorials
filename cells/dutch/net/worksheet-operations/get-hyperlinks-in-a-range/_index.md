---
title: Hyperlinks in een bereik in .NET ophalen
linktitle: Hyperlinks in een bereik in .NET ophalen
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Haal eenvoudig hyperlinks uit Excel-bestanden en beheer ze met Aspose.Cells voor .NET. Inclusief stapsgewijze handleiding en codevoorbeelden.
weight: 10
url: /nl/net/worksheet-operations/get-hyperlinks-in-a-range/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hyperlinks in een bereik in .NET ophalen

## Invoering
Heb je jezelf ooit verdronken in spreadsheets en je afgevraagd hoe je efficiënt hyperlinks kunt extraheren? Dan ben je hier aan het juiste adres! In deze gids leiden we je door het proces om hyperlinks in een bepaald bereik te krijgen met Aspose.Cells voor .NET. Deze krachtige bibliotheek neemt de vervelende taak uit het werken met Excel-bestanden, waardoor het gemakkelijk voor je wordt om hyperlinks op te halen en zelfs te verwijderen. Pak dus een kop koffie en laten we duiken in de wereld van Aspose.Cells!
## Vereisten
Voordat we in de details van het coderen duiken, zijn er een paar vereisten die je moet hebben. Maak je geen zorgen, dit is geen lange lijst!
### Maak uw ontwikkelomgeving gereed
1. .NET Framework: Zorg ervoor dat u een compatibele .NET-omgeving op uw machine hebt ingesteld. Dit kan .NET Core of het volledige .NET Framework zijn. Zorg ervoor dat uw versie de Aspose.Cells-bibliotheek ondersteunt.
2.  Aspose.Cells Library: U hebt de Aspose.Cells-bibliotheek nodig. U kunt de nieuwste versie downloaden van[hier](https://releases.aspose.com/cells/net/) Als u net begint, overweeg dan om de[gratis proefperiode](https://releases.aspose.com/) om het water te testen.
3. IDE: Een goede Integrated Development Environment (IDE) zoals Visual Studio maakt uw leven makkelijker. Hiermee kunt u uw code soepel schrijven, debuggen en uitvoeren.
4. Basiskennis van C#: Kennis van C#-programmering is nuttig, maar als u bereid bent om te leren, bent u klaar om te gaan!
Met deze vereisten op hun plaats, zijn we klaar om te gaan. Laten we doorgaan met wat fundamentele codering: de benodigde pakketten importeren en ons voorbeeld stap voor stap opsplitsen.
## Pakketten importeren
Een van de eerste stappen in het coderen is het importeren van de benodigde pakketten. U moet een referentie toevoegen aan de Aspose.Cells-bibliotheek in uw project. Dit kan doorgaans worden gedaan via NuGet Package Manager. Dit is hoe u het doet:
1. Open Visual Studio.
2. Klik op uw project in de Solution Explorer.
3. Klik met de rechtermuisknop en selecteer NuGet-pakketten beheren.
4. Zoek naar “Aspose.Cells” en installeer het.
```csharp
using System.IO;
using System;
using Aspose.Cells;
```
Nu de bibliotheek klaar is, kunnen we aan de slag met de code om hyperlinks te extraheren!
## Stap 1: Stel uw directorypaden in
Laten we beginnen met het definiëren van het pad van uw documenten. U wilt de bronmap instellen waar uw Excel-bestand zich bevindt en de uitvoermap waar het verwerkte bestand wordt opgeslagen.
```csharp
// Het pad naar de documentenmap.
string sourceDir = "Your Document Directory"; // Wijzig dit naar het pad van uw Excel-bestand
// Uitvoermap
string outputDir = "Your Document Directory"; // Zorg ervoor dat deze methode een geldig uitvoerpad biedt
```
 Vervang in dit fragment`"Your Document Directory"` met het daadwerkelijke pad naar uw directory met het Excel-bestand. Dit is net als het opzetten van het podium voor uw optreden: het is cruciaal om te weten waar uw materialen zijn.
## Stap 2: Instantieer het werkmapobject
 Vervolgens maken we een`Workbook` object om het Excel-bestand te openen waarmee we werken.
```csharp
// Een werkmapobject instantiëren
// Open een Excel-bestand
Workbook workbook = new Workbook(sourceDir + "HyperlinksSample.xlsx");
```
 Hier creëren we een nieuwe`Workbook` voorbeeld. De`Workbook`class is in feite uw toegangspoort tot alle bewerkingen met betrekking tot een Excel-bestand. U kunt het zien als het openen van het boek dat al uw inhoud bevat.
## Stap 3: Toegang tot het werkblad
Nu we de werkmap klaar hebben, gaan we het eerste werkblad eruit halen. In Excel zijn werkbladen als pagina's in je boek, en we moeten aangeven op welke pagina we werken.
```csharp
// Ontvang het eerste (standaard) werkblad
Worksheet worksheet = workbook.Worksheets[0];
```
 Door toegang te krijgen`Worksheets[0]`, we kiezen het eerste werkblad. Werkbladen worden geïndexeerd vanaf nul, dus zorg ervoor dat je de juiste selecteert.
## Stap 4: Een bereik maken
Nu is het tijd om een bereik te definiëren waarin we willen zoeken naar hyperlinks. In ons geval willen we bijvoorbeeld kijken in de cellen A2 tot en met B3.
```csharp
// Maak een bereik A2:B3
Range range = worksheet.Cells.CreateRange("A2", "B3");
```
 Door te bellen`CreateRange`, specificeren we de begin- en eindcellen. Dit is waar de magie gebeurt: we zullen later de hyperlinks controleren die zich in dit opgegeven bereik bevinden.
## Stap 5: Hyperlinks ophalen uit het bereik
In deze stap krijgen we daadwerkelijk toegang tot de hyperlinks in ons gedefinieerde bereik.
```csharp
//Hyperlinks binnen bereik krijgen
Hyperlink[] hyperlinks = range.Hyperlinks;
```
 De`Hyperlinks` eigendom van een`Range` object retourneert een array van`Hyperlink`objecten die in dat bereik te vinden zijn. Het is alsof je alle belangrijke notities van je pagina in één keer pakt!
## Stap 6: Loop door en geef links weer
Laten we nu door de opgehaalde hyperlinks itereren. We zullen hun adressen en gebieden voor nu in de console afdrukken.
```csharp
foreach (Hyperlink link in hyperlinks)
{
    Console.WriteLine(link.Area + " : " + link.Address);
}
```
Hier doorlopen we elke hyperlink en tonen we het gebied en adres ervan. Het is vergelijkbaar met het hardop voorlezen van de belangrijke details van elke hyperlink die u hebt gevonden. 
## Stap 7: Optioneel - Hyperlinks verwijderen
Indien nodig kunt u eenvoudig hyperlinks uit uw bereik verwijderen! Dit kan superhandig zijn als u uw spreadsheet wilt opschonen.
```csharp
foreach (Hyperlink link in hyperlinks)
{
    // Gebruik de methode Hyperlink.Delete() om de koppeling te verwijderen.
    link.Delete();
}
```
 Met behulp van de`Delete()` methode op elke hyperlink kunt u hyperlinks verwijderen die u mogelijk niet meer nodig hebt. Het is alsof u een krabbeltje verwijdert dat u niet meer nodig hebt van uw pagina.
## Stap 8: Sla uw wijzigingen op
Tot slot slaan we de werkmap op met alle aanpassingen die we hebben gemaakt.
```csharp
workbook.Save(outputDir + "HyperlinksSample_out.xlsx");
```
Deze regel code slaat uw aangepaste werkmap op in de opgegeven uitvoermap. Dit is uw manier om de wijzigingen die u hebt aangebracht te publiceren, zoals het boek sluiten na de laatste bewerkingen.
## Conclusie
En daar heb je het: een uitgebreide stapsgewijze handleiding voor het extraheren van hyperlinks uit een opgegeven bereik in een Excel-sheet met Aspose.Cells voor .NET! Je hebt geleerd hoe je je omgeving instelt, de code schrijft en bewerkingen uitvoert op hyperlinks in een Excel-werkmap. Of je nu gegevens beheert voor zakelijke of persoonlijke projecten, deze tool kan je op de lange termijn enorm veel tijd besparen.
## Veelgestelde vragen
### Wat is Aspose.Cells?
Aspose.Cells is een .NET-bibliotheek waarmee u Excel-bestanden kunt bewerken zonder dat u Microsoft Excel op uw computer hoeft te installeren.
### Kan ik Aspose.Cells gratis gebruiken?
Ja, er is een gratis proefversie beschikbaar, zodat u de functies kunt uitproberen voordat u tot aankoop overgaat.
### Zijn er beperkingen in de proefversie?
De proefversie kan enkele functionele beperkingen hebben, zoals watermerken op opgeslagen bestanden.
### Moet ik kunnen programmeren om Aspose.Cells te gebruiken?
Om de bibliotheek effectief te kunnen gebruiken, wordt basiskennis van programmeren in C# of .NET aanbevolen.
### Hoe kan ik ondersteuning krijgen als ik problemen heb met Aspose.Cells?
 U kunt toegang krijgen tot het ondersteuningsforum[hier](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
