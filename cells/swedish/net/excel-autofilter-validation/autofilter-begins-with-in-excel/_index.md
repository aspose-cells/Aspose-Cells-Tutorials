---
"description": "Lär dig hur du enkelt autofiltrerar Excel-rader med Aspose.Cells i .NET med den här omfattande steg-för-steg-guiden."
"linktitle": "Autofilter börjar med i Excel"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Autofilter börjar med i Excel"
"url": "/sv/net/excel-autofilter-validation/autofilter-begins-with-in-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Autofilter börjar med i Excel

## Introduktion

När det gäller att arbeta med data har Excel etablerat sig som ett självklart program för otaliga branscher och ändamål. En av dess kraftfullaste funktioner är AutoFilter, vilket gör det enkelt att söka igenom omfattande datamängder. Om du använder Aspose.Cells för .NET kan du utnyttja den här funktionen programmatiskt och avsevärt förbättra dina datahanteringsuppgifter. I den här guiden kommer vi att guida dig genom processen att implementera en funktion som filtrerar Excel-rader baserat på om de börjar med en viss sträng.

## Förkunskapskrav

Innan du ger dig i kast med det, se till att du har följande förutsättningar på plats:

1. Utvecklingsmiljö: Bekanta dig med en .NET-utvecklingsmiljö. Detta kan vara Visual Studio eller någon annan IDE som du väljer.
2. Aspose.Cells för .NET: Du behöver ha Aspose.Cells för .NET installerat. Om du inte redan har gjort det kan du enkelt ladda ner det. [här](https://releases.aspose.com/cells/net/).
3. Grundläggande kunskaper i C#: En grundläggande förståelse för C# och hur man arbetar med .NET-bibliotek hjälper dig att följa med smidigt.
4. Exempeldata: Du bör ha en Excel-fil, helst med namnet `sourseSampleCountryNames.xlsx`, som finns i din angivna källkatalog. Den här filen kommer att innehålla de data vi kommer att filtrera.
5. Licensiering: För full funktionalitet, överväg att skaffa en licens via detta [länk](https://purchase.aspose.com/buy)Om du vill testa funktionerna kan du begära en [tillfällig licens](https://purchase.aspose.com/temporary-license/).

Har du allt klart? Nu kör vi!

## Importera paket

För att komma igång, importera de nödvändiga namnrymderna högst upp i din C#-fil:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Detta importerar kärnfunktionaliteten i Aspose.Cells tillsammans med grundläggande systemfunktioner som vi kommer att förlita oss på för konsolinteraktion.

Nu när du har konfigurerat din miljö och importerat de nödvändiga paketen, låt oss dela upp autofilterfunktionen i hanterbara steg. Vi kommer att implementera ett filter som extraherar rader som börjar med "Ba".

## Steg 1: Definiera käll- och utdatakataloger

Först, låt oss definiera var vår Excel-indatafil finns, samt var vi vill spara vår filtrerade utdata:

```csharp
// Källkatalog
string sourceDir = "Your Document Directory\\";

// Utdatakatalog
string outputDir = "Your Document Directory\\";
```

Förklaring: Ersätt här `"Your Document Directory\\"` med den faktiska sökvägen till dina kataloger. Se till att avsluta katalogsökvägarna med ett dubbelt omvänt snedstreck (`\\`) för att undvika problem med vägen.

## Steg 2: Instansiera arbetsboksobjektet

Nästa steg är att skapa ett arbetsboksobjekt som pekar på vår Excel-fil:

```csharp
// Instansiera ett arbetsboksobjekt som innehåller exempeldata
Workbook workbook = new Workbook(sourceDir + "sourseSampleCountryNames.xlsx");
```

Förklaring: Den här raden initierar en ny arbetsboksinstans med den angivna filsökvägen. `Workbook` klassen är grundläggande eftersom den representerar hela Excel-filen.

## Steg 3: Åtkomst till det första arbetsbladet

Nu behöver vi komma åt det specifika arbetsbladet som vi vill arbeta med:

```csharp
// Åtkomst till det första kalkylbladet i Excel-filen
Worksheet worksheet = workbook.Worksheets[0];
```

Förklaring: Den `Worksheets` samlingen ger oss åtkomst till enskilda ark. Använda `[0]` refererar till det första kalkylbladet i din Excel-fil, vilket vanligtvis är vanligt när man arbetar med en fil med ett enda ark.

## Steg 4: Konfigurera autofiltret

Här börjar magin! Vi skapar ett AutoFilter-område för våra data:

```csharp
// Skapa autofilter genom att ge cellerna ett intervall
worksheet.AutoFilter.Range = "A1:A18";
```

Förklaring: Den `AutoFilter.Range` Med egenskapen kan du ange vilka rader som ska filtreras. I det här fallet filtrerar vi rader inom intervallet A1 till A18, vilka antas innehålla våra data.

## Steg 5: Tillämpa filtervillkor

Nästa steg är att definiera filtervillkoret. Vi vill bara visa de rader vars första kolumnvärden börjar med "Ba":

```csharp
// Initiera filter för rader som börjar med strängen "Ba"
worksheet.AutoFilter.Custom(0, FilterOperatorType.BeginsWith, "Ba");
```

Förklaring: Den `Custom` Metoden definierar vår filtreringslogik. Det första argumentet (`0`) indikerar att vi filtrerar baserat på den första kolumnen (A), och `FilterOperatorType.BeginsWith` anger vårt villkor att söka efter rader som börjar med "Ba".

## Steg 6: Uppdatera filtret

Efter att vi har tillämpat vårt filtervillkor måste vi se till att Excel uppdateras för att återspegla ändringarna:

```csharp
// Uppdatera filtret för att visa/dölja filtrerade rader
worksheet.AutoFilter.Refresh();
```

Förklaring: Den här raden anropar en uppdatering av AutoFilter för att säkerställa att de synliga raderna motsvarar de tillämpade filterkriterierna. Det är ungefär som att trycka på uppdateringsknappen i Excel.

## Steg 7: Spara den modifierade Excel-filen

Nu är det dags att spara de ändringar vi har gjort:

```csharp
// Spara den modifierade Excel-filen
workbook.Save(outputDir + "outSourseSampleCountryNames.xlsx");
```

Förklaring: Den `Save` Metoden skriver tillbaka den modifierade arbetsboken till den angivna utdatasökvägen. Detta faller under att skriva dina definierade filter till en ny fil så att dina ursprungliga data förblir intakta.

## Steg 8: Bekräftelse av utdata

Slutligen, låt oss bekräfta att vår operation lyckades:

```csharp
Console.WriteLine("AutofilterBeginsWith executed successfully.\r\n");
```

Förklaring: Den här enkla raden skickar ett bekräftelsemeddelande till konsolen som meddelar att filtreringsprocessen slutfördes utan fel.

## Slutsats

I en värld där datahantering kan kännas överväldigande, ger bemästring av funktioner som AutoFilter i Excel genom Aspose.Cells för .NET dig möjlighet att manipulera data effektivt och ändamålsenligt. Du har lärt dig hur du filtrerar Excel-rader som börjar med "Ba" och implementerar metoden steg för steg. Med övning kommer du att kunna anpassa den här metoden för olika datafiltreringsbehov i dina pågående projekt.

## Vanliga frågor

### Vad är syftet med AutoFilter i Excel?  
Med AutoFilter kan användare snabbt sortera och filtrera data i ett kalkylblad, vilket gör det enkelt att fokusera på specifika datamängder.

### Kan jag filtrera baserat på flera kriterier med Aspose.Cells?  
Ja, Aspose.Cells stöder avancerade filtreringsalternativ som låter dig ange flera kriterier.

### Behöver jag en licens för att använda Aspose.Cells?  
Även om du kan börja med en gratis provperiod krävs en licens för full funktionalitet och för att ta bort eventuella begränsningar i provperioden.

### Vilka typer av filtrering kan jag utföra med Aspose.Cells?  
Du kan filtrera data efter värde, villkor (t.ex. börjar med eller slutar med) och anpassad filtrering för att möta dina specifika krav.

### Var kan jag hitta mer information om Aspose.Cells för .NET?  
Du kan kontrollera dokumentationen [här](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}