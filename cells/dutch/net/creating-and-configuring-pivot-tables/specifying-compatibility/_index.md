---
"description": "Leer hoe u draaitabellen in Excel bewerkt met Aspose.Cells voor .NET, inclusief gegevensupdates, compatibiliteitsinstellingen en celopmaak."
"linktitle": "Compatibiliteit van Excel-bestand programmatisch specificeren in .NET"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Compatibiliteit van Excel-bestand programmatisch specificeren in .NET"
"url": "/nl/net/creating-and-configuring-pivot-tables/specifying-compatibility/"
"weight": 23
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Compatibiliteit van Excel-bestand programmatisch specificeren in .NET

## Invoering

In de huidige datagedreven wereld is het programmatisch beheren en manipuleren van Excel-bestanden essentieel geworden voor veel ontwikkelaars. Als u met Excel in .NET werkt, is Aspose.Cells een krachtige bibliotheek waarmee u eenvoudig Excel-bestanden kunt maken, lezen, wijzigen en opslaan. Een belangrijke functie van deze bibliotheek is dat u de compatibiliteit van Excel-bestanden programmatisch kunt specificeren. In deze tutorial onderzoeken we hoe u Excel-bestanden kunt bewerken, met name gericht op het beheren van compatibiliteit met Aspose.Cells voor .NET. Aan het einde begrijpt u hoe u de compatibiliteit voor Excel-bestanden, met name draaitabellen, kunt instellen en tegelijkertijd gegevens kunt vernieuwen en beheren.

## Vereisten

Voordat u met de coderingsfase begint, moet u ervoor zorgen dat u over het volgende beschikt:

