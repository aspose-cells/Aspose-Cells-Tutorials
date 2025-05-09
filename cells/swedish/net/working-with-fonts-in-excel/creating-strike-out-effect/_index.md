---
"description": "Lär dig hur du använder en utstrykningseffekt på text i Excel med Aspose.Cells för .NET i den här detaljerade steg-för-steg-handledningen."
"linktitle": "Skapa en överstruken effekt på text i Excel"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Skapa en överstruken effekt på text i Excel"
"url": "/sv/net/working-with-fonts-in-excel/creating-strike-out-effect/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Skapa en överstruken effekt på text i Excel

## Introduktion
När det gäller Excel är visuella element lika viktiga som själva informationen. Oavsett om du markerar viktiga ändringar eller markerar objekt som inte längre är relevanta är en överstruken effekt på text ett klassiskt sätt att hantera visuell representation i kalkylblad. I den här guiden guidar vi dig genom processen att implementera en överstruken effekt på text i Excel med Aspose.Cells för .NET. Den här handledningen täcker inte bara de nödvändiga förutsättningarna utan ger också en steg-för-steg-metod för att säkerställa att du enkelt kan replikera denna effekt.
## Förkunskapskrav
Innan du börjar med handledningen, se till att du har följande förutsättningar uppfyllda:
1. Utvecklingsmiljö: Du bör ha en .NET-utvecklingsmiljö konfigurerad. Detta kan vara Visual Studio eller någon annan IDE som du föredrar och som stöder .NET-utveckling.
2. Aspose.Cells för .NET: Se till att du har Aspose.Cells installerat i ditt projekt. Du kan ladda ner det från följande länk: [Ladda ner Aspose.Cells](https://releases.aspose.com/cells/net/).
3. Grundläggande kunskaper i C#: En grundläggande förståelse för C#-programmering är bra eftersom exemplen kommer att kodas i C#.
4. .NET Framework: Se till att ditt projekt riktar sig mot en kompatibel .NET Framework-version, vanligtvis .NET Core eller .NET Framework 4.5 och senare.
## Importera paket
Innan du skriver någon kod måste du importera de namnrymder som krävs från Aspose.Cells. Detta är avgörande för att komma åt olika funktioner som tillhandahålls av biblioteket. Så här importerar du de namnrymder som behövs:
```csharp
using System.IO;
using Aspose.Cells;
```
Med dessa importer har du tillgång till klasserna Arbetsbok, Arbetsblad och Stil som kommer att användas i den här handledningen.
Nu när vi har förberett oss, låt oss dela upp processen i hanterbara steg. Varje steg kommer att åtföljas av tydliga instruktioner som vägleder dig genom att skapa en överstruken effekt på text i Excel.
## Steg 1: Definiera dokumentkatalogen
Börja med att definiera sökvägen där dina Excel-dokument ska lagras. Det här är platsen där du sparar dina utdatafiler.
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
```
Ersätta `"Your Document Directory"` med den faktiska katalogsökvägen där du vill spara din Excel-fil. Detta konfigurerar katalogen för din utdata.
## Steg 2: Skapa katalogen
Sedan måste du se till att katalogen du angav i föregående steg finns. Om den inte finns kan du skapa den programmatiskt.
```csharp
// Skapa katalog om den inte redan finns.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Denna kod kontrollerar om katalogen finns och skapar den om den inte finns. Detta hjälper till att undvika fel när du försöker spara filen senare.
## Steg 3: Instansiera ett arbetsboksobjekt
Nu är det dags att skapa ett nytt arbetsboksobjekt. Detta är grunden för din Excel-fil där du kommer att lägga till data och använda format.
```csharp
// Instansiera ett arbetsboksobjekt
Workbook workbook = new Workbook();
```
De `Workbook` klassen representerar en Excel-fil. Genom att skapa en instans av den här klassen skapar du i princip ett nytt Excel-dokument.
## Steg 4: Lägg till ett nytt arbetsblad
Varje arbetsbok kan innehålla flera arbetsblad. Nu går vi vidare och skapar ett nytt arbetsblad i din arbetsbok.
```csharp
// Lägga till ett nytt kalkylblad i Excel-objektet
int i = workbook.Worksheets.Add();
```
De `Add` metod för `Worksheets` samlingen lägger till ett nytt kalkylblad i arbetsboken och returnerar dess index. 
## Steg 5: Hämta referensen till det nya arbetsbladet
När du har skapat kalkylbladet behöver du använda det som referens för framtida operationer.
```csharp
// Hämta referensen till det nyligen tillagda kalkylbladet genom att skicka dess arkindex
Worksheet worksheet = workbook.Worksheets[i];
```
Här hämtar du det nyskapade kalkylbladet med hjälp av dess index (`i`Detta ger dig tillgång att manipulera kalkylbladet.
## Steg 6: Åtkomst till en cell
Du vill komma åt en specifik cell i ditt kalkylblad där du ska använda överstrukningsformatet. I det här exemplet använder vi cell `A1`.
```csharp
// Åtkomst till cellen "A1" från kalkylbladet
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```
I Excel refereras celler till med sina kolumn- och radidentifierare (t.ex. "A1"). Vi får en referens till cell `A1` för vidare manipulation.
## Steg 7: Lägg till värde i cellen
Nu ska vi infoga lite text i cellen. Vi skriver "Hej Aspose!" i cellen. `A1`.
```csharp
// Lägger till värde i cellen "A1"
cell.PutValue("Hello Aspose!");
```
De `PutValue` Metoden används för att tilldela ett strängvärde till cellen. Du kan ändra denna sträng till vad du vill ska visas.
## Steg 8: Hämta cellens stil
Nu när vi har text i vår cell är det dags att komma åt cellens stil för att tillämpa önskad formatering, inklusive genomstrykningseffekten.
```csharp
// Att få cellens stil
Style style = cell.GetStyle();
```
De `GetStyle` Metoden hämtar cellens aktuella stil, vilket gör att du kan ändra egenskaper som teckensnitt, storlek och effekter.
## Steg 9: Ställ in utstrykningseffekten
Nu använder vi en överstruken effekt på texten i cellen. Vi ändrar cellens teckensnitt.
```csharp
// ExStart:SetStrikeout
// Ställa in överstrukningseffekten på teckensnittet
style.Font.IsStrikeout = true;
// ExEnd:SetStrikeout
```
Genom att ställa in `IsStrikeout` till sant, instruerar du Excel att visuellt stryka över texten i den markerade cellen som genomstryks – ungefär som att visuellt markera något i en lista.
## Steg 10: Använd stilen på cellen
Efter att du har ändrat stilen måste du tillämpa den igen på cellen för att återspegla ändringarna.
```csharp
// Tillämpa stilen på cellen
cell.SetStyle(style);
```
De `SetStyle` Metoden uppdaterar cellen med den nya stilen, som nu inkluderar överstruken formatering.
## Steg 11: Spara Excel-filen
Slutligen är det dags att spara din arbetsbok i den angivna katalogen. I det här exemplet sparar vi filen med namnet `book1.out.xls`.
```csharp
// Spara Excel-filen
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
De `Save` Metoden skriver arbetsboken till disken i Excel-formatet 97-2003. Du kan ange andra format om det behövs.
## Slutsats
Att skapa en överstruken effekt på text i Excel med Aspose.Cells för .NET är en enkel process när du bryter ner den steg för steg. Genom att följa den här guiden har du nu kunskaperna för att förbättra dina kalkylblad med visuella ledtrådar, vilket gör dina data inte bara informativa utan också visuellt engagerande.
## Vanliga frågor
### Vad är Aspose.Cells?
Aspose.Cells är ett kraftfullt bibliotek för att hantera Excel-filer i .NET-applikationer, vilket gör att du kan skapa, manipulera och konvertera Excel-dokument programmatiskt.
### Kan jag använda Aspose.Cells gratis?
Ja, du kan använda det gratis under en provperiod. En gratis provperiod finns tillgänglig på [Aspose.Cells Gratis provperiod](https://releases.aspose.com/).
### Hur köper jag Aspose.Cells?
Du kan köpa en licens för Aspose.Cells via deras webbplats [Köp Aspose.Cells](https://purchase.aspose.com/buy).
### Finns det exempel tillgängliga för hur man använder Aspose.Cells?
Ja, du kan hitta massor av exempel och kodavsnitt i [Aspose.Cells-dokumentation](https://reference.aspose.com/cells/net/).
### Var kan jag få support för Aspose.Cells?
Du kan få stöd och hjälp från samhället [Aspose-forumet](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}