---
"description": "Lär dig hur du lägger till en textbox i diagram i Excel med Aspose.Cells för .NET. Förbättra din datavisualisering utan ansträngning."
"linktitle": "Lägg till textboxkontroll i diagram"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Lägg till textboxkontroll i diagram"
"url": "/sv/net/inserting-controls-in-charts/add-textbox-control-to-chart/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till textboxkontroll i diagram

## Introduktion

Att skapa dynamiska och visuellt tilltalande diagram i Excel är ett fantastiskt sätt att representera data effektivt. En smart funktion du kan använda är att lägga till en textbox i ett diagram. Med Aspose.Cells för .NET blir den här uppgiften enkel och rolig! I den här guiden guidar vi dig genom processen att integrera en textbox i ditt diagram steg för steg. Oavsett om du är en erfaren utvecklare eller precis har börjat, kommer den här handledningen att ge dig alla verktyg du behöver för att förbättra dina Excel-diagram. Så, är du redo att dyka in?

## Förkunskapskrav

Innan vi börjar med kodning finns det några saker du bör ha på plats:

- Grundläggande förståelse för C#: Grundläggande kunskaper i C#-programmering är till hjälp. Oroa dig inte; du behöver inte vara expert, bara vara bekväm med att navigera syntaxen.
- Installerat Aspose.Cells-bibliotek: Se till att du har Aspose.Cells för .NET-biblioteket installerat. Du kan ladda ner det från [här](https://releases.aspose.com/cells/net/) om du inte redan har gjort det.
- Visual Studio: Det är viktigt att du har goda kunskaper om Visual Studio eller någon annan IDE som du föredrar att använda för .NET Framework.
- En befintlig Excel-fil: I det här exemplet arbetar vi med en befintlig Excel-fil med namnet "sampleAddingTextBoxControlInChart.xls". Du kan skapa en eller ladda ner ett exempel.

Nu när vi har allt på plats, låt oss gå vidare till kodningsdelen!

## Importera paket

Först och främst måste vi importera de nödvändiga Aspose.Cells-namnrymderna till vårt C#-projekt. Du kan enkelt göra detta genom att inkludera följande rader högst upp i din kodfil:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using System.Drawing;
```

## Steg 1: Definiera dina käll- och utdatakataloger

Innan vi börjar arbeta med Excel-filen är det viktigt att definiera var din indatafil finns och var du vill spara utdatafilen. Detta hjälper till att hålla ditt projekt organiserat.

```csharp
// Källkatalog
string sourceDir = "Your Document Directory";

// Utdatakatalog
string outputDir = "Your Output Directory";
```
Ersätta `"Your Document Directory"` och `"Your Output Directory"` med de faktiska sökvägarna på ditt system.

## Steg 2: Öppna den befintliga Excel-filen

Sedan behöver vi öppna Excel-filen som innehåller diagrammet vi vill ändra. Detta gör att vi kan hämta diagrammet och göra ändringar.

```csharp
// Öppna den befintliga filen.
Workbook workbook = new Workbook(sourceDir + "sampleAddingTextBoxControlInChart.xls");
```
Den här raden initierar ett nytt arbetsboksobjekt med vår angivna fil.

## Steg 3: Öppna diagrammet i arbetsbladet

Eftersom diagram i Excel lagras i ett kalkylblad måste vi först komma åt kalkylbladet och sedan hämta önskat diagram. I det här exemplet kommer vi att komma åt det första diagrammet i det första kalkylbladet.

```csharp
// Hämta designerdiagrammet i det första arket.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```
Genom att ändra indexvärdet kan du välja olika kalkylblad eller diagram om din fil har fler.

## Steg 4: Lägg till en ny textruta i diagrammet

Nu är vi redo att lägga till vår textruta. Vi anger dess position och storlek när vi skapar den.

```csharp
// Lägg till en ny textruta i diagrammet.
Aspose.Cells.Drawing.TextBox textbox0 = chart.Shapes.AddTextBoxInChart(400, 1100, 350, 2550);
```
I det här kommandot definierar parametrarna platsen (x, y) och storleken (bredd, höjd) för textrutan i diagrammet. Justera dessa värden baserat på dina specifika layoutbehov.

## Steg 5: Ange texten för textrutan

När textrutan är på plats är det dags att fylla den med innehåll. Du kan lägga till vilken text du anser nödvändig för ditt diagram.

```csharp
// Fyll i texten.
textbox0.Text = "Sales By Region";
```
Du kan gärna ersätta "Försäljning per region" med valfri text som är relevant för dina data.

## Steg 6: Justera textrutans egenskaper

Nu ska vi få vår textruta att se bra ut! Du kan anpassa olika egenskaper som teckensnittsfärg, storlek och stil.

```csharp
// Ställ in teckenfärgen.
textbox0.Font.Color = Color.Maroon; // Ändra till önskad färg

// Ställ in teckensnittet på fetstil.
textbox0.Font.IsBold = true;

// Ställ in teckenstorleken.
textbox0.Font.Size = 14;

// Ställ in teckensnittsattributet till kursiv.
textbox0.Font.IsItalic = true;
```

Var och en av dessa rader modifierar textens utseende i din textruta, vilket förbättrar synligheten och attraktionskraften.

## Steg 7: Formatera textrutans utseende

Det är också viktigt att formatera textrutans bakgrund och kantlinje. Detta gör att den syns tydligt i diagrammet.

```csharp
// Hämta fyllningsformatet för textrutan.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;

// Hämta radformattypen för textrutan.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;

// Ställ in linjetjockleken.
lineformat.Weight = 2;

// Ställ in streckstilen till heldragen.
lineformat.DashStyle = Aspose.Cells.Drawing.MsoLineDashStyle.Solid;
```

Med dessa alternativ kan du ställa in bakgrundsfyllningen för textrutan och anpassa dess kantlinje.

## Steg 8: Spara den modifierade Excel-filen

Det sista steget är att spara de ändringar du har gjort i en ny Excel-fil. Detta säkerställer att din ursprungliga fil förblir orörd.

```csharp
// Spara Excel-filen.
workbook.Save(outputDir + "outputAddingTextBoxControlInChart.xls");
```
Ersätta `"outputAddingTextBoxControlInChart.xls"` med vilket filnamn du föredrar.

## Slutsats

Grattis! Du har lagt till en TextBox-kontroll i ett diagram med hjälp av Aspose.Cells för .NET. Denna enkla men effektiva ändring kan göra dina diagram mer informativa och visuellt tilltalande. Datarepresentation är nyckeln till effektiv kommunikation, och med verktyg som Aspose har du möjlighet att förbättra presentationen med minimal ansträngning.

## Vanliga frågor

### Vad är Aspose.Cells för .NET?
Aspose.Cells för .NET är ett kraftfullt bibliotek för att skapa, manipulera och konvertera Excel-filer utan att behöva förlita sig på Microsoft Excel.

### Kan jag lägga till flera textrutor i ett enda diagram?
Ja! Du kan lägga till så många textrutor som du behöver genom att upprepa stegen för att skapa textrutor med olika positioner.

### Är Aspose.Cells gratis att använda?
Aspose.Cells är ett betalt bibliotek, men du kan ladda ner en gratis testversion från [här](https://releases.aspose.com/).

### Var kan jag hitta mer dokumentation om Aspose.Cells?
Du kan få tillgång till omfattande dokumentation [här](https://reference.aspose.com/cells/net/).

### Hur får jag support om jag stöter på problem?
Du kan söka hjälp via Asposes supportforum [här](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}