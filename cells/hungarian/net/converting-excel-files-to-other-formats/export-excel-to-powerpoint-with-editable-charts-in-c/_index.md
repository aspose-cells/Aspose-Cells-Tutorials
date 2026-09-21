---
category: general
date: 2026-09-21
description: Exportálja az Excelt PowerPointba szerkeszthető diagramokkal az Aspose.Cells
  segítségével. Kövesse ezt a lépésről‑lépésre útmutatót, hogy egy munkalapot PPTX
  formátumba konvertáljon, miközben a diagramok szerkeszthetőek maradnak.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- worksheet to powerpoint
- export excel chart pptx
- editable charts pptx
language: hu
lastmod: 2026-09-21
og_description: Exportálja az Excelt PowerPointba szerkeszthető diagramokkal az Aspose.Cells
  segítségével. Ismerje meg, hogyan konvertálhat egy munkalapot PPTX formátumba, miközben
  a diagramok teljes szerkeszthetőségét megőrzi.
og_image_alt: Screenshot of a PowerPoint slide showing an editable Excel chart after
  export
og_title: Excel exportálása PowerPointba szerkeszthető diagramokkal – C# oktatóanyag
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  headline: Export Excel to PowerPoint with editable charts in C#
  type: TechArticle
- description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  name: Export Excel to PowerPoint with editable charts in C#
  steps:
  - name: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
    text: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
  - name: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
    text: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
  - name: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
    text: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
  - name: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
    text: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel‑to‑PowerPoint
- PPTX export
title: Excel exportálása PowerPointba szerkeszthető diagramokkal C#‑ban
url: /hu/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-editable-charts-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel exportálása PowerPointba szerkeszthető diagramokkal C#-ban

Az Excel exportálása PowerPointba szerkeszthető diagramokkal gyakori igény, amikor a táblázati vizualizációkat prezentációkban szeretnénk újra felhasználni. Ez az útmutató bemutatja, hogyan **exportálhatja az Excelt PowerPointba**, miközben megőrzi a diagramok szerkeszthetőségét, az Aspose.Cells for .NET használatával.

Tanulni fogja, hogyan:

* Betölteni egy meglévő munkafüzetet, amely diagramokat és szövegdobozokat tartalmaz.  
* Beállítani a PPTX exportálási beállításokat úgy, hogy a diagramok és alakzatok szerkeszthetőek maradjanak.  
* Átalakítani egy adott munkalapot egy PowerPoint fájlba, amely megnyitható és szerkeszthető a Microsoft PowerPointban.

Az útmutató feltételezi, hogy alapvető C# ismeretekkel és egy friss .NET verzióval (≥ .NET 6) rendelkezik. Az Aspose.Cells előzetes tapasztalata nem szükséges.

---

## Export Excel to PowerPoint – áttekintés

A **export Excel to PowerPoint** mögötti alapgondolat az, hogy minden munkalapot képforrásként kezelünk, amely PPTX diára renderelhető. Az `ExportChartAsEditableText` és `ExportShapeAsEditableText` jelzők átkapcsolásával az Aspose.Cells a diagram alapszámait PowerPoint rajzobjektumokként írja ki, nem pedig lapos bitmapként. Ez a végeredményként kapott diát teljesen szerkeszthetővé teszi – akárcsak egy közvetlenül PowerPointban létrehozott diagram.

> **Miért használjunk szerkeszthető diagramokat?**  
> A szerkeszthető diagramok lehetővé teszik a bemutatók számára, hogy adatokat, színeket vagy címkéket módosítsanak az eredeti Excel fájl visszaállítása nélkül, felgyorsítva az utolsó pillanatban történő változtatásokat és zökkenőmentessé téve a prezentációs munkafolyamatot.

## Munkalap átalakítása PowerPointba (worksheet to PowerPoint)

