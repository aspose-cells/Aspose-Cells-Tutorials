---
title: Kopieer VBAMacro User Form Designer-opslag naar werkmap met behulp van Aspose.Cells
linktitle: Kopieer VBAMacro User Form Designer-opslag naar werkmap met behulp van Aspose.Cells
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u VBA Macro User Form Designer efficiënt kopieert in Aspose.Cells voor .NET met onze uitgebreide stapsgewijze tutorial! Ontgrendel het potentieel van Excel.
weight: 11
url: /nl/net/workbook-vba-project/copy-vbamacro-user-form-designer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopieer VBAMacro User Form Designer-opslag naar werkmap met behulp van Aspose.Cells

## Invoering
Welkom! Als u uw Excel-ervaring wilt verbeteren met VBA-macro's en gebruikersformulieren, bent u hier aan het juiste adres! In deze gids duiken we in hoe u naadloos een VBA Macro UserForm Designer van de ene werkmap naar de andere kunt kopiëren met Aspose.Cells voor .NET. Of u nu een doorgewinterde ontwikkelaar bent of net begint, we leiden u door elke cruciale stap. Beschouw dit als uw playbook om de kunst van het programmatisch verwerken van Excel-bestanden onder de knie te krijgen. Klaar om erin te duiken? Laten we beginnen!
## Vereisten
Voordat we in de details van het coderen duiken, willen we ervoor zorgen dat je alles hebt wat je nodig hebt:
1. C# Development Environment: U moet een werkomgeving hebben die klaar is voor C#-ontwikkeling. Visual Studio wordt sterk aanbevolen.
2.  Aspose.Cells voor .NET-bibliotheek: zorg ervoor dat u de Aspose.Cells-bibliotheek in uw project hebt geïntegreerd. U kunt eenvoudig[download het hier](https://releases.aspose.com/cells/net/).
3. Basiskennis van VBA- en Excel-macro's: Een goed begrip van VBA en de werking van Excel-macro's helpt u om deze tutorial gemakkelijk te doorlopen.
4. Een Excel-bestand met een gebruikersformulier: om te experimenteren, kunt u een Excel-werkmap maken of verkrijgen die een gebruikersformulier bevat, bij voorkeur met ingeschakelde macro's (zoals`.xlsm` bestanden).
## Pakketten importeren
In uw C#-project moet u bepaalde naamruimten boven aan uw bestand importeren om Aspose.Cells-functionaliteiten te gebruiken. Dit is hoe u dat doet:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Vba;
```
Als u deze naamruimten opneemt, krijgt u toegang tot alle krachtige tools die zijn ingebouwd in de Aspose.Cells-bibliotheek. 
Nu we onze vereisten en pakketten hebben behandeld, is het tijd om door te gaan naar het leuke gedeelte: coderen! Laten we het stap voor stap uitleggen.
## Stap 1: Definieer uw bron- en uitvoermappen
Eerst moet u bepalen waar uw bestanden zich bevinden:
```csharp
// Bron directory
string sourceDir = "Your Document Directory";
// Uitvoermap
string outputDir = "Your Document Directory";
```
 Hier, vervang`"Your Document Directory"` met het werkelijke pad waar uw bestanden zijn opgeslagen. Dit is waar onze bronwerkmap (met het UserForm) vandaan wordt gehaald en waar de nieuwe werkmap wordt opgeslagen.
## Stap 2: Maak een lege doelwerkmap
Laten we nu onze doelwerkmap maken waar we ons gebruikersformulier en onze macro's naartoe kopiëren:
```csharp
// Maak een lege doelwerkmap
Workbook target = new Workbook();
```
Deze regel code initialiseert een nieuwe, lege werkmap die we kunnen vullen met data. Zie het als een leeg canvas voor je meesterwerk!
## Stap 3: Laad uw sjabloonwerkmap
We moeten de werkmap laden die uw gebruikersformulier en macro's bevat:
```csharp
// Laad het Excel-bestand met VBA-Macro Designer User Form
Workbook templateFile = new Workbook(sourceDir + "sampleDesignerForm.xlsm");
```
 Zorg ervoor dat je verandert`"sampleDesignerForm.xlsm"` naar de naam van uw eigenlijke bestand. Deze werkmap is als uw receptenboek: het is waar we onze ingrediënten uit halen!
## Stap 4: Kopieer werkbladen naar doelwerkmap
Laten we nu beginnen met het kopiëren van werkbladen uit onze sjabloon naar de doelwerkmap:
```csharp
// Kopieer alle sjabloonwerkbladen naar de doelwerkmap
foreach (Worksheet ws in templateFile.Worksheets)
{
    if (ws.Type == SheetType.Worksheet)
    {
        Worksheet s = target.Worksheets.Add(ws.Name);
        s.Copy(ws);
        // Plaats bericht in cel A2 van het doelwerkblad
        s.Cells["A2"].PutValue("VBA Macro and User Form copied from template to target.");
    }
}
```
In deze stap doorlopen we elk werkblad in de template en kopiëren we ze naar onze doelwerkmap. Als je erover nadenkt, is het alsof je je beste recepten van het ene kookboek naar het andere overzet!
## Stap 5: VBA-macro's kopiëren uit de sjabloon
Vervolgens kopiëren we de VBA-macro's, inclusief de UserForm Designer-modules, naar onze nieuwe werkmap:
```csharp
// Kopieer het VBA-Macro Designer UserForm van sjabloon naar doel
foreach (VbaModule vbaItem in templateFile.VbaProject.Modules)
{
    if (vbaItem.Name == "ThisWorkbook")
    {
        // Kopieer ThisWorkbook modulecode
        target.VbaProject.Modules["ThisWorkbook"].Codes = vbaItem.Codes;
    }
    else
    {
        // Kopieer code en gegevens van andere modules
        System.Diagnostics.Debug.Print(vbaItem.Name);
        int vbaMod = 0;
        Worksheet sheet = target.Worksheets.GetSheetByCodeName(vbaItem.Name);
        if (sheet == null)
        {
            vbaMod = target.VbaProject.Modules.Add(vbaItem.Type, vbaItem.Name);
        }
        else
        {
            vbaMod = target.VbaProject.Modules.Add(sheet);
        }
        target.VbaProject.Modules[vbaMod].Codes = vbaItem.Codes;
        if ((vbaItem.Type == VbaModuleType.Designer))
        {
            // Haal de gegevens van het gebruikersformulier op, d.w.z. de ontwerperopslag
            byte[] designerStorage = templateFile.VbaProject.Modules.GetDesignerStorage(vbaItem.Name);
            // Voeg de ontwerpopslag toe aan het doel-VBA-project
            target.VbaProject.Modules.AddDesignerStorage(vbaItem.Name, designerStorage);
        }
    }
}
```
Deze flinke brok code regelt het controleren van elke VBA-module in het sjabloonbestand. We kopiëren het UserForm-ontwerp en de bijbehorende codes. Het is alsof je niet alleen het beroemde taartrecept van oma krijgt, maar ook haar exacte baktechnieken!
## Stap 6: Sla de doelwerkmap op
Nadat we al onze kopieën hebben gemaakt, is het tijd om ons harde werk op te slaan:
```csharp
// Sla de doelwerkmap op
target.Save(outputDir + "outputDesignerForm.xlsm", SaveFormat.Xlsm);
```
Zorg ervoor dat u de uitvoerbestandsnaam indien nodig aanpast. Zodra u het opslaat, creëert u effectief uw eigen aangepaste versie van de werkmap vol met macro's en gebruikersformulieren. Hoe spannend is dat?
## Stap 7: Bevestig succes
Ten slotte printen we een succesbericht naar de console:
```csharp
Console.WriteLine("CopyVBAMacroUserFormDesignerStorageToWorkbook executed successfully.\r\n");
```
Deze kleine zin verzekert je ervan dat je proces soepel is verlopen. Het is de kers op de taart van je codeer-sundae!
## Conclusie
Gefeliciteerd! U hebt de stapsgewijze handleiding voor het kopiëren van een VBA Macro User Form Designer van de ene werkmap naar de andere voltooid met Aspose.Cells voor .NET. Het lijkt misschien wat overweldigend in het begin, maar met wat oefening zult u werkmapmanipulaties als een pro kunnen hanteren. Vergeet niet dat coderen draait om oefening, dus schroom niet om verschillende dingen in uw Excel-bestanden te proberen. Als u vragen hebt of problemen ondervindt, kunt u gerust de Aspose-forums of documentatie raadplegen voor ondersteuning!
## Veelgestelde vragen
### Welke versies van Excel worden door Aspose.Cells ondersteund?
Aspose.Cells ondersteunt een breed scala aan Excel-indelingen, waaronder XLSX, XLSM, CSV en meer.
### Kan ik Aspose.Cells gratis gebruiken?
 Ja! U kunt beginnen met een gratis proefperiode, waarmee u de bibliotheek kunt evalueren:[Gratis proefperiode](https://releases.aspose.com/).
### Heb ik Visual Studio nodig om deze code uit te voeren?
Hoewel het sterk wordt aanbevolen vanwege de gebruiksvriendelijke functies, voldoet elke C# IDE, zolang deze maar .NET-ontwikkeling ondersteunt.
### Waar kan ik meer voorbeelden en documentatie vinden?
 Je kunt de[Aspose.Cells-documentatie](https://reference.aspose.com/cells/net/) voor meer voorbeelden en diepgaande uitleg.
### Hoe los ik problemen op bij het gebruik van Aspose.Cells?
 Je moet de[Aspose Ondersteuningsforum](https://forum.aspose.com/c/cells/9) voor hulp van de community en Aspose-ondersteunend personeel.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
