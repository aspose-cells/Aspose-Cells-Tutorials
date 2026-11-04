---
category: general
date: 2026-10-01
description: Adj diagramot a Word-hez az Aspose-szal néhány perc alatt. Tanulja meg,
  hogyan ágyazhat be Excel-diagramot a Word-be, exportálhatja a diagramot Excelből
  Word-be, létrehozhat Word-dokumentumot az Aspose-szal, és mentheti a diagramot a
  Word-dokumentumba.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add chart to word
- embed excel chart word
- export chart excel word
- create word document aspose
- save chart word document
language: hu
lastmod: 2026-10-01
og_description: Adj hozzá diagramot a Word-hez az Aspose-szal percek alatt. Ez az
  útmutató bemutatja, hogyan ágyazhat be Excel-diagramot a Word-be, exportálhat diagramot
  Excelből Wordbe, hozhat létre Word-dokumentumot Aspose-szal, és mentheti a diagramot
  a Word-dokumentumba.
og_image_alt: Screenshot illustrating how to add chart to Word using Aspose
og_title: Diagram hozzáadása Word-hez az Aspose segítségével – Excel-diagram beágyazása
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  headline: How to add chart to Word with Aspose – embed Excel chart
  type: TechArticle
- description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  name: How to add chart to Word with Aspose – embed Excel chart
  steps:
  - name: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
    text: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
  - name: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
    text: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
  - name: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
    text: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
  - name: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
    text: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
  - name: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
    text: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
  type: HowTo
tags:
- Aspose
- C#
- Word automation
title: Hogyan adjunk hozzá diagramot a Wordhöz az Aspose segítségével – Excel-diagram
  beágyazása
url: /hu/net/chart-rendering-and-conversion/how-to-add-chart-to-word-with-aspose-embed-excel-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan adjunk diagrammot a Word dokumentumhoz az Aspose‑szal – Excel diagram beágyazása

Ha gyorsan **diagramot szeretne hozzáadni a Wordhöz**, ez a bemutató egy teljes, azonnal futtatható megoldást nyújt. Megmutatjuk, hogyan ágyazhat be egy Excel diagramot egy Word fájlba, hogyan exportálhatja a diagramot az Exceltől a Wordhez, és végül **diagramot menthet Word dokumentumba** néhány C# sorral.

A diagramok beágyazása gyakori igény jelentések, számlák vagy műszerfalak programozott generálásakor. A leírás végére képes lesz **Word dokumentumot létrehozni Aspose‑szal**, amely bármely diagramot tartalmaz egy Excel munkafüzetből, manuális másolás‑beillesztés nélkül.

## Előfeltételek

- .NET 6.0 vagy újabb (a kód .NET Framework 4.7+‑tel is működik)
- Aspose.Cells és Aspose.Words NuGet csomagok (telepítés: `dotnet add package Aspose.Cells` és `dotnet add package Aspose.Words`)
- Egy meglévő Excel fájl (`Chart.xlsx`), amely legalább egy diagramot tartalmaz
- Fejlesztői környezet, például Visual Studio 2022 vagy VS Code

## Diagram hozzáadása a Wordhöz Aspose‑szal

Az alábbiakban a teljes, önálló program látható. Másolja be egy új konzolos projektbe, állítsa vissza a csomagokat, és futtassa. A program betölti az Excel munkafüzetet, létrehozza a Word dokumentumot, beilleszti az első diagramot, és elmenti az eredményt.

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

