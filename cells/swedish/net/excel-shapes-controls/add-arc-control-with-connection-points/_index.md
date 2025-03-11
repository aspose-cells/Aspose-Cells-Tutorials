---
title: Lägg till bågkontroll med anslutningspunkter
linktitle: Lägg till bågkontroll med anslutningspunkter
second_title: Aspose.Cells .NET Excel Processing API
description: Upptäck hur du lägger till bågkontroller med anslutningspunkter med Aspose.Cells för .NET i den här detaljerade guiden.
weight: 27
url: /sv/net/excel-shapes-controls/add-arc-control-with-connection-points/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till bågkontroll med anslutningspunkter

## Introduktion
När det gäller att skapa visuellt engagerande Excel-rapporter spelar illustrationer en viktig roll. Oavsett om du skapar en finansiell rapport eller en projektuppdelning, kan användning av former som bågar lägga till djup och tydlighet till din datapresentation. Idag dyker vi djupt in i hur man använder Aspose.Cells för .NET för att lägga till bågkontroller med anslutningspunkter i dina Excel-kalkylblad. Så om du någonsin har undrat hur du kan piffa upp dina kalkylblad eller få din data att sjunga, läs vidare!
## Förutsättningar
Innan vi hoppar in i spänningen med kodning, låt oss se till att du är klar. Här är vad du behöver:
1. .NET Framework: Se till att du har en kompatibel version installerad. Aspose.Cells fungerar med flera versioner, inklusive .NET Core.
2.  Aspose.Cells för .NET: Du måste ladda ner och installera Aspose.Cells-biblioteket. Du kan enkelt ta den från[nedladdningslänk](https://releases.aspose.com/cells/net/).
3. En bra IDE: Visual Studio, den trogna följeslagaren till alla .NET-utvecklare, hjälper till att effektivisera din kodningsupplevelse.
4. Grundläggande kunskaper om C#: Om du känner dig runt C#, kommer du att tycka att denna handledning fungerar smidigt.
5. Tillgång till din dokumentkatalog: Vet var du ska spara dina Excel-filer. Det är viktigt för att organisera din produktion effektivt.
## Importera paket
Nästa steg är att se till att du har rätt paket importerade till ditt projekt. Aspose.Cells för .NET har olika funktioner, så vi håller det enkelt. Här är vad du behöver inkludera:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Dessa namnutrymmen ger dig tillgång till alla ritfunktioner och cellhanteringsfunktioner som du kommer att använda i den här guiden.
## Steg 1: Konfigurera din dokumentkatalog
Först till kvarn – låt oss skapa en katalog där du kommer att spara dessa glänsande nya Excel-filer. Så här gör vi:
```csharp
string dataDir = "Your Document Directory";
// Skapa katalog om den inte redan finns.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Denna kodbit kontrollerar om din angivna mapp finns. Om inte, skapar det en. Enkelt, eller hur? Det är alltid bra att ha en specifik plats för dina filer för att undvika skräp.
## Steg 2: Instantiera en arbetsbok
Nu när vi har vår katalog redo, låt oss skapa en ny Excel-arbetsbok.
```csharp
Workbook excelbook = new Workbook();
```
 Genom att ringa till`Workbook` konstruktör, du säger i huvudsak, "Hej, låt oss starta en ny Excel-fil!" Detta kommer att vara arbetsytan för alla dina former och data.
## Steg 3: Lägga till den första bågformen
Det är här det roliga börjar! Låt oss lägga till vår första bågform.
```csharp
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
Denna kodrad lägger till en bågeform till det första kalkylbladet. Parametrarna anger bågens koordinater och vinklarna som definierar dess krökning. 
## Steg 4: Anpassa bågens utseende
En blank bågeform är som en duk utan färg – den behöver lite känsla!
### Ställ in bågfyllningsfärg
```csharp
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
```
Detta gör bågen fast blå. Du kan ändra färgen till vilken nyans du vill genom att byta ut`Color.Blue` för en annan färg.
### Ställ in bågplacering
```csharp
arc1.Placement = PlacementType.FreeFloating;
```
Genom att ställa in placeringen på "FreeFloating" kan bågen röra sig oberoende av cellgränser, vilket ger dig flexibilitet i positioneringen.
### Justera linjevikt och stil
```csharp
arc1.Line.Weight = 1;      
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Här definierar du linjens vikt och stil, vilket gör den mer framträdande och visuellt tilltalande.
## Steg 5: Lägga till ytterligare en bågform
Varför stanna vid en? Låt oss lägga till ytterligare en bågform för att berika vår Excel-visual.
```csharp
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Liksom den första bågen läggs den här till i en annan position - det är här designens magi äger rum!
## Steg 6: Anpassa den andra bågen
Låt oss ge vår andra båge lite personlighet också!
### Ändra båglinjefärg
```csharp
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
```
Vi håller det konsekvent med en blå färg, men du kan alltid mixa och matcha för att se vad som passar bäst i din design!
### Ställ in egenskaper som liknar den första bågen
Se till att replikera dessa estetiska val:
```csharp
arc2.Placement = PlacementType.FreeFloating;
arc2.Line.Weight = 1;           
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Här ser du helt enkelt till att den andra bågen matchar den första, vilket skapar ett sammanhängande utseende genom hela ditt arbetsblad.
## Steg 7: Spara din arbetsbok
Inget mästerverk är komplett utan att bli räddat, eller hur? Dags att skriva dina bågar i en Excel-fil.
```csharp
excelbook.Save(dataDir + "book1.out.xls");
```
Den här raden sparar dina nyskapade bågar i en Excel-fil med namnet "book1.out.xls" i din angivna katalog.
## Slutsats
Grattis! Du har precis bemästrat grunderna för att lägga till bågkontroller med anslutningspunkter i dina Excel-ark med Aspose.Cells för .NET. Denna funktion förskönar inte bara dina kalkylblad utan kan också göra komplexa data lättare att smälta. Oavsett om du är en erfaren utvecklare eller precis har börjat, kan dessa visuella element förvandla dina rapporter från intetsägande till storslagna.
## FAQ's
### Vad är Aspose.Cells?
Aspose.Cells är ett kraftfullt .NET-bibliotek som låter utvecklare skapa och manipulera Excel-filer programmatiskt.
### Kan jag använda Aspose.Cells gratis?
 Ja! Du kan prova en gratis provperiod. Besök[denna länk](https://releases.aspose.com/) att börja.
### Hur lägger jag till andra former förutom bågar?
Du kan använda olika klasser som är tillgängliga i namnområdet Aspose.Cells.Drawing för att lägga till olika former som rektanglar, cirklar och mer.
### Vilken typ av filer kan jag skapa med Aspose.Cells?
Du kan skapa och manipulera olika Excel-format inklusive XLS, XLSX, CSV och mer.
### Finns teknisk support tillgänglig för Aspose.Cells?
 Absolut! Du kan komma åt[Aspose supportforum](https://forum.aspose.com/c/cells/9) för hjälp.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
