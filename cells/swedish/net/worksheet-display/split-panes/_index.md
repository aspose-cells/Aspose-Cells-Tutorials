---
title: Dela paneler i kalkylblad med Aspose.Cells
linktitle: Dela paneler i kalkylblad med Aspose.Cells
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du delar upp kalkylbladsrutor med Aspose.Cells för .NET i en steg-för-steg-guide. Perfekt för förbättrad dataanalys och vyanpassning.
weight: 21
url: /sv/net/worksheet-display/split-panes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dela paneler i kalkylblad med Aspose.Cells

## Introduktion
Att dela upp kalkylbladsrutor är ett fantastiskt sätt att arbeta med stora datamängder i Excel. Föreställ dig att du har rader på rader med data men att du behöver jämföra värden högst upp och längst ned på arket – utan att ständigt rulla. Det är där delade rutor kommer till undsättning. Med Aspose.Cells för .NET kan du enkelt dela upp rutor i ett kalkylblad programmatiskt, vilket sparar tid och gör din dataanalys mycket smidigare.
I den här handledningen kommer vi att dyka in i detaljerna för att använda Aspose.Cells för .NET för att dela upp rutor i ett Excel-kalkylblad. Med varje steg nedbrutet, kommer du att tycka att det är lätt att följa och tillämpa. Är du redo att effektivisera ditt dataarbete? Låt oss dyka in!
## Förutsättningar
Innan du börjar, se till att du har följande på plats:
1. Aspose.Cells för .NET: Ladda ner och installera Aspose.Cells-biblioteket från[Aspose.Cells nedladdningssida](https://releases.aspose.com/cells/net/). Du behöver en licensierad eller testversion för att använda alla funktioner.
2. IDE: Konfigurera en .NET-kompatibel IDE som Visual Studio.
3. Grundläggande C#-kunskaper: Bekantskap med C#- och .NET-programmeringsgrunderna kommer att vara till hjälp för att följa med kodexemplen.
## Importera paket
För att använda Aspose.Cells för .NET, börja med att importera de nödvändiga namnrymden till ditt projekt. Dessa namnområden innehåller de klasser och metoder som krävs för att hantera Excel-arbetsböcker och kalkylblad.
```csharp
using System.IO;
using Aspose.Cells;
```
Nedan kommer vi att dela upp varje steg i ett kalkylblad med Aspose.Cells för .NET.
## Steg 1: Initiera arbetsboken
 Det första steget är att skapa en`Workbook` instans, som låter dig arbeta med dina Excel-filer. Du kan antingen skapa en ny arbetsbok eller ladda en befintlig fil. Så här gör du:
```csharp
// Definiera sökvägen till dokumentkatalogen
string dataDir = "Your Document Directory";
// Instantiera en ny arbetsbok genom att ladda en befintlig Excel-fil
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
I denna kod:
- `dataDir` representerar platsen för din Excel-fil.
- `Book1.xls` är filen vi ska arbeta med. Ersätt den med ditt eget filnamn efter behov.
## Steg 2: Ställ in den aktiva cellen
Nu ska vi specificera den aktiva cellen. Att ställa in en aktiv cell är särskilt användbart när du delar upp rutor, eftersom det avgör var delingen kommer att ske.
```csharp
// Ställ in den aktiva cellen till "A20" i det första kalkylbladet
workbook.Worksheets[0].ActiveCell = "A20";
```
Här:
- Vi kommer åt det första kalkylbladet i arbetsboken (`workbook.Worksheets[0]`).
- `"A20"`är cellen vi anger som aktiv cell. Du kan ändra detta baserat på var du vill att uppdelningen ska ske.
## Steg 3: Dela kalkylbladsrutan
 Med den aktiva celluppsättningen är vi nu redo att dela upp kalkylbladet. Aspose.Cells låter dig dela upp rutor utan ansträngning med`Split` metod.
```csharp
// Dela kalkylbladsfönstret i den aktiva cellen
workbook.Worksheets[0].Split();
```
I det här steget:
-  Kallelse`Split()` på kalkylbladet delar automatiskt rutan vid den aktiva cellen (`A20`).
- Du kommer att se två eller flera rutor, så att du kan visa olika delar av kalkylbladet samtidigt.
## Steg 4: Spara arbetsboken
När du har delat upp rutorna sparar du din arbetsbok för att bevara ändringarna. Låt oss spara den som en ny fil för att undvika att skriva över originalet.
```csharp
// Spara den ändrade arbetsboken
workbook.Save(dataDir + "output.xls");
```
På denna rad:
- `output.xls` är namnet på den nya filen med delade rutor. Du kan byta namn på den eller ange en annan sökväg om du föredrar det.
Och där går du! Du har framgångsrikt delat upp rutor i ett Excel-kalkylblad med Aspose.Cells för .NET. Enkelt, eller hur?
## Slutsats
Dela rutor i Excel är en kraftfull funktion, särskilt när du arbetar med stora datamängder. Genom att följa denna handledning har du lärt dig hur du automatiserar den här funktionen med Aspose.Cells för .NET, vilket ger dig bättre kontroll över datavisualisering och analys. Med Aspose.Cells kan du ytterligare utforska en rad funktioner som att slå samman celler, lägga till diagram och mycket mer.
## FAQ's
### Vad är fördelen med att dela upp rutor i Excel?  
Med delade rutor kan du visa och jämföra data från olika delar av ett kalkylblad samtidigt, vilket gör det lättare att analysera stora datamängder.
### Kan jag styra var rutorna delas?  
Ja, genom att ställa in den aktiva cellen bestämmer du den delade platsen. Uppdelningen kommer att ske vid den specifika cellen.
### Är det möjligt att dela rutor vertikalt och horisontellt?  
Absolut! Genom att ställa in olika aktiva celler kan du skapa vertikala, horisontella eller båda typerna av uppdelningar i kalkylbladet.
### Kan jag ta bort de delade rutorna programmatiskt?  
 Ja, använd`RemoveSplit()`metod för att ta bort de delade rutorna från ditt kalkylblad.
### Behöver jag en licens för att använda Aspose.Cells?  
 Ja, medan du kan prova Aspose.Cells med en gratis provperiod, krävs en licens för obegränsad åtkomst. Du kan få en tillfällig licens[här](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
