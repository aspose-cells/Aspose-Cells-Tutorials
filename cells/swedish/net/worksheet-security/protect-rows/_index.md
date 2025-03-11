---
title: Skydda rader i kalkylblad med Aspose.Cells
linktitle: Skydda rader i kalkylblad med Aspose.Cells
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du skyddar rader i ett Excel-kalkylblad med Aspose.Cells för .NET. Säkra dina data med skydd på radnivå och förhindra oavsiktliga ändringar.
weight: 18
url: /sv/net/worksheet-security/protect-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skydda rader i kalkylblad med Aspose.Cells

## Introduktion
Att arbeta med Excel-filer programmatiskt är ofta en uppgift som kräver inte bara datamanipulation utan även dataskydd. Oavsett om du behöver skydda känslig data eller förhindra oavsiktlig redigering, kan skydd av rader i ett kalkylblad vara ett avgörande steg. I den här handledningen kommer vi att dyka in i hur man skyddar specifika rader i ett Excel-kalkylblad med Aspose.Cells för .NET. Vi går igenom alla nödvändiga steg, från att förbereda din miljö till att implementera skyddsfunktionerna på ett enkelt, lätt att följa sätt.
## Förutsättningar
Innan du kan börja skydda rader i ett kalkylblad finns det några saker du måste ha på plats:
1.  Aspose.Cells for .NET: Se till att du har Aspose.Cells for .NET installerat på din utvecklingsmaskin. Om du inte redan har gjort detta kan du enkelt ladda ner det från[Aspose Cells nedladdningssida](https://releases.aspose.com/cells/net/).
2. Visual Studio eller valfri .NET IDE: För att implementera lösningen måste du ha en utvecklingsmiljö inrättad. Visual Studio är ett bra alternativ, men alla .NET-kompatibla IDE kommer att fungera.
3. Grundläggande C#-kunskap: Att förstå grunderna i C#-programmering hjälper dig att följa handledningen och modifiera exempelkoden för att passa dina behov.
4.  Aspose.Cells API-dokumentation: Bekanta dig med[Aspose.Cells för .NET-dokumentation](https://reference.aspose.com/cells/net/) för att få en överblick över klassstrukturen och metoder som används i biblioteket.
Om du är klar med förutsättningarna kan vi dyka direkt in i implementeringen.
## Importera paket
För att börja måste du importera de nödvändiga paketen. Dessa bibliotek är avgörande för att interagera med Excel-filer i ditt C#-projekt.
```csharp
using System.IO;
using Aspose.Cells;
```
När du har importerat de nödvändiga paketen kan du börja koda. 
Låt oss nu dela upp processen i mindre steg för att göra det superenkelt för dig att följa. Varje steg kommer att fokusera på en specifik del av implementeringen, vilket säkerställer att du kan förstå och tillämpa det snabbt. 
## Steg 1: Skapa en ny arbetsbok och ett arbetsblad
Innan du kan tillämpa några skyddsinställningar måste du skapa en ny arbetsbok och välja det kalkylblad du vill arbeta med. Detta kommer att vara ditt arbetsdokument.
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
// Skapa katalog om den inte redan finns.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Skapa en ny arbetsbok.
Workbook wb = new Workbook();
// Skapa ett kalkylbladsobjekt och få det första arket.
Worksheet sheet = wb.Worksheets[0];
```
I det här exemplet skapar vi en ny arbetsbok med ett enda kalkylblad (vilket är standardinställningen när du skapar en ny arbetsbok med Aspose.Cells). Vi tar sedan tag i det första kalkylbladet i arbetsboken, som kommer att vara målet för vårt radskydd.
## Steg 2: Definiera stil och stilFlagga objekt
Nästa steg är att definiera stil- och stilflaggobjekten. Dessa objekt låter dig ändra cellens egenskaper, till exempel om den är låst eller olåst.
```csharp
// Definiera stilobjektet.
Style style;
// Definiera styleflag-objektet.
StyleFlag flag;
```
Du kommer att använda dessa objekt i senare steg för att anpassa cellegenskaperna och tillämpa dem på ditt kalkylblad.
## Steg 3: Lås upp alla kolumner i arbetsbladet
Som standard är alla celler i ett Excel-kalkylblad låsta. Men när du skyddar ett kalkylblad upprätthålls den låsta statusen. För att säkerställa att endast specifika rader eller celler är skyddade kan du först låsa upp alla kolumner. Detta steg är viktigt om du bara vill skydda vissa rader.
```csharp
// Gå igenom alla kolumner i kalkylbladet och lås upp dem.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
 I den här koden går vi igenom alla 256 kolumner i kalkylbladet (Excel-kalkylblad har maximalt 256 kolumner, indexerade från 0 till 255) och ställer in deras`IsLocked` egendom till`false`. Den här åtgärden säkerställer att alla kolumner är upplåsta, men vi kommer fortfarande att låsa specifika rader senare.
## Steg 4: Lås den första raden
När du har låst upp kolumnerna är nästa steg att låsa specifika rader som du vill skydda. I det här exemplet låser vi den första raden. Detta säkerställer att användare inte kan ändra det medan andra rader lämnas olåsta.
```csharp
//Få den första radens stil.
style = sheet.Cells.Rows[0].Style;
// Lås den.
style.IsLocked = true;
//Instantiera flaggan.
flag = new StyleFlag();
// Ställ in låsinställningen.
flag.Locked = true;
// Applicera stilen på den första raden.
sheet.Cells.ApplyRowStyle(0, style, flag);
```
Här kommer vi åt stilen på den första raden och ställer in dess`IsLocked` egendom till`true` . Efter det använder vi`ApplyRowStyle()` metod för att tillämpa låsstilen på hela raden. Du kan upprepa detta steg för att låsa alla andra rader som du vill skydda.
## Steg 5: Skydda arket
Nu när vi har låst upp och låst de nödvändiga raderna är det dags att skydda kalkylbladet. Skyddet säkerställer att ingen kan ändra de låsta raderna eller cellerna om de inte tar bort skyddslösenordet (om det finns).
```csharp
// Skydda arket.
sheet.Protect(ProtectionType.All);
```
 I detta steg tillämpar vi skydd på hela arket med hjälp av`ProtectionType.All`. Denna typ av skydd innebär att alla aspekter av arket, inklusive låsta rader och celler, är skyddade. Du kan också anpassa detta skydd genom att ange olika skyddstyper om det behövs.
## Steg 6: Spara arbetsboken
Slutligen måste vi spara arbetsboken efter att ha tillämpat nödvändiga stilar och skydd. Arbetsboken kan sparas i olika format, som Excel 97-2003, Excel 2010, etc.
```csharp
// Spara Excel-filen.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Denna kodrad sparar arbetsboken i Excel 97-2003-formatet med ändringarna tillämpade. Du kan ändra filformatet enligt dina behov genom att välja från en mängd olika`SaveFormat` alternativ.
## Slutsats
Och där har du det! Du har framgångsrikt lärt dig hur du skyddar rader i ett kalkylblad med Aspose.Cells för .NET. Genom att följa stegen ovan kan du låsa upp eller låsa alla rader eller kolumner efter behov, och tillämpa skydd för att säkerställa integriteten hos dina data.
## FAQ's
### Hur kan jag skydda flera rader samtidigt?  
 Du kan gå igenom flera rader och tillämpa låsstilen på var och en individuellt. Byt bara ut`0` med det radindex du vill låsa.
### Kan jag ställa in ett lösenord för arkskyddet?  
 Ja! Du kan skicka ett lösenord till`sheet.Protect()` metod för att upprätthålla lösenordsskydd.
### Kan jag låsa upp celler istället för hela kolumner?  
Ja! Istället för att låsa upp kolumner kan du låsa upp enskilda celler genom att ändra deras stilegenskaper.
### Vad händer om jag försöker redigera en skyddad rad?  
När en rad är skyddad kommer Excel att förhindra att ändringar görs i de låsta cellerna om du inte tar bort skyddet för arket.
### Kan jag skydda specifika intervall i rad?  
 Ja! Du kan låsa enskilda intervall i rad genom att ställa in`IsLocked` egenskap för specifika celler inom intervallet.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
