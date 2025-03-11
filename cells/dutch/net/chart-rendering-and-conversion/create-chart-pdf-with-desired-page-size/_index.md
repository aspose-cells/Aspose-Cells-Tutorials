---
title: Maak een PDF-grafiek met de gewenste paginagrootte
linktitle: Maak een PDF-grafiek met de gewenste paginagrootte
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Maak een PDF met uw Excel-grafiek met Aspose.Cells voor .NET. Leer hoe met deze stapsgewijze handleiding.
weight: 12
url: /nl/net/chart-rendering-and-conversion/create-chart-pdf-with-desired-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak een PDF-grafiek met de gewenste paginagrootte

## Invoering

Het maken van visueel aantrekkelijke en informatieve grafieken is essentieel voor datarepresentatie in verschillende velden. Of u nu te maken hebt met verkoopgegevens, prestatiemetingen of een ander type informatie, de mogelijkheid om grafieken van hoge kwaliteit te produceren geeft uw bevindingen diepte en helderheid. Als u met .NET-toepassingen werkt, is Aspose.Cells een krachtige bibliotheek die het verwerken van Excel-documenten en het genereren van grafieken een fluitje van een cent maakt. In deze tutorial leiden we u door het proces van het maken van een PDF van een grafiek uit een Excel-bestand met een gewenste paginagrootte.

## Vereisten

Voordat u in de code duikt, moet u aan een aantal voorwaarden voldoen om een soepele ervaring te garanderen:

### Basiskennis van C# en .NET

U hebt een fundamenteel begrip van C#-programmering en het .NET-framework nodig. Dit zal u helpen de structuur van de code te begrijpen die u in deze gids tegenkomt.

### Aspose.Cells voor .NET

