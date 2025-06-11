---
"description": "Automatisera talformatering i Excel med Aspose.Cells för .NET. Lär dig hur du använder datum-, procent- och valutaformat programmatiskt."
"linktitle": "Använda inbyggda talformat i Excel programmatiskt"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Använda inbyggda talformat i Excel programmatiskt"
"url": "/sv/net/number-and-display-formats-in-excel/using-built-in-number-formats/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Använda inbyggda talformat i Excel programmatiskt

## Introduktion
den här handledningen går vi igenom hur du använder inbyggda talformat i Excel med Aspose.Cells för .NET. Vi går igenom allt från att konfigurera din miljö till att tillämpa olika format som datum, procenttal och valutor. Oavsett om du är ett erfaret proffs eller bara har börjat utforska .NET-ekosystemet, kommer den här guiden att hjälpa dig formatera Excel-celler som en barnlek.
## Förkunskapskrav
Innan du dyker in, se till att du har följande:
- Aspose.Cells för .NET-biblioteket är installerat. Du kan [ladda ner den här](https://releases.aspose.com/cells/net/).
- Goda kunskaper i C# och grundläggande .NET-programmering.
- Visual Studio eller någon .NET IDE installerad på din dator.
- En giltig Aspose-licens eller [tillfällig licens](https://purchase.aspose.com/temporary-license/).
- .NET framework installerat (version 4.0 eller senare).
  
Om du saknar något av ovanstående, följ länkarna som finns för att ställa in allt. Klara? Nu kör vi vidare till det roliga!
## Importera paket
Innan vi börjar med handledningen, se till att importera de namnrymder som krävs för att arbeta med Aspose.Cells för .NET:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
När du har importerat dessa är du redo att manipulera Excel-filer programmatiskt. Nu ska vi dyka in i steg-för-steg-guiden!
## Steg 1: Skapa eller få åtkomst till din Excel-arbetsbok
I det här steget skapar du en ny arbetsbok. Tänk på det som att öppna en ny Excel-fil, fast du gör det via kod!
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
// Skapa katalog om den inte redan finns.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Instansiera ett arbetsboksobjekt
Workbook workbook = new Workbook();
```
Här instansierar vi helt enkelt en ny `Workbook` objekt. Detta fungerar som din Excel-fil, redo för databehandling. Du kan också ladda en befintlig fil genom att ange dess sökväg.
## Steg 2: Öppna arbetsbladet
Excel-arbetsböcker kan innehålla flera kalkylblad. I det här steget kommer vi åt det första kalkylbladet i din arbetsbok:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Vi öppnar nu det första kalkylbladet i arbetsboken. Om du behöver manipulera ytterligare blad kan du referera till dem med hjälp av deras index eller namn.
## Steg 3: Lägg till data i celler
Låt oss börja lägga till lite data i specifika celler. Först infogar vi det aktuella systemdatumet i cell "A1":
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
Den här raden infogar dagens datum i cell A1. Ganska coolt, eller hur? Tänk dig att göra detta manuellt för hundratals celler – det skulle vara en mardröm. Nu går vi vidare till formateringen!
## Steg 4: Formatera datum i cell "A1"
Nu ska vi formatera datumet i ett mer läsbart format, som "15-okt-24". Det är här Aspose.Cells verkligen glänser:
1. Hämta cellens stil:
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
Här tar vi stilen för cell A1. Tänk på detta som att ta cellens "stil" innan du gör några justeringar.
2. Ställ in datumformat:
```csharp
style.Number = 15;
```
Inställning av `Number` egenskapen till 15 tillämpar önskat datumformat. Detta är en inbyggd talformatkod för att visa datum i formatet "d-mmm-åå".
3. Använd stilen på cellen:
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
Den här raden tillämpar stiländringarna på cellen. Nu, istället för ett standarddatumformat, ser du något mycket mer användarvänligt som "15-okt-24".
## Steg 5: Lägg till och formatera en procentandel i cell "A2"
Låt oss gå vidare till formatering av procentsatser. Tänk dig att du vill infoga ett värde och visa det som en procentandel. I det här steget lägger vi till ett numeriskt värde i cell "A2" och formaterar det som en procentandel:
1. Infoga numeriskt värde:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
Detta infogar siffran 20 i cell A2. Du kanske tänker: "Det är bara ett vanligt tal – hur gör jag om det till en procentandel?" Ja, vi ska snart komma till det.
2. Hämta stilen och ange procentformat:
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // Formatera som procentandel
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
Här lägger vi till 2546 i cell A3. Sedan formaterar vi detta tal så att det visas som valuta.
2. Hämta stilen och ange valutaformat:
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // Formatera som valuta
worksheet.Cells["A3"].SetStyle(style);
```
Inställning av `Number` egenskapen till 6 tillämpar valutaformatet. Nu visas värdet i cell A3 som "2 546,00", komplett med kommatecken och två decimaler.
## Steg 7: Spara Excel-filen
Nu när vi har tillämpat all formateringsmagi är det dags att spara filen:
```csharp
// Spara Excel-filen
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
Den här raden sparar Excel-filen i Excel 97-2003-formatet. Du kan ändra `SaveFormat` för att passa dina behov. Och precis så har du skapat och formaterat en Excel-fil programmatiskt!
## Slutsats
Grattis! Du har nu lärt dig hur du använder Aspose.Cells för .NET för att tillämpa inbyggda talformat på celler i en Excel-fil. Från datum till procentsatser och valutor har vi gått igenom några av de vanligaste formateringsbehoven för Excel-databehandling. Nu kan du automatisera hela processen istället för att formatera celler manuellt – vilket sparar tid och minskar antalet fel.
## Vanliga frågor
### Kan jag använda anpassade talformat med Aspose.Cells för .NET?
Ja! Förutom inbyggda format stöder Aspose.Cells även anpassade talformat. Du kan skapa mycket specifika format med hjälp av `Custom` egendom i `Style` klass.
### Hur kan jag formatera en cell som en valuta med en specifik symbol?
För att använda en specifik valutasymbol kan du använda anpassad formatering genom att ställa in `Style.Custom` egendom.
### Kan jag formatera hela rader eller kolumner?
Absolut! Du kan tillämpa stilar på hela rader eller kolumner med hjälp av `Rows` eller `Columns` samlingar i `Worksheet` objekt.
### Hur kan jag formatera flera celler samtidigt?
Du kan använda `Range` objekt för att markera flera celler och tillämpa format på dem alla samtidigt.
### Behöver jag ha Microsoft Excel installerat för att använda Aspose.Cells?
Nej, Aspose.Cells fungerar oberoende av Microsoft Excel, så du behöver inte ha Excel installerat på din dator.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}