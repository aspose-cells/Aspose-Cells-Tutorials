---
"description": "Leer hoe u HTML-tekenreekswaarden uit Excel-cellen naar een DataTable exporteert met Aspose.Cells voor .NET in een eenvoudige, stapsgewijze zelfstudie."
"linktitle": "Exporteer HTML-tekenreekswaarde van cellen naar DataTable in Excel"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Exporteer HTML-tekenreekswaarde van cellen naar DataTable in Excel"
"url": "/nl/net/excel-data-sorting-exporting/export-html-string-value-of-cells-to-datatable-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Exporteer HTML-tekenreekswaarde van cellen naar DataTable in Excel

## Invoering

Wanneer u met Excel-bestanden in een .NET-omgeving werkt, moet u mogelijk informatie uit cellen halen, niet alleen als platte tekst, maar als HTML-strings. Dit kan erg handig zijn wanneer u met RTF-gegevens werkt of wanneer u de opmaak wilt behouden. In deze handleiding laat ik u zien hoe u de HTML-stringwaarde van cellen kunt exporteren naar een DataTable met behulp van Aspose.Cells voor .NET. 

## Vereisten

Voordat we de code induiken, controleren we of alles wat je nodig hebt aanwezig is. Hier is een korte checklist:

1. Basiskennis van C# en .NET: Voordat u begint met coderen, moet u ervoor zorgen dat u bekend bent met C#-programmering en de basisprincipes van het .NET Framework.
2. Aspose.Cells voor .NET: Als u dat nog niet hebt gedaan, moet u Aspose.Cells voor .NET installeren. U kunt een gratis proefversie downloaden van [hier](https://releases.aspose.com/).
3. Visual Studio of IDE naar keuze: Stel uw omgeving in om C#-code te schrijven. Visual Studio wordt aanbevolen vanwege de uitgebreide functionaliteit en het gebruiksgemak.
4. Voorbeeld Excel-bestand: U hebt een voorbeeld Excel-bestand nodig (`sampleExportTableAsHtmlString.xlsx`) om mee te werken. Zorg ervoor dat het in een toegankelijke map staat.
5. NuGet Package Manager: Zorg ervoor dat u toegang hebt tot NuGet Package Manager in uw project om de Aspose.Cells-bibliotheek eenvoudig toe te voegen.

Nu we aan deze voorwaarden voldoen, kunnen we aan de slag met coderen!

## Pakketten importeren

Voordat we met Aspose.Cells kunnen werken, moeten we de benodigde pakketten importeren. Dit houdt meestal in dat we het NuGet-pakket van Aspose.Cells aan je project toevoegen. Zo doe je dat:

### Open NuGet-pakketbeheer

Klik in Visual Studio met de rechtermuisknop op uw project in Solution Explorer en selecteer NuGet-pakketten beheren.

### Zoeken naar Aspose.Cells

Typ in de NuGet-pakketbeheerder `Aspose.Cells` in de zoekbalk.

### Het pakket installeren

Zodra je Aspose.Cells hebt gevonden, klik je op de knop Installeren. Hiermee voeg je de bibliotheek toe aan je project en kun je deze importeren in je code.

### Importeer de naamruimte

Voeg de volgende using -richtlijn bovenaan uw codebestand toe:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Data;
```

Nu we alles hebben ingesteld, duiken we in het stapsgewijze proces voor het exporteren van HTML-tekenreekswaarden van een Excel-bestand naar een DataTable. 

## Stap 1: Definieer de bronmap

Je begint met het definiëren van de map waarin je Excel-voorbeeldbestand is opgeslagen. Dit is cruciaal, omdat het je applicatie vertelt waar het bestand te vinden is. Hier is de code daarvoor:

```csharp
string sourceDir = "Your Document Directory";
```

Zorg ervoor dat u vervangt `"Your Document Directory"` met het daadwerkelijke pad naar uw Excel-bestand.

## Stap 2: Laad het voorbeeld-Excelbestand

De volgende stap is het laden van de Excel-werkmap. U gebruikt de `Workbook` klasse van Aspose.Cells om dit te doen. Zo laadt u het bestand:

```csharp
Workbook wb = new Workbook(sourceDir + "sampleExportTableAsHtmlString.xlsx");
```

Met deze eenvoudige coderegel wordt de werkmap geïnitialiseerd en het opgegeven Excel-bestand geladen.

## Stap 3: Toegang tot het eerste werkblad

Zodra de werkmap is geladen, wilt u toegang krijgen tot het specifieke werkblad met de gegevens waarin u geïnteresseerd bent. Over het algemeen begint u met het eerste werkblad:

```csharp
Worksheet ws = wb.Worksheets[0];
```

Hier werken we met het eerste werkblad (index 0). Zorg ervoor dat je gegevens op het juiste werkblad staan.

## Stap 4: Opties voor exporttabel opgeven

Om te bepalen hoe de gegevens worden geëxporteerd, moet u het volgende instellen: `ExportTableOptions`In dit geval wilt u ervoor zorgen dat de kolomnamen niet worden geëxporteerd en wilt u dat de celgegevens worden geëxporteerd als HTML-strings:

```csharp
ExportTableOptions opts = new ExportTableOptions();
opts.ExportColumnName = false;
opts.ExportAsHtmlString = true;
```

Met deze configuratie kunt u de rijke opmaak van uw celgegevens behouden bij het exporteren.

## Stap 5: Cellen exporteren naar DataTable

Nu komt het cruciale deel, namelijk het daadwerkelijk exporteren van de gegevens. Met behulp van de `ExportDataTable` Met deze methode kunt u de gegevens uit het werkblad in een `DataTable`Zo doe je dat:

```csharp
DataTable dt = ws.Cells.ExportDataTable(0, 0, 3, 3, opts);
```

Met deze code wordt een opgegeven cellenbereik (van rij 0, kolom 0 tot rij 3, kolom 3) naar een DataTable geëxporteerd met behulp van de eerder opgegeven opties.

## Stap 6: De HTML-tekenreekswaarde afdrukken

Laten we tot slot de HTML-tekenreekswaarde van een specifieke cel in de DataTable afdrukken om te zien wat we hebben geëxporteerd. Als u bijvoorbeeld de waarde van de derde rij en de tweede kolom wilt afdrukken, doet u het volgende:

```csharp
Console.WriteLine(dt.Rows[2][1].ToString());
```

Met deze regel wordt de gewenste HTML-tekenreeks uit de DataTable in de console afgedrukt. 

## Conclusie 

En voilà! Je hebt met succes HTML-tekenreekswaarden uit cellen in een Excel-bestand geëxporteerd naar een DataTable met Aspose.Cells voor .NET. Deze mogelijkheid verrijkt niet alleen je vaardigheden in dataverwerking, maar verbreedt ook je mogelijkheden bij het werken met opgemaakte content rechtstreeks vanuit Excel-bestanden. 

## Veelgestelde vragen

### Kan ik Aspose.Cells gebruiken voor andere bestandsindelingen dan Excel?  
Ja, Aspose.Cells is primair bedoeld voor Excel, maar Aspose biedt andere bibliotheken voor verschillende formaten.

### Heb ik een licentie nodig voor Aspose.Cells?  
Ja, voor productiegebruik is een geldige licentie vereist. U kunt een tijdelijke licentie krijgen. [hier](https://purchase.aspose.com/temporary-license/).

### Wat als mijn Excel-bestand formules bevat? Worden deze correct geëxporteerd?  
Ja, Aspose.Cells kan formules verwerken en bij het exporteren worden deze geëvalueerd op basis van de resulterende waarden.

### Is het mogelijk om de exportopties te wijzigen?  
Absoluut! Je kunt het aanpassen `ExportTableOptions` afgestemd op uw specifieke behoeften.

### Waar kan ik meer gedetailleerde documentatie voor Aspose.Cells vinden?  
Uitgebreide documentatie is beschikbaar [hier](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}