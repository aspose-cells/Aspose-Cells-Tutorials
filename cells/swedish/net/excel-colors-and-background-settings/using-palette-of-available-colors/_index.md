---
title: Använda palett av tillgängliga färger i Excel
linktitle: Använda palett av tillgängliga färger i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du skapar anpassade färgpaletter och tillämpar dem på dina Excel-kalkylblad med Aspose.Cells för .NET. Förbättra det visuella tilltalande av dina data med livfulla färger och formateringsalternativ.
weight: 11
url: /sv/net/excel-colors-and-background-settings/using-palette-of-available-colors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Använda palett av tillgängliga färger i Excel

## Introduktion
Har du någonsin stirrat på ett intetsägande, monokromt kalkylblad och önskat dig en färgklick? Aspose.Cells för .NET kommer till undsättning och ger dig möjlighet att utöva kraften i anpassade färgpaletter och förvandla dina kalkylblad till visuellt fantastiska mästerverk. I den här omfattande guiden ger vi oss ut på en steg-för-steg-resa för att låsa upp hemligheterna med färganpassning i Excel med Aspose.Cells. 

## Förutsättningar

- Aspose.Cells for .NET Library: Ladda ner den senaste versionen från webbplatsen ([https://releases.aspose.com/cells/net/](https://releases.aspose.com/cells/net/)) för att komma igång. 
- En textredigerare eller IDE: Välj ditt val av vapen, som Visual Studio eller någon annan .NET-utvecklingsmiljö. 
- Grundläggande programmeringskunskap: Den här guiden förutsätter att du har en grundläggande förståelse för C# och att arbeta med bibliotek i .NET-projekt.

## Importera paket

 Dessutom måste du importera några systemnamnrymder som`System.IO` för filmanipulering. 

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Skapa färgglada kalkylblad: en steg-för-steg-guide

Låt oss nu dyka in i koden och se hur man skapar en anpassad färgpalett och tillämpar den på en Excel-cell. Föreställ dig att måla ditt kalkylblad med en levande "Orchid"-färg!

## Steg 1: Konfigurera katalogen:

```csharp
// Definiera sökvägen till din dokumentkatalog
string dataDir = "Your Document Directory";

// Skapa katalogen om den inte finns
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
{
   System.IO.Directory.CreateDirectory(dataDir);
}
```

Detta kodavsnitt upprättar katalogen där du vill spara din sista Excel-fil. Kom ihåg att ersätta "Din dokumentkatalog" med den faktiska sökvägen på ditt system.

## Steg 2: Instantiera arbetsboksobjektet:

```csharp
// Skapa ett nytt arbetsboksobjekt
Workbook workbook = new Workbook();
```

 Tänk på`Workbook` objekt som den tomma duken där du ska måla ditt färgglada mästerverk. Den här raden skapar en ny arbetsboksinstans, redo att fyllas med data och formatering.

## Steg 3: Lägga till en anpassad färg till paletten:

```csharp
// Lägg till Orchid-färgen till paletten vid index 55
workbook.ChangePalette(Color.Orchid, 55);
```

Här händer magin! Den här raden lägger till en anpassad färg, "Orchid" i det här fallet, till Excel-färgpaletten. De`ChangePalette` Metoden tar två argument: den önskade färgen och indexet inom paletten (från 0 till 55) där du vill placera den. 

Viktig anmärkning: Excel har en begränsad standardfärgpalett. Om du försöker använda en färg som inte finns i standarduppsättningen måste du lägga till den i paletten med den här metoden innan du applicerar den på något element i ditt kalkylark.

## Steg 4: Skapa ett nytt arbetsblad:

```csharp
// Lägg till ett nytt kalkylblad i arbetsboken
int i = workbook.Worksheets.Add();

// Få referensen till det nyligen tillagda kalkylbladet
Worksheet worksheet = workbook.Worksheets[i];
```

Med en tom duk (arbetsbok) i handen är det dags att skapa ett ark för dina konstnärliga ansträngningar. Det här kodavsnittet lägger till ett nytt kalkylblad i arbetsboken och hämtar en referens till det med hjälp av dess index.

## Steg 5: Åtkomst till målcellen:

```csharp
// Gå till cellen vid position "A1"
Cell cell = worksheet.Cells["A1"];
```

Föreställ dig ditt kalkylblad som ett gigantiskt rutnät. Varje cell har en unik adress, identifierad av en kombination av en kolumnbokstav (A, B, C...) och ett radnummer (1, 2, 3...). Den här raden hämtar en referens till cellen som finns vid "A1" i det nyskapade kalkylbladet.

## Steg 6: Lägga till innehåll i cellen:

```csharp
// Lägg till lite text i cell A1
cell.PutValue("Hello Aspose!");
```

Nu när du har din målarpensel (cellreferens) är det dags att lägga till lite innehåll på duken. Denna rad infogar texten "

## Steg 7: Applicera den anpassade färgen

```csharp
// Skapa ett nytt Style-objekt
Style styleObject = workbook.CreateStyle();

// Ställ in Orchid-färgen på typsnittet
styleObject.Font.Color = Color.Orchid;

// Använd stilen på cellen
cell.SetStyle(styleObject);
```

 I det här steget skapar vi en ny`Style` objekt för att definiera formateringen för vår text. De`styleObject.Font.Color` egenskapen är inställd på "Orchid"-färgen som vi lade till i paletten tidigare. Slutligen, den`cell.SetStyle` metoden tillämpar stilen på den tidigare valda cellen vid "A1".

## Steg 8: Spara arbetsboken

```csharp
// Spara arbetsboken
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Auto);
```

Denna sista rad sparar arbetsboken med alla dess formateringsändringar i den angivna katalogen. De`SaveFormat.Auto` argument bestämmer automatiskt lämpligt filformat baserat på filtillägget.

## Slutsats

Genom att följa dessa steg har du framgångsrikt anpassat färgpaletten i Excel med Aspose.Cells för .NET. Du kan nu släppa loss din kreativitet och skapa visuellt tilltalande kalkylblad som sticker ut från mängden. 

## FAQ's

### Kan jag använda andra färgformat än Color.Orchid?
 Absolut! Du kan använda vilken färg som helst från`Color` uppräkning eller definiera anpassade färger med hjälp av`Color` strukturera.

### Hur använder jag den anpassade färgen på flera celler?
 Du kan skapa en`Style` objekt och tillämpa det på flera celler med loopar eller intervall.

### Kan jag skapa anpassade färggradienter?
Ja, Aspose.Cells låter dig skapa anpassade färggradienter för celler eller former. Se dokumentationen för mer information.

### Är det möjligt att ändra bakgrundsfärgen för en cell?
Säkert! Du kan ändra`Style` föremålets`BackgroundColor` egenskap för att ändra bakgrundsfärgen.

### Var kan jag hitta fler exempel och dokumentation?
Besök Aspose.Cells för .NET-dokumentationen ([https://reference.aspose.com/cells/net/](https://reference.aspose.com/cells/net/)) för omfattande information och kodexempel.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
