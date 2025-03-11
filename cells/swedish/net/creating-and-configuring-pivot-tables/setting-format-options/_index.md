---
title: Ställa in formatalternativ för pivottabell i .NET
linktitle: Ställa in formatalternativ för pivottabell i .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig att använda Aspose.Cells för .NET för att formatera pivottabeller utan ansträngning. Utforska steg-för-steg-tekniker för att förbättra din datapresentation.
weight: 20
url: /sv/net/creating-and-configuring-pivot-tables/setting-format-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ställa in formatalternativ för pivottabell i .NET

## Introduktion
Har du någonsin känt dig överväldigad av den stora mängden data som står till ditt förfogande? Eller har du haft svårt att presentera denna data på ett tydligt och insiktsfullt sätt? Välkommen ombord i så fall! Idag dyker vi in i den fantastiska världen av pivottabeller i Excel med hjälp av Aspose.Cells-biblioteket för .NET. Pivottabeller kan vara datapresentationens superhjältar, förvandla massor av siffror till strukturerade, insiktsfulla rapporter som gör beslutsfattande enkelt. Är inte det en game changer?
## Förutsättningar
Innan vi går in i handledningen, låt oss se till att du är utrustad med allt du behöver för att lyckas. Här är förutsättningarna:
1. Grundläggande kunskaper i C#: Du bör ha en grundläggande förståelse för programmeringsspråket C#. Om du är bekväm med grunderna är du redo att ta itu med detta!
2. Visual Studio eller valfri C# IDE: Du måste ha en integrerad utvecklingsmiljö (IDE) som Visual Studio. Det är här magin händer. 
3. Aspose.Cells Library: För att utnyttja kraften i Aspose.Cells måste du ladda ner det här paketet. Du hittar den lätt på[Aspose.Cells nedladdningssida](https://releases.aspose.com/cells/net/).
4. Excel-fil: Ett exempel på Excel-fil krävs för att öva på handledningen. Skapa gärna ett enkelt dataset i ett Excel-ark (som "Book1.xls") för denna övning.
5. .NET Framework: Se till att du har .NET Framework installerat på din dator.
Har du allt det där? Fantastisk! Låt oss nu gå in i vårt första steg.
## Importera paket
För att börja använda Aspose.Cells-biblioteket måste vi först importera de nödvändiga paketen. Så här gör du:
### Öppna ditt projekt
Öppna din Visual Studio (eller någon C# IDE du använder) och skapa ett nytt projekt. Välj ett konsolprogram eftersom det gör att du enkelt kan köra skriptet.
### Lägg till Aspose.Cells Reference
1. Högerklicka på ditt projekt i Solution Explorer.
2. Välj Hantera NuGet-paket.
3.  Skriv i sökrutan`Aspose.Cells` och installera den.
Nu är du redo att ta in biblioteket. Du måste lägga till följande med hjälp av direktiv i början av din kodfil:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Den här raden låter dig komma åt alla klasser och metoder som finns tillgängliga i Aspose.Cells-biblioteket.
Med marken lagd, låt oss gå igenom varje del av processen steg för steg. Vi kommer att täcka hur du ställer in olika formatalternativ för en pivottabell effektivt.
## Steg 1: Definiera din dokumentkatalog
Först måste du ställa in sökvägen till din dokumentkatalog där din indata Excel-fil finns. Denna kodrad anger var dina filer finns.
```csharp
string dataDir = "Your Document Directory";
```
 Ersätta`"Your Document Directory"` med den faktiska sökvägen där din "Book1.xls"-fil är lagrad. Detta hjälper programmet att veta var det ska leta efter indatafilen.
## Steg 2: Ladda mallfilen
 Därefter laddar vi Excel-filen vi vill manipulera. Detta görs med hjälp av`Workbook` klass.
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
I grund och botten säger detta kommando åt ditt program att öppna filen "Book1.xls" så att vi kan arbeta med dess data.
## Steg 3: Skaffa det första arbetsbladet
Nu när vi har vår arbetsbok öppen, låt oss dyka in i arbetsbladet som innehåller våra data. 
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Här kommer vi åt det första kalkylbladet i arbetsboken (eftersom indexeringen börjar från noll). Om dina data finns på ett annat blad, justera helt enkelt indexet.
## Steg 4: Åtkomst till pivottabellen
Pivottabeller är kraftfulla, men först måste vi ta tag i den vi vill arbeta med. Förutsatt att du känner till din pivottabells index, så här kommer du åt det.
```csharp
int pivotindex = 0;
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
I det här fallet kommer vi åt den första pivottabellen (index 0) i kalkylbladet. 
## Steg 5: Ställ in pivottabellens totalsummor för rader
Låt oss börja formatera! Vi kan konfigurera om vi ska visa totalsummor för rader i vår pivottabell.
```csharp
pivotTable.RowGrand = true;
```
 Ställer in den här egenskapen till`true` kommer att visa totalsummorna längst ner på varje rad i din pivottabell. Det är ett enkelt men effektivt sätt att ge sammanfattningar.
## Steg 6: Ställ in pivottabellens totalsummor för kolumner
Precis som vi anger totalsummor för rader kan vi också göra detta för kolumner.
```csharp
pivotTable.ColumnGrand = true;
```
Om du aktiverar detta visas totaler till höger om varje kolumn. Nu är din pivottabell en mästare på att sammanfatta data åt båda hållen!
## Steg 7: Visar anpassad sträng för nollvärden
En ofta förbisedd detalj är att hantera nollvärden. Du kanske vill att en specifik sträng ska visas i celler där det finns nollvärden. 
```csharp
pivotTable.DisplayNullString = true;
pivotTable.NullString = "null";
```
Detta ställer in pivottabellen för att visa "null" när den stöter på en tom cell, vilket ger klarhet och konsekvens till dina rapporter.
## Steg 8: Ställ in pivottabellens layout
Pivottabeller kan ha olika layouter, och vi kan anpassa det utifrån våra krav. Låt oss ställa in layouten till "DownThenOver".
```csharp
pivotTable.PageFieldOrder = PrintOrderType.DownThenOver;
```
Detta kommando justerar i vilken ordning fälten visas i din rapport, vilket gör det lättare att läsa. 
## Steg 9: Spara Excel-filen
Slutligen, när du har gjort alla dessa vackra justeringar, måste du spara dina ändringar tillbaka i en Excel-fil. 
```csharp
workbook.Save(dataDir + "output.xls");
```
Den här raden sparar den ändrade arbetsboken som "output.xls" i din angivna katalog. 
Och precis så har du förbättrat din pivottabell med alla dessa fantastiska formateringsalternativ!
## Slutsats
Wow, vi har gjort en hel resa tillsammans, eller hur? Genom att utnyttja funktionerna i Aspose.Cells-biblioteket för .NET kan du enkelt förändra hur din data ser ut och beter sig i Excel. Vi tog upp hur man laddar en arbetsbok, får åtkomst till och formaterar en pivottabell och kulminerade allt genom att spara våra ändringar. Data behöver inte vara trist och trist; med några justeringar kan den lysa briljant.
## FAQ's
### Vad är en pivottabell?
Pivottabeller är en Excel-funktion som sammanfattar och analyserar data dynamiskt.
### Behöver jag installera Excel för att använda Aspose.Cells?
Nej, Aspose.Cells är ett fristående bibliotek som inte kräver att Excel är installerat.
### Kan jag skapa pivottabeller med Aspose.Cells?
Ja, Aspose.Cells låter dig skapa, modifiera och manipulera pivottabeller.
### Är Aspose.Cells gratis?
Aspose.Cells är ett betalbibliotek, men en gratis provperiod är tillgänglig.
### Var kan jag hitta mer Aspose.Cells-dokumentation?
 Kolla in[Aspose.Cells dokumentation](https://reference.aspose.com/cells/net/) för djupgående guider och exempel.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
