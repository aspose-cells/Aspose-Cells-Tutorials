---
"description": "Leer hoe u kopteksten en voetteksten in Excel-werkbladen instelt met Aspose.Cells voor .NET met een stapsgewijze zelfstudie, praktische voorbeelden en nuttige tips."
"linktitle": "Koptekst en voettekst in werkblad implementeren"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Koptekst en voettekst in werkblad implementeren"
"url": "/nl/net/worksheet-page-setup-features/implement-header-and-footer/"
"weight": 22
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Koptekst en voettekst in werkblad implementeren

## Invoering

Bij het werken met Excel-spreadsheets spelen kop- en voetteksten een belangrijke rol bij het overbrengen van belangrijke contextuele informatie, zoals bestandsnamen, datums of paginanummers, aan uw doelgroep. Of u nu rapporten automatiseert of dynamische bestanden genereert, Aspose.Cells voor .NET maakt het eenvoudig om kop- en voetteksten in werkbladen programmatisch aan te passen. Deze handleiding behandelt een uitgebreide, stapsgewijze aanpak voor het toevoegen van kop- en voetteksten met Aspose.Cells voor .NET, waardoor uw Excel-bestanden extra verfijnd en professioneel ogen.

## Vereisten

Zorg ervoor dat u het volgende geregeld hebt voordat u begint:

