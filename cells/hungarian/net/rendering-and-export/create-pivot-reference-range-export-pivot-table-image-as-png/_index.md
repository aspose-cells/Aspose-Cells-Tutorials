---
category: general
date: 2026-02-09
description: Hozzon létre pivot hivatkozási tartományt C#-ban, és exportálja a pivot
  táblázat képét. Tanulja meg, hogyan mentse el az Excel tartományt PNG formátumban
  az Aspose.Cells használatával – gyors, teljes útmutató.
draft: false
keywords:
- create pivot reference range
- export pivot table image
- save excel range as png
- Aspose.Cells C#
- Excel automation C#
language: hu
og_description: Hozzon létre pivot hivatkozási tartományt C#‑ban, és exportálja a
  pivot táblázat képét PNG‑ként. Teljes lépésről‑lépésre útmutató az Excel‑tartomány
  PNG‑ként való mentéséhez.
og_title: Pivot hivatkozási tartomány létrehozása – Pivot tábla kép exportálása PNG
  formátumban
tags:
- Aspose.Cells
- C#
- Excel
title: Pivot hivatkozási tartomány létrehozása – Pivot tábla kép exportálása PNG formátumban
url: /hu/net/rendering-and-export/create-pivot-reference-range-export-pivot-table-image-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pivot referencia tartomány létrehozása – Pivot tábla kép exportálása PNG formátumban

Szükséged van **pivot referencia tartomány** létrehozására egy Excel munkafüzetben C#‑al? Néhány sor kóddal **exportálhatod a pivot tábla képét** és **elmentheted az Excel tartományt PNG‑ként**. Tapasztalatom szerint egy élő pivot statikus képpé alakítása praktikus módja az elemzések beágyazásának jelentésekbe, e‑mailekbe vagy irányítópultokba anélkül, hogy az egész munkafüzetet át kellene vinni.

Ebben az útmutatóban mindent végigvázolunk, amit tudnod kell: a szükséges könyvtárakat, a pontos kódot, hogy miért fontos minden hívás, és néhány csapdát, amibe belefuthatsz. A végére képes leszel bármely pivot tábla PNG fájlját magabiztosan generálni, és megérted, hogyan alkalmazhatod a mintát több munkalapra vagy egyedi képformátumokra.

## Előfeltételek

Mielőtt belevágnánk, győződj meg róla, hogy a következők rendelkezésre állnak:

- **Aspose.Cells for .NET** (a ingyenes próba verzió teszteléshez tökéletes).  
- **.NET 6.0** vagy újabb – a használt API teljes mértékben kompatibilis a .NET Standard 2.0+-val, így régebbi keretrendszerek is lefordíthatók.  
- Egy alap C# projekt (Console App, WinForms vagy ASP.NET – bármi, ami képes NuGet csomagra hivatkozni).  

Ha még nem telepítetted az Aspose.Cells‑t, futtasd:

```bash
dotnet add package Aspose.Cells
```

Ennyi – nincs COM interop, nincs Excel telepítve a szerveren.

## 1. lépés: A munkafüzet megnyitása és az első munkalap elérése

Az első dolog, amit csinálsz, betöltöd a munkafüzet fájlt, és lekéred azt a munkalapot, amelyik a pivot táblát tartalmazza. Szándékosan az **első munkalapot** (`Worksheets[0]`) választjuk, mert a legtöbb demo fájl ott helyezi el a pivotot, de ha szeretnéd, az indexet cserélheted névre is.

```csharp
using Aspose.Cells;
using System;

// Load an existing Excel file (replace with your own path)
Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Access the first worksheet – this is where our pivot lives
Worksheet worksheet = wb.Worksheets[0];
```

*Miért fontos:* A `Worksheet` a belépési pont minden tartomány‑alapú művelethez. Ha a rossz lapra mutatsz, a későbbi `PivotTables[0]` hívás `IndexOutOfRangeException`‑t dob.

## 2. lépés: Pivot referencia tartomány létrehozása

