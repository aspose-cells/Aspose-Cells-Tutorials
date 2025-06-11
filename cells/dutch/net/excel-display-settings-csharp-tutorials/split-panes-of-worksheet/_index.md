---
"description": "Leer hoe je werkbladvensters kunt splitsen in Aspose.Cells voor .NET met onze stapsgewijze handleiding. Verbeter de navigatie door Excel-bestanden met deze eenvoudige tutorial."
"linktitle": "Gesplitste panelen van werkblad"
"second_title": "Aspose.Cells voor .NET API-referentie"
"title": "Gesplitste panelen van werkblad"
"url": "/nl/net/excel-display-settings-csharp-tutorials/split-panes-of-worksheet/"
"weight": 130
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Gesplitste panelen van werkblad

## Invoering

Bent u klaar om de deelvensters van een Excel-werkblad te splitsen met Aspose.Cells voor .NET? Stelt u zich eens voor: u hebt een gigantische Excel-sheet en u bent het zat om steeds terug te scrollen naar de kopteksten om te onthouden met welke kolom u werkt. Voer 'Deelvensters splitsen' in. Met deze handige functie kunt u een deel van uw werkblad vastzetten, waardoor navigeren veel gemakkelijker wordt. Of u nu werkt met financiële gegevens, voorraadbeheer of enorme datasets, het splitsen van deelvensters kan uw productiviteit vertienvoudigen. 

## Vereisten

Voordat we beginnen met het splitsen van deelvensters als een spreadsheet-wizard, moeten we eerst de juiste instellingen maken. Dit heb je nodig:

