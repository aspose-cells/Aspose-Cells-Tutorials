---
"description": "Leer hoe je JSON programmatisch naar CSV converteert in .NET met Aspose.Cells. Volg onze stapsgewijze handleiding voor een naadloze datatransformatie."
"linktitle": "JSON programmatisch naar CSV converteren in .NET"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "JSON programmatisch naar CSV converteren in .NET"
"url": "/nl/net/converting-excel-files-to-other-formats/converting-json-to-csv/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# JSON programmatisch naar CSV converteren in .NET

## Invoering
In de digitale wereld van vandaag is het verwerken van gegevens in meerdere formaten gemeengoed geworden, en JSON (JavaScript Object Notation) is een van de meest gebruikte formaten voor gegevensuitwisseling. Maar wat gebeurt er als je die JSON moet omzetten naar een formaat dat toegankelijker is voor analyse, zoals CSV (Comma Separated Values)? Deze tutorial leidt je door het proces van het programmatisch converteren van JSON naar CSV met behulp van Aspose.Cells voor .NET, een gebruiksvriendelijke maar krachtige API voor spreadsheetmanipulatie. 
## Vereisten
Voordat we de code induiken, is het essentieel om ervoor te zorgen dat je alle benodigde componenten hebt en een basiskennis hebt van de tools die we gaan gebruiken. Laten we eens schetsen wat je nodig hebt:
- Aspose.Cells voor .NET: Dit is de primaire bibliotheek die we zullen gebruiken voor het converteren van JSON naar CSV. U kunt [download het hier](https://releases.aspose.com/cells/net/).
- Visual Studio: U hebt een Integrated Development Environment (IDE) zoals Visual Studio nodig om de .NET-code te schrijven en uit te voeren.
- .NET Framework: Zorg ervoor dat u .NET Framework hebt geïnstalleerd. Aspose.Cells is compatibel met zowel .NET Core als .NET Framework.
- Basiskennis van C#: Hoewel deze gids elk onderdeel van de code behandelt, is het handig als u enigszins bekend bent met C#.
## Pakketten importeren
Om Aspose.Cells in uw .NET-project te gebruiken, moet u eerst de bibliotheek installeren. Dit kunt u doen via NuGet Package Manager:
1. Visual Studio openen.
2. Ga naar Extra > NuGet Package Manager > NuGet-pakketten beheren voor oplossing.
3. Zoek naar Aspose.Cells en installeer de nieuwste versie.
Zorg ervoor dat u na de installatie de volgende naamruimten in uw code opneemt:
```csharp
using Aspose.Cells.Utility;
using System;
using System.IO;
```
Nu alles is ingesteld, gaan we de code stap voor stap uitleggen, zodat u kunt zien hoe eenvoudig u een JSON-bestand kunt converteren naar een CSV-bestand met behulp van Aspose.Cells.
## Stap 1: Lees het JSON-bestand
Het eerste wat we moeten doen, is de JSON-gegevens uit een bestand lezen. We gaan ervan uit dat je al een JSON-bestand hebt (laten we het een JSON-bestand noemen). `SampleJson.json`) opgeslagen in een directory op uw systeem.
Je kunt de `File.ReadAllText()` methode in C# om de inhoud van het JSON-bestand in een tekenreeks te lezen.
```csharp
// Bronmap
string sourceDir = "Your Document Directory";
// JSON-bestand lezen
string str = File.ReadAllText(sourceDir + "SampleJson.json");
```

Deze stap is cruciaal omdat je de ruwe JSON-gegevens nodig hebt om het conversieproces te starten. Door deze als een string te lezen, bereid je deze voor op verwerking door Aspose.Cells.
## Stap 2: Een lege werkmap maken
Aspose.Cells werkt voornamelijk met werkmappen (Excel-bestanden). Om JSON-gegevens te importeren, moet u eerst een lege werkmap maken waarin deze gegevens worden ingevoegd.
```csharp
// Lege werkmap maken
Workbook workbook = new Workbook();
```
Hier initialiseert u een lege werkmap die uiteindelijk de CSV-gegevens zal bevatten. Zie het als het aanmaken van een lege spreadsheet in Excel die binnenkort wordt gevuld met uw JSON-gegevens.
## Stap 3: Toegang tot de cellen in de werkmap
Nu we een lege werkmap hebben, moeten we toegang krijgen tot de cellen ervan. `Cells` verzameling in Aspose.Cells vertegenwoordigt alle cellen in een werkblad waarin u uw JSON-gegevens plaatst.
```csharp
// Cellen ophalen
Cells cells = workbook.Worksheets[0].Cells;
```
Met dit codefragment wordt het eerste werkblad (werkblad op index 0) geselecteerd en wordt de bijbehorende `Cells` verzameling. Deze cellen zijn als het raster van een spreadsheet waaraan gegevens worden toegevoegd.
## Stap 4: JsonLayoutOptions instellen
Aspose.Cells biedt verschillende aanpassingsopties voor hoe uw JSON-gegevens worden geïmporteerd. Hier definiëren we `JsonLayoutOptions` om aan te geven hoe Aspose arrays, numerieke gegevens en objecttitels moet verwerken.
```csharp
// JsonLayoutOptions instellen
JsonLayoutOptions importOptions = new JsonLayoutOptions();
importOptions.ConvertNumericOrDate = true;
importOptions.ArrayAsTable = true;
importOptions.IgnoreArrayTitle = true;
importOptions.IgnoreObjectTitle = true;
```

