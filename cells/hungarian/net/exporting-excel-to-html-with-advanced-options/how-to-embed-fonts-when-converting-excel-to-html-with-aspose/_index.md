---
category: general
date: 2026-10-01
description: Ismerje meg, hogyan ágyazhat be betűtípusokat HTML-be az Excel HTML-re
  konvertálása során az Aspose.Cells segítségével. Exportálja az Excelt HTML-be beágyazott
  betűtípusokkal néhány lépésben.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- convert excel to html
- embed fonts in html
- how to export excel
- export excel as html
language: hu
lastmod: 2026-10-01
og_description: Hogyan ágyazzunk be betűtípusokat HTML-be Excel-fájlok exportálásakor.
  Kövesse ezt a lépésről‑lépésre útmutatót az Excel HTML-re konvertálásához beágyazott
  betűtípusokkal.
og_image_alt: Screenshot of Aspose.Cells code embedding fonts in exported HTML
og_title: Hogyan ágyazzunk be betűtípusokat HTML-be Excelből – Aspose.Cells útmutató
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  headline: How to embed fonts when converting Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  name: How to embed fonts when converting Excel to HTML with Aspose.Cells
  steps:
  - name: 'Edge case: unsupported fonts'
    text: If the workbook uses a font that is not installed on the server, Aspose.Cells
      falls back to a default system font. To avoid this, install the required fonts
      on the server or embed them manually after export.
  - name: Converting multiple worksheets
    text: If you need to **convert Excel to HTML** for all worksheets, set `ExportActiveWorksheetOnly
      = false` (the default). Aspose.Cells will create a separate HTML file for each
      sheet.
  - name: Controlling CSS output
    text: 'You can reduce the HTML size by disabling inline CSS:'
  - name: Using a stream instead of a file
    text: 'When integrating into a web API, write the HTML to a `MemoryStream` and
      return it directly:'
  type: HowTo
tags:
- Aspose.Cells
- .NET
- Excel conversion
title: Hogyan ágyazzunk be betűtípusokat az Excel HTML-re konvertálásakor az Aspose.Cells
  használatával
url: /hu/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-converting-excel-to-html-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan ágyazzunk be betűtípusokat Excel HTML-re konvertálásakor az Aspose.Cells használatával

Az Excel munkafüzet HTML-re konvertálásakor a betűtípusok beágyazása elengedhetetlen az eredeti megjelenés böngészők közötti megőrzéséhez. Ha Excel‑t HTML‑re kell konvertálni, miközben a saját betűtípusokat érintetlenül szeretné megtartani, ez az útmutató bemutatja a teljes folyamatot. Emellett megmutatjuk, hogyan exportálhatja az Excelt HTML‑ként, és miért fontos a betűtípusok beágyazása a HTML‑ben a következetes megjelenítés érdekében.

Ez a bemutató mindent lefed, amit tudnia kell: a szükséges könyvtárakat, a kódkonfigurációt és a létrehozott HTML‑fájl ellenőrzését. A végére képes lesz az Excelt HTML‑ként exportálni beágyazott betűtípusokkal, mindössze néhány C#‑sorral.

## Amire szüksége lesz

* **.NET 6.0 vagy újabb** – a kód a .NET 6‑ra céloz, de bármely .NET verzió, amely támogatja az Aspose.Cells‑t, működik.
* **Aspose.Cells for .NET** – szerezzen licencet, vagy használja az ingyenes értékelő verziót az Aspose weboldaláról.
* **C# fejlesztői környezet** (Visual Studio, Rider vagy VS Code) – bármely IDE, amely .NET projekteket tud fordítani.
* Egy Excel munkafüzet (`Styled.xlsx`), amely a megőrizni kívánt egyedi betűtípusokat használja.

## 1. lépés: Aspose.Cells beállítása a .NET projektben

Először adja hozzá az Aspose.Cells NuGet csomagot a projekthez:

```bash
dotnet add package Aspose.Cells
```

