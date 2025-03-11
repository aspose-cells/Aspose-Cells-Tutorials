---
title: Ställa in datafältsformat programmerat i .NET
linktitle: Ställa in datafältsformat programmerat i .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Huvudinställning av datafältsformat i pivottabeller med Aspose.Cells för .NET med denna steg-för-steg handledning. Förbättra din Excel-dataformatering.
weight: 19
url: /sv/net/creating-and-configuring-pivot-tables/setting-data-field-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ställa in datafältsformat programmerat i .NET

## Introduktion
Om du dyker in i Excel-filmanipulationer med .NET, har du förmodligen korsat vägar med datauppsättningar som kräver lite snygg formatering. Ett vanligt krav är att ställa in dina datafält, särskilt i pivottabeller, på ett sätt som gör dina data inte bara begripliga, utan även visuellt tilltalande och insiktsfulla. Med Aspose.Cells för .NET kan denna uppgift vara en bris. I den här handledningen kommer vi bokstavligen att dela upp hur man ställer in datafältsformat programmatiskt i .NET steg för steg, utmanar den skrämmande komplexiteten och gör det hela lättsmält!
## Förutsättningar
Innan vi ger oss ut på den här resan, låt oss se till att du har allt i ordning. Här är en snabb checklista över vad du behöver:
1. Visual Studio: För vem älskar inte en bra integrerad utvecklingsmiljö (IDE)?
2.  Aspose.Cells för .NET Library: Du kan enkelt ladda ner det från[Sidan Aspose Releases](https://releases.aspose.com/cells/net/).
3. Grundläggande kunskaper i C#: Om du förstår grunderna i ett programmeringsspråk är du bra att gå!
### Varför Aspose.Cells?
Aspose.Cells för .NET är ett kraftfullt bibliotek speciellt utformat för att hantera Excel-filoperationer. Det låter dig läsa, skriva, manipulera och konvertera Excel-filer enkelt. Föreställ dig att kunna skapa rapporter, pivottabeller eller till och med diagram utan att behöva gräva i Excel-gränssnittet – låter som magiskt, eller hur?
## Importera paket
Nu när vi har våra förutsättningar klara, låt oss dyka in i nästa steg. Börja med att importera nödvändiga paket. Så här kan du få igång dem:
### Skapa ett nytt projekt
Öppna Visual Studio och skapa ett nytt C#-projekt. Välj en konsolappmall eftersom vi kommer att göra backend-bearbetning.
### Lägg till referens till Aspose.Cells
1. Högerklicka på ditt projekt i Solution Explorer.
2. Välj "Hantera NuGet-paket."
3. I avsnittet Bläddra, sök efter "Aspose.Cells."
4. Installera biblioteket. När det är installerat är du redo att importera!
### Importera de nödvändiga namnområdena
Överst i din C#-kodfil lägger du till följande namnrymder:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Detta ger dig tillgång till funktionerna som erbjuds av Aspose.Cells.

Okej, nu kommer vi till det snälla i vårt program. Vi kommer att arbeta med en befintlig Excel-fil — låt oss döpa den till "Book1.xls" för den här handledningens skull.
## Steg 1: Definiera din datakatalog
Först och främst måste du tala om för ditt program var du kan hitta den värdefulla Excel-filen.
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory"; // Se till att ändra detta till din faktiska väg!
```
## Steg 2: Ladda arbetsboken
Att ladda din arbetsbok är som att öppna en bok innan du läser den. Så här gör du:
```csharp
// Ladda en mallfil
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Se till att Book1.xls sitter snyggt i den angivna katalogen, annars kan du stöta på några få hicka!
## Steg 3: Öppna det första arbetsbladet
Nu när vi har vår arbetsbok, låt oss lägga vantarna på det första arbetsbladet (som omslaget till vår bok):
```csharp
// Skaffa det första arbetsbladet
Worksheet worksheet = workbook.Worksheets[0]; // Index börjar på 0!
```
## Steg 4: Gå till pivottabellen
Med kalkylbladet i vårt grepp är det dags att hitta pivottabellen vi behöver arbeta med.
```csharp
int pivotindex = 0; // Förutsatt att du vill ha den första pivottabellen
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
## Steg 5: Hämta datafälten
Nu när vi är i pivottabellen, låt oss dra ut datafälten. Se det här som att gå in i ett bibliotek och hämta specifika böcker (eller datafält).
```csharp
Aspose.Cells.Pivot.PivotFieldCollection pivotFields = pivotTable.DataFields;
```
## Steg 6: Öppna det första datafältet
Från samlingen av fält kan vi komma åt det första. Det här är som att välja den första boken från hyllan att läsa.
```csharp
Aspose.Cells.Pivot.PivotField pivotField = pivotFields[0]; // Hämta första datafältet
```
## Steg 7: Ställ in datavisningsformatet
Nästa upp, låt oss ställa in datavisningsformatet för pivotfältet. Det är här du kan börja visa meningsfulla bilder – till exempel procentsatser:
```csharp
// Ställa in datavisningsformat
pivotField.DataDisplayFormat = Aspose.Cells.Pivot.PivotFieldDataDisplayFormat.PercentageOf;
```
## Steg 8: Ställ in basfältet och basobjektet
Varje pivotfält kan knytas till ett annat fält som basreferens. Låt oss ställa in det:
```csharp
//Ställa in basfältet
pivotField.BaseFieldIndex = 1; // Använd lämpligt index för basfält
// Ställa in basobjektet
pivotField.BaseItemPosition = Aspose.Cells.Pivot.PivotItemPosition.Next; // Välj nästa objekt
```
## Steg 9: Ställ in sifferformatet
Ta det ett steg längre, låt oss justera nummerformatet. Detta är ungefär som att bestämma hur du vill att siffrorna ska visas - låt oss göra dem snygga!
```csharp
// Ställa in talformat
pivotField.Number = 10; // Använd formatindex efter behov
```
## Steg 10: Spara Excel-filen
Allt klart och klart! Dags att spara dina ändringar. Din arbetsbok kommer nu att återspegla alla mäktiga förändringar du just gjort.
```csharp
// Sparar Excel-filen
workbook.Save(dataDir + "output.xls");
```
Och där har ni det, gott folk! Din pivottabells datafält är nu formaterade till perfektion!
## Slutsats
Grattis! Du har precis gått igenom en handledning om hur du ställer in datafältsformat programmatiskt i .NET med Aspose.Cells. Med varje steg, har vi skalat tillbaka lager av komplexitet, så att du kan interagera dynamiskt med Excel, ändra pivottabeller och visa data i handlingsbara format. Fortsätt öva, utforska fler funktioner.
## FAQ's
### Kan jag använda Aspose.Cells för att skapa Excel-filer från grunden?
Absolut! Du kan skapa och manipulera Excel-filer med Aspose.Cells från grunden.
### Finns det en gratis provperiod?
 Ja! Du kan kolla in[Gratis provperiod](https://releases.aspose.com/).
### Vilka format stöder Aspose.Cells för Excel-filer?
Den stöder olika format inklusive XLS, XLSX, CSV och mer.
### Behöver jag betala för en licens?
 Du har ett par alternativ! Du kan köpa en licens på[Köpsida](https://purchase.aspose.com/buy) . Alternativt, a[Tillfällig licens](https://purchase.aspose.com/temporary-license/) finns också tillgänglig.
### Var kan jag hitta support om jag har problem?
 Du kan hitta support på deras[Supportforum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
