---
category: general
date: 2026-10-26
description: Lär dig hur du använder WRAPCOLS i C# för att dela upp ett område i kolumner,
  tillämpa WRAPROWS för rader och spara arbetsboken som XLSX programatiskt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split range into rows
- excel wrapcols example
- save workbook as xlsx
- create excel workbook programmatically
language: sv
lastmod: 2026-10-26
og_description: Hur man använder WRAPCOLS i C# för att dela upp data i kolumner, använder
  WRAPROWS för rader och sparar arbetsboken som XLSX. Följ den kompletta steg‑för‑steg‑guiden.
og_image_alt: Screenshot illustrating how to use WRAPCOLS to split a range into columns
  in Excel
og_title: Hur man använder WRAPCOLS i C# – dela upp intervall och spara som XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  headline: How to use WRAPCOLS in C# and save workbook as XLSX
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  name: How to use WRAPCOLS in C# and save workbook as XLSX
  steps:
  - name: What the saved file looks like
    text: 'When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:'
  - name: Changing the number of columns or rows
    text: '* **More columns:** Increase the second argument of `WRAPCOLS`. Example:
      `=WRAPCOLS(A1:A10,5)` creates five columns, leaving empty cells where data runs
      out. * **Dynamic column count:** Use a cell reference instead of a hard‑coded
      number. `=WRAPCOLS(A1:A10, G1)` where `G1` holds the desired column c'
  - name: Handling empty or non‑numeric cells
    text: WRAPCOLS and WRAPROWS ignore empty cells by default, but they preserve the
      order of non‑empty values. If you need to preserve blanks, wrap the source range
      with `IFERROR` or `TEXT` functions before applying WRAPCOLS.
  - name: Saving to other formats
    text: 'While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells
      supports many formats (`.xls`, `.csv`, `.pdf`, etc.):'
  - name: What’s next?
    text: '* Explore **conditional formatting** to highlight the spilled data. * Combine
      **WRAPCOLS** with **SORT** or **FILTER** for dynamic dashboards. * Use Aspose.Cells’
      **charting API** to visualize the rearranged data directly from code.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hur man använder WRAPCOLS i C# och sparar arbetsboken som XLSX
url: /sv/net/row-and-column-management/how-to-use-wrapcols-in-c-and-save-workbook-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder WRAPCOLS i C# och sparar arbetsbok som XLSX

Om du behöver **how to use WRAPCOLS** för att omorganisera data i en Excel-fil, visar den här guiden en komplett, körbar lösning. Du kommer att se ett **excel wrapcols example**, lära dig hur du **split range into rows** med WRAPROWS, och avsluta med **save workbook as XLSX**—allt gjort **programmatically**.

Att arbeta med Excel från C# innebär ofta att skapa en arbetsbok, tillämpa formler och spara filen. Koden nedan använder Aspose.Cells-biblioteket, som låter dig manipulera Excel-filer utan att behöva Microsoft Office installerat. I slutet av den här handledningen kommer du att kunna **create excel workbook programmatically**, dela data både horisontellt och vertikalt, och producera en ren `.xlsx`-fil klar för vidare bearbetning.

## Förutsättningar

* .NET 6.0 eller senare (koden fungerar också med .NET Framework 4.7+)
* En referens till **Aspose.Cells** NuGet-paketet  
  ```bash
  dotnet add package Aspose.Cells
  ```
* Grundläggande kunskap om C# och Excel-formler

## Steg 1: Hur man använder WRAPCOLS för att dela ett område i kolumner

Funktionen **WRAPCOLS** tar ett endimensionellt område och sprider dess värden över det angivna antalet kolumner. I det här exemplet börjar vi med värden i `A1:A10` och ber WRAPCOLS att skapa tre kolumner.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is the “create excel workbook programmatically” step
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Populate source data for demonstration
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 0].PutValue($"Item {i + 1}");
        }

        // Apply WRAPCOLS: split A1:A10 into 3 columns starting at C1
        // The formula is entered in cell C1 (row 0, column 2)
        ws.Cells[0, 2].Formula = "=WRAPCOLS(A1:A10,3)";

        // -------------------------------------------------
        // Why this works:
        // -------------------------------------------------
        // * WRAPCOLS reads the source range (A1:A10) vertically.
        // * The second argument (3) tells Excel to create three columns.
        // * The function returns a 2‑dimensional array that Excel spills into the
        //   surrounding cells automatically.
        // -------------------------------------------------
