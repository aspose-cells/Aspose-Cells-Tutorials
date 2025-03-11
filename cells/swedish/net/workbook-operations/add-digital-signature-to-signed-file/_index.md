---
title: Lägg till digital signatur till signerad Excel-fil
linktitle: Lägg till digital signatur till signerad Excel-fil
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du lägger till en digital signatur i en redan signerad Excel-fil med Aspose.Cells för .NET i den här steg-för-steg-guiden. Säkra dina dokument.
weight: 12
url: /sv/net/workbook-operations/add-digital-signature-to-signed-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till digital signatur till signerad Excel-fil

## Introduktion
dagens digitala värld är det avgörande att säkerställa dokumentens autenticitet och integritet. Digitala signaturer fungerar som ett robust sätt att verifiera att ett dokument inte har ändrats och att det kommer från en legitim källa. Om du arbetar med Excel-filer i .NET och vill lägga till en digital signatur till en fil som redan är signerad, är du på rätt plats! I den här guiden går vi igenom processen att lägga till en ny digital signatur till en befintlig signerad Excel-fil med Aspose.Cells för .NET. 
## Förutsättningar
Innan vi dyker in i det nitty-gritty, låt oss se till att du har allt du behöver för att komma igång:
1.  Aspose.Cells för .NET: Först och främst måste du ha Aspose.Cells installerat i din .NET-miljö. Du kan ladda ner den från[släpp sida](https://releases.aspose.com/cells/net/).
2. .NET Framework: Se till att du har konfigurerat .NET Framework på din dator. Den här guiden förutsätter att du är bekant med grundläggande .NET-programmeringskoncept.
3. Digitalt certifikat: Du behöver ett giltigt digitalt certifikat (i .pfx-format) för att skapa en digital signatur. Om du inte har ett, kan du skapa ett självsignerat certifikat för teständamål.
4. Utvecklingsmiljö: En kodredigerare eller IDE som Visual Studio där du kan skriva och köra din C#-kod.
5. Exempel på Excel-fil: Du bör ha en befintlig Excel-fil som redan är digitalt signerad. Det här kommer att vara filen vi lägger till en annan signatur till.
Med dessa förutsättningar ur vägen, låt oss hoppa in i koden!
## Importera paket
Innan du börjar koda, se till att importera de nödvändiga namnrymden. Här är vad du behöver inkludera överst i din C#-fil:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Dessa namnrymder ger dig tillgång till de klasser och metoder som krävs för att manipulera Excel-filer och hantera digitala signaturer.
Låt oss nu dela upp processen i hanterbara steg. Vi går igenom varje steg för att säkerställa att du förstår hur du lägger till en digital signatur i en redan signerad Excel-fil.
## Steg 1: Definiera dina kataloger
Först måste du ange var dina källfiler finns och var du ska spara utdatafilen. Detta är enkelt men avgörande:
```csharp
// Källkatalog
string sourceDir = "Your Document Directory"; // Ersätt med din faktiska katalog
// Utdatakatalog
string outputDir = "Your Document Directory"; // Ersätt med din faktiska katalog
```
 Ersätta`"Your Document Directory"` med den faktiska sökvägen där dina filer lagras. Detta sätter scenen för dina filoperationer.
## Steg 2: Ladda den befintliga signerade arbetsboken
Därefter ska du ladda den befintliga Excel-arbetsboken som redan är signerad. Det är här magin börjar:
```csharp
// Ladda arbetsboken som redan är digitalt signerad för att lägga till ny digital signatur
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```
 Denna rad initierar en ny`Workbook` objekt med den angivna filen. Se till att filnamnet matchar din befintliga signerade Excel-fil.
## Steg 3: Skapa en digital signatursamling
För att hantera dina digitala signaturer måste du skapa en samling. Detta gör att du kan hålla flera signaturer om det behövs:
```csharp
// Skapa den digitala signatursamlingen
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```
Den här samlingen kommer att vara där du lägger till din nya digitala signatur innan du applicerar den på arbetsboken.
## Steg 4: Ladda ditt certifikat
Nu är det dags att ladda ditt digitala certifikat. Detta certifikat kommer att användas för att skapa den nya signaturen:
```csharp
// Certifikatfil och dess lösenord
string certFileName = sourceDir + "AsposeDemo.pfx"; // Din certifikatfil
string password = "aspose"; //Ditt certifikatlösenord
// Skapa nytt certifikat
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```
 Se till att byta ut`AsposeDemo.pfx` med namnet på din certifikatfil och uppdatera lösenordet därefter. Detta steg är avgörande eftersom utan rätt certifikat kommer du inte att kunna skapa en giltig signatur.
## Steg 5: Skapa en ny digital signatur
Med ditt certifikat laddat kan du nu skapa en ny digital signatur. Denna signatur kommer att läggas till i din samling:
```csharp
// Skapa ny digital signatur och lägg till den i digital signatursamling
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
dsCollection.Add(signature);
```
Här lämnar du ett meddelande som beskriver signaturen, vilket kan vara till hjälp för journalföringen. Tidsstämpeln säkerställer att signaturen är associerad med rätt tidpunkt.
## Steg 6: Lägg till signatursamlingen i arbetsboken
Efter att ha skapat signaturen är det dags att lägga till hela samlingen i arbetsboken:
```csharp
// Lägg till digital signatursamling i arbetsboken
workbook.AddDigitalSignature(dsCollection);
```
Detta steg tillämpar effektivt din nya digitala signatur på arbetsboken och markerar den med den extra äktheten.
## Steg 7: Spara arbetsboken
Spara slutligen arbetsboken med den nya digitala signaturen som ingår. Det här är ögonblicket då allt ditt hårda arbete lönar sig:
```csharp
//Spara arbetsboken och kassera den.
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```
Se till att ange ett namn för din utdatafil. Detta kommer att vara den nya versionen av din Excel-fil, komplett med den extra digitala signaturen.
## Steg 8: Bekräfta framgång
För att avsluta saken är det en bra idé att ge feedback när operationen har slutförts framgångsrikt:
```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```
Den här raden kommer att skriva ut ett bekräftelsemeddelande till konsolen som låter dig veta att allt gick smidigt.
## Slutsats
Och där har du det! Du har framgångsrikt lagt till en ny digital signatur till en redan signerad Excel-fil med Aspose.Cells för .NET. Denna process ökar inte bara säkerheten för dina dokument utan säkerställer också att de är pålitliga och verifierbara. 
Digitala signaturer är viktiga i dagens digitala landskap, särskilt för företag och yrkesverksamma som behöver upprätthålla integriteten hos sina dokument. Genom att följa den här guiden kan du enkelt hantera digitala signaturer i dina Excel-filer och se till att dina data förblir säkra och autentiska.
## FAQ's
### Vad är en digital signatur?
En digital signatur är ett matematiskt schema för att verifiera äktheten och integriteten hos digitala meddelanden eller dokument. Den säkerställer att dokumentet inte har ändrats och bekräftar undertecknarens identitet.
### Behöver jag ett speciellt certifikat för att skapa en digital signatur?
Ja, du behöver ett digitalt certifikat utfärdat av en betrodd certifikatutfärdare (CA) för att skapa en giltig digital signatur.
### Kan jag använda ett självsignerat certifikat för testning?
Absolut! Du kan skapa ett självsignerat certifikat för utvecklings- och testsyften, men för produktion är det bäst att använda ett certifikat från en betrodd CA.
### Vad händer om jag försöker lägga till en signatur i ett icke-signerat dokument?
Om du försöker lägga till en digital signatur i ett dokument som inte redan är signerat kommer det att fungera utan problem, men den ursprungliga signaturen kommer inte att finnas.
### Var kan jag hitta mer information om Aspose.Cells?
 Du kan kontrollera[Aspose.Cells dokumentation](https://reference.aspose.com/cells/net/) för detaljerade guider och API-referenser.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
