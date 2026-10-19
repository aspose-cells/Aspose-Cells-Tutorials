---
category: general
date: 2026-09-15
description: Tanulja meg, hogyan ágyazhat be betűtípusokat SVG-be, és exportálhatja
  az Excel-diagramot PowerPointba, bemutatva az XLSX SVG-re és az XLSX PPTX-re konvertálását
  teljes kódrészletekkel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: hu
lastmod: 2026-09-15
og_description: Betűtípusok beágyazása SVG-be és Excel-diagram exportálása PowerPointba
  lépésről‑lépésre C# kóddal. XLSX gyorsan és megbízhatóan konvertálható SVG‑be és
  PPTX‑be.
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: Betűtípusok beágyazása SVG-be és Excel-diagram exportálása PowerPointba
  – teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hogyan ágyazzuk be a betűtípusokat SVG-be Excel-fájlok SVG- és PowerPoint-konvertálása
  során
url: /hu/net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan ágyazzunk be betűtípusokat SVG-be Excel-fájlok SVG‑re és PowerPoint‑ra konvertálásakor  

Ha **betűtípusokat kell beágyazni SVG-be** egy Excel-munkafüzet konvertálása során, ez az útmutató pontosan megmutatja, hogyan teheted meg. Megtanulod, hogyan **exportálj Excel-diagramot PowerPointba**, valamint hogyan **konvertálj XLSX‑t SVG‑re** és **konvertálj XLSX‑t PPTX‑re** szerkeszthető diagramokkal.  

Az Excel‑adatok programozott kezelése gyakran azt jelenti, hogy ugyanazt a vizuális tartalmat különböző fájlformátumok között kell mozgatni. A diagram manuális újraalkotása PowerPointban vagy a betűtípusok újbóli alkalmazása SVG‑ben hibára és időpazarlásra hajlamos. A tutorial végére egyetlen, újrahasználható C# kódrészletet kapsz, amely:

* Egy munkafüzetet SVG‑fájlként ment beágyazott betűtípusokkal és betűtípus‑variációs szelektorokkal.  
* Ugyanezt a munkafüzetet PPTX‑fájlként exportálja, ahol a diagram szerkeszthető marad.  

Az egyetlen előfeltétel a **Aspose.Cells for .NET** (2024‑x vagy újabb) legfrissebb verziója és egy .NET fejlesztői környezet, például a Visual Studio 2022.

---

## Amire szükséged lesz  

* .NET 6.0 vagy újabb (a kód .NET Framework 4.8‑on is működik).  
* Aspose.Cells for .NET NuGet csomag (`Install-Package Aspose.Cells`).  
* Egy Excel‑fájl (`input.xlsx`), amely legalább egy diagramot tartalmaz.  
* Írási jogosultság a kimeneti könyvtárban.  

---

## Betűtípusok beágyazása SVG‑be XLSX‑ről SVG‑re konvertáláskor  

A betűtípusok beágyazása biztosítja, hogy az SVG bármilyen eszközön helyesen jelenjen meg, még akkor is, ha a célrendszer nem rendelkezik az eredeti betűtípusokkal. A `SvgSaveOptions` osztály két zászlót biztosít, amelyek ezt lehetővé teszik: `EmbedFonts` és `FontVariationSelectors`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**Miért működik:**  
* `EmbedFonts = true` a betűtípus‑fájlokat az SVG `<defs>` szekciójába másolja, ezzel megszüntetve a külső függőségeket.  
* `FontVariationSelectors = true` hozzáadja a szükséges szelektorokat az OpenType funkciókat támogató betűtípusokhoz, megőrizve a glif‑variációkat, például a ligatúrákat.  

**Várt eredmény:** Nyisd meg a `WithFonts.svg` fájlt bármely modern böngészőben; a diagram vagy cellák szövege pontosan úgy jelenik meg, ahogy az Excel‑ben, még azokban a gépekben is, ahol a betűtípus nincs telepítve.

---

## Excel‑diagram exportálása PowerPointba szerkeszthető diagramokkal  

Amikor egy diagramot kell beágyazni egy PowerPoint‑diaba, de a címzettnek továbbra is szerkeszteni kell a diagram adatait, az Aspose.Cells `PptxSaveOptions` osztálya a `ExportEditableChart` zászlót kínálja.

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**Miért fontos:**  
A `ExportEditableChart` értékét `true`‑ra állítva a diagram Office Open XML diagramobjektumként kerül mentésre, nem statikus képként. Amikor megnyitod a `EditableChart.pptx` fájlt PowerPointban, jobb‑kattintással a diagramra → **Edit Data** (Adatok szerkesztése) lehetőséget választva módosíthatod a sorozatokat, mintha natív PowerPoint‑diagramról lenne szó.

**Ellenőrző lépések:**  

