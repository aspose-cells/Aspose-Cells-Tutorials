---
title: Skapa genomstruken effekt på text i Excel
linktitle: Skapa genomstruken effekt på text i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du tillämpar en överstruken effekt på text i Excel med Aspose.Cells för .NET i denna detaljerade steg-för-steg handledning.
weight: 15
url: /sv/net/working-with-fonts-in-excel/creating-strike-out-effect/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa genomstruken effekt på text i Excel

## Introduktion
När det kommer till Excel är visuella element lika viktiga som själva data. Oavsett om du markerar viktiga ändringar eller markerar objekt som inte längre är relevanta, är genomstruken effekt på text ett klassiskt sätt att hantera visuell representation i kalkylblad. I den här guiden går vi igenom processen för att implementera en överstruken effekt på text i Excel med Aspose.Cells för .NET. Denna handledning kommer inte bara att täcka de nödvändiga förutsättningarna utan kommer också att tillhandahålla ett steg-för-steg tillvägagångssätt för att säkerställa att du kan replikera denna effekt med lätthet.
## Förutsättningar
Innan du dyker in i handledningen, se till att du har följande förutsättningar uppfyllda:
1. Utvecklingsmiljö: Du bör ha en .NET-utvecklingsmiljö inrättad. Detta kan vara Visual Studio eller någon annan IDE du föredrar som stöder .NET-utveckling.
2. Aspose.Cells för .NET: Se till att du har Aspose.Cells installerat i ditt projekt. Du kan ladda ner den från följande länk:[Ladda ner Aspose.Cells](https://releases.aspose.com/cells/net/).
3. Grundläggande kunskaper om C#: En grundläggande förståelse för C#-programmering är till hjälp eftersom exemplen kommer att kodas i C#.
4. .NET Framework: Se till att ditt projekt är inriktat på en kompatibel .NET Framework-version, vanligtvis .NET Core eller .NET Framework 4.5 och senare.
## Importera paket
Innan du skriver någon kod måste du importera de nödvändiga namnrymden från Aspose.Cells. Detta är avgörande för att komma åt olika funktioner som tillhandahålls av biblioteket. Så här kan du importera de nödvändiga namnrymden:
```csharp
using System.IO;
using Aspose.Cells;
```
Med dessa importer får du tillgång till klasserna Workbook, Worksheet och Style som kommer att användas i den här självstudien.
Nu när vi har satt scenen, låt oss dela upp processen i hanterbara steg. Varje steg kommer att åtföljas av tydliga instruktioner för att guida dig genom att skapa en överstruken effekt på text i Excel.
## Steg 1: Definiera dokumentkatalogen
Börja med att definiera sökvägen där dina Excel-dokument ska lagras. Detta kommer att vara platsen för att spara dina utdatafiler.
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
```
 Ersätta`"Your Document Directory"` med den faktiska katalogsökvägen där du vill spara din Excel-fil. Detta ställer in katalogen för din utdata.
## Steg 2: Skapa katalogen
Därefter måste du se till att katalogen du angav i föregående steg finns. Om det inte finns kan du skapa det programmatiskt.
```csharp
// Skapa katalog om den inte redan finns.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Denna kod kontrollerar om katalogen finns och skapar den om inte. Detta hjälper till att undvika fel när du försöker spara din fil senare.
## Steg 3: Instantiera ett arbetsboksobjekt
Nu är det dags att skapa ett nytt arbetsboksobjekt. Detta är grunden för din Excel-fil där du kommer att lägga till data och tillämpa format.
```csharp
// Instantiera ett arbetsboksobjekt
Workbook workbook = new Workbook();
```
 De`Workbook` klass representerar en Excel-fil. Genom att skapa en instans av den här klassen skapar du i princip ett nytt Excel-dokument.
## Steg 4: Lägg till ett nytt arbetsblad
Varje arbetsbok kan innehålla flera kalkylblad. Låt oss gå vidare och skapa ett nytt kalkylblad i din arbetsbok.
```csharp
// Lägga till ett nytt kalkylblad till Excel-objektet
int i = workbook.Worksheets.Add();
```
 De`Add` metod för`Worksheets` samling lägger till ett nytt kalkylblad i arbetsboken och returnerar dess index. 
## Steg 5: Skaffa referensen till det nya arbetsbladet
När du har skapat kalkylbladet måste du referera till det för framtida operationer.
```csharp
// Få referensen till det nyligen tillagda kalkylbladet genom att skicka dess arkindex
Worksheet worksheet = workbook.Worksheets[i];
```
Här hämtar du det nyskapade kalkylbladet med dess index (`i`). Detta ger dig tillgång till att manipulera kalkylbladet.
## Steg 6: Gå till en cell
 Du vill komma åt en specifik cell i ditt kalkylblad där du kommer att använda överstruket format. I det här exemplet använder vi cell`A1`.
```csharp
// Åtkomst till "A1"-cellen från kalkylbladet
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```
 I Excel hänvisas till celler med kolumn- och radidentifierare (t.ex. "A1"). Vi skaffar en referens till cell`A1` för ytterligare manipulation.
## Steg 7: Lägg till värde till cellen
 Låt oss sedan infoga lite text i cellen. Vi kommer att skriva "Hej Aspose!" i cellen`A1`.
```csharp
// Lägga till något värde till "A1"-cellen
cell.PutValue("Hello Aspose!");
```
 De`PutValue` metod används för att tilldela ett strängvärde till cellen. Du kan ändra denna sträng till allt du vill ska visas.
## Steg 8: Skaffa cellens stil
Nu när vi har text i vår cell är det dags att komma åt cellens stil för att tillämpa vår önskade formatering, inklusive överstruken effekt.
```csharp
// Få cellens stil
Style style = cell.GetStyle();
```
 De`GetStyle` metod hämtar den aktuella stilen för cellen, så att du kan ändra egenskaper som typsnitt, storlek och effekter.
## Steg 9: Ställ in genomstruken effekt
Låt oss tillämpa överstruken effekt på texten i cellen. Vi kommer att ändra teckensnittet för cellen.
```csharp
// ExStart:SetStrikeout
// Ställer in överstruken effekt på typsnittet
style.Font.IsStrikeout = true;
// ExEnd:SetStrikeout
```
 Genom att ställa in`IsStrikeout` sannerligen instruerar du Excel att visuellt stryka över texten i den valda cellen - ungefär som att visuellt markera något från en lista.
## Steg 10: Applicera stilen på cellen
Efter att ha modifierat stilen måste du återställa den i cellen för att återspegla ändringarna.
```csharp
// Använder stilen på cellen
cell.SetStyle(style);
```
 De`SetStyle` metod uppdaterar cellen med den nya stilen, som nu inkluderar överstruken formatering.
## Steg 11: Spara Excel-filen
 Slutligen är det dags att spara din arbetsbok i den angivna katalogen. I det här exemplet sparar vi filen med namnet`book1.out.xls`.
```csharp
// Sparar Excel-filen
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
 De`Save`metoden skriver arbetsboken till disken i 97-2003 Excel-format. Du kan ange olika format om det behövs.
## Slutsats
Att skapa en överstruken effekt på text i Excel med Aspose.Cells för .NET är en enkel process när du bryter ner den steg för steg. Genom att följa den här guiden har du nu kompetensen att förbättra dina kalkylblad med visuella ledtrådar, vilket gör din data inte bara informativ utan också visuellt engagerande.
## FAQ's
### Vad är Aspose.Cells?
Aspose.Cells är ett kraftfullt bibliotek för att hantera Excel-filer i .NET-applikationer, vilket gör att du kan skapa, manipulera och konvertera Excel-dokument programmatiskt.
### Kan jag använda Aspose.Cells gratis?
 Ja, du kan använda det gratis under en provperiod. En gratis provperiod finns på[Aspose.Cells gratis provperiod](https://releases.aspose.com/).
### Hur köper jag Aspose.Cells?
 Du kan köpa en licens för Aspose.Cells via deras hemsida[Köp Aspose.Cells](https://purchase.aspose.com/buy).
### Finns det exempel tillgängliga för användning av Aspose.Cells?
 Ja, du kan hitta massor av exempel och kodavsnitt i[Aspose.Cells dokumentation](https://reference.aspose.com/cells/net/).
### Var kan jag få support för Aspose.Cells?
 Du kan få stöd och hjälp från samhället[Aspose Forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