1. Aspose.Cells voor .NET: Aspose.Cells voor .NET moet geïnstalleerd zijn. [Download het hier](https://releases.aspose.com/cells/net/).
2. IDE-installatie: Visual Studio (of uw favoriete IDE) met .NET Framework geïnstalleerd.
3. Licentie: U kunt met de gratis proefversie aan de slag, maar u kunt het volledige potentieel van Aspose.Cells benutten door een volledige of tijdelijke licentie aan te schaffen. [Vraag een tijdelijk rijbewijs aan](https://purchase.aspose.com/temporary-license/).

De documentatie voor Aspose.Cells is een handige naslagbron gedurende dit proces. U kunt deze vinden [hier](https://reference.aspose.com/cells/net/).

## Pakketten importeren

Importeer de vereiste naamruimten in uw project:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Als u dit pakket importeert, krijgt u toegang tot de klassen en methoden die u nodig hebt om met kopteksten, voetteksten en andere Excel-functionaliteiten in Aspose.Cells te werken.

In deze handleiding leggen we elke stap uit, zodat u deze eenvoudig kunt volgen, zelfs als u nog geen ervaring hebt met Aspose.Cells of .NET.

## Stap 1: Uw werkmap en pagina-instelling instellen

Allereerst: maak een nieuwe werkmap aan en open de pagina-instelling van het werkblad. Dit geeft je de tools die je nodig hebt om de kop- en voettekst van het werkblad aan te passen.

```csharp
// Definieer het pad om uw document op te slaan
string dataDir = "Your Document Directory";

// Een werkmapobject instantiëren
Workbook excel = new Workbook();
```

Hier hebben we een `Workbook` object, dat ons Excel-bestand vertegenwoordigt. De `PageSetup` In het gedeelte 'Koptekst' van het werkblad kunnen we de opties voor de kop- en voettekst wijzigen.


## Stap 2: Toegang tot de eigenschappen van het werkblad en de pagina-instelling

In Aspose.Cells heeft elk werkblad een `PageSetup` eigenschap die lay-outfuncties regelt, inclusief kop- en voetteksten. Laten we de `PageSetup` object voor ons werkblad.

```csharp
// Verkrijg de referentie naar de PageSetup van het eerste werkblad
PageSetup pageSetup = excel.Worksheets[0].PageSetup;
```

Hiermee, `pageSetup` bevat nu alle instellingen die nodig zijn om kopteksten en voetteksten aan te passen.


## Stap 3: Stel het linkergedeelte van de koptekst in

Kopteksten in Excel zijn verdeeld in drie secties: links, midden en rechts. Laten we beginnen met het instellen van de linkersectie om de naam van het werkblad weer te geven.

```csharp
// Geef de werkbladnaam op in het linkergedeelte van de koptekst
pageSetup.SetHeader(0, "&A");
```

Gebruiken `&A` Hiermee kunt u de naam van het werkblad dynamisch weergeven. Dit is vooral handig als u meerdere werkbladen in een werkmap hebt en wilt dat elke koptekst de bijbehorende werkbladtitel weergeeft.


## Stap 4: Datum en tijd toevoegen aan het midden van de koptekst

Laten we vervolgens de huidige datum en tijd toevoegen aan het middelste gedeelte van de header. Daarnaast gebruiken we een aangepast lettertype voor de styling.

```csharp
// Stel de datum en tijd in het middengedeelte van de koptekst in met een vetgedrukt lettertype
pageSetup.SetHeader(1, "&\"Times New Roman,Bold\"&D-&T");
```

In deze code:
- `&D` voegt de huidige datum in.
- `&T` Voegt de huidige tijd in.
- `"Times New Roman,Bold"` past Times New Roman vetgedrukt toe op deze elementen.


## Stap 5: Bestandsnaam weergeven in het rechtergedeelte van de koptekst

Om de header af te ronden, geven we aan de rechterkant de bestandsnaam weer, samen met een aangepast lettertype.

```csharp
// Geef de bestandsnaam weer in het rechtergedeelte van de header met een aangepaste lettergrootte
pageSetup.SetHeader(2, "&\"Times New Roman,Bold\"&12&F");
```

- `&F` staat voor de bestandsnaam, zodat duidelijk is bij welk bestand de afgedrukte pagina's horen.
- `&12` verandert de lettergrootte naar 12 voor deze sectie.


## Stap 6: Voeg tekst met een aangepast lettertype toe aan de linkervoettekstsectie

Laten we verder gaan met de voetteksten! We beginnen met het instellen van de linkervoettekst met aangepaste tekst en een specifiek lettertype.

```csharp
// Voeg aangepaste tekst met lettertypestijl toe aan het linkergedeelte van de voettekst
pageSetup.SetFooter(0, "Hello World! &\"Courier New\"&14 123");
```

De `&\"Courier New\"&14` instelling in de bovenstaande code past het lettertype "Courier New" met grootte 14 toe op de opgegeven tekst (`123`). De rest van de tekst blijft in het standaardvoettekstlettertype.


## Stap 7: Paginanummer invoegen in het midden van de voettekst

Het opnemen van paginanummers in de voettekst is een goede manier om lezers te helpen overzicht te houden in documenten met meerdere pagina's.

```csharp
// Paginanummer invoegen in het middelste gedeelte van de voettekst
pageSetup.SetFooter(1, "&P");
```

Hier, `&P` Voegt het huidige paginanummer toe aan het middengedeelte van de voettekst. Het is een klein detail, maar cruciaal voor professioneel ogende documenten.


## Stap 8: Toon het totale aantal pagina's in de rechtervoettekstsectie

Tot slot maken we de voettekst af door het totale aantal pagina's in de rechtersectie weer te geven.

```csharp
// Geef het totale aantal pagina's weer in het rechtergedeelte van de voettekst
pageSetup.SetFooter(2, "&N");
```

- `&N` Geeft het totale aantal pagina's weer, zodat lezers weten hoe lang het document is.


## Stap 9: Sla de werkmap op

Nadat je de kop- en voetteksten hebt ingesteld, is het tijd om de werkmap op te slaan. Dit is de laatste stap om een Excel-bestand te genereren met volledig aangepaste kop- en voetteksten.

```csharp
// Werkboek opslaan
excel.Save(dataDir + "SetHeadersAndFooters_out.xls");
```

Met deze regel wordt het bestand opgeslagen in de door u aangewezen map, met de aangepaste kop- en voetteksten op de juiste plaats.


## Conclusie

Het toevoegen van kop- en voetteksten aan Excel-werkbladen is een waardevolle vaardigheid voor het creëren van overzichtelijke, professionele documenten. Met Aspose.Cells voor .NET hebt u volledige controle over de kop- en voetteksten van uw Excel-bestanden, van het weergeven van de werkbladnaam tot het invoegen van aangepaste tekst, datum, tijd en zelfs dynamische paginanummers. Nu u elke stap in actie hebt gezien, kunt u uw Excel-automatisering naar een hoger niveau tillen.

## Veelgestelde vragen

### Kan ik verschillende lettertypen gebruiken voor verschillende secties van kop- en voetteksten?  
Ja, met Aspose.Cells voor .NET kunt u lettertypen voor elke sectie van de kop- en voettekst opgeven met behulp van specifieke lettertypetags.

### Hoe verwijder ik kop- en voetteksten?  
kunt kop- en voetteksten wissen door de kop- of voettekst in te stellen op een lege tekenreeks met `SetHeader` of `SetFooter`.

### Kan ik afbeeldingen in kop- of voetteksten invoegen met Aspose.Cells voor .NET?  
Momenteel ondersteunt Aspose.Cells voornamelijk tekst in kop- en voetteksten. Voor afbeeldingen is mogelijk een tijdelijke oplossing nodig, zoals het invoegen van afbeeldingen in het werkblad zelf.

### Ondersteunt Aspose.Cells dynamische gegevens in kop- en voetteksten?  
Ja, u kunt verschillende dynamische codes gebruiken (zoals `&D` voor datum of `&P` (voor paginanummer) om dynamische inhoud toe te voegen.

### Hoe kan ik de hoogte van de kop- of voettekst aanpassen?  
Aspose.Cells biedt opties binnen de `PageSetup` klasse om de marges van kop- en voetteksten aan te passen, zodat u controle hebt over de afstand.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}