Ezután importálja a névteret a C# fájl tetején:

```csharp
using Aspose.Cells;
```

A csomag hozzáadása elérhetővé teszi a `Workbook`, `HtmlSaveOptions` és a kapcsolódó osztályokat.

## 2. lépés: Az Excel munkafüzet betöltése

A munkafüzet betöltése az első konkrét lépés a **Excel exportálásának** folyamatában. A `Workbook` konstruktor beolvassa a fájlt a lemezről:

```csharp
// Step 1: Load the Excel workbook
var workbook = new Workbook("YOUR_DIRECTORY/Styled.xlsx");
```

*Miért fontos:* Az Aspose.Cells feldolgozza a munkafüzetet, beleértve a cellastílusokat, képleteket és a betűtípus‑információkat. Ha a fájl nem található, kivétel keletkezik, ezért ellenőrizze, hogy az elérési út helyes-e.

## 3. lépés: HTML mentési beállítások konfigurálása a betűtípusok beágyazásához

A **betűtípusok beágyazása HTML‑ben** központi eleme a `HtmlSaveOptions` osztály. Állítsa az `EmbedFonts` értékét `true`‑ra, hogy a munkafüzetben használt minden betűtípus Base64‑kódolt `@font-face` szabályként kerüljön be az HTML‑kimenetbe.

```csharp
// Step 2: Set HTML save options to embed fonts in the output
var htmlOptions = new HtmlSaveOptions
{
    EmbedFonts = true,
    // Optional: keep the original worksheet name as the HTML file name
    ExportActiveWorksheetOnly = true
};
```

*Miért fontos:* Alapértelmezés szerint az Aspose.Cells külső betűtípus‑fájlokra hivatkozik, amelyek a kliens gépen nem biztos, hogy elérhetők. Az `EmbedFonts` engedélyezése garantálja, hogy a megjelenített HTML pontosan úgy nézzen ki, mint az eredeti Excel‑lap, függetlenül a felhasználó telepített betűtípusaitól.

### Szélsőséges eset: nem támogatott betűtípusok

Ha a munkafüzet olyan betűtípust használ, amely nincs telepítve a szerveren, az Aspose.Cells egy alapértelmezett rendszer‑betűtípusra vált. Ennek elkerülése érdekében telepítse a szükséges betűtípusokat a szerverre, vagy exportálás után manuálisan ágyazza be őket.

## 4. lépés: A munkafüzet mentése HTML‑ként a konfigurált beállításokkal

Most már kiírhatja a HTML‑fájlt. A `Save` metódus megkapja a kimeneti útvonalat és a `HtmlSaveOptions` példányt:

```csharp
// Step 3: Save the workbook as an HTML file using the configured options
workbook.Save("YOUR_DIRECTORY/Styled.html", htmlOptions);
```

A végrehajtás után a `Styled.html` tartalmazza a táblázat adatait és egy `<style>` blokkot, amely Base64‑kódolt `@font-face` definíciókat tartalmaz minden egyedi betűtípushoz.

## 5. lépés: A beágyazott betűtípusok ellenőrzése

Nyissa meg a `Styled.html` fájlt egy böngészőben. Ellenőrizze a `<head>` részt; valami ilyesmit kell látnia:

```html
<style>
@font-face {
    font-family: 'Calibri';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
}
...
</style>
```

Ha a betűtípusok helyesen jelennek meg a megjelenített táblázatban, a beágyazás sikeres volt. Ha hiányzó karaktereket észlel, ellenőrizze újra, hogy a forrás‑betűtípus‑fájlok telepítve vannak-e a konverziót végző gépen.

## Gyakori variációk és további beállítások

### Több munkalap konvertálása

Ha **Excel‑t HTML‑re** kell konvertálni az összes munkalaphoz, állítsa be az `ExportActiveWorksheetOnly = false` értéket (ez az alapértelmezett). Az Aspose.Cells minden laphoz külön HTML‑fájlt hoz létre.

