---
title: Implementera Cell Formula Local liknande Range Formula Local
linktitle: Implementera Cell Formula Local liknande Range Formula Local
second_title: Aspose.Cells .NET Excel Processing API
description: Upptäck hur du implementerar en cellformel som liknar intervallformelns lokala funktionalitet i Aspose.Cells för .NET. Lär dig att anpassa inbyggda Excel-funktionsnamn och mer.
weight: 13
url: /sv/net/workbook-settings/implement-cell-formula-local-similar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Implementera Cell Formula Local liknande Range Formula Local

## Introduktion
Aspose.Cells för .NET är ett kraftfullt och flexibelt API för hantering av kalkylblad som låter dig skapa, manipulera och konvertera Excel-filer programmatiskt. En av de många funktionerna som erbjuds av Aspose.Cells är möjligheten att anpassa beteendet hos inbyggda Excel-funktioner, inklusive möjligheten att skapa dina egna lokala funktionsnamn. I den här handledningen går vi igenom stegen för att implementera en cellformel som liknar intervallformelns lokala funktionalitet i Aspose.Cells för .NET.
## Förutsättningar
Innan du börjar, se till att du har följande:
1. Microsoft Visual Studio 2010 eller senare installerat på ditt system.
2.  Den senaste versionen av Aspose.Cells for .NET-biblioteket installerad i ditt projekt. Du kan ladda ner biblioteket från[Aspose.Cells för .NET nedladdningssida](https://releases.aspose.com/cells/net/).
## Importera paket
För att komma igång måste du importera de nödvändiga paketen i ditt C#-projekt. Lägg till följande med hjälp av satser överst i din kodfil:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Steg 1: Skapa en klass för anpassade globaliseringsinställningar
 Det första steget är att skapa en anpassad`GlobalizationSettings`klass som låter dig åsidosätta standardbeteendet för Excel-funktioner. I det här exemplet kommer vi att ändra namnen på`SUM` och`AVERAGE` funktioner till`UserFormulaLocal_SUM` och`UserFormulaLocal_AVERAGE`, respektive.
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //Ändra SUM-funktionens namn enligt dina behov.
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //Ändra AVERAGE-funktionsnamnet enligt dina behov.
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## Steg 2: Skapa en ny arbetsbok och tilldela anpassade globaliseringsinställningar
 Skapa sedan en ny Workbook-instans och tilldela den anpassade`GlobalizationSettings` implementeringsklass till arbetsbokens`Settings.GlobalizationSettings` egendom.
```csharp
//Skapa arbetsbok
Workbook wb = new Workbook();
//Tilldela implementeringsklass GlobalizationSettings
wb.Settings.GlobalizationSettings = new GS();
```
## Steg 3: Öppna det första kalkylbladet och en cell
Låt oss nu komma åt det första kalkylbladet i arbetsboken och en specifik cell i det kalkylbladet.
```csharp
//Öppna första kalkylbladet
Worksheet ws = wb.Worksheets[0];
//Få tillgång till någon cell
Cell cell = ws.Cells["C4"];
```
## Steg 4: Tilldela formler och skriv ut FormulaLocal
 Slutligen, låt oss tilldela`SUM` och`AVERAGE` formler till cellen och skriv ut resultatet`FormulaLocal` värden.
```csharp
//Tilldela SUM-formel och skriv ut dess FormulaLocal
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//Tilldela AVERAGE formel och skriv ut dess FormulaLocal
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## Slutsats
 den här handledningen har du lärt dig hur du implementerar en cellformel som liknar den lokala funktionen för intervallformeln i Aspose.Cells för .NET. Genom att skapa en anpassad`GlobalizationSettings` klass, kan du åsidosätta standardbeteendet för Excel-funktioner och anpassa de lokala funktionsnamnen så att de passar dina behov. Detta kan vara särskilt användbart när du arbetar med lokaliserade eller internationaliserade Excel-dokument.
## FAQ's
###  Vad är syftet med`GlobalizationSettings` class in Aspose.Cells?
 De`GlobalizationSettings` klass i Aspose.Cells låter dig anpassa beteendet hos inbyggda Excel-funktioner, inklusive möjligheten att ändra de lokala funktionsnamnen.
###  Kan jag åsidosätta beteendet hos andra funktioner än`SUM` and `AVERAGE`?
 Ja, du kan åsidosätta beteendet för alla inbyggda Excel-funktioner genom att ändra`GetLocalFunctionName` metod i din egen`GlobalizationSettings` klass.
### Finns det något sätt att återställa funktionsnamnen till deras standardvärden?
 Ja, du kan återställa funktionsnamnen genom att antingen ta bort det anpassade`GlobalizationSettings` klass eller genom att returnera en tom sträng från`GetLocalFunctionName` metod.
### Kan jag använda den här funktionen för att skapa anpassade funktioner i Aspose.Cells?
 Nej, den`GlobalizationSettings`klass är utformad för att åsidosätta beteendet hos inbyggda Excel-funktioner, inte för att skapa anpassade funktioner. Om du behöver skapa anpassade funktioner kan du använda`UserDefinedFunction` klass i Aspose.Cells.
### Är den här funktionen tillgänglig i alla versioner av Aspose.Cells för .NET?
 Ja, den`GlobalizationSettings` klass och möjligheten att anpassa funktionsnamn finns i alla versioner av Aspose.Cells för .NET.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
