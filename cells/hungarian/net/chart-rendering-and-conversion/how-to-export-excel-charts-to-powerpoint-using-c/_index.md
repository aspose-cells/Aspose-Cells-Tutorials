---
category: general
date: 2026-10-26
description: Tanulja meg, hogyan exportálhatja az Excel-diagramokat PowerPointba C#-al.
  Tartsa meg a formák szerkeszthetőségét, és néhány sor kóddal mentse PPTX formátumban.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel charts to powerpoint
- Aspose.Cells export
- C# Excel to PowerPoint conversion
- preserve shape editability
- SaveFormat.Pptx
- Workbook.Save method
language: hu
lastmod: 2026-10-26
og_description: Exportálja az Excel diagramokat PowerPointba C#‑val. Ez az útmutató
  bemutatja, hogyan lehet a formákat szerkeszthetően megtartani, és PPTX‑ként menteni
  az Aspose.Cells segítségével.
og_image_alt: Export Excel charts to PowerPoint example showing a chart transferred
  from Excel to a slide
og_title: Excel diagramok exportálása PowerPointba C#‑val – lépésről‑lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  headline: How to export Excel charts to PowerPoint using C#
  type: TechArticle
- description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  name: How to export Excel charts to PowerPoint using C#
  steps:
  - name: Load the Excel workbook
    text: '```csharp using Aspose.Cells;'
  - name: (Optional) Adjust workbook settings
    text: In most cases the default settings are sufficient for a clean export. However,
      if you need to change the calculation mode, page setup, or hide certain sheets,
      you can do it here.
  - name: Save the workbook as a PowerPoint file
    text: '```csharp // Export the workbook to PPTX while keeping chart shapes editable
      workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx); ```'
  - name: Verify the result
    text: 'Open `Shapes.pptx` in PowerPoint and:'
  - name: 'Edge case: Exporting multiple worksheets with separate charts'
    text: If your Excel file contains several worksheets, each with its own chart,
      Aspose.Cells creates a separate slide for each chart automatically. You can
      control slide order by rearranging worksheets before the save operation.
  - name: 'Performance tip: Stream the output instead of writing to disk'
    text: When generating PowerPoint files in a web API, avoid temporary files by
      writing to a `MemoryStream`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- PowerPoint
title: Hogyan exportáljunk Excel-diagramokat PowerPointba C#‑val
url: /hu/net/chart-rendering-and-conversion/how-to-export-excel-charts-to-powerpoint-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel diagramok exportálása PowerPointba C#-val

Ha **Excel diagramokat szeretne exportálni PowerPointba**, ez az útmutató egy komplett, azonnal futtatható megoldáson keresztül vezet végig. Akár jelentéskészítő irányítópultot épít, akár diakészleteket automatizál, láthatja, hogyan tartanak néhány C# sor a diagram alakzatokat teljesen szerkeszthető állapotban a konverzió után.

Ebben a tutorialban megtanulja, hogyan:

* Betöltsön egy meglévő Excel munkafüzetet, amely diagramokat tartalmaz.  
* (Opcionálisan) finomhangolja a munkafüzet beállításait az exportálás előtt.  
* Mentse a munkafüzetet PowerPoint fájlként, miközben megőrzi az alakzatok szerkeszthetőségét.  

Mindez a **Aspose.Cells for .NET** segítségével valósul meg, egy olyan könyvtárral, amely Excel‑ról PowerPointra konvertál, anélkül hogy a szerveren a Microsoft Office-ra lenne szükség.

## Amire szüksége lesz

| Követelmény | Ok |
|-------------|----|
| .NET 6.0 vagy újabb | Modern futtatókörnyezet teljes nyelvi funkciókkal |
| Visual Studio 2022 (vagy bármely IDE) | Kényelmes szerkesztő és hibakereső |
| **Aspose.Cells for .NET** NuGet csomag | Biztosítja a `Workbook` osztályt és a `SaveFormat.Pptx` támogatást |
| Egy Excel fájl (`ChartAndShapes.xlsx`), amely legalább egy diagramot tartalmaz | Az exportálni kívánt diagramok forrása |

> **Pro tipp:** Használja az ingyenes **Aspose.Cells Evaluation** verziót a kód teszteléséhez; egy licenckulcs eltávolítja az értékelési vízjelet.

```bash
dotnet add package Aspose.Cells
```

## Excel diagramok exportálása PowerPointba – teljes munkafolyamat

Az alábbi kód a teljes folyamatot valósítja meg, miközben **megőrzi az alakzatok szerkeszthetőségét**. Minden lépést részletesen kifejtünk.

### 1. lépés: Az Excel munkafüzet betöltése

```csharp
using Aspose.Cells;

// Load the workbook that holds the charts you want to export
Workbook workbook = new Workbook(@"C:\Projects\ChartAndShapes.xlsx");
```

*A `Workbook` osztály képviseli az egész Excel fájlt. A fájl betöltése beolvassa az összes munkalapot, diagramot és alakzatot a memóriába, ami minden további manipulációhoz szükséges.*

### 2. lépés: (Opcionális) A munkafüzet beállításainak módosítása

A legtöbb esetben az alapértelmezett beállítások elegendőek egy tiszta exportáláshoz. Ha azonban módosítani kell a számítási módot, az oldalbeállításokat, vagy el kell rejteni bizonyos lapokat, ezt itt teheti meg.

```csharp
// Example: ensure all formulas are calculated before export
workbook.CalculateFormula();

