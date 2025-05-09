---
"description": "Leer hoe je programmatisch een keuzelijst met invoervak aan een Excel-werkblad toevoegt met Aspose.Cells voor .NET. Deze stapsgewijze handleiding leidt je door elk detail."
"linktitle": "Keuzelijst met invoervak toevoegen aan werkblad in Excel"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Keuzelijst met invoervak toevoegen aan werkblad in Excel"
"url": "/nl/net/excel-shapes-controls/add-combo-box-to-worksheet-excel/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Keuzelijst met invoervak toevoegen aan werkblad in Excel

## Invoering
Het maken van interactieve Excel-spreadsheets kan de gebruikerservaring aanzienlijk verbeteren, vooral wanneer u formulierelementen zoals keuzelijsten met invoervakken toevoegt. Met keuzelijsten met invoervakken kunnen gebruikers opties selecteren uit een vooraf gedefinieerde lijst, wat de gegevensinvoer eenvoudiger en efficiënter maakt. Met Aspose.Cells voor .NET kunt u programmatisch keuzelijsten met invoervakken in Excel-sheets maken zonder Excel rechtstreeks te gebruiken. Deze krachtige bibliotheek stelt ontwikkelaars in staat om Excel-bestanden op verschillende manieren te bewerken, waaronder de mogelijkheid om formulierbesturingselementen te automatiseren.
In deze tutorial laten we je zien hoe je een keuzelijst met invoervak toevoegt aan een werkblad in Excel met behulp van Aspose.Cells voor .NET. Als je dynamische, gebruiksvriendelijke spreadsheets wilt bouwen, helpt deze handleiding je op weg.
## Vereisten
Voordat we in de code duiken, controleren we of je alles hebt wat je nodig hebt:
- Aspose.Cells voor .NET: Download en installeer de Aspose.Cells voor .NET-bibliotheek van de [downloadpagina](https://releases.aspose.com/cells/net/).
- .NET Framework: Zorg ervoor dat .NET Framework op uw computer is geïnstalleerd. Elke versie die door Aspose.Cells wordt ondersteund, werkt.
- Ontwikkelomgeving: Gebruik een IDE zoals Visual Studio om uw project te beheren en code te schrijven.
- Aspose-licentie: U kunt zonder licentie werken in de evaluatiemodus, maar voor een volledige versie moet u een licentie aanvragen. [tijdelijke licentie](https://purchase.aspose.com/temporary-license/) indien nodig.
## Pakketten importeren
Om te beginnen moet je de vereiste naamruimten in je project importeren. Dit heb je nodig:
```csharp
using System.IO;
using Aspose.Cells;
```
Deze zijn essentieel voor de interactie met Excel-bestanden en het bewerken van formulierelementen, zoals keuzelijsten met invoervakken, in de werkmap.
Laten we het proces voor het toevoegen van een keuzelijst opsplitsen in meerdere eenvoudige stappen, zodat het gemakkelijk te begrijpen is.
## Stap 1: De documentenmap instellen
De eerste stap is het aanmaken van een map waarin uw Excel-bestanden worden opgeslagen. U kunt een nieuwe map aanmaken als deze nog niet bestaat.
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
// Maak een map aan als deze nog niet bestaat.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: Geeft de locatie aan waar het uitvoerbestand wordt opgeslagen.
- System.IO.Directory.Exists: controleert of de directory al bestaat.
- System.IO.Directory.CreateDirectory: Maakt de directory aan als deze ontbreekt.
## Stap 2: Een nieuwe werkmap maken
Maak nu een nieuwe Excel-werkmap waaraan u de keuzelijst gaat toevoegen.

```csharp
// Maak een nieuwe werkmap.
Workbook workbook = new Workbook();
```

- Werkmap werkmap: Initialiseert een nieuw exemplaar van de klasse Workbook, dat een Excel-bestand vertegenwoordigt.
## Stap 3: Het werkblad en de cellen ophalen
Open vervolgens het eerste werkblad vanuit de werkmap en haal de cellenverzameling op waarin u de gegevens wilt invoeren.

```csharp
// Pak het eerste werkblad.
Worksheet sheet = workbook.Worksheets[0];
// Haal de cellenverzameling van het werkblad op.
Cells cells = sheet.Cells;
```

- Werkblad: Haalt het eerste werkblad op uit de werkmap.
- Cellen cellen: Haalt de verzameling cellen op uit het werkblad.
## Stap 4: Invoerwaarden voor keuzelijst
Nu moeten we een aantal waarden in de cellen invoeren. Deze waarden dienen als opties voor de keuzelijst.

```csharp
// Voer een waarde in.
cells["B3"].PutValue("Employee:");
// Maak het vetgedrukt.
cells["B3"].GetStyle().Font.IsBold = true;
// Voer enkele waarden in die het invoerbereik voor de keuzelijst aangeven.
cells["A2"].PutValue("Emp001");
cells["A3"].PutValue("Emp002");
cells["A4"].PutValue("Emp003");
cells["A5"].PutValue("Emp004");
cells["A6"].PutValue("Emp005");
cells["A7"].PutValue("Emp006");
```

- cells["B3"].PutValue: Plaatst het label "Werknemer" in cel B3.
- Font.IsBold = true: Hiermee maakt u de tekst vetgedrukt, zodat deze beter opvalt.
- Invoerbereik: Voert meerdere medewerkers-ID's in cellen A2 tot en met A7 in. Deze verschijnen in de vervolgkeuzelijst met invoervak.
## Stap 5: Voeg de keuzelijst toe aan het werkblad
De volgende stap is het toevoegen van de keuzelijst met invoervak aan uw werkblad. Met deze keuzelijst kunnen gebruikers een van de eerder ingevoerde medewerkers-ID's kiezen.

```csharp
// Voeg een nieuwe keuzelijst toe.
Aspose.Cells.Drawing.ComboBox comboBox = sheet.Shapes.AddComboBox(2, 0, 2, 0, 22, 100);
```

- AddComboBox: Voegt een nieuwe keuzelijst met invoervak toe aan het werkblad. De getallen (2, 0, 2, 0, 22, 100) geven de positie en afmetingen van de keuzelijst met invoervak aan.
## Stap 6: Koppel de keuzelijst aan een cel en stel het invoerbereik in
Om de keuzelijst functioneel te maken, moeten we deze koppelen aan een specifieke cel en het bereik van cellen definiëren waaruit de opties worden gehaald.

```csharp
// Stel de gekoppelde cel in.
comboBox.LinkedCell = "A1";
// Stel het invoerbereik in.
comboBox.InputRange = "A2:A7";
```

- LinkedCell: koppelt de selectie van de keuzelijst aan cel A1. De geselecteerde waarde uit de keuzelijst verschijnt in deze cel.
- InputRange: Definieert het celbereik (A2:A7) dat de waarden bevat die in de keuzelijstopties worden ingevuld.
## Stap 7: Pas het uiterlijk van de keuzelijst aan
U kunt de keuzelijst verder aanpassen door het aantal vervolgkeuzemenu's op te geven en 3D-schaduw in te schakelen voor een mooier uiterlijk.

```csharp
// Stel het aantal lijstregels in dat in het lijstgedeelte van de keuzelijst wordt weergegeven.
comboBox.DropDownLines = 5;
// Stel de keuzelijst in met 3D-arcering.
comboBox.Shadow = true;
```

- DropDownLines: Hiermee bepaalt u hoeveel opties er tegelijk zichtbaar zijn in de vervolgkeuzelijst.
- Schaduw: voegt een 3D-schaduweffect toe aan de keuzelijst.
## Stap 8: Kolommen automatisch aanpassen en de werkmap opslaan
Ten slotte passen we de kolommen automatisch aan voor een overzichtelijke lay-out en slaan we de werkmap op.

```csharp
// Kolommen automatisch aanpassen
sheet.AutoFitColumns();
// Slaat het bestand op.
workbook.Save(dataDir + "book1.out.xls");
```

- AutoFitColumns: past de kolombreedtes automatisch aan de inhoud aan.
- Opslaan: slaat de werkmap op als een Excel-bestand in de opgegeven map.

## Conclusie
Het toevoegen van een keuzelijst met invoervak aan uw Excel-werkbladen met Aspose.Cells voor .NET is een eenvoudig proces dat de flexibiliteit van de gegevensinvoer aanzienlijk verbetert. Door programmatisch formulierbesturingselementen te maken, kunt u eenvoudig interactieve spreadsheets bouwen. Deze tutorial heeft u laten zien hoe u een keuzelijst met invoervak toevoegt, deze aan een cel koppelt en het invoerbereik configureert, allemaal met Aspose.Cells.
Aspose.Cells biedt een breed scala aan functies voor het bewerken van Excel-bestanden, waardoor het een ideale keuze is voor ontwikkelaars die spreadsheettaken willen automatiseren. Probeer het uit met een [gratis proefperiode](https://releases.aspose.com/).
## Veelgestelde vragen
### Kan ik Aspose.Cells gebruiken zonder dat Excel is geïnstalleerd?
Ja, Aspose.Cells werkt onafhankelijk van Excel en vereist niet dat Excel geïnstalleerd is.
### Hoe pas ik een licentie toe in Aspose.Cells?
kunt een licentie aanvragen door deze te verkrijgen bij [hier](https://purchase.aspose.com/buy) en roepen `License.SetLicense()` in je code.
### Welke formaten ondersteunt Aspose.Cells voor het opslaan van bestanden?
Aspose.Cells ondersteunt het opslaan van bestanden in verschillende formaten, zoals XLSX, XLS, CSV, PDF en meer.
### Zit er een limiet aan het aantal keuzelijsten dat ik kan toevoegen?
Nee, er is geen strikte limiet. U kunt zoveel keuzelijsten toevoegen als nodig is voor uw project.
### Hoe krijg ik ondersteuning voor Aspose.Cells?
U kunt ondersteuning krijgen van de [Aspose-forum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}