---
title: Brongegevens van draaitabel programmatisch wijzigen in .NET
linktitle: Brongegevens van draaitabel programmatisch wijzigen in .NET
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u de brongegevens van draaitabellen programmatisch kunt wijzigen met Aspose.Cells voor .NET met onze uitgebreide stapsgewijze zelfstudie.
weight: 10
url: /nl/net/creating-and-configuring-pivot-tables/changing-source-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Brongegevens van draaitabel programmatisch wijzigen in .NET

## Invoering
In de wereld van data-analyse zijn er maar weinig tools die zo goed presteren als Microsoft Excel. Elke dag vertrouwen talloze gebruikers op Excel voor het beheren en analyseren van data, maar achter de schermen is het een stuk complexer dan alleen klikken en slepen. Als u ooit Excel-bestanden programmatisch hebt willen manipuleren, met name om de brongegevens van een draaitabel te wijzigen, bent u hier aan het juiste adres! In deze handleiding onderzoeken we hoe u dit kunt bereiken met Aspose.Cells voor .NET. Of u nu een doorgewinterde ontwikkelaar bent of net begint met programmeren, u zult deze tutorial boordevol waardevolle informatie vinden die gemakkelijk te volgen is.
## Vereisten
Voordat we beginnen met het wijzigen van de brongegevens van een draaitabel, zorgen we ervoor dat alles is ingesteld en klaar is voor gebruik:
1. Visual Studio: Zorg ervoor dat u een exemplaar van Microsoft Visual Studio hebt geïnstalleerd, aangezien we hier onze code gaan schrijven.
2. Aspose.Cells-bibliotheek: u moet de Aspose.Cells-bibliotheek hebben gedownload en ernaar verwijzen in uw project. U kunt deze downloaden[hier](https://releases.aspose.com/cells/net/).
3. Basiskennis van C#: Hoewel deze tutorial eenvoudig is, kunt u de code beter begrijpen als u C# al kent.
4. Excel-bestand: U zou een voorbeeld van een Excel-bestand moeten hebben (zoals 'Book1.xlsx') met een draaitabel die we kunnen bewerken.
Oké, nu we aan deze vereisten voldoen, kunnen we doorgaan met het importeren van de benodigde pakketten en beginnen met coderen!
## Pakketten importeren
Laten we eerst de pakketten importeren die we nodig hebben. Open uw C#-project in Visual Studio en voeg het volgende toe met behulp van richtlijnen boven aan uw codebestand:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Met deze naamruimten krijgt u toegang tot de essentiële klassen die u nodig hebt om met Excel-bestanden te werken en de inhoud ervan te bewerken met Aspose.Cells.

Laten we het proces nu opsplitsen in beheersbare stappen. We doorlopen het openen van een Excel-bestand, het aanpassen van het werkblad, het wijzigen van de gegevensbron van de draaitabel en het opslaan van de resultaten.
## Stap 1: Definieer uw documentendirectory
 Eerst moet u opgeven waar uw Excel-bestand zich bevindt. Wijzig de`dataDir` variabele om te verwijzen naar de map die uw "Book1.xlsx" bevat.
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
```
Met deze regel stelt u de map in waar uw Excel-bestand wordt opgeslagen, zodat u het later gemakkelijker kunt openen.
## Stap 2: Geef het invoerpad op
Laten we nu een tekenreeks maken om het volledige pad naar uw Excel-invoerbestand op te geven:
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
Hiermee stroomlijnt u de toegang tot uw bestanden; u hoeft niet steeds hetzelfde pad meerdere keren in uw code te typen.
## Stap 3: Een bestandsstroom maken
 Nu is het tijd om het Excel-bestand te openen. We gaan een`FileStream` waarmee u de inhoud van het Excel-bestand kunt lezen:
```csharp
// Een bestandsstroom maken met het te openen Excel-bestand
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
Deze regel opent het bestand in de leesmodus, zodat we toegang krijgen tot de gegevens.
## Stap 4: Laad de werkmap
Zodra de bestandsstroom is voltooid, is de volgende stap het laden van de werkmap:
```csharp
// Het Excel-bestand openen via de bestandsstroom
Workbook workbook = new Workbook(fstream);
```
 Met deze opdracht laadt u uw Excel-bestand in een`Workbook` object. Zodra het is geladen, kunt u het bestand naar wens bewerken.
## Stap 5: Toegang tot het werkblad
Tijd om in de details te duiken. We gaan naar het eerste werkblad in de werkmap:
```csharp
// Toegang krijgen tot het eerste werkblad in het Excel-bestand
Worksheet worksheet = workbook.Worksheets[0];
```
Hiermee krijgt u direct toegang tot de gegevens in het eerste werkblad, waardoor u deze eenvoudig kunt wijzigen.
## Stap 6: Nieuwe gegevens invullen
Vervolgens willen we nieuwe gegevens in de cellen invoegen. In dit voorbeeld voegen we wat voorbeeldgegevens toe:
```csharp
// Nieuwe gegevens in de werkbladcellen invoeren
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
 Hier plaatsen we de waarden "Golf", "Qtr4" en`7000` in specifieke cellen. U kunt deze waarden naar wens aanpassen.
## Stap 7: Wijzig het benoemde bereik
Nu gaan we het benoemde bereik wijzigen waarnaar de draaitabel verwijst. Dit houdt in dat we een bereik moeten maken of bijwerken:
```csharp
// Benoemd bereik "DataSource" wijzigen
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
Door een nieuw bereik te definiëren, zorgen we ervoor dat de draaitabel deze nieuwe gegevens gebruikt wanneer deze wordt vernieuwd.
## Stap 8: Sla het gewijzigde Excel-bestand op
Na alle wijzigingen is het cruciaal om uw werk op te slaan! Laten we de aangepaste werkmap opslaan:
```csharp
// Het gewijzigde Excel-bestand opslaan
workbook.Save(dataDir + "output.xls");
```
Met deze opdracht slaat u de werkmap op in een nieuw bestand. U overschrijft het oorspronkelijke bestand dus niet, tenzij u dat wilt!
## Stap 9: Sluit de bestandsstroom
Ten slotte is het essentieel om de bestandsstroom te sluiten om alle bronnen die u gebruikt vrij te geven:
```csharp
// De bestandsstroom sluiten om alle bronnen vrij te maken
fstream.Close();
```
Met deze stap zorgt u ervoor dat uw applicatie geen geheugenlek veroorzaakt en efficiënt blijft.
## Conclusie
Gefeliciteerd! U hebt zojuist met succes de brongegevens van een draaitabel programmatisch gewijzigd in .NET met behulp van Aspose.Cells. Deze functionaliteit opent veel mogelijkheden voor het automatiseren van Excel-taken en het verbeteren van uw workflow. Of u nu financiële rapporten bijwerkt, verkoopgegevens bijhoudt of gewoon met datasets speelt, de mogelijkheid om dit programmatisch te doen kan u veel tijd besparen en het risico op fouten verkleinen.

## Veelgestelde vragen
### Wat is Aspose.Cells?
Aspose.Cells is een krachtige .NET-bibliotheek voor het werken met Excel-bestanden, waarmee gebruikers Excel-documenten programmatisch kunnen maken, wijzigen en manipuleren.
### Kan ik de brongegevens van bestaande draaitabellen met deze methode wijzigen?
Absoluut! Met deze methode kunt u de gegevensbron voor bestaande draaitabellen in uw Excel-werkmap bijwerken.
### Moet ik Office geïnstalleerd hebben om Aspose.Cells te kunnen gebruiken?
Nee hoor! Aspose.Cells is een zelfstandige bibliotheek, wat betekent dat u Microsoft Office niet hoeft te installeren om met Excel-bestanden te werken.
### Is Aspose.Cells gratis te gebruiken?
Aspose.Cells biedt een gratis proefversie, maar voor volledige functionaliteit moet u een licentie kopen. U kunt de details vinden[hier](https://purchase.aspose.com/buy).
### Waar kan ik meer voorbeelden en ondersteuning vinden?
 Voor meer voorbeelden en ondersteuning, bekijk de[Aspose.Cells-documentatie](https://reference.aspose.com/cells/net/) en hun communityforum[hier](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
