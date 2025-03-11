---
title: Wijzig cirkeldiagram
linktitle: Wijzig cirkeldiagram
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Ontgrendel de kracht van Aspose.Cells voor .NET om moeiteloos uw Excel-cirkeldiagrammen aan te passen. Volg deze tutorial voor stapsgewijze begeleiding.
weight: 16
url: /nl/net/manipulating-chart-types/modify-pie-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wijzig cirkeldiagram

## Invoering

Heb je je ooit afgevraagd hoe je die cirkeldiagrammen in je Excel-sheets kunt opfleuren? Cirkeldiagrammen kunnen een fantastische manier zijn om gegevens te visualiseren en je publiek betrokken en geïnformeerd te houden. Soms vertellen die diagrammen echter niet direct het verhaal dat je wilt vertellen. Daar komt Aspose.Cells voor .NET om de hoek kijken. Met deze krachtige bibliotheek kun je Excel-bestanden programmatisch bewerken, waardoor je de tools krijgt die je nodig hebt om je cirkeldiagrammen tot in het kleinste detail aan te passen. In deze tutorial duiken we diep in het aanpassen van een cirkeldiagram met Aspose.Cells. Of het nu gaat om het wijzigen van gegevenslabels of het aanpassen van de esthetiek van het diagram.

## Vereisten

Voordat we dieper ingaan op het aanpassen van cirkeldiagrammen, moet u aan een aantal voorwaarden voldoen:

