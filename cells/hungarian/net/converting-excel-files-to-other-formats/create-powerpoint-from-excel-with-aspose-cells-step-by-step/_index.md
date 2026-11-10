---
category: general
date: 2026-10-01
description: PowerPoint létrehozása Excelből az Aspose.Cells segítségével C#-ban.
  Exportálja az Excelt PowerPointba, és gyorsan konvertálja az XLSX-et PPTX-re egy
  teljes kódrészlettel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create PowerPoint from Excel
- export Excel to PowerPoint
- convert Excel to PPTX
- convert XLSX to PPTX
- generate PowerPoint from Excel
language: hu
lastmod: 2026-10-01
og_description: Készítsen PowerPoint prezentációt Excelből az Aspose.Cells segítségével
  C#-ban. Tanulja meg, hogyan exportálhat Excel-t PowerPointba, és konvertálhatja
  az XLSX-et PPTX-re néhány kódsorral.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel using Aspose.Cells
og_title: PowerPoint létrehozása Excelből az Aspose.Cells segítségével – gyors útmutató
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create PowerPoint from Excel using Aspose.Cells in C#. Export Excel
    to PowerPoint and convert XLSX to PPTX quickly with a complete code example.
  headline: Create PowerPoint from Excel with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Office automation
title: PowerPoint létrehozása Excelből az Aspose.Cells segítségével – lépésről‑lépésre
  útmutató
url: /hu/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PowerPoint létrehozása Excelből az Aspose.Cells segítségével – lépésről lépésre útmutató

Ha **PowerPointot kell létrehoznia Excelből**, ez a bemutató megmutatja, hogyan teheti meg az Aspose.Cells for .NET segítségével. Megtanulja, hogyan **exportálja az Excelt PowerPointba**, hogyan konvertál egy XLSX munkafüzetet PPTX prezentációvá, és hogyan testreszabja a kapott diákot anélkül, hogy elhagyná a C# projektjét.

Az útmutató mindent lefed, ami szükséges a kód .NET 6 vagy újabb verzión való futtatásához, beleértve a projekt beállítását, a szükséges NuGet csomagokat, és egy teljes, futtatható példát. A végére egy PowerPoint fájlt kap, amely az eredeti Excel diagramot pontosan úgy tartalmazza, ahogy a munkafüzetben megjelenik.

## Amire szüksége lesz

| Előfeltétel | Indoklás |
|---|---|
| .NET 6 SDK vagy újabb | Biztosítja a futtatókörnyezetet a C# konzolos alkalmazáshoz |
| Visual Studio 2022 (vagy bármely IDE) | Lehetővé teszi a könnyű projekt létrehozást és hibakeresést |
| Aspose.Cells for .NET NuGet csomag | Biztosítja a `Workbook` osztályt és az export API-kat |
| Egy Excel fájl (`.xlsx`), amely legalább egy diagramot tartalmaz | A PowerPoint dia forrásadata |

> **Pro tipp:** Az Aspose.Cells Windows, Linux és macOS rendszereken működik, így ugyanazt a kódot futtathatja Docker konténerekben vagy CI csővezetékekben.

## 1. lépés: Új konzolos projekt létrehozása és az Aspose.Cells hozzáadása

Nyisson egy terminált (vagy a Visual Studio Package Manager Console-t) és futtassa:

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
dotnet add package Aspose.Cells
```

A `dotnet add package` parancs letölti a **Aspose.Cells** legújabb stabil verzióját, amely tartalmazza a később használt `ExportPptx` metódust.

## 2. lépés: A forrás Excel munkafüzet hozzáadása

Helyezze a konvertálni kívánt Excel fájlt a projekt mappájába. Ebben a bemutatóban a `ChartOle.xlsx` fájlt használjuk, amely egyetlen diagramot tartalmaz az első munkalapon.

```
/ExcelToPptxDemo
│   Program.cs
│   ChartOle.xlsx   ← your source workbook
```

## 3. lépés: Írja meg a kódot, amely **PowerPointot hoz létre Excelből**

Nyissa meg a `Program.cs` fájlt, és cserélje le a tartalmát a következő kóddal. A példa bemutatja a **mag export** műveletet, és megmutatja, hogyan kezelhetők a gyakori széljegyek, például hiányzó fájlok és nem támogatott diagramtípusok.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelToPptxDemo
{
    class Program
    {
        static void Main()
        {
            // Define input and output paths
            string inputPath = Path.Combine(AppContext.BaseDirectory, "ChartOle.xlsx");
            string outputPath = Path.Combine(AppContext.BaseDirectory, "Exported.pptx");

            // Verify that the source workbook exists
            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: The file '{inputPath}' was not found.");
                return;
            }

            try
            {
                // Load the Excel workbook that contains the chart
                var workbook = new Workbook(inputPath);

                // Export the first worksheet as a PowerPoint presentation
                // This call performs the **convert Excel to PPTX** operation.
                workbook.Worksheets[0].ExportPptx(outputPath);

                Console.WriteLine($"Success: PowerPoint file created at '{outputPath}'.");
            }
            catch (Exception ex)
            {
                // Catch any errors thrown by Aspose.Cells (e.g., unsupported chart)
                Console.WriteLine($"Export failed: {ex.Message}");
            }
        }
    }
}
```

### Miért működik ez