Zorg ervoor dat je Aspose.Cells voor .NET hebt geïnstalleerd. Je kunt alle details vinden op de[Aspose.Cells-documentatie](https://reference.aspose.com/cells/net/). 

### Ontwikkelomgeving

 Stel uw ontwikkelomgeving in. Dit kan Visual Studio zijn of een andere IDE die C# ondersteunt. Download en installeer de Aspose.Cells-bibliotheek van de[downloadpagina](https://releases.aspose.com/cells/net/).

### Voorbeeld Excel-bestand

U hebt een voorbeeld-Excelbestand nodig dat ten minste één grafiek bevat. U kunt een voorbeeldbestand maken of downloaden om te gebruiken in deze tutorial.

## Pakketten importeren

Om te beginnen met Aspose.Cells moet u de benodigde namespaces importeren in uw C#-applicatie. Dit is hoe u dat doet:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
```

Met deze naamruimten krijgt u toegang tot de klassen en methoden die u nodig hebt om Excel-werkmappen en hun inhoud te bewerken.

Nu we alle vereisten hebben geregeld, kunnen we het proces opsplitsen in gedetailleerde stappen.

## Stap 1: Uitvoer- en bronmappen instellen

Om te beginnen moet u definiëren waar de PDF-uitvoer wordt opgeslagen en waar uw Excel-brondocument zich bevindt.

```csharp
//Uitvoermap
string outputDir = "Your Output Directory";

//Bron directory
string sourceDir = "Your Document Directory";
```

Zorg ervoor dat u "Your Output Directory" en "Your Document Directory" vervangt door de werkelijke paden op uw systeem. Dit bepaalt waar Aspose de gegenereerde PDF opslaat en waar het het Excel-bestand vindt.

## Stap 2: Laad het voorbeeld-Excelbestand

Vervolgens moet u het Excel-bestand laden dat de grafiek bevat. Dit doet u als volgt:

```csharp
//Laad een voorbeeld-Excel-bestand met de grafiek.
Workbook wb = new Workbook(sourceDir + "sampleCreateChartPDFWithDesiredPageSize.xlsx");
```

 De`Workbook` klasse is essentieel voor de interactie met uw Excel-document. Zorg ervoor dat het pad correct naar uw Excel-bestand verwijst. Een fout hier voorkomt dat de rest van de code wordt uitgevoerd.

## Stap 3: Toegang tot het eerste werkblad

Zodra de werkmap is geladen, is de volgende stap het openen van het werkblad met de gewenste grafiek.

```csharp
//Open het eerste werkblad.
Worksheet ws = wb.Worksheets[0];
```

 In Aspose.Cells worden werkbladen geïndexeerd vanaf nul, dus`Worksheets[0]` verwijst naar het eerste blad.

## Stap 4: Toegang tot de eerste grafiek

Laten we nu de grafiek openen die u wilt exporteren naar een PDF. Deze stap gaat ervan uit dat uw werkblad ten minste één grafiek bevat.

```csharp
//Open de eerste grafiek in het werkblad.
Chart ch = ws.Charts[0];
```

Ook hierbij krijgt u toegang tot de eerste grafiek in het werkblad. Zorg ervoor dat de structuur van uw werkblad geschikt is voor deze aanpak.

## Stap 5: Maak een PDF met de gewenste paginagrootte

Ten slotte is het tijd om de PDF te maken van de grafiek met een opgegeven paginagrootte. Hier is de magische regel code die het allemaal doet:

```csharp
//Maak een pdf-grafiek met de gewenste paginagrootte.
ch.ToPdf(outputDir + "outputCreateChartPDFWithDesiredPageSize.pdf", 7, 7, PageLayoutAlignmentType.Center, PageLayoutAlignmentType.Center);
```

In deze code:
- Het PDF-bestand wordt opgeslagen in de uitvoermap die u eerder hebt opgegeven.
-  De cijfers`7, 7` geven respectievelijk de breedte en hoogte van het gewenste paginaformaat weer.
- PageLayoutAlignmentType.Center zorgt ervoor dat de grafiek gecentreerd op de pagina wordt weergegeven.

## Stap 6: Bevestigingsbericht

Om uzelf (en anderen) te laten weten dat alles soepel is verlopen, voegt u aan het einde van uw code een bevestigingsbericht toe:

```csharp
Console.WriteLine("CreateChartPDFWithDesiredPageSize executed successfully.");
```

Zodra het proces is voltooid, verschijnt dit bericht in het consolevenster. Dit bericht geeft aan dat uw PDF-bestand zonder problemen is gemaakt.

## Conclusie

Gefeliciteerd! U hebt zojuist geleerd hoe u Aspose.Cells voor .NET kunt gebruiken om een PDF te maken van een grafiek in een Excel-bestand. Deze krachtige bibliotheek stroomlijnt het proces van het manipuleren van Excel-documenten en het genereren van visuele representaties van gegevens, waardoor u uren aan handmatige opmaak bespaart. Zorg ervoor dat u de overvloed aan andere functies verkent die Aspose.Cells biedt naast alleen PDF-generatie: u weet nooit wat uw projecten verder kan verbeteren!

## Veelgestelde vragen

### Waarvoor wordt Aspose.Cells voor .NET gebruikt?  
Aspose.Cells voor .NET wordt gebruikt voor het programmatisch maken, bewerken en converteren van Excel-documenten in .NET-toepassingen.

### Kan ik Aspose.Cells gratis gebruiken?  
 Ja, Aspose.Cells biedt een[gratis proefperiode](https://releases.aspose.com/) voor evaluatiedoeleinden.

### Is er een manier om mijn proefperiode te verlengen na de initiële periode?  
 U kunt een aanvraag indienen voor een[tijdelijke licentie](https://purchase.aspose.com/temporary-license/) voor uitgebreide tests.

### Wat als ik problemen tegenkom of vragen heb?  
 U kunt hulp zoeken bij de Aspose-community op hun[ondersteuningsforum](https://forum.aspose.com/c/cells/9).

### Hoe kan ik Aspose.Cells kopen?  
 U kunt Aspose.Cells kopen bij de[aankooppagina](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
