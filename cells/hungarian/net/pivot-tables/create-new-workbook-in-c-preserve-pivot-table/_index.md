---
category: general
date: 2026-02-15
description: Új munkafüzet létrehozása C#-ban és pivot tábla másolása a definíció
  elvesztése nélkül. Tanulja meg, hogyan másolhat sorokat, megőrizheti a pivot táblát,
  és könnyen duplikálhatja azt.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- duplicate pivot table
language: hu
og_description: Új munkafüzet létrehozása C#‑ban és egy pivot tábla másolása a definíciójának
  megőrzésével. Lépésről‑lépésre útmutató fejlesztőknek.
og_title: Új munkafüzet létrehozása C#-ban – Pivot tábla megőrzése
tags:
- Aspose.Cells
- C#
- Excel automation
title: Új munkafüzet létrehozása C#-ban – Pivot tábla megőrzése
url: /hu/net/pivot-tables/create-new-workbook-in-c-preserve-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Új munkafüzet létrehozása C#‑ban – Pivot tábla megőrzése

Valaha is szükséged volt **új munkafüzet** létrehozására C#‑ban, amely pontos másolata egy másik fájlban lévő pivot táblának? Nem vagy egyedül. Sok jelentéskészítési folyamatban a pivot tábla a elemzés szíve, és az adat áthelyezésekor a definíció elvesztése rémálom.

A jó hír? Néhány Aspose.Cells sorral másolhatod a sorokat – beleértve a pivot táblát – egy friss munkafüzetbe, és minden változatlanul megmarad. Az alábbiakban **hogyan másolj sorokat**, **megőrizd a pivot tábla** beállításait, és akár **duplikáld a pivot táblát** fájlok között anélkül, hogy a képletek vagy a gyorsítótár megsérülne.

## Mit fed le ez a bemutató

Ebben az útmutatóban a következőket járjuk körül:

1. A forrás munkafüzet betöltése, amely már tartalmaz egy pivot táblát.  
2. **Új munkafüzet** objektumok létrehozása a célhoz.  
3. A `CopyRows` használata a pivot táblát tartalmazó tartomány átviteléhez.  
4. Az eredmény mentése úgy, hogy a pivot tábla továbbra is működőképes maradjon.  

Külső dokumentációra nincs szükség – csak a kód, a magyarázat és néhány gyakorlati tipp, amelyet közvetlenül beilleszthetsz a projektedbe.

> **Pro tipp:** Az Aspose.Cells működik .NET Core, .NET Framework és még Xamarin környezetben is, így ugyanaz a kódrészlet bárhol futtatható, ahol szükséged van rá.

---

![Új munkafüzet létrehozása másolt pivot táblával](/images/create-new-workbook-pivot.png "új munkafüzet létrehozása másolt pivot táblával")

## 1. lépés – Új munkafüzet létrehozása és a forrásfájl betöltése

Az első dolog, amit teszünk, **új munkafüzet** objektumok létrehozása. Az egyik a eredeti adatokat tartja, a másik a másolt tartományt fogja megkapni.

```csharp
using Aspose.Cells;

// Load the source workbook that already contains a pivot table
var sourceWorkbook = new Workbook(@"C:\Data\source.xlsx");

// Create an empty workbook that will become the destination
var destinationWorkbook = new Workbook();
```

*Miért fontos:*  
A `Workbook` az Excel manipulációjának belépési pontja az Aspose.Cells‑ben. Egy friss munkafüzet példányosításával biztosítjuk a tiszta kiindulási állapotot – nincsenek rejtett stílusok vagy felesleges munkalapok, amelyek később problémát okozhatnának.

## 2. lépés – Sorok másolása pivot táblával együtt

Most jön a probléma középpontja: **hogyan másolj sorokat**, amelyek a pivot táblát körülveszik anélkül, hogy azt "laposítanák". A `CopyRows` metódus pontosan ezt teszi.

```csharp
// Copy the first 20 rows (adjust as needed) from the source to the destination
// Parameters: startRow, totalRows, targetCells, targetStartRow
sourceWorkbook.Worksheets[0].Cells.CopyRows(
    startRow: 0,
    totalRows: 20,
    targetCells: destinationWorkbook.Worksheets[0].Cells,
    targetStartRow: 0);
```

Néhány fontos megjegyzés:

* A `startRow` és a `totalRows` határozza meg a pivot táblát tartalmazó blokkot.  
* A metódus **mindkettőt** másolja: a nyers adatokat és a pivot gyorsítótárat, így a cél munkafüzet tudja, hogyan építse újra a pivot táblát a futás során.  
* Ha a pivot mélyebben kezdődik a munkalapon, csak módosítsd a indexeket – nincs szükség másik API hívásra.

> **Gyakori kérdés:** *Elveszíti-e a másolt pivot a forrásadat-referenciáját?*  
> Nem. Az Aspose.Cells a gyorsítótárat közvetlenül a munkalapba ágyazza, így a pivot önállóvá válik az új fájlban.

## 3. lépés – Pivot tábla megőrzése a cél mentésekor

