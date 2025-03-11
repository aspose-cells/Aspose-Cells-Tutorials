---
title: Getallenspreadsheet programmatisch lezen in .NET
linktitle: Getallenspreadsheet programmatisch lezen in .NET
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer in deze gedetailleerde tutorial hoe u Numbers-spreadsheets kunt lezen en ze naar PDF kunt converteren met Aspose.Cells voor .NET.
weight: 18
url: /nl/net/converting-excel-files-to-other-formats/reading-numbers-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Getallenspreadsheet programmatisch lezen in .NET

## Invoering
In de digitale wereld van vandaag is databeheer een essentiële vaardigheid en spreadsheets staan voorop bij data-organisatie. Maar wat als u met een Numbers-spreadsheet moet werken (de bestanden die zijn gemaakt door de Numbers-app van Apple) met behulp van .NET? Maak u geen zorgen, u bent niet de enige! In deze tutorial doorlopen we het proces van het programmatisch lezen van een Numbers-spreadsheet met Aspose.Cells voor .NET. U leert hoe u een Numbers-bestand laadt en converteert naar PDF.
## Vereisten
Voordat we beginnen, zijn er een paar dingen die u moet regelen:
1. Aspose.Cells voor .NET: Zorg ervoor dat u de Aspose.Cells-bibliotheek hebt geïnstalleerd. U kunt deze downloaden[hier](https://releases.aspose.com/cells/net/).
2. Visual Studio: Het is raadzaam om Visual Studio (of een andere .NET-compatibele IDE) op uw computer te installeren.
3. Basiskennis van C#: Een beetje vertrouwdheid met C#-programmering helpt u om de cursus soepel te volgen.
4. Uw documentenmap: U hebt een map nodig waarin uw Numbers-bestand is opgeslagen, samen met een locatie om de geconverteerde PDF op te slaan.
Zodra je aan deze vereisten voldoet, kun je beginnen!
## Pakketten importeren
Om te beginnen moeten we de benodigde pakketten importeren in ons C#-project. Dit is een cruciale stap, omdat het ons in staat stelt om de functionaliteiten van de Aspose.Cells-bibliotheek te benutten.
1. Open uw C#-project in Visual Studio.
2. Voeg een verwijzing toe naar de Aspose.Cells-bibliotheek:
   - Als u NuGet gebruikt, voert u eenvoudigweg de volgende opdracht uit in de Package Manager Console:
```
 Install-Package Aspose.Cells
 ```
3. Importeer de benodigde naamruimten in uw code:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Nu we de benodigde pakketten hebben geïmporteerd, gaan we verder met de stapsgewijze handleiding voor het lezen van een Numbers-spreadsheet.
## Stap 1: Geef de bron- en uitvoermappen op
In deze stap stellen we de mappen in waar uw Numbers-bronbestand zich bevindt en waar u de PDF-uitvoer wilt opslaan.
```csharp
// Bron directory
string sourceDir = "Your Document Directory"; // Werk dit bij naar uw huidige directory
// Uitvoermap
string outputDir = "Your Document Directory"; // Werk dit bij naar uw huidige directory
```
 Hier definiëren we twee tekenreeksvariabelen,`sourceDir` En`outputDir` , om de locaties van de invoer- en uitvoerbestanden op te geven. Zorg ervoor dat u vervangt`"Your Document Directory"` met de werkelijke paden op uw systeem.
## Stap 2: Laadopties instellen voor getallenopmaak
Vervolgens specificeren we de laadopties voor het lezen van een Numbers-spreadsheet. Deze stap is essentieel omdat het Aspose vertelt hoe het Numbers-bestand moet worden geïnterpreteerd.
```csharp
// Geef laadopties op; we willen het Numbers-spreadsheet laden
LoadOptions opts = new LoadOptions(LoadFormat.Numbers);
```
 Wij creëren een`LoadOptions` object en specificeer het formaat als`LoadFormat.Numbers`Hiermee wordt aan de Aspose.Cells-bibliotheek doorgegeven dat we met een Numbers-bestand werken. 
## Stap 3: Laad het getallenblad in een werkmap
Nu is het tijd om het eigenlijke Numbers-spreadsheet in een`Workbook` voorwerp.
```csharp
// Laad het Numbers-spreadsheet in de werkmap met de bovenstaande laadopties
Workbook wb = new Workbook(sourceDir + "sampleNumbersByAppleInc.numbers", opts);
```
 Wij instantiëren een`Workbook` object en geef het bestandspad van het Numbers-bestand door, samen met onze laadopties. Zorg ervoor dat de bestandsnaam (`sampleNumbersByAppleInc.numbers`) komt overeen met de werkelijke naam van uw Numbers-bestand.
## Stap 4: Sla de werkmap op als PDF
Zodra het Numbers-bestand succesvol is geladen, is de volgende stap het opslaan ervan in een ander formaat, namelijk PDF.
```csharp
// Sla de werkmap op in PDF-formaat
wb.Save(outputDir + "outputNumbersByAppleInc.pdf", SaveFormat.Pdf);
```
 Hier noemen we de`Save` methode op de`Workbook` object, waarbij het pad van het uitvoerbestand en de indeling waarin we het willen opslaan, worden opgegeven. In dit geval slaan we het op als een PDF. Zorg ervoor dat de naam van het uitvoerbestand (`outputNumbersByAppleInc.pdf`) is uniek en overschrijft geen bestaande bestanden.
## Stap 5: Bevestig succes
Tot slot voegen we een bericht toe om te bevestigen dat de bewerking succesvol is verlopen.
```csharp
Console.WriteLine("ReadNumbersSpreadsheet executed successfully.\r\n");
```
Deze regel code zal een succesbericht naar de console sturen zodra alles is voltooid. Het is altijd fijn om feedback te krijgen, toch?
## Conclusie
En daar heb je het! Je hebt succesvol een Numbers-spreadsheet gelezen en geconverteerd naar PDF met Aspose.Cells voor .NET. Met deze krachtige bibliotheek kun je moeiteloos spreadsheets manipuleren, waardoor je taken voor gegevensbeheer een fluitje van een cent worden. Of je nu applicaties ontwikkelt of spreadsheets gewoon efficiënter wilt verwerken, Aspose.Cells is een fantastische tool om in je gereedschapskist te hebben.
## Veelgestelde vragen
### Welke bestandstypen kan Aspose.Cells lezen?  
Aspose.Cells kan verschillende bestandsformaten lezen, waaronder XLS-, XLSX-, CSV- en Numbers-bestanden. 
### Kan ik Numbers-bestanden bewerken met Aspose.Cells?  
Ja, u kunt Numbers-bestanden lezen, bewerken en opslaan met Aspose.Cells.
### Is Aspose.Cells gratis te gebruiken?  
 Aspose.Cells biedt een gratis proefperiode, maar voor uitgebreid gebruik heb je een licentie nodig. Bekijk de prijzen[hier](https://purchase.aspose.com/buy).
### Wat moet ik doen als er een fout optreedt tijdens het laden van een Numbers-bestand?  
 Zorg ervoor dat u de juiste laadopties gebruikt en dat het bestandspad correct is. Voor meer ondersteuning, bezoek de[Aspose Ondersteuningsforum](https://forum.aspose.com/c/cells/9).
### Hoe kan ik een tijdelijke licentie voor Aspose.Cells krijgen?  
 U kunt een tijdelijke vergunning aanvragen[hier](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
