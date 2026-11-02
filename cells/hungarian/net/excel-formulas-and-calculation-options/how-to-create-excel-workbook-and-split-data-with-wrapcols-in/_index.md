---
category: general
date: 2026-10-10
description: Excel munkafüzet létrehozása C#‑ban és a WRAPCOLS függvény használata
  a tömbadatok oszlopokra bontásához. Kövess egy teljes lépésről‑lépésre útmutatót
  futtatható kóddal.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: hu
lastmod: 2026-10-10
og_description: Excel munkafüzet létrehozása C#-ban, és a WRAPCOLS függvény alkalmazása
  a tömbadatok oszlopokra bontásához. Ez az útmutató megmutatja a teljes kódot, és
  lépésről lépésre magyarázza.
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: Excel munkafüzet létrehozása és adatok felosztása WRAPCOLS-szal C#-ban
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  headline: How to create Excel workbook and split data with WRAPCOLS in C#
  type: TechArticle
- description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  name: How to create Excel workbook and split data with WRAPCOLS in C#
  steps:
  - name: Using the function with different data types
    text: 'The `WRAPCOLS` function is not limited to numbers. You can split text values,
      dates, or mixed types:'
  - name: Variable column count at runtime
    text: 'Often the number of columns you need depends on user input. You can build
      the formula string dynamically:'
  - name: Large arrays and performance
    text: '`WRAPCOLS` can handle thousands of elements, but evaluating extremely large
      arrays in a single cell may increase calculation time. If you notice slowdown:'
  - name: Handling empty cells
    text: If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS`
      inserts blank cells, preserving the column layout. This behavior is useful when
      you need placeholder columns for later data entry.
  - name: Using named ranges instead of literals
    text: 'For maintainability, define a named range that holds the source data, then
      reference it:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hogyan hozhatunk létre Excel munkafüzetet, és oszthatjuk fel az adatokat a
  WRAPCOLS segítségével C#-ban
url: /hu/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan hozzunk létre Excel munkafüzetet és bontsuk fel az adatokat a WRAPCOLS segítségével C#-ban

Ha programozott módon **Excel munkafüzetet** kell létrehoznod, ez az útmutató pontosan megmutatja, hogyan teheted ezt meg, valamint hogyan **bontsd fel a tömb adatokat** oszlopokba a `WRAPCOLS` függvény használatával. Teljes, futtatható példát kapsz, amely egy `.xlsx` fájlt hoz létre, a data három oszlopba elosztva.

A tutorial mindent lefed, amire szükséged lehet: a szükséges NuGet csomagok, a kódsorok magyarázata, hogy miért működik a `WRAPCOLS` képlet, és hogyan adaptálhatod a megoldást különböző tömbméretek vagy oszlopszámok esetén. A végére képes leszel beágyazni a **use wrapcols function** technikát bármely C# projektbe, amely Excel fájlokat generál.

## Előfeltételek

Mielőtt elkezdenéd, győződj meg róla, hogy rendelkezel:

* .NET 6.0 SDK vagy újabb telepítve  
* C# IDE-vel (Visual Studio, VS Code, Rider, stb.)  
* **Aspose.Cells for .NET** NuGet csomaggal – a könyvtár, amely a példákban használt `Workbook` osztályt biztosítja  

Nem szükséges Office telepítés; az Aspose.Cells közvetlenül írja a `.xlsx` fájlt.

## 1. lépés – Excel munkafüzet létrehozása

Az első feladat egy új workbook objektum példányosítása és az első munkalapra való hivatkozás megszerzése. Ez a lépés minden további manipuláció alapja.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();                // creates an empty Excel file in memory
        Worksheet ws = wb.Worksheets[0];             // the default worksheet is at index 0
```

`Workbook` a teljes fájlt képviseli, míg a `Worksheet` egyetlen lapot. A munkafüzet memóriában történő létrehozásával elkerülöd a lemez‑I/O‑t, amíg explicit módon nem mented el.

## 2. lépés – WRAPCOLS alkalmazása a tömboszlopok felosztásához

Most egy képletet helyezel el az **A1** cellában, amely a `WRAPCOLS` függvényt használja. A függvény két argumentumot kap: a forrás tömböt és a kívánt oszlopszámot, amelybe a tömböt szeretnéd csomagolni.

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**Miért működik ez:** `WRAPCOLS` a lapos `{1,2,3,4,5,6}` tömböt soronként tölti ki, három oszlopot hozva létre soronként. Az első argumentum lehet bármilyen Excel tömbliterál, egy névvel ellátott tartomány vagy egy dinamikus tömbképlet. A második argumentum (`3`) azt mondja meg az Excelnek, hány oszlopot generáljon, mielőtt a következő sorba lépne.

### A függvény használata különböző adattípusokkal

A `WRAPCOLS` függvény nem csak számokra korlátozódik. Szöveges értékeket, dátumokat vagy vegyes típusokat is fel lehet osztani:

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

Amikor a forrás tömb karakterláncokat tartalmaz, az Excel automatikusan szövegcellákként kezeli az eredményt. Ez a rugalmasság lehetővé teszi, hogy **excel formula split data** jelentésekhez, irányítópultokhoz vagy adat‑migrációs feladatokhoz használj.

## 3. lépés – képletek kiszámítása a munkalap feltöltéséhez

