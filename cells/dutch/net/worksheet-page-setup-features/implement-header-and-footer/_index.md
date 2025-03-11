---
title: Koptekst en voettekst in werkblad implementeren
linktitle: Koptekst en voettekst in werkblad implementeren
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u kopteksten en voetteksten in Excel-werkbladen instelt met Aspose.Cells voor .NET met een stapsgewijze zelfstudie, praktische voorbeelden en nuttige tips.
weight: 22
url: /nl/net/worksheet-page-setup-features/implement-header-and-footer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Koptekst en voettekst in werkblad implementeren

## Invoering

Bij het werken met Excel-spreadsheets spelen kopteksten en voetteksten een belangrijke rol bij het leveren van belangrijke contextuele informatie, zoals bestandsnamen, datums of paginanummers, aan uw publiek. Of u nu rapporten automatiseert of dynamische bestanden genereert, Aspose.Cells voor .NET maakt het eenvoudig om kopteksten en voetteksten in werkbladen programmatisch aan te passen. Deze gids duikt in een uitgebreide, stapsgewijze aanpak om kopteksten en voetteksten toe te voegen met Aspose.Cells voor .NET, waardoor uw Excel-bestanden extra gepolijst en professioneel overkomen.

## Vereisten

Voordat u begint, moet u ervoor zorgen dat u het volgende geregeld hebt:

