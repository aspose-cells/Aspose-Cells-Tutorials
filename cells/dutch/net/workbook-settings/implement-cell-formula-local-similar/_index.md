---
title: Implementeer celformule lokaal vergelijkbaar met bereikformule lokaal
linktitle: Implementeer celformule lokaal vergelijkbaar met bereikformule lokaal
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Ontdek hoe u een celformule implementeert die vergelijkbaar is met de bereikformule lokale functionaliteit in Aspose.Cells voor .NET. Leer hoe u ingebouwde Excel-functienamen aanpast en meer.
weight: 13
url: /nl/net/workbook-settings/implement-cell-formula-local-similar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Implementeer celformule lokaal vergelijkbaar met bereikformule lokaal

## Invoering
Aspose.Cells voor .NET is een krachtige en flexibele API voor spreadsheetmanipulatie waarmee u programmatisch Excel-bestanden kunt maken, manipuleren en converteren. Een van de vele functies die Aspose.Cells biedt, is de mogelijkheid om het gedrag van ingebouwde Excel-functies aan te passen, inclusief de mogelijkheid om uw eigen lokale functienamen te maken. In deze tutorial leiden we u door de stappen om een celformule te implementeren die vergelijkbaar is met de lokale functionaliteit van de bereikformule in Aspose.Cells voor .NET.
## Vereisten
Voordat u begint, moet u ervoor zorgen dat u het volgende bij de hand hebt:
1. Microsoft Visual Studio 2010 of later op uw systeem geïnstalleerd.
2.  De nieuwste versie van de Aspose.Cells for .NET-bibliotheek die in uw project is geïnstalleerd. U kunt de bibliotheek downloaden van de[Aspose.Cells voor .NET downloadpagina](https://releases.aspose.com/cells/net/).
## Pakketten importeren
Om te beginnen moet u de benodigde pakketten importeren in uw C#-project. Voeg de volgende using statements toe bovenaan uw codebestand:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Stap 1: Een aangepaste globalisatie-instellingenklasse maken
 De eerste stap is het maken van een aangepaste`GlobalizationSettings`klasse waarmee u het standaardgedrag van Excel-functies kunt overschrijven. In dit voorbeeld wijzigen we de namen van de`SUM` En`AVERAGE` functies om`UserFormulaLocal_SUM` En`UserFormulaLocal_AVERAGE`, respectievelijk.
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //Wijzig de naam van de SUM-functie naar wens.
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //Wijzig de naam van de functie GEMIDDELDE naar wens.
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## Stap 2: Maak een nieuwe werkmap en wijs de aangepaste globalisatie-instellingen toe
 Maak vervolgens een nieuw werkmapexemplaar en wijs de aangepaste`GlobalizationSettings` implementatieklasse voor de werkmap`Settings.GlobalizationSettings` eigendom.
```csharp
//Werkmap maken
Workbook wb = new Workbook();
//Implementatieklasse GlobalizationSettings toewijzen
wb.Settings.GlobalizationSettings = new GS();
```
## Stap 3: Toegang tot het eerste werkblad en een cel
Laten we nu naar het eerste werkblad in de werkmap gaan en naar een specifieke cel in dat werkblad.
```csharp
//Toegang tot eerste werkblad
Worksheet ws = wb.Worksheets[0];
//Toegang tot een cel
Cell cell = ws.Cells["C4"];
```
## Stap 4: Formules toewijzen en de formule afdrukkenLokaal
 Laten we ten slotte de`SUM` En`AVERAGE` formules naar de cel en print de resulterende`FormulaLocal` waarden.
```csharp
//Wijs de SUM-formule toe en druk de FormulaLocal af
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//Wijs de GEMIDDELDE formule toe en druk de FormulaLocal af
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## Conclusie
In deze tutorial hebt u geleerd hoe u een celformule implementeert die vergelijkbaar is met de lokale functionaliteit van de bereikformule in Aspose.Cells voor .NET. Door een aangepaste`GlobalizationSettings` klasse, kunt u het standaardgedrag van Excel-functies overschrijven en de lokale functienamen aanpassen aan uw behoeften. Dit kan met name handig zijn bij het werken met gelokaliseerde of geïnternationaliseerde Excel-documenten.
## Veelgestelde vragen
###  Wat is het doel van de`GlobalizationSettings` class in Aspose.Cells?
 De`GlobalizationSettings` Met de klasse Aspose.Cells kunt u het gedrag van ingebouwde Excel-functies aanpassen, inclusief de mogelijkheid om de namen van lokale functies te wijzigen.
###  Kan ik het gedrag van andere functies dan`SUM` and `AVERAGE`?
 Ja, u kunt het gedrag van elke ingebouwde Excel-functie overschrijven door de`GetLocalFunctionName` methode in uw aangepaste`GlobalizationSettings` klas.
### Is er een manier om de functienamen terug te zetten naar de standaardwaarden?
 Ja, u kunt de functienamen opnieuw instellen door de aangepaste`GlobalizationSettings` klasse of door een lege string terug te sturen van de`GetLocalFunctionName` methode.
### Kan ik deze functie gebruiken om aangepaste functies in Aspose.Cells te maken?
 Nee, de`GlobalizationSettings`klasse is ontworpen om het gedrag van ingebouwde Excel-functies te overschrijven, niet om aangepaste functies te maken. Als u aangepaste functies moet maken, kunt u de`UserDefinedFunction` klasse in Aspose.Cells.
### Is deze functie beschikbaar in alle versies van Aspose.Cells voor .NET?
 Ja, de`GlobalizationSettings` klasse en de mogelijkheid om functienamen aan te passen is beschikbaar in alle versies van Aspose.Cells voor .NET.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
