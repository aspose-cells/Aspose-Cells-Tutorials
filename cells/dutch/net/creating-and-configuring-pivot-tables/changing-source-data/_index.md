---
"description": "Leer hoe u de brongegevens van een draaitabel programmatisch kunt wijzigen met Aspose.Cells voor .NET met onze uitgebreide stapsgewijze zelfstudie."
"linktitle": "Brongegevens van draaitabel programmatisch wijzigen in .NET"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Brongegevens van draaitabel programmatisch wijzigen in .NET"
"url": "/nl/net/creating-and-configuring-pivot-tables/changing-source-data/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Brongegevens van draaitabel programmatisch wijzigen in .NET

## Invoering
In de wereld van data-analyse schitteren weinig tools zo sterk als Microsoft Excel. Dagelijks vertrouwen talloze gebruikers op Excel voor het beheren en analyseren van data, maar achter de schermen is het een stuk complexer dan alleen klikken en slepen. Als je ooit programmatisch Excel-bestanden hebt willen bewerken – met name om de brongegevens van een draaitabel te wijzigen – dan ben je hier aan het juiste adres! In deze handleiding onderzoeken we hoe je dit kunt bereiken met Aspose.Cells voor .NET. Of je nu een ervaren ontwikkelaar bent of net begint met programmeren, deze tutorial staat boordevol waardevolle informatie die gemakkelijk te volgen is.
## Vereisten
Voordat we beginnen met het wijzigen van de brongegevens van een draaitabel, zorgen we ervoor dat alles is ingesteld en klaar voor gebruik:
1. Visual Studio: Zorg ervoor dat u een exemplaar van Microsoft Visual Studio hebt geïnstalleerd, aangezien we hier onze code schrijven.
2. Aspose.Cells-bibliotheek: Je moet de Aspose.Cells-bibliotheek downloaden en ernaar verwijzen in je project. Je kunt deze downloaden [hier](https://releases.aspose.com/cells/net/).
3. Basiskennis van C#: Hoewel deze tutorial vereenvoudigd is, zult u de code beter begrijpen als u C# al kent.
4. Excel-bestand: U zou een voorbeeld van een Excel-bestand moeten hebben (zoals "Book1.xlsx") met daarin een draaitabel die we kunnen bewerken.
Oké, nu we aan deze vereisten voldoen, kunnen we doorgaan met het importeren van de benodigde pakketten en beginnen met coderen!
## Pakketten importeren
Laten we beginnen met het importeren van de pakketten die we nodig hebben. Open je C#-project in Visual Studio en voeg de volgende instructies toe bovenaan je codebestand:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Met deze naamruimten krijgt u toegang tot de essentiële klassen die nodig zijn om met Excel-bestanden te werken en de inhoud ervan te bewerken met Aspose.Cells.

Laten we het proces nu opsplitsen in beheersbare stappen. We doorlopen het openen van een Excel-bestand, het aanpassen van het werkblad, het wijzigen van de gegevensbron van de draaitabel en het opslaan van de resultaten.
## Stap 1: Definieer uw documentenmap
Eerst moet u opgeven waar uw Excel-bestand zich bevindt. Wijzig de `dataDir` variabele om te verwijzen naar de map met uw bestand "Book1.xlsx".
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
```
Met deze regel stelt u de map in waar uw Excel-bestand wordt opgeslagen, zodat u het later gemakkelijker kunt openen.
## Stap 2: Geef het invoerpad op
Laten we vervolgens een tekenreeks maken om het volledige pad naar uw Excel-invoerbestand op te geven:
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
Hiermee stroomlijnt u de toegang tot uw bestanden: u hoeft niet steeds hetzelfde pad meerdere keren in uw code te typen.
## Stap 3: Een bestandsstroom maken
Nu is het tijd om het Excel-bestand te openen. We gaan een `FileStream` waarmee u de inhoud van het Excel-bestand kunt lezen:
```csharp
// Een bestandsstroom maken met het te openen Excel-bestand
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
Met deze regel wordt het bestand in de leesmodus geopend, zodat we toegang krijgen tot de gegevens.
## Stap 4: Laad de werkmap
Zodra de bestandsstroom op zijn plaats staat, is de volgende stap het laden van de werkmap:
```csharp
// Het Excel-bestand openen via de bestandsstroom
Workbook workbook = new Workbook(fstream);
```
Met deze opdracht laadt u uw Excel-bestand in een `Workbook` object. Nadat het is geladen, kunt u het bestand naar wens bewerken.
## Stap 5: Toegang tot het werkblad
Tijd om in de details te duiken. We gaan naar het eerste werkblad in de werkmap:
```csharp
// Toegang krijgen tot het eerste werkblad in het Excel-bestand
Worksheet worksheet = workbook.Worksheets[0];
```
Hiermee krijgt u direct toegang tot de gegevens in het eerste werkblad, waardoor u deze eenvoudig kunt aanpassen.
## Stap 6: Nieuwe gegevens invullen
Vervolgens willen we nieuwe gegevens in de cellen invoegen. In dit voorbeeld voegen we wat voorbeeldgegevens toe:
```csharp
// Nieuwe gegevens in de werkbladcellen invullen
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
Hier plaatsen we de waarden "Golf", "Qtr4" en `7000` in specifieke cellen. U kunt deze waarden naar wens aanpassen.
## Stap 7: Wijzig het benoemde bereik
Nu gaan we het benoemde bereik waarnaar de draaitabel verwijst, wijzigen. Dit houdt in dat we een bereik moeten aanmaken of bijwerken:
```csharp
// Benoemd bereik "DataSource" wijzigen
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
Door een nieuw bereik te definiëren, zorgen we ervoor dat de draaitabel deze nieuwe gegevens gebruikt wanneer deze wordt vernieuwd.
## Stap 8: Sla het gewijzigde Excel-bestand op
Na alle wijzigingen is het cruciaal om je werk op te slaan! Laten we de gewijzigde werkmap opslaan:
```csharp
// Het gewijzigde Excel-bestand opslaan
workbook.Save(dataDir + "output.xls");
```
Met deze opdracht slaat u de werkmap op in een nieuw bestand. U overschrijft dus niet uw oorspronkelijke bestand, tenzij u dat wilt!
## Stap 9: Sluit de bestandsstroom
Ten slotte is het essentieel om de bestandsstroom te sluiten om alle bronnen die u gebruikt vrij te geven:
```csharp
// De bestandsstroom sluiten om alle bronnen vrij te maken
fstream.Close();
```
Met deze stap zorgt u ervoor dat uw applicatie geen geheugenlek veroorzaakt en efficiënt blijft.
## Conclusie
Gefeliciteerd! U hebt zojuist met succes de brongegevens van een draaitabel programmatisch gewijzigd in .NET met behulp van Aspose.Cells. Deze functionaliteit opent talloze mogelijkheden voor het automatiseren van Excel-taken en het verbeteren van uw workflow. Of u nu financiële rapporten bijwerkt, verkoopgegevens bijhoudt of gewoon met datasets speelt, de mogelijkheid om dit programmatisch te doen, bespaart u enorm veel tijd en verkleint de kans op fouten.

## Veelgestelde vragen
### Wat is Aspose.Cells?
Aspose.Cells is een krachtige .NET-bibliotheek voor het werken met Excel-bestanden, waarmee gebruikers programmatisch Excel-documenten kunnen maken, wijzigen en manipuleren.
### Kan ik de brongegevens van bestaande draaitabellen met deze methode wijzigen?
Absoluut! Met deze methode kunt u de gegevensbron voor bestaande draaitabellen in uw Excel-werkmap bijwerken.
### Moet ik Office geïnstalleerd hebben om Aspose.Cells te gebruiken?
Nee! Aspose.Cells is een zelfstandige bibliotheek, wat betekent dat u geen Microsoft Office hoeft te installeren om met Excel-bestanden te werken.
### Is Aspose.Cells gratis te gebruiken?
Aspose.Cells biedt een gratis proefversie aan, maar voor volledige functionaliteit moet u een licentie aanschaffen. Meer informatie vindt u hier. [hier](https://purchase.aspose.com/buy).
### Waar kan ik meer voorbeelden en ondersteuning vinden?
Voor meer voorbeelden en ondersteuning, bekijk de [Aspose.Cells-documentatie](https://reference.aspose.com/cells/net/) en hun communityforum [hier](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}