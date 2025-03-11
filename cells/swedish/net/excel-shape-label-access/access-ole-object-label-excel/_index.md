---
title: Få tillgång till OLE Object Label i Excel
linktitle: Få tillgång till OLE Object Label i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du kommer åt och ändrar OLE-objektetiketter i Excel med Aspose.Cells för .NET. Enkel guide med kodexempel ingår.
weight: 10
url: /sv/net/excel-shape-label-access/access-ole-object-label-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Få tillgång till OLE Object Label i Excel

## Introduktion
Om du någonsin har sysslat med Excel vet du hur kraftfullt och komplicerat det kan vara. Ibland kan du snubbla över data inbäddade i OLE-objekt (Object Linking and Embedding) - se det som ett "minifönster" till ett annat programverktyg, som ett Word-dokument eller en PowerPoint-bild, allt bekvämt inbäddat i ditt kalkylark. Men hur kommer vi åt och manipulerar dessa etiketter i våra OLE-objekt med Aspose.Cells för .NET? Spänn fast dig, för i den här handledningen delar vi upp det steg för steg!
## Förutsättningar
 
Innan vi hoppar in i den actionfyllda världen av Aspose.Cells för .NET, här är vad du behöver ha i din verktygslåda:
1. Visual Studio installerad: Detta kommer att vara din lekplats där du kommer att koda och testa din C#-applikation.
2. .NET Framework: Se till att du arbetar med minst .NET Framework 4.0 eller högre. Detta kommer att ge vårt program den nödvändiga grunden för att fungera smidigt.
3.  Aspose.Cells Library: Du behöver en kopia av Aspose.Cells-biblioteket. Du kan ladda ner den från[här](https://releases.aspose.com/cells/net/) . Om du vill prova innan du köper, kolla in[gratis provperiod](https://releases.aspose.com/).
4. Grundläggande förståelse för C#: Bekantskap med C# hjälper dig att ta dig igenom koden.
Med det ur vägen, låt oss dyka in i det rena med att komma åt och ändra etiketter på OLE-objekt!
## Importera paket 
För att börja måste vi importera de nödvändiga paketen till vårt projekt. Detta kommer att göra våra liv enklare genom att ge oss tillgång till alla funktioner och klasser vi behöver. Så här gör du:
### Skapa ett nytt C#-projekt 
- Öppna Visual Studio och skapa ett nytt C# Console Application-projekt.
- Döp det till något i stil med "OLEObjectLabelExample".
### Lägg till Aspose.Cells Reference 
- Högerklicka på ditt projekt i Solution Explorer.
- Välj "Hantera NuGet-paket".
- Sök efter "Aspose.Cells" och installera biblioteket.
### Importera namnområden
 Överst i din programfil (t.ex.`Program.cs`), måste du importera de nödvändiga namnrymden:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Dessa namnrymder hjälper oss komma åt klasser och metoder som behövs för våra Excel-manipulationer.
Nu när allt är på plats, låt oss komma åt och ändra etiketten för ett OLE-objekt inbäddat i en Excel-fil. Följ steg-för-steg-guiden nedan:
## Steg 1: Ställ in källkatalogen
 Först definierar vi katalogen där ditt Excel-dokument finns. Ersätta`"Your Document Directory"` med din faktiska dokumentsökväg.
```csharp
string sourceDir = "Your Document Directory";
```
## Steg 2: Ladda Excel-exempelfilen 
Därefter laddar vi .xlsx Excel-filen som innehåller vårt OLE-objekt:
```csharp
Workbook wb = new Workbook(sourceDir + "sampleAccessAndModifyLabelOfOleObject.xlsx");
```
 Denna rad initierar en`Workbook` objekt som ger oss tillgång till alla kalkylblad och komponenter i Excel-filen.
## Steg 3: Öppna det första arbetsbladet
Låt oss nu komma åt det första kalkylbladet i vår arbetsbok:
```csharp
Worksheet ws = wb.Worksheets[0];
```
 Här,`Worksheets[0]` är det första arbetsbladet i samlingen.
## Steg 4: Öppna det första OLE-objektet 
Därefter hämtar vi det första OLE-objektet:
```csharp
Aspose.Cells.Drawing.OleObject oleObject = ws.OleObjects[0];
```
Detta gör att vi kan interagera med OLE-objektet vi vill arbeta med.
## Steg 5: Visa etiketten för OLE-objektet
Innan vi ändrar etiketten, låt oss skriva ut dess nuvarande värde:
```csharp
Console.WriteLine("Ole Object Label - Before: " + oleObject.Label);
```
Detta ger oss en tydlig bild av etiketten innan några ändringar görs.
## Steg 6: Ändra etiketten 
Nu till det roliga - låt oss ändra etiketten för OLE-objektet:
```csharp
oleObject.Label = "Aspose APIs";
```
Du kan ställa in detta till vad du vill. "Aspose APIs" är bara ett snyggt sätt att visa vad vi gör.
## Steg 7: Spara arbetsboken i minnesström 
Vi sparar sedan våra ändringar i en minnesström innan vi laddar om arbetsboken:
```csharp
MemoryStream ms = new MemoryStream();
wb.Save(ms, SaveFormat.Xlsx);
```
Detta sparar vår modifierade arbetsbok i minnet, vilket gör det enkelt att komma åt senare.
## Steg 8: Ställ in arbetsboksreferensen på Null 
För att rensa minnet bör vi ställa in arbetsboksreferensen till null:
```csharp
wb = null;
```
## Steg 9: Ladda arbetsbok från Memory Stream 
Därefter laddar vi om vår arbetsbok från minnesströmmen vi just sparade:
```csharp
wb = new Workbook(ms);
```
## Steg 10: Öppna det första arbetsbladet igen 
Precis som tidigare måste vi komma åt det första kalkylbladet igen:
```csharp
ws = wb.Worksheets[0];
```
## Steg 11: Åtkomst till det första OLE-objektet igen
Hämta nu OLE-objektet igen för den sista kontrollen:
```csharp
oleObject = ws.OleObjects[0];
```
## Steg 12: Visa den modifierade etiketten 
För att se om våra ändringar trädde i kraft, låt oss skriva ut den nya etiketten:
```csharp
Console.WriteLine("Ole Object Label - After: " + oleObject.Label);
```
## Steg 13: Bekräfta exekvering 
Till sist, ge ett framgångsmeddelande så att vi vet att allt gick som planerat:
```csharp
Console.WriteLine("AccessAndModifyLabelOfOleObject executed successfully.");
```
## Slutsats 
Och där har du det! Du har framgångsrikt öppnat och ändrat etiketten för ett OLE-objekt i Excel med Aspose.Cells för .NET. Det är ett utmärkt sätt att sätta en personlig touch till dina inbäddade dokument, vilket förbättrar tydlighet och kommunikation i dina kalkylblad. 
Oavsett om du utvecklar en cool applikation eller bara piffar upp dina rapporter, kan manipulera OLE-objekt vara en spelomvandlare. Fortsätt utforska vad Aspose.Cells erbjuder, så kommer du att upptäcka en hel värld av möjligheter.
## FAQ's
### Vad är ett OLE-objekt i Excel?  
OLE-objekt är inbäddade filer som låter dig integrera dokument från andra Microsoft Office-program i ett Excel-kalkylblad.
### Kan Aspose.Cells fungera med andra filformat?  
Ja! Aspose.Cells stöder en mängd olika format, inklusive XLS, XLSX, CSV och mer.
### Finns det en gratis testversion tillgänglig för Aspose.Cells?  
 Ja! Du kan prova det[här](https://releases.aspose.com/).
### Kan jag komma åt flera OLE-objekt i ett kalkylblad?  
Absolut! Du kan gå igenom`ws.OleObjects` för att komma åt alla inbäddade OLE-objekt i ett kalkylblad.
### Hur köper jag en licens för Aspose.Cells?  
 Du kan köpa en licens direkt från[här](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
