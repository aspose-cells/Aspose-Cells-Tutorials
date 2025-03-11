---
title: Anpassa visningsformat med användardefinierade nummer
linktitle: Anpassa visningsformat med användardefinierade nummer
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du anpassar visningsformat med Aspose.Cells för .NET. Formatera datum, procentsatser och valuta med hjälp av den här steg-för-steg-guiden.
weight: 11
url: /sv/net/number-and-display-formats-in-excel/customizing-display-formats-with-user-defined-numbers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Anpassa visningsformat med användardefinierade nummer

## Introduktion
Att arbeta med Excel-filer kräver ofta anpassad formatering av celler för att presentera data på ett mer meningsfullt och användarvänligt sätt. Föreställ dig att du bygger en Excel-fil för en rapport. Du vill inte bara ha råa siffror. Du vill att datum, procentsatser och valutor ska se snygga och professionella ut, eller hur? Det är där anpassade visningsformat kommer in i bilden. I den här handledningen dyker vi djupt in i Aspose.Cells för .NET för att visa dig hur du anpassar visningsformatet för siffror med användardefinierade inställningar.
## Förutsättningar
Innan du börjar, se till att du har allt klart att följa tillsammans med denna handledning. Här är vad du behöver:
-  Aspose.Cells för .NET installerat.[Ladda ner den här](https://releases.aspose.com/cells/net/).
- Grundläggande kunskaper i C# och .NET framework.
-  En giltig licens för Aspose.Cells. Om du inte har en, ta en[gratis provperiod](https://releases.aspose.com/) eller begära en[tillfällig licens](https://purchase.aspose.com/temporary-license/).
- En IDE som Visual Studio.
- .NET Framework 4.0 eller senare.
 Om du saknar något, oroa dig inte. Du kan alltid besöka dessa länkar igen för att ladda ner nödvändiga filer eller söka hjälp från[Aspose supportforum](https://forum.aspose.com/c/cells/9).
## Importera namnområden
Innan du hoppar in i koden måste du importera de nödvändiga namnområdena för att komma åt alla nödvändiga Aspose.Cells-funktioner.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Dessa två namnområden kommer att vara dina kärnverktyg i den här handledningen. Låt oss nu gå vidare till den roliga delen:
## Steg 1: Konfigurera projektkatalogen
Först behöver du en plats att lagra dina filer på, eller hur? Låt oss skapa en katalog för att spara den utgående Excel-filen. I det här steget ser vi också till att katalogen finns innan vi sparar något.
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
// Skapa katalog om den inte redan finns.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
-  Vi definierar en`dataDir` variabel för att lagra sökvägen dit utdata Excel-filen kommer att gå.
-  Vi kontrollerar sedan om katalogen finns med`System.IO.Directory.Exists()`.
-  Om katalogen inte finns skapas den med`System.IO.Directory.CreateDirectory()`.
## Steg 2: Skapa en ny arbetsbok och lägg till ett arbetsblad
Nu när vi har fått vår katalog, låt oss skapa en ny Excel-arbetsbok och lägga till ett kalkylblad till den.
```csharp
// Instantiera ett arbetsboksobjekt
Workbook workbook = new Workbook();
// Lägga till ett nytt kalkylblad till Excel-objektet
int i = workbook.Worksheets.Add();
// Få referensen till det nyligen tillagda kalkylbladet genom att skicka dess arkindex
Worksheet worksheet = workbook.Worksheets[i];
```
-  Först skapar vi en ny`Workbook` objekt. Se detta som din Excel-fil.
-  Vi lägger till ett nytt kalkylblad till den här arbetsboken med hjälp av`Add()`metod och lagra indexet i variabel`i`.
-  Vi hänvisar till detta arbetsblad med hjälp av`workbook.Worksheets[i]`.
## Steg 3: Lägga till datum i en cell och anpassa dess format
 Låt oss nu infoga det aktuella datumet i en cell och formatera det så att det visas på ett anpassat sätt. Istället för standarddatumformatet ställer vi in ett anpassat format som`d-mmm-yy`.
```csharp
// Lägger till aktuellt systemdatum i "A1"-cellen
worksheet.Cells["A1"].PutValue(DateTime.Now);
// Få stilen med A1-cell
Style style = worksheet.Cells["A1"].GetStyle();
// Ställa in det anpassade visningsformatet för att visa datum som "d-mmm-yy"
style.Custom = "d-mmm-yy";
// Använder stilen på A1-cellen
worksheet.Cells["A1"].SetStyle(style);
```
-  Vi lägger till det aktuella systemdatumet i cellen`A1` använder`PutValue(DateTime.Now)`.
-  Vi hämtar den nuvarande cellstilen`A1` använder`GetStyle()`.
-  Vi ändrar cellens stil genom att ställa in`style.Custom = "d-mmm-yy"`, som formaterar datumet för att visa dagen, förkortad månad och år.
-  Slutligen tillämpar vi den nya stilen på cellen med`SetStyle()`.
## Steg 4: Formatera en cell som en procentandel
 Nästa upp, låt oss arbeta med siffror. Vi lägger till ett numeriskt värde till en annan cell, till exempel`A2`, och formatera den som en procentandel.
```csharp
//Lägga till ett numeriskt värde till "A2"-cellen
worksheet.Cells["A2"].PutValue(20);
// Få stilen med A2-cell
style = worksheet.Cells["A2"].GetStyle();
// Ställa in det anpassade visningsformatet för att visa värdet i procent
style.Custom = "0.0%";
// Använder stilen på A2-cell
worksheet.Cells["A2"].SetStyle(style);
```
-  Vi lägger till värdet`20` till cellen`A2`.
-  Vi hämtar cellens stil`A2` och ställ in det anpassade formatet till`0.0%` för att visa värdet i procent (dvs. 20%).
-  Slutligen tillämpar vi stilen på cellen med hjälp av`SetStyle()`.
## Steg 5: Formatera en cell som valuta
 Låt oss lägga till ytterligare ett värde, säg till cellen`A3`, och formatera den så att den visas som valuta. För att göra saker mer intressanta använder vi ett format som visar positiva värden som valuta i pund och negativa värden i dollar.
```csharp
// Lägga till ett numeriskt värde till "A3"-cellen
worksheet.Cells["A3"].PutValue(2546);
// Få stilen med A3-cell
style = worksheet.Cells["A3"].GetStyle();
// Ställa in det anpassade visningsformatet för att visa värde som valuta
style.Custom = "£#,##0;[Red]$-#,##0";
// Använder stilen på A3-cell
worksheet.Cells["A3"].SetStyle(style);
```
-  Vi lägger till värdet`2546` till cellen`A3`.
-  Vi ställer in ett anpassat format`£#,##0;[Red]$-#,##0`, som visar positiva värden med ett pundtecken och negativa värden i rött med ett dollartecken.
- Vi applicerar stilen på cellen med hjälp av`SetStyle()`.
## Steg 6: Spara arbetsboken
Det sista steget är att spara arbetsboken som en Excel-fil. Vi använder Excel 97-2003-formatet för den här handledningen.
```csharp
// Sparar Excel-filen
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
-  De`Save()` metod sparar arbetsboken i den angivna katalogen.
-  Vi väljer`SaveFormat.Excel97To2003` för att säkerställa kompatibilitet med äldre versioner av Excel.
## Slutsats
Där har du det! Vi har precis skapat en Excel-fil, lagt till anpassade datum-, procent- och valutaformat till specifika celler med Aspose.Cells för .NET och sparat filen. Anpassad formatering gör dina Excel-filer mycket mer läsbara och professionella. Glöm inte att utforska andra formateringsalternativ i Aspose.Cells, som villkorlig formatering, för ännu mer kontroll över hur din data ser ut.
## FAQ's
### Hur kan jag använda mer komplexa formateringsalternativ i Aspose.Cells?
Du kan kombinera olika formateringsstilar, som teckensnittsfärg, ramar och bakgrundsfärger, med anpassade talformat.
### Kan jag använda ett anpassat talformat på ett cellintervall?
Ja, Aspose.Cells låter dig tillämpa en stil på en rad celler med hjälp av`Range.SetStyle()` metod.
### Vilka andra filformat kan jag spara arbetsboken i?
 Aspose.Cells stöder många format, inklusive XLSX, CSV och PDF. Ändra helt enkelt`SaveFormat` i`Save()` metod.
### Kan jag formatera negativa tal annorlunda?
Absolut! Du kan använda anpassade talformat för att visa negativa tal med olika färger eller symboler.
### Är Aspose.Cells för .NET gratis?
 Aspose.Cells erbjuder en gratis provperiod, men för full funktionalitet behöver du en giltig licens. Du kan få en[tillfällig licens här](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
