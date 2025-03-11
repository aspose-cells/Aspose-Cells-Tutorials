---
title: Lägg till listruta till kalkylblad i Excel
linktitle: Lägg till listruta till kalkylblad i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du lägger till en listruta i ett Excel-kalkylblad med Aspose.Cells för .NET. Följ vår enkla, steg-för-steg-guide och gör dina Excel-ark interaktiva.
weight: 20
url: /sv/net/excel-shapes-controls/add-list-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till listruta till kalkylblad i Excel

## Introduktion
Att lägga till interaktiva element i dina Excel-kalkylblad, som en listruta, kan förbättra datahanteringen och presentationen avsevärt. Oavsett om du skapar ett interaktivt formulär eller ett anpassat datainmatningsverktyg är möjligheten att kontrollera användarinmatning med en listruta ovärderlig. Aspose.Cells för .NET ger ett effektivt sätt att lägga till och hantera dessa kontroller i dina Excel-filer. I den här guiden går vi igenom processen att lägga till en listruta i ett kalkylblad med Aspose.Cells för .NET.
## Förutsättningar
Innan du dyker in i kodningen, se till att du har följande verktyg och resurser på plats:
-  Aspose.Cells för .NET Library: Du kan ladda ner det från[Aspose.Cells för .NET nedladdningssida](https://releases.aspose.com/cells/net/).
- Utvecklingsmiljö: Alla IDE som stöder .NET-utveckling, till exempel Visual Studio.
- .NET Framework: Se till att ditt projekt är inriktat på en version av .NET-ramverket som stöds.
 Överväg också att skaffa en[tillfällig licens](https://purchase.aspose.com/temporary-license/) om du vill utforska alla funktioner utan begränsningar.
## Importera paket
Innan du börjar, se till att du har importerat de nödvändiga Aspose.Cells-namnrymden. Så här gör du det:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
I den här handledningen kommer vi att dela upp processen att lägga till en listruta i flera enkla steg. Följ varje steg noga för att säkerställa att allt fungerar som förväntat.
## Steg 1: Konfigurera din dokumentkatalog
Innan du skapar en Excel-fil behöver du en plats för att spara den. Så här ställer du in katalogen:
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
// Skapa katalog om den inte redan finns.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
I det här steget definierar du var din fil ska lagras. Koden kontrollerar om katalogen finns, och om den inte gör det skapar den en åt dig. Detta säkerställer att du inte stöter på några "filen hittades inte"-fel senare.
## Steg 2: Skapa en ny arbetsbok och få tillgång till det första arbetsbladet
Därefter skapar vi en ny arbetsbok och kommer åt det första kalkylbladet där vi lägger till vår listruta.
```csharp
// Skapa en ny arbetsbok.
Workbook workbook = new Workbook();
// Skaffa det första arbetsbladet.
Worksheet sheet = workbook.Worksheets[0];
```
En arbetsbok är i grunden din Excel-fil. Här skapar vi en ny arbetsbok och kommer åt det första kalkylbladet, där vi placerar vår listruta. Se det här som att skapa en tom duk där du ska måla kontrollerna.
## Steg 3: Mata in data för listrutan
Innan vi lägger till listrutan måste vi fylla i några data som listrutan kommer att referera till.
```csharp
// Hämta samlingen av kalkylbladsceller.
Cells cells = sheet.Cells;
// Ange ett värde för etiketten.
cells["B3"].PutValue("Choose Dept:");
// Ställ in etiketten till fetstil.
cells["B3"].GetStyle().Font.IsBold = true;
// Inmatningsvärden för listrutan.
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
Här lägger vi till lite text i kalkylbladet. Etiketten "Välj avd:" placeras i cell B3 och dess teckensnitt är inställt i fetstil. I kolumn A infogar vi värden som kommer att fungera som inmatningsintervall för vår listruta, som representerar olika avdelningar. Detta inmatningsintervall är vad användarna kommer att välja mellan när de interagerar med listrutan.
## Steg 4: Lägg till listrutan i arbetsbladet
Nu när vi har ställt in data, låt oss lägga till listboxkontrollen själv.
```csharp
// Lägg till en ny listruta.
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
Denna kod lägger till listrutan i kalkylbladet. Parametrarna definierar placeringen och storleken på listrutan. Listrutan är placerad på rad 2, kolumn 0 med en bredd på 122 och höjd på 100. Dessa är koordinaterna och storleken som avgör var listrutan kommer att visas i kalkylbladet.
## Steg 5: Ställ in listboxegenskaper
Därefter kommer vi att ställa in olika egenskaper för listrutan för att göra den fullt funktionell.
```csharp
// Ställ in placeringstypen.
listBox.Placement = PlacementType.FreeFloating;
// Ställ in den länkade cellen.
listBox.LinkedCell = "A1";
// Ställ in ingångsintervallet.
listBox.InputRange = "A2:A7";
// Ställ in urvalstyp.
listBox.SelectionType = SelectionType.Single;
// Ställ in listrutan med 3D-skuggning.
listBox.Shadow = true;
```
- PlacementType.FreeFloating: Den här egenskapen ser till att listrutan förblir i sin position oavsett hur kalkylbladet ändras.
- LinkedCell: Detta ställer in en cell (i detta fall A1) där det valda värdet från listrutan kommer att visas.
- InputRange: Detta talar om för listrutan var den ska leta efter dess lista med alternativ (A2 till A7, som vi ställde in tidigare).
- SelectionType.Single: Detta begränsar användaren till att endast välja ett objekt från listrutan.
- Skugga: Skuggeffekten ger listrutan ett mer tredimensionellt utseende, vilket gör den visuellt tilltalande.
## Steg 6: Spara Excel-filen
Slutligen, låt oss spara vår arbetsbok med listrutan inkluderad.
```csharp
// Spara arbetsboken.
workbook.Save(dataDir + "book1.out.xls");
```
Den här kodraden sparar arbetsboken i katalogen som vi skapade tidigare. Filen heter "book1.out.xls" men du kan välja vilket namn som helst som passar ditt projekt.
## Slutsats
Och där har du det! Du har framgångsrikt lagt till en listruta i ett Excel-kalkylblad med Aspose.Cells för .NET. Med bara några rader kod skapade vi en fullt fungerande listruta, vilket gör kalkylbladet mer interaktivt och dynamiskt. Denna handledning bör ge dig en solid grund för att utforska andra kontroller och funktioner i Aspose.Cells för .NET. Fortsätt experimentera, och snart kommer du att bemästra bibliotekets enorma funktionalitet!
## FAQ's
### Kan jag tillåta flera val i listrutan?  
 Ja, du kan ändra`SelectionType` till`SelectionType.Multi` för att tillåta flera val.
### Kan jag ändra utseendet på listrutan?  
Absolut! Aspose.Cells låter dig anpassa utseendet på listrutan, inklusive dess storlek, teckensnitt och till och med färg.
### Vad händer om jag behöver ta bort listrutan senare?  
 Du kan komma åt och ta bort listrutan från`Shapes` samling med hjälp av`sheet.Shapes.RemoveAt(index)`.
### Kan jag länka listrutan till en annan cell?  
 Ja, ändra helt enkelt`LinkedCell` egenskap till någon annan cell där du vill visa det valda värdet.
### Hur lägger jag till fler objekt i listrutan?  
Uppdatera bara inmatningsintervallet genom att infoga fler värden i de angivna cellerna, så uppdateras listrutan automatiskt.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
