---
title: Pivottabell Anpassad sortering Programmatiskt i .NET
linktitle: Pivottabell Anpassad sortering Programmatiskt i .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du programmatiskt sorterar pivottabeller i .NET med Aspose.Cells. En steg-för-steg-guide som täcker inställning, konfiguration, sortering och sparande av resultat som Excel- och PDF-filer.
weight: 29
url: /sv/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pivottabell Anpassad sortering Programmatiskt i .NET

## Introduktion
När det gäller att arbeta med Excel i en .NET-miljö sticker ett bibliotek ut bland resten: Aspose.Cells. Älskar du inte bara när ett verktyg låter dig manipulera kalkylark programmatiskt? Det är precis vad Aspose.Cells gör! I dagens självstudie dyker vi djupt in i pivottabellernas värld och visar dig hur du implementerar anpassad sortering programmatiskt med detta mångsidiga bibliotek.
## Förutsättningar
Innan vi kavlar upp ärmarna och hoppar in i koden, se till att du har några saker på plats:
1. Visual Studio: Du behöver en fungerande version av Visual Studio. Det är lekplatsen där all magi händer.
2. .NET Framework: Bekantskap med .NET-programmering är viktigt. Oavsett om du är en .NET Core- eller .NET Framework-entusiast är du bra att gå.
3.  Aspose.Cells Library: Du måste installera Aspose.Cells-biblioteket. Du kan få det från[Ladda ner länk](https://releases.aspose.com/cells/net/) och lägg till det i ditt projekt.
4. Grundläggande förståelse för pivottabeller: Även om du inte behöver vara expert, kommer lite kunskap om hur pivottabeller fungerar att vara till nytta när vi går igenom den här handledningen.
5.  Exempel på Excel-fil: Låt ett exempel på Excel-fil namnges`SamplePivotSort.xlsx` redo i din arbetskatalog för testning.
## Importera paket
När du har sorterat alla dina förutsättningar är det första steget att importera de nödvändiga paketen. För att göra detta, inkludera följande rader överst i koden:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
Detta paket tillhandahåller all funktionalitet du behöver för att manipulera Excel-filer med Aspose.Cells.

Okej, låt oss gå in på den roliga delen! Vi kommer att dela upp processen att skapa en pivottabell och tillämpa anpassad sortering i hanterbara steg.
## Steg 1: Konfigurera arbetsboken
För att få igång saker och ting måste vi sätta upp vår arbetsbok. Så här gör du:
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
 I det här steget initierar vi en ny`Workbook` instans med sökvägen till vår Excel-fil. Detta fungerar som duken där vårt pivotbord kommer till liv.
## Steg 2: Öppna arbetsbladet
Därefter måste vi komma åt kalkylbladet där vi lägger till vår pivottabell.
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
 Här tar vi tag i det första kalkylbladet i vår arbetsbok och ringer till`PivotTableCollection`. Den här samlingen låter oss hantera alla pivottabeller i detta kalkylblad.
## Steg 3: Skapa din första pivottabell
Nu är det dags att skapa vår pivottabell.
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
Vi lägger till en ny pivottabell i vårt kalkylblad, som anger dataintervallet och dess plats. "E3" indikerar var vi vill att vår pivottabell ska börja. Vi refererar sedan till denna nya pivottabell med hjälp av dess index.
## Steg 4: Konfigurera pivottabellinställningar
Låt oss konfigurera vår pivottabell! Detta innebär att kontrollera aspekter som totalsummor och fältarrangemang.
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
Vi ser till att totalsummor för rader och kolumner inte visas, vilket kan göra data renare. Sedan lägger vi till det första fältet i radområdet, vilket möjliggör automatisk sortering och en stigande sortering.
## Steg 5: Lägg till kolumn- och datafält
När raderna är inställda, låt oss lägga till kolumnen och datafälten.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
Vi lägger till det andra fältet som en kolumn och formaterar det som ett datum. Återigen, vi aktiverar automatisk sortering och stigande ordning för att hålla ordning på saker och ting. Slutligen måste vi lägga till det tredje fältet till vårt dataområde:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## Steg 6: Uppdatera och beräkna pivottabellen
Efter att ha lagt till alla nödvändiga fält, låt oss se till att vår pivottabell är fräsch och klar.
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
Dessa metoder uppdaterar data och räknar om dem, vilket säkerställer att allt är uppdaterat och visas korrekt i vår pivottabell.
## Steg 7: Anpassad sortering baserat på radfältsvärden
Låt oss lägga till lite känsla genom att sortera pivottabellen baserat på specifika värden, som "SeaFood".
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
Vi upprepar processen genom att skapa en annan pivottabell och ställa in den på samma sätt som den första. Vi kan nu anpassa det ytterligare:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## Steg 8: Ytterligare sorteringsanpassningLåt oss prova en annan sorteringsmetod baserat på ett specifikt datum:
```csharp
// Lägga till ytterligare en pivottabell för sortering efter ett datum
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// Upprepa rad- och kolumninställningar som liknar tidigare steg
```
Du går bara igenom samma process och skapar en tredje pivottabell med dess sorteringskriterier skräddarsydda efter dina behov.
## Steg 9: Spara WorkbookTime för att spara allt hårt arbete vi har lagt ner!
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
 Här sparar du arbetsboken som en Excel-fil och en PDF. De`PdfSaveOptions` möjliggör bättre formatering, vilket säkerställer att varje ark visas på en separat sida när det konverteras.
## Steg 10: Avsluta UpWrap det hela genom att låta användaren veta att allt är coolt.
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## Slutsats
Vid det här laget har du lärt dig hur du kan utnyttja kraften i Aspose.Cells för att skapa och anpassa pivottabeller i dina .NET-applikationer. Från den första installationen till anpassad sortering kombineras varje steg för att leverera en sömlös upplevelse. Oavsett om du behöver presentera årliga försäljningsdata eller spåra lagerstatistik, kommer dessa färdigheter att tjäna dig väl!
## FAQ's
### Vad är en pivottabell?
En pivottabell är ett databearbetningsverktyg i Excel som låter dig sammanfatta och analysera data, vilket ger ett flexibelt sätt att extrahera insikter enkelt.
### Hur installerar jag Aspose.Cells?
 Du kan installera den via NuGet i Visual Studio eller ladda ner den direkt från[Ladda ner länk](https://releases.aspose.com/cells/net/).
### Finns det en testversion av Aspose.Cells?
 Ja! Du kan prova det gratis genom att besöka[Gratis testlänk](https://releases.aspose.com/).
### Kan jag sortera flera fält i en pivottabell?
Absolut! Du kan lägga till och sortera flera fält baserat på dina krav.
### Var kan jag hitta support för Aspose.Cells?
 Gemenskapen är ganska aktiv, och du kan ställa frågor på deras forum[här](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