1.  Aspose.Cells voor .NET: Aspose.Cells voor .NET moet geïnstalleerd zijn.[Download het hier](https://releases.aspose.com/cells/net/).
2. IDE-installatie: Visual Studio (of uw favoriete IDE) met .NET Framework geïnstalleerd.
3.  Licentie: U kunt beginnen met de gratis proefversie, maar u kunt ook een volledige of tijdelijke licentie aanschaffen om het volledige potentieel van Aspose.Cells te benutten.[Vraag een tijdelijk rijbewijs aan](https://purchase.aspose.com/temporary-license/).

De documentatie voor Aspose.Cells is een handige bron voor referentie tijdens dit proces. U kunt het vinden[hier](https://reference.aspose.com/cells/net/).

## Pakketten importeren

Importeer de vereiste naamruimten in uw project:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Door dit pakket te importeren, krijgt u toegang tot de klassen en methoden die u nodig hebt om met kopteksten, voetteksten en andere Excel-functionaliteiten in Aspose.Cells te werken.

In deze handleiding leggen we elke stap uit, zodat u deze eenvoudig kunt volgen, zelfs als u nog niet bekend bent met Aspose.Cells of .NET.

## Stap 1: Stel uw werkmap en pagina-instelling in

Eerst het belangrijkste: maak een nieuwe werkmap en open de pagina-instellingen van het werkblad. Dit geeft u de tools die u nodig hebt om de kop- en voettekst van het werkblad te wijzigen.

```csharp
// Definieer het pad om uw document op te slaan
string dataDir = "Your Document Directory";

// Een werkmapobject instantiëren
Workbook excel = new Workbook();
```

 Hier hebben we een`Workbook` object, dat ons Excel-bestand vertegenwoordigt.`PageSetup` In het gedeelte van het werkblad kunnen we de opties voor de kop- en voettekst wijzigen.


## Stap 2: Toegang tot de eigenschappen van het werkblad en de pagina-instelling

 In Aspose.Cells heeft elk werkblad een`PageSetup`eigenschap die lay-outfuncties bestuurt, inclusief kop- en voetteksten. Laten we de`PageSetup` object voor ons werkblad.

```csharp
// Verkrijg de referentie naar de PageSetup van het eerste werkblad
PageSetup pageSetup = excel.Worksheets[0].PageSetup;
```

 Hiermee,`pageSetup` bevat nu alle instellingen die nodig zijn om kopteksten en voetteksten aan te passen.


## Stap 3: Stel het linkergedeelte van de koptekst in

Headers in Excel zijn verdeeld in drie secties: left, center en right. Laten we beginnen met het instellen van de linkersectie om de naam van het werkblad weer te geven.

```csharp
// Werkbladnaam instellen in het linkergedeelte van de koptekst
pageSetup.SetHeader(0, "&A");
```

 Gebruik makend van`&A` kunt u de naam van het werkblad dynamisch weergeven. Dit is vooral handig als u meerdere werkbladen in een werkmap hebt en wilt dat elke koptekst de bijbehorende werkbladtitel weergeeft.


## Stap 4: Voeg datum en tijd toe aan het midden van de koptekst

Vervolgens voegen we de huidige datum en tijd toe aan het middelste gedeelte van de header. Daarnaast gebruiken we een aangepast lettertype voor de styling.

```csharp
// Stel de datum en tijd in het middelste gedeelte van de header in met een vetgedrukt lettertype
pageSetup.SetHeader(1, "&\"Times New Roman,Bold\"&D-&T");
```

In deze code:
- `&D`voegt de huidige datum in.
- `&T` Voegt de huidige tijd in.
- `"Times New Roman,Bold"` past Times New Roman vetgedrukt toe op deze elementen.


## Stap 5: Bestandsnaam weergeven in het rechtergedeelte van de koptekst

Om de header af te maken, geven we aan de rechterkant de bestandsnaam weer, samen met een aanpassing van het lettertype.

```csharp
// Geef de bestandsnaam weer in het rechtergedeelte van de header met een aangepaste lettergrootte
pageSetup.SetHeader(2, "&\"Times New Roman,Bold\"&12&F");
```

- `&F` staat voor de bestandsnaam, zodat duidelijk is bij welk bestand de afgedrukte pagina's horen.
- `&12` wijzigt de lettergrootte naar 12 voor deze sectie.


## Stap 6: Voeg tekst met aangepast lettertype toe aan de linkervoettekstsectie

Door naar footers! We beginnen met het instellen van de linker footer sectie met aangepaste tekst en een opgegeven lettertype.

```csharp
// Voeg aangepaste tekst met lettertypestijl toe aan het linkergedeelte van de voettekst
pageSetup.SetFooter(0, "Hello World! &\"Courier New\"&14 123");
```

 De`&\"Courier New\"&14` instelling in de bovenstaande code past het lettertype "Courier New" met grootte 14 toe op de opgegeven tekst (`123`). De rest van de tekst blijft in het standaardvoettekstlettertype.


## Stap 7: Paginanummer invoegen in het midden van de voettekst

Door paginanummers in de voettekst op te nemen, kunnen lezers gemakkelijker overzicht houden op documenten met meerdere pagina's.

```csharp
// Paginanummer invoegen in het middelste gedeelte van de voettekst
pageSetup.SetFooter(1, "&P");
```

 Hier,`&P` voegt het huidige paginanummer toe aan het middengedeelte van de voettekst. Het is een klein detail, maar cruciaal voor professioneel ogende documenten.


## Stap 8: Toon het totale aantal pagina's in de rechtervoettekstsectie

Tot slot maken we de voettekst af door het totale aantal pagina's in de rechtersectie weer te geven.

```csharp
// Geef het totale aantal pagina's weer in het rechtergedeelte van de voettekst
pageSetup.SetFooter(2, "&N");
```

- `&N` Geeft het totale aantal pagina's weer, zodat lezers weten hoe lang het document is.


## Stap 9: Sla de werkmap op

Zodra u uw kop- en voetteksten hebt ingesteld, is het tijd om de werkmap op te slaan. Dit is de laatste stap om een Excel-bestand te genereren met volledig aangepaste kop- en voetteksten.

```csharp
// Werkboek opslaan
excel.Save(dataDir + "SetHeadersAndFooters_out.xls");
```

Met deze regel wordt het bestand opgeslagen in de door u aangewezen map, met de aangepaste kop- en voetteksten op de juiste plaats.


## Conclusie

Het toevoegen van kop- en voetteksten aan Excel-werkbladen is een waardevolle vaardigheid voor het maken van georganiseerde, professionele documenten. Met Aspose.Cells voor .NET hebt u volledige controle over de kop- en voetteksten van uw Excel-bestanden, van het weergeven van de naam van het werkblad tot het invoegen van aangepaste tekst, datum, tijd en zelfs dynamische paginanummers. Nu u elke stap in actie hebt gezien, kunt u uw Excel-automatisering naar een hoger niveau tillen.

## Veelgestelde vragen

### Kan ik verschillende lettertypen gebruiken voor verschillende secties van kop- en voetteksten?  
Ja, met Aspose.Cells voor .NET kunt u lettertypen opgeven voor elk gedeelte van de kop- en voettekst met behulp van specifieke lettertypetags.

### Hoe verwijder ik kop- en voetteksten?  
 U kunt kop- en voetteksten wissen door de kop- of voettekst in te stellen op een lege tekenreeks met`SetHeader` of`SetFooter`.

### Kan ik afbeeldingen in kop- of voetteksten invoegen met Aspose.Cells voor .NET?  
Momenteel ondersteunt Aspose.Cells voornamelijk tekst in kop- en voetteksten. Afbeeldingen vereisen mogelijk een tijdelijke oplossing, zoals het invoegen van afbeeldingen in het werkblad zelf.

### Ondersteunt Aspose.Cells dynamische gegevens in kop- en voetteksten?  
 Ja, u kunt verschillende dynamische codes gebruiken (zoals`&D` voor datum of`&P` (voor paginanummer) om dynamische inhoud toe te voegen.

### Hoe kan ik de hoogte van de kop- of voettekst aanpassen?  
 Aspose.Cells biedt opties binnen de`PageSetup` klasse om de marges van kop- en voetteksten aan te passen, zodat u controle hebt over de afstand.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
