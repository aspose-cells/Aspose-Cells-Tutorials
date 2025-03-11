---
title: Ange programmets kompatibilitet för Excel-fil i .NET
linktitle: Ange programmets kompatibilitet för Excel-fil i .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig att manipulera Excel-pivottabeller med Aspose.Cells för .NET, inklusive datauppdateringar, kompatibilitetsinställningar och cellformatering.
weight: 23
url: /sv/net/creating-and-configuring-pivot-tables/specifying-compatibility/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ange programmets kompatibilitet för Excel-fil i .NET

## Introduktion

dagens datadrivna värld har det blivit viktigt för många utvecklare att hantera och manipulera Excel-filer programmatiskt. Om du arbetar med Excel i .NET är Aspose.Cells ett kraftfullt bibliotek som gör det enkelt att skapa, läsa, ändra och spara Excel-filer. En viktig funktion i detta bibliotek låter dig ange kompatibiliteten för Excel-filer programmatiskt. I den här handledningen kommer vi att utforska hur man manipulerar Excel-filer, särskilt med fokus på att hantera kompatibilitet med Aspose.Cells för .NET. I slutet kommer du att förstå hur du ställer in kompatibilitet för Excel-filer, särskilt för pivottabeller, samtidigt som du uppdaterar och hanterar data.

## Förutsättningar

Innan du dyker in i kodningsfasen, se till att du har följande:

