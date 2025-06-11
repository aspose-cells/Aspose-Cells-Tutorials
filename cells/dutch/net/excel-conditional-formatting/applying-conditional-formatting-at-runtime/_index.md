---
"description": "Leer hoe u voorwaardelijke opmaak kunt toepassen tijdens runtime in Excel met Aspose.Cells voor .NET in deze uitgebreide, stapsgewijze handleiding."
"linktitle": "Voorwaardelijke opmaak toepassen tijdens runtime in Excel"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Voorwaardelijke opmaak toepassen tijdens runtime in Excel"
"url": "/nl/net/excel-conditional-formatting/applying-conditional-formatting-at-runtime/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Voorwaardelijke opmaak toepassen tijdens runtime in Excel

## Invoering

Het zijn krachtige tools voor data-analyse en -visualisatie. Een van de meest opvallende functies van Excel is voorwaardelijke opmaak, waarmee gebruikers specifieke opmaakstijlen op cellen kunnen toepassen op basis van hun waarden. Dit kan het gemakkelijker maken om trends te identificeren, belangrijke datapunten te markeren of gegevens gewoon leesbaarder te maken. Als u voorwaardelijke opmaak programmatisch in uw Excel-bestanden wilt implementeren, bent u hier aan het juiste adres! In deze handleiding laten we zien hoe u voorwaardelijke opmaak tijdens runtime kunt toepassen met Aspose.Cells voor .NET.

## Vereisten
Voordat we in de code duiken, controleren we of je alles hebt wat je nodig hebt om te beginnen:

