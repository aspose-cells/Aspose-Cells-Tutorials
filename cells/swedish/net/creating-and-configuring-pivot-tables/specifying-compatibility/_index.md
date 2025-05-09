---
"description": "Lär dig att manipulera pivottabeller i Excel med Aspose.Cells för .NET, inklusive datauppdateringar, kompatibilitetsinställningar och cellformatering."
"linktitle": "Ange kompatibilitet för Excel-filer programmatiskt i .NET"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Ange kompatibilitet för Excel-filer programmatiskt i .NET"
"url": "/sv/net/creating-and-configuring-pivot-tables/specifying-compatibility/"
"weight": 23
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ange kompatibilitet för Excel-filer programmatiskt i .NET

## Introduktion

I dagens datadrivna värld har det blivit viktigt för många utvecklare att hantera och manipulera Excel-filer programmatiskt. Om du arbetar med Excel i .NET är Aspose.Cells ett kraftfullt bibliotek som gör det enkelt att skapa, läsa, ändra och spara Excel-filer. En viktig funktion i detta bibliotek låter dig ange kompatibiliteten för Excel-filer programmatiskt. I den här handledningen kommer vi att utforska hur man manipulerar Excel-filer, med särskilt fokus på att hantera kompatibilitet med Aspose.Cells för .NET. I slutet kommer du att förstå hur du ställer in kompatibilitet för Excel-filer, särskilt för pivottabeller, samtidigt som du uppdaterar och hanterar data.

## Förkunskapskrav

Innan du går in i kodningsfasen, se till att du har följande:

