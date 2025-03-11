---
title: Sortera data i en kolumn med anpassad sorteringslista i Excel
linktitle: Sortera data i en kolumn med anpassad sorteringslista i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du sorterar data i Excel med hjälp av en anpassad sorteringslista med Aspose.Cells för .NET i den här omfattande självstudien.
weight: 10
url: /sv/net/excel-data-sorting-exporting/sort-data-in-a-column-with-custom-sort-list-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sortera data i en kolumn med anpassad sorteringslista i Excel

## Introduktion

Denna handledning guidar dig genom processen att ställa in ditt projekt, ladda en Excel-fil och sortera data inom ett specificerat intervall med hjälp av en anpassad sorteringsordning. Genom att följa den här guiden får du praktisk erfarenhet som kan förbättra dina datahanteringsfärdigheter och användbarheten av Aspose.Cells-biblioteket.

## Förutsättningar

Innan vi dyker in i handledningen, låt oss skissera några förutsättningar för att säkerställa en smidig inlärningsupplevelse.

### Grundläggande kunskaper i C#

Även om handledningen är utformad för att guida dig genom varje steg, kommer en grundläggande förståelse av C# att göra det lättare att förstå de presenterade koncepten.

### .NET utvecklingsmiljö

Se till att du har en fungerande .NET-utvecklingsmiljö inställd. Du kan använda Visual Studio eller någon annan IDE som stöder .NET-utveckling.

### Aspose.Cells för .NET NuGet-paket

Du behöver Aspose.Cells-biblioteket för .NET installerat i ditt projekt. Du kan enkelt lägga till den via NuGet Package Manager. 

Så här gör du:

1. Öppna ditt projekt i Visual Studio.
2. Gå till "Verktyg" > "NuGet Package Manager" > "Manage NuGet Packages for Solution".
3.  Leta efter`Aspose.Cells` och installera den senaste versionen.

### Grundläggande Excel-fil för testning

Du behöver ett exempel på Excel-fil att arbeta med. Du kan skapa en enkel Excel-fil med slumpmässiga landsnamn och deras koder.

## Importera paket

För att komma igång, låt oss importera de nödvändiga paketen till ditt projekt. Här är ett utdrag av hur du ställer in din kod:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Med paketen importerade är vi redo att gå vidare.

## Steg 1: Definiera käll- och utdatakatalogerna 

Det första steget är att definiera var din indatafil finns och var du vill att utdata (sorterad fil) ska sparas. Du måste ange två sökvägar: en för Excel-källfilen och en annan för att spara utdata efter sortering.

```csharp
string sourceDir = "Your Document Directory\\";
string outputDir = "Your Document Directory\\";
```

## Steg 2: Ladda källfilen för Excel

Därefter laddar vi Excel-filen som innehåller de data du vill sortera. Detta görs genom att skapa en instans av`Workbook` klass och skickar sökvägen till din källfil.

```csharp
Workbook wb = new Workbook(sourceDir + "sampleSortData_CustomSortList.xlsx");
```

## Steg 3: Öppna det första arbetsbladet 

När filen har laddats måste vi komma åt det specifika kalkylbladet som innehåller de data vi tänker sortera. I det här fallet riktar vi oss mot det första kalkylbladet.

```csharp
Worksheet ws = wb.Worksheets[0];
```

## Steg 4: Ange cellområdet som ska sorteras

 Vi måste bestämma intervallet av celler som vi ska sortera. I det här exemplet kommer vi att sortera cellerna från A1 till A40. Använd`CellArea.CreateCellArea` metod för att definiera cellarean.

```csharp
CellArea ca = CellArea.CreateCellArea("A1", "A40");
```

## Steg 5: Skapa en anpassad sorteringslista

Innan vi sorterar måste vi fastställa kriterierna vi kommer att använda för vår anpassade sortering. Du kan definiera en sorteringslista som en array av strängar. Den anpassade sorteringslistan kommer att diktera sorteringsordningen.

```csharp
string[] customSortList = new string[] { "USA,US", "Brazil,BR", "China,CN", "Russia,RU", "Canada,CA" };
```

## Steg 6: Lägg till sorteringsnyckel och utför sorteringen

Nu är det dags att sortera! Vi kommer att använda klassen DataSorter för detta. Skapa en nyckel för sortering baserat på vår anpassade lista och utför sorteringsoperationen.

```csharp
wb.DataSorter.AddKey(0, SortOrder.Ascending, customSortList);
wb.DataSorter.Sort(ws.Cells, ca);
```

## Steg 7: Spara Excel-filen

När sorteringen är klar är det sista steget att spara ändringarna i en ny Excel-fil. Ange utdatafilens namn och spara arbetsboken.

```csharp
wb.Save(outputDir + "outputSortData_CustomSortList.xlsx");
```

## Steg 8: Bekräfta framgångsrik exekvering

För att säkerställa att allt har fungerat smidigt kan du skriva ut ett bekräftelsemeddelande till konsolen. Detta hjälper till att felsöka och ger dig tillfredsställelse att operationen lyckades.

```csharp
Console.WriteLine("SortDataInColumnWithCustomSortList executed successfully.\r\n");
```

## Slutsats

Och där har du det! Du har framgångsrikt sorterat data i en Excel-kolumn med hjälp av en anpassad sorteringslista med Aspose.Cells för .NET. Sortering hjälper till att ge din data struktur och klarhet, vilket gör det lättare att analysera och tolka. Jag hoppas att den här guiden tar dina kunskaper till nästa nivå och hjälper dig att inse hur kraftfull Aspose.Cells kan vara för dina Excel-relaterade uppgifter.

## FAQ's

### Vad är Aspose.Cells för .NET?
Aspose.Cells för .NET är ett omfattande bibliotek som låter dig manipulera Excel-filer i .NET-applikationer, inklusive skapa, redigera och konvertera dem.

### Kan jag sortera mer än en kolumn med hjälp av en anpassad sorteringslista?
Ja! Du kan lägga till ytterligare nycklar för att sortera efter flera kolumner om det behövs, följ bara samma procedur för varje nyckel.

### Behöver jag förkunskaper i C# för att använda Aspose.Cells?
Även om det är användbart kan du följa med i den här handledningen och lära dig allt eftersom! Att ha en viss grundläggande förståelse för C# kommer att förbättra din inlärningsupplevelse.

### Är det möjligt att använda en tillfällig licens för Aspose.Cells?
Absolut! Du kan skaffa en tillfällig licens om du vill testa alla funktioner i biblioteket utan begränsningar.

### Kan jag ladda ner exempel eller dokumentation för Aspose.Cells?
 Ja! Aspose tillhandahåller omfattande dokumentation och exempel på projekt som kan hjälpa dig. Kolla in[Aspose.Cells dokumentation](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
