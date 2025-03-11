---
title: Samengevoegde cellen in Excel ontkoppelen
linktitle: Samengevoegde cellen in Excel ontkoppelen
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Maak samengevoegde cellen in Excel eenvoudig los met Aspose.Cells voor .NET. Volg onze stapsgewijze handleiding om betere spreadsheets te maken.
weight: 10
url: /nl/net/excel-merging-unmerging-cells/unmerge-merged-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Samengevoegde cellen in Excel ontkoppelen

## Invoering

Bent u het zat om met samengevoegde cellen in uw Excel-spreadsheets te werken? U bent niet de enige! Samengevoegde cellen kunnen een handige functie zijn voor opmaak, maar ze kunnen vaak leiden tot hoofdpijn als het gaat om gegevensmanipulatie en -analyse. Maar raad eens? Het samenvoegen van die vervelende cellen is gemakkelijker dan u zou denken, vooral als u Aspose.Cells voor .NET gebruikt. In dit artikel laat ik u stap voor stap zien hoe u samengevoegde cellen kunt samenvoegen, zodat uw gegevens netjes, opgeruimd en klaar voor actie zijn! Dus pak uw programmeerhoed en duik in de wereld van Aspose.Cells.

## Vereisten

Voordat we aan de slag gaan, zijn er een paar essentiële zaken die u op orde moet hebben:

### Basiskennis van C# en .NET Framework
Als u bekend bent met C#-programmering en een basiskennis hebt van het .NET-framework, bent u al goed op weg. Zo niet, maak u dan geen zorgen! Deze tutorial is ontworpen om eenvoudig te zijn, zodat u onderweg de nodige concepten oppikt.

