---
title: Formules in Excel programmatisch berekenen
linktitle: Formules in Excel programmatisch berekenen
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Automatiseer uw Excel-taken met Aspose.Cells voor .NET. Leer formules programmatisch berekenen in deze uitgebreide tutorial.
weight: 11
url: /nl/net/excel-formulas-and-calculation-options/calculating-formulas/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formules in Excel programmatisch berekenen

## Invoering
In de huidige datagedreven wereld kan het automatiseren van taken tijd besparen en de efficiëntie verbeteren, vooral bij het verwerken van spreadsheets. Als u ooit met complexe formules in Excel hebt gewerkt, weet u hoe belangrijk het is om het goed te doen. Met Aspose.Cells voor .NET kunt u programmatisch formules berekenen en uw Excel-bestanden eenvoudig beheren. In deze tutorial doorlopen we elke stap die betrokken is bij het maken van een Excel-bestand, het toevoegen van waarden en formules en het vervolgens berekenen van die formules met een beetje C#. Laten we erin duiken!
## Vereisten
Voordat we beginnen, moet u ervoor zorgen dat u een aantal dingen geregeld hebt:
1. Ontwikkelomgeving: Zorg ervoor dat u Visual Studio of een andere C#-omgeving hebt waarin u .NET-toepassingen kunt uitvoeren.
2.  Aspose.Cells voor .NET: Download en installeer de Aspose.Cells-bibliotheek. U kunt deze verkrijgen via de[Aspose-website](https://releases.aspose.com/cells/net/).
3. Basiskennis van C#: Met basiskennis van C# kunt u de concepten en codefragmenten die we gaan gebruiken, beter begrijpen.
4. .NET Framework: Zorg ervoor dat de juiste versie van .NET Framework op uw computer is geïnstalleerd.
5.  Aspose.Cells-licentie: Als u het na de gratis proefperiode wilt gebruiken, overweeg dan om een[tijdelijke licentie](https://purchase.aspose.com/temporary-license/).
Nu we alles gereed hebben, kunnen we de code gaan bekijken en deze stap voor stap uitleggen!
## Pakketten importeren
Voordat u code schrijft, moet u ervoor zorgen dat u de benodigde naamruimten voor Aspose.Cells in uw C#-bestand importeert:
```csharp
using System.IO;
using Aspose.Cells;
```
Hiermee krijgt u toegang tot de functionaliteiten van de Aspose.Cells-bibliotheek om Excel-bestanden te bewerken.
## Stap 1: Stel de documentdirectory in
Begin met het definiëren van het pad waar u uw Excel-document wilt opslaan. Het is essentieel om ervoor te zorgen dat deze directory bestaat, of maak hem aan als dat niet zo is.
```csharp
// Het pad naar de documentenmap
string dataDir = "Your Document Directory";
// Maak een map aan als deze nog niet aanwezig is
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
In deze stap controleert u of de directory bestaat. Als dat niet zo is, maakt u deze aan. Deze eenvoudige stap helpt fouten te voorkomen wanneer u later uw Excel-bestand probeert op te slaan.
## Stap 2: Een werkmapobject instantiëren
## Een nieuwe werkmap maken
Nu uw directory is ingesteld, gaan we een werkmapobject maken dat uw Excel-bestand vertegenwoordigt:
```csharp
// Een werkmapobject instantiëren
Workbook workbook = new Workbook();
```
Deze regel creëert simpelweg een nieuwe werkmap in het geheugen. Zie het als het openen van een leeg Excel-bestand waar u gegevens en formules kunt toevoegen.
## Stap 3: Een nieuw werkblad toevoegen
## Werken met werkbladen
In onze werkmap willen we een nieuw werkblad toevoegen waar we onze data kunnen manipuleren. Dit is hoe we dat doen:
```csharp
// Een nieuw werkblad toevoegen aan het Excel-object
int sheetIndex = workbook.Worksheets.Add();
// De referentie van het nieuw toegevoegde werkblad verkrijgen door de index van het werkblad door te geven
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
Eerst voegt u een nieuw werkblad toe, dat u automatisch de index van dat werkblad geeft. Vervolgens haalt u dat werkblad op via de index. Het is alsof u een nieuw tabblad opent in uw Excel-werkmap!
## Stap 4: Waarden in cellen invoegen
## Gegevens vullen
Nu we ons werkblad hebben gemaakt, moeten we er wat gegevens aan toevoegen:
```csharp
// Een waarde toevoegen aan cel "A1"
worksheet.Cells["A1"].PutValue(1);
// Een waarde toevoegen aan cel "A2"
worksheet.Cells["A2"].PutValue(2);
// Een waarde toevoegen aan cel "A3"
worksheet.Cells["A3"].PutValue(3);
```
In deze stap voegt u waarden in de eerste drie cellen (A1, A2, A3) van het werkblad in. Deze actie is vergelijkbaar met het rechtstreeks typen van waarden in een Excel-sheet. 
## Stap 5: Voeg een formule toe
## De waarden optellen
Nadat u waarden hebt ingevoerd, is het tijd om een formule toe te voegen die de som van deze cellen berekent. Dit doet u als volgt:
```csharp
// Een SOM-formule toevoegen aan cel "A4"
worksheet.Cells["A4"].Formula = "=SUM(A1:A3)";
```
Deze regel code voegt een SUM-formule toe aan cel A4, die de waarden van A1 tot A3 optelt. Het is net als het schrijven van een formule in Excel, maar dan programmatisch!
## Stap 6: Bereken de formule
## De berekening uitvoeren
Nu komt het moment van de waarheid! We moeten de resultaten van de formules die we hebben ingevoerd berekenen:
```csharp
// Berekenen van de resultaten van formules
workbook.CalculateFormula();
```
 Door te bellen`CalculateFormula()`, vertel je de werkmap om alle formules erin te verwerken. Dit is vergelijkbaar met het indrukken van "Enter" na het typen van een formule in een Excel-cel.
## Stap 7: De berekende waarde ophalen
## Het resultaat lezen
Zodra de formules zijn berekend, kunnen we de waarde uit A4 ophalen:
```csharp
// De berekende waarde van de cel ophalen
string value = worksheet.Cells["A4"].Value.ToString();
```
In deze stap haalt u het resultaat van onze SUM-formule op. Dit zou u het totaal van 1 + 2 + 3 geven, wat 6 is!
## Stap 8: Sla het Excel-bestand op
## Schrijven naar schijf
Sla de werkmap ten slotte op in de opgegeven map, zodat u er later toegang toe hebt:
```csharp
// Het Excel-bestand opslaan
workbook.Save(dataDir + "output.xls");
```
Deze code slaat uw Excel-bestand op met de naam "output.xls" in de map die u hebt opgegeven. Het is alsof u op "Opslaan als" klikt in Excel en kiest waar u uw bestand wilt bewaren.
## Conclusie
In deze tutorial hebben we behandeld hoe u programmatisch een Excel-bestand kunt maken met Aspose.Cells voor .NET. Van het toevoegen van waarden en formules tot het berekenen en opslaan van de uiteindelijke uitvoer, we hebben elke kritieke stap doorlopen, zodat u een solide basis hebt voor toekomstige automatiseringen.
## Veelgestelde vragen
### Wat is Aspose.Cells voor .NET?
Aspose.Cells voor .NET is een bibliotheek waarmee ontwikkelaars Excel-documenten in .NET-toepassingen programmatisch kunnen bewerken.
### Kan ik formules in Excel evalueren met Aspose.Cells?
Ja! U kunt Aspose.Cells gebruiken om formules te berekenen en evalueren, net zoals u dat in Excel zou doen.
### Is er een gratis proefversie beschikbaar voor Aspose.Cells?
Absoluut! Je kunt een gratis proefversie krijgen[hier](https://releases.aspose.com/).
### Kan ik bestaande Excel-bestanden bewerken met Aspose.Cells?
Ja, met Aspose.Cells kunt u bestaande Excel-bestanden laden en indien nodig wijzigen.
### Waar kan ik meer documentatie vinden over Aspose.Cells voor .NET?
 kunt uitgebreide documentatie vinden[hier](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
