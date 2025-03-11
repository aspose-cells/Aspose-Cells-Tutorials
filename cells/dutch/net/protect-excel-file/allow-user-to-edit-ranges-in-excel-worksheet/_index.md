---
title: Sta gebruikers toe om bereiken in Excel-werkblad te bewerken
linktitle: Sta gebruikers toe om bereiken in Excel-werkblad te bewerken
second_title: Aspose.Cells voor .NET API-referentie
description: Gebruikers toestaan om specifieke bereiken in een Excel-spreadsheet te bewerken met Aspose.Cells voor .NET. Stapsgewijze handleiding met broncode in C#.
weight: 10
url: /nl/net/protect-excel-file/allow-user-to-edit-ranges-in-excel-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sta gebruikers toe om bereiken in Excel-werkblad te bewerken

## Invoering

Als het gaat om het werken met Excel-werkbladen, is flexibiliteit vaak de sleutel, vooral wanneer meerdere gebruikers toegang nodig hebben om specifieke gebieden te bewerken zonder de gegevensintegriteit van het hele werkblad in gevaar te brengen. Dit is waar Aspose.Cells voor .NET schittert! In deze tutorial duiken we in hoe gebruikers bepaalde bereiken in een Excel-werkblad kunnen bewerken terwijl de rest van het document wordt beschermd. Aan het einde van dit artikel begrijpt u niet alleen de concepten, maar hebt u ook een tastbaar voorbeeld om mee te werken. 

## Vereisten

Voordat we in de details duiken, willen we ervoor zorgen dat u alles bij de hand hebt om te beginnen:

