---
title: Lägg till digital signatur till en redan signerad Excel-fil
linktitle: Lägg till digital signatur till en redan signerad Excel-fil
second_title: Aspose.Cells för .NET API-referens
description: Lär dig hur du lägger till en digital signatur i en redan signerad Excel-fil med Aspose.Cells för .NET med denna detaljerade steg-för-steg-guide.
weight: 30
url: /sv/net/excel-workbook/add-digital-signature-to-an-already-signed-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till digital signatur till en redan signerad Excel-fil

## Introduktion

I dagens digitala värld är det viktigare än någonsin att säkra dokument. Digitala signaturer ger ett sätt att säkerställa äktheten och integriteten hos dina filer, särskilt när du hanterar känslig information. Om du arbetar med Excel-filer och vill lägga till en ny digital signatur i en arbetsbok som redan är signerad, är du på rätt plats! I den här guiden går vi igenom processen att lägga till en digital signatur till en redan signerad Excel-fil med Aspose.Cells för .NET. Så, låt oss dyka in!

## Förutsättningar

Innan vi går in i det snälla med kodning, finns det några saker du måste ha på plats:

1.  Aspose.Cells för .NET: Se till att du har Aspose.Cells-biblioteket installerat i ditt .NET-projekt. Du kan ladda ner den från[plats](https://releases.aspose.com/cells/net/).
2.  Certifikatfil: Du behöver en giltig certifikatfil (vanligtvis en`.pfx`fil) som innehåller ditt digitala certifikat. Se till att du känner till lösenordet för den här filen.
3. Utvecklingsmiljö: Konfigurera din utvecklingsmiljö med Visual Studio eller någon annan IDE som stöder .NET.
4. Grundläggande kunskaper i C#: Bekantskap med C#-programmering hjälper dig att följa med smidigt.
5. Exempelfiler: Ha ett exempel på Excel-fil som redan är digitalt signerad. Detta kommer att vara filen som du lägger till en ny signatur till.

Nu när vi har allt på plats, låt oss börja koda!

## Importera paket

För att komma igång måste du importera de nödvändiga paketen i din C#-fil. Så här gör du:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Dessa namnutrymmen låter dig arbeta med Excel-filer och hantera digitala signaturer sömlöst.

## Steg 1: Ställ in dina käll- och utdatakataloger

Innan du kan manipulera dina Excel-filer måste du definiera var dina källfiler finns och var du vill spara utdatafilen. Så här gör du:

```csharp
// Källkatalog
string sourceDir = "Your Document Directory";
// Utdatakatalog
string outputDir = "Your Document Directory";
```

I det här steget använder vi en metod för att få sökvägarna för käll- och utdatakatalogerna. Se till att dessa kataloger finns och innehåller de nödvändiga filerna.

## Steg 2: Ladda den redan signerade arbetsboken

 Därefter måste du ladda Excel-arbetsboken som du vill ändra. Detta görs genom att skapa en instans av`Workbook` klass och passerar sökvägen till den signerade filen.

```csharp
// Ladda arbetsboken som redan är digitalt signerad
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```

 Här laddar vi arbetsboken med namnet`sampleDigitallySignedByCells.xlsx`. Se till att den här filen redan är signerad.

## Steg 3: Skapa en digital signatursamling

Låt oss nu skapa en digital signatursamling. Den här samlingen kommer att innehålla alla digitala signaturer som du vill lägga till i arbetsboken.

```csharp
// Skapa den digitala signatursamlingen
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```

Detta steg är avgörande eftersom det låter dig hantera flera signaturer om det behövs.

## Steg 4: Skapa ett nytt certifikat

 Du måste ladda din certifikatfil för att skapa en ny digital signatur. Det är här du anger sökvägen till din`.pfx` filen och dess lösenord.

```csharp
// Certifikatfil och dess lösenord
string certFileName = sourceDir + "AsposeDemo.pfx";
string password = "aspose";

// Skapa nytt certifikat
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```

 Se till att byta ut`AsposeDemo.pfx`och lösenordet med ditt faktiska certifikatfilnamn och lösenord.

## Steg 5: Skapa den digitala signaturen

Med certifikatet i handen kan du nu skapa en digital signatur. Du vill också ange en anledning till signaturen och aktuellt datum och tid.

```csharp
// Skapa ny digital signatur och lägg till den i digital signatursamling
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
```

Det här steget lägger till den nya signaturen i din samling, som du senare kommer att tillämpa på arbetsboken.

## Steg 6: Lägg till den digitala signatursamlingen i arbetsboken

Nu är det dags att lägga till den digitala signatursamlingen i arbetsboken. Det är här magin händer!

```csharp
// Lägg till digital signatursamling i arbetsboken
workbook.AddDigitalSignature(dsCollection);
```

Genom att köra den här raden bifogar du effektivt den nya digitala signaturen till den redan signerade arbetsboken.

## Steg 7: Spara och kassera arbetsboken

Slutligen vill du spara den modifierade arbetsboken i din utdatakatalog och släppa alla resurser som används.

```csharp
//Spara arbetsboken och kassera den.
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```

Det här steget säkerställer att dina ändringar sparas och att arbetsboken kasseras på rätt sätt för att frigöra resurser.

## Steg 8: Bekräfta exekvering

För att avsluta saken är det en bra idé att bekräfta att din kod kördes framgångsrikt. Du kan göra detta med ett enkelt konsolmeddelande.

```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```

Detta ger feedback om att din operation var framgångsrik, vilket alltid är trevligt att se!

## Slutsats

Och där har du det! Du har framgångsrikt lagt till en ny digital signatur till en redan signerad Excel-fil med Aspose.Cells för .NET. Digitala signaturer är ett kraftfullt sätt att säkerställa äktheten av dina dokument, och nu vet du hur du hanterar dem programmatiskt. Oavsett om du arbetar med finansiella dokument, kontrakt eller annan känslig information, kan implementering av digitala signaturer öka säkerheten och förtroendet.

## FAQ's

### Vad är en digital signatur?
En digital signatur är en kryptografisk metod som används för att validera äktheten och integriteten hos ett meddelande eller dokument.

### Kan jag lägga till flera digitala signaturer i samma Excel-fil?
Ja, du kan skapa en digital signatursamling och lägga till flera signaturer i samma arbetsbok.

### Vilka format stöder Aspose.Cells för digitala signaturer?
 Aspose.Cells stöder olika format, inklusive`.pfx` för certifikat.

### Behöver jag en specifik version av .NET för att använda Aspose.Cells?
 Kontrollera[Aspose.Cells dokumentation](https://reference.aspose.com/cells/net/) för kompatibilitet med din .NET-version.

### Hur kan jag få en tillfällig licens för Aspose.Cells?
 Du kan begära en tillfällig licens från[Asposes köpsida](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
