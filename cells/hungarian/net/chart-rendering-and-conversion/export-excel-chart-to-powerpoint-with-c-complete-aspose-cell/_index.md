---
category: general
date: 2026-08-04
description: Exportálja az Excel-diagramot PowerPointba az Aspose.Cells használatával
  C#‑ban. Kövesse ezt a lépésről‑lépésre útmutatót az Excel‑PowerPoint átalakításhoz,
  és tartsa szerkeszthetőnek az alakzatokat.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: hu
lastmod: 2026-08-04
og_description: Exportálja az Excel-diagramot PowerPointba az Aspose.Cells segítségével
  C#-ban. Tanulja meg, hogyan hozhat létre szerkeszthető PPTX fájlt, őrizze meg a
  diagram adatait, és automatizálja az Excel‑PowerPoint konverziót.
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: Excel-diagram exportálása PowerPointba C#-vel – teljes Aspose.Cells útmutató
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: Excel-diagram exportálása PowerPointba C#-val – teljes Aspose.Cells útmutató
url: /hu/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel diagram PowerPointba C#‑val – teljes Aspose.Cells útmutató

Ha **Excel diagramot kell exportálni PowerPointba**, ez a bemutató megmutatja, hogyan teheti ezt meg Aspose.Cells és Aspose.Slides segítségével C#‑ban. Teljesen szerkeszthető PPTX‑et kap, amely megőrzi a diagram adatait és alakjait, így a konverzió készen áll a további tervezési munkára.

Diagramok exportálása Excelből PowerPointba gyakori igény automatizált jelentéskészítési folyamatok, értékesítési prezentációk vagy képzési anyagok készítésekor. Ebben az útmutatóban megtanulja a pontos lépéseket egy **Excel‑ról‑PowerPoint konverzió** elvégzéséhez, amely minden diagram elemet szerkeszthetővé tesz. Kézi másolás‑beillesztés nem szükséges, a kód .NET 6+ és a klasszikus .NET Framework esetén is működik.

## Előfeltételek

- Érvényes Aspose.Cells licenc (vagy egy ingyenes értékelő kulcs)  
- Aspose.Slides for .NET hozzáadva a projekthez (a könyvtár kezeli a PPTX kimenetet)  
- .NET 6 SDK vagy újabb telepítve  
- Egy Excel munkafüzet, amely legalább egy diagramot tartalmaz (ebben a példában a `Shapes.xlsx`‑t használjuk)  

A NuGet csomagokat a következő parancsokkal telepítheti:

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## 1. lépés: Az Excel munkafüzet betöltése

Az első művelet a munkafüzet megnyitása, amely a exportálandó diagramot tartalmazza. A `Workbook` osztály képviseli az egész Excel fájlt.

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**Miért fontos:** A munkafüzet betöltése hozzáférést biztosít a munkalapokhoz, diagramokhoz és formázáshoz. Az Aspose.Cells a fájlt Office telepítése nélkül olvassa, ami könnyűsúlyúvá és szerver‑baráttá teszi a megoldást.

## 2. lépés: A munkalap kiválasztása és a nyomtatási terület meghatározása

Egy munkalap sok diagramot tartalmazhat, de általában egy konkrét területet exportálunk. A `PrintArea` beállítása megmondja az Aspose.Cells‑nek, mely cellákat (beleértve a diagramokat) kell renderelni.

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**Miért fontos:** Az export korlátozása egy meghatározott nyomtatási területre megakadályozza a felesleges üres diák létrejöttét, és kis méretű PPTX‑et eredményez. A területet a diagram pontos tartományához igazíthatja.

## 3. lépés: Exportálási beállítások konfigurálása szerkeszthető PPTX‑hez

Az Aspose.Cells az `ImageOrPrintOptions` osztályt használja a kimeneti formátum és a szerkeszthetőség szabályozására. Az `ImageFormat` `ImageFormat.Pptx`‑re állítása PowerPoint fájlt hoz létre, míg az `ExportEditableShapes = true` megőrzi a diagram objektumokat szerkeszthető alakzatokként.

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**Miért fontos:** Az `ExportEditableShapes` jelző a **szerkeszthető alakzatok PowerPointban** eredmény kulcsa. Enélkül a diagram képként kerül rasterizálásra, és elveszíti a későbbi adatpont‑ vagy stílusmódosítás lehetőségét.

## 4. lépés: A munkalap mentése PowerPoint prezentációként

Végül hívja meg a `Save` metódust a `Workbook` objektumon. A `SaveFormat.Pptx` enum azt mondja az Aspose.Cells‑nek, hogy PowerPoint fájlt hozzon létre.

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

A kód befejezése után nyissa meg a `ShapesExport.pptx`‑et PowerPointban. Egy olyan diát fog látni, amely az eredeti Excel diagramot natív PowerPoint diagramobjektumként tartalmazza. Kattintson duplán a diagramra az adatok szerkesztéséhez, színek módosításához vagy animációk hozzáadásához – mintha közvetlenül PowerPointban hozta volna létre.

