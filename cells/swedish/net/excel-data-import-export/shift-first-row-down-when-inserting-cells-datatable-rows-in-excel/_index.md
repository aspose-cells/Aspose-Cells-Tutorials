---
title: Flytta första raden nedåt när du infogar datatabellrader i Excel
linktitle: Flytta första raden nedåt när du infogar datatabellrader i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig att infoga DataTable-rader i Excel utan att flytta den första raden nedåt med Aspose.Cells för .NET. Steg-för-steg-guide för enkel automatisering.
weight: 11
url: /sv/net/excel-data-import-export/shift-first-row-down-when-inserting-cells-datatable-rows-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Flytta första raden nedåt när du infogar datatabellrader i Excel

## Introduktion

Är du trött på att manuellt flytta rader när du infogar ny data i dina Excel-kalkylblad? Tja, du har tur! I den här artikeln kommer vi att dyka in i hur man automatiserar denna process med Aspose.Cells för .NET. I slutet av den här handledningen kommer du inte bara att lära dig hur du arbetar med datatabeller i Excel utan också hur du anpassar importalternativen så att de bättre passar dina behov. Lita på mig; detta kan spara mycket tid och krångel! Så ta en kopp kaffe, så sätter vi igång!

## Förutsättningar

Innan vi går in i kodningen, låt oss se till att du har allt inställt:

1. Visual Studio: Se till att du har Visual Studio installerat (2017 eller senare borde fungera bra).
2.  Aspose.Cells för .NET: Du måste ha Aspose.Cells-biblioteket. Om du inte har gjort det ännu kan du ladda ner det[här](https://releases.aspose.com/cells/net/).
3. Grundläggande förståelse för C# och Excel: En grundläggande förståelse för C#-programmering och hur Excel fungerar kommer säkert att hjälpa dig att följa med mer effektivt.

 Du vill också ha ett exempel på en Excel-fil till hands. I den här guiden använder vi ett exempel som heter`sampleImportTableOptionsShiftFirstRowDown.xlsx`. Du kan skapa den här filen eller hitta en mall som passar dina behov.

## Importera paket

Innan vi dyker in i kodning måste vi se till att vi importerar de nödvändiga paketen. Inkludera följande namnrymder i ditt C#-projekt:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Dessa paket är viktiga för att arbeta med arbetsboken, kalkylbladet och tabellerna.

## Steg 1: Konfigurera ditt projekt

### Skapa ett nytt C#-projekt

Börja med att skapa en ny C# Console Application i Visual Studio. Ge ditt projekt ett passande namn, som "ExcelDataImport".

### Lägg till Aspose.Cells NuGet-paket

För att lägga till Aspose.Cells-paketet, högerklicka på ditt projekt i Solution Explorer, välj Hantera NuGet-paket och sök efter "Aspose.Cells". Installera paketet för att se till att du kan komma åt alla funktioner vi behöver.

## Steg 2: Definiera datatabellen

 Därefter kommer vi att implementera`ICellsDataTable` gränssnitt för att skapa en klass som tillhandahåller data som ska importeras. Så här kan du strukturera`CellsDataTable` klass:

```csharp
class CellsDataTable : ICellsDataTable
{
    int m_index = -1;
    static String[] colsNames = new String[] { "Pet", "Fruit", "Country", "Color" };
    static String[] col0data = new String[] { "Dog", "Cat", "Duck" };
    static String[] col1data = new String[] { "Apple", "Pear", "Banana" };
    static String[] col2data = new String[] { "UK", "USA", "China" };
    static String[] col3data = new String[] { "Red", "Green", "Blue" };
    static String[][] colsData = new String[][] { col0data, col1data, col2data, col3data };
    
    // ... Implementera andra medlemmar ...
}
```

Här definierar vi kolumnnamnen och data för varje kolumn, vilket kommer att underlätta strukturen för vår importerade tabell.

## Steg 3: Implementera ICellsDataTable-gränssnittsmedlemmar

 Inom`CellsDataTable` klass, måste du implementera medlemmarna i`ICellsDataTable` gränssnitt. Här är den nödvändiga implementeringen:

```csharp
public object this[string columnName]
{
    get
    {
        throw new NotImplementedException();
    }
}

object ICellsDataTable.this[int columnIndex]
{
    get
    {
        return colsData[columnIndex][m_index];
    }
}

string[] ICellsDataTable.Columns
{
    get { return colsNames; }
}

int ICellsDataTable.Count
{
    get { return col0data.Length; }
}

void ICellsDataTable.BeforeFirst()
{
    m_index = -1;
}

bool ICellsDataTable.Next()
{
    m_index++;
    return (m_index < Count);
}
```

Den här delen av klassen hanterar datahämtning, definierar hur många rader och kolumner det finns och hanterar det aktuella indextillståndet.

## Steg 4: Skriv huvudfunktionen

 Låt oss nu skapa`Run`metod för att orkestrera hela tabellimportprocessen:

```csharp
public static void Run()
{
    string sourceDir = "Your Document Directory\\";
    string outputDir = "Your Document Directory\\";
    
    CellsDataTable cellsDataTable = new CellsDataTable();
    Workbook wb = new Workbook(sourceDir + "sampleImportTableOptionsShiftFirstRowDown.xlsx");
    Worksheet ws = wb.Worksheets[0];
```

## Steg 5: Ställ in importalternativ

 För att kontrollera importbeteendet bör du skapa en instans av`ImportTableOptions` och ställ in egenskaperna därefter. Specifikt vill vi ställa in`ShiftFirstRowDown` till`false`.

```csharp
    ImportTableOptions opts = new ImportTableOptions();
    opts.ShiftFirstRowDown = false; // Vi vill inte flytta ned den första raden
```

## Steg 6: Importera datatabellen

 Nu kan vi importera data från vår`CellsDataTable` i arbetsbladet.

```csharp
    ws.Cells.ImportData(cellsDataTable, 2, 2, opts);
}
```

Detta kommando infogar din datatabell direkt med början på den angivna raden och kolumnen.

## Steg 7: Spara arbetsboken

Slutligen kommer vi att spara den modifierade arbetsboken tillbaka till en fil:

```csharp
    wb.Save(outputDir + "outputImportTableOptionsShiftFirstRowDown-False.xlsx");
}
```

## Slutsats

Och där har du det! Du har lärt dig hur du infogar DataTable-rader i ett Excel-ark utan att flytta den första raden med Aspose.Cells för .NET. Denna process effektiviserar inte bara datamanipulation i Excel utan förbättrar också din applikations prestanda genom att automatisera en typiskt besvärlig uppgift. Med denna kunskap i din verktygslåda är du bättre rustad att hantera Excel-automationsuppgifter, vilket sparar tid och ansträngning.

## FAQ's

### Vad är Aspose.Cells för .NET?
Aspose.Cells för .NET är ett programmeringsbibliotek som låter utvecklare skapa, manipulera och konvertera Excel-filer i .NET-applikationer.

### Behöver jag en licens för att använda Aspose.Cells?
Ja, du behöver en giltig licens för alla funktioner. En gratis provperiod är dock tillgänglig för första testning.

### Kan jag använda Aspose.Cells i webbapplikationer?
Absolut! Aspose.Cells är perfekt för skrivbords-, webb- och molnbaserade applikationer utvecklade i .NET.

### Vilka typer av Excel-filer kan jag skapa med Aspose.Cells?
Du kan skapa en mängd olika Excel-filformat, inklusive XLSX, XLS, CSV och mer.

### Var kan jag få support för Aspose.Cells?
 Du kan ställa frågor eller få hjälp i[Aspose forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
