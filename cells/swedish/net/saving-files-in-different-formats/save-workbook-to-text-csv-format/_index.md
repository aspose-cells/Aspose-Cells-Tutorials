---
"description": "Lär dig hur du enkelt konverterar Excel-arbetsböcker till CSV-format med Aspose.Cells i den här omfattande steg-för-steg-handledningen utformad för .NET-utvecklare."
"linktitle": "Spara arbetsboken till text i CSV-format"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Spara arbetsboken till text i CSV-format"
"url": "/sv/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Spara arbetsboken till text i CSV-format

## Introduktion
När du hanterar data kan det format du väljer verkligen avgöra hur enkelt du kan arbeta med det. Bland de vanligaste formaten för att hantera tabelldata är CSV (kommaseparerade värden). Om du är en utvecklare som arbetar med Excel-filer och behöver konvertera arbetsböcker till CSV-format är Aspose.Cells för .NET ett fantastiskt bibliotek som förenklar denna uppgift. I den här handledningen kommer vi att bryta ner stegen för att konvertera en Excel-arbetsbok till ett text-CSV-format smidigt.
## Förkunskapskrav
Innan vi börjar, låt oss se till att du har allt på plats för att komma igång:
1. Grundläggande kunskaper i C# och .NET: Eftersom vi kommer att skriva kod i C# är det viktigt att du är förtrogen med språket och .NET-ramverket.
2. Aspose.Cells-biblioteket: Se till att du har Aspose.Cells för .NET-biblioteket installerat i din utvecklingsmiljö. Du kan ladda ner det [här](https://releases.aspose.com/cells/net/).
3. Visual Studio eller valfri C# IDE: Du behöver en integrerad utvecklingsmiljö (IDE) för att skriva och exekvera din kod. Visual Studio är ett populärt val.
4. Excel-arbetsbok: Förbered ett exempel på en Excel-arbetsbok (t.ex. "bok1.xls") som innehåller data för att testa konverteringen.
## Importera paket
Nu när vi har uppfyllt våra förkunskapskrav är det första steget i processen att importera de nödvändiga paketen. I ditt C#-projekt måste du inkludera följande namnrymd högst upp i din kodfil:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Dessa namnrymder ger dig tillgång till de klasser och metoder som behövs för att arbeta med Excel-filer och hantera minnesströmmar.
## Steg 1: Definiera sökvägen till dokumentkatalogen
Det första steget i vår process är att definiera var våra dokument (Excel-arbetsböcker) lagras. Detta är viktigt eftersom det gör att vårt program kan veta var de filer det behöver bearbeta finns. 
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
```
Se till att byta ut `"Your Document Directory"` med den faktiska sökvägen där din "book1.xls"-fil finns. Detta kan vara en katalog på din dator eller en sökväg till en server.
## Steg 2: Ladda din källarbetsbok
Nästa steg är att ladda Excel-arbetsboken som ska konverteras till CSV-format.
```csharp
// Ladda din källarbetsbok
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
De `Workbook` Klassen från Aspose.Cells-biblioteket möjliggör manipulation och åtkomst till Excel-arbetsböcker. Genom att ange filsökvägen laddar vi den angivna arbetsboken för bearbetning.
## Steg 3: Initiera en byte-matris för arbetsboksdata
Innan vi börjar konvertera arbetsboken till CSV måste vi initiera en tom byte-array som så småningom kommer att innehålla all arbetsbladsdata.
```csharp
// 0-byte-matris
byte[] workbookData = new byte[0];
```
Denna byte-array kombinerar data från varje kalkylblad till en enda struktur som vi kan skriva ut till en fil senare.
## Steg 4: Konfigurera alternativ för att spara text
Nu ska vi ställa in alternativen för hur vi vill spara textformatet. Du kan välja anpassade avgränsare eller hålla dig till tabbtecken.
```csharp
// Alternativ för att spara text. Du kan använda valfri typ av avgränsare
TxtSaveOptions opts = new TxtSaveOptions();
opts.Separator = '\t'; // Ställa in tabb som avgränsare
```
I det här exemplet använder vi ett tabbtecken som avgränsare. Du kan ersätta `'\t'` med valfritt tecken du vill, som ett kommatecken (`,`), beroende på hur du vill att din CSV-fil ska vara formaterad.
## Steg 5: Iterera igenom varje arbetsblad
Nästa steg är att gå igenom alla arbetsblad i arbetsboken och spara vart och ett av dem i vår `workbookData` array, men du måste först välja vilket kalkylblad du vill arbeta med.
```csharp
// Kopiera varje kalkylbladsdata i textformat inuti arbetsbokens datamatris
for (int idx = 0; idx < workbook.Worksheets.Count; idx++)
{
    // Spara det aktiva arbetsbladet i textformat
    MemoryStream ms = new MemoryStream();
    workbook.Worksheets.ActiveSheetIndex = idx;
    workbook.Save(ms, opts);
```
Loopen går igenom varje kalkylblad i arbetsboken. `ActiveSheetIndex` är inställd så att vi sparar det aktuella arbetsbladet varje gång genom loopen. Resultaten sparas i minnet med hjälp av en `MemoryStream`.
## Steg 6: Hämta arbetsbladsdata
Efter att ha sparat ett kalkylblad i minnesströmmen är nästa steg att hämta dessa data och lägga till dem i vår `workbookData` matris.
```csharp
    // Spara kalkylbladsdata i arkdatamatrisen
    ms.Position = 0; // Återställ positionen för minnesströmmen
    byte[] sheetData = ms.ToArray(); // Hämta byte-arrayen
```
`ms.Position = 0;` återställer positionen för läsning efter skrivning. Sedan använder vi `ToArray()` för att konvertera minnesströmmen till en byte-array som innehåller kalkylbladsdata.
## Steg 7: Kombinera kalkylbladsdata
Nu ska vi kombinera data från varje kalkylblad till det enda `workbookData` arrayen initialiserades tidigare.
```csharp
    // Kombinera dessa kalkylbladsdata till en arbetsbladsdatamatris
    byte[] combinedArray = new byte[workbookData.Length + sheetData.Length];
    Array.Copy(workbookData, 0, combinedArray, 0, workbookData.Length);
    Array.Copy(sheetData, 0, combinedArray, workbookData.Length, sheetData.Length);
    workbookData = combinedArray;
}
```
Vi skapar en ny array som är tillräckligt stor för att innehålla både befintliga arbetsboksdata och nya kalkylbladsdata. Vi kopierar sedan befintliga och nya data till denna kombinerade array för senare användning.
## Steg 8: Spara alla arbetsboksdata i en fil
Slutligen, med all data kombinerad i vår `workbookData` array, kan vi spara denna array till en specificerad filsökväg.
```csharp
// Spara alla arbetsboksdata i en fil
File.WriteAllBytes(dataDir + "out.txt", workbookData);
```
`WriteAllBytes` tar den kombinerade byte-arrayen och skriver den till en textfil med namnet "out.txt" i den angivna katalogen.
## Slutsats
Och där har du det! Du har framgångsrikt konverterat en Excel-arbetsbok till ett CSV-format med hjälp av Aspose.Cells för .NET. Denna process är inte bara effektiv, utan möjliggör också enkel manipulation av Excel-data för vidare analys eller rapportering. Nu kan du automatisera dina databehandlingsuppgifter eller till och med integrera denna funktion i större applikationer.
## Vanliga frågor
### Kan jag använda olika avgränsare för CSV-filen?
Ja, du kan ändra `opts.Separator` till vilket tecken du vill, till exempel kommatecken eller streck.
### Är Aspose.Cells gratis att använda?
Aspose.Cells är inte gratis, men du kan få en gratis provperiod [här](https://releases.aspose.com/).
### Vilka typer av format kan jag spara i förutom CSV?
Aspose.Cells tillåter sparning i flera format, inklusive XLSX, PDF och mer.
### Kan jag bearbeta stora Excel-filer med Aspose.Cells?
Ja, Aspose.Cells är utformat för att hantera stora filer effektivt, men prestandan kan bero på systemresurser.
### Var kan jag hitta mer detaljerad dokumentation?
Du hittar omfattande dokumentation och exempel på deras [referensplats](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}