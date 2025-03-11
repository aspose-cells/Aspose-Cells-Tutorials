---
title: Lägg till Oval till kalkylblad i Excel
linktitle: Lägg till Oval till kalkylblad i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du lägger till en oval i ett Excel-kalkylblad med Aspose.Cells för .NET. Steg-för-steg-guide med detaljerade kodförklaringar.
weight: 17
url: /sv/net/excel-shapes-controls/add-oval-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till Oval till kalkylblad i Excel

## Introduktion
Att skapa fantastiska och interaktiva Excel-filer kan involvera mer än bara siffror och formler. Former som ovaler kan lägga till ett visuellt tilltal eller tillhandahålla funktionella element i dina kalkylblad. I den här handledningen kommer vi att utforska hur man använder Aspose.Cells för .NET för att lägga till ovaler till ett Excel-kalkylblad programmatiskt. Oavsett om du vill lägga till lite känsla eller funktionalitet, har vi en steg-för-steg-guide som bryter ner allt.
## Förutsättningar
Innan du dyker in i koden finns det några saker du måste ha på plats:
1.  Aspose.Cells för .NET Library: Du kan ladda ner det från[här](https://releases.aspose.com/cells/net/) eller installera det med NuGet i Visual Studio.
2. Utvecklingsmiljö: AC# IDE som Visual Studio.
3. Grundläggande förståelse för C#: Du bör vara bekant med grundläggande kodningskoncept i C#.
 Kom också ihåg att ställa in ditt projekt genom att installera Aspose.Cells for .NET-biblioteket. Om du inte har en licens ännu kan du ansöka om en[tillfällig licens](https://purchase.aspose.com/temporary-license/) eller använd[gratis provperiod](https://releases.aspose.com/) version.
## Importera paket
Innan du skriver någon kod, se till att du har inkluderat de nödvändiga namnrymden. Här är C#-kodavsnittet för att säkerställa att du använder rätt bibliotek:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Steg 1: Konfigurera din katalog
Det första steget för att lägga till en oval till ett Excel-ark är att ange var din Excel-fil ska sparas. Låt oss definiera katalogsökvägen och se till att katalogen finns innan vi sparar vårt arbete.

Vi skapar en katalogsökväg och verifierar om den finns. Om mappen inte finns skapas den.
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
// Skapa katalog om den inte redan finns.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Detta steg är avgörande eftersom det säkerställer att din fil sparas på rätt plats och att du inte stöter på problem med filsökvägar senare.
## Steg 2: Initiera en ny arbetsbok
Därefter måste vi skapa en ny arbetsbok där vi lägger till våra ovala former. Arbetsboken representerar en Excel-fil och vi kan lägga till innehåll eller former i den.

 I det här steget instansierar vi en ny`Workbook` objekt som kommer att fungera som vår Excel-filbehållare.
```csharp
// Instantiera en ny arbetsbok.
Workbook excelbook = new Workbook();
```
## Steg 3: Lägg till den första ovala formen
Nu kommer den roliga delen - att lägga till en oval form till arbetsbladet. Denna ovala kan representera ett visuellt element som en knapp eller en höjdpunkt. Vi börjar med att lägga till den första ovala formen i det första kalkylbladet i vår arbetsbok.

 Här använder vi`Shapes.AddOval()` metod för att skapa en oval på kalkylbladet vid en specifik rad och kolumn.
```csharp
// Lägg till en oval form.
Aspose.Cells.Drawing.Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```
 Parametrarna inuti`AddOval()` är följande:
- De två första siffrorna representerar raden och kolumnen för det övre vänstra hörnet av ovalen.
- De följande två siffrorna representerar ovalens höjd och bredd.
## Steg 4: Ställ in ovalens placering och stil
 När ovalen har skapats kan vi ställa in dess position, linjevikt och streckstil. De`Placement` egenskapen bestämmer hur ovalen beter sig när du ändrar storlek på eller flyttar celler i kalkylbladet.

Vi gör ovalen fritt flytande och anpassar dess utseende.
```csharp
// Ställ in placeringen av ovalen.
oval1.Placement = PlacementType.FreeFloating;
// Ställ in linjevikten.
oval1.Line.Weight = 1;
// Ställ in streckstilen för ovalen.
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Detta gör att ovalen kan röra sig fritt inom kalkylbladet, och dess linjevikt och stil är inställda för visuell konsekvens.
## Steg 5: Lägg till ytterligare en oval (cirkel) form
Varför stanna vid en? I det här steget lägger vi till ytterligare en oval form, denna gång skapar vi en perfekt cirkel genom att göra höjden och bredden lika.

Vi skapar en annan oval, placerar den på en annan plats och säkerställer att den har en cirkulär form genom att ställa in lika höjd och bredd.
```csharp
// Lägg till ytterligare en oval (cirkel) form.
Aspose.Cells.Drawing.Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```
## Steg 6: Style den andra ovalen
Precis som tidigare kommer vi att justera placeringen, vikten och streckstilen för denna andra ovala (eller cirkel).

Vi tillämpar liknande egenskaper på den andra ovalen för att matcha stilen på den första.
```csharp
// Ställ in placeringen av ovalen.
oval2.Placement = PlacementType.FreeFloating;
// Ställ in linjevikten.
oval2.Line.Weight = 1;
// Ställ in streckstilen för ovalen.
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Steg 7: Spara arbetsboken
Slutligen måste vi spara arbetsboken med de ovaler vi just har lagt till. Att spara filen säkerställer att alla våra ändringar lagras.

Vi sparar arbetsboken till den katalogsökväg vi definierade tidigare.
```csharp
// Spara excel-filen.
excelbook.Save(dataDir + "book1.out.xls");
```
Och det är det! Du har framgångsrikt lagt till ovaler till ditt Excel-kalkylblad och sparat filen.
## Slutsats
Att lägga till former som ovaler till ett Excel-ark med Aspose.Cells för .NET är inte bara enkelt utan också ett roligt sätt att förbättra dina kalkylblad med ytterligare visuella element. Oavsett om det är för designändamål eller för att lägga till klickbara element, kan former spela en viktig roll för hur dina Excel-filer ser ut och fungerar. Så nästa gång du arbetar med ett projekt som kräver interaktiva eller visuellt tilltalande Excel-ark, vet du exakt hur du lägger till de perfekta ovalarna!
## FAQ's
### Kan jag lägga till andra former som rektanglar eller linjer med Aspose.Cells för .NET?
 Ja, du kan lägga till olika former som rektanglar, linjer och pilar med hjälp av`Shapes` samling i Aspose.Cells.
### Är det möjligt att ändra storlek på ovalerna efter att ha lagt till dem?
Absolut! Du kan ändra höjd- och breddegenskaperna för ovalerna efter att ha lagt till dem.
### Vilka filformat kan jag spara arbetsboken i förutom XLS?
Aspose.Cells stöder flera format som XLSX, CSV och PDF, bland andra.
### Kan jag ändra färgen på ovalens kontur?
 Ja, du kan ändra ovalens linjefärg med hjälp av`Line.Color` egendom.
### Är det nödvändigt att ha en licens för Aspose.Cells?
 Även om du kan prova Aspose.Cells med en gratis provperiod, behöver du en[licens](https://purchase.aspose.com/buy) för långvarig användning eller för åtkomst till avancerade funktioner.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
