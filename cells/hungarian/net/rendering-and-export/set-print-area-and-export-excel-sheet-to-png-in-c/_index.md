---
category: general
date: 2026-10-26
description: Állítsd be a nyomtatási területet, és exportáld az Excel munkalapot PNG
  formátumba C#-ban. Ismerd meg a képexportálási lehetőségeket, a PNG exportálás módját,
  és hogyan kaphatsz nyomtatható képet egy munkafüzetből.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: hu
lastmod: 2026-10-26
og_description: Állítsa be a nyomtatási területet, és exportálja az Excel munkalapot
  PNG formátumba C#-ban. Ez a lépésről‑lépésre útmutató bemutatja a képexportálási
  lehetőségeket, valamint azt, hogyan exportáljon PNG-t egy munkafüzetből.
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: Nyomtatási terület beállítása és Excel munkalap exportálása PNG formátumba
  – C# útmutató
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Nyomtatási terület beállítása és Excel munkalap PNG formátumba exportálása
  C#‑ban
url: /hu/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Set print area and export Excel sheet to PNG in C#

Ha **set print area**-ra van szüksége, mielőtt egy Excel munkalapot PNG‑ként exportálna, ez az útmutató megmutatja, hogyan teheti. Egy teljes C# példát fog látni, amely beállítja a kép exportálási opciókat, módosítja a munkalap nyomtatási területét, és az eredményt képként menti.

Az Excel munkalap PNG‑ként történő exportálása gyakori igény, ha egy munkalap pillanatfelvételét szeretné beágyazni jelentésbe, e‑mailbe vagy weboldalra. Az alábbi kód bármely, pivot tábla tartalmazó munkafüzeten működik, de a technika normál adat tartományokra is alkalmazható. Külső eszközök nem szükségesek – csak az Aspose.Cells for .NET könyvtár.

## Előkövetelmények

- .NET 6.0 vagy újabb (a minta a .NET 6‑ra céloz, de bármely friss .NET verzió működik)
- Aspose.Cells for .NET (telepítés NuGet‑en keresztül: `Install-Package Aspose.Cells`)
- Alapvető ismeretek C#‑ban és az Excel fogalmakban, például munkalapok és nyomtatási területek

## 1. lépés: Kép exportálási beállítások konfigurálása

Az első dolog, amit megtesz, egy `ImageOrPrintOptions` példány létrehozása. Ez az objektum azt mondja meg az Aspose.Cells‑nek, hogyan renderelje a munkalapot képként.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**Miért fontos:** A `ImageOrPrintOptions` szabályozza a kimeneti formátumot, a felbontást és egyéb renderelési részleteket. PNG használata veszteségmentes minőséget biztosít, ami ideális jelentésekhez, amelyek éles szöveget és grafikát igényelnek.

## 2. lépés: A munkafüzet betöltése és a cél munkalap elérése

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**Miért fontos:** Egy konkrét `Worksheet` objektummal kell dolgozni, mivel a nyomtatási terület a munkalap szintű beállítás.

## 3. lépés: Azonosítsa a nyomtatni kívánt tartományt

Sok esetben a kívánt adatok egy pivot táblában találhatók. Az alábbi kód kinyeri az első pivot tábla adat tartományát a munkalapon.

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

Ha a munkalap nem tartalmaz pivot táblát, a `pivotDataRange`‑t bármely manuálisan létrehozott `CellArea`‑val helyettesítheti, például:

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## 4. lépés: **Set print area** beállítása a kiválasztott tartományhoz

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**Miért fontos:** A nyomtatási terület megmondja az Excelnek (és az Aspose.Cells‑nek), mely cellákat vegye fel a munkalap képbe renderelésekor. A nyomtatási terület a pivot adat tartománnyal való összehangolásával elkerülhetők az üres margók, és biztosítható, hogy az exportált PNG csak a releváns adatokat tartalmazza.

## 5. lépés: A munkalap exportálása PNG képként

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**Miért fontos:** A `worksheet.ToImage` figyelembe veszi a korábban beállított nyomtatási területet, így a PNG fájl pontosan az Ön által definiált cellákat tartalmazza. A kép hozzárendelése egy kép alakzathoz lehetővé teszi, hogy szükség esetén visszaágyazza a munkafüzetbe, míg a lemezre mentés egy önálló fájlt eredményez.

## Teljes működő példa

Az összes lépés egyesítése egy önálló programot eredményez, amelyet azonnal futtathat.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### Várt kimenet

A program futtatása létrehozza a `C:\Temp\WorksheetExport.png` fájlt. A fájl megnyitása egy éles PNG képet mutat, amely csak a **set print area** által definiált cellákat tartalmazza (ebben a példában a pivot tábla adatai). A képet be lehet illeszteni Word dokumentumokba, PowerPoint diákba vagy weboldalakra további konverziós lépések nélkül.

## Több munkalap vagy pivot tábla kezelése

- **Több munkalap:** Iteráljon a `wb.Worksheets`‑en, és ismételje meg a 3‑5. lépéseket minden exportálandó munkalaphoz.
- **Több pivot tábla:** Válassza ki a megfelelő `PivotTables[index]`‑t, vagy iteráljon a `worksheet.PivotTables`‑en, hogy minden táblát egyenként exportálja.
- **Nincs pivot tábla:** Hozzon létre egy `CellArea`‑t manuálisan (lásd a 3. lépésben lévő megjegyzést), és rendelje hozzá a `PrintArea`‑hoz.

## Gyakorlati tippek (E‑E‑A‑T)

- **Pro tipp:** Állítsa a `HorizontalResolution` és `VerticalResolution` értékeket 300 DPI‑re a nyomtatásra kész PNG‑khez; alacsonyabb értékek csökkentik a fájlméretet webes használathoz.
- **Figyeljen az üres kép alakzatokra:** Ha a munkalapon nincs kép alakzat, adjon hozzá egyet a kép hozzárendelése előtt:

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **Teljesítmény:** Egyetlen `ImageOrPrintOptions` példány újrahasználata több munkalap esetén elkerüli a felesleges allokációkat.
- **Kompatibilitás:** Az Aspose.Cells 23.9+ teljes mértékben támogatja a .NET 6‑ot és újabbakat; a korábbi verziók esetén szükség lehet az API nevek módosítására.

## Következtetés

Most már tudja, hogyan kell **set print area** és exportálni egy Excel

## Mit érdemes legközelebb megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [Hogyan exportáljunk Excel-t PNG‑ként – teljes lépésről‑lépésre útmutató](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [Hogyan exportáljunk Excel tartományt képként C#‑val és Aspose.Cells‑szel](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [excel munkalap png‑be – Pivot tábla exportálása PNG‑ként C#‑ban](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}