---
"description": "Lär dig hur du anpassar visningsformat med Aspose.Cells för .NET. Formatera datum, procenttal och valuta med hjälp av den här steg-för-steg-guiden."
"linktitle": "Anpassa visningsformat med användardefinierade siffror"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Anpassa visningsformat med användardefinierade siffror"
"url": "/sv/net/number-and-display-formats-in-excel/customizing-display-formats-with-user-defined-numbers/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Anpassa visningsformat med användardefinierade siffror

## Introduktion
Att arbeta med Excel-filer kräver ofta anpassad formatering av celler för att presentera data på ett mer meningsfullt och användarvänligt sätt. Tänk dig att du bygger en Excel-fil för en rapport. Du vill inte bara ha råa siffror. Du vill att datum, procenttal och valutor ska se snygga och professionella ut, eller hur? Det är där anpassade visningsformat kommer in i bilden. I den här handledningen fördjupar vi oss i Aspose.Cells för .NET för att visa dig hur du anpassar visningsformatet för tal med hjälp av användardefinierade inställningar.
## Förkunskapskrav
Innan du börjar, se till att du har allt klart för att följa den här handledningen. Här är vad du behöver:
- Aspose.Cells för .NET installerat. [Ladda ner den här](https://releases.aspose.com/cells/net/).
- Grundläggande kunskaper i C# och .NET framework.
- En giltig licens för Aspose.Cells. Om du inte har en, skaffa en [gratis provperiod](https://releases.aspose.com/) eller begära en [tillfällig licens](https://purchase.aspose.com/temporary-license/).
- En IDE som Visual Studio.
- .NET Framework 4.0 eller senare.
Om du saknar något, oroa dig inte. Du kan alltid besöka dessa länkar igen för att ladda ner nödvändiga filer eller söka hjälp från [Aspose supportforum](https://forum.aspose.com/c/cells/9).
## Importera namnrymder
Innan du börjar med koden måste du importera de namnrymder som krävs för att komma åt alla nödvändiga Aspose.Cells-funktioner.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Dessa två namnrymder kommer att vara dina huvudverktyg i den här handledningen. Nu går vi vidare till det roliga:
## Steg 1: Konfigurera projektkatalogen
Först behöver du en plats att lagra dina filer, eller hur? Nu skapar vi en katalog för att spara den utgående Excel-filen. I det här steget kontrollerar vi också att katalogen finns innan vi sparar något.
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
// Skapa katalog om den inte redan finns.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- Vi definierar en `dataDir` variabel för att lagra sökvägen dit den utgående Excel-filen ska hamna.
- Vi kontrollerar sedan om katalogen finns med hjälp av `System.IO.Directory.Exists()`.
- Om katalogen inte finns skapas den med hjälp av `System.IO.Directory.CreateDirectory()`.
## Steg 2: Skapa en ny arbetsbok och lägg till ett arbetsblad
Nu när vi har vår katalog, låt oss skapa en ny Excel-arbetsbok och lägga till ett kalkylblad i den.
```csharp
// Instansiera ett arbetsboksobjekt
Workbook workbook = new Workbook();
// Lägga till ett nytt kalkylblad i Excel-objektet
int i = workbook.Worksheets.Add();
// Hämta referensen till det nyligen tillagda kalkylbladet genom att skicka dess arkindex
Worksheet worksheet = workbook.Worksheets[i];
```
- Först skapar vi ett nytt `Workbook` objekt. Tänk på detta som din Excel-fil.
- Vi lägger till ett nytt arbetsblad i den här arbetsboken med hjälp av `Add()` metoden och lagra indexet i variabeln `i`.
- Vi refererar till detta arbetsblad med hjälp av `workbook.Worksheets[i]`.
## Steg 3: Lägga till datum i en cell och anpassa dess format
Nu ska vi infoga aktuellt datum i en cell och formatera det så att det visas på ett anpassat sätt. Istället för standarddatumformatet ställer vi in ett anpassat format som `d-mmm-yy`.
```csharp
// Lägger till aktuellt systemdatum i cellen "A1"
worksheet.Cells["A1"].PutValue(DateTime.Now);
// Få stilen på A1-cellen
Style style = worksheet.Cells["A1"].GetStyle();
// Ställa in det anpassade visningsformatet för att visa datum som "d-mmm-åå"
style.Custom = "d-mmm-yy";
// Tillämpa stilen på A1-cellen
worksheet.Cells["A1"].SetStyle(style);
```
- Vi lägger till det aktuella systemdatumet i cellen `A1` använder `PutValue(DateTime.Now)`.
- Vi hämtar den aktuella cellstilen `A1` använder `GetStyle()`.
- Vi ändrar cellens stil genom att ställa in `style.Custom = "d-mmm-yy"`, som formaterar datumet för att visa dag, förkortad månad och år.
- Slutligen tillämpar vi den nya stilen på cellen med `SetStyle()`.
## Steg 4: Formatera en cell som en procentandel
Nu ska vi arbeta med siffror. Vi lägger till ett numeriskt värde i en annan cell, till exempel `A2`och formatera det som en procentandel.
```csharp
// Lägga till ett numeriskt värde i cellen "A2"
worksheet.Cells["A2"].PutValue(20);
// Få stilen på A2-cellen
style = worksheet.Cells["A2"].GetStyle();
// Ställa in det anpassade visningsformatet för att visa värde som procentandel
style.Custom = "0.0%";
// Tillämpa stilen på en A2-cell
worksheet.Cells["A2"].SetStyle(style);
```
- Vi tillför värdet `20` till cell `A2`.
- Vi hämtar cellens stil `A2` och ställ in det anpassade formatet till `0.0%` för att visa värdet som en procentandel (dvs. 20 %).
- Slutligen tillämpar vi stilen på cellen med hjälp av `SetStyle()`.
## Steg 5: Formatera en cell som valuta
Låt oss lägga till ett annat värde, säg till en cell `A3`och formatera den så att den visas som valuta. För att göra det mer intressant använder vi ett format som visar positiva värden som valuta i pund och negativa värden i dollar.
```csharp
// Lägga till ett numeriskt värde i cellen "A3"
worksheet.Cells["A3"].PutValue(2546);
// Att få stilen på A3-cellen
style = worksheet.Cells["A3"].GetStyle();
// Ställa in det anpassade visningsformatet för att visa värde som valuta
style.Custom = "£#,##0;[Red]$-#,##0";
// Tillämpa stilen på en A3-cell
worksheet.Cells["A3"].SetStyle(style);
```
- Vi tillför värdet `2546` till cell `A3`.
- Vi sätter ett anpassat format `£#,##0;[Red]$-#,##0`, som visar positiva värden med ett pundtecken och negativa värden i rött med ett dollartecken.
- Vi tillämpar stilen på cellen med hjälp av `SetStyle()`.
## Steg 6: Spara arbetsboken
Det sista steget är att spara arbetsboken som en Excel-fil. Vi använder Excel 97-2003-formatet för den här handledningen.
```csharp
// Spara Excel-filen
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
- De `Save()` Metoden sparar arbetsboken i den angivna katalogen.
- Vi väljer `SaveFormat.Excel97To2003` för att säkerställa kompatibilitet med äldre versioner av Excel.
## Slutsats
Där har du det! Vi har precis skapat en Excel-fil, lagt till anpassade datum-, procent- och valutaformat till specifika celler med Aspose.Cells för .NET och sparat filen. Anpassad formatering gör dina Excel-filer mycket mer läsbara och professionella. Glöm inte att utforska andra formateringsalternativ i Aspose.Cells, som villkorsstyrd formatering, för ännu mer kontroll över hur dina data ser ut.
## Vanliga frågor
### Hur kan jag tillämpa mer komplexa formateringsalternativ i Aspose.Cells?
Du kan kombinera olika formateringsstilar, till exempel teckenfärg, kantlinjer och bakgrundsfärger, med anpassade talformat.
### Kan jag tillämpa ett anpassat talformat på ett cellområde?
Ja, Aspose.Cells låter dig tillämpa en stil på ett cellområde med hjälp av `Range.SetStyle()` metod.
### Vilka andra filformat kan jag spara arbetsboken i?
Aspose.Cells stöder många format, inklusive XLSX, CSV och PDF. Ändra bara `SaveFormat` i `Save()` metod.
### Kan jag formatera negativa tal på olika sätt?
Absolut! Du kan använda anpassade talformat för att visa negativa tal med olika färger eller symboler.
### Är Aspose.Cells för .NET gratis?
Aspose.Cells erbjuder en gratis provperiod, men för full funktionalitet behöver du en giltig licens. Du kan få en [tillfällig licens här](https://purchase.aspose.com/temporary-license/).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}