---
title: Spara arbetsboken i text-CSV-format
linktitle: Spara arbetsboken i text-CSV-format
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du enkelt konverterar Excel-arbetsböcker till CSV-format med Aspose.Cells i denna omfattande, steg-för-steg handledning utformad för .NET-utvecklare.
weight: 17
url: /sv/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Spara arbetsboken i text-CSV-format

## Introduktion
När du hanterar data kan formatet du väljer verkligen avgöra hur enkelt du kan arbeta med det. Bland de vanligaste formaten för hantering av tabelldata är CSV (Comma-Separated Values). Om du är en utvecklare som arbetar med Excel-filer och behöver konvertera arbetsböcker till CSV-format, är Aspose.Cells för .NET ett fantastiskt bibliotek som förenklar denna uppgift. I den här handledningen kommer vi att bryta ner stegen för att sömlöst konvertera en Excel-arbetsbok till ett text-CSV-format.
## Förutsättningar
Innan vi dyker in, låt oss se till att du har allt på plats för att komma igång:
1. Grundläggande kunskaper om C# och .NET: Eftersom vi kommer att skriva kod i C#, är det viktigt att du känner till språket och .NET-ramverket.
2. Aspose.Cells Library: Se till att du har Aspose.Cells for .NET-biblioteket installerat i din utvecklingsmiljö. Du kan ladda ner den[här](https://releases.aspose.com/cells/net/).
3. Visual Studio eller valfri C# IDE: Du behöver en integrerad utvecklingsmiljö (IDE) för att skriva och köra din kod. Visual Studio är ett populärt val.
4. Excel-arbetsbok: Förbered ett exempel på Excel-arbetsbok (t.ex. "book1.xls") som innehåller data för att testa konverteringen.
## Importera paket
Nu när vi har täckt våra förutsättningar är det första steget i processen att importera de nödvändiga paketen. I ditt C#-projekt måste du inkludera följande namnområde överst i din kodfil:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Dessa namnrymder ger dig tillgång till de klasser och metoder som behövs för att arbeta med Excel-filer och hantera minnesströmmar.
## Steg 1: Definiera sökvägen till dokumentkatalogen
Det första steget i vår process är att definiera var våra dokument (Excel-arbetsböcker) lagras. Detta är viktigt eftersom det gör att vårt program kan veta var det ska hitta filerna som det behöver bearbeta. 
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
```
 Se till att byta ut`"Your Document Directory"` med den faktiska sökvägen där din "book1.xls"-fil finns. Detta kan vara en katalog på din dator eller en sökväg till en server.
## Steg 2: Ladda din källarbetsbok
Därefter måste vi ladda Excel-arbetsboken som kommer att konverteras till CSV-format.
```csharp
// Ladda din källarbetsbok
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 De`Workbook` klass från Aspose.Cells-biblioteket möjliggör manipulering och åtkomst till Excel-arbetsböcker. Genom att skicka filsökvägen laddar vi den angivna arbetsboken för bearbetning.
## Steg 3: Initiera en bytearray för arbetsboksdata
Innan vi börjar konvertera arbetsboken till CSV måste vi initiera en tom byte-array som så småningom kommer att hålla alla kalkylbladsdata.
```csharp
// 0-byte array
byte[] workbookData = new byte[0];
```
Denna byte-array kommer att kombinera data från varje kalkylblad till en enda struktur som vi kan skriva ut till en fil senare.
## Steg 4: Ställ in alternativ för textspara
Låt oss nu ställa in alternativen för hur vi vill spara textformatet. Du kan välja anpassade avgränsare eller hålla dig till flikar.
```csharp
// Alternativ för att spara text. Du kan använda vilken typ av separator som helst
TxtSaveOptions opts = new TxtSaveOptions();
opts.Separator = '\t'; // Inställning av flik som avgränsare
```
 I det här exemplet använder vi ett tabbtecken som avgränsare. Du kan byta ut`'\t'` med vilken karaktär du vill, som ett kommatecken (`,`), beroende på hur du vill ha din CSV-formaterad.
## Steg 5: Iterera genom varje arbetsblad
 Därefter går vi igenom alla kalkylblad i arbetsboken och sparar var och en i vår`workbookData` array, men du måste först välja vilket kalkylblad du vill arbeta på.
```csharp
// Kopiera varje kalkylbladsdata i textformat inuti arbetsboksdatamatrisen
for (int idx = 0; idx < workbook.Worksheets.Count; idx++)
{
    // Spara det aktiva kalkylbladet i textformat
    MemoryStream ms = new MemoryStream();
    workbook.Worksheets.ActiveSheetIndex = idx;
    workbook.Save(ms, opts);
```
 Slingan går igenom varje kalkylblad i arbetsboken.`ActiveSheetIndex` är inställd så att varje gång genom slingan, vi sparar det aktuella kalkylbladet. Resultaten kommer att sparas i minnet med hjälp av a`MemoryStream`.
## Steg 6: Hämta kalkylbladsdata
 Efter att ha sparat ett kalkylblad i minnesströmmen är nästa steg att hämta denna data och lägga till den i vår`workbookData` array.
```csharp
    // Spara kalkylbladets data i arkdatamatrisen
    ms.Position = 0; // Återställ positionen för minnesströmmen
    byte[] sheetData = ms.ToArray(); // Hämta byte-arrayen
```
`ms.Position = 0;` återställer positionen för läsning efter att ha skrivit. Sedan använder vi`ToArray()` för att konvertera minnesströmmen till en byte-array som innehåller kalkylbladsdata.
## Steg 7: Kombinera kalkylbladsdata
 Nu kommer vi att kombinera data från varje kalkylblad till singeln`workbookData` array initierats tidigare.
```csharp
    // Kombinera denna kalkylbladsdata till arbetsboksdatamatris
    byte[] combinedArray = new byte[workbookData.Length + sheetData.Length];
    Array.Copy(workbookData, 0, combinedArray, 0, workbookData.Length);
    Array.Copy(sheetData, 0, combinedArray, workbookData.Length, sheetData.Length);
    workbookData = combinedArray;
}
```
Vi skapar en ny array som är tillräckligt stor för att rymma både befintliga arbetsboksdata och nya kalkylbladsdata. Vi kopierar sedan befintliga och nya data till denna kombinerade array för senare användning.
## Steg 8: Spara hela arbetsbokdata i fil
 Slutligen, med all data kombinerad i vår`workbookData` array, kan vi spara denna array till en specificerad filsökväg.
```csharp
//Spara hela arbetsboksdata i en fil
File.WriteAllBytes(dataDir + "out.txt", workbookData);
```
`WriteAllBytes` tar den kombinerade byte-arrayen och skriver den till en textfil med namnet "out.txt" i den angivna katalogen.
## Slutsats
Och där har du det! Du har framgångsrikt konverterat en Excel-arbetsbok till ett CSV-format med Aspose.Cells för .NET. Denna process är inte bara effektiv, utan den möjliggör enkel manipulering av Excel-data för ytterligare analys eller rapportering. Nu kan du automatisera dina databearbetningsuppgifter eller till och med integrera denna funktion i större applikationer.
## FAQ's
### Kan jag använda olika avgränsare för CSV-filen?
 Ja, du kan ändra`opts.Separator` till vilken karaktär du vill, till exempel kommatecken eller pipor.
### Är Aspose.Cells gratis att använda?
 Aspose.Cells är inte gratis, men du kan få en gratis provperiod[här](https://releases.aspose.com/).
### Vilka typer av format kan jag spara i förutom CSV?
Aspose.Cells tillåter att spara till flera format inklusive XLSX, PDF och mer.
### Kan jag bearbeta stora Excel-filer med Aspose.Cells?
Ja, Aspose.Cells är utformad för att hantera stora filer effektivt, men prestanda kan bero på systemresurser.
### Var kan jag hitta mer detaljerad dokumentation?
Du kan hitta omfattande dokumentation och exempel på deras[referenssida](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
