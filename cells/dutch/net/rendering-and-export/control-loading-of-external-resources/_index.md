---
"description": "Ontdek hoe u externe bronnen kunt beheren bij de conversie van Excel naar PDF met Aspose.Cells voor .NET met behulp van onze eenvoudig te volgen handleiding."
"linktitle": "Beheer externe bronnen in Excel naar PDF in Aspose.Cells"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Beheer externe bronnen in Excel naar PDF in Aspose.Cells"
"url": "/nl/net/rendering-and-export/control-loading-of-external-resources/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Beheer externe bronnen in Excel naar PDF in Aspose.Cells

## Invoering
In het digitale tijdperk van vandaag is het converteren van Excel-spreadsheets naar PDF-documenten een veelvoorkomende taak. Of het nu gaat om het opstellen van rapporten, financiële gegevens of presentatiemateriaal, u wilt er zeker van zijn dat uw PDF's er precies zo uitzien als u wilt. Aspose.Cells voor .NET is een robuuste bibliotheek waarmee u dit conversieproces tot in de puntjes kunt beheren, met name bij het verwerken van externe bronnen zoals afbeeldingen bij uw Excel-bestanden. In deze handleiding gaan we dieper in op hoe u externe bronnen kunt beheren tijdens de Excel-naar-PDF-conversie met Aspose.Cells. Dus pak uw favoriete drankje en laten we beginnen!
## Vereisten
Voordat we in de details duiken, zorgen we ervoor dat je alles hebt wat je nodig hebt om te kunnen rijden. Hier is een korte checklist:
1. Visual Studio of een andere .NET-compatibele IDE: u hebt een omgeving nodig om uw code te schrijven en testen.
2. Aspose.Cells voor .NET: Als u het nog niet hebt geïnstalleerd, ga dan naar de [Aspose-downloads](https://releases.aspose.com/cells/net/) pagina en download de nieuwste versie.
3. Basiskennis van C#: Kennis van de programmeertaal C# is nuttig. Als je twijfelt over bepaalde concepten, aarzel dan niet om ze op te zoeken.
4. Een voorbeeld van een Excel-bestand: Bereid een Excel-bestand voor met externe bronnen die u wilt converteren. U kunt hiervoor het meegeleverde voorbeeldbestand "samplePdfSaveOptions_StreamProvider.xlsx" gebruiken.
5. Een afbeeldingsbestand voor testen: dit wordt gebruikt als externe bron tijdens de conversie. Het afbeeldingsbestand "newPdfSaveOptions_StreamProvider.png" is een goede tijdelijke aanduiding.
## Pakketten importeren
Om te beginnen moet je de benodigde naamruimten importeren uit de Aspose.Cells-bibliotheek. Dit is cruciaal voor toegang tot de functionaliteiten. Zorg ervoor dat je de volgende using-richtlijnen bovenaan je bestand toevoegt:
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
Deze pakketten bieden alle essentiële klassen en methoden die u nodig hebt om uw taken uit te voeren.
## Stap 1: Maak uw streamproviderklasse aan
De eerste taak is het creëren van een streamproviderklasse die de `IStreamProvider` interface. Met deze klasse kunt u bepalen hoe externe bronnen worden geladen.
```csharp
class MyStreamProvider : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        Debug.WriteLine("-----Close Stream-----");
    }
    public void InitStream(StreamProviderOptions options)
    {
        string sourceDir = "Your Document Directory";
        Debug.WriteLine("-----Init Stream-----");
        // Lees de nieuwe afbeelding in een geheugenstroom en wijs deze toe aan de eigenschap Stream
        byte[] bts = File.ReadAllBytes(sourceDir + "newPdfSaveOptions_StreamProvider.png");
        MemoryStream ms = new MemoryStream(bts);
        options.Stream = ms;
    }
}
```
In deze les:
- CloseStream: Deze methode wordt aangeroepen wanneer de stream gesloten is. Voorlopig schrijven we alleen een debugbericht voor tracking.
- InitStream: Dit is waar de magie begint. Hier lees je je externe afbeelding als een byte-array, converteer je deze naar een geheugenstroom en wijs je deze toe aan de `options.Stream` eigendom.
## Stap 2: Bron- en uitvoermappen instellen
Nu uw streamprovider klaar is, is het tijd om te bepalen waar uw Excel-bestand zich bevindt en waar u uw PDF wilt opslaan.
```csharp
// Bronmap
string sourceDir = "Your Document Directory";
// Uitvoermap
string outputDir = "Your Document Directory";
```
Eenvoudig vervangen `"Your Document Directory"` met het daadwerkelijke pad op uw computer waar uw bestanden zich bevinden. Het is essentieel om uw bestanden georganiseerd te houden!
## Stap 3: Laad uw Excel-bestand
Vervolgens laadt u het Excel-bestand waarvan u de PDF wilt maken.
```csharp
// Bron Excel-bestand laden met externe afbeeldingen
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
Wij gebruiken de `Workbook` klasse van Aspose.Cells, dat uw Excel-bestand vertegenwoordigt. Het bestand kan verschillende externe bronnen bevatten, zoals afbeeldingen, die u tijdens de conversie wilt beheren.
## Stap 4: PDF-opslagopties instellen
Voordat u de werkmap als PDF opslaat, geven we aan hoe u deze wilt opslaan. U kunt deze opties naar wens aanpassen.
```csharp
// PDF-opslagopties specificeren - Streamprovider
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // Sla elk blad op een nieuwe pagina op
```
Hier maken we een nieuw exemplaar van `PdfSaveOptions`waarmee u kunt aanpassen hoe uw PDF wordt opgemaakt. De `OnePagePerSheet` Deze optie is handig om ervoor te zorgen dat elk Excel-werkblad een eigen pagina krijgt in de uiteindelijke PDF.
## Stap 5: Wijs uw streamprovider toe
Nadat u uw PDF-opties hebt ingesteld, moet u Aspose vertellen dat uw aangepaste streamprovider moet worden gebruikt voor externe bronnen.
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
Deze lijn verbindt uw `Workbook` bijvoorbeeld met de `MyStreamProvider` klasse die u eerder hebt aangemaakt. Dit betekent dat wanneer er tijdens de conversie externe bronnen worden aangetroffen, uw provider deze zoals gespecificeerd zal verwerken.
## Stap 6: Sla de werkmap op als PDF
Nu alles is ingesteld, is het tijd om uw Excel-werkmap als PDF op te slaan.
```csharp
// Sla de werkmap op als PDF
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
Door de `Save` Door de methode op het werkmapobject toe te passen en de uitvoermap samen met de PDF-opties door te geven, converteert u het Excel-bestand naar een fraai opgemaakte PDF.
## Stap 7: Bevestig succesvolle uitvoering
Om het af te ronden: het is altijd fijn om te bevestigen dat jouw proces succesvol is geweest!
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
Door een succesbericht op de console af te drukken, blijft u op de hoogte van de status van uw bewerking. Het is een goede gewoonte om deze kleine bevestigingen in uw code op te nemen.
## Conclusie
Zo, dat is het! Door deze eenvoudige stappen te volgen, kunt u met Aspose.Cells vakkundig bepalen hoe externe bronnen worden verwerkt tijdens Excel-naar-PDF-conversies. Dit betekent dat uw documenten nu nauwkeurig afbeeldingen en andere externe elementen kunnen bevatten, wat elke keer weer een gepolijst eindproduct garandeert.
## Veelgestelde vragen
### Wat is Aspose.Cells?  
Aspose.Cells is een krachtige bibliotheek voor .NET-ontwikkelaars waarmee u Excel-bestanden in verschillende indelingen kunt maken, bewerken, converteren en weergeven.
### Hoe download ik Aspose.Cells?  
U kunt de nieuwste versie van Aspose.Cells downloaden van de [Downloadlink](https://releases.aspose.com/cells/net/).
### Kan ik Aspose.Cells gratis uitproberen?  
Ja! U kunt een gratis proefperiode krijgen door naar de [Gratis proefpagina](https://releases.aspose.com/).
### Waar kan ik ondersteuning voor Aspose.Cells vinden?  
Voor alle ondersteuningsgerelateerde vragen kunt u terecht op de [Aspose Supportforum](https://forum.aspose.com/c/cells/9).
### Hoe kan ik een tijdelijke licentie voor Aspose.Cells verkrijgen?  
U kunt een tijdelijke vergunning aanvragen [hier](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}