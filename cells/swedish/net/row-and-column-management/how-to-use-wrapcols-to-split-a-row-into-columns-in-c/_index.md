---
category: general
date: 2026-11-16
description: Lär dig hur du använder WRAPCOLS i C# för att dela en rad i kolumner,
  automatisera en Excel-arbetsbok, beräkna formler och spara Excel-filen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split row into columns
- automate excel workbook
- excel formula calculation
- save excel file c#
language: sv
lastmod: 2026-11-16
og_description: Hur man använder WRAPCOLS i C# för att dela upp en rad i kolumner,
  automatisera en Excel-arbetsbok, köra formelberäkning och spara Excel-filen.
og_image_alt: Screenshot showing WRAPCOLS function splitting a row into columns in
  an Excel workbook
og_title: Hur man använder WRAPCOLS i C# – dela rader, beräkna formler och spara Excel-filer
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  headline: How to use WRAPCOLS to split a row into columns in C#
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  name: How to use WRAPCOLS to split a row into columns in C#
  steps:
  - name: How WRAPCOLS works
    text: '* **Source range** – `A1:T1` contains the original 20 values. * **Column
      count** – `5` tells Excel to create five columns per row. * **Result** – Excel
      fills cells `A2:E5` with the wrapped data automatically.'
  - name: Expected output
    text: 'Open `WrapColsDemo.xlsx` and you’ll see:'
  - name: Next steps
    text: '* Explore other dynamic array functions such as `SEQUENCE`, `FILTER`, and
      `UNIQUE` to enrich your Excel automation toolkit. * Combine `WRAPCOLS` with
      chart generation APIs to produce ready‑to‑publish reports. * Integrate the code
      into a background service that processes CSV uploads and outputs resha'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
title: Hur man använder WRAPCOLS för att dela upp en rad i kolumner i C#
url: /sv/net/row-and-column-management/how-to-use-wrapcols-to-split-a-row-into-columns-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder WRAPCOLS för att dela upp en rad i kolumner i C#

Om du behöver **how to use WRAPCOLS** i ett C#-projekt, visar den här guiden en komplett, körbar lösning. Du kommer att se hur du delar upp en rad i kolumner, automatiserar en Excel-arbetsbok, triggar beräkning av Excel-formler och slutligen sparar Excel-filen på C#‑sätt.

Att arbeta med Excel programmässigt innebär ofta hantering av stora datamängder, och `WRAPCOLS`‑funktionen låter dig omforma en enda rad till en matris utan manuella loopar. Stegen nedan täcker allt du behöver – från skapande av arbetsbok till slutlig filutmatning – så att du kan integrera tekniken i vilken .NET‑applikation som helst.

## Vad den här handledningen täcker

* Skapa en ny arbetsbok och komma åt dess första kalkylblad.  
* Fyll en rad med sekventiella värden (1‑20).  
* Applicera `WRAPCOLS`‑Excel‑formeln för att dela upp raden i 5‑kolumnsblock.  
* Kör **excel formula calculation** så att resultatet blir en del av bladet.  
* Använd **save excel file c#** för att skriva arbetsboken till disk.  

Ingen extern konfiguration krävs utöver Aspose.Cells för .NET‑biblioteket (eller något kompatibelt API som stödjer `WRAPCOLS`). I slutet av guiden har du en fil med namnet `WrapColsDemo.xlsx` som innehåller fyra rader med fem kolumner vardera, hämtade från den ursprungliga enkla raden.

## Förutsättningar

* .NET 6.0 eller senare (koden fungerar även med .NET Core 3.1 och .NET Framework 4.7+).  
* En referens till **Aspose.Cells** (tillgänglig via NuGet: `Install-Package Aspose.Cells`).  
* Grundläggande kunskap om C#‑syntax och Excel‑formler.  

> **Pro tip:** Om du föredrar ett gratisalternativ stödjer det öppna källkods‑biblioteket EPPlus också anpassade formler, men `WRAPCOLS` är inbyggt endast i bibliotek som implementerar hela Excel‑beräkningsmotorn, såsom Aspose.Cells.