- ConvertNumericOrDate: Converteert automatisch numerieke of datumtekenreekswaarden.
- ArrayAsTable: behandel arrays in JSON als tabellen in de werkmap.
- IgnoreArrayTitle en IgnoreObjectTitle: met deze opties worden titels voor arrays en objecten genegeerd. Zo wordt ervoor gezorgd dat alleen de onbewerkte gegevens worden geïmporteerd.
## Stap 5: Importeer de JSON-gegevens
Zodra de lay-outopties zijn ingesteld, is het tijd om de JSON-gegevens in te voeren. `JsonUtility.ImportData()` De methode doet hier het zware werk en voegt de JSON-gegevens in de cellen van de werkmap in.
```csharp
JsonUtility.ImportData(str, cells, 0, 0, importOptions);
```
Deze methode heeft meerdere parameters nodig:
- `str`: De JSON-string die we in stap 1 lezen.
- `cells`: De celverzameling waar de gegevens worden geplaatst.
- `0, 0`:Dit zijn de rij- en kolomindexen die aangeven waar de gegevens moeten beginnen (d.w.z. de linkerbovenhoek).
- `importOptions`: De lay-outopties die we in stap 4 hebben ingesteld.
## Stap 6: Sla de werkmap op als CSV
Nu de JSON-gegevens in de werkmap staan, kunnen we de werkmap eenvoudig opslaan als een CSV-bestand. CSV is een eenvoudig, lichtgewicht formaat voor het opslaan van tabelgegevens, waardoor het perfect is voor data-analyse.
```csharp
// Uitvoermap
string outputDir = "Your Document Directory";
// Werkboek opslaan
workbook.Save(outputDir + @"SampleJson_out.csv");
```
In deze stap slaan we de werkmap op als een CSV-bestand. U geeft het pad en de bestandsnaam op (`SampleJson_out.csv`) waar de CSV wordt opgeslagen.
## Stap 7: Bevestig het proces
Om te controleren of alles naar behoren is verlopen, kunnen we een bevestigingsbericht in de console weergeven.
```csharp
Console.WriteLine("ConvertJsonToCsv executed successfully.");
```
Een eenvoudig succesbericht bevestigt dat het proces soepel is verlopen.
## Conclusie
Het converteren van JSON naar CSV met Aspose.Cells voor .NET is een eenvoudig maar krachtig proces. Met slechts een paar regels code kunt u complexe JSON-gegevens omzetten naar een toegankelijker CSV-formaat. Of u nu werkt met arrays, objecten of numerieke gegevens, Aspose.Cells maakt het eenvoudig om het conversieproces aan uw behoeften aan te passen.
## Veelgestelde vragen
### Kan Aspose.Cells grote JSON-bestanden verwerken?
Ja, Aspose.Cells is ontworpen om grote datasets efficiënt te verwerken, waardoor het geschikt is voor de verwerking van grote JSON-bestanden zonder prestatieproblemen.
### Hoe kan ik de CSV-uitvoer aanpassen?
U kunt de CSV-uitvoer aanpassen door de `JsonLayoutOptions` of door de opmaak van de werkmap te manipuleren voordat u deze als CSV opslaat.
### Is er een manier om bepaalde gegevens uit de JSON uit te sluiten tijdens de conversie?
Ja, door de JSON aan te passen of aangepaste codelogica te gebruiken vóór het importeren, kunt u specifieke gegevensvelden uitsluiten of filteren.
### Ondersteunt Aspose.Cells andere bestandsformaten dan CSV?
Absoluut! Aspose.Cells ondersteunt een breed scala aan formaten, waaronder Excel (XLS, XLSX), PDF, HTML en nog veel meer.
### Hoe kan ik Aspose.Cells gratis uitproberen?
Je kan [download hier een gratis proefversie](https://releases.aspose.com/) om alle functies te testen voordat u tot aankoop overgaat.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}