// Example: hide a sheet that you don’t want in the PowerPoint
workbook.Worksheets["SecretData"].IsVisible = false;
```

> **Miért fontos:** A beállítások konverzió előtti módosítása garantálja, hogy a generált diák pontosan azt az állapotot tükrözzék, amit szeretne, különösen akkor, ha képletek vagy rejtett lapok befolyásolhatják a diagram adatait.

### 3. lépés: A munkafüzet mentése PowerPoint fájlként

```csharp
// Export the workbook to PPTX while keeping chart shapes editable
workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx);
```

*A `SaveFormat.Pptx` állandó azt mondja az Aspose.Cells-nek, hogy PowerPoint prezentációt írjon. A könyvtár belsőleg minden Excel diagramot PowerPoint alakzattá konvertál, amely teljesen szerkeszthető marad a Microsoft PowerPointban.*

### 4. lépés: Az eredmény ellenőrzése

Nyissa meg a `Shapes.pptx` fájlt PowerPointban, majd:

1. Válasszon ki egy diagramot bármely dián.  
2. Jobb‑kattintás → **Edit Data**.  
3. Ellenőrizze, hogy megjelenik a diagram adat táblázata, és módosíthatja az értékeket.

Ha a diagram megnyitja a **Edit Data** ablaktáblát, a konverzió sikeres volt, és a **alakzatok szerkeszthetősége** megmaradt.

![Export Excel charts to PowerPoint example](export-excel-charts-to-powerpoint.png){.img-fluid alt="Excel diagramok exportálása PowerPointba példa"}

## Gyakori buktatók és hogyan kerülhetők el

| Probléma | Ok | Megoldás |
|----------|----|----------|
| A diagramok statikus képként jelennek meg | Régebbi Aspose.Cells verzió használata, amely nem támogatja a PPTX exportot | Frissítsen a legújabb Aspose.Cells 23.x vagy újabb verzióra |
| Hiányzó adatok a PowerPoint diagramon | A munkafüzet nincs teljesen kiszámítva exportálás előtt | Hívja a `workbook.CalculateFormula()` metódust a `Save` előtt |
| Az alakzatok nem szerkeszthetők | `SaveFormat.Xlsx` használata `SaveFormat.Pptx` helyett | Győződjön meg róla, hogy a `Workbook.Save` hívásnál `SaveFormat.Pptx`-t ad át |
| Licenc kivétel futás közben | Értékelő verzió regisztrált licenc nélkül | Regisztrálja licencét a `License license = new License(); license.SetLicense("Aspose.Cells.lic");` kóddal |

### Szélsőséges eset: Több munkalap exportálása külön diagramokkal

Ha az Excel fájl több munkalapot tartalmaz, mindegyik saját diagrammal, az Aspose.Cells automatikusan külön diát hoz létre minden diagramhoz. A diák sorrendjét a munkalapok átrendezésével szabályozhatja a mentés előtt.

```csharp
// Move the worksheet that should appear first in the slide deck
workbook.Worksheets.MoveTo(2, 0); // move sheet index 2 to position 0
```

### Teljesítmény tipp: Az output streamelése a lemezre írás helyett

Web API-ban PowerPoint fájlok generálásakor kerülje a temporális fájlokat, írjon egy `MemoryStream`-be.

```csharp
using (MemoryStream pptStream = new MemoryStream())
{
    workbook.Save(pptStream, SaveFormat.Pptx);
    // Return the stream as a file download
    FileContentResult result = new FileContentResult(pptStream.ToArray(),
        "application/vnd.openxmlformats-officedocument.presentationml.presentation")
    {
        FileDownloadName = "Charts.pptx"
    };
    return result;
}
```

## Teljes, futtatható példa

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing charts
            string excelPath = @"C:\Projects\ChartAndShapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2. (Optional) Ensure formulas are up‑to‑date
            workbook.CalculateFormula();

            // 3. Export to PowerPoint while preserving shape editability
            string pptxPath = @"C:\Projects\Shapes.pptx";
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export complete. PowerPoint saved to: {pptxPath}");
        }
    }
}
```

**Várható kimenet:** A konzol kiírja a megerősítő üzenetet, és a `Shapes.pptx` megnyílik PowerPointban, ahol minden Excel diagram saját dián jelenik meg. Egy diagram kiválasztása lehetővé teszi az adat szerkesztését, ezzel megerősítve, hogy a **alakzatok szerkeszthetősége** megmaradt.

## Összefoglalás és a következő lépések

Most már tudja, hogyan **exportáljon Excel diagramokat PowerPointba** C#-val, miközben a diagramok teljesen szerkeszthetőek maradnak. A megoldás középpontjában a `Workbook.Save` metódus `SaveFormat.Pptx` paraméterrel áll, amely a **Aspose.Cells export** funkció része, és elrejti a bonyolult Open XML kezelését.

Innen továbbfejlesztheti:

* Egyedi diacímek vagy megjegyzések hozzáadása a **Aspose.Slides** API-val.  
* Egyéb Excel objektumok (táblázatok, képek) konvertálása diagramok mellett.  
* Több munkafüzet kötegelt feldolgozásának automatizálása háttérszolgáltatásban.

Kísérletezzen nyugodtan a fent bemutatott opcionális beállításokkal, és integrálja ezt a mintát jelentéskészítő folyamataiba a gyors, megbízható PowerPoint generálás érdekében.

## Mit érdemes legközelebb megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz komplett, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [Excel diagram exportálása PowerPointba C#-val – komplett Aspose.Cells útmutató](/cells/english/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/)
- [Hogyan exportáljunk Excel-t PowerPointba C#-val – komplett útmutató](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)
- [Hogyan exportáljunk alakzatokat Excelből PowerPointba – komplett útmutató](/cells/english/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}