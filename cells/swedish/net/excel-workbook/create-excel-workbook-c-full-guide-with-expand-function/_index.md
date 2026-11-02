---
category: general
date: 2026-06-08
description: Skapa Excel-arbetsbok i C# steg för steg och lär dig hur du använder
  expand‑funktionen i Excel för dynamiska områden. Perfekt för .NET‑utvecklare.
draft: false
keywords:
- create excel workbook c#
- use expand function in excel
language: sv
og_description: Skapa en Excel-arbetsbok i C# med ett tydligt exempel och upptäck
  hur du använder expand-funktionen i Excel för att generera dynamiska arrayer.
og_title: Skapa Excel-arbetsbok C# – Komplett programmeringsguide
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  headline: Create Excel Workbook C# – Full Guide with Expand Function
  type: TechArticle
- description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  name: Create Excel Workbook C# – Full Guide with Expand Function
  steps:
  - name: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
    text: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
  - name: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
    text: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
  - name: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
    text: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
  - name: '**Creates an Excel workbook C#** using Aspose.Cells.'
    text: '**Creates an Excel workbook C#** using Aspose.Cells.'
  - name: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
    text: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
  - name: Adds a cotangent formula (`COT(PI()/4)`).
    text: Adds a cotangent formula (`COT(PI()/4)`).
  - name: Saves the file and optionally auto‑fits columns.
    text: Saves the file and optionally auto‑fits columns.
  type: HowTo
- questions:
  - answer: Absolutely. Aspose.Cells targets .NET Standard 2.0, which is compatible
      with both .NET Core and the classic Framework.
    question: Does this work with .NET Framework 4.8?
  - answer: Use `ws.Protect(ProtectionType.All, "yourPassword");` before saving.
    question: What if I need to protect the sheet?
  - answer: 'Yes—`workbook.Save(stream, SaveFormat.Xlsx);` is handy for web APIs that
      return the file as a download. --- ## TL;DR We built a **complete C# console
      app** that: 1. **Creates an Excel workbook C#** using Aspose.Cells. 2. **Uses
      the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5 block.'
    question: Can I write the workbook directly to a `MemoryStream`?
  type: FAQPage
tags:
- csharp
- excel
- aspose-cells
- .net
title: Skapa Excel‑arbetsbok i C# – Fullständig guide med expand‑funktionen
url: /sv/net/excel-workbook/create-excel-workbook-c-full-guide-with-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel-arbetsbok C# – Fullständig guide med EXPAND-funktionen

Har du någonsin undrat hur man **skapar Excel-arbetsbok C#** utan att kämpa med COM-interoperabilitet eller trassla med XML? Du är inte ensam. I många .NET‑projekt behöver vi generera ett kalkylblad, fylla det med formler och överlämna det till icke‑tekniska användare. De goda nyheterna? Med ett modernt bibliotek som **Aspose.Cells** är hela processen en barnlek.

I den här handledningen går vi igenom ett komplett, körbart exempel som **skapar en Excel-arbetsbok C#**, lägger till ett par formler—inklusive hur man **använder EXPAND-funktionen i Excel**—och sparar filen så att du kan öppna den i Excel omedelbart. I slutet vet du inte bara *vad* du ska skriva, utan också *varför* varje rad är viktig, och du får en mall som du kan kopiera in i vilket projekt som helst.

## Förutsättningar

- .NET 6 SDK (eller någon nyare .NET‑version) installerad.
- En NuGet‑kompatibel IDE (Visual Studio, VS Code, Rider, osv.).
- **Aspose.Cells**‑paketet från NuGet – det tillhandahåller klasserna `Workbook` och `Worksheet` som används i koden.
- Grundläggande kunskaper i C#; ingen Excel‑specifik erfarenhet krävs.

Har du allt detta? Bra—låt oss börja.

## Steg 1: Skapa projektet och lägg till Aspose.Cells

Först, skapa en konsolapp och hämta in biblioteket.

