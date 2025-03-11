---
title: Skapa en ny pivottabell programmatiskt i .NET
linktitle: Skapa en ny pivottabell programmatiskt i .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig att skapa en pivottabell programmatiskt i .NET med Aspose.Cells med vår steg-för-steg-guide. Analysera dina data effektivt.
weight: 13
url: /sv/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa en ny pivottabell programmatiskt i .NET

## Introduktion
Att skapa en pivottabell kan verka som en skrämmande uppgift, speciellt när du gör det programmatiskt. Men frukta inte! Med Aspose.Cells för .NET är det inte bara enkelt att sätta ihop en pivottabell utan också ganska kraftfullt för dataanalys. I den här handledningen guidar vi dig steg-för-steg om hur du skapar en ny pivottabell i en .NET-applikation. Oavsett om du lägger till data för försäljning, sport eller något annat affärsmått, hjälper den här guiden dig att få igång dina pivottabeller på nolltid.

## Förutsättningar
Innan du dyker in, låt oss se till att du har allt redo att gå. Här är vad du behöver göra:

1. Installera .NET Framework: Se till att du har .NET Framework installerat på din dator. Aspose.Cells stöder olika versioner, men det är bäst att hålla sig till den senaste.
2.  Aspose.Cells Library: Du måste ha Aspose.Cells-biblioteket. Du kan[ladda ner den här](https://releases.aspose.com/cells/net/)eller skaffa en[tillfällig licens](https://purchase.aspose.com/temporary-license/) för utvärdering.
3. IDE-installation: Ha en C#-kompatibel IDE redo, som Visual Studio, där du kan starta ett nytt projekt.
4. Grundläggande kunskaper om C#: Bekantskap med C#-programmering hjälper dig att följa med utan att bli alltför fast.

Är du redo? Stor! Låt oss börja importera de nödvändiga paketen.

## Importera paket
Först måste du importera de nödvändiga namnrymden till ditt C#-projekt. Öppna din C#-fil och lägg till följande med hjälp av direktiv:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Dessa namnrymder ger dig tillgång till arbetsboken, kalkylbladet och pivottabellfunktionerna som vi kommer att använda i den här självstudien.

## Steg 1: Skapa ett arbetsboksobjekt
Att skapa en arbetsbok är början på din resa. Låt oss börja med att instansiera en ny arbetsbok och komma åt det första kalkylbladet.

```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
// Instantiera ett arbetsboksobjekt
Workbook workbook = new Workbook();

// Få referensen till det nyligen tillagda kalkylbladet
Worksheet sheet = workbook.Worksheets[0];
```

 I detta steg skapar vi en`Workbook`instans som representerar vår Excel-fil och ta det allra första kalkylbladet, som kommer att vara vår lekplats för pivottabellen.

## Steg 2: Infoga data i celler
Låt oss sedan fylla i vårt kalkylblad med några exempeldata. Vi kommer att mata in rader för olika sporter, kvartal och försäljningssiffror för att ge vår pivottabell något att sammanfatta.

```csharp
Cells cells = sheet.Cells;

// Ställer in värdet på cellerna
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

// Fylla datacell = celler["A2"];
cell.PutValue("Golf");
// ... Fler datainmatningar
```

Här definierar vi våra kolumnrubriker och infogar värden under varje rubrik. Denna data kommer att fungera som källan för vår pivottabell, så se till att den är organiserad! Följ det här blocket så skapar du en omfattande datauppsättning.

## Steg 3: Lägga till en pivottabell
Med vår data redo är det dags att skapa pivottabellen. Vi kommer att använda pivottabellsamlingen från kalkylbladet för att lägga till vår nya pivottabell.

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// Lägga till en pivottabell till kalkylbladet
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

det här utdraget lägger vi till en pivottabell i kalkylbladet som refererar till vårt dataområde (i det här fallet cellerna A1 till C8). Vi placerar pivottabellen med början vid cell E3 och ger den namnet "Pivottabell2". Ganska enkelt, eller hur?

## Steg 4: Anpassa pivottabellen
Nu när vi har vår pivottabell, låt oss anpassa den för att visa meningsfulla sammanfattningar. Vi kan styra vad som visas i raderna, kolumnerna och dataområdena i pivottabellen.

```csharp
// Åtkomst till instansen av den nyligen tillagda pivottabellen
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

// Avvisar totalsummor för rader.
pivotTable.RowGrand = false;

// Dra det första fältet till radområdet.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

// Dra det andra fältet till kolumnområdet.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

// Dra det tredje fältet till dataområdet.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

I det här steget säger vi åt pivottabellen att dölja totalsummor för rader och sedan specificera vilka fält som ska gå in i rad-, kolumn- och dataområdena. Sportnamnen kommer att fylla raderna, kvartalen kommer att fylla kolumnerna och försäljningssiffrorna kommer att ge sammanfattningarna.

## Steg 5: Spara arbetsboken
Slutligen vill vi spara vår nyskapade arbetsbok för att se frukterna av vårt arbete.

```csharp
// Sparar Excel-filen
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

Ange bara en korrekt sökväg, så har du din pivottabellsutdata sparad i en Excel-fil som du kan öppna och granska.

## Slutsats
Att skapa pivottabeller programmatiskt med Aspose.Cells för .NET kan avsevärt spara tid, särskilt när du hanterar stora datamängder. Du har lärt dig hur du ställer in ditt projekt, importerar nödvändiga paket, fyller i data och skapar en anpassningsbar pivottabell från början. Så nästa gång du drunknar i siffror, kom ihåg den här handledningen och låt Aspose.Cells göra det tunga arbetet åt dig.

## FAQ's
### Vad är Aspose.Cells?
Aspose.Cells är ett kraftfullt .NET-bibliotek för att skapa och hantera Excel-kalkylblad programmatiskt.

### Finns det en gratis provperiod för Aspose.Cells?
 Ja, du kan få en gratis provperiod[här](https://releases.aspose.com/).

### Kan jag anpassa utseendet på pivottabellen?
Absolut! Du kan anpassa formatering, layout och till och med stilar för pivottabellen enligt dina behov.

### Var kan jag hitta fler exempel och dokumentation om Aspose.Cells?
 Du kan kontrollera[dokumentation](https://reference.aspose.com/cells/net/) för omfattande guider och exempel.

### Hur får jag support för Aspose.Cells?
 Du kan få stöd genom[Aspose forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
