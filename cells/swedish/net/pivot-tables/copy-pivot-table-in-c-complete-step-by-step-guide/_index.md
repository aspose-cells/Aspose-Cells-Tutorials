---
category: general
date: 2026-03-25
description: Kopiera pivottabell med C# och Aspose.Cells. Lär dig hur du kopierar
  pivottabellen, exporterar pivottabellfilen och bevarar data på några minuter.
draft: false
keywords:
- copy pivot table
- how to copy pivot
- export pivot table file
- Aspose.Cells pivot
- C# Excel automation
language: sv
og_description: Kopiera pivottabell i C# med Aspose.Cells. Denna guide visar hur du
  kopierar pivottabell, exporterar pivottabellfil och behåller alla inställningar
  intakta.
og_title: Kopiera pivottabell i C# – Fullständig programmeringshandledning
tags:
- C#
- Excel
- Aspose.Cells
- Data Export
title: Kopiera pivottabell i C# – Komplett steg‑för‑steg‑guide
url: /sv/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopiera pivottabell i C# – Komplett steg‑för‑steg‑guide

Har du någonsin behövt **copy pivot table** från en arbetsbok till en annan och undrat om pivottlogiken överlever flytten? Du är inte ensam. I många rapporteringspipelines genererar vi en huvudarbetsbok och skickar sedan en lättviktig kopia som fortfarande låter slutanvändare skiva data. Den goda nyheten? Med några rader C# och Aspose.Cells kan du göra exakt det—ingen manuell hackning krävs.

I den här handledningen går vi igenom hela processen: laddar källfilen, väljer området som innehåller pivottabellen, klistrar in den i en ny arbetsbok samtidigt som pivottdefinitionen bevaras, och slutligen **export pivot table file** för vidare konsumtion. I slutet kommer du att veta *how to copy pivot* programatiskt och ha ett färdigt exempel som du kan lägga in i ditt projekt.

## Förutsättningar

- .NET 6+ (eller .NET Framework 4.6+) installerat  
- Aspose.Cells för .NET NuGet‑paket (`Install-Package Aspose.Cells`)  
- En käll‑Excel‑fil (`source.xlsx`) som redan innehåller en pivottabell (valfri storlek fungerar)  
- Grundläggande C#‑kunskaper; ingen djup Excel‑intern kunskap krävs  

Om du saknar någon av dessa, lägg bara till NuGet‑paketet och öppna Visual Studio—inget mer.

## Vad koden gör (Översikt)

1. **Load** arbetsboken som innehåller den ursprungliga pivottabellen.  
2. **Define** ett `Range` som omsluter hela pivottabellen (inklusive dess cache).  
3. **Create** en helt ny arbetsbok som blir destinationen.  
4. **Paste** området med `CopyPivotTable = true` så pivottdefinitionen kopieras, inte bara värdena.  
5. **Save** destinationsfilen, vilket ger dig en **export pivot table file** som du kan dela.  

Det är hela arbetsflödet i fem enkla steg. Låt oss dyka in i varje steg.

## Steg 1 – Ladda källarboken som innehåller pivottabellen

Först måste vi läsa in källfilen i minnet. Aspose.Cells gör detta till en enradare.

```csharp
using Aspose.Cells;

// Load the source workbook (replace the path with your actual file)
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet – adjust the index if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
```

*Why this matters:* Laddning av arbetsboken ger oss åtkomst till den underliggande pivottcachen. Om du bara kopierar cellvärden förlorar pivottabellen sin slicer‑funktion. Genom att hålla arbetsboksobjektet levande bevarar vi hela pivottmetadata.

## Steg 2 – Definiera området som inkluderar pivottabellen

En pivottabell är inte bara ett block med celler; den har också dold cache‑data. Det säkraste sättet är att välja en rektangel som helt omger det synliga området. I de flesta fall fungerar `A1:E20`, men du kan programatiskt upptäcka de exakta gränserna med `PivotTable`‑egenskaper.

```csharp
// Example range – adjust to match your pivot's size
Range sourceRange = sourceSheet.Cells.CreateRange("A1:E20");

// (Optional) Dynamically get the used range of the pivot:
PivotTable pivot = sourceSheet.PivotTables[0];
int firstRow = pivot.Row - 1;      // include header row
int firstCol = pivot.Column - 1;   // include field list
int lastRow  = pivot.Row + pivot.RowCount;
int lastCol  = pivot.Column + pivot.ColumnCount;
Range dynamicRange = sourceSheet.Cells.CreateRange(firstRow, firstCol,
                                                    lastRow - firstRow + 1,
                                                    lastCol - firstCol + 1);
```

*Why we choose a range:* `Paste`‑metoden fungerar på ett `Range`‑objekt. Genom att ange det exakta området säkerställer vi att både pivottlayouten och dess cache färdas tillsammans.

## Steg 3 – Skapa en ny destinationsarbetsbok

Nu skapar vi en tom arbetsbok som ska ta emot den kopierade pivottabellen. Inget avancerat, bara en ren start.

```csharp
// Initialize an empty workbook – it comes with one default worksheet
Workbook destinationWorkbook = new Workbook();
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

*Tip:* Om du behöver bevara befintliga kalkylblad (t.ex. en mall) kan du lägga till den nya arbetsboken som en klon av en mallfil istället för att använda den tomma konstruktorn.

## Steg 4 – Klistra in området medan pivottabellen bevaras

Här är hjärtat i operationen. Att sätta `CopyPivotTable = true` instruerar Aspose.Cells att överföra pivottdefinitionen, inte bara de visade värdena.

```csharp
destinationSheet.Cells.Paste(
    sourceRange,
    new PasteOptions
    {
        PasteType = PasteType.All,      // copy everything: formulas, formats, etc.
        CopyPivotTable = true           // crucial – keeps the pivot functional
    });
