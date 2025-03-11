---
title: Specificera dokumentversionen av Excel-filen programmatiskt i .NET
linktitle: Specificera dokumentversionen av Excel-filen programmatiskt i .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du anger dokumentegenskaper som version, författare och titel i en Excel-fil programmatiskt med Aspose.Cells för .NET med steg-för-steg-instruktioner.
weight: 12
url: /sv/net/saving-and-exporting-excel-files-with-options/specifying-document-version-of-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Specificera dokumentversionen av Excel-filen programmatiskt i .NET

## Introduktion
Aspose.Cells för .NET är ett kraftfullt bibliotek som låter utvecklare programmässigt manipulera Excel-filer med lätthet. Oavsett om du vill skapa Excel-filer från grunden eller modifiera befintliga, erbjuder Aspose.Cells ett omfattande API för att uppnå dina mål. En sådan funktion är att specificera dokumentegenskaper som version, författare eller titel. Denna handledning går igenom hur du anger dokumentversionen av en Excel-fil programmatiskt med Aspose.Cells för .NET.
## Förutsättningar
Innan vi dyker in i detaljerna, låt oss se till att du har allt du behöver följa tillsammans med den här handledningen:
1. Aspose.Cells för .NET: Du kan ladda ner den senaste versionen[här](https://releases.aspose.com/cells/net/) . Om du inte har köpt en licens ännu kan du välja en[tillfällig licens](https://purchase.aspose.com/temporary-license/) för att utforska funktionerna.
2. .NET-utvecklingsmiljö: Du kan använda Visual Studio eller vilken .NET-kompatibel IDE som helst.
3. Grundläggande kunskaper i C#: Förståelse för C#-programmering gör det lättare att följa med.
## Importera paket
Innan du kan börja koda måste du importera de nödvändiga namnrymden från Aspose.Cells-biblioteket. Detta ger dig tillgång till de klasser och metoder som krävs för Excel-filmanipulation.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Dessa två namnområden kommer att vara viktiga för att interagera med arbetsboken och dess inbyggda dokumentegenskaper.
Låt oss nu bryta ner processen för att ange dokumentegenskaper i en Excel-fil, inklusive version, titel och författare.
## Steg 1: Initiera arbetsboksobjektet
 Det första steget är att skapa en ny instans av`Workbook` objekt. Detta objekt representerar hela Excel-filen du kommer att arbeta med.
```csharp
Workbook wb = new Workbook();
```
 De`Workbook`klass ger en representation av en Excel-fil. Genom att instansiera det skapar vi en tom Excel-arbetsbok som vi kan manipulera.
## Steg 2: Få åtkomst till inbyggda dokumentegenskaper
 Aspose.Cells erbjuder inbyggda dokumentegenskaper, som inkluderar fält som titel, författare och dokumentversion. Du kan komma åt dessa egenskaper via`BuiltInDocumentProperties`samling.
```csharp
Aspose.Cells.Properties.BuiltInDocumentPropertyCollection bdpc = wb.BuiltInDocumentProperties;
```
 De`BuiltInDocumentPropertyCollection` klass ger åtkomst till en samling inbyggda dokumentegenskaper, såsom titel, författare och annan metadata som vanligtvis associeras med dokumentet.
## Steg 3: Ställ in titeln på Excel-dokumentet
Därefter anger vi titeln på Excel-dokumentet. Denna metadata hjälper till att identifiera och hantera filen senare.
```csharp
bdpc.Title = "Aspose File Format APIs";
```
Att ställa in titeln är viktigt för dokumentorganisationen. Denna metadata kan ses i filegenskaper och kan användas av externa system för att katalogisera eller identifiera dokumentet mer effektivt.
## Steg 4: Ange författaren
Författaren till dokumentet kan också anges för att återspegla vem som skapade eller modifierade filen.
```csharp
bdpc.Author = "Aspose APIs Developers";
```
Det här steget hjälper till att tillskriva dokumentet till dess skapare, och tillhandahåller ytterligare metadata för dokumenthantering eller samarbetsscenarier.
## Steg 5: Ange dokumentversionen
En av de mest avgörande egenskaperna vi tar upp i den här handledningen är dokumentversionen. Det här steget låter dig ange versionen av dokumentet, vilket är användbart när du arbetar i miljöer som kräver versionskontroll.
```csharp
bdpc.DocumentVersion = "Aspose.Cells Version - 18.3";
```
Att ställa in dokumentversionen ger klarhet om vilken version av dokumentet eller biblioteket som användes för att skapa filen. Detta är särskilt viktigt i miljöer som behöver spåra filrevisioner eller kompatibilitet med olika biblioteksversioner.
## Steg 6: Spara Excel-filen
 Slutligen kan du spara Excel-filen med alla egenskaper du just har ställt in. Aspose.Cells låter dig spara filen i olika format, men för det här exemplet håller vi oss till`.xlsx` formatera.
```csharp
wb.Save("outputSpecifyDocumentVersionOfExcelFile.xlsx", SaveFormat.Xlsx);
```
 De`Save` metod används för att spara filen i din angivna katalog. Här sparar vi den som en Excel-fil i`.xlsx`formatera. Om det behövs stöder Aspose.Cells även format som`.xls`, `.csv` , och`.pdf`, vilket ger flexibilitet baserat på dina projektbehov.
## Slutsats
I den här handledningen gick vi igenom hur man anger dokumentegenskaper, särskilt dokumentversionen, i en Excel-fil med Aspose.Cells för .NET. Aspose.Cells är ett extremt flexibelt och kraftfullt verktyg som låter dig manipulera Excel-filer programmatiskt, vilket gör det till en stor tillgång för alla .NET-utvecklare som arbetar med kalkylblad.
## FAQ's
### Kan jag ändra andra inbyggda egenskaper med Aspose.Cells?  
Ja, du kan ändra andra inbyggda egenskaper som ämne, nyckelord och kommentarer, bland annat.
### Vilka filformat stöds av Aspose.Cells?  
 Aspose.Cells stöder en mängd olika format inklusive`.xls`, `.xlsx`, `.csv`, `.pdf`, och mer.
### Behöver jag en licens för att använda Aspose.Cells för .NET?  
 Du kan utforska Aspose.Cells med en[gratis provperiod](https://releases.aspose.com/) eller ansök om en[tillfällig licens](https://purchase.aspose.com/temporary-license/) för utökade tester.
### Kan jag använda Aspose.Cells i en webbapplikation?  
Ja, Aspose.Cells kan användas i både skrivbords- och webbapplikationer. Det är mycket mångsidigt och integreras väl med .NET webbramverk.
### Var kan jag få support för Aspose.Cells?  
 Du kan få tillgång till gemenskap och stöd genom[Aspose.Cells supportforum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
