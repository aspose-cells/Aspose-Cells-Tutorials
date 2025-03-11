---
title: Lägg till Spinner Control till kalkylblad i Excel
linktitle: Lägg till Spinner Control till kalkylblad i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du lägger till en Spinner-kontroll till ett Excel-kalkylblad med Aspose.Cells för .NET i denna steg-för-steg-handledning.
weight: 23
url: /sv/net/excel-shapes-controls/add-spinner-control-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till Spinner Control till kalkylblad i Excel

## Introduktion
Om du dyker in i en värld av Excel-automatisering med .NET, har du förmodligen stött på behovet av mer interaktiva kontroller i dina kalkylblad. En sådan kontroll är Spinnern, som tillåter användare att enkelt öka eller minska ett värde. I den här handledningen kommer vi att utforska hur man lägger till en Spinner-kontroll i ett Excel-kalkylblad med Aspose.Cells för .NET. Vi delar upp det i lättsmälta steg så att du kan följa med sömlöst. 
## Förutsättningar
Innan vi hoppar in i koden, låt oss se till att du har allt inställt för en smidig upplevelse:
1.  Aspose.Cells för .NET: Se till att du har Aspose.Cells-biblioteket. Om du inte har installerat det ännu kan du hämta den senaste versionen från[nedladdningslänk](https://releases.aspose.com/cells/net/).
2. Visual Studio: Du bör ha en fungerande installation av Visual Studio eller någon annan .NET IDE som du föredrar.
3. Grundläggande kunskaper om C#: Bekantskap med C#-programmering hjälper dig att enkelt förstå kodavsnitten. Om du precis har börjat, oroa dig inte! Jag går igenom varje del.
## Importera paket
För att använda Aspose.Cells i ditt projekt måste du importera de nödvändiga namnrymden. Så här kan du ställa in din miljö:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Dessa namnutrymmen ger dig tillgång till kärnfunktionerna i Aspose.Cells, inklusive manipulering av arbetsbok och ritfunktioner för former som Spinner.
Nu när vi har täckt förutsättningarna och importerat de nödvändiga paketen, låt oss dyka in i steg-för-steg-guiden. Varje steg är utformat för att vara tydligt och kortfattat så att du enkelt kan implementera det.
## Steg 1: Konfigurera din projektkatalog
Innan du börjar koda är det bra att organisera dina filer. Låt oss skapa en katalog för våra Excel-filer.
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
// Skapa katalog om den inte redan finns.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Här anger vi en sökväg för vår dokumentkatalog. Om katalogen inte finns skapar vi den. Detta säkerställer att alla våra genererade filer har ett avsett hem.
## Steg 2: Skapa en ny arbetsbok
Nu är det dags att skapa en Excel-arbetsbok där vi lägger till vår Spinner-kontroll.
```csharp
// Instantiera en ny arbetsbok.
Workbook excelbook = new Workbook();
```
 De`Workbook` klass representerar en Excel-fil. Genom att instansiera den skapar vi en ny arbetsbok redo för ändringar.
## Steg 3: Öppna det första arbetsbladet
Vi lägger till vår Spinner i det första kalkylbladet i arbetsboken.
```csharp
// Skaffa det första arbetsbladet.
Worksheet worksheet = excelbook.Worksheets[0];
```
Den här raden kommer åt det första kalkylbladet (index 0) från vår arbetsbok. Du kan ha flera kalkylblad, men för det här exemplet ska vi hålla det enkelt.
## Steg 4: Arbeta med celler
Låt oss sedan arbeta med cellerna i vårt kalkylblad. Vi kommer att sätta några värderingar och stilar.
```csharp
// Hämta kalkylbladets celler.
Cells cells = worksheet.Cells;
// Mata in ett strängvärde i A1-cellen.
cells["A1"].PutValue("Select Value:");
// Ställ in cellens teckensnittsfärg.
cells["A1"].GetStyle().Font.Color = Color.Red;
// Ställ in teckensnittstexten i fet stil.
cells["A1"].GetStyle().Font.IsBold = true;
// Mata in värde i A2-cell.
cells["A2"].PutValue(0);
```
Här fyller vi cell A1 med en prompt, applicerar en röd färg och gör texten fet. Vi ställer också in cell A2 till ett initialt värde på 0, vilket kommer att kopplas till vår Spinner.
## Steg 5: Style A2-cellen
Låt oss sedan tillämpa några stilar på A2-cellen för att göra den mer visuellt tilltalande.
```csharp
// Ställ in skuggningsfärgen till svart med solid bakgrund.
cells["A2"].GetStyle().ForegroundColor = Color.Black;
cells["A2"].GetStyle().Pattern = BackgroundType.Solid;
// Ställ in cellens teckensnittsfärg.
cells["A2"].GetStyle().Font.Color = Color.White;
// Ställ in teckensnittstexten i fet stil.
cells["A2"].GetStyle().Font.IsBold = true;
```
Vi lägger till en svart bakgrund med ett solidt mönster i cell A2 och ställer in teckensnittsfärgen till vit. Denna kontrast kommer att få den att sticka ut på arbetsbladet.
## Steg 6: Lägg till spinnerkontrollen
Nu är vi redo att lägga till Spinner-kontrollen i vårt kalkylblad.
```csharp
// Lägg till en spinnerkontroll.
Aspose.Cells.Drawing.Spinner spinner = excelbook.Worksheets[0].Shapes.AddSpinner(1, 0, 1, 0, 20, 18);
```
Den här raden lägger till en Spinner-kontroll till kalkylbladet. Parametrarna anger spinnarens position och storlek (rad, kolumn, bredd, höjd).
## Steg 7: Konfigurera Spinner-egenskaperna
Låt oss anpassa Spinnerns beteende för att passa våra behov.
```csharp
// Ställ in placeringstypen för spinnaren.
spinner.Placement = PlacementType.FreeFloating;
// Ställ in den länkade cellen för kontrollen.
spinner.LinkedCell = "A2";
// Ställ in maxvärdet.
spinner.Max = 10;
//Ställ in minimivärdet.
spinner.Min = 0;
// Ställ in stegändringen för kontrollen.
spinner.IncrementalChange = 2;
// Ställ in 3D-skuggning.
spinner.Shadow = true;
```
Här ställer vi in Spinnerns egenskaper. Vi länkar den till cell A2, så att den kan styra värdet som visas där. Minsta och högsta värden definierar intervallet som Spinnern kan arbeta inom, medan den inkrementella förändringen anger hur mycket värdet ändras med varje klick. Genom att lägga till 3D-skuggning får den ett polerat utseende.
## Steg 8: Spara Excel-filen
Slutligen, låt oss spara vår Excel-arbetsbok med Spinnern inkluderad.
```csharp
// Spara excel-filen.
excelbook.Save(dataDir + "book1.out.xls");
```
Detta kommando sparar arbetsboken i den angivna katalogen. Du kan ändra filnamnet efter behov.
## Slutsats
Och där har du det! Du har framgångsrikt lagt till en Spinner-kontroll till ett Excel-kalkylblad med Aspose.Cells för .NET. Detta interaktiva element förbättrar användarupplevelsen genom att tillåta snabba justeringar av värden. Oavsett om du skapar ett dynamiskt rapporteringsverktyg eller ett datainmatningsformulär kan Spinner-kontrollen vara ett värdefullt tillägg. 
## FAQ's
### Vad är en Spinner-kontroll i Excel?
En Spinner-kontroll tillåter användare att enkelt öka eller minska ett numeriskt värde, vilket ger ett intuitivt sätt att göra val.
### Kan jag anpassa spinnerns utseende?
Ja, du kan ändra dess storlek, position och till och med dess 3D-skuggning för en mer polerad look.
### Behöver jag en licens för att använda Aspose.Cells?
 Aspose.Cells erbjuder en gratis provperiod, men en betald licens krävs för produktionsanvändning. Kolla in[köpa optioner](https://purchase.aspose.com/buy).
### Hur kan jag få hjälp med Aspose.Cells?
 För support, besök[Aspose forum](https://forum.aspose.com/c/cells/9) där du kan ställa frågor och hitta svar.
### Är det möjligt att lägga till flera spinnare i samma arbetsblad?
Absolut! Du kan lägga till så många spinnare som behövs genom att följa samma steg för varje kontroll.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
