---
category: general
date: 2026-11-16
description: Tanulja meg, hogyan lehet kibővíteni a tömböt az Excelben az Aspose.Cells,
  a dinamikus tömbfüggvények és egy lambda redukáló segítségével, majd C#‑ból írja
  ki az Excel‑fájlt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: hu
lastmod: 2026-11-16
og_description: Hogyan bővítsük a tömböt Excelben az Aspose.Cells, dinamikus tömbfüggvények
  és egy lambda redukáló segítségével. Kövesse a teljes C# példát az Excel fájl írásához.
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: Hogyan bővítsük a tömböt Excelben az Aspose.Cells segítségével – lépésről
  lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hogyan bővítsük a tömböt Excelben az Aspose.Cells segítségével
url: /hu/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan bővítsünk tömböt Excelben az Aspose.Cells segítségével

Ha **hogyan bővítsünk tömböt** egy Excel munkalapon C#‑ból, ez a tutorial pontos lépéseket mutat. Létrehozunk egy Excel munkafüzetet, dinamikus tömbfüggvényeket használunk, mint a `EXPAND` és a `REDUCE`, alkalmazunk egy **lambda** akumulátort, és végül **írjuk ki az Excel fájlt** a lemezre. A megközelítés az Aspose.Cells 23.10 vagy újabb verzióval működik, és nem igényel manuális Excel telepítést.

A útmutató végére egy teljesen működő `ExpandReduceDemo.xlsx` fájlt kapunk, amely bemutatja a dinamikus tömbképletek erejét programozott környezetben.

## Amire szükséged lesz

- .NET 6.0 (vagy bármely, az Aspose.Cells által támogatott .NET verzió)
- Aspose.Cells for .NET csomag (`dotnet add package Aspose.Cells`)
- Kódszerkesztő vagy IDE (Visual Studio, VS Code, Rider, stb.)

További COM interop vagy Office telepítés nem szükséges, mivel az Aspose.Cells belsőleg kezeli a fájlformátumot.

## 1. lépés: Excel munkafüzet létrehozása

Az első feladat a **excel munkafüzet** memóriában való **létrehozása**. Az Aspose.Cells a `Workbook` osztályt biztosítja, amely egy teljes XLSX fájlt képvisel.

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **Miért fontos:** Egy `Workbook` példányosítása tiszta vásznat ad. Az alapértelmezett munkalap már elő van készítve, így nem kell manuálisan hozzáadni, kivéve ha több lapra van szükség.

## 2. lépés: Függőleges tömbkonstans beszúrása

Az Excel dinamikus tömbmotorja képes literális tömbkonstansokkal dolgozni. A `{1;2;3;4;5}` függőleges tömböt helyezzük az **A1** cellába.

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **Tipp:** A pontosvessző (`;`) sorokat választ el a konstansban, míg a vessző (`,`) oszlopokat. Ez tükrözi az Excel saját szintaxisát.

## 3. lépés: A tömb kiterjesztése mátrixszá

Most válaszolunk a fő kérdésre – **hogyan bővítsünk tömböt** – a `EXPAND` függvény segítségével. A képlet a egyoszlopos tömböt 5 × 2‑es mátrixszá bővíti, a **B1** cellától kezdve.

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **Miért az EXPAND?** `EXPAND(source, rows, cols)` arra kényszeríti a forrás tartományt, hogy a megadott méretet foglalja el, szükség esetén üres cellákkal kitöltve. Ez a legátláthatóbb módja egy nagyobb mátrix előállításának egyetlen tömbből.

## 4. lépés: A mátrix csökkentése lambda akumulátorral

A `REDUCE` függvény egy tartományon iterál, és a **lambda** kifejezéssel aggregálja az értékeket. Itt minden oszlop értékét összegezzük egyetlen oszlopba, az eredményt a **D1** cellába helyezve.

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **Hogyan használjuk a lambdát:** A `LAMBDA(acc, val, acc+val)` megkapja a jelenlegi akumulátort (`acc`) és a következő cella értékét (`val`). Visszaadja az új akumulátort, így futó összeget számol. Ez demonstrálja, **hogyan használjuk a lambdát** Excel képletekben kódból.