1. Grundläggande kunskaper i C#: Eftersom vi kommer att skriva kod i C#, kommer förtrogenhet med språket att hjälpa dig att förstå handledningen bättre.
2. Aspose.Cells för .NET-biblioteket: Du kan ladda ner det från [Aspose Cells utgivningssida](https://releases.aspose.com/cells/net/)Om du inte redan har gjort det, överväg att testa gratis för att utforska funktionerna först.
3. Visual Studio: En IDE där du effektivt kan skriva och testa din C#-kod.
4. Exempel på Excel-fil: Se till att du har en exempelfil i Excel, helst en som innehåller en pivottabell för demon. I vårt exempel använder vi `sample-pivot-table.xlsx`.

Med dessa förutsättningar på plats, låt oss börja med kodningsprocessen.

## Importera paket

Innan du börjar skriva din applikation måste du inkludera de namnrymder som behövs i din kod för att kunna använda Aspose.Cells-biblioteket effektivt. Så här gör du.

### Importera Aspose.Cells namnrymd

```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Pivot;
using System.Drawing;
```

Den här kodraden säkerställer att du kan komma åt alla klasser och metoder i Aspose.Cells-biblioteket.

Nu ska vi gå igenom processen i detalj för att säkerställa att allt är tydligt och förståeligt.

## Steg 1: Konfigurera din katalog

Först och främst, konfigurera katalogen där dina Excel-filer finns. Det är viktigt att ange rätt sökväg.

```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
```

Här, ersätt `"Your Document Directory"` med den faktiska sökvägen till dina Excel-filer. Det är här din exempelpivottabellfil ska finnas.

## Steg 2: Ladda källfilen i Excel

Sedan måste vi ladda Excel-filen som innehåller exempelpivottabellen. 

```csharp
// Ladda källfilen i Excel som innehåller exempelpivottabellen
Workbook wb = new Workbook(dataDir + "sample-pivot-table.xlsx");
```

I det här steget skapar vi en instans av `Workbook` klassen, som laddar den angivna Excel-filen. 

## Steg 3: Få åtkomst till arbetsbladen

Nu när arbetsboken är laddad måste du komma åt kalkylbladet som innehåller pivottabelldata.

```csharp
// Åtkomst till det första kalkylbladet som innehåller pivottabelldata
Worksheet dataSheet = wb.Worksheets[0];
```

Här öppnar vi det första kalkylbladet där pivottabellen finns. Du kan också loopa igenom eller ange andra kalkylblad baserat på din Excel-struktur.

## Steg 4: Manipulera celldata

Nästa steg är att ändra några cellvärden i kalkylbladet. 

### Steg 4.1: Ändra cell A3

Låt oss börja med att komma åt cell A3 och ange dess värde.

```csharp
// Gå till cell A3 och ange dess data
Cells cells = dataSheet.Cells;
Cell cell = cells["A3"];
cell.PutValue("FooBar");
```

Det här kodavsnittet uppdaterar cell A3 med värdet ”FooBar”.

### Steg 4.2: Ändra cell B3 med lång sträng

Nu ska vi ange en lång sträng i cell B3, som överskrider Excels standardteckengränser.

```csharp
// Åtkomst till cell B3, anger dess data
string longStr = "Very long text 1. very long text 2.... [continue your long string]";
cell = cells["B3"];
cell.PutValue(longStr);
```

Den här koden är viktig eftersom den anger dina förväntningar gällande datagränser, särskilt när du arbetar med kompatibilitetsinställningar i Excel.

## Steg 5: Kontrollera längden på cell B3

Det är också viktigt att bekräfta längden på strängen vi angav.

```csharp
// Skriv ut längden på cell B3-strängen
Console.WriteLine("Length of original data string: " + cell.StringValue.Length);
```

Detta är bara för verifiering för att visa hur många tecken din cell innehåller.

## Steg 6: Ange andra cellvärden

Nu ska vi komma åt fler celler och ange några värden.

```csharp
// Gå till cell C3 och ange dess data
cell = cells["C3"];
cell.PutValue("closed");

// Gå till cell D3 och ange dess data
cell = cells["D3"];
cell.PutValue("2016/07/21");
```

Var och en av dessa kodavsnitt uppdaterar flera ytterligare celler i kalkylbladet.

## Steg 7: Åtkomst till pivottabellen

Därefter kommer du åt det andra kalkylbladet, som består av pivottabelldata.

```csharp
// Få åtkomst till det andra kalkylbladet som innehåller pivottabellen
Worksheet pivotSheet = wb.Worksheets[1];

// Åtkomst till pivottabellen
PivotTable pivotTable = pivotSheet.PivotTables[0];
```

Det här kodavsnittet låter dig manipulera pivottabellen för kompatibilitetsinställningar.

## Steg 8: Ställ in kompatibilitet för Excel 2003

Det är avgörande att ange om din pivottabell är kompatibel med Excel 2003 eller inte. 

```csharp
// Egenskapen IsExcel2003Compatible anger om pivottabellen är kompatibel med Excel 2003 när pivottabellen uppdateras
pivotTable.IsExcel2003Compatible = true;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

Det är här den verkliga förvandlingen börjar. Genom att sätta `IsExcel2003Compatible` till `true`begränsar du teckenlängden till 255 vid uppdatering.

## Steg 9: Kontrollera längden efter kompatibilitetsinställningen

Efter att ha ställt in kompatibiliteten, låt oss se hur det påverkar data.

```csharp
// Kontrollera värdet i cell B5 i pivotarket.
Cell b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to True: " + b5.StringValue.Length);
```

Du kommer sannolikt att se en utdata som bekräftar trunkeringseffekten om initialdata överstiger 255 tecken.

## Steg 10: Ändra kompatibilitetsinställningen

Nu ska vi ändra kompatibilitetsinställningen och kontrollera igen.

```csharp
// Ställ nu in egenskapen IsExcel2003Compatible till falskt och uppdatera igen
pivotTable.IsExcel2003Compatible = false;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

Detta gör att dina data kan återspegla sin ursprungliga längd utan tidigare begränsningar.

## Steg 11: Verifiera längden igen 

Låt oss verifiera att informationen nu korrekt återspeglar dess verkliga längd.

```csharp
// Nu kommer den att skriva ut den ursprungliga längden på celldata. Informationen har inte avkortats nu.
b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to False: " + b5.StringValue.Length);
```

Du bör se att utdata bekräftar borttagningen av trunkeringen.

## Steg 12: Formatera cellerna

För att förbättra den visuella upplevelsen kanske du vill formatera cellerna. 

```csharp
// Ställ in radhöjd och kolumnbredd för cell B5 och radbryt även texten
pivotSheet.Cells.SetRowHeight(b5.Row, 100);
pivotSheet.Cells.SetColumnWidth(b5.Column, 65);
Style st = b5.GetStyle();
st.IsTextWrapped = true;
b5.SetStyle(st);
```

Dessa kodrader gör informationen lättare att läsa genom att justera celldimensionerna och aktivera textbrytning.

## Steg 13: Spara arbetsboken

Spara slutligen din arbetsbok med de ändringar du har gjort.

```csharp
// Spara arbetsboken i xlsx-format
wb.Save(dataDir + "SpecifyCompatibility_out.xlsx", SaveFormat.Xlsx);
```

Att välja ett lämpligt filformat är avgörande när man sparar Excel-filer. `Xlsx` Formatet används flitigt och är kompatibelt med många Excel-versioner.

## Slutsats

Grattis! Du har nu programmerat kompatibilitetsinställningar för Excel-filer med Aspose.Cells för .NET. Den här handledningen beskriver varje steg, från att konfigurera din miljö till att ändra kompatibilitetsinställningar för pivottabeller. Om du någonsin har arbetat med data som krävt specifika begränsningar eller kompatibilitet är detta en färdighet du inte vill förbise.

## Vanliga frågor

### Vad är Aspose.Cells?  
Aspose.Cells är ett .NET-bibliotek utformat för att hjälpa utvecklare att skapa, manipulera och konvertera Excel-filer sömlöst.

### Varför är Excel-kompatibilitet viktig?  
Excel-kompatibilitet är avgörande för att säkerställa att filer kan öppnas och användas i avsedda versioner av Excel, särskilt om de innehåller funktioner eller format som inte stöds i tidigare versioner.

### Kan jag programmatiskt skapa pivottabeller med Aspose.Cells?  
Ja, du kan skapa och manipulera pivottabeller programmatiskt med hjälp av Aspose.Cells. Biblioteket tillhandahåller olika metoder för att lägga till datakällor, fält och funktioner som är associerade med pivottabeller.

### Hur kontrollerar jag längden på en sträng i en Excel-cell?  
Du kan använda `StringValue` egendom tillhörande en `Cell` objekt för att hämta innehållet i cellen och sedan anropa `.Length` egenskapen för att ta reda på strängens längd.

### Kan jag anpassa cellformatering utöver radhöjd och bredd?  
Absolut! Aspose.Cells tillåter omfattande cellformatering. Du kan ändra teckensnitt, färger, ramar, talformat och mycket mer genom `Style` klass.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}