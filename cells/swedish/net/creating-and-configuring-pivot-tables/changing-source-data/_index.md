---
"description": "Lär dig hur du ändrar källdata för pivottabeller programmatiskt med Aspose.Cells för .NET med vår omfattande steg-för-steg-handledning."
"linktitle": "Ändra källdata för pivottabell programmatiskt i .NET"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Ändra källdata för pivottabell programmatiskt i .NET"
"url": "/sv/net/creating-and-configuring-pivot-tables/changing-source-data/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ändra källdata för pivottabell programmatiskt i .NET

## Introduktion
I dataanalysvärlden är det få verktyg som lyser så starkt som Microsoft Excel. Varje dag förlitar sig otaliga användare på Excel för att hantera och analysera data, men bakom kulisserna är det mycket mer komplext än att bara klicka och dra. Om du någonsin velat manipulera Excel-filer programmatiskt – närmare bestämt ändra källdata i en pivottabell – har du kommit rätt! I den här guiden utforskar vi hur du kan uppnå detta med Aspose.Cells för .NET. Oavsett om du är en erfaren utvecklare eller bara håller på att ge dig ut i programmeringens hav, hittar du den här handledningen full av värdefull information som är lätt att följa.
## Förkunskapskrav
Innan vi börjar vår resa med att ändra källdata för en pivottabell, låt oss se till att du har allt konfigurerat och redo att börja:
1. Visual Studio: Se till att du har en kopia av Microsoft Visual Studio installerad, eftersom vi kommer att skriva vår kod här.
2. Aspose.Cells-biblioteket: Du behöver ha Aspose.Cells-biblioteket nedladdat och refererat till det i ditt projekt. Du kan ladda ner det [här](https://releases.aspose.com/cells/net/).
3. Grundläggande kunskaper i C#: Även om den här handledningen är förenklad, kommer det att hjälpa dig att bättre förstå koden om du har goda kunskaper i C#.
4. Excel-fil: Du bör ha en exempelfil i Excel (som "Book1.xlsx") som innehåller en pivottabell som vi kan manipulera.
Okej, med dessa förutsättningar i schack kan vi fortsätta med att importera de nödvändiga paketen och börja koda!
## Importera paket
Först och främst – låt oss importera de paket vi behöver. Öppna ditt C#-projekt i Visual Studio och lägg till följande med hjälp av direktiv högst upp i din kodfil:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Dessa namnrymder ger dig tillgång till de viktiga klasser som behövs för att arbeta med Excel-filer och manipulera deras innehåll med hjälp av Aspose.Cells.

Nu ska vi dela upp processen i hanterbara steg. Vi går igenom hur man öppnar en Excel-fil, ändrar kalkylbladet, ändrar pivottabellens datakälla och sparar resultaten.
## Steg 1: Definiera din dokumentkatalog
Först måste du ange var din Excel-fil finns. Ändra `dataDir` variabeln ska peka på mappen som innehåller din "Book1.xlsx".
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
```
Den här raden anger katalogen där din Excel-fil lagras, vilket gör den enklare att komma åt senare.
## Steg 2: Ange inmatningsvägen
Nu skapar vi en sträng för att ange den fullständiga sökvägen till din Excel-indatafil:
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
Detta hjälper till att effektivisera din filåtkomst; du behöver inte skriva samma sökväg flera gånger i din kod.
## Steg 3: Skapa en filström
Nu är det dags att öppna Excel-filen. Vi skapar en `FileStream` som låter dig läsa innehållet i Excel-filen:
```csharp
// Skapa en filström som innehåller Excel-filen som ska öppnas
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
Den här raden öppnar filen i läsläge, vilket gör att vi kan komma åt dess data.
## Steg 4: Läs in arbetsboken
Med filströmmen på plats är nästa steg att ladda arbetsboken:
```csharp
// Öppna Excel-filen via filströmmen
Workbook workbook = new Workbook(fstream);
```
Det här kommandot tar din Excel-fil och laddar den till en `Workbook` objekt. När filen har laddats kan du manipulera den efter behov.
## Steg 5: Öppna arbetsbladet
Dags att dyka in i detaljerna. Vi ska gå igenom det första arbetsbladet i arbetsboken:
```csharp
// Åtkomst till det första kalkylbladet i Excel-filen
Worksheet worksheet = workbook.Worksheets[0];
```
Detta ger dig direkt åtkomst till informationen i det första kalkylbladet, vilket gör det enkelt att ändra.
## Steg 6: Fyll i nya data
Nästa steg är att infoga nya data i cellerna. I det här exemplet lägger vi till några exempeldata:
```csharp
// Fyllning av nya data i kalkylbladets celler
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
Här lägger vi in värdena "Golf", "Qtr4" och `7000` i specifika celler. Du kan ändra dessa värden till vad som passar dina behov.
## Steg 7: Ändra det namngivna området
Nu ska vi ändra det namngivna området som pivottabellen refererar till. Detta innebär att skapa eller uppdatera ett område:
```csharp
// Ändra namngivet område "DataSource"
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
Genom att definiera ett nytt område säkerställer vi att pivottabellen använder dessa nya data när den uppdateras.
## Steg 8: Spara den modifierade Excel-filen
Efter alla ändringar är det avgörande att spara ditt arbete! Nu sparar vi den modifierade arbetsboken:
```csharp
// Spara den modifierade Excel-filen
workbook.Save(dataDir + "output.xls");
```
Det här kommandot sparar arbetsboken till en ny fil, så att du inte skriver över originalfilen om du inte vill!
## Steg 9: Stäng filströmmen
Slutligen är det viktigt att stänga filströmmen för att frigöra alla resurser du använder:
```csharp
// Stänger filströmmen för att frigöra alla resurser
fstream.Close();
```
Det här steget säkerställer att din applikation inte läcker minne och förblir effektiv.
## Slutsats
Grattis! Du har just lyckats ändra källdata för en pivottabell programmatiskt i .NET med hjälp av Aspose.Cells. Den här funktionen öppnar upp många möjligheter för att automatisera Excel-uppgifter och förbättra ditt arbetsflöde. Oavsett om du uppdaterar finansiella rapporter, spårar försäljningsdata eller bara experimenterar med datamängder, kan möjligheten att göra detta programmatiskt spara dig massor av tid och minska risken för fel.

## Vanliga frågor
### Vad är Aspose.Cells?
Aspose.Cells är ett kraftfullt .NET-bibliotek för att arbeta med Excel-filer, vilket gör det möjligt för användare att skapa, modifiera och manipulera Excel-dokument programmatiskt.
### Kan jag ändra källdata för befintliga pivottabeller med den här metoden?
Absolut! Den här metoden låter dig uppdatera datakällan för befintliga pivottabeller i din Excel-arbetsbok.
### Behöver jag ha Office installerat för att använda Aspose.Cells?
Nej! Aspose.Cells är ett fristående bibliotek, vilket innebär att du inte behöver Microsoft Office installerat för att arbeta med Excel-filer.
### Är Aspose.Cells gratis att använda?
Aspose.Cells erbjuder en gratis testversion, men för full funktionalitet måste du köpa en licens. Du hittar detaljerna [här](https://purchase.aspose.com/buy).
### Var kan jag hitta fler exempel och stöd?
För fler exempel och stöd, se [Aspose.Cells-dokumentation](https://reference.aspose.com/cells/net/) och deras communityforum [här](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}