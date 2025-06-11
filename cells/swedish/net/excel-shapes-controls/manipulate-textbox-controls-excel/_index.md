---
"description": "Lär dig hur du manipulerar textrutor i Excel med Aspose.Cells för .NET med den här lättförståeliga steg-för-steg-handledningen."
"linktitle": "Manipulera textrutekontroller i Excel"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Manipulera textrutekontroller i Excel"
"url": "/sv/net/excel-shapes-controls/manipulate-textbox-controls-excel/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Manipulera textrutekontroller i Excel

## Introduktion
Om du någonsin har arbetat med Excel har du förmodligen stött på de där små textrutorna som låter dig lägga till flytande text i ett kalkylblad. Men tänk om du behöver manipulera dessa textrutor programmatiskt? Det är där Aspose.Cells för .NET kommer väl till pass. Med det kan du enkelt komma åt och ändra textrutor, vilket gör det perfekt för att automatisera uppgifter eller anpassa rapporter. I den här handledningen guidar vi dig genom processen att manipulera textrutor i Excel med hjälp av Aspose.Cells för .NET.
## Förkunskapskrav
Innan vi går in i själva koden, låt oss se till att du har allt korrekt konfigurerat:
1. Aspose.Cells för .NET: Du behöver ladda ner Aspose.Cells för .NET-biblioteket. Du hittar nedladdningslänken [här](https://releases.aspose.com/cells/net/).
2. .NET-utvecklingsmiljö: Alla IDE:er som stöder .NET, till exempel Visual Studio, fungerar.
3. Grundläggande kunskaper i C#: Den här handledningen förutsätter att du är bekant med grundläggande C#-syntax och strukturen i Excel-arbetsböcker.
4. Excel-fil: En befintlig Excel-fil med textrutor (vi använder `book1.xls` i det här exemplet).
5. Aspose-licens: Om du inte använder den kostnadsfria testversionen måste du [köpa](https://purchase.aspose.com/buy) en licens eller skaffa en [tillfällig](https://purchase.aspose.com/temporary-license/).
Nu, låt oss dyka in i stegen!
## Importera paket
Innan du kan manipulera Excel-arbetsböcker och textrutor med Aspose.Cells måste du importera de nödvändiga namnrymderna. Här är kodavsnittet du kommer att använda högst upp i din C#-fil:
```csharp
using System.IO;
using Aspose.Cells;
```
Dessa paket ger dig tillgång till arbetsbokshantering, åtkomst till arbetsblad och ritobjekt (som textrutor).
Nu när vi har allt klart, låt oss dela upp processen för att manipulera textrutor i lättförståeliga steg.
## Steg 1: Konfigurera din arbetsbokskatalog
Det första steget är att ange var dina Excel-filer finns på ditt system. Du måste ersätta platshållaren `Your Document Directory` med den faktiska sökvägen till din fil. Denna sökväg lagras i `dataDir` variabel för enkel referens i hela koden.
```csharp
string dataDir = "Your Document Directory";
```
Detta gör att ditt program kan veta var det hittar indatafilen i Excel (`book1.xls`) och var utdatafilen ska sparas.
## Steg 2: Öppna Excel-filen
Därefter måste du ladda den befintliga Excel-filen till Aspose.Cells Workbook-objektet. Den här arbetsboken fungerar som behållare för dina Excel-data och ger dig åtkomst till dess kalkylblad och alla ritobjekt (som textrutor).
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
De `Workbook` Klassen från Aspose.Cells kommer att ladda den angivna Excel-filen från din katalog. Om filen inte finns i den angivna katalogen kommer den att utlösa ett undantag, så se till att sökvägen är korrekt.
## Steg 3: Öppna det första arbetsbladet
Nu när du har laddat arbetsboken kan du komma åt dess kalkylblad. I det här exemplet öppnar vi det första kalkylbladet i arbetsboken, som är lagrat vid index 0.
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
De `Worksheets` Egenskapen ger dig åtkomst till alla ark i arbetsboken. Här är vi bara intresserade av det första arket, men du kan arbeta med vilket ark som helst genom att ange rätt index.
## Steg 4: Hämta det första textboxobjektet
Textrutor i ett Excel-ark betraktas som ritobjekt. Klassen Aspose.Cells.Drawing.TextBox tillhandahåller egenskaper och metoder för att manipulera dem. För att komma åt den första textrutan i kalkylbladet refererar du helt enkelt till `TextBoxes` samling efter index.
```csharp
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[0];
```
Detta hämtar det första textruteobjektet från `TextBoxes` samling. Om ditt kalkylblad inte har en textruta vid det indexet kommer det att generera ett undantag, så se alltid till att indexet är giltigt.
## Steg 5: Hämta text från den första textrutan
När du har öppnat textrutan kan du extrahera texten den innehåller med hjälp av `.Text` egendom.
```csharp
string text0 = textbox0.Text;
```
Detta kommer att fånga texten från den första textrutan in i `text0` sträng. Du kan nu visa den, manipulera den eller bearbeta den i din applikation.
## Steg 6: Åtkomst till det andra textboxobjektet
För att hantera flera textrutor kan vi hämta ytterligare rutor från kalkylbladet. Här kommer vi åt den andra textrutan på ett liknande sätt som den första:
```csharp
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[1];
```
Återigen öppnar vi den andra textrutan med hjälp av index 1 från `TextBoxes` samling.
## Steg 7: Hämta text från den andra textrutan
Precis som med den första textrutan kan du hämta texten från den andra textrutan och lagra den i en sträng:
```csharp
string text1 = textbox1.Text;
```
Detta kommer att hämta den aktuella texten från den andra textrutan.
## Steg 8: Ändra texten i den andra textrutan
Låt oss nu säga att du vill ändra texten i den andra textrutan. Du kan enkelt göra detta genom att tilldela en ny sträng till `.Text` egenskapen för textruteobjektet.
```csharp
textbox1.Text = "This is an alternative text";
```
Detta ändrar texten i den andra textrutan till det nya innehållet. Du kan infoga valfri text här baserat på dina behov.
## Steg 9: Spara den uppdaterade Excel-filen
Slutligen, efter att du har ändrat textrutorna, är det dags att spara dina ändringar. Aspose.Cells låter dig spara den modifierade arbetsboken med hjälp av `.Save()` metod. Du kan ange ett nytt filnamn eller skriva över den befintliga filen.
```csharp
workbook.Save(dataDir + "output.out.xls");
```
Detta sparar den modifierade Excel-filen till din angivna utdatasökväg. När du nu öppnar Excel-filen ser du de ändringar du har gjort i textrutorna.
## Slutsats
Och där har du det! Du har precis lärt dig hur man manipulerar textrutor i Excel med hjälp av Aspose.Cells för .NET. Oavsett om du automatiserar rapportgenerering, anpassar Excel-ark eller bygger dynamiskt innehåll, gör Aspose.Cells det enkelt att kontrollera alla aspekter av dina Excel-filer programmatiskt. Från att extrahera och modifiera text till att spara uppdaterade filer är detta bibliotek ett kraftfullt verktyg för utvecklare som arbetar med Excel i .NET-miljöer.
## Vanliga frågor
### Kan jag manipulera andra ritobjekt med Aspose.Cells förutom textrutor?
Ja, Aspose.Cells låter dig manipulera andra ritobjekt som former, diagram och bilder.
### Vad händer om jag försöker komma åt en textruta som inte finns?
Om textrutans index ligger utanför intervallet, en `IndexOutOfRangeException` kommer att kastas.
### Kan jag lägga till nya textrutor i ett Excel-kalkylblad med Aspose.Cells?
Ja, Aspose.Cells låter dig lägga till nya textrutor med hjälp av `AddTextBox` metod.
### Behöver jag en licens för att använda Aspose.Cells?
Ja, du måste köpa en licens, men Aspose erbjuder även en [gratis provperiod](https://releases.aspose.com/).
### Kan jag använda Aspose.Cells med andra programmeringsspråk förutom C#?
Ja, Aspose.Cells kan användas med alla .NET-stödda språk, till exempel VB.NET.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}