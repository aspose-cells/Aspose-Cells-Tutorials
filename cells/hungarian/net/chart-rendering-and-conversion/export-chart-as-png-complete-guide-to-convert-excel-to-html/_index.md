---
category: general
date: 2026-06-30
description: Exportálja a diagramot PNG formátumban, miközben az Excelt HTML-re konvertálja
  az Aspose.Cells segítségével. Tanulja meg, hogyan ágyazhat be képeket Base64‑ként,
  és mentse a munkafüzetet HTML‑ként percek alatt.
draft: false
keywords:
- export chart as png
- convert excel to html
- embed images as base64
- save workbook as html
- export excel chart to png
language: hu
og_description: Exportálja a diagramot PNG formátumban, és ágyazza be a képeket Base64-ként
  az Excel HTML-re konvertálása során. Kövesse ezt a lépésről‑lépésre C#‑os útmutatót,
  hogy könnyedén mentse a munkafüzetet HTML‑ként.
og_title: Diagram exportálása PNG formátumban – Excel konvertálása HTML-re az Aspose.Cells
  segítségével
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  headline: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  name: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  steps:
  - name: Open Visual Studio and create a new **Console App** (`dotnet new console`).
    text: Open Visual Studio and create a new **Console App** (`dotnet new console`).
  - name: 'Add the Aspose.Cells NuGet package:'
    text: 'Add the Aspose.Cells NuGet package:'
  - name: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
    text: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
  - name: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
    text: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
  - name: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
    text: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
  - name: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
    text: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Diagram exportálása PNG‑ként – Teljes útmutató az Excel HTML‑re konvertálásához
  az Aspose.Cells segítségével
url: /hu/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Chart as PNG – Teljes útmutató az Excel HTML‑re konvertálásához az Aspose.Cells segítségével

Gondoltad már, hogyan **export chart as PNG** közvetlenül egy Excel munkafüzetből, miközben az egész lapot tiszta, reszponzív HTML‑vé alakítod? Nem vagy egyedül. Sok fejlesztő akad el, amikor web‑kész jelentésre van szüksége, amely diagramokat mutat különálló képfájlok kezelése nélkül. A jó hír, hogy az Aspose.Cells ezt könnyedén megoldja.

Ebben a bemutatóban végigvezetünk a pontos lépéseken, hogy **convert Excel to HTML**, **embed images as Base64**, és végül **save workbook as HTML** – mindezt úgy, hogy minden diagram PNG képként kerül mentésre. A végére egyetlen HTML fájlt kapsz, amelyet bármely weboldalba beilleszthetsz, és minden diagram azonnal megjelenik, extra erőforrások nélkül.

## What You’ll Learn

- Hogyan töltsünk be egy meglévő munkafüzetet, amely már tartalmaz diagramokat.  
- Mely `HtmlSaveOptions` jelzők szabályozzák a képexportálást, a diagramformátumot és a reszponzivitást.  
- A pontos kód, amely **export chart as PNG** és beágyazza ezeket a PNG‑ket Base64 karakterláncokként.  
- Hogyan **save workbook as HTML** egyetlen metódushívással.  
- Tippek a gyakori problémák, például hiányzó diagramképek vagy túl nagy Base64 karakterláncok hibaelhárításához.  

**Prerequisites:**  
- .NET 6+ (vagy .NET Framework 4.6+) telepítve.  
- Érvényes Aspose.Cells licenc (vagy ideiglenes értékelő kulcs).  
- Alapvető ismeretek C#‑ról és Visual Studio‑ról (vagy a kedvenc IDE‑dról).  

Ha bármelyik ismeretlen, állj meg egy pillanatra és állítsd be őket; a további útmutató feltételezi, hogy készen állsz.

---

## Step 1: Set Up Your Project and Install Aspose.Cells

Mielőtt **export chart as PNG**-t tudnánk végrehajtani, szükségünk van egy C# projektre, amely hivatkozik az Aspose.Cells könyvtárra.

1. Nyisd meg a Visual Studio‑t és hozz létre egy új **Console App**‑ot (`dotnet new console`).  
2. Add hozzá az Aspose.Cells NuGet csomagot:

```bash
dotnet add package Aspose.Cells
```

3. (Opcionális) Ha van licencfájlod, helyezd el a projekt gyökerében és aktiváld futásidőben:

```csharp
// Activate license – skip this line if you’re using the trial version
Aspose.Cells.License license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

> **Pro tip:** Tartsd a licencfájlt a forráskódtáron kívül. Használj környezeti változókat vagy biztonságos titkos tárolókat a production környezetben.

---

## Step 2: Load the Workbook That Contains the Chart

Most betöltjük azt az Excel fájlt, amely már tartalmazza a diagramot, amelyet **export chart as PNG**‑ként szeretnénk menteni.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;   // Needed for ImageFormat enum

// Path to the source workbook – change this to your actual file location
string sourcePath = @"C:\Reports\ReportWithChart.xlsx";

// Load the workbook
Workbook workbook = new Workbook(sourcePath);
```

