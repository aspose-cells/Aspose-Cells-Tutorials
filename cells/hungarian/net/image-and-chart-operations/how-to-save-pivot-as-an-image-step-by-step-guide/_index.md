---
category: general
date: 2026-03-01
description: Hogyan mentheted el a pivotot gyorsan és megbízhatóan. Tanuld meg, hogyan
  exportálhatod a pivotot, a pivot képét, és hogyan konvertálhatod a tartományt képpé
  néhány C# sorral.
draft: false
keywords:
- how to save pivot
- how to export pivot
- export pivot image
- convert range to image
language: hu
og_description: Hogyan mentheted el a pivotet C#-ban néhány másodperc alatt. Kövesd
  ezt az útmutatót a pivot exportálásához, a pivot kép exportálásához, és a tartomány
  képpé konvertálásához tiszta kóddal.
og_title: Hogyan mentheted a Pivotot képként – Gyors C#-os útmutató
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Hogyan mentheted el a Pivotot képként – Lépésről lépésre útmutató
url: /hu/net/image-and-chart-operations/how-to-save-pivot-as-an-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan mentse el a Pivot táblát képként – Teljes C# útmutató

Gondolt már arra, **hogyan mentse el a pivot** közvetlenül egy Excel munkalapról anélkül, hogy manuálisan megnyitná a fájlt? Ön sem egyedül van. Sok jelentéscsővezetékben a pivot tábla a végső vizuális elem, és a következő lépés—PDF-be ágyazása, e‑mailben küldése vagy egy irányítópulton való elhelyezése—egy statikus képet igényel. A jó hír? Néhány API hívással **hogyan mentse el a pivot** null UI interakcióval.

Ebben az útmutatóban végigvezetjük a pontos kódot, amire szüksége van a **hogyan exportálja a pivot**, átalakítva azt egy **export pivot image**-re, és még a **convert range to image** funkciót is használhatja bármilyen egyéni területhez. A végére egy újrahasználható metódust kap, amelyet bármely .NET projektbe beilleszthet.

> **Gyors megjegyzés:** A példák a népszerű Aspose.Cells for .NET könyvtárat használják, de a koncepciók bármely olyan könyvtárra is alkalmazhatók, amely biztosítja a `PivotTable`, `Range` és a kép‑export funkciókat.

## Előkövetelmények – Amit a kezdés előtt szükséges

- **.NET 6+** (vagy .NET Framework 4.7.2+) telepítve legyen a gépén.  
- **Aspose.Cells for .NET** (ingyenes próba vagy licencelt verzió). A NuGet-en keresztül adható hozzá:  

  ```bash
  dotnet add package Aspose.Cells
  ```
- Alapvető C# és Excel ismeretek. Mély belső részletek nem szükségesek.  
- Egy meglévő Excel fájl (`sample.xlsx`), amely legalább egy pivot táblát tartalmaz.

Ha bármelyik ismeretlennek tűnik, álljon meg és telepítse először a csomagot—nincs értelme mélyebbre menni, amíg a könyvtár nem áll készen.

## Hogyan mentse el a Pivot táblát képként – A központi metódus

