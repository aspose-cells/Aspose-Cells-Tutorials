---
title: Positie Afbeelding (Proportioneel) in Excel
linktitle: Positie Afbeelding (Proportioneel) in Excel
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u afbeeldingen proportioneel kunt positioneren in Excel met Aspose.Cells voor .NET. Maak uw spreadsheets visueel aantrekkelijker.
weight: 14
url: /nl/net/excel-ole-picture-objects/position-picture-proportional-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Positie Afbeelding (Proportioneel) in Excel

## Invoering
Bent u die gepixelde afbeeldingen zat die nooit helemaal goed lijken te passen in uw Excel-spreadsheets? Stel u voor: u hebt een prachtig logo dat prominent in uw Excel-sheet moet worden weergegeven, maar het wordt geplet, uitgerekt of slecht geplaatst. Dat wil niemand! Nou, houd uw stoelen vast, want vandaag gaat u leren hoe u afbeeldingen proportioneel kunt positioneren in Excel met behulp van de Aspose.Cells-bibliotheek voor .NET. Deze krachtige bibliotheek maakt het een fluitje van een cent om Excel-bestanden te bewerken, of het nu gaat om rapportage, gegevensanalyse of gewoon om uw presentaties op te fleuren. Laten we dieper ingaan op het perfect uitlijnen van uw afbeeldingen!
## Vereisten
Voordat we beginnen met coderen, moet u een aantal zaken op uw computer hebben ingesteld:
1. Visual Studio: Zorg ervoor dat u Visual Studio hebt geïnstalleerd. Dit biedt een handige omgeving voor uw .NET-project.
2.  Aspose.Cells-bibliotheek: U hebt de Aspose.Cells-bibliotheek nodig. U kunt een gratis proefversie krijgen of deze kopen via de[Aspose-website](https://purchase.aspose.com/buy).
3. Basiskennis van C#: Een beetje kennis van C#-programmering is essentieel om de voorbeelden die we gaan bespreken, te begrijpen.
4. Een afbeeldingsbestand: Zorg dat u een afbeelding bij de hand hebt (bijvoorbeeld uw logo) die u in het Excel-bestand wilt invoegen.
Nu alles op zijn plaats staat, kunnen we beginnen met coderen!
## Pakketten importeren
Om Aspose.Cells in uw project te gebruiken, moet u de specifieke namespaces importeren. Dit is hoe u dat doet:
### Een nieuw project maken
Maak een nieuw project in Visual Studio:
- Open Visual Studio.
- Klik op 'Een nieuw project maken'.
- Kies 'Klassenbibliotheek (.NET Framework)' of 'Consoletoepassing', afhankelijk van uw voorkeur.
### Aspose.Cells installeren
U kunt het Aspose.Cells-pakket via NuGet aan uw project toevoegen. Dit doet u als volgt:
- Klik met de rechtermuisknop op uw project in de Solution Explorer.
- Selecteer 'NuGet-pakketten beheren'.
- Zoek naar "Aspose.Cells" en klik op "Installeren".
### Voeg richtlijnen toe
Voeg bovenaan uw codebestand de volgende richtlijnen toe:
```csharp
using System.IO;
using Aspose.Cells;
```
Met deze richtlijnen krijgt u toegang tot de klassen die u nodig hebt om uw Excel-bestanden te bewerken.
Laten we dit nu opsplitsen in gedetailleerde stappen om een afbeelding proportioneel te positioneren in Excel.
## Stap 1: Stel uw directory in
Zorg er allereerst voor dat u een aangewezen map voor uw documenten hebt. Zo maakt u een directory als deze nog niet bestaat:
```csharp
string dataDir = "Your Document Directory";
// Maak een map aan als deze nog niet bestaat.
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
 Dit fragment maakt een nieuwe map (als deze nog niet bestaat) om uw Excel-bestanden op te slaan. Vervang gewoon`"Your Document Directory"` met het daadwerkelijke pad waar u uw bestanden wilt opslaan.
## Stap 2: Een werkmap instantiëren
Laten we nu een nieuwe werkmap maken:
```csharp
Workbook workbook = new Workbook();
```
Met deze regel wordt een nieuw werkmapobject geïnitialiseerd, zodat u op een leeg canvas kunt werken.
## Stap 3: Een nieuw werkblad toevoegen
Nu we onze werkmap hebben ingesteld, kunnen we er een nieuw werkblad aan toevoegen:
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
Hiermee wordt een nieuw werkblad toegevoegd en wordt de index van dat werkblad geretourneerd. Deze index kunnen we later gebruiken om het werkblad te bewerken.
## Stap 4: Toegang tot het nieuwe werkblad
Om het nieuw toegevoegde werkblad te kunnen bewerken, moet u het als volgt openen:
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
 Nu,`worksheet` Hiermee kunnen we inhoud en afbeeldingen aan dat specifieke blad toevoegen.
## Stap 5: De afbeelding invoegen
Nu komt het spannende gedeelte! Laten we jouw mooie afbeelding toevoegen. Vervangen`"logo.jpg"` met de naam van uw afbeeldingsbestand:
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
 Deze regel voegt de afbeelding toe aan cel F6 (omdat rijen en kolommen een nulindex hebben,`5` verwijst naar de zesde cel).
## Stap 6: Toegang tot de toegevoegde afbeelding
Zodra de afbeelding is ingevoegd, kunt u deze als volgt openen:
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
Hiermee kunt u de eigenschappen van de afbeelding manipuleren.
## Stap 7: Plaats de afbeelding proportioneel
Laten we de afbeelding nu proportioneel positioneren:
```csharp
picture.UpperDeltaX = 200;
picture.UpperDeltaY = 200;
```
 Hier,`UpperDeltaX` En`UpperDeltaY` Pas de positie van de afbeelding aan ten opzichte van de afmetingen van de cel. U kunt deze waarden aanpassen om uw afbeelding precies goed te krijgen.
## Stap 8: Sla uw wijzigingen op
Sla ten slotte uw werkmap op om alle wijzigingen te behouden:
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
 Deze regel slaat uw werkmap op als`book1.out.xls` in de daarvoor bestemde directory.
## Conclusie
En daar heb je het! Je hebt zojuist geleerd hoe je afbeeldingen proportioneel kunt positioneren in Excel met Aspose.Cells voor .NET. Het gaat niet alleen om het invoegen van afbeeldingen; het gaat erom dat ze er perfect uitzien in je spreadsheets. Onthoud: een goed geplaatste afbeelding kan je datapresentatie aanzienlijk verbeteren.
Experimenteer met verschillende afbeeldingen en plaatsingen en aarzel niet om dieper in de rijke functies van Aspose.Cells te duiken. Uw Excel-sheets krijgen binnenkort een serieuze make-over!
## Veelgestelde vragen
### Wat is Aspose.Cells?
Aspose.Cells is een krachtige bibliotheek voor .NET waarmee gebruikers Excel-bestanden kunnen maken, bewerken en converteren zonder dat Microsoft Excel geïnstalleerd hoeft te zijn.
### Kan ik Aspose.Cells gratis gebruiken?
 Ja, Aspose.Cells biedt een gratis proefversie aan, die u kunt downloaden[hier](https://releases.aspose.com/).
### Waar kan ik de documentatie vinden?
 U kunt toegang krijgen tot de uitgebreide[documentatie](https://reference.aspose.com/cells/net/) voor Aspose.Cells.
### Ondersteunt Aspose.Cells alle afbeeldingsformaten?
Aspose.Cells ondersteunt verschillende formaten, waaronder JPEG, PNG, BMP, GIF en TIFF.
### Hoe kan ik ondersteuning krijgen voor Aspose.Cells?
 Voor vragen kunt u gerust een bezoek brengen aan de[ondersteuningsforum](https://forum.aspose.com/c/cells/9)waar u uw vragen kunt stellen.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