1. Basiskennis van C#: Omdat we code in C# gaan schrijven, is het beter om de tutorial te begrijpen als je bekend bent met de taal.
2. Aspose.Cells voor .NET-bibliotheek: u kunt deze downloaden van de [Aspose Cells-releasepagina](https://releases.aspose.com/cells/net/)Als u dat nog niet heeft gedaan, overweeg dan om eerst een gratis proefperiode te proberen om de functies te ontdekken.
3. Visual Studio: een IDE waarmee u effectief uw C#-code kunt schrijven en testen.
4. Voorbeeld Excel-bestand: Zorg ervoor dat u een voorbeeld Excel-bestand hebt, bij voorkeur een bestand met een draaitabel voor de demo. Voor ons voorbeeld gebruiken we `sample-pivot-table.xlsx`.

Nu deze voorwaarden vervuld zijn, kunnen we beginnen met het codeerproces.

## Pakketten importeren

Voordat u begint met het schrijven van uw applicatie, moet u de benodigde naamruimten in uw code opnemen om de Aspose.Cells-bibliotheek effectief te gebruiken. Hier leest u hoe u dat doet.

### Importeer Aspose.Cells-naamruimte

```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Pivot;
using System.Drawing;
```

Met deze coderegel krijgt u toegang tot alle klassen en methoden in de Aspose.Cells-bibliotheek.

Laten we het proces nu gedetailleerd uitleggen om ervoor te zorgen dat alles duidelijk en begrijpelijk is.

## Stap 1: Stel uw directory in

Allereerst moet u de map instellen waar uw Excel-bestanden zich bevinden. Het is belangrijk dat u het juiste bestandspad opgeeft.

```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
```

Hier vervangen `"Your Document Directory"` met het daadwerkelijke pad naar uw Excel-bestanden. Dit is de plek waar uw voorbeelddraaitabelbestand zou moeten staan.

## Stap 2: Laad het bron-Excelbestand

Vervolgens moeten we het Excel-bestand laden dat de voorbeelddraaitabel bevat. 

```csharp
// Bronbestand van Excel laden met voorbeeld draaitabel
Workbook wb = new Workbook(dataDir + "sample-pivot-table.xlsx");
```

In deze stap maken we een exemplaar van de `Workbook` klasse, die het opgegeven Excel-bestand laadt. 

## Stap 3: Toegang tot de werkbladen

Nu de werkmap is geladen, moet u het werkblad openen dat de draaitabelgegevens bevat.

```csharp
// Toegang tot het eerste werkblad dat draaitabelgegevens bevat
Worksheet dataSheet = wb.Worksheets[0];
```

Hier openen we het eerste werkblad met de draaitabel. Je kunt ook andere werkbladen doorlopen of specificeren op basis van je Excel-structuur.

## Stap 4: Celgegevens manipuleren

Vervolgens gaat u een aantal celwaarden in het werkblad wijzigen. 

### Stap 4.1: Cel A3 wijzigen

Laten we beginnen met het openen van cel A3 en het instellen van de waarde ervan.

```csharp
// Toegang tot cel A3 en de gegevens ervan instellen
Cells cells = dataSheet.Cells;
Cell cell = cells["A3"];
cell.PutValue("FooBar");
```

Met dit codefragment wordt cel A3 bijgewerkt met de waarde “FooBar”.

### Stap 4.2: Cel B3 wijzigen met een lange tekenreeks

Laten we nu een lange tekenreeks in cel B3 plaatsen die de standaard tekenlimiet van Excel overschrijdt.

```csharp
// Toegang tot cel B3, gegevens instellen
string longStr = "Very long text 1. very long text 2.... [continue your long string]";
cell = cells["B3"];
cell.PutValue(longStr);
```

Deze code is belangrijk omdat deze uw verwachtingen met betrekking tot gegevenslimieten aangeeft, vooral wanneer u werkt met compatibiliteitsinstellingen in Excel.

## Stap 5: Controleer de lengte van cel B3

Het is ook belangrijk om de lengte van de ingevoerde tekenreeks te bevestigen.

```csharp
// De lengte van de cel B3-string afdrukken
Console.WriteLine("Length of original data string: " + cell.StringValue.Length);
```

Dit is alleen ter verificatie, om te zien hoeveel tekens uw cel bevat.

## Stap 6: Andere celwaarden instellen

Nu gaan we meer cellen benaderen en een aantal waarden instellen.

```csharp
// Toegang tot cel C3 en het instellen van de gegevens
cell = cells["C3"];
cell.PutValue("closed");

// Toegang tot cel D3 en de gegevens ervan instellen
cell = cells["D3"];
cell.PutValue("2016/07/21");
```

Elk van deze fragmenten werkt meerdere extra cellen in het werkblad bij.

## Stap 7: Toegang tot de draaitabel

Vervolgens krijgt u toegang tot het tweede werkblad, dat bestaat uit de draaitabelgegevens.

```csharp
// Toegang tot het tweede werkblad dat een draaitabel bevat
Worksheet pivotSheet = wb.Worksheets[1];

// Toegang tot de draaitabel
PivotTable pivotTable = pivotSheet.PivotTables[0];
```

Met dit fragment kunt u de draaitabel bewerken voor compatibiliteitsinstellingen.

## Stap 8: Compatibiliteit instellen voor Excel 2003

Het is belangrijk om in te stellen of uw draaitabel compatibel is met Excel 2003. 

```csharp
// De eigenschap IsExcel2003Compatible geeft aan of de draaitabel compatibel is met Excel 2003 tijdens het vernieuwen van de draaitabel.
pivotTable.IsExcel2003Compatible = true;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

Dit is waar de echte transformatie begint. Door het instellen `IsExcel2003Compatible` naar `true`beperk je de tekenlengte tot 255 bij het vernieuwen.

## Stap 9: Controleer de lengte na het instellen van de compatibiliteit

Nadat u de compatibiliteit hebt ingesteld, bekijken we welke invloed dit op de gegevens heeft.

```csharp
// Controleer de waarde van cel B5 van het draaitabelblad.
Cell b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to True: " + b5.StringValue.Length);
```

Als de oorspronkelijke gegevens langer zijn dan 255 tekens, ziet u waarschijnlijk een uitvoer die het afkappingseffect bevestigt.

## Stap 10: Compatibiliteitsinstelling wijzigen

Laten we nu de compatibiliteitsinstelling wijzigen en opnieuw controleren.

```csharp
// Stel nu de eigenschap IsExcel2003Compatible in op false en vernieuw de database opnieuw.
pivotTable.IsExcel2003Compatible = false;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

Hierdoor behouden uw gegevens hun oorspronkelijke lengte, zonder de voorgaande beperkingen.

## Stap 11: Controleer de lengte opnieuw 

Laten we controleren of de gegevens nu correct de werkelijke lengte weergeven.

```csharp
// Nu wordt de oorspronkelijke lengte van de celgegevens afgedrukt. De gegevens zijn nu niet afgekapt.
b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to False: " + b5.StringValue.Length);
```

U zou moeten zien dat de uitvoer de verwijdering van de afkapping bevestigt.

## Stap 12: De cellen opmaken

Om de visuele ervaring te verbeteren, kunt u de cellen opmaken. 

```csharp
// Stel de rijhoogte en kolombreedte van cel B5 in en laat de tekst ervan doorlopen
pivotSheet.Cells.SetRowHeight(b5.Row, 100);
pivotSheet.Cells.SetColumnWidth(b5.Column, 65);
Style st = b5.GetStyle();
st.IsTextWrapped = true;
b5.SetStyle(st);
```

Deze coderegels zorgen ervoor dat de gegevens gemakkelijker te lezen zijn door de celafmetingen aan te passen en tekstomloop mogelijk te maken.

## Stap 13: Sla de werkmap op

Sla ten slotte uw werkmap op met de wijzigingen die u hebt aangebracht.

```csharp
// Werkmap opslaan in xlsx-formaat
wb.Save(dataDir + "SpecifyCompatibility_out.xlsx", SaveFormat.Xlsx);
```

Het kiezen van een geschikt bestandsformaat is cruciaal bij het opslaan van Excel-bestanden. `Xlsx` Het formaat wordt veel gebruikt en is compatibel met veel Excel-versies.

## Conclusie

Gefeliciteerd! Je hebt nu de compatibiliteitsinstellingen voor Excel-bestanden geprogrammeerd met Aspose.Cells voor .NET. In deze tutorial hebben we elke stap beschreven, van het instellen van je omgeving tot het aanpassen van de compatibiliteitsinstellingen voor draaitabellen. Als je ooit hebt gewerkt met gegevens die specifieke beperkingen of compatibiliteit vereisten, is dit een vaardigheid die je niet wilt vergeten.

## Veelgestelde vragen

### Wat is Aspose.Cells?  
Aspose.Cells is een .NET-bibliotheek waarmee ontwikkelaars naadloos Excel-bestanden kunnen maken, bewerken en converteren.

### Waarom is Excel-compatibiliteit belangrijk?  
Compatibiliteit met Excel is van cruciaal belang om ervoor te zorgen dat bestanden kunnen worden geopend en gebruikt in de beoogde versies van Excel, vooral als ze functies of indelingen bevatten die in eerdere versies niet werden ondersteund.

### Kan ik programmatisch draaitabellen maken met Aspose.Cells?  
Ja, u kunt draaitabellen programmatisch maken en bewerken met Aspose.Cells. De bibliotheek biedt verschillende methoden om gegevensbronnen, velden en functies toe te voegen die aan draaitabellen zijn gekoppeld.

### Hoe controleer ik de lengte van een tekenreeks in een Excel-cel?  
Je kunt de `StringValue` eigendom van een `Cell` object om de inhoud van de cel te verkrijgen en vervolgens de `.Length` eigenschap om de lengte van de tekenreeks te achterhalen.

### Kan ik de celopmaak aanpassen aan meer dan alleen de rijhoogte en -breedte?  
Absoluut! Aspose.Cells biedt uitgebreide celopmaak. Je kunt lettertypen, kleuren, randen, getalnotaties en nog veel meer wijzigen via de `Style` klas.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}