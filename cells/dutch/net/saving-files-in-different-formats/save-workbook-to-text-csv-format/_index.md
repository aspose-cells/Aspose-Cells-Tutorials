---
title: Werkmap opslaan in tekst-CSV-indeling
linktitle: Werkmap opslaan in tekst-CSV-indeling
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u Excel-werkmappen moeiteloos naar CSV-indeling kunt converteren met Aspose.Cells in deze uitgebreide, stapsgewijze zelfstudie, speciaal ontworpen voor .NET-ontwikkelaars.
weight: 17
url: /nl/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Werkmap opslaan in tekst-CSV-indeling

## Invoering
Bij het werken met data kan het formaat dat u kiest bepalen hoe gemakkelijk u ermee kunt werken. Een van de meest voorkomende formaten voor het verwerken van tabelgegevens is CSV (Comma-Separated Values). Als u een ontwikkelaar bent die met Excel-bestanden werkt en werkmappen naar CSV-formaat moet converteren, is Aspose.Cells voor .NET een fantastische bibliotheek die deze taak vereenvoudigt. In deze tutorial zullen we de stappen uiteenzetten om een Excel-werkmap naadloos naar een tekst-CSV-formaat te converteren.
## Vereisten
Voordat we beginnen, willen we ervoor zorgen dat u alles paraat hebt om te beginnen:
1. Basiskennis van C# en .NET: Omdat we code in C# gaan schrijven, is kennis van de taal en het .NET Framework essentieel.
2. Aspose.Cells Library: Zorg ervoor dat u de Aspose.Cells for .NET-bibliotheek in uw ontwikkelomgeving hebt geïnstalleerd. U kunt deze downloaden[hier](https://releases.aspose.com/cells/net/).
3. Visual Studio of een C# IDE: U hebt een geïntegreerde ontwikkelomgeving (IDE) nodig om uw code te schrijven en uit te voeren. Visual Studio is een populaire keuze.
4. Excel-werkmap: bereid een voorbeeld-Excel-werkmap voor (bijvoorbeeld 'book1.xls') die wat gegevens bevat om de conversie te testen.
## Pakketten importeren
Nu we onze vereisten hebben behandeld, is de eerste stap in het proces het importeren van de benodigde pakketten. In uw C#-project moet u de volgende naamruimte bovenaan uw codebestand opnemen:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Met deze naamruimten krijgt u toegang tot de klassen en methoden die u nodig hebt om met Excel-bestanden te werken en geheugenstromen te beheren.
## Stap 1: Definieer het pad naar de documentenmap
De eerste stap in ons proces is om te definiëren waar onze documenten (Excel-werkmappen) worden opgeslagen. Dit is essentieel omdat het ons programma laat weten waar de bestanden te vinden zijn die het moet verwerken. 
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
```
 Zorg ervoor dat u vervangt`"Your Document Directory"` met het daadwerkelijke pad waar uw "book1.xls" bestand zich bevindt. Dit kan een directory op uw computer zijn of een pad naar een server.
## Stap 2: Laad uw bronwerkboek
Vervolgens moeten we de Excel-werkmap laden die naar CSV-formaat moet worden geconverteerd.
```csharp
// Laad uw bronwerkmap
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 De`Workbook` klasse uit de Aspose.Cells-bibliotheek biedt manipulatie en toegang tot Excel-werkmappen. Door het bestandspad door te geven, laden we de opgegeven werkmap voor verwerking.
## Stap 3: Initialiseer een byte-array voor werkmapgegevens
Voordat we de werkmap naar CSV gaan converteren, moeten we een lege byte-array initialiseren waarin uiteindelijk alle werkbladgegevens worden opgeslagen.
```csharp
// 0-byte-array
byte[] workbookData = new byte[0];
```
Deze byte-array combineert de gegevens van elk werkblad in één structuur. Deze structuur kunnen we later naar een bestand schrijven.
## Stap 4: Stel de opties voor het opslaan van tekst in
Laten we nu de opties instellen voor hoe we de tekstopmaak willen opslaan. U kunt aangepaste scheidingstekens kiezen of bij tabs blijven.
```csharp
// Opties voor het opslaan van tekst. U kunt elk type scheidingsteken gebruiken
TxtSaveOptions opts = new TxtSaveOptions();
opts.Separator = '\t'; // Tabblad instellen als scheidingsteken
```
 In dit voorbeeld gebruiken we een tab-teken als scheidingsteken. U kunt`'\t'` met elk gewenst teken, zoals een komma (`,`), afhankelijk van hoe u uw CSV wilt opmaken.
## Stap 5: Herhaal elk werkblad
 Vervolgens gaan we door alle werkbladen in de werkmap heen en slaan we elk werkblad op in onze`workbookData` array, maar u moet eerst selecteren met welk werkblad u wilt werken.
```csharp
// Kopieer alle werkbladgegevens in tekstformaat in de werkmapgegevensarray
for (int idx = 0; idx < workbook.Worksheets.Count; idx++)
{
    // Sla het actieve werkblad op in tekstformaat
    MemoryStream ms = new MemoryStream();
    workbook.Worksheets.ActiveSheetIndex = idx;
    workbook.Save(ms, opts);
```
 De lus doorloopt elk werkblad in de werkmap.`ActiveSheetIndex` is zo ingesteld dat we elke keer dat we de lus doorlopen, het huidige werkblad opslaan. De resultaten worden in het geheugen opgeslagen met behulp van een`MemoryStream`.
## Stap 6: Werkbladgegevens ophalen
 Nadat u een werkblad in de geheugenstroom hebt opgeslagen, is de volgende stap het ophalen van deze gegevens en het toevoegen ervan aan ons`workbookData` reeks.
```csharp
    // Sla de werkbladgegevens op in een werkbladgegevensarray
    ms.Position = 0; // Positie van geheugenstroom resetten
    byte[] sheetData = ms.ToArray(); // Haal de byte-array op
```
`ms.Position = 0;` reset de positie voor het lezen na het schrijven. Vervolgens gebruiken we`ToArray()` om de geheugenstroom om te zetten in een byte-array die de werkbladgegevens bevat.
## Stap 7: Werkbladgegevens combineren
 Nu gaan we de gegevens van elk werkblad combineren tot één enkel werkblad.`workbookData` array eerder geïnitialiseerd.
```csharp
    // Combineer deze werkbladgegevens in een werkmapgegevensarray
    byte[] combinedArray = new byte[workbookData.Length + sheetData.Length];
    Array.Copy(workbookData, 0, combinedArray, 0, workbookData.Length);
    Array.Copy(sheetData, 0, combinedArray, workbookData.Length, sheetData.Length);
    workbookData = combinedArray;
}
```
We maken een nieuwe array die groot genoeg is om zowel bestaande werkmapgegevens als nieuwe werkbladgegevens te bevatten. Vervolgens kopiëren we de bestaande en nieuwe gegevens naar deze gecombineerde array voor later gebruik.
## Stap 8: Sla de volledige werkmapgegevens op in een bestand
 Ten slotte, met alle gegevens gecombineerd in onze`workbookData` array, kunnen we deze array opslaan in een opgegeven bestandspad.
```csharp
//Sla de volledige werkmapgegevens op in een bestand
File.WriteAllBytes(dataDir + "out.txt", workbookData);
```
`WriteAllBytes` neemt de gecombineerde byte-array en schrijft deze naar een tekstbestand met de naam "out.txt" in de opgegeven directory.
## Conclusie
En daar heb je het! Je hebt met succes een Excel-werkmap omgezet naar een CSV-formaat met Aspose.Cells voor .NET. Dit proces is niet alleen efficiënt, maar het maakt ook eenvoudige manipulatie van Excel-gegevens mogelijk voor verdere analyse of rapportage. Nu kun je je gegevensverwerkingstaken automatiseren of deze functionaliteit zelfs integreren in grotere toepassingen.
## Veelgestelde vragen
### Kan ik verschillende scheidingstekens gebruiken voor het CSV-bestand?
 Ja, u kunt de`opts.Separator` naar elk gewenst teken, bijvoorbeeld komma's of liggende streepjes.
### Is Aspose.Cells gratis te gebruiken?
 Aspose.Cells is niet gratis, maar je kunt een gratis proefversie krijgen[hier](https://releases.aspose.com/).
### In welke formaten kan ik opslaan, naast CSV?
Met Aspose.Cells kunt u bestanden opslaan in verschillende formaten, waaronder XLSX, PDF en meer.
### Kan ik grote Excel-bestanden verwerken met Aspose.Cells?
Ja, Aspose.Cells is ontworpen om grote bestanden efficiënt te verwerken, maar de prestaties zijn mogelijk afhankelijk van de systeembronnen.
### Waar kan ik meer gedetailleerde documentatie vinden?
Uitgebreide documentatie en voorbeelden vindt u op hun[referentie site](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
