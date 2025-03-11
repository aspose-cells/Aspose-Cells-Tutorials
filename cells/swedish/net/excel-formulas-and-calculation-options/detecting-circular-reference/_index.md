---
title: Upptäck cirkulär referens i Excel programmatiskt
linktitle: Upptäck cirkulär referens i Excel programmatiskt
second_title: Aspose.Cells .NET Excel Processing API
description: Upptäck enkelt cirkulära referenser i Excel med Aspose.Cells för .NET. Följ vår steg-för-steg-guide för att säkerställa korrekta beräkningar i dina kalkylblad.
weight: 13
url: /sv/net/excel-formulas-and-calculation-options/detecting-circular-reference/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Upptäck cirkulär referens i Excel programmatiskt

## Introduktion
När det gäller att arbeta med Excel-filer är ett av de mest frustrerande problemen du kan stöta på en cirkulär referens. Detta händer när en formel refererar tillbaka till sin egen cell, antingen direkt eller indirekt, och skapar en loop som kan förvirra Excels beräkningsmotor. Men frukta inte! Med Aspose.Cells för .NET kan du programmatiskt upptäcka dessa irriterande cirkulära referenser, vilket säkerställer att dina kalkylblad förblir funktionella och korrekta. I den här guiden går vi igenom processen steg för steg, vilket gör det så enkelt som en plätt.
## Förutsättningar
Innan vi dyker in i det tråkiga med att upptäcka cirkulära referenser, låt oss se till att du har allt du behöver för att komma igång:
1. Visual Studio: Se till att du har Visual Studio installerat på din dator. Detta kommer att vara din utvecklingsmiljö.
2. .NET Framework: Se till att du använder en kompatibel version av .NET Framework (minst .NET Framework 4.0).
3.  Aspose.Cells Library: Du måste ha Aspose.Cells-biblioteket. Du kan ladda ner den från[Aspose hemsida](https://releases.aspose.com/cells/net/).
4. Grundläggande kunskaper i C#: Bekantskap med C#-programmering kommer att vara fördelaktigt, eftersom vi kommer att skriva kod på detta språk.
5. Excel-fil: Ha en Excel-fil redo som innehåller cirkulära referenser för testning. Du kan skapa en enkel eller ladda ner ett prov.
Nu när vi har våra förutsättningar på plats, låt oss gå vidare till det roliga!
## Importera paket
Innan du kan börja koda måste du importera de nödvändiga paketen. Så här gör du:
### Skapa ett nytt projekt
- Öppna Visual Studio och skapa ett nytt C# Console Application-projekt.
### Lägg till Aspose.Cells Reference
- Högerklicka på ditt projekt i Solution Explorer.
- Välj "Hantera NuGet-paket."
- Sök efter "Aspose.Cells" och installera den senaste versionen.
### Importera nödvändiga namnområden
 Överst på din`Program.cs` fil, importera de nödvändiga namnrymden:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Nu när vi har allt inställt, låt oss dyka in i koden för att upptäcka cirkulära referenser i en Excel-fil.
## Steg 1: Definiera indatakatalogen
Först måste du ange katalogen där din Excel-fil finns. Det är här du ska ladda din Excel-fil.
```csharp
// Inmatningskatalog
string sourceDir = "Your Document Directory";
```
 Ersätta`"Your Document Directory"` med den faktiska sökvägen till din Excel-fil.
## Steg 2: Ladda arbetsboken med LoadOptions
Därefter ska du ladda din Excel-arbetsbok. Det är här magin börjar!
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
 Här skapar vi en ny instans av`LoadOptions` och laddar arbetsboken från den angivna sökvägen. Se till att ditt Excel-filnamn matchar!
## Steg 3: Aktivera Iterationsinställningar
För att tillåta cirkulära referenser måste du aktivera iterationsinställningarna i arbetsboken.
```csharp
objWB.Settings.Iteration = true;
```
Detta säger till Aspose.Cells att tillåta cirkulära referenser under beräkningen.
## Steg 4: Skapa beräkningsalternativ och cirkulär monitor
Låt oss nu skapa beräkningsalternativen och vår anpassade cirkulära monitor.
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
 Här skapar vi en instans av`CalculationOptions` och en sed`CircularMonitor`Denna monitor hjälper till att spåra alla cirkulära referenser som hittas under beräkningar.
## Steg 5: Beräkna formlerna
Nu är det dags att beräkna formlerna i din arbetsbok.
```csharp
objWB.CalculateFormula(copts);
```
Denna rad utför beräkningen och kontrollerar om det finns cirkulära referenser.
## Steg 6: Räkna cirkulära referenser
Efter beräkningen kan du räkna hur många cirkulära referenser som hittades.
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
Detta kommer att mata ut antalet cirkulära referenser som upptäckts i din Excel-fil.
## Steg 7: Visa resultat
Slutligen, låt oss visa resultaten och bekräfta att vår metod kördes framgångsrikt.
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## Steg 8: Implementera CircularMonitor-klassen
 För att slutföra processen måste du implementera`CircularMonitor` klass. Denna klass kommer att ärva från`AbstractCalculationMonitor` och hantera detektering av cirkulära referenser.
```csharp
public class CircularMonitor : AbstractCalculationMonitor
{
    public ArrayList circulars = new ArrayList();
    public ArrayList Circulars { get { return circulars; } }
    public override bool OnCircular(IEnumerator circularCellsData)
    {
        CalculationCell cc = null;
        ArrayList cur = new ArrayList();
        while (circularCellsData.MoveNext())
        {
            cc = (CalculationCell)circularCellsData.Current;
            cur.Add(cc.Worksheet.Name + "!" + CellsHelper.CellIndexToName(cc.CellRow, cc.CellColumn));
        }
        circulars.Add(cur);
        return true;
    }
}
```
Den här klassen fångar informationen om varje cirkulär referens som hittas, inklusive kalkylbladets namn och cellindex.
## Slutsats
Att upptäcka cirkulära referenser i Excel med Aspose.Cells för .NET är en enkel process när du delar upp den i hanterbara steg. Genom att följa den här guiden kan du enkelt identifiera och hantera cirkulära referenser i dina kalkylblad, vilket säkerställer att dina beräkningar förblir korrekta och tillförlitliga. Oavsett om du är en erfaren utvecklare eller precis har börjat, erbjuder Aspose.Cells kraftfulla verktyg för att förbättra dina Excel-manipulationsmöjligheter. 
## FAQ's
### Vad är en cirkulär referens i Excel?
En cirkulär referens uppstår när en formel hänvisar tillbaka till sin egen cell, vilket orsakar en oändlig loop i beräkningar.
### Hur kan jag upptäcka cirkulära referenser programmatiskt?
Du kan använda Aspose.Cells-biblioteket i .NET för att programmatiskt upptäcka cirkulära referenser genom att implementera en anpassad beräkningsmonitor.
### Vilka är förutsättningarna för att använda Aspose.Cells?
Du behöver Visual Studio, .NET Framework och Aspose.Cells-biblioteket installerade.
### Kan jag använda Aspose.Cells gratis?
Ja, Aspose.Cells erbjuder en gratis provperiod som du kan använda för att utforska dess funktioner.
### Var kan jag hitta mer information om Aspose.Cells?
 Du kan besöka[Aspose.Cells dokumentation](https://reference.aspose.com/cells/net/) för detaljerad information och exempel.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
