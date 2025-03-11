---
title: Positie Afbeelding (Absoluut) in Excel
linktitle: Positie Afbeelding (Absoluut) in Excel
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u afbeeldingen absoluut kunt positioneren in Excel met behulp van Aspose.Cells voor .NET met deze uitgebreide stapsgewijze zelfstudie.
weight: 13
url: /nl/net/excel-ole-picture-objects/position-picture-absolute-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Positie Afbeelding (Absoluut) in Excel

## Invoering
Heb je ooit moeite gehad met het correct positioneren van afbeeldingen in een Excel-spreadsheet? Je bent niet de enige! Veel gebruikers hebben hier last van, vooral wanneer hun datavisualisatiebehoeften absolute positionering vereisen voor een betere esthetiek of helderheid. Zoek niet verder; deze gids leidt je door het eenvoudige proces van het absoluut positioneren van afbeeldingen in een Excel-werkblad met behulp van Aspose.Cells voor .NET. Of je nu een ontwikkelaar bent die werkt aan Excel-manipulatie of een data-analist die je rapporten wil verbeteren, onze stapsgewijze tutorial is er om je Excel-ervaringen met afbeeldingen te vereenvoudigen!
## Vereisten
Voordat u zich verdiept in de code en de details, moet u een aantal dingen paraat hebben:
1.  Aspose.Cells-bibliotheek: zorg dat u de nieuwste versie van de Aspose.Cells voor .NET-bibliotheek hebt. U kunt deze downloaden van de[releases pagina](https://releases.aspose.com/cells/net/).
2. Development Environment: Zorg ervoor dat u een werkende .NET development environment hebt ingesteld. U kunt Visual Studio of een andere IDE naar keuze gebruiken.
3. Basiskennis van C#: Kennis van de programmeertaal C# is nuttig om de codefragmenten te begrijpen.
4. Afbeeldingsbestand: Sla een afbeeldingsbestand (bijvoorbeeld 'logo.jpg') op in de door u aangewezen documentmap en voeg dit bestand toe aan uw Excel-werkblad.

## Pakketten importeren
Om te beginnen, laten we ervoor zorgen dat we de benodigde pakketten voor ons project importeren. Uw projectbestand moet de volgende naamruimten bevatten:
```csharp
using System.IO;
using Aspose.Cells;
```
Door deze naamruimten te importeren, zorgen we ervoor dat ons programma de functies van Aspose.Cells kan benutten.
Laten we het voor de duidelijkheid opsplitsen in hanteerbare stappen.
## Stap 1: Stel uw documentenmap in
In deze eerste stap moet u de directory definiëren waar uw documenten zich bevinden. Dit is essentieel voor het programma om te weten waar bestanden moeten worden opgeslagen of opgehaald. Hier is hoe u dit kunt instellen:
```csharp
string dataDir = "Your Document Directory";
```
 Gewoon vervangen`"Your Document Directory"` met het werkelijke pad waar uw afbeeldingsbestand zich bevindt. Dit kan zoiets zijn als`"C:\\Users\\YourUsername\\Documents\\"`.
## Stap 2: Een werkmapobject instantiëren
 Vervolgens moet u een nieuw exemplaar van de`Workbook` klasse. Dit object vertegenwoordigt uw Excel-bestand:
```csharp
Workbook workbook = new Workbook();
```
U hebt nu een werkmap die u kunt vullen met gegevens en afbeeldingen.
## Stap 3: Een nieuw werkblad toevoegen
Nu u de werkmap hebt, moet u er een werkblad aan toevoegen. Dit is waar de magie van het toevoegen en positioneren van afbeeldingen plaatsvindt:
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
 Deze regel creëert een nieuw werkblad binnen uw werkmap en retourneert de index ervan, die we opslaan in de variabele`sheetIndex`.
## Stap 4: Het nieuwe werkblad verkrijgen
Laten we verwijzen naar het nieuw gecreëerde werkblad. Met behulp van de index die we net hebben gekregen, kunnen we het werkblad openen en manipuleren:
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
 Nu kunt u met de`worksheet` object om inhoud toe te voegen, inclusief afbeeldingen.
## Stap 5: Een afbeelding toevoegen
Nu het spannende gedeelte! Hier voegen we de afbeelding toe aan ons werkblad. We specificeren de rij- en kolomindices waar we de afbeelding willen verankeren (in dit geval in cel "F6", wat rij 5 en kolom 5 is):
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
Deze lijn vergrendelt de afbeelding effectief op de opgegeven locatie ten opzichte van het hele werkblad. Op dit moment is het echter nog steeds onderhevig aan het wijzigen van de grootte, samen met de cellen.
## Stap 6: Toegang krijgen tot de nieuw toegevoegde afbeelding
Om de afbeelding verder te bewerken, moet u de eigenschappen ervan openen:
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
Hiermee krijgt u toegang tot de eigenschappen van de afbeelding die we zojuist hebben toegevoegd!
## Stap 7: Absolute positionering voor de afbeelding instellen
 Om de afbeelding absoluut (in pixels) te positioneren, moet u de positie ervan definiëren met behulp van de`Left` En`Top` eigenschappen. Hier heb je controle over waar de afbeelding verschijnt:
```csharp
picture.Left = 60;
picture.Top = 10;
```
U kunt beide waarden naar wens aanpassen; ze geven respectievelijk de horizontale en verticale positionering van de afbeelding weer.
## Stap 8: Het Excel-bestand opslaan
Nadat u alle wijzigingen hebt aangebracht, is het tijd om de werkmap op te slaan:
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
 Hiermee wordt een Excel-bestand met de naam gemaakt`book1.out.xls` in uw eerder gedefinieerde documentmap, die uw werkblad bevat met de afbeelding er absoluut in geplaatst.

## Conclusie
En daar heb je het! Je hebt met succes een afbeelding in een Excel-sheet geplaatst met absolute positionering met behulp van Aspose.Cells voor .NET. Dit eenvoudige proces verbetert niet alleen de visuele presentatie van je Excel-documenten, maar zorgt er ook voor dat de afbeeldingen precies op de gewenste plek blijven staan, ongeacht eventuele wijzigingen in celgroottes en rijhoogtes. Nu kun je ervoor zorgen dat je afbeeldingen altijd perfect worden geplaatst, of je nu een rapport voorbereidt of een dashboard maakt.
## Veelgestelde vragen
### Wat is Aspose.Cells voor .NET?
Aspose.Cells voor .NET is een .NET-bibliotheek waarmee ontwikkelaars programmatisch Excel-spreadsheets kunnen maken, bewerken en converteren zonder dat ze Microsoft Excel nodig hebben.
### Kan ik andere beeldmanipulaties uitvoeren met Aspose.Cells?
Ja, met de Aspose.Cells-bibliotheek kunt u niet alleen afbeeldingen in Excel-spreadsheets positioneren, maar ook het formaat ervan wijzigen, ze roteren en aanpassen.
### Is Aspose.Cells gratis te gebruiken?
 Aspose.Cells is een commercieel product, maar u kunt beginnen met een gratis proefversie die beschikbaar is op hun website.[gratis proefpagina](https://releases.aspose.com/).
### Hoe verkrijg ik een tijdelijke licentie voor Aspose.Cells?
 U kunt een tijdelijke vergunning aanvragen via de[tijdelijke licentiepagina](https://purchase.aspose.com/temporary-license/) geleverd door Aspose.
### Waar kan ik meer voorbeelden en documentatie vinden?
 De[Aspose.Cells-documentatie](https://reference.aspose.com/cells/net/) bevat uitgebreide bronnen, waaronder codevoorbeelden en meer gedetailleerde functies.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
