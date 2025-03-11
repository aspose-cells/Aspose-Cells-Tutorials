---
title: Selectievakje toevoegen aan werkblad in Excel
linktitle: Selectievakje toevoegen aan werkblad in Excel
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Ontdek hoe u eenvoudig selectievakjes kunt toevoegen aan Excel-werkbladen met Aspose.Cells voor .NET met onze stapsgewijze zelfstudie, compleet met codevoorbeelden en uitleg.
weight: 18
url: /nl/net/excel-shapes-controls/add-checkbox-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Selectievakje toevoegen aan werkblad in Excel

## Invoering
Als het gaat om het beheren van gegevens in Excel, zijn er talloze functies en methoden die uw taken kunnen stroomlijnen en uw spreadsheets kunnen verbeteren. Een van die functies is het selectievakje - een handig hulpmiddel waarmee gebruikers binaire keuzes kunnen maken in hun Excel-werkbladen. In deze gids leiden we u door het proces van het toevoegen van een selectievakje aan een Excel-werkblad met behulp van de Aspose.Cells-bibliotheek voor .NET. Dus, gesp u vast en maak u klaar voor een spannende reis in de wereld van Excel-automatisering!
## Vereisten
Voordat we in de details van het coderen duiken, zorgen we ervoor dat je alles hebt wat je nodig hebt om te beginnen. Dit zijn de vereisten:
- Visuele Studio: We gaan ervan uit dat u een werkomgeving hebt ingesteld met Visual Studio. Als dat niet zo is, kunt u het eenvoudig downloaden van[Visual Studio](https://visualstudio.microsoft.com/vs/).
- .NET Framework: Zorg ervoor dat u het .NET Framework op uw systeem hebt geïnstalleerd. Controleer de compatibiliteit van Aspose.Cells met uw .NET-versie.
-  Aspose.Cells voor .NET: U moet de Aspose.Cells-bibliotheek hebben gedownload en gerefereerd in uw project. U kunt deze downloaden van[hier](https://releases.aspose.com/cells/net/).
- Basiskennis van C#: Een basiskennis van C#-programmering helpt u de voorbeelden gemakkelijker te volgen.
Nu u deze vereisten hebt afgevinkt, kunnen we aan de slag!
## Pakketten importeren
Voordat we beginnen met coderen, moeten we de benodigde pakketten importeren in ons C#-project. De Aspose.Cells-bibliotheek is essentieel voor onze taak en het importeren ervan is een fluitje van een cent. Volg gewoon deze stappen:
### Een nieuw C#-project maken
- Open Visual Studio en maak een nieuwe C# Console-toepassing.
### Voeg een referentie toe aan Aspose.Cells
- Klik met de rechtermuisknop op uw project in de Solution Explorer.
- Selecteer 'NuGet-pakketten beheren'.
- Zoek in de NuGet Package Manager naar 'Aspose.Cells' en installeer het.
### Importeer de naamruimte
Voeg bovenaan het bestand Program.cs de volgende verwijzing naar de naamruimte Aspose.Cells toe:
```csharp
using System.IO;
using Aspose.Cells;
```
Nu bent u helemaal klaar om te beginnen met coderen!

Nu gaan we aan de slag. Hieronder staan de stapsgewijze instructies over hoe u een selectievakje toevoegt aan een Excel-werkblad met Aspose.Cells.
## Stap 1: De directory instellen
Ten eerste moeten we ervoor zorgen dat de directory voor het opslaan van ons Excel-bestand bestaat. Dit is een cruciale stap, omdat het runtime-fouten voorkomt wanneer we ons bestand proberen op te slaan.
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
// Maak een map aan als deze nog niet bestaat.
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
## Stap 2: Een nieuwe werkmap instantiëren
Vervolgens moeten we een nieuwe workbook instance maken. Dit zal dienen als de basis voor ons hele Excel-bestand.
```csharp
// Een nieuwe werkmap maken.
Workbook excelBook = new Workbook();
```
## Stap 3: Voeg een selectievakje toe aan het werkblad
 Laten we nu een selectievakje toevoegen aan het eerste werkblad van onze werkmap. U kunt de positie en grootte van het selectievakje opgeven met behulp van de`Add` methode:
```csharp
// Voeg een selectievakje toe aan het eerste werkblad in de werkmap.
int index = excelBook.Worksheets[0].CheckBoxes.Add(5, 5, 100, 120);
```
## Stap 4: Het Checkbox-object ophalen
Nadat we het selectievakje hebben toegevoegd, moeten we het selectievakjeobject ophalen om verdere aanpassingen te kunnen maken.
```csharp
// Haal het checkbox-object op.
Aspose.Cells.Drawing.CheckBox checkbox = excelBook.Worksheets[0].CheckBoxes[index];
```
## Stap 5: Stel de tekst van het selectievakje in
Wat is een checkbox zonder label? Laten we onze checkbox wat tekst geven zodat gebruikers weten waar het over gaat!
```csharp
// Stel de tekstreeks in.
checkbox.Text = "Click it!";
```
## Stap 6: Koppel het selectievakje aan een cel
Door ons selectievakje aan een specifieke cel te koppelen, kunnen we de status ervan eenvoudig volgen. In dit geval koppelen we het aan cel B1.
```csharp
// Voer een waarde in cel B1 in.
excelBook.Worksheets[0].Cells["B1"].PutValue("LnkCell");
// Stel cel B1 in als gekoppelde cel voor het selectievakje.
checkbox.LinkedCell = "B1";
```
## Stap 7: Standaardwaarde voor selectievakje instellen
Als u wilt dat het selectievakje standaard is aangevinkt wanneer het bestand wordt geopend, kunt u dat ook eenvoudig instellen!
```csharp
// Het selectievakje is standaard ingeschakeld.
checkbox.Value = true;
```
## Stap 8: Sla het Excel-bestand op
Na al deze stappen is het tijd om ons meesterwerk op te slaan in de opgegeven directory. 
```csharp
// Sla het Excel-bestand op.
excelBook.Save(dataDir + "book1.out.xls");
```
En voilà, u hebt een Excel-bestand met een werkend selectievakje gemaakt!
## Conclusie
Gefeliciteerd! U hebt zojuist een selectievakje toegevoegd aan een Excel-werkblad met Aspose.Cells voor .NET. Deze krachtige bibliotheek biedt een veelvoud aan spreadsheetmanipulaties en het toevoegen van selectievakjes is nog maar het begin. U kunt nu uw Excel-documenten aanpassen met interactieve elementen die de gebruikerservaring verbeteren. Waar wacht u nog op? Duik in de wereld van Excel-automatisering en ontdek alle mogelijkheden die Aspose.Cells biedt!
## Veelgestelde vragen
### Wat is Aspose.Cells?
Aspose.Cells is een krachtige .NET-bibliotheek waarmee ontwikkelaars programmatisch Excel-bestanden kunnen maken, bewerken en beheren.
### Kan ik Aspose.Cells gratis gebruiken?
 Ja, Aspose biedt een gratis proefversie van Aspose.Cells. U kunt deze downloaden van[hier](https://releases.aspose.com/).
### Heb ik een licentie nodig om Aspose.Cells te gebruiken?
 Hoewel u de proefversie gratis kunt gebruiken, is een betaalde licentie vereist voor continu gebruik en om toegang te krijgen tot alle functies. U kunt deze kopen[hier](https://purchase.aspose.com/buy).
### Waar kan ik documentatie voor Aspose.Cells vinden?
 De volledige documentatie is beschikbaar[hier](https://reference.aspose.com/cells/net/).
### Hoe kan ik ondersteuning krijgen voor Aspose.Cells?
 Als u vragen hebt of hulp nodig hebt, kunt u het Aspose-ondersteuningsforum bezoeken[hier](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
