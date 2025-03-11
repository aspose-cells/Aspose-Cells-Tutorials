---
title: Kopiera VBAMacro User Form Designer Storage till arbetsbok med Aspose.Cells
linktitle: Kopiera VBAMacro User Form Designer Storage till arbetsbok med Aspose.Cells
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du effektivt kopierar VBA Macro User Form Designer i Aspose.Cells för .NET med vår omfattande steg-för-steg handledning! Lås upp Excels potential.
weight: 11
url: /sv/net/workbook-vba-project/copy-vbamacro-user-form-designer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopiera VBAMacro User Form Designer Storage till arbetsbok med Aspose.Cells

## Introduktion
Välkomna! Om du vill förbättra din Excel-upplevelse med VBA-makron och användarformulär är du på rätt plats! I den här guiden dyker vi in på hur du sömlöst kan kopiera en VBA Macro UserForm Designer från en arbetsbok till en annan med Aspose.Cells för .NET. Oavsett om du är en erfaren utvecklare eller precis har börjat, kommer vi att leda dig genom varje avgörande steg. Se detta som din spelbok för att behärska konsten att hantera Excel-filer programmatiskt. Redo att dyka i? Låt oss gå!
## Förutsättningar
Innan vi går in i det snåriga med kodning, låt oss se till att du har allt du behöver:
1. C#-utvecklingsmiljö: Du bör ha en arbetsmiljö redo för C#-utveckling. Visual Studio rekommenderas starkt.
2.  Aspose.Cells för .NET Library: Se till att du har Aspose.Cells-biblioteket integrerat i ditt projekt. Du kan enkelt[ladda ner den här](https://releases.aspose.com/cells/net/).
3. Grundläggande kunskaper om VBA och Excel-makron: En god förståelse för VBA och hur Excel-makron fungerar hjälper dig att enkelt navigera genom den här handledningen.
4. En Excel-fil med ett användarformulär: För att experimentera med, skapa eller skaffa en Excel-arbetsbok som innehåller ett användarformulär, helst med makron aktiverade (som`.xlsm` filer).
## Importera paket
I ditt C#-projekt måste du importera vissa namnområden högst upp i filen för att använda Aspose.Cells-funktioner. Så här gör du:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Vba;
```
Om du inkluderar dessa namnrymder får du tillgång till alla kraftfulla verktyg som är inbäddade i Aspose.Cells-biblioteket. 
Nu när vi har våra förutsättningar och paket täckta är det dags att gå vidare till den roliga delen: kodning! Låt oss dela upp det steg för steg.
## Steg 1: Definiera dina käll- och utdatakataloger
Först måste du fastställa var dina filer finns:
```csharp
// Källkatalog
string sourceDir = "Your Document Directory";
// Utdatakatalog
string outputDir = "Your Document Directory";
```
 Här, byt ut`"Your Document Directory"` med den faktiska sökvägen där dina filer lagras. Det är här vår källarbetsbok (med användarformuläret) kommer att hämtas ifrån och där den nya arbetsboken kommer att sparas.
## Steg 2: Skapa en tom målarbetsbok
Låt oss sedan skapa vår målarbetsbok där vi kopierar våra användarformulär och makron:
```csharp
// Skapa en tom målarbetsbok
Workbook target = new Workbook();
```
Denna kodrad initierar en ny, tom arbetsbok som vi kan fylla med data. Se det som en tom duk för ditt mästerverk!
## Steg 3: Ladda din mallarbetsbok
Vi måste ladda upp arbetsboken som innehåller ditt användarformulär och makron:
```csharp
// Ladda Excel-filen som innehåller VBA-Macro Designer User Form
Workbook templateFile = new Workbook(sourceDir + "sampleDesignerForm.xlsm");
```
 Se till att byta`"sampleDesignerForm.xlsm"` till namnet på din faktiska fil. Den här arbetsboken är som din receptbok – det är det vi kommer att hämta våra ingredienser från!
## Steg 4: Kopiera arbetsblad till målarbetsbok
Låt oss nu börja kopiera kalkylblad från vår mall till målarbetsboken:
```csharp
// Kopiera alla mallkalkylblad till målarbetsboken
foreach (Worksheet ws in templateFile.Worksheets)
{
    if (ws.Type == SheetType.Worksheet)
    {
        Worksheet s = target.Worksheets.Add(ws.Name);
        s.Copy(ws);
        // Lägg meddelandet i cell A2 i målarbetsbladet
        s.Cells["A2"].PutValue("VBA Macro and User Form copied from template to target.");
    }
}
```
I det här steget går vi igenom varje kalkylblad i mallen och kopierar dem till vår målarbetsbok. Om du tänker efter är det som att överföra dina bästa recept från en kokbok till en annan!
## Steg 5: Kopiera VBA-makron från mallen
Därefter kopierar vi VBA-makron, inklusive UserForm Designer-modulerna, till vår nya arbetsbok:
```csharp
// Kopiera VBA-Macro Designer UserForm från mall till mål
foreach (VbaModule vbaItem in templateFile.VbaProject.Modules)
{
    if (vbaItem.Name == "ThisWorkbook")
    {
        // Kopiera ThisWorkbook-modulkoden
        target.VbaProject.Modules["ThisWorkbook"].Codes = vbaItem.Codes;
    }
    else
    {
        // Kopiera andra modulers kod och data
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
            // Få data från användarformuläret, dvs designerlagring
            byte[] designerStorage = templateFile.VbaProject.Modules.GetDesignerStorage(vbaItem.Name);
            // Lägg till designerlagringen till målet Vba Project
            target.VbaProject.Modules.AddDesignerStorage(vbaItem.Name, designerStorage);
        }
    }
}
```
Denna rejäla kodbit hanterar kontroll av varje VBA-modul i mallfilen. Vi kopierar över UserForm-designen och dess tillhörande koder. Det är som att se till att du inte bara får mormors berömda pajercept utan också hennes exakta bakteknik!
## Steg 6: Spara målarbetsboken
När vi har uppnått alla våra kopior är det dags att spara vårt hårda arbete:
```csharp
// Spara målarbetsboken
target.Save(outputDir + "outputDesignerForm.xlsm", SaveFormat.Xlsm);
```
Se till att ändra utdatafilnamnet efter behov. När du väl har sparat den skapar du effektivt din egen skräddarsydda version av arbetsboken fylld av makron och användarformulär. Hur spännande är det?
## Steg 7: Bekräfta framgång
Låt oss slutligen skriva ut ett framgångsmeddelande till konsolen:
```csharp
Console.WriteLine("CopyVBAMacroUserFormDesignerStorageToWorkbook executed successfully.\r\n");
```
Denna lilla rad försäkrar dig om att din process gick smidigt. Det är körsbäret ovanpå din kodande fruktglass!
## Slutsats
Grattis! Du har slutfört steg-för-steg-guiden för att kopiera en VBA Macro User Form Designer från en arbetsbok till en annan med Aspose.Cells för .NET. Det kan tyckas lite överväldigande till en början, men med övning kommer du att hantera arbetsboksmanipulationer som ett proffs. Kom ihåg att kodning handlar om övning, så dra dig inte för att prova olika saker i dina Excel-filer. Om du har några frågor eller stöter på några problem, kolla gärna in Aspose-forumen eller dokumentationen för support!
## FAQ's
### Vilka versioner av Excel stöder Aspose.Cells?
Aspose.Cells stöder ett brett utbud av Excel-format inklusive XLSX, XLSM, CSV och mer.
### Kan jag använda Aspose.Cells gratis?
 Ja! Du kan börja med en gratis provperiod, som låter dig utvärdera biblioteket:[Gratis provperiod](https://releases.aspose.com/).
### Behöver jag Visual Studio för att köra den här koden?
Även om det rekommenderas starkt på grund av dess användarvänliga funktioner, så fungerar alla C# IDE så länge de stöder .NET-utveckling.
### Var kan jag hitta fler exempel och dokumentation?
 Du kan utforska[Aspose.Cells dokumentation](https://reference.aspose.com/cells/net/) för fler exempel och djupgående förklaringar.
### Hur löser jag problem när jag använder Aspose.Cells?
 Du bör besöka[Aspose Support Forum](https://forum.aspose.com/c/cells/9) för hjälp från samhället och Asposes supportpersonal.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
