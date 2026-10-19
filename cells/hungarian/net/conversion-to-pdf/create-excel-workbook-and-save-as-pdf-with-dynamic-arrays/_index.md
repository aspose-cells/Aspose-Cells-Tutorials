---
category: general
date: 2026-09-15
description: Excel munkafüzet létrehozása C#‑ban, és megtanulni, hogyan menthetjük
  a munkafüzetet PDF‑ként, miközben a dinamikus tömböket az EXPAND függvénnyel terítjük
  ki.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save workbook as pdf
- spill dynamic array
- use expand function
- how to create dynamic array in excel
language: hu
lastmod: 2026-09-15
og_description: Excel munkafüzet létrehozása C#-ban, és a munkafüzet gyors PDF-ként
  való mentése, miközben az EXPAND függvényt használjuk egy dinamikus tömb kibontásához.
og_image_alt: Create Excel workbook screenshot showing dynamic array and PDF output
og_title: Excel munkafüzet létrehozása és PDF‑be mentése dinamikus tömbökkel
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Create Excel workbook in C# and learn how to save workbook as PDF while
    spilling dynamic arrays using the EXPAND function.
  headline: Create Excel workbook and save as PDF with dynamic arrays
  type: TechArticle
tags:
- excel
- csharp
- aspose-cells
- pdf
- dynamic-array
title: Excel munkafüzet létrehozása és PDF-be mentése dinamikus tömbökkel
url: /hu/net/conversion-to-pdf/create-excel-workbook-and-save-as-pdf-with-dynamic-arrays/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel munkafüzet létrehozása és PDF‑ként mentése dinamikus tömbökkel

Ha **programozottan szeretne Excel munkafüzetet** létrehozni, majd **PDF‑ként menteni a munkafüzetet**, ez az útmutató egy komplett, vég‑től‑végig megoldást mutat be C#‑ban. Emellett megmutatjuk, hogyan **bontson ki dinamikus tömböt** a **EXPAND függvény** használatával, ami a modern módja a tömbök generálásának VBA nélkül.  

Akár jelentéskészítő szolgáltatást, ERP rendszer export funkciót vagy adat‑vezérelt irányítópultot épít, az alábbi lépések segítségével generálhat munkafüzetet, töltheti fel smart‑marker adatokkal, és előállíthat egy PDF‑et, amely megőrzi a fejlett betűtípus‑jellemzőket.

## Előfeltételek

Mielőtt elkezdené, győződjön meg róla, hogy rendelkezik:

* .NET 6.0 vagy újabb (a kód .NET Framework 4.8‑al is működik)
* A **Aspose.Cells for .NET** legújabb verziójával (v25.8 vagy újabb) – biztosítja a `Workbook`, `PdfSaveOptions` és `SmartMarkerProcessor` osztályokat.
* Visual Studio 2022‑vel vagy bármely C#‑ot képes fordítóval rendelkező IDE‑vel.

Adja hozzá a NuGet csomagot a projektjéhez:

```bash
dotnet add package Aspose.Cells --version 25.8
```

## 1. lépés: Excel munkafüzet létrehozása és az első munkalap beállítása

Az első feladat a **Excel munkafüzet** létrehozása és a alapértelmezett munkalap hivatkozásának megszerzése. Ez a munkalap fogja tartalmazni a dinamikus tömböt és a Smart Marker sablont.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook in memory
        Workbook wb = new Workbook();

        // Get the first (default) worksheet
        Worksheet ws = wb.Worksheets[0];
```

*Miért fontos*: A `Workbook` példányosítása lefoglalja a belső munkafüzet‑struktúrát, míg a `Worksheets[0]` elérése egy azonnal használható lapot ad, anélkül, hogy manuálisan kellene hozzáadni.

## 2. lépés: Dinamikus tömb kibontása az EXPAND függvény segítségével

Az Excel **EXPAND függvénye** képes egy statikus tömbliterált bármilyen méretű spill‑tartománnyá alakítani. Itt azt kérjük az Excelt, hogy a `{1,2,3}` értéket egy 5‑soros × 1‑oszlopos tartománnyá bővítse, kezdve az `A1`‑től.

```csharp
        // Write the EXPAND formula into A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // Force calculation so the spill occurs immediately
        ws.Calculate();
