---
category: general
date: 2026-09-21
description: Állítsa be a SmartMarkerOptions ArrayAsSingle opciót C#-ban, hogy a JSON
  tömböket egyetlen cellaértékként exportálja egy Excel munkafüzetbe.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: hu
lastmod: 2026-09-21
og_description: Állítsa be a SmartMarkerOptions ArrayAsSingle opciót C#-ban, hogy
  a JSON tömböket egyetlen cellaértékként exportálja. Ismerje meg a teljes lépésről‑lépésre
  megoldást.
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: SmartMarkerOptions ArrayAsSingle beállítása C#-ban – teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: SmartMarkerOptions ArrayAsSingle konfigurálása C#‑ban JSON tömbök esetén
url: /hu/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SmartMarkerOptions ArrayAsSingle beállítása C#-ban JSON tömbökhöz

Ha **SmartMarkerOptions ArrayAsSingle** beállítására van szükséged az Aspose.Cells segítségével Excel fájlok generálása közben, ez az útmutató pontosan megmutatja, hogyan kell ezt megtenni. Megmutatjuk, hogyan tartható egy JSON tömb érintetlenül egy cellában, ahelyett, hogy elemei több sorra szétosztódnának.

A JSON adatokkal való munka táblázatokban gyakran a lapos nézet és a kompakt ábrázolás között kell választani. Sok jelentéskészítési helyzetben – például címkék listájának vagy azonosítók halmazának tárolásakor – azt szeretnéd, hogy a teljes JSON karakterlánc egyetlen cellában maradjon. Az **ArrayAsSingle** jelző a `SmartMarkerOptions`‑ban ezt lehetővé teszi.

Ebben a tutorialban:

* Létrehozunk egy `DataTable`‑t, amely egy JSON tömböt tartalmaz egy oszlopban.
* Smart Markereket helyezünk el egy Excel munkalapon.
* **SmartMarkerOptions ArrayAsSingle**‑t konfigurálunk, hogy a JSON tömb egyetlen cellaértékként legyen kezelve.
* Feldolgozzuk a markereket és elmentjük a munkafüzetet.
* Ellenőrizzük a kimenetet.

> **Előkövetelmények** – Szükséged van az Aspose.Cells for .NET könyvtárra (v23.12 vagy újabb) és egy .NET fejlesztői környezetre (ajánlott a Visual Studio 2022). Alapvető C# és DataTable ismeretek feltételezettek.

---

## 1. lépés: Az adatforrás előkészítése JSON tömbbel

Először építsünk fel egy `DataTable`‑t, amely utánozza azt az adatot, amit egy szolgáltatásból vagy adatbázisból kapnál. A **Names** oszlop egy JSON‑kódolt karakterláncot tartalmaz, amely egy névlistát reprezentál.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*Miért ez a lépés?*  
A Smart Markerek közvetlenül .NET objektumokból olvasnak adatot. Ha a JSON tömböt egy karakterlánc oszlopban helyezzük el, megőrizhetjük a pontos JSON szintaxist, amely később változtatás nélkül írható be egy cellába.

---

## 2. lépés: Smart Markerek beszúrása egy új munkafüzetbe

Hozzunk létre egy friss munkafüzetet, válasszuk ki az első munkalapot, és írjuk be a Smart Markereket, amelyek az egész táblára és a konkrét **Names** oszlopra hivatkoznak.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

A `&=dataTable.Names` marker azt mondja az Aspose.Cells‑nek, hogy cserélje le a cellát a **Names** oszlop értékével minden egyes `dataTable` sorra. Mivel csak egy sorunk van, a marker egyszer lesz feldolgozva.

---

## 3. lépés: **SmartMarkerOptions ArrayAsSingle** konfigurálása

Alapértelmezés szerint az Aspose.Cells egy tömb‑szerű karakterláncot külön sorokra bont. Az `ArrayAsSingle` értékének `true`‑ra állítása felülírja ezt a viselkedést, és a teljes JSON karakterláncot egyetlen cellában tartja.

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*Miért engedélyezzük az `ArrayAsSingle`‑t?*  
Ha az `ArrayAsSingle` **false**, a motor a `["Alice","Bob"]` értéket két különálló értékként értelmezi, és egymás melletti sorokba írja. `true`‑ra állítva a karakterlánc atomikus értékként kezelődik, ami elengedhetetlen a JSON formátum Excel‑beli megőrzéséhez.

