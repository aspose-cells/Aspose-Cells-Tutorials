---
category: general
date: 2026-03-25
description: Ismerje meg, hogyan ágyazhat be betűtípusokat HTML-be Excel HTML-be exportálásakor.
  Ez a lépésről‑lépésre útmutató megmutatja, hogyan ágyazhat be betűtípusokat HTML-be,
  és hogyan mentheti a munkafüzetet HTML formátumban.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- export excel to html
- how to export excel
- save workbook as html
language: hu
og_description: Hogyan ágyazzuk be a betűtípusokat HTML-be Excel exportálásakor? Kövesd
  ezt az útmutatót a betűtípusok HTML-be ágyazásához, az Excel HTML-be exportálásához,
  és a munkafüzet HTML-ként történő mentéséhez az Aspose.Cells segítségével.
og_title: Hogyan ágyazzunk be betűtípusokat HTML-be Excelből – Teljes útmutató
tags:
- Aspose.Cells
- C#
- HTML export
- Font embedding
title: Hogyan ágyazzunk be betűtípusokat HTML-be Excelből – Teljes útmutató
url: /hu/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-from-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan ágyazzunk be betűtípusokat HTML-be Excelből – Teljes útmutató

Gondolkodtál már azon, **hogyan ágyazzunk be betűtípusokat** egy Excel munkafüzetből generált HTML fájlba? Nem vagy egyedül. Sok fejlesztő szembesül azzal a problémával, hogy az exportált HTML a saját gépén rendben néz ki, de egy másik eszközön elveszíti az eredeti tipográfiát. A jó hír? A megoldás meglehetősen egyszerű az Aspose.Cells segítségével, és a betűtípusok közvetlenül a HTML kimenetbe ágyazhatók.

Ebben az útmutatóban végigvezetünk a pontos lépéseken, hogy **betűtípusokat ágyazzunk be html‑be**, megmutatjuk, hogyan **exportáljunk Excel-t html‑be**, és végül bemutatjuk, hogyan **menthetjük el a munkafüzetet html‑ként** a szükséges beállításokkal. A végére egy azonnal használható HTML fájlt kapsz, amely pontosan úgy jelenik meg, mint a forrás‑táblázat – hiányzó karakterek és helyettesítő betűtípusok nélkül.

## Előfeltételek

- .NET 6.0 vagy újabb (a kód .NET Framework‑kel is működik)
- Aspose.Cells for .NET (ingyenes próba vagy licencelt verzió)
- Egy minta Excel fájl (`sample.xlsx`), amely legalább egy egyedi betűtípust használ
- Visual Studio 2022 vagy bármelyik kedvenc C# szerkesztő

Az Aspose.Cells-en kívül nincs szükség további NuGet csomagokra.

## 1. lépés: A projekt beállítása és a munkafüzet betöltése

Először is—hozz létre egy új konzolos alkalmazást, és add hozzá az Aspose.Cells hivatkozást.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToHtmlWithFonts
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load an existing Excel workbook
            string excelPath = @"C:\Temp\sample.xlsx";
            Workbook workbook = new Workbook(excelPath);
            
            // We'll configure the export options in the next step
        }
    }
}
```

**Miért fontos:** A munkafüzet betöltése az alap. Ha a munkafüzet nincs megfelelően betöltve, a későbbi betűtípus‑ágyazási beállítások nem fognak hatni. Emellett vegyük figyelembe, hogy az Aspose.Cells automatikusan beolvassa a fájlban tárolt betűtípus‑információkat, így nem kell kézzel megadni a betűtípusok nevét.

## 2. lépés: HtmlSaveOptions létrehozása és a betűtípus‑ágyazás engedélyezése

Most létrehozunk egy `HtmlSaveOptions` példányt, és bekapcsoljuk az `EmbedAllFonts` jelzőt. Ez azt mondja az Aspose.Cells‑nek, hogy ágyazza be a munkafüzet által hivatkozott minden betűtípust közvetlenül a generált HTML‑be.

```csharp
// Step 2: Create HTML save options
HtmlSaveOptions htmlSaveOptions = new HtmlSaveOptions();

