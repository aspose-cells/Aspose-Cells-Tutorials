---
category: general
date: 2026-03-29
description: Tanulja meg, hogyan szúrjon be sorokat a GridJs-ben gyorsan. Ez az útmutató
  azt is bemutatja, hogyan adjon hozzá sorokat, és hogyan adjon hozzá több sort a
  rácshoz kötegelt művelettel.
draft: false
keywords:
- how to insert rows
- how to add rows
- add multiple rows grid
- batch row insertion
- large grid performance
language: hu
og_description: Tanulja meg, hogyan szúrjon be gyorsan sorokat a GridJs-ben. Ez az
  útmutató bemutatja, hogyan adjon hozzá sorokat, hogyan adjon hozzá több soros rácsot,
  és hogyan kezeljen nagy mennyiségű kötegelt beszúrást.
og_title: Hogyan szúrjunk be sorokat a GridJs-ben – Több sor hozzáadása a rácshoz
  hatékonyan
tags:
- GridJs
- C#
- data‑grid
title: Hogyan szúrjunk be sorokat a GridJs-ben – Több sor hozzáadása a rácshoz hatékonyan
url: /hu/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-grid-efficien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan szúrjunk be sorokat a GridJs‑ben – Több sor hozzáadása a rácshoz hatékonyan

Valaha is elgondolkodtál **hogyan szúrjunk be sorokat** egy hatalmas GridJs táblába anélkül, hogy lefagyna a felhasználói felület? Lehet, hogy elakadtál, miközben **sorokat** próbáltál egy‑esével hozzáadni, és a teljesítmény egyszerűen összeomlott. A jó hír, hogy a GridJs egy kötegelt API‑t kínál, amely lehetővé teszi, hogy **több sort adjunk hozzá a rácshoz** egyetlen hívásban, így a rendszer gyors marad még akkor is, ha milliók számát kell kezelni.

Ebben a tutorialban egy teljes, futtatható példán keresztül mutatjuk be, hogyan **szúrjunk be sorokat** a `InsertRowsBatch` használatával. Megtudod, miért fontos a kötegelt művelet, hogyan ellenőrizheted az eredményt, és mire kell figyelni, ha a cél index óriási. A végére magabiztosan tudsz majd ezer új rekordot beilleszteni bármely GridJs példányba.

## Előfeltételek

Mielőtt belevágnánk, győződj meg róla, hogy a következők rendelkezésre állnak:

- .NET 6.0 vagy újabb (a kód bármely friss SDK‑val lefordítható)
- Hivatkozás a `GridJs` NuGet csomagra (vagy a DLL‑re, ha egyedi buildet használsz)
- Alapvető C# ismeretek – nem kell guru lenned, csak kényelmesen kell tudnod osztályokkal és metódusokkal dolgozni
- Kedvenc IDE‑d vagy szerkesztőd (Visual Studio, Rider, VS Code… mind működik)

> **Pro tipp:** Ha valóban hatalmas rácsokkal (több tízmillió sor) dolgozol, engedélyezd a `gridJs.EnableVirtualization = true;` beállítást, hogy a UI renderelése könnyű maradjon.

## 1. lépés: A GridJs példány létrehozása és konfigurálása

Elsőként szükséged van egy élő `GridJs` objektumra. Gondolj rá úgy, mint egy vászonra, amelyre a sorokat festheted.

```csharp
using System;
using GridJsLibrary;   // Assume this is the namespace for GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Initialize the grid
            GridJs gridJs = new GridJs();

            // Optional: turn on virtualization for huge data sets
            gridJs.EnableVirtualization = true;

            // Populate the grid with some dummy data so we can see the effect
            SeedInitialData(gridJs);

            // Now we’re ready to insert rows in bulk
            InsertRowsInBatch(gridJs);
        }

        // Helper: add 2 000 000 rows so our batch lands at index 2 000 001
        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }
```

> **Miért fontos ez a lépés:** A rács inicializálása és esetleges adatbetöltése egy valós helyzetet szimulál, ahol a rács már nagy mennyiségű információt tartalmaz. A később végrehajtandó kötegelt beszúrásnak tisztelnie kell a null‑alapú indexelést, ezért előre feltöltjük a példát, hogy pontosan bemutassuk a beszúrási pontot.

## 2. lépés: `InsertRowsBatch` használata a **több sor hozzáadása a rácshoz** érdekében

Most jön a tutorial középpontja – a hívás, amely ténylegesen **sorokat ad hozzá** kötegelt módon. A metódus aláírása `InsertRowsBatch(int startIndex, int count)`. Példánkban a 2 000 000‑as indexnél (ami a 2 000 001‑edik sor) kezdünk, és tíz sort adunk hozzá.

```csharp
        // Step 2 – Insert a batch of rows
        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based, so this is row 2 000 001
            int rowsToAdd = 10;

            // The batch call creates placeholder rows; you can later populate them
            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Verify by reading back a few rows
            VerifyInsertion(grid, startIndex, rowsToAdd);
        }
```

