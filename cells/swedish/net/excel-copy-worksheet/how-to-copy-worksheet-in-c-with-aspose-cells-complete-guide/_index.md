---
category: general
date: 2026-03-30
description: Så här kopierar du ett kalkylblad i C# med Aspose.Cells – steg‑för‑steg‑guide
  som täcker kopiering av cellområde, kopiering av kolumner mellan blad, kopiering
  av pivottabell i kalkylbladet och kod för att lägga till ett nytt kalkylblad.
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: sv
og_description: Lär dig hur du kopierar kalkylblad i C# med Aspose.Cells. Den här
  guiden visar hur du kopierar cellområde, bevarar pivottabeller, kopierar kolumner
  mellan blad och lägger till kod för ett nytt kalkylblad.
og_title: Hur man kopierar kalkylblad i C# – Fullständig Aspose.Cells-handledning
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Hur man kopierar kalkylblad i C# med Aspose.Cells – Komplett guide
url: /sv/net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man kopierar arbetsblad i C# med Aspose.Cells – Komplett guide

Har du någonsin undrat **how to copy worksheet** i C# utan att förlora en enda pivottabell eller formel? Du är inte ensam—många utvecklare stöter på problem när de måste duplicera ett blad samtidigt som alla funktioner behålls. I den här handledningen går vi igenom en praktisk, end‑to‑end‑lösning som inte bara kopierar data utan också bevarar **copy worksheet pivot table**, hanterar **copy cell range**, och visar den **add new worksheet code** du behöver.

Vi kommer att gå igenom allt från att ladda källarboken till att spara destinationsfilen, så att du kan **copy columns between sheets**, bevara objekt och hålla din kod ren. Inga vaga referenser, bara ett komplett, körbart exempel som du kan lägga in i ditt projekt idag.

## Vad den här handledningen täcker

- Laddar en befintlig Excel-fil med Aspose.Cells  
- Använder **add new worksheet code** för att skapa ett målblad  
- Definierar ett **copy cell range** som inkluderar en pivottabell  
- Ställer in **CopyOptions** för att behålla diagram, formler och pivottabeller intakta  
- Utför **copy columns between sheets** med rad‑vis precision  
- Sparar resultatet och verifierar att arbetsbladet kopierades korrekt  

I slutet av den här guiden kommer du kunna svara på frågan “how to copy worksheet” med självförtroende, oavsett om du automatiserar rapporter eller bygger ett kalkylblads‑drivet UI.

## Så kopierar du arbetsblad – Översikt

Innan vi dyker ner i koden, låt oss beskriva den övergripande flödet. Tänk på det som ett recept:

1. **Load** källarboken (`Source.xlsx`).  
2. **Add** ett nytt arbetsblad för att hålla kopian (`add new worksheet code`).  
3. **Define** området du vill duplicera (`copy cell range`).  
4. **Configure** kopieringsalternativen så att pivottabellen överlever (`copy worksheet pivot table`).  
5. **Copy** rader och kolumner (`copy columns between sheets`).  
6. **Save** den nya arbetsboken (`Destination.xlsx`).  

Det är allt—sex steg, ingen magi. Varje steg förklaras nedan med kodsnuttar och resonemanget bakom.

## Steg 1 – Ladda källarboken

Först och främst: du behöver en `Workbook`‑instans som pekar på filen du vill duplicera. Detta steg är avgörande eftersom Aspose.Cells arbetar direkt med filsystemet, inte med Office‑gränssnittet.

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*Varför detta är viktigt:* Att ladda filen skapar en minnesrepresentation av varje blad, cell och objekt. Utan detta finns det inget att kopiera, och varje försök att `add new worksheet code` senare skulle misslyckas eftersom källdata saknas.

## Steg 2 – Lägg till ett nytt arbetsblad (add new worksheet code)

