---
title: Ladda endast synliga ark från Excel-fil
linktitle: Ladda endast synliga ark från Excel-fil
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du laddar endast synliga ark från Excel-filer med Aspose.Cells för .NET i den här steg-för-steg-guiden.
weight: 12
url: /sv/net/excel-file-handling/load-visible-sheets-only/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ladda endast synliga ark från Excel-fil

## Introduktion
När du arbetar med Excel-filer i dina .NET-applikationer blir utmaningen med att hantera flera kalkylblad uppenbar, särskilt när några är dolda eller inte är relevanta för din verksamhet. Aspose.Cells för .NET är ett kraftfullt bibliotek som hjälper dig att manipulera Excel-filer effektivt. I den här artikeln kommer vi att undersöka hur du bara laddar de synliga arken från en Excel-fil och filtrerar bort eventuella dolda data. Om du någonsin har känt dig överväldigad av att navigera i dina Excel-data, är den här guiden för dig!
## Förutsättningar
Innan vi dyker in i handledningen, låt oss se till att du har allt du behöver för att följa med:
1. Grundläggande förståelse för C#: Denna handledning är designad för utvecklare som är bekanta med programmeringsspråket C#.
2.  Aspose.Cells for .NET: Du måste ha Aspose.Cells for .NET-biblioteket nedladdat och konfigurerat. Du kan[ladda ner biblioteket här](https://releases.aspose.com/cells/net/).
3. Visual Studio eller vilken IDE som helst: Du bör ha en IDE där du kan skriva och testa din C#-kod.
4. .NET Framework: Se till att du har det nödvändiga .NET Framework installerat för att köra dina applikationer.
5. Ett exempel på en Excel-fil: För övning, skapa ett exempel på en Excel-fil eller följ koden som tillhandahålls.
Har du allt klart? Fantastisk! Låt oss gå in i det!
## Importera paket
Ett av de första stegen i alla C#-projekt som arbetar med Aspose.Cells är att importera de nödvändiga paketen. Detta ger dig tillgång till alla funktioner som tillhandahålls av biblioteket. Så här gör du:
1. Öppna ditt projekt: Börja med att öppna ditt C#-projekt i Visual Studio eller någon annan föredragen IDE.
2. Lägg till referenser: Högerklicka på ditt projekt i Solution Explorer, välj "Lägg till" och sedan "Referens". 
3. Bläddra efter Aspose.Cells: Leta upp filen Aspose.Cells.dll som du laddade ner tidigare och lägg till den i dina projektreferenser.
Detta steg är avgörande eftersom det länkar Aspose.Cells-funktionaliteten till ditt projekt. 
```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Nu när du har importerat de nödvändiga paketen skapar vi ett exempel på en Excel-arbetsbok. I den här arbetsboken kommer vi att ha flera ark, och ett av dem kommer att döljas för den här handledningen.
## Steg 1: Ställ in din miljö
Låt oss först ställa in miljön och ange sökvägarna för exempelfilen.
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
string sampleFile = "output.xlsx";
string samplePath = dataDir + sampleFile;
```
 I det här kodavsnittet, ersätt`"Your Document Directory"` med den faktiska sökvägen där du vill spara din arbetsbok. 
## Steg 2: Skapa arbetsboken
Låt oss sedan skapa arbetsboken och lägga till lite data.
```csharp
// Skapa en exempelarbetsbok
Workbook createWorkbook = new Workbook();
createWorkbook.Worksheets["Sheet1"].Cells["A1"].Value = "Aspose";
createWorkbook.Worksheets.Add("Sheet2").Cells["A1"].Value = "Aspose";
createWorkbook.Worksheets.Add("Sheet3").Cells["A1"].Value = "Aspose";
createWorkbook.Worksheets["Sheet3"].IsVisible = false; // Gör Sheet3 dolt
createWorkbook.Save(samplePath);
```
Här är en sammanfattning av vad som händer:
- Vi skapar en ny arbetsbok och lägger till tre ark.
- "Sheet1" och "Sheet2" kommer att vara synliga, medan "Sheet3" kommer att döljas.
- Vi sparar sedan arbetsboken till den angivna sökvägen.
## Steg 3: Ladda provarbetsboken med laddningsalternativ
Nu när vi har en arbetsbok med synliga och dolda ark är det dags att ladda den samtidigt som vi ser till att vi bara kommer åt de synliga arken.
```csharp
LoadOptions loadOptions = new LoadOptions();
loadOptions.LoadFilter = new CustomLoad();
```
Det här kodavsnittet ställer in laddningsalternativen för arbetsboken, som vi kommer att anpassa för att filtrera bort dolda ark.
## Steg 4: Definiera det anpassade belastningsfiltret
För att bara ladda synliga ark måste vi skapa ett anpassat laddningsfilter. Så här definierar du det:
```csharp
class CustomLoad : LoadFilter
{
    public override void StartSheet(Worksheet sheet)
    {
        if (sheet.IsVisible)
        {
            this.LoadDataFilterOptions = LoadDataFilterOptions.All;
        }
        else
        {
            this.LoadDataFilterOptions = LoadDataFilterOptions.Structure;
        }
    }
}
```
-  De`StartSheet` metoden kontrollerar om varje ark är synligt.
- Om den är synlig, laddar den all data från det bladet.
- Om det inte är synligt hoppar det över att ladda all data från det bladet.
## Steg 5: Ladda arbetsboken med hjälp av laddningsalternativen
Låt oss nu ladda arbetsboken och visa data från de synliga arken.
```csharp
Workbook loadWorkbook = new Workbook(samplePath, loadOptions);
Console.WriteLine("Sheet1: A1: {0}", loadWorkbook.Worksheets["Sheet1"].Cells["A1"].Value);
Console.WriteLine("Sheet2: A1: {0}", loadWorkbook.Worksheets["Sheet2"].Cells["A1"].Value);
```
 Det här kodavsnittet använder`loadOptions` att endast importera data från de synliga arken och visar innehållet i cell A1 från "Sheet1" och "Sheet2." 
## Slutsats
Och där har du det! Du har framgångsrikt lärt dig hur du bara laddar synliga ark från en Excel-fil med Aspose.Cells för .NET. Att hantera dina Excel-kalkylblad kan vara enkelt när du vet hur du begränsar den data du hämtar och bara arbetar med det du behöver. Detta förbättrar inte bara effektiviteten i dina applikationer utan gör också din kod renare och lättare att hantera. 
## FAQ's
### Kan jag ladda dolda ark om det behövs?
Ja, du kan helt enkelt justera villkoren i det anpassade laddningsfiltret för att inkludera dolda ark.
### Vad används Aspose.Cells till?
Aspose.Cells används för att manipulera Excel-filer utan att Microsoft Excel behöver installeras, och erbjuder funktioner som att läsa, skriva och hantera Excel-kalkylblad.
### Finns det en testversion av Aspose.Cells?
 Ja, det kan du[ladda ner en gratis testversion](https://releases.aspose.com/) för att testa dess funktioner.
### Var kan jag hitta dokumentation för Aspose.Cells?
 De[dokumentation](https://reference.aspose.com/cells/net/) ger omfattande information om alla funktioner.
### Hur köper jag Aspose.Cells?
 Du kan enkelt[köpa Aspose.Cells](https://purchase.aspose.com/buy) från deras köpsida.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