```

> **Resultat:** Cellerna `C1:E4` innehåller nu de ursprungliga tio objekten ordnade i tre kolumner (den sista kolumnen innehåller de återstående objekten).

![Skärmbild som visar hur man använder WRAPCOLS för att dela ett område i kolumner i Excel](image-url.png)

## Steg 2: Dela område i rader med WRAPROWS

Medan **WRAPCOLS** fungerar horisontellt, utför **WRAPROWS** det motsatta: den sprider ett område över ett givet antal rader. Här tar vi värden från `B1:B10` och ordnar dem i två rader med start i `F1`.

```csharp
        // Populate a second source column for WRAPROWS
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 1].PutValue($"Value {i + 1}");
        }

        // Apply WRAPROWS: split B1:B10 into 2 rows starting at F1
        ws.Cells[0, 5].Formula = "=WRAPROWS(B1:B10,2)";

        // -------------------------------------------------
        // Why WRAPROWS is useful:
        // -------------------------------------------------
        // * It converts a vertical list into a matrix with the specified row count.
        // * Handy when you need to prepare data for pivot tables, charts, or
        //   reporting layouts that expect a horizontal orientation.
        // -------------------------------------------------
```

> **Resultat:** Formeln fyller cellerna `F1:K2` med de tio värdena fördelade över två rader.

## Steg 3: Spara arbetsbok som XLSX

Efter att ha tillämpat formlerna är sista steget att spara filen. Operationen **save workbook as xlsx** skriver den minnesbaserade arbetsboken till disk i det moderna OpenXML-formatet.

```csharp
        // Save the workbook – this completes the “save workbook as xlsx” step
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "wrapcols_wraprows_output.xlsx");

        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Så ser den sparade filen ut

När du öppnar `wrapcols_wraprows_output.xlsx` i Excel kommer du att se:

| C | D | E |
|---|---|---|
| Item 1 | Item 4 | Item 7 |
| Item 2 | Item 5 | Item 8 |
| Item 3 | Item 6 | Item 9 |
|        |        | Item 10 |

and

| F | G | H | I | J | K |
|---|---|---|---|---|---|
| Value 1 | Value 3 | Value 5 | Value 7 | Value 9 | |
| Value 2 | Value 4 | Value 6 | Value 8 | Value 10 | |

Formlerna finns kvar i cellerna, så eventuella senare ändringar i källområdena återspeglas automatiskt.

## Steg 4: Vanliga variationer och kantfall

### Ändra antalet kolumner eller rader

* **Fler kolumner:** Öka det andra argumentet i `WRAPCOLS`.  
  Exempel: `=WRAPCOLS(A1:A10,5)` skapar fem kolumner och lämnar tomma celler där data tar slut.
* **Dynamiskt kolumnantal:** Använd en cellreferens istället för ett hårdkodat tal.  
  `=WRAPCOLS(A1:A10, G1)` där `G1` innehåller önskat kolumnantal.

### Hantera tomma eller icke‑numeriska celler

WRAPCOLS och WRAPROWS ignorerar tomma celler som standard, men de bevarar ordningen på icke‑tomma värden. Om du behöver bevara tomma celler, omslut källområdet med `IFERROR`‑ eller `TEXT`‑funktioner innan du använder WRAPCOLS.

### Spara till andra format

Även om den här handledningen fokuserar på **save workbook as xlsx**, stöder Aspose.Cells många format (`.xls`, `.csv`, `.pdf`, etc.):

```csharp
workbook.Save("output.pdf", SaveFormat.Pdf);   // Export to PDF
workbook.Save("output.csv", SaveFormat.Csv);   // Export to CSV
```

## Pro‑tips och fallgropar

* **Pro tip:** Sätt `Workbook.Settings.CalcEngineEnabled = true` om du planerar att utvärdera formler omedelbart efter sparning.
* **Se upp för:** Stora källområden kan skapa mycket stora spill‑områden, vilket kan påverka prestandan. Begränsa områdesstorleken eller dela upp operationen i flera arbetsblad.
* **Trådsäkerhet:** Aspose.Cells‑objekt är **inte** trådsäkra. Skapa en separat `Workbook`‑instans per tråd om du bearbetar filer parallellt.

## Slutsats

Du vet nu **how to use WRAPCOLS** för att dela ett vertikalt område i flera kolumner, hur du **split range into rows** med WRAPROWS, och hur du **save workbook as XLSX** efter att ha utfört dessa transformationer. Genom att följa stegen ovan kan du **create excel workbook programmatically**, tillämpa kraftfulla spill‑formler och generera färdiga Excel‑filer att dela utan manuell inblandning.

### Vad blir nästa?

* Utforska **conditional formatting** för att markera de spillade data.
* Kombinera **WRAPCOLS** med **SORT** eller **FILTER** för dynamiska instrumentpaneler.
* Använd Aspose.Cells **charting API** för att visualisera de omarrangerade data direkt från kod.

Lycka till med kodningen, och njut av att automatisera dina Excel‑arbetsflöden!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [hur man använder wrapcols i C# – Fullständig guide med Excel WRAPROWS & omberäkna formler](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [Hur man använder WRAPCOLS i C# – Omforma en array till en matris i Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)
- [Hur man använder WRAPCOLS – Komplett guide för C# Excel‑automatisering](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}