// Enable embedding of all fonts in the output HTML
htmlSaveOptions.EmbedAllFonts = true;

// Optional: Reduce the size of the generated HTML by using base64 encoding
htmlSaveOptions.ExportEmbeddedImages = true;
```

**Miért kapcsoljuk be az `EmbedAllFonts`‑t:** Ha Excel‑t HTML‑be exportálsz e jelző nélkül, a HTML a betűtípusokat név szerint hivatkozza. Ha a néző rendszerén nincsenek telepítve ezek a betűtípusok, a böngésző egy általános családra vált, ami tönkreteszi a megjelenést. Az ágyazás garantálja, hogy a pontos karakterek a HTML fájllal együtt utaznak.

**Pro tipp:** Ha csak egy részhalmazra van szükséged a betűtípusokból (például tudod, hogy a munkafüzet csak a *Calibri* és *Arial* betűtípusokat használja), beállíthatod a `htmlSaveOptions.FontsList`‑et egy egyedi gyűjteményre. Ez jelentősen csökkentheti a végleges fájlméretet.

## 3. lépés: A munkafüzet mentése HTML‑ként beágyazott betűtípusokkal

Végül hívd meg a `Save` metódust a `Workbook` objektumon, átadva az elérési utat és a most beállított opciókat.

```csharp
// Step 3: Save the workbook as an HTML file with embedded fonts
string htmlPath = @"C:\Temp\embedded.html";
workbook.Save(htmlPath, htmlSaveOptions);

Console.WriteLine($"HTML file with embedded fonts saved to: {htmlPath}");
```

Ennyi—az `embedded.html` most már `<style>` blokkokat tartalmaz `@font-face` definíciókkal és base64‑kódolt betűtípusadatokkal. Nyisd meg bármely modern böngészőben, és ugyanazt a tipográfiát kell látnod, mint a `sample.xlsx`‑ben.

### Várt eredmény

Amikor megnyitod az `embedded.html`‑t:

- A saját betűtípus pontosan úgy jelenik meg, mint az Excelben.
- Nem kér le külső betűtípus fájlokat (ellenőrizd a Fejlesztői eszközök Network fülét—semmit sem kell betölteni).
- Az oldal mérete nagyobb lehet, mint egy egyszerű HTML export esetén, de a vizuális hűség tökéletes.

## Excel exportálása HTML‑be – Teljes példa

Összegezve, itt a teljes, futtatható program:

```csharp
using System;
using Aspose.Cells;