Most a pivot táblát kérjük meg, hogy adja meg a **referencia tartományt**. Ez a tartomány pontosan azokat a cellákat tartalmazza, amelyek a pivotot alkotják – fejlécek, adat sorok és összesítések. A `CreateReferenceRange()` metódus belsőleg végzi el a nehéz munkát, kezelve az egyesített cellákat és a rejtett sorokat.

```csharp
// Grab the first pivot table on the worksheet
PivotTable pivot = worksheet.PivotTables[0];

// Build a reference range that covers the whole pivot
Range pivotReferenceRange = pivot.CreateReferenceRange();
```

> **Pro tipp:** Ha a munkafüzet több pivotot tartalmaz, iteráld a `worksheet.PivotTables` gyűjteményt, és válaszd ki a szükségeset a `Name` tulajdonsága alapján.

## 3. lépés: A referencia tartomány képként való renderelése

Az Aspose.Cells bármely `Range`‑t képpé tud renderelni. A visszaadott objektum támogatja mind a raszteres (PNG, JPEG), mind a vektoralapú (SVG) formátumokat. Itt a default raszteres képet kérjük, ami egy `System.Drawing.Image`‑kompatibilis objektum.

```csharp
// Convert the pivot reference range into an image object
ImageOrVector pivotImage = pivotReferenceRange.ToImage();
```

*Mi történik a háttérben?* Az API lefotózza a tartomány vizuális elrendezését, figyelembe véve a cellastílusokat, betűtípusokat és a feltételes formázást. Gyakorlatilag ugyanaz, mint egy képernyőfotó készítése, csak programozottan és UI nélkül.

## 4. lépés: A generált kép mentése fájlba

Végül elmentjük a képet. A `Save` metódus automatikusan PNG‑t választ, ha “.png” kiterjesztést adsz meg. Ha DPI‑vezérlést vagy más formátumot szeretnél, átadhatsz egy `SaveOptions` objektumot is.

```csharp
// Save the image as PNG – the extension drives the format
pivotImage.Save("YOUR_DIRECTORY/pivot.png");
```

Ez a sor lefutása után nyisd meg a `pivot.png` fájlt, és egy pixel‑pontos pillanatképet látsz a pivot tábláról, készen arra, hogy bárhol beágyazd.

## Teljes működő példa

Összegezve, itt egy önálló konzol program, amit egyszerűen másolj‑beilleszthetsz és futtathatsz:

```csharp
using Aspose.Cells;
using System;

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

            // 2️⃣ Access first worksheet
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Get first pivot table
            if (worksheet.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found on the first sheet.");
                return;
            }
            PivotTable pivot = worksheet.PivotTables[0];

            // 4️⃣ Create a reference range that covers the whole pivot
            Range pivotReferenceRange = pivot.CreateReferenceRange();

            // 5️⃣ Render the range to an image
            ImageOrVector pivotImage = pivotReferenceRange.ToImage();

            // 6️⃣ Save as PNG
            string outputPath = "YOUR_DIRECTORY/pivot.png";
            pivotImage.Save(outputPath);

            Console.WriteLine($"Pivot table image saved to {outputPath}");
        }
    }
}
```

**Várható kimenet:** egy `pivot.png` nevű fájl a `YOUR_DIRECTORY` könyvtárban. Nyisd meg bármely képnézővel – a pivot eredeti elrendezése, beleértve az oszlopfejléceket, adat sorokat és a grand total‑t, pontosan megjelenik.

## Pivot tábla kép exportálása – Méret és DPI testreszabása

Néha az alapértelmezett kép túl kicsi egy prezentációs diára. A felbontást egy `ImageOrVectorSaveOptions` objektummal szabályozhatod:

```csharp
using Aspose.Cells.Drawing;

// Define PNG options – 300 DPI for high‑quality print
ImageOrVectorSaveOptions options = new ImageOrVectorSaveOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300 // DPI
};

pivotImage.Save("YOUR_DIRECTORY/pivot_highres.png", options);
```

