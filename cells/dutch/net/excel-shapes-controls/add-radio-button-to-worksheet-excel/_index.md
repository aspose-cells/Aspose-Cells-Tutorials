---
"description": "Leer hoe u keuzerondjes toevoegt aan een Excel-werkblad met Aspose.Cells voor .NET met deze eenvoudige stapsgewijze handleiding. Perfect voor het maken van interactieve Excel-formulieren."
"linktitle": "Keuzerondje toevoegen aan werkblad in Excel"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Keuzerondje toevoegen aan werkblad in Excel"
"url": "/nl/net/excel-shapes-controls/add-radio-button-to-worksheet-excel/"
"weight": 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Keuzerondje toevoegen aan werkblad in Excel

## Invoering
Heb je je ooit afgevraagd hoe je je Excel-sheets kunt opfleuren met interactieve elementen zoals keuzerondjes? Of je nu een enquête, een formulier of een analysetool maakt, het toevoegen van keuzerondjes kan de gebruikersinteractie aanzienlijk verbeteren. In deze tutorial laten we je zien hoe je keuzerondjes toevoegt aan je Excel-sheets met Aspose.Cells voor .NET. We leggen alles uit in eenvoudig te volgen stappen, zodat je aan het einde van dit artikel een pro bent. Klaar om aan de slag te gaan? Aan de slag!
## Vereisten
Voordat we met het leuke gedeelte van het toevoegen van keuzerondjes beginnen, controleren we of alles goed is ingesteld.
1. Aspose.Cells voor .NET: Zorg er eerst voor dat u de [Aspose.Cells voor .NET](https://releases.aspose.com/cells/net/) bibliotheek. Je kunt het downloaden via NuGet in Visual Studio of vanaf de downloadpagina.
2. IDE (Integrated Development Environment): U hebt een IDE zoals Visual Studio nodig om uw C#-code te schrijven en uit te voeren.
3. .NET Framework: Zorg ervoor dat .NET Framework 4.0 of hoger op uw computer is geïnstalleerd. Aspose.Cells vereist dit om te werken.
4. Basiskennis van C#: Kennis van de C#-syntaxis en .NET-programmering maakt het volgen van de cursus een stuk eenvoudiger.
Zodra alles op zijn plaats is, zijn we klaar voor vertrek!
## Pakketten importeren
Voordat u begint met coderen, is het essentieel om de benodigde naamruimten te importeren om latere fouten te voorkomen. Voeg het volgende toe aan uw code:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Drawing;
```
Deze imports zijn essentieel voor het verkrijgen van toegang tot werkmapfunctionaliteiten, het toevoegen van keuzerondjes en het verwerken van bestandsbewerkingen.
## Stap 1: De werkmap instellen
Laten we eerst een nieuwe Excel-werkmap maken.
Om te beginnen moet u een nieuwe instantie maken `Workbook` object. Dit vertegenwoordigt uw Excel-bestand in code.
```csharp
// Een nieuwe werkmap instantiëren.
Workbook excelbook = new Workbook();
```
In deze stap maak je een lege werkmap. Stel je dit voor als een leeg canvas waar je in de volgende stappen keuzerondjes aan toevoegt.
## Stap 2: Een celwaarde toevoegen en opmaken
Laten we nu een titel aan het werkblad toevoegen. We voegen wat tekst toe aan de cel. `C2` en formatteer het om het vetgedrukt te maken. Deze stap voegt context toe aan je keuzerondjes.
### Tekst in cel invoegen
```csharp
// Voer een waarde in cel C2 in.
excelbook.Worksheets[0].Cells["C2"].PutValue("Age Groups");
```
### Maak de tekst vetgedrukt
```csharp
// Maak de tekst in cel C2 vetgedrukt.
excelbook.Worksheets[0].Cells["C2"].GetStyle().Font.IsBold = true;
```
Hier hebben we een eenvoudige titel, 'Leeftijdsgroepen', toegevoegd aan cel `C2`, en maakte het vetgedrukt zodat het opvalt. Makkelijk toch?
## Stap 3: De eerste keuzerondje toevoegen
Nu komt het spannende deel: uw eerste keuzerondje toevoegen aan het werkblad!
### Een keuzerondje toevoegen
```csharp
// Voeg een keuzerondje toe aan het eerste werkblad.
Aspose.Cells.Drawing.RadioButton radio1 = excelbook.Worksheets[0].Shapes.AddRadioButton(3, 0, 2, 0, 30, 110);
```
Met deze regel wordt het keuzerondje aan een specifieke positie op uw werkblad toegevoegd. De getallen geven de plaatsing en grootte aan. Zie het als het instellen van de X- en Y-coördinaten van de knop.
### Stel radioknoptekst in
```csharp
// Stel de tekstreeks in.
radio1.Text = "20-29";
```
Hier hebben we de keuzerondje het label '20-29' gegeven, wat staat voor een leeftijdscategorie.
### Koppel de radioknop aan een cel
```csharp
// Stel cel A1 in als een gekoppelde cel voor het keuzerondje.
radio1.LinkedCell = "A1";
```
Hiermee wordt de keuzerond aan de cel gekoppeld `A1`, wat betekent dat het resultaat van de knopselectie in die cel wordt opgeslagen.
### 3D-effect toevoegen
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
Met deze coderegels kunt u de dikte en het streepje van de rand van het keuzerondje aanpassen, zodat het visueel aantrekkelijker wordt.
## Stap 4: Extra keuzerondjes toevoegen
Laten we twee extra keuzerondjes toevoegen voor de overige leeftijdsgroepen: '30-39' en '40-49'. De stappen zijn hetzelfde, alleen met kleine variaties in de coördinaten en labels.
### Voeg de tweede keuzerond toe
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
In deze stap wordt de werkmap opgeslagen in de door u opgegeven map. Zo eenvoudig is het: uw interactieve werkblad is nu klaar!
## Conclusie
Zo, dat is het! Je hebt zojuist keuzerondjes toegevoegd aan een Excel-werkblad met Aspose.Cells voor .NET. Deze tutorial behandelde alles, van het instellen van de werkmap, het invoegen en opmaken van een waarde, het toevoegen van meerdere keuzerondjes en het koppelen ervan aan een cel. Nu ben je helemaal klaar om interactieve Excel-sheets te maken die er niet alleen fantastisch uitzien, maar ook een verbeterde gebruikerservaring bieden. Veel plezier met het ontdekken van meer mogelijkheden met Aspose.Cells!
## Veelgestelde vragen
### Kan ik extra keuzerondjes aan verschillende werkbladen toevoegen?  
Absoluut! U kunt het proces op elk werkblad in de werkmap herhalen door de juiste werkbladindex op te geven.
### Kan ik het uiterlijk van de keuzerondjes verder aanpassen?  
Ja, Aspose.Cells biedt verschillende aanpassingsopties, waaronder het wijzigen van kleuren, formaten en andere opmaakkenmerken.
### Hoe kan ik detecteren welk keuzerondje is geselecteerd?  
De gekoppelde cel (bijv. A1) toont de index van het geselecteerde keuzerondje. U kunt de waarde van de gekoppelde cel controleren om te zien welke geselecteerd is.
### Zit er een limiet aan het aantal keuzerondjes dat ik kan toevoegen?  
Nee, er is geen vaste limiet aan het aantal keuzerondjes dat je kunt toevoegen. Het is echter wel belangrijk om de interface gebruiksvriendelijk te houden.
### Kan ik Aspose.Cells gebruiken met andere programmeertalen?  
Ja, Aspose.Cells ondersteunt meerdere programmeertalen, waaronder Java. Maar deze tutorial richt zich specifiek op .NET.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}