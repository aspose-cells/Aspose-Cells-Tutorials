---
"description": "Stel gebruikers in staat specifieke bereiken in een Excel-spreadsheet te bewerken met Aspose.Cells voor .NET. Stapsgewijze handleiding met broncode in C#."
"linktitle": "Sta gebruikers toe om bereiken in Excel-werkbladen te bewerken"
"second_title": "Aspose.Cells voor .NET API-referentie"
"title": "Sta gebruikers toe om bereiken in Excel-werkbladen te bewerken"
"url": "/nl/net/protect-excel-file/allow-user-to-edit-ranges-in-excel-worksheet/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Sta gebruikers toe om bereiken in Excel-werkbladen te bewerken

## Invoering

Bij het werken met Excel-werkbladen is flexibiliteit vaak essentieel, vooral wanneer meerdere gebruikers toegang nodig hebben om specifieke gebieden te bewerken zonder de gegevensintegriteit van het hele werkblad in gevaar te brengen. Dit is waar Aspose.Cells voor .NET in uitblinkt! In deze tutorial gaan we dieper in op hoe je gebruikers in staat stelt om bepaalde bereiken in een Excel-werkblad te bewerken en tegelijkertijd de rest van het document te beschermen. Aan het einde van dit artikel begrijp je niet alleen de concepten, maar heb je ook een concreet voorbeeld om mee te werken. 

## Vereisten

Voordat we in de details duiken, willen we ervoor zorgen dat je alles hebt wat je nodig hebt om te beginnen:

1. .NET-ontwikkelomgeving: U dient over een functionerende .NET-ontwikkelomgeving te beschikken (dit kan Visual Studio zijn of een andere IDE naar keuze).
2. Aspose.Cells voor .NET-bibliotheek: download en installeer de Aspose.Cells-bibliotheek. U kunt deze vinden [hier](https://releases.aspose.com/cells/net/).
3. Basiskennis van C#: Kennis van C#-programmering helpt u om eenvoudig door de codevoorbeelden te navigeren.
4. Begrijp de basisbeginselen van Excel: Kennis van de werking van Excel vormt de basis voor de functionaliteiten die we gaan bespreken.

Zodra u aan deze vereisten hebt voldaan, kunt u aan de slag!

## Pakketten importeren

Voordat we beginnen met coderen, moeten we ervoor zorgen dat ons project de Aspose.Cells-naamruimte herkent. Zo importeert u de benodigde pakketten:

```csharp
using System.IO;
using Aspose.Cells;
```

Nu we hebben geïmporteerd wat we nodig hebben, gaan we stap voor stap door onze tutorial heen.

## Stap 1: De documentenmap instellen

Voor alle bestandsbewerkingen is het cruciaal om een vaste locatie te hebben waar onze documenten worden opgeslagen. Laten we onze werkmap instellen voor het opslaan van de Excel-bestanden.

```csharp
// Het pad naar de documentenmap.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Maak een map aan als deze nog niet bestaat.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

Vervang eerst `"YOUR DOCUMENT DIRECTORY"` met het pad waar u uw bestanden wilt opslaan. Deze code controleert of de map bestaat; als dat niet zo is, wordt er een aangemaakt.

## Stap 2: Een nieuwe werkmap instantiëren

Nu onze werkmap klaar is, is het tijd om onze Excel-werkmap te maken. 

```csharp
// Een nieuwe werkmap instantiëren
Workbook book = new Workbook();
```

Hier maken we een nieuw exemplaar van de `Workbook` klasse die wordt geleverd door Aspose.Cells, waarmee we het Excel-bestand kunnen bewerken.

## Stap 3: Toegang tot het standaardwerkblad

Elke nieuwe werkmap bevat minstens één werkblad. Laten we dat eens bekijken.

```csharp
// Ontvang het eerste (standaard) werkblad
Worksheet sheet = book.Worksheets[0];
```

In dit codefragment openen we het eerste werkblad van onze werkmap, dat we in de volgende stappen gaan bewerken.

## Stap 4: Bereiken voor toegestane bewerkingen ophalen

Om specifieke bereiken van het werkblad voor bewerking in te schakelen, moeten we toegang hebben tot de `AllowEditRanges` eigendom.

```csharp
// De optie 'Bewerkingsbereiken toestaan' verkrijgen
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```

Met deze verzameling kunnen we bepalen welke bereiken we in ons werkblad kunnen bewerken.

## Stap 5: Definieer het beschermde bereik

Vervolgens definiëren we welk deel van het werkblad we willen beveiligen, maar toch bewerkingen binnen een bepaald bereik willen toestaan.

```csharp
// Definieer ProtectedRange
ProtectedRange proteced_range;

// Creëer het bereik
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
proteced_range = allowRanges[idx];

// Geef het wachtwoord op
proteced_range.Password = "123";
```

In deze stap voegen we een nieuw bewerkbaar bereik toe met de naam 'r2'. Hiermee kunnen de cellen van rij 1 kolom 1 tot en met rij 3 kolom 3 worden bewerkt. Daarnaast stellen we een wachtwoord in om dit bereik te beschermen, zodat alleen geautoriseerde gebruikers het kunnen wijzigen.

## Stap 6: Bescherm het werkblad

Nu we het bewerkbare bereik hebben ingesteld, moeten we het werkblad beveiligen.

```csharp
// Bescherm het blad
sheet.Protect(ProtectionType.All);
```

Deze code beschermt het gehele werkblad tegen ongewenste wijzigingen, behalve het bereik dat we zojuist hebben opgegeven.

## Stap 7: Sla het Excel-bestand op

Laten we de werkmap opslaan, zodat we onze wijzigingen in een Excel-bestand kunnen bekijken.

```csharp
// Sla het Excel-bestand op
book.Save(dataDir + "protectedrange.out.xls");
```

Zorg ervoor dat u de bestandsnaam indien nodig aanpast. Dit creëert een Excel-bestand in de door u opgegeven map met de instellingen die we hebben geconfigureerd.

## Conclusie

Zo! Je hebt met succes een Excel-werkblad gemaakt dat bewerkingen beperkt tot een bepaald bereik, terwijl de rest van het werkblad wordt beschermd. Met Aspose.Cells voor .NET wordt het beheer van dit soort taken veel eenvoudiger en efficiënter. Of je nu een complexe applicatie ontwikkelt of gewoon gegevens veilig wilt beheren, deze mogelijkheden kunnen je workflow aanzienlijk verbeteren.

## Veelgestelde vragen

### Wat is Aspose.Cells?
Aspose.Cells is een krachtige .NET-bibliotheek voor het verwerken van Excel-bestanden en biedt functionaliteiten zoals het programmatisch maken, bewerken en converteren van spreadsheets.

### Kan ik meerdere bewerkbare bereiken toepassen?
Absoluut! Je kunt de `Add` methode op de `allowRanges` verzameling meerdere keren om meerdere bewerkbare bereiken op te geven.

### Wat gebeurt er als ik mijn wachtwoord vergeet?
Als u het wachtwoord voor een bewerkbaar bereik bent vergeten, moet u helaas de beveiliging verwijderen of op een vooraf gedefinieerde manier toegang tot het bestand krijgen. Hiervoor zijn mogelijk inloggegevens vereist.

### Bestaat er een gratis versie van Aspose.Cells?
Ja, Aspose biedt een gratis proefperiode aan, zodat u de functies kunt uitproberen voordat u tot aankoop overgaat.

### Waar kan ik meer informatie vinden over Aspose.Cells?
Je kunt de [documentatie](https://reference.aspose.com/cells/net/) voor gedetailleerde handleidingen en referenties.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}