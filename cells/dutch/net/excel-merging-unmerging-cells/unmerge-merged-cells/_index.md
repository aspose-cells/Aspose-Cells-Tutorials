---
"description": "Splits samengevoegde cellen in Excel eenvoudig op met Aspose.Cells voor .NET. Volg onze stapsgewijze handleiding om betere spreadsheets te maken."
"linktitle": "Samengevoegde cellen in Excel ontkoppelen"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Samengevoegde cellen in Excel ontkoppelen"
"url": "/nl/net/excel-merging-unmerging-cells/unmerge-merged-cells/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Samengevoegde cellen in Excel ontkoppelen

## Invoering

Bent u het zat om te worstelen met samengevoegde cellen in uw Excel-spreadsheets? U bent niet de enige! Samengevoegde cellen kunnen een handige functie zijn voor opmaak, maar ze kunnen vaak tot hoofdpijn leiden bij het manipuleren en analyseren van gegevens. Maar raad eens? Het samenvoegen van die vervelende cellen is makkelijker dan u denkt, vooral met Aspose.Cells voor .NET. In dit artikel leg ik u stap voor stap uit hoe u samengevoegde cellen kunt ontkoppelen, zodat uw gegevens netjes, overzichtelijk en klaar voor gebruik zijn! Dus, pak uw programmeerhoed en duik in de wereld van Aspose.Cells.

## Vereisten

Voordat we aan de slag gaan, zijn er een paar essentiële zaken die je op orde moet hebben:

### Basiskennis van C# en .NET Framework
Als je bekend bent met C# programmeren en een basiskennis hebt van het .NET Framework, ben je al goed op weg. Zo niet, maak je dan geen zorgen! Deze tutorial is zo eenvoudig mogelijk opgezet, zodat je de nodige concepten gaandeweg leert.

