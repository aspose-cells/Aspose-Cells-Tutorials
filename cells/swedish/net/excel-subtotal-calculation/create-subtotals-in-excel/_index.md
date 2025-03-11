---
title: Skapa delsummor i Excel
linktitle: Skapa delsummor i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du skapar delsummor i Excel med Aspose.Cells för .NET med denna enkla steg-för-steg handledning.
weight: 10
url: /sv/net/excel-subtotal-calculation/create-subtotals-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa delsummor i Excel

## Introduktion
Är du redo att höja dina Excel-kunskaper och göra dina kalkylblad mer dynamiska? Att skapa delsummor i Excel kan hjälpa dig att kategorisera och sammanfatta data effektivt, vilket möjliggör bättre datatolkning och rapportering. Om du är någon som ofta brottas med massor av siffror är det viktigt att skapa strukturerade sammanfattningar. Idag ska vi dyka in i hur du skapar delsummor utan ansträngning med Aspose.Cells för .NET, ett kraftfullt bibliotek som är designat för att hantera alla dina Excel-filmanipulationer.
## Förutsättningar
Innan vi dyker in i det snåriga med att skapa delsummor i Excel, finns det några förutsättningar du bör ha på plats:
1.  Aspose.Cells för .NET installerat: Se till att du har Aspose.Cells-biblioteket inställt i din utvecklingsmiljö. Om du inte har gjort detta än kan du enkelt[ladda ner den här](https://releases.aspose.com/cells/net/).
2. .NET-miljö: Du bör ha en fungerande .NET-miljö där vi kan arbeta med biblioteket. Oavsett om det är Visual Studio eller någon annan IDE, se till att du är bekväm med att koda i C#.
3. Grundläggande kunskaper i C#: Bekantskap med C# kommer att vara fördelaktigt. Exemplen vi kommer att tillhandahålla är i C#-syntax, så att vara bekväm med det hjälper dig att förstå processen.
4.  Excel-arbetsblad: Ett exempel på Excel-fil att öva på. Vi kommer att använda en fil som heter`book1.xls` i vår handledning.
5.  Tillgång till onlinedokumentation och support: Bekanta dig med[Aspose.Cells dokumentation](https://reference.aspose.com/cells/net/) kan vara otroligt hjälpsam när du går vidare med att använda biblioteket.
Nu när vi har lagt grunden, låt oss hoppa in i den tekniska delen!
## Importera paket
Innan vi börjar med den faktiska koden måste vi se till att vi har alla nödvändiga paket. Nedan är hur du kan importera den nödvändiga namnrymden i ditt projekt:
```csharp
using System.IO;
using Aspose.Cells;
```
Detta importerar allt vi behöver från Aspose-biblioteket för att manipulera Excel-filer. Låt oss nu dela upp koden steg-för-steg för att skapa delsummor i ett Excel-kalkylblad.
## Steg 1: Ställ in filsökvägen
Till att börja med måste vi definiera var vår Excel-fil finns. Det är här vi berättar för programmet om vår dokumentkatalog.
```csharp
string dataDir = "Your Document Directory";
```
 Ersätta`"Your Document Directory"` med den faktiska vägen där din`book1.xls` lagras. Detta talar om för programmet var Excel-filen vi kommer att manipulera kan hitta.
## Steg 2: Instantiera en ny arbetsbok
Nästa upp kommer vi att skapa en ny instans av Workbook-objektet. Detta gör att vi kan öppna och redigera vår Excel-fil.
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 Här skapar vi ett objekt av`Workbook` och ladda den med vår specificerade`book1.xls` fil. Detta arbetsboksobjekt innehåller nu all information från Excel-filen och låter oss ändra den.
## Steg 3: Gå till Cells Collection
För att arbeta med innehållet i Excel-arbetsbladet måste vi komma åt samlingen "Celler".
```csharp
Cells cells = workbook.Worksheets[0].Cells;
```
 Detta hämtar cellerna från det första kalkylbladet (index 0) i vår arbetsbok. De`cells` objekt låter oss interagera med de enskilda cellerna i kalkylarket.
## Steg 4: Definiera cellområdet för delsummor
Nu är det dags att specificera intervallet av celler där vi vill tillämpa delsumman. 
```csharp
CellArea ca = new CellArea();
ca.StartRow = 2; // B3
ca.StartColumn = 1; 
ca.EndRow = 18; // C19
ca.EndColumn = 2;
```
 Här definierar vi a`CellArea` som anger intervallet vi är intresserade av. I det här fallet har vi valt området från B3 (rad 2, kolumn 1) till C19 (rad 18, kolumn 2). Det är här vi kommer att beräkna våra delsummor.
## Steg 5: Tillämpa delsummor
Detta är hjärtat i vår verksamhet – att tillämpa delsumman på det definierade cellområdet.
```csharp
cells.Subtotal(ca, 0, ConsolidationFunction.Sum, new int[] { 1 });
```
 På den här raden kallar vi`Subtotal` metod. De definierade parametrarna är:
- `ca`: Cellintervallet vi definierade tidigare.
- `0`: Detta index hänvisar till kolumnen som innehåller värdena som ska subtotalas. 
- `ConsolidationFunction.Sum`Detta anger att vi vill summera värdena.
- `new int[] { 1 }`: Detta indikerar att vi summerar värdena från den andra kolumnen (kolumn C).
## Steg 6: Spara den modifierade Excel-filen
Äntligen måste vi spara våra ändringar i en ny Excel-fil. 
```csharp
workbook.Save(dataDir + "output.out.xls");
```
 De`Save` metod skriver ändringarna till en ny fil med namnet`output.out.xls`. Du kan ange vilket namn som helst för utdatafilen enligt dina krav.
## Slutsats
Med dessa enkla steg har du framgångsrikt skapat delsummor i ditt Excel-kalkylblad med Aspose.Cells för .NET! Från att instansiera en arbetsbok till att tillämpa delsummor och spara resultaten täckte vi alla grunder. Det här biblioteket förenklar inte bara dina Excel-manipulationer utan ger dig också möjlighet att hantera data mer effektivt.
Nu, varsågod och ge det ett försök! Du kommer att bli förvånad över hur mycket enklare det blir att hantera data i kalkylblad när du vet hur du använder rätt verktyg. 
## FAQ's
### Vad är Aspose.Cells för .NET?
Aspose.Cells för .NET är ett kraftfullt bibliotek som låter utvecklare manipulera Excel-filer i .NET-applikationer programmatiskt.
### Behöver jag installera något speciellt för att använda Aspose.Cells?
 Ja, du måste ladda ner och lägga till Aspose.Cells-biblioteket till ditt .NET-projekt.[Ladda ner här](https://releases.aspose.com/cells/net/).
### Är det möjligt att skapa andra typer av Excel-funktioner med Aspose.Cells?
Absolut! Aspose.Cells låter dig utföra olika Excel-operationer som att skapa diagram, hantera kalkylblad och ändra cellformat bland många andra.
### Kan jag använda Aspose.Cells gratis?
 Du kan[prova en gratis provperiod](https://releases.aspose.com/) av Aspose.Cells för att utforska dess funktioner innan du bestämmer dig för att köpa.
### Vilka supportalternativ finns tillgängliga?
 För eventuella problem kan du besöka[Aspose supportforum](https://forum.aspose.com/c/cells/9) för att få hjälp och dela insikter med en community av användare och utvecklare.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
