---
title: Gesplitste panelen van werkblad
linktitle: Gesplitste panelen van werkblad
second_title: Aspose.Cells voor .NET API-referentie
description: Leer hoe u werkbladvensters splitst in Aspose.Cells voor .NET met onze stapsgewijze handleiding. Verbeter de navigatie in Excel-bestanden met deze eenvoudige tutorial.
weight: 130
url: /nl/net/excel-display-settings-csharp-tutorials/split-panes-of-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gesplitste panelen van werkblad

## Invoering

Bent u klaar om de panelen van een Excel-werkblad te splitsen met Aspose.Cells voor .NET? Stel u voor: u hebt een gigantisch Excel-blad en u bent het zat om steeds terug te scrollen naar de headers om te onthouden met welke kolom u werkt. Voer 'Panelen splitsen' in. Met deze handige functie kunt u een deel van uw werkblad bevriezen, waardoor u er veel gemakkelijker doorheen kunt navigeren. Of u nu werkt met financiële gegevens, voorraadbeheer of enorme datasets, het splitsen van panelen kan uw productiviteit vertienvoudigen. 

## Vereisten

Voordat we beginnen met het splitsen van panelen als een spreadsheet-wizard, moeten we eerst onze instellingen goed krijgen. Dit is wat je nodig hebt:

-  Aspose.Cells voor .NET: Zorg ervoor dat je het hebt gedownload en geïnstalleerd. Als je dat nog niet hebt gedaan, pak het dan[hier](https://releases.aspose.com/cells/net/).
- .NET Framework: In deze handleiding wordt ervan uitgegaan dat u in een .NET-omgeving werkt.
- Een Excel-werkmap: We gebruiken een voorbeeld-Excel-bestand om te laten zien hoe deze functie werkt.
-  Een tijdelijke of volledige licentie: Aspose.Cells vereist een licentie. Als u het gewoon uitprobeert, neem dan een[gratis tijdelijke licentie](https://purchase.aspose.com/temporary-license/) om evaluatiebeperkingen te vermijden.

## Pakketten importeren

Voordat we in de code duiken, importeren we eerst de benodigde namespaces. Je kunt eigenlijk niets doen in Aspose.Cells zonder deze op te nemen.

```csharp
using System.IO;
using Aspose.Cells;
```

Nu we de basis hebben besproken, kunnen we verder met het spannende gedeelte: het splitsen van panelen!

## Stap 1: Een werkmap instantiëren

 De eerste stap in dit proces is het creëren van een`Workbook` object, dat het Excel-bestand vertegenwoordigt dat u wilt wijzigen. In dit geval laden we een bestand uit een directory. Dit is uw canvas, het Excel-blad waarop u uw magie zult uitvoeren.

Voordat we panelen kunnen splitsen, hebben we een werkboek nodig om mee te werken! Deze stap is net zo essentieel als het openen van een boek voordat je begint met lezen.

```csharp
// Het pad naar de documentenmap
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Een nieuwe werkmap instantiëren en een sjabloonbestand openen
Workbook book = new Workbook(dataDir + "Book1.xls");
```

 Vervang in de bovenstaande code`"YOUR DOCUMENT DIRECTORY"` met het werkelijke pad waar uw Excel-bestand zich bevindt. De`Workbook`klasse laadt het Excel-bestand in het geheugen.

## Stap 2: Stel de actieve cel in

 Nadat u de werkmap hebt geladen, is het tijd om de actieve cel in te stellen. In Excel-termen is de actieve cel de cel die momenteel is geselecteerd of in focus is. In deze tutorial selecteren we cel`A20` in het eerste werkblad.

Het instellen van de actieve cel is cruciaal omdat de splitsing van het paneel start vanaf deze actieve cel. Het is net als kiezen waar je de eerste snede in een pizza maakt: kies je punt!

```csharp
// Actieve cel instellen
book.Worksheets[0].ActiveCell = "A20";
```

 Dit stukje code maakt`A20` de actieve cel. Het is belangrijk omdat splitsing rond dit punt plaatsvindt, net zoals uw navigatie in Excel vaak rond een specifieke cel draait.

## Stap 3: Splits het werkblad

Nu de actieve cel is ingesteld, gaan we naar het leuke gedeelte: het werkblad splitsen! Deze stap is waar de magie gebeurt. U kunt het werkblad in meerdere panelen verdelen voor eenvoudiger bekijken en navigeren.

Dit is de kern van de hele tutorial. Door het werkblad te splitsen, creëert u afzonderlijke panelen waarmee u door verschillende secties van uw Excel-sheet kunt scrollen zonder de headers of andere belangrijke gebieden uit het oog te verliezen.

```csharp
// Werkbladvenster splitsen
book.Worksheets[0].Split();
```

 Met de`Split()` Met deze methode vertelt u Aspose.Cells om het werkblad te splitsen in de actieve cel (`A20` in dit geval). Vanaf dit punt maakt Excel een scheiding in het werkblad die de deelvensters scheidt, zodat u onafhankelijk van elkaar kunt navigeren.

## Stap 4: Sla de werkmap op

Nadat u de panelen hebt gesplitst, hoeft u alleen nog maar uw werk op te slaan. Deze laatste stap zorgt ervoor dat uw wijzigingen worden opgeslagen in het opgegeven uitvoerbestand.

Wat heb je aan al je harde werk als je het niet bewaart? Bewaren zorgt ervoor dat je prachtig gespleten ruiten intact blijven voor toekomstig gebruik.

```csharp
// Sla het Excel-bestand op
book.Save(dataDir + "output.xls");
```

 Hier, de`Save()` methode slaat de werkmap met uw nieuw gesplitste panelen op in een Excel-uitvoerbestand. De wijzigingen die u hebt aangebracht, zijn nu klaar voor u, of iemand anders, om te gebruiken.

## Conclusie

En daar heb je het! Je hebt net geleerd hoe je panelen in een Excel-werkblad kunt splitsen met Aspose.Cells voor .NET. Nooit meer eindeloos scrollen of het overzicht verliezen over je gegevens. Deze methode maakt het verwerken van grote Excel-bestanden veel minder overweldigend en veel efficiënter. Met de mogelijkheid om panelen te splitsen, kun je nu kritieke datapunten bijhouden terwijl je met complexe spreadsheets werkt.

## Veelgestelde vragen

### Kan ik meer dan twee panelen splitsen?  
 Ja, u kunt het werkblad in meerdere deelvensters splitsen door verschillende actieve cellen op te geven en de`Split()` methode.

### Wat is het verschil tussen het splijten van ruiten en het bevriezen van ruiten?  
Door panelen te splitsen kunt u onafhankelijk van elkaar in beide panelen scrollen. Door panelen te bevriezen worden de headers of specifieke rijen/kolommen vergrendeld, zodat ze zichtbaar blijven tijdens het scrollen.

### Kan ik de scheur verwijderen nadat ik het heb aangebracht?  
Ja, u kunt de splitsing ongedaan maken door de werkmap te sluiten en opnieuw te openen, of door deze programmatisch opnieuw in te stellen.

### Werkt het splitsen van deelvensters hetzelfde voor verschillende Excel-bestandsformaten (XLS, XLSX)?  
 Ja, de`Split()` Deze methode werkt voor zowel XLS- als XLSX-formaten.

### Kan ik Aspose.Cells gebruiken zonder licentie?  
 Ja, maar het heeft beperkingen. Voor een volledige ervaring is het het beste om een[tijdelijk](https://purchase.aspose.com/temporary-license/) of[betaalde licentie](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