namespace AddChartToWordDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the Excel workbook that contains the chart
            var workbookPath = @"YOUR_DIRECTORY\Chart.xlsx";
            var workbook = new Workbook(workbookPath);

            // Step 2: Create a new Word document that will receive the chart
            var wordDoc = new Document();

            // Step 3: Initialise a DocumentBuilder for the Word document
            var builder = new DocumentBuilder(wordDoc);

            // Step 4: Insert the first chart from the first worksheet into the Word document
            // This uses Aspose.Words' InsertChart overload that accepts an Aspose.Cells chart object
            builder.InsertChart(workbook.Worksheets[0].Charts[0]);

            // Step 5: Save the resulting Word document
            var outputPath = @"YOUR_DIRECTORY\Chart.docx";
            wordDoc.Save(outputPath);

            Console.WriteLine($"Chart successfully added and saved to '{outputPath}'.");
        }
    }
}
```

### Miért fontos minden sor

1. **A munkafüzet betöltése** – A `Workbook` beolvassa az Excel fájlt, és programozott hozzáférést biztosít a munkalapokhoz és diagramokhoz.  
2. **A Word dokumentum létrehozása** – A `Document` az Aspose.Words belépési pontja minden Word‑feldolgozási feladathoz.  
3. **DocumentBuilder** – Ez a segédosztály lehetővé teszi tartalom (szöveg, képek, diagramok) beillesztését az aktuális kurzorpozícióba.  
4. **InsertChart** – Az a túlterhelés, amely egy `Aspose.Cells.Chart` objektumot fogad, közvetlenül átmásolja a diagram adatait, formázását és sorozatait a Word fájlba. Nem szükséges köztes képkonverzió, így megmarad a vektoros minőség.  
5. **Save** – A `Save` a .docx csomagot a lemezre írja, befejezve a **diagram mentése Word dokumentumba** lépést.

#### Várt kimenet

A program futtatása után nyissa meg a `Chart.docx` fájlt. Látni fogja a pontosan ugyanazt a diagramot, amely a `Chart.xlsx`‑ben volt tárolva, a dokumentum elején (ahol a builder elhelyezkedett). A diagram teljesen szerkeszthető a Wordben (átméretezhető, színek módosíthatók, vagy a forrásadatok változtathatók).

## Excel diagram beágyazása a Wordbe

Ha egynél több diagramot kell beágyazni, ismételje meg az `InsertChart` hívást minden diagramobjektumnál. Például az összes diagram beágyazása az első munkalapról:

```csharp
var sheet = workbook.Worksheets[0];
foreach (Chart chart in sheet.Charts)
{
    builder.InsertChart(chart);
    builder.Writeln(); // add a line break between charts
}
```

**Pro tipp:** Használja a `builder.Writeln()`‑t bekezdésváltás beillesztéséhez, így minden diagram új sorban kezdődik.

## Diagram exportálása Excel‑ről Word‑be – több munkalap kezelése

Ha a diagramok több munkalapon helyezkednek el, iteráljon a munkafüzet `Worksheets` gyűjteményén:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    foreach (Chart chart in ws.Charts)
    {
        builder.InsertChart(chart);
        builder.Writeln();
    }
}
```

Ez a megközelítés **diagram exportálása Excel‑ről Word‑be** bármilyen munkafüzet‑elrendezéshez, így a megoldás robusztus a komplex jelentések esetén.

## Word dokumentum létrehozása Aspose‑szal – megjelenés testreszabása

A beillesztett diagram méretét és pozícióját a `InsertChart` által visszaadott `Shape` módosításával szabályozhatja:

```csharp
Shape chartShape = builder.InsertChart(chart);
chartShape.Width = 500;   // width in points
chartShape.Height = 300;  // height in points
chartShape.WrapType = WrapType.Inline; // make the chart flow with text
```

A `WrapType` `Inline`‑ra állítása biztosítja, hogy a diagram úgy viselkedjen, mint egy normál bekezdés, ami gyakran kívánatos automatizált dokumentumgenerálásnál.

## Diagram mentése Word dokumentumba – legjobb gyakorlatok

- **Használjon leíró fájlnevet** (`Report_Q1_2026.docx`) a verziókezelés egyszerűsítéséhez.
- **Szabadítsa fel az objektumokat**, amikor már nincs rájuk szükség, különösen nagy kötegelt folyamatoknál:

```csharp
wordDoc.Dispose();
workbook.Dispose();
```

