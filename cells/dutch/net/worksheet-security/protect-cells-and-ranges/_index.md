---
title: Bescherm cellen en bereiken in werkbladen met Aspose.Cells
linktitle: Bescherm cellen en bereiken in werkbladen met Aspose.Cells
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u cellen en bereiken in een Excel-werkblad kunt beveiligen met Aspose.Cells voor .NET. Volg deze stapsgewijze handleiding om uw spreadsheets te beveiligen.
weight: 11
url: /nl/net/worksheet-security/protect-cells-and-ranges/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bescherm cellen en bereiken in werkbladen met Aspose.Cells

## Invoering
Werken met spreadsheets houdt vaak in dat bepaalde delen van het werkblad worden beschermd tegen ongewenste wijzigingen, vooral in collaboratieve omgevingen. In deze tutorial gaan we onderzoeken hoe u specifieke cellen en bereiken in een werkblad kunt beschermen met Aspose.Cells voor .NET. We begeleiden u door het proces van het instellen van een beschermd werkblad, het specificeren van welke bereiken bewerkbaar zijn en het opslaan van het bestand. Dit kan een uiterst nuttige functie zijn wanneer u de toegang tot gevoelige gegevens wilt beperken, terwijl u bepaalde secties door anderen wilt laten wijzigen.
## Vereisten
Voordat u met de tutorial begint, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:
1. Aspose.Cells voor .NET: U moet de Aspose.Cells-bibliotheek in uw project hebben geïnstalleerd. Als u dat nog niet hebt gedaan, kunt u deze downloaden van de[Aspose-website](https://releases.aspose.com/cells/net/).
2. Visual Studio: in deze handleiding wordt ervan uitgegaan dat u Visual Studio of een vergelijkbare IDE gebruikt die C#-ontwikkeling ondersteunt.
3. Basiskennis van C#: U moet bekend zijn met de basisbeginselen van C#-programmering en weten hoe u een project in Visual Studio opzet.
4.  Aspose.Cells Licentie: Hoewel Aspose een gratis proefperiode aanbiedt, kunt u met een geldige licentie de volledige functieset van de bibliotheek gebruiken. Als u er geen hebt, kunt u een[tijdelijke licentie hier](https://purchase.aspose.com/temporary-license/).
Zodra u er zeker van bent dat u alle bovenstaande zaken bij de hand hebt, kunnen we verder met het coderen.
## Pakketten importeren
Om met Aspose.Cells te kunnen werken, moet u eerst de benodigde namespaces importeren in uw C#-bestand. Zo importeert u ze:
```csharp
using System.IO;
using Aspose.Cells;
```
 De`Aspose.Cells` Met de naamruimte krijgt u toegang tot de kernfunctionaliteiten voor het bewerken van Excel-bestanden en`System.IO` wordt gebruikt voor bestandsbewerkingen, zoals het opslaan van de werkmap.
Laten we nu de stappen voor het beveiligen van cellen en bereiken in een werkblad met behulp van Aspose.Cells doornemen.
## Stap 1: Stel uw omgeving in
Maak eerst een directory waar u uw Excel-bestanden wilt opslaan. Als de directory nog niet bestaat, maken we er een. Dit helpt ervoor te zorgen dat u een plek hebt om uw uitvoerbestand op te slaan.
```csharp
// Definieer het pad naar uw documentenmap
string dataDir = "Your Document Directory";
// Controleer of de directory bestaat, indien niet, maak deze dan aan
bool IsExists = Directory.Exists(dataDir);
if (!IsExists)
    Directory.CreateDirectory(dataDir);
```
 Hier gebruiken we`System.IO.Directory.Exists()` om te controleren of de map bestaat, en als dat niet zo is, maken we deze aan met behulp van`Directory.CreateDirectory()`.
## Stap 2: Maak een nieuwe werkmap
Laten we nu een nieuw Workbook-object instantiëren. Dit zal dienen als ons Excel-bestand waarin we onze cellen en bereiken definiëren.
```csharp
// Een nieuw werkmapobject instantiëren
Workbook book = new Workbook();
```
 De`Workbook` class is het startpunt voor het werken met Excel-bestanden in Aspose.Cells. Het vertegenwoordigt het Excel-document.
## Stap 3: Toegang tot het standaardwerkblad
Elke nieuw aangemaakte werkmap heeft een standaardwerkblad. We halen het op om met de inhoud ervan te werken.
```csharp
// Haal het eerste (standaard) werkblad in de werkmap op
Worksheet sheet = book.Worksheets[0];
```
 Hier,`Worksheets[0]` geeft ons het eerste werkblad in de werkmap (indexering start bij 0).
## Stap 4: bewerkbare bereiken definiëren
Om bepaalde delen van het werkblad te beschermen en gebruikers toch toe te staan specifieke cellen te bewerken, moeten we bewerkbare bereiken definiëren. We maken een bereik dat kan worden bewerkt en voegen het toe aan de AllowEditRanges-collectie van het werkblad.
```csharp
// Haal de AllowEditRanges-collectie op
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
// Definieer een ProtectedRange en voeg deze toe aan de verzameling
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
ProtectedRange protectedRange = allowRanges[idx];
```
In de bovenstaande code:
- `"r2"` is de naam van het bewerkbare bereik.
-  De cijfers`1, 1, 3, 3` geven de begin- en eindrij- en kolomindices voor het bereik weer (d.w.z. van cel B2 tot D4).
## Stap 5: Stel een wachtwoord in voor het beveiligde bereik
Nu we het bewerkbare bereik hebben gedefinieerd, voegen we een wachtwoord toe om het te beschermen. Dit betekent dat gebruikers het wachtwoord nodig hebben om dit specifieke bereik te bewerken.
```csharp
// Geef het wachtwoord op voor het bewerkbare bereik
protectedRange.Password = "123";
```
 Hier hebben we het wachtwoord ingesteld als`"123"`, maar u kunt elk veilig wachtwoord kiezen. Deze stap is essentieel voor het beheren van de toegang tot de bewerkbare gebieden.
## Stap 6: Bescherm het hele blad
In deze fase beveiligen we het hele werkblad. Het beveiligen van het werkblad zorgt ervoor dat andere delen van het werkblad, behalve de toegestane bereiken, niet bewerkbaar zijn.
```csharp
// Bescherm het blad met het opgegeven beschermingstype (Alle)
sheet.Protect(ProtectionType.All);
```
Hiermee zorgt u ervoor dat alle cellen in het werkblad vergrendeld zijn, behalve de cellen in de bewerkbare bereiken.
## Stap 7: Sla de werkmap op
Tot slot slaan we de werkmap op in een bestand. Het beveiligde werkblad wordt opgeslagen onder de naam die u opgeeft.
```csharp
// Sla het Excel-bestand op in de opgegeven directory
book.Save(dataDir + "protectedrange.out.xls");
```
 Hier wordt het Excel-bestand opgeslagen als`protectedrange.out.xls` in de directory die we eerder hebben gedefinieerd. Als u het onder een andere naam of formaat wilt opslaan, kunt u de bestandsnaam en extensie wijzigen.
## Conclusie
Door deze tutorial te volgen, hebt u geleerd hoe u cellen en bereiken in een Excel-werkblad kunt beschermen met Aspose.Cells voor .NET. Deze aanpak geeft u flexibiliteit in het bepalen welke gebieden van uw spreadsheet kunnen worden bewerkt en welke niet. U kunt deze vaardigheden nu toepassen in uw eigen projecten, zodat uw gevoelige gegevens veilig blijven en gebruikers bewerkbare gebieden krijgen.
Vergeet niet dat Aspose.Cells een robuuste set hulpmiddelen biedt voor het werken met Excel-bestanden. Dit is slechts een van de vele dingen die u ermee kunt doen. 
## Veelgestelde vragen
### Kan ik alleen bepaalde cellen in een werkblad beveiligen?
 Ja, door gebruik te maken van de`AllowEditRanges` Met de eigenschap kunt u opgeven welke cellen of bereiken kunnen worden bewerkt, terwijl de rest van het werkblad beveiligd blijft.
### Kan ik de bescherming later verwijderen?
 Ja, u kunt de beveiliging van een werkblad opheffen door de`Unprotect()` methode, en als er een wachtwoord is ingesteld, moet u dit opgeven.
### Hoe beveilig ik een heel werkblad met een wachtwoord?
 Om het hele blad te beschermen, gebruikt u eenvoudig de`Protect()` methode met of zonder wachtwoord. Bijvoorbeeld,`sheet.Protect("password")`.
### Kan ik meerdere bewerkbare bereiken toevoegen?
 Absoluut! U kunt zoveel bewerkbare bereiken toevoegen als u nodig hebt door`allowRanges.Add()` meerdere keren.
### Welke andere beveiligingsfuncties biedt Aspose.Cells?
Aspose.Cells ondersteunt diverse beveiligingsfuncties, zoals werkmapversleuteling, het instellen van bestandswachtwoorden en het beveiligen van cellen en werkbladen.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
