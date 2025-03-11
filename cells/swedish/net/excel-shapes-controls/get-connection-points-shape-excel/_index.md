---
title: Skaffa anslutningspunkter i Excel
linktitle: Skaffa anslutningspunkter i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du får formanslutningspunkter i Excel med Aspose.Cells för .NET. Följ vår steg-för-steg-guide för att enkelt extrahera och visa formpunkter programmatiskt.
weight: 11
url: /sv/net/excel-shapes-controls/get-connection-points-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skaffa anslutningspunkter i Excel

## Introduktion
När vi arbetar med Excel-filer programmatiskt behöver vi ofta interagera med former inbäddade i arken. En av de mer avancerade uppgifterna du kan utföra är att extrahera anslutningspunkter från en form. Kopplingspunkter används för att fästa former med kopplingar och hantera deras layout mer exakt. Om du vill få anslutningspunkterna för en form i Excel, är Aspose.Cells för .NET verktyget du behöver. I den här handledningen tar vi dig genom en steg-för-steg-process för att uppnå detta.
## Förutsättningar
Innan du dyker in i koden, se till att du har följande förutsättningar:
- Aspose.Cells för .NET: Du måste ha Aspose.Cells installerat i din utvecklingsmiljö. Om du inte har det än så kan du[ladda ner den senaste versionen här](https://releases.aspose.com/cells/net/).
- Utvecklingsmiljö: Se till att du har en fungerande installation av Visual Studio eller någon annan .NET-kompatibel IDE.
- Grundläggande kunskaper om C#: Denna handledning förutsätter att du har en grundläggande förståelse för C#-programmering och objektorienterade principer.
 Du kan också anmäla dig till en[gratis provversion av Aspose.Cells](https://releases.aspose.com/) om du inte redan har gjort det. Detta ger dig tillgång till alla funktioner som krävs för den här guiden.

## Importera paket
För att arbeta med Aspose.Cells i ditt projekt måste du inkludera de nödvändiga namnrymden. Följande importsatser ska placeras överst i koden:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Dessa namnrymder ger dig tillgång till kärnfunktionaliteten i Aspose.Cells och låter dig manipulera kalkylblad och former.

## Steg-för-steg-guide för att få anslutningspunkter för en form
det här avsnittet kommer vi att gå igenom hur du extraherar anslutningspunkterna för en form i ett Excel-kalkylblad. Följ varje steg noggrant för en tydlig förståelse.
## Steg 1: Instantiera en ny arbetsbok
 Först och främst måste vi skapa en instans av`Workbook` klass. Detta representerar en Excel-fil i Aspose.Cells. Om du inte har en befintlig fil, inga problem – du kan börja med en tom arbetsbok.
```csharp
// Instantiera en ny arbetsbok
Workbook workbook = new Workbook();
```
 I det här steget har vi skapat en tom Excel-arbetsbok, men du kan också ladda en befintlig genom att skicka filsökvägen till`Workbook` konstruktör.
## Steg 2: Öppna det första arbetsbladet
Därefter måste vi komma åt kalkylbladet där vi vill arbeta med former. I det här fallet kommer vi att använda det första kalkylbladet i arbetsboken.
```csharp
// Få det första arbetsbladet i arbetsboken
Worksheet worksheet = workbook.Worksheets[0];
```
 Den här raden kommer åt det första kalkylbladet från samlingen av kalkylblad i arbetsboken. Om du arbetar med ett specifikt blad kan du byta ut indexet`0` med önskat index.
## Steg 3: Lägg till en ny textruta (form)
Låt oss nu lägga till en ny form i kalkylbladet. Vi skapar en textruta, som är en typ av form. Du kan också lägga till andra typer av former, men för enkelhetens skull håller vi oss till en textruta i den här handledningen.
```csharp
// Lägg till en ny textruta i samlingen
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
Här är vad vi har gjort:
-  Lade till en textruta på raden`2` , kolumn`1`.
-  Ställ in textrutans mått till`160` enheter i bredd och`200` enheter på höjden.
## Steg 4: Få tillgång till Shape från Shapes Collection
 När vi har lagt till textrutan blir den en del av kalkylbladets formsamling. Nu kommer vi åt den formen med hjälp av`Shapes`samling.
```csharp
// Få åtkomst till formen (textrutan) från formsamlingen
Shape shape = workbook.Worksheets[0].Shapes[0];
```
I det här steget hämtar vi den första formen (vår textruta) från samlingen. Om du har flera former kan du ange indexet eller till och med hitta formen efter namn.
## Steg 5: Hämta anslutningspunkter
Nu när vi har vår form, låt oss extrahera dess kopplingspunkter. Dessa punkter används för att fästa kopplingar till formen. De`ConnectionPoints` egenskapen för formen returnerar alla tillgängliga anslutningspunkter.
```csharp
// Få alla anslutningspunkter i denna form
var connectionPoints = shape.ConnectionPoints;
```
Detta ger oss en samling av alla anslutningspunkter som finns tillgängliga för den formen.
## Steg 6: Visa anslutningspunkter
Slutligen vill vi visa koordinaterna för varje anslutningspunkt. Det är här vi går igenom anslutningspunkterna och skriver ut dem till konsolen.
```csharp
// Visa alla formpunkter
foreach (var pt in connectionPoints)
{
    System.Console.WriteLine(string.Format("X = {0}, Y = {1}", pt.X, pt.Y));
}
```
 Denna loop itererar över varje anslutningspunkt och skriver ut`X` och`Y` koordinater. Detta kan vara användbart för att felsöka eller visuellt bekräfta anslutningspunkterna för en form.
## Steg 7: Kör och slutför
När du har ställt in alla steg ovan kan du köra koden. Här är den sista raden som säkerställer att processen slutförs framgångsrikt:
```csharp
System.Console.WriteLine("GetShapeConnectionPoints executed successfully.");
```
Den här raden loggar helt enkelt ett meddelande till konsolen som indikerar att processen har slutförts.

## Slutsats
I den här handledningen tog vi upp hur man hämtar anslutningspunkter för en form i Excel med Aspose.Cells för .NET. Genom att dela upp uppgiften i små, lättsmälta steg, utforskade vi processen att skapa en arbetsbok, lägga till en form och extrahera anslutningspunkterna.
Genom att förstå hur man manipulerar former programmatiskt låser du upp en värld av möjligheter för att bygga dynamiska och interaktiva Excel-ark. Oavsett om du bygger rapporter, designar instrumentpaneler eller skapar diagram, kommer denna kunskap att vara användbar.
## FAQ's
### Vad är en anslutningspunkt i en form?
En anslutningspunkt är en specifik punkt på en form där du kan fästa kontakter eller länka den till andra former.
### Kan jag hämta anslutningspunkter för alla former i ett kalkylblad?
Ja, Aspose.Cells låter dig hämta anslutningspunkter för vilken form som helst som stöder dem. Gå helt enkelt igenom formsamlingen i kalkylbladet.
### Behöver jag en licens för att använda Aspose.Cells?
Ja, medan du kan prova det gratis, krävs en licens för alla funktioner. Du kan[köp en licens här](https://purchase.aspose.com/buy)eller skaffa en[tillfällig licens](https://purchase.aspose.com/temporary-license/).
### Hur kan jag lägga till olika typer av former i Aspose.Cells?
Du kan använda`Add` metod för former som rektanglar, ellipser och mer. Varje form har specifika parametrar som du kan anpassa.
### Hur laddar jag en befintlig Excel-fil istället för att skapa en ny?
 För att ladda en befintlig fil, skicka filsökvägen till`Workbook` konstruktör, så här:  
```csharp
Workbook workbook = new Workbook("path_to_file.xlsx");
```
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
