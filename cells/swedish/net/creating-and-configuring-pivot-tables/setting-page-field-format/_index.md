---
title: Ställa in sidfältsformat Programmatiskt i .NET
linktitle: Ställa in sidfältsformat Programmatiskt i .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du ställer in sidfältsformat i pivottabeller programmatiskt med Aspose.Cells för .NET. Följ vår steg-för-steg handledning för sömlös datahantering.
weight: 21
url: /sv/net/creating-and-configuring-pivot-tables/setting-page-field-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ställa in sidfältsformat Programmatiskt i .NET

## Introduktion
Att skapa och manipulera Excel-filer genom kod kan vara ganska givande, särskilt när du behöver analysera stora datamängder. Ett av de fantastiska verktygen i din arsenal är Aspose.Cells för .NET, som låter dig interagera programmatiskt med Excel-filer och skapa komplexa rapporteringsstrukturer. I den här handledningen kommer vi att fördjupa oss i hur du kan ställa in sidfältsformat i en pivottabell med detta kraftfulla bibliotek. Oavsett om du är en erfaren utvecklare eller nybörjare, i slutet av den här guiden har du ett bra grepp om hur du arbetar med pivottabeller och deras olika inställningar i .NET.
## Förutsättningar
Innan vi går in i kodning först, låt oss se till att du har allt rätt inställt. Du behöver följande:
- Visual Studio: En arbetsmiljö där du kan skriva och köra din .NET-kod.
-  Aspose.Cells: Du kan ladda ner biblioteket[här](https://releases.aspose.com/cells/net/).
- Grundläggande kunskaper i C#: Bekantskap med C#-programmering hjälper dig att förstå kodavsnitten bättre.
-  Excel-fil: Ha en Excel-fil redo (som`Book1.xls`) som innehåller data som är lämpliga för att skapa pivottabeller. 
 Om du inte redan har gjort det kan du prova Aspose.Cells gratis[här](https://releases.aspose.com/).
## Importera paket
För att komma igång måste du importera rätt paket i ditt projekt. Börja med att lägga till referenser till Aspose.Cells-biblioteket i ditt C#-projekt. Så här gör du:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Detta kommer att dra in alla nödvändiga klasser och metoder som behövs för att manipulera Excel-filer med Aspose.Cells.
## Steg 1: Konfigurera din arbetsyta
Börja med att definiera din arbetskatalog där dina Excel-filer ska lagras. Du kan till exempel deklarera en variabel så här:
```csharp
string dataDir = "Your Document Directory";
```
## Laddar arbetsboken
Nästa steg måste vi ladda vår Excel-mall. Detta är ett viktigt steg eftersom det skapar sammanhanget för vår verksamhet:
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Den här raden laddar den befintliga arbetsboken från den angivna katalogen.
## Steg 2: Öppna arbetsbladet
När din arbetsbok har laddats är det dags att komma åt kalkylbladet som innehåller pivottabellen eller de data du vill analysera. Så här kan du göra det:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Detta tar det första kalkylbladet i den laddade arbetsboken. Du kan enkelt ändra indexet om du arbetar med flera ark.
## Steg 3: Åtkomst till pivottabellen
 Fortsätter vi, låt oss komma åt pivottabellen i vårt valda kalkylblad. Om du använder en enda pivottabell kan du ställa in dess index till`0`:
```csharp
int pivotindex = 0;
// Åtkomst till pivottabellen
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
Detta kodavsnitt väljer den första pivottabellen i kalkylbladet. 
## Steg 4: Konfigurera pivottabellen
Nu kommer den spännande delen! Låt oss ställa in pivottabellen för att visa totalsummor för raderna:
```csharp
pivotTable.RowGrand = true;
```
Den här raden säkerställer att din rapport visar totalsummor som kan vara en användbar sammanfattning för dataanalys.
## Steg 5: Få åtkomst till och konfigurera radfält
Därefter måste vi komma åt radfälten i pivottabellen:
```csharp
Aspose.Cells.Pivot.PivotFieldCollection pivotFields = pivotTable.RowFields;
```
Denna samling låter oss manipulera fälten efter behov.
## Konfigurera första radfältet
Vill du ställa in specifika delsummatyper? Låt oss komma åt det första fältet i vår samling och konfigurera det:
```csharp
Aspose.Cells.Pivot.PivotField pivotField = pivotFields[0];
// Ställa in delsummor.
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Sum, true);
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Count, true);
```
 Genom att aktivera`Sum` och`Count` delsummor kan vi snabbt sammanfatta data i vår rapport.
## Steg 6: Ställa in alternativ för autosortering
Låt oss sedan sätta in lite smart sortering. På så sätt kommer din pivottabell att ordna data i en meningsfull ordning:
```csharp
// Ställa in alternativ för autosortering.
pivotField.IsAutoSort = true;
pivotField.IsAscendSort = true;
pivotField.AutoSortField = -5; // Använder ett fördefinierat sorteringsfält.
```
Detta kodavsnitt möjliggör automatisk sortering och anger stigande ordning. 
## Steg 7: Ställa in AutoShow-alternativ
Vill du filtrera din data ytterligare? Alternativet AutoShow är användbart för att visa specifika datapunkter under definierade förhållanden:
```csharp
// Ställa in alternativ för autoShow.
pivotField.IsAutoShow = true;
pivotField.IsAscendShow = false;
pivotField.AutoShowField = 0; // Ange fältet som ska visas automatiskt.
```
Detta säkerställer att din pivottabell endast visar relevant data, vilket förbättrar tydlighet och fokus.
## Steg 8: Spara ditt arbete
Efter alla dessa konfigurationer skulle du inte vilja förlora ditt arbete! Spara den ändrade arbetsboken så här:
```csharp
workbook.Save(dataDir + "output.xls");
```
Nu kan du hitta den nyskapade Excel-filen i din dokumentkatalog.
## Slutsats
Och där har du det! Vi har gått igenom en omfattande och praktisk metod för att ställa in sidfältsformat programmatiskt i en pivottabell med Aspose.Cells för .NET. Med de enkla stegen som tillhandahålls bör du känna dig säker på att modifiera dina Excel-data för att passa dina rapporteringsbehov. Det är otroligt vad du kan uppnå när du kombinerar kraften i C# med Aspose.Cells.
## FAQ's
### Vad är Aspose.Cells?
Aspose.Cells är ett .NET-bibliotek som låter utvecklare skapa, manipulera och konvertera Excel-filer programmatiskt.
### Hur installerar jag Aspose.Cells?
 Du kan ladda ner den direkt från[Aspose hemsida](https://releases.aspose.com/cells/net/).
### Kan jag använda Aspose.Cells utan en Excel-installation?
Ja, Aspose.Cells är ett fristående bibliotek som inte kräver att Microsoft Excel installeras.
### Var kan jag hitta detaljerad support?
 Du kan komma åt detaljerad support och forum på[Aspose Support](https://forum.aspose.com/c/cells/9).
### Hur kan jag få en tillfällig licens?
 Du kan skaffa en tillfällig licens från[här](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
