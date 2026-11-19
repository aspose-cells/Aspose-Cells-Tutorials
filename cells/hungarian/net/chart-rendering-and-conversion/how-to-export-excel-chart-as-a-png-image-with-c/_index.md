---
category: general
date: 2026-11-19
description: Hogyan exportáljunk Excel-diagramot PNG-képként az Aspose.Cells segítségével.
  Tanulja meg, hogyan mentse el az Excel-diagram képét, és állítsa be a képfájlt PNG
  formátumra néhány lépésben.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel chart
- save excel chart image
- set image format png
- save excel picture file
language: hu
lastmod: 2026-11-19
og_description: Hogyan exportáljunk Excel-diagramot PNG képként az Aspose.Cells segítségével.
  Kövesse ezt a lépésről‑lépésre útmutatót az Excel-diagram képének mentéséhez és
  a PNG képformátum hatékony beállításához.
og_image_alt: How to export Excel chart as a PNG image
og_title: Hogyan exportáljunk Excel-diagramot PNG képként – gyors C# útmutató
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to export Excel chart as a PNG image using Aspose.Cells. Learn
    to save Excel chart image and set image format PNG in just a few steps.
  headline: How to export Excel chart as a PNG image with C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Chart export
title: Hogyan exportálhatunk Excel-diagramot PNG képként C#‑al
url: /hu/net/chart-rendering-and-conversion/how-to-export-excel-chart-as-a-png-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan exportáljunk Excel diagramot PNG képként C#‑ban

Ha **how to export Excel chart**‑t szeretne hordozható képként elmenteni, ez az útmutató egy teljes, azonnal futtatható megoldást mutat be. Az Aspose.Cells segítségével **save Excel chart image**‑t PNG formátumban csak három kódsorral menthet, és a tutorial elmagyarázza, hogyan **set image format png** és **save Excel picture file** biztonságosan.

A cikk végére egy futtatható programot kap, amely betölti a munkafüzetet, rendereli az első diagramot, és egy `pivot.png` fájlt ír a lemezre. Nincs szükség további eszközökre, manuális másolás‑beillesztésre – csak tiszta C# kód, amely bármely .NET projektbe beilleszthető.

## Előfeltételek

Mielőtt elkezdené, győződjön meg róla, hogy rendelkezik:

* .NET 6.0 SDK vagy újabb (a kód .NET Framework 4.6+‑al is működik)
* Visual Studio 2022 vagy bármely C# szerkesztő
* Aspose.Cells for .NET licenc (vagy ideiglenes értékelő kulcs)
* Egy Excel fájl (`pivot.xlsx`), amely legalább egy diagramot tartalmaz az első munkalapon

Ezek az egyetlen külső függőségek; a tutorial nem igényel Office telepítést a gépen.

## 1. lépés: Aspose.Cells telepítése

Nyisson egy terminált a projekt mappájában, és futtassa:

```bash
dotnet add package Aspose.Cells
```

A csomag hozzáadja az `Aspose.Cells` névteret, amely biztosítja a `Workbook`, `ImageOrPrintOptions` és egyéb osztályokat a **save Excel chart image** végrehajtásához.

## 2. lépés: Minimális konzolprogram létrehozása

Hozzon létre egy új konzolalkalmazást (`dotnet new console -n ExportChartDemo`), és cserélje le az automatikusan generált `Program.cs`‑t az alábbi kóddal. A program bemutatja, **how to export Excel chart**, és megjegyzésekkel magyarázza minden döntését.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for ImageOrPrintOptions
using System.Drawing.Imaging;  // Provides ImageFormat enum

