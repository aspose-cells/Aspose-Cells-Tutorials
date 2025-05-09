---
"description": "Leer hoe u rijen in een Excel-werkblad kunt beveiligen met Aspose.Cells voor .NET. Beveilig uw gegevens met beveiliging op rijniveau en voorkom onbedoelde wijzigingen."
"linktitle": "Rijen in werkbladen beveiligen met Aspose.Cells"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Rijen in werkbladen beveiligen met Aspose.Cells"
"url": "/nl/net/worksheet-security/protect-rows/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Rijen in werkbladen beveiligen met Aspose.Cells

## Invoering
Programmatisch werken met Excel-bestanden vereist vaak niet alleen gegevensmanipulatie, maar ook gegevensbescherming. Of u nu gevoelige gegevens wilt beschermen of onbedoelde bewerking wilt voorkomen, het beveiligen van rijen in een werkblad kan een cruciale stap zijn. In deze tutorial gaan we dieper in op hoe u specifieke rijen in een Excel-werkblad kunt beveiligen met Aspose.Cells voor .NET. We doorlopen alle noodzakelijke stappen, van het voorbereiden van uw omgeving tot het implementeren van de beveiligingsfuncties op een eenvoudige en gemakkelijk te volgen manier.
## Vereisten
Voordat u rijen in een werkblad kunt beveiligen, moet u een aantal zaken regelen:
1. Aspose.Cells voor .NET: Zorg ervoor dat Aspose.Cells voor .NET op uw ontwikkelcomputer is geïnstalleerd. Als u dit nog niet heeft gedaan, kunt u het eenvoudig downloaden van de [Aspose Cells downloadpagina](https://releases.aspose.com/cells/net/).
2. Visual Studio of een andere .NET IDE: Om de oplossing te implementeren, moet u een ontwikkelomgeving opzetten. Visual Studio is een goede optie, maar elke .NET-compatibele IDE werkt.
3. Basiskennis van C#: Als u de basisbeginselen van C#-programmering begrijpt, kunt u de tutorial beter volgen en de voorbeeldcode aanpassen aan uw eigen behoeften.
4. Aspose.Cells API-documentatie: Maak uzelf vertrouwd met de [Aspose.Cells voor .NET-documentatie](https://reference.aspose.com/cells/net/) om een overzicht te krijgen van de klassenstructuur en methoden die in de bibliotheek worden gebruikt.
Zodra u aan de vereisten hebt voldaan, kunnen we direct met de implementatie beginnen.
## Pakketten importeren
Om te beginnen moet u de vereiste pakketten importeren. Deze bibliotheken zijn cruciaal voor de interactie met Excel-bestanden in uw C#-project.
```csharp
using System.IO;
using Aspose.Cells;
```
Zodra u de benodigde pakketten hebt geïmporteerd, kunt u beginnen met coderen. 
Laten we het proces nu opsplitsen in kleinere stappen, zodat je het supergemakkelijk kunt volgen. Elke stap richt zich op een specifiek onderdeel van de implementatie, zodat je het snel kunt begrijpen en toepassen. 
## Stap 1: Een nieuwe werkmap en werkblad maken
Voordat u beveiligingsinstellingen kunt toepassen, moet u een nieuwe werkmap maken en het werkblad selecteren waarmee u wilt werken. Dit wordt uw werkdocument.
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
// Maak een map aan als deze nog niet bestaat.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Maak een nieuwe werkmap.
Workbook wb = new Workbook();
// Maak een werkbladobject en verkrijg het eerste werkblad.
Worksheet sheet = wb.Worksheets[0];
```
In dit voorbeeld maken we een nieuwe werkmap met één werkblad (dit is de standaardinstelling wanneer u een nieuwe werkmap maakt met Aspose.Cells). Vervolgens selecteren we het eerste werkblad in de werkmap, dat het doel zal zijn van onze rijbeveiliging.
## Stap 2: Stijl- en StyleFlag-objecten definiëren
De volgende stap is het definiëren van de stijl- en stijlvlagobjecten. Met deze objecten kunt u de eigenschappen van de cel wijzigen, bijvoorbeeld of deze vergrendeld of ontgrendeld is.
```csharp
// Definieer het stijlobject.
Style style;
// Definieer het styleflag-object.
StyleFlag flag;
```
U zult deze objecten in latere stappen gebruiken om de celeigenschappen aan te passen en ze op uw werkblad toe te passen.
## Stap 3: Ontgrendel alle kolommen in het werkblad
Standaard zijn alle cellen in een Excel-werkblad vergrendeld. Wanneer u een werkblad echter beveiligt, blijft de vergrendelde status gehandhaafd. Om ervoor te zorgen dat alleen specifieke rijen of cellen worden beveiligd, kunt u eerst alle kolommen ontgrendelen. Deze stap is essentieel als u alleen bepaalde rijen wilt beveiligen.
```csharp
// Doorloop alle kolommen in het werkblad en ontgrendel ze.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
In deze code doorlopen we alle 256 kolommen in het werkblad (Excel-werkbladen hebben maximaal 256 kolommen, geïndexeerd van 0 tot 255) en stellen we hun `IsLocked` eigendom van `false`Met deze actie worden alle kolommen ontgrendeld, maar we vergrendelen later nog steeds specifieke rijen.
## Stap 4: Vergrendel de eerste rij
Nadat u de kolommen hebt ontgrendeld, is de volgende stap het vergrendelen van de specifieke rijen die u wilt beveiligen. In dit voorbeeld vergrendelen we de eerste rij. Dit zorgt ervoor dat gebruikers deze niet kunnen wijzigen terwijl de andere rijen ontgrendeld blijven.
```csharp
// Kies voor de stijl van de eerste rij.
style = sheet.Cells.Rows[0].Style;
// Doe het op slot.
style.IsLocked = true;
// De vlag instantiëren.
flag = new StyleFlag();
// Vergrendelingsinstelling instellen.
flag.Locked = true;
// Pas de stijl toe op de eerste rij.
sheet.Cells.ApplyRowStyle(0, style, flag);
```
Hier benaderen we de stijl van de eerste rij en stellen deze in `IsLocked` eigendom van `true`Daarna gebruiken we de `ApplyRowStyle()` Methode om de vergrendelingsstijl op de hele rij toe te passen. U kunt deze stap herhalen om andere rijen te vergrendelen die u wilt beveiligen.
## Stap 5: Bescherm het blad
Nu we de benodigde rijen hebben ontgrendeld en vergrendeld, is het tijd om het werkblad te beveiligen. De beveiliging zorgt ervoor dat niemand de vergrendelde rijen of cellen kan wijzigen, tenzij het wachtwoord (indien opgegeven) wordt verwijderd.
```csharp
// Bescherm het blad.
sheet.Protect(ProtectionType.All);
```
In deze stap brengen we bescherming aan op het hele blad met behulp van `ProtectionType.All`Dit type beveiliging houdt in dat alle aspecten van het werkblad, inclusief vergrendelde rijen en cellen, beveiligd zijn. U kunt deze beveiliging ook aanpassen door indien nodig verschillende beveiligingstypen op te geven.
## Stap 6: Sla de werkmap op
Ten slotte moeten we de werkmap opslaan nadat we de benodigde stijlen en beveiliging hebben toegepast. De werkmap kan in verschillende formaten worden opgeslagen, zoals Excel 97-2003, Excel 2010, enz.
```csharp
// Sla het Excel-bestand op.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Deze regel code slaat de werkmap op in de Excel 97-2003-indeling met de toegepaste wijzigingen. U kunt de bestandsindeling naar wens aanpassen door te kiezen uit verschillende opties. `SaveFormat` opties.
## Conclusie
En voilà! Je hebt met succes geleerd hoe je rijen in een werkblad kunt beveiligen met Aspose.Cells voor .NET. Door de bovenstaande stappen te volgen, kun je rijen of kolommen naar wens ontgrendelen of vergrendelen en beveiliging toepassen om de integriteit van je gegevens te waarborgen.
## Veelgestelde vragen
### Hoe kan ik meerdere rijen tegelijk beveiligen?  
U kunt door meerdere rijen heen bladeren en de vergrendelingsstijl op elke rij afzonderlijk toepassen. Vervang eenvoudig `0` met de rijindex die u wilt vergrendelen.
### Kan ik een wachtwoord instellen voor de bladbeveiliging?  
Ja! Je kunt een wachtwoord doorgeven aan de `sheet.Protect()` methode om wachtwoordbeveiliging af te dwingen.
### Kan ik cellen ontgrendelen in plaats van hele kolommen?  
Ja! In plaats van kolommen te ontgrendelen, kunt u individuele cellen ontgrendelen door hun stijlkenmerken te wijzigen.
### Wat gebeurt er als ik een beveiligde rij probeer te bewerken?  
Wanneer een rij is beveiligd, kan Excel geen bewerkingen meer uitvoeren in de vergrendelde cellen, tenzij u de beveiliging van het werkblad opheft.
### Kan ik specifieke bereiken achter elkaar beschermen?  
Ja! U kunt individuele bereiken in een rij vergrendelen door de `IsLocked` eigenschap voor specifieke cellen binnen het bereik.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}