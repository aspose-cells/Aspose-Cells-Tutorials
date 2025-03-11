---
title: Ange Far East & Latin Font i Excel
linktitle: Ange Far East & Latin Font i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du anger Fjärran Östern och latinska teckensnitt i Excel med Aspose.Cells för .NET i denna omfattande och lättanvända handledning.
weight: 17
url: /sv/net/excel-shape-text-modifications/specify-far-east-latin-font-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ange Far East & Latin Font i Excel

## Introduktion
Vill du förbättra dina Excel-rapporter eller dokument med specifika teckensnittskrav? Oavsett om du har att göra med flera språk eller helt enkelt strävar efter en unik estetik i dina kalkylblad, är det en avgörande färdighet att förstå hur man specificerar Fjärran Östern och latinska teckensnitt i Excel. Tur för dig, vi har en lösning! I den här handledningen utforskar vi hur man använder Aspose.Cells för .NET för att implementera den här funktionen sömlöst. Låt oss dyka in!
## Förutsättningar
Innan vi går in i det snälla, finns det några saker du måste ställa in innan du börjar med Aspose.Cells:
### .NET Framework eller .NET Core
Se till att du har .NET Framework eller .NET Core installerat på din dator. Det här biblioteket fungerar bra med båda.
### Installation av Aspose.Cells
 Du måste ladda ner Aspose.Cells-biblioteket. Du kan[ladda ner den härifrån](https://releases.aspose.com/cells/net/) . Om du inte är bekant med att installera NuGet-paket, följ[denna guide](https://www.nuget.org/).
### Integrated Development Environment (IDE)
Att ha en IDE som Visual Studio eller JetBrains Rider kan förenkla kodning, felsökning och körning av ditt projekt.
### Grundläggande kunskaper i C#
Bekantskap med C#-programmering kommer att vara mycket fördelaktigt för att följa denna handledning.
## Importera paket
Innan vi kan arbeta med Aspose.Cells måste vi importera de nödvändiga paketen till vårt projekt. Så här kan du göra det:
### Skapa ett nytt projekt
1. Öppna din IDE och skapa ett nytt konsolapplikationsprojekt.
2.  Namnge ditt projekt något beskrivande, som`FontSpecifyingApp`.
### Lägg till Aspose.Cells NuGet-paket
1. Högerklicka på ditt projekt i Solution Explorer.
2.  Välja`Manage NuGet Packages...`.
3.  Leta efter`Aspose.Cells` och installera den.
I slutet av dessa steg bör du ha allt på plats för att börja koda!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
När installationen är klar är det dags att kavla upp ärmarna och börja koda. Närmare bestämt kommer vi att skapa en ny Excel-arbetsbok och specificera både Fjärran Östern och latinska teckensnitt för textrutor. Så här gör du steg för steg:
## Steg 1: Konfigurera utdatakatalogen
Vi börjar med att ange var vi vill spara vår Excel-fil. Detta är avgörande eftersom vi vill säkerställa att vår utdatafil lagras på en plats som är lättillgänglig.
```csharp
// Utdatakatalog
string outputDir = "Your Document Directory";
```
## Steg 2: Skapa en tom arbetsbok
Nu när vi har ställt in vår katalog, låt oss skapa en ny arbetsbok där vi lägger till vårt innehåll. Detta liknar att börja med en ny duk innan du målar.
```csharp
// Skapa en tom arbetsbok.
Workbook wb = new Workbook();
```
## Steg 3: Öppna det första arbetsbladet
Därefter vill vi arbeta med ett kalkylblad från vår arbetsbok. Tänk på ett kalkylblad som en sida i din bok där all magi händer.
```csharp
// Öppna första kalkylbladet.
Worksheet ws = wb.Worksheets[0];
```
## Steg 4: Lägg till en textruta
Nu kommer vi att lägga till en textruta i vårt kalkylblad. Det är här vi skriver in vår text. Föreställ dig detta som att skapa en textruta i en bild i en presentation.
```csharp
// Lägg till textruta i kalkylbladet.
int idx = ws.TextBoxes.Add(5, 5, 50, 200);
Aspose.Cells.Drawing.TextBox tb = ws.TextBoxes[idx];
```
## Steg 5: Ställ in texten i textrutan
Låt oss skriva in lite text. I det här exemplet kommer vi att mata in japanska tecken för att demonstrera typsnittet Fjärran Östern. Det är lika enkelt som att skriva i en textruta på din dator!
```csharp
// Ställ in texten i textrutan.
tb.Text = "こんにちは世界"; //Detta betyder "Hello World" på japanska.
```
## Steg 6: Ange teckensnitt
Nu kommer den spännande delen! Vi kommer att ställa in både latinska och Fjärran Östern-teckensnitten för texten. Detta är ungefär som att välja det perfekta typsnittet för en snygg bröllopsinbjudan!
```csharp
// Ange Fjärran Östern och det latinska namnet på teckensnittet.
tb.TextOptions.LatinName = "Comic Sans MS"; // Detta är vårt valda latinska teckensnitt.
tb.TextOptions.FarEastName = "KaiTi"; // Detta är vårt önskade typsnitt i Fjärran Östern.
```
## Steg 7: Spara Excel-filen
Till sist, låt oss spara vår arbetsbok! Detta steg avslutar vår uppgift och säkerställer att allt hårt arbete vi har gjort sparas ordentligt. 
```csharp
// Spara den utgående Excel-filen.
wb.Save(outputDir + "outputSpecifyFarEastAndLatinNameOfFontInTextOptionsOfShape.xlsx", SaveFormat.Xlsx);
```
## Steg 8: Bekräftelsemeddelande
Vi skriver ut ett bekräftelsemeddelande till konsolen för att låta oss veta att allt har utförts framgångsrikt:
```csharp
Console.WriteLine("SpecifyFarEastAndLatinNameOfFontInTextOptionsOfShape executed successfully.");
```
## Slutsats
Och där har du det! Du har framgångsrikt angett Fjärran Östern och latinska teckensnitt i en Excel-arbetsbok med Aspose.Cells för .NET. Denna färdighet ger inte bara dina dokument en professionell touch utan berikar också läsupplevelsen för användare på olika språk.
Experimentera gärna med olika typsnitt och stilar för att hitta en kombination som passar dina specifika behov. Glad kodning!
## FAQ's
### Vad är Aspose.Cells?
Aspose.Cells är ett .NET-bibliotek för att skapa och hantera Excel-kalkylblad utan att behöva Microsoft Excel installerat på din maskin. 
### Kan jag använda Aspose.Cells för webbapplikationer?
Ja! Aspose.Cells kan användas för både stationära applikationer och webbapplikationer byggda med .NET.
### Finns det en gratisversion av Aspose.Cells?
 Ja, Aspose erbjuder en gratis provperiod. Du kan[ladda ner den här](https://releases.aspose.com/).
### Hur får jag support för Aspose.Cells?
 Du kan be om stöd och hitta värdefulla resurser på[Aspose forum](https://forum.aspose.com/c/cells/9).
### Var kan jag köpa Aspose.Cells?
 Du kan köpa Aspose.Cells direkt från[Aspose hemsida](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