> **Why this matters:** A munkafüzet korai betöltése hozzáférést biztosít az összes munkalaphoz, diagramhoz és beágyazott objektumhoz. Ha a munkafüzet betöltése sikertelen, a későbbi **export chart to PNG** lépés sosem fut le.

---

## Step 3: Configure HTML Save Options

A megoldás szíve a `HtmlSaveOptions`. Néhány tulajdonság beállításával:

- **ExportChartImageFormat = ImageFormat.Png** → biztosítja, hogy minden diagram PNG legyen.  
- **ExportImagesAsBase64 = true** → beágyazza a PNG adatokat közvetlenül a HTML‑be, kiküszöbölve a külső fájlokat.  
- **IsResponsive = true** → a generált táblázatok alkalmazkodnak a mobil képernyőkhöz.  
- **ExportPrintingHeadersFooters = false** → eltávolítja a felesleges nyomtatási metaadatokat.  

A teljes konfiguráció:

```csharp
// Create HTML save options and fine‑tune them
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // 1️⃣ Embed PNG/JPEG images directly as Base64 strings
    ExportImagesAsBase64 = true,

    // 2️⃣ Force chart images to be saved as PNG files
    ExportChartImageFormat = ImageFormat.Png,

    // 3️⃣ Omit printing headers/footers for a cleaner web view
    ExportPrintingHeadersFooters = false,

    // 4️⃣ Generate responsive tables for mobile friendliness
    IsResponsive = true,

    // 5️⃣ Target modern browsers with HTML5
    HtmlVersion = HtmlVersion.Html5
};
```

### Why These Settings?

- **ExportChartImageFormat = ImageFormat.Png** az egyetlen módja annak, hogy veszteségmentes, web‑biztonságos diagramképet kapjunk.  
- **ExportImagesAsBase64 = true** azt jelenti, hogy **embed images as Base64**, ami tökéletes e‑mail jelentésekhez vagy egy‑fájlos telepítésekhez.  
- **IsResponsive = true** megoldja a gyakori panaszt: a táblázatok túlcsordulnak okostelefonokon.  
- **ExportPrintingHeadersFooters = false** könnyűsúlyú HTML‑t eredményez – nincs rejtett nyomtatási információ, amely a weben soha nem kerül felhasználásra.  

---

## Step 4: Save the Workbook as HTML

Az opciók beállítása után egyetlen hívás elvégzi a **convert excel to html** és a **export chart as PNG** feladatot a háttérben.

```csharp
// Destination HTML file – adjust the folder as needed
string outputPath = @"C:\Reports\Report.html";

// Save the workbook using the configured options
workbook.Save(outputPath, htmlOptions);
```

Amikor ez a sor befejeződik, egy `Report.html` nevű fájlod lesz. Nyisd meg bármely böngészőben, és láthatod:

- Az összes munkalap adatát tiszta HTML táblázatokként.  
- Minden diagramot beágyazott PNG képként (köszönhetően a Base64 beágyazásnak).  
- Nincsenek extra képfájlok a HTML mellett.  

### Expected Output

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Report</title>
    <style>
        /* Aspose.Cells generated responsive CSS */
    </style>
</head>
<body>
    <table class="aspose">
        <!-- Table rows here -->
    </table>

    <!-- Example of an embedded chart image -->
    <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA..." alt="Chart 1" />