### Aspose.Cells-bibliotheek
Zorg ervoor dat u de Aspose.Cells-bibliotheek in uw .NET-omgeving hebt geïnstalleerd. U kunt deze eenvoudig verkrijgen door naar de[Aspose.Cells Downloadpagina](https://releases.aspose.com/cells/net/).

### IDE-installatie
U moet een ontwikkelomgeving opzetten, zoals Visual Studio, waar u uw C#-code kunt schrijven en uitvoeren.

### Voorbeeld Excel-bestand
Download een voorbeeld van een Excel-bestand met samengevoegde cellen. Dit bestand gaat u gebruiken om te oefenen met het ongedaan maken van samenvoegingen.

Nu we aan al deze voorwaarden hebben voldaan, kunnen we beginnen met het spannende gedeelte: het coderen van onze oplossing!

## Pakketten importeren

Laten we eerst de benodigde pakketten importeren. Met Aspose.Cells werkt u met verschillende klassen om uw Excel-bestanden effectief te beheren. Dit is wat u bovenaan uw C#-bestand moet opnemen:

```csharp
using System;
using System.IO;

using Aspose.Cells;
```

Wanneer u dit pakket aanschaft, krijgt u toegang tot alle functies die Aspose.Cells biedt.

Laten we het unmerging-proces opsplitsen in beheersbare stappen. Elke stap wordt duidelijk gedefinieerd, zodat u het gemakkelijk kunt volgen.

## Stap 1: Definieer mappen

De eerste stap is het definiëren van de mappen waar uw invoer Excel-bestand (degene met samengevoegde cellen) en uw uitvoerbestand (degene waar de niet-samengevoegde gegevens worden opgeslagen) zich bevinden. Hier is hoe u dat instelt:

```csharp
// Bron directory
string sourceDir = "Your Document Directory"; 

// Uitvoermap
string outputDir = "Your Document Directory"; 
```

 Zorg ervoor dat u vervangt`"Your Document Directory"` met het daadwerkelijke pad naar uw bestanden.

## Stap 2: Maak een werkmap

Nu u de mappen hebt ingesteld, is het tijd om een Workbook-object te maken. Met dit object kunt u het Excel-bestand manipuleren. U kunt dit doen met de volgende code:

```csharp
// Maak een werkboek
Workbook wbk = new Aspose.Cells.Workbook(sourceDir + "sampleUnMergingtheMergedCells.xlsx");
```

Deze regel code leest uw voorbeeld-Excel-bestand en bereidt het voor op verwerking. 

## Stap 3: Toegang tot het werkblad

Elke werkmap bestaat uit sheets. U moet toegang hebben tot het specifieke werkblad waar u de cellen wilt unmergen. Dit is hoe u dat doet:

```csharp
// Maak een werkblad en ontvang het eerste werkblad
Worksheet worksheet = wbk.Worksheets[0];
```

Deze code pakt het eerste werkblad. Als uw samengevoegde cellen zich op een ander werkblad bevinden, werkt u de index dienovereenkomstig bij.

## Stap 4: Toegang tot cellen in het werkblad

Vervolgens moet u een verwijzing naar de cellen in uw werkblad krijgen. Dit kunt u doen met:

```csharp
//Maak een Cells-object om alle cellen op te halen
Cells cells = worksheet.Cells;
```

Met deze regel hebt u nu toegang tot alle cellen in het werkblad, zodat u ze naar wens kunt bewerken.

## Stap 5: Cellen samenvoegen

Hier komt de cruciale stap: de cellen samenvoegen! U wilt het bereik van de samengevoegde cellen opgeven die u wilt samenvoegen. Gebruik de volgende code:

```csharp
// Cellen samenvoegen
cells.UnMerge(5, 2, 2, 3);
```

 In dit voorbeeld is de`UnMerge` De methode heeft vier parameters: de beginrij-index (5), de beginkolom-index (2), het aantal rijen waarvan de samenvoeging ongedaan moet worden gemaakt (2) en het aantal kolommen waarvan de samenvoeging ongedaan moet worden gemaakt (3). Pas deze parameters aan zodat ze overeenkomen met de specifieke samengevoegde cellen in uw Excel-bestand.

## Stap 6: Sla de werkmap op

Na het samenvoegen wilt u uw wijzigingen opslaan in een nieuw Excel-bestand. Dit is hoe u dat doet:

```csharp
// Sla het bestand op
wbk.Save(outputDir + "outputUnMergingtheMergedCells.xlsx");
```

Deze regel slaat uw niet-samengevoegde gegevens op in de opgegeven uitvoermap. Zo simpel is het!

## Stap 7: Bevestig het proces

Tot slot is het een goed idee om te bevestigen dat alles soepel is verlopen. U kunt een bericht naar de console afdrukken om u te laten weten dat de bewerking succesvol is uitgevoerd:

```csharp
Console.WriteLine("UnMerging the Cells executed successfully.");
```

En daar heb je het! Je hebt succesvol cellen in een Excel-bestand samengevoegd met Aspose.Cells voor .NET.

## Conclusie

Cellen samenvoegen lijkt misschien omslachtig, vooral als u met grote spreadsheets werkt, maar met Aspose.Cells voor .NET is het een fluitje van een cent! Deze tutorial leidde u door alles heen, van het instellen van uw omgeving tot het uitvoeren van de code die nodig is om cellen effectief samen te voegen. De flexibiliteit die de Aspose.Cells-bibliotheek biedt, stelt u in staat om spreadsheets efficiënt te verwerken, waardoor het een ideale keuze is voor ontwikkelaars die met Excel-bestanden werken. Dus duik erin en begin te genieten van schonere, beter beheerbare spreadsheets.

## Veelgestelde vragen

### Wat is Aspose.Cells?  
Aspose.Cells is een krachtige bibliotheek voor het maken, bewerken en converteren van Excel-documenten in .NET-toepassingen.

### Heb ik een licentie nodig om Aspose.Cells te gebruiken?  
 Terwijl Aspose.Cells een gratis proefversie aanbiedt, is een licentie vereist voor volledig gebruik. U kunt een[tijdelijke licentie hier](https://purchase.aspose.com/temporary-license/).

### Kan ik cellen in meerdere werkbladen tegelijk samenvoegen?  
Ja, u kunt door meerdere werkbladen in een werkmap bladeren en cellen indien nodig opsplitsen.

### Is Aspose.Cells compatibel met .NET Core?  
Ja, Aspose.Cells is compatibel met .NET Core, waardoor het veelzijdig is voor verschillende .NET-toepassingen.

### Waar kan ik meer documentatie over Aspose.Cells vinden?  
 U kunt de volledige documentatie op de[Aspose.Cells Referentiepagina](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
