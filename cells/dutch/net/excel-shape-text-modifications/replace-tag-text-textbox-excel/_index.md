---
title: Tag vervangen door tekst in tekstvak in Excel
linktitle: Tag vervangen door tekst in tekstvak in Excel
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Vervang moeiteloos tekst in tekstvakken in uw Excel-sheets met Aspose.Cells voor .NET. Een stapsgewijze handleiding voor Excel-automatisering.
weight: 11
url: /nl/net/excel-shape-text-modifications/replace-tag-text-textbox-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tag vervangen door tekst in tekstvak in Excel

## Invoering
In dit artikel duiken we in een specifieke taak: tags vervangen door tekst in tekstvakken in een Excel-sheet met Aspose.Cells. We leiden je stap voor stap door het hele proces, zodat je elk detail begrijpt. Aan het einde van deze tutorial heb je niet alleen je begrip van Aspose.Cells verbeterd, maar ook je Excel-gerelateerde taken gestroomlijnd!
## Vereisten
Voordat u kunt beginnen, moet u een aantal dingen klaar hebben:
1. Visual Studio: Zorg ervoor dat u Visual Studio hebt geïnstalleerd. Het is een flexibele IDE die coderen in C# een fluitje van een cent maakt.
2.  Aspose.Cells-bibliotheek: Als u dat nog niet hebt gedaan, download dan de Aspose.Cells-bibliotheek voor .NET van de[pagina](https://releases.aspose.com/cells/net/)kunt ook een gratis proefversie downloaden om de functies ervan uit te proberen.
3. Basiskennis van C#: Een basiskennis van C#-programmering helpt u bij het volgen van deze gids.
Nu je alles hebt ingesteld, kunnen we beginnen met het leukste gedeelte: het schrijven van de code!
## Pakketten importeren
Laten we eerst de benodigde pakketten importeren. Dit is cruciaal, want zonder de juiste imports herkent uw code de klassen en methoden die we gaan gebruiken niet.
## Start uw C#-project
Open Visual Studio en maak een nieuw C#-project, bij voorkeur een consoletoepassing, omdat u hiermee de uitvoer eenvoudig kunt bekijken.
## Voeg Aspose.Cells-referentie toe
- Klik met de rechtermuisknop op uw project in de Solution Explorer.
- Selecteer “Toevoegen” > “Referentie”.
- Blader naar de locatie waar u de Aspose.Cells-bibliotheek hebt gedownload en neem deze op in uw project.
## Importeer de benodigde naamruimten
 Nadat u de referentie hebt toegevoegd, voegt u het volgende toe`using` richtlijn bovenaan uw hoofdbestand:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Hiermee krijgt u toegang tot klassen binnen de Aspose.Cells-naamruimte.
Nu we onze omgeving hebben ingesteld, kunnen we beginnen met het sappige gedeelte: coderen! Ons doel is om specifieke tags in tekstvakken in een Excel-bestand te vinden en deze te vervangen door de meegeleverde tekst.
## Stap 1: Definieer de bron- en uitvoermap
Eerst moeten we aangeven waar ons Excel-bronbestand zich bevindt en waar we de gewijzigde versie willen opslaan.
```csharp
// Bron- en uitvoermap
string sourceDir = "Your Document Directory"; // Wijzigen in uw directory
string outputDir = "Your Document Directory"; // Wijzigen in uw directory
```
## Stap 2: Laad de werkmap
Hier laden we onze Excel-werkmap. Als het bestand niet bestaat, geeft het een foutmelding. Zorg er dus voor dat het bestandspad correct is!
```csharp
Workbook wb = new Workbook(sourceDir + "sampleReplaceTagWithText.xlsx");
```
 Hier laden we een bestaand Excel-bestand met de naam`sampleReplaceTagWithText.xlsx`.
## Stap 3: Tags en vervangende tekst definiëren
Vervolgens moeten we definiëren welke tags we zoeken en waarmee we ze willen vervangen.
```csharp
string tag = "TAG_2$TAG_1";
string replace = "1$ys";
```
 In dit voorbeeld worden de tags gesplitst met behulp van`$`U kunt dit vervangen door elk gewenst scheidingsteken.
## Stap 4: Loop over tags en vervang
We maken een lus om door elke tag te gaan die we willen vervangen. Hier gebeurt de magie!
```csharp
for (int i = 0; i < tag.Split('$').Length; i++)
{
    sheetReplace(wb, "<" + tag.Split('$')[i] + ">", replace.Split('$')[i]);
}
```
## Stap 5: Sla de werkmap op
Nu we onze vervangingen hebben gemaakt, is het tijd om de aangepaste werkmap op te slaan in een gewenst formaat. Hier is hoe we het converteren naar een PDF.
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
wb.Save(outputDir + "outputReplaceTagWithText.pdf", opts);
```
U kunt het ook in verschillende andere formaten opslaan, waaronder XLSX.
## Stap 6: Implementeer de vervangingslogica
 Dit is waar het hart van onze functionaliteit zich bevindt. De`sheetReplace` Deze methode zal de daadwerkelijke vervanging in de Excel-werkbladen verwerken.
```csharp
public static void sheetReplace(Workbook workbook, string sFind, string sReplace)
{
    string finding = sFind;
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sheet.Replace(finding, sReplace);
        for (int j = 0; j < 3; j++)
        {
            if (sheet.PageSetup.GetHeader(j) != null)
                sheet.PageSetup.SetHeader(j, sheet.PageSetup.GetHeader(j).Replace(finding, sReplace));
                
            if (sheet.PageSetup.GetFooter(j) != null)
                sheet.PageSetup.SetFooter(j, sheet.PageSetup.GetFooter(j).Replace(finding, sReplace));
        }
    }
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sFind = sFind.Replace("<", "&lt;");
        sFind = sFind.Replace(">", "&gt;");
        foreach (Aspose.Cells.Drawing.TextBox mytextbox in sheet.TextBoxes)
        {
            if (mytextbox.HtmlText != null)
            {
                if (mytextbox.HtmlText.IndexOf(sFind) >= 0)
                {
                    mytextbox.HtmlText = mytextbox.HtmlText.Replace(sFind, sReplace);
                }
            }
        }
    }
}
```
- Eerst doorlopen we elk werkblad in de werkmap.
- We vervangen de hoofdtag niet alleen in de celinhoud, maar ook in de kop- en voetteksten (indien aanwezig).
- Ten slotte controleren we elk tekstvak in het werkblad en vervangen we de tekst erin op basis van de tag die we zoeken.
## Conclusie
En voila! U hebt nu geleerd hoe u tags vervangt met tekst in tekstvakken in uw Excel-documenten met Aspose.Cells voor .NET. Dit kan een echte tijdsbesparing zijn, vooral bij het werken met repetitieve taken in spreadsheets.
## Veelgestelde vragen
### Kan ik tags in meerdere Excel-bestanden tegelijk vervangen?
Ja, door een lijst met bestanden te doorlopen, kunt u dezelfde logica op meerdere Excel-bestanden toepassen.
### Heb ik een betaalde licentie nodig om Aspose.Cells te gebruiken?
 U kunt beginnen met een gratis proefperiode, maar voor volledige functionaliteit moet u een licentie aanschaffen. Bekijk[Aankoopopties van Aspose](https://purchase.aspose.com/buy).
### Kan ik afbeeldingen in tekstvakken vervangen met Aspose.Cells?
Aspose.Cells gaat voornamelijk over tekst. U kunt echter afbeeldingen afzonderlijk manipuleren indien nodig.
### In welke formaten kan ik mijn gewijzigde Excel-bestand opslaan?
U kunt het in verschillende formaten opslaan, waaronder XLSX, PDF, CSV, enz.
### Waar kan ik ondersteuning vinden voor Aspose.Cells?
 U kunt ondersteuning vinden en vragen stellen op de[Aspose-forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