- Aspose.Cells voor .NET: Zorg ervoor dat je het hebt gedownload en geïnstalleerd. Als je dat nog niet hebt gedaan, download het dan. [hier](https://releases.aspose.com/cells/net/).
- .NET Framework: in deze handleiding wordt ervan uitgegaan dat u in een .NET-omgeving werkt.
- Een Excel-werkmap: We gebruiken een voorbeeld-Excel-bestand om te laten zien hoe deze functie werkt.
- Een tijdelijke of volledige licentie: Aspose.Cells vereist een licentie. Als je het gewoon wilt uitproberen, neem dan een [gratis tijdelijke licentie](https://purchase.aspose.com/temporary-license/) om evaluatiebeperkingen te vermijden.

## Pakketten importeren

Voordat we de code induiken, importeren we eerst de benodigde naamruimten. Je kunt in Aspose.Cells eigenlijk niets doen zonder deze op te nemen.

```csharp
using System.IO;
using Aspose.Cells;
```

Nu we de basis hebben besproken, kunnen we verder met het leukste gedeelte: het splitsen van de ruiten!

## Stap 1: Een werkmap instantiëren

De eerste stap in dit proces is het creëren van een `Workbook` object, dat het Excel-bestand vertegenwoordigt dat u wilt wijzigen. In dit geval laden we een bestand uit een map. Dit is uw canvas, het Excel-bestand waarop u uw magie gaat uitoefenen.

Voordat we vensters kunnen splitsen, hebben we een werkmap nodig om mee te werken! Deze stap is net zo essentieel als het openen van een boek voordat je begint met lezen.

```csharp
// Het pad naar de documentenmap
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Een nieuwe werkmap instantiëren en een sjabloonbestand openen
Workbook book = new Workbook(dataDir + "Book1.xls");
```

Vervang in de bovenstaande code `"YOUR DOCUMENT DIRECTORY"` met het daadwerkelijke pad waar uw Excel-bestand zich bevindt. De `Workbook` klasse laadt het Excel-bestand in het geheugen.

## Stap 2: De actieve cel instellen

Nadat de werkmap is geladen, is het tijd om de actieve cel in te stellen. In Excel-termen is de actieve cel de cel die momenteel is geselecteerd of de focus heeft. In deze tutorial selecteren we cel `A20` in het eerste werkblad.

Het instellen van de actieve cel is cruciaal, omdat het splitsen van het venster vanuit deze actieve cel begint. Het is net als kiezen waar je de eerste snede in een pizza maakt: kies je punt!

```csharp
// De actieve cel instellen
book.Worksheets[0].ActiveCell = "A20";
```

Dit stukje code maakt `A20` De actieve cel. Dit is belangrijk omdat de splitsing rond dit punt plaatsvindt, net zoals uw navigatie in Excel vaak rond een specifieke cel draait.

## Stap 3: Splits het werkblad

Nu de actieve cel is ingesteld, gaan we verder met het leukste gedeelte: het werkblad splitsen! Deze stap is waar de magie gebeurt. Je kunt het werkblad in meerdere deelvensters verdelen voor eenvoudiger bekijken en navigeren.

Dit is de kern van de hele tutorial. Door het werkblad te splitsen, creëert u aparte deelvensters waarmee u door verschillende secties van uw Excel-bestand kunt scrollen zonder kopteksten of andere belangrijke onderdelen uit het oog te verliezen.

```csharp
// Het werkbladvenster splitsen
book.Worksheets[0].Split();
```

Met de `Split()` Met deze methode vertelt u Aspose.Cells om het werkblad te splitsen in de actieve cel (`A20` (in dit geval). Vanaf dit punt maakt Excel een scheiding in het werkblad, waardoor u onafhankelijk van elkaar door de deelvensters kunt navigeren.

## Stap 4: Sla de werkmap op

Nadat u de deelvensters hebt gesplitst, hoeft u uw werk alleen nog maar op te slaan. Deze laatste stap zorgt ervoor dat uw wijzigingen worden opgeslagen in het opgegeven uitvoerbestand.

Wat heb je aan al je harde werk als je het niet bewaart? Door te bewaren, zorg je ervoor dat je prachtig gespleten ruiten intact blijven voor toekomstig gebruik.

```csharp
// Sla het Excel-bestand op
book.Save(dataDir + "output.xls");
```

Hier, de `Save()` Met deze methode wordt de werkmap met de nieuw gesplitste deelvensters opgeslagen in een Excel-uitvoerbestand. De wijzigingen die u hebt aangebracht, zijn nu klaar voor gebruik door u – of iemand anders.

## Conclusie

En voilà! Je hebt net geleerd hoe je deelvensters in een Excel-werkblad kunt splitsen met Aspose.Cells voor .NET. Nooit meer eindeloos scrollen of het overzicht verliezen over je gegevens. Deze methode maakt het werken met grote Excel-bestanden veel minder overweldigend en veel efficiënter. Dankzij de mogelijkheid om deelvensters te splitsen, kun je nu kritieke datapunten bijhouden terwijl je met complexe spreadsheets werkt.

## Veelgestelde vragen

### Kan ik meer dan twee panelen splitsen?  
Ja, u kunt het werkblad in meerdere deelvensters splitsen door verschillende actieve cellen op te geven en de `Split()` methode.

### Wat is het verschil tussen het splijten en het bevriezen van ruiten?  
Door deelvensters te splitsen, kunt u onafhankelijk van elkaar in beide deelvensters scrollen. Door deelvensters te blokkeren, worden de kopteksten of specifieke rijen/kolommen vergrendeld, zodat ze zichtbaar blijven tijdens het scrollen.

### Kan ik de scheur verwijderen nadat ik het heb aangebracht?  
Ja, u kunt de splitsing ongedaan maken door de werkmap te sluiten en opnieuw te openen, of door deze programmatisch te resetten.

### Werkt het splitsen van deelvensters hetzelfde voor verschillende Excel-bestandsindelingen (XLS, XLSX)?  
Ja, de `Split()` Deze methode werkt voor zowel XLS- als XLSX-formaten.

### Kan ik Aspose.Cells gebruiken zonder licentie?  
Ja, maar het heeft beperkingen. Voor een volledige ervaring is het het beste om een [tijdelijk](https://purchase.aspose.com/tempofary-license/) or [betaalde licentie](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}