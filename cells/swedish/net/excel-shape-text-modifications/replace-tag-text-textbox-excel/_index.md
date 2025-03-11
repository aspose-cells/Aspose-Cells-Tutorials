---
title: Ersätt tagg med text i TextBox i Excel
linktitle: Ersätt tagg med text i TextBox i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Byt enkelt ut text i textrutor i dina Excel-ark med Aspose.Cells för .NET. En steg-för-steg-guide för Excel-automatisering.
weight: 11
url: /sv/net/excel-shape-text-modifications/replace-tag-text-textbox-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ersätt tagg med text i TextBox i Excel

## Introduktion
I den här artikeln kommer vi att dyka in i en specifik uppgift: ersätta taggar med text inuti textrutor i ett Excel-ark med Aspose.Cells. Vi guidar dig genom hela processen steg för steg, så att du förstår varje detalj. I slutet av denna handledning kommer du inte bara att förbättra din förståelse av Aspose.Cells utan också effektivisera dina Excel-relaterade uppgifter!
## Förutsättningar
Innan du kan börja behöver du några saker redo:
1. Visual Studio: Se till att du har Visual Studio installerat. Det är en flexibel IDE som gör kodning i C# till en lek.
2.  Aspose.Cells Library: Om du inte redan har gjort det, ladda ner Aspose.Cells-biblioteket för .NET från[sida](https://releases.aspose.com/cells/net/)Du kan också få en gratis testversion för att kolla in dess funktioner.
3. Grundläggande kunskaper om C#: En grundläggande förståelse för C#-programmering kommer att hjälpa dig att enkelt följa den här guiden.
Nu när du är klar, låt oss gå vidare till den roliga delen – att skriva koden!
## Importera paket
Först till kvarn – låt oss importera de nödvändiga paketen. Detta är avgörande eftersom utan rätt import kommer din kod inte att känna igen klasserna och metoderna vi kommer att använda.
## Starta ditt C#-projekt
Öppna Visual Studio och skapa ett nytt C#-projekt, helst en konsolapplikation, eftersom det gör att du enkelt kan se utdata.
## Lägg till Aspose.Cells Reference
- Högerklicka på ditt projekt i Solution Explorer.
- Välj "Lägg till" > "Referens".
- Bläddra till platsen där du laddade ner Aspose.Cells-biblioteket och inkludera det i ditt projekt.
## Importera de nödvändiga namnområdena
 När du har lagt till referensen lägger du till följande`using` direktiv högst upp i din huvudfil:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Detta ger dig tillgång till klasser inom Aspose.Cells namnutrymme.
Nu när vi har ställt in vår miljö, låt oss gå in på den saftiga delen – kodning! Vårt mål är att hitta specifika taggar i textrutor i en Excel-fil och ersätta dem med tillhandahållen text.
## Steg 1: Definiera käll- och utdatakatalogen
Först måste vi ange var vår Excel-källfil finns och var vi vill spara den modifierade versionen.
```csharp
// Käll- och utdatakatalog
string sourceDir = "Your Document Directory"; // Byt till din katalog
string outputDir = "Your Document Directory"; // Byt till din katalog
```
## Steg 2: Ladda arbetsboken
Det är här vi laddar vår Excel-arbetsbok. Om filen inte finns ger den ett felmeddelande. Så se till att din sökväg är korrekt!
```csharp
Workbook wb = new Workbook(sourceDir + "sampleReplaceTagWithText.xlsx");
```
 Här laddar vi en befintlig Excel-fil som heter`sampleReplaceTagWithText.xlsx`.
## Steg 3: Definiera taggar och ersättningstext
Därefter måste vi definiera taggarna vi letar efter och vad vi vill ersätta dem med.
```csharp
string tag = "TAG_2$TAG_1";
string replace = "1$ys";
```
 I det här exemplet delas taggarna med`$`. Du kan ersätta detta med vilken avgränsare du föredrar.
## Steg 4: Slinga över taggar och ersätt
Vi skapar en slinga för att gå igenom varje tagg vi vill ersätta. Här händer magin!
```csharp
for (int i = 0; i < tag.Split('$').Length; i++)
{
    sheetReplace(wb, "<" + tag.Split('$')[i] + ">", replace.Split('$')[i]);
}
```
## Steg 5: Spara arbetsboken
Nu när vi har gjort våra ersättningar är det dags att spara den modifierade arbetsboken i önskat format. Så här konverterar vi den till en PDF.
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
wb.Save(outputDir + "outputReplaceTagWithText.pdf", opts);
```
Du kan också spara den i olika andra format, inklusive XLSX.
## Steg 6: Implementera ersättningslogiken
 Det är här hjärtat av vår funktionalitet finns. De`sheetReplace` metod kommer att hantera själva ersättningen i Excel-kalkylbladen.
```csharp
public static void sheetReplace(Workbook workbook, string sFind, string sReplace)
{
    string finding = sFind;
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sheet.Replace(finding, sReplace);
        for (int j = 0; j < 3; j++)
        {
            if (sheet.PageSetup.GetHeader(j) != null)
                sheet.PageSetup.SetHeader(j, sheet.PageSetup.GetHeader(j).Replace(finding, sReplace));
                
            if (sheet.PageSetup.GetFooter(j) != null)
                sheet.PageSetup.SetFooter(j, sheet.PageSetup.GetFooter(j).Replace(finding, sReplace));
        }
    }
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sFind = sFind.Replace("<", "&lt;");
        sFind = sFind.Replace(">", "&gt;");
        foreach (Aspose.Cells.Drawing.TextBox mytextbox in sheet.TextBoxes)
        {
            if (mytextbox.HtmlText != null)
            {
                if (mytextbox.HtmlText.IndexOf(sFind) >= 0)
                {
                    mytextbox.HtmlText = mytextbox.HtmlText.Replace(sFind, sReplace);
                }
            }
        }
    }
}
```
- Först går vi igenom varje arbetsblad i arbetsboken.
- Vi ersätter huvudtaggen inte bara i cellinnehållet utan även i sidhuvuden och sidfötter (om de finns).
- Slutligen kontrollerar vi varje textruta i arket och ersätter texten i dem, baserat på taggen vi letar efter.
## Slutsats
Och voila! Du har nu lärt dig hur du ersätter taggar med text i textrutor i dina Excel-dokument med Aspose.Cells för .NET. Detta kan vara en verklig tidsbesparing, särskilt när du hanterar repetitiva uppgifter i kalkylblad.
## FAQ's
### Kan jag ersätta taggar över flera Excel-filer samtidigt?
Ja, genom att gå igenom en lista med filer kan du tillämpa samma logik på flera Excel-filer.
### Behöver jag en betald licens för att använda Aspose.Cells?
 Du kan börja med en gratis provperiod, men för full funktionalitet måste du köpa en licens. Checka ut[Asposes köpoptioner](https://purchase.aspose.com/buy).
### Kan jag ersätta bilder i textrutor med Aspose.Cells?
Aspose.Cells handlar främst om text. Du kan dock manipulera bilder separat om det behövs.
### Vilka format kan jag spara min modifierade Excel-fil i?
Du kan spara den i olika format inklusive XLSX, PDF, CSV, etc.
### Var kan jag hitta support för Aspose.Cells?
 Du kan hitta support och ställa frågor på[Aspose forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
