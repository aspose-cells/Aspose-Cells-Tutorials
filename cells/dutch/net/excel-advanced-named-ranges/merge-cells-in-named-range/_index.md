---
title: Cellen in benoemd bereik samenvoegen in Excel
linktitle: Cellen in benoemd bereik samenvoegen in Excel
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u cellen in een benoemd bereik samenvoegt met Aspose.Cells voor .NET in deze stapsgewijze tutorial. Ontdek hoe u Excel-rapporten opmaakt, stileert en automatiseert.
weight: 11
url: /nl/net/excel-advanced-named-ranges/merge-cells-in-named-range/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cellen in benoemd bereik samenvoegen in Excel

## Invoering

Wanneer u programmatisch met Excel-bestanden werkt, is een van de meest voorkomende taken die u tegen kunt komen het samenvoegen van cellen binnen een benoemd bereik. Of u nu het genereren van rapporten automatiseert, dashboards bouwt of gewoon grote datasets beheert, het samenvoegen van cellen is een essentiële techniek. In deze tutorial onderzoeken we hoe u cellen in een benoemd bereik samenvoegt met Aspose.Cells voor .NET, een krachtige bibliotheek waarmee ontwikkelaars Excel-bestanden kunnen bewerken zonder dat Microsoft Excel geïnstalleerd hoeft te zijn.

## Vereisten

Zorg ervoor dat u het volgende bij de hand heeft voordat u begint:

