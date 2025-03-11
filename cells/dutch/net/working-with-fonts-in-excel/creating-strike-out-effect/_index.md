---
title: Doorstreepeffect op tekst in Excel maken
linktitle: Doorstreepeffect op tekst in Excel maken
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer in deze gedetailleerde stapsgewijze zelfstudie hoe u een doorhalingseffect op tekst in Excel toepast met Aspose.Cells voor .NET.
weight: 15
url: /nl/net/working-with-fonts-in-excel/creating-strike-out-effect/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Doorstreepeffect op tekst in Excel maken

## Invoering
Als het om Excel gaat, zijn visuele elementen net zo belangrijk als de gegevens zelf. Of u nu belangrijke wijzigingen markeert of items markeert die niet langer relevant zijn, het doorhalingseffect op tekst is een klassieke manier om visuele weergave in spreadsheets te beheren. In deze handleiding leiden we u door het proces van het implementeren van een doorhalingseffect op tekst in Excel met behulp van Aspose.Cells voor .NET. Deze tutorial behandelt niet alleen de noodzakelijke vereisten, maar biedt ook een stapsgewijze aanpak om ervoor te zorgen dat u dit effect eenvoudig kunt repliceren.
## Vereisten
Voordat u met de tutorial begint, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:
1. Development Environment: U moet een .NET development environment hebben ingesteld. Dit kan Visual Studio zijn of een andere IDE die u verkiest en die .NET development ondersteunt.
2. Aspose.Cells voor .NET: Zorg ervoor dat u Aspose.Cells in uw project hebt geïnstalleerd. U kunt het downloaden via de volgende link:[Download Aspose.Cellen](https://releases.aspose.com/cells/net/).
3. Basiskennis van C#: Een basiskennis van C#-programmering is nuttig, aangezien de voorbeelden in C# zijn gecodeerd.
4. .NET Framework: Zorg ervoor dat uw project is gericht op een compatibele .NET Framework-versie, meestal .NET Core of .NET Framework 4.5 en hoger.
## Pakketten importeren
Voordat u code schrijft, moet u de vereiste naamruimten importeren uit Aspose.Cells. Dit is cruciaal voor toegang tot verschillende functies die door de bibliotheek worden geboden. Hier leest u hoe u de vereiste naamruimten kunt importeren:
```csharp
using System.IO;
using Aspose.Cells;
```
Met deze imports krijgt u toegang tot de klassen Workbook, Worksheet en Style die in deze zelfstudie worden gebruikt.
Nu we de toon hebben gezet, gaan we het proces opsplitsen in beheersbare stappen. Elke stap wordt vergezeld door duidelijke instructies om u te begeleiden bij het maken van een doorhalingseffect op tekst in Excel.
## Stap 1: Definieer de documentdirectory
Begin met het definiëren van het pad waar uw Excel-documenten worden opgeslagen. Dit is de locatie voor het opslaan van uw uitvoerbestanden.
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
```
 Vervangen`"Your Document Directory"` met het daadwerkelijke directorypad waar u uw Excel-bestand wilt opslaan. Dit stelt de directory in voor uw uitvoer.
## Stap 2: Maak de directory
Vervolgens moet u ervoor zorgen dat de directory die u in de vorige stap hebt opgegeven, bestaat. Als deze niet bestaat, kunt u deze programmatisch aanmaken.
```csharp
// Maak een map aan als deze nog niet bestaat.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Deze code controleert of de directory bestaat en maakt deze aan als dat niet zo is. Dit helpt fouten te voorkomen wanneer u later uw bestand probeert op te slaan.
## Stap 3: Een werkmapobject instantiëren
Nu is het tijd om een nieuw Workbook-object te maken. Dit is de basis van uw Excel-bestand waar u gegevens aan toevoegt en formaten toepast.
```csharp
// Een werkmapobject instantiëren
Workbook workbook = new Workbook();
```
 De`Workbook` class vertegenwoordigt een Excel-bestand. Door een instantie van deze klasse te maken, maakt u in feite een nieuw Excel-document.
## Stap 4: Een nieuw werkblad toevoegen
Elke werkmap kan meerdere werkbladen bevatten. Laten we doorgaan en een nieuw werkblad in uw werkmap maken.
```csharp
// Een nieuw werkblad toevoegen aan het Excel-object
int i = workbook.Worksheets.Add();
```
 De`Add` methode van de`Worksheets` collection voegt een nieuw werkblad toe aan de werkmap en retourneert de index ervan. 
## Stap 5: Verkrijg de referentie van het nieuwe werkblad
Nadat u het werkblad hebt gemaakt, moet u het gebruiken als referentie voor toekomstige bewerkingen.
```csharp
// De referentie van het nieuw toegevoegde werkblad verkrijgen door de index van het werkblad door te geven
Worksheet worksheet = workbook.Worksheets[i];
```
Hier haalt u het nieuw gemaakte werkblad op met behulp van de index (`i`). Hiermee krijgt u toegang om het werkblad te bewerken.
## Stap 6: Toegang tot een cel
 U wilt een specifieke cel in uw werkblad openen waar u de doorhalingsopmaak wilt toepassen. In dit voorbeeld gebruiken we cel`A1`.
```csharp
// Toegang tot cel "A1" vanuit het werkblad
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```
 In Excel worden cellen aangeduid met hun kolom- en rij-identificaties (bijv. "A1"). We verkrijgen een verwijzing naar cel`A1` voor verdere manipulatie.
## Stap 7: Voeg waarde toe aan de cel
 Vervolgens voegen we wat tekst toe aan de cel. We schrijven "Hallo Aspose!" in cel`A1`.
```csharp
// Waarde toevoegen aan cel "A1"
cell.PutValue("Hello Aspose!");
```
 De`PutValue` methode wordt gebruikt om een tekenreekswaarde aan de cel toe te wijzen. U kunt deze tekenreeks wijzigen naar alles wat u wilt weergeven.
## Stap 8: Verkrijg de stijl van de cel
Nu er tekst in de cel staat, is het tijd om de stijl van de cel te wijzigen en de gewenste opmaak toe te passen, inclusief het doorhalen.
```csharp
// Het verkrijgen van de stijl van de cel
Style style = cell.GetStyle();
```
 De`GetStyle` Met deze methode wordt de huidige stijl van de cel opgehaald, zodat u eigenschappen zoals lettertype, grootte en effecten kunt wijzigen.
## Stap 9: Stel het Strikeout-effect in
Laten we het doorstreepeffect toepassen op de tekst in de cel. We zullen de lettertypestijl van de cel aanpassen.
```csharp
// ExStart:Stel doorhalen in
// Het doorhalen van het lettertype instellen
style.Font.IsStrikeout = true;
// ExEnd:SetDoorhalen
```
 Door het instellen`IsStrikeout` Als u de waarde true instelt, geeft u Excel opdracht om de tekst in de geselecteerde cel visueel door te strepen. Dit is vergelijkbaar met het visueel markeren van iets in een lijst.
## Stap 10: Pas de stijl toe op de cel
Nadat u de stijl hebt gewijzigd, moet u deze weer op de cel toepassen om de wijzigingen door te voeren.
```csharp
// De stijl op de cel toepassen
cell.SetStyle(style);
```
 De`SetStyle` Met de methode wordt de cel bijgewerkt met de nieuwe stijl, die nu ook de doorgehaalde opmaak bevat.
## Stap 11: Sla het Excel-bestand op
 Ten slotte is het tijd om uw werkmap op te slaan in de opgegeven directory. In dit voorbeeld slaan we het bestand op met de naam`book1.out.xls`.
```csharp
// Het Excel-bestand opslaan
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
 De`Save`methode schrijft de werkmap naar de schijf in de 97-2003 Excel-indeling. U kunt indien nodig verschillende indelingen opgeven.
## Conclusie
Het maken van een doorhalingseffect op tekst in Excel met Aspose.Cells voor .NET is een eenvoudig proces wanneer u het stap voor stap opsplitst. Door deze handleiding te volgen, beschikt u nu over de vaardigheden om uw spreadsheets te verbeteren met visuele aanwijzingen, waardoor uw gegevens niet alleen informatief maar ook visueel aantrekkelijk worden.
## Veelgestelde vragen
### Wat is Aspose.Cells?
Aspose.Cells is een krachtige bibliotheek voor het beheren van Excel-bestanden in .NET-toepassingen, waarmee u Excel-documenten programmatisch kunt maken, bewerken en converteren.
### Kan ik Aspose.Cells gratis gebruiken?
 Ja, u kunt het gratis gebruiken tijdens een proefperiode. Een gratis proefperiode is beschikbaar op[Aspose.Cells gratis proefperiode](https://releases.aspose.com/).
### Hoe kan ik Aspose.Cells kopen?
 U kunt een licentie voor Aspose.Cells kopen via hun website[Koop Aspose.Cells](https://purchase.aspose.com/buy).
### Zijn er voorbeelden beschikbaar voor het gebruik van Aspose.Cells?
 Ja, je kunt veel voorbeelden en codefragmenten vinden in de[Aspose.Cells-documentatie](https://reference.aspose.com/cells/net/).
### Waar kan ik ondersteuning krijgen voor Aspose.Cells?
 U kunt gemeenschapsondersteuning en hulp krijgen van de[Aspose-forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
