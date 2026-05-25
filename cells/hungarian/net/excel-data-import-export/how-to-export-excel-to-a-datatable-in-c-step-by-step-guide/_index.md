---
category: general
date: 2026-03-18
description: Hogyan exportáljuk az Excel adatokat egy DataTable-be C#-ban, kóddal,
  amely kezeli a specifikus cellákat, átalakítja az Excelt DataTable-re, és formázza
  a számokat. Tanulja meg a specifikus cellák exportálását és még sok mást.
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: hu
og_description: Hogyan exportáljuk az Excel adatokat DataTable-be C#-ban. Ez az útmutató
  bemutatja, hogyan exportáljunk konkrét cellákat, konvertáljuk az Excelt DataTable-re,
  és könnyedén formázzuk a számokat.
og_title: Hogyan exportáljunk Excel-t egy DataTable-be C#-ban – Teljes útmutató
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: Hogyan exportáljuk az Excelt egy DataTable-be C#-ban – Lépésről‑lépésre útmutató
url: /hu/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan exportáljunk Excel-t DataTable-be C#-ban – Lépésről‑lépésre útmutató

Gondolkodtál már azon, **hogyan exportáljunk Excel** adatokat egy `DataTable`-be anélkül, hogy elveszítenénk a formázást? Nem vagy egyedül – a fejlesztőknek folyamatosan szükségük van egy táblázat szeletének memóriába töltésére jelentéskészítés, validáció vagy tömeges beszúrási műveletek céljából. A jó hír? Néhány C# sorral exportálhatsz egy pontos tartományt (például *A1:F11*), kényszerítheted, hogy minden cellát karakterláncként kezeljen, és még egy egyéni számformátumot is alkalmazhatsz.

Ebben az útmutatóban mindent áttekintünk, amit tudnod kell: a munkafüzet betöltésétől, a **specifikus cellák exportálásának** beállításáig, a tartomány `DataTable`-be konvertálásáig, valamint az olyan széljegyek kezeléséig, mint az üres sorok vagy a helyi beállításoktól függő számok. A végére egy újrahasználható metódust kapsz, amely **excel to datatable c#** helyzetekben is működik a termelési kódban.

> **Előfeltételek** – Szükséged lesz az Aspose.Cells for .NET könyvtárra (vagy bármely hasonló API-ra, amely támogatja a `ExportDataTable`-t). A példa .NET 6+ környezetet feltételez, de a koncepciók korábbi verziókra is alkalmazhatók.

---

## Mit fogsz megtanulni

- Hogyan **konvertáljunk Excel-t DataTable-be** az Aspose.Cells használatával.
- Egy egyedi tartomány exportálása (`excel range to datatable`) úgy, hogy minden értéket karakterláncként kezelünk.
- Két tizedesjegyű számformátum alkalmazása (`#,#00.00`) exportálás közben.
- Gyakori buktatók (null sorok, rejtett oszlopok) és azok elkerülése.
- Egy másolásra kész, teljesen futtatható kódminta.

## Előfeltételek és beállítások

Mielőtt a kódba merülnénk, győződj meg róla, hogy rendelkezel a következőkkel:

1. **Aspose.Cells for .NET** telepítve NuGet-en keresztül:

   ```bash
   dotnet add package Aspose.Cells
   ```

2. Egy Excel fájl (`input.xlsx`) elhelyezve egy mappában, amelyre hivatkozhatsz, például `YOUR_DIRECTORY/input.xlsx`.

3. Egy projekt, amely .NET 6 vagy újabb célkeretet használ (az alább látható `using` utasítások azonnal működnek).

> **Pro tipp:** Ha másik könyvtárat használsz (pl. EPPlus vagy ClosedXML), a koncepció ugyanaz – töltsd be a munkafüzetet, válassz ki egy tartományt, és hívd meg azt a metódust, amely egy `DataTable`-t ad vissza.

## 1. lépés: A munkafüzet betöltése és az első munkalap lekérése

Az első dolog, amire szükséged van, egy `Workbook` objektum, amely a Excel fájlodat képviseli. Miután megvan, bármely munkalaphoz hozzáférhetsz index vagy név alapján.

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**Miért fontos:** A munkafüzet korai betöltése lehetővé teszi a struktúrájának (rejtett lapok, védelem) ellenőrzését, mielőtt eldöntenéd, mely cellákat exportálod. Ha a fájl nagy, fontold meg a `LoadOptions` használatát, hogy csak a szükséges részeket streameld.

## 2. lépés: Exportálási beállítások konfigurálása – Minden érték kezelése karakterláncként

Amikor adatot exportálsz további feldolgozásra (pl. tömeges beszúrás SQL-be), gyakran egy **konzisztens karakterlánc ábrázolásra** van szükség. Ez elkerüli a típuseltérésből adódó hibákat később.

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**Magyarázat:**  
- `ExportAsString = true` azt mondja az Aspose.Cells-nek, hogy hagyja figyelmen kívül a natív cellatípust, és a formázott szöveget adja vissza.  
- `NumberFormat = "#,##0.00"` biztosítja, hogy a `1234.5` számok `"1,234.50"`-ként jelenjenek meg – hasznos pénzügyi jelentésekhez.