Az alábbiakban egy teljes, futtatható példa látható, amely bemutatja a **worksheet to PowerPoint** átalakítást.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the chart and textbox
            // Replace YOUR_DIRECTORY with the actual folder path on your machine.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Configure PPTX export options to keep charts and shapes editable
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,               // Target format: PPTX
                ExportChartAsEditableText = true,           // Enable editable charts
                ExportShapeAsEditableText = true            // Enable editable shapes/textboxes
            };

            // Step 3: Export the first worksheet (index 0) to a PowerPoint file
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";
            workbook.Worksheets[0].ConvertToImage(exportOptions, outputPath);

            Console.WriteLine($"Worksheet successfully exported to {outputPath}");
        }
    }
}
```

### Az egyes lépések magyarázata

| Lépés | Mit csinál a kód | Miért fontos a **export excel chart pptx** szempontjából |
|------|-------------------|----------------------------------------------|
| 1️⃣   | `input.xlsx` betölti egy `Aspose.Cells.Workbook` objektumba. | A munkafüzet hozzáférést biztosít a exportálni kívánt diagramokhoz. |
| 2️⃣   | `ExportType` értékét `Pptx`-re állítja, és engedélyezi az `ExportChartAsEditableText` és `ExportShapeAsEditableText` beállításokat. | Ezek a jelzők a **editable charts pptx** kulcsa – azt mondják a könyvtárnak, hogy a diagram geometriát PowerPoint rajzobjektumként írja ki raster képek helyett. |
| 3️⃣   | A `ConvertToImage` metódust hívja az első munkalapon, és `Worksheet.pptx`-t hoz létre. | A metódus végrehajtja a **export excel to powerpoint** műveletet, és egy PPTX fájlt ír ki, amely közvetlenül megnyitható a PowerPointban. |

> **Pro tipp:** Ha *több* munkalapot kell exportálni, iteráljon a `workbook.Worksheets`-en, és minden egyeshez hívja meg a `ConvertToImage`-t, opcionálisan az output fájlokat `Sheet1.pptx`, `Sheet2.pptx`, stb. néven nevezve.

## Szerkeszthető diagramok engedélyezése a PPTX-ben (export excel chart pptx)

Ha az `ExportChartAsEditableText` értéke `true`, az Aspose.Cells minden diagramot `<a:graphic>` elemek gyűjteményeként ír a PPTX XML-be. A PowerPoint ezeket az elemeket natív diagramobjektumként kezeli, amelyet duplán kattintva megnyithat a diagram szerkesztőben.

**Gyakori buktatók**

* **Hiányzó Aspose.Cells licenc** – Licenc nélkül a könyvtár vízjelet ad a kimenethez. Regisztráljon licencet a program elején (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`).  
* **Nem támogatott diagramtípusok** – Bár a legtöbb 2‑D diagram (oszlop, vonal, kör) teljesen szerkeszthető, egyes összetett 3‑D vagy kombinált diagramok képekké konvertálódhatnak. Tesztelje a konkrét diagramtípusokat, ha a teljes szerkeszthetőségre támaszkodik.  
* **Nagy munkalapok** – Nagyon nagy munkalapok exportálása jelentős memóriát fogyaszthat. Fontolja meg az `ExportMaxRows` vagy `ExportMaxColumns` használatát az `ImageOrPrintOptions`-ban, hogy korlátozza a konvertálandó területet.

## Tippek a diagramok szerkeszthető állapotának megőrzéséhez (editable charts pptx)

1. **Diagram adat tartományok megőrzése** – Győződjön meg arról, hogy a diagram adatforrása ugyanabban a munkalapban van, amelyet exportál. A munkalapok közötti hivatkozások statikus értékekké alakulnak a PPTX-ben.  
2. **Használja a legújabb Aspose.Cells verziót** – Az új kiadások javítják a további diagramfunkciók támogatását és kijavítják a PPTX exportálással kapcsolatos széljegyzet hibákat.  
3. **Ellenőrizze a kimenetet** – Az átalakítás után nyissa meg a generált PPTX-et a PowerPointban, és ellenőrizze, hogy szerkesztheti-e a diagram címét, sorozatait és tengelycímkéit. Ha bármely elem képként jelenik meg, ellenőrizze újra, hogy az `ExportChartAsEditableText` engedélyezve van-e, és hogy a diagramtípus támogatott-e.  
4. **Kötegelt feldolgozás** – Automatizálási esetekben (pl. diavetítés generálása számos Excel jelentésből) csomagolja az átalakítási logikát egy olyan metódusba, amely `Workbook`, `int worksheetIndex` és `string outputPath` paramétereket fogad. Ez elkülöníti a **export excel to powerpoint** munkafolyamatot, és újrahasználhatóvá teszi.

## Teljes működő példa összefoglaló

Mindent összevonva, itt van a minimális program, amelyet beilleszthet egy új .NET konzolprojektbe:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Register license (optional but removes evaluation watermark)
            // var license = new License();
            // license.SetLicense("Aspose.Cells.lic");

            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";

            Workbook workbook = new Workbook(inputPath);

            ImageOrPrintOptions options = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,
                ExportChartAsEditableText = true,
                ExportShapeAsEditableText = true
            };

            workbook.Worksheets[0].ConvertToImage(options, outputPath);

            Console.WriteLine($"Export complete: {outputPath}");
        }
    }
}
```

**Várható eredmény**

* A `Worksheet.pptx` nevű fájl megjelenik a `YOUR_DIRECTORY`-ben.  
* A fájl megnyitása a Microsoft PowerPointban egy olyan diát mutat, amely tartalmazza az eredeti diagramot és a szövegdobozokat.  
* A diagram duplán kattintva megnyílik a PowerPoint diagram szerkesztője, lehetővé téve a sorozatértékek, színek vagy tengelycímkék módosítását – ez megerősíti, hogy a **editable charts pptx** funkció a kívánt módon működik.

## Következtetés

Most már egy teljes megoldása van a **export Excel to PowerPoint** feladatra, amely a diagramokat szerkeszthető állapotban tartja. Az `ImageOrPrintOptions` `ExportChartAsEditableText` és `ExportShapeAsEditableText` beállításával a konverziós folyamat egy natív PPTX fájlt hoz létre, ahol a diagramok úgy viselkednek, mint a PowerPointban közvetlenül létrehozottak.  

Innen tovább:

* Bővítse a kódot, hogy több munkalapot kezeljen (mindegyikhez **worksheet to PowerPoint**).  
* Kombinálja az exportálást más Aspose.Cells funkciókkal, például diacímek hozzáadásával vagy képek beillesztésével.  
* Fedezze fel a kapcsolódó témákat, például a **export Excel chart PPTX** egyedi témákkal vagy a teljes diakészlet generálási folyamatának automatizálását.

Nyugodtan kísérletezzen különböző diagramtípusokkal, adjon hozzá adatcímkéket, vagy integrálja ezt a munkafolyamatot egy nagyobb jelentési rendszerbe. Jó kódolást!

## Mit érdemes következőként megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}