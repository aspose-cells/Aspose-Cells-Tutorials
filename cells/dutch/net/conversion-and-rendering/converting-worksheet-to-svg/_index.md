---
title: Werkblad converteren naar SVG in .NET
linktitle: Werkblad converteren naar SVG in .NET
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u een Excel-werkblad naar SVG converteert met Aspose.Cells voor .NET met deze stapsgewijze handleiding. Perfect voor .NET-ontwikkelaars die Excel naar SVG willen renderen.
weight: 11
url: /nl/net/conversion-and-rendering/converting-worksheet-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Werkblad converteren naar SVG in .NET

## Invoering

Als u een Excel-werkblad wilt converteren naar SVG-formaat, bent u hier aan het juiste adres! Aspose.Cells voor .NET is een krachtige tool waarmee ontwikkelaars Excel-bestanden kunnen bewerken en converteren naar verschillende formaten, waaronder de breed ondersteunde SVG (Scalable Vector Graphics). Deze tutorial leidt u door het proces van het converteren van een werkblad naar een SVG in .NET, waarbij het stap voor stap wordt uitgelegd, zodat zelfs beginners het gemakkelijk kunnen volgen.

## Vereisten

Voordat we in de code duiken, controleren we of je alles hebt wat je nodig hebt:

1.  Aspose.Cells voor .NET: Download en installeer de nieuwste versie van Aspose.Cells voor .NET van[Aspose.Cells voor .NET](https://releases.aspose.com/cells/net/).
2. .NET-ontwikkelomgeving: Visual Studio of een andere .NET IDE moet geïnstalleerd zijn.
3. Basiskennis van C#: Kennis van C# is vereist, maar maak je geen zorgen, we leggen alles duidelijk uit.
4. Excel-bestand: Zorg dat u een Excel-bestand bij de hand hebt dat u naar SVG-formaat wilt converteren.

## Noodzakelijke pakketten importeren

Voordat u met coderen begint, moet u ervoor zorgen dat u de vereiste naamruimten bovenaan uw C#-bestand opneemt.

```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```

Deze pakketten zijn nodig voor het werken met Aspose.Cells en het verwerken van renderingopties zoals SVG-export.

Nu we de basis hebben behandeld, gaan we verder met de daadwerkelijke stappen voor het converteren van een Excel-werkblad naar een SVG-afbeelding.

## Stap 1: Stel het pad naar uw documentenmap in

Het eerste wat we nodig hebben is het pad naar de map te definiëren waar uw Excel-bestand zich bevindt. Dit is cruciaal omdat uw code naar de map zal verwijzen om bestanden te laden en op te slaan.

```csharp
// Het pad naar de documentenmap
string dataDir = "Your Document Directory";
```

 Zorg ervoor dat u vervangt`"Your Document Directory"`met het werkelijke pad waar uw Excel-bestand zich bevindt.

##  Stap 2: Laad het Excel-bestand met behulp van`Workbook`

 Vervolgens moeten we het Excel-bestand laden in een exemplaar van de`Workbook` klasse. De`Workbook` klasse vertegenwoordigt het volledige Excel-bestand, inclusief alle werkbladen erin.

```csharp
string filePath = dataDir + "Template.xlsx";
Workbook book = new Workbook(filePath);
```

 Hier,`"Template.xlsx"` is de naam van het Excel-bestand waarmee u werkt. Zorg ervoor dat dit bestand in de opgegeven directory staat, anders krijgt u fouten.

## Stap 3: Stel afbeeldings- of afdrukopties in voor SVG-conversie

 Voordat we het werkblad naar SVG-formaat kunnen converteren, moeten we de afbeeldingsopties opgeven.`ImageOrPrintOptions` klasse kunt u bepalen hoe het werkblad wordt geconverteerd. Meer specifiek moeten we de`SaveFormat` naar`SVG` en zorg ervoor dat elk werkblad wordt omgezet naar één pagina.

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.SaveFormat = SaveFormat.Svg;
imgOptions.OnePagePerSheet = true;
```

 De`SaveFormat.Svg` optie zorgt ervoor dat het uitvoerformaat SVG zal zijn, terwijl`OnePagePerSheet` zorgt ervoor dat elk werkblad op één pagina wordt weergegeven.

## Stap 4: Door elk werkblad in de werkmap itereren

Nu moeten we alle werkbladen in het Excel-bestand doorlopen. Elk werkblad wordt afzonderlijk geconverteerd.

```csharp
foreach (Worksheet sheet in book.Worksheets)
{
    // We zullen elk werkblad één voor één verwerken
}
```

Deze lus zorgt ervoor dat elk werkblad, ongeacht het aantal werkbladen in uw werkmap, wordt verwerkt.

##  Stap 5: Maak een`SheetRender` Object for Rendering

 Voor elk werkblad maken we een`SheetRender` object. Dit object is verantwoordelijk voor het converteren van het werkblad naar het gewenste afbeeldingsformaat, in dit geval SVG.

```csharp
SheetRender sr = new SheetRender(sheet, imgOptions);
```

 De`SheetRender` object heeft twee argumenten: het werkblad dat u wilt converteren en de afbeeldingsopties die u eerder hebt gedefinieerd.

## Stap 6: Converteer het werkblad naar SVG

 Tot slot zullen we binnen de lus elk werkblad omzetten naar SVG-formaat. We gebruiken een geneste lus om door de pagina's te itereren (hoewel er in dit geval slechts één pagina per werkblad is, dankzij de`OnePagePerSheet` optie).

```csharp
for (int i = 0; i < sr.PageCount; i++)
{
    // Werkblad uitvoeren in SVG-afbeeldingsformaat
    sr.ToImage(i, filePath + sheet.Name + i + ".out.svg");
}
```

Deze code slaat het werkblad op als een SVG-bestand in dezelfde map als het Excel-bestand. Elk SVG-bestand krijgt een naam die overeenkomt met de naam van het werkblad en een indexnummer om naamgevingsconflicten te voorkomen.

## Conclusie

En dat is alles! U hebt met succes een Excel-werkblad omgezet naar SVG-formaat met Aspose.Cells voor .NET. Met dit proces behoudt u de lay-out en het ontwerp van uw werkblad, terwijl u het in elke browser of op elk apparaat kunt bekijken dat SVG ondersteunt, wat vrijwel alle browsers en apparaten zijn. Of u nu werkt met complexe Excel-bestanden of gewoon een eenvoudige tabel, deze methode zorgt ervoor dat uw gegevens prachtig worden weergegeven in een webvriendelijk formaat.

## Veelgestelde vragen

### Wat is SVG en waarom zou ik het gebruiken?
SVG (Scalable Vector Graphics) is een webvriendelijk formaat dat oneindig kan schalen zonder kwaliteitsverlies. Het is perfect voor grafieken, diagrammen en afbeeldingen die in verschillende formaten moeten worden weergegeven.

### Kan Aspose.Cells grote Excel-bestanden converteren?
Ja, Aspose.Cells kan grote Excel-bestanden efficiënt verwerken en converteren naar SVG zonder noemenswaardige prestatieproblemen.

### Is er een limiet aan het aantal werkbladen dat ik naar SVG kan converteren?
Nee, er is geen inherente limiet in Aspose.Cells voor het converteren van meerdere werkbladen. De enige beperking zou het geheugen en de prestaties van uw systeem zijn.

### Heb ik een licentie nodig om Aspose.Cells te gebruiken?
 Ja, Aspose.Cells vereist een licentie voor productiegebruik. U kunt een tijdelijke licentie verkrijgen[hier](https://purchase.aspose.com/temporary-license/) of verken de[gratis proefperiode](https://releases.aspose.com/).

### Kan ik de SVG-uitvoer aanpassen?
 Ja, je kunt de`ImageOrPrintOptions` om verschillende aspecten van de SVG-uitvoer aan te passen, zoals resolutie en schaal.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
