---
"description": "Lär dig hur du lägger till en listruta i ett Excel-ark med hjälp av Aspose.Cells för .NET. Följ vår enkla steg-för-steg-guide och gör dina Excel-ark interaktiva."
"linktitle": "Lägg till listruta i kalkylblad i Excel"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Lägg till listruta i kalkylblad i Excel"
"url": "/sv/net/excel-shapes-controls/add-list-box-to-worksheet-excel/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till listruta i kalkylblad i Excel

## Introduktion
Att lägga till interaktiva element i dina Excel-kalkylblad, som en listruta, kan förbättra datahantering och presentation avsevärt. Oavsett om du skapar ett interaktivt formulär eller ett anpassat datainmatningsverktyg är möjligheten att kontrollera användarinmatning med en listruta ovärderlig. Aspose.Cells för .NET ger ett effektivt sätt att lägga till och hantera dessa kontroller i dina Excel-filer. I den här guiden guidar vi dig genom processen att lägga till en listruta i ett kalkylblad med hjälp av Aspose.Cells för .NET.
## Förkunskapskrav
Innan du börjar med kodningen, se till att du har följande verktyg och resurser på plats:
- Aspose.Cells för .NET-biblioteket: Du kan ladda ner det från [Nedladdningssida för Aspose.Cells för .NET](https://releases.aspose.com/cells/net/).
- Utvecklingsmiljö: Alla IDE som stöder .NET-utveckling, till exempel Visual Studio.
- .NET Framework: Se till att ditt projekt riktar sig mot en version av .NET Framework som stöds.
Överväg också att skaffa en [tillfällig licens](https://purchase.aspose.com/temporary-license/) om du vill utforska alla funktioner utan begränsningar.
## Importera paket
Innan du börjar, se till att du har importerat de nödvändiga Aspose.Cells-namnrymderna. Så här gör du:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
I den här handledningen kommer vi att dela upp processen för att lägga till en listruta i flera enkla steg. Följ varje steg noggrant för att säkerställa att allt fungerar som förväntat.
## Steg 1: Konfigurera din dokumentkatalog
Innan du skapar en Excel-fil behöver du en plats att spara den på. Så här konfigurerar du katalogen:
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
// Skapa en katalog om den inte redan finns.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
det här steget definierar du var din fil ska lagras. Koden kontrollerar om katalogen finns, och om den inte gör det skapar den en åt dig. Detta säkerställer att du inte stöter på några "filen hittades inte"-fel senare.
## Steg 2: Skapa en ny arbetsbok och få åtkomst till det första arbetsbladet
Nästa steg är att skapa en ny arbetsbok och öppna det första kalkylbladet där vi lägger till vår listruta.
```csharp
// Skapa en ny arbetsbok.
Workbook workbook = new Workbook();
// Hämta det första arbetsbladet.
Worksheet sheet = workbook.Worksheets[0];
```
En arbetsbok är i huvudsak din Excel-fil. Här skapar vi en ny arbetsbok och öppnar det första kalkylbladet, där vi placerar vår listruta. Tänk på detta som att skapa en tom arbetsyta där du målar upp kontrollerna.
## Steg 3: Inmatningsdata för listrutan
Innan vi lägger till listrutan måste vi fylla i lite data som listrutan kommer att referera till.
```csharp
// Hämta cellsamlingen i kalkylbladet.
Cells cells = sheet.Cells;
// Ange ett värde för etiketten.
cells["B3"].PutValue("Choose Dept:");
// Ställ in etiketten i fetstil.
cells["B3"].GetStyle().Font.IsBold = true;
// Inmatningsvärden för listrutan.
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
Här lägger vi till lite text i kalkylbladet. Etiketten "Välj avdelning:" placeras i cell B3 och dess teckensnitt är fetstilt. I kolumn A infogar vi värden som fungerar som inmatningsområde för vår listruta och representerar olika avdelningar. Detta inmatningsområde är vad användarna kommer att välja mellan när de interagerar med listrutan.
## Steg 4: Lägg till listrutan i arbetsbladet
Nu när vi har konfigurerat data, låt oss lägga till själva listrutekontrollen.
```csharp
// Lägg till en ny listruta.
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
Den här koden lägger till listrutan i kalkylbladet. Parametrarna definierar listrutans position och storlek. Listrutan placeras på rad 2, kolumn 0 med en bredd på 122 och en höjd på 100. Det är koordinaterna och storleken som avgör var listrutan ska visas i kalkylbladet.
## Steg 5: Ange egenskaper för listbox
Nästa steg är att ställa in olika egenskaper för listrutan för att göra den fullt fungerande.
```csharp
// Ange placeringstyp.
listBox.Placement = PlacementType.FreeFloating;
// Ställ in den länkade cellen.
listBox.LinkedCell = "A1";
// Ställ in inmatningsintervallet.
listBox.InputRange = "A2:A7";
// Ange valtyp.
listBox.SelectionType = SelectionType.Single;
// Ställ in listrutan med 3D-skuggning.
listBox.Shadow = true;
```
- PlacementType.FreeFloating: Den här egenskapen säkerställer att listrutan förblir i sin position oavsett hur kalkylbladet ändras.
- Länkad cell: Detta ställer in en cell (i det här fallet A1) där det valda värdet från listrutan visas.
- InputRange: Detta anger var listrutan ska leta efter listan med alternativ (A2 till A7, som vi angav tidigare).
- SelectionType.Single: Detta begränsar användaren till att endast välja ett objekt från listrutan.
- Skugga: Skuggeffekten ger listrutan ett mer tredimensionellt utseende, vilket gör den visuellt tilltalande.
## Steg 6: Spara Excel-filen
Slutligen, låt oss spara vår arbetsbok med listrutan inkluderad.
```csharp
// Spara arbetsboken.
workbook.Save(dataDir + "book1.out.xls");
```
Den här kodraden sparar arbetsboken i katalogen vi skapade tidigare. Filen heter "book1.out.xls" men du kan välja vilket namn som helst som passar ditt projekt.
## Slutsats
Och där har du det! Du har lagt till en listruta i ett Excel-kalkylblad med hjälp av Aspose.Cells för .NET. Med bara några få rader kod har vi skapat en fullt fungerande listruta, vilket gör kalkylbladet mer interaktivt och dynamiskt. Den här handledningen bör ge dig en solid grund för att utforska andra kontroller och funktioner i Aspose.Cells för .NET. Fortsätt experimentera, så kommer du snart att bemästra bibliotekets omfattande funktionalitet!
## Vanliga frågor
### Kan jag tillåta flera val i listrutan?  
Ja, du kan ändra `SelectionType` till `SelectionType.Multi` för att tillåta flera val.
### Kan jag ändra utseendet på listrutan?  
Absolut! Med Aspose.Cells kan du anpassa utseendet på listrutan, inklusive dess storlek, teckensnitt och till och med färg.
### Vad händer om jag behöver ta bort listrutan senare?  
Du kan komma åt och ta bort listrutan från `Shapes` samling med hjälp av `sheet.Shapes.RemoveAt(index)`.
### Kan jag länka listrutan till en annan cell?  
Ja, ändra bara `LinkedCell` egenskapen till en annan cell där du vill visa det valda värdet.
### Hur lägger jag till fler objekt i listrutan?  
Uppdatera bara inmatningsområdet genom att infoga fler värden i de angivna cellerna, så uppdateras listrutan automatiskt.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}