---
category: general
date: 2026-02-28
description: Készíts master‑detail jelentést C#‑ban, és tanuld meg, hogyan töltsd
  fel az Excel sablont, egyesítsd az adatokat Excelben, valamint hogyan tölts be Excel
  munkafüzetet C#‑ban néhány lépésben.
draft: false
keywords:
- create master detail report
- populate excel template
- merge data into excel
- load excel workbook c#
- how to create master detail
language: hu
og_description: Készíts master‑detail jelentést C#‑ban az Aspose.Cells SmartMarker
  használatával. Tanulja meg, hogyan töltsön be Excel munkafüzetet C#‑ban, egyesítse
  az adatokat Excelben, és töltse fel egy Excel sablont.
og_title: Mester‑részlet jelentés létrehozása C#‑ban – Excel sablon kitöltése
tags:
- C#
- Aspose.Cells
- Excel automation
- SmartMarker
title: Mester‑részlet jelentés létrehozása C#‑ban – Excel sablon feltöltése SmartMarkerrel
url: /hu/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mester‑részlet jelentés létrehozása C#‑ban – Excel sablon feltöltése SmartMarker‑rel

Valaha szükséged volt **create master detail report** létrehozására C#‑ban, de nem tudtad, hogyan juttasd az adatokat egy Excel fájlba? Nem vagy egyedül. Ebben az útmutatóban lépésről lépésre bemutatjuk, hogyan **populate Excel template**, **merge data into Excel**, és **load Excel workbook C#**‑stílusban, hogy egy kifinomult master‑detail jelentést kapj, amely készen áll a terjesztésre.

Az Aspose.Cells SmartMarker‑t fogjuk használni, egy erőteljes motor, amely natívan érti a master‑detail kapcsolatokat. A tutorial végére egy teljes, futtatható példát kapsz, amelyet bármely .NET projektbe beilleszthetsz. Nincs homályos „lásd a dokumentációt” megoldás – csak egy önálló megoldás, amit másolással és beillesztéssel futtathatsz.

## Mit fogsz megtanulni

- Hogyan **create master detail** adatstruktúrákat készíts C#‑ban, amelyek közvetlenül egy Excel sablonra illeszkednek.
- A pontos módja a **load Excel workbook C#** kódnak, amely megnyit egy `.xlsx` fájlt, amely SmartMarker címkéket tartalmaz.
- A folyamat a **populate Excel template** végrehajtásához a `SmartMarkerProcessor` futtatásával.
- Tippek a szélsőséges esetek kezelésére, például hiányzó címkék vagy nagy adathalmazok.
- Hogyan ellenőrizd az eredményt, és hogy néz ki a végleges **master detail report**.

### Előfeltételek

- .NET 6.0 vagy újabb (a kód .NET Framework 4.8‑on is működik).
- Aspose.Cells for .NET (letöltheted egy ingyenes próba NuGet csomagként: `Install-Package Aspose.Cells`).
- Egy alap Excel fájl (`template.xlsx`), amely SmartMarker címkéket tartalmaz (megmutatjuk a szükséges minimális jelölést).

Ha ezek készen állnak, merüljünk el.

## 1. lépés – A master‑detail adatforrás létrehozása *(how to create master detail)*

Az első dolog, amire szükséged van, egy C# objektum, amely a master sorokat (rendelések) és azok gyermek sorait (rendelési tételek) képviseli. A SmartMarker automatikusan beolvassa ezt a hierarchiát, ha a `MasterDetail` értéke `true`.

```csharp
using System;

// Step 1: Build the master‑detail data object
var orderData = new
{
    // Master collection – each order is a row in the master table
    Orders = new[]
    {
        new
        {
            Id = 1,
            // Detail collection – items belonging to order 1
            Items = new[] { new { Sku = 101, Qty = 2 }, new { Sku = 102, Qty = 1 } }
        },
        new
        {
            Id = 2,
            Items = new[] { new { Sku = 202, Qty = 1 } }
        }
    }
};
```

**Miért fontos ez:**  
A SmartMarker egy `Orders` nevű tulajdonságot (a master) keres, majd minden rendelésnél egy `Items` nevű gyűjteményt. Ha ezek a nevek egyeznek, automatikusan kapsz egy **master‑detail report**‑ot anélkül, hogy saját ciklusokat írnál.

> **Pro tipp:** Tartsd a tulajdonságneveket röviden és érthetően; ezek lesznek a helyőrzők az Excel sablonodban.

## 2. lépés – SmartMarker beállítások konfigurálása master‑detail feldolgozáshoz

Mondd meg a motornak, hogy master‑detail helyzetről van szó, és add meg a részletlap nevét, amely a gyermek sorokat fogja kapni.

```csharp
using Aspose.Cells;

// Step 2: Set up SmartMarker options
SmartMarkerOptions options = new SmartMarkerOptions
{
    // Enables master‑detail processing
    MasterDetail = true,
    // The sheet in the template that holds the detail rows
    DetailSheetName = "OrderDetail"
};
```

**Miért fontos ez:**  
Ha kihagyod a `MasterDetail = true` beállítást, a SmartMarker a adatokat egy lapos listaként kezeli, és a részlet sorok soha nem jelennek meg. A `DetailSheetName`-nek meg kell egyeznie a sablonban létrehozott munkalap nevével (kis‑nagy betű érzékeny).

## 3. lépés – Excel munkafüzet betöltése C# stílusban

Most megnyitjuk a SmartMarker címkéket tartalmazó sablont. Ez a **load Excel workbook C#** lépés, amelyen sok fejlesztő elakad, mert elfelejtik a helyes fájlútvonalat használni vagy megfelelően felszabadítani a munkafüzetet.