Ha az eredeti adat típusokra van szükséged, egyszerűen állítsd `ExportAsString`-t `false`-ra, és magad végezd a konverziót.

## 3. lépés: Egy specifikus tartomány (A1:F11) exportálása DataTable-be

Most következik a **specifikus cellák exportálása** magja. Az `ExportDataTable` metódus a kezdő és befejező sor/oszlop indexeket (nulla‑alapú) valamint egy fejlécek beillesztését jelző jelzőt várja.

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**Mit kapsz:** Egy `DataTable` 11 sorral (beleértve a fejlécet) és 6 oszloppal (`A`‑`F`). Minden érték karakterláncként van formázva az `exportOptions` szerint.

## 4. lépés: Az eredmény ellenőrzése – Kiírás a konzolra

Mindig jó ötlet ellenőrizni a kimenetet, mielőtt a táblát átadnád egy másik komponensnek.

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

Valami ilyesmit kell látnod:

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

Vedd észre, hogy a numerikus oszlopok két tizedesjegyet jelenítenek meg, pontosan úgy, ahogy megadtuk.

## Teljes működő példa (másolásra kész)

Az alábbiakban a teljes program látható, amely mindent összekapcsol. Helyezd be egy új konzolos projektbe, állítsd be a fájl útvonalát, és futtasd – nincs szükség további konfigurációra.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**A kódból levont fő tanulságok:**

- Az `ExportTableOptions` objektum újrahasználható; több `ExportDataTable` hívásnál is átadhatod, ha több tartományt kell exportálni.
- Az indexelés **0**-tól kezdődik, így az `A1` a `(0,0)`-nak felel meg.
- Az `includeColumnNames` `true` értékre állítása automatikusan az első sort használja oszlopfejlécként – ez nagyszerű a további `DataTable` műveletekhez.

## Széljegyek kezelése és gyakori kérdések

### Mi van, ha a munkalap rejtett sorokat vagy oszlopokat tartalmaz?

Az Aspose.Cells alapértelmezés szerint tiszteletben tartja a láthatóságot. Ha rejtett adatokat is exportálni szeretnél, állítsd `exportOptions.ExportHiddenRows = true` és `ExportHiddenColumns = true` értékre.

### Az Excel fájlom képleteket tartalmaz – a számított értékeket kapom meg?

Igen. Alapértelmezés szerint az `ExportDataTable` a **megjelenített értéket** adja vissza (a képlet eredménye). Ha a nyers képlet szöveget szeretnéd, állítsd `exportOptions.ExportFormulas = true` értékre.

### Hogyan hagyjam ki a teljesen üres sorokat?

Az exportálás után megtisztíthatod a `DataTable`-t:

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### Exportálhatok-e nem összefüggő tartományt (pl. A1:B5 és D1:E5)?

Az Aspose.Cells egy hívásban nem támogatja a széttagolt tartományokat. Ehelyett exportáld minden blokkot külön, majd a kapott `DataTable`-eket manuálisan egyesítsd.

## Teljesítmény tippek

- **Használd újra az `ExportTableOptions`-t** több exportáláshoz; minden alkalommal új példány létrehozása elhanyagolható terhet jelent, de csak a kódot szennyezi.
- **Nagy fájlok streamelése** `LoadOptions`-szel, hogy elkerüld a teljes munkafüzet memóriába töltését.
- **Kerüld a `DataTable`-t**, ha csak egy gyors CSV exportra van szükséged – az `ExportDataTable` kényelmes, de nem a legmemória‑hatékonyabb megoldás hatalmas lapok esetén.

## Következtetés

Áttekintettük, **hogyan exportáljunk Excel** adatokat egy `DataTable`-be, miközben a formázást szabályozzuk, a specifikus cellatartományokat kezeljük, és biztosítjuk, hogy minden érték karakterláncként érkezzen. A teljes példa egy tiszta, termelés‑kész megközelítést mutat, amelyet könnyen adaptálhatsz **convert excel to datatable**, **export specific cells**, vagy bármely **excel range to datatable** szituációhoz, amellyel találkozol.

Nyugodtan kísérletezz: változtasd meg a tartományt, állítsd át az `ExportAsString`-t, vagy csatlakoztasd a `DataTable`-t közvetlenül az Entity Framework-hez tömeges beszúrásokhoz. A lehetőségek csak a képzeleted határáig terjednek, ha van ez a stabil alapod.

### Következő lépések és kapcsolódó témák

- **DataTable importálása vissza Excel-be** – ismerd meg a fordított műveletet az `ImportDataTable` segítségével.
- **DataTable tömeges beszúrása SQL Server-be** – használd a `SqlBulkCopy`-t villámgyors betöltéshez.
- **Munkavégzés EPPlus vagy ClosedXML használatával** – nézd meg, hogyan néz ki ugyanaz a feladat alternatív könyvtárakkal.
- **Cellák formázása exportáláskor** – fedezd fel tovább az `ExportTableOptions`-t dátumformátumok, egyéni kultúra beállítások és egyéb lehetőségek tekintetében.

Van kérdésed vagy más felhasználási eseted? Írj egy megjegyzést, és tartsuk a beszélgetést folytonosnak. Boldog kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}