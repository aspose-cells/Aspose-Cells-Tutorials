---
title: Ingesloten Mol-bestand uit werkmap extraheren
linktitle: Ingesloten Mol-bestand uit werkmap extraheren
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer in deze gedetailleerde stapsgewijze zelfstudie hoe u ingesloten MOL-bestanden uit Excel-werkmappen kunt extraheren met Aspose.Cells voor .NET.
weight: 18
url: /nl/net/workbook-operations/extract-embedded-mol-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ingesloten Mol-bestand uit werkmap extraheren

## Invoering
Wanneer het aankomt op het beheren van gegevens in Excel-werkmappen, kom je soms verschillende ingebedde objecten tegen die niet in een standaardformaat staan. Een dergelijk formaat is het MOL (Molecular Structure File), dat veel wordt gebruikt in de scheikunde om moleculaire informatie weer te geven. Als je deze MOL-bestanden uit een Excel-werkmap wilt halen met Aspose.Cells voor .NET, dan ben je bij de juiste gids terechtgekomen. In dit artikel leiden we je stap voor stap door het proces en ontmystificeren we elk onderdeel.
## Vereisten
Voordat je in de code duikt, is het essentieel om ervoor te zorgen dat je de benodigde vaardigheden en tools hebt. Dit is wat je nodig hebt:
1. Basiskennis van .NET-programmering: U moet bekend zijn met C# en het .NET Framework.
2.  Aspose.Cells voor .NET: Zorg dat u de Aspose.Cells-bibliotheek hebt. U kunt[download het hier](https://releases.aspose.com/cells/net/).
3. Een IDE: U kunt Visual Studio of een andere .NET-compatibele IDE gebruiken.
4. Excel-werkmap met ingebedde MOL-bestanden: voor deze tutorial hebt u een Excel-bestand met MOL-objecten nodig. U kunt uw eigen bestand maken of een voorbeeldbestand gebruiken.
## Pakketten importeren
Om te beginnen moet u de benodigde naamruimten in uw project importeren. Dit is cruciaal voor toegang tot de Aspose.Cells-functionaliteiten. Dit is hoe u dit kunt doen:

```csharp
using Aspose.Cells.Drawing;
using Aspose.Cells.WebExtensions;
using System;
using System.IO;
```

Met deze naamruimten kunt u werkmappen bewerken, werkbladen openen en in het algemeen met bestanden werken.
Nu we aan de vereisten hebben voldaan, duiken we in de code en begrijpen we elke stap die nodig is om ingesloten MOL-bestanden uit een Excel-werkmap te extraheren. 
## Stap 1: Uw mappen instellen
De eerste stap is om te definiëren waar uw brondocument zich bevindt en waar u de geëxtraheerde MOL-bestanden wilt opslaan. Laten we die mappen instellen.
```csharp
string SourceDir = "Your Document Directory"; // Vervang door uw directorypad
string outputDir = "Your Document Directory"; // Vervang met uw uitvoerpad
```
 Hier vervang je`"Your Document Directory"`met het pad naar uw werkelijke mappen. Het is belangrijk dat zowel de bron- als de uitvoermappen toegankelijk zijn voor uw toepassing.
## Stap 2: De werkmap laden
Zodra u uw mappen hebt ingesteld, is de volgende taak het laden van de Excel-werkmap. Laten we dat nu doen.

```csharp
Workbook workbook = new Workbook(SourceDir + "EmbeddedMolSample.xlsx");
```

 We maken een exemplaar van de`Workbook` klasse en het pad naar ons Excel-bestand met de naam doorgeven`EmbeddedMolSample.xlsx`Met deze stap wordt de werkmap geïnitialiseerd, zodat u toegang krijgt tot de inhoud ervan.
## Stap 3: Itereren over werkbladen
Nu uw werkmap is geladen, moet u door elk werkblad in de werkmap heen lopen. Hiermee kunt u elk werkblad onderzoeken op ingesloten objecten.

```csharp
var index = 1; // Wordt gebruikt voor het benoemen van geëxtraheerde MOL-bestanden
foreach (Worksheet sheet in workbook.Worksheets)
{
    OleObjectCollection oles = sheet.OleObjects;
    // Verdere extractielogica gaat hier
}
```

 Hier gebruik je een`foreach` lus om door de werkbladen te navigeren. Voor elk werkblad heb je toegang tot de`OleObjects` verzameling, die alle ingesloten objecten bevat.
## Stap 4: MOL-bestanden extraheren
Nu komt het kritieke deel: het extraheren van de MOL-bestanden uit de OLE-objecten. Hiervoor is een andere lus in de werkbladlus nodig.

```csharp
foreach (OleObject ole in oles)
{
    string fileName = outputDir + "OleObject" + index + ".mol ";
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
    index++;
}
```

 Voor elk OLE-object dat u hebt gevonden, maakt u een nieuw bestand in de uitvoermap.`ObjectData` eigendom van de`OleObject` bevat de gegevens van het ingesloten object, die u naar een nieuw gemaakt bestand schrijft met behulp van een`FileStream`. Het bestand heeft een sequentiele naam (`OleObject1.mol`, `OleObject2.mol` , enz.) op basis van de`index` variabel.
## Stap 5: Bevestiging van de voltooiing van het proces
Als alle MOL-bestanden zijn uitgepakt, is het een goed idee om de gebruiker te informeren dat het proces succesvol is voltooid.

```csharp
Console.WriteLine("ExtractEmbeddedMolFile executed successfully.");
```

Deze regel print gewoon een bericht naar de console om u te laten weten dat de extractie succesvol was. Het is een aardige touch voor gebruikersfeedback.
## Conclusie
En daar heb je het! Je hebt met succes ingebedde MOL-bestanden uit een Excel-werkmap geëxtraheerd met Aspose.Cells voor .NET. Dit proces integreert een paar kernstappen, wat zorgt voor een gestructureerde aanpak voor het verwerken van ingebedde objecten. Of je nu bezig bent met wetenschappelijk onderzoek, chemische analyse of gewoon met complexe datasets, het kunnen extraheren en manipuleren van deze bestandstypen kan een groot verschil maken in de manier waarop je je informatie beheert. 
## Veelgestelde vragen
### Kan ik naast MOL ook andere bestandstypen uit Excel halen?
Ja, u kunt verschillende andere ingesloten bestandstypen met vergelijkbare technieken extraheren.
### Is Aspose.Cells gratis te gebruiken?
 Aspose.Cells is een commerciële bibliotheek, maar u kunt[probeer het gratis voor een beperkte periode](https://releases.aspose.com/).
### Werkt deze methode met alle Excel-versies?
Ja, zolang het bestandsformaat wordt ondersteund door Aspose.Cells.
### Kan ik dit extractieproces automatiseren?
Absoluut! Je kunt dit proces automatiseren door de code in een geplande taak of een script te plaatsen.
### Waar kan ik meer documentatie over Aspose.Cells vinden?
 U kunt de[Aspose.Cells-documentatie](https://reference.aspose.com/cells/net/) voor meer details en voorbeelden.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