---

## 4. lépés: A Smart Markerek feldolgozása a beállított opciókkal

Most futtassuk a Smart Marker motorját, átadva a most konfigurált opciós objektumot.

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

Feldolgozás közben az Aspose.Cells beolvassa a `dataTable`‑t, alkalmazza a markereket, és figyelembe veszi az `ArrayAsSingle` jelzőt, így a JSON tömb érintetlen marad.

---

## 5. lépés: A munkafüzet mentése és az eredmény ellenőrzése

Végül írjuk a munkafüzetet a lemezre. Nyisd meg a generált fájlt Excelben vagy bármely táblázatkezelőben, és ellenőrizd, hogy az **A2** cella pontosan a JSON karakterláncot tartalmazza.

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### Várt kimenet

| A   |
|-----|
| **["Alice","Bob"]** |

Az **A2** cella a JSON tömböt egyetlen szöveges értékként jeleníti meg, pontosan úgy, ahogy a `DataTable`‑ben tárolták. Nem jönnek létre extra sorok.

---

## Gyakori variációk és szél‑eset kezelése

| Helyzet | Hogyan alkalmazzuk |
|-----------|--------------|
| **Több sor JSON tömbökkel** | Az ugyanaz a `ArrayAsSingle` beállítás működik; minden sor JSON tömbje a saját cellájában marad. |
| **Különböző JSON struktúrák (objektumok, beágyazott tömbök)** | Amíg a JSON karakterlánc, a `ArrayAsSingle` érintetlenül tartja. Összetett objektumok esetén szükség lehet az idézőjelek escape‑elésére. |
| **Más adatforrás használata (pl. List\<T\>)** | Cseréld le a `DataTable`‑t bármilyen enumerálható gyűjteményre; a marker szintaxis (`&=myList.Property`) változatlan marad. |
| **Exportálás CSV-be XLSX helyett** | `ArrayAsSingle` továbbra is érvényes, de ne feledd, hogy a CSV nem őrzi meg a cellaformázást; előfordulhat, hogy a JSON‑t idézőjelek közé kell tenni. |

**Pro tipp:** Mindig állítsd be az `ArrayAsSingle`‑t *mielőtt* meghívod a `ProcessSmartMarkers`‑t. A jelző módosítása a feldolgozás után nincs hatással a már létrehozott cellákra.

---

## Teljes, futtatható példa

Az alábbi program a teljes kód, amelyet egyszerűen bemásolhatsz egy konzolalkalmazásba. Tartalmazza az összes `using` direktívát és a magyarázó megjegyzéseket.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

Futtasd a programot, nyisd meg a `SmartMarkerJson.xlsx` fájlt, és láthatod, hogy a JSON tömb megmaradt az **A2** cellában.

---

## Összegzés

Most már tudod, hogyan **SmartMarkerOptions ArrayAsSingle**‑t kell konfigurálni C#‑ban, hogy egy JSON tömb egyetlen cellaértékként maradjon meg az Aspose.Cells smart markerekkel történő exportáláskor. A lépések – `DataTable` előkészítése, markerek beszúrása, az `ArrayAsSingle` jelző beállítása, feldolgozás és mentés – egy ismételhető mintát alkotnak, amely bármely olyan esetben alkalmazható, ahol a kompakt JSON ábrázolás Excelben szükséges.

A következőkre is érdemes rátérned:

* **Aspose.Cells smart markerek** a gyűjtemények bejárásához.
* **Beágyazott JSON objektumok** exportálása cellaformázás testreszabásával.
* **Feltételes formázás** kombinálása smart markerekkel a gazdagabb jelentésekhez.

Nyugodtan kísérletezz különböző adatstruktúrákkal, és oszd meg az eredményeidet. Boldog kódolást!

## Mi legyen a következő tanulnivalód?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutató technikáira építenek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek az API további funkcióinak elsajátításában és alternatív megvalósítási megközelítések felfedezésében saját projektjeidben.

- [Excel munkafüzet létrehozása JSON-ból – Teljes Aspose.Cells útmutató](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Excel munkafüzet létrehozása és konfigurálása Aspose Cells .NET](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Excel munkafüzet létrehozása és konfigurálása Aspose Cells .NET](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}