---
"description": "Automatiseer je Excel-taken met Aspose.Cells voor .NET. Leer formules programmatisch berekenen in deze uitgebreide tutorial."
"linktitle": "Formules in Excel programmatisch berekenen"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Formules in Excel programmatisch berekenen"
"url": "/nl/net/excel-formulas-and-calculation-options/calculating-formulas/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Formules in Excel programmatisch berekenen

## Invoering
In de huidige datagedreven wereld kan het automatiseren van taken tijd besparen en de efficiëntie verbeteren, vooral bij het werken met spreadsheets. Als je ooit met complexe formules in Excel hebt gewerkt, weet je hoe belangrijk het is om het goed te doen. Met Aspose.Cells voor .NET kun je programmatisch formules berekenen en je Excel-bestanden eenvoudig beheren. In deze tutorial doorlopen we elke stap die nodig is om een Excel-bestand te maken, waarden en formules toe te voegen en die formules vervolgens met een beetje C# te berekenen. Laten we beginnen!
## Vereisten
Voordat we beginnen, moet u ervoor zorgen dat u een paar dingen geregeld hebt:
1. Ontwikkelomgeving: Zorg ervoor dat u Visual Studio of een andere C#-omgeving hebt waarin u .NET-toepassingen kunt uitvoeren.
2. Aspose.Cells voor .NET: Download en installeer de Aspose.Cells-bibliotheek. Je kunt deze vinden op de [Aspose-website](https://releases.aspose.com/cells/net/).
3. Basiskennis van C#: Met basiskennis van C# kunt u de concepten en codefragmenten die we gaan gebruiken, beter begrijpen.
4. .NET Framework: Zorg ervoor dat de juiste versie van .NET Framework op uw computer is geïnstalleerd.
5. Aspose.Cells-licentie: Als u het na de gratis proefperiode wilt gebruiken, overweeg dan om een [tijdelijke licentie](https://purchase.aspose.com/temporary-license/).
Nu we alles gereed hebben, kunnen we de code gaan analyseren en deze stap voor stap uitleggen!
## Pakketten importeren
Voordat u code schrijft, moet u ervoor zorgen dat u de benodigde naamruimten voor Aspose.Cells in uw C#-bestand importeert:
```csharp
using System.IO;
using Aspose.Cells;
```
Hiermee krijgt u toegang tot de functionaliteiten die de Aspose.Cells-bibliotheek biedt om Excel-bestanden te bewerken.
## Stap 1: Stel de documentmap in
Begin met het definiëren van het pad waar u uw Excel-document wilt opslaan. Het is essentieel om ervoor te zorgen dat deze map bestaat, of maak hem aan als dat niet zo is.
```csharp
// Het pad naar de documentenmap
string dataDir = "Your Document Directory";
// Maak een map aan als deze nog niet aanwezig is
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
In deze stap controleer je of de map bestaat. Zo niet, dan maak je hem aan. Deze eenvoudige stap helpt fouten te voorkomen wanneer je je Excel-bestand later probeert op te slaan.
## Stap 2: Een werkmapobject instantiëren
## Een nieuwe werkmap maken
Nu uw directory is ingesteld, gaan we een werkmapobject maken dat uw Excel-bestand vertegenwoordigt:
```csharp
// Een werkmapobject instantiëren
Workbook workbook = new Workbook();
```
Deze regel creëert simpelweg een nieuwe werkmap in het geheugen. Zie het als het openen van een leeg Excel-bestand waarin u gegevens en formules kunt toevoegen.
## Stap 3: Een nieuw werkblad toevoegen
## Werken met werkbladen
In onze werkmap willen we een nieuw werkblad toevoegen waarmee we onze gegevens kunnen bewerken. Zo doen we dat:
```csharp
// Een nieuw werkblad toevoegen aan het Excel-object
int sheetIndex = workbook.Worksheets.Add();
// De referentie van het nieuw toegevoegde werkblad verkrijgen door de index van het werkblad door te geven
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
Eerst voeg je een nieuw werkblad toe, waardoor je automatisch de index van dat werkblad krijgt. Vervolgens haal je dat werkblad op via de index. Het is alsof je een nieuw tabblad opent in je Excel-werkmap!
## Stap 4: Waarden in cellen invoegen
## Gegevens vullen
Nu we ons werkblad hebben gemaakt, moeten we er enkele gegevens aan toevoegen:
```csharp
// Een waarde toevoegen aan cel "A1"
worksheet.Cells["A1"].PutValue(1);
// Een waarde toevoegen aan cel "A2"
worksheet.Cells["A2"].PutValue(2);
// Een waarde toevoegen aan cel "A3"
worksheet.Cells["A3"].PutValue(3);
```
In deze stap voert u waarden in de eerste drie cellen (A1, A2, A3) van het werkblad in. Deze actie is vergelijkbaar met het rechtstreeks typen van waarden in een Excel-bestand. 
## Stap 5: Een formule toevoegen
## De waarden optellen
Nadat u de waarden hebt ingevoerd, is het tijd om een formule toe te voegen die de som van deze cellen berekent. Zo werkt het:
```csharp
// Een SOM-formule toevoegen aan cel "A4"
worksheet.Cells["A4"].Formula = "=SUM(A1:A3)";
```
Deze regel code voegt een SOM-formule toe aan cel A4, die de waarden van A1 tot en met A3 optelt. Het is net als het schrijven van een formule in Excel, maar dan programmatisch!
## Stap 6: Bereken de formule
## De berekening uitvoeren
Nu is het moment van de waarheid aangebroken! We moeten de resultaten van de ingevoerde formules berekenen:
```csharp
// De resultaten van formules berekenen
workbook.CalculateFormula();
```
Door te bellen `CalculateFormula()`, geef je de werkmap opdracht alle formules erin te verwerken. Dit is vergelijkbaar met het indrukken van "Enter" na het typen van een formule in een Excel-cel.
## Stap 7: De berekende waarde ophalen
## Het resultaat lezen
Zodra de formules zijn berekend, kunnen we de waarde uit A4 ophalen:
```csharp
// De berekende waarde van de cel ophalen
string value = worksheet.Cells["A4"].Value.ToString();
```
In deze stap bereken je het resultaat van onze SOM-formule. Dit levert je de som op van 1 + 2 + 3, wat neerkomt op 6!
## Stap 8: Sla het Excel-bestand op
## Schrijven naar schijf
Sla de werkmap ten slotte op in de opgegeven directory, zodat u er later toegang toe hebt:
```csharp
// Het Excel-bestand opslaan
workbook.Save(dataDir + "output.xls");
```
Deze code slaat je Excel-bestand op onder de naam "output.xls" in de door jou opgegeven map. Het is alsof je in Excel op "Opslaan als" klikt en kiest waar je je bestand wilt bewaren.
## Conclusie
In deze tutorial hebben we uitgelegd hoe je programmatisch een Excel-bestand kunt maken met Aspose.Cells voor .NET. Van het toevoegen van waarden en formules tot het berekenen en opslaan van de uiteindelijke uitvoer: we hebben elke belangrijke stap doorlopen, zodat je een solide basis hebt voor toekomstige automatisering.
## Veelgestelde vragen
### Wat is Aspose.Cells voor .NET?
Aspose.Cells voor .NET is een bibliotheek waarmee ontwikkelaars Excel-documenten in .NET-toepassingen programmatisch kunnen bewerken.
### Kan ik formules in Excel evalueren met Aspose.Cells?
Jazeker! U kunt Aspose.Cells gebruiken om formules te berekenen en evalueren, net zoals u dat in Excel zou doen.
### Is er een gratis proefversie beschikbaar voor Aspose.Cells?
Absoluut! Je kunt een gratis proefperiode krijgen. [hier](https://releases.aspose.com/).
### Kan ik bestaande Excel-bestanden bewerken met Aspose.Cells?
Ja, met Aspose.Cells kunt u bestaande Excel-bestanden laden en indien nodig wijzigen.
### Waar kan ik meer documentatie vinden over Aspose.Cells voor .NET?
U kunt uitgebreide documentatie vinden [hier](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}