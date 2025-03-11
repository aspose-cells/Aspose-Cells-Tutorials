---
title: Extrahera OLE-objekt från Excel
linktitle: Extrahera OLE-objekt från Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du extraherar OLE-objekt från Excel-filer med Aspose.Cells för .NET. Steg-för-steg-guide för enkel utvinning.
weight: 10
url: /sv/net/excel-ole-picture-objects/extract-ole-object-from-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera OLE-objekt från Excel

## Introduktion
dagens teknikkunniga värld är det en vanlig uppgift att hantera Excel-filer, särskilt för dem som arbetar med dataanalys, ekonomi och projektledning. En aspekt som ofta förbises är hanteringen av OLE-objekt (Object Linking and Embedding) i Excel-kalkylblad. Dessa kan vara inbäddade dokument, bilder eller till och med komplexa datatyper som spelar en avgörande roll för att förbättra funktionaliteten och rikedomen hos dina Excel-filer. Om du är en Aspose.Cells-användare som vill extrahera dessa OLE-objekt programmatiskt med .NET, är du på rätt plats! Den här guiden leder dig genom processen steg-för-steg, så att du inte bara förstår hur du gör det, utan också varför varje del av processen är viktig.
## Förutsättningar
Innan vi dyker in i de små detaljerna för att extrahera OLE-objekt, finns det några saker du måste ha på plats:
1. Grundläggande kunskaper om C#: Om du är bekant med C# är du redan på rätt väg. Om inte, oroa dig inte! Vi ska hålla saker raka.
2. Aspose.Cells installerat: Du behöver Aspose.Cells-biblioteket. Du kan ladda ner den från webbplatsen[här](https://releases.aspose.com/cells/net/).
3. En kompatibel utvecklingsmiljö: Se till att du har en .NET-utvecklingsmiljö inställd, som Visual Studio, redo att börja.
4. Ett exempel på Excel-fil: Du behöver en Excel-fil med OLE-objekt inbäddade för testning. 
När du har dessa förutsättningar på plats kan vi börja vår resa in i världen av OLE-objektutvinning.
## Importera paket
Låt oss först importera de nödvändiga paketen som vi kommer att använda i vår handledning. I ditt C#-projekt måste du inkludera Aspose.Cells-namnrymden. Så här kan du göra det:
```csharp
using System.IO;
using Aspose.Cells;
```
## Steg 1: Ställ in dokumentkatalogen
I det här steget kommer vi att definiera sökvägen där vår Excel-fil finns. Du kanske undrar varför detta är viktigt. Det är som att sätta scenen för en föreställning – det hjälper manuset att veta var man kan hitta skådespelarna (i vårt fall Excel-filen).
```csharp
string dataDir = "Your Document Directory";
```
 Ersätta`"Your Document Directory"` med den faktiska sökvägen där din Excel-fil (`book1.xls`) lagras.
## Steg 2: Öppna Excel-filen
Nu när vi har ställt in vår dokumentkatalog är nästa steg att öppna Excel-filen. Se det här som att öppna en bok innan du börjar läsa – det är viktigt att se vad som finns inuti.
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
## Steg 3: Gå till OLE-objektsamlingen
Varje kalkylblad i en Excel-arbetsbok kan innehålla olika objekt, inklusive OLE-objekt. Här kommer vi åt det första kalkylbladets OLE-objektsamling. Det liknar att välja en sida för att kolla in inbäddade bilder och dokument.
```csharp
Aspose.Cells.Drawing.OleObjectCollection oles = workbook.Worksheets[0].OleObjects;
```
## Steg 4: Slinga genom OLE-objekten
Nu kommer den roliga delen – att gå igenom alla OLE-objekt i vår samling. Detta steg är avgörande eftersom det tillåter oss att hantera flera OLE-objekt effektivt. Föreställ dig att gå igenom en skattkista för att hitta värdefulla föremål!
```csharp
for (int i = 0; i < oles.Count; i++)
{
    Aspose.Cells.Drawing.OleObject ole = oles[i];
    // Ytterligare logik för att hantera varje objekt
}
```
## Steg 5: Ange utdatafilnamnet
När vi gräver djupare i varje OLE-objekt måste vi komma på ett filnamn för de extraherade objekten. Varför? För när vi väl har tagit ut dem vill vi hålla allt organiserat så att vi enkelt kan hitta våra skatter senare.
```csharp
string fileName = dataDir + "ole_" + i + ".";
```
## Steg 6: Bestäm filformatstypen
Varje OLE-objekt kan vara av olika typer (t.ex. dokument, kalkylblad, bilder). Det är viktigt att bestämma formattypen så att du kan extrahera den korrekt. Det är som att känna till receptet på en maträtt – du måste känna till ingredienserna!
```csharp
switch (ole.FileFormatType)
{
    case FileFormatType.Doc:
        fileName += "doc";
        break;
    case FileFormatType.Xlsx:
        fileName += "xlsx";
        break;
    case FileFormatType.Ppt:
        fileName += "ppt";
        break;
    case FileFormatType.Pdf:
        fileName += "pdf";
        break;
    case FileFormatType.Unknown:
        fileName += "jpg";
        break;
    default:
        // Hantera andra filformat
        break;
}
```
## Steg 7: Spara OLE-objektet
 Låt oss nu gå vidare till att spara OLE-objektet. Om objektet är en Excel-fil sparar vi den med hjälp av en`MemoryStream` vilket gör att vi kan hantera data i minnet innan vi skriver ut dem. Det här steget liknar att paketera din skatt innan du skickar den till en vän.
```csharp
if (ole.FileFormatType == FileFormatType.Xlsx)
{
    MemoryStream ms = new MemoryStream();
    ms.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    Workbook oleBook = new Workbook(ms);
    oleBook.Settings.IsHidden = false;
    oleBook.Save(dataDir + "Excel_File" + i + ".out.xlsx");
}
```
 För andra typer av filer använder vi en`FileStream` för att skapa filen på disken.
```csharp
else
{
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
}
```

## Slutsats
Och precis som det, du har framgångsrikt navigerat vattnet i OLE-objektextraktion med Aspose.Cells för .NET! Genom att följa dessa steg kan du enkelt extrahera och hantera inbäddade objekt från dina Excel-filer. Kom ihåg, precis som alla värdefulla färdigheter, övning ger färdighet. Så, ta dig tid att experimentera med olika Excel-filer, och snart kommer du att bli ett OLE-extraktionsproffs!
## FAQ's
### Vad är OLE-objekt i Excel?
OLE-objekt är teknologi som tillåter inbäddning och länkning till dokument och data i andra applikationer i ett Excel-kalkylblad.
### Varför skulle jag behöva extrahera OLE-objekt?
Genom att extrahera OLE-objekt kan du komma åt och manipulera inbäddade dokument eller bilder oberoende av den ursprungliga Excel-filen.
### Kan Aspose.Cells hantera alla typer av inbäddade filer?
Ja, Aspose.Cells kan hantera olika OLE-objekt, inklusive Word-dokument, Excel-ark, PowerPoint-presentationer och bilder.
### Hur installerar jag Aspose.Cells för .NET?
 Du kan installera Aspose.Cells genom att ladda ner det från deras[släpp sida](https://releases.aspose.com/cells/net/).
### Var kan jag hitta support för Aspose.Cells?
Du kan få support för Aspose.Cells på deras[supportforum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