Miután a sorok másolásra kerültek, a pivot tábla a cél munkafüzetben pontosan úgy él, mint a forrásban. A fájl mentése egyszerű.

```csharp
// Save the destination workbook; the pivot table remains functional
destinationWorkbook.Save(@"C:\Data\destination.xlsx");
```

Amikor megnyitod a `destination.xlsx` fájlt Excelben, a pivot tábla készen áll a frissítésre. A **pivot tábla megőrzése** viselkedés automatikus, mivel a gyorsítótár a sorokkal együtt utazott.

### Az eredmény ellenőrzése

Nyisd meg a fájlt, és:

1. Kattints a pivot táblára.  
2. Figyeld meg, hogy megjelenik a mezőlista – ez azt jelenti, hogy a gyorsítótár érintetlen.  
3. Próbálj meg frissíteni; az adatok hibák nélkül frissülnek.

Ha *#REF!* hibát látsz, ellenőrizd, hogy a másolt tartomány tartalmazza-e a rejtett gyorsítótár sorait (általában a látható adatok után).

## 4. lépés – Pivot tábla duplikálása több munkafüzetbe (opcionális)

Néha ugyanazt a pivot táblát több jelentésben is szükséges használni. Az általunk most használt minta könnyen skálázható – egyszerűen ismételd meg a másolást minden új munkafüzethez.

```csharp
string[] targets = {
    @"C:\Reports\Q1.xlsx",
    @"C:\Reports\Q2.xlsx",
    @"C:\Reports\Q3.xlsx"
};

foreach (var path in targets)
{
    var wb = new Workbook(); // fresh workbook each loop
    sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 20, wb.Worksheets[0].Cells, 0);
    wb.Save(path);
}
```

Ez a kódrészlet **duplikálja a pivot táblát** háromszor egyetlen ciklusban. Állítsd be a `targets` tömböt a jelentési ütemtervednek megfelelően.

### Figyelemre méltó széljegyek

| Helyzet | Mire figyelj | Javítás |
|-----------|-------------------|-----|
| A pivot külső adatforrást használ | A gyorsítótár egy olyan kapcsolatra hivatkozhat, amely az új gépen nem létezik | Ágyazd be az adatforrást, vagy hozd létre a kapcsolatot a cél munkafüzetben |
| Nagyon nagy pivot ( > 100 k sor ) | A `CopyRows` memóriaigényes lehet | Használd a `CopyRows`‑t darabokban, vagy fontold meg a `Copy`‑t `PasteOptions`‑szel a memóriahasználat korlátozásához |
| A munkalapon rejtett sorok/oszlopok vannak | A rejtett gyorsítótár sorok kimaradhatnak, ha csak a látható sorokat másolod | Mindig másold a pontos sor tartományt, amely a gyorsítótárat tartalmazza, ne csak a látható területet |

## Teljes működő példa

Összegezve, itt egy önálló program, amelyet beilleszthetsz egy konzolalkalmazásba.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook (contains the original pivot)
            var sourcePath = @"C:\Data\source.xlsx";
            var sourceWorkbook = new Workbook(sourcePath);

            // 2️⃣ Prepare destination workbook
            var destinationWorkbook = new Workbook();

            // 3️⃣ Copy rows that include the pivot (adjust range as needed)
            sourceWorkbook.Worksheets[0].Cells.CopyRows(
                startRow: 0,
                totalRows: 20,
                targetCells: destinationWorkbook.Worksheets[0].Cells,
                targetStartRow: 0);

            // 4️⃣ Save – the pivot table is preserved
            var destPath = @"C:\Data\destination.xlsx";
            destinationWorkbook.Save(destPath);

            Console.WriteLine("Pivot table successfully copied!");
        }
    }
}
```

Futtasd a programot, nyisd meg a `destination.xlsx` fájlt, és ugyanazt a pivot táblát fogod látni, készen arra, hogy szeleteld és darabold az adataidat. Nincs szükség manuális újraalkotásra.

---

## Összegzés

Megmutattuk, hogyan **hozhatsz létre új munkafüzetet** C#‑ban és **másolhatsz pivot táblát**, miközben minden beállítás megmarad. A `CopyRows` használatával megbízható módot kapsz a **pivot tábla megőrzésére**, megválaszolod a régóta fennálló „**hogyan másolj sorokat**” kérdést, és akár **duplikálhatod a pivot táblát** több jelentésben is minimális kóddal.

Mi a következő lépés? Próbáld meg módosítani a másolt tartományt, hogy diagramokat is tartalmazzon, amelyek ugyanarra a pivot táblára hivatkoznak, vagy kísérletezz a `PasteOptions`‑szel a formázás pontos megtartásához. Ugyanez a minta működik más Aspose.Cells objektumokra is, például táblákra és névvel ellátott tartományokra, szóval bátran bővítsd.

Van egy sajátos helyzeted – például egy pivot, amely külső adatbázisból húz, vagy egy felhőben élő munkafüzet? Írj egy megjegyzést alább, és együtt megoldjuk. Boldog kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}