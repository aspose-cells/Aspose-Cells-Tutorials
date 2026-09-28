---
category: general
date: 2026-09-27
description: Állítsa be a nyomtatási területet az Excelben, és tanulja meg, hogyan
  exportálhat PNG képeket a kijelölt cellákról. Ez az útmutató a tartomány képként
  való mentését és a kép munkalapra való hozzáadását is bemutatja.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: hu
lastmod: 2026-09-27
og_description: Állítsa be a nyomtatási területet Excelben, és exportálja PNG formátumban
  az Aspose.Cells segítségével. Kövesse ezt a lépésről‑lépésre útmutatót a tartomány
  képként mentéséhez és a kép hozzáadásához a munkalaphoz.
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: Nyomtatási terület beállítása Excelben – PNG exportálása C#‑ban
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Hogyan állítsuk be a nyomtatási területet Excelben, és exportáljuk PNG-ként
url: /hu/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan állítsuk be a nyomtatási területet Excelben, és exportáljuk PNG‑ként

Ha **set print area excel**‑t kell beállítanod, mielőtt képet hoznál létre, ez az útmutató pontosan megmutatja, hogyan teheted meg. Emellett megtanulod, hogyan **exportálj png** fájlokat egy adott tartományból, **save range as image**, és **add picture to worksheet** egyetlen, ismételhető munkafolyamatban.

Az Excel programozott kezelése gyakran azt jelenti, hogy csak egy cellacsoportot – például egy pivot táblát vagy diagramot – szeretnél képpé alakítani. Ha először meghatározod a nyomtatási területet, garantálod, hogy az exportált PNG pontosan az általad várt cellákat tartalmazza, semmi többet, semmi kevesebbet. Ez a tutorial minden lépést végigvezet, a munkafüzet betöltésétől a végső PNG fájl mentéséig, és elmagyarázza, miért fontos minden beállítás.

## Előkövetelmények

Mielőtt elkezdenéd, győződj meg róla, hogy a következők telepítve vannak:

* .NET 6.0 vagy újabb
* Visual Studio 2022 (vagy bármely C# IDE)
* Az **Aspose.Cells for .NET** NuGet csomag (`Install-Package Aspose.Cells`)
* Egy Excel fájl (`input.xlsx`) egy ismert könyvtárban

Ezek a követelmények biztosítják, hogy a kód további konfiguráció nélkül fusson.

## 1. lépés: Töltsd be a munkafüzetet, amivel dolgozni szeretnél

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

A `Workbook` osztály képviseli az egész Excel fájlt. Az első betöltés után hozzáférsz a munkalapokhoz, cellákhoz és az oldalbeállítási opciókhoz.

## 2. lépés: **Set print area excel** a célzott tartományra

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

A **print area** beállítása megmondja az Excelnek (és az Aspose.Cells‑nek), mely cellák tartoznak a nyomtatható oldalhoz. Amikor később képként exportálod a munkalapot, csak ez a terület lesz renderelve, ami elengedhetetlen egy tiszta **export selected cells image** létrehozásához.

## 3. lépés: Képexportálási beállítások konfigurálása – **how to export png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

Az `ImageOrPrintOptions` szabályozza a kimeneti formátumot. A `ImageFormat.Png` kiválasztásával magas felbontású, átlátszó háttérrel rendelkező képet kapsz, amely jól működik webes és asztali környezetben egyaránt.

## 4. lépés: Kép létrehozása a meghatározott tartományból és **add picture to worksheet**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

A `Pictures.Add` metódus új képet szúr be a munkalapba. Ha a 2. lépésben létrehozott tartományt adod át, akkor **save range as image** közvetlenül a lapra kerül, ami hasznos, ha később a képet más részekben is hivatkozni szeretnéd.

## 5. lépés: **Save the picture as an image file** – a **export selected cells image** munkafolyamat befejezése

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

A `Save` hívás a 3. lépésben definiált opciók szerint írja a képet a fájlrendszerbe. Az eredményül kapott `selected_range.png` pontosan a **set print area excel** parancs által meghatározott cellákat tartalmazza.

## Teljes, futtatható példa

Az összes részegység egyesítése egy kompakt programot ad, amelyet bármely konzolos alkalmazásba beilleszthetsz:

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### Várható kimenet

A program futtatása a következőt írja ki:

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

És megtalálod a `selected_range.png` fájlt, amely csak az `input.xlsx` A1‑től G20‑ig terjedő celláit mutatja.

## Gyakori hibák és hogyan kerülhetők el

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| Az exportált kép az egész munkalapot tartalmazza | Nem lett definiálva nyomtatási terület | Győződj meg róla, hogy **set print area excel**‑t állítasz be a kép létrehozása előtt |
| A PNG elmosódott | Alapértelmezett DPI alacsony | Állítsd be az `imageOptions.DpiX` és `imageOptions.DpiY` értékét magasabbra (pl. 300) |
| Fájl nem található hiba | Rossz könyvtárútvonal | Használd a `Path.Combine`‑t, vagy ellenőrizd, hogy a mappa létezik |
| A kép eltolódik | Hibás sor/oszlop indexek | A `Pictures.Add` első két paramétere a kép bal‑felső cellájának koordinátája; tartsd őket `0,0`‑nál a tiszta exporthoz |

## Pro tipp: Több tartomány exportálása egy futtatásban

Ha több területre is **export selected cells image**‑t szeretnél, ismételd meg a 2‑5. lépéseket egy ciklusban, minden iterációban módosítva a `printArea`‑t. Ne felejts egyedi fájlnevet adni minden képnél, különben a későbbi mentés felülírja az előzőt.

## Összegzés

Most már tudod, hogyan **set print area excel**, hogyan konfiguráld a **how to export png**‑t, hogyan **save range as image**, és hogyan **add picture to worksheet** az Aspose.Cells segítségével. Ez az end‑to‑end megoldás néhány C# sorral bármely cellablokkot magas minőségű PNG‑vé alakít.

A következőket is felfedezheted:

* Szegélyek vagy vízjelek hozzáadása az exportált PNG‑hez (keresd a *add picture to worksheet* stílusra vonatkozó példákat)
* Közvetlen exportálás PDF‑be nyomtatható jelentésekhez (*export selected cells image* → PDF munkafolyamat)
* A folyamat automatizálása több munkafüzet esetén kötegelt feladatként

Nyugodtan kísérletezz különböző tartományokkal, DPI beállításokkal vagy képformátumokkal, hogy a projekted igényeinek megfeleljen. Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy könnyedén elsajátíthasd az API további funkcióit, és alternatív megvalósítási megközelítéseket is felfedezhess a saját projektjeidben.

- [Set Print Area in Excel and Export to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Export Excel Print Area to HTML with Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}