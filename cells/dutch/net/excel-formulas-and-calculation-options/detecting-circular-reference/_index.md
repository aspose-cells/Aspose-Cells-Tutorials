---
title: Circulaire verwijzingen in Excel programmatisch detecteren
linktitle: Circulaire verwijzingen in Excel programmatisch detecteren
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Detecteer eenvoudig circulaire verwijzingen in Excel met Aspose.Cells voor .NET. Volg onze stapsgewijze handleiding om nauwkeurige berekeningen in uw spreadsheets te garanderen.
weight: 13
url: /nl/net/excel-formulas-and-calculation-options/detecting-circular-reference/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Circulaire verwijzingen in Excel programmatisch detecteren

## Invoering
Als het gaat om het werken met Excel-bestanden, is een van de meest frustrerende problemen die u kunt tegenkomen een circulaire verwijzing. Dit gebeurt wanneer een formule terugverwijst naar zijn eigen cel, direct of indirect, waardoor een lus ontstaat die de rekenmachine van Excel in de war kan brengen. Maar vrees niet! Met Aspose.Cells voor .NET kunt u deze vervelende circulaire verwijzingen programmatisch detecteren, zodat uw spreadsheets functioneel en nauwkeurig blijven. In deze handleiding leiden we u stap voor stap door het proces, waardoor het zo eenvoudig als een fluitje van een cent wordt.
## Vereisten
Voordat we dieper ingaan op het detecteren van circulaire verwijzingen, controleren we eerst of u alles bij de hand hebt om aan de slag te gaan:
1. Visual Studio: Zorg ervoor dat Visual Studio op uw machine is geïnstalleerd. Dit wordt uw ontwikkelomgeving.
2. .NET Framework: Zorg ervoor dat u een compatibele versie van .NET Framework gebruikt (minimaal .NET Framework 4.0).
3.  Aspose.Cells Library: U moet de Aspose.Cells-bibliotheek hebben. U kunt deze downloaden van de[Aspose-website](https://releases.aspose.com/cells/net/).
4. Basiskennis van C#: Kennis van C#-programmering is nuttig, omdat we code in deze taal gaan schrijven.
5. Excel-bestand: Zorg dat u een Excel-bestand bij de hand hebt dat circulaire verwijzingen bevat voor het testen. U kunt een eenvoudige maken of een voorbeeld downloaden.
Nu we aan de voorwaarden hebben voldaan, kunnen we beginnen met het leukste gedeelte!
## Pakketten importeren
Voordat u kunt beginnen met coderen, moet u de benodigde pakketten importeren. Dit is hoe u dat doet:
### Een nieuw project maken
- Open Visual Studio en maak een nieuw C# Console Application-project.
### Voeg Aspose.Cells-referentie toe
- Klik met de rechtermuisknop op uw project in de Solution Explorer.
- Selecteer 'NuGet-pakketten beheren'.
- Zoek naar “Aspose.Cells” en installeer de nieuwste versie.
### Vereiste naamruimten importeren
 Bovenaan je`Program.cs` bestand, importeer de benodigde naamruimten:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Nu we alles hebben ingesteld, gaan we dieper in op de code voor het detecteren van circulaire verwijzingen in een Excel-bestand.
## Stap 1: Definieer de invoerdirectory
Eerst moet u de directory opgeven waar uw Excel-bestand zich bevindt. Dit is waar u uw Excel-bestand laadt.
```csharp
// Invoermap
string sourceDir = "Your Document Directory";
```
 Vervangen`"Your Document Directory"` met het daadwerkelijke pad naar uw Excel-bestand.
## Stap 2: Laad de werkmap met LoadOptions
Vervolgens laadt u uw Excel-werkmap. Dit is waar de magie begint!
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
 Hier maken we een nieuw exemplaar van`LoadOptions` en laad de werkmap vanaf het opgegeven pad. Zorg ervoor dat uw Excel-bestandsnaam overeenkomt!
## Stap 3: Iteratie-instellingen inschakelen
Om circulaire verwijzingen toe te staan, moet u de iteratie-instellingen in de werkmap inschakelen.
```csharp
objWB.Settings.Iteration = true;
```
Hiermee wordt aan Aspose.Cells doorgegeven dat circulaire verwijzingen tijdens de berekening moeten worden toegestaan.
## Stap 4: Berekeningsopties en circulaire monitor maken
Laten we nu de berekeningsopties en onze aangepaste cirkelmonitor aanmaken.
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
 Hier maken we een instantie van`CalculationOptions` en een aangepaste`CircularMonitor`Met deze monitor kunt u eventuele circulaire verwijzingen die u tijdens berekeningen tegenkomt, bijhouden.
## Stap 5: Bereken de formules
Nu is het tijd om de formules in uw werkmap te berekenen.
```csharp
objWB.CalculateFormula(copts);
```
Deze regel voert de berekening uit en controleert op circulaire verwijzingen.
## Stap 6: Circulaire verwijzingen tellen
Na de berekening kunt u tellen hoeveel circulaire verwijzingen er zijn gevonden.
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
Hiermee wordt het aantal circulaire verwijzingen weergegeven dat in uw Excel-bestand is gedetecteerd.
## Stap 7: Resultaten weergeven
Tot slot tonen we de resultaten en bevestigen we dat onze methode succesvol is uitgevoerd.
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## Stap 8: Implementeer de CircularMonitor-klasse
 Om het proces te voltooien, moet u de volgende stappen uitvoeren:`CircularMonitor` klasse. Deze klasse zal erven van`AbstractCalculationMonitor` en de detectie van circulaire verwijzingen afhandelen.
```csharp
public class CircularMonitor : AbstractCalculationMonitor
{
    public ArrayList circulars = new ArrayList();
    public ArrayList Circulars { get { return circulars; } }
    public override bool OnCircular(IEnumerator circularCellsData)
    {
        CalculationCell cc = null;
        ArrayList cur = new ArrayList();
        while (circularCellsData.MoveNext())
        {
            cc = (CalculationCell)circularCellsData.Current;
            cur.Add(cc.Worksheet.Name + "!" + CellsHelper.CellIndexToName(cc.CellRow, cc.CellColumn));
        }
        circulars.Add(cur);
        return true;
    }
}
```
In deze klasse worden de details van elke gevonden circulaire verwijzing vastgelegd, inclusief de naam van het werkblad en de celindex.
## Conclusie
Het detecteren van circulaire verwijzingen in Excel met Aspose.Cells voor .NET is een eenvoudig proces als u het opsplitst in beheersbare stappen. Door deze handleiding te volgen, kunt u eenvoudig circulaire verwijzingen in uw spreadsheets identificeren en verwerken, zodat uw berekeningen nauwkeurig en betrouwbaar blijven. Of u nu een doorgewinterde ontwikkelaar bent of net begint, Aspose.Cells biedt krachtige tools om uw Excel-manipulatiemogelijkheden te verbeteren. 
## Veelgestelde vragen
### Wat is een kringverwijzing in Excel?
Er is sprake van een circulaire verwijzing wanneer een formule terugverwijst naar zijn eigen cel, waardoor er een eindeloze lus ontstaat in de berekeningen.
### Hoe kan ik circulaire verwijzingen programmatisch detecteren?
U kunt de Aspose.Cells-bibliotheek in .NET gebruiken om circulaire verwijzingen programmatisch te detecteren door een aangepaste berekeningsmonitor te implementeren.
### Wat zijn de vereisten voor het gebruik van Aspose.Cells?
U hebt Visual Studio, .NET Framework en de Aspose.Cells-bibliotheek nodig.
### Kan ik Aspose.Cells gratis gebruiken?
Ja, Aspose.Cells biedt een gratis proefperiode aan waarmee u de functies kunt uitproberen.
### Waar kan ik meer informatie vinden over Aspose.Cells?
 U kunt de[Aspose.Cells-documentatie](https://reference.aspose.com/cells/net/) voor gedetailleerde informatie en voorbeelden.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
