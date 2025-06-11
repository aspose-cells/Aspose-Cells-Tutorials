---
"description": "Lär dig hur du importerar data till Excel-ark med angivna formelfält med hjälp av Aspose.Cells för .NET i den här detaljerade handledningen."
"linktitle": "Ange formelfält vid import av data till Excel-ark"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Ange formelfält vid import av data till Excel-ark"
"url": "/sv/net/excel-custom-number-date-formatting/specify-formula-fields-while-importing-data-to-worksheet-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ange formelfält vid import av data till Excel-ark

## Introduktion

När det gäller att hantera Excel-filer programmatiskt är Aspose.Cells för .NET ett ovärderligt verktyg. Det ger robust funktionalitet för att enkelt skapa, modifiera och manipulera Excel-kalkylblad. En av de intressanta funktionerna är möjligheten att ange formelfält när data importeras till ett Excel-ark. Tänk dig att du arbetar med en finansiell rapport och behöver automatiskt beräkna totalsummor baserat på användarinmatning. Den här handledningen guidar dig steg för steg för att uppnå just detta med en ren och enkel metod.

## Förkunskapskrav

Innan vi går in i koden, låt oss se till att du har allt du behöver. 

1. Visual Studio eller någon annan integrerad .NET-utvecklingsmiljö (IDE): Se till att du har en lämplig IDE för att skriva och köra din C#-kod.
2. Aspose.Cells för .NET: Du måste ladda ner och referera till Aspose.Cells-biblioteket i ditt projekt. Du kan ladda ner det från [Aspose-utgåvor](https://releases.aspose.com/cells/net/).
3. Grundläggande C#-kunskaper: Bekantskap med C# och objektorienterade programmeringskoncept hjälper dig att förstå exemplen bättre.
4. .NET Framework: Den här handledningen förutsätter att du använder .NET Framework 4.5 eller senare.

När du har bestämt dig för förutsättningarna kan vi importera data till ett Excel-ark med angivna formelfält.

## Importera paket

Innan du börjar skriva din kod måste du importera det nödvändiga namnutrymmet Aspose.Cells. Detta görs vanligtvis högst upp i din C#-fil:

```csharp
using Aspose.Cells;
using System;
using System.Collections.Generic;
```

Detta gör att du kan använda klasser och metoder som tillhandahålls av Aspose.Cells-biblioteket utan att behöva prefixa dem med namnrymden varje gång.

Låt oss dela upp hela processen i hanterbara steg:

## Steg 1: Definiera utdatakatalogen

Först måste du bestämma var du vill spara din Excel-fil. Så här gör du:

```csharp
static string outputDir = "Your Document Directory"; // ange din dokumentkatalog här
```

Ersätta `"Your Document Directory"` med din faktiska sökväg. Det är här den genererade Excel-filen sparas.

## Steg 2: Skapa en användardefinierad klass för dataobjekt

Nästa steg är att definiera en klass för att strukturera den data vi planerar att importera.

```csharp
class DataItems
{
    public int Number1 { get; set; }
    public int Number2 { get; set; }
    public string Formula1 { get; set; }
    public string Formula2 { get; set; }
}
```

Detta `DataItems` Klassen kommer att innehålla de råa heltalen och formlerna som vi kommer att skriva till Excel-arket. 

## Steg 3: Initiera en lista för att innehålla dataobjekt

Vi kommer att använda en lista för att lagra flera instanser av vår `DataItems` klass.

```csharp
List<DataItems> dis = new List<DataItems>();
```

## Steg 4: Lägg till dataobjekt i listan

Nu ska vi lägga till några poster i vår lista. Varje post kommer att innehålla två tal och två formler.

```csharp
// Definiera och lägg till varje dataelement
DataItems di = new DataItems();
di.Number1 = 2002;
di.Number2 = 3502;
di.Formula1 = "=SUM(A2,B2)";
di.Formula2 = "=HYPERLINK(\"https://www.aspose.com\",\"Aspose webbplats\")
dis.Add(di);

// Upprepa för ytterligare dataelement
```

Se till att anpassa varje `DataItems` instans med unika värden och formler.

## Steg 5: Skapa arbetsbok och Access-arbetsblad

Skapa sedan arbetsboken och öppna det första kalkylbladet där vi så småningom ska importera data.

```csharp
Workbook wb = new Workbook(); // skapa en ny arbetsbok
Worksheet ws = wb.Worksheets[0]; // komma åt det första arbetsbladet
```

## Steg 6: Ange importtabellalternativ

Det är här magin händer. Du måste ange vilka fält i dina data som motsvarar formler. 

```csharp
ImportTableOptions opts = new ImportTableOptions();
opts.IsFormulas = new bool[] { false, false, true, true };
```

I det här exemplet innehåller de två sista fälten formler, vilket indikeras av `true`, medan de två första fälten är inställda på `false`.

## Steg 7: Importera anpassade objekt

Nu när allt är konfigurerat, låt oss importera vår lista med dataelement till kalkylbladet.

```csharp
ws.Cells.ImportCustomObjects(dis, 0, 0, opts);
```

Den här raden importerar i praktiken data från och med cell A1.

## Steg 8: Beräkna formler

Eftersom vi har importerat några formler är det viktigt att beräkna dem.

```csharp
wb.CalculateFormula();
```

Den här metoden säkerställer att dina formler utvärderas baserat på deras beroenden.

## Steg 9: Anpassa kolumner automatiskt

För att säkerställa att dina data är visningsvänliga kan du automatiskt anpassa kolumnerna baserat på innehållet.

```csharp
ws.AutoFitColumns();
```

Det här steget optimerar Excel-filens layout. 

## Steg 10: Spara din Excel-fil

Slutligen är det dags att spara din nyskapade Excel-fil. 

```csharp
wb.Save(outputDir + "outputSpecifyFormulaFieldsWhileImportingDataToWorksheet.xlsx");
```

Se till att ditt filnamn är relevant och beskrivande!

## Steg 11: Kontrollera körning

Som ett enkelt sätt att bekräfta att allt gick korrekt kanske du vill skriva ut ett meddelande.

```csharp
Console.WriteLine("SpecifyFormulaFieldsWhileImportingDataToWorksheet executed successfully.");
```

Detta ger dig omedelbar feedback på att koden har fungerat utan problem.

## Slutsats

Och där har du det! Du har framgångsrikt importerat data till ett Excel-ark med hjälp av Aspose.Cells för .NET och specificerade formelfält. Genom att följa dessa steg kan du tillämpa liknande tekniker för att automatisera databehandlingsuppgifter anpassade efter dina behov. Oavsett om du bearbetar siffror för rapporter eller helt enkelt underhåller data, är det värt att bemästra konsten att manipulera Excel med Aspose.

## Vanliga frågor

### Vad är Aspose.Cells?
Aspose.Cells är ett .NET-bibliotek utformat för att skapa, manipulera och konvertera Excel-filer programmatiskt.

### Hur installerar jag Aspose.Cells för .NET?
Du kan ladda ner den från [Aspose-utgåvor](https://releases.aspose.com/cells/net/) och referera till det i ditt projekt.

### Kan jag använda Aspose.Cells gratis?
Ja, Aspose erbjuder en gratis provperiod på [den här länken](https://releases.aspose.com/).

### Var kan jag hitta fler exempel?
Ytterligare exempel och dokumentation finns på [Aspose-dokumentationssida](https://reference.aspose.com/cells/net/).

### Vad händer om jag stöter på problem när jag använder Aspose?
Du kan söka hjälp från Aspose supportforum [här](https://forum.aspose.com/c/cells/9).
 

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}