---
category: general
date: 2026-07-14
description: Mentse az Excel fájlt gyorsan HTML formátumba, és tanulja meg, hogyan
  konvertálja az Excelt teljes formázással HTML-re. Exportálja az Excelt formázással
  az Aspose.Cells segítségével percek alatt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as html
- convert excel to html
- export excel with formatting
- Aspose.Cells HTML export
- Grid.js number formatting
language: hu
lastmod: 2026-07-14
og_description: Mentse el az Excelt azonnal HTML-ként. Ez az útmutató bemutatja, hogyan
  konvertálja az Excelt HTML-re, miközben megőrzi a stílusokat, és engedélyezi a Grid.js
  számformázását.
og_image_alt: Screenshot of a spreadsheet saved as HTML using Aspose.Cells – save
  excel as html example
og_title: Excel mentése HTML-ként – Lépésről lépésre exportálás teljes formázással
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  headline: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  type: TechArticle
- description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  name: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  steps:
  - name: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
    text: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
  - name: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
    text: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
  - name: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
    text: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
  - name: '**Browser console clean?** No JavaScript errors related to Grid.js.'
    text: '**Browser console clean?** No JavaScript errors related to Grid.js.'
  type: HowTo
tags:
- Excel
- HTML
- Aspose.Cells
title: Excel mentése HTML-ként – Teljes útmutató az Excel formázott exportálásához
url: /hu/net/exporting-excel-to-html-with-advanced-options/save-excel-as-html-complete-guide-to-export-excel-with-forma/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel mentése HTML‑ként – Teljes útmutató az Excel formázott exportálásához

Gondolkodtál már azon, hogyan **mentheted az Excelt HTML‑ként** anélkül, hogy elveszítenéd a színeket, szegélyeket vagy a számformátumokat? Nem vagy egyedül. Sok jelentési helyzetben egy web‑kész nézetre van szükség a munkafüzetből, és a leggyorsabb módja, ha a fájlt közvetlenül HTML‑re exportálod.  

Ebben az útmutatóban végigvezetünk a pontos lépéseken, hogy **Excel‑t HTML‑re konvertálj** az Aspose.Cells segítségével, engedélyezd a Grid.js számformázását, és biztosítsd, hogy a kimenet pontosan úgy nézzen ki, mint az eredeti táblázat. A végére egy azonnal használható HTML‑fájlt kapsz, amelyet bármely webszerverről kiszolgálhatsz.

## Mit fogsz megtanulni

- Előkövetelmények és csomagtelepítés  
- Létező munkafüzet betöltése (vagy dinamikus létrehozása)  
- A `HtmlSaveOptions` konfigurálása a tökéletes vizuális hűséghez  
- `GridJsOptions.EnableNumberFormat` engedélyezése a numerikus stílusok megőrzéséhez  
- A fájl mentése és az eredmény ellenőrzése  

Ha már valaha próbáltad **az Excel formázott exportálását** egy általános CSV kiírással, tudod, milyen frusztráló lehet, amikor a számok egyszerű szöveggé válnak. Ez az útmutató elkerüli ezt a csapdát.

---

## Előkövetelmények – Fejlesztőkörnyezet beállítása

Mielőtt a kódba merülnénk, győződj meg róla, hogy rendelkezel a következőkkel:

