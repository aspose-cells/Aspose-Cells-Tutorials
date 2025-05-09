---
"description": "Upptäck hur du implementerar decimaldatavalidering i Excel med Aspose.Cells för .NET med vår lättförståeliga guide. Förbättra dataintegriteten utan ansträngning."
"linktitle": "Decimaldatavalidering i Excel"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Decimaldatavalidering i Excel"
"url": "/sv/net/excel-autofilter-validation/decimal-data-validation-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Decimaldatavalidering i Excel

## Introduktion

Att skapa kalkylblad med korrekta data är avgörande för tydlig kommunikation i alla företag. Ett sätt att säkerställa datanoggrannhet är genom att använda datavalidering i Excel. I den här handledningen ska vi utnyttja kraften i Aspose.Cells för .NET för att skapa en decimal datavalideringsmekanism som håller dina data tillförlitliga och rena. Om du vill förbättra dina Excel-kunskaper har du kommit rätt!

## Förkunskapskrav

Innan du dyker ner i koden, se till att du har allt konfigurerat för en smidig seglingsupplevelse:

1. Visual Studio: Ladda ner och installera Visual Studio om du inte redan har gjort det. Det är den perfekta miljön för att utveckla .NET-applikationer.
2. Aspose.Cells för .NET: Du måste ha lagt till Aspose.Cells-biblioteket i ditt projekt. Du kan ladda ner det via [den här länken](https://releases.aspose.com/cells/net/).
3. Grundläggande kunskaper i C#: Vi kommer att förklara allt steg för steg, men en grundläggande förståelse för C#-programmering ger dig en bättre förståelse för koncepten.
4. .NET Framework: Se till att du har den nödvändiga .NET Framework-versionen installerad som är kompatibel med Aspose.Cells.
5. Bibliotek: Använd Aspose.Cells-biblioteket i ditt projekt för att undvika kompileringsfel.

Nu när vi har gått igenom grunderna, låt oss hoppa in i den spännande delen: kodning.

## Importera paket

För att börja måste du importera de nödvändiga paketen till din C#-fil. Detta gör att du kan komma åt Aspose.Cells-funktioner.

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Genom att inkludera den här raden högst upp i din fil, ber du C# att leta efter Aspose.Cells-funktionen som låter dig manipulera Excel-filer.

Nu när vi har förberett oss, låt oss gå igenom stegen som krävs för att skapa decimaldatavalidering i ett Excel-kalkylblad.

## Steg 1: Konfigurera din dokumentkatalog

Innan du kan spara några filer måste du se till att din dokumentkatalog är korrekt konfigurerad:

```csharp
string dataDir = "Your Document Directory";
```

Ersätta `"Your Document Directory"` med sökvägen där du vill spara dina Excel-filer.

## Steg 2: Kontrollera om katalogen finns

Det här kodavsnittet kontrollerar om katalogen finns och skapar den om den inte gör det:

```csharp
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

Det här steget är som att se till att din arbetsyta är redo innan du påbörjar ett nytt projekt. Ingen röra, ingen stress!

## Steg 3: Skapa ett arbetsboksobjekt

Nu ska vi skapa ett nytt arbetsboksobjekt, vilket i huvudsak är en Excel-fil:

```csharp
Workbook workbook = new Workbook();
```

Tänk på en arbetsbok som en tom duk för dina data. Vid det här laget har den inget innehåll men är redo att målas upp.

## Steg 4: Skapa och öppna arbetsbladet


Nu ska vi skapa ett kalkylblad och komma åt det första arket i arbetsboken:

```csharp
Worksheet ExcelWorkSheet = workbook.Worksheets[0];
```

Precis som en bok har flera sidor, kan en arbetsbok ha flera arbetsblad. Vi fokuserar just nu på det första.

## Steg 5: Hämta valideringssamlingen

Nu ska vi hämta valideringssamlingen från kalkylbladet eftersom det är här vi kommer att hantera våra datavalideringsregler:

```csharp
ValidationCollection validations = ExcelWorkSheet.Validations;
```

Det här steget är som att kolla igenom verktygslådan innan du påbörjar ett projekt.

## Steg 6: Definiera cellområdet för validering

Vi behöver definiera det område där valideringen gäller:

```csharp
CellArea ca = new CellArea();
ca.StartRow = 0;
ca.EndRow = 0;
ca.StartColumn = 0;
ca.EndColumn = 0;
```

Här anger vi att datavalideringen ska tillämpas på en enda cell – närmare bestämt den första cellen i kalkylbladet (A1).

## Steg 7: Skapa och lägg till validering

Låt oss skapa vårt valideringsobjekt och lägga till det i valideringssamlingen:

```csharp
Validation validation = validations[validations.Add(ca)];
```

Nu har vi ett valideringsobjekt som vi ska konfigurera för att framtvinga våra decimalvillkor.

## Steg 8: Ange valideringstyp

Nästa steg är att ange vilken typ av validering vi vill ha:

```csharp
validation.Type = ValidationType.Decimal;
```

Genom att ställa in typen till Decimal instruerar vi Excel att förvänta sig decimalvärden i den validerade cellen.

## Steg 9: Ange operatorn

Nu ska vi ange villkoret för tillåtna värden. Vi vill säkerställa att den angivna informationen hamnar mellan två intervall:

```csharp
validation.Operator = OperatorType.Between;
```

Tänk på det som att rita en gränslinje. Alla tal utanför detta intervall kommer att avvisas, vilket håller dina data rena!

## Steg 10: Fastställ gränser för validering

Nästa steg är att sätta de nedre och övre gränserna för vår validering:

```csharp
validation.Formula1 = Decimal.MinValue.ToString();
validation.Formula2 = Decimal.MaxValue.ToString();
```

Med dessa gränser accepteras alla decimaltal, oavsett hur stora eller små de är, så länge de är giltiga!

## Steg 11: Anpassa felmeddelandet

Låt oss se till att användarna vet varför deras inmatning avvisades genom att lägga till ett felmeddelande:

```csharp
validation.ErrorMessage = "Please enter a valid integer or decimal number";
```

Detta leder till en användarvänlig upplevelse, eftersom det ger vägledning om vad man ska mata in.

## Steg 12: Definiera valideringsområdet

Nu ska vi ange de celler som ska ha denna validering:

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

Din validering är nu ordentligt på plats, redo att fånga upp eventuella felaktiga inmatningar!

## Steg 14: Spara arbetsboken

Slutligen, låt oss spara arbetsboken med vår decimaldatavalidering på plats:

```csharp
workbook.Save(dataDir + "output.out.xls");
```

Och där har du det! Du har skapat en arbetsbok med decimal datavalidering med Aspose.Cells för .NET.

## Slutsats

Att implementera decimaldatavalidering i Excel med Aspose.Cells för .NET är en barnlek när du följer dessa enkla steg. Du säkerställer inte bara att informationen förblir ren och strukturerad, utan du förbättrar också den övergripande dataintegriteten i dina kalkylblad, vilket gör dem tillförlitliga och användarvänliga.
Oavsett om du arbetar inom ekonomi, projektledning eller något annat område som använder datarapportering, kommer att behärska dessa färdigheter att öka din produktivitet avsevärt. Så fortsätt, testa! Dina kalkylblad kommer att tacka dig för det.

## Vanliga frågor

### Vad är datavalidering i Excel?
Datavalidering i Excel är en funktion som begränsar vilken typ av data som kan anges i en viss cell eller ett visst område, vilket säkerställer dataintegritet.

### Kan jag anpassa felmeddelandet i datavalideringen?
Ja! Du kan tillhandahålla anpassade felmeddelanden för att vägleda användare när felaktiga datainmatningar görs.

### Är Aspose.Cells gratis att använda?
Aspose.Cells erbjuder en gratis provperiod, men du behöver en licens för långvarig användning. Du kan hitta mer information om hur du skaffar en tillfällig licens. [här](https://purchase.aspose.com/temporary-license/).

### Vilka datatyper kan jag validera i Excel?
Med Aspose.Cells kan du validera olika datatyper, inklusive heltal, decimaler, datum, listor och anpassade formler.

### Var kan jag hitta mer dokumentation om Aspose.Cells?
Du kan utforska den omfattande dokumentationen [här](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}