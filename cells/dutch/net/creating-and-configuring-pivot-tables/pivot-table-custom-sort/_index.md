---
"description": "Leer hoe u draaitabellen programmatisch sorteert in .NET met Aspose.Cells. Een stapsgewijze handleiding voor het instellen, configureren, sorteren en opslaan van resultaten als Excel- en PDF-bestanden."
"linktitle": "Draaitabel aangepast sorteren programmatisch in .NET"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Draaitabel aangepast sorteren programmatisch in .NET"
"url": "/nl/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/"
"weight": 29
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Draaitabel aangepast sorteren programmatisch in .NET

## Invoering
Als het gaat om werken met Excel in een .NET-omgeving, springt één bibliotheek er echt uit: Aspose.Cells. Vind je het niet geweldig als een tool je in staat stelt om spreadsheets programmatisch te bewerken? Dat is precies wat Aspose.Cells doet! In de tutorial van vandaag duiken we diep in de wereld van draaitabellen en laten we je zien hoe je aangepaste sortering programmatisch kunt implementeren met behulp van deze veelzijdige bibliotheek.
## Vereisten
Voordat we de mouwen opstropen en aan de code beginnen, moet je ervoor zorgen dat je een paar dingen op orde hebt:
1. Visual Studio: Je hebt een werkende versie van Visual Studio nodig. Het is de speeltuin waar alle magie gebeurt.
2. .NET Framework: Kennis van .NET-programmering is essentieel. Of je nu een .NET Core- of .NET Framework-fanaat bent, je kunt aan de slag.
3. Aspose.Cells-bibliotheek: U moet de Aspose.Cells-bibliotheek installeren. U kunt deze downloaden via de [Downloadlink](https://releases.aspose.com/cells/net/) en voeg het toe aan uw project.
4. Basiskennis van draaitabellen: Hoewel u geen expert hoeft te zijn, is een beetje kennis over de werking van draaitabellen nuttig voor deze tutorial.
5. Voorbeeld Excel-bestand: Heb een voorbeeld Excel-bestand met de naam `SamplePivotSort.xlsx` klaar in uw werkmap voor testen.
## Pakketten importeren
Zodra je alle vereisten hebt gesorteerd, is de eerste stap het importeren van de benodigde pakketten. Voeg hiervoor de volgende regels bovenaan je code toe:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
Dit pakket biedt alle functionaliteit die u nodig hebt voor het bewerken van Excel-bestanden met Aspose.Cells.

Oké, laten we beginnen met het leukste gedeelte! We gaan het proces van het maken van een draaitabel en het toepassen van aangepaste sortering opsplitsen in beheersbare stappen.
## Stap 1: De werkmap instellen
Om te beginnen, moeten we onze werkmap opzetten. Zo doe je dat:
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
In deze stap initialiseren we een nieuwe `Workbook` instantie met het pad naar ons Excel-bestand. Dit fungeert als het canvas waarop onze draaitabel tot leven komt.
## Stap 2: Toegang tot het werkblad
Vervolgens moeten we het werkblad openen waaraan we onze draaitabel gaan toevoegen.
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
Hier pakken we het eerste werkblad in onze werkmap en roepen de `PivotTableCollection`Met deze verzameling kunnen we alle draaitabellen in dit werkblad beheren.
## Stap 3: Maak uw eerste draaitabel
Nu is het tijd om onze draaitabel te maken.
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
We voegen een nieuwe draaitabel toe aan ons werkblad en specificeren het gegevensbereik en de locatie ervan. "E3" geeft aan waar we onze draaitabel willen laten beginnen. Vervolgens verwijzen we naar deze nieuwe draaitabel met behulp van de index.
## Stap 4: Draaitabelinstellingen configureren
Laten we onze draaitabel configureren! Dit betekent dat we aspecten zoals eindtotalen en veldindelingen moeten beheren.
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
We zorgen ervoor dat er geen eindtotalen voor rijen en kolommen worden weergegeven, wat de gegevens overzichtelijker maakt. Vervolgens voegen we het eerste veld toe aan het rijgebied, waardoor automatisch sorteren en oplopend sorteren mogelijk worden.
## Stap 5: Kolom en gegevensvelden toevoegen
Zodra de rijen zijn ingesteld, voegen we de kolommen en gegevensvelden toe.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
We voegen het tweede veld toe als kolom en formatteren het als een datum. Opnieuw schakelen we automatisch sorteren en oplopende volgorde in om alles overzichtelijk te houden. Ten slotte moeten we het derde veld toevoegen aan ons gegevensgebied:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## Stap 6: Vernieuw en bereken de draaitabel
Nadat u alle benodigde velden hebt toegevoegd, controleren we of uw draaitabel actueel en gereed is.
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
Met deze methoden worden de gegevens vernieuwd en opnieuw berekend. Zo weet u zeker dat alles up-to-date is en correct wordt weergegeven in uw draaitabel.
## Stap 7: Aangepaste sortering op basis van rijveldwaarden
Laten we het wat aantrekkelijker maken door de draaitabel te sorteren op basis van specifieke waarden, zoals 'Zeevruchten'.
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
We herhalen het proces door nog een draaitabel te maken en deze op dezelfde manier in te stellen als de eerste. We kunnen deze nu verder aanpassen:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## Stap 8: Extra sorteeraanpassingenLaten we een andere sorteermethode proberen op basis van een specifieke datum:
```csharp
// Een extra draaitabel toevoegen voor sorteren op datum
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// Herhaal de rij- en kolominstellingen op dezelfde manier als in de vorige stappen
```
U doorloopt gewoon hetzelfde proces en maakt een derde draaitabel met sorteercriteria die zijn afgestemd op uw behoeften.
## Stap 9: Sla het werkboek op. Tijd om al het harde werk dat we hebben verricht, op te slaan!
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
Hier slaat u de werkmap op als een Excel-bestand en een PDF. `PdfSaveOptions` zorgt voor een betere opmaak, zodat elk blad na de conversie op een aparte pagina wordt weergegeven.
## Stap 10: Rond afRond het geheel af door de gebruiker te laten weten dat alles goed is.
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## Conclusie
Je hebt nu geleerd hoe je de kracht van Aspose.Cells kunt benutten om draaitabellen in je .NET-applicaties te maken en aan te passen. Van de eerste installatie tot aangepaste sortering, elke stap zorgt voor een naadloze ervaring. Of je nu jaarlijkse verkoopgegevens moet presenteren of voorraadstatistieken moet bijhouden, deze vaardigheden komen goed van pas!
## Veelgestelde vragen
### Wat is een draaitabel?
Een draaitabel is een hulpmiddel voor gegevensverwerking in Excel waarmee u gegevens kunt samenvatten en analyseren. Zo kunt u op flexibele wijze eenvoudig inzichten verkrijgen.
### Hoe installeer ik Aspose.Cells?
U kunt het installeren via NuGet in Visual Studio of het rechtstreeks downloaden van de [Downloadlink](https://releases.aspose.com/cells/net/).
### Bestaat er een proefversie van Aspose.Cells?
Ja! U kunt het gratis uitproberen door naar de [Link naar gratis proefperiode](https://releases.aspose.com/).
### Kan ik meerdere velden in een draaitabel sorteren?
Absoluut! U kunt meerdere velden toevoegen en sorteren op basis van uw wensen.
### Waar kan ik ondersteuning voor Aspose.Cells vinden?
De community is behoorlijk actief en je kunt vragen stellen op hun forum [hier](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}