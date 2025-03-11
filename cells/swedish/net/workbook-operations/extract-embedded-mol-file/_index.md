---
title: Extrahera inbäddad Mol-fil från arbetsbok
linktitle: Extrahera inbäddad Mol-fil från arbetsbok
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du extraherar inbäddade MOL-filer från Excel-arbetsböcker med Aspose.Cells för .NET i denna detaljerade steg-för-steg-handledning.
weight: 18
url: /sv/net/workbook-operations/extract-embedded-mol-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera inbäddad Mol-fil från arbetsbok

## Introduktion
När det gäller att hantera data i Excel-arbetsböcker, stöter man ibland på olika inbäddade objekt som inte är i standardformat. Ett sådant format är MOL (Molecular Structure File), som vanligtvis används inom kemi för att representera molekylär information. Om du vill extrahera dessa MOL-filer från en Excel-arbetsbok med Aspose.Cells för .NET, har du hamnat på rätt guide. I den här artikeln går vi igenom processen steg-för-steg, och avmystifierar varje del på vägen.
## Förutsättningar
Innan du dyker in i koden är det viktigt att se till att du har nödvändiga färdigheter och verktyg. Här är vad du behöver:
1. Grundläggande förståelse för .NET-programmering: Du bör vara bekant med C# och .NET-ramverket.
2.  Aspose.Cells för .NET: Se till att du har Aspose.Cells-biblioteket. Du kan[ladda ner den här](https://releases.aspose.com/cells/net/).
3. En IDE: Du kan använda Visual Studio eller någon annan .NET-kompatibel IDE.
4. Excel-arbetsbok med inbäddade MOL-filer: För den här handledningen behöver du en Excel-fil som innehåller MOL-objekt. Du kan skapa din egen eller använda valfri exempelfil.
## Importera paket
För att komma igång måste du importera de nödvändiga namnrymden i ditt projekt. Detta är avgörande för att få tillgång till Aspose.Cells-funktionerna. Så här kan du göra det:

```csharp
using Aspose.Cells.Drawing;
using Aspose.Cells.WebExtensions;
using System;
using System.IO;
```

Dessa namnutrymmen låter dig manipulera arbetsböcker, komma åt arbetsblad och arbeta med filer i allmänhet.
Nu när vi har löst våra förutsättningar, låt oss dyka in i koden och förstå varje steg som är involverat i att extrahera inbäddade MOL-filer från en Excel-arbetsbok. 
## Steg 1: Konfigurera dina kataloger
Det första steget är att definiera var ditt källdokument finns och var du vill spara de extraherade MOL-filerna. Låt oss skapa de katalogerna.
```csharp
string SourceDir = "Your Document Directory"; // Ersätt med din katalogsökväg
string outputDir = "Your Document Directory"; // Ersätt med din utdatabana
```
 Här byter du ut`"Your Document Directory"`med vägen till dina faktiska kataloger. Det är viktigt att både käll- och utdatakatalogerna är tillgängliga för din applikation.
## Steg 2: Ladda arbetsboken
När du har ställt in dina kataloger är nästa uppgift att ladda Excel-arbetsboken. Låt oss göra det nu.

```csharp
Workbook workbook = new Workbook(SourceDir + "EmbeddedMolSample.xlsx");
```

 Vi skapar en instans av`Workbook` klass och skickar in sökvägen till vår Excel-fil som heter`EmbeddedMolSample.xlsx`. Detta steg initierar arbetsboken, så att du kan komma åt dess innehåll.
## Steg 3: Iterera över arbetsblad
Nu när din arbetsbok är laddad måste du gå igenom varje kalkylblad i arbetsboken. Detta låter dig undersöka varje ark för inbäddade objekt.

```csharp
var index = 1; // Används för att namnge extraherade MOL-filer
foreach (Worksheet sheet in workbook.Worksheets)
{
    OleObjectCollection oles = sheet.OleObjects;
    // Ytterligare extraktionslogik går här
}
```

 Här använder du en`foreach` loop för att navigera genom kalkylbladen. För varje kalkylblad kommer du åt`OleObjects` samling, som innehåller alla inbäddade objekt.
## Steg 4: Extrahera MOL-filer
Nu kommer den kritiska delen - att extrahera MOL-filerna från OLE-objekten. Detta kräver en annan slinga inuti kalkylbladsslingan.

```csharp
foreach (OleObject ole in oles)
{
    string fileName = outputDir + "OleObject" + index + ".mol ";
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
    index++;
}
```

 För varje OLE-objekt du har hittat skapar du en ny fil i utdatakatalogen. De`ObjectData` egendom av`OleObject` innehåller data för det inbäddade objektet, som du skriver till en nyskapad fil med hjälp av en`FileStream`. Filen heter sekventiellt (`OleObject1.mol`, `OleObject2.mol` , etc.) baserat på`index` variabel.
## Steg 5: Bekräftelse på slutförande av processen
Slutligen, när alla MOL-filer har extraherats, är det bra att informera användaren om att processen har slutförts framgångsrikt.

```csharp
Console.WriteLine("ExtractEmbeddedMolFile executed successfully.");
```

Den här raden skriver helt enkelt ut ett meddelande till konsolen som låter dig veta att extraheringen lyckades. Det är en fin touch för användarfeedback.
## Slutsats
Och där har du det! Du har framgångsrikt extraherat inbäddade MOL-filer från en Excel-arbetsbok med Aspose.Cells för .NET. Denna process integrerar några kärnsteg, vilket säkerställer ett strukturerat tillvägagångssätt för att hantera inbäddade objekt. Oavsett om du arbetar med vetenskaplig forskning, kemisk analys eller helt enkelt hanterar komplexa datauppsättningar, kan att kunna extrahera och manipulera dessa filtyper göra en betydande skillnad i hur du hanterar din information. 
## FAQ's
### Kan jag extrahera andra filtyper än MOL från Excel?
Ja, du kan extrahera olika andra inbäddade filtyper med liknande tekniker.
### Är Aspose.Cells gratis att använda?
 Aspose.Cells är ett kommersiellt bibliotek, men du kan[prova gratis under en begränsad period](https://releases.aspose.com/).
### Fungerar den här metoden med alla Excel-versioner?
Ja, så länge filformatet stöds av Aspose.Cells.
### Kan jag automatisera den här utvinningsprocessen?
Absolut! Du kan automatisera denna process genom att placera koden i en schemalagd uppgift eller ett skript.
### Var kan jag hitta ytterligare dokumentation om Aspose.Cells?
 Du kan kolla in[Aspose.Cells dokumentation](https://reference.aspose.com/cells/net/) för mer information och exempel.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
