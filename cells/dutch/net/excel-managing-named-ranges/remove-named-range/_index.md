---
"description": "Leer hoe u benoemde bereiken in Excel verwijdert met Aspose.Cells voor .NET, met gedetailleerde, stapsgewijze instructies."
"linktitle": "Benoemd bereik in Excel verwijderen"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Benoemd bereik in Excel verwijderen"
"url": "/nl/net/excel-managing-named-ranges/remove-named-range/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Benoemd bereik in Excel verwijderen

## Invoering
Excel is voor veel mensen en organisaties een onmisbaar hulpmiddel geworden in databeheer en -analyse. Of je nu een ervaren data-analist bent of gewoon iemand die graag je data organiseert, Excel beheersen is essentieel. Vandaag duiken we in een specifieke maar krachtige functie: benoemde bereiken verwijderen met Aspose.Cells voor .NET. Deze handleiding leidt je door de stappen om dit effectief te doen. Dus, stroop je mouwen op en laten we aan de slag gaan!

## Vereisten

Voordat we met het daadwerkelijke coderen beginnen, zijn er een paar dingen die je moet regelen:

### .NET-omgeving instellen

Om naadloos met Aspose.Cells voor .NET te kunnen werken, moet u het volgende doen:

1. Visual Studio: Download en installeer Visual Studio (Community Edition is prima), die u kunt vinden op de [Visual Studio-website](https://visualstudio.microsoft.com/).
2. .NET Framework: Zorg ervoor dat u de juiste versie van .NET Framework gebruikt. Aspose.Cells ondersteunt .NET Framework 4.0 en hoger.
3. Aspose.Cells-bibliotheek: U moet de Aspose.Cells voor .NET-bibliotheek downloaden en raadplegen in uw applicatie. U kunt het downloadbare pakket vinden [hier](https://releases.aspose.com/cells/net/).

### Basiskennis van C#

Je hebt een basiskennis van C#-programmering nodig. Dit helpt je de codefragmenten die we zullen bespreken, te begrijpen.

### Toegang tot Excel-bestanden

Zorg ervoor dat je een Excel-bestand bij de hand hebt om mee te experimenteren. Zo niet, dan kun je er snel een maken met Microsoft Excel.

## Pakketten importeren

Nu we aan de vereisten hebben voldaan, kunnen we de pakketten importeren die we in ons project nodig hebben. Open Visual Studio en maak een nieuwe consoletoepassing. Neem vervolgens de volgende naamruimte op in je programma:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Met deze instelling kunt u gebruikmaken van de functionaliteiten van Aspose.Cells om eenvoudig met Excel-sheets te werken.

## Stap 1: De uitvoermap instellen

Allereerst moeten we bepalen waar ons uitvoerbestand wordt opgeslagen. Dit is cruciaal om later verwarring over de opslaglocatie van je bestanden te voorkomen.

```csharp
// Uitvoermap
string outputDir = "Your Document Directory Here\\";
```

Vervangen `"Your Document Directory Here\\"` met het pad op uw computer waar u het bestand wilt opslaan.

## Stap 2: Een nieuwe werkmap instantiëren

Hoe begin je met een schone lei? Door een nieuw werkboek te maken, natuurlijk! Dit werkboek dient als ons blanco canvas.

```csharp
// Een nieuwe werkmap instantiëren.
Workbook workbook = new Workbook();
```

Deze regel code creëert een nieuwe werkmap die we kunnen bewerken.

## Stap 3: Toegang tot de werkbladcollectie

Elke werkmap bestaat uit een of meer werkbladen. Om binnen een specifiek werkblad te kunnen werken, hebben we toegang tot deze verzameling nodig.

```csharp
// Download alle werkbladen uit het boek.
WorksheetCollection worksheets = workbook.Worksheets;
```

Hier vindt u alle werkbladen die beschikbaar zijn in onze nieuwe werkmap.

## Stap 4: Het eerste werkblad selecteren

Vervolgens willen we binnen het eerste werkblad werken. In veel gevallen is dit het standaard startpunt.

```csharp
// Ontvang het eerste werkblad uit de werkbladenverzameling.
Worksheet worksheet = workbook.Worksheets[0];
```

Met dit codefragment kunnen we eenvoudig het eerste werkblad selecteren.

## Stap 5: Benoemde bereiken maken

Laten we nu een benoemd bereik aanmaken, wat een essentieel onderdeel is van deze tutorial. Dit stelt ons in staat om later te illustreren hoe je een benoemd bereik verwijdert.

```csharp
// Maak een cellenbereik.
Range range1 = worksheet.Cells.CreateRange("E12", "I12");

// Geef het bereik een naam.
range1.Name = "FirstRange";
```

Hier definiëren we een bereik van cellen E12 tot en met I12 en noemen dit “FirstRange.”

## Stap 6: Het benoemde bereik formatteren

Om te laten zien hoe veelzijdig Aspose.Cells is, voegen we wat opmaak toe aan ons benoemde bereik.

```csharp
// Stel de omtrekgrens in op het bereik.
range1.SetOutlineBorder(BorderType.TopBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
range1.SetOutlineBorder(BorderType.BottomBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
range1.SetOutlineBorder(BorderType.LeftBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
range1.SetOutlineBorder(BorderType.RightBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
```

We voegen een marineblauwe, middelgrote rand toe rondom ons assortiment om het visueel aantrekkelijker te maken.

## Stap 7: Gegevens in het bereik invoegen

Vervolgens kunnen we onze cellen vullen met gegevens om ze functioneel te maken.

```csharp
// Voer wat gegevens met wat opmaak in een paar cellen in het bereik in.
range1[0, 0].PutValue("Test");            
range1[0, 4].PutValue(123);
```

In deze stap plaatsen we het woord "Test" in cel E12 en het getal 123 in cel I12.

## Stap 8: Een ander benoemd bereik maken

Om ons punt verder te illustreren, maken we nog een benoemd bereik dat lijkt op het eerste.

```csharp
// Maak een nieuw cellenbereik.
Range range2 = worksheet.Cells.CreateRange("B3", "F3");

// Geef het bereik een naam.
range2.Name = "SecondRange";
```

We hebben nu een ander bereik met de naam "SecondRange" beschikbaar voor gebruik.

## Stap 9: Het eerste bereik kopiëren naar het tweede bereik

Laten we demonstreren hoe we ons tweede bereik kunnen gebruiken door gegevens uit het eerste bereik te kopiëren.

```csharp
// Kopieer het eerste bereik naar het tweede bereik.
range2.Copy(range1);
```

Met deze stap hebben we de gegevens van 'FirstRange' effectief gedupliceerd naar 'SecondRange'.

## Stap 10: Het benoemde bereik verwijderen

En nu het hoogtepunt van onze tutorial: het verwijderen van het benoemde bereik. Hier komt alles samen.

```csharp
// Verwijder het eerder genoemde bereik (bereik1) met zijn inhoud.
worksheet.Cells.ClearRange(range1.FirstRow, range1.FirstColumn, range1.FirstRow + range1.RowCount - 1, range1.FirstColumn + range1.ColumnCount - 1);
```

Met deze regel wordt de inhoud van het bereik dat we willen verwijderen gewist. Er blijven geen sporen achter!

## Stap 11: Het benoemde bereik uit het werkblad verwijderen

Een belangrijke laatste stap is het verwijderen van het benoemde bereik uit de namenverzameling van het werkblad.

```csharp
worksheets.Names.RemoveAt(0);
```

Hiermee wordt het benoemde bereik ‘FirstRange’ effectief uit de werkmap verwijderd.

## Stap 12: De werkmap opslaan

En als laatste, maar zeker niet onbelangrijk: laten we ons werk opslaan. 

```csharp
// Sla het Excel-bestand op.
workbook.Save(outputDir + "outputRemoveNamedRange.xlsx");
```

Met deze opdracht slaan we uw werkmap op met de wijzigingen die we hebben aangebracht. Dit is de plek waar al uw harde werk wordt bewaard!

## Stap 13: Bevestigen van succesvolle uitvoering

Om het geheel netjes af te ronden, kunt u een succesbericht naar de console sturen.

```csharp
Console.WriteLine("RemoveNamedRange executed successfully.");
```

Hiermee weet u dat de hele operatie vlekkeloos is verlopen!

## Conclusie

Door deze handleiding te volgen, hebt u geleerd hoe u benoemde bereiken in Excel kunt bewerken met Aspose.Cells voor .NET. U hebt bereiken gemaakt, ze gevuld met gegevens, de inhoud gekopieerd en uiteindelijk verwijderd, terwijl u ervoor zorgde dat uw Excel-bestand georganiseerd en overzichtelijk bleef. Excel, net als een bruisend café, draait om organisatie. Dus, of u nu gegevens voor een rapport beheert of uw persoonlijke budgetblad opfleurt, het beheersen van benoemde bereiken kan u helpen bij het ontwikkelen van efficiënte oplossingen. 

## Veelgestelde vragen

### Wat is Aspose.Cells?
Aspose.Cells is een .NET-bibliotheek die is ontworpen voor het programmatisch bewerken van Excel-bestanden.

### Kan ik meerdere benoemde bereiken tegelijk verwijderen?
Ja, u kunt door de verzameling benoemde bereiken heen lussen en ze indien nodig verwijderen.

### Is er een proefversie beschikbaar?
Ja, u kunt een gratis proefversie van Aspose.Cells downloaden [hier](https://releases.aspose.com/).

### Welke programmeertalen ondersteunt Aspose.Cells?
Het ondersteunt voornamelijk .NET-talen zoals C# en VB.NET.

### Waar kan ik terecht voor ondersteuning als ik problemen heb?
U kunt de [Aspose-ondersteuningsforum](https://forum.aspose.com/c/cells/9) voor hulp bij eventuele vragen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}