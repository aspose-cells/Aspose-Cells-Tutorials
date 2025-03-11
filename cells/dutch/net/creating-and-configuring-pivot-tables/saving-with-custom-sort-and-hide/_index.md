---
title: Draaitabellen opslaan met aangepaste sortering en verbergen in .NET
linktitle: Draaitabellen opslaan met aangepaste sortering en verbergen in .NET
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u draaitabellen met aangepaste sortering en het verbergen van rijen kunt opslaan met Aspose.Cells voor .NET. Stapsgewijze handleiding met praktische voorbeelden inbegrepen.
weight: 26
url: /nl/net/creating-and-configuring-pivot-tables/saving-with-custom-sort-and-hide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Draaitabellen opslaan met aangepaste sortering en verbergen in .NET

## Invoering
In de wereld van data-analyse zijn draaitabellen een van de krachtigste tools voor het samenvatten, analyseren en presenteren van data in een verteerbaar formaat. Als u met .NET werkt en op zoek bent naar een eenvoudige manier om draaitabellen te manipuleren, met name om ze op te slaan met aangepaste sortering en specifieke rijen te verbergen, dan bent u hier aan het juiste adres! Vandaag pakken we de techniek van het opslaan van draaitabellen met Aspose.Cells voor .NET uit. Deze gids leidt u door alles heen, van vereisten tot praktische voorbeelden, zodat u bent uitgerust om soortgelijke taken zelf uit te voeren. Dus laten we er meteen induiken!
## Vereisten
Voordat u zich verdiept in de details van het coderen, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:
1. Visual Studio: Idealiter wilt u een solide IDE om uw .NET-projecten te verwerken. Visual Studio is een geweldige keuze.
2.  Aspose.Cells voor .NET: U hebt toegang nodig tot de bibliotheek van Aspose om Excel-bestanden programmatisch te beheren. U kunt[download Aspose.Cells voor .NET hier](https://releases.aspose.com/cells/net/).
3. Basiskennis van C#: Kennis van de basisconcepten van programmeren en de syntaxis van C# zorgt ervoor dat het proces soepeler verloopt.
4.  Voorbeeld Excel-bestand: We gebruiken een voorbeeldbestand met de naam`PivotTableHideAndSortSample.xlsx`Zorg ervoor dat dit bestand zich in de aangewezen documentmap bevindt.
Zodra u uw ontwikkelomgeving hebt ingesteld en uw voorbeeldbestand gereed is, bent u klaar!
## Pakketten importeren
Nu we de vereisten hebben aangevinkt, kunnen we de benodigde pakketten importeren. Gebruik in uw C#-bestand de volgende richtlijn om Aspose.Cells op te nemen:
```csharp
using System;
using Aspose.Cells.Pivot;
```
Met deze richtlijn krijgt u toegang tot de klassen en methoden die worden geleverd door de Aspose.Cells-bibliotheek. Zorg ervoor dat u Aspose.Cells.dll hebt toegevoegd aan uw projectreferenties.
## Stap 1: De werkmap instellen
Het eerste wat we moeten doen, is onze werkmap laden. Het volgende codefragment bereikt dat:
```csharp
// Mappen voor bron- en uitvoerbestanden
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
// Laad de werkmap
Workbook workbook = new Workbook(sourceDir + "PivotTableHideAndSortSample.xlsx");
```
 In deze stap definieert u de mappen waarin uw bron- en uitvoerbestanden worden opgeslagen.`Workbook`constructor laadt uw bestaande Excel-bestand, zodat u het kunt bewerken.
## Stap 2: Toegang tot het werkblad en de draaitabel
Laten we nu het specifieke werkblad in de werkmap openen en de draaitabel selecteren waarmee we willen werken.
```csharp
// Toegang tot het eerste werkblad
Worksheet worksheet = workbook.Worksheets[0];
// Toegang tot de eerste draaitabel in het werkblad
var pivotTable = worksheet.PivotTables[0];
```
 In dit fragment,`Worksheets[0]` selecteert het eerste werkblad in uw Excel-document en`PivotTables[0]` haalt de eerste draaitabel op. Hiermee kunt u de exacte draaitabel selecteren die u wilt wijzigen.
## Stap 3: Sorteer draaitabelrijen
Vervolgens implementeren we aangepaste sortering om onze gegevens te ordenen. Meer specifiek sorteren we scores in aflopende volgorde.
```csharp
// Het eerste rijveld in aflopende volgorde sorteren
PivotField field = pivotTable.RowFields[0];
field.IsAutoSort = true;
field.IsAscendSort = false;  // false voor aflopend
field.AutoSortField = 0;     // Sorteren op basis van de eerste kolom
```
 Hier gebruiken we de`PivotField` om de sorteerparameters in te stellen. Dit vertelt de draaitabel om het opgegeven rijveld te sorteren op basis van de eerste kolom, en dit in aflopende volgorde te doen. 
## Stap 4: Gegevens vernieuwen en berekenen
Nadat u de sortering hebt toegepast, is het belangrijk om de gegevens in de draaitabel te vernieuwen om er zeker van te zijn dat de wijzigingen worden doorgevoerd.
```csharp
// Vernieuw en bereken de draaitabelgegevens
pivotTable.RefreshData();
pivotTable.CalculateData();
```
Deze stap synchroniseert de draaitabel met uw huidige gegevens, waarbij alle sorteer- of filterwijzigingen die u tot nu toe hebt gemaakt, worden toegepast. Zie het als het klikken op 'vernieuwen' om de nieuwe organisatie van uw gegevens te zien!
## Stap 5: Verberg specifieke rijen
Laten we nu de rijen verbergen die scores bevatten onder een bepaalde drempelwaarde, bijvoorbeeld minder dan 60. Hier kunnen we de gegevens nog verder filteren.
```csharp
// Geef de startrij op voor het controleren van scores
int currentRow = 3;
int rowsUsed = pivotTable.DataBodyRange.EndRow;
// Verberg rijen met een score lager dan 60
while (currentRow < rowsUsed)
{
    Cell cell = worksheet.Cells[currentRow, 1]; // Ervan uitgaande dat de score in de eerste kolom staat
    double score = Convert.ToDouble(cell.Value);
    if (score < 60)
    {
        worksheet.Cells.HideRow(currentRow);  // Verberg de rij als de score lager is dan 60
    }
    currentRow++;
}
```
In deze lus controleren we elke rij binnen het data body-bereik van de draaitabel. Als een score lager is dan 60, verbergen we die rij. Het is alsof je je werkruimte opruimt: de rommel verwijderen die je niet helpt het grotere geheel te zien!
## Stap 6: Laatste vernieuwing en opslaan van de werkmap
Voordat we afronden, vernieuwen we nog een laatste keer de draaitabel om er zeker van te zijn dat het verbergen van rijen effect heeft. Daarna slaan we de werkmap op in een nieuw bestand.
```csharp
// Vernieuw en bereken de gegevens nog een laatste keer
pivotTable.RefreshData();
pivotTable.CalculateData();
// Sla de gewijzigde werkmap op
workbook.Save(outputDir + "PivotTableHideAndSort_out.xlsx");
```
Met deze laatste vernieuwing zorgen we ervoor dat alles up-to-date is. Door de werkmap op te slaan, maakt u een nieuw bestand dat alle wijzigingen weerspiegelt die we hebben aangebracht.
## Stap 7: Bevestig succes
Ten slotte drukken we een succesbericht af om te bevestigen dat de bewerking zonder problemen is voltooid.
```csharp
Console.WriteLine("PivotTableSortAndHide executed successfully.");
```
Deze regel dient een dubbel doel: het bevestigen van succes en het geven van feedback in uw console, waardoor het proces interactiever en gebruiksvriendelijker wordt.
## Conclusie
En daar heb je het! Je hebt succesvol geleerd hoe je draaitabellen opslaat met aangepaste sorteer- en verbergfuncties met Aspose.Cells voor .NET. Van het laden van je werkmap tot het sorteren van gegevens en het verbergen van onnodige details, deze stappen bieden een gestructureerde aanpak voor het programmatisch beheren van je draaitabellen. Of je nu verkoopgegevens analyseert, teamprestaties bijhoudt of gewoon informatie organiseert, het beheersen van deze vaardigheden met Aspose.Cells kan je kostbare tijd besparen en je workflow voor gegevensanalyse verbeteren.
## Veelgestelde vragen
### Wat is Aspose.Cells voor .NET?
Aspose.Cells voor .NET is een .NET-bibliotheek waarmee ontwikkelaars Excel-spreadsheets kunnen maken, bewerken en converteren zonder afhankelijk te zijn van Microsoft Excel. Het is perfect voor het automatiseren van taken in Excel-documenten.
### Kan ik Aspose.Cells gebruiken zonder dat Microsoft Office is geïnstalleerd?
Absoluut! Aspose.Cells is een zelfstandige bibliotheek, dus u hoeft Microsoft Office niet op uw systeem te hebben geïnstalleerd om met Excel-bestanden te werken.
### Hoe kan ik een tijdelijke licentie voor Aspose.Cells krijgen?
 U kunt een tijdelijke vergunning aanvragen via de[tijdelijke licentiepagina](https://purchase.aspose.com/temporary-license/).
### Waar kan ik ondersteuning vinden voor Aspose.Cells-problemen?
 Voor vragen of problemen kunt u terecht op de[Aspose-forum](https://forum.aspose.com/c/cells/9), waar u ondersteuning krijgt van de community en het Aspose-team.
### Is er een gratis proefversie beschikbaar voor Aspose.Cells?
 Ja! U kunt een gratis proefversie van Aspose.Cells downloaden om de functies te testen voordat u een aankoop doet. Bezoek de[gratis proefpagina](https://releases.aspose.com/) om te beginnen.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
