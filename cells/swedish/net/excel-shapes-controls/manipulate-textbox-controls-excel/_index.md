---
title: Manipulera TextBox-kontroller i Excel
linktitle: Manipulera TextBox-kontroller i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du manipulerar textrutor i Excel med Aspose.Cells för .NET med denna lättanvända, steg-för-steg handledning.
weight: 15
url: /sv/net/excel-shapes-controls/manipulate-textbox-controls-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Manipulera TextBox-kontroller i Excel

## Introduktion
Om du någonsin har arbetat med Excel har du förmodligen stött på de där små textrutorna som låter dig lägga till flytande text i ett kalkylblad. Men vad händer om du behöver manipulera de textrutorna programmatiskt? Det är där Aspose.Cells för .NET kommer väl till pass. Med den kan du enkelt komma åt och ändra textrutor, vilket gör den perfekt för att automatisera uppgifter eller anpassa rapporter. I den här handledningen går vi igenom processen att manipulera textrutor i Excel med Aspose.Cells för .NET.
## Förutsättningar
Innan vi dyker in i den faktiska koden, låt oss se till att du har allt korrekt inställt:
1.  Aspose.Cells for .NET: Du måste ladda ner Aspose.Cells for .NET-biblioteket. Du hittar nedladdningslänken[här](https://releases.aspose.com/cells/net/).
2. .NET-utvecklingsmiljö: Alla IDE som stöder .NET, som Visual Studio, kommer att fungera.
3. Grundläggande kunskaper om C#: Denna handledning förutsätter att du är bekant med grundläggande C#-syntax och strukturen i Excel-arbetsböcker.
4.  Excel-fil: En befintlig Excel-fil med textrutor (vi kommer att använda`book1.xls` det här exemplet).
5.  Aspose-licens: Om du inte använder den kostnadsfria testversionen måste du göra det[köpa](https://purchase.aspose.com/buy) en licens eller få en[tillfälligt](https://purchase.aspose.com/temporary-license/).
Nu, låt oss dyka ner i stegen!
## Importera paket
Innan du kan manipulera Excel-arbetsböcker och textrutor med Aspose.Cells måste du importera de nödvändiga namnrymden. Här är kodavsnittet som du använder högst upp i din C#-fil:
```csharp
using System.IO;
using Aspose.Cells;
```
Dessa paket ger dig tillgång till manipulering av arbetsbok, åtkomst till kalkylblad och ritobjekt (som textrutor).
Nu när vi har allt installerat, låt oss dela upp processen att manipulera textrutor i lätta att följa steg.
## Steg 1: Konfigurera din arbetsbokskatalog
 Det första steget är att ange var dina Excel-filer finns på ditt system. Du måste byta ut platshållaren`Your Document Directory` med den faktiska sökvägen till din fil. Denna sökväg lagras i`dataDir` variabel för enkel referens genom hela koden.
```csharp
string dataDir = "Your Document Directory";
```
Detta gör att ditt program kan veta var man hittar indata Excel-filen (`book1.xls`) och var du ska spara utdatafilen.
## Steg 2: Öppna Excel-filen
Därefter måste du ladda den befintliga Excel-filen i Aspose.Cells Workbook-objektet. Den här arbetsboken fungerar som behållare för dina Excel-data och ger dig tillgång till dess kalkylblad och alla ritobjekt (som textrutor).
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 De`Workbook` class från Aspose.Cells kommer att ladda den angivna Excel-filen från din katalog. Om filen inte finns i den angivna katalogen kommer den att skapa ett undantag, så se till att sökvägen är korrekt.
## Steg 3: Öppna det första arbetsbladet
Nu när du har laddat arbetsboken kan du komma åt dess kalkylblad. I det här exemplet kommer vi åt det första kalkylbladet i arbetsboken, som lagras i index 0.
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
 De`Worksheets` egenskap ger dig tillgång till alla ark i arbetsboken. Här är vi bara intresserade av det första arket, men du kan arbeta med vilket ark som helst genom att ange rätt index.
## Steg 4: Skaffa det första TextBox-objektet
Textrutor i ett Excel-ark betraktas som ritobjekt. Klassen Aspose.Cells.Drawing.TextBox tillhandahåller egenskaper och metoder för att manipulera dem. För att komma åt den första textrutan på kalkylbladet hänvisar du helt enkelt till`TextBoxes` insamling efter index.
```csharp
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[0];
```
 Detta hämtar det första textruteobjektet från`TextBoxes` samling. Om ditt kalkylblad inte har en textruta vid det indexet kommer det att skapa ett undantag, så se alltid till att indexet är giltigt.
## Steg 5: Hämta text från den första textrutan
 När du har öppnat textrutan kan du extrahera texten den innehåller med hjälp av`.Text` egendom.
```csharp
string text0 = textbox0.Text;
```
 Detta kommer att fånga texten från den första textrutan till`text0` sträng. Du kan nu visa det, manipulera det eller bearbeta det i din applikation.
## Steg 6: Gå till det andra TextBox-objektet
För att manipulera flera textrutor kan vi hämta ytterligare från arbetsbladet. Här kommer vi åt den andra textrutan på liknande sätt som den första:
```csharp
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[1];
```
Återigen kommer vi åt den andra textrutan med index 1 från`TextBoxes`samling.
## Steg 7: Hämta text från den andra textrutan
Precis som med den första textrutan kan du hämta texten från den andra textrutan och lagra den i en sträng:
```csharp
string text1 = textbox1.Text;
```
Detta kommer att fånga den aktuella texten från den andra textrutan.
## Steg 8: Ändra texten i den andra textrutan
 Låt oss nu säga att du vill ändra texten i den andra textrutan. Du kan enkelt göra detta genom att tilldela en ny sträng till`.Text` egenskapen för textruteobjektet.
```csharp
textbox1.Text = "This is an alternative text";
```
Detta ändrar texten i den andra textrutan till det nya innehållet. Du kan infoga vilken text som helst här baserat på dina krav.
## Steg 9: Spara den uppdaterade Excel-filen
 Slutligen, efter att ha ändrat textrutorna, är det dags att spara dina ändringar. Aspose.Cells låter dig spara den modifierade arbetsboken med hjälp av`.Save()` metod. Du kan ange ett nytt filnamn eller skriva över den befintliga filen.
```csharp
workbook.Save(dataDir + "output.out.xls");
```
Detta kommer att spara den modifierade Excel-filen till din angivna utdatasökväg. Nu, när du öppnar Excel-filen, ser du de ändringar du gjort i textrutorna.
## Slutsats
Och där har du det! Du har precis lärt dig hur man manipulerar textrutor i Excel med Aspose.Cells för .NET. Oavsett om du automatiserar rapportgenerering, anpassar Excel-ark eller bygger dynamiskt innehåll, gör Aspose.Cells det enkelt att kontrollera varje aspekt av dina Excel-filer programmatiskt. Från att extrahera och ändra text till att spara de uppdaterade filerna, detta bibliotek är ett kraftfullt verktyg för utvecklare som arbetar med Excel i .NET-miljöer.
## FAQ's
### Kan jag manipulera andra ritobjekt med Aspose.Cells förutom textrutor?
Ja, Aspose.Cells låter dig manipulera andra ritobjekt som former, diagram och bilder.
### Vad händer om jag försöker komma åt en textruta som inte finns?
 Om indexet för textrutan ligger utanför intervallet, an`IndexOutOfRangeException` kommer att kastas.
### Kan jag lägga till nya textrutor i ett Excel-kalkylblad med Aspose.Cells?
 Ja, Aspose.Cells låter dig lägga till nya textrutor med hjälp av`AddTextBox` metod.
### Behöver jag en licens för att använda Aspose.Cells?
 Ja, du måste köpa en licens, men Aspose erbjuder också en[gratis provperiod](https://releases.aspose.com/).
### Kan jag använda Aspose.Cells med andra programmeringsspråk än C#?
Ja, Aspose.Cells kan användas med alla .NET-stödda språk, såsom VB.NET.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
