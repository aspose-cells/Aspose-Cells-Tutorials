---
title: Afbeelding toevoegen aan grafiek
linktitle: Afbeelding toevoegen aan grafiek
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u eenvoudig afbeeldingen aan Excel-grafieken kunt toevoegen met Aspose.Cells voor .NET. Verbeter uw grafieken en presentaties in slechts een paar eenvoudige stappen.
weight: 11
url: /nl/net/inserting-controls-in-charts/add-picture-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Afbeelding toevoegen aan grafiek

## Invoering

Bent u saaie grafieken die een persoonlijke touch missen zat? Wilt u leren hoe u uw Excel-visuals kunt opfleuren door afbeeldingen toe te voegen? Dan heeft u geluk! In deze tutorial duiken we in de wereld van Aspose.Cells voor .NET en leren we hoe u afbeeldingen toevoegt aan grafieken in Excel. Pak dus uw favoriete kop koffie en laten we beginnen!

## Vereisten

Voordat we in de details van het coderen duiken, zijn er een paar voorwaarden waaraan je moet voldoen om het proces soepel te kunnen volgen:

- Visual Studio: Dit is waar u uw .NET-code schrijft en uitvoert. Zorg ervoor dat u het hebt geïnstalleerd.
-  Aspose.Cells voor .NET: U hebt deze bibliotheek nodig om met Excel-bestanden te werken. U kunt[download het hier](https://releases.aspose.com/cells/net/).
- Basiskennis van C#: Ik leid je door de code, maar als je de basisbeginselen van C# kent, wordt alles duidelijker.

### Installatiestappen

1. Aspose.Cells installeren: U kunt Aspose.Cells toevoegen aan uw Visual Studio-project via NuGet Package Manager. Doe dit door te navigeren naar Tools > NuGet Package Manager > Manage NuGet Packages for Solution en te zoeken naar "Aspose.Cells". Klik op Install.
2. Uw project instellen: maak een nieuw C# consoletoepassingsproject in Visual Studio.

## Pakketten importeren

Zodra je alles hebt ingesteld, is de volgende stap het importeren van de benodigde pakketten in je project. Dit is hoe je dat doet:

### Importeer de vereiste naamruimten

Bovenaan uw C#-codebestand moet u de volgende naamruimten importeren:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

Hiermee vertelt u uw programma: "Hé! Ik ga deze coole functies van Aspose.Cells gebruiken."

Nu we aan de voorwaarden hebben voldaan, kunnen we het proces opsplitsen in kleinere stappen. 

## Stap 1: Definieer uw mappen

Allereerst moeten we de paden voor onze invoer- en uitvoerbestanden instellen. Deze stap is cruciaal omdat we moeten weten waar we ons bestaande Excel-bestand kunnen vinden en waar we het gewijzigde bestand kunnen opslaan.

```csharp
//Bron directory
string sourceDir = "Your Document Directory/";

//Uitvoermap
string outputDir = "Your Output Directory/";
```

 Vervangen`Your Document Directory` En`Your Output Directory` met echte paden op uw computer. 

## Stap 2: Laad de bestaande werkmap

Laten we nu het bestaande Excel-bestand laden waar we onze afbeelding aan de grafiek willen toevoegen.

```csharp
// Open het bestaande bestand.
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

Deze code opent de werkmap, zodat u deze kunt bewerken.

## Stap 3: Bereid de beeldstroom voor

Voordat we de afbeelding toevoegen, moeten we de afbeelding die we in de grafiek willen invoegen, lezen. 

```csharp
// Voeg een afbeeldingsbestand toe aan de stream.
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

Zorg ervoor dat de afbeelding in de opgegeven map is opgeslagen.

## Stap 4: Richt de grafiek

Laten we nu specificeren aan welke grafiek we onze afbeelding gaan toevoegen. In dit voorbeeld richten we ons op de eerste grafiek op het eerste werkblad.

```csharp
// Haal het ontwerpersdiagram op het tweede blad.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

U kunt elk werkblad openen door de index dienovereenkomstig te wijzigen.

## Stap 5: Voeg de afbeelding toe aan de grafiek

Nu u de grafiek hebt geselecteerd, kunt u de afbeelding toevoegen! 

```csharp
// Voeg een nieuwe afbeelding toe aan de grafiek.
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

 Hier,`50` En`50` zijn de X- en Y-coördinaten waar de afbeelding wordt geplaatst, en`200` is de breedte en hoogte van de afbeelding.

## Stap 6: Pas de lijnopmaak van de afbeelding aan

Wil je wat flair toevoegen aan je foto? Je kunt de rand aanpassen! Zo doe je dat:

```csharp
// Selecteer het lijnformaattype van de afbeelding.
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

// Stel de streepjesstijl in.
lineformat.DashStyle = MsoLineDashStyle.Solid;

// Stel de lijndikte in.
lineformat.Weight = 4;    
```

Met dit fragment kunt u kiezen hoe de rand eruitziet en hoe dik deze is. Kies een stijl die past bij uw presentatie!

## Stap 7: Sla de aangepaste werkmap op

Na al dat harde werk kunnen we uw wijzigingen opslaan door de volgende regel code uit te voeren:

```csharp
// Sla het Excel-bestand op.
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

Uw afbeelding is nu succesvol geïntegreerd in de grafiek en uw uitvoerbestand is klaar om te bekijken!

## Stap 8: Geef succes aan

Tot slot kunt u een eenvoudig bericht toevoegen om te bevestigen dat uw bewerking succesvol is verlopen:

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## Conclusie

In deze tutorial hebben we onderzocht hoe u een beetje persoonlijkheid kunt toevoegen aan uw Excel-grafieken door afbeeldingen toe te voegen met Aspose.Cells voor .NET. Met slechts een paar eenvoudige stappen kunt u uw presentaties van alledaags naar gedenkwaardig verheffen. Dus, waar wacht u nog op? Probeer het eens en laat uw grafieken schitteren!

## Veelgestelde vragen

### Kan ik meerdere afbeeldingen aan één grafiek toevoegen?
 Ja! U kunt de`AddPictureInChart` Herhaal deze methode meerdere keren om zoveel afbeeldingen toe te voegen als u wilt.

### Welke afbeeldingsformaten ondersteunt Aspose.Cells?
Aspose.Cells ondersteunt verschillende afbeeldingsformaten, waaronder PNG, JPEG, BMP en GIF.

### Kan ik de positie van de afbeelding aanpassen?
 Zeker! De X- en Y-coördinaten in de`AddPictureInChart` methode maakt nauwkeurige positionering mogelijk.

### Is Aspose.Cells gratis te gebruiken?
Aspose.Cells biedt een gratis proefperiode, maar voor volledige functies is een licentie vereist. U kunt de prijzen vinden[hier](https://purchase.aspose.com/buy).

### Waar kan ik meer voorbeelden vinden?
 Bekijk de[Aspose.Cells-documentatie](https://reference.aspose.com/cells/net/) voor meer gedetailleerde voorbeelden en functionaliteiten.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