```bash
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

> **Proffstips:** Om du befinner dig på ett företagsnätverk kan du behöva konfigurera en NuGet‑proxy. Aspose.Cells‑paketet är lättviktigt, så installationen slutförs på några sekunder.

Öppna nu `Program.cs`. Du kommer att se standard‑`Main`‑metoden—ersätt den med skelettet nedan.

```csharp
using System;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // All of our Excel logic will go here.
        }
    }
}
```

`using Aspose.Cells;`‑raden importerar kalkylblads‑klasserna i scopet. Om du glömmer den kommer kompilatorn klaga på att `Workbook` är odefinierad—något vi undviker senare.

## Steg 2: Skapa Excel-arbetsbok C# och få åtkomst till det första kalkylbladet

När projektet är klart kan vi äntligen **skapa Excel-arbetsbok C#**. `Workbook`‑konstruktorn ger oss en ny, tom arbetsbok, och indexet `Worksheets[0]` returnerar standardbladet (namngivet “Sheet1”).

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty .xlsx file in memory
Worksheet ws = workbook.Worksheets[0];            // reference to the first (default) sheet
```

Varför hämtar vi det första kalkylbladet explicit? Eftersom många efterföljande API:er (som att sätta formler) kräver ett `Worksheet`‑objekt, inte bara `Workbook`. Detta gör också koden tydligare för den som läser den senare.

## Steg 3: Använd EXPAND-funktionen i Excel för att fylla ett dynamiskt område

Nu kommer stjärnan i showen: **använd EXPAND-funktionen i Excel**. `EXPAND`‑funktionen (tillgänglig från Excel 365 och framåt) tar en källarray och fyller ut den till en önskad storlek. I vårt exempel börjar vi med en vertikal array på 3 rader som genereras av `SEQUENCE(3)` och expanderar den till ett 5 × 5‑block.

```csharp
// Step 3: Insert the EXPAND formula into cell A1
ws.Cells["A1"].Formula = "EXPAND(SEQUENCE(3),5,5)";
```

Vad händer egentligen?

1. `SEQUENCE(3)` producerar en vertikal array `{1;2;3}`.
2. `EXPAND(...,5,5)` instruerar Excel att växa den arrayen till 5 rader och 5 kolumner.
3. Resultatet blir ett 5 × 5‑rutnät där de första tre raderna innehåller siffrorna 1‑3 upprepade över kolumnerna, och de återstående två raderna är tomma.

Eftersom vi skriver formeln som en sträng, utvärderar Excel den *när filen öppnas*, inte vid körning. Det betyder att arbetsboken förblir lättviktig, och eventuella ändringar i källarrayen sprids automatiskt.

> **Edge case:** Om en användare öppnar arbetsboken i en äldre version av Excel som inte stödjer `EXPAND`, kommer cellen att visa `#NAME?`. För att skydda mot det kan du omsluta formeln med `IFERROR`, men i moderna miljöer är det säkert att förlita sig på funktionen.

## Steg 4: Lägg till en cotangensformel för god mått

Låt oss strö över en annan formel för att visa hur enkelt det är att lägga till matematiska uttryck. Vi beräknar cotangensen av π/4, vilket exakt är `1`.

```csharp
// Step 4: Insert a cotangent calculation in cell B1
ws.Cells["B1"].Formula = "COT(PI()/4)";
```

Excels `COT`‑funktion används inte lika ofta som `SIN` eller `COS`, men den är perfekt för trigonometriska arbetsflöden. När du öppnar arbetsboken kommer cell **B1** att visa `1`.

## Steg 5: Spara arbetsboken och verifiera resultatet

Allt detta arbete vore meningslöst om vi inte sparade filen. `Save`‑metoden skriver den minnesbaserade arbetsboken till disk. Välj en mapp du har skrivbehörighet till och ge filen ett vänligt namn.