1. Nyisd meg az `EditableChart.pptx` fájlt PowerPointban.  
2. Keresd meg azt a diát, amely a diagramot tartalmazza.  
3. Válaszd a **Chart Tools → Design → Edit Data** menüpontot.  
4. Erősítsd meg, hogy megjelenik az Excel‑stílusú adat‑rács, és hogy módosíthatod az értékeket.

---

## XLSX‑ról SVG‑re konvertálás – teljes munkafolyamat összefoglalása  

Az alábbi kompakt változat egyesíti a betöltést, az opcionális adatmanipulációt és az SVG‑ként mentést. Akkor használd, ha csak az SVG‑kimenetre van szükséged.

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

A metódus hívása a következőképpen történik:

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**Szél eset tip:** Ha a munkafüzeted egyedi betűtípusokat tartalmaz, amelyek nincsenek telepítve a szerveren, a `Save` hívása előtt ágyazd be őket manuálisan. Használd a `FontInfoCollection`‑t a betűtípus‑fájlok hozzáadásához a `SvgSaveOptions` `CustomFonts` tulajdonságán keresztül (újabb Aspose.Cells kiadásokban elérhető).

---

## XLSX‑ról PPTX‑re konvertálás – a diagram szerkeszthetőségének megőrzése  

Az alábbi segédmetódus bemutatja az **XLSX‑ról PPTX‑re konvertálás** útvonalát, miközben biztosítja, hogy a diagram szerkeszthető maradjon.

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

Használat:

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**Gyakori kérdés:** *Mi van, ha a munkafüzet több munkalapot és diagramot is tartalmaz?*  
**Válasz:** Az Aspose.Cells alapértelmezés szerint az első munkalapot exportálja. További lapok bevonásához iterálj a `workbook.Worksheets` gyűjteményen, másold át minden diagramot egy új diára, és mentsd el az egyes diákot külön‑külön a Aspose.Slides `Presentation` objektumaival. Ez a haladó forgatókönyv meghaladja az egyszerű „munkafüzet mentése SVG‑ként” és „Excel‑diagram exportálása PowerPointba” folyamatot, de a fő zászlók változatlanok maradnak.

---

## Gyakorlati tippek és buktatók  

* **Teljesítmény:** A betűtípusok beágyazása növeli az SVG fájlméretét. Ha a méret kritikus, állítsd `EmbedFonts = false`‑ra, és támaszkodj web‑biztonságos betűtípusokra.  
* **Betűtípus‑licenc:** Győződj meg róla, hogy jogod van a betűtípusok beágyazásához; egyes kereskedelmi betűtípusok korlátozzák a beágyazást.  
* **Diagram‑kompatibilitás:** A szerkeszthető diagramok `chart.xml` részekként kerülnek mentésre a PPTX‑ben. Nagyon összetett diagramok (pl. 3‑D vagy kombinált diagramok) elveszíthetnek bizonyos stílusokat a PowerPoint‑ban történő szerkesztéskor. Teszteld a leggyakrabban használt diagramtípusokat.  
* **Verzió‑eltérések:** A `ExportEditableChart` zászló az Aspose.Cells 20.10 vagy újabb verzióját igényli. Régebbi verzió esetén a rendszer csendben raszteres képre vált.  
* **Szálbiztonság:** A `Workbook` objektumok nem szálbiztosak. Webszolgáltatás esetén kérésenként hozz létre új `Workbook` példányt.  

---

## Teljes vég‑től‑végig példakód  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

A program futtatása két fájlt hoz létre:

* **WithFonts.svg** – egy SVG, amely pontosan úgy jelenik meg, mint az Excel‑nézet, betűtípusokkal együtt.  
* **EditableChart.pptx** – egy PowerPoint‑prezentáció, ahol a diagram közvetlenül szerkeszthető.

---

## Összegzés  

Most már tudod, hogyan **ágyazz be betűtípusokat SVG‑be**, amikor **XLSX‑t SVG‑re konvertálsz**, és hogyan **exportáld az Excel‑diagramot PowerPointba**, miközben a diagram szerkeszthető marad. Ugyanez a kód tiszta módon bemutatja, hogyan **mentsd a munkafüzetet SVG‑ként** és hogyan **konvertáld XLSX‑t PPTX‑re** minimális erőfeszítéssel.  

Innen tovább felfedezheted a következő témákat:

* Egyedi betűtípusok programozott hozzáadása (`svgOptions.CustomFonts`).  
* Több munkafüzet kötegelt feldolgozása háttérszolgáltatásban.  
* Aspose.Slides használata többdiás PPTX‑fájlok létrehozásához, amelyek több Excel‑diagramot kombinálnak.  

Kísérletezz a beállításokkal, igazítsd a kódrészleteket a projektedhez, és élvezd a megbízható Excel‑to‑SVG/PPTX konverziót manuális utófeldolgozás nélkül. Jó kódolást!


## Mit érdemes legközelebb megtanulni?


Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek az API további funkcióinak elsajátításában és alternatív megvalósítási módok felfedezésében saját projektjeidben.

- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}