namespace ExcelToHtmlWithFonts
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string excelPath = @"C:\Temp\sample.xlsx";
            Workbook workbook = new Workbook(excelPath);
            
            // 2️⃣ Configure HTML export options
            HtmlSaveOptions htmlOptions = new HtmlSaveOptions
            {
                EmbedAllFonts = true,          // ✅ Embed every used font
                ExportEmbeddedImages = true,   // ✅ Include images as base64
                ExportChartImageFormat = ImageFormat.Png,
                ExportImagesAsBase64 = true    // ✅ Keep everything in one file
            };
            
            // 3️⃣ Save as HTML
            string htmlPath = @"C:\Temp\embedded.html";
            workbook.Save(htmlPath, htmlOptions);
            
            Console.WriteLine($"✅ HTML with embedded fonts saved at: {htmlPath}");
        }
    }
}
```

**Miért működik:** A `HtmlSaveOptions` objektum egy erőteljes tároló. Az `EmbedAllFonts` átkapcsolásával azt mondod az Aspose.Cells‑nek, hogy átvizsgálja a munkafüzet stílusgyűjteményét, lekérje a betűtípus fájlokat az operációs rendszerből, és beágyazza őket. Az `ExportEmbeddedImages` és `ExportImagesAsBase64` jelzők a HTML‑t önállóvá teszik, ami hasznos, ha a fájlt e‑mailben kell elküldeni vagy adatbázisban tárolni.

## Gyakori hibák betűtípusok HTML‑be ágyazásakor

Még a megfelelő kóddal is előfordulhatnak kisebb problémák. Nézzük meg őket, mielőtt fejfájást okoznának.

| Probléma | Miért fordul elő | Hogyan javítsuk |
|----------|------------------|-----------------|
| **Hiányzó betűtípus a szerveren** | Az a szerver, ahol a kód fut, esetleg nem rendelkezik a saját betűtípussal telepítve. | Telepítsd a szükséges betűtípusokat a szerveren, vagy másold a `.ttf/.otf` fájlokat egy ismert mappába, és állítsd be a `htmlSaveOptions.FontsLocation`‑t arra az útvonalra. |
| **Nagy HTML fájl** | Sok nehéz betűtípus beágyazása felduzzadhatja a HTML‑t (néha >5 MB). | Használd a `htmlSaveOptions.FontsList`‑et, hogy csak a szükséges betűtípusokat ágyazd be, vagy fontold alá a betűtípusokat egy olyan eszközzel, mint a FontForge, mielőtt beágyaznád. |
| **Licencelési korlátozások** | Néhány kereskedelmi betűtípus tiltja az ágyazást. | Ellenőrizd a betűtípus EULA‑ját. Ha az ágyazás tiltott, válassz web‑biztonságos alternatívát, vagy konvertáld a táblázatot PDF‑be. |
| **Böngésző kompatibilitás** | Nagyon régi böngészők (IE 8) esetleg figyelmen kívül hagyják a base64 adatot tartalmazó `@font-face`‑t. | Adj meg egy tartalék CSS szabályt, vagy szolgálj ki egy külön CSS fájlt a régi böngészőknek. |
| **Helytelen Unicode tartomány** | Az ágyazott betűtípus nem tartalmazhatja az összes használt karaktert (pl. ázsiai glyph-ek). | Győződj meg arról, hogy a forrás betűtípus támogatja a szükséges Unicode blokkokat, vagy ágyazz be egy másodlagos betűtípust, amely lefedi a hiányzó tartományt. |

## Haladó: Csak kiválasztott betűtípusok ágyazása

Ha tudod, hogy a munkafüzet csak a *Calibri* és *Times New Roman* betűtípusokat használja, korlátozhatod az ágyazást így:

```csharp
htmlSaveOptions.FontsList = new string[] { "Calibri", "Times New Roman" };
```

Ez drámaian csökkenti a HTML méretét, miközben megőrzi a megjelenést.

## A kimenet tesztelése

Miután legeneráltad az `embedded.html`‑t, hajtsd végre ezeket a gyors ellenőrzéseket:

1. Nyisd meg a fájlt Chrome/Edge/Firefox böngészőben.
2. Nyisd meg a Fejlesztői eszközöket → Network → szűrd **font** szerint. Nem szabad **külső** kéréseket látnod.
3. Ellenőrizd a `<style>` blokkot; megtalálod a `@font-face` szabályokat a `src: url(data:font/ttf;base64,…)` formában.
4. Hasonlítsd össze a megjelenített szöveget az eredeti Excel nézettel – a pixel‑pontos igazítás azt jelenti, hogy sikerült.

## Összefoglalás

Ebben az útmutatóban bemutattuk, **hogyan ágyazzunk be betűtípusokat** HTML‑be, amikor **Excel‑t exportálunk HTML‑be** az Aspose.Cells segítségével. Egy `HtmlSaveOptions` példány létrehozásával, az `EmbedAllFonts = true` beállításával és a `Workbook.Save` meghívásával egy önálló HTML fájlt kapsz, amely hűen reprodukálja az eredeti táblázat tipográfiáját. Emellett áttekintettük a gyakori hibákat, a teljesítmény trükköket, és egy gyors módszert, hogy csak a valóban szükséges betűtípusokat ágyazd be.

---

### Mi következik?

- **Excel exportálása PDF-be beágyazott betűtípusokkal** – tökéletes nyomtatásra kész dokumentumokhoz.
- **Több munkalap konvertálása egyetlen HTML fájlba** – ismerd meg a `HtmlSaveOptions.OnePagePerSheet` lehetőséget.
- **Dinamikus HTML generálás ASP.NET Core-ban** – streameld a HTML‑t közvetlenül a böngészőbe anélkül, hogy a fájlrendszert érintenéd.

Nyugodtan kísérletezz a beállításokkal, hagyj megjegyzést, ha elakadsz, és jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}