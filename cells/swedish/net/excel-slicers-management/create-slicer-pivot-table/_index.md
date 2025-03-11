---
title: Skapa Slicer för pivottabell i Aspose.Cells .NET
linktitle: Skapa Slicer för pivottabell i Aspose.Cells .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du skapar en slicer för pivottabeller i Aspose.Cells .NET med vår steg-för-steg-guide. Förbättra dina Excel-rapporter.
weight: 12
url: /sv/net/excel-slicers-management/create-slicer-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Slicer för pivottabell i Aspose.Cells .NET

## Introduktion
dagens datadrivna värld är pivottabeller ovärderliga för att analysera och sammanfatta stora datamängder. Men varför stanna vid enbart sammanfattning när du kan göra dina pivottabeller mer interaktiva? Gå in i en värld av skärmaskiner! De är som fjärrkontrollen för dina Excel-rapporter, vilket ger dig möjlighet att filtrera data snabbt och enkelt. I den här guiden går vi igenom hur man skapar en slicer för en pivottabell med Aspose.Cells för .NET. Så ta den där koppen kaffe, slå dig ner och låt oss dyka in!
## Förutsättningar
Innan du sätter igång finns det några förutsättningar du måste tänka på:
1.  Aspose.Cells för .NET: Se till att du har Aspose.Cells installerat i ditt projekt. Du kan få det från[nedladdningssida](https://releases.aspose.com/cells/net/).
2. Visual Studio eller en annan IDE: Du behöver en IDE där du kan skapa och köra dina .NET-projekt. Visual Studio är ett populärt val.
3. Grundläggande kunskaper om C#: Att kunna lite C# hjälper dig att smidigt navigera i kodningsdelarna.
4. Exempel på Excel-fil: För den här handledningen behöver du ett exempel på en Excel-fil som innehåller en pivottabell. Vi kommer att använda en fil som heter`sampleCreateSlicerToPivotTable.xlsx`.
Nu när du har markerat alla dessa rutor, låt oss importera de nödvändiga paketen!
## Importera paket
För att använda Aspose.Cells effektivt måste du importera följande paket i ditt projekt:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Se till att du lägger till detta överst i din kodfil. Denna importsats ger dig tillgång till alla funktioner som erbjuds av Aspose.Cells-biblioteket.
Nu, låt oss komma in på det nitty-gritty. Vi delar upp detta i hanterbara steg, så att du enkelt kan följa med. 
## Steg 1: Definiera käll- och utdatakataloger
Först och främst måste vi definiera var dina in- och utdatafiler finns. Detta säkerställer att vår kod vet var vi kan hitta vår Excel-fil och var resultaten ska sparas.
```csharp
// Källkatalog
string sourceDir = "Your Document Directory"; // Ange sökvägen till din källkatalog
// Utdatakatalog
string outputDir = "Your Document Directory"; // Ange sökvägen till din utdatakatalog
```
 Förklaring: I det här steget deklarerar du helt enkelt variabler för käll- och utdatakatalogerna. Ersätta`"Your Document Directory"`med den faktiska katalogen där dina filer finns.
## Steg 2: Ladda arbetsboken
Därefter ska vi ladda Excel-arbetsboken som innehåller pivottabellen. 
```csharp
// Ladda exempel på Excel-fil som innehåller pivottabell.
Workbook wb = new Workbook(sourceDir + "sampleCreateSlicerToPivotTable.xlsx");
```
 Förklaring: Här skapar vi en instans av`Workbook` klass och passerar sökvägen till Excel-filen. Denna kodrad tillåter oss att komma åt och manipulera arbetsboken.
## Steg 3: Öppna det första arbetsbladet
Nu när vi har arbetsboken laddad måste vi komma åt kalkylbladet där vår pivottabell finns.
```csharp
// Öppna första kalkylbladet.
Worksheet ws = wb.Worksheets[0];
```
Förklaring: Kalkylblad i Aspose.Cells är nollindexerade, vilket betyder att det första bladet är på index 0. Med den här raden får vi vårt kalkylbladsobjekt för vidare manipulation.
## Steg 4: Gå till pivottabellen
Vi närmar oss! Låt oss ta tag i pivottabellen som vi vill att skivaren ska associeras med.
```csharp
// Få åtkomst till den första pivottabellen i kalkylbladet.
Aspose.Cells.Pivot.PivotTable pt = ws.PivotTables[0];
```
Förklaring: I likhet med kalkylblad indexeras även pivottabeller. Den här raden drar den första pivottabellen från kalkylbladet så att vi kan lägga till vår skivare till den.
## Steg 5: Lägg till en skivare
Nu kommer den spännande delen – att lägga till skivaren! Detta steg binder skivaren till vårt pivottabellbasfält.
```csharp
// Lägg till slicer relaterad till pivottabellen med det första basfältet i cell B22.
int idx = ws.Slicers.Add(pt, "B22", pt.BaseFields[0]);
```
 Förklaring: Här lägger vi till skivaren och anger positionen (cell B22) och basfältet från pivottabellen (den första). Metoden returnerar ett index, som vi lagrar i`idx` för framtida referens.
## Steg 6: Gå till den nyligen tillagda skivaren
När skivaren har skapats är det bra att ha en referens till den, särskilt om du vill göra ytterligare ändringar senare.
```csharp
// Få tillgång till den nyligen tillagda skivaren från skivsamlingen.
Aspose.Cells.Slicers.Slicer slicer = ws.Slicers[idx];
```
Förklaring: Med indexet för den nyskapade slicern kan vi nu komma åt den direkt från slicer-samlingen i kalkylbladet.
## Steg 7: Spara arbetsboken
Äntligen är det dags att spara ditt hårda arbete! Du kan spara arbetsboken i olika format.
```csharp
// Spara arbetsboken i utdata XLSX-format.
wb.Save(outputDir + "outputCreateSlicerToPivotTable.xlsx", SaveFormat.Xlsx);
// Spara arbetsboken i output XLSB-format.
wb.Save(outputDir + "outputCreateSlicerToPivotTable.xlsb", SaveFormat.Xlsb);
```
Förklaring: I det här steget sparar vi arbetsboken i både XLSX- och XLSB-format. Detta ger dig alternativ beroende på dina behov.
## Steg 8: Kör koden
Som grädde på moset, låt oss låta användaren veta att allt har utförts framgångsrikt!
```csharp
Console.WriteLine("CreateSlicerToPivotTable executed successfully.");
```
Förklaring: Ett enkelt konsolmeddelande för att försäkra användaren om att allt har slutförts utan fel.
## Slutsats
Och där har du det! Du har framgångsrikt skapat en slicer för en pivottabell med Aspose.Cells för .NET. Denna lilla funktion kan avsevärt öka interaktiviteten i dina Excel-rapporter, vilket gör dem användarvänliga och visuellt tilltalande.
Om du har följt med bör du hitta på att skapa och manipulera pivottabeller med skärmaskiner en promenad i parken nu. Tyckte du om den här handledningen? Jag hoppas att det väckte ditt intresse för att ytterligare utforska funktionerna hos Aspose.Cells!
## FAQ's
### Vad är en slicer i Excel?
En slicer är ett visuellt filter som låter användare snabbt filtrera data från en pivottabell.
### Kan jag lägga till flera skivare till en pivottabell?
Ja, du kan lägga till så många skärare som du behöver i en pivottabell för olika fält.
### Är Aspose.Cells gratis att använda?
Aspose.Cells är ett betalbibliotek, men du kan prova det gratis under provperioden.
### Var kan jag hitta mer Aspose.Cells-dokumentation?
 Du kan kontrollera[Aspose.Cells dokumentation](https://reference.aspose.com/cells/net/) för mer information.
### Finns det något sätt att få support för Aspose.Cells?
 Absolut! Du kan nå ut för att få stöd på[Asposes forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
