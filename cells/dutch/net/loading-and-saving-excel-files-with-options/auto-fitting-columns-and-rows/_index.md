---
"description": "Leer hoe u kolommen en rijen automatisch kunt aanpassen terwijl u HTML in Excel laadt met Aspose.Cells voor .NET. Inclusief stapsgewijze handleiding."
"linktitle": "Kolommen en rijen automatisch aanpassen tijdens het laden van HTML in een werkmap"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Kolommen en rijen automatisch aanpassen tijdens het laden van HTML in een werkmap"
"url": "/nl/net/loading-and-saving-excel-files-with-options/auto-fitting-columns-and-rows/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Kolommen en rijen automatisch aanpassen tijdens het laden van HTML in een werkmap

## Invoering
Heb je je ooit afgevraagd hoe je de kolom- en rijgroottes automatisch kunt aanpassen tijdens het laden van HTML-inhoud in een Excel-werkmap met Aspose.Cells voor .NET? Dan ben je hier aan het juiste adres! In deze tutorial gaan we dieper in op hoe je een HTML-tabel in een werkmap kunt laden en ervoor kunt zorgen dat de kolommen en rijen automatisch worden aangepast aan de inhoud. Als je werkt met dynamische gegevens die regelmatig veranderen, is deze handleiding dé manier om goed opgemaakte Excel-sheets te maken van HTML.
### Vereisten
Voordat je aan de slag gaat met de code, moet je een paar dingen op je systeem hebben ingesteld. Maak je geen zorgen, het is simpel en duidelijk!
1. Visual Studio geïnstalleerd: U hebt Visual Studio of een andere .NET-ontwikkelomgeving nodig.
2. Aspose.Cells voor .NET: U kunt [download de nieuwste versie](https://releases.aspose.com/cells/net/) of gebruik de NuGet-pakketbeheerder om het te installeren.
3. .NET Framework: Zorg ervoor dat u .NET Framework 4.0 of hoger hebt geïnstalleerd.
4. Basiskennis van C#: Als u enige kennis van C# hebt, verloopt deze tutorial soepeler.
5. HTML-tabelgegevens: bereid wat HTML-inhoud voor (zelfs een eenvoudige tabel) die u in Excel wilt laden.
## Pakketten importeren
Laten we beginnen met het importeren van de benodigde naamruimten om aan de slag te gaan. Hier is een eenvoudige lijst met wat je moet importeren:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Met deze pakketten kunt u de werkmap verwerken, HTML-gegevens bewerken en deze naadloos in Excel laden.
Laten we dit proces opsplitsen in hanteerbare stukken, zodat je het gemakkelijk kunt volgen. Aan het einde heb je een werkend voorbeeld van hoe je kolommen en rijen automatisch kunt aanpassen tijdens het laden van HTML in een werkmap met Aspose.Cells voor .NET.
## Stap 1: De documentenmap instellen
Om bestanden eenvoudig op te slaan en terug te vinden, specificeren we het pad waar uw documenten worden opgeslagen. U kunt het directorypad vervangen door uw eigen maplocatie.
```csharp
string dataDir = "Your Document Directory";
```
Deze regel stelt de map in waar uw Excel-bestanden worden opgeslagen. Het is belangrijk om uw bestanden goed te ordenen wanneer u aan meerdere projecten werkt. Stel u dit voor als de archiefkast van uw project!
## Stap 2: HTML-gegevens als een tekenreeks maken
Vervolgens definiëren we wat basis-HTML-inhoud. Voor dit voorbeeld gebruiken we een eenvoudige HTML-tabel. U kunt deze aanpassen aan de behoeften van uw project.
```csharp
string sampleHtml = "<html><body><table><tr><td>This is sample text.</td><td>Some text.</td></tr><tr><td>This is another sample text.</td><td>Some text.</td></tr></table></body></html>";
```
We definiëren hier een heel eenvoudige HTML-string. Deze bevat een tabel met een paar rijen en kolommen. Je kunt naar wens meer rijen of kolommen toevoegen. Zie het als het bereiden van de ingrediënten voordat je een maaltijd kookt!
## Stap 3: HTML-string laden in MemoryStream
Nu we onze HTML-inhoud gereed hebben, is de volgende stap om deze in het geheugen te laden met behulp van `MemoryStream`Hierdoor kunnen we de HTML-inhoud in het geheugen bewerken zonder deze eerst op schijf op te slaan.
```csharp
MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(sampleHtml));
```
Door de HTML-string om te zetten in een byte-array en deze in een `MemoryStream`We kunnen met de HTML-gegevens in het geheugen werken. Stel je deze stap voor als het bereiden van het gerecht in een pan voordat het in de oven wordt gezet!
## Stap 4: Laad de MemoryStream in een werkmap (zonder automatische aanpassing)
Zodra we de HTML-inhoud in het geheugen hebben, laden we deze in een Aspose `Workbook`Op dit moment passen we de kolommen en rijen nog niet automatisch aan. Dit is ons 'voor'-scenario, om later te vergelijken met de automatisch aangepaste versie.
```csharp
Workbook wb = new Workbook(ms);
wb.Save(dataDir + "outputWithout_AutoFitColsAndRows.xlsx");
```
De werkmap is geladen met de HTML-inhoud, maar de kolommen en rijen zijn nog niet automatisch aan de tekst aangepast. Stel je dit voor als het bakken van een cake, maar vergeten de temperatuur te controleren: het werkt, maar het is misschien niet perfect!
## Stap 5: Geef HTML-laadopties op met Auto-Fit ingeschakeld
En nu komt de magie! We creëren een instantie van `HtmlLoadOptions` en schakel de `AutoFitColsAndRows` eigenschap. Dit zorgt ervoor dat wanneer de HTML-inhoud wordt geladen, de kolommen en rijen worden aangepast aan de inhoud erin.
```csharp
HtmlLoadOptions opts = new HtmlLoadOptions();
opts.AutoFitColsAndRows = true;
```
Door deze optie in te stellen, geven we Aspose.Cells de opdracht om de grootte van de rijen en kolommen automatisch aan te passen. Stel je dit voor als het instellen van de oven op de perfecte temperatuur, zodat de cake perfect rijst!
## Stap 6: HTML in werkmap laden met automatische aanpassing ingeschakeld
Nu laden we de HTML-inhoud opnieuw, maar deze keer met de `AutoFitColsAndRows` Optie ingeschakeld. Hiermee worden de kolombreedtes en rijhoogtes aangepast op basis van de inhoud erin.
```csharp
wb = new Workbook(ms, opts);
wb.Save(dataDir + "outputWith_AutoFitColsAndRows.xlsx");
```
Deze stap laadt de HTML-inhoud in een nieuwe werkmap en slaat deze op als een Excel-bestand, maar nu worden de kolommen en rijen automatisch aangepast! Zie dit als een perfect gebakken taart, waarbij alles precies de juiste grootte heeft.
## Conclusie
Door deze eenvoudige stappen te volgen, hebt u geleerd hoe u HTML-inhoud in een werkmap laadt met Aspose.Cells voor .NET en de kolommen en rijen automatisch invult. Zo ziet uw Excel-sheet er altijd netjes uit, ongeacht hoe dynamisch de inhoud is. Het is een eenvoudige maar krachtige functie die u veel tijd bespaart bij het opmaken en organiseren van uw Excel-gegevens.
Nu u over deze kennis beschikt, kunt u experimenteren met complexere HTML-inhoud, opmaak toevoegen en zelfs hele Excel-werkmappen van webpagina's maken!
## Veelgestelde vragen
### Kan ik deze methode gebruiken om grote HTML-tabellen te laden?
Ja, Aspose.Cells kan grote HTML-tabellen efficiënt verwerken, maar voor optimale prestaties is het raadzaam om eerst te testen met uw datagroottes.
### Kan ik handmatig specifieke kolombreedtes en rijhoogtes toepassen na automatisch aanpassen?
Absoluut! Je kunt nog steeds individuele kolommen en rijen aanpassen, zelfs nadat je de functie voor automatisch aanpassen hebt gebruikt.
### Hoe kan ik de tabel stylen nadat ik HTML heb geladen?
Nadat u de HTML hebt geladen, kunt u stijlen toepassen met behulp van de uitgebreide stylingopties van Aspose.Cells.
### Is Aspose.Cells voor .NET compatibel met oudere versies van .NET Framework?
Ja, Aspose.Cells voor .NET ondersteunt .NET Framework 4.0 en hoger.
### Kan ik met Aspose.Cells ook andere soorten inhoud dan HTML in Excel laden?
Ja, Aspose.Cells ondersteunt het laden van verschillende formaten zoals CSV, JSON en XML in Excel.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}