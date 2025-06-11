---
"description": "Lär dig hur du hämtar formkopplingspunkter i Excel med Aspose.Cells för .NET. Följ vår steg-för-steg-guide för att enkelt extrahera och visa formpunkter programmatiskt."
"linktitle": "Hämta kopplingspunkter för former i Excel"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Hämta kopplingspunkter för former i Excel"
"url": "/sv/net/excel-shapes-controls/get-connection-points-shape-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Hämta kopplingspunkter för former i Excel

## Introduktion
När vi arbetar med Excel-filer programmatiskt behöver vi ofta interagera med former som är inbäddade i arken. En av de mer avancerade uppgifterna du kan utföra är att extrahera kopplingspunkter från en form. Kopplingspunkter används för att koppla former med kopplingar och hantera deras layout mer exakt. Om du vill hämta kopplingspunkterna för en form i Excel är Aspose.Cells för .NET verktyget du behöver. I den här handledningen tar vi dig igenom en steg-för-steg-process för att uppnå detta.
## Förkunskapskrav
Innan du går in i koden, se till att du har följande förutsättningar:
- Aspose.Cells för .NET: Du måste ha Aspose.Cells installerat i din utvecklingsmiljö. Om du inte redan har det kan du göra det [ladda ner den senaste versionen här](https://releases.aspose.com/cells/net/).
- Utvecklingsmiljö: Se till att du har en fungerande installation av Visual Studio eller någon annan .NET-kompatibel IDE.
- Grundläggande kunskaper i C#: Den här handledningen förutsätter att du har en grundläggande förståelse för C#-programmering och objektorienterade principer.
Du kan också anmäla dig till en [gratis provperiod av Aspose.Cells](https://releases.aspose.com/) om du inte redan har gjort det. Detta ger dig tillgång till alla funktioner som krävs för den här guiden.

## Importera paket
För att arbeta med Aspose.Cells i ditt projekt måste du inkludera nödvändiga namnrymder. Följande import-satser bör placeras högst upp i din kod:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Dessa namnrymder ger dig tillgång till kärnfunktionerna i Aspose.Cells och låter dig manipulera kalkylblad och former.

## Steg-för-steg-guide för att hämta kopplingspunkter för en form
I det här avsnittet går vi igenom hur du extraherar kopplingspunkterna för en form i ett Excel-ark. Följ varje steg noggrant för en tydlig förståelse.
## Steg 1: Instansiera en ny arbetsbok
Först och främst måste vi skapa en instans av `Workbook` klass. Detta representerar en Excel-fil i Aspose.Cells. Om du inte har en befintlig fil är det inga problem – du kan börja med en tom arbetsbok.
```csharp
// Skapa en ny arbetsbok
Workbook workbook = new Workbook();
```
I det här steget har vi skapat en tom Excel-arbetsbok, men du kan också läsa in en befintlig genom att skicka sökvägen till `Workbook` konstruktör.
## Steg 2: Öppna det första arbetsbladet
Nästa steg är att komma åt det arbetsblad där vi vill arbeta med former. I det här fallet använder vi det första arbetsbladet i arbetsboken.
```csharp
// Hämta det första arbetsbladet i arbetsboken
Worksheet worksheet = workbook.Worksheets[0];
```
Den här raden öppnar det första kalkylbladet från samlingen av kalkylblad i arbetsboken. Om du arbetar med ett specifikt ark kan du ersätta indexet `0` med önskat index.
## Steg 3: Lägg till en ny textruta (form)
Nu ska vi lägga till en ny form i kalkylbladet. Vi skapar en textruta, som är en typ av form. Du kan också lägga till andra typer av former, men för enkelhetens skull håller vi oss till en textruta i den här handledningen.
```csharp
// Lägg till en ny textruta i samlingen
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
Här är vad vi har gjort:
- Lade till en textruta på raden `2`, kolumn `1`.
- Ställ in textrutans dimensioner till `160` enheter i bredd och `200` enheter i höjd.
## Steg 4: Komma åt formen från formsamlingen
När vi har lagt till textrutan blir den en del av kalkylbladets formsamling. Nu kommer vi åt formen med hjälp av `Shapes` samling.
```csharp
// Åtkomst till formen (textrutan) från formsamlingen
Shape shape = workbook.Worksheets[0].Shapes[0];
```
I det här steget hämtar vi den första formen (vår textruta) från samlingen. Om du har flera former kan du ange indexet eller till och med hitta formen efter namn.
## Steg 5: Hämta kopplingspunkter
Nu när vi har vår form, låt oss extrahera dess kopplingspunkter. Dessa punkter används för att fästa kopplingar till formen. `ConnectionPoints` Egenskapen för formen returnerar alla tillgängliga kopplingspunkter.
```csharp
// Få alla kopplingspunkter i den här formen
var connectionPoints = shape.ConnectionPoints;
```
Detta ger oss en samling av alla tillgängliga kopplingspunkter för den formen.
## Steg 6: Visa kopplingspunkter
Slutligen vill vi visa koordinaterna för varje kopplingspunkt. Det är här vi loopar igenom kopplingspunkterna och skriver ut dem till konsolen.
```csharp
// Visa alla formpunkter
foreach (var pt in connectionPoints)
{
    System.Console.WriteLine(string.Format("X = {0}, Y = {1}", pt.X, pt.Y));
}
```
Denna loop itererar över varje anslutningspunkt och skriver ut `X` och `Y` koordinater. Detta kan vara användbart för felsökning eller visuell bekräftelse av en forms kopplingspunkter.
## Steg 7: Utför och slutför
När du har konfigurerat alla steg ovan kan du köra koden. Här är den sista raden som säkerställer att processen slutförs korrekt:
```csharp
System.Console.WriteLine("GetShapeConnectionPoints executed successfully.");
```
Den här raden loggar helt enkelt ett meddelande till konsolen som indikerar att processen har slutförts.

## Slutsats
den här handledningen gick vi igenom hur man hämtar kopplingspunkter för en form i Excel med hjälp av Aspose.Cells för .NET. Genom att dela upp uppgiften i små, lättsmälta steg utforskade vi processen att skapa en arbetsbok, lägga till en form och extrahera kopplingspunkterna.
Genom att förstå hur man manipulerar former programmatiskt låser du upp en värld av möjligheter för att bygga dynamiska och interaktiva Excel-ark. Oavsett om du bygger rapporter, designar dashboards eller skapar diagram kommer denna kunskap att vara praktisk.
## Vanliga frågor
### Vad är en kopplingspunkt i en form?
En kopplingspunkt är en specifik punkt på en form där du kan koppla kopplingar eller länka den till andra former.
### Kan jag hämta kopplingspunkter för alla former i ett kalkylblad?
Ja, Aspose.Cells låter dig hämta kopplingspunkter för alla former som stöder dem. Gå bara igenom formsamlingen i kalkylbladet.
### Behöver jag en licens för att använda Aspose.Cells?
Ja, även om du kan prova det gratis krävs en licens för alla funktioner. Du kan [köp en licens här](https://purchase.aspose.com/buy) eller få en [tillfällig licens](https://purchase.aspose.com/temporary-license/).
### Hur kan jag lägga till olika typer av former i Aspose.Cells?
Du kan använda `Add` metod för former som rektanglar, ellipser med mera. Varje form har specifika parametrar som du kan anpassa.
### Hur laddar jag en befintlig Excel-fil istället för att skapa en ny?
För att ladda en befintlig fil, ange filsökvägen till `Workbook` konstruktor, så här:  
```csharp
Workbook workbook = new Workbook("path_to_file.xlsx");
```

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}