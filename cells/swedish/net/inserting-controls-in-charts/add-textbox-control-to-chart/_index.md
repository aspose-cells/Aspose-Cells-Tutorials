---
title: Lägg till TextBox Control till diagrammet
linktitle: Lägg till TextBox Control till diagrammet
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du lägger till en textruta i diagram i Excel med Aspose.Cells för .NET. Förbättra din datavisualisering utan ansträngning.
weight: 12
url: /sv/net/inserting-controls-in-charts/add-textbox-control-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till TextBox Control till diagrammet

## Introduktion

Att skapa dynamiska och visuellt tilltalande diagram i Excel är ett fantastiskt sätt att representera data effektivt. En fiffig funktion du kan använda är att lägga till en textruta i ett diagram. Med Aspose.Cells för .NET blir denna uppgift enkel och rolig! I den här guiden kommer vi att gå igenom processen att integrera en textruta i ditt diagram steg för steg. Oavsett om du är en erfaren utvecklare eller precis har börjat, kommer den här handledningen att ge dig alla verktyg du behöver för att förbättra dina Excel-diagram. Så, är du redo att dyka in?

## Förutsättningar

Innan vi går in på kodning finns det några saker du bör ha på plats:

- Grundläggande förståelse för C#: En grundläggande förståelse för C#-programmering kommer att vara till hjälp. Oroa dig inte; du behöver inte vara expert, bara bekväm att navigera i syntaxen.
-  Installerat Aspose.Cells-bibliotek: Se till att du har Aspose.Cells for .NET-biblioteket installerat. Du kan ladda ner den från[här](https://releases.aspose.com/cells/net/) om du inte redan har gjort det.
- Visual Studio: Bekantskap med Visual Studio eller någon IDE som du föredrar att använda för .NET-ramverket är viktigt.
- En befintlig Excel-fil: I det här exemplet kommer vi att arbeta med en befintlig Excel-fil som heter "sampleAddingTextBoxControlInChart.xls". Du kan skapa en eller ladda ner ett prov.

Nu när vi har allt på plats, låt oss gå till kodningsdelen!

## Importera paket

Först och främst måste vi importera de nödvändiga Aspose.Cells-namnrymden till vårt C#-projekt. Du kan göra detta enkelt genom att inkludera följande rader överst i din kodfil:

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
 Ersätta`"Your Document Directory"` och`"Your Output Directory"` med de faktiska sökvägarna på ditt system.

## Steg 2: Öppna den befintliga Excel-filen

Därefter måste vi öppna Excel-filen som innehåller diagrammet vi vill ändra. Detta gör att vi kan hämta diagrammet och göra ändringar.

```csharp
// Öppna den befintliga filen.
Workbook workbook = new Workbook(sourceDir + "sampleAddingTextBoxControlInChart.xls");
```
Den här raden initierar ett nytt arbetsboksobjekt med vår specificerade fil.

## Steg 3: Öppna diagrammet i arbetsbladet

Eftersom diagram i Excel lagras i ett kalkylblad måste vi först komma åt kalkylbladet och sedan få önskat diagram. För det här exemplet kommer vi åt det första diagrammet i det första kalkylbladet.

```csharp
// Få designerdiagrammet i det första arket.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```
Genom att ändra indexvärdet kan du välja olika kalkylblad eller diagram om din fil har fler.

## Steg 4: Lägg till en ny textruta i diagrammet

Nu är vi redo att lägga till vår TextBox. Vi anger dess position och storlek när du skapar den.

```csharp
// Lägg till en ny textruta i diagrammet.
Aspose.Cells.Drawing.TextBox textbox0 = chart.Shapes.AddTextBoxInChart(400, 1100, 350, 2550);
```
det här kommandot definierar parametrarna platsen (x, y) och storleken (bredd, höjd) för textrutan i diagrammet. Justera dessa värden baserat på dina specifika layoutbehov.

## Steg 5: Ställ in texten för textrutan

När TextBox är på plats är det dags att fylla den med innehåll. Du kan lägga till vilken text som helst som du anser vara nödvändig för ditt diagram.

```csharp
// Fyll i texten.
textbox0.Text = "Sales By Region";
```
Ersätt gärna "Försäljning per region" med vilken text som helst som är relevant för dina uppgifter.

## Steg 6: Justera TextBox-egenskaper

Låt oss nu få vår TextBox att se bra ut! Du kan anpassa olika egenskaper som teckensnittsfärg, storlek och stil.

```csharp
// Ställ in teckensnittsfärgen.
textbox0.Font.Color = Color.Maroon; // Byt till önskad färg

// Ställ in teckensnittet till fetstil.
textbox0.Font.IsBold = true;

// Ställ in teckenstorleken.
textbox0.Font.Size = 14;

// Ställ in teckensnittsattributet till kursiv.
textbox0.Font.IsItalic = true;
```

Var och en av dessa rader ändrar utseendet på texten i din textruta, vilket förbättrar synlighet och tilltal.

## Steg 7: Formatera textrutans utseende

Det är också viktigt att formatera textrutans bakgrund och kant. Detta gör att den sticker ut på diagrammet.

```csharp
// Hämta fyllningsformatet för textrutan.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;

// Hämta textrutans linjeformattyp.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;

// Ställ in linjevikten.
lineformat.Weight = 2;

// Ställ in streckstilen till solid.
lineformat.DashStyle = Aspose.Cells.Drawing.MsoLineDashStyle.Solid;
```

Dessa alternativ låter dig ställa in bakgrundsfyllningen för TextBox och anpassa dess kant.

## Steg 8: Spara den modifierade Excel-filen

Det sista steget är att spara ändringarna du har gjort i en ny Excel-fil. Detta kommer att säkerställa att din originalfil förblir orörd.

```csharp
// Spara excel-filen.
workbook.Save(outputDir + "outputAddingTextBoxControlInChart.xls");
```
 Ersätta`"outputAddingTextBoxControlInChart.xls"` med vilket filnamn du föredrar.

## Slutsats

Grattis! Du har framgångsrikt lagt till en TextBox-kontroll till ett diagram med Aspose.Cells för .NET. Denna enkla men effektiva förändring kan göra dina diagram mer informativa och visuellt tilltalande. Datarepresentation är nyckeln till effektiv kommunikation, och med verktyg som Aspose har du kraften att förbättra den presentationen med minimal ansträngning.

## FAQ's

### Vad är Aspose.Cells för .NET?
Aspose.Cells för .NET är ett kraftfullt bibliotek för att skapa, manipulera och konvertera Excel-filer utan att behöva lita på Microsoft Excel.

### Kan jag lägga till flera textrutor i ett enda diagram?
Ja! Du kan lägga till så många TextBoxar som du behöver genom att upprepa stegen för att skapa TextBox med olika positioner.

### Är Aspose.Cells gratis att använda?
Aspose.Cells är ett betalbibliotek, men du kan ladda ner en gratis testversion från[här](https://releases.aspose.com/).

### Var kan jag hitta mer dokumentation om Aspose.Cells?
 Du kan få tillgång till omfattande dokumentation[här](https://reference.aspose.com/cells/net/).

### Hur får jag support om jag stöter på problem?
 Du kan söka hjälp via Asposes supportforum[här](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