```csharp
htmlOptions.ExportActiveWorksheetOnly = false;
workbook.Save("YOUR_DIRECTORY/AllSheets.html", htmlOptions);
```

### CSS kimenet szabályozása

Az HTML méretét csökkentheti az inline CSS letiltásával:

```csharp
htmlOptions.ExportCssSeparately = true; // Generates a .css file alongside the .html
```

### Stream használata fájl helyett

Web API‑ba való integráláskor írja a HTML‑t egy `MemoryStream`‑be, és adja vissza közvetlenül:

```csharp
using var stream = new MemoryStream();
workbook.Save(stream, htmlOptions);
stream.Position = 0; // Reset for reading
// Return stream as a file download in ASP.NET Core
```

## Pro tipp: Licencelje a terméket az értékelő vízjelek eltávolításához

Ha az értékelő verziót használja, a generált HTML vízjel‑kommentárt tartalmazhat. A munkafüzet betöltése előtt alkalmazza az Aspose.Cells licencet, hogy tiszta kimenetet kapjon:

```csharp
var license = new License();
license.SetLicense("Aspose.Total.lic");
```

## Teljes működő példa

Az alábbiakban egy teljes, futtatható program látható, amely bemutatja, hogyan **ágyazzunk be betűtípusokat**, **konvertáljunk Excel‑t HTML‑re**, és **exportáljunk Excel‑t HTML‑ként** egy lépésben:

```csharp
using System;
using Aspose.Cells;

class ExcelToHtmlWithEmbeddedFonts
{
    static void Main()
    {
        // Apply license if you have one (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Total.lic");

        // 1️⃣ Load the Excel workbook
        var workbookPath = @"YOUR_DIRECTORY/Styled.xlsx";
        var workbook = new Workbook(workbookPath);

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportActiveWorksheetOnly = true, // Export only the first sheet
            ExportCssSeparately = false        // Keep CSS inline for a single file
        };

        // 3️⃣ Save as HTML
        var htmlPath = @"YOUR_DIRECTORY/Styled.html";
        workbook.Save(htmlPath, htmlOptions);

        Console.WriteLine($"Excel workbook '{workbookPath}' has been exported to HTML with embedded fonts at '{htmlPath}'.");
    }
}
```

**Várt kimenet:** A program futtatása után a `Styled.html` megjelenik a `YOUR_DIRECTORY` könyvtárban. A fájl megnyitása bármely modern böngészőben a táblázatot mutatja az eredeti Excel‑fájlhoz hasonló betűtípusokkal, még olyan gépeken is, ahol ezek a betűtípusok nincsenek telepítve.

## Következtetés

Most már tudja, hogyan **ágyazzunk be betűtípusokat**, amikor **Excel‑t HTML‑re** konvertál az Aspose.Cells segítségével, és látta a teljes folyamatot a munkafüzet betöltésétől a beágyazott betűtípusok ellenőrzéséig. Ez a megközelítés biztosítja, hogy az Excel‑fájlok vizuális hűsége megmaradjon a generált HTML‑ben, ami ideálissá teszi webes jelentésekhez, e‑mail hírlevelekhez vagy bármely olyan helyzethez, ahol **Excel‑t HTML‑ként** kell exportálni egyedi tipográfiával.

Ezután fedezze fel a kapcsolódó témákat, például **Excel exportálása PDF‑ként**, **HTML‑kimenet stílusozása egyedi CSS‑sel**, vagy **több munkafüzet kötegelt feldolgozása**. Mindegyik azonos `HtmlSaveOptions` mintára épül, így a kódot minimális módosítással alkalmazhatja.

Boldog kódolást!

## Mit érdemes még megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeiben.

- [How to Export Excel to HTML – Step‑by‑Step Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [How to Embed Fonts in HTML – Complete C# Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/)
- [How to embed fonts when converting Excel to PDF – Step‑by‑Step Guide](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}