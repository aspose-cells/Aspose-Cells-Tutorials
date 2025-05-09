---
"description": "Lär dig hur du lägger till en Spinner-kontroll i ett Excel-kalkylblad med hjälp av Aspose.Cells för .NET i den här steg-för-steg-handledningen."
"linktitle": "Lägg till spinnerkontroll i kalkylblad i Excel"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Lägg till spinnerkontroll i kalkylblad i Excel"
"url": "/sv/net/excel-shapes-controls/add-spinner-control-to-worksheet-excel/"
"weight": 23
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till spinnerkontroll i kalkylblad i Excel

## Introduktion
Om du dyker ner i världen av Excel-automation med hjälp av .NET har du förmodligen stött på behovet av fler interaktiva kontroller i dina kalkylblad. En sådan kontroll är Spinner, som låter användare enkelt öka eller minska ett värde. I den här handledningen ska vi utforska hur man lägger till en Spinner-kontroll i ett Excel-kalkylblad med hjälp av Aspose.Cells för .NET. Vi delar upp det i lättförståeliga steg så att du kan följa med smidigt. 
## Förkunskapskrav
Innan vi går in i koden, låt oss se till att du har allt konfigurerat för en smidig upplevelse:
1. Aspose.Cells för .NET: Se till att du har Aspose.Cells-biblioteket. Om du inte har installerat det än kan du hämta den senaste versionen från [nedladdningslänk](https://releases.aspose.com/cells/net/).
2. Visual Studio: Du bör ha en fungerande installation av Visual Studio eller någon annan .NET IDE som du föredrar.
3. Grundläggande kunskaper i C#: Bekantskap med C#-programmering hjälper dig att enkelt förstå kodavsnitten. Om du precis har börjat, oroa dig inte! Jag guidar dig genom varje del.
## Importera paket
För att använda Aspose.Cells i ditt projekt måste du importera de nödvändiga namnrymderna. Så här konfigurerar du din miljö:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Dessa namnrymder ger dig åtkomst till kärnfunktionerna i Aspose.Cells, inklusive manipulation av arbetsböcker och ritfunktioner för former som Spinnern.
Nu när vi har gått igenom förutsättningarna och importerat de nödvändiga paketen, låt oss dyka ner i steg-för-steg-guiden. Varje steg är utformat för att vara tydligt och koncist så att du enkelt kan implementera det.
## Steg 1: Konfigurera din projektkatalog
Innan du börjar koda är det en bra idé att organisera dina filer. Nu skapar vi en katalog för våra Excel-filer.
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
// Skapa katalog om den inte redan finns.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Här anger vi en sökväg för vår dokumentkatalog. Om katalogen inte finns skapar vi den. Detta säkerställer att alla våra genererade filer har en angiven hemadress.
## Steg 2: Skapa en ny arbetsbok
Nu är det dags att skapa en Excel-arbetsbok där vi ska lägga till vår Spinner-kontroll.
```csharp
// Skapa en ny arbetsbok.
Workbook excelbook = new Workbook();
```
De `Workbook` klassen representerar en Excel-fil. Genom att instansiera den skapar vi en ny arbetsbok som är redo för ändringar.
## Steg 3: Öppna det första arbetsbladet
Vi lägger till vår Spinner i det första arbetsbladet i arbetsboken.
```csharp
// Hämta det första arbetsbladet.
Worksheet worksheet = excelbook.Worksheets[0];
```
Den här raden öppnar det första kalkylbladet (index 0) från vår arbetsbok. Du kan ha flera kalkylblad, men i det här exemplet håller vi det enkelt.
## Steg 4: Arbeta med celler
Nu ska vi arbeta med cellerna i vårt kalkylblad. Vi ska ange några värden och stilar.
```csharp
// Hämta kalkylbladets celler.
Cells cells = worksheet.Cells;
// Mata in ett strängvärde i cellen A1.
cells["A1"].PutValue("Select Value:");
// Ange teckenfärgen för cellen.
cells["A1"].GetStyle().Font.Color = Color.Red;
// Ställ in teckensnittet i fetstil.
cells["A1"].GetStyle().Font.IsBold = true;
// Mata in värdet i cell A2.
cells["A2"].PutValue(0);
```
Här fyller vi cell A1 med en prompt, applicerar en röd färg och gör texten fetstil. Vi ställer också in cell A2 till ett initialt värde på 0, vilket kommer att länkas till vår Spinner.
## Steg 5: Stilisera A2-cellen
Nu ska vi tillämpa några stilar på A2-cellen för att göra den mer visuellt tilltalande.
```csharp
// Ställ in skuggningsfärgen på svart med en solid bakgrund.
cells["A2"].GetStyle().ForegroundColor = Color.Black;
cells["A2"].GetStyle().Pattern = BackgroundType.Solid;
// Ange teckenfärgen för cellen.
cells["A2"].GetStyle().Font.Color = Color.White;
// Ställ in teckensnittet i fetstil.
cells["A2"].GetStyle().Font.IsBold = true;
```
Vi lägger till en svart bakgrund med ett heltäckande mönster i cell A2 och ställer in teckenfärgen på vit. Denna kontrast kommer att få den att sticka ut i kalkylbladet.
## Steg 6: Lägg till spinnerkontrollen
Nu är vi redo att lägga till Spinner-kontrollen i vårt kalkylblad.
```csharp
// Lägg till en snurrningskontroll.
Aspose.Cells.Drawing.Spinner spinner = excelbook.Worksheets[0].Shapes.AddSpinner(1, 0, 1, 0, 20, 18);
```
Den här raden lägger till en Spinner-kontroll i kalkylbladet. Parametrarna anger spinnerns position och storlek (rad, kolumn, bredd, höjd).
## Steg 7: Konfigurera spinneregenskaperna
Låt oss anpassa Spinnerns beteende efter våra behov.
```csharp
// Ange placeringstyp för spinnaren.
spinner.Placement = PlacementType.FreeFloating;
// Ange den länkade cellen för kontrollen.
spinner.LinkedCell = "A2";
// Ställ in det maximala värdet.
spinner.Max = 10;
// Ställ in minimivärdet.
spinner.Min = 0;
// Ställ in stegändringen för kontrollen.
spinner.IncrementalChange = 2;
// Ställ in den på 3D-skuggning.
spinner.Shadow = true;
```
Här ställer vi in egenskaperna för Spinnern. Vi länkar den till cell A2, vilket gör att den kan styra värdet som visas där. Minimi- och maximivärdena definierar det område som Spinnern kan arbeta inom, medan den stegvisa ändringen anger hur mycket värdet ändras med varje klick. Att lägga till 3D-skuggning ger den ett polerat utseende.
## Steg 8: Spara Excel-filen
Slutligen, låt oss spara vår Excel-arbetsbok med Spinnern inkluderad.
```csharp
// Spara Excel-filen.
excelbook.Save(dataDir + "book1.out.xls");
```
Det här kommandot sparar arbetsboken i den angivna katalogen. Du kan ändra filnamnet efter behov.
## Slutsats
Och där har du det! Du har lagt till en Spinner-kontroll i ett Excel-ark med hjälp av Aspose.Cells för .NET. Detta interaktiva element förbättrar användarupplevelsen genom att möjliggöra snabba justeringar av värden. Oavsett om du skapar ett dynamiskt rapporteringsverktyg eller ett datainmatningsformulär kan Spinner-kontrollen vara ett värdefullt tillägg. 
## Vanliga frågor
### Vad är en Spinner-kontroll i Excel?
En rotationskontroll låter användare enkelt öka eller minska ett numeriskt värde, vilket ger ett intuitivt sätt att göra val.
### Kan jag anpassa Spinnerns utseende?
Ja, du kan ändra dess storlek, position och till och med dess 3D-skuggning för ett mer polerat utseende.
### Behöver jag en licens för att använda Aspose.Cells?
Aspose.Cells erbjuder en gratis provperiod, men en betald licens krävs för produktionsanvändning. Kolla in [köpoptioner](https://purchase.aspose.com/buy).
### Hur kan jag få hjälp med Aspose.Cells?
För support, besök [Aspose-forumet](https://forum.aspose.com/c/cells/9) där du kan ställa frågor och få svar.
### Är det möjligt att lägga till flera Spinners i samma arbetsblad?
Absolut! Du kan lägga till så många spinnare som behövs genom att följa samma steg för varje kontroll.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}