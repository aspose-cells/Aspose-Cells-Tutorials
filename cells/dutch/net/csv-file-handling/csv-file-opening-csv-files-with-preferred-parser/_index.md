---
"description": "Leer hoe je CSV-bestanden opent en parseert met aangepaste parsers in Aspose.Cells voor .NET. Verwerk tekst en datums moeiteloos. Perfect voor ontwikkelaars."
"linktitle": "CSV-bestanden openen met de voorkeursparser"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "CSV-bestanden openen met de voorkeursparser"
"url": "/nl/net/csv-file-handling/csv-file-opening-csv-files-with-preferred-parser/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# CSV-bestanden openen met de voorkeursparser

## Invoering
Bij het werken met CSV-bestanden wil je soms verschillende gegevenstypen verwerken met aangepaste parsers. Deze tutorial laat je zien hoe je CSV-bestanden opent met een voorkeursparser met Aspose.Cells voor .NET. Of je nu tekst, datums of andere aangepaste formaten wilt verwerken, deze handleiding leidt je door elke stap met een duidelijke uitleg.
## Vereisten
Voordat we in de code duiken, bespreken we eerst de essentiële onderdelen die je nodig hebt om aan de slag te gaan.
1. Aspose.Cells voor .NET-bibliotheek: Zorg ervoor dat u de Aspose.Cells-bibliotheek hebt geïnstalleerd. U kunt deze downloaden. [hier](https://releases.aspose.com/cells/net/)U kunt ook de gratis proefperiode gebruiken [hier](https://releases.aspose.com/).
2. .NET-ontwikkelomgeving: Visual Studio wordt aanbevolen, maar elke .NET-compatibele IDE werkt ook.
3. Basiskennis van C#: in deze tutorial wordt ervan uitgegaan dat u bekend bent met C# en objectgeoriënteerd programmeren.
## Pakketten importeren
Om Aspose.Cells te gebruiken, moet u de benodigde naamruimten bovenaan uw C#-bestand importeren:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Nu we alles onder de knie hebben, gaan we kijken hoe u een CSV-bestand opent met een voorkeursparser, die verschillende gegevensformaten, zoals tekst en datums, verwerkt.
## Stap 1: Aangepaste parsers definiëren
Om verschillende gegevenstypen te verwerken, zoals tekst of specifieke datumnotaties, moet u aangepaste parsers definiëren. In Aspose.Cells implementeren aangepaste parsers de `ICustomParser` interface.
### 1.1 Een tekstparser maken
Deze parser verwerkt gewone tekstwaarden. De opmaak wordt niet gewijzigd, dus de waarde wordt ongewijzigd geretourneerd.
```csharp
class TextParser : ICustomParser
{
    public object ParseObject(string value)
    {
        return value;
    }
    public string GetFormat()
    {
        return "";
    }
}
```
De `ParseObject` De methode retourneert simpelweg de invoerwaarde. Het is alsof je zegt: "Verander niets, geef me gewoon de tekst!"
### 1.2 Een datumparser maken
Voor datums moet u ervoor zorgen dat de CSV-gegevens correct worden geparseerd in `DateTime` objecten. Zo maak je een datumparser:
```csharp
class DateParser : ICustomParser
{
    public object ParseObject(string value)
    {
        DateTime myDate = DateTime.ParseExact(value, "dd/MM/yyyy", 
            System.Globalization.CultureInfo.InvariantCulture);
        return myDate;
    }
    public string GetFormat()
    {
        return "dd/MM/yyyy";
    }
}
```
In deze parser gebruiken we `ParseExact` om ervoor te zorgen dat de datum correct wordt geïnterpreteerd op basis van een vooraf gedefinieerd formaat (`"dd/MM/yyyy"`). Op deze manier worden alle datums in uw CSV-bestand met dit formaat zonder problemen verwerkt.
## Stap 2: Laadopties configureren
Vervolgens moet u configureren hoe het CSV-bestand wordt geladen. Dit doet u met behulp van de `TxtLoadOptions` klasse, waarmee u parseeropties kunt opgeven, waaronder codering en aangepaste parsers.
### 2.1 Laadopties instellen
We beginnen met het initialiseren van de `TxtLoadOptions` en het definiëren van sleutelparameters zoals de scheidingsteken en de codering:
```csharp
TxtLoadOptions oTxtLoadOptions = new TxtLoadOptions(LoadFormat.Csv);
oTxtLoadOptions.Separator = Convert.ToChar(",");
oTxtLoadOptions.Encoding = Encoding.UTF8;
oTxtLoadOptions.ConvertDateTimeData = true;
```
- Scheidingsteken: Hiermee definieert u het teken dat wordt gebruikt om waarden in het CSV-bestand te scheiden (in dit geval komma's).
- Codering: We gebruiken UTF-8-codering om een breed scala aan tekens te verwerken.
- ConvertDateTimeData: Als u dit op true instelt, worden datumwaarden automatisch omgezet naar `DateTime` voorwerpen indien mogelijk.
### 2.2 Aangepaste parsers toepassen
Vervolgens wijzen we de parsers die we eerder hebben gemaakt toe om de waarden in de CSV te verwerken:
```csharp
oTxtLoadOptions.PreferredParsers = new ICustomParser[] 
{ 
    new TextParser(), 
    new DateParser() 
};
```
Dit vertelt Aspose.Cells om de `TextParser` voor algemene tekstwaarden en de `DateParser` voor alle datumvelden die het in het CSV-bestand tegenkomt.
## Stap 3: Het CSV-bestand laden en lezen
Nu de laadopties zijn geconfigureerd, kunt u het CSV-bestand in een `Aspose.Cells.Workbook` voorwerp.
### 3.1 Het CSV-bestand laden
We laden het CSV-bestand door het bestandspad en de geconfigureerde `TxtLoadOptions` naar de `Workbook` constructeur:
```csharp
string sourceDir = "Your Document Directory";
Workbook oExcelWorkBook = new Aspose.Cells.Workbook(sourceDir + "samplePreferredParser.csv", oTxtLoadOptions);
```
Met deze stap worden uw CSV-gegevens omgezet in een volledig functionele Excel-werkmap, waarbij elke waarde wordt geparseerd volgens uw voorkeursregels.
## Stap 4: Toegang tot en weergave van celgegevens
Zodra het CSV-bestand in de werkmap is geladen, kunt u met de gegevens aan de slag. U kunt bijvoorbeeld het type en de waarde van specifieke cellen afdrukken.
### 4.1 Cel A1 ophalen en weergeven
Laten we de eerste cel (A1) ophalen en de waarde en het type ervan weergeven:
```csharp
Cell oCell = oExcelWorkBook.Worksheets[0].Cells["A1"];
Console.WriteLine("A1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
Hier, de `Type` eigenschap geeft het gegevenstype weer (zoals `String` of `DateTime`), En `DisplayStringValue` geeft u de geformatteerde waarde.
### 4.2 Cel B1 ophalen en weergeven
Op dezelfde manier kunnen we een andere cel ophalen en weergeven, bijvoorbeeld B1:
```csharp
oCell = oExcelWorkBook.Worksheets[0].Cells["B1"];
Console.WriteLine("B1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
U kunt dit proces herhalen voor zoveel cellen als u wilt onderzoeken.
## Stap 5: Sla de werkmap op
Nadat u met de gegevens hebt gewerkt, kunt u de werkmap opslaan in een nieuw bestand. Aspose.Cells maakt dit eenvoudig met een eenvoudige `Save` methode:
```csharp
string outputDir = "Your Document Directory";
oExcelWorkBook.Save(outputDir + "outputsamplePreferredParser.xlsx");
```
Hiermee slaat u de werkmap op als een Excel-bestand, waarbij alle opmaak en gegevensverwerking die u hebt toegepast, behouden blijven.
## Conclusie
Het openen van CSV-bestanden met een voorkeursparser in Aspose.Cells voor .NET is een flexibele en krachtige manier om verschillende gegevenstypen te verwerken. Door aangepaste parsers te maken en laadopties te configureren, kunt u ervoor zorgen dat uw CSV-bestanden precies zo worden geparseerd als u wilt, of het nu gaat om tekst, datums of andere aangepaste formaten. Met deze tutorial bent u nu in staat om complexere scenario's voor dataparsing in uw projecten aan te kunnen.
## Veelgestelde vragen
### Wat is het doel van aangepaste parsers in Aspose.Cells voor .NET?
Met aangepaste parsers kunt u definiëren hoe specifieke gegevenstypen, zoals tekst of datums, moeten worden geparseerd bij het laden van een CSV-bestand.
### Kan ik een ander scheidingsteken gebruiken in het CSV-bestand?
Ja, u kunt elk teken opgeven als scheidingsteken in de `TxtLoadOptions.Separator` eigendom.
### Hoe ga ik om met codering in Aspose.Cells bij het laden van een CSV?
U kunt de `Encoding` eigendom van `TxtLoadOptions` naar elk coderingsschema zoals UTF-8, ASCII, etc.
### Wat gebeurt er als de datumnotatie in het CSV-bestand anders is?
U kunt de specifieke datumnotatie definiëren met behulp van een aangepaste parser. Zo bent u verzekerd van een correcte verwerking van datumwaarden.
### Kan ik de werkmap in andere formaten opslaan?
Ja, met Aspose.Cells kunt u de werkmap opslaan in verschillende formaten, zoals XLSX, CSV, PDF en meer.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}