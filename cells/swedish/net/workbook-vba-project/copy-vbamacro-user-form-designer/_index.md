---
"description": "Lär dig hur du effektivt kopierar VBA Macro User Form Designer i Aspose.Cells för .NET med vår omfattande steg-för-steg-handledning! Frigör Excels potential."
"linktitle": "Kopiera VBAMacro User Form Designer Storage till arbetsbok med Aspose.Cells"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Kopiera VBAMacro User Form Designer Storage till arbetsbok med Aspose.Cells"
"url": "/sv/net/workbook-vba-project/copy-vbamacro-user-form-designer/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Kopiera VBAMacro User Form Designer Storage till arbetsbok med Aspose.Cells

## Introduktion
Välkommen! Om du vill förbättra din Excel-upplevelse med VBA-makron och användarformulär har du kommit rätt! I den här guiden går vi in på hur du smidigt kan kopiera en VBA-makro UserForm Designer från en arbetsbok till en annan med hjälp av Aspose.Cells för .NET. Oavsett om du är en erfaren utvecklare eller precis har börjat, kommer vi att guida dig genom varje viktig steg. Se detta som din handbok för att bemästra konsten att hantera Excel-filer programmatiskt. Redo att dyka in? Nu kör vi!
## Förkunskapskrav
Innan vi går in på det allra viktigaste med kodning, låt oss se till att du har allt du behöver:
1. C#-utvecklingsmiljö: Du bör ha en arbetsmiljö redo för C#-utveckling. Visual Studio rekommenderas starkt.
2. Aspose.Cells för .NET-biblioteket: Se till att du har Aspose.Cells-biblioteket integrerat i ditt projekt. Du kan enkelt [ladda ner den här](https://releases.aspose.com/cells/net/).
3. Grundläggande kunskaper om VBA och Excel-makron: En god förståelse för VBA och hur Excel-makron fungerar hjälper dig att navigera genom den här handledningen med lätthet.
4. En Excel-fil med ett användarformulär: För att experimentera, skapa eller hämta en Excel-arbetsbok som innehåller ett användarformulär, helst med makron aktiverade (som `.xlsm` filer).
## Importera paket
I ditt C#-projekt måste du importera vissa namnrymder högst upp i din fil för att kunna använda Aspose.Cells-funktioner. Så här gör du:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Vba;
```
Genom att inkludera dessa namnrymder får du tillgång till alla kraftfulla verktyg som är inbäddade i Aspose.Cells-biblioteket. 
Nu när vi har täckt våra förkunskapskrav och paket är det dags att gå vidare till den roliga delen: kodning! Låt oss gå igenom det steg för steg.
## Steg 1: Definiera dina käll- och utdatakataloger
Först måste du fastställa var dina filer finns:
```csharp
// Källkatalog
string sourceDir = "Your Document Directory";
// Utdatakatalog
string outputDir = "Your Document Directory";
```
Här, ersätt `"Your Document Directory"` med den faktiska sökvägen där dina filer lagras. Det är härifrån vår källarbetsbok (med UserForm) hämtas och där den nya arbetsboken sparas.
## Steg 2: Skapa en tom målarbetsbok
Nu ska vi skapa vår målarbetsbok där vi ska kopiera vårt användarformulär och våra makron:
```csharp
// Skapa en tom målarbetsbok
Workbook target = new Workbook();
```
Den här kodraden initierar en ny, tom arbetsbok som vi kan fylla med data. Tänk på den som en tom duk för ditt mästerverk!
## Steg 3: Ladda din mallarbetsbok
Vi behöver ladda upp arbetsboken som innehåller ditt användarformulär och makron:
```csharp
// Ladda Excel-filen som innehåller VBA-Makrodesignerns användarformulär
Workbook templateFile = new Workbook(sourceDir + "sampleDesignerForm.xlsm");
```
Se till att ändra `"sampleDesignerForm.xlsm"` till namnet på din faktiska fil. Den här arbetsboken är som din kokbok – det är från den vi hämtar våra ingredienser!
## Steg 4: Kopiera kalkylblad till målarbetsboken
Nu ska vi börja kopiera kalkylblad från vår mall till målarbetsboken:
```csharp
// Kopiera alla mallarbetsblad till målarbetsboken
foreach (Worksheet ws in templateFile.Worksheets)
{
    if (ws.Type == SheetType.Worksheet)
    {
        Worksheet s = target.Worksheets.Add(ws.Name);
        s.Copy(ws);
        // Placera meddelandet i cell A2 i målarbetsbladet
        s.Cells["A2"].PutValue("VBA Macro and User Form copied from template to target.");
    }
}
```
I det här steget loopar vi igenom varje arbetsblad i mallen och kopierar dem till vår målarbetsbok. Om du tänker efter är det som att överföra dina bästa recept från en kokbok till en annan!
## Steg 5: Kopiera VBA-makron från mallen
Härnäst kopierar vi VBA-makron, inklusive UserForm Designer-modulerna, till vår nya arbetsbok:
```csharp
// Kopiera VBA-makrodesignerns användarformulär från mall till mål
foreach (VbaModule vbaItem in templateFile.VbaProject.Modules)
{
    if (vbaItem.Name == "ThisWorkbook")
    {
        // Kopiera ThisWorkbook-modulens kod
        target.VbaProject.Modules["ThisWorkbook"].Codes = vbaItem.Codes;
    }
    else
    {
        // Kopiera kod och data för andra moduler
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
            // Hämta data från användarformuläret, dvs. designerlagring
            byte[] designerStorage = templateFile.VbaProject.Modules.GetDesignerStorage(vbaItem.Name);
            // Lägg till designerlagringen till mål-VBA-projektet
            target.VbaProject.Modules.AddDesignerStorage(vbaItem.Name, designerStorage);
        }
    }
}
```
Denna rejäla kodbit hanterar kontrollen av varje VBA-modul i mallfilen. Vi kopierar över UserForm-designen och dess tillhörande kod. Det är som att se till att du inte bara får mormors berömda pajrecept utan också hennes exakta baktekniker!
## Steg 6: Spara målarbetsboken
När vi har fått alla våra kopior är det dags att spara vårt hårda arbete:
```csharp
// Spara målarbetsboken
target.Save(outputDir + "outputDesignerForm.xlsm", SaveFormat.Xlsm);
```
Se till att ändra filnamnet efter behov. När du har sparat den skapar du i praktiken din egen skräddarsydda version av arbetsboken, full av makron och användarformulär. Hur spännande är inte det?
## Steg 7: Bekräfta att det lyckades
Slutligen, låt oss skriva ut ett framgångsmeddelande till konsolen:
```csharp
Console.WriteLine("CopyVBAMacroUserFormDesignerStorageToWorkbook executed successfully.\r\n");
```
Den här lilla raden försäkrar dig om att din process gick smidigt. Det är pricken över i:et på din kodglass!
## Slutsats
Grattis! Du har slutfört steg-för-steg-guiden för att kopiera en VBA-makroanvändarformulärdesigner från en arbetsbok till en annan med Aspose.Cells för .NET. Det kan verka lite överväldigande till en början, men med övning kommer du att hantera arbetsboksmanipulationer som ett proffs. Kom ihåg att kodning handlar om övning, så tveka inte att prova olika saker i dina Excel-filer. Om du har några frågor eller stöter på problem kan du gärna kolla in Aspose-forumen eller dokumentationen för support!
## Vanliga frågor
### Vilka versioner av Excel stöds av Aspose.Cells?
Aspose.Cells stöder ett brett utbud av Excel-format, inklusive XLSX, XLSM, CSV och fler.
### Kan jag använda Aspose.Cells gratis?
Ja! Du kan börja med en gratis provperiod, vilket gör att du kan utvärdera biblioteket: [Gratis provperiod](https://releases.aspose.com/).
### Behöver jag Visual Studio för att köra den här koden?
Även om det starkt rekommenderas på grund av dess användarvänliga funktioner, fungerar vilken C# IDE som helst så länge den stöder .NET-utveckling.
### Var kan jag hitta fler exempel och dokumentation?
Du kan utforska [Aspose.Cells-dokumentation](https://reference.aspose.com/cells/net/) för fler exempel och djupgående förklaringar.
### Hur löser jag problem när jag använder Aspose.Cells?
Du borde besöka [Aspose Supportforum](https://forum.aspose.com/c/cells/9) för hjälp från samhället och Asposes supportpersonal.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}