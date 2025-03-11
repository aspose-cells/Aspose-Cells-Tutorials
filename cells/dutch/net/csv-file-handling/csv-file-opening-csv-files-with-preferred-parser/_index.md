---
title: CSV-bestanden openen met de voorkeursparser
linktitle: CSV-bestanden openen met de voorkeursparser
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u CSV-bestanden opent en parseert met aangepaste parsers in Aspose.Cells voor .NET. Verwerk tekst en datums moeiteloos. Perfect voor ontwikkelaars.
weight: 11
url: /nl/net/csv-file-handling/csv-file-opening-csv-files-with-preferred-parser/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# CSV-bestanden openen met de voorkeursparser

## Invoering
Bij het werken met CSV-bestanden wilt u soms verschillende gegevenstypen verwerken met aangepaste parsers. Deze tutorial begeleidt u bij het openen van CSV-bestanden met een voorkeursparser met behulp van Aspose.Cells voor .NET. Of u nu tekst, datums of andere aangepaste formaten wilt verwerken, deze gids begeleidt u door elke stap met een duidelijke uitleg.
## Vereisten
Voordat we in de code duiken, bespreken we eerst de essentiële onderdelen die je nodig hebt om aan de slag te gaan.
1.  Aspose.Cells voor .NET-bibliotheek: zorg dat u de Aspose.Cells-bibliotheek hebt geïnstalleerd. U kunt deze downloaden[hier](https://releases.aspose.com/cells/net/) . U kunt ook de gratis proefperiode gebruiken[hier](https://releases.aspose.com/).
2. .NET-ontwikkelomgeving: Visual Studio wordt aanbevolen, maar elke .NET-compatibele IDE is ook geschikt.
3. Basiskennis van C#: in deze tutorial wordt ervan uitgegaan dat u bekend bent met C# en objectgeoriënteerd programmeren.
## Pakketten importeren
Om Aspose.Cells te gebruiken, moet u de benodigde naamruimten boven aan uw C#-bestand importeren:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Nu we alles hebben uitgelegd, gaan we kijken hoe u een CSV-bestand opent met een favoriete parser die verschillende gegevensformaten, zoals tekst en datums, verwerkt.
## Stap 1: Aangepaste parsers definiëren
 Om verschillende gegevenstypen te verwerken, zoals tekst of specifieke datumnotaties, moet u aangepaste parsers definiëren. In Aspose.Cells implementeren aangepaste parsers de`ICustomParser` interface.
### 1.1 Een tekstparser maken
Deze parser verwerkt gewone tekstwaarden. Het wijzigt de opmaak niet, dus de waarde wordt geretourneerd zoals deze is.
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
 De`ParseObject` methode retourneert simpelweg de invoerwaarde. Het is alsof je zegt: "Verander niets, geef me gewoon de tekst!"
### 1.2 Een datumparser maken
 Voor datums moet u ervoor zorgen dat de CSV-gegevens correct worden geparseerd in`DateTime` objecten. Zo maakt u een datumparser:
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
 In deze parser gebruiken we`ParseExact` om ervoor te zorgen dat de datum correct wordt geïnterpreteerd op basis van een vooraf gedefinieerde notatie (`"dd/MM/yyyy"`). Op deze manier worden alle datums in uw CSV-bestand met dit formaat zonder problemen verwerkt.
## Stap 2: Laadopties configureren
 Vervolgens moet u configureren hoe het CSV-bestand wordt geladen. Dit doet u met behulp van de`TxtLoadOptions` klasse, waarmee u parseeropties kunt opgeven, waaronder codering en aangepaste parsers.
### 2.1 Laadopties instellen
 We beginnen met het initialiseren van de`TxtLoadOptions` en het definiëren van sleutelparameters zoals de scheidingsteken en de codering:
```csharp
TxtLoadOptions oTxtLoadOptions = new TxtLoadOptions(LoadFormat.Csv);
oTxtLoadOptions.Separator = Convert.ToChar(",");
oTxtLoadOptions.Encoding = Encoding.UTF8;
oTxtLoadOptions.ConvertDateTimeData = true;
```
- Scheidingsteken: Hiermee definieert u het teken dat wordt gebruikt om waarden in het CSV-bestand te scheiden (in dit geval een komma).
- Codering: We gebruiken UTF-8-codering om een breed scala aan tekens te verwerken.
-  ConvertDateTimeData: Als u dit op true instelt, worden datumwaarden automatisch geconverteerd naar`DateTime` voorwerpen indien mogelijk.
### 2.2 Aangepaste parsers toepassen
Vervolgens wijzen we de parsers die we eerder hebben gemaakt toe om de waarden in de CSV te verwerken:
```csharp
oTxtLoadOptions.PreferredParsers = new ICustomParser[] 
{ 
    new TextParser(), 
    new DateParser() 
};
```
 Dit vertelt Aspose.Cells om de`TextParser` voor algemene tekstwaarden en de`DateParser`voor alle datumvelden die het in het CSV-bestand tegenkomt.
## Stap 3: Laad en lees het CSV-bestand
 Nu de laadopties zijn geconfigureerd, kunt u het CSV-bestand in een`Aspose.Cells.Workbook` voorwerp.
### 3.1 Het CSV-bestand laden
 We laden het CSV-bestand door het bestandspad en de geconfigureerde`TxtLoadOptions` naar de`Workbook` constructeur:
```csharp
string sourceDir = "Your Document Directory";
Workbook oExcelWorkBook = new Aspose.Cells.Workbook(sourceDir + "samplePreferredParser.csv", oTxtLoadOptions);
```
Met deze stap worden uw CSV-gegevens omgezet in een volledig functionele Excel-werkmap, waarbij elke waarde wordt geparseerd volgens uw voorkeursregels.
## Stap 4: Toegang tot en weergave van celgegevens
Zodra de CSV in de werkmap is geladen, kunt u beginnen met werken met de gegevens. U wilt bijvoorbeeld het type en de waarde van specifieke cellen afdrukken.
### 4.1 Cel A1 ophalen en weergeven
Laten we de eerste cel (A1) ophalen en de waarde en het type ervan weergeven:
```csharp
Cell oCell = oExcelWorkBook.Worksheets[0].Cells["A1"];
Console.WriteLine("A1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
 Hier, de`Type` eigenschap toont het gegevenstype (zoals`String` of`DateTime` ), En`DisplayStringValue` geeft u de geformatteerde waarde.
### 4.2 Cel B1 ophalen en weergeven
Op dezelfde manier kunnen we een andere cel ophalen en weergeven, bijvoorbeeld B1:
```csharp
oCell = oExcelWorkBook.Worksheets[0].Cells["B1"];
Console.WriteLine("B1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
kunt dit proces herhalen voor zoveel cellen als u wilt inspecteren.
## Stap 5: Sla de werkmap op
 Nadat u met de gegevens hebt gewerkt, wilt u de werkmap mogelijk opslaan in een nieuw bestand. Aspose.Cells maakt dit eenvoudig met een eenvoudige`Save` methode:
```csharp
string outputDir = "Your Document Directory";
oExcelWorkBook.Save(outputDir + "outputsamplePreferredParser.xlsx");
```
Hiermee wordt de werkmap opgeslagen als een Excel-bestand, waarbij alle opmaak en gegevensverwerking die u hebt toegepast, behouden blijven.
## Conclusie
CSV-bestanden openen met een voorkeursparser in Aspose.Cells voor .NET is een flexibele en krachtige manier om verschillende gegevenstypen te verwerken. Door aangepaste parsers te maken en laadopties te configureren, kunt u ervoor zorgen dat uw CSV-bestanden precies worden geparseerd zoals u dat wilt, of u nu met tekst, datums of andere aangepaste formaten werkt. Met deze tutorial bent u nu uitgerust om complexere scenario's voor het parseren van gegevens in uw projecten te verwerken.
## Veelgestelde vragen
### Wat is het doel van aangepaste parsers in Aspose.Cells voor .NET?
Met aangepaste parsers kunt u definiëren hoe specifieke gegevenstypen, zoals tekst of datums, moeten worden geparseerd bij het laden van een CSV-bestand.
### Kan ik een ander scheidingsteken gebruiken in het CSV-bestand?
 Ja, u kunt elk teken opgeven als scheidingsteken in de`TxtLoadOptions.Separator` eigendom.
### Hoe ga ik om met codering in Aspose.Cells bij het laden van een CSV?
 U kunt de`Encoding` eigendom van`TxtLoadOptions` naar elk coderingsschema zoals UTF-8, ASCII, enz.
### Wat gebeurt er als de datumnotatie in het CSV-bestand afwijkt?
U kunt de specifieke datumnotatie definiëren met behulp van een aangepaste parser, zodat de datumwaarden correct worden geparseerd.
### Kan ik de werkmap in andere formaten opslaan?
Ja, met Aspose.Cells kunt u de werkmap opslaan in verschillende formaten, zoals XLSX, CSV, PDF en meer.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