A képletek karakterláncként tárolódnak, amíg a workbook nem kérdezi le a kiértékelésüket. A `CalculateFormula` hívása kényszeríti a kiértékelést, és az eredményeket a cellákba írja.

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

Ez a hívás nélkül a mentett fájl csak a képlet szövegét tartalmazná, nem a kiszámított értékeket. A metódus az egész munkafüzetre vonatkozik, így további képleteket is elhelyezhetsz máshol, és mindegyik egyetlen hívással feloldódik.

## 4. lépés – a munkafüzet mentése a végeredmény megtekintéséhez

Végül írd a munkafüzetet a lemezre. Válassz egy mappát, amelyhez írási jogosultságod van, és adj a fájlnak egy egyértelmű nevet.

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

Amikor megnyitod a `output.xlsx` fájlt Excelben (vagy bármely kompatibilis megjelenítőben), a következőt fogod látni:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

Ha a vegyes‑típusú példát használtad, a 3‑4. sorok a szöveget és a számokat tartalmazzák a megfelelő módon.

## Haladó változatok és szélső‑eset kezelése

### Változó oszlopszám futásidőben

Gyakran a szükséges oszlopszám a felhasználói bemenettől függ. Dinamikusan építheted fel a képlet karakterláncát:

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### Nagy tömbök és teljesítmény

A `WRAPCOLS` több ezer elemet is képes kezelni, de egyetlen cellában nagyon nagy tömbök kiértékelése növelheti a számítási időt. Ha lassulást észlelsz:

* Törd fel a forrás tömböt kisebb darabokra, és írd őket külön kezdőcellába.  
* Használd a `WorkbookSettings`-et a több szálú számítás engedélyezéséhez:

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### Üres cellák kezelése

Ha a forrás tömb üres karakterláncokat (`""`) vagy `NULL` értékeket tartalmaz, a `WRAPCOLS` üres cellákat szúr be, megőrizve az oszlopszerkezetet. Ez a viselkedés akkor hasznos, amikor későbbi adatbevitelhez helyőrző oszlopokra van szükség.

### Névtelen tartományok használata literálok helyett

A karbantarthatóság érdekében definiálj egy névtelen tartományt, amely a forrás adatot tartalmazza, majd hivatkozz rá:

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

Most a képlet a munkalapról olvassa az adatokat, lehetővé téve a **how to use wrapcols** dinamikus jelentéskészítési forgatókönyvekben.

## Gyakori hibák és profi tippek

* **Ne hagyd ki a második argumentumot.** `WRAPCOLS(array)` oszlopszám nélkül egyetlen oszlopot ad vissza, ami aláássa az adatfelosztás célját.  
* **Kerüld a tömbdimenziók keverését.** A forrás tömbnek egydimenziósnek kell lennie; kétdimenziós tömb (pl. `{ {1,2},{3,4} }`) `#VALUE!` hibát eredményez.  
* **Ments a számítás után.** Ha a `wb.Save`-et a `CalculateFormula` előtt hívod, a fájl csak a képlet szövegét tartalmazza.  
* **Ellenőrizd a fájl jogosultságokat.** Korlátozott környezetben (pl. ASP.NET) győződj meg róla, hogy a folyamat identitása írni tud a célmappába.  

## Teljes működő példa

Az alábbi teljes programot másolhatod, beillesztheted és futtathatod. Tartalmazza az összes importot, hibakezelést és megjegyzést.

```csharp
using System;
using Aspose.Cells;

class ExcelWrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Split a numeric array into 3 columns
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

        // Split a mixed array (text + numbers) into 3 columns, starting at row 3
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";

        // Dynamically build a formula with a variable column count
        int columnCount = 4;
        string sourceArray = "{10,20,30,40,50,60,70,80}";
        ws.Cells[5, 0].Formula = $"=WRAPCOLS({sourceArray},{columnCount})";

        // Evaluate all formulas
        wb.CalculateFormula();

        // Save the workbook
        string outputPath = "output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

A program futtatása `output.xlsx` fájlt hoz létre, három különálló területtel, amelyek **excel formula split data** használatával mutatják be a `WRAPCOLS` függvény működését.

## Következtetés

Most már tudod, hogyan **create Excel workbook** fájlokat kell készíteni C#‑ban, és hogyan **use wrapcols function**‑t kell alkalmazni a **split array columns** hatékony felosztásához. Az alapvető lépések – a `Workbook` példányosítása, a `WRAPCOLS` képlet beillesztése, a számítás és a mentés – újrahasználható mintát adnak bármely automatizálási feladathoz, amely oszlopok közötti adat elosztást igényel.

Innen tovább:

* Kombináld a `WRAPCOLS`‑t más dinamikus tömbfüggvényekkel, mint a `FILTER` vagy a `SORT`.  
* Exportálj nagy adatkészleteket adatbázisokból, és hagyd, hogy az Excel automatikusan elrendezze őket.  
* Készíts felhasználó‑vezérelt jelentéseket, ahol az oszlopszám egy UI vezérlőből választható.

Kísérletezz különböző tömbforrásokkal, oszlopszámokkal és további képletekkel, hogy bővítsd ezt az alapot. Boldog kódolást!

## Mit érdemes még megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Create Excel Workbook – Convert Array to Matrix with WRAPCOLS](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [Create Excel Workbook C# – Step‑by‑Step Guide](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}