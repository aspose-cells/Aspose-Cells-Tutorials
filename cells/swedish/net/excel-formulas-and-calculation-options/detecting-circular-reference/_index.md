---
"description": "Identifiera enkelt cirkulära referenser i Excel med Aspose.Cells för .NET. Följ vår steg-för-steg-guide för att säkerställa korrekta beräkningar i dina kalkylblad."
"linktitle": "Programmatiskt identifiera cirkulär referens i Excel"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Programmatiskt identifiera cirkulär referens i Excel"
"url": "/sv/net/excel-formulas-and-calculation-options/detecting-circular-reference/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Programmatiskt identifiera cirkulär referens i Excel

## Introduktion
När det gäller att arbeta med Excel-filer är ett av de mest frustrerande problemen du kan stöta på en cirkelreferens. Detta händer när en formel refererar tillbaka till sin egen cell, antingen direkt eller indirekt, vilket skapar en loop som kan förvirra Excels beräkningsmotor. Men frukta inte! Med Aspose.Cells för .NET kan du programmatiskt upptäcka dessa irriterande cirkelreferenser och säkerställa att dina kalkylblad förblir funktionella och korrekta. I den här guiden guidar vi dig genom processen steg för steg, vilket gör det hur enkelt som helst.
## Förkunskapskrav
Innan vi dyker in i detaljerna kring att upptäcka cirkulära referenser, låt oss se till att du har allt du behöver för att komma igång:
1. Visual Studio: Se till att du har Visual Studio installerat på din dator. Detta kommer att vara din utvecklingsmiljö.
2. .NET Framework: Se till att du använder en kompatibel version av .NET Framework (minst .NET Framework 4.0).
3. Aspose.Cells-biblioteket: Du behöver ha Aspose.Cells-biblioteket. Du kan ladda ner det från [Aspose webbplats](https://releases.aspose.com/cells/net/).
4. Grundläggande kunskaper i C#: Bekantskap med C#-programmering är fördelaktigt, eftersom vi kommer att skriva kod i detta språk.
5. Excel-fil: Ha en Excel-fil redo som innehåller cirkulära referenser för testning. Du kan skapa en enkel fil eller ladda ner ett exempel.
Nu när vi har våra förutsättningar på plats, låt oss gå vidare till det roliga!
## Importera paket
Innan du kan börja koda måste du importera de nödvändiga paketen. Så här gör du:
### Skapa ett nytt projekt
- Öppna Visual Studio och skapa ett nytt C# Console Application-projekt.
### Lägg till Aspose.Cells-referens
- Högerklicka på ditt projekt i lösningsutforskaren.
- Välj "Hantera NuGet-paket".
- Sök efter “Aspose.Cells” och installera den senaste versionen.
### Importera obligatoriska namnrymder
Högst upp på din `Program.cs` fil, importera nödvändiga namnrymder:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Nu när vi har allt konfigurerat, låt oss dyka ner i koden för att upptäcka cirkulära referenser i en Excel-fil.
## Steg 1: Definiera inmatningskatalogen
Först måste du ange katalogen där din Excel-fil finns. Det är här du laddar din Excel-fil.
```csharp
// Inmatningskatalog
string sourceDir = "Your Document Directory";
```
Ersätta `"Your Document Directory"` med den faktiska sökvägen till din Excel-fil.
## Steg 2: Läs in arbetsboken med LoadOptions
Nästa steg är att ladda din Excel-arbetsbok. Det är här magin börjar!
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
Här skapar vi en ny instans av `LoadOptions` och laddar arbetsboken från den angivna sökvägen. Se till att ditt Excel-filnamn matchar!
## Steg 3: Aktivera iterationsinställningar
För att tillåta cirkulära referenser måste du aktivera iterationsinställningarna i arbetsboken.
```csharp
objWB.Settings.Iteration = true;
```
Detta anger att Aspose.Cells ska tillåta cirkulära referenser under beräkningen.
## Steg 4: Skapa beräkningsalternativ och cirkulär monitor
Nu ska vi skapa beräkningsalternativen och vår anpassade cirkulära bildskärm.
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
Här skapar vi en instans av `CalculationOptions` och en sedvänja `CircularMonitor`Denna monitor hjälper till att spåra eventuella cirkulära referenser som hittas under beräkningar.
## Steg 5: Beräkna formlerna
Nu är det dags att beräkna formlerna i din arbetsbok.
```csharp
objWB.CalculateFormula(copts);
```
Den här raden utför beräkningen och kontrollerar om det finns cirkulära referenser.
## Steg 6: Räkna cirkulära referenser
Efter beräkningen kan du räkna hur många cirkulära referenser som hittades.
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
Detta visar antalet cirkulära referenser som upptäckts i din Excel-fil.
## Steg 7: Visa resultat
Slutligen, låt oss visa resultaten och bekräfta att vår metod utfördes korrekt.
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## Steg 8: Implementera CircularMonitor-klassen
För att slutföra processen måste du implementera `CircularMonitor` klass. Denna klass kommer att ärva från `AbstractCalculationMonitor` och hantera detektering av cirkulära referenser.
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
Den här klassen samlar in detaljerna för varje hittad cirkulär referens, inklusive kalkylbladets namn och cellindex.
## Slutsats
Att identifiera cirkulära referenser i Excel med Aspose.Cells för .NET är en enkel process när du väl har uppdelat den i hanterbara steg. Genom att följa den här guiden kan du enkelt identifiera och hantera cirkulära referenser i dina kalkylblad, vilket säkerställer att dina beräkningar förblir korrekta och tillförlitliga. Oavsett om du är en erfaren utvecklare eller precis har börjat, erbjuder Aspose.Cells kraftfulla verktyg för att förbättra dina Excel-hanteringsmöjligheter. 
## Vanliga frågor
### Vad är en cirkulär referens i Excel?
En cirkulär referens uppstår när en formel refererar tillbaka till sin egen cell, vilket orsakar en oändlig loop i beräkningar.
### Hur kan jag identifiera cirkulära referenser programmatiskt?
Du kan använda Aspose.Cells-biblioteket i .NET för att programmatiskt identifiera cirkulära referenser genom att implementera en anpassad beräkningsmonitor.
### Vilka är förutsättningarna för att använda Aspose.Cells?
Du behöver Visual Studio, .NET Framework och Aspose.Cells-biblioteket installerade.
### Kan jag använda Aspose.Cells gratis?
Ja, Aspose.Cells erbjuder en gratis provperiod som du kan använda för att utforska dess funktioner.
### Var kan jag hitta mer information om Aspose.Cells?
Du kan besöka [Aspose.Cells-dokumentation](https://reference.aspose.com/cells/net/) för detaljerad information och exempel.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}