- Basiskennis van C#: Een fundamenteel begrip van C#-programmering helpt u de cursus gemakkelijk te volgen.
- Aspose.Cells voor .NET: U moet de Aspose.Cells-bibliotheek geïnstalleerd hebben. Of u nu besluit de volledige versie te gebruiken of kiest voor een gratis proefversie, zorg ervoor dat deze klaar is voor gebruik.
- Visual Studio of een andere C# IDE: u hebt een omgeving nodig om uw C#-code te schrijven en uit te voeren.
-  Excel-voorbeeldbestand: voor deze tutorial is een voorbeeld-Excel-bestand met de naam`sampleModifyPieChart.xlsx` zal worden gebruikt.

 U kunt de Aspose.Cells-bibliotheek downloaden[hier](https://releases.aspose.com/cells/net/).

## Pakketten importeren

De eerste stap in onze reis is het importeren van de benodigde pakketten in ons C#-project. Dit is hoe u dat kunt doen:

## Stel uw project in

Om te beginnen opent u uw C# IDE (Visual Studio wordt sterk aanbevolen) en maakt u een nieuw project:

1. Open Visual Studio.
2. Selecteer 'Een nieuw project maken'.
3. Kies een C# consoletoepassing.
4.  Geef uw project een naam (bijv.`ModifyPieChartDemo`).
5. Klik op Maken.

## Aspose.Cells installeren

Zodra uw project klaar is, is het tijd om de Aspose.Cells-bibliotheek toe te voegen. U kunt deze installeren met NuGet:

1. Klik in de “Solution Explorer” met de rechtermuisknop op uw project.
2. Selecteer NuGet-pakketten beheren.
3. Ga naar het tabblad Bladeren.
4. Zoeken naar Aspose.Cells.
5. Klik op Installeren en accepteer eventuele licentieovereenkomsten.

Nu u de bibliotheek hebt geïnstalleerd, kunt u de benodigde naamruimten in uw code importeren.

## Naamruimten importeren

 Bovenaan je`Program.cs` bestand, importeer de volgende naamruimten:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

Nu dat gedaan is, kunnen we verder met de daadwerkelijke code!

## Stap 1: Definieer invoer- en uitvoermappen

Laten we beginnen met het definiëren van de mappen voor uw invoer- en uitvoerbestanden. Hier specificeert u waar uw Excel-bestand zich bevindt en waar u het gewijzigde bestand wilt opslaan.

 In jouw`Main` methode, typ de volgende code:

```csharp
// Uitvoermap
string outputDir = "Your Output Directory Path";

// Bron directory
string sourceDir = "Your Document Directory Path";
```

 Zorg ervoor dat u vervangt`Your Output Directory Path` En`Your Document Directory Path` met de werkelijke paden op uw systeem.

## Stap 2: Open de bestaande werkmap

 Vervolgens moeten we het Excel-bestand openen dat het cirkeldiagram bevat dat u wilt wijzigen. Gebruik hiervoor de`Workbook` klas:

```csharp
// Open het bestaande bestand.
Workbook workbook = new Workbook(sourceDir + "sampleModifyPieChart.xlsx");
```

 In dit fragment maken we een nieuwe`Workbook` object en het laden van ons Excel-bestand erin.

## Stap 3: Toegang tot het werkblad

Laten we nu eens duiken in het specifieke blad dat het cirkeldiagram bevat. We gaan ervan uit dat het cirkeldiagram op het tweede werkblad staat (index 1):

```csharp
// Haal het ontwerpersdiagram op het tweede blad.
Worksheet sheet = workbook.Worksheets[1];
```

 Door toegang te krijgen tot de`Worksheets` verzameling, kunnen we naar het specifieke blad gaan dat we nodig hebben.

## Stap 4: Haal de grafiek op

Nu zijn we klaar om toegang te krijgen tot de grafiek zelf. Ervan uitgaande dat er maar één grafiek op dat werkblad staat, kunnen we deze direct ophalen:

```csharp
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

Hier pakken we de eerste grafiek uit het opgegeven werkblad.

## Stap 5: Toegang tot gegevenslabels

Nu komt het spannende gedeelte: het aanpassen van de datalabels op het cirkeldiagram. Laten we de datalabels van de dataseries benaderen:

```csharp
// Haal de gegevenslabels op in de gegevensreeks van het derde gegevenspunt.
Aspose.Cells.Charts.DataLabels datalabels = chart.NSeries[0].Points[2].DataLabels;
```

Met deze regel richten we ons specifiek op de gegevenslabels voor het derde punt van onze gegevensreeks. 

## Stap 6: Wijzig de labeltekst

Vervolgens is het tijd om te veranderen wat dat label zegt. Voor ons voorbeeld gaan we het updaten naar "Verenigd Koninkrijk, 400K":

```csharp
// Wijzig de tekst van het label.
datalabels.Text = "United Kingdom, 400K";
```

Zo, we hebben het etiket bijgewerkt! 

## Stap 7: Sla de werkmap op

Nu we de wijzigingen hebben aangebracht, slaan we de aangepaste werkmap op. 

```csharp
// Sla het Excel-bestand op.
workbook.Save(outputDir + "outputModifyPieChart.xlsx");
```

Met deze regel wordt de werkmap opgeslagen in de opgegeven uitvoermap. 

## Stap 8: Bevestig de uitvoering

Tot slot sturen we een bevestigingsbericht om te controleren of alles soepel is verlopen:

```csharp
Console.WriteLine("ModifyPieChart executed successfully.");
```

Dit geeft u de zekerheid dat uw wijzigingen zijn doorgevoerd zoals verwacht.

# Conclusie

Daar heb je het! Met slechts een paar eenvoudige stappen heb je succesvol een cirkeldiagram aangepast met Aspose.Cells voor .NET. Deze krachtige bibliotheek maakt het niet alleen eenvoudig om Excel-bestanden te manipuleren, maar stelt je ook in staat om je datavisualisaties te personaliseren voor maximale impact. Als je datapresentaties in je werk verwerkt, zal het zeker lonen om tijd te investeren in het leren gebruiken van Aspose.Cells. Dus ga je gang, experimenteer met die diagrammen en zie hoe je je data tot leven kunt brengen!

# Veelgestelde vragen

### Wat is Aspose.Cells voor .NET?  
Aspose.Cells voor .NET is een krachtige bibliotheek waarmee u programmatisch Excel-bestanden kunt maken, bewerken en converteren zonder dat u Microsoft Excel nodig hebt.

### Kan ik ook andere grafieken dan cirkeldiagrammen aanpassen?  
Absoluut! Aspose.Cells ondersteunt verschillende grafiektypen, waaronder staaf-, lijn- en vlakdiagrammen, wat flexibele datavisualisatie mogelijk maakt.

### Bestaat er een gratis versie van Aspose.Cells?  
Jazeker! Aspose biedt een gratis proefversie aan waarmee u de bibliotheek kunt testen voordat u tot aankoop overgaat.

### Waar kan ik ondersteuning vinden voor Aspose.Cells?  
U kunt ondersteuning krijgen op de Aspose-forums, waar communityleden en Aspose-medewerkers u kunnen helpen.

### Moet ik Microsoft Excel geïnstalleerd hebben om Aspose.Cells te kunnen gebruiken?  
Nee, Aspose.Cells werkt onafhankelijk van Microsoft Excel. U hoeft het niet op uw systeem te installeren.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
