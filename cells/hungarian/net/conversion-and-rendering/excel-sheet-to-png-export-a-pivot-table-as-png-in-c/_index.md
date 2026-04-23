---
category: general
date: 2026-03-18
description: Excel munkalap PNG-re konvertálása útmutató, amely bemutatja, hogyan
  exportáljuk a pivot táblát, beállítjuk a nyomtatási területet a pivot táblához,
  és exportáljuk az Excel tartomány képét az Aspose.Cells használatával.
draft: false
keywords:
- excel sheet to png
- how to export pivot
- set print area pivot
- export excel range image
- export worksheet to image
language: hu
og_description: Excel munkalap PNG-re konvertálása útmutató, amely lépésről lépésre
  bemutatja, hogyan exportálhatók pivot táblák, hogyan állítható be a nyomtatási terület
  a pivot táblához, és hogyan exportálhatók Excel tartomány képek C#‑val.
og_title: Excel munkalap PNG-re – A pivot táblák exportálásának teljes útmutatója
tags:
- Aspose.Cells
- C#
- Excel automation
title: excel munkalap png-re – Pivot tábla exportálása PNG-ként C#-ban
url: /hu/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excel sheet to png – Pivot tábla exportálása PNG-ként C#-ban

Szükséged volt már arra, hogy egy **excel sheet to png**-t készíts, de nem tudtad, hogyan rögzítsd csak a pivot táblát? Nem vagy egyedül. Sok jelentéskészítési folyamatban a pivot vizualizáció a főszereplő, és a PNG‑ként való exportálás lehetővé teszi, hogy e‑mailben, műszerfalakon vagy dokumentációban ágyazd be anélkül, hogy az egész munkafüzetet magaddal vinnéd.

Ebben az útmutatóban megmutatjuk, hogyan **exportáljunk pivot** adatot, hogyan **állítsuk be a nyomtatási területet pivot**-ra, és végül hogyan **exportáljunk excel tartomány képet**, hogy egy tiszta **export worksheet to image** fájlt kapj. Nincs rejtett hivatkozás külső dokumentumokra – csak egy teljes, futtatható kódrészlet és a sorok mögötti magyarázat.

## Amire szükséged lesz

- **Aspose.Cells for .NET** (a `Aspose.Cells` NuGet csomag – 23.12 vagy újabb verzió).  
- .NET fejlesztői környezet (Visual Studio, Rider vagy a `dotnet` CLI).  
- Egy Excel fájl (`input.xlsx`), amely legalább egy pivot táblát tartalmaz.

Ennyi. Ha ezek megvannak, vágjunk bele.

## 1. lépés – A munkafüzet betöltése és az első munkalap lekérése

Mielőtt a pivotot megérintenénk, a munkafüzetet memóriába kell töltenünk.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");

            // Get the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];
```

*Miért fontos:* A fájl betöltése hozzáférést biztosít minden objektumhoz (táblák, diagramok, pivotok). Az első munkalap használata egyszerű alapértelmezés; szükség esetén a `0`-t cserélheted a tényleges lap indexre vagy névre.

## 2. lépés – A pivot tábla tartományának lekérése

A pivot tábla egy cellatartományban található. Erre a tartományra van szükségünk, hogy megmondhassuk az Excelnek, mit nyomtasson.

```csharp
            // Assume the first pivot table on the sheet
            PivotTable pivot = worksheet.PivotTables[0];

            // The range that the pivot occupies (e.g., A1:D20)
            CellArea pivotRange = pivot.PivotTableRange;
```

*Miért csináljuk:* A `PivotTableRange` megadja a pontos kezdő és befejező sorokat/oszlopokat. Enélkül az export az egész lapot tartalmazná, ami aláássa a **set print area pivot** célját.

## 3. lépés – A nyomtatási terület meghatározása, hogy csak a pivot jelenjen meg

Az Excel nyomtatási motorja figyelembe veszi a `PrintArea` tulajdonságot. Ha csak a pivotra szűkítjük, elkerüljük a felesleges adatokat vagy üres cellákat.

```csharp
            // Build the address string: "StartRow,StartColumn:EndRow,EndColumn"
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";

            worksheet.PageSetup.PrintArea = printArea;
```

*Pro tipp:* Ha több pivot van ugyanazon a lapon, a tartományaikat egy vesszővel elválasztott listával (`"0,0:10,5,12,0:22,5"`) kombinálhatod. Ez a **export excel range image** technika több blokk esetén.

## 4. lépés – Képexportálási beállítások konfigurálása (PNG formátum)

Az Aspose.Cells lehetővé teszi a kimenet finomhangolását. A PNG veszteségmentes, tökéletes a tiszta pivot vizuálokhoz.

```csharp
            // Configure image export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: increase resolution for sharper output
                HorizontalResolution = 300,
                VerticalResolution = 300
            };