### Aspose.Cells Bibliotheek
Zorg ervoor dat de Aspose.Cells-bibliotheek in uw .NET-omgeving is geïnstalleerd. U kunt deze eenvoudig verkrijgen via de website [Aspose.Cells downloadpagina](https://releases.aspose.com/cells/net/).

### IDE-installatie
U dient een ontwikkelomgeving in te richten, zoals Visual Studio, waar u uw C#-code kunt schrijven en uitvoeren.

### Voorbeeld Excel-bestand
Download een Excel-voorbeeldbestand met enkele samengevoegde cellen. U gaat dit bestand gebruiken om te oefenen met het ongedaan maken van samenvoegingen.

Nu alle vereisten zijn geregeld, kunnen we beginnen met het spannende deel: het coderen van onze oplossing!

## Pakketten importeren

Laten we eerst de benodigde pakketten importeren. Met Aspose.Cells werk je met verschillende klassen om je Excel-bestanden effectief te beheren. Dit is wat je bovenaan je C#-bestand moet opnemen:

```csharp
using System;
using System.IO;

using Aspose.Cells;
```

Wanneer u dit pakket aanschaft, krijgt u toegang tot alle functies die Aspose.Cells biedt.

Laten we het ontkoppelingsproces opsplitsen in beheersbare stappen. Elke stap wordt duidelijk beschreven, zodat u het gemakkelijk kunt volgen.

## Stap 1: Mappen definiëren

De eerste stap is het definiëren van de mappen waar uw invoerbestand (het bestand met samengevoegde cellen) en uw uitvoerbestand (het bestand waar de niet-samengevoegde gegevens worden opgeslagen) zich bevinden. Zo stelt u dat in:

```csharp
// Bronmap
string sourceDir = "Your Document Directory"; 

// Uitvoermap
string outputDir = "Your Document Directory"; 
```

Zorg ervoor dat u vervangt `"Your Document Directory"` met het daadwerkelijke pad naar uw bestanden.

## Stap 2: Maak een werkboek

Nu je de mappen hebt ingesteld, is het tijd om een werkmapobject aan te maken. Met dit object kun je het Excel-bestand bewerken. Je kunt dit doen met de volgende code:

```csharp
// Maak een werkboek
Workbook wbk = new Aspose.Cells.Workbook(sourceDir + "sampleUnMergingtheMergedCells.xlsx");
```

Deze regel code leest uw voorbeeld-Excel-bestand en bereidt het voor op verwerking. 

## Stap 3: Toegang tot het werkblad

Elke werkmap bestaat uit werkbladen. Je moet het specifieke werkblad openen waarvan je de cellen wilt samenvoegen. Zo doe je dat:

```csharp
// Maak een werkblad en ontvang het eerste werkblad
Worksheet worksheet = wbk.Worksheets[0];
```

Deze code pakt het eerste werkblad. Als je samengevoegde cellen zich op een ander werkblad bevinden, werk dan de index dienovereenkomstig bij.

## Stap 4: Toegang tot cellen in het werkblad

Vervolgens moet je een verwijzing naar de cellen in je werkblad krijgen. Dit kun je doen met:

```csharp
// Maak een Cells-object om alle cellen op te halen
Cells cells = worksheet.Cells;
```

Dankzij deze regel hebt u nu toegang tot alle cellen in het werkblad, zodat u ze naar wens kunt bewerken.

## Stap 5: De cellen samenvoegen

Hier komt de cruciale stap: het samenvoegen van de cellen! Geef het bereik van de samengevoegde cellen op dat u wilt samenvoegen. Gebruik de volgende code:

```csharp
// Cellen samenvoegen
cells.UnMerge(5, 2, 2, 3);
```

In dit voorbeeld is de `UnMerge` De methode heeft vier parameters: de beginrij-index (5), de beginkolom-index (2), het aantal rijen waarvan de samenvoeging ongedaan moet worden gemaakt (2) en het aantal kolommen waarvan de samenvoeging ongedaan moet worden gemaakt (3). Pas deze parameters aan zodat ze overeenkomen met de specifieke samengevoegde cellen in uw Excel-bestand.

## Stap 6: Sla de werkmap op

Nadat u de samenvoeging hebt ongedaan gemaakt, wilt u uw wijzigingen opslaan in een nieuw Excel-bestand. Zo doet u dat:

```csharp
// Sla het bestand op
wbk.Save(outputDir + "outputUnMergingtheMergedCells.xlsx");
```

Deze regel slaat uw niet-samengevoegde gegevens op in de opgegeven uitvoermap. Zo simpel is het!

## Stap 7: Bevestig het proces

Tot slot is het een goed idee om te bevestigen dat alles goed is verlopen. U kunt een bericht naar de console sturen om u te laten weten dat de bewerking succesvol is uitgevoerd:

```csharp
Console.WriteLine("UnMerging the Cells executed successfully.");
```

En voilà! Je hebt met succes cellen in een Excel-bestand samengevoegd met Aspose.Cells voor .NET.

## Conclusie

Het samenvoegen van cellen lijkt misschien omslachtig, vooral als je met grote spreadsheets werkt, maar met Aspose.Cells voor .NET is het een fluitje van een cent! Deze tutorial heeft je door alles heen geleid, van het instellen van je omgeving tot het uitvoeren van de code die nodig is om cellen effectief te ontkoppelen. De flexibiliteit van de Aspose.Cells-bibliotheek stelt je in staat om spreadsheets efficiënt te verwerken, waardoor het een ideale keuze is voor ontwikkelaars die met Excel-bestanden werken. Dus duik erin en geniet van overzichtelijke, beter beheerbare spreadsheets.

## Veelgestelde vragen

### Wat is Aspose.Cells?  
Aspose.Cells is een krachtige bibliotheek voor het maken, bewerken en converteren van Excel-documenten in .NET-toepassingen.

### Heb ik een licentie nodig om Aspose.Cells te gebruiken?  
Hoewel Aspose.Cells een gratis proefperiode aanbiedt, is een licentie vereist voor volledig gebruik. U kunt een [tijdelijke licentie hier](https://purchase.aspose.com/temporary-license/).

### Kan ik cellen in meerdere werkbladen tegelijk samenvoegen?  
Ja, u kunt door meerdere werkbladen in een werkmap bladeren en cellen indien nodig samenvoegen.

### Is Aspose.Cells compatibel met .NET Core?  
Ja, Aspose.Cells is compatibel met .NET Core, waardoor het veelzijdig is voor diverse .NET-toepassingen.

### Waar kan ik meer documentatie over Aspose.Cells vinden?  
U kunt de volledige documentatie op de [Aspose.Cells Referentiepagina](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}