1. Visual Studio: Zorg ervoor dat Visual Studio op uw computer is geïnstalleerd. U kunt elke versie gebruiken die .NET-ontwikkeling ondersteunt.
2. Aspose.Cells voor .NET: Je moet Aspose.Cells voor .NET geïnstalleerd hebben. Je kunt het downloaden van de [Aspose-website](https://releases.aspose.com/cells/net/).
3. Basiskennis van C#: Kennis van C#-programmering helpt u de codefragmenten beter te begrijpen.
4. .NET Framework: zorg ervoor dat uw project gericht is op een compatibele versie van .NET Framework.

Nu we de vereisten besproken hebben, kunnen we beginnen met het leukste gedeelte!

## Pakketten importeren
Om aan de slag te gaan met Aspose.Cells, moet je de benodigde naamruimten importeren in je C#-project. Zo doe je dat:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Via deze naamruimten krijgt u toegang tot de klassen en methoden die nodig zijn om Excel-bestanden te bewerken en voorwaardelijke opmaak toe te passen.

Laten we het proces van het toepassen van voorwaardelijke opmaak opsplitsen in hanteerbare stappen.

## Stap 1: Stel uw project in
Allereerst moet je een nieuw C#-project in Visual Studio maken. Zo doe je dat:

1. Open Visual Studio en selecteer Bestand > Nieuw > Project.
2. Kies Console App (.NET Framework) en geef uw project een naam.
3. Klik op Maken.

## Stap 2: Aspose.Cells-referentie toevoegen
Zodra uw project is ingesteld, moet u een verwijzing naar de Aspose.Cells-bibliotheek toevoegen:

1. Klik met de rechtermuisknop op uw project in Solution Explorer.
2. Selecteer NuGet-pakketten beheren.
3. Zoek naar Aspose.Cells en installeer het.

Hiermee kunt u alle functionaliteiten van de Aspose.Cells-bibliotheek gebruiken.

## Stap 3: Een werkmapobject maken
Laten we nu een nieuwe werkmap en een werkblad aanmaken. Dit is waar de magie gebeurt:

```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
string filePath = dataDir + "Book1.xlsx";

// Een werkmapobject instantiëren
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

In deze stap definiëren we de map waarin ons Excel-bestand wordt opgeslagen, maken we een nieuwe werkmap en openen we het eerste werkblad.

## Stap 4: Voorwaardelijke opmaak toevoegen
Laten we nu wat voorwaardelijke opmaak toevoegen. We beginnen met het aanmaken van een leeg object voor voorwaardelijke opmaak:

```csharp
// Voegt een lege voorwaardelijke opmaak toe
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```

Hier voegen we een nieuwe verzameling voorwaardelijke opmaak toe aan ons werkblad, waarin onze opmaakregels worden opgeslagen.

## Stap 5: Definieer het opmaakbereik
Vervolgens moeten we het celbereik specificeren waarop de voorwaardelijke opmaak van toepassing is. Stel dat we de eerste rij en de tweede kolom willen opmaken:

```csharp
// Stelt het bereik van de voorwaardelijke opmaak in.
CellArea ca = new CellArea();
ca.StartRow =0;
ca.EndRow =0;
ca.StartColumn =0;
ca.EndColumn =0;
fcs.AddArea(ca);

ca = new CellArea();
ca.StartRow =1;
ca.EndRow =1;
ca.StartColumn =1;
ca.EndColumn =1;
fcs.AddArea(ca);
```

In deze code definiëren we twee gebieden voor voorwaardelijke opmaak. Het eerste gebied is voor de cel op (0,0) en het tweede voor (1,1). U kunt deze bereiken naar eigen wens aanpassen!

## Stap 6: Voorwaardelijke opmaakvoorwaarden toevoegen
Nu is het tijd om de voorwaarden voor onze opmaak te definiëren. Stel dat we cellen willen markeren op basis van hun waarden:

```csharp
// Voegt voorwaarden toe.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "=A2", "100");

// Voegt voorwaarden toe.
int conditionIndex2 = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```

In deze stap voegen we twee voorwaarden toe: één voor waarden tussen `A2` En `100`, en een andere voor waarden tussen `50` En `100`Hiermee kunt u cellen dynamisch markeren op basis van hun waarden.

## Stap 7: Opmaakstijlen instellen
Nu de voorwaarden zijn ingesteld, kunnen we de opmaakstijlen instellen. Laten we de achtergrondkleur voor onze voorwaarden wijzigen:

```csharp
// Stelt de achtergrondkleur in.
FormatCondition fc = fcs[conditionIndex];
fc.Style.BackgroundColor = Color.Red;
```

Hier stellen we de achtergrondkleur van de eerste voorwaarde in op rood. Je kunt dit verder aanpassen door de kleur van het lettertype, de randen en andere stijlen naar wens aan te passen!

## Stap 8: Sla het Excel-bestand op
Eindelijk is het tijd om ons werk op te slaan! We slaan de werkmap op in de opgegeven map:

```csharp
// Het Excel-bestand opslaan
workbook.Save(dataDir + "output.xls");
```

Deze regel code slaat het Excel-bestand op met de voorwaardelijke opmaak. Controleer de opgegeven map voor uw uitvoerbestand!

## Conclusie
En voilà! U hebt met succes voorwaardelijke opmaak tijdens runtime in Excel toegepast met Aspose.Cells voor .NET. Deze krachtige bibliotheek maakt het eenvoudig om Excel-bestanden programmatisch te bewerken, waardoor u tijdrovende taken kunt automatiseren en uw gegevenspresentaties kunt verbeteren. Of u nu werkt aan een klein project of een grootschalige applicatie, Aspose.Cells kan u helpen uw workflow te stroomlijnen en uw productiviteit te verbeteren.

## Veelgestelde vragen

### Wat is Aspose.Cells?
Aspose.Cells is een .NET-bibliotheek waarmee ontwikkelaars programmatisch Excel-bestanden kunnen maken, bewerken en converteren.

### Kan ik Aspose.Cells gebruiken met andere programmeertalen?
Ja, Aspose.Cells is beschikbaar voor meerdere programmeertalen, waaronder Java, Python en meer.

### Is er een gratis proefversie beschikbaar voor Aspose.Cells?
Ja, u kunt een gratis proefversie downloaden van de [Aspose-website](https://releases.aspose.com/).

### Hoe kan ik ondersteuning krijgen voor Aspose.Cells?
U kunt ondersteuning krijgen door de [Aspose-ondersteuningsforum](https://forum.aspose.com/c/cells/9).

### Heb ik een licentie nodig om Aspose.Cells te gebruiken?
Ja, voor commercieel gebruik is een licentie vereist, maar u kunt een tijdelijke licentie aanvragen [hier](https://purchase.aspose.com/temporary-license/).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}