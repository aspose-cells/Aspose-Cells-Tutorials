---
"description": "Upptäck hur du implementerar en cellformel som liknar den lokala funktionen för intervallformeln i Aspose.Cells för .NET. Lär dig att anpassa inbyggda Excel-funktionsnamn och mer."
"linktitle": "Implementera cellformel lokalt på liknande sätt som områdesformel lokalt"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Implementera cellformel lokalt på liknande sätt som områdesformel lokalt"
"url": "/sv/net/workbook-settings/implement-cell-formula-local-similar/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Implementera cellformel lokalt på liknande sätt som områdesformel lokalt

## Introduktion
Aspose.Cells för .NET är ett kraftfullt och flexibelt API för kalkylbladsmanipulation som låter dig programmatiskt skapa, manipulera och konvertera Excel-filer. En av de många funktioner som erbjuds av Aspose.Cells är möjligheten att anpassa beteendet hos inbyggda Excel-funktioner, inklusive möjligheten att skapa dina egna lokala funktionsnamn. I den här handledningen guidar vi dig genom stegen för att implementera en cellformel som liknar den lokala funktionen för intervallformeln i Aspose.Cells för .NET.
## Förkunskapskrav
Innan du börjar, se till att du har följande:
1. Microsoft Visual Studio 2010 eller senare installerat på ditt system.
2. Den senaste versionen av Aspose.Cells för .NET-biblioteket installerat i ditt projekt. Du kan ladda ner biblioteket från [Nedladdningssida för Aspose.Cells för .NET](https://releases.aspose.com/cells/net/).
## Importera paket
För att komma igång måste du importera de nödvändiga paketen i ditt C#-projekt. Lägg till följande using-satser högst upp i din kodfil:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Steg 1: Skapa en anpassad globaliseringsklass
Det första steget är att skapa en anpassad `GlobalizationSettings` klass som låter dig åsidosätta standardbeteendet för Excel-funktioner. I det här exemplet kommer vi att ändra namnen på `SUM` och `AVERAGE` funktioner till `UserFormulaLocal_SUM` och `UserFormulaLocal_AVERAGE`respektive.
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //Ändra namnet på SUM-funktionen efter behov.
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //Ändra namnet på AVERAGE-funktionen efter behov.
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## Steg 2: Skapa en ny arbetsbok och tilldela anpassade globaliseringsinställningar
Skapa sedan en ny arbetsboksinstans och tilldela den anpassade `GlobalizationSettings` implementeringsklassen till arbetsbokens `Settings.GlobalizationSettings` egendom.
```csharp
//Skapa arbetsbok
Workbook wb = new Workbook();
//Tilldela implementeringsklass för GlobalizationSettings
wb.Settings.GlobalizationSettings = new GS();
```
## Steg 3: Få åtkomst till det första arbetsbladet och en cell
Nu ska vi komma åt det första kalkylbladet i arbetsboken och en specifik cell i det kalkylbladet.
```csharp
//Åtkomst till första kalkylbladet
Worksheet ws = wb.Worksheets[0];
//Åtkomst till vissa celler
Cell cell = ws.Cells["C4"];
```
## Steg 4: Tilldela formler och skriv ut FormulaLocal
Slutligen, låt oss tilldela `SUM` och `AVERAGE` formler till cellen och skriv ut resultatet `FormulaLocal` värden.
```csharp
//Tilldela SUM-formeln och skriv ut dess FormulaLocal
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//Tilldela AVERAGE-formeln och skriv ut dess FormulaLocal
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## Slutsats
I den här handledningen har du lärt dig hur du implementerar en cellformel som liknar den lokala funktionen för intervallformeln i Aspose.Cells för .NET. Genom att skapa en anpassad `GlobalizationSettings` I klassen kan du åsidosätta standardbeteendet för Excel-funktioner och anpassa de lokala funktionsnamnen efter dina behov. Detta kan vara särskilt användbart när du arbetar med lokaliserade eller internationaliserade Excel-dokument.
## Vanliga frågor
### Vad är syftet med `GlobalizationSettings` klass i Aspose.Cells?
De `GlobalizationSettings` Med klassen Aspose.Cells kan du anpassa beteendet hos inbyggda Excel-funktioner, inklusive möjligheten att ändra de lokala funktionsnamnen.
### Kan jag åsidosätta beteendet hos andra funktioner än `SUM` och `AVERAGE`?
Ja, du kan åsidosätta beteendet hos alla inbyggda Excel-funktioner genom att ändra `GetLocalFunctionName` metod i din egen `GlobalizationSettings` klass.
### Finns det något sätt att återställa funktionsnamnen till deras standardvärden?
Ja, du kan återställa funktionsnamnen genom att antingen ta bort den anpassade `GlobalizationSettings` klassen eller genom att returnera en tom sträng från `GetLocalFunctionName` metod.
### Kan jag använda den här funktionen för att skapa anpassade funktioner i Aspose.Cells?
Nej, den `GlobalizationSettings` Klassen är utformad för att åsidosätta beteendet hos inbyggda Excel-funktioner, inte för att skapa anpassade funktioner. Om du behöver skapa anpassade funktioner kan du använda `UserDefinedFunction` klassen i Aspose.Cells.
### Är den här funktionen tillgänglig i alla versioner av Aspose.Cells för .NET?
Ja, den `GlobalizationSettings` klassen och möjligheten att anpassa funktionsnamn finns i alla versioner av Aspose.Cells för .NET.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}