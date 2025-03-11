---
title: Keuzelijst met invoervak toevoegen aan werkblad in Excel
linktitle: Keuzelijst met invoervak toevoegen aan werkblad in Excel
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u een keuzelijst met invoervak programmatisch toevoegt aan een Excel-werkblad met Aspose.Cells voor .NET. Deze stapsgewijze handleiding leidt u door elk detail.
weight: 21
url: /nl/net/excel-shapes-controls/add-combo-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Keuzelijst met invoervak toevoegen aan werkblad in Excel

## Invoering
Het maken van interactieve Excel-spreadsheets kan de gebruikerservaring aanzienlijk verbeteren, vooral wanneer u formulierelementen zoals keuzelijsten toevoegt. Keuzelijsten stellen gebruikers in staat om opties te selecteren uit een vooraf gedefinieerde lijst, wat de invoer van gegevens eenvoudiger en efficiënter maakt. Met Aspose.Cells voor .NET kunt u programmatisch keuzelijsten maken in Excel-sheets zonder Excel rechtstreeks te gebruiken. Deze krachtige bibliotheek stelt ontwikkelaars in staat om Excel-bestanden op verschillende manieren te manipuleren, waaronder de mogelijkheid om formulierbesturingselementen te automatiseren.
In deze tutorial leiden we u door het proces van het toevoegen van een keuzelijst aan een werkblad in Excel met behulp van Aspose.Cells voor .NET. Als u dynamische, gebruiksvriendelijke spreadsheets wilt bouwen, helpt deze gids u op weg.
## Vereisten
Voordat we in de code duiken, controleren we of je alles hebt wat je nodig hebt:
- Aspose.Cells voor .NET: Download en installeer de Aspose.Cells voor .NET-bibliotheek van de[downloadpagina](https://releases.aspose.com/cells/net/).
- .NET Framework: Zorg ervoor dat u .NET Framework op uw machine hebt geïnstalleerd. Elke versie die door Aspose.Cells wordt ondersteund, werkt.
- Ontwikkelomgeving: Gebruik een IDE zoals Visual Studio om uw project te beheren en code te schrijven.
-  Aspose-licentie: U kunt in de evaluatiemodus zonder licentie werken, maar voor een volledige versie moet u een licentie aanvragen. Verkrijg een[tijdelijke licentie](https://purchase.aspose.com/temporary-license/) indien nodig.
## Pakketten importeren
Om te beginnen moet u de vereiste namespaces importeren in uw project. Dit is wat u nodig hebt:
```csharp
using System.IO;
using Aspose.Cells;
```
Deze zijn essentieel voor de interactie met Excel-bestanden en het bewerken van formulierelementen, zoals keuzelijsten met invoervakken, in de werkmap.
Laten we het proces voor het toevoegen van een keuzelijst opsplitsen in een aantal eenvoudige stappen, zodat u het gemakkelijk kunt begrijpen.
## Stap 1: De documentenmap instellen
De eerste stap is het maken van een directory waar uw Excel-bestanden worden opgeslagen. U kunt een nieuwe folder maken als deze nog niet bestaat.
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
// Maak een map aan als deze nog niet bestaat.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: Geeft de locatie op waar het uitvoerbestand wordt opgeslagen.
- System.IO.Directory.Exists: controleert of de directory al bestaat.
- System.IO.Directory.CreateDirectory: Maakt de directory aan als deze ontbreekt.
## Stap 2: Maak een nieuwe werkmap
Maak nu een nieuwe Excel-werkmap waaraan u de keuzelijst met invoervak wilt toevoegen.

```csharp
// Maak een nieuwe werkmap.
Workbook workbook = new Workbook();
```

- Werkmap werkmap: Initialiseert een nieuw exemplaar van de klasse Werkmap, dat een Excel-bestand vertegenwoordigt.
## Stap 3: Haal het werkblad en de cellen op
Open vervolgens het eerste werkblad in de werkmap en haal de cellenverzameling op waarin u de gegevens wilt invoeren.

```csharp
// Pak het eerste werkblad.
Worksheet sheet = workbook.Worksheets[0];
// Haal de cellenverzameling van het werkblad op.
Cells cells = sheet.Cells;
```

- Werkblad: Haalt het eerste werkblad uit de werkmap.
- Cellen cellen: Haalt de verzameling cellen uit het werkblad op.
## Stap 4: Invoerwaarden voor keuzelijst
Nu moeten we een aantal waarden in de cellen invoeren. Deze waarden dienen als opties voor de combobox.

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

- cellen["B3"].PutValue: Plaatst het label "Werknemer" in cel B3.
- Font.IsBold = true: Hiermee maakt u de tekst vetgedrukt, zodat deze beter opvalt.
- Invoerbereik: Voert meerdere werknemers-ID's in cellen A2 tot en met A7 in. Deze worden weergegeven in de vervolgkeuzelijst met keuzelijsten.
## Stap 5: Voeg de keuzelijst toe aan het werkblad
De volgende stap is om de combo box control toe te voegen aan uw werkblad. Deze combo box laat gebruikers een van de werknemers-ID's kiezen die u eerder hebt ingevoerd.

```csharp
// Voeg een nieuwe keuzelijst toe.
Aspose.Cells.Drawing.ComboBox comboBox = sheet.Shapes.AddComboBox(2, 0, 2, 0, 22, 100);
```

- AddComboBox: Voegt een nieuwe combobox toe aan het werkblad. De getallen (2, 0, 2, 0, 22, 100) geven de positie en afmetingen van de combobox weer.
## Stap 6: Koppel de keuzelijst aan een cel en stel het invoerbereik in
Om de keuzelijst functioneel te maken, moeten we deze koppelen aan een specifieke cel en het bereik van cellen definiëren waaruit de opties worden gehaald.

```csharp
// Stel de gekoppelde cel in.
comboBox.LinkedCell = "A1";
// Stel het invoerbereik in.
comboBox.InputRange = "A2:A7";
```

- LinkedCell: Koppelt de selectie van de keuzelijst met invoervak aan cel A1. De geselecteerde waarde uit de keuzelijst met invoervak wordt in deze cel weergegeven.
- InputRange: Definieert het celbereik (A2:A7) dat de waarden bevat die in de keuzelijstopties worden ingevuld.
## Stap 7: Pas het uiterlijk van de keuzelijst aan
U kunt de keuzelijst verder aanpassen door het aantal vervolgkeuzemenu's op te geven en 3D-schaduw in te schakelen voor een mooier uiterlijk.

```csharp
// Stel het aantal regels in dat in het lijstgedeelte van de keuzelijst wordt weergegeven.
comboBox.DropDownLines = 5;
// Stel de keuzelijst in met 3D-arcering.
comboBox.Shadow = true;
```

- DropDownLines: Hiermee bepaalt u hoeveel opties er tegelijk zichtbaar zijn in de vervolgkeuzelijst.
- Schaduw: Voegt een 3D-schaduweffect toe aan de keuzelijst.
## Stap 8: Kolommen automatisch aanpassen en de werkmap opslaan
Ten slotte passen we de kolommen automatisch aan voor een overzichtelijke lay-out en slaan we de werkmap op.

```csharp
// AutoFit-kolommen
sheet.AutoFitColumns();
// Slaat het bestand op.
workbook.Save(dataDir + "book1.out.xls");
```

- AutoFitColumns: Past automatisch de kolombreedtes aan zodat deze bij de inhoud passen.
- Opslaan: Hiermee slaat u de werkmap op als een Excel-bestand in de opgegeven map.

## Conclusie
Het toevoegen van een keuzelijst met invoervak aan uw Excel-werkbladen met Aspose.Cells voor .NET is een eenvoudig proces dat de flexibiliteit van de gegevensinvoer aanzienlijk verbetert. Door programmatisch formulierbesturingselementen te maken, kunt u eenvoudig interactieve spreadsheets maken. Deze tutorial liet u zien hoe u een keuzelijst met invoervak toevoegt, deze koppelt aan een cel en het invoerbereik configureert, allemaal met Aspose.Cells.
 Aspose.Cells biedt een breed scala aan functies voor Excel-bestandsmanipulatie, waardoor het een ideale keuze is voor ontwikkelaars die spreadsheettaken willen automatiseren. Probeer het uit met een[gratis proefperiode](https://releases.aspose.com/).
## Veelgestelde vragen
### Kan ik Aspose.Cells gebruiken zonder dat Excel is geïnstalleerd?
Ja, Aspose.Cells werkt onafhankelijk van Excel en vereist geen installatie van Excel.
### Hoe pas ik een licentie toe in Aspose.Cells?
 U kunt een licentie aanvragen door deze te verkrijgen bij[hier](https://purchase.aspose.com/buy) en roepen`License.SetLicense()` in uw code.
### Welke formaten ondersteunt Aspose.Cells voor het opslaan van bestanden?
Aspose.Cells ondersteunt het opslaan van bestanden in verschillende formaten, zoals XLSX, XLS, CSV, PDF en meer.
### Is er een limiet aan het aantal keuzelijsten dat ik kan toevoegen?
Nee, er is geen strikte limiet. U kunt zoveel keuzelijsten toevoegen als nodig is voor uw project.
### Hoe krijg ik ondersteuning voor Aspose.Cells?
 U kunt ondersteuning krijgen van de[Aspose-forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