```

*Miért fontos*: Az `EXPAND` használata elkerüli a manuális ciklusok írását C#‑ban. A motor kiszámítja a spill‑tartományt, és közvetlenül a munkalapba helyezi az értékeket, amelyek később a PDF‑ben is megjelennek.

## 3. lépés: Munkafüzet mentése PDF‑ként a betűtípus‑variációs szelektorok megőrzésével

Amikor **PDF‑ként kell menteni a munkafüzetet**, engedélyezhetők a fejlett tipográfiai funkciók, például a betűtípus‑variációs szelektorok (az Aspose.Cells v25.8‑tól elérhetők). Ez biztosítja, hogy a PDF‑ek helyesen jelenítsék meg a komplex írásrendszereket.

```csharp
        // Configure PDF options
        PdfSaveOptions pdfOpts = new PdfSaveOptions
        {
            FontVariationSelectors = true   // keeps variation selectors for OpenType fonts
        };

        // Save the current workbook (with the spilled array) as PDF
        wb.Save(@"YOUR_DIRECTORY\VarSelector.pdf", pdfOpts);
```

*Miért fontos*: A `FontVariationSelectors` értékének `true`‑ra állítása elengedhetetlen azoknál a nyelveknél, amelyek glif‑variációra támaszkodnak (pl. kínai, japán, emoji). A létrehozott PDF tükrözi a képernyőn látható Excel‑nézetet.

## 4. lépés: Smart Marker sablon beillesztése, amely egy beágyazott adatforrást hivatkozik

A Smart Marker‑ek lehetővé teszik helyőrzők közvetlen beágyazását a munkalapba. Az alábbi sablon egy rendelés‑listát és azok tételeit generálja.

```csharp
        // Define a Smart Marker template in cell A1
        string template = "${Orders.OrderId}\n${Orders.Items:ItemName}\n";
        ws.Cells["A1"].PutValue(template);
```

*Miért fontos*: Az `A1`‑be helyezett sablonnal megmondja az Aspose.Cells‑nek, hol kezdje el a data kibontását. A `:` szintaxis (`Items:ItemName`) azt jelzi a processzornak, hogy egy beágyazott gyűjteményen iteráljon.

## 5. lépés: A beágyazott adatforrás (rendelések elemekkel) definiálása

Létrehozunk egy anonim tömböt a rendelésekből, ahol minden rendelés saját elemgyűjteménnyel rendelkezik. Ez egy tipikus master‑detail szituációt tükröz.

```csharp
        // Sample nested data source
        var orders = new[]
        {
            new
            {
                OrderId = 1,
                Items = new[]
                {
                    new { ItemName = "Apple" },
                    new { ItemName = "Banana" }
                }
            },
            new
            {
                OrderId = 2,
                Items = new[]
                {
                    new { ItemName = "Carrot" }
                }
            }
        };
