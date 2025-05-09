---
"description": "Lär dig hur du programmatiskt sorterar pivottabeller i .NET med hjälp av Aspose.Cells. En steg-för-steg-guide som täcker installation, konfiguration, sortering och sparning av resultat som Excel- och PDF-filer."
"linktitle": "Anpassad sortering av pivottabell programmatiskt i .NET"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Anpassad sortering av pivottabell programmatiskt i .NET"
"url": "/sv/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/"
"weight": 29
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Anpassad sortering av pivottabell programmatiskt i .NET

## Introduktion
När det gäller att arbeta med Excel i en .NET-miljö finns det ett bibliotek som sticker ut bland de andra: Aspose.Cells. Visst älskar du det när ett verktyg låter dig manipulera kalkylblad programmatiskt? Det är precis vad Aspose.Cells gör! I dagens handledning dyker vi djupt ner i pivottabellernas värld och visar dig hur du implementerar anpassad sortering programmatiskt med hjälp av detta mångsidiga bibliotek.
## Förkunskapskrav
Innan vi kavlar upp ärmarna och börjar med koden, se till att du har några saker på plats:
1. Visual Studio: Du behöver en fungerande version av Visual Studio. Det är lekplatsen där all magi händer.
2. .NET Framework: Kunskap om .NET-programmering är viktigt. Oavsett om du är en .NET Core- eller .NET Framework-entusiast är du redo att köra.
3. Aspose.Cells-biblioteket: Du behöver installera Aspose.Cells-biblioteket. Du kan hämta det från [Nedladdningslänk](https://releases.aspose.com/cells/net/) och lägg till det i ditt projekt.
4. Grundläggande förståelse för pivottabeller: Även om du inte behöver vara expert, kommer lite kunskap om hur pivottabeller fungerar att vara fördelaktigt när vi går igenom den här handledningen.
5. Exempel på Excel-fil: Ha en exempel-Excel-fil med namnet `SamplePivotSort.xlsx` redo i din arbetskatalog för testning.
## Importera paket
När du har sorterat alla dina förutsättningar är det första steget att importera de nödvändiga paketen. För att göra detta, inkludera följande rader högst upp i din kod:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
Det här paketet tillhandahåller all funktionalitet du behöver för att manipulera Excel-filer med Aspose.Cells.

Okej, låt oss gå vidare till det roliga! Vi ska dela upp processen att skapa en pivottabell och tillämpa anpassad sortering i hanterbara steg.
## Steg 1: Konfigurera arbetsboken
För att komma igång behöver vi ställa in vår arbetsbok. Så här gör du:
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
I det här steget initierar vi ett nytt `Workbook` exempel med sökvägen till vår Excel-fil. Detta fungerar som arbetsytan där vår pivottabell kommer att komma till liv.
## Steg 2: Öppna arbetsbladet
Nästa steg är att komma åt kalkylbladet där vi ska lägga till vår pivottabell.
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
Här tar vi det första arbetsbladet i vår arbetsbok och anropar `PivotTableCollection`Den här samlingen låter oss hantera alla pivottabeller i det här kalkylbladet.
## Steg 3: Skapa din första pivottabell
Nu är det dags att skapa vår pivottabell.
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
Vi lägger till en ny pivottabell i vårt kalkylblad och anger dataområdet och dess plats. "E3" anger var vi vill att vår pivottabell ska börja. Vi refererar sedan till den nya pivottabellen med hjälp av dess index.
## Steg 4: Konfigurera pivottabellinställningar
Nu konfigurerar vi vår pivottabell! Det innebär att kontrollera aspekter som totalsummor och fältarrangemang.
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
Vi ser till att totalsummor för rader och kolumner inte visas, vilket kan göra informationen renare. Sedan lägger vi till det första fältet i radområdet, vilket möjliggör automatisk sortering och stigande sortering.
## Steg 5: Lägg till kolumn- och datafält
När raderna är inställda lägger vi till kolumnen och datafälten.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
Vi lägger till det andra fältet som en kolumn och formaterar det som ett datum. Återigen aktiverar vi automatisk sortering och stigande ordning för att hålla ordning. Slutligen behöver vi lägga till det tredje fältet i vårt dataområde:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## Steg 6: Uppdatera och beräkna pivottabellen
När vi har lagt till alla nödvändiga fält, låt oss se till att vår pivottabell är färsk och redo.
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
Dessa metoder uppdaterar informationen och beräknar den på nytt, vilket säkerställer att allt är uppdaterat och visas korrekt i vår pivottabell.
## Steg 7: Anpassad sortering baserat på radfältvärden
Låt oss ge pivottabellen lite extra stil genom att sortera den efter specifika värden, som "Skaldjur".
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
Vi upprepar processen genom att skapa en annan pivottabell och konfigurera den på liknande sätt som den första. Vi kan nu anpassa den ytterligare:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## Steg 8: Ytterligare sorteringsanpassningLåt oss prova en annan sorteringsmetod baserad på ett specifikt datum:
```csharp
// Lägga till ytterligare en pivottabell för sortering efter datum
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// Upprepa rad- och kolumninställningar på samma sätt som i föregående steg
```
Du itererar bara igenom samma process och skapar en tredje pivottabell med dess sorteringskriterier anpassade efter dina behov.
## Steg 9: Spara WorkbookTime för att spara allt det hårda arbete vi har lagt ner!
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
Här sparar du arbetsboken som en Excel-fil och en PDF. `PdfSaveOptions` möjliggör bättre formatering, vilket säkerställer att varje ark visas på en separat sida när det konverteras.
## Steg 10: AvslutaAvsluta allt genom att låta användaren veta att allt är okej.
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## Slutsats
Vid det här laget har du lärt dig hur du utnyttjar kraften i Aspose.Cells för att skapa och anpassa pivottabeller i dina .NET-applikationer. Från initial installation till anpassad sortering kombineras varje steg för att ge en sömlös upplevelse. Oavsett om du behöver presentera årlig försäljningsdata eller spåra lagerstatistik, kommer dessa färdigheter att vara till stor nytta för dig!
## Vanliga frågor
### Vad är en pivottabell?
En pivottabell är ett databehandlingsverktyg i Excel som låter dig sammanfatta och analysera data, vilket ger ett flexibelt sätt att enkelt extrahera insikter.
### Hur installerar jag Aspose.Cells?
Du kan installera det via NuGet i Visual Studio eller ladda ner det direkt från [Nedladdningslänk](https://releases.aspose.com/cells/net/).
### Finns det en testversion av Aspose.Cells?
Ja! Du kan prova det gratis genom att besöka [Länk för gratis provperiod](https://releases.aspose.com/).
### Kan jag sortera flera fält i en pivottabell?
Absolut! Du kan lägga till och sortera flera fält baserat på dina behov.
### Var kan jag hitta support för Aspose.Cells?
Communityn är ganska aktiv, och du kan ställa frågor på deras forum [här](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}