> **Hogyan működik:** Az `InsertRowsBatch` belsőleg lefoglalja a kért számú sort, és lejjebb tolja a meglévő sorokat. Mivel a művelet egyetlen tranzakcióban történik, a UI csak egyszer frissül, ezért ez a módszer a **hogyan adjunk hozzá sorokat** hatékony megvalósítása.

## 3. lépés: A beszúrás ellenőrzése – A sorok a várt helyen landoltak-e?

A kötegelt művelet után szeretnéd megbizonyosodni arról, hogy a sorok ott vannak, ahol gondoltad. Az alábbi segédfüggvény kiolvassa az új blokk első és utolsó sorát, majd kiírja őket a konzolra.

```csharp
        // Step 3 – Simple verification
        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

**Várható kimenet**

```
Initial seed completed – 2 000 000 rows present.
Inserted 10 rows starting at index 2000001.
Verifying inserted rows:
Row 2000001: , 
Row 2000002: , 
...
Row 2000010: , 
```

A üres cellák azt jelzik, hogy a sorok helyőrzők, amelyek még adatot várnak. Most már egyenként feltöltheted őket, vagy indíthatsz egy újabb kötegelt frissítést.

> **Szél eset megjegyzés:** Ha a `startIndex` meghaladja a jelenlegi sorok számát, a GridJs automatikusan a végére fűzi az új sorokat. Negatív index esetén `ArgumentOutOfRangeException` keletkezik, ezért mindig ellenőrizd a felhasználó által megadott indexeket.

## 4. lépés: Az új sorok feltöltése (opcionális, de gyakori)

Gyakran nem csak üres sorokra van szükség, hanem értelmes adatokkal kell feltölteni őket. Végigiterálhatsz az újonnan létrehozott tartományon, és meghívhatod a `SetCell` vagy egy hasonló API‑t.

```csharp
        // Optional: fill the newly added rows with sample data
        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }
```

Például közvetlenül a kötegelt beszúrás után meghívhatod a `PopulateNewRows(gridJs, startIndex, rowsToAdd);`‑t, ha azonnal meg akarod jeleníteni a sorokat.

## 5. lépés: Teljesítmény tippek nagyon nagy rácsokhoz

Amikor **több sor hozzáadása a rácshoz** milliók nagyságában történik, tartsd szem előtt ezeket a trükköket:

1. **A köteg mérete számít** – 10 000 sor egyszerre beszúrása gyorsabb lehet, mint tíz különálló 1 000‑es köteg, mert minden köteg csak egy UI‑frissítést okoz.
2. **UI‑frissítések kikapcsolása** – Egyes GridJs verziókban elérhető a `grid.SuspendLayout()` / `grid.ResumeLayout()`. Csomagold be a kötegelt műveletet ezekkel, ha lagot észlelsz.
3. **Virtualizáció használata** – Ahogy korábban láttuk, az `EnableVirtualization` drámaian csökkenti a memóriahasználatot és a renderelési időt.
4. **Kerüld a mély másolatokat** – Adj egyszerű értéktípusokat vagy könnyű objektumokat a rácshoz; a nehéz objektumok klónozása lelassítja a rendszert.

## Teljes működő példa

Mindent összerakva, itt a teljes program, amelyet egyszerűen beilleszthetsz egy új konzolprojektbe:

```csharp
using System;
using GridJsLibrary;   // Replace with the actual namespace of your GridJs library

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            GridJs gridJs = new GridJs
            {
                EnableVirtualization = true
            };

            SeedInitialData(gridJs);
            InsertRowsInBatch(gridJs);
        }

        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }

        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based index for row 2 000 001
            int rowsToAdd = 10;

            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Optional: fill them with data
            PopulateNewRows(grid, startIndex, rowsToAdd);

            VerifyInsertion(grid, startIndex, rowsToAdd);
        }

        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }

        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

Futtasd a programot, és a konzol kimenete megerősíti, hogy a tíz sor a megfelelő helyre került, majd fel lett töltve.

## Összegzés

Áttekintettük, **hogyan szúrjunk be sorokat** a GridJs‑ben a kötegelt API segítségével, bemutattuk, **hogyan adjunk hozzá sorokat** hatékonyan, és megvizsgáltuk, hogyan **több sor hozzáadása a rácshoz** anélkül, hogy a UI elakadna. A legfontosabb tanulságok:

- Használd az `InsertRowsBatch(startIndex, count)`‑t minden kötegelt művelethez.
- Ellenőrizd az indexeket, és fontold meg a virtualizációt hatalmas adathalmazoknál.
- Töltsd fel a sorokat a köteg után, ha azonnali tartalomra van szükség.

Ezután érdemes lehet **hogyan töröljünk sorokat** felfedezni, megvalósítani **undo/redo** funkciókat a kötegelt szerkesztésekhez, vagy integrálni a GridJs‑t egy háttérszolgáltatással, amely igény szerint streameli az adatokat. Mindezek a témák közvetlenül az itt tanultakon alapulnak.

Nyugodtan kísérletezz – változtasd a köteg méretét, próbálj meg a rács legelső sorába beszúrni, vagy kombinálj több köteget egyetlen tranzakcióban. Minél többet játszol vele, annál magabiztosabb leszel a nagy méretű adatkezelésben.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}