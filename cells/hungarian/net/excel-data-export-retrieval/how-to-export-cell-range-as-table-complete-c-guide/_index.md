---
category: general
date: 2026-07-13
description: Hogyan exportáljunk cellatartományt táblaként C# és ExportTableOptions
  segítségével. Tanulja meg lépésről lépésre a munkafüzet beállítását, formázását
  és a tábla exportálását.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export cell range as table
- ExportTableOptions usage
- Workbook and Worksheet handling
- cell value formatting C#
- scientific notation export
language: hu
lastmod: 2026-07-13
og_description: Hogyan exportáljuk a cellatartományt táblázatként C#-ban az ExportTableOptions
  segítségével. Kövesd ezt az útmutatót a cellák formázásához, munkafüzet létrehozásához
  és a táblázat könnyed exportálásához.
og_image_alt: Diagram illustrating a C# code snippet that exports a single cell range
  as a formatted table
og_title: Hogyan exportáljunk cellatartományt táblázatként – Teljes C# útmutató
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to export cell range as table using C# and ExportTableOptions.
    Learn step‑by‑step workbook setup, formatting, and table export.
  headline: How to Export Cell Range as Table – Complete C# Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
- data export
title: Hogyan exportáljunk cellatartományt táblázatként – Teljes C# útmutató
url: /hu/net/excel-data-export-retrieval/how-to-export-cell-range-as-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan exportáljunk cellatartományt táblázatként – Teljes C# útmutató

Gondolkodtál már azon, **hogyan exportáljunk cellatartományt táblázatként** anélkül, hogy a formázási sajátosságok miatt a hajadba vágod a kezed? Nem vagy egyedül. Akár adatot küldesz egy jelentésfeldolgozó csővezetékbe, akár csak egy gyors CSV‑szerű dumpra van szükséged, az export folyamatának elsajátítása órákat takaríthat meg a manuális másolás‑beillesztés helyett.

Ebben a bemutatóban lépésről‑lépésre végigvezetünk, hogyan vegyünk egy numerikus cellát, alkalmazzunk tudományos jelölést, és exportáljuk táblázatként a **ExportTableOptions** használatával. A végére lesz egy futtatható kódrészlet, megérted az egyes hívások *miért* fontosak, és tudni fogod, hogyan módosítsd a kódot nagyobb tartományok vagy különböző formátumok esetén.

## Előfeltételek

- .NET 6 vagy újabb (az API ugyanúgy működik a .NET Framework 4.7+ verziókon)
- Aspose.Cells for .NET telepítve (`Install-Package Aspose.Cells`)
- Alapvető C# szintaxis ismeret; mély Excel belső működés nem szükséges

Rendben van? Remek – vágjunk bele.

## 1. lépés: Exportálási beállítások konfigurálása – Hogyan exportáljunk cellatartományt táblázatként

Az első dolog, amire szükséged van, egy **ExportTableOptions** példány, amely megmondja a könyvtárnak, hogyan kezelje a cella tartalmát. Enélkül az export alapértelmezés szerint nyers numerikus értékeket ad, ami problémát okozhat a downstream fogyasztóknak, akik szöveget várnak.

```csharp
// Step 1: Define export options – export the cell value as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Return the cell content as text
    CustomFormat = "0.00E+00"       // Apply scientific notation format
};
```

**Miért fontos:**  
- `ExportAsString = true` arra kényszeríti a könyvtárat, hogy a cella megjelenített szövegét írja ki, ne pedig az alatta lévő double értéket.  
- `CustomFormat` lehetővé teszi a **tudományos jelöléses export** megadását, ami hasznos nagyon nagy vagy nagyon kis számok esetén.

> **Pro tipp:** Ha dátum vagy pénznem formátumra van szükséged, cseréld a `"0.00E+00"`‑t `"yyyy‑MM‑dd"`‑re vagy `"$#,##0.00"`‑ra megfelelően.

## 2. lépés: Workbook létrehozása és az első Worksheet lekérése – Workbook és Worksheet kezelése

A **Workbook** az egész Excel fájlt képviseli, míg a **Worksheet** egyetlen fület. Egy egyszerű exporthoz az első lapot használjuk, amely mindig a 0‑s indexen létezik.