namespace ExportChartDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook that contains the pivot chart
            // -----------------------------------------------------------------
            // Replace the path with the actual location of your Excel file.
            string workbookPath = @"YOUR_DIRECTORY\pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -----------------------------------------------------------------
            // 2️⃣ Set up image export options (PNG format)
            // -----------------------------------------------------------------
            // This is where we **set image format png** for the exported picture.
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: control the resolution (DPI) of the output image.
                // Higher DPI yields larger files but sharper charts.
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 3️⃣ Render the first picture (the chart) on the first worksheet
            // -----------------------------------------------------------------
            // Aspose.Cells stores charts as Picture objects inside the worksheet.
            // The index [0] refers to the first chart; adjust if you have multiple.
            Worksheet sheet = workbook.Worksheets[0];
            if (sheet.Pictures.Count == 0)
            {
                Console.WriteLine("No pictures found on the first worksheet.");
                return;
            }

            // Render the picture to a PNG file.
            string outputPath = @"YOUR_DIRECTORY\pivot.png";
            sheet.Pictures[0].RenderToImage(imageOptions, outputPath);

            Console.WriteLine($"Chart exported successfully to: {outputPath}");
        }
    }
}
```

### Miért fontos minden rész

* **A munkafüzet betöltése** – A `Workbook` a `.xlsx` fájlt elemzi anélkül, hogy a Microsoft Excel telepítve lenne.
* **ImageOrPrintOptions** – Ez az objektum szabályozza a kimeneti formátumot. Az `ImageFormat = ImageFormat.Png` beállítás **sets image format png**, amely veszteségmentes és széles körben támogatott.
* **RenderToImage** – A `RenderToImage` metódus a diagramot (egy `Picture` objektumot) képfájllá konvertálja. A metódus automatikusan kezeli a méretezést, DPI‑t és az átlátszóságot is.
* **Hibakezelés** – A `sheet.Pictures.Count == 0` ellenőrzés megakadályozza a futásidejű kivételt, ha a munkalapon nincs diagram, ami gyakori hiba, ha a felhasználó rossz lapra mutat.

## 3. lépés: A program futtatása és az eredmény ellenőrzése

1. Építse fel a projektet: `dotnet build`.
2. Futtassa: `dotnet run --project ExportChartDemo`.

Ha minden helyesen van beállítva, a következőt fogja látni:

```
Chart exported successfully to: YOUR_DIRECTORY\pivot.png
```

Nyissa meg a `pivot.png` fájlt bármely képmegjelenítővel. Látnia kell az Excel diagram pontos vizuális ábrázolását, ami megerősíti, hogy sikeresen **saved Excel picture file**.

### Várt kimenet

Az alábbiakban egy példa látható arra, hogy a exportált PNG hogyan nézhet ki (a tényleges diagram az Ön forrásfájljától függ).

![Exportált Excel diagram PNG képként mentve](images/exported-chart.png){: .center alt="Hogyan exportáljunk Excel diagramot PNG képként"}

## 4. lépés: Haladó beállítások – több diagram exportálása

Ha a munkafüzet több diagramot tartalmaz, végigiterálhat a `Pictures` gyűjteményen:

```csharp
for (int i = 0; i < sheet.Pictures.Count; i++)
{
    string chartPath = $@"YOUR_DIRECTORY\chart_{i + 1}.png";
    sheet.Pictures[i].RenderToImage(imageOptions, chartPath);
    Console.WriteLine($"Chart {i + 1} saved to {chartPath}");
}
```

Ez a minta lehetővé teszi, hogy **save Excel chart image** minden diagramra a lapon, ami hasznos jelentéskészítő csővezetékekhez.

## Gyakori buktatók és elkerülésük

| Tünet | Valószínű ok | Megoldás |
|---------|--------------|-----|
| `ArgumentOutOfRangeException` a `Pictures[0]`‑nál | A munkalapon nincs diagram, vagy a diagram másik lapon van. | Ellenőrizze a lap indexet (`Worksheets[0]`) és győződjön meg a diagram létezéséről. Szükség esetén használja a `Worksheets["SheetName"]`‑t. |
| Az exportált kép homályos | A DPI túl alacsony (alapértelmezett 96). | Növelje a `HorizontalResolution` és `VerticalResolution` értékeket az `ImageOrPrintOptions`‑ban. |
| PNG fájl üres vagy sérült | Hiányzó licenc, ami értékelő korlátozásokat okoz. | Alkalmazzon érvényes Aspose.Cells licencet a munkafüzet betöltése előtt (`License license = new License(); license.SetLicense("Aspose.Total.lic");`). |
| Fájlútvonal hibák (`FileNotFoundException`) | Hibás `YOUR_DIRECTORY` helyőrző. | Használjon abszolút útvonalakat vagy `Path.Combine(Environment.CurrentDirectory, "pivot.xlsx")`‑t. |

Ezeknek a problémáknak a kezelése biztosítja a zökkenőmentes **save excel picture file** élményt.

## Pro tipp: Exportálás közvetlenül memóriába

Előfordulhat, hogy a képet memóriában kell tartania (pl. egy web API‑nak feltölteni), a lemezre írás helyett:

```csharp
using (var ms = new MemoryStream())
{
    sheet.Pictures[0].RenderToImage(imageOptions, ms);
    // ms now contains the PNG bytes – you can send them over HTTP, store in DB, etc.
}
```

Az ugyanaz a **set image format png** logika érvényes; csak a fájlútvonalat cseréli egy stream‑re.

## Összegzés

Most már tudja, **how to export Excel chart** PNG fájlként az Aspose.Cells for .NET segítségével. A tutorial lefedte:

* A könyvtár telepítését
* A munkafüzet betöltését
* **Setting image format png**
* **Saving Excel chart image** lemezre
* Több diagram és gyakori hibák kezelése

Ezzel az alapokkal beépítheti a diagramexportot automatizált jelentésekbe, webszolgáltatásokba vagy asztali segédprogramokba. Következő lépésként fedezze fel a kapcsolódó témákat, például a **save excel picture file** JPEG‑ként (`ImageFormat.Jpeg`) vagy a diagramok PDF‑be konvertálását nyomtatási jelentésekhez.

Boldog kódolást!

## Mit érdemes még tanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [Convert Excel Pie Chart to Image Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)
- [Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/)
- [Export Excel Cells to Image Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}