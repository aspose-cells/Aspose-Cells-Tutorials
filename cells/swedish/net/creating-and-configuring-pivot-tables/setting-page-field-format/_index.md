---
"description": "Lär dig hur du programmatiskt ställer in sidfältformat i pivottabeller med Aspose.Cells för .NET. Följ vår steg-för-steg-handledning för sömlös datahantering."
"linktitle": "Ställa in sidfältsformat programmatiskt i .NET"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Ställa in sidfältsformat programmatiskt i .NET"
"url": "/sv/net/creating-and-configuring-pivot-tables/setting-page-field-format/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ställa in sidfältsformat programmatiskt i .NET

## Introduktion
Att skapa och manipulera Excel-filer med hjälp av kod kan vara ganska kraftfullt, särskilt när du behöver analysera stora datamängder. Ett av de fantastiska verktygen i din arsenal är Aspose.Cells för .NET, vilket låter dig programmatiskt interagera med Excel-filer och skapa komplexa rapporteringsstrukturer. I den här handledningen går vi in på hur du kan konfigurera sidfältformat i en pivottabell med hjälp av detta kraftfulla bibliotek. Oavsett om du är en erfaren utvecklare eller nybörjare, kommer du i slutet av den här guiden att ha en god förståelse för hur man arbetar med pivottabeller och deras olika inställningar i .NET.
## Förkunskapskrav
Innan vi kastar oss in i kodningen, låt oss se till att du har allt korrekt konfigurerat. Du behöver följande:
- Visual Studio: En arbetsmiljö där du kan skriva och exekvera din .NET-kod.
- Aspose.Cells: Du kan ladda ner biblioteket [här](https://releases.aspose.com/cells/net/).
- Grundläggande kunskaper i C#: Bekantskap med C#-programmering hjälper dig att förstå kodavsnitten bättre.
- Excel-fil: Ha en Excel-fil redo (t.ex. `Book1.xls`) som innehåller data som är lämpliga för att skapa pivottabeller. 
Om du inte redan har gjort det, skaffa en gratis provversion av Aspose.Cells [här](https://releases.aspose.com/).
## Importera paket
För att komma igång behöver du importera rätt paket i ditt projekt. Börja med att lägga till referenser till Aspose.Cells-biblioteket i ditt C#-projekt. Så här gör du:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Detta kommer att hämta alla nödvändiga klasser och metoder som behövs för att manipulera Excel-filer med Aspose.Cells.
## Steg 1: Konfigurera din arbetsyta
Börja med att definiera din arbetskatalog där dina Excel-filer ska lagras. Du kan till exempel deklarera en variabel så här:
```csharp
string dataDir = "Your Document Directory";
```
## Läser in arbetsboken
Nästa steg är att ladda vår Excel-mall. Detta är ett viktigt steg eftersom det etablerar sammanhanget för vår verksamhet:
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Den här raden laddar den befintliga arbetsboken från den angivna katalogen.
## Steg 2: Öppna arbetsbladet
När din arbetsbok har laddats är det dags att öppna kalkylbladet som innehåller pivottabellen eller de data du vill analysera. Så här gör du det:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Detta hämtar det första kalkylbladet i den laddade arbetsboken. Du kan enkelt ändra indexet om du arbetar med flera kalkylblad.
## Steg 3: Åtkomst till pivottabellen
Vi fortsätter och öppnar pivottabellen i vårt valda kalkylblad. Om du använder en enda pivottabell kan du ställa in dess index till `0`:
```csharp
int pivotindex = 0;
// Åtkomst till pivottabellen
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
Det här kodavsnittet väljer den första pivottabellen i kalkylbladet. 
## Steg 4: Konfigurera pivottabellen
Nu kommer den spännande delen! Låt oss ställa in pivottabellen så att den visar totalsummor för raderna:
```csharp
pivotTable.RowGrand = true;
```
Den här raden säkerställer att din rapport visar totalsummor, vilket kan vara en användbar sammanfattning för dataanalys.
## Steg 5: Åtkomst till och konfigurera radfält
Nästa steg är att komma åt radfälten i pivottabellen:
```csharp
Aspose.Cells.Pivot.PivotFieldCollection pivotFields = pivotTable.RowFields;
```
Den här samlingen låter oss manipulera fälten efter behov.
## Konfigurera fältet för första raden
Vill du ange specifika typer av delsummor? Nu ska vi öppna det första fältet i vår samling och konfigurera det:
```csharp
Aspose.Cells.Pivot.PivotField pivotField = pivotFields[0];
// Ställa in delsummor.
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Sum, true);
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Count, true);
```
Genom att aktivera `Sum` och `Count` delsummor kan vi snabbt sammanfatta data i vår rapport.
## Steg 6: Ställa in alternativ för automatisk sortering
Nu ska vi sätta igång lite smart sortering. På så sätt ordnar din pivottabell data i en meningsfull ordning:
```csharp
// Ställa in alternativ för automatisk sortering.
pivotField.IsAutoSort = true;
pivotField.IsAscendSort = true;
pivotField.AutoSortField = -5; // Använda ett fördefinierat sorteringsfält.
```
Det här kodavsnittet möjliggör automatisk sortering och anger stigande ordning. 
## Steg 7: Ställa in alternativ för automatisk visning
Vill du filtrera dina data ytterligare? Alternativet Visa automatiskt är användbart för att visa specifika datapunkter under definierade villkor:
```csharp
// Ställa in alternativ för automatisk visning.
pivotField.IsAutoShow = true;
pivotField.IsAscendShow = false;
pivotField.AutoShowField = 0; // Ange fältet som ska visas automatiskt.
```
Detta säkerställer att din pivottabell endast visar relevant data, vilket förbättrar tydlighet och fokus.
## Steg 8: Spara ditt arbete
Efter alla dessa konfigurationer vill du inte förlora ditt arbete! Spara den modifierade arbetsboken så här:
```csharp
workbook.Save(dataDir + "output.xls");
```
Nu kan du hitta den nyskapade Excel-filen i din dokumentkatalog.
## Slutsats
Och där har du det! Vi har gått igenom en omfattande och praktisk metod för att programmatiskt ställa in sidfältformat i en pivottabell med hjälp av Aspose.Cells för .NET. Med de enkla stegen som anges bör du känna dig trygg med att modifiera dina Excel-data för att passa dina rapporteringsbehov. Det är otroligt vad du kan uppnå när du kombinerar kraften i C# med Aspose.Cells.
## Vanliga frågor
### Vad är Aspose.Cells?
Aspose.Cells är ett .NET-bibliotek som låter utvecklare skapa, manipulera och konvertera Excel-filer programmatiskt.
### Hur installerar jag Aspose.Cells?
Du kan ladda ner den direkt från [Aspose webbplats](https://releases.aspose.com/cells/net/).
### Kan jag använda Aspose.Cells utan en Excel-installation?
Ja, Aspose.Cells är ett fristående bibliotek som inte kräver att Microsoft Excel är installerat.
### Var kan jag hitta detaljerad support?
Du kan få tillgång till detaljerad support och forum på [Aspose-stöd](https://forum.aspose.com/c/cells/9).
### Hur kan jag få en tillfällig licens?
Du kan få en tillfällig licens från [här](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}