```

*What happens under the hood?* Aspose.Cells återskapar pivottcachen i destinationsarboken, omkopplar pivottens datakälla och behåller slicers, filter och beräknade fält. Resultatet är en fullt interaktiv pivottabell—precis vad du skulle förvänta dig om du duplicerade bladet manuellt i Excel.

## Steg 5 – Spara den resulterande arbetsboken (Export Pivot Table File)

Till sist skriver vi destinationsarboken till disk. Filen du får är din **export pivot table file** klar för distribution.

```csharp
destinationWorkbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");
```

Öppna `copy-pivot.xlsx` i Excel, så ser du pivottabellen intakt, redo att uppdateras eller skivas.

## Fullständigt fungerande exempel (Alla steg kombinerade)

Nedan är det kompletta programmet som du kan copy‑paste in i en konsolapp. Det inkluderar felhantering och kommentarer för tydlighet.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // 1️⃣ Load source workbook with the pivot table
                Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
                Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

                // 2️⃣ Define the range that fully encloses the pivot
                // Adjust "A1:E20" as needed, or use dynamic detection shown earlier
                Range sourceRange = sourceSheet.Cells.CreateRange("A1:E20");

                // 3️⃣ Create a fresh destination workbook
                Workbook destinationWorkbook = new Workbook();
                Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

                // 4️⃣ Paste the range and keep the pivot definition
                destinationSheet.Cells.Paste(
                    sourceRange,
                    new PasteOptions
                    {
                        PasteType = PasteType.All,
                        CopyPivotTable = true
                    });

                // 5️⃣ Save the new file – this is your exported pivot table file
                destinationWorkbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");

                Console.WriteLine("✅ Pivot table copied successfully! File saved as copy-pivot.xlsx");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❌ An error occurred: {ex.Message}");
            }
        }
    }
}
```

**Expected outcome:** När du öppnar `copy-pivot.xlsx` visas pivottabellen exakt som i `source.xlsx`. Du kan uppdatera den, ändra filter eller till och med lägga till nya datakällor utan att förlora funktionalitet.

## Vanliga frågor & edge‑cases

### Vad händer om källarboken har flera pivottabeller?

Loopa igenom `sourceSheet.PivotTables` och upprepa copy‑paste för varje. Se bara till att varje destinationsområde inte överlappar.

```csharp
int destRow = 0;
foreach (PivotTable pt in sourceSheet.PivotTables)
{
    // Calculate a non‑overlapping destination range for each pivot
    Range src = sourceSheet.Cells.CreateRange(pt.Row, pt.Column,
                                              pt.RowCount + 5, pt.ColumnCount + 5);
    destinationSheet.Cells.Paste(src, new PasteOptions { PasteType = PasteType.All, CopyPivotTable = true });
    destRow += pt.RowCount + 10; // move down for the next pivot
}
```

### Fungerar detta med externa datakällor (t.ex. SQL)?

Om den ursprungliga pivottabellen hämtar data från en extern anslutning kopieras även anslutningssträngen. Dock måste destinationsarboken ha åtkomst till samma datakälla. Du kan behöva justera autentiseringsuppgifter eller använda `WorkbookSettings` för att tillåta externa anslutningar.

### Kan jag bara kopiera pivottlayouten (utan data)?

Ställ in `PasteOptions.PasteType = PasteType.Formulas` och behåll `CopyPivotTable = true`. Detta kopierar strukturen medan datacachen lämnas tom, vilket tvingar en uppdatering vid första öppning.

### Vad händer med skydd av bladet?

Om källbladet är skyddat, avskydda det innan kopiering, eller skicka med rätt `Password` till `Worksheet.Unprotect`. Efter klistring kan du återapplicera skydd på destinationsbladet.

## Pro‑tips & fallgropar

- **Pro tip:** Använd alltid den senaste versionen av Aspose.Cells; äldre versioner hade en bugg där `CopyPivotTable` ignorerade slicers.  
- **Watch out for:** Stora pivottcacher kan göra destinationsfilen onödigt stor. Om storlek är viktigt, överväg att rensa oanvända fält innan kopiering.  
- **Performance tip:** När du kopierar många kalkylblad, inaktivera temporärt `WorkbookSettings.EnableThreadedCalculation` för att snabba upp operationen.  
- **Naming clash:** Om destinationsarboken redan innehåller en pivottabell med samma namn, kommer Aspose att byta namn på den inkommande (`PivotTable1_1`). Byt namn manuellt om du behöver en specifik identifierare.

## Visuell sammanfattning

![Kopiera pivottabell i C# – diagram som visar källarbok → områdesval → klistra in med pivottbevarande → destinationsfil](copy-pivot-diagram.png "Illustration av arbetsflöde för kopiera pivottabell")

*Alt text:* **Copy pivot table** arbetsflödesdiagram som illustrerar källa, område, klistringsalternativ och exporterad fil.

## Slutsats

Vi har gått igenom allt du behöver för att **copy pivot table** med C# och Aspose.Cells: ladda källan, välja rätt område, bevara pivottdefinitionen under klistring och slutligen exportera resultatet som en fristående fil. Snutten ovan är produktionsklar; bara ange dina sökvägar så är du redo att köra.

Nu när du vet *how to copy pivot* programatiskt kan du automatisera rapportdistribution, bygga mallgeneratorer eller integrera Excel‑analys i större .NET‑tjänster. Nästa steg kan vara att utforska **export pivot table file** till andra format (PDF, CSV) eller bädda in arbetsboken i ett web‑API för analys i realtid.

Har du ett knep du vill dela—kanske att kopiera pivoter mellan olika Excel‑versioner eller hantera PowerPivot‑modeller? Lägg en kommentar, så fortsätter vi diskussionen. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}