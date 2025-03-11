---
title: Ställ in första sidnummer för kalkylblad
linktitle: Ställ in första sidnummer för kalkylblad
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du ställer in första sidnumret i Excel-kalkylblad med Aspose.Cells för .NET med denna lättanvända guide. Steg-för-steg instruktioner medföljer.
weight: 21
url: /sv/net/worksheet-page-setup-features/set-first-page-number/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ställ in första sidnummer för kalkylblad

## Introduktion
Att ställa in det första sidnumret i ett Excel-kalkylblad kan vara en förändring om du formaterar sidor för utskrift eller får ditt dokument att se mer professionellt ut. I den här handledningen kommer vi att dela upp hur man ställer in det första sidnumret i ett kalkylblad med Aspose.Cells för .NET. Oavsett om du numrerar sidor för enkel referens eller anpassar dig till ett större dokument, erbjuder Aspose.Cells ett kraftfullt men enkelt sätt att få det gjort.
## Förutsättningar
Innan vi börjar, se till att du har följande:
-  Aspose.Cells för .NET Library: Du kan ladda ner den senaste versionen[här](https://releases.aspose.com/cells/net/).
- .NET-utvecklingsmiljö: Visual Studio fungerar bra, men alla .NET-kompatibla redigerare är bra.
- Grundläggande kunskaper i C# och Excel: Bekantskap med C# och Excel-filhantering är till hjälp.
 För all installationsvägledning, kolla in[Aspose.Cells dokumentation](https://reference.aspose.com/cells/net/).
## Importera paket
Innan du börjar, importera den nödvändiga Aspose.Cells-namnrymden i ditt C#-projekt för att arbeta med biblioteket:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
I den här guiden går vi igenom stegen för att ställa in första sidnumret i ett kalkylblad i Excel med Aspose.Cells för .NET.
## Steg 1: Definiera katalogsökvägen
För att göra ditt filsparande smidigt, börja med att ange en katalogsökväg där ditt dokument ska sparas. Detta gör det lättare att hitta och organisera dina utdatafiler.
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
```
 Här, byt ut`"Your Document Directory"` med den faktiska sökvägen du vill använda. Denna variabel hjälper till att referera till platsen för att spara den slutliga utdatafilen.
## Steg 2: Initiera arbetsboksobjektet
 Skapa nu en ny instans av`Workbook` klass. Tänk på detta som kärnbehållaren i din Excel-fil. Det här objektet representerar hela arbetsboken, där varje ark, cell och inställning lagras.
```csharp
// Instantiera ett arbetsboksobjekt
Workbook workbook = new Workbook();
```
 Genom att skapa en`Workbook`, sätter du scenen för alla dina Excel-relaterade anpassningar.
## Steg 3: Öppna arbetsbladet
En arbetsbok kan innehålla flera arbetsblad. För att ställa in sidnumret på ett specifikt kalkylblad, öppna det första genom att inrikta index`0`. Detta låter dig konfigurera arket i arbetsboken.
```csharp
// Åtkomst till det första kalkylbladet i Excel-filen
Worksheet worksheet = workbook.Worksheets[0];
```
 Om din arbetsbok innehåller flera ark kan du komma åt var och en genom att ändra indexet. Till exempel,`workbook.Worksheets[1]` skulle komma åt det andra kalkylbladet.
## Steg 4: Ställ in det första sidnumret
Nu kommer kärnsteget - att ställa in det första sidnumret. Som standard börjar Excel sidnumrering vid 1, men du kan justera den så att den börjar med valfritt nummer. Detta är särskilt användbart om du fortsätter en sekvens från ett annat dokument.
```csharp
// Ställa in det första sidnumret på kalkylbladssidorna
worksheet.PageSetup.FirstPageNumber = 2;
```
I det här exemplet börjar sidnumret från 2 när du skriver ut dokumentet. Du kan ställa in det till vilket heltal som helst som passar dina behov.
## Steg 5: Spara arbetsboken
Det sista steget är att spara din arbetsbok med de ändrade inställningarna. Ange filformatet och sökvägen så att du kan granska dina ändringar i Excel.
```csharp
// Spara arbetsboken.
workbook.Save(dataDir + "SetFirstPageNumber_out.xls");
```
 Här,`"SetFirstPageNumber_out.xls"`är namnet på utdatafilen. Du kan byta namn på den baserat på dina önskemål. När du har sparat den öppnar du filen i Excel för att se den uppdaterade sidnumreringen.
## Slutsats
Att ställa in första sidnumret i ett Excel-kalkylblad med Aspose.Cells för .NET är enkelt, särskilt när du bryter ner det steg för steg. Med bara några rader kod kan du styra sidnumreringen för att förbättra ditt dokuments professionalism och läsbarhet. Den här funktionen är ovärderlig för tryckta rapporter, formella presentationer och mer.
## FAQ's
### Kan jag ställa in första sidnumret till vilket värde som helst?  
Ja, du kan ställa in första sidnumret till valfritt heltal, beroende på dina krav.
### Vad händer om jag inte ställer in ett första sidnummer?  
Om det inte anges startar Excel som standard sidnumret på 1.
### Behöver jag en licens för att använda Aspose.Cells?  
 Ja, för full funktionalitet i en produktionsmiljö behöver du en licens. Du kan[få en gratis provperiod](https://releases.aspose.com/) eller[köp en här](https://purchase.aspose.com/buy).
### Fungerar den här metoden med andra kalkylbladsegenskaper?  
Ja, Aspose.Cells låter dig kontrollera olika kalkylbladsegenskaper som sidhuvuden, sidfötter och marginaler.
### Var kan jag hitta mer dokumentation om Aspose.Cells?  
 För detaljerade guider och API-referenser, besök[Aspose.Cells dokumentation](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
