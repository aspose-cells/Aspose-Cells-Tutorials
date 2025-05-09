---
"description": "Leer hoe u bewerkbare bereiken in Excel-werkbladen kunt maken met Aspose.Cells voor .NET. Zo kunt u specifieke cellen bewerken en de rest beveiligen met werkbladbeveiliging."
"linktitle": "Gebruikers toestaan bereiken in werkbladen te bewerken met Aspose.Cells"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Gebruikers toestaan bereiken in werkbladen te bewerken met Aspose.Cells"
"url": "/nl/net/worksheet-security/allow-edit-ranges/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Gebruikers toestaan bereiken in werkbladen te bewerken met Aspose.Cells

## Invoering
Excel-documenten bevatten vaak gevoelige gegevens of gestructureerde inhoud die u wilt beschermen tegen ongewenste bewerkingen. Het kan echter zijn dat u specifieke cellen of bereiken bewerkbaar wilt maken voor bepaalde gebruikers. Daar komt Aspose.Cells voor .NET om de hoek kijken: een krachtige tool waarmee u een volledig werkblad kunt beveiligen en toch bewerkingsrechten kunt verlenen aan bepaalde bereiken. Stelt u zich eens voor dat u een budgetspreadsheet deelt waarin alleen bepaalde cellen bewerkbaar zijn en andere veilig blijven: Aspose.Cells maakt dit eenvoudig en efficiënt.
## Vereisten
Voordat we met coderen beginnen, controleren we eerst of je alles hebt wat je nodig hebt:
- Aspose.Cells voor .NET: Zorg ervoor dat je de Aspose.Cells voor .NET-bibliotheek hebt geïnstalleerd. Je kunt deze downloaden. [hier](https://releases.aspose.com/cells/net/).
- Ontwikkelomgeving: Visual Studio of een C#-compatibele IDE.
- .NET Framework: versie 4.0 of later.
- Licentie: Overweeg een licentie aan te vragen om beperkingen tijdens de proefperiode te vermijden. U kunt een [tijdelijke licentie hier](https://purchase.aspose.com/temporary-license/).
## Pakketten importeren
Zorg ervoor dat u de benodigde Aspose.Cells-naamruimte aan het begin van uw code opneemt:
```csharp
using System.IO;
using Aspose.Cells;
```
Hiermee weet u zeker dat u toegang hebt tot alle klassen en methoden die nodig zijn om beveiligde bereiken in Excel-bestanden in te stellen.
Nu de basis is gelegd, gaan we de code stap voor stap gedetailleerd doornemen.
## Stap 1: De directory instellen
Voordat u met bestanden aan de slag gaat, moet u de map instellen waar u het Excel-bestand wilt opslaan. Zo weet u zeker dat uw bestanden goed georganiseerd en veilig opgeslagen zijn.
```csharp
// Definieer het pad naar uw documentenmap
string dataDir = "Your Document Directory";
// Controleer of de directory bestaat, indien niet, maak deze dan aan
bool isExists = Directory.Exists(dataDir);
if (!isExists)
{
    Directory.CreateDirectory(dataDir);
}
```
Dit deel van de code zorgt ervoor dat je directory klaar is voor bestandsbewerkingen. Zie het als de basis voor alles wat volgt.
## Stap 2: Initialiseer de werkmap en het werkblad
Laten we nu verdergaan door een nieuwe werkmap te maken en het standaardwerkblad te openen.
```csharp
// Een nieuwe werkmap initialiseren
Workbook book = new Workbook();
// Toegang tot het eerste werkblad in de werkmap
Worksheet sheet = book.Worksheets[0];
```
Hier initialiseren we een Excel-werkmap en selecteren we het eerste werkblad erin. Dit werkblad is het canvas waarop we onze beveiligingsinstellingen toepassen en bewerkbare bereiken definiëren.
## Stap 3: Toegang tot de verzameling 'Bewerkingsbereiken toestaan'
Aspose.Cells heeft een functie genaamd `AllowEditRanges`, een verzameling bereiken die u kunt bewerken, zelfs als het werkblad is beveiligd.
```csharp
// Toegang tot de verzameling 'Bewerkingsbereiken toestaan'
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```
Deze regel geeft toegang tot een speciale verzameling bereiken die u kunt bewerken. Zie het als een 'VIP'-gebied in uw werkblad, waar alleen specifieke bereiken de beveiliging mogen omzeilen.
## Stap 4: Definieer en creëer een beschermd bereik
Laten we nu een beveiligd bereik definiëren en aanmaken in ons werkblad. We specificeren de begin- en eindcellen voor dit bereik.
```csharp
// Definieer een ProtectedRange-variabele
ProtectedRange protectedRange;
// Voeg een nieuw bereik toe aan de verzameling met een specifieke naam en celposities
int idx = allowRanges.Add("EditableRange", 1, 1, 3, 3);
protectedRange = allowRanges[idx];
```
In dit codeblok:
- `EditableRange` is de naam die aan het bereik is toegewezen.
- De getallen (1, 1, 3, 3) definiëren de coördinaten van het bereik, wat betekent dat het bereik begint bij cel B2 (rij 1, kolom 1) en eindigt bij cel D4 (rij 3, kolom 3).
## Stap 5: Stel een wachtwoord in voor het beveiligde bereik
Voor extra beveiliging kunt u een wachtwoord instellen voor het beveiligde bereik. Deze stap voegt een extra beveiligingslaag toe om ervoor te zorgen dat alleen geautoriseerde gebruikers het bereik kunnen bewerken.
```csharp
// Stel een wachtwoord in voor het bewerkbare bereik
protectedRange.Password = "123";
```
Hier hebben we een wachtwoord toegevoegd (`"123"`) naar het beschermde bereik. Deze wachtwoordvereiste biedt extra controle over wie wijzigingen kan aanbrengen.
## Stap 6: Bescherm het werkblad
Nu het bewerkbare bereik is ingesteld, is de volgende stap het beveiligen van het hele werkblad. Deze beveiligingsinstelling zorgt ervoor dat alle cellen buiten het gedefinieerde bereik vergrendeld en niet-bewerkbaar zijn.
```csharp
// Bescherming toepassen op het werkblad, waardoor alle andere cellen niet meer te bewerken zijn
sheet.Protect(ProtectionType.All);
```
De `Protect` De methode vergrendelt het hele werkblad, met uitzondering van de bereiken die we als bewerkbaar hebben gedefinieerd. Deze stap creëert in feite een veilige 'alleen-lezen'-omgeving, met toegang tot specifieke cellen indien nodig.
## Stap 7: Sla de werkmap op
De laatste stap is het opslaan van de werkmap, zodat uw instellingen worden toegepast en opgeslagen.
```csharp
// Sla het Excel-bestand op in de opgegeven directory
book.Save(dataDir + "protectedrange.out.xls");
```
In deze stap slaan we onze werkmap op als "protectedrange.out.xls" in de map die we in stap 1 hebben aangemaakt. Nu heb je een volledig functioneel, beveiligd Excel-bestand waarin alleen specifieke bereiken kunnen worden bewerkt!
## Conclusie
Aspose.Cells voor .NET biedt een uitstekende manier om de beveiliging en machtigingen binnen uw Excel-bestanden te beheren. Door bewerkbare bereiken te creëren, kunt u uw werkbladen beveiligen en toch specifieke gedeelten toegankelijk houden. Deze functionaliteit is vooral handig voor documenten waaraan wordt samengewerkt, waarbij slechts enkele cellen open moeten staan voor bewerking en andere vergrendeld moeten blijven.
## Veelgestelde vragen
### Kan ik meerdere bewerkbare bereiken aan een werkblad toevoegen?
Ja, u kunt meerdere bereiken toevoegen door simpelweg de `allowRanges.Add()` methode voor elk nieuw bereik.
### Wat als ik een beschermd bereik later wil verwijderen?
Gebruik de `allowRanges.RemoveAt()` met de index van het bereik dat u wilt verwijderen.
### Kan ik voor elk bereik een ander wachtwoord instellen?
Absoluut. Elk `ProtectedRange` kan een eigen uniek wachtwoord hebben, waardoor u nauwkeurige controle heeft.
### Wat gebeurt er als ik het werkblad beveilig zonder bewerkbare bereiken?
Als u geen bewerkbare bereiken definieert, is het hele werkblad niet bewerkbaar nadat het is beveiligd.
### Is het beschermde bereik zichtbaar voor andere gebruikers?
Nee, de beveiliging is intern. Gebruikers worden alleen om een wachtwoord gevraagd als ze het beveiligde gebied proberen te bewerken.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}