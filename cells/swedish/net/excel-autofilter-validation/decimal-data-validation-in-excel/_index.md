---
title: Decimaldatavalidering i Excel
linktitle: Decimaldatavalidering i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Upptäck hur du implementerar decimaldatavalidering i Excel med Aspose.Cells för .NET med vår lättanvända guide. Förbättra dataintegriteten utan ansträngning.
weight: 11
url: /sv/net/excel-autofilter-validation/decimal-data-validation-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Decimaldatavalidering i Excel

## Introduktion

Att skapa kalkylblad med korrekt data är avgörande för tydlig kommunikation i alla företag. Ett sätt att säkerställa dataprecision är att använda datavalidering i Excel. I den här handledningen kommer vi att utnyttja kraften i Aspose.Cells för .NET för att skapa en decimaldatavalideringsmekanism som håller dina data tillförlitliga och rena. Om du vill förbättra ditt Excel-spel har du kommit rätt!

## Förutsättningar

Innan du dyker in i koden, se till att du har allt förberett för en smidig seglingsupplevelse:

1. Visual Studio: Ladda ner och installera Visual Studio om du inte redan har gjort det. Det är den perfekta miljön för att utveckla .NET-applikationer.
2.  Aspose.Cells för .NET: Du måste lägga till Aspose.Cells-biblioteket i ditt projekt. Du kan ladda ner den via[denna länk](https://releases.aspose.com/cells/net/).
3. Grundläggande kunskaper om C#: Även om vi kommer att förklara allt steg-för-steg, kommer en grundläggande förståelse av C#-programmering att ge dig ett bättre grepp om begreppen.
4. .NET Framework: Se till att du har det nödvändiga .NET Framework installerat som är kompatibelt med Aspose.Cells.
5. Bibliotek: Referera till Aspose.Cells-biblioteket i ditt projekt för att undvika kompileringsfel.

Nu när vi har täckt grunderna, låt oss hoppa in i den spännande delen: kodning.

## Importera paket

För att börja måste du importera de nödvändiga paketen i din C#-fil. Detta ger dig tillgång till Aspose.Cells funktioner.

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Genom att inkludera den här raden överst i din fil, säger du till C# att leta efter Aspose.Cells-funktionen som låter dig manipulera Excel-filer.

Nu när vi har satt scenen, låt oss gå igenom stegen som krävs för att skapa decimaldatavalidering i ett Excel-kalkylblad.

## Steg 1: Konfigurera din dokumentkatalog

Innan du kan spara några filer måste du se till att din dokumentkatalog är korrekt inställd:

```csharp
string dataDir = "Your Document Directory";
```

 Ersätta`"Your Document Directory"` med sökvägen där du vill spara dina Excel-filer.

## Steg 2: Kontrollera om det finns en katalog

Det här utdraget kontrollerar om katalogen finns och skapar den om den inte gör det:

```csharp
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

Det här steget är som att se till att din arbetsyta är klar innan du startar ett nytt projekt. Ingen röra, ingen stress!

## Steg 3: Skapa ett arbetsboksobjekt

Låt oss sedan skapa ett nytt arbetsboksobjekt, som i huvudsak är en Excel-fil:

```csharp
Workbook workbook = new Workbook();
```

Se en arbetsbok som en tom arbetsyta för dina data. Vid det här laget har den inget innehåll men är redo att målas.

## Steg 4: Skapa och få åtkomst till kalkylbladet


Låt oss nu skapa ett kalkylblad och komma åt det första bladet i arbetsboken:

```csharp
Worksheet ExcelWorkSheet = workbook.Worksheets[0];
```

Precis som en bok har flera sidor kan en arbetsbok ha flera kalkylblad. Vi fokuserar just nu på den första.

## Steg 5: Skaffa valideringssamlingen

Låt oss nu ta fram valideringssamlingen från kalkylbladet eftersom det är här vi kommer att hantera våra datavalideringsregler:

```csharp
ValidationCollection validations = ExcelWorkSheet.Validations;
```

Det här steget liknar att kolla in verktygslådan innan du startar ett projekt.

## Steg 6: Definiera cellområdet för validering

Vi måste definiera området där valideringen gäller:

```csharp
CellArea ca = new CellArea();
ca.StartRow = 0;
ca.EndRow = 0;
ca.StartColumn = 0;
ca.EndColumn = 0;
```

Här stipulerar vi att datavalideringen kommer att tillämpas på en enskild cell – närmare bestämt den första cellen i kalkylbladet (A1).

## Steg 7: Skapa och lägg till validering

Låt oss skapa vårt valideringsobjekt och lägga till det i valideringssamlingen:

```csharp
Validation validation = validations[validations.Add(ca)];
```

Nu har vi ett valideringsobjekt som vi ska konfigurera för att upprätthålla våra decimalvillkor.

## Steg 8: Ställ in valideringstyp

Därefter anger vi vilken typ av validering vi vill ha:

```csharp
validation.Type = ValidationType.Decimal;
```

Genom att ställa in typen till Decimal, instruerar vi Excel att förvänta sig decimalvärden i den validerade cellen.

## Steg 9: Ange operatör

Nu ska vi specificera villkoret för tillåtna värden. Vi vill säkerställa att inmatade data hamnar mellan två intervall:

```csharp
validation.Operator = OperatorType.Between;
```

Se det som att dra en gränslinje. Alla nummer utanför detta intervall kommer att avvisas, vilket håller din data ren!

## Steg 10: Fastställ gränser för validering

Därefter ställer vi in de nedre och övre gränserna för vår validering:

```csharp
validation.Formula1 = Decimal.MinValue.ToString();
validation.Formula2 = Decimal.MaxValue.ToString();
```

Med dessa gränser accepteras varje decimaltal, oavsett hur stort eller litet det är, så länge det är giltigt!

## Steg 11: Anpassa felmeddelandet

Låt oss se till att användarna vet varför deras input avvisades genom att lägga till ett felmeddelande:

```csharp
validation.ErrorMessage = "Please enter a valid integer or decimal number";
```

Detta leder till en användarvänlig upplevelse, eftersom det ger vägledning om vad som ska matas in.

## Steg 12: Definiera valideringsområdet

Låt oss nu specificera cellerna som ska bära denna validering:

```csharp
CellArea area;
area.StartRow = 0;
area.EndRow = 9;
area.StartColumn = 0;
area.EndColumn = 0;
```

den här konfigurationen säger vi att valideringen gäller från cell A1 till A10.

## Steg 13: Lägg till valideringsområdet

Nu när vi har definierat vårt valideringsområde, låt oss tillämpa det:

```csharp
validation.AddArea(area);
```

Din validering är nu stadigt på plats, redo att fånga alla olämpliga input!

## Steg 14: Spara arbetsboken

Slutligen, låt oss spara arbetsboken med vår decimaldatavalidering på plats:

```csharp
workbook.Save(dataDir + "output.out.xls");
```

Och där har du det! Du har framgångsrikt skapat en arbetsbok med decimaldatavalidering med Aspose.Cells för .NET.

## Slutsats

Att implementera decimaldatavalidering i Excel med Aspose.Cells för .NET är en bris när du följer dessa enkla steg. Du säkerställer inte bara att data förblir rena och strukturerade, utan du förbättrar också den övergripande dataintegriteten i dina kalkylblad, vilket gör dem tillförlitliga och användarvänliga.
Oavsett om du är inom ekonomi, projektledning eller något annat område som använder datarapportering, kommer att bemästra dessa färdigheter att förbättra din produktivitet avsevärt. Så varsågod, ge det ett försök! Dina kalkylblad kommer att tacka dig för det.

## FAQ's

### Vad är datavalidering i Excel?
Datavalidering i Excel är en funktion som begränsar vilken typ av data som kan matas in i en viss cell eller område, vilket säkerställer dataintegritet.

### Kan jag anpassa felmeddelandet i datavalidering?
Ja! Du kan tillhandahålla anpassade felmeddelanden för att vägleda användare när felaktiga datainmatningar görs.

### Är Aspose.Cells gratis att använda?
 Aspose.Cells erbjuder en gratis provperiod, men du behöver en licens för långvarig användning. Du kan hitta mer information om hur du skaffar en tillfällig licens[här](https://purchase.aspose.com/temporary-license/).

### Vilka datatyper kan jag validera i Excel?
Med Aspose.Cells kan du validera olika datatyper inklusive heltal, decimaler, datum, listor och anpassade formler.

### Var kan jag hitta mer Aspose.Cells-dokumentation?
 Du kan utforska den omfattande dokumentationen[här](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