```csharp
// Step 5: Save the workbook to the output folder
string outputPath = @"./output.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Kör programmet:

```bash
dotnet run
```

Du bör se konsolmeddelandet som bekräftar sparandet. Öppna `output.xlsx` i Excel, och du kommer att märka:

- Cellerna **A1:E5** är fyllda med den expanderade sekvensen (1,2,3 på de första tre raderna, tomma på raderna 4‑5).
- Cell **B1** visar värdet `1` från cotangensformeln.

Det är hela cykeln: **skapa excel-arbetsbok c#**, bädda in formler och producera ett användbart kalkylblad.

![Skärmdump av den genererade Excel-arbetsboken som visar den expanderade arrayen och cotangensresultatet](/images/create-excel-workbook-csharp.png "exempel på skapa excel-arbetsbok c#")

*Bildtext: skapa excel-arbetsbok c# – vy av det ifyllda kalkylbladet.*

## Steg 6: Valfritt – Auto‑Fit kolumner för ett polerat utseende

Om du planerar att distribuera filen till slutanvändare, ger en snabb auto‑fit den ett professionellt utseende.

```csharp
// Optional: Auto‑fit all columns in the used range
ws.AutoFitColumns(0, ws.Cells.MaxColumn);
```

Denna rad loopar igenom varje kolumn som innehåller data och justerar dess bredd till det längsta värdet. Det är en liten detalj, men den förhindrar den fruktade “…###”‑översvämningen när siffror är bredare än standardkolumnbredden.

## Steg 7: Sammanfattning och nästa steg

Grattis—du har precis bemästrat hur man **skapar excel-arbetsbok c#** från grunden och lärt dig hur man **använder EXPAND-funktionen i Excel** för att generera dynamiska arrayer. Koden är avsiktligt minimal så att du kan kopiera‑klistra in den i vilket projekt som helst, men koncepten kan skalas:

- **Dynamiska datakällor:** Ersätt `SEQUENCE(3)` med en referens till ett annat område eller en namngiven tabell.
- **Villkorsstyrd formatering:** Använd `ws.Cells["A1:E5"].Style` för att lägga till färger baserat på värden.
- **Diagram och grafik:** Aspose.Cells kan bädda in diagram, bilder och även pivottabeller.

Känn dig fri att experimentera—byt ut `EXPAND`‑dimensionerna, prova `FILTER` eller `SORT`, eller kedja flera formler tillsammans. Biblioteket hanterar allt utan att du någonsin behöver röra det lågnivå OpenXML‑formatet.

---

### Vanliga frågor

**Q: Fungerar detta med .NET Framework 4.8?**  
A: Absolut. Aspose.Cells riktar sig mot .NET Standard 2.0, vilket är kompatibelt med både .NET Core och det klassiska Frameworket.

**Q: Vad händer om jag behöver skydda bladet?**  
A: Använd `ws.Protect(ProtectionType.All, "yourPassword");` innan du sparar.

**Q: Kan jag skriva arbetsboken direkt till en `MemoryStream`?**  
A: Ja—`workbook.Save(stream, SaveFormat.Xlsx);` är praktiskt för webb‑API:er som returnerar filen som en nedladdning.

## TL;DR

Vi byggde en **komplett C#‑konsolapp** som:

1. **Skapar en Excel-arbetsbok C#** med Aspose.Cells.  
2. **Använder EXPAND‑funktionen i Excel** för att omvandla en 3‑raders array till ett 5 × 5‑block.  
3. Lägger till en cotangensformel (`COT(PI()/4)`).  
4. Sparar filen och auto‑fit:ar kolumnerna valfritt.

Du har nu en solid grund för alla automatiseringsuppgifter som innebär att generera Excel‑filer från .NET. Lycka till med kodningen, och må dina kalkylblad alltid vara felfria!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man skapar arbetsboks‑specifika namngivna områden i Excel med Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [Hur man skapar och använder union‑områden i Excel med Aspose.Cells .NET (C#‑guide)](/cells/english/net/range-management/excel-union-range-aspose-cells-net/)
- [Skapa Excel‑arbetsbok med diagram med Aspose.Cells .NET | Steg‑för‑steg‑guide](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}