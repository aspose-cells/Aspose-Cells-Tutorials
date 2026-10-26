---
category: general
date: 2026-10-26
description: Tanulja meg, hogyan használja a WRAPCOLS-t C#-ban egy tartomány oszlopokra
  bontásához, alkalmazza a WRAPROWS-t sorokhoz, és programozottan mentse a munkafüzetet
  XLSX formátumban.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split range into rows
- excel wrapcols example
- save workbook as xlsx
- create excel workbook programmatically
language: hu
lastmod: 2026-10-26
og_description: Hogyan használjuk a WRAPCOLS-t C#-ban az adatok oszlopokra bontásához,
  a WRAPROWS-t a sorokhoz, és hogyan menthetjük a munkafüzetet XLSX formátumban. Kövesse
  a teljes lépésről‑lépésre útmutatót.
og_image_alt: Screenshot illustrating how to use WRAPCOLS to split a range into columns
  in Excel
og_title: Hogyan használjuk a WRAPCOLS-t C#‑ban – tartományok felosztása és XLSX‑be
  mentés
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  headline: How to use WRAPCOLS in C# and save workbook as XLSX
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  name: How to use WRAPCOLS in C# and save workbook as XLSX
  steps:
  - name: What the saved file looks like
    text: 'When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:'
  - name: Changing the number of columns or rows
    text: '* **More columns:** Increase the second argument of `WRAPCOLS`. Example:
      `=WRAPCOLS(A1:A10,5)` creates five columns, leaving empty cells where data runs
      out. * **Dynamic column count:** Use a cell reference instead of a hard‑coded
      number. `=WRAPCOLS(A1:A10, G1)` where `G1` holds the desired column c'
  - name: Handling empty or non‑numeric cells
    text: WRAPCOLS and WRAPROWS ignore empty cells by default, but they preserve the
      order of non‑empty values. If you need to preserve blanks, wrap the source range
      with `IFERROR` or `TEXT` functions before applying WRAPCOLS.
  - name: Saving to other formats
    text: 'While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells
      supports many formats (`.xls`, `.csv`, `.pdf`, etc.):'
  - name: What’s next?
    text: '* Explore **conditional formatting** to highlight the spilled data. * Combine
      **WRAPCOLS** with **SORT** or **FILTER** for dynamic dashboards. * Use Aspose.Cells’
      **charting API** to visualize the rearranged data directly from code.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hogyan használjuk a WRAPCOLS-t C#-ban, és mentjük a munkafüzetet XLSX formátumban
url: /hu/net/row-and-column-management/how-to-use-wrapcols-in-c-and-save-workbook-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjuk a WRAPCOLS függvényt C#-ban és mentsük el a munkafüzetet XLSX formátumban

Ha szükséged van a **WRAPCOLS használatára** az Excel-fájlban lévő adatok átrendezéséhez, ez az útmutató egy teljes, futtatható megoldást mutat be. Megtekintheted egy **excel wrapcols példát**, megtanulhatod, hogyan **oszd fel a tartományt sorokra** a WRAPROWS segítségével, és befejezheted a **munkafüzet XLSX formátumban mentésével** — mindezt **programozottan**.

Az Excel-lel való munka C#-ból gyakran egy munkafüzet létrehozását, képletek alkalmazását és a fájl mentését jelenti. Az alábbi kód az Aspose.Cells könyvtárat használja, amely lehetővé teszi az Excel-fájlok manipulálását anélkül, hogy a Microsoft Office telepítve lenne. A tutorial végére képes leszel **excel munkafüzet programozott létrehozására**, az adatok vízszintes és függőleges felosztására, és egy tiszta `.xlsx` fájl előállítására, amely készen áll a további feldolgozásra.

## Előfeltételek

* .NET 6.0 vagy újabb (a kód .NET Framework 4.7+‑vel is működik)
* Hivatkozás a **Aspose.Cells** NuGet csomagra  
  ```bash
  dotnet add package Aspose.Cells
  ```
* Alapvető ismeretek C#-ban és Excel képletekben

## 1. lépés: A WRAPCOLS használata egy tartomány oszlopokra bontásához

A **WRAPCOLS** függvény egy egydimenziós tartományt vesz, és az értékeit a megadott számú oszlopra osztja szét. Ebben a példában az `A1:A10` tartomány értékeivel kezdünk, és a WRAPCOLS‑t arra kérjük, hogy három oszlopot hozzon létre.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is the “create excel workbook programmatically” step
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Populate source data for demonstration
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 0].PutValue($"Item {i + 1}");
        }

        // Apply WRAPCOLS: split A1:A10 into 3 columns starting at C1
        // The formula is entered in cell C1 (row 0, column 2)
        ws.Cells[0, 2].Formula = "=WRAPCOLS(A1:A10,3)";

        // -------------------------------------------------
        // Why this works:
        // -------------------------------------------------
        // * WRAPCOLS reads the source range (A1:A10) vertically.
        // * The second argument (3) tells Excel to create three columns.
        // * The function returns a 2‑dimensional array that Excel spills into the
        //   surrounding cells automatically.
        // -------------------------------------------------
