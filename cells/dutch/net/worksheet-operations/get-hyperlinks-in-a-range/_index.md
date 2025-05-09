---
"description": "Haal eenvoudig hyperlinks uit Excel-bestanden en beheer ze met Aspose.Cells voor .NET. Inclusief stapsgewijze handleiding en codevoorbeelden."
"linktitle": "Hyperlinks in een bereik ophalen in .NET"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Hyperlinks in een bereik ophalen in .NET"
"url": "/nl/net/worksheet-operations/get-hyperlinks-in-a-range/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Hyperlinks in een bereik ophalen in .NET

## Invoering
Heb je je ooit verdiept in spreadsheets en je afgevraagd hoe je efficiënt hyperlinks kunt extraheren? Zo ja, dan ben je hier aan het juiste adres! In deze handleiding leiden we je door het proces om hyperlinks binnen een bepaald bereik te verkrijgen met Aspose.Cells voor .NET. Deze krachtige bibliotheek neemt de vervelende taak van het werken met Excel-bestanden uit handen en maakt het gemakkelijk om hyperlinks op te halen en zelfs te verwijderen. Dus pak een kop koffie en duik in de wereld van Aspose.Cells!
## Vereisten
Voordat we in de details van het coderen duiken, zijn er een paar vereisten waaraan je moet voldoen. Maak je geen zorgen, dit is geen lange lijst!
### Maak uw ontwikkelomgeving gereed
1. .NET Framework: Zorg ervoor dat u een compatibele .NET-omgeving op uw computer hebt geïnstalleerd. Dit kan .NET Core of het volledige .NET Framework zijn. Zorg ervoor dat uw versie de Aspose.Cells-bibliotheek ondersteunt.
2. Aspose.Cells-bibliotheek: Je hebt de Aspose.Cells-bibliotheek nodig. Je kunt de nieuwste versie downloaden van [hier](https://releases.aspose.com/cells/net/)Als u net begint, overweeg dan om de [gratis proefperiode](https://releases.aspose.com/) om het water te testen.
3. IDE: Een goede Integrated Development Environment (IDE) zoals Visual Studio maakt je leven een stuk makkelijker. Hiermee kun je soepel code schrijven, debuggen en uitvoeren.
4. Basiskennis van C#: Kennis van C#-programmering is nuttig, maar als u bereid bent om te leren, kunt u aan de slag!
Met deze vereisten zijn we klaar om te beginnen. Laten we beginnen met wat basiscodering: de benodigde pakketten importeren en ons voorbeeld stap voor stap analyseren.
## Pakketten importeren
Een van de eerste stappen in het coderen is het importeren van de benodigde pakketten. Je moet een verwijzing naar de Aspose.Cells-bibliotheek in je project toevoegen. Dit kan meestal via NuGet Package Manager. Zo doe je dat:
1. Visual Studio openen.
2. Klik op uw project in de Solution Explorer.
3. Klik met de rechtermuisknop en selecteer NuGet-pakketten beheren.
4. Zoek naar “Aspose.Cells” en installeer het.
```csharp
using System.IO;
using System;
using Aspose.Cells;
```
Nu de bibliotheek klaar is, kunnen we aan de code beginnen om hyperlinks te extraheren!
## Stap 1: Stel uw directorypaden in
Laten we beginnen met het definiëren van het pad van uw documenten. U wilt de bronmap instellen waar uw Excel-bestand zich bevindt en de uitvoermap waar het verwerkte bestand wordt opgeslagen.
```csharp
// Het pad naar de documentenmap.
string sourceDir = "Your Document Directory"; // Verander dit naar het pad van uw Excel-bestand
// Uitvoermap
string outputDir = "Your Document Directory"; // Zorg ervoor dat deze methode een geldig uitvoerpad biedt
```
Vervang in dit fragment `"Your Document Directory"` met het daadwerkelijke pad naar de map met het Excel-bestand. Dit is vergelijkbaar met het voorbereiden van het podium vóór je optreden: het is cruciaal om te weten waar je materialen zijn.
## Stap 2: Het werkmapobject instantiëren
Vervolgens maken we een `Workbook` object om het Excel-bestand te openen waarmee we werken.
```csharp
// Een werkmapobject instantiëren
// Open een Excel-bestand
Workbook workbook = new Workbook(sourceDir + "HyperlinksSample.xlsx");
```
Hier creëren we een nieuwe `Workbook` bijvoorbeeld. De `Workbook` De klasse is in feite uw toegangspoort tot alle bewerkingen met betrekking tot een Excel-bestand. U kunt het zien als het openen van het boek dat al uw inhoud bevat.
## Stap 3: Toegang tot het werkblad
Nu we de werkmap klaar hebben, gaan we het eerste werkblad eruit halen. In Excel zijn werkbladen net als pagina's in je boek, en we moeten aangeven op welke pagina we werken.
```csharp
// Ontvang het eerste (standaard) werkblad
Worksheet worksheet = workbook.Worksheets[0];
```
Door toegang te krijgen tot `Worksheets[0]`we kiezen het eerste werkblad. Werkbladen worden geïndexeerd vanaf nul, dus zorg ervoor dat je het juiste kiest.
## Stap 4: Een bereik maken
Nu is het tijd om een bereik te definiëren waarin we naar hyperlinks willen zoeken. Stel dat we in ons geval in de cellen A2 tot en met B3 willen zoeken.
```csharp
// Maak een bereik A2:B3
Range range = worksheet.Cells.CreateRange("A2", "B3");
```
Door te bellen `CreateRange`, specificeren we de begin- en eindcellen. Dit is waar de magie gebeurt: we controleren later de hyperlinks in dit opgegeven bereik.
## Stap 5: Hyperlinks ophalen uit het bereik
In deze stap krijgen we daadwerkelijk toegang tot de hyperlinks in het door ons gedefinieerde bereik.
```csharp
// Hyperlinks binnen bereik krijgen
Hyperlink[] hyperlinks = range.Hyperlinks;
```
De `Hyperlinks` eigendom van een `Range` object retourneert een array van `Hyperlink` objecten die in dat bereik voorkomen. Het is alsof je alle belangrijke notities in één keer van je pagina pakt!
## Stap 6: Loop door en geef links weer
Laten we nu de opgehaalde hyperlinks doorlopen. We zullen hun adressen en gebieden voorlopig in de console weergeven.
```csharp
foreach (Hyperlink link in hyperlinks)
{
    Console.WriteLine(link.Area + " : " + link.Address);
}
```
Hier doorlopen we elke hyperlink en geven we het gebied en adres ervan weer. Het is vergelijkbaar met het hardop voorlezen van de belangrijke details van elke hyperlink die je hebt gevonden. 
## Stap 7: Optioneel - Hyperlinks verwijderen
Indien nodig kun je hyperlinks eenvoudig uit je bereik verwijderen! Dit kan superhandig zijn als je je spreadsheet wilt opschonen.
```csharp
foreach (Hyperlink link in hyperlinks)
{
    // Gebruik de methode Hyperlink.Delete() om de koppeling te verwijderen.
    link.Delete();
}
```
Met behulp van de `Delete()` Met de methode op elke hyperlink kunt u hyperlinks verwijderen die u mogelijk niet meer nodig hebt. Het is alsof u een overbodige krabbel van uw pagina verwijdert.
## Stap 8: Sla uw wijzigingen op
Ten slotte slaan we de werkmap op met alle aanpassingen die we hebben gemaakt.
```csharp
workbook.Save(outputDir + "HyperlinksSample_out.xlsx");
```
Deze regel code slaat je gewijzigde werkmap op in de opgegeven uitvoermap. Dit is jouw manier om de aangebrachte wijzigingen te publiceren, net zoals je het boek sluit na de laatste bewerkingen.
## Conclusie
En voilà: een uitgebreide stapsgewijze handleiding voor het extraheren van hyperlinks uit een bepaald bereik in een Excel-sheet met Aspose.Cells voor .NET! U hebt geleerd hoe u uw omgeving instelt, de code schrijft en bewerkingen uitvoert op hyperlinks in een Excel-werkmap. Of u nu gegevens beheert voor zakelijke of persoonlijke projecten, deze tool kan u op de lange termijn enorm veel tijd besparen.
## Veelgestelde vragen
### Wat is Aspose.Cells?
Aspose.Cells is een .NET-bibliotheek waarmee u Excel-bestanden kunt bewerken zonder dat u Microsoft Excel op uw computer hoeft te installeren.
### Kan ik Aspose.Cells gratis gebruiken?
Ja, er is een gratis proefversie beschikbaar, zodat u de functies kunt uitproberen voordat u tot aankoop overgaat.
### Zijn er beperkingen in de proefversie?
Er kunnen enkele functionaliteitsbeperkingen gelden voor de proefversie, zoals watermerken op opgeslagen bestanden.
### Moet ik programmeren om Aspose.Cells te gebruiken?
Om de bibliotheek effectief te kunnen gebruiken, wordt basiskennis van programmeren in C# of .NET aanbevolen.
### Hoe kan ik ondersteuning krijgen als ik problemen heb met Aspose.Cells?
U kunt toegang krijgen tot het ondersteuningsforum [hier](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}