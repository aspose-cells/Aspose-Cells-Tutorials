---
title: Keuzelijst toevoegen aan werkblad in Excel
linktitle: Keuzelijst toevoegen aan werkblad in Excel
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u een keuzelijst toevoegt aan een Excel-werkblad met Aspose.Cells voor .NET. Volg onze eenvoudige, stapsgewijze handleiding en maak uw Excel-bladen interactief.
weight: 20
url: /nl/net/excel-shapes-controls/add-list-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Keuzelijst toevoegen aan werkblad in Excel

## Invoering
Het toevoegen van interactieve elementen aan uw Excel-werkbladen, zoals een keuzelijst, kan het gegevensbeheer en de presentatie aanzienlijk verbeteren. Of u nu een interactief formulier of een aangepaste tool voor gegevensinvoer maakt, de mogelijkheid om gebruikersinvoer te beheren met een keuzelijst is van onschatbare waarde. Aspose.Cells voor .NET biedt een efficiënte manier om deze besturingselementen toe te voegen en te beheren in uw Excel-bestanden. In deze handleiding leiden we u door het proces van het toevoegen van een keuzelijst aan een werkblad met behulp van Aspose.Cells voor .NET.
## Vereisten
Voordat u met coderen begint, moet u ervoor zorgen dat u de volgende hulpmiddelen en bronnen tot uw beschikking hebt:
-  Aspose.Cells voor .NET-bibliotheek: u kunt het downloaden van de[Aspose.Cells voor .NET downloadpagina](https://releases.aspose.com/cells/net/).
- Ontwikkelomgeving: Elke IDE die .NET-ontwikkeling ondersteunt, zoals Visual Studio.
- .NET Framework: Zorg ervoor dat uw project gericht is op een ondersteunde versie van het .NET Framework.
 Overweeg ook om een[tijdelijke licentie](https://purchase.aspose.com/temporary-license/) als u alle functies zonder beperkingen wilt verkennen.
## Pakketten importeren
Voordat u begint, moet u ervoor zorgen dat u de benodigde Aspose.Cells-naamruimten hebt geïmporteerd. Dit is hoe u dat doet:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
In deze tutorial splitsen we het proces van het toevoegen van een keuzelijst op in meerdere eenvoudige stappen. Volg elke stap nauwkeurig om ervoor te zorgen dat alles werkt zoals verwacht.
## Stap 1: Uw documentenmap instellen
Voordat u een Excel-bestand maakt, hebt u een locatie nodig om het op te slaan. Hier ziet u hoe u de directory instelt:
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
// Maak een map aan als deze nog niet bestaat.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
In deze stap definieert u waar uw bestand wordt opgeslagen. De code controleert of de directory bestaat en als dat niet zo is, maakt hij er een voor u aan. Dit zorgt ervoor dat u later geen "bestand niet gevonden"-fouten krijgt.
## Stap 2: Maak een nieuwe werkmap en open het eerste werkblad
Vervolgens maken we een nieuwe werkmap en openen we het eerste werkblad, waar we onze keuzelijst aan toevoegen.
```csharp
// Maak een nieuwe werkmap.
Workbook workbook = new Workbook();
// Pak het eerste werkblad.
Worksheet sheet = workbook.Worksheets[0];
```
Een werkmap is in feite uw Excel-bestand. Hier maken we een nieuwe werkmap en openen we het eerste werkblad, waar we onze keuzelijst plaatsen. Zie dit als het maken van een leeg canvas waarop u de bedieningselementen schildert.
## Stap 3: Gegevens invoeren voor de keuzelijst
Voordat we de keuzelijst toevoegen, moeten we een aantal gegevens invullen waarnaar de keuzelijst zal verwijzen.
```csharp
// Haal de cellenverzameling van het werkblad op.
Cells cells = sheet.Cells;
// Voer een waarde in voor het label.
cells["B3"].PutValue("Choose Dept:");
// Maak het label vet.
cells["B3"].GetStyle().Font.IsBold = true;
// Invoerwaarden voor de keuzelijst.
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
Hier voegen we wat tekst toe aan het werkblad. Het label "Choose Dept:" staat in cel B3 en het lettertype is vetgedrukt. In kolom A voegen we waarden in die dienen als invoerbereik voor onze keuzelijst, die verschillende afdelingen vertegenwoordigen. Dit invoerbereik is wat gebruikers kiezen bij interactie met de keuzelijst.
## Stap 4: Voeg de keuzelijst toe aan het werkblad
Nu we de gegevens hebben ingesteld, kunnen we het keuzelijstbesturingselement zelf toevoegen.
```csharp
// Voeg een nieuwe keuzelijst toe.
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
Deze code voegt de keuzelijst toe aan het werkblad. De parameters definiëren de positie en grootte van de keuzelijst. De keuzelijst wordt geplaatst op rij 2, kolom 0 met een breedte van 122 en een hoogte van 100. Dit zijn de coördinaten en grootte die bepalen waar de keuzelijst in het werkblad verschijnt.
## Stap 5: Eigenschappen van keuzelijst instellen
Vervolgens stellen we diverse eigenschappen voor de keuzelijst in, zodat deze volledig functioneel is.
```csharp
// Stel het plaatsingstype in.
listBox.Placement = PlacementType.FreeFloating;
// Stel de gekoppelde cel in.
listBox.LinkedCell = "A1";
// Stel het invoerbereik in.
listBox.InputRange = "A2:A7";
// Stel het selectietype in.
listBox.SelectionType = SelectionType.Single;
// Geef de keuzelijst een 3D-arcering.
listBox.Shadow = true;
```
- PlacementType.FreeFloating: Deze eigenschap zorgt ervoor dat de keuzelijst op zijn positie blijft staan, ongeacht hoe het werkblad wordt gewijzigd.
- LinkedCell: Hiermee stelt u een cel in (in dit geval A1) waarin de geselecteerde waarde uit de keuzelijst wordt weergegeven.
- InputRange: Hiermee vertelt u de keuzelijst waar deze moet zoeken naar de lijst met opties (A2 tot en met A7, die we eerder hebben ingesteld).
- SelectionType.Single: Hiermee wordt de gebruiker beperkt tot het selecteren van slechts één item uit de keuzelijst.
- Schaduw: Het schaduweffect geeft de keuzelijst een driedimensionaal uiterlijk, waardoor deze visueel aantrekkelijker wordt.
## Stap 6: Sla het Excel-bestand op
Laten we tot slot onze werkmap opslaan, inclusief de keuzelijst.
```csharp
// Sla de werkmap op.
workbook.Save(dataDir + "book1.out.xls");
```
Deze regel code slaat de werkmap op in de directory die we eerder hebben ingesteld. Het bestand heet "book1.out.xls", maar u kunt elke naam kiezen die bij uw project past.
## Conclusie
En daar heb je het! Je hebt succesvol een keuzelijst toegevoegd aan een Excel-werkblad met Aspose.Cells voor .NET. Met slechts een paar regels code hebben we een volledig functionele keuzelijst gemaakt, waardoor het werkblad interactiever en dynamischer is geworden. Deze tutorial zou je een solide basis moeten geven om andere besturingselementen en functies in Aspose.Cells voor .NET te verkennen. Blijf experimenteren en binnenkort zul je de uitgebreide functionaliteit van de bibliotheek onder de knie krijgen!
## Veelgestelde vragen
### Kan ik meerdere selecties in de keuzelijst toestaan?  
 Ja, u kunt de`SelectionType` naar`SelectionType.Multi` om meerdere selecties mogelijk te maken.
### Kan ik het uiterlijk van de keuzelijst wijzigen?  
Absoluut! Met Aspose.Cells kunt u het uiterlijk van de keuzelijst aanpassen, inclusief de grootte, het lettertype en zelfs de kleur.
### Wat als ik de keuzelijst later wil verwijderen?  
 U kunt de keuzelijst openen en verwijderen uit de`Shapes` verzameling met behulp van`sheet.Shapes.RemoveAt(index)`.
### Kan ik de keuzelijst koppelen aan een andere cel?  
 Ja, verander gewoon de`LinkedCell` eigenschap naar een andere cel waarin u de geselecteerde waarde wilt weergeven.
### Hoe voeg ik meer items toe aan de keuzelijst?  
Werk het invoerbereik bij door meer waarden in de opgegeven cellen in te voeren. De keuzelijst wordt dan automatisch bijgewerkt.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
