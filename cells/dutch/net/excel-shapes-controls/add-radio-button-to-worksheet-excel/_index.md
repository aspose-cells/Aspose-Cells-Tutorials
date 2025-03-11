---
title: Keuzerondje toevoegen aan werkblad in Excel
linktitle: Keuzerondje toevoegen aan werkblad in Excel
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u keuzerondjes toevoegt aan een Excel-werkblad met Aspose.Cells voor .NET met deze eenvoudige stapsgewijze handleiding. Perfect voor het maken van interactieve Excel-formulieren.
weight: 19
url: /nl/net/excel-shapes-controls/add-radio-button-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Keuzerondje toevoegen aan werkblad in Excel

## Invoering
Heb je je ooit afgevraagd hoe je je Excel-sheets kunt opfleuren met interactieve elementen zoals keuzerondjes? Of je nu een enquête, een formulier of een analysetool maakt, het toevoegen van keuzerondjes kan de gebruikersinteractie echt verbeteren. In deze tutorial leiden we je door het proces van het toevoegen van keuzerondjes aan je Excel-sheets met Aspose.Cells voor .NET. We splitsen alles op in eenvoudig te volgen stappen, zodat je aan het einde van dit artikel een pro bent. Klaar om erin te duiken? Laten we beginnen!
## Vereisten
Voordat we beginnen met het leuke gedeelte: het toevoegen van keuzerondjes, controleren we eerst of alles goed is ingesteld.
1.  Aspose.Cells voor .NET: Zorg er eerst voor dat u de[Aspose.Cells voor .NET](https://releases.aspose.com/cells/net/) bibliotheek. U kunt het ophalen via NuGet in Visual Studio of vanaf de downloadpagina.
2. IDE (Integrated Development Environment): U hebt een IDE zoals Visual Studio nodig om uw C#-code te schrijven en uit te voeren.
3. .NET Framework: Zorg ervoor dat u .NET Framework 4.0 of hoger op uw machine hebt geïnstalleerd. Aspose.Cells heeft dit nodig om te werken.
4. Basiskennis van C#: Kennis van de C#-syntaxis en .NET-programmering maakt het volgen van de cursus een stuk eenvoudiger.
Zodra alles geregeld is, zijn we klaar voor vertrek!
## Pakketten importeren
Voordat u gaat coderen, is het essentieel om de benodigde namespaces te importeren om latere fouten te voorkomen. Voeg het volgende toe aan uw code:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Drawing;
```
Deze imports zijn essentieel voor toegang tot werkmapfunctionaliteiten, het toevoegen van keuzerondjes en het verwerken van bestandsbewerkingen.
## Stap 1: De werkmap instellen
Laten we eerst een nieuwe Excel-werkmap maken.
 Om te beginnen moet u een nieuwe instantie maken`Workbook` object. Dit zal uw Excel-bestand in code weergeven.
```csharp
// Een nieuwe werkmap maken.
Workbook excelbook = new Workbook();
```
In deze stap maakt u een lege werkmap. Stelt u het voor als uw lege canvas waar u in de volgende stappen keuzerondjes aan toevoegt.
## Stap 2: Een celwaarde toevoegen en opmaken
Laten we nu een titel toevoegen aan het werkblad. We voegen wat tekst toe aan cel`C2` en formatteer het om het vet te maken. Deze stap voegt context toe aan uw keuzerondjes.
### Tekst in cel invoegen
```csharp
// Voeg een waarde in cel C2 in.
excelbook.Worksheets[0].Cells["C2"].PutValue("Age Groups");
```
### Maak de tekst vetgedrukt
```csharp
// Stel het lettertype in cel C2 in op vet.
excelbook.Worksheets[0].Cells["C2"].GetStyle().Font.IsBold = true;
```
 Hier hebben we een eenvoudige titel, "Leeftijdsgroepen", toegevoegd aan cel`C2`, en maakte het vet zodat het opvalt. Makkelijk toch?
## Stap 3: De eerste keuzerondje toevoegen
Nu komt het spannende gedeelte: uw eerste keuzerondje toevoegen aan het werkblad!
### Een keuzerondje toevoegen
```csharp
// Voeg een keuzerondje toe aan het eerste werkblad.
Aspose.Cells.Drawing.RadioButton radio1 = excelbook.Worksheets[0].Shapes.AddRadioButton(3, 0, 2, 0, 30, 110);
```
Deze regel voegt de radioknop toe aan een specifieke positie op uw werkblad. De getallen geven de plaatsing en grootte ervan weer. Zie het als het instellen van de X- en Y-coördinaten van de knop.
### Stel radioknoptekst in
```csharp
// Stel de tekstreeks in.
radio1.Text = "20-29";
```
Hier hebben we de keuzerondje een label gegeven, '20-29', wat staat voor een leeftijdscategorie.
### Koppel de radioknop aan een cel
```csharp
// Stel cel A1 in als een gekoppelde cel voor het keuzerondje.
radio1.LinkedCell = "A1";
```
 Hiermee wordt de keuzerond aan de cel gekoppeld`A1`wat betekent dat het resultaat van de knopselectie in die cel wordt opgeslagen.
### Voeg 3D-effect toe
```csharp
// Maak de keuzerondje 3D.
radio1.Shadow = true;
```
Omdat we willen dat dit keuzerondje opvalt, hebben we een 3D-effect toegevoegd.
### Pas de regel van de keuzerondje aan
```csharp
// Stel de dikte van de keuzerondlijn in.
radio1.Line.Weight = 4;
// Stel de streepjesstijl van de keuzerondjeslijn in.
radio1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Met deze coderegels worden de dikte en het streepje van de rand van de keuzerondjes aangepast, zodat ze er visueel aantrekkelijker uitzien.
## Stap 4: Extra keuzerondjes toevoegen
Laten we nog twee keuzerondjes toevoegen voor de overige leeftijdsgroepen: '30-39' en '40-49'. De stappen zijn hetzelfde, alleen de coördinaten en labels variëren enigszins.
### Voeg de tweede radioknop toe
```csharp
// Voeg nog een keuzerondje toe aan het eerste werkblad.
Aspose.Cells.Drawing.RadioButton radio2 = excelbook.Worksheets[0].Shapes.AddRadioButton(6, 0, 2, 0, 30, 110);
// Stel de tekstreeks in.
radio2.Text = "30-39";
// Stel cel A1 in als een gekoppelde cel voor het keuzerondje.
radio2.LinkedCell = "A1";
// Maak de keuzerondje 3D.
radio2.Shadow = true;
// Stel het gewicht van de keuzerondje in.
radio2.Line.Weight = 4;
// Stel de streepjesstijl van het keuzerondje in.
radio2.Line.DashStyle = MsoLineDashStyle.Solid;
```
### Voeg de derde keuzerond toe
```csharp
// Voeg nog een keuzerondje toe aan het eerste werkblad.
Aspose.Cells.Drawing.RadioButton radio3 = excelbook.Worksheets[0].Shapes.AddRadioButton(9, 0, 2, 0, 30, 110);
// Stel de tekstreeks in.
radio3.Text = "40-49";
// Stel cel A1 in als een gekoppelde cel voor het keuzerondje.
radio3.LinkedCell = "A1";
// Maak de keuzerondje 3D.
radio3.Shadow = true;
// Stel het gewicht van de keuzerondje in.
radio3.Line.Weight = 4;
// Stel de streepjesstijl van het keuzerondje in.
radio3.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Stap 5: Het Excel-bestand opslaan
Zodra u alle keuzerondjes hebt toegevoegd en opgemaakt, kunt u het bestand opslaan.
```csharp
// Sla het Excel-bestand op.
string dataDir = "Your Document Directory";
excelbook.Save(dataDir + "book1.out.xls");
```
In deze stap wordt de werkmap opgeslagen in de door u opgegeven directory. Zo simpel is het: uw interactieve werkblad is nu klaar!
## Conclusie
Daar heb je het! Je hebt zojuist keuzerondjes toegevoegd aan een Excel-werkblad met Aspose.Cells voor .NET. Deze tutorial behandelde alles, van het instellen van de werkmap, het invoegen en opmaken van een waarde, het toevoegen van meerdere keuzerondjes en het koppelen ervan aan een cel. Nu ben je helemaal klaar om interactieve Excel-bladen te maken die er niet alleen geweldig uitzien, maar ook een verbeterde gebruikerservaring bieden. Veel plezier met het verkennen van meer mogelijkheden met Aspose.Cells!
## Veelgestelde vragen
### Kan ik meer keuzerondjes aan verschillende werkbladen toevoegen?  
Absoluut! U kunt het proces op elk werkblad in de werkmap herhalen door de juiste werkbladindex op te geven.
### Kan ik het uiterlijk van de keuzerondjes verder aanpassen?  
Ja, Aspose.Cells biedt diverse aanpassingsopties, waaronder het wijzigen van kleuren, formaten en andere opmaakkenmerken.
### Hoe kan ik detecteren welk keuzerondje is geselecteerd?  
De gekoppelde cel (bijv. A1) toont de index van de geselecteerde radioknop. U kunt de waarde van de gekoppelde cel controleren om erachter te komen welke is geselecteerd.
### Is er een limiet aan het aantal keuzerondjes dat ik kan toevoegen?  
Nee, er is geen harde limiet op het aantal radioknoppen dat u kunt toevoegen. Het is echter wel goed om de interface gebruiksvriendelijk te houden.
### Kan ik Aspose.Cells gebruiken met andere programmeertalen?  
Ja, Aspose.Cells ondersteunt meerdere programmeertalen, waaronder Java. Maar deze tutorial richt zich specifiek op .NET.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