-  Aspose.Cells voor .NET: U kunt het downloaden van de[Aspose.Cells releasepagina](https://releases.aspose.com/cells/net/).
- .NET Framework op uw computer geïnstalleerd.
- Basiskennis van C#: Kennis van concepten zoals klassen, methoden en objecten is nuttig.

## Pakketten importeren

Voordat we beginnen met coderen, moet u de benodigde namespaces importeren. Deze namespaces geven u toegang tot de functionaliteit van de Aspose.Cells-bibliotheek.

```csharp
using System;
using System.IO;
using Aspose.Cells;
```

Nu we de vereisten en pakketten hebben besproken, kunnen we beginnen met het leukste gedeelte: coderen!

Hieronder leest u hoe u cellen in een benoemd bereik in een Excel-werkblad kunt samenvoegen met Aspose.Cells voor .NET.

## Stap 1: Maak een nieuwe werkmap

Het eerste wat we nodig hebben is een werkmap. Een werkmap is in Excel-termen het equivalent van een Excel-bestand. Laten we er een maken.

```csharp
// Een nieuwe werkmap maken.
Workbook wb1 = new Workbook();
```

Door een nieuwe werkmap te initialiseren, hebben we nu een leeg Excel-bestand dat klaar is om te worden bewerkt. Het is alsof we beginnen met een leeg canvas!

## Stap 2: Toegang tot het eerste werkblad

Elke werkmap bevat werkbladen, en in dit geval willen we met de eerste werken. Laten we die pakken!

```csharp
// Pak het eerste werkblad uit de werkmap.
Worksheet worksheet1 = wb1.Worksheets[0];
```

Beschouw het werkblad als de afzonderlijke tabbladen in een Excel-bestand waar de werkelijke gegevens zich bevinden. Standaard benaderen we het allereerste tabblad.

## Stap 3: Een cellenbereik maken

Nu we ons werkblad hebben, is het tijd om een bereik te maken. Een bereik verwijst naar een blok cellen, dat meerdere rijen en kolommen kan beslaan.

```csharp
//Maak een bereik.
Range mrange = worksheet1.Cells.CreateRange("D6", "I12");
```

Hier selecteren we cellen van D6 tot I12, een blok dat meerdere rijen en kolommen beslaat. We gaan dit bereik binnenkort samenvoegen!

## Stap 4: Geef het bereik een naam

Door een bereik een naam te geven, kunt u er later gemakkelijker naar verwijzen, vooral bij grote datasets.

```csharp
// Geef het bereik een naam.
mrange.Name = "TestRange";
```

Door dit bereik 'TestRange' te noemen, kunnen we het later in de code snel ophalen, zonder dat we de celcoördinaten opnieuw hoeven op te geven.

## Stap 5: Het cellenbereik samenvoegen

En nu de magie: het samenvoegen van de cellen binnen het bereik dat we zojuist hebben gecreëerd!

```csharp
// Voeg de cellen van het bereik samen.
mrange.Merge();
```

Deze stap voegt alle cellen van D6 tot I12 samen in één enkele cel. Perfect voor dingen als titels of samenvattingen!

## Stap 6: Het benoemde bereik ophalen

Zodra de cellen zijn samengevoegd, willen we misschien wat opmaak toepassen. Laten we eerst ons benoemde bereik ophalen.

```csharp
// Ontdek het bereik.
Range range1 = wb1.Worksheets.GetRangeByName("TestRange");
```

Als u het bereik op naam ophaalt, kunt u verdere bewerkingen uitvoeren, zoals het toevoegen van stijlen of het invoeren van gegevens.

## Stap 7: Definieer een stijl voor de samengevoegde cellen

Wat heb je aan een samengevoegde cel als hij er niet gepolijst uitziet? Laten we een stijlobject maken om de tekst uit te lijnen en een achtergrondkleur toe te passen.

```csharp
// Definieer een stijlobject.
Style style = wb1.CreateStyle();

// Stel de uitlijning in.
style.HorizontalAlignment = TextAlignmentType.Center;
style.VerticalAlignment = TextAlignmentType.Center;
style.Pattern = BackgroundType.Solid;
style.ForegroundColor = System.Drawing.Color.Aqua;
```

Hier lijnen we de tekst horizontaal en verticaal uit in het midden en stellen we een lichtblauwe (aqua) achtergrondkleur in. Stijlvol, toch?

## Stap 8: Pas de stijl toe op het bereik

Nadat u de stijl hebt gedefinieerd, is het tijd om deze toe te passen op het samengevoegde bereik.

```csharp
// Maak een StyleFlag-object.
StyleFlag flag = new StyleFlag();

// Zet het relatieve stijlkenmerk op AAN.
flag.HorizontalAlignment = true;
flag.VerticalAlignment = true;
flag.CellShading = true;

// Pas de stijl toe op het bereik.
range1.ApplyStyle(style, flag);
```

 De`StyleFlag` vertelt Aspose.Cells welke stijleigenschappen moeten worden toegepast: uitlijning, arcering, enz. Dit geeft u gedetailleerde controle over hoe de stijl wordt toegepast.

## Stap 9: Gegevens invoeren in het samengevoegde bereik

Wat is een geformatteerd bereik zonder inhoud? Laten we wat tekst toevoegen.

```csharp
// Voer gegevens in het bereik in.
range1[0, 0].PutValue("Welcome to Aspose APIs.");
```

Hiermee wordt de tekst "Welcome to Aspose APIs" in de eerste cel van ons samengevoegde bereik geplaatst. Wanneer de cel wordt samengevoegd, zal deze tekst alle cellen van D6 tot I12 beslaan.

## Stap 10: Sla het Excel-bestand op

Laten we tot slot de werkmap opslaan als Excel-bestand.

```csharp
// Sla het Excel-bestand op.
wb1.Save(dataDir + "outputMergeCellsInNamedRange.xlsx");
```

Hier wordt de werkmap opgeslagen met de naam 'outputMergeCellsInNamedRange.xlsx' in de door u opgegeven map.

## Conclusie

En daar heb je het! Je hebt cellen in een benoemd bereik succesvol samengevoegd, prachtige opmaak toegepast en zelfs wat gegevens ingevoerd, allemaal met Aspose.Cells voor .NET. Of je nu werkt aan het automatiseren van rapporten, het manipuleren van Excel-bestanden of gewoon nieuwe technieken leert, deze stapsgewijze handleiding zou je de basis moeten geven die je nodig hebt.

## Veelgestelde vragen

### Kan ik meerdere niet-aangrenzende bereiken samenvoegen in Aspose.Cells?  
Nee, u kunt alleen aangrenzende cellen samenvoegen in Aspose.Cells.

### Kan ik een samenvoegingsbewerking programmatisch ongedaan maken?  
 Zodra cellen zijn samengevoegd, kunt u ze weer samenvoegen met behulp van de`UnMerge()` methode in Aspose.Cells.

### Worden de gegevens in cellen verwijderd als ik ze samenvoeg?  
Als er vóór het samenvoegen gegevens in de cellen staan, blijven de gegevens uit de eerste cel van het bereik behouden.

### Kan ik verschillende stijlen toepassen op afzonderlijke cellen binnen een samengevoegd bereik?  
Nee, een samengevoegd bereik fungeert als één cel. U kunt dus geen verschillende stijlen toepassen op afzonderlijke cellen binnen het bereik.

### Hoe krijg ik toegang tot een samengevoegde cel nadat ik deze heb samengevoegd?  
Na het samenvoegen kunt u de samengevoegde cel nog steeds openen met behulp van de coördinaten in de linkerbovenhoek.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