</body>
</html>
```

Vedd észre a `src="data:image/png;base64,..."` attribútumot – ez a **embed images as base64** varázslat. Nem jönnek létre külön `.png` fájlok a lemezen.

---

## Step 5: Verify the PNG Export and Tweak If Needed

Néha egy diagram kicsit eltorzul a konverzió után, különösen ha egyedi betűtípusokat vagy összetett színátmeneteket használ. Így ellenőrizheted:

1. Nyisd meg a generált HTML‑t Chrome‑ban. Jobb‑kattints a diagram képre és válaszd a **Open image in new tab** lehetőséget. Az URL továbbra is `data:image/png;base64,`‑vel kezdődik.  
2. Ha a kép elmosódott, fontold meg a diagram felbontásának növelését mentés előtt:

```csharp
htmlOptions.ImageResolution = 300; // DPI – higher values = sharper PNGs
```

3. Azoknál a diagramoknál, amelyek külső adatforrásokra támaszkodnak, győződj meg róla, hogy a munkafüzet teljesen frissítve van mentés előtt:

```csharp
workbook.CalculateFormula(); // Force recalculation
```

Ezek a finomhangolások biztosítják, hogy a **export excel chart to png** lépés éles, termék‑kész grafikát adjon.

---

## Step 6: Deploy the HTML Anywhere

Mivel minden kép be van ágyazva, most már:

- Elküldheted a HTML‑t egyetlen csatolmányként e‑mailben.  
- Beillesztheted a HTML‑t egy nyers kódot elfogadó CMS‑be.  
- Hosztolhatod statikus oldalként anélkül, hogy hiányzó PNG fájlok miatt aggódnál.  

Ha valaha is külön PNG fájlokra lenne szükséged (például későbbi PDF‑hez), átkapcsolhatod az `ExportImagesAsBase64`‑t `false`‑ra, és megadhatod a `HtmlSaveOptions`‑nak a képek kimeneti mappáját.

```csharp
htmlOptions.ExportImagesAsBase64 = false;
htmlOptions.ImageFolder = @"C:\Reports\Images";
```

Ekkor a HTML külső PNG fájlokra hivatkozik, továbbra is biztosítva a **export chart as png** funkciót, de egyedi képfájlokat is kapva egyéb felhasználásokhoz.

---

## Common Pitfalls & How to Avoid Them

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Chart missing from HTML | `ExportChartImageFormat` maradt alapértelmezett (`Jpeg`) és a böngésző blokkolja a vegyes tartalmat. | Állítsd `ExportChartImageFormat = ImageFormat.Png`‑ra. |
| HTML file huge (several MB) | Nagy diagramok vagy sok nagy felbontású kép beágyazva Base64‑ként. | Csökkentsd az `htmlOptions.ImageResolution`‑t vagy tömörítsd a diagramot Excelben a konverzió előtt. |
| Tables overflow on mobile | `IsResponsive` nincs engedélyezve. | Győződj meg róla, hogy `IsResponsive = true` a `HtmlSaveOptions`‑ban. |
| Base64 strings contain newline characters | Régebbi .NET verziók hosszú karakterláncokat tördelnek. | Frissíts .NET 6+ verzióra vagy állítsd `htmlOptions.ExportBase64StringInOneLine = true`. |

---

## Bonus: Wrap It All in a Reusable Method

Ha ezt a konverziót gyakran kell elvégezned, csomagold be a logikát egy újrahasználható metódusba:

```csharp
public static void ConvertExcelToHtmlWithPngCharts(string excelPath, string htmlPath)
{
    // Load workbook
    Workbook wb = new Workbook(excelPath);

    // Prepare options
    HtmlSaveOptions opts = new HtmlSaveOptions
    {
        ExportImagesAsBase64 = true,
        ExportChartImageFormat = ImageFormat.Png,
        ExportPrintingHeadersFooters = false,
        IsResponsive = true,
        HtmlVersion = HtmlVersion.Html5,
        ImageResolution = 150 // reasonable default DPI
    };

    // Force recalculation for up‑to‑date charts
    wb.CalculateFormula();

    // Save as HTML
    wb.Save(htmlPath, opts);
}
```

Most már bárhonnan meghívhatod a `ConvertExcelToHtmlWithPngCharts(@"C:\Reports\MyFile.xlsx", @"C:\Reports\MyFile.html");` metódust a kódbázisodban.

---

## Conclusion

Most már elsajátítottad, hogyan **export chart as PNG** miközben **convert Excel to HTML**, **embed images as Base64**, és **save workbook as HTML** az Aspose.Cells segítségével. A lényeg, hogy néhány jól megválasztott `HtmlSaveOptions` beállítás egy önálló, minden eszközön működő HTML fájlt eredményez – extra PNG fájlok vagy rendezetlen mappák nélkül.

Készen állsz a következő kihívásra? Próbáld ki a **export excel chart to PNG** kombinálását PDF generálással, vagy kísérletezz egyedi CSS‑szel a táblázatok további stílusozásához. A lehetőségek csak a képzeleted határain belül vannak, ha programozottan kezeled az adatot és a megjelenítést.

Nyugodtan hagyj megjegyzést, ha elakadsz, vagy oszd meg, hogyan alkalmaztad ezt a mintát a saját projektjeidben. Boldog kódolást!

## What Should You Learn Next?

A következő bemutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódpéldákat lépésről‑lépésre magyarázatokkal, hogy segítsenek további API‑funkciók elsajátításában és alternatív megvalósítási megközelítések felfedezésében a saját projektjeidben.

- [Export Excel to HTML Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/export-excel-html-aspose-cells-net/)
- [Export Excel to HTML Without Frame Scripts Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-to-html-aspose-cells-net/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}