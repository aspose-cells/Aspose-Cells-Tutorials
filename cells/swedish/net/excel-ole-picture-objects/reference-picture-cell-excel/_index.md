---
title: Referera till bildcell i Excel
linktitle: Referera till bildcell i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du refererar till en bildcell i Excel med Aspose.Cells för .NET med denna steg-för-steg handledning. Förbättra dina kalkylblad.
weight: 15
url: /sv/net/excel-ole-picture-objects/reference-picture-cell-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Referera till bildcell i Excel

## Introduktion
Om du arbetar med Excel-kalkylblad har du sannolikt stött på situationer där grafik kan förbättra din datapresentation avsevärt. Föreställ dig att du vill länka en bild till specifika celler för att representera data visuellt. Nåväl, spänn fast dig, för idag går vi in på att använda Aspose.Cells för .NET för att referera till en bildcell i Excel. I slutet av den här guiden kommer du att vara ett proffs på att integrera bilder i dina kalkylblad sömlöst. Låt oss inte slösa mer tid och hoppa direkt in!
## Förutsättningar
Innan vi börjar, låt oss se till att du har allt du behöver:
- Visual Studio: Se till att du har en kompatibel version av Visual Studio installerad på din dator för att hantera .NET-projektet.
- Aspose.Cells för .NET: Du måste ha Aspose.Cells-biblioteket. Om du inte har laddat ner det ännu, gå till[Aspose Nedladdningssida](https://releases.aspose.com/cells/net/) och hämta den senaste versionen.
- Grundläggande kunskaper om C#: Den här guiden förutsätter att du är bekväm med programmeringskoncepten C# och .NET. Om du är ny, oroa dig inte; Jag kommer att förklara varje steg i detalj.
Nu när vi är klara, låt oss importera de nödvändiga paketen!
## Importera paket
För att utnyttja kraften i Aspose.Cells måste du importera de relevanta namnområdena till ditt projekt. Så här gör du det:
1. Skapa ett nytt projekt: Öppna Visual Studio och skapa en ny C#-konsolapplikation.
2. Lägg till referenser: Se till att lägga till en referens till Aspose.Cells-biblioteket. Du kan göra detta genom att högerklicka på ditt projekt, välja "Lägg till" och sedan "Referens" och bläddra till platsen där du laddade ner Aspose.Cells DLL.
```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
Låt oss nu skriva lite kod för att uppnå vårt mål att referera till en bild i Excel.
## Steg 1: Ställ in din miljö
Först måste vi skapa en ny arbetsbok och ställa in de nödvändiga cellerna. Så här gör du:
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
// Instantiera en ny arbetsbok
Workbook workbook = new Workbook();
// Hämta det första kalkylbladets cellsamling
Cells cells = workbook.Worksheets[0].Cells;
```
 
- Du definierar sökvägen dit du vill spara din Excel-fil.
-  Skapa en ny`Workbook` instans, som representerar din Excel-fil.
- Gå till cellerna i det första kalkylbladet där vi kommer att infoga vår data och bild.
## Steg 2: Lägg till strängvärden i cellerna
Låt oss nu lägga till några strängvärden i cellerna. 
```csharp
// Lägg till strängvärden i cellerna
cells["A1"].PutValue("A1");
cells["C10"].PutValue("C10");
```
 
-  Med hjälp av`PutValue` metoden, fyller vi cell A1 med strängen "A1" och cell C10 med "C10". Detta är bara ett grundläggande exempel, men det kommer att hjälpa oss att visa hur vår bild refererar till dessa områden.
## Steg 3: Lägg till en tom bild
Därefter lägger vi till en bildform till vårt kalkylblad:
```csharp
// Lägg till en tom bild i D1-cellen
Picture pic = workbook.Worksheets[0].Shapes.AddPicture(0, 3, 10, 6, null);
```
 
- På denna rad lägger vi till en tom bild vid koordinater (0, 3) som motsvarar rad 1, kolumn 4 (D1). Måtten (10, 6) anger bildens bredd och höjd i pixlar.
## Steg 4: Ange formeln för bildreferens
Låt oss länka vår bild till de celler vi tidigare fyllt i.
```csharp
// Ange formeln som hänvisar till källintervallet för celler
pic.Formula = "A1:C10";
```

- Här ställer vi in en formel för bilden som hänvisar till området från A1 till C10. Detta gör att bilden visuellt representerar data i detta intervall. Föreställ dig att dina celler är duken, och bilden blir en fantastisk fokuspunkt!
## Steg 5: Uppdatera det valda värdet för former
För att säkerställa att våra ändringar återspeglas i kalkylbladet måste vi uppdatera formerna:
```csharp
// Uppdatera de valda formerna i kalkylbladet
workbook.Worksheets[0].Shapes.UpdateSelectedValue();
```

- Detta steg säkerställer att Excel känner igen våra uppdateringar av bildformen och eventuella referenser till celler.
## Steg 6: Spara Excel-filen
Slutligen, låt oss spara vår arbetsbok i den angivna katalogen:
```csharp
// Spara Excel-filen.
workbook.Save(dataDir + "output.out.xls");
```

-  De`Save`metoden tar sökvägen där Excel-filen kommer att lagras, tillsammans med filnamnet. När du har utfört detta hittar du din nyskapade Excel-fil i den angivna mappen.
## Steg 7: Felhantering
För att avsluta det hela, glöm inte att inkludera lite felhantering så att du kan fånga eventuella undantag som kan uppstå när du kör din kod:
```csharp
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}
```

- Detta kommer att mata ut eventuella felmeddelanden till konsolen, vilket hjälper dig att felsöka om något inte fungerar som förväntat. Kom ihåg att även de bästa kodarna får hicka ibland!
## Slutsats
Och där har du det! Du har framgångsrikt refererat till en bild i en Excel-cell med Aspose.Cells för .NET. Denna enkla men kraftfulla teknik kan förbättra ditt sätt att presentera data, vilket gör dina kalkylblad inte bara mer informativa utan också mer visuellt tilltalande. Oavsett om du skapar rapporter, instrumentpaneler eller datapresentationer är möjligheten att inkludera bilder kopplade till celldata ovärderlig.
## FAQ's
### Vad är Aspose.Cells?
Aspose.Cells är ett .NET-bibliotek för att hantera Excel-filer, vilket gör att utvecklare kan skapa, manipulera och konvertera Excel-dokument utan att behöva installera Microsoft Excel.
### Kan jag använda Aspose.Cells med Xamarin?
Ja, Aspose.Cells kan användas i Xamarin-projekt, vilket möjliggör plattformsoberoende utvecklingsmöjligheter för hantering av Excel-filer.
### Finns det en gratis provperiod?
 Absolut! Du kan få en gratis provperiod från[Aspose gratis provsida](https://releases.aspose.com/).
### Vilka format kan jag spara Excel-filerna i?
Aspose.Cells stöder olika format, inklusive XLSX, XLS, CSV, PDF och mer.
### Hur kan jag söka stöd om jag stöter på problem?
 Du kan få stöd genom[Aspose Support Forum](https://forum.aspose.com/c/cells/9), där communityn och Aspose-personalen kan hjälpa dig med dina frågor.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