### Várható kimenet

| Fájlnév                | Dia tartalma                                                                 |
|-----------------------|------------------------------------------------------------------------------|
| `ShapesExport.pptx`   | A `Shapes.xlsx`‑ből származó diagram, szerkeszthető PowerPoint diagramként, tengelycímkékkel, jelmagyarázattal és adat sorozatokkal. |

## Teljes, futtatható példa

Az alábbi teljes programot másolhatja, beillesztheti és futtathatja. Tartalmazza az összes szükséges `using` utasítást, hibakezelést és megjegyzéseket.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**Az egyes blokkok magyarázata**

| Blokk | Cél |
|-------|-----|
| `using` direktívák | Betölti az Aspose.Cells és Aspose.Slides névtereket. |
| `Workbook workbook = new Workbook(excelPath);` | Betölti az Excel fájlt Office telepítése nélkül. |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | Korlátozza az exportot a diagramot tartalmazó területre. |
| `ImageOrPrintOptions` | Beállítja a PPTX kimenetet és engedélyezi az **Aspose.Cells PPTX exportot** szerkeszthető alakzatokkal. |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | A PowerPoint fájlt lemezre írja. |
| `try / catch` | Alapvető hibakezelést biztosít hiányzó fájlok vagy licencproblémák esetén. |

A program futtatása egy PowerPoint diát hoz létre, amelyet megnyithat a Microsoft PowerPointban, a Google Slides‑ben (konvertálás után) vagy bármely kompatibilis megjelenítőben.

## Általános variációk és szélsőséges esetek

### Több munkalap exportálása

Ha minden munkalaphoz külön diát szeretne, iteráljon a `workbook.Worksheets`‑en, és hívja meg a `Save`‑t egyedi fájlnévvel minden iterációban.

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### Diakialakítás vezérlése

Az Aspose.Slides lehetővé teszi egy egyedi diakialakítás hozzáadását az export után. Hozzon létre egy új prezentációt, importálja a generált diát, majd alkalmazzon egy mester‑témát.

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### Diagramok kezelése külső adatforrásokkal

Ha egy diagram olyan adat tartományra hivatkozik, amely kívül esik a meghatározott nyomtatási területen, bővítse a `PrintArea`‑t, hogy tartalmazza ezeket a cellákat. Ellenkező esetben a diagram adat sorozatai elveszhetnek az export során.

### Licencelési szempontok

Az Aspose könyvtárak értékelő módban vízjellel működnek. A vízjel eltávolításához állítsa be a licencet minden API hívás előtt:

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

Ugyanezt tegye meg az Aspose.Slides‑nél, ha annak fejlett funkcióit használja.

## Pro tippek

- **Exportálási beállítások újrahasználata:** Hozzon létre egyetlen `ImageOrPrintOptions` példányt, és rendelje minden munkalaphoz, hogy a kód DRY maradjon.  
- **Kötegelt feldolgozás:** Nagy‑léptékű jelentéskészítés esetén kombinálja ezt az exportlogikát egy háttér‑munkával vagy Azure Function‑nel, hogy igény szerint PPTX fájlokat generáljon.  
- **Teljesítmény:** Ha csak a diagram képe szükséges (nem szerkeszthető), állítsa `ExportEditableShapes = false`‑ra. Ez csökkenti a memóriahasználatot és felgyorsítja a konverziót.  
- **Tesztelés:** Ellenőrizze a generált PPTX‑et mind Windows, mind macOS PowerPoint telepítéseken, mivel egyes megjelenítési sajátosságok platformonként eltérhetnek.  

## Összegzés

Most már rendelkezik egy teljes, vég‑től‑végig megoldással a **Excel diagram PowerPointba exportálásához** C#‑ban. A bemutató lefedte a munkafüzet betöltését, a nyomtatási terület kiválasztását, a **Aspose.Cells PPTX export** konfigurálását **szerkeszthető alakzatokkal PowerPointban**, és a végeredmény mentését egy teljesen szerkeszthető PPTX fájlként.  

Innen tovább felfedezheti a további **Excel‑ról‑PowerPoint konverzió** forgatókönyveket, például kötegelt exportálást, egyedi diakialakításokat vagy a folyamat integrálását egy web‑API‑ba. Kísérletezzen különböző diagramtípusokkal, adjon hozzá képeket, vagy kombináljon több munkalapot egyetlen prezentációba, hogy a kimenetet az üzleti igényeihez igazítsa.

Készen áll a jelentéskészítési munkafolyamat automatizálására? Próbálja ki a forrásfájl cseréjét, a nyomtatási terület módosítását, és integrálja a kódot meglévő .NET szolgáltatásaiba. Boldog kódolást!

## Mi legyen a következő tanulnivaló?

Az alábbi bemutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Export Excel Cells to Image Using Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}