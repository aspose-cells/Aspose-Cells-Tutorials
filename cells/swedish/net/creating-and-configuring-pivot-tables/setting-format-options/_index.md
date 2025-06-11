---
"description": "Lär dig använda Aspose.Cells för .NET för att formatera pivottabeller utan ansträngning. Utforska steg-för-steg-tekniker för att förbättra din datapresentation."
"linktitle": "Ställa in formatalternativ för pivottabell i .NET"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Ställa in formatalternativ för pivottabell i .NET"
"url": "/sv/net/creating-and-configuring-pivot-tables/setting-format-options/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ställa in formatalternativ för pivottabell i .NET

## Introduktion
Har du någonsin känt dig överväldigad av den stora datamängden som finns till ditt förfogande? Eller har du haft svårt att presentera denna data på ett tydligt och insiktsfullt sätt? Om så är fallet, välkommen ombord! Idag dyker vi ner i den fantastiska världen av pivottabeller i Excel med hjälp av Aspose.Cells-biblioteket för .NET. Pivottabeller kan vara superhjältar inom datapresentation och omvandla massor av siffror till strukturerade, insiktsfulla rapporter som gör beslutsfattandet till en barnlek. Är inte det revolutionerande?
## Förkunskapskrav
Innan vi går in i handledningen, låt oss se till att du är utrustad med allt du behöver för att lyckas. Här är förkunskapskraven:
1. Grundläggande kunskaper i C#: Du bör ha en grundläggande förståelse för programmeringsspråket C#. Om du är bekväm med grunderna är du redo att ta dig an detta!
2. Visual Studio eller valfri C# IDE: Du behöver en integrerad utvecklingsmiljö (IDE) som Visual Studio. Det är här magin händer. 
3. Aspose.Cells-biblioteket: För att utnyttja kraften i Aspose.Cells behöver du ladda ner det här paketet. Du hittar det enkelt på [Aspose.Cells nedladdningssida](https://releases.aspose.com/cells/net/).
4. Excel-fil: En exempelfil i Excel krävs för att öva på handledningen. Skapa gärna en enkel datauppsättning i ett Excel-ark (som "Book1.xls") för den här övningen.
5. .NET Framework: Se till att du har .NET Framework installerat på din dator.
Fattar du allt? Fantastiskt! Nu ska vi ta steget in.
## Importera paket
För att börja använda Aspose.Cells-biblioteket måste vi först importera de nödvändiga paketen. Så här gör du:
### Öppna ditt projekt
Öppna Visual Studio (eller vilken C# IDE du än använder) och skapa ett nytt projekt. Välj ett konsolprogram eftersom det gör att du enkelt kan köra skriptet.
### Lägg till Aspose.Cells-referens
1. Högerklicka på ditt projekt i lösningsutforskaren.
2. Välj Hantera NuGet-paket.
3. I sökrutan skriver du `Aspose.Cells` och installera den.
Nu är du redo att hämta biblioteket. Du måste lägga till följande `using`-direktiv i början av din kodfil:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Den här raden ger dig åtkomst till alla klasser och metoder som finns tillgängliga i Aspose.Cells-biblioteket.
När grunden är lagd, låt oss gå igenom varje del av processen steg för steg. Vi kommer att gå igenom hur man effektivt ställer in olika formatalternativ för en pivottabell.
## Steg 1: Definiera din dokumentkatalog
Först måste du ange sökvägen till dokumentkatalogen där din Excel-fil finns. Denna kodrad anger var dina filer finns.
```csharp
string dataDir = "Your Document Directory";
```
Ersätta `"Your Document Directory"` med den faktiska sökvägen där din "Book1.xls"-fil finns lagrad. Detta hjälper programmet att veta var det ska leta efter indatafilen.
## Steg 2: Ladda mallfilen
Nästa steg är att ladda in Excel-filen vi vill manipulera. Detta görs med hjälp av `Workbook` klass.
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
I huvudsak säger det här kommandot åt ditt program att öppna filen "Book1.xls" så att vi kan arbeta med dess data.
## Steg 3: Hämta det första arbetsbladet
Nu när vi har vår arbetsbok öppen, låt oss dyka ner i kalkylbladet som innehåller våra data. 
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Här öppnar vi det första kalkylbladet i arbetsboken (eftersom indexeringen börjar från noll). Om dina data finns på ett annat kalkylblad justerar du helt enkelt indexet.
## Steg 4: Åtkomst till pivottabellen
Pivottabeller är kraftfulla, men först måste vi välja den vi vill arbeta med. Om du antar att du känner till din pivottabells index, så här får du tillgång till den.
```csharp
int pivotindex = 0;
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
I det här fallet använder vi den första pivottabellen (index 0) i kalkylbladet. 
## Steg 5: Ställ in totalsummorna för rader i pivottabellen
Nu börjar vi formatera! Vi kan konfigurera om totalsummor för rader i vår pivottabell ska visas.
```csharp
pivotTable.RowGrand = true;
```
Att ställa in den här egenskapen till `true` kommer att visa totalsummorna längst ner på varje rad i din pivottabell. Det är ett enkelt men effektivt sätt att ge sammanfattningar.
## Steg 6: Ställ in totalsummorna för pivottabellen för kolumner
Precis som vi anger totalsummor för rader kan vi även göra detta för kolumner.
```csharp
pivotTable.ColumnGrand = true;
```
Om du aktiverar detta visas totalsummor till höger om varje kolumn. Nu är din pivottabell en mästare på att sammanfatta data åt båda hållen!
## Steg 7: Visa anpassad sträng för nullvärden
En ofta förbisedd detalj är hanteringen av nullvärden. Du kanske vill att en specifik sträng ska visas i celler där det finns nullvärden. 
```csharp
pivotTable.DisplayNullString = true;
pivotTable.NullString = "null";
```
Detta ställer in pivottabellen så att den visar "null" när den stöter på en tom cell, vilket ger tydligare och mer konsekvens i dina rapporter.
## Steg 8: Ställ in pivottabellens layout
Pivottabeller kan ha olika layouter, och vi kan anpassa dem baserat på våra behov. Låt oss ställa in layouten till "DownThenOver".
```csharp
pivotTable.PageFieldOrder = PrintOrderType.DownThenOver;
```
Det här kommandot justerar ordningen i vilken fälten visas i rapporten, vilket gör den lättare att läsa. 
## Steg 9: Spara Excel-filen
Slutligen, när du har gjort alla dessa vackra justeringar, måste du spara dina ändringar tillbaka till en Excel-fil. 
```csharp
workbook.Save(dataDir + "output.xls");
```
Den här raden sparar den ändrade arbetsboken som "output.xls" i den angivna katalogen. 
Och precis så har du förbättrat din pivottabell med alla dessa fantastiska formateringsalternativ!
## Slutsats
Wow, vi har gjort en rejäl resa tillsammans, eller hur? Genom att utnyttja funktionerna i Aspose.Cells-biblioteket för .NET kan du enkelt förändra hur dina data ser ut och beter sig i Excel. Vi gick igenom hur man laddar en arbetsbok, öppnar och formaterar en pivottabell och avslutade allt genom att spara våra ändringar. Data behöver inte vara trist och trist; med några få justeringar kan de glänsa fantastiskt.
## Vanliga frågor
### Vad är en pivottabell?
Pivottabeller är en funktion i Excel som sammanfattar och analyserar data dynamiskt.
### Behöver jag Excel installerat för att använda Aspose.Cells?
Nej, Aspose.Cells är ett fristående bibliotek som inte kräver att Excel är installerat.
### Kan jag skapa pivottabeller med Aspose.Cells?
Ja, Aspose.Cells låter dig skapa, modifiera och manipulera pivottabeller.
### Är Aspose.Cells gratis?
Aspose.Cells är ett betalt bibliotek, men en gratis provversion finns tillgänglig.
### Var kan jag hitta mer dokumentation om Aspose.Cells?
Kolla in [Aspose.Cells-dokumentation](https://reference.aspose.com/cells/net/) för djupgående guider och exempel.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}