## Steg 1: Skapa en ny arbetsbok och hämta det första kalkylbladet

Den första operationen är att instansiera ett `Workbook`‑objekt och hämta dess standardkalkylblad. Detta objekt representerar hela Excel‑filen i minnet.

```csharp
using Aspose.Cells;

...

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                 // creates an empty workbook
Worksheet sheet = workbook.Worksheets[0];           // the first worksheet (named "Sheet1")
```

Att skapa arbetsboken programmässigt är grunden för **automate excel workbook**‑uppgifter. `Worksheet`‑referensen låter dig manipulera celler direkt.

## Steg 2: Fyll den första raden med värden 1‑20

Nästa steg, fyll cellerna `A1` till `T1` med siffrorna 1 till 20. En enkel `for`‑loop skriver varje värde till rätt kolumnindex.

```csharp
// Step 2: Fill the first row with values 1‑20
for (int col = 0; col < 20; col++)
{
    sheet.Cells[0, col].PutValue(col + 1);   // Row 0 = first row, column index starts at 0
}
```

Varför skriva värdena programmässigt? Det garanterar att demonstrationen fungerar på vilken maskin som helst utan manuell datainmatning, vilket är avgörande när du **automate excel workbook**‑generering i batch‑processer.

## Steg 3: Använd WRAPCOLS‑funktionen för att dela upp raden i 5‑kolumnsblock

Nu använder vi Excel‑formeln `WRAPCOLS`. Den tar ett källintervall och ett kolumnantal, och returnerar en tvådimensionell array som “wrappar” källdata i det angivna antalet kolumner.

```csharp
// Step 3: Use the WRAPCOLS function to split the row into 5‑column blocks
sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";
```

Att placera formeln i cell `A2` talar om för Excel att börja utskriften på den andra raden. Resultatet blir en 4 × 5‑matris eftersom 20 objekt delat på 5 kolumner ger fyra rader.

### Så fungerar WRAPCOLS

- **Källintervall** – `A1:T1` innehåller de ursprungliga 20 värdena.  
- **Kolumnantal** – `5` talar om för Excel att skapa fem kolumner per rad.  
- **Resultat** – Excel fyller cellerna `A2:E5` med den omslagna datan automatiskt.  

Om du någonsin behöver **split row into columns** med en annan blockstorlek, ändra helt enkelt det andra argumentet. Till exempel skulle `WRAPCOLS(A1:T1,4)` producera fem rader med fyra kolumner vardera.

## Steg 4: Beräkna formler så att WRAPCOLS‑resultatet materialiseras

En nyinlagd formel förblir oevaluerad tills beräkningsmotorn körs. Genom att anropa `CalculateFormula()` säkerställer du att steget **excel formula calculation** skriver de faktiska värdena till kalkylbladet.

```csharp
// Step 4: Calculate formulas so the WRAPCOLS result is materialised
workbook.CalculateFormula();
```

Att köra beräkningen är avgörande när du senare **save excel file c#**, eftersom den sparade filen måste innehålla de beräknade värdena, inte bara formeltexten. Utan detta steg skulle den exporterade arbetsboken visa `#N/A` eller den råa formeln istället för de förväntade siffrorna.

## Steg 5: Spara arbetsboken till disk

Till sist, spara arbetsboken med `Save`‑metoden. Du kan ange vilken giltig filsökväg som helst; exemplet använder en platshållarkatalog som du bör ersätta med din egen.

