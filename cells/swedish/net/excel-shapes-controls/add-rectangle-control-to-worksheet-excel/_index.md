---
"description": "Lär dig hur du lägger till en rektangelkontroll i ett Excel-kalkylblad med hjälp av Aspose.Cells för .NET med en detaljerad steg-för-steg-guide."
"linktitle": "Lägg till rektangelkontroll i kalkylblad i Excel"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Lägg till rektangelkontroll i kalkylblad i Excel"
"url": "/sv/net/excel-shapes-controls/add-rectangle-control-to-worksheet-excel/"
"weight": 25
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till rektangelkontroll i kalkylblad i Excel

## Introduktion
När det gäller att automatisera Excel-uppgifter är Aspose.Cells för .NET ett kraftfullt verktyg som kan hjälpa dig att uppnå en mängd olika mål, varav ett är att lägga till former som rektanglar i dina kalkylblad. I den här guiden utforskar vi hur man lägger till en rektangelkontroll i ett Excel-kalkylblad med hjälp av Aspose.Cells för .NET. Till slut kommer du att kunna skapa, anpassa och spara ett kalkylblad med en inbäddad rektangelkontroll.
Men innan vi dyker in, låt oss prata om förutsättningarna.
## Förkunskapskrav
För att följa den här handledningen, se till att du har följande förutsättningar på plats:
1. Aspose.Cells för .NET-biblioteket: Om du inte redan har gjort det, [ladda ner biblioteket](https://releases.aspose.com/cells/net/) eller installera den med NuGet i Visual Studio.
2. .NET Framework: Du måste ha .NET-utvecklingsmiljön konfigurerad på din dator.
3. Grundläggande kunskaper i C#: Även om vi guidar dig steg för steg är grundläggande förtrogenhet med C# och objektorienterad programmering fördelaktigt.
4. Licens: Att använda Aspose.Cells i utvärderingsläge fungerar bra för grundläggande uppgifter, men för full funktionalitet, överväg att skaffa en [tillfällig licens](https://purchase.aspose.com/temporary-license/) eller köper en från [här](https://purchase.aspose.com/buy).
Nu, låt oss dyka in i koden!
## Importera paket
För att komma igång med Aspose.Cells, se till att du har importerat de nödvändiga namnrymderna till ditt projekt. Dessa importer ger åtkomst till olika klasser och metoder som du behöver för att interagera med Excel-filer.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Dessa rader säkerställer att ditt projekt kan interagera med filkataloger (`System.IO`), Excel-arbetsböcker (`Aspose.Cells`), och formteckning (`Aspose.Cells.Drawing`).
Nu ska vi dela upp processen i enkla steg så att du enkelt kan följa med och kopiera detta i dina egna projekt.
## Steg 1: Konfigurera katalogsökvägen
Det första du behöver göra är att definiera katalogen där din Excel-fil ska sparas. Detta steg säkerställer att ditt projekt vet var utdatafilen ska skapas och lagras.
### Definiera datakatalogen
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
```
Här anger du sökvägen till katalogen där Excel-filen ska lagras. Du kan ersätta `"Your Document Directory"` med den faktiska sökvägen på din maskin, eller skapa en mapp dynamiskt om den inte finns.
### Kontrollera och skapa katalogen
```csharp
// Skapa katalog om den inte redan finns.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Det här blocket kontrollerar om katalogen finns. Om inte, skapas en. Tänk på det som att ha ditt arkivskåp redo innan du lagrar några dokument.
## Steg 2: Instansiera en ny arbetsbok
I det här steget skapar du en ny Excel-arbetsbok med hjälp av `Aspose.Cells.Workbook` klass. Detta kommer att fungera som behållare för ditt arbetsblad och dina former.
```csharp
// Skapa en ny arbetsbok.
Workbook excelbook = new Workbook();
```
Genom att ringa `Workbook` konstruktorn, du har nu en tom Excel-arbetsbok redo för anpassning.
## Steg 3: Lägga till en rektangelkontroll
Det är här magin händer. Du lägger till en rektangelform i det första kalkylbladet i din arbetsbok.
```csharp
// Lägg till en rektangelkontroll.
Aspose.Cells.Drawing.RectangleShape rectangle = excelbook.Worksheets[0].Shapes.AddRectangle(3, 0, 2, 0, 70, 130);
```
Låt oss bryta ner detta:
- `excelbook.Worksheets[0]`Detta öppnar det första kalkylbladet i din arbetsbok.
- `.Shapes.AddRectangle(3, 0, 2, 0, 70, 130)`Detta lägger till en rektangelform i kalkylbladet. Parametrarna här definierar positionen (rad och kolumn), samt bredden och höjden på rektangeln.
## Steg 4: Anpassa rektangeln
Att bara lägga till en rektangel räcker inte – du vill anpassa den. I det här steget ställer vi in placering, linjetjocklek och streckstil för rektangeln.
### Ställa in placeringen
```csharp
// Ange placeringen av rektangeln.
rectangle.Placement = PlacementType.FreeFloating;
```
Detta anger att rektangeln är fritt flytande, vilket betyder att den inte kommer att vara bunden av celldimensioner.
### Ställa in linjetjockleken
```csharp
// Ställ in linjetjockleken.
rectangle.Line.Weight = 4;
```
Här ställer vi in linjetjockleken för rektangeln till 4 punkter. Ju högre siffra, desto tjockare linje.
### Ställa in streckstilen
```csharp
// Ställ in streckstilen för rektangeln.
rectangle.Line.DashStyle = MsoLineDashStyle.Solid;
```
Den här linjen ställer in streckstilen för rektangelns kantlinje till heldragen. Du kan experimentera med olika stilar som `Dash` eller `Dot` beroende på dina krav.
## Steg 5: Spara arbetsboken
När rektangeln har lagts till och anpassats är det sista steget att spara arbetsboken i den angivna katalogen.
```csharp
// Spara Excel-filen.
excelbook.Save(dataDir + "book1.out.xls");
```
Detta sparar arbetsboken som en `.xls` filen i mappen du definierade tidigare. Du kan ändra filformatet genom att ändra filändelsen, till exempel `.xlsx` om du föredrar det nyare Excel-formatet.
## Slutsats
Och där har du det! Att lägga till en rektangelkontroll i ett Excel-kalkylblad med Aspose.Cells för .NET är en enkel process när du väl har brytt ner det steg för steg. Oavsett om du behöver lägga till former för visuellt tilltalande, markera delar av dina data eller anpassa dina rapporter, ger Aspose.Cells dig flexibiliteten att göra det programmatiskt.
Den här guiden borde ha utrustat dig med all den kunskap du behöver för att börja lägga till former som rektanglar i dina Excel-ark med Aspose.Cells. Nu är det dags att experimentera och se vad mer du kan uppnå med detta kraftfulla bibliotek!
## Vanliga frågor
### Kan jag lägga till andra former som cirklar eller linjer med Aspose.Cells för .NET?  
Ja, Aspose.Cells låter dig lägga till en mängd olika former, inklusive cirklar, linjer, pilar och mer.
### Vilka andra egenskaper kan jag ange för rektangelkontrollen?  
Du kan anpassa fyllningsfärg, linjefärg, genomskinlighet och till och med lägga till text i rektangeln.
### Är Aspose.Cells kompatibelt med .NET Core?  
Ja, Aspose.Cells stöder .NET Core, såväl som .NET Framework och andra .NET-baserade plattformar.
### Kan jag placera rektangeln i förhållande till en specifik cell?  
Ja, du kan placera rektangeln inom specifika rader och kolumner, eller använda `PlacementType` att kontrollera hur den är förankrad.
### Finns det en gratis provversion av Aspose.Cells?  
Ja, du kan få en [gratis provperiod](https://releases.aspose.com/) från webbplatsen för att testa bibliotekets funktioner innan du köper.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}