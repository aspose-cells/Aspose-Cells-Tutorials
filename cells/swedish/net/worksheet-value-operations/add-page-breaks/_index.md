---
title: Lägg till sidbrytningar i kalkylblad med Aspose.Cells
linktitle: Lägg till sidbrytningar i kalkylblad med Aspose.Cells
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du lägger till horisontella och vertikala sidbrytningar i Excel med Aspose.Cells för .NET med denna steg-för-steg-guide. Gör dina Excel-filer utskriftsvänliga.
weight: 10
url: /sv/net/worksheet-value-operations/add-page-breaks/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till sidbrytningar i kalkylblad med Aspose.Cells

## Introduktion
I den här självstudien går vi igenom processen att lägga till både horisontella och vertikala sidbrytningar i ditt Excel-kalkylblad. Du kommer också att se en steg-för-steg-guide om hur du använder Aspose.Cells för .NET för att enkelt manipulera sidbrytningar, och i slutet av den här guiden kommer du att vara bekväm med att använda dessa tekniker i dina egna projekt. Låt oss komma igång!
## Förutsättningar
Innan vi dyker in i koden, låt oss se till att du är redo att följa den här handledningen. Här är några förutsättningar:
- Visual Studio: Du behöver Visual Studio installerat på ditt system.
-  Aspose.Cells för .NET: Du bör ha Aspose.Cells-biblioteket installerat. Om du inte har gjort det ännu, oroa dig inte! Du kan ladda ner en gratis testversion för att komma igång. (Du kan få det[här](https://releases.aspose.com/cells/net/)).
- .NET Framework: Denna handledning förutsätter att du arbetar med .NET Framework eller .NET Core. Om du använder en annan miljö kan processen variera något.
Dessutom bör du ha grundläggande kunskaper i C#-programmering och konceptet med sidbrytningar i Excel.
## Importera paket
För att börja arbeta med Aspose.Cells måste vi importera de relevanta namnområdena till vårt projekt. Detta ger oss tillgång till funktionerna som tillhandahålls av Aspose.Cells för att manipulera Excel-filer.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
När du har importerat dessa namnområden kan du börja interagera med Excel-filer och tillämpa olika ändringar, inklusive att lägga till sidbrytningar.
Nu när du är konfigurerad, låt oss gå igenom stegen för att lägga till sidbrytningar i ditt kalkylblad. Vi kommer att bryta ner varje del av processen och förklara varje kodrad i detalj.
## Steg 1: Konfigurera din arbetsbok
 Först måste du skapa en ny arbetsbok. De`Workbook` klass i Aspose.Cells representerar en Excel-arbetsbok och är utgångspunkten för att manipulera Excel-filer.
```csharp
// Definiera sökvägen till katalogen där din fil ska sparas
string dataDir = "Your Document Directory";
// Skapa ett nytt arbetsboksobjekt
Workbook workbook = new Workbook();
```
I denna kod:
- `dataDir` anger var din fil ska sparas.
-  De`Workbook` objekt skapas, som kommer att användas för att hålla och manipulera din Excel-fil.
## Steg 2: Lägg till horisontell sidbrytning
Därefter lägger vi till en horisontell sidbrytning i kalkylbladet. En horisontell sidbrytning kommer att dela upp kalkylbladet i två delar horisontellt, vilket innebär att det avgör var innehållet kommer att brytas vertikalt på en ny sida vid utskrift.
```csharp
//Lägg till en horisontell sidbrytning på rad 30
workbook.Worksheets[0].HorizontalPageBreaks.Add("Y30");
```
I det här exemplet:
- `Worksheets[0]` hänvisar till det första bladet i arbetsboken (kom ihåg att kalkylblad är nollindexerade).
- `HorizontalPageBreaks.Add("Y30")` lägger till en sidbrytning på rad 30. Detta innebär att innehållet före rad 30 kommer att visas på en sida, och allt under det kommer att börja på en ny sida.
## Steg 3: Lägg till vertikal sidbrytning
På samma sätt kan du lägga till en vertikal sidbrytning. Detta kommer att bryta kalkylbladet i en specifik kolumn, vilket säkerställer att innehållet till vänster om pausen visas på en sida och innehållet till höger visas på nästa.
```csharp
// Lägg till en vertikal sidbrytning i kolumn Y
workbook.Worksheets[0].VerticalPageBreaks.Add("Y30");
```
Här:
-  De`VerticalPageBreaks.Add("Y30")` metod lägger till en vertikal sidbrytning vid kolumn Y (dvs efter den 25:e kolumnen). Detta skapar en sidbrytning mellan kolumnerna X och Y.
## Steg 4: Spara arbetsboken
När du har lagt till dina sidbrytningar är det sista steget att spara arbetsboken i en fil. Du kan ange sökvägen där du vill spara Excel-filen.
```csharp
// Spara Excel-filen
workbook.Save(dataDir + "AddingPageBreaks_out.xls");
```
Detta kommer att spara arbetsboken med de tillagda sidbrytningarna till den angivna sökvägen (`AddingPageBreaks_out.xls`).
## Slutsats
Att lägga till sidbrytningar i Excel är en avgörande funktion när du arbetar med stora datamängder eller förbereder dokument för utskrift. Med Aspose.Cells för .NET kan du enkelt automatisera processen att infoga både horisontella och vertikala sidbrytningar i dina Excel-kalkylblad, vilket säkerställer att dina dokument är välorganiserade och lätta att läsa.
## FAQ's
### Hur lägger jag till flera sidbrytningar i Aspose.Cells för .NET?
 Du kan lägga till flera sidbrytningar genom att helt enkelt anropa`HorizontalPageBreaks.Add()` eller`VerticalPageBreaks.Add()` metoder flera gånger med olika cellreferenser.
### Kan jag lägga till sidbrytningar i ett specifikt kalkylblad i en arbetsbok?
 Ja, du kan ange kalkylbladet genom att använda`Worksheets[index]` egendom var`index` är det nollbaserade indexet för kalkylbladet.
### Hur tar jag bort en sidbrytning i Aspose.Cells för .NET?
 Du kan ta bort en sidbrytning med hjälp av`HorizontalPageBreaks.RemoveAt()` eller`VerticalPageBreaks.RemoveAt()` metoder genom att ange indexet för sidbrytningen du vill ta bort.
### Vad händer om jag vill lägga till sidbrytningar automatiskt baserat på innehållets storlek?
Aspose.Cells tillhandahåller inte en automatisk funktion för att lägga till sidbrytningar baserat på innehållsstorlek, men du kan programmatiskt beräkna var avbrott ska ske baserat på antal rader/kolumner.
### Kan jag ställa in sidbrytningar baserat på ett specifikt cellintervall?
Ja, du kan ange sidbrytningar för valfri cell eller område genom att ange motsvarande cellreferens, till exempel "A1" eller "B15".

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