```csharp
// Step 5: Save the workbook
string outputPath = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "WrapColsDemo.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

`Save`‑anropet demonstrerar **save excel file c#** i dess enklaste form. Aspose.Cells väljer automatiskt XLSX‑formatet baserat på filändelsen. Om du behöver en äldre `.xls`‑fil, ändra filändelsen därefter.

### Förväntad utdata

Open `WrapColsDemo.xlsx` and you’ll see:

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 2 | 3 | 4 | 5 |
| 6 | 7 | 8 | 9 |10 |
|11 |12 |13 |14 |15 |
|16 |17 |18 |19 |20 |

Den ursprungliga enkla raden har **split row into columns** över fyra rader, var och en med fem kolumner.

## Fullständig källkod

Att sätta ihop alla steg ger ett kompakt, självständigt program:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class WrapColsDemo
{
    static void Main()
    {
        // Step 1: Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Step 2: Fill first row with values 1‑20
        for (int col = 0; col < 20; col++)
        {
            sheet.Cells[0, col].PutValue(col + 1);
        }

        // Step 3: Apply WRAPCOLS to split into 5‑column blocks
        sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";

        // Step 4: Force calculation so values are materialised
        workbook.CalculateFormula();

        // Step 5: Save the workbook (change the path as needed)
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "WrapColsDemo.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Kopiera koden till ett nytt konsolprojekt, återställ Aspose.Cells‑NuGet‑paketet och kör. Programmet skapar Excel‑filen på ditt skrivbord på några sekunder.

## Vanliga variationer och kantfall

| Situation | Adjustment |
|-----------|------------|
| **Olika blockstorlek** | Ändra `WRAPCOLS(A1:T1,5)` till `WRAPCOLS(A1:T1, n)` där `n` är önskat kolumnantal. |
| **Flera källrader** | Använd `WRAPCOLS(A1:A10,5)` för att omsluta ett vertikalt intervall till en 5‑kolumnsmatris. |
| **Dynamiskt källintervall** | Bygg adresssträngen i C# (`$"A1:{CellIndexToName(0, lastCol)}1"`) innan du tilldelar formeln. |
| **Stora kalkylblad** | Anropa `workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)` för att hoppa över celler som orsakar fel och förbättra prestanda. |
| **Spara som CSV** | Ersätt `workbook.Save(outputPath)` med `workbook.Save(outputPath, SaveFormat.Csv)`. |

Dessa variationer visar att samma **how to use wrapcols**‑mönster kan anpassas för många data‑omformningsscenarier.

## Felsökningstips

* **Formel ej utvärderad** – Se till att du anropar `workbook.CalculateFormula()` *efter* att ha satt formeln. Att hoppa över detta steg lämnar cellen med den råa `WRAPCOLS`‑texten.  
* **Filåtkomst nekad** – Verifiera att målkatalogen finns och att din process har skrivbehörighet. Att använda `Environment.SpecialFolder.Desktop` undviker de flesta behörighetsproblem.  
* **Fel antal rader** – Dubbelkolla det andra argumentet i `WRAPCOLS`. Det definierar kolumnantalet, inte radantalet; raderna härleds från det totala antalet källceller delat med det kolumnantalet.  

## Slutsats

Du vet nu **how to use WRAPCOLS** i C# för att **split row into columns**, fullt **automate excel workbook**‑skapande, köra **excel formula calculation**, och **save excel file c#** med en enda, ren kodbas. Denna teknik eliminerar manuella kopiera‑och‑klistra‑operationer och skalar utan ansträngning för stora datatransformations‑pipelines.

### Nästa steg

* Utforska andra dynamiska matrisfunktioner såsom `SEQUENCE`, `FILTER` och `UNIQUE` för att berika ditt Excel‑automatiseringsverktyg.  
* Kombinera `WRAPCOLS` med API:er för diagramgenerering för att producera färdiga rapporter.  
* Integrera koden i en bakgrundstjänst som bearbetar CSV‑uppladdningar och genererar omformade Excel‑filer för efterföljande analys.  

Känn dig fri att experimentera med olika källintervall och kolumnantal – justera formeln, kör beräkningen igen, och se arbetsboken uppdateras omedelbart. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [hur man använder wrapcols i C# – Fullständig guide med Excel WRAPROWS & omberäkning av formler](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [Hur man använder WRAPCOLS – Komplett guide för C# Excel‑automatisering](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)
- [Hur man använder WRAPCOLS i C# – Omforma en array till en matris i Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}