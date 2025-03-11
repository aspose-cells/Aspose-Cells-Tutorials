---
title: Gebruikers toestaan om bereiken in werkbladen te bewerken met behulp van Aspose.Cells
linktitle: Gebruikers toestaan om bereiken in werkbladen te bewerken met behulp van Aspose.Cells
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u bewerkbare bereiken in Excel-werkbladen kunt maken met Aspose.Cells voor .NET. Zo kunt u specifieke cellen bewerken en de rest beveiligen met werkbladbeveiliging.
weight: 10
url: /nl/net/worksheet-security/allow-edit-ranges/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gebruikers toestaan om bereiken in werkbladen te bewerken met behulp van Aspose.Cells

## Invoering
Excel-documenten bevatten vaak gevoelige gegevens of gestructureerde inhoud die u wilt beschermen tegen ongewenste bewerkingen. Er zijn echter mogelijk specifieke cellen of bereiken die u bewerkbaar wilt maken voor bepaalde gebruikers. Dat is waar Aspose.Cells voor .NET in beeld komt als een krachtige tool waarmee u een heel werkblad kunt beschermen en toch bewerkingsmachtigingen kunt verlenen aan aangewezen bereiken. Stel u voor dat u een budgetspreadsheet deelt waarin alleen bepaalde cellen bewerkbaar zijn en andere veilig blijven: Aspose.Cells maakt dit eenvoudig en efficiënt.
## Vereisten
Voordat we met coderen beginnen, willen we eerst controleren of je alles hebt wat je nodig hebt:
-  Aspose.Cells voor .NET: Zorg ervoor dat u de Aspose.Cells voor .NET-bibliotheek hebt geïnstalleerd. U kunt deze downloaden[hier](https://releases.aspose.com/cells/net/).
- Ontwikkelomgeving: Visual Studio of een andere C#-compatibele IDE.
- .NET Framework: versie 4.0 of hoger.
- Licentie: Overweeg een licentie aan te schaffen om beperkingen van de proefperiode te vermijden. U kunt een[tijdelijke licentie hier](https://purchase.aspose.com/temporary-license/).
## Pakketten importeren
Zorg ervoor dat u de benodigde Aspose.Cells-naamruimte aan het begin van uw code opneemt:
```csharp
using System.IO;
using Aspose.Cells;
```
Hiermee weet u zeker dat u toegang hebt tot alle klassen en methoden die nodig zijn om beveiligde bereiken in Excel-bestanden in te stellen.
Nu de basis is gelegd, gaan we de code stap voor stap in detail doornemen.
## Stap 1: De directory instellen
Voordat u met bestanden gaat werken, moet u de directory instellen waar u het Excel-bestand wilt opslaan. Dit zorgt ervoor dat uw bestanden goed georganiseerd en veilig opgeslagen zijn.
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
Dit deel van de code zorgt ervoor dat uw directory klaar is voor bestandsbewerkingen. Zie het als het leggen van de basis voor alles wat volgt.
## Stap 2: Initialiseer de werkmap en het werkblad
Laten we nu een nieuwe werkmap maken en het standaardwerkblad openen.
```csharp
// Een nieuwe werkmap initialiseren
Workbook book = new Workbook();
// Toegang tot het eerste werkblad in de werkmap
Worksheet sheet = book.Worksheets[0];
```
Hier initialiseren we een Excel-werkmap en selecteren we het eerste werkblad erin. Dit werkblad is het canvas waarop we onze beveiligingsinstellingen toepassen en bewerkbare bereiken definiëren.
## Stap 3: Toegang tot de verzameling Bereiken bewerken toestaan
 Aspose.Cells heeft een functie genaamd`AllowEditRanges`, een verzameling bereiken die u kunt bewerken, zelfs als het werkblad is beveiligd.
```csharp
// Toegang tot de collectie Bereiken bewerken toestaan
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```
Deze regel stelt toegang in tot een speciale verzameling bereiken die bewerkbaar zijn. Zie het als een "VIP"-gebied in uw werkblad, waar alleen specifieke bereiken de beveiliging mogen omzeilen.
## Stap 4: Definieer en creëer een beschermd bereik
Laten we nu een beschermd bereik definiëren en maken in ons werkblad. We specificeren de begin- en eindcellen voor dit bereik.
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
Voor extra beveiliging kunt u een wachtwoord instellen voor het beschermde bereik. Deze stap voegt een extra beschermingslaag toe om ervoor te zorgen dat alleen geautoriseerde gebruikers het bereik kunnen bewerken.
```csharp
// Stel een wachtwoord in voor het bewerkbare bereik
protectedRange.Password = "123";
```
Hier hebben we een wachtwoord toegevoegd (`"123"`) naar het beschermde bereik. Deze wachtwoordvereiste biedt een extra niveau van controle over wie wijzigingen kan aanbrengen.
## Stap 6: Bescherm het werkblad
Nu ons bewerkbare bereik is vastgesteld, is de volgende stap het beschermen van het hele werkblad. Deze beschermingsinstelling zorgt ervoor dat alle cellen buiten het gedefinieerde bereik worden vergrendeld en niet-bewerkbaar zijn.
```csharp
// Bescherming toepassen op het werkblad, waardoor alle andere cellen niet meer bewerkbaar zijn
sheet.Protect(ProtectionType.All);
```
 De`Protect`methode vergrendelt het hele werkblad, behalve de bereiken die we als bewerkbaar hebben gedefinieerd. Deze stap creëert in feite een veilige 'alleen-lezen'-omgeving, met toegang tot specifieke cellen indien nodig.
## Stap 7: Sla de werkmap op
De laatste stap is het opslaan van de werkmap, zodat uw instellingen worden toegepast en opgeslagen.
```csharp
// Sla het Excel-bestand op in de opgegeven directory
book.Save(dataDir + "protectedrange.out.xls");
```
In deze stap slaan we onze werkmap op als "protectedrange.out.xls" in de map die we in stap 1 hebben ingesteld. Nu hebt u een volledig functioneel, beveiligd Excel-bestand waarin alleen specifieke bereiken bewerkbaar zijn!
## Conclusie
Aspose.Cells voor .NET biedt een uitstekende manier om beveiliging en machtigingen binnen uw Excel-bestanden te beheren. Door bewerkbare bereiken te maken, kunt u uw werkbladen beveiligen en toch specifieke gebieden toegankelijk houden. Deze functionaliteit is vooral handig voor collaboratieve documenten, waarbij slechts een paar cellen open moeten zijn voor bewerking, terwijl andere vergrendeld blijven.
## Veelgestelde vragen
### Kan ik meerdere bewerkbare bereiken aan een werkblad toevoegen?
Ja, u kunt meerdere bereiken toevoegen door simpelweg de`allowRanges.Add()` methode voor elk nieuw bereik.
### Wat als ik een beschermd bereik later wil verwijderen?
 Gebruik de`allowRanges.RemoveAt()` methode met de index van het bereik dat u wilt verwijderen.
### Kan ik voor elk bereik een ander wachtwoord instellen?
 Absoluut. Elk`ProtectedRange` kan een eigen uniek wachtwoord hebben, waardoor u nauwkeurige controle hebt.
### Wat gebeurt er als ik het werkblad beveilig zonder bewerkbare bereiken?
Als u geen bewerkbare bereiken definieert, kan het hele werkblad niet meer worden bewerkt nadat het is beveiligd.
### Is het beschermde bereik zichtbaar voor andere gebruikers?
Nee, de beveiliging is intern. Gebruikers worden alleen gevraagd een wachtwoord in te voeren als ze proberen het beveiligde gebied te bewerken.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
