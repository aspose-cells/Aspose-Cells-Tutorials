---
category: general
date: 2026-10-26
description: Az ExportAsStrin esetén a testreszabott ExportTableOptions lehetővé teszi,
  hogy az Excel adatokat karakterláncként exportálja C#-ban. Kövesse a lépésről‑lépésre
  útmutatót a beállításhoz és az export futtatásához.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: hu
lastmod: 2026-10-26
og_description: Az egyéni ExportTableOptions, amikor az ExportAsString engedélyezi
  a csak karakterláncokból álló Excel exportot. Ismerje meg a pontos lépéseket az
  export konfigurálásához és futtatásához C#‑ban.
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: Egyéni ExportTableOptions az ExportAsString használatakor – Excel exportálása
  stringként C#‑ban
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Custom ExportTableOptions when ExportAsStrin lets you export Excel
    data as strings in C#. Follow the step‑by‑step guide to configure and run the
    export.
  headline: Custom ExportTableOptions when ExportAsStrin for Excel
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Egyéni ExportTableOptions az ExportAsStrin esetén Excelhez
url: /hu/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Egyéni ExportTableOptions az ExportAsStrin használatakor – Excel exportálása stringként C#-ban

Ha **Custom ExportTableOptions when ExportAsStrin**-re van szükséged, hogy minden cellaértéket egyszerű szövegként kapj, ez az útmutató pontosan megmutatja, hogyan kell ezt megtenni. Akár adatimport csővezetékét építed, akár tiszta CSV‑kész dumpra van szükséged, látni fogod, miért kerülhető el a típuskonverziós meglepetés az opciók ilyen beállításával.

Ebben az oktatóanyagról megtanulod, **hogyan exportálj excel-t stringként** az Aspose.Cells könyvtár használatával, megtekintheted a teljes, futtatható kódot, és megértheted az egyes beállítások mögötti logikát. Külső dokumentációra nincs szükség – minden, amire szükséged van, itt található.

## Előfeltételek

* .NET 6.0 SDK vagy újabb telepítve  
* Visual Studio 2022 (vagy bármely .NET-et támogató IDE)  
* Aspose.Cells for .NET csomag (telepítés NuGet-en keresztül: `Install-Package Aspose.Cells`)  
* Egy Excel munkafüzet (`sample.xlsx`) a projekt gyökérkönyvtárában elhelyezve  

Ezek az egyetlen függőségek; a kód Windows, Linux vagy macOS rendszeren fut extra könyvtárak nélkül.

## 1. lépés: A kívánt munkafüzet betöltése exportáláshoz

Az első dolog, amit a **Custom ExportTableOptions when ExportAsStrin** használatakor teszel, hogy egy `Worksheet` objektumot nyersz ki egy betöltött munkafüzetből. Ez az objektum hozzáférést biztosít a sorokhoz, oszlopokhoz és az export API-hoz.

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*Miért fontos:*  
`Workbook` egyszer olvassa be a fájlt, és minden formázási információt memóriában tart. Egy adott `Worksheet` kiválasztásával korlátozod az export hatókörét, és elkerülöd a rejtett lapok felesleges feldolgozását.

## 2. lépés: ExportTableOptions beállítása ExportAsString = true értékkel

Az **Custom ExportTableOptions when ExportAsStrin** lényege a `ExportTableOptions` objektum. Az `ExportAsString` beállítása arra kényszeríti az exportálót, hogy minden cellát stringként kezeljen, függetlenül az eredeti adattípustól (dátum, szám, logikai érték stb.). A `PreserveFormatting` engedélyezése megőrzi a vizuális stílust (pl. pénznem jelek) a kapott szövegben.

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*Miért fontos:*  
Amikor később meghívod a `ExportDataTable`-t, a könyvtár általában megpróbálja meghatározni a .NET típust minden oszlophoz. Az `ExportAsString = true` esetén ez a meghatározási lépés kimarad, így elkerülhetők a váratlan `DateTime` vagy `double` konverziók, amelyek a későbbi CSV‑elemzőket hibára vihetik.

## 3. lépés: Tartomány exportálása DataTable-be az egyéni beállításokkal

Most már exportálhatsz egy téglalap alakú tartományt (0‑9. sorok, 0‑4. oszlopok) a munkalapról. A metódus egy `DataTable`‑t ad vissza, ahol minden mező `string` típusú.

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*Miért fontos:*  
A `ExportDataTable` a legkényelmesebb módja annak, hogy az Excel adatokat egy relációs struktúrába helyezd, amelyet számos .NET API már ismer (pl. Entity Framework, Dapper). Az **Custom ExportTableOptions when ExportAsStrin** átadásával garantálod, hogy minden `DataColumn.DataType` `typeof(string)` lesz.

## 4. lépés: Az eredmény ellenőrzése – minden érték string

Jó gyakorlat megerősíteni, hogy az export a várt módon működött. Az alábbi ciklus kiírja minden cella értékét és futásidejű típusát.

```csharp
Console.WriteLine("Exported DataTable (all values as strings):");
foreach (DataRow row in dataTable.Rows)
{
    for (int i = 0; i < dataTable.Columns.Count; i++)
    {
        object value = row[i];
        Console.Write($"{value} ({value.GetType().Name})\t");
    }
    Console.WriteLine();
}
```

**Várt kimenet**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

Minden cella `String` típusát mutatja, ami megerősíti, hogy a **Custom ExportTableOptions when ExportAsStrin** helyesen működött.

## 5. lépés: Opcionális – DataTable írása CSV-be

Ha a végső célod egy egyszerű szövegfájl, könnyedén sorosíthatod a `DataTable`‑t CSV‑be:



## Mit tanulj meg legközelebb?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Export HTML Strings from Excel to DataTable using Aspose.Cells for .NET: A Step‑by‑Step Guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [Export Custom Properties Excel Pdf Aspose Cells Net](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}