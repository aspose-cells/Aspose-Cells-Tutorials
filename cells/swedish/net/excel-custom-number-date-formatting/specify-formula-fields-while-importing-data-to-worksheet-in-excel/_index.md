---
title: Ange formelfält när du importerar data till Excel-ark
linktitle: Ange formelfält när du importerar data till Excel-ark
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du importerar data till Excel-ark med specificerade formelfält med Aspose.Cells för .NET i denna detaljerade självstudiekurs.
weight: 11
url: /sv/net/excel-custom-number-date-formatting/specify-formula-fields-while-importing-data-to-worksheet-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ange formelfält när du importerar data till Excel-ark

## Introduktion

När det gäller att hantera Excel-filer programmatiskt är Aspose.Cells för .NET ett ovärderligt verktyg. Det ger robust funktionalitet för att skapa, ändra och manipulera Excel-kalkylblad med lätthet. En av de intressanta funktionerna som den erbjuder är möjligheten att specificera formelfält medan du importerar data till ett Excel-ark. Föreställ dig att du arbetar med en finansiell rapport och behöver automatiskt beräkna totalsummor baserat på användarinmatning. Denna handledning guidar dig steg-för-steg för att uppnå just det med ett rent och okomplicerat tillvägagångssätt.

## Förutsättningar

Innan vi dyker in i koden, låt oss se till att du har allt du behöver. 

1. Visual Studio eller någon integrerad .NET-utvecklingsmiljö (IDE): Se till att du har en lämplig IDE för att skriva och köra din C#-kod.
2.  Aspose.Cells för .NET: Du måste ladda ner och referera till Aspose.Cells-biblioteket i ditt projekt. Du kan ladda ner den från[Aspose släpper](https://releases.aspose.com/cells/net/).
3. Grundläggande C#-kunskaper: Bekantskap med C# och objektorienterade programmeringskoncept hjälper dig att förstå exemplen bättre.
4. .NET Framework: Denna handledning förutsätter att du använder .NET Framework 4.5 eller högre.

När du har löst förutsättningarna, låt oss fortsätta att importera vissa data till ett Excel-ark med specificerade formelfält.

## Importera paket

Innan du börjar skriva din kod måste du importera den nödvändiga Aspose.Cells-namnrymden. Detta görs vanligtvis överst i din C#-fil:

```csharp
using Aspose.Cells;
using System;
using System.Collections.Generic;
```

Detta gör att du kan använda klasserna och metoderna som tillhandahålls av Aspose.Cells-biblioteket utan att behöva prefixa dem med namnutrymmet varje gång.

Låt oss dela upp hela processen i hanterbara steg:

## Steg 1: Definiera utdatakatalogen

Först måste du fastställa var du vill spara din Excel-fil. Så här kan du göra det:

```csharp
static string outputDir = "Your Document Directory"; // ange din dokumentkatalog här
```

 Ersätta`"Your Document Directory"` med din faktiska filsökväg. Det är här den genererade Excel-filen kommer att sparas.

## Steg 2: Skapa en användardefinierad klass för dataobjekt

Därefter kommer vi att definiera en klass för att strukturera de data vi planerar att importera.

```csharp
class DataItems
{
    public int Number1 { get; set; }
    public int Number2 { get; set; }
    public string Formula1 { get; set; }
    public string Formula2 { get; set; }
}
```

 Detta`DataItems` klass kommer att hålla de råa heltal och formlerna som vi kommer att skriva till Excel-arket. 

## Steg 3: Initiera en lista för att hålla dataobjekt

 Vi kommer att använda en lista för att hålla flera instanser av vår`DataItems` klass.

```csharp
List<DataItems> dis = new List<DataItems>();
```

## Steg 4: Lägg till dataobjekt till listan

Låt oss nu lägga till några poster till vår lista. Varje post kommer att innehålla två siffror och två formler.

```csharp
// Definiera och lägg till varje dataobjekt
DataItems di = new DataItems();
di.Number1 = 2002;
di.Number2 = 3502;
di.Formula1 = "=SUM(A2,B2)";
di.Formula2 = "=HYPERLINK(\"https://www.aspose.com\",\"Aspose webbplats\"";
dis.Add(di);

// Upprepa för ytterligare dataobjekt
```

 Se till att anpassa var och en`DataItems` instans med unika värden och formler.

## Steg 5: Skapa arbetsbok och åtkomstkalkylblad

Skapa sedan arbetsboken och få tillgång till det första kalkylbladet där vi så småningom kommer att importera data.

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

 I det här exemplet innehåller de två sista fälten formler, vilket indikeras med`true` , medan de två första fälten är inställda på`false`.

## Steg 7: Importera anpassade objekt

Nu när allt är inställt, låt oss importera vår lista över dataobjekt till kalkylbladet.

```csharp
ws.Cells.ImportCustomObjects(dis, 0, 0, opts);
```

Denna rad importerar effektivt data från cell A1.

## Steg 8: Beräkna formler

Eftersom vi har importerat några formler är det viktigt att beräkna dem.

```csharp
wb.CalculateFormula();
```

Den här metoden säkerställer att dina formler utvärderas utifrån deras beroenden.

## Steg 9: Anpassa kolumner automatiskt

För att se till att din data är visningsvänlig kan du automatiskt anpassa kolumnerna baserat på innehållet.

```csharp
ws.AutoFitColumns();
```

Detta steg optimerar Excel-filens layout. 

## Steg 10: Spara din Excel-fil

Äntligen är det dags att spara din nyskapade Excel-fil. 

```csharp
wb.Save(outputDir + "outputSpecifyFormulaFieldsWhileImportingDataToWorksheet.xlsx");
```

Se till att ditt utdatafilnamn är relevant och beskrivande!

## Steg 11: Kontrollera utförande

Som ett enkelt sätt att bekräfta att allt fungerade korrekt, kanske du vill skriva ut ett meddelande.

```csharp
Console.WriteLine("SpecifyFormulaFieldsWhileImportingDataToWorksheet executed successfully.");
```

Detta ger dig omedelbar feedback om att koden har fungerat utan några problem.

## Slutsats

Och där har du det! Du har framgångsrikt importerat data till ett Excel-ark med Aspose.Cells för .NET och specificerade formelfält. Genom att följa dessa steg kan du använda liknande tekniker för att automatisera databearbetningsuppgifter som är skräddarsydda för dina behov. Oavsett om du håller på med siffror för rapporter eller bara underhåller data, är det en färdighet värd att ha att behärska konsten att manipulera Excel med Aspose.

## FAQ's

### Vad är Aspose.Cells?
Aspose.Cells är ett .NET-bibliotek designat för att skapa, manipulera och konvertera Excel-filer programmatiskt.

### Hur installerar jag Aspose.Cells för .NET?
 Du kan ladda ner den från[Aspose släpper](https://releases.aspose.com/cells/net/) och referera till det i ditt projekt.

### Kan jag använda Aspose.Cells gratis?
 Ja, Aspose erbjuder en gratis provperiod tillgänglig på[denna länk](https://releases.aspose.com/).

### Var kan jag hitta fler exempel?
 Ytterligare exempel och dokumentation finns på[Aspose dokumentationssida](https://reference.aspose.com/cells/net/).

### Vad händer om jag stöter på problem när jag använder Aspose?
 Du kan söka hjälp från Asposes supportforum[här](https://forum.aspose.com/c/cells/9).
 
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
