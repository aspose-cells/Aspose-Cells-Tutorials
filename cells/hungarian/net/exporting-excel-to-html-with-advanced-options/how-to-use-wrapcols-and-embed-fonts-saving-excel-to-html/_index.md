---
category: general
date: 2026-10-20
description: Ismerje meg, hogyan használja a wrapcols-t az Aspose.Cells-ben, hogyan
  ágyazhat be betűtípusokat HTML-be, és hogyan mentheti az Excelt HTML-ként egy teljes
  C# példával.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: hu
lastmod: 2026-10-20
og_description: Hogyan használjuk a wrapcols-t az Aspose.Cells-ben, ágyazzuk be a
  betűtípusokat HTML-be, és konvertáljuk a munkafüzetet HTML-re egy világos C# útmutatóval
  fejlesztők számára.
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: Hogyan használjuk a wrapcols‑t és ágyazzuk be a betűtípusokat az Excel HTML‑be
  exportálásakor
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and
    save Excel as HTML with a complete C# example.
  headline: How to use wrapcols and embed fonts saving Excel to HTML
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to HTML
- Smart Markers
title: Hogyan használjuk a wrapcols-t és ágyazzuk be a betűtípusokat az Excel HTML-be
  mentésekor
url: /hu/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# A wrapcols használata és betűtípusok beágyazása Excel HTML-be mentésekor

Ha szükséged van arra, hogy **how to use wrapcols** egy Aspose.Cells képletben, ez az útmutató pontos lépéseket mutat. Emellett megtanulod, hogyan **ágyazz be betűtípusokat HTML-be** és **mentsd az Excelt HTML-ként**, hogy a kimenet minden böngészőben azonosuljon.  

Az útmutató három gyakorlati forgatókönyvet fed le: a `WRAPCOLS` függvény használata, egy munkafüzet exportálása beágyazott betűtípusokkal, valamint egy master‑detail jelentés generálása Smart Markerekkel. A végére egyetlen, futtatható C# programod lesz, amely bemutatja ezeket a funkciókat.

## Előfeltételek

* .NET 6.0 (vagy újabb) telepítve.
* Aspose.Cells for .NET hozzáadva a projekthez (`dotnet add package Aspose.Cells`).
* Alapvető ismeretek C#‑ban és Excel képletekben.

Nem szükséges további harmadik féltől származó könyvtár; az Aspose.Cells belsőleg kezeli a HTML konverziót és a betűtípusok beágyazását.

## 1. lépés: A **how to use wrapcols** függvény bemutatása egy képletben

A `WRAPCOLS` függvény egy egydimenziós tartományt két‑dimenziós tömbbé alakít, először oszlopok szerint töltve. Ez akkor hasznos, ha adatokat kell átalakítanod jelentéshez vagy diagramokhoz.

```csharp
using Aspose.Cells;
using System;

class WrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Populate a vertical range A1:A3
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // Apply WRAPCOLS(A1:A3, 2) – this creates a 2‑column array {1,2}
        sheet.Cells["B1"].Formula = "=WRAPCOLS(A1:A3, 2)";

        // Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // Output the result to verify the function works
        Console.WriteLine("Result of WRAPCOLS: " + sheet.Cells["B1"].Value);
        // Expected output: Result of WRAPCOLS: 1
    }
}
```

**Miért működik ez:**  
`WRAPCOLS` két argumentumot vesz – a forrástartományt és az oszlopok számát. A függvény oszloponként tölti a tömböt, eldobva a felesleges értékeket (a példában a `3`‑at). Az eredmény a cél tartomány bal‑felső cellájában (`B1`) jelenik meg, és a teljes tömbhöz manuálisan kibővítheted a tartományt, ha szükséges.

> **Pro tipp:** A képlet beállítása után hívd meg a `workbook.CalculateFormula()`‑t, hogy a cellaértékek olvasása előtt a eredmény naprakész legyen.

## 2. lépés: **Munkafüzet konvertálása HTML-be** és **betűtípusok beágyazása HTML-be**

Amikor egy Excel fájlt HTML-be exportálsz, a betűtípusokat gyakran a böngésző alapértelmezettjei helyettesítik, ami tönkreteheti a megjelenést. Az Aspose.Cells lehetővé teszi, hogy a munkafüzetben használt pontos betűtípusokat közvetlenül a HTML fájlba ágyazd be.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for HtmlSaveOptions
using System;

class HtmlExportDemo
{
    static void Main()
    {
        // Re‑use the workbook from the previous step
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Hello");
        sheet.Cells["A2"].PutValue("World");

        // Configure HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Embedding fonts ensures the output looks the same on any device
            EmbedFonts = true,
            // Optional: specify a folder for supporting files (images, CSS)
            ExportEmbeddedImages = true
        };

        // Save the workbook as an HTML file with embedded fonts
        string outputPath = @"C:\Temp\WorkbookWithFonts.html";
        workbook.Save(outputPath, htmlOptions);

        Console.WriteLine($"Workbook saved to HTML with embedded fonts at: {outputPath}");
    }
}
```

**Miért fontos a betűtípusok beágyazása:**  
Ha az `EmbedFonts` értéke `true`, az Aspose.Cells minden használt TrueType/OpenType betűtípust Base64‑kódolt `@font-face` szabályba konvertál a generált HTML-ben. Ez megszünteti a kliens gépen a betűtípusok telepítésének szükségességét, és pixel‑pontos megjelenítést biztosít.

> **Különleges eset:** Ha a forrás munkafüzet olyan betűtípust hivatkozik, amely nincs telepítve a szerveren, az Aspose.Cells egy alapértelmezett betűtípusra vált, és figyelmeztetést ad. Győződj meg arról, hogy a szükséges betűtípusok elérhetők.

## Mit kellene legközelebb megtanulnod?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészletet tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan használjuk a WRAPCOLS‑t C#‑ban – Excel munkafüzet létrehozása wrap függvényekkel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Hogyan ágyazzunk be betűtípusokat HTML-be – Excel konvertálása HTML-be C#‑al](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [Hogyan konvertáljunk Excel fájlokat HTML-be az Aspose.Cells for .NET használatával: átfedő tartalom elrejtése](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}