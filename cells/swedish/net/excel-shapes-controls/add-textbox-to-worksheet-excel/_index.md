---
title: Lägg till en textruta till kalkylblad i Excel
linktitle: Lägg till en textruta till kalkylblad i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du lägger till anpassningsbara textrutor i Excel med Aspose.Cells för .NET i denna steg-för-steg-handledning.
weight: 14
url: /sv/net/excel-shapes-controls/add-textbox-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till en textruta till kalkylblad i Excel

## Introduktion
Är du angelägen om att förbättra dina Excel-kalkylblad med unika bilder som kan engagera din publik? Att lägga till textrutor är ett bra sätt att åstadkomma detta! Med Aspose.Cells för .NET kan du enkelt integrera textrutor i dina Excel-kalkylblad, vilket gör dina dokument mer informativa och visuellt tilltalande. Den här steg-för-steg-guiden leder dig genom den enkla processen att lägga till textrutor med Aspose.Cells, och visar hur du anpassar dem med text, färger, hyperlänkar och mer!
## Förutsättningar
Innan vi dyker in i kodningsunderverket, här är de grundläggande förutsättningarna för att säkerställa en smidig seglingsupplevelse:
1. .NET-utvecklingsmiljö: Du behöver ett fungerande .NET-ramverk tillsammans med en IDE som Visual Studio. Se till att den är uppdaterad till den senaste versionen!
2.  Aspose.Cells för .NET: Se till att du har Aspose.Cells-biblioteket nedladdat. Du kan hämta den senaste versionen från[här](https://releases.aspose.com/cells/net/).
3. Grundläggande programmeringskunskaper: Bekantskap med C# och några allmänna koncept för hantering av Excel-filer kommer att göra denna handledning enklare!
## Importera paket
Se till att importera de nödvändiga paketen i början av din C#-fil. Så här kan du göra det:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Installera Aspose.Cells
Om du inte redan har gjort det kan du lägga till Aspose.Cells genom NuGet Package Manager i Visual Studio:
1. Öppna Visual Studio.
2.  Gå till`Tools` ->`NuGet Package Manager` ->`Manage NuGet Packages for Solution`.
3. Sök efter "Aspose.Cells" och installera det för ditt projekt.
Nu när vi har lagt grunden, låt oss hoppa in i den roliga delen!
## Steg 1: Konfigurera din dokumentkatalog
Först och främst, låt oss ställa in katalogen där alla dina Excel-dokument kommer att lagras. Det är viktigt att se till att den här katalogen finns innan vi börjar skapa vår arbetsbok.
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory"; 
// Skapa katalog om den inte redan finns.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists) 
    System.IO.Directory.CreateDirectory(dataDir);
```
Detta kodavsnitt skapar en katalog med namnet`Your Document Directory` (ersätt detta med din faktiska sökväg) om den inte redan finns. Easy peasy, eller hur?
## Steg 2: Instantiera en ny arbetsbok
Därefter måste vi skapa en ny arbetsbok där vi lägger till våra textrutor. Detta kan enkelt göras med några rader kod:
```csharp
// Instantiera en ny arbetsbok.
Workbook workbook = new Workbook();
```
Denna kodrad skapar en ny Excel-arbetsbok. Enkelt och rakt på sak!
## Steg 3: Få åtkomst till det första arbetsbladet
Nu när vi har vår arbetsbok redo, låt oss få det första kalkylbladet där vi lägger till vår textruta:
```csharp
// Skaffa det första arbetsbladet i boken.
Worksheet worksheet = workbook.Worksheets[0];
```
 Precis så har du nu tillgång till det första kalkylbladet som heter`worksheet`. Det är dags att få det att glänsa!
## Steg 4: Lägga till en textruta
Okej, det är dags att lägga till i vår första textruta! Så här gör du:
```csharp
// Lägg till en ny textruta i samlingen.
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
På den här raden anger vi raden och kolumnen där textrutan ska placeras, samt anger dess bredd och höjd (160 respektive 200). Justera gärna dessa siffror baserat på din layout!
## Steg 5: Skaffa TextBox-objektet
Efter att ha lagt till textrutan måste vi få en referens till den så att vi kan anpassa innehållet:
```csharp
// Hämta textbox-objektet.
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[textboxIndex];
```
 Nu,`textbox0` är din gyllene biljett till att ändra denna textruta!
## Steg 6: Fyll textrutan med innehåll
Låt oss sedan ge lite text till textrutan:
```csharp
// Fyll i texten.
textbox0.Text = "ASPOSE______The .NET & JAVA Component Publisher!";
```
Att infoga text i din textruta är så enkelt! 
## Steg 7: Anpassa textrutans utseende
Vad sägs om att vi piffar till det lite? Du kan justera teckensnittsfärger, stilar och mer!
```csharp
// Ställ in teckensnittsfärgen.
textbox0.Font.Color = Color.Blue;
// Ställ in teckensnittet till fetstil.
textbox0.Font.IsBold = true;
// Ställ in teckenstorleken.
textbox0.Font.Size = 14;
// Ställ in teckensnittsattributet till kursiv.
textbox0.Font.IsItalic = true;
```
Lek gärna med olika färger och stilar för att se vad som syns bäst visuellt!
## Steg 8: Lägga till en hyperlänk
Vill du göra din textruta till en klickbar länk? Låt oss göra just det:
```csharp
// Lägg till en hyperlänk i textrutan.
textbox0.AddHyperlink("http://www.aspose.com/");
```
Nu kommer alla som klickar på din textruta att transporteras till Asposes webbplats. Det är som magi!
## Steg 9: Ställa in textboxplaceringstyp
Du har olika val på hur du vill att textrutan ska bete sig i förhållande till ditt kalkylblad. Här är ett exempel på hur du ställer in den så att den är fritt flytande:
```csharp
// Ställ in placeringen.
textbox0.Placement = PlacementType.FreeFloating;
```
Alternativt, om du vill att den ska ändra storlek och flytta med celler, kan du ställa in den så här:
```csharp
// Ställ in placeringstypen eftersom textrutan kommer att flyttas och ändra storlek med celler.
textbox1.Placement = PlacementType.MoveAndSize;
```
## Steg 10: Anpassa linje- och fyllningsformat
Så här kan du ändra utseendet på textrutans ram och fyllning:
```csharp
// Hämta fyllningsformatet för textrutan.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;            
// Hämta textrutans linjeformattyp.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;           
// Ställ in linjevikten.
lineformat.Weight = 6;
// Ställ in streckstilen till squaredot.
lineformat.DashStyle = MsoLineDashStyle.SquareDot;
```
Med detta kan du anpassa din textruta ytterligare och lägga till bilder som passar din stil.
## Steg 11: Lägga till ytterligare en textruta
Ingen sa att vi bara kunde lägga till en textruta! Låt oss lägga in en annan med lite annan text:
```csharp
// Lägg till ytterligare en textruta.
textboxIndex = worksheet.TextBoxes.Add(15, 4, 85, 120);
// Skaffa den andra textrutan.
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[textboxIndex];
// Skriv in lite text till den.
textbox1.Text = "This is another simple text box";
```
Nu piffar du verkligen upp ditt Excel-ark med flera textrutor!
## Steg 12: Spara din arbetsbok
Äntligen är det dags att rädda vårt mästerverk! Här är den sista raden i koden för dagen:
```csharp
// Spara excel-filen.
workbook.Save(dataDir + "book1.out.xls");
```
Med bara denna kodrad har du skapat och modifierat en Excel-fil med anpassningsbara textrutor!
## Slutsats
Grattis! Du har framgångsrikt navigerat genom en värld av textrutor i Excel med Aspose.Cells för .NET. Du har inte bara lärt dig hur du lägger till en textruta utan också hur du anpassar den för att göra dina kalkylblad mer engagerande. Från att ändra färger och stilar till att lägga till hyperlänkar, möjligheterna är praktiskt taget oändliga! 
Är du redo att börja transformera dina Excel-dokument? Låt din kreativitet lysa och experimentera med olika layouter!
## FAQ's
### Vad är Aspose.Cells för .NET?
Aspose.Cells för .NET är ett kraftfullt bibliotek som låter utvecklare skapa, manipulera och konvertera Excel-filer utan ansträngning.
### Kan jag prova Aspose.Cells innan jag köper?
 Ja! Du kan ladda ner och använda en gratis testversion[här](https://releases.aspose.com/).
### Var kan jag hitta dokumentationen för Aspose.Cells?
 Du kan få tillgång till omfattande dokumentation på[Aspose.Cells dokumentation](https://reference.aspose.com/cells/net/).
### Finns det support tillgängligt om jag stöter på problem?
 Absolut! Om du behöver hjälp, gå till[Aspose Forum](https://forum.aspose.com/c/cells/9) för hjälp.
### Kan jag använda Aspose.Cells utan licens?
 Även om du kan använda en gratis testversion måste du köpa en licens för att få tillgång till full funktionalitet. Kolla in priset[här](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