*Miért állítsuk be a DPI‑t?* A magasabb DPI élesebb éleket eredményez, különösen ha a PNG‑t nagyítod PowerPointban vagy PDF‑ben.

## Excel tartomány mentése PNG‑ként – Több munkalap kezelése

Ha több lapon kell pivotokat exportálni, iterálj a `Workbook.Worksheets` gyűjteményen, és ismételd meg a lépéseket. Egy tömör kódrészlet:

```csharp
foreach (Worksheet ws in wb.Worksheets)
{
    foreach (PivotTable pt in ws.PivotTables)
    {
        Range refRange = pt.CreateReferenceRange();
        ImageOrVector img = refRange.ToImage();
        string fileName = $"pivot_{ws.Name}_{pt.Name}.png";
        img.Save($"YOUR_DIRECTORY/{fileName}");
        Console.WriteLine($"Saved {fileName}");
    }
}
```

Ez a minta **exportálja a pivot tábla képet** minden pivotra a munkafüzetben, és minden fájlt a lap és a pivot neve alapján nevezi el – tökéletes kötegelt feldolgozáshoz.

## Gyakori hibák és megoldások

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| `IndexOutOfRangeException` a `PivotTables[0]`‑nál | A munkalapon nincs pivot tábla. | Ellenőrizd a `worksheet.PivotTables.Count` értékét, mielőtt hozzáférnél. |
| Üres kép kimenet | A pivot szűrve van, és minden sor rejtve van. | Győződj meg róla, hogy a pivot látható adatot tartalmaz, vagy hívd meg a `pivot.RefreshData();`‑t a tartomány létrehozása előtt. |
| Alacsony felbontású PNG | Alap DPI 96. | Használd a `ImageOrVectorSaveOptions.Resolution`‑t, ahogy fent látható. |
| Fájl‑útvonal hibák | Érvénytelen karakterek a `YOUR_DIRECTORY`‑ben. | Használd a `Path.Combine`‑t és a `Path.GetInvalidPathChars()`‑t a tisztításhoz. |

## Ellenőrzés – Gyors teszt

A teljes példa futtatása után:

1. Nyisd meg a `pivot.png` fájlt a Windows Photo Viewer‑ben.  
2. Ellenőrizd, hogy az oszlopfejlécek, adat sorok és összesítő sorok megegyeznek az Excel nézettel.  
3. Ha hiányzó sorokat látsz, ellenőrizd, hogy a pivot **RefreshData** metódusa meghívásra került‑e a `CreateReferenceRange()` előtt.

## Bónusz: PNG beágyazása Word dokumentumba

Mivel a kép már PNG, közvetlenül betáplálható az Aspose.Words‑ba:

```csharp
using Aspose.Words;
Document doc = new Document();
DocumentBuilder builder = new DocumentBuilder(doc);
builder.InsertImage("YOUR_DIRECTORY/pivot.png");
doc.Save("YOUR_DIRECTORY/report.docx");
```

Most már van egy Word jelentésed, amely a pivot pontos pillanatképét tartalmazza – nincs szükség kézi másolás‑beillesztésre.

## Összegzés

Most már tudod, hogyan **hozd létre a pivot referencia tartományt**, **exportáld a pivot tábla képét**, és **mentsd el az Excel tartományt PNG‑ként** az Aspose.Cells segítségével C#‑ban. A legfontosabb tanulságok:

- Használd a `PivotTable.CreateReferenceRange()`‑t a pivot vizuális területének izolálásához.  
- Konvertáld a tartományt képpé a `Range.ToImage()`‑val.  
- Mentsd el a képet PNG‑ként, opcionálisan állítsd be a DPI‑t nyomtatási minőséghez.  

Innen már felfedezheted a kötegelt exportálást, különböző képformátumokat (SVG, JPEG), vagy akár a PNG beágyazását PDF‑be vagy Word dokumentumba. A lehetőségek csak a képzeletedre vannak korlátozva, amint a pivotot statikus grafikává alakítottad.

Van kérdésed vagy egy bonyolult szituáció? Írj kommentet alább, és jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}