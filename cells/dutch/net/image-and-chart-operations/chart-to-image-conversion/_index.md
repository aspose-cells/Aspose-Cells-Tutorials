---
title: Grafiek naar afbeeldingconversie in .NET
linktitle: Grafiek naar afbeeldingconversie in .NET
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u grafieken naar afbeeldingen in .NET converteert met Aspose.Cells met deze stapsgewijze handleiding. Converteer Excel-grafieken eenvoudig naar afbeeldingen van hoge kwaliteit.
weight: 10
url: /nl/net/image-and-chart-operations/chart-to-image-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Grafiek naar afbeeldingconversie in .NET

## Invoering
Het converteren van een grafiek van Excel naar een afbeelding kan een cruciale vereiste zijn bij het bouwen van rapportagesystemen of het delen van visuele datarepresentaties. Gelukkig is dit proces met Aspose.Cells voor .NET een fluitje van een cent! Of u nu rapporten genereert of gewoon Excel-grafieken converteert naar afbeeldingen voor een betere weergave, deze gids leidt u stap voor stap door het proces.
## Vereisten
Voordat we beginnen, controleren we of je alles bij de hand hebt om deze tutorial te kunnen volgen.
### Aspose.Cells voor .NET-bibliotheek
Eerst moet u de Aspose.Cells for .NET-bibliotheek in uw project downloaden en ernaar verwijzen. U kunt de nieuwste versie hier downloaden:
- [Download Aspose.Cells voor .NET](https://releases.aspose.com/cells/net/)
### .NET-omgeving
Zorg ervoor dat u het .NET Framework op uw systeem hebt geïnstalleerd. U kunt Visual Studio of een andere .NET-ontwikkelomgeving gebruiken om dit voorbeeld uit te voeren.
### Licentie-instelling (optioneel)
 Hoewel u Aspose.Cells met een gratis proefversie kunt gebruiken, kunt u voor volledige functionaliteit zonder beperkingen overwegen om een aanvraag in te dienen voor een[tijdelijke licentie](https://purchase.aspose.com/temporary-license/) of koop er een bij[hier](https://purchase.aspose.com/buy).

## Pakketten importeren
Om te beginnen importeren we de benodigde namespaces om met de Aspose.Cells-bibliotheek te werken. Hiermee kunnen we Excel-bestanden manipuleren en afbeeldingen genereren.
```csharp
using System.IO;
using System.Drawing;
using Aspose.Cells;
```
Zorg ervoor dat u deze pakketten gereed hebt voordat u met het coderen begint.

Laten we het proces voor het omzetten van een grafiek naar een afbeelding nu opsplitsen in eenvoudige stappen.
## Stap 1: Stel uw projectdirectory in
Je hebt een plek nodig om je gegenereerde afbeeldingen op te slaan, toch? Laten we eerst een directory maken waar de output-afbeeldingen worden opgeslagen.

We beginnen met het definiëren van het pad voor onze documentdirectory en zorgen ervoor dat de map bestaat. Als dat niet zo is, maken we er een.
```csharp
// Definieer de map waarin de afbeeldingen moeten worden opgeslagen
string dataDir = "Your Document Directory";
//Controleer of de directory bestaat
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Met deze stap bent u klaar om uw grafiekafbeeldingen te genereren en op te slaan in deze map.
## Stap 2: Maak een nieuwe werkmap
Hier instantiëren we een Workbook-object. Dit zal ons Excel-bestand vertegenwoordigen waarin de grafiek zal worden ingesloten.

Een werkmap is als een Excel-bestand dat werkbladen bevat. Door een nieuwe werkmap te maken, beginnen we helemaal opnieuw met een leeg Excel-bestand.
```csharp
// Een nieuw werkmapobject maken
Workbook workbook = new Workbook();
```
## Stap 3: Een nieuw werkblad toevoegen
Elk Excel-bestand heeft werkbladen (of tabbladen). Laten we er een aan onze werkmap toevoegen.

Het toevoegen van een nieuw werkblad is essentieel, omdat we onze gegevens en grafieken in dit werkblad zullen invoegen. Zodra het werkblad is toegevoegd, halen we de referentie ervan op.
```csharp
// Een nieuw werkblad toevoegen aan de werkmap
int sheetIndex = workbook.Worksheets.Add();
// Haal het nieuw toegevoegde werkblad op
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
## Stap 4: Vul het werkblad met gegevens
Om een zinvolle grafiek te maken, hebben we wat data nodig, toch? Laten we een paar cellen vullen met voorbeeldwaarden.

We voegen data toe aan specifieke cellen op het werkblad. Deze data wordt later gebruikt om onze grafiek te genereren.
```csharp
// Voorbeeldgegevens aan cellen toevoegen
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```
## Stap 5: Voeg een grafiek toe aan het werkblad
Laten we nu een kolomdiagram maken waarin de zojuist toegevoegde gegevens worden gevisualiseerd.

We specificeren het type grafiek (kolomdiagram) en definiëren de grootte en positie ervan in het werkblad.
```csharp
// Voeg een kolomdiagram toe aan het werkblad
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 15, 5);
```
## Stap 6: Definieer de grafiekgegevensbron
En hier gebeurt de magie: het koppelen van de grafiek aan de gegevens in het werkblad!

We koppelen de grafiek aan de data in kolommen A1 tot en met B3. Dit vertelt de grafiek waar de data vandaan moet komen.
```csharp
// Koppel de grafiek aan de gegevens in het bereik A1 tot en met B3
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("A1:B3", true);
```
## Stap 7: Converteer de grafiek naar een afbeelding
Het moment van de waarheid: we gaan deze grafiek omzetten in een afbeeldingsbestand!

 Hier gebruiken we de`ToImage` methode om de grafiek om te zetten in een afbeeldingsformaat naar keuze. In dit geval zetten we het om naar een EMF (Enhanced Metafile) formaat.
```csharp
// Converteer de grafiek naar een afbeelding en sla deze op in de map
chart.ToImage(dataDir + "Chart.emf", ImageFormat.Emf);
```
En dat is het! Uw grafiek is nu opgeslagen als afbeelding. Tijd om uzelf een schouderklopje te geven.
## Stap 8: Succesbericht weergeven
Ter afsluiting geven we een bericht weer waarin de generatie van de afbeelding wordt bevestigd.
```csharp
// Geef een bericht weer om aan te geven dat het is gelukt
System.Console.WriteLine("Image generated successfully.");
```
## Conclusie
Boem! Zo eenvoudig is het om een grafiek van Excel naar een afbeelding te converteren met Aspose.Cells voor .NET. Dit proces vereenvoudigt niet alleen de presentatie van gegevens, maar verbetert ook de flexibiliteit van rapporten of dashboards waarbij afbeeldingen de voorkeur krijgen boven ingebedde grafieken.
Door de stappen in deze handleiding te volgen, kunt u nu elk Excel-diagram omzetten in een afbeelding. Zo kunt u visuele gegevens naadloos integreren in verschillende toepassingen.
## Veelgestelde vragen
### Kan ik verschillende soorten grafieken met deze methode converteren?
Ja, u kunt elk grafiektype converteren dat door Aspose.Cells wordt ondersteund, inclusief cirkeldiagrammen, staafdiagrammen, lijndiagrammen en meer!
### Is het mogelijk om het afbeeldingsformaat te wijzigen?
 Absoluut! Hoewel we in dit voorbeeld EMF hebben gebruikt, kunt u het afbeeldingsformaat wijzigen naar PNG, JPEG, BMP en andere door eenvoudigweg de`ImageFormat` parameter.
### Ondersteunt Aspose.Cells afbeeldingen met een hoge resolutie?
Ja, met Aspose.Cells kunt u de resolutie en kwaliteitsinstellingen van afbeeldingen bepalen bij het exporteren van grafieken naar afbeeldingen.
### Kan ik meerdere grafieken in één keer naar afbeeldingen converteren?
Ja, u kunt door meerdere grafieken in een werkmap bladeren en ze met slechts een paar regels code omzetten in afbeeldingen.
### Zit er een limiet aan het aantal grafieken dat ik kan converteren?
Aspose.Cells kent geen inherente limiet, maar de verwerking van grote hoeveelheden gegevens kan afhankelijk zijn van het geheugen en de prestatiemogelijkheden van uw systeem.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