1. .NET-ontwikkelomgeving: U dient over een functionerende .NET-ontwikkelomgeving te beschikken (dit kan Visual Studio zijn of een andere IDE naar keuze).
2.  Aspose.Cells voor .NET-bibliotheek: Download en installeer de Aspose.Cells-bibliotheek. U kunt deze vinden[hier](https://releases.aspose.com/cells/net/).
3. Basiskennis van C#: Als u bekend bent met C#-programmering, kunt u gemakkelijk door de codevoorbeelden navigeren.
4. Begrijp de basisprincipes van Excel: Als u weet hoe Excel werkt, legt u een basis voor de functionaliteiten die we gaan bespreken.

Zodra deze vereisten zijn geregeld, bent u klaar om te gaan!

## Pakketten importeren

Voordat we beginnen met coderen, moeten we ervoor zorgen dat ons project de Aspose.Cells-naamruimte herkent. Hier leest u hoe u de benodigde pakketten importeert:

```csharp
using System.IO;
using Aspose.Cells;
```

Nu we hebben geïmporteerd wat we nodig hebben, gaan we stap voor stap door onze tutorial heen.

## Stap 1: De documentenmap instellen

Voor alle bestandsbewerkingen is het cruciaal om een gedefinieerde locatie te hebben waar onze documenten worden opgeslagen. Laten we onze werkdirectory instellen om de Excel-bestanden op te slaan.

```csharp
// Het pad naar de documentenmap.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Maak een map aan als deze nog niet bestaat.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

 Vervang eerst`"YOUR DOCUMENT DIRECTORY"` met het pad waar u uw bestanden wilt opslaan. Deze code controleert of de directory bestaat; als dat niet zo is, maakt hij er een aan.

## Stap 2: Een nieuwe werkmap instantiëren

Nu onze werkmap klaar is, is het tijd om onze Excel-werkmap te maken. 

```csharp
// Een nieuwe werkmap instantiëren
Workbook book = new Workbook();
```

 Hier maken we een nieuw exemplaar van de`Workbook` klasse geleverd door Aspose.Cells, waarmee we het Excel-bestand kunnen bewerken.

## Stap 3: Toegang tot het standaardwerkblad

Elke nieuw aangemaakte werkmap bevat minstens één werkblad. Laten we dat eens bekijken.

```csharp
// Ontvang het eerste (standaard) werkblad
Worksheet sheet = book.Worksheets[0];
```

In dit codefragment openen we het eerste werkblad van onze werkmap, dat we in de volgende stappen gaan bewerken.

## Stap 4: Toestaan dat bewerkingsbereiken worden bewerkt

 Om specifieke bereiken van het werkblad voor bewerking in te schakelen, moeten we toegang krijgen tot de`AllowEditRanges` eigendom.

```csharp
// De optie Bewerken toestaan ophalen
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```

Met deze verzameling kunnen we bepalen welke bereiken in ons werkblad bewerkbaar zijn.

## Stap 5: Definieer het beschermde bereik

Vervolgens definiëren we welk deel van het werkblad we willen beveiligen, terwijl we bewerkingen binnen een bepaald bereik willen toestaan.

```csharp
// Definieer ProtectedRange
ProtectedRange proteced_range;

// Maak het bereik
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
proteced_range = allowRanges[idx];

// Geef het wachtwoord op
proteced_range.Password = "123";
```

In deze stap voegen we een nieuw bewerkbaar bereik toe met de naam 'r2' waarmee bewerkingen in de cellen van rij 1 kolom 1 tot rij 3 kolom 3 mogelijk zijn. Daarnaast stellen we een wachtwoord in om dit bereik te beschermen, zodat alleen geautoriseerde gebruikers het kunnen wijzigen.

## Stap 6: Bescherm het werkblad

Nu we het bewerkbare bereik hebben ingesteld, moeten we het werkblad beveiligen.

```csharp
// Bescherm het blad
sheet.Protect(ProtectionType.All);
```

Deze code beschermt het gehele werkblad tegen ongewenste wijzigingen, met uitzondering van het bereik dat we zojuist hebben opgegeven.

## Stap 7: Sla het Excel-bestand op

Laten we de werkmap opslaan, zodat we onze wijzigingen in een Excel-bestand kunnen bekijken.

```csharp
// Sla het Excel-bestand op
book.Save(dataDir + "protectedrange.out.xls");
```

Zorg ervoor dat u de bestandsnaam indien nodig aanpast. Dit zal een Excel-bestand in uw opgegeven directory aanmaken met de instellingen die we hebben geconfigureerd.

## Conclusie

Daar heb je het! Je hebt met succes een Excel-werkblad gemaakt dat bewerkingen beperkt tot een bepaald bereik, terwijl de rest van het werkblad wordt beschermd. Met Aspose.Cells voor .NET wordt het beheren van dit soort taken veel eenvoudiger en efficiënter. Of je nu een complexe applicatie ontwikkelt of gewoon gegevens veilig wilt beheren, deze mogelijkheden kunnen je workflow aanzienlijk verbeteren.

## Veelgestelde vragen

### Wat is Aspose.Cells?
Aspose.Cells is een krachtige .NET-bibliotheek voor het verwerken van Excel-bestanden en biedt functionaliteiten zoals het programmatisch maken, bewerken en converteren van spreadsheets.

### Kan ik meerdere bewerkbare bereiken toepassen?
 Absoluut! Je kunt de`Add` methode op de`allowRanges` verzameling meerdere keren om meerdere bewerkbare bereiken op te geven.

### Wat gebeurt er als ik mijn wachtwoord vergeet?
Als u het wachtwoord voor een bewerkbaar bereik vergeet, moet u helaas de beveiliging verwijderen of het bestand op een vooraf gedefinieerde manier openen. Hiervoor zijn mogelijk inloggegevens nodig.

### Bestaat er een gratis versie van Aspose.Cells?
Ja, Aspose biedt een gratis proefperiode aan waarmee u de functies kunt uitproberen voordat u tot aankoop overgaat.

### Waar kan ik meer informatie vinden over Aspose.Cells?
 U kunt de[documentatie](https://reference.aspose.com/cells/net/)voor gedetailleerde handleidingen en referenties.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
