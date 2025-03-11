---
title: Rijen in werkblad beveiligen met Aspose.Cells
linktitle: Rijen in werkblad beveiligen met Aspose.Cells
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u rijen in een Excel-werkblad kunt beveiligen met Aspose.Cells voor .NET. Beveilig uw gegevens met beveiliging op rijniveau en voorkom onbedoelde wijzigingen.
weight: 18
url: /nl/net/worksheet-security/protect-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rijen in werkblad beveiligen met Aspose.Cells

## Invoering
Werken met Excel-bestanden op een programmatische manier is vaak een taak die niet alleen gegevensmanipulatie vereist, maar ook gegevensbescherming. Of u nu gevoelige gegevens wilt beschermen of onbedoelde bewerking wilt voorkomen, het beschermen van rijen in een werkblad kan een cruciale stap zijn. In deze tutorial duiken we in hoe u specifieke rijen in een Excel-werkblad kunt beschermen met Aspose.Cells voor .NET. We doorlopen alle noodzakelijke stappen, van het voorbereiden van uw omgeving tot het implementeren van de beschermingsfuncties op een eenvoudige, gemakkelijk te volgen manier.
## Vereisten
Voordat u rijen in een werkblad kunt beveiligen, moet u een aantal zaken regelen:
1.  Aspose.Cells voor .NET: Zorg ervoor dat u Aspose.Cells voor .NET op uw ontwikkelmachine hebt geïnstalleerd. Als u dit nog niet hebt gedaan, kunt u het eenvoudig downloaden van de[Aspose Cells downloadpagina](https://releases.aspose.com/cells/net/).
2. Visual Studio of een .NET IDE: Om de oplossing te implementeren, moet u een ontwikkelomgeving hebben ingesteld. Visual Studio is een geweldige optie, maar elke .NET-compatibele IDE werkt.
3. Basiskennis van C#: Als u de basisbeginselen van C#-programmering begrijpt, kunt u de tutorial beter volgen en de voorbeeldcode aanpassen aan uw behoeften.
4.  Aspose.Cells API-documentatie: Maak uzelf vertrouwd met de[Aspose.Cells voor .NET-documentatie](https://reference.aspose.com/cells/net/) om een overzicht te krijgen van de klassenstructuur en de methoden die in de bibliotheek worden gebruikt.
Zodra u aan de vereisten hebt voldaan, kunnen we direct met de implementatie beginnen.
## Pakketten importeren
Om te beginnen moet u de vereiste pakketten importeren. Deze bibliotheken zijn cruciaal voor interactie met Excel-bestanden in uw C#-project.
```csharp
using System.IO;
using Aspose.Cells;
```
Zodra u de benodigde pakketten hebt geïmporteerd, kunt u beginnen met coderen. 
Laten we het proces nu opsplitsen in kleinere stappen om het supermakkelijk voor u te maken om te volgen. Elke stap richt zich op een specifiek onderdeel van de implementatie, zodat u het snel kunt begrijpen en toepassen. 
## Stap 1: Maak een nieuwe werkmap en werkblad
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
In dit voorbeeld maken we een nieuwe werkmap met één werkblad (dit is de standaardinstelling wanneer u een nieuwe werkmap maakt met Aspose.Cells). Vervolgens pakken we het eerste werkblad in de werkmap, dat het doel is voor onze rijbeveiliging.
## Stap 2: Stijl- en StyleFlag-objecten definiëren
De volgende stap is het definiëren van de stijl- en stijlvlagobjecten. Met deze objecten kunt u de eigenschappen van de cel wijzigen, zoals of deze vergrendeld of ontgrendeld is.
```csharp
// Definieer het stijlobject.
Style style;
// Definieer het styleflag-object.
StyleFlag flag;
```
gebruikt deze objecten in latere stappen om de celeigenschappen aan te passen en toe te passen op uw werkblad.
## Stap 3: Ontgrendel alle kolommen in het werkblad
Standaard zijn alle cellen in een Excel-werkblad vergrendeld. Wanneer u echter een werkblad beveiligt, wordt de vergrendelde status afgedwongen. Om ervoor te zorgen dat alleen specifieke rijen of cellen worden beveiligd, kunt u eerst alle kolommen ontgrendelen. Deze stap is essentieel als u alleen bepaalde rijen wilt beveiligen.
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
 In deze code doorlopen we alle 256 kolommen in het werkblad (Excel-werkbladen hebben maximaal 256 kolommen, geïndexeerd van 0 tot 255) en stellen we hun`IsLocked` eigendom van`false`Met deze actie worden alle kolommen ontgrendeld, maar we vergrendelen later nog steeds specifieke rijen.
## Stap 4: Vergrendel de eerste rij
Zodra u de kolommen hebt ontgrendeld, is de volgende stap het vergrendelen van specifieke rijen die u wilt beschermen. In dit voorbeeld vergrendelen we de eerste rij. Dit zorgt ervoor dat gebruikers deze niet kunnen wijzigen terwijl andere rijen ontgrendeld blijven.
```csharp
//Kies voor de stijl van de eerste rij.
style = sheet.Cells.Rows[0].Style;
// Doe het op slot.
style.IsLocked = true;
//De vlag instantiëren.
flag = new StyleFlag();
// Stel de vergrendelingsinstelling in.
flag.Locked = true;
// Pas de stijl toe op de eerste rij.
sheet.Cells.ApplyRowStyle(0, style, flag);
```
Hier benaderen we de stijl van de eerste rij en stellen deze in`IsLocked` eigendom van`true` Daarna gebruiken we de`ApplyRowStyle()` methode om de lock-stijl toe te passen op de hele rij. U kunt deze stap herhalen om andere rijen te vergrendelen die u wilt beveiligen.
## Stap 5: Bescherm het blad
Nu we de benodigde rijen hebben ontgrendeld en vergrendeld, is het tijd om het werkblad te beveiligen. De beveiliging zorgt ervoor dat niemand de vergrendelde rijen of cellen kan wijzigen, tenzij ze het beveiligingswachtwoord verwijderen (indien opgegeven).
```csharp
// Bescherm het blad.
sheet.Protect(ProtectionType.All);
```
 In deze stap brengen we bescherming aan op het gehele blad met behulp van`ProtectionType.All`. Dit type bescherming betekent dat alle aspecten van het werkblad, inclusief vergrendelde rijen en cellen, beschermd zijn. U kunt deze bescherming ook aanpassen door indien nodig verschillende beschermingstypen op te geven.
## Stap 6: Sla de werkmap op
Ten slotte moeten we de werkmap opslaan nadat we de benodigde stijlen en beveiliging hebben toegepast. De werkmap kan in verschillende formaten worden opgeslagen, zoals Excel 97-2003, Excel 2010, etc.
```csharp
// Sla het Excel-bestand op.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Deze regel code slaat de werkmap op in de Excel 97-2003-indeling met de toegepaste wijzigingen. U kunt de bestandsindeling naar wens wijzigen door te kiezen uit een verscheidenheid aan`SaveFormat` opties.
## Conclusie
En daar heb je het! Je hebt succesvol geleerd hoe je rijen in een werkblad kunt beveiligen met Aspose.Cells voor .NET. Door de bovenstaande stappen te volgen, kun je rijen of kolommen ontgrendelen of vergrendelen indien nodig, en beveiliging toepassen om de integriteit van je gegevens te waarborgen.
## Veelgestelde vragen
### Hoe kan ik meerdere rijen tegelijk beveiligen?  
 U kunt door meerdere rijen heen lussen en de vergrendelingsstijl op elke rij afzonderlijk toepassen. Vervang eenvoudig`0` met de rij-index die u wilt vergrendelen.
### Kan ik een wachtwoord instellen voor de bladbeveiliging?  
 Ja! U kunt een wachtwoord doorgeven aan de`sheet.Protect()` methode om wachtwoordbeveiliging af te dwingen.
### Kan ik cellen ontgrendelen in plaats van hele kolommen?  
Ja! In plaats van kolommen te ontgrendelen, kunt u individuele cellen ontgrendelen door hun stijleigenschappen te wijzigen.
### Wat gebeurt er als ik een beveiligde rij probeer te bewerken?  
Wanneer een rij is beveiligd, voorkomt Excel dat er wijzigingen in de vergrendelde cellen worden aangebracht, tenzij u de beveiliging van het werkblad opheft.
### Kan ik specifieke bereiken achter elkaar beschermen?  
 Ja! U kunt afzonderlijke bereiken in een rij vergrendelen door de`IsLocked` eigenschap voor specifieke cellen binnen het bereik.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