Nu behöver vi en plats att klistra in de kopierade data. Det är här **add new worksheet code** kommer till sin rätt. Du kan namnge bladet hur du vill; här kallar vi det `"Copy"`.

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*Proffstips:* Om du planerar att kopiera flera blad, anropa `Worksheets.Add` i en loop och ge varje blad ett unikt namn. På så sätt undviker du namnkonflikter och håller din arbetsbok prydlig.

## Steg 3 – Definiera copy cell range

Ett **copy cell range** talar om för Aspose.Cells exakt vilka rader och kolumner som ska dupliceras. I många verkliga scenarier inkluderar området en pivottabell, så vi måste vara precisa.

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*Varför vi behöver detta:* Genom att uttryckligen ange området undviker du att kopiera hela bladet (vilket kan vara slöseri) och du garanterar att pivottabellen finns inom det kopierade området. Detta är kärnan i **how to copy worksheet** när du bara behöver en del av bladet.

## Steg 4 – Ställ in CopyOptions (bevara copy worksheet pivot table)

Aspose.Cells erbjuder ett `CopyOptions`‑objekt som styr vad som klistras in. För att behålla pivottabellen, diagram och formler, sätter vi `PasteType.All` och aktiverar `PasteSpecial`.

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*Förklaring:* `PasteType.All` är det mest omfattande alternativet, medan `PasteSpecial` instruerar motorn att hantera komplexa objekt—som pivottabeller—på rätt sätt. Att hoppa över detta steg är en vanlig fallgrop; det kopierade bladet skulle förlora sina interaktiva funktioner.

## Steg 5 – Kopiera rader och kolumner (copy columns between sheets)

Nu kommer det tunga arbetet: att faktiskt flytta data. Vi använder `CopyRows` och `CopyColumns` för att hantera **copy columns between sheets**. Att göra båda säkerställer att sammanslagna celler och kolumnbredder bevaras.

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*Vad som händer:* `CopyRows` flyttar data rad för rad, medan `CopyColumns` gör samma sak kolumn för kolumn. Att köra båda garanterar att hela det rektangulära blocket dupliceras, vilket är avgörande när du behöver **copy columns between sheets** som har olika kolumnbredder eller dolda kolumner.

## Steg 6 – Spara arbetsboken

Till sist, skriv tillbaka ändringarna till disk. Detta steg slutför processen **how to copy worksheet**.

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*Verifieringstips:* Öppna `Destination.xlsx` och kontrollera att bladet `"Copy"` ser identiskt ut som originalet, pivottabellerna fungerar och kolumnbredderna matchar. Om något ser fel ut, gå tillbaka till `CopyOptions`‑inställningarna.

## Edge Cases & vanliga variationer

### Kopiera flera arbetsblad

Om du behöver duplicera flera blad, omslut logiken ovan i en `foreach`‑loop:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### Bevara formler mellan olika arbetsböcker

När käll- och destinationsarbetsböcker har olika namngivna områden, sätt `copyOptions` till `PasteType.Formulas` utöver `All`:

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### Stora områden och prestanda

För enorma dataset (hundratusentals rader), överväg att bara använda `CopyRows` och hoppa över `CopyColumns` om kolumnbredder inte är kritiska. Detta kan spara några sekunder.

## Fullständigt fungerande exempel

Nedan är det kompletta, färdiga programmet som innehåller allt vi har diskuterat. Klistra in det i en konsolapp, justera filsökvägarna och tryck på **F5**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**Förväntat resultat:** När du öppnar `Destination.xlsx` visas ett blad med namnet **Copy** som speglar det första bladet i `Source.xlsx`—inklusive eventuella pivottabeller, formatering och kolumnbredder. Originalfilen förblir orörd.

## Vanliga frågor

**Q: Fungerar detta med .xlsx‑filer skapade av Excel 2019?**  
A: Absolut. Aspose.Cells stöder alla moderna Excel‑format, så samma kod fungerar för `.xlsx`, `.xlsm` och även äldre `.xls`‑filer

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}