- **Ellenőrizze az eredményt** programozottan, ha sok fájlt generál:

```csharp
if (System.IO.File.Exists(outputPath))
{
    Console.WriteLine("File saved successfully.");
}
else
{
    Console.Error.WriteLine("Failed to save the document.");
}
```

## Gyakori kérdések & edge case‑ek

| Kérdés | Válasz |
|----------|--------|
| *Be tudok-e illeszteni egy diagramot, amely nem az első a lapon?* | Igen. Index szerint érheti el: `sheet.Charts[2]` a harmadik diagramhoz. |
| *Mi van, ha az Excel diagram adatforrása nincs a munkafüzetben?* | Az Aspose.Cells közvetlenül a diagramobjektumba ágyazza be az adatokat, így a diagram működőképes marad még akkor is, ha a forrás tartományt eltávolítják. |
| *Szükségem van licencre az Aspose‑hoz?* | Egy ingyenes értékelő verzió működik, de a licencelt verzió eltávolítja a vízjelet és feloldja a teljes funkcionalitást. |
| *A diagram szerkeszthető lesz a Wordben a beillesztés után?* | Igen, a diagram natív Word diagramként kerül be, így a felhasználók szerkeszthetik a sorozatokat, címeket és stílusokat a Word felületén. |
| *Hogyan illeszthetek be egy diagramot képként a natív diagram helyett?* | Használja a `builder.InsertImage(chart.ToImage())`‑t rasterkép beágyazásához. Ez akkor hasznos, ha a pontos vizuális megjelenést szeretné megőrizni Word‑szintű szerkeszthetőség nélkül. |

## Teljes működő példa (másolás‑beillesztés)

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

class AddChartToWord
{
    static void Main()
    {
        // Load Excel workbook
        var wb = new Workbook(@"C:\Data\Chart.xlsx");

        // Create Word document
        var doc = new Document();
        var builder = new DocumentBuilder(doc);

        // Insert every chart from every worksheet
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (Chart ch in ws.Charts)
            {
                Shape shape = builder.InsertChart(ch);
                shape.Width = 500;
                shape.Height = 300;
                builder.Writeln(); // separate charts
            }
        }

        // Save the document
        var outPath = @"C:\Data\ReportWithCharts.docx";
        doc.Save(outPath);
        Console.WriteLine($"Document saved to {outPath}");
    }
}
```

A kód futtatása egy Word fájlt (`ReportWithCharts.docx`) hoz létre, amely **diagram hozzáadása a Wordhöz** eredményeket tartalmaz a forrás munkafüzet minden diagramjához.

## Összegzés

Most már tudja, hogyan **adjunk diagramot a Wordhöz** az Aspose.Cells és Aspose.Words segítségével, hogyan **beágyazzuk az Excel diagramot Wordbe**, **exportáljuk a diagramot Excel‑ről Word‑be**, **létrehozzuk a Word dokumentumot Aspose‑szal**, és végül **mentse a diagramot Word dokumentumba**. A megközelítés egy‑diagramos esetekre és összetett, több munkalapot tartalmazó munkafüzetekre egyaránt alkalmazható.

Következő lépések, amelyeket érdemes felfedezni:

- Egyedi stílusok alkalmazása a beillesztett diagramokra (színek, betűtípusok) a `Chart` API‑val.
- Diagrambeillesztés kombinálása szöveggenerálással a teljesen automatizált jelentések előállításához.
- Aspose.Slides használata, ha szüksége van


## Mit tanuljon meg legközelebb?


Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [How to Save DOCX from Excel – Complete Guide to Export Charts to Word](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-docx-from-excel-complete-guide-to-export-charts/)
- [Create Excel Workbook with Pie Chart Using Aspose.Cells .NET - Comprehensive Guide](/cells/english/net/charts-graphs/create-excel-workbook-pie-chart-aspose-cells-net/)
- [Create a Bubble Chart in Excel Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/create-bubble-chart-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}