```

*Miért fontos*: A beágyazott struktúra bemutatja, **hogyan lehet dinamikus tömböt létrehozni Excelben** Smart Marker‑ek segítségével, VBA vagy manuális cella‑ciklusok írása nélkül.

## 6. lépés: A Smart Marker‑ek feldolgozása és a végleges Excel fájl mentése

Most átadjuk a munkafüzetet és az adatforrást a `SmartMarkerProcessor`‑nek. A feldolgozás után a helyőrzők valós sorokra cserélődnek, és a végeredményt egy szokásos `.xlsx` fájlként mentjük.

```csharp
        // Process the Smart Markers
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Process(wb, orders);

        // Save the populated workbook
        wb.Save(@"YOUR_DIRECTORY\NestedSmartMarker.xlsx");
    }
}
```

*Miért fontos*: A `SmartMarkerProcessor` automatikusan kibontja a sablont, létrehozza a szükséges sorokat, és feltölti őket adatokkal. A végleges munkafüzet megnyitható Excelben, hogy ellenőrizze, minden rendelés és tétel helyesen jelenik‑e meg.

## Várható kimenet

* **VarSelector.pdf** – egy PDF‑fájl, amely az 1‑3 számokat öt sorban kifolyik, és az engedélyezett OpenType betűtípus‑variációkat használja.
* **NestedSmartMarker.xlsx** – egy Excel‑fájl a következő sorokkal (kezdve az `A1`‑től):

| RendelésAzonosító | TételNév |
|-------------------|----------|
| 1                 | Apple    |
| 1                 | Banana   |
| 2                 | Carrot   |

A PDF‑verzió ugyanazt a numerikus spill‑tartományt tartja meg, mivel a munkalap állapota a Smart Marker feldolgozása előtt lett mentve; ha a végső adatokat is PDF‑ben szeretné, egyszerűen ismételje meg a PDF‑mentést a feldolgozás után.

## Hasznos tippek és gyakori buktatók

| Tipp | Magyarázat |
|------|------------|
| **Használja újra ugyanazt a `PdfSaveOptions` objektumot** | Az opcióobjektum egyszeri létrehozása és újrahasználata elkerüli a megjelenítés finom eltéréseit (pl. hiányzó variációs szelektorok). |
| **Hívja meg a `ws.Calculate()` metódust a képletek beállítása után** | Kifejezett számítás nélkül a spill tartomány üres maradhat, amikor programból vizsgálja a munkafüzetet. |
| **Helyezze a Smart Marker sablonokat egy tiszta munkalapra** | A sablonok meglévő adatokkal való keverése váratlan sorbeszúrást okozhat. Ha lehetséges, használjon dedikált munkalapot. |
| **Figyeljen a fájlútvonalakra** | Használja a `Path.Combine(Environment.CurrentDirectory, "output.pdf")` kifejezést a különböző gépeken lévő keménykódolt könyvtárak elkerüléséhez. |
| **Verzió ellenőrzés** | `FontVariationSelectors` csak a 25.8‑as verziótól érhető el; a régebbi verziók figyelmen kívül hagyják a tulajdonságot anélkül, hogy hibát dobnának. |

## Következő lépések

Most, hogy tudja, hogyan **hozzon létre Excel munkafüzetet**, **bontson ki dinamikus tömböt**, és **mentse a munkafüzetet PDF‑ként**, a következőket fedezheti fel:

* Diagramok vagy képek hozzáadása a PDF konverzió előtt.
* A munkafüzet ugyanannak az exportálása más formátumokba (pl. HTML, CSV) a `Save` metódus túlterheléseivel.
* **Smart Marker kifejezések** (`${Orders.Total:SUM(Items.Price)}`) használata az aggregálások valós idejű kiszámításához.
* A kód integrálása egy ASP.NET Core API‑ba, hogy a felhasználók közvetlenül egy webes végpontról letölthessék a generált PDF‑et.

---

**Összefoglalás** – Ez a tutorial megmutatta, hogyan **hozzon létre Excel munkafüzetet**, használja az **EXPAND függvényt** a **dinamikus tömb kibontásához**, ágyazzon be egy **Smart Marker‑t**, amely beágyazott adatforrással dolgozik, és végül **mentse a munkafüzetet PDF‑ként**, miközben megőrzi a fejlett betűtípus‑jellemzőket. A komplett, futtatható példát bármely C# projektbe be lehet másolni, és saját adatstruktúráihoz igazítható. Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépés‑ről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [Excel munkafüzet létrehozása és PDF‑ként mentése ASP.NET‑ben az Aspose.Cells használatával](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Excel munkafüzet létrehozása és ODS‑ként mentése Aspose.Cells for .NET használatával](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Excel munkafüzet létrehozása és SVG‑ként mentése Aspose.Cells for Java használatával](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}