---
title: Lägg till Arc till kalkylblad i Excel
linktitle: Lägg till Arc till kalkylblad i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig att lägga till bågar till Excel-kalkylblad med Aspose.Cells för .NET. Följ vår steg-för-steg-guide för att förbättra dina kalkylbladsdesigner.
weight: 16
url: /sv/net/excel-shapes-controls/add-arc-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till Arc till kalkylblad i Excel

## Introduktion
Att skapa visuellt tilltalande Excel-kalkylblad är avgörande för datapresentation, och Aspose.Cells-biblioteket förser utvecklare med robusta verktyg för att utföra denna uppgift. En intressant funktion som du kanske vill infoga i dina Excel-dokument är möjligheten att lägga till former, till exempel bågar. I den här handledningen går vi igenom steg-för-steg hur du lägger till bågar i ett Excel-kalkylblad med Aspose.Cells för .NET. I slutet av den här artikeln kommer du inte bara att lära dig hur du lägger till bågar utan också få insikt i hur du hanterar former i allmänhet.
## Förutsättningar
Innan vi dyker in i krångligheterna med att lägga till bågar i ditt kalkylblad är det viktigt att se till att du har några saker på plats. Här är förutsättningarna du behöver för att komma igång:
1. Visual Studio: Du måste ha Visual Studio installerat på din dator eftersom vi kommer att använda C# som vårt programmeringsspråk.
2. .NET Framework: Se till att du har .NET Framework eller .NET Core installerat. Aspose.Cells stöder båda.
3. Aspose.Cells för .NET: Du måste ha Aspose.Cells-biblioteket. Du kan ladda ner den från[Aspose.Cells Nedladdningar](https://releases.aspose.com/cells/net/) sida.
4. Grundläggande förståelse för C#: Bekantskap med C# hjälper dig att följa med i kodavsnitten utan mycket krångel.
## Importera paket
För att börja arbeta med Aspose.Cells i ditt projekt måste du importera de nödvändiga paketen. Så här gör du:
### Skapa ett nytt projekt
- Öppna Visual Studio.
- Välj "Skapa ett nytt projekt."
- Välj en mall som fungerar med .NET (som Console Application).
  
### Lägg till Aspose.Cells-referenser
- Högerklicka på ditt projekt i Solution Explorer.
- Välj "Hantera NuGet-paket."
- Sök efter "Aspose.Cells" och installera den.
Nu är du redo att börja koda bågtillägget.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Här är en steg-för-steg-uppdelning av koden som visar hur man lägger till bågar till ett kalkylblad i Excel.
## Steg 1: Konfigurera katalogen
Det första steget är att skapa en katalog där du ska spara din Excel-fil. Detta hjälper till att hantera dina utdatafiler enkelt.
```csharp
string dataDir = "Your Document Directory";
// Skapa katalog om den inte redan finns.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
I det här kodavsnittet anger vi sökvägen till dokumentkatalogen. Vi kontrollerar även om katalogen finns; om inte, skapar vi det. Detta lägger grunden för vår produktion.
## Steg 2: Instantiera en arbetsbok
Låt oss sedan skapa en ny arbetsboksinstans.
```csharp
// Instantiera en ny arbetsbok.
Workbook excelbook = new Workbook();
```
Den här raden skapar en ny Excel-arbetsbok. Se det här som en tom duk där vi kan lägga till former, data och mer.
## Steg 3: Lägg till den första bågformen
Låt oss nu lägga till vår första bågform till kalkylbladet.
```csharp
// Lägg till en bågeform.
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
 Här lägger vi till en båge till det första kalkylbladet. Parametrarna definierar bågens position och storlek:`(left, top, width, height, startAngle, endAngle)`. Det är som att rita ett segment av en cirkel!
## Steg 4: Anpassa den första bågen
När du har lagt till bågen kanske du vill anpassa dess utseende.
```csharp
// Ställ in fyllningsformens färg
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
// Ställ in placeringen av bågen.
arc1.Placement = PlacementType.FreeFloating;           
// Ställ in linjevikten.
arc1.Line.Weight = 1;      
// Ställ in streckstilen för bågen.
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
I det här avsnittet anpassar vi bågen. Vi ställer in dess fyllningstyp till enfärgad (blå i det här fallet), definierar hur den ska placeras, fastställer linjevikten och väljer en streckstil. I grund och botten klär vi upp vår båge för att göra den visuellt tilltalande!
## Steg 5: Lägg till en andra bågeform
Låt oss lägga till en annan bågform för att ge mer sammanhang.
```csharp
// Lägg till ytterligare en bågeform.
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
I likhet med den första bågen lägger vi till en andra båge på samma kalkylblad. Koordinaterna här är lite förskjutna för att placera den annorlunda.
## Steg 6: Anpassa den andra bågen
Precis som vi gjorde med den första bågen kommer vi att anpassa den andra också.
```csharp
// Ställ in linjefärgen
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
// Ställ in placeringen av bågen.
arc2.Placement = PlacementType.FreeFloating;          
// Ställ in linjevikten.
arc2.Line.Weight = 1;           
// Ställ in streckstilen för bågen.
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Här ger vi den andra bågen samma stil som den första. Du kan ändra färg eller styling efter önskemål för unika eller tematiska ändamål.
## Steg 7: Spara arbetsboken
Äntligen är det dags att spara din nyskapade arbetsbok med bågarna.
```csharp
// Spara excel-filen.
excelbook.Save(dataDir + "book1.out.xls");
```
Den här raden fungerar som att trycka på spara-knappen. Vi sparar vårt arbete på den angivna platsen med ett angivet filnamn. Se till att kontrollera din katalog för att se ditt mästerverk i Excel-format!
## Slutsats
den här handledningen har vi utforskat processen att lägga till bågformer till ett Excel-kalkylblad med Aspose.Cells för .NET. Genom en enkel steg-för-steg-guide har du lärt dig hur du skapar en ny arbetsbok, lägger till bågar, anpassar deras utseende och sparar ditt dokument. Denna funktion förbättrar inte bara det visuella tilltalande av dina kalkylblad utan gör också dina datapresentationer mer informativa. Oavsett om du skapar diagram, rapporter eller bara experimenterar, kan använda former som bågar ge dina projekt en kreativ twist.
## FAQ's
### Vad är Aspose.Cells?
Aspose.Cells är ett kraftfullt bibliotek som låter utvecklare skapa, manipulera och konvertera Excel-filer programmatiskt utan behov av Microsoft Excel.
### Behöver jag installera Microsoft Excel för att använda Aspose.Cells?
Nej, Aspose.Cells är helt oberoende och kräver inte att Microsoft Excel installeras.
### Kan jag prova Aspose.Cells gratis?
 Ja, du kan prova Aspose.Cells med deras[Gratis provperiod](https://releases.aspose.com/).
### Vilka programmeringsspråk stöder Aspose.Cells?
Aspose.Cells stöder flera språk, inklusive C#, VB.NET och mer.
### Var kan jag få support för Aspose.Cells?
 Du kan få stöd genom[Aspose Forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
