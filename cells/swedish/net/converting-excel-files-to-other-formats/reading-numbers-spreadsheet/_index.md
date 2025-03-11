---
title: Läsa siffror kalkylblad Programmatiskt i .NET
linktitle: Läsa siffror kalkylblad Programmatiskt i .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du läser Numbers-kalkylblad och konverterar dem till PDF med Aspose.Cells för .NET i denna detaljerade handledning.
weight: 18
url: /sv/net/converting-excel-files-to-other-formats/reading-numbers-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Läsa siffror kalkylblad Programmatiskt i .NET

## Introduktion
I dagens digitala värld är datahantering en viktig färdighet, och kalkylblad ligger i framkant av dataorganisation. Men vad händer om du behöver arbeta med ett Numbers-kalkylblad – de filer som skapats av Apples Numbers-app – med .NET? Oroa dig inte; du är inte ensam! I den här handledningen går vi igenom processen att läsa ett Numbers-kalkylblad programmatiskt med Aspose.Cells för .NET. Du lär dig hur du laddar en Numbers-fil och konverterar den till PDF.
## Förutsättningar
Innan vi sätter igång finns det några saker du måste ha på plats:
1. Aspose.Cells för .NET: Se till att du har Aspose.Cells-biblioteket installerat. Du kan ladda ner den[här](https://releases.aspose.com/cells/net/).
2. Visual Studio: Det rekommenderas att ha Visual Studio (eller någon annan .NET-kompatibel IDE) installerad på din maskin.
3. Grundläggande kunskaper om C#: Lite förtrogenhet med C#-programmering hjälper dig att följa med smidigt.
4. Din dokumentkatalog: Du behöver en katalog där din Numbers-fil lagras, tillsammans med en plats för att spara den konverterade PDF-filen.
När du har täckt dessa förutsättningar är du redo att börja!
## Importera paket
Till att börja med måste vi importera de nödvändiga paketen till vårt C#-projekt. Detta är ett avgörande steg eftersom det tillåter oss att utnyttja funktionerna som tillhandahålls av Aspose.Cells-biblioteket.
1. Öppna ditt C#-projekt i Visual Studio.
2. Lägg till en referens till Aspose.Cells-biblioteket:
   - Om du använder NuGet kör du helt enkelt följande kommando i Package Manager Console:
```
 Install-Package Aspose.Cells
 ```
3. Importera de nödvändiga namnrymden i din kod:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Nu när vi har importerat de nödvändiga paketen, låt oss gå vidare till steg-för-steg-guiden för att läsa ett Numbers-kalkylblad.
## Steg 1: Ange käll- och utdatakataloger
I det här steget kommer vi att ställa in katalogerna där din källnummerfil finns och där du vill spara den utgående PDF-filen.
```csharp
// Källkatalog
string sourceDir = "Your Document Directory"; // Uppdatera detta till din faktiska katalog
// Utdatakatalog
string outputDir = "Your Document Directory"; // Uppdatera detta till din faktiska katalog
```
 Här definierar vi två strängvariabler,`sourceDir` och`outputDir` , för att ange var inmatnings- och utdatafilerna finns. Se till att byta ut`"Your Document Directory"` med de faktiska sökvägarna på ditt system.
## Steg 2: Ställ in laddningsalternativ för nummerformat
Därefter kommer vi att specificera laddningsalternativen för att läsa ett Numbers-kalkylblad. Detta steg är viktigt eftersom det talar om för Aspose hur man tolkar Numbers-filen.
```csharp
// Ange laddningsalternativ; vi vill ladda kalkylarket Numbers
LoadOptions opts = new LoadOptions(LoadFormat.Numbers);
```
 Vi skapar en`LoadOptions` objekt och ange formatet som`LoadFormat.Numbers`. Detta talar om för Aspose.Cells-biblioteket att vi arbetar med en Numbers-fil. 
## Steg 3: Ladda Numbers-kalkylbladet i en arbetsbok
Nu är det dags att ladda det faktiska Numbers-kalkylarket i ett`Workbook` objekt.
```csharp
// Ladda kalkylarket Numbers i arbetsboken med laddningsalternativen ovan
Workbook wb = new Workbook(sourceDir + "sampleNumbersByAppleInc.numbers", opts);
```
 Vi instansierar en`Workbook` objekt och skicka filsökvägen till Numbers-filen tillsammans med våra laddningsalternativ. Se till att filnamnet (`sampleNumbersByAppleInc.numbers`) matchar det faktiska namnet på din Numbers-fil.
## Steg 4: Spara arbetsboken som en PDF
När Numbers-filen väl har laddats är nästa steg att spara den i ett annat format, närmare bestämt PDF.
```csharp
// Spara arbetsboken i PDF-format
wb.Save(outputDir + "outputNumbersByAppleInc.pdf", SaveFormat.Pdf);
```
 Här kallar vi`Save` metod på`Workbook` objekt, som anger sökvägen till utdatafilen och formatet vi vill spara den i. I det här fallet sparar vi den som en PDF. Se till att utdatafilens namn (`outputNumbersByAppleInc.pdf`) är unik och skriver inte över några befintliga filer.
## Steg 5: Bekräfta framgång
Låt oss slutligen lägga till ett meddelande för att bekräfta att vår operation lyckades.
```csharp
Console.WriteLine("ReadNumbersSpreadsheet executed successfully.\r\n");
```
Denna kodrad kommer att skriva ut ett framgångsmeddelande till konsolen när allt är klart. Det är alltid trevligt med feedback, eller hur?
## Slutsats
Och där har du det! Du har framgångsrikt läst ett Numbers-kalkylblad och konverterat det till PDF med Aspose.Cells för .NET. Detta kraftfulla bibliotek låter dig manipulera kalkylblad utan ansträngning, vilket gör dina datahanteringsuppgifter till en lek. Oavsett om du utvecklar applikationer eller bara behöver hantera kalkylblad mer effektivt är Aspose.Cells ett fantastiskt verktyg att ha i din verktygslåda.
## FAQ's
### Vilka typer av filer kan Aspose.Cells läsa?  
Aspose.Cells kan läsa en mängd olika filformat, inklusive XLS-, XLSX-, CSV- och Numbers-filer. 
### Kan jag redigera Numbers-filer med Aspose.Cells?  
Ja, du kan läsa, manipulera och spara Numbers-filer med Aspose.Cells.
### Är Aspose.Cells gratis att använda?  
 Aspose.Cells erbjuder en gratis provperiod, men du behöver en licens för utökad användning. Kolla priset[här](https://purchase.aspose.com/buy).
### Vad gör jag om jag stöter på ett fel när jag laddar en Numbers-fil?  
 Se till att du använder rätt laddningsalternativ och att filsökvägen är korrekt. För mer support, besök[Aspose Support Forum](https://forum.aspose.com/c/cells/9).
### Hur kan jag få en tillfällig licens för Aspose.Cells?  
 Du kan ansöka om en tillfällig licens[här](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