1. Grundläggande kunskaper i C#: Eftersom vi kommer att skriva kod i C#, kommer kunskaper i språket att hjälpa dig att förstå handledningen bättre.
2.  Aspose.Cells för .NET-bibliotek: Du kan ladda ner det från[Aspose Cells släpper sida](https://releases.aspose.com/cells/net/)Om du inte redan har gjort det, överväg att få en gratis provperiod för att utforska dess funktioner först.
3. Visual Studio: En IDE där du kan skriva och testa din C#-kod effektivt.
4.  Exempel på Excel-fil: Se till att du har ett exempel på Excel-fil, helst en som innehåller en pivottabell för demon. För vårt exempel kommer vi att använda`sample-pivot-table.xlsx`.

Med dessa förutsättningar på plats, låt oss komma igång med kodningsprocessen.

## Importera paket

Innan du börjar skriva din ansökan måste du inkludera de nödvändiga namnrymden i din kod för att kunna använda Aspose.Cells-biblioteket effektivt. Så här gör du.

### Importera Aspose.Cells namnområde

```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Pivot;
using System.Drawing;
```

Denna kodrad säkerställer att du kan komma åt alla klasser och metoder inom Aspose.Cells-biblioteket.

Låt oss nu bryta ner processen i detalj för att säkerställa att allt är klart och begripligt.

## Steg 1: Konfigurera din katalog

Först och främst, ställ in katalogen där dina Excel-filer finns. Det är viktigt att ange rätt filsökväg.

```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
```

 Här, byt ut`"Your Document Directory"`med den faktiska sökvägen till dina Excel-filer. Det är här din exempelpivottabellsfil ska finnas.

## Steg 2: Ladda källfilen för Excel

Därefter måste vi ladda Excel-filen som innehåller exempelpivottabellen. 

```csharp
// Ladda källexcel-fil som innehåller exempel på pivottabell
Workbook wb = new Workbook(dataDir + "sample-pivot-table.xlsx");
```

 I det här steget skapar vi en instans av`Workbook` klass, som laddar den angivna Excel-filen. 

## Steg 3: Öppna arbetsbladen

Nu när arbetsboken är laddad måste du komma åt kalkylbladet som innehåller pivottabellsdata.

```csharp
// Få tillgång till det första kalkylbladet som innehåller pivottabelldata
Worksheet dataSheet = wb.Worksheets[0];
```

Här kommer vi åt det första kalkylbladet där pivottabellen finns. Du kan också gå igenom eller specificera andra kalkylblad baserat på din Excel-struktur.

## Steg 4: Manipulera celldata

Nästa upp kommer du att ändra några cellvärden i kalkylbladet. 

### Steg 4.1: Ändra cell A3

Låt oss börja med att komma åt cell A3 och ställa in dess värde.

```csharp
// Gå till cell A3 och ställer in dess data
Cells cells = dataSheet.Cells;
Cell cell = cells["A3"];
cell.PutValue("FooBar");
```

Detta kodavsnitt uppdaterar cell A3 med värdet "FooBar".

### Steg 4.2: Ändra cell B3 med lång sträng

Låt oss nu sätta en lång sträng i cell B3, som överskrider Excels standardteckengränser.

```csharp
// Åtkomst till cell B3, ställer in dess data
string longStr = "Very long text 1. very long text 2.... [continue your long string]";
cell = cells["B3"];
cell.PutValue(longStr);
```

Den här koden är viktig eftersom den sätter dina förväntningar på datagränser, särskilt när du arbetar med kompatibilitetsinställningar i Excel.

## Steg 5: Kontrollera längden på cell B3

Det är också viktigt att bekräfta längden på strängen vi skrev in.

```csharp
// Skriv ut längden på cell B3-strängen
Console.WriteLine("Length of original data string: " + cell.StringValue.Length);
```

Detta är bara för verifiering för att visa hur många tecken din cell innehåller.

## Steg 6: Ställ in andra cellvärden

Nu kommer vi åt fler celler och ställer in några värden.

```csharp
// Gå till cell C3 och ställer in dess data
cell = cells["C3"];
cell.PutValue("closed");

// Gå till cell D3 och ställer in dess data
cell = cells["D3"];
cell.PutValue("2016/07/21");
```

Var och en av dessa utdrag uppdaterar flera ytterligare celler i kalkylbladet.

## Steg 7: Gå till pivottabellen

Därefter kommer du åt det andra kalkylbladet, som består av pivottabellsdata.

```csharp
//Öppna det andra kalkylbladet som innehåller pivottabellen
Worksheet pivotSheet = wb.Worksheets[1];

// Gå till pivottabellen
PivotTable pivotTable = pivotSheet.PivotTables[0];
```

Det här utdraget låter dig manipulera pivottabellen för kompatibilitetsinställningar.

## Steg 8: Ställ in kompatibilitet för Excel 2003

Det är avgörande att ställa in om din pivottabell är kompatibel med Excel 2003 eller inte. 

```csharp
// IsExcel2003Compatible-egenskapen talar om om PivotTable är kompatibel med Excel2003 medan pivottabellen uppdateras
pivotTable.IsExcel2003Compatible = true;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

 Det är här den verkliga förvandlingen börjar. Genom att ställa in`IsExcel2003Compatible` till`true`, begränsar du teckenlängder till 255 vid uppdatering.

## Steg 9: Kontrollera längden efter kompatibilitetsinställning

Efter att ha ställt in kompatibiliteten, låt oss se hur det påverkar data.

```csharp
// Kontrollera värdet på cell B5 på pivotbladet.
Cell b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to True: " + b5.StringValue.Length);
```

Du kommer sannolikt att se en utdata som bekräftar trunkeringseffekten om den ursprungliga data överstiger 255 tecken.

## Steg 10: Ändra kompatibilitetsinställning

Låt oss nu ändra kompatibilitetsinställningen och kontrollera igen.

```csharp
//Ställ nu in IsExcel2003Compatible-egenskapen på false och uppdatera igen
pivotTable.IsExcel2003Compatible = false;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

Detta gör att dina data återspeglar sin ursprungliga längd utan de tidigare begränsningarna.

## Steg 11: Verifiera längden igen 

Låt oss verifiera att data nu exakt återspeglar dess verkliga längd.

```csharp
// Nu kommer den att skriva ut den ursprungliga längden på celldata. Uppgifterna har inte trunkerats nu.
b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to False: " + b5.StringValue.Length);
```

Du bör se att utgången bekräftar borttagningen av trunkeringen.

## Steg 12: Formatera cellerna

För att förbättra den visuella upplevelsen kanske du vill formatera cellerna. 

```csharp
// Ställ in radhöjd och kolumnbredd för cell B5 och radbryt även dess text
pivotSheet.Cells.SetRowHeight(b5.Row, 100);
pivotSheet.Cells.SetColumnWidth(b5.Column, 65);
Style st = b5.GetStyle();
st.IsTextWrapped = true;
b5.SetStyle(st);
```

Dessa kodrader gör data lättare att läsa genom att justera celldimensionerna och aktivera textbrytning.

## Steg 13: Spara arbetsboken

Slutligen, spara din arbetsbok med de ändringar du har gjort.

```csharp
// Spara arbetsbok i xlsx-format
wb.Save(dataDir + "SpecifyCompatibility_out.xlsx", SaveFormat.Xlsx);
```

 Att välja ett lämpligt filformat är avgörande när du sparar Excel-filer. De`Xlsx`formatet används ofta och är kompatibelt med många Excel-versioner.

## Slutsats

Grattis! Du har nu programmerat Excel-filkompatibilitetsinställningar med Aspose.Cells för .NET. Den här handledningen beskrev varje steg, från att ställa in din miljö till att ändra kompatibilitetsinställningar för pivottabeller. Om du någonsin har arbetat med data som krävde specifika begränsningar eller kompatibilitet, är detta en färdighet du inte vill förbise.

## FAQ's

### Vad är Aspose.Cells?  
Aspose.Cells är ett .NET-bibliotek designat för att hjälpa utvecklare att skapa, manipulera och konvertera Excel-filer sömlöst.

### Varför är Excel-kompatibilitet viktigt?  
Excel-kompatibilitet är avgörande för att säkerställa att filer kan öppnas och användas i de avsedda versionerna av Excel, särskilt om de innehåller funktioner eller format som inte stöds i tidigare versioner.

### Kan jag skapa pivottabeller programmatiskt med Aspose.Cells?  
Ja, du kan skapa och manipulera pivottabeller programmatiskt med Aspose.Cells. Biblioteket tillhandahåller olika metoder för att lägga till datakällor, fält och funktioner associerade med pivottabeller.

### Hur kontrollerar jag längden på en sträng i en Excel-cell?  
Du kan använda`StringValue` egendom hos en`Cell` objekt för att få innehållet i cellen och anropa sedan`.Length` egenskap för att ta reda på längden på strängen.

### Kan jag anpassa cellformatering utöver radhöjd och bredd?  
 Absolut! Aspose.Cells möjliggör omfattande cellformatering. Du kan ändra teckensnitt, färger, ramar, talformat och mycket mer genom`Style` klass.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
