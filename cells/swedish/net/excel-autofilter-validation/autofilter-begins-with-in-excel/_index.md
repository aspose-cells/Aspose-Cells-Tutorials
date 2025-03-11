---
title: Autofilter börjar med i Excel
linktitle: Autofilter börjar med i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du autofiltrerar Excel-rader med Aspose.Cells i .NET utan ansträngning med den här omfattande steg-för-steg-guiden.
weight: 10
url: /sv/net/excel-autofilter-validation/autofilter-begins-with-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Autofilter börjar med i Excel

## Introduktion

När det kommer till att arbeta med data har Excel etablerat sig som en go-to-applikation för otaliga branscher och ändamål. En av dess mest kraftfulla funktioner är AutoFilter, som gör det enkelt att gå igenom omfattande datauppsättningar. Om du använder Aspose.Cells för .NET kan du utnyttja den här funktionen programmatiskt och förbättra dina datahanteringsuppgifter avsevärt. I den här guiden kommer vi att leda dig genom processen att implementera en funktion som filtrerar Excel-rader baserat på om de börjar med en viss sträng.

## Förutsättningar

Innan du dyker in, se till att du har följande förutsättningar på plats:

1. Utvecklingsmiljö: Bekanta dig med en .NET-utvecklingsmiljö. Detta kan vara Visual Studio eller någon annan IDE du väljer.
2.  Aspose.Cells för .NET: Du måste ha Aspose.Cells för .NET installerat. Om du inte har gjort det ännu kan du enkelt ladda ner det[här](https://releases.aspose.com/cells/net/).
3. Grundläggande kunskaper om C#: En grundläggande förståelse för C# och hur man arbetar med .NET-bibliotek hjälper dig att följa med sömlöst.
4.  Exempeldata: Du bör ha en Excel-fil, helst namngiven`sourseSampleCountryNames.xlsx`, som finns i din angivna källkatalog. Den här filen kommer att innehålla den data vi kommer att filtrera.
5.  Licensiering: För full funktionalitet, överväg att skaffa en licens via denna[länk](https://purchase.aspose.com/buy) . Om du vill testa funktionerna kan du begära en[tillfällig licens](https://purchase.aspose.com/temporary-license/).

Har du allt klart? Låt oss gå!

## Importera paket

För att komma igång, importera de nödvändiga namnrymden överst i din C#-fil:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Detta importerar Aspose.Cells kärnfunktionalitet tillsammans med grundläggande systemfunktioner som vi kommer att lita på för konsolinteraktion.

Nu när du har konfigurerat din miljö och de nödvändiga paketen importerade, låt oss dela upp Autofilter-funktionen i hanterbara steg. Vi kommer att implementera ett filter som extraherar rader som börjar med "Ba".

## Steg 1: Definiera käll- och utdatakataloger

Först och främst, låt oss definiera var vår indata Excel-fil finns, samt var vi vill spara vår filtrerade utdata:

```csharp
// Källkatalog
string sourceDir = "Your Document Directory\\";

// Utdatakatalog
string outputDir = "Your Document Directory\\";
```

 Förklaring: Här, byt ut`"Your Document Directory\\"` med den faktiska sökvägen till dina kataloger. Se till att avsluta katalogsökvägarna med ett dubbelt omvänt snedstreck (`\\`) för att undvika vägproblem.

## Steg 2: Instantiera arbetsboksobjektet

Därefter skapar vi ett arbetsboksobjekt som pekar på vår Excel-fil:

```csharp
// Instantiera ett arbetsboksobjekt som innehåller exempeldata
Workbook workbook = new Workbook(sourceDir + "sourseSampleCountryNames.xlsx");
```

 Förklaring: Den här raden initierar en ny arbetsboksinstans med den angivna sökvägen. De`Workbook` klass är grundläggande eftersom den representerar hela Excel-filen.

## Steg 3: Få åtkomst till det första arbetsbladet

Nu måste vi komma åt det specifika kalkylblad som vi vill arbeta med:

```csharp
// Åtkomst till det första kalkylbladet i Excel-filen
Worksheet worksheet = workbook.Worksheets[0];
```

 Förklaring: The`Worksheets` samling ger oss tillgång till enskilda ark. Använder`[0]` refererar till det första kalkylbladet i din Excel-fil, vilket vanligtvis är vanligt när du arbetar med en fil med ett ark.

## Steg 4: Konfigurera autofiltret

Här börjar magin! Vi skapar ett autofilterintervall för våra data:

```csharp
// Skapa AutoFilter genom att ge cellerna intervall
worksheet.AutoFilter.Range = "A1:A18";
```

 Förklaring: The`AutoFilter.Range` egenskap låter dig ange vilka rader som ska filtreras. I det här fallet filtrerar vi rader inom intervallet A1 till A18, som antas innehålla våra data.

## Steg 5: Tillämpa filtervillkor

Nästa steg är att definiera filtervillkoret. Vi vill bara visa de rader vars första kolumnvärden börjar med "Ba":

```csharp
// Initiera filter för rader som börjar med strängen "Ba"
worksheet.AutoFilter.Custom(0, FilterOperatorType.BeginsWith, "Ba");
```

 Förklaring: The`Custom` metoden definierar vår filtreringslogik. Det första argumentet (`0` ) indikerar att vi filtrerar baserat på den första kolumnen (A), och den`FilterOperatorType.BeginsWith` anger vårt villkor för att leta efter rader som börjar med "Ba".

## Steg 6: Uppdatera filtret

Efter att ha tillämpat vårt filtervillkor måste vi se till att Excel uppdateras för att återspegla ändringarna:

```csharp
// Uppdatera filtret för att visa/dölja filtrerade rader
worksheet.AutoFilter.Refresh();
```

Förklaring: Den här raden anropar en uppdatering av autofiltret för att säkerställa att de synliga raderna motsvarar de tillämpade filterkriterierna. Det liknar att trycka på uppdateringsknappen i Excel.

## Steg 7: Spara den modifierade Excel-filen

Nu är det dags att spara ändringarna vi har gjort:

```csharp
// Sparar den ändrade Excel-filen
workbook.Save(outputDir + "outSourseSampleCountryNames.xlsx");
```

 Förklaring: The`Save` metod skriver den modifierade arbetsboken tillbaka till den angivna utdatasökvägen. Detta faller under att skriva dina definierade filter till en ny fil så att dina ursprungliga data förblir intakta.

## Steg 8: Utdatabekräftelse

Låt oss slutligen bekräfta att vår operation var framgångsrik:

```csharp
Console.WriteLine("AutofilterBeginsWith executed successfully.\r\n");
```

Förklaring: Denna enkla rad matar ut ett bekräftelsemeddelande till konsolen, som låter dig veta att filtreringsprocessen slutfördes utan fel.

## Slutsats

en värld där datahantering kan kännas överväldigande, bemästra funktioner som AutoFilter i Excel genom Aspose.Cells för .NET ger dig möjlighet att manipulera data effektivt och effektivt. Du har lärt dig hur du filtrerar Excel-rader som börjar med "Ba", och implementerar metoden steg för steg. Med övning kommer du att kunna anpassa denna metod för olika datafiltreringsbehov i dina pågående projekt.

## FAQ's

### Vad är syftet med AutoFilter i Excel?  
AutoFilter tillåter användare att snabbt sortera och filtrera data i ett kalkylblad, vilket gör det enkelt att fokusera på specifika datamängder.

### Kan jag filtrera baserat på flera kriterier med Aspose.Cells?  
Ja, Aspose.Cells stöder avancerade filtreringsalternativ som låter dig ställa in flera kriterier.

### Behöver jag en licens för att Aspose.Cells ska kunna använda den?  
Även om du kan börja med en gratis provperiod, krävs en licens för full funktionalitet och för att ta bort eventuella provperioder.

### Vilka typer av filtrering kan jag utföra med Aspose.Cells?  
Du kan filtrera data efter värde, villkor (som börjar med eller slutar med) och anpassad filtrering för att uppfylla dina specifika krav.

### Var kan jag hitta mer information om Aspose.Cells för .NET?  
 Du kan kontrollera dokumentationen[här](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
