---
title: Ändra källdata för pivottabellen programmatiskt i .NET
linktitle: Ändra källdata för pivottabellen programmatiskt i .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du ändrar pivottabellens källdata programmatiskt med Aspose.Cells för .NET med vår omfattande steg-för-steg handledning.
weight: 10
url: /sv/net/creating-and-configuring-pivot-tables/changing-source-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ändra källdata för pivottabellen programmatiskt i .NET

## Introduktion
en värld av dataanalys är det få verktyg som lyser så starkt som Microsoft Excel. Varje dag är otaliga användare beroende av Excel för att hantera och analysera data, men bakom kulisserna är det mycket mer komplext än att bara klicka och dra. Om du någonsin har velat manipulera Excel-filer programmässigt – specifikt för att ändra källdata för en pivottabell – är du på rätt plats! I den här guiden kommer vi att utforska hur du kan uppnå detta med Aspose.Cells för .NET. Oavsett om du är en erfaren utvecklare eller bara doppa tårna i havet av programmering, hittar du den här handledningen fullspäckad med värdefull information som är lätt att följa.
## Förutsättningar
Innan vi börjar på vår resa med att ändra källdata för en pivottabell, låt oss se till att du har allt inställt och redo att köra:
1. Visual Studio: Se till att du har en kopia av Microsoft Visual Studio installerad, eftersom vi kommer att skriva vår kod här.
2. Aspose.Cells Library: Du måste ha Aspose.Cells-biblioteket nedladdat och refererat till i ditt projekt. Du kan ladda ner den[här](https://releases.aspose.com/cells/net/).
3. Grundläggande kunskaper om C#: Även om den här handledningen är förenklad, kommer ett grepp om C# att hjälpa dig att bättre förstå koden.
4. Excel-fil: Du bör ha ett exempel på en Excel-fil (som "Book1.xlsx") som innehåller en pivottabell som vi kan manipulera.
Okej, med dessa förutsättningar i schack kan vi fortsätta att importera de nödvändiga paketen och få kodning!
## Importera paket
Först till kvarn – låt oss importera de paket vi behöver. Öppna ditt C#-projekt i Visual Studio och lägg till följande med hjälp av direktiv överst i din kodfil:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Dessa namnrymder ger dig tillgång till de grundläggande klasserna som behövs för att arbeta med Excel-filer och manipulera deras innehåll med Aspose.Cells.

Låt oss nu dela upp processen i hanterbara steg. Vi går igenom att öppna en Excel-fil, ändra kalkylbladet, ändra pivottabellens datakälla och spara resultaten.
## Steg 1: Definiera din dokumentkatalog
 Först måste du ange var din Excel-fil finns. Ändra`dataDir` variabel för att peka på mappen som innehåller din "Book1.xlsx".
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
```
Den här raden ställer in katalogen där din Excel-fil är lagrad, vilket gör det lättare att komma åt senare.
## Steg 2: Ange inmatningsvägen
Låt oss sedan skapa en sträng för att ange den fullständiga sökvägen till din indata Excel-fil:
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
Detta hjälper till att effektivisera din filåtkomst; du behöver inte fortsätta skriva samma sökväg flera gånger genom hela koden.
## Steg 3: Skapa en filström
 Nu är det dags att öppna Excel-filen. Vi skapar en`FileStream` som låter dig läsa innehållet i Excel-filen:
```csharp
// Skapa en filström som innehåller Excel-filen som ska öppnas
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
Denna rad öppnar filen i läsläge, vilket ger oss tillgång till dess data.
## Steg 4: Ladda arbetsboken
Med filströmmen på plats är nästa steg att ladda arbetsboken:
```csharp
// Öppna Excel-filen genom filströmmen
Workbook workbook = new Workbook(fstream);
```
 Detta kommando tar din Excel-fil och laddar den i en`Workbook` objekt. När den har laddats kan du manipulera filen efter behov.
## Steg 5: Öppna arbetsbladet
Dags att dyka in i detaljerna. Vi kommer åt det första kalkylbladet i arbetsboken:
```csharp
// Åtkomst till det första kalkylbladet i Excel-filen
Worksheet worksheet = workbook.Worksheets[0];
```
Detta ger dig direkt tillgång till data i det första kalkylbladet, vilket gör det enkelt att ändra.
## Steg 6: Fyll i nya data
Därefter vill vi infoga ny data i cellerna. I det här exemplet lägger vi till några exempeldata:
```csharp
// Fyller på nya data till kalkylbladscellerna
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
 Här sätter vi värdena "Golf", "Qtr4" och`7000` in i specifika celler. Du kan ändra dessa värden till vad som passar dina behov.
## Steg 7: Ändra det namngivna intervallet
Nu kommer vi att ändra det namngivna området som pivottabellen refererar till. Detta innebär att skapa eller uppdatera ett intervall:
```csharp
// Ändra namngett intervall "Datakälla"
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
Genom att definiera ett nytt intervall säkerställer vi att pivottabellen använder denna nya data när den uppdateras.
## Steg 8: Spara den modifierade Excel-filen
Efter alla ändringar är det avgörande att spara ditt arbete! Låt oss spara den ändrade arbetsboken:
```csharp
// Sparar den ändrade Excel-filen
workbook.Save(dataDir + "output.xls");
```
Detta kommando sparar arbetsboken till en ny fil, så att du inte skriver över din ursprungliga fil om du inte vill!
## Steg 9: Stäng filströmmen
Slutligen är det viktigt att stänga filströmmen för att frigöra alla resurser du använder:
```csharp
// Stänger filströmmen för att frigöra alla resurser
fstream.Close();
```
Detta steg säkerställer att din applikation inte läcker minne och förblir effektiv.
## Slutsats
Grattis! Du har precis ändrat källdata för en pivottabell programmatiskt i .NET med Aspose.Cells. Denna funktion öppnar många möjligheter för att automatisera Excel-uppgifter och förbättra ditt arbetsflöde. Oavsett om du uppdaterar finansiella rapporter, spårar försäljningsdata eller till och med bara leker med datauppsättningar, kan möjligheten att göra detta programmatiskt spara massor av tid och minska risken för fel.

## FAQ's
### Vad är Aspose.Cells?
Aspose.Cells är ett kraftfullt .NET-bibliotek för att arbeta med Excel-filer, vilket tillåter användare att skapa, ändra och manipulera Excel-dokument programmatiskt.
### Kan jag ändra källdata för befintliga pivottabeller med den här metoden?
Absolut! Den här metoden låter dig uppdatera datakällan för befintliga pivottabeller i din Excel-arbetsbok.
### Måste jag ha Office installerat för att kunna använda Aspose.Cells?
Nej! Aspose.Cells är ett fristående bibliotek, vilket innebär att du inte behöver installera Microsoft Office för att arbeta med Excel-filer.
### Är Aspose.Cells gratis att använda?
Aspose.Cells erbjuder en gratis testversion, men för full funktionalitet måste du köpa en licens. Du kan hitta detaljerna[här](https://purchase.aspose.com/buy).
### Var kan jag hitta fler exempel och stöd?
 För fler exempel och support, kolla in[Aspose.Cells dokumentation](https://reference.aspose.com/cells/net/) och deras gemenskapsforum[här](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