* `Workbook` beolvassa a teljes Excel fájlt, beleértve a beágyazott diagramokat, táblázatokat és formázást.  
* `ExportPptx` átalakítja az aktív munkalapot PPTX diakészletté. A metódus automatikusan átalakítja az Excel diagramokat PowerPoint alakzatokká, megőrizve a vizuális hűséget.  
* A kód egy `try/catch` blokkba ágyazza a műveletet, hogy a hibákat, például a **convert XLSX to PPTX** hibákat, amelyek sérült fájlok miatt fordulnak elő, láthatóvá tegye.

## 4. lépés: A program futtatása és a kimenet ellenőrzése

Futtassa az alkalmazást:

```bash
dotnet run
```

A konzolon a következő üzenetet kell látnia:

```
Success: PowerPoint file created at '.../Exported.pptx'.
```

Nyissa meg az `Exported.pptx` fájlt a Microsoft PowerPointban vagy bármely kompatibilis megjelenítőben. Az első dia pontosan úgy jeleníti meg a diagramot, ahogy az a `ChartOle.xlsx` fájlban megjelent. Ez megerősíti, hogy sikeresen **létrehozott PowerPointot Excelből**.

## 5. lépés: Haladó – több munkalap exportálása vagy egyedi diaelrendezések

Az alap példa csak az első munkalapot exportálja. Valós körülmények között előfordulhat, hogy:

* **Több munkalap exportálása** külön diákra.  
* **Dia méretének szabályozása** vagy címhelyőrző hozzáadása.  
* **Rejtett munkalapok** belefoglalása a konverzióba.

Az alábbi tömör kódrészlet végigiterál az összes munkalapon, és mindegyiket külön diaként hozzáadja:

```csharp
// Export each worksheet as a separate slide
var pptxPath = Path.Combine(AppContext.BaseDirectory, "FullExport.pptx");
var presentation = new Presentation(); // Aspose.Slides.Presentation, if you have the Slides library

foreach (Worksheet ws in workbook.Worksheets)
{
    // Convert worksheet to an image first (optional for custom layout)
    var imgStream = new MemoryStream();
    ws.PageSetup.PrintArea = ws.Cells.MaxDisplayRange; // ensure full content
    ws.Pictures[0].ToImage(imgStream, ImageFormat.Png);

    // Add a new slide and insert the image
    var slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
    slide.Shapes.AddPictureFrame(ShapeType.Rectangle, 0, 0, presentation.SlideSize.Size.Width, presentation.SlideSize.Size.Height, imgStream);
}

// Save the final presentation
presentation.Save(pptxPath, SaveFormat.Pptx);
```

> **Megjegyzés:** A haladó kódrészlethez a **Aspose.Slides for .NET** könyvtár szükséges. Ha csak az egyszerű egy‑munkalapos konverzióra van szüksége, az előző `ExportPptx` hívás elegendő.

## Gyakori buktatók és hogyan kerülhetők el

| Probléma | Ok | Megoldás |
|---|---|---|
| Üres dia exportálás után | A munkalap nem tartalmaz látható objektumokat | Győződjön meg arról, hogy legalább egy diagram, táblázat vagy alakzat jelen van, mielőtt meghívná a `ExportPptx`-t. |
| Hiányzó betűtípusok a PowerPointban | A betűtípus nincs telepítve azon a gépen, ahol a PPTX meg van nyitva | Ágyazza be a szükséges betűtípusokat az Excel munkafüzetbe, vagy telepítse őket a célrendszeren. |
| Váratlan méretezés | A nagy diagram meghaladja a dia méreteit | Állítsa be a munkalap `PageSetup.Zoom` tulajdonságát exportálás előtt. |
| `convert XLSX to PPTX` `NotSupportedException`-t dob | A diagramtípus nem támogatott az Aspose.Cells által (pl. 3‑D térképek) | Cserélje le a diagramot egy támogatott típusra, vagy először exportálja a munkalapot képként. |

Ezeknek a széljegyeknek a kezelése biztosítja a megbízható **export Excel to PowerPoint** munkafolyamatot a termelési környezetekben.

## Összegzés

Most már tudja, hogyan **hozzon létre PowerPointot Excelből** az Aspose.Cells for .NET segítségével. A bemutató a következőket fedte le:

* Projekt beállítása és NuGet telepítés
* Excel munkafüzet betöltése és a `ExportPptx` meghívása
* A kód futtatása és a generált PPTX megerősítése
* A megoldás kiterjesztése több munkalap és egyedi elrendezések kezelésére
* Gyakorlati tippek a gyakori konverziós problémák elkerülésére

Ezzel a tudással automatizálhatja a jelentéskészítést, felépíthet prezentációs csővezetékeket, vagy beépítheti az Excel‑to‑PowerPoint konverziót bármely C# alkalmazásba. Kísérletezzen különböző diagramtípusokkal, adjon hozzá dia címeket, vagy kombinálja az exportot az Aspose.Slides-szel a teljes funkcionalitású prezentációk létrehozásához.

--- 

*Készen áll a további felfedezésre? Nézze meg a kapcsolódó témákat, például **convert Excel to PDF**, **embed Excel data in Word**, vagy **use Aspose.Slides to programmatically edit PPTX files**.*

## Mit érdemes még megtanulni?

A következő bemutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeiben.

- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/french/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/spanish/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}