Az alábbi **teljes, futtatható** kódrészlet bemutatja a teljes folyamatot. Tartalmaz importokat, hibakezelést és megjegyzéseket, így közvetlenül beillesztheti egy konzolos alkalmazásba.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;   // Needed for Image handling
using System.Drawing;        // System.Drawing.Image

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the workbook that holds the pivot table
            string workbookPath = @"C:\Temp\sample.xlsx";

            // Destination folder for the exported image
            string outputFolder = @"C:\Temp\Images";

            try
            {
                // Ensure output directory exists
                System.IO.Directory.CreateDirectory(outputFolder);

                // Call the helper that does the actual work
                SavePivotAsImage(workbookPath, outputFolder, "pivot.png");
                Console.WriteLine("Pivot saved successfully!");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }

        /// <summary>
        /// Saves the first pivot table in the given workbook as an image file.
        /// This method shows exactly **how to export pivot** and **convert range to image**.
        /// </summary>
        /// <param name="workbookPath">Full path to the source .xlsx file.</param>
        /// <param name="outputFolder">Folder where the image will be written.</param>
        /// <param name="fileName">Desired image file name (e.g., pivot.png).</param>
        public static void SavePivotAsImage(string workbookPath, string outputFolder, string fileName)
        {
            // Load the workbook
            Workbook wb = new Workbook(workbookPath);

            // --------------------------------------------------------------
            // Step 1: Get the first pivot table from the first worksheet
            // --------------------------------------------------------------
            Worksheet ws = wb.Worksheets[0];
            if (ws.PivotTables.Count == 0)
                throw new InvalidOperationException("No pivot tables found in the worksheet.");

            // This is the object we will eventually export.
            PivotTable pivot = ws.PivotTables[0];

            // --------------------------------------------------------------
            // Step 2: Create a range that covers the entire pivot table
            // --------------------------------------------------------------
            // The CreateRange method returns a Range object that precisely
            // matches the pivot's visual bounds.
            Range pivotRange = pivot.CreateRange();

            // --------------------------------------------------------------
            // Step 3: Convert the range to an image (the **export pivot image** step)
            // --------------------------------------------------------------
            // ToImage returns a System.Drawing.Image instance.
            Image pivotImg = pivotRange.ToImage();

            // --------------------------------------------------------------
            // Step 4: Save the image to a file
            // --------------------------------------------------------------
            string fullPath = System.IO.Path.Combine(outputFolder, fileName);
            pivotImg.Save(fullPath, System.Drawing.Imaging.ImageFormat.Png);
        }
    }
}
```

### Miért működik ez

- **A Pivot elérése:** `ws.PivotTables[0]` az első pivot táblát veszi, ami gyakran a kívánt exportálandó. Ha több pivotja van, egyszerűen módosítsa az indexet vagy iteráljon a gyűjteményen.
- **A tartomány létrehozása:** `pivot.CreateRange()` egy `Range` objektumot ad, amely pontosan a képernyőn megjelenített celláknak felel meg. Ez a kulcsfontosságú lépés, amely lehetővé teszi a **convert range to image** végrehajtását anélkül, hogy manuálisan számolná ki a címeket.
- **A tartomány képpé alakítása:** `pivotRange.ToImage()` belsőleg raszterizálja a cellákat, megőrizve a formázást, színeket és szegélyeket—pontosan azt, amit az Excelben lát.
- **A PNG mentése:** Az utolsó `Save` hívás egy hordozható PNG fájlt ír, így az **export pivot image** készen áll bármely további folyamat (PDF, e‑mail, web) számára.

## Hogyan exportálja a Pivot – Változatok, amelyekre szüksége lehet

### Export több pivotot ugyanarról a lapról

Ha a munkafüzet több pivotot tartalmaz, ciklussal végigmehet rajtuk:

```csharp
foreach (PivotTable pt in ws.PivotTables)
{
    Range r = pt.CreateRange();
    Image img = r.ToImage();
    string name = $"pivot_{pt.Index}.png";
    img.Save(System.IO.Path.Combine(outputFolder, name), ImageFormat.Png);
}
```

### Exportálás más formátumokba (JPEG, BMP, GIF)

Az `Image.Save` metódus bármely `ImageFormat`-ot elfogad. Csak cserélje le az `ImageFormat.Png`-t `ImageFormat.Jpeg`-re vagy `ImageFormat.Bmp`-re:

```csharp
pivotImg.Save(fullPath, System.Drawing.Imaging.ImageFormat.Jpeg);
```

### Kép felbontásának beállítása

Néha nagyobb felbontású képernyőfelvételre van szükség nyomtatáshoz. Használja azt a túlterhelést, amelyik `ImageOrPrintOptions`-t fogad:

```csharp
ImageOrPrintOptions opts = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300   // DPI
};
Image highRes = pivotRange.ToImage(opts);
highRes.Save(fullPath, ImageFormat.Png);
```

## Tartomány képpé konvertálása – Pivotokon túl

A `ToImage` metódus nem csak pivotokra korlátozódik. Szeretne egy diagramot, adat táblát vagy egy egyéni cellatartományt rögzíteni? Csak adja át bármely `Range`-t:

```csharp
// Capture cells B2:E20 as an image
Range customRange = ws.Cells.CreateRange("B2", "E20");
Image rangeImg = customRange.ToImage();
rangeImg.Save(@"C:\Temp\custom_range.png", ImageFormat.Png);
```

Ez a **convert range to image** lényege—az ugyanaz az API, amit a pivothoz használt, bármely téglalap alakú blokkra működik.

## Gyakori hibák és profi tippek

- **Pivot frissítés:** Ha a forrásadatok változnak, hívja meg a `pivot.RefreshData()`-t a tartomány létrehozása előtt. Ennek kihagyása elavult képet eredményezhet.
- **Rejtett sorok/oszlopok:** Alapértelmezés szerint a rejtett sorok/oszlopok figyelmen kívül maradnak. Ha láthatóakra van szükség, állítsa be a `pivot.ShowHiddenData = true` értéket a `CreateRange()` előtt.
- **Memória kezelés:** Az `Image` implementálja az `IDisposable`-t. Gyártási kódban csomagolja a képet egy `using` blokkba, vagy hívja a `Dispose()`-t a mentés után, hogy elkerülje a memória szivárgást.
- **Szálbiztonság:** Az Aspose.Cells objektumok nem szálbiztosak. Ha több szálról exportál pivotokat, hozzon létre egy külön `Workbook` példányt szálanként.

## Teljes működő példa – Egy‑fájl megoldás

Azok számára, akik szeretik a copy‑paste-et, itt van az egész program egyetlen fájlba sűrítve. Helyezze be egy új konzolos projektbe, frissítse az elérési útvonalakat, és futtassa.

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using System.IO;
using Aspose.Cells;

namespace PivotExportDemo
{
    class Program
    {
        static void Main()
        {
            string src = @"C:\Temp\sample.xlsx";
            string outDir = @"C:\Temp\Images";

            Directory.CreateDirectory(outDir);
            SaveFirstPivotAsPng(src, outDir, "pivot.png");
        }

        static void SaveFirstPivotAsPng(string workbookPath, string folder, string fileName)
        {
            Workbook wb = new Workbook(workbookPath);
            Worksheet ws = wb.Worksheets[0];

            if (ws.PivotTables.Count == 0)
                throw new Exception("Worksheet contains no pivots.");

            PivotTable pt = ws.PivotTables[0];
            Range r = pt.CreateRange();

            using (Image img = r.ToImage())
            {
                string full = Path.Combine(folder, fileName);
                img.Save(full, ImageFormat.Png);
            }
        }
    }
}
```