```csharp
// Step 2: Create a new workbook and access the first worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

**Miért fontos:**  
Egy friss `Workbook` létrehozása tiszta kiindulási alapot biztosít – nincsenek rejtett stílusok vagy maradék adatok, amelyek akadályozhatnának. A `Worksheets[0]` a leggyorsabb módja az aktív lap elérésének anélkül, hogy a lap nevét kellene kezelni.

## 3. lépés: Célcella feltöltése – Cell Value Formatting C#

Most egy numerikus értéket helyezünk a **A1** cellába (0‑s sor, 0‑s oszlop). Az általunk választott érték szándékosan hosszú tizedesjegyű, hogy láthasd a tudományos jelölés működését.

```csharp
// Step 3: Insert a numeric value into cell A1 (row 0, column 0)
sheet.Cells[0, 0].PutValue(12345.6789);
```

**Miért fontos:**  
A `PutValue` automatikusan meghatározza a cella adattípusát. Mivel később stringként exportálunk, a nyers double a korábban beállított formátummal lesz konvertálva, így egy rendezett `"1.23E+04"` kimenetet kapunk.

## 4. lépés: A meghatározott cellatartomány exportálása táblázatként – Exportálás cellatartományként táblázatba

A beállítások és az adatok megvannak, az utolsó lépés, hogy az Aspose.Cells‑nek megmondjuk, írja ki a tartományt. Az `ExportTable` metódus a kezdősor/oszlop, a tartomány mérete és a korábban épített opciós objektum paramétereit várja.

```csharp
// Step 4: Export the defined cell range as a table using the options above
// Parameters: startRow, startColumn, totalRows, totalColumns, options
sheet.ExportTable(0, 0, 1, 1, exportOptions);
```

**Miért fontos:**  
- `totalRows = 1` és `totalColumns = 1` korlátozza az exportot egyetlen cellára, de ezeket a számokat bővítheted, hogy nagyobb blokkokat fedj le (pl. `5, 3` egy 5 soros × 3 oszlopos tartományhoz).  
- A metódus az adatot egy belső táblázatszerkezetbe írja, amely CSV‑ként, HTML‑ként vagy akár közvetlenül egy kliensnek streamelve is menthető.

### Eredmény mentése (opcionális)

Ha szeretnéd a exportált táblázatot lemezre menteni, írd ki CSV fájlba:

```csharp
// Optional: Save the exported table as CSV for verification
using (var stream = new MemoryStream())
{
    sheet.ExportTableToCSV(stream, exportOptions);
    File.WriteAllBytes("ExportedTable.csv", stream.ToArray());
}
```

A fenti kód futtatása egy olyan fájlt generál, amely a következőt tartalmazza:

```
1.23E+04
```

## Szélső esetek és gyakori variációk

| Helyzet | Mit kell módosítani | Ok |
|-----------|----------------|--------|
| **Több sor exportálása** | Állítsd be a `totalRows`‑t, és szükség esetén iterálj a sorokon | Lehetővé teszi a kötegelt exportot az `ExportTable` többszöri hívása nélkül |
| **Képletek megőrzése** | `ExportAsString = false` beállítása | Az eredeti képletet tartja meg a megjelenített érték helyett |
| **Eltérő elválasztók** | `ExportTableToCSV(..., ',', ...)` overload használata | Váltás a vessző‑elválasztottól tab‑ vagy pipe‑elválasztott értékekre |
| **Nagy munkalapok** | Streameld az exportot, hogy elkerüld az `OutOfMemoryException`‑t | Jól működik >10 000 sor esetén |

## Teljes működő példa

Az alább látható a komplett, másolás‑beillesztés‑kész program. Bármely .NET konzolos projekttel lefordítható, amely hivatkozik az Aspose.Cells‑re.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class ExportCellRangeDemo
{
    static void Main()
    {
        // 1️⃣ Define export options – how to export cell range as table
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            CustomFormat = "0.00E+00"
        };

        // 2️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Put a numeric value into A1
        sheet.Cells[0, 0].PutValue(12345.6789);

        // 4️⃣ Export the single‑cell range as a table
        sheet.ExportTable(0, 0, 1, 1, exportOptions);

        // Optional: write to CSV to see the result
        using (var ms = new MemoryStream())
        {
            sheet.ExportTableToCSV(ms, exportOptions);
            File.WriteAllBytes("ExportedTable.csv", ms.ToArray());
        }

        Console.WriteLine("Export complete! Check ExportedTable.csv");
    }
}
```

**Várt kimenet:**  
Egy `ExportedTable.csv` nevű fájl, amely egyetlen sort tartalmaz:

```
1.23E+04
```

Ha szövegszerkesztőben nyitod meg a CSV‑t, a tudományos jelölés pontosan úgy lesz alkalmazva, ahogy definiáltad.

## Összegzés

Áttekintettük, **hogyan exportáljunk cellatartományt táblázatként** a kezdetektől a befejezésig: `ExportTableOptions` beállítása, `Workbook` létrehozása, adat beszúrása, majd az `ExportTable` meghívása. Az egyes lépések megértésével most már skálázhatod a megoldást nagyobb tartományokra, különböző formátumokra, vagy akár egy web‑API‑ba is beépítheted, amely Excel‑alapú adatokat szolgáltat „on‑the‑fly”.

A jövőben érdemes megvizsgálni:

- **ExportTableToHTML** web‑kész előnézetekhez  
- **ExportTableToDataTable** közvetlenül ADO.NET csövekbe való betápláláshoz  
- Haladó **custom formats** dátumok, pénznemek vagy százalékok számára  

Próbáld ki ezeket, és egy egyszerű cella‑exportot egy sokoldalú adat‑szállító motorra változtathatsz. Van kérdésed vagy egy különös felhasználási eseted? Írj kommentet lent – jó kódolást!


## Mit érdemes még megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden erőforrás komplett, működő kódrészleteket és lépésről‑lépésre magyarázatokat tartalmaz, hogy további API‑funkciókat saját projektjeidben is könnyedén alkalmazhasd.

- [Hogyan exportáljunk látható Excel sorokat Aspose.Cells for .NET‑el: Lépésről‑lépésre útmutató](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [Hogyan exportáljunk Excel fájlokat .NET‑ben Aspose.Cells‑szel: Átfogó útmutató](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [Hogyan érjünk el egy Excel cellát név alapján Aspose.Cells for .NET‑el: Lépésről‑lépésre útmutató](/cells/english/net/cell-operations/access-cell-by-name-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}