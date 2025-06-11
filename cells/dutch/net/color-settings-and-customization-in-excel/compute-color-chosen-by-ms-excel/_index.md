---
"description": "Leer hoe u de door MS Excel gekozen kleur berekent met Aspose.Cells voor .NET. Volg deze stapsgewijze handleiding om programmatisch toegang te krijgen tot de voorwaardelijke opmaakkleur van Excel."
"linktitle": "Bereken de door MS Excel gekozen kleur programmatisch"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Bereken de door MS Excel gekozen kleur programmatisch"
"url": "/nl/net/color-settings-and-customization-in-excel/compute-color-chosen-by-ms-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Bereken de door MS Excel gekozen kleur programmatisch

## Invoering
Heb je ooit met Excel-bestanden gewerkt en je afgevraagd hoe bepaalde kleuren automatisch worden geselecteerd voor opmaak? Je bent niet de enige. De voorwaardelijke opmaak van Excel kan een beetje een mysterie zijn, vooral wanneer je probeert de exacte kleur te achterhalen die Excel toewijst. Maar maak je geen zorgen, wij helpen je! In deze tutorial duiken we diep in hoe je de door MS Excel gekozen kleur programmatisch kunt berekenen met Aspose.Cells voor .NET. We leggen het stap voor stap uit, zodat je het kunt volgen en gemakkelijk kunt toepassen op je eigen projecten. Laten we beginnen!
## Vereisten
Voordat we in de code duiken, bespreken we wat je nodig hebt om deze tutorial te volgen:
- Aspose.Cells voor .NET geïnstalleerd. Als je het nog niet hebt, kun je... [download het hier](https://releases.aspose.com/cells/net/).
- Werkkennis van C# en .NET Framework.
- Een voorbeeld van een Excel-bestand (Book1.xlsx) met voorwaardelijke opmaak toegepast.
Je kunt ook de gratis proefversie van Aspose.Cells voor .NET uitproberen als je nog geen licentie hebt. Download de proefversie [hier](https://releases.aspose.com/).
## Pakketten importeren
Voordat we beginnen met coderen, moeten we de benodigde pakketten importeren om ervoor te zorgen dat alles soepel verloopt. Zorg ervoor dat je de volgende naamruimten in je project opneemt:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using System;
```
Deze imports bieden toegang tot de belangrijkste Aspose.Cells-klassen en de systeemeigen tekenbibliotheek van .NET voor het verwerken van kleuren.

Nu we alles op zijn plaats hebben, kunnen we de taak opdelen in behapbare stappen:
## Stap 1: Het werkmapobject instellen
Het eerste wat we moeten doen is een instantie maken van `Workbook` object en laad het Excel-bestand waarmee we willen werken. Dit is waar de reis begint!
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
// Een werkmapobject instantiëren en het sjabloonbestand openen
Workbook workbook = new Workbook(dataDir + "Book1.xlsx");
```
In deze stap maken we een nieuw exemplaar van de `Workbook` klasse van Aspose.Cells. De `Workbook` klasse vertegenwoordigt een Excel-bestand en door het pad naar ons bestand op te geven, kunnen we het eenvoudig laden voor verdere bewerking.
## Stap 2: Toegang tot het eerste werkblad
Zodra de werkmap is geladen, moeten we het specifieke werkblad openen waar we de kleur uit willen halen. In dit voorbeeld werken we met het eerste werkblad.
```csharp
// Ontvang het eerste werkblad
Worksheet worksheet = workbook.Worksheets[0];
```
Hier halen we het eerste werkblad in de werkmap op met behulp van de `Worksheets[0]` index. Met Aspose.Cells kunt u elk werkblad in het Excel-bestand openen via de index of naam.
## Stap 3: Selecteer de cel van interesse
Vervolgens kiezen we een specifieke cel in het werkblad. Voor deze tutorial concentreren we ons op cel "A1", maar je kunt elke cel met voorwaardelijke opmaak selecteren.
```csharp
// Haal de A1-cel
Cell a1 = worksheet.Cells["A1"];
```
Wij gebruiken de `Cells` Eigenschap om naar een specifieke cel te verwijzen via het adres. In dit geval selecteren we cel "A1" omdat we de resultaten van de voorwaardelijke opmaak die op deze cel is toegepast, willen extraheren.
## Stap 4: Het resultaat van de voorwaardelijke opmaak ophalen
En nu komt de magie! We gebruiken Aspose.Cells om het resultaat van de voorwaardelijke opmaak voor de geselecteerde cel te bepalen. Zo berekent Excel de opmaak dynamisch, inclusief kleuren.
```csharp
// Het resulterende object van de voorwaardelijke opmaak ophalen
ConditionalFormattingResult cfr1 = a1.GetConditionalFormattingResult();
```
De `GetConditionalFormattingResult()` De methode is cruciaal in deze stap. Deze retourneert een object dat de resultaten bevat van de voorwaardelijke opmaak die op de cel is toegepast. Dit is waar we de kleurinformatie die Excel gebruikt, gaan benutten.
## Stap 5: Toegang tot het ColorScaleResult
Zodra we het resultaat van de voorwaardelijke opmaak hebben, kunnen we dieper graven en de kleurenschaal benaderen die Excel voor deze specifieke cel heeft gebruikt.
```csharp
// Haal het resulterende kleurobject van ColorScale op
Color c = cfr1.ColorScaleResult;
```
Voorwaardelijke opmaak in Excel is vaak afhankelijk van kleurenschalen. Met deze regel kunnen we de resulterende kleur extraheren die is toegepast op basis van de regels voor voorwaardelijke opmaak.
## Stap 6: De kleurgegevens weergeven
Ten slotte willen we de Excel-kleur toegepast zien. Laten we de kleurdetails afdrukken in een gemakkelijk te begrijpen formaat, inclusief de ARGB-waarde en de naam.
```csharp
// Lees de kleur
Console.WriteLine(c.ToArgb().ToString());
Console.WriteLine(c.Name);
```
De `ToArgb()` methode geeft ons de kleur in ARGB-formaat (Alfa, Rood, Groen, Blauw), terwijl de `Name` De eigenschap geeft de kleurnaam weer in een leesbaarder formaat. U kunt deze kleurdetails gebruiken om ze in andere toepassingen te vergelijken of uw Excel-bestanden programmatisch aan te passen.

## Conclusie
En voilà! Door deze stappen te volgen, hebt u zojuist geleerd hoe u de door MS Excel gekozen kleur programmatisch kunt berekenen met Aspose.Cells voor .NET. Deze aanpak kan ongelooflijk handig zijn voor het automatiseren van Excel-taken, vooral bij complexe voorwaardelijke opmaak. De volgende keer dat u een mysterieuze kleur in Excel tegenkomt, weet u precies hoe u de geheimen ervan kunt onthullen.
## Veelgestelde vragen
### Kan ik voorwaardelijke opmaak programmatisch toepassen met behulp van Aspose.Cells?
Ja, met Aspose.Cells kunt u voorwaardelijke opmaak in Excel-bestanden programmatisch toepassen, wijzigen en zelfs verwijderen.
### Ondersteunt Aspose.Cells alle versies van Excel?
Absoluut! Aspose.Cells ondersteunt Excel 97-2003 (XLS), Excel 2007-2019/365 (XLSX) en meer formaten, waaronder PDF, HTML en CSV.
### Is Aspose.Cells beschikbaar voor andere platforms dan .NET?
Ja, Aspose.Cells is beschikbaar voor verschillende platforms, waaronder Java, C++ en Android via Java.
### Hoe kan ik Aspose.Cells gratis uitproberen?
U kunt een gratis proefversie van Aspose.Cells voor .NET downloaden van [hier](https://releases.aspose.com/).
### Hoe werk ik met grote Excel-bestanden met Aspose.Cells?
Aspose.Cells is geoptimaliseerd voor prestaties, zelfs bij het verwerken van grote bestanden. U kunt streaming API's gebruiken om grote hoeveelheden data efficiënt te verwerken.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}