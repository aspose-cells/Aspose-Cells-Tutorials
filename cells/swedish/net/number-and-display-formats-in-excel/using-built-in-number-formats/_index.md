---
title: Använda inbyggda talformat i Excel Programmatiskt
linktitle: Använda inbyggda talformat i Excel Programmatiskt
second_title: Aspose.Cells .NET Excel Processing API
description: Automatisera nummerformatering i Excel med Aspose.Cells för .NET. Lär dig hur du tillämpar datum-, procent- och valutaformat programmatiskt.
weight: 10
url: /sv/net/number-and-display-formats-in-excel/using-built-in-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Använda inbyggda talformat i Excel Programmatiskt

## Introduktion
den här handledningen går vi igenom hur du använder inbyggda talformat i Excel med Aspose.Cells för .NET. Vi täcker allt från att ställa in din miljö till att använda olika format som datum, procentsatser och valutor. Oavsett om du är ett erfaret proffs eller bara doppar tårna i .NET-ekosystemet, kommer den här guiden att få dig att formatera Excel-celler som en bris.
## Förutsättningar
Innan du dyker in, se till att du har följande:
-  Aspose.Cells för .NET-biblioteket installerat. Du kan[ladda ner den här](https://releases.aspose.com/cells/net/).
- En praktisk kunskap om C# och grundläggande .NET-programmering.
- Visual Studio eller någon .NET IDE installerad på din maskin.
-  En giltig Aspose-licens eller[tillfällig licens](https://purchase.aspose.com/temporary-license/).
- .NET framework installerat (version 4.0 eller senare).
  
Om du saknar något av ovanstående, följ länkarna för att ställa in allt. Redo? Låt oss hoppa in i den roliga delen!
## Importera paket
Innan vi börjar med handledningen, se till att importera de nödvändiga namnrymden för att arbeta med Aspose.Cells för .NET:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
När du har importerat dessa är du redo att manipulera Excel-filer programmatiskt. Låt oss nu dyka in i steg-för-steg-guiden!
## Steg 1: Skapa eller komma åt din Excel-arbetsbok
I det här steget skapar du en ny arbetsbok. Se det här som att öppna en ny Excel-fil, förutom att du gör det genom kod!
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
// Skapa katalog om den inte redan finns.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Instantiera ett arbetsboksobjekt
Workbook workbook = new Workbook();
```
 Här instansierar vi helt enkelt en ny`Workbook` objekt. Detta fungerar som din Excel-fil, redo för datamanipulation. Du kan också ladda en befintlig fil genom att ange dess sökväg.
## Steg 2: Öppna arbetsbladet
Excel-arbetsböcker kan innehålla flera kalkylblad. I det här steget kommer vi åt det första kalkylbladet i din arbetsbok:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Vi kommer nu åt det första kalkylbladet i arbetsboken. Om du behöver manipulera ytterligare blad kan du referera till dem med hjälp av deras index eller namn.
## Steg 3: Lägg till data i celler
Låt oss börja lägga till lite data till specifika celler. Först infogar vi det aktuella systemdatumet i cell "A1":
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
Denna rad infogar det aktuella datumet i cell A1. Ganska coolt, eller hur? Föreställ dig att göra detta manuellt för hundratals celler - det skulle vara en mardröm. Nu ska vi gå vidare till formatering!
## Steg 4: Formatera datum i cell "A1"
Låt oss sedan formatera det datumet i ett mer läsbart format, som "15-okt-24". Det är här Aspose.Cells verkligen lyser:
1. Hämta cellens stil:
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
Här tar vi tag i stilen med cell A1. Se det här som att ta tag i cellens "mode" innan du gör några justeringar.
2. Ställ in datumformat:
```csharp
style.Number = 15;
```
 Ställa in`Number` egenskapen till 15 tillämpar önskat datumformat. Detta är en inbyggd sifferformatkod för att visa datum i formatet "d-mmm-yy".
3. Tillämpa stilen på cellen:
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
Den här raden tillämpar stiländringarna på cellen. Nu, istället för ett standarddatumformat, kommer du att se något mycket mer användarvänligt som "15-okt-24."
## Steg 5: Lägg till och formatera en procentandel i cell "A2"
Låt oss gå vidare till formatering av procentsatser. Föreställ dig att du vill infoga ett värde och visa det som en procentsats. I det här steget lägger vi till ett numeriskt värde i cell "A2" och formaterar det som en procentandel:
1. Infoga numeriskt värde:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
Detta infogar siffran 20 i cell A2. Du kanske tänker: "Det är bara en vanlig siffra - hur förvandlar jag det till en procentsats?" Nåväl, vi är på väg att komma till det.
2. Hämta stilen och ange procentformat:
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // Format som procent
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
Här lägger vi till 2546 till cell A3. Därefter formaterar vi det här numret så att det visas som valuta.
2. Hämta stilen och ange valutaformat:
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // Formatera som valuta
worksheet.Cells["A3"].SetStyle(style);
```
 Ställa in`Number` egenskapen till 6 tillämpar valutaformatet. Nu kommer värdet i cell A3 att visas som "2 546,00", komplett med kommatecken och två decimaler.
## Steg 7: Spara Excel-filen
Nu när vi har tillämpat all formateringsmagi är det dags att spara filen:
```csharp
// Sparar Excel-filen
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
 Denna rad sparar Excel-filen i Excel 97-2003-format. Du kan ändra`SaveFormat`för att passa dina behov. Och precis så har du skapat och formaterat en Excel-fil programmatiskt!
## Slutsats
Grattis! Du har framgångsrikt lärt dig hur du använder Aspose.Cells för .NET för att tillämpa inbyggda talformat på celler i en Excel-fil. Från datum till procenttal och valutor, vi har täckt några av de vanligaste formateringsbehoven för Excel-databehandling. Nu, istället för att manuellt formatera celler, kan du automatisera hela processen – vilket sparar tid och minskar antalet fel.
## FAQ's
### Kan jag använda anpassade talformat med Aspose.Cells för .NET?
 Ja! Förutom inbyggda format stöder Aspose.Cells även anpassade talformat. Du kan skapa mycket specifika format med hjälp av`Custom` egendom i`Style` klass.
### Hur kan jag formatera en cell som en valuta med en specifik symbol?
 För att tillämpa en specifik valutasymbol kan du använda anpassad formatering genom att ställa in`Style.Custom` egendom.
### Kan jag formatera hela rader eller kolumner?
 Absolut! Du kan tillämpa stilar på hela rader eller kolumner med hjälp av`Rows` eller`Columns`samlingar i`Worksheet` objekt.
### Hur kan jag formatera flera celler samtidigt?
Du kan använda`Range` objekt för att markera flera celler och tillämpa stilar på dem alla samtidigt.
### Behöver jag installera Microsoft Excel för att använda Aspose.Cells?
Nej, Aspose.Cells fungerar oberoende av Microsoft Excel, så du behöver inte ha Excel installerat på din maskin.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