```csharp
using System.IO;

// Step 3: Load the workbook that holds the SmartMarker tags
string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
Workbook workbook = new Workbook(templatePath);
```

**Miért fontos ez:**  
Az Aspose.Cells beolvassa az egész munkafüzetet a memóriába, így a fájl lehet a lemezen, beágyazva erőforrásként, vagy akár egy webszolgáltatásból streamelve. Csak győződj meg róla, hogy az útvonal egy érvényes `.xlsx` fájlra mutat, amely a következőben tárgyalt címkéket tartalmazza.

## 4. lépés – SmartMarker címkék beszúrása a sablonba (populate Excel template)

Ha most megnyitod a `template.xlsx`‑t, két munkalapot látsz:

- **Orders** – a master lap egy `&=Orders.Id` sorral.
- **OrderDetail** – a részlet lap sorokkal, mint `&=Items.Sku` és `&=Items.Qty`.

Íme egy minimális nézet a jelölésről:

| Sheet | Cell A1 | Cell B1 |
|-------|---------|---------|
| Orders | `&=Orders.Id` | *(empty)* |
| OrderDetail | `&=Items.Sku` | `&=Items.Qty` |

Nem kell kódot írnod a címkékhez – azok az Excel fájlban élnek. A **populate Excel template** lépés egyszerűen a processzor meghívása:

```csharp
// Step 4: Run SmartMarker to merge data into Excel
new SmartMarkerProcessor().Process(workbook, orderData, options);
```

**Miért fontos ez:**  
A processzor minden munkalapot átvizsgál, a `&=` helyőrzőket valós értékekkel helyettesíti, és sorokat bővít minden master és detail rekordhoz. Mivel a `MasterDetail` be van kapcsolva, automatikusan új sort hoz létre minden tételhez a megfelelő rendelés alatt.

## 5. lépés – A master detail jelentés mentése

Végül írd a feltöltött munkafüzetet a lemezre. Ez a pillanat, amikor egy kész‑megosztásra alkalmas **master detail report**‑ot kapsz.

```csharp
// Step 5: Save the populated workbook
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);

// Optional: open the file automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Várható kimenet:**  

- **Orders** munkalap két sort mutat: `1` és `2` (rendelésazonosítók).  
- **OrderDetail** munkalap három sort mutat:  
  - SKU 101 Qty 2  
  - SKU 102 Qty 1  
  - SKU 202 Qty 1  

Ez egy teljesen működő **create master detail report**, amelyet e‑mailben elküldhetsz, kinyomtathatsz, vagy egy másik rendszerbe betáplálhatsz.

## Szélsőséges esetek és gyakori kérdések

### Mi van, ha a sablonból hiányzik egy címke?
A SmartMarker csendben figyelmen kívül hagyja az ismeretlen címkéket, de üres cellákat kapsz. Ellenőrizd a címke helyesírását, és győződj meg róla, hogy a C# objektumodban a tulajdonságnevek pontosan egyeznek.

### Hogyan kezeli a nagy adathalmazokat?
A processzor sorokat streameli, így akár több ezer részlet rekord sem terheli túl a memóriát. Rendkívül nagy fájlok esetén érdemes lehet növelni a `MemorySetting`‑et a `LoadOptions`‑ban.

```csharp
var loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeWorkbook = new Workbook(templatePath, loadOptions);
```

### Használhatok másik munkalap nevet a masterhez?
Igen – egyszerűen nevezd át a munkalapot a sablonban, és állítsd be a `DetailSheetName`‑t, ha van részletlapod. A master munkalap neve a helyőrzőből (`&=Orders.Id`) származik.

### Mi van, ha egy összegző sort kell hozzáadni?
Adj hozzá egy szokásos Excel képletet a sablonban (pl. `=SUM(B2:B{#})`). A SmartMarker a képletet megőrzi az adatok beszúrása után.

## Teljes futtatható példa

Az alábbiakban a teljes programot találod, amelyet másolással beilleszthetsz egy konzolalkalmazásba. Tartalmazza az összes `using` direktívát, az adatmodellt, a beállításokat és a fájlkezelést.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace MasterDetailReportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Create master‑detail data ----------
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Sku = 101, Qty = 2 },
                            new { Sku = 102, Qty = 1 }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Sku = 202, Qty = 1 }
                        }
                    }
                }
            };

            // ---------- Step 2: SmartMarker options ----------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                MasterDetail = true,
                DetailSheetName = "OrderDetail"
            };

            // ---------- Step 3: Load the template ----------
            string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
            Workbook workbook = new Workbook(templatePath);

            // ---------- Step 4: Process the template ----------
            new SmartMarkerProcessor().Process(workbook, orderData, options);

            // ---------- Step 5: Save the result ----------
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);

            Console.WriteLine($"Master detail report generated at: {outputPath}");
        }
    }
}
```

Futtasd a programot, nyisd meg az `output.xlsx`‑t, és a master‑detail adatok szépen feltöltve fognak megjelenni.

## Vizuális referencia

![Create master detail report output screenshot](https://example.com/images/master-detail-report.png "Create master detail report example")

*A kép az Orders munkalapot mutatja 1 és 2 azonosítókkal, valamint az OrderDetail munkalapot a három SKU‑Qty sorral.*

## Következtetés

Most már tudod, **how to create master detail report** C#‑ban az Aspose.Cells SmartMarker használatával, az adatforrás felépítésétől a **loading Excel workbook C#**, **populating Excel template**, és végül

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}