```

*Miért PNG?* A JPEG-től eltérően a PNG megőrzi a szöveg élességét és az átlátszó hátteret, így az ideális **excel sheet to png** esetekben.

## 5. lépés – A munkalap (pivot terület) exportálása PNG fájlba

Most jön a varázslat – a meghatározott nyomtatási terület képpé alakítása.

```csharp
            // Export the first page (index 0) of the worksheet to an image
            // The page corresponds to the print area we set earlier
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            // Inform the user
            System.Console.WriteLine("Pivot exported to PNG successfully!");
        }
    }
}
```

*Mit látsz majd:* Egy `pivot.png` fájl, amely csak a pivot táblát tartalmazza, extra sorok vagy oszlopok nélkül. Nyisd meg bármely képnézőben, és egy megosztható vizuált kapsz.

---

## Gyakran Ismételt Kérdések és Különleges Esetek

### Mi van, ha a munkafüzetnek **több pivot táblája** van?

Szerezd meg minden pivot `PivotTableRange`-jét, egyesítsd a tartományokat, és a kombinált karakterláncot állítsd be a `PrintArea`-ba. Példa:

```csharp
string combinedArea = "";
foreach (PivotTable pt in worksheet.PivotTables)
{
    CellArea ca = pt.PivotTableRange;
    combinedArea += $"{ca.StartRow},{ca.StartColumn}:{ca.EndRow},{ca.EndColumn},";
}
combinedArea = combinedArea.TrimEnd(','); // Remove trailing comma
worksheet.PageSetup.PrintArea = combinedArea;
```

### Exportálhatok **más képformátumokba**?

Természetesen. Módosítsd a `imgOptions.ImageFormat = ImageFormat.Jpeg;` sort (vagy `Bmp`, `Gif`, `Tiff`). Ne feledd, a JPEG tömörítési hibákat okoz – általában nem ideális szöveggazdag pivotokhoz.

### Hogyan kezeljem a **nagy pivotokat**, amelyek több oldalra terjednek?

Állítsd be a `imgOptions.OnePagePerSheet = false;` értéket a többoldalas rendereléshez, majd iterálj az oldalakon:

```csharp
int pageCount = worksheet.PageCount;
for (int i = 0; i < pageCount; i++)
{
    worksheet.ToImage(i, imgOptions).Save($@"C:\Data\pivot_page{i + 1}.png");
}
```

### Mi a helyzet a **rejtett sorok/oszlopok** esetén?

Az Aspose tiszteletben tartja a munkalap láthatósági beállításait. Ha a rejtett elemeket figyelmen kívül kell hagyni, ideiglenesen jelenítsd meg őket exportálás előtt, vagy állítsd be kézzel a `PrintArea`-t.

---

## Teljes működő példa (másolás‑beillesztés készen)

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook & select sheet
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Get the first pivot table's range
            PivotTable pivot = worksheet.PivotTables[0];
            CellArea pivotRange = pivot.PivotTableRange;

            // 3️⃣ Set print area to the pivot only
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";
            worksheet.PageSetup.PrintArea = printArea;

            // 4️⃣ Prepare PNG export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // 5️⃣ Export to PNG
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            System.Console.WriteLine("✅ Pivot exported to PNG at C:\\Data\\pivot.png");
        }
    }
}
```

Futtasd a programot, és megtalálod a `pivot.png`-t ott, ahová mutattad. Nyisd meg a fájlt – tiszta renderelést kell látnod csak a pivot tábláról, semmi más.

---

## Összegzés

Most már van egy **teljes, vég‑től‑végig megoldás** az **excel sheet to png** átalakítására, amely kizárólag egy pivot táblára fókuszál. A **print area pivot** beállításával, a **kép exportálási beállítások** konfigurálásával és az Aspose.Cells `ToImage` metódusának használatával automatizálhatod a jelentéskészítést, beágyazhatod a vizuálokat weboldalakba, vagy egyszerűen archiválhatod az elemzési pillanatképeket.

Mi a következő? Próbáld meg a PNG-t egy nagy felbontású PDF‑re (`ImageFormat.Pdf`) cserélni, kísérletezz több pivottal egy lapon, vagy kombináld ezt a megközelítést diagram exportokkal egy teljes körű műszerfal export pipeline-hoz.

Van valami saját trükköd, amit meg szeretnél osztani? Írj egy megjegyzést, vagy nézd meg a következő útmutatót, ahol a **export worksheet to image**-t vizsgáljuk teljes lapképekhez, beleértve a diagramokat és a feltételes formázást. Jó kódolást!  

<img src="pivot.png" alt="excel sheet to png example of pivot table export">

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}