| Követelmény | Miért fontos |
|-------------|----------------|
| .NET 6.0 vagy újabb (az útmutató .NET 6‑ot használ) | Modern API‑k és jobb teljesítmény |
| Visual Studio 2022 (vagy VS Code C# kiegészítővel) | Kényelmes szerkesztés és hibakeresés |
| Aspose.Cells for .NET NuGet csomag | A könyvtár, amely a `HtmlSaveOptions` és `GridJsOptions` működését biztosítja |
| Egy minta Excel fájl (`sample.xlsx`) vagy egy kódból generált munkafüzet | A forrás, amelyet konvertálni fogsz |

Telepítsd az Aspose.Cells‑t a következő parancs segítségével a Package Manager Console‑ban:

```powershell
Install-Package Aspose.Cells
```

> **Pro tipp:** Ha CI pipeline‑on vagy, add hozzá ugyanazt a `dotnet add package` sort a build szkriptedhez, hogy a függőség mindig jelen legyen.

---

## 1. lépés: Munkafüzet betöltése vagy létrehozása

Betölthetsz egy meglévő fájlt, vagy programozottan építhetsz egy újat. Íme egy minimális példa, amely néhány formázott cellát hoz létre, hogy láthasd a formázás megmaradását az exportálás során.

```csharp
using Aspose.Cells;
using System.Drawing;

// Create a new workbook
Workbook wb = new Workbook();
Worksheet sheet = wb.Worksheets[0];
sheet.Name = "Report";

// Populate some data
sheet.Cells["A1"].PutValue("Product");
sheet.Cells["B1"].PutValue("Price");
sheet.Cells["A2"].PutValue("Widget");
sheet.Cells["B2"].PutValue(19.99);
sheet.Cells["A3"].PutValue("Gadget");
sheet.Cells["B3"].PutValue(42.5);

// Apply basic styling
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = Color.LightGray;
headerStyle.Pattern = BackgroundType.Solid;
sheet.Cells["A1:B1"].SetStyle(headerStyle);

// Format the price column as currency
Style priceStyle = wb.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format
sheet.Cells["B2:B3"].SetStyle(priceStyle);
```

> **Miért fontos:** A számformátumok kifejezett beállításával később láthatod, hogy a `GridJsOptions.EnableNumberFormat` életben tartja ezeket a formátumokat a HTML kimenetben.

---

## 2. lépés: HTML mentési beállítások konfigurálása

Most létrehozunk egy `HtmlSaveOptions` példányt. Ez az objektum pontosan megmondja az Aspose.Cells‑nek, hogyan szeretnéd, hogy a HTML megjelenjen.

```csharp
// Step 2: Create HTML save options
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // Export the entire workbook as a single HTML page
    ExportActiveWorksheetOnly = false,

    // Keep the original cell styles (fonts, colors, borders)
    ExportGridLines = true,
    ExportColumnHeaders = true,
    ExportRowHeaders = true
};
```

### Grid.js számformázás engedélyezése

Ha azt tervezed, hogy a HTML‑t egy olyan oldalba ágyazod, amely **Grid.js**‑t használ interaktív táblázatokhoz, akkor szeretnéd, hogy a számok formázva maradjanak (pl. pénznem szimbólumok, ezres elválasztók). A következő sor ezt pontosan megteszi:

```csharp
// Step 3: Enable number formatting for Grid.js tables
htmlOptions.GridJsOptions = new GridJsOptions { EnableNumberFormat = true };
```

> **Mi történik a háttérben?** A `EnableNumberFormat` egy apró JavaScript kódrészletet injektál, amely azt mondja a Grid.js‑nek, hogy értelmezze a cella `data-format` attribútumát, megőrizve az Excel‑stílusú formázást a böngészőben.

---

## 3. lépés: Munkafüzet mentése HTML fájlként

Miután a munkafüzet készen áll és a beállítások finomhangoltak, az utolsó sor a HTML fájlt a lemezre írja.

```csharp
// Step 4: Save the workbook as an HTML file with the configured options
string outputPath = @"C:\Temp\gridjs.html";
wb.Save(outputPath, htmlOptions);
Console.WriteLine($"Workbook successfully saved as HTML to: {outputPath}");
```

A program futtatása egy `gridjs.html` fájlt hoz létre, amely így néz ki (egyszerűsített nézet):

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>Report</title>
    <link rel="stylesheet" href="gridjs.css" />
    <script src="gridjs.js"></script>
</head>
<body>
    <table class="gridjs-table">
        <thead>
            <tr><th>Product</th><th>Price</th></tr>
        </thead>
        <tbody>
            <tr><td>Widget</td><td data-format="$#,##0.00">19.99</td></tr>
            <tr><td>Gadget</td><td data-format="$#,##0.00">42.5</td></tr>
        </tbody>
    </table>
</body>
</html>
```

Nyisd meg a fájlt bármely böngészőben, és egy szépen formázott táblázatot látsz, világosszürke fejléc háttérrel és pénznem formázással. Ha a lapot egy olyan oldalra helyezed, amely már betölti a Grid.js‑t, a számok automatikusan a megfelelő vesszőkkel és szimbólumokkal jelennek meg.

---

## Gyakori buktatók, amikor **Excel‑t HTML‑re konvertálsz**

| Probléma | Miért fordul elő | Hogyan kerülhető el |
|----------|-------------------|---------------------|
| **Elveszett képletek** | A HTML statikus; a képletek egyszerű értékekké válnak. | Ha élő számításokra van szükség, tartsd a munkafüzetet a szerveren, és használj JavaScript könyvtárakat, például SheetJS‑t. |
| **Hiányzó képek** | A képek külön erőforrásként vannak tárolva. | Állítsd be a `HtmlSaveOptions.ExportImagesAsBase64 = true` értéket, hogy közvetlenül beágyazd őket. |
| **Nagy fájlok** | Nagy munkafüzetek hatalmas HTML‑t + JS‑t generálnak. | Használd az `ExportOnlyVisibleSheets` beállítást, vagy oszd több oldalra a `HtmlSaveOptions.OnePagePerSheet` segítségével. |
| **Helytelen számhelyi beállítás** | Az Excel a számokat invariáns kultúrában tárolja, a böngészők helyi beállításokat alkalmazhatnak. | Állítsd be kifejezetten a `htmlOptions.Encoding = Encoding.UTF8` értéket, és használd a `GridJsOptions.EnableNumberFormat`‑t. |

---

## Haladó: Több lap exportálása egyedi Grid.js példányokkal

Ha a munkafüzet több lapot tartalmaz, és azt szeretnéd, hogy mindegyik saját Grid.js táblázattá váljon, végigiterálhatsz a munkalapokon, és mindegyiket külön mentheted:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet ws = wb.Worksheets[i];
    HtmlSaveOptions opt = new HtmlSaveOptions
    {
        ExportActiveWorksheetOnly = true,
        GridJsOptions = new GridJsOptions { EnableNumberFormat = true }
    };
    string sheetPath = $@"C:\Temp\{ws.Name}.html";
    wb.Save(sheetPath, opt);
    Console.WriteLine($"Saved {ws.Name} to {sheetPath}");
}
```

Minden fájl saját `<table class="gridjs-table">` elemet tartalmaz majd, készen állva a független manipulációra.

---

## A kimenet ellenőrzése – Gyors ellenőrzőlista

1. **Stílus érintetlen?** Hasonlítsd össze a cella háttérszíneket és szegélyeket az eredeti Excel nézettel.  
2. **Számformátumok megmaradtak?** Keresd a `data-format` attribútumot a `<td>` elemekben.  
3. **Képek megjelennek?** Ha a képeket Base64‑ként exportáltad, akkor beágyazottan kell megjelenniük.  
4. **Böngésző konzol tiszta?** Nincsenek Grid.js‑hez kapcsolódó JavaScript hibák.  

Ha bármelyik ellenőrzés nem sikerül, nézd át a megfelelő `HtmlSaveOptions` tulajdonságot – a legtöbb probléma egy hiányzó flag‑ből ered.

---

## Összegzés

Most már egy stabil, termelés‑kész módszered van a **Excel HTML‑ként mentésére**, miközben minden stílus, szegély és numerikus ábrázolás érintetlen marad. A `HtmlSaveOptions` konfigurálásával és a `GridJsOptions.EnableNumberFormat` átkapcsolásával egy statikus táblázatot web‑barát táblává alakítottál, amely zökkenőmentesen működik a Grid.js‑szel.  

Röviden, ez az útmutató bemutatja, hogyan **konvertálhatod az Excelt HTML‑re** és hogyan **exportálhatod az Excelt formázással** az Aspose.Cells segítségével. Nyugodtan kísérletezz: próbálj ki különböző témákat, ágyazz be diagramokat, vagy akár szolgáld ki a HTML‑t egy ASP.NET végponton keresztül, hogy futás közben konvertálj.  

Ha bármilyen akadályba ütközöl, hagyj megjegyzést alább, vagy nézd meg az Aspose.Cells dokumentációt a részletesebb konfigurációs lehetőségekért. Boldog kódolást!

## Mi a következő lépés?

- **Fedezd fel a többi export formátumot**: PDF, PNG vagy CSV a `Workbook.Save` segítségével.  
- **Integrálás ASP.NET Core‑dal**: A HTML stringet közvetlenül egy controller akcióból adja vissza.  
- **Kombináld a SheetJS‑szel**: Töltsd be a generált HTML‑t vissza egy JavaScript munkafüzetbe kliensoldali szerkesztéshez.  

> Ha bármilyen akadályba ütközöl, hagyj megjegyzést alább, vagy nézd meg az Aspose.Cells dokumentációt a részletesebb konfigurációs lehetőségekért. Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan exportáljunk Excelt HTML‑re rácsvonalakkal az Aspose.Cells for .NET használatával](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)
- [Excel exportálása HTML‑re a szegélystílusok megőrzésével az Aspose.Cells for Java használatával](/cells/english/java/workbook-operations/aspose-cells-java-export-excel-html-border-styles/)
- [HTML konvertálása Excel‑be az Aspose.Cells .NET használatával: Átfogó útmutató](/cells/english/net/workbook-operations/convert-html-to-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}