## 5. lépés: Képletek kiszámítása, hogy az eredmények megjelenjenek

Az Aspose.Cells nem számítja ki automatikusan a képleteket, amikor beállítod őket. A `CalculateFormula` hívása kényszeríti a motorot, hogy minden képletet kiszámítson a munkafüzetben.

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **Megjegyzés:** Ha a generált fájlt Excelben nyitod meg, az értékek már láthatók lesznek, mivel előre ki lettek számítva.

## 6. lépés: Excel fájl írása a lemezre

Végül a **excel fájl írása** a `Save` metódussal történik. Válassz egy olyan mappát, amelyhez írási jogosultsággal rendelkezel.

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Várt eredmény

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **B oszlop** és **C oszlop** tartalmazza az `EXPAND` által előállított 5 × 2‑es mátrixot.
- **D1 cella** `15`‑öt mutat, ami a `REDUCE` + **lambda** képlet által számított összeg.

## Gyakori kérdések és széljegyek

- **Bővíthetek több oszlopra, mint amennyi a forrásban van?**  
  Igen. Az `EXPAND` hiányzó oszlopokat üres cellákkal tölti fel. Ugyanez igaz a sorokra is.

- **Mi van, ha a forrás tömb vízszintes (`{1,2,3,4,5}`)?**  
  Az `EXPAND` egyetlen sorként kezeli a forrást; továbbra is megadhatod a sor- és oszlopszámot a átalakításhoz.

- **A `REDUCE` működik nem‑számtani adatokkal?**  
  A lambda-nak olyan értéket kell visszaadnia, amely kompatibilis az akumulátor típusával. Szövegösszefűzéshez használhatod például `LAMBDA(acc, val, acc & val)`‑t.

- **Kell-e minden változtatás után meghívni a `CalculateFormula`‑t?**  
  Csak akkor, ha a mentés előtt szükséged van a kiszámított értékekre. Excel megnyitáskor újraszámolja, ha kihagyod.

## Profi tippek

- **Teljesítmény:** Nagy munkafüzetek esetén hívd meg egyszer a `workbook.CalculateFormula`‑t minden képlet beállítása után, ne minden cellánál külön-külön.
- **Verzióbiztonság:** Az `EXPAND` és a `REDUCE` elérhető az Excel 365‑ben és későbbi verziókban. Az Aspose.Cells ezeket implementálja függetlenül a célnak szánt Excel verziótól, mivel a számítási motor beépített.
- **Képletek hibakeresése:** Használd a `sheet.Cells["B1"].Formula`‑t, hogy visszaolvasd a pontosan beállított képlet szövegét; ez segít dinamikus képletek építésekor.

## Összegzés

Most már tudod, **hogyan bővítsünk tömböt** Excelben az Aspose.Cells segítségével, hogyan használjunk **dinamikus tömbfüggvényeket**, alkalmazzunk egy **lambda**‑t a `REDUCE`‑dal, és hogyan **írjuk ki az excel fájlt** C#‑ból. Ez az vég‑től‑végig példát könnyen adaptálhatod összetettebb adattranszformációkra, például mátrix transzponálásra, kumulatív összegekre vagy egyedi aggregációkra.

---

*Következő lépések:*  
- Ismerd meg a többi dinamikus függvényt, mint a `FILTER`, `SORT` és `UNIQUE`.  
- Kombináld több `LAMBDA` kifejezést, hogy újrahasználható felhasználó‑definiált függvényeket hozz létre.  
- Integráld a munkafüzet-generálást ASP.NET Core API‑kba, hogy helyben, kérésre készülő jelentéseket állíts elő.


## Mit érdemes legközelebb megtanulni?


Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódpéldákat és lépésről‑lépésre magyarázatokat tartalmaz, hogy könnyedén elsajátíthasd az API további funkcióit, és alternatív megvalósítási módokat fedezhess fel saját projektjeidben.

- [How to create Excel workbook C# with a dynamic array formula](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [How to expand array in Excel and populate a template](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [How to Expand Array in C# with Aspose.Cells – Step‑by‑Step Guide](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}