```

> **Eredmény:** A `C1:E4` cellák most már az eredeti tíz elemet tartalmazzák három oszlopban elrendezve (az utolsó oszlop a maradék elemeket tartalmazza).

![Képernyőfelvétel, amely bemutatja a WRAPCOLS használatát egy tartomány oszlopokra bontásához Excelben](image-url.png)

## 2. lépés: Tartomány sorokra bontása a WRAPROWS segítségével

Míg a **WRAPCOLS** vízszintesen működik, a **WRAPROWS** a ellentétes feladatot végzi: egy tartományt a megadott számú sorra oszt szét. Itt a `B1:B10` értékeit vesszük, és két sorba rendezzük őket a `F1`-től kezdve.

```csharp
        // Populate a second source column for WRAPROWS
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 1].PutValue($"Value {i + 1}");
        }

        // Apply WRAPROWS: split B1:B10 into 2 rows starting at F1
        ws.Cells[0, 5].Formula = "=WRAPROWS(B1:B10,2)";

        // -------------------------------------------------
        // Why WRAPROWS is useful:
        // -------------------------------------------------
        // * It converts a vertical list into a matrix with the specified row count.
        // * Handy when you need to prepare data for pivot tables, charts, or
        //   reporting layouts that expect a horizontal orientation.
        // -------------------------------------------------
```

> **Eredmény:** A képlet a `F1:K2` cellákat tölti ki a tíz értékkel, amely két sorra van elosztva.

## 3. lépés: Munkafüzet mentése XLSX formátumban

A képletek alkalmazása után az utolsó lépés a fájl mentése. A **munkafüzet mentése xlsx‑ként** művelet a memóriában lévő munkafüzetet a modern OpenXML formátumban írja a lemezre.

```csharp
        // Save the workbook – this completes the “save workbook as xlsx” step
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "wrapcols_wraprows_output.xlsx");

        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### A mentett fájl kinézete

When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:

| C | D | E |
|---|---|---|
| Item 1 | Item 4 | Item 7 |
| Item 2 | Item 5 | Item 8 |
| Item 3 | Item 6 | Item 9 |
|        |        | Item 10 |

and

| F | G | H | I | J | K |
|---|---|---|---|---|---|
| Value 1 | Value 3 | Value 5 | Value 7 | Value 9 | |
| Value 2 | Value 4 | Value 6 | Value 8 | Value 10 | |

A képletek a cellákban maradnak, így a forrástartományok későbbi módosításai automatikusan tükröződnek.

## 4. lépés: Gyakori variációk és szélhelyzetek

### Az oszlopok vagy sorok számának módosítása

* **Több oszlop:** Növeld a `WRAPCOLS` második argumentumát.  
  Példa: `=WRAPCOLS(A1:A10,5)` öt oszlopot hoz létre, üres cellákat hagyva ott, ahol az adatok elfogynak.
* **Dinamikus oszlopszám:** Használj cellahivatkozást a keményen kódolt szám helyett.  
  `=WRAPCOLS(A1:A10, G1)`, ahol a `G1` tartalmazza a kívánt oszlopszámot.

### Üres vagy nem numerikus cellák kezelése

A WRAPCOLS és a WRAPROWS alapértelmezés szerint figyelmen kívül hagyják az üres cellákat, de megőrzik a nem üres értékek sorrendjét. Ha a szóközöket is meg kell tartani, a forrástartományt csomagold `IFERROR` vagy `TEXT` függvényekkel a WRAPCOLS alkalmazása előtt.

### Mentés más formátumokba

Miközben ez az útmutató a **munkafüzet mentésére xlsx‑ként** fókuszál, az Aspose.Cells számos formátumot támogat (`.xls`, `.csv`, `.pdf`, stb.):

```csharp
workbook.Save("output.pdf", SaveFormat.Pdf);   // Export to PDF
workbook.Save("output.csv", SaveFormat.Csv);   // Export to CSV
```

## Profi tippek és buktatók

* **Pro tipp:** Állítsd be a `Workbook.Settings.CalcEngineEnabled = true` értéket, ha a mentés után azonnal szeretnéd kiértékelni a képleteket.
* **Vigyázz:** Nagy forrástartományok nagyon nagy spill területeket hozhatnak létre, ami befolyásolhatja a teljesítményt. Korlátozd a tartomány méretét, vagy oszd fel a műveletet több munkalapra.
* **Szálbiztonság:** Az Aspose.Cells objektumok **nem** szálbiztosak. Hozz létre egy külön `Workbook` példányt szálanként, ha párhuzamosan dolgozol fájlokkal.

## Következtetés

Most már tudod, **hogyan használjuk a WRAPCOLS‑t** egy függőleges tartomány több oszlopra bontásához, **hogyan bontsuk fel a tartományt sorokra** a WRAPROWS‑szal, és **hogyan mentsük el a munkafüzetet XLSX‑ként** a transzformációk után. A fenti lépések követésével **excel munkafüzetet hozhatsz létre programozottan**, erőteljes spill képleteket alkalmazhatsz, és kész‑megosztható Excel fájlokat generálhatsz manuális beavatkozás nélkül.

### Mi a következő?

* Fedezd fel a **feltételes formázást**, hogy kiemeld a spill adatokat.
* Kombináld a **WRAPCOLS**‑t a **SORT** vagy **FILTER** függvényekkel dinamikus irányítópultokhoz.
* Használd az Aspose.Cells **diagram API‑ját**, hogy közvetlenül a kódból megjelenítsd az átrendezett adatokat.

Boldog kódolást, és élvezd az Excel munkafolyamatok automatizálását!

## Mit érdemes még megtanulni?

A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [hogyan használjuk a wrapcols‑t C#‑ban – Teljes útmutató Excel WRAPROWS‑szal és képletek újraszámolásával](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [Hogyan használjuk a WRAPCOLS‑t C#‑ban – Tömb átalakítása mátrixszá Excelben](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)
- [Hogyan használjuk a WRAPCOLS‑t – Teljes útmutató C# Excel automatizáláshoz](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}