A futtatáskor kiírja a „Pivot saved successfully!” üzenetet, és a `pivot.png` fájlt a megadott helyen hozza létre.

## Összegzés

Áttekintettük a **hogyan mentse el a pivot** C#-ban a kezdetektől a végéig, bemutattuk a **hogyan exportálja a pivot** több forgatókönyvhöz, demonstráltuk az **export pivot image** különböző formátumokban, és elmagyaráztuk a háttérben lévő **convert range to image** mechanikát. Ezekkel a kódrészletekkel automatizálhatja a jelentéskészítést, képeket helyezhet PDF-ekbe, vagy egyszerűen archiválhatja az analitikai irányítópultokat anélkül, hogy manuálisan megnyitná az Excelt.

Következő lépések? Próbálja meg beágyazni a generált PNG-t egy PDF-be az Aspose.PDF segítségével, vagy küldje fel egy Azure Blob-ba webes felhasználáshoz. Felfedezheti a diagramok exportálását is ugyanígy—csak cserélje le a `PivotTable`-t egy `Chart` objektumra, és hívja meg a `ToImage()`-t.

Van kérdése a szélsőséges esetekkel, licenceléssel vagy teljesítménnyel kapcsolatban? Hagyjon megjegyzést alább, és jó kódolást!

![hogyan mentse el a pivot](/images/pivot-save-example.png "hogyan mentse el a pivot")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}