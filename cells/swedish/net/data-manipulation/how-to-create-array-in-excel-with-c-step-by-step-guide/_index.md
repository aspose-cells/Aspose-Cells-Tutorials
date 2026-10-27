---
category: general
date: 2026-02-09
description: Hur man skapar en array i Excel med C# förklarat på några minuter – lär
  dig att generera sekvensnummer, använda COT och spara arbetsboken som XLSX.
draft: false
keywords:
- how to create array
- create excel workbook c#
- generate sequence numbers
- save workbook as xlsx
- how to use cot
language: sv
og_description: Hur man skapar en array i Excel med C# behandlas steg för steg, inklusive
  att generera sekvensnummer, använda COT och spara arbetsboken som XLSX.
og_title: Hur du skapar en array i Excel med C# – Snabbguide
tags:
- C#
- Excel
- Aspose.Cells
title: Hur man skapar en array i Excel med C# – Steg‑för‑steg‑guide
url: /sv/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar en array i Excel med C# – Steg‑för‑steg‑guide

Har du någonsin funderat **hur man skapar en array** i Excel med C# utan att spendera timmar på att gräva i dokumentationen? Du är inte ensam. Många utvecklare fastnar när de behöver ett dynamiskt spill‑område, ett snabbt trigonometriskt värde eller helt enkelt en ren XLSX‑fil sparad på disk. I den här handledningen löser vi problemet direkt – genom att bygga en liten arbetsbok som skriver en expanderande array‑formel, stoppar in en cotangens‑beräkning och sparar allt som en XLSX‑fil.  

Vi strör också in några extra knep: generera sekvensnummer, bemästra `COT`‑funktionen och se till att filen hamnar där du vill. I slutet har du ett återanvändbart kodstycke som du kan slänga in i vilket .NET‑projekt som helst. Inga onödiga utsvävningar, bara kod som fungerar.

> **Proffstips:** Exemplet använder det populära **Aspose.Cells**‑biblioteket, men koncepten kan överföras till andra Excel‑automatiseringspaket (EPPlus, ClosedXML) med bara små ändringar.

---

## Vad du behöver

- **.NET 6** eller senare (koden kompileras även på .NET Framework 4.7+)  
- **Aspose.Cells för .NET** – du kan hämta det från NuGet (`Install-Package Aspose.Cells`)  
- En textredigerare eller IDE (Visual Studio, Rider, VS Code…)  
- Skrivbehörighet till en mapp där utdatafilen ska sparas  

Det är allt—ingen extra konfiguration, ingen COM‑interop, bara en ren hanterad assembly.

---

## Steg 1: Hur man skapar en array i Excel – Initiera arbetsboken

Det allra första du måste göra när du vill **hur man skapar en array** i ett Excel‑blad är att skapa ett workbook‑objekt. Tänk på arbetsboken som en tom duk; arbetsbladet är där du målar dina formler.

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // <- fresh workbook
        Worksheet worksheet = workbook.Worksheets[0];    // first (and only) sheet

        // The rest of the steps follow...
```

Varför använda `Workbook()` utan parametrar? Det ger dig en arbetsbok i minnet med ett standardsheet, vilket är perfekt för snabba, programatiska uppgifter. Om du behöver öppna en befintlig fil, skicka bara filvägen till konstruktorn.

---

## Steg 2: Generera sekvensnummer med EXPAND och SEQUENCE

Nu när vi har ett blad, låt oss besvara delen **generera sekvensnummer** i pusslet. Excels nya dynamiska array‑funktioner (`SEQUENCE`, `EXPAND`) låter oss skapa en vertikal lista med 3 rader och automatiskt spilla den i ett 3 × 5‑område.

```csharp
        // Write a dynamic array formula that expands a 3‑row sequence into a 3×5 spill range
        // EXPAND pads the result to 5 columns, SEQUENCE generates numbers 1‑3 vertically
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

**Vad händer här?**  
- `SEQUENCE(3,1,1,1)` → producerar en vertikal array `{1;2;3}`.  
- `EXPAND(...,5,1)` → tar den tre‑rader‑kolumnen och sträcker den till fem kolumner, fyller de extra cellerna med tomma värden.  

När du öppnar den resulterande `output.xlsx` ser du ett 3 × 5‑block som börjar i **A1** där den första kolumnen innehåller 1, 2, 3 och de återstående fyra kolumnerna är tomma. Denna teknik är ryggraden i **hur man skapar en array**‑liknande spill‑områden utan att manuellt skriva varje cell.

---

## Steg 3: Hur man använder COT – Lägga till en trigonometrisk formel

Om du också är nyfiken på **hur man använder cot** i en Excel‑formel, är `COT`‑funktionen ett praktiskt sätt att få cotangenten av en vinkel uttryckt i radianer. Låt oss beräkna `cot(π/4)`, vilket bör ge **1**.

```csharp
        // Write a simple trigonometric formula that calculates cotangent of 45° (π/4)
        // COT(π/4) evaluates to 1
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

Observera att vi använde `PI()` för att få radianvärdet för 180°, och sedan delade med 4 för att nå 45°. Excel gör det tunga lyftet, och cell **B1** kommer visa `1` när arbetsboken öppnas. Detta demonstrerar **hur man använder cot** för snabba ingenjörs‑ eller finansberäkningar utan att behöva ett separat matematikbibliotek.

---

## Steg 4: Spara arbetsbok som XLSX – Persistera filen

Allt det roliga med att skapa en array och infoga formler är bortkastat om du aldrig skriver filen till disk. Här är det enkla sättet att **spara arbetsbok som xlsx** med Aspose.Cells:

```csharp
        // Save the workbook to verify the formulas (optional)
        string outputPath = @"C:\Temp\output.xlsx";   // adjust to your folder
        workbook.Save(outputPath, SaveFormat.Xlsx);

        // Let the user know we’re done
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Varför specificera `SaveFormat.Xlsx`? Det garanterar det moderna OpenXML‑formatet, som är universellt läsbart (Excel, LibreOffice, Google Sheets). Om du behöver en äldre `.xls`‑fil, byt bara ut enum‑värdet.

---

## Fullt fungerande exempel (Alla steg kombinerade)

Nedan är det kompletta, körklara programmet. Kopiera‑klistra in det i ett konsolprojekt, återställ Aspose.Cells‑NuGet‑paketet och tryck **F5**.

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Create a dynamic spill range (how to create array)
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";

        // Step 3: Calculate cotangent (how to use cot)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";

        // Step 4: Persist the file (save workbook as xlsx)
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Förväntat resultat** efter att du öppnat `output.xlsx`:

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 |   |   |   |
| 2 |   |   |   |   |
| 3 |   |   |   |   |

- Kolumn A visar siffrorna 1‑3 som genererats av `SEQUENCE`.  
- Kolumn B innehåller värdet **1** från `COT`‑formeln.  
- Kolumnerna C‑E är tomma, vilket illustrerar utfyllnadseffekten av `EXPAND`.

---

## Vanliga frågor & kantfall

### Vad händer om jag behöver fler rader eller kolumner?

Justera bara argumenten i `SEQUENCE` och `EXPAND`.  
- `SEQUENCE(10,2,5,2)` skulle ge en 10‑rad × 2‑kolumn‑matris som startar på 5 och ökar med 2.  
- `EXPAND(...,10,5)` skulle paddra resultatet till 10 kolumner och 5 rader.

### Fungerar detta med äldre Excel‑versioner?

Dynamiska array‑funktioner (`SEQUENCE`, `EXPAND`) kräver Excel 365 eller 2019+. För äldre filer kan du falla tillbaka på klassiska formler eller skriva värden direkt via `Cells[row, col].PutValue(value)`.

### Kan jag skriva formeln i R1C1‑stil?

Absolut. Byt ut `A1` mot `Cells[0, 0]` och använd egenskapen `FormulaR1C1`:

```csharp
worksheet.Cells[0, 0].FormulaR1C1 = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

### Vad händer med kulturspecifika decimalavgränsare?

Aspose.Cells respekterar arbetsbokens locale. Om du behöver en specifik kultur, sätt `workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");` innan du skriver formler.

---

## Visuell sammanfattning

![hur man skapar array i Excel med C#](/images/how-to-create-array-excel-csharp.png "hur man skapar array i Excel med C#")

*Skärmbilden visar det slutgiltiga spill‑området och cotangensresultatet.*

---

## Slutsats

Där har du det—**hur man skapar en array** i Excel med C# från grunden, generera sekvensnummer, utnyttja `COT`‑funktionen och **spara arbetsbok som XLSX** i ett enda, prydligt program. De viktigaste lärdomarna är:

1. Använd `Workbook` och `Worksheet`‑objekt för att starta din Excel‑automation.  
2. Utnyttja dynamiska array‑funktioner (`SEQUENCE`, `EXPAND`) för flexibla spill‑områden.  
3. Lägg in trigonometriska funktioner som `COT` för snabb matematik utan extra bibliotek.  
4. Persistera resultatet med `SaveFormat.Xlsx` för att få en universellt läsbar fil.

Redo för nästa steg? Prova att byta ut `COT(PI()/4)`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}