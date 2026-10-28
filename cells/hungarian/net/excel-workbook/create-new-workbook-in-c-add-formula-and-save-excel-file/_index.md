---
category: general
date: 2026-02-23
description: Új munkafüzet létrehozása programozottan C#-ban, és képlet hozzáadása
  egy cellához. Tanulja meg, hogyan kell használni az EXPAND-et, majd könnyedén mentse
  el az Excel munkafüzetet.
draft: false
keywords:
- create new workbook
- add formula to cell
- save excel workbook
- how to use expand
- create excel file programmatically
language: hu
og_description: Hozzon létre új munkafüzetet programozottan C#-ban. Adjon képletet
  egy cellához, tanulja meg az EXPAND használatát, és mentse el az Excel munkafüzetet
  néhány másodperc alatt.
og_title: Új munkafüzet létrehozása C#-ban – Képlet hozzáadása és Excel fájl mentése
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Új munkafüzet létrehozása C#-ban – képlet hozzáadása és Excel-fájl mentése
url: /hu/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Új munkafüzet létrehozása C#-ban – Képlet hozzáadása és Excel fájl mentése

Gondolkodtál már azon, hogyan lehet **create new workbook** objektumokat kódolásból létrehozni anélkül, hogy valaha megnyitnád az Excelt? Nem vagy egyedül. Sok fejlesztő akad el, amikor egy táblázatot kell gyorsan generálni – lehet ez egy jelentés, egy export, vagy egy gyors adatkiíratás.  

A jó hír? Ebben az útmutatóban pontosan megmutatjuk, hogyan **create new workbook**, hogyan **add formula to cell**, majd hogyan **save excel workbook** csak néhány C#-sorral. Emellett elmerülünk a **how to use expand** témában, hogy manuális másolás nélkül tudj dinamikus tömböket generálni. A végére képes leszel **create excel file programmatically** létrehozni és felhasználóknak vagy downstream szolgáltatásoknak továbbküldeni.

## Előfeltételek

- .NET 6.0 vagy újabb (bármely friss .NET runtime működik)
- Aspose.Cells for .NET (ingyenes próba vagy licencelt verzió) – ez a könyvtár biztosítja a `Workbook` és `Worksheet` osztályokat, amelyeket alább használunk.
- Alapvető C# szintaxis ismeret – mély Excel tudás nem szükséges.

Ha már megvannak, nagyszerű! Ha nincs, szerezd be az Aspose.Cells-t a NuGet-ről (`Install-Package Aspose.Cells`), és már készen állsz a munkára.

---

## 1. lépés: Új munkafüzet létrehozása – Az alap

Kezdésként egy új munkafüzet objektumot kell példányosítanunk. Gondolj rá úgy, mint egy vadonatúj, teljesen üres Excel fájl megnyitására.

```csharp
using Aspose.Cells;

public class ExcelGenerator
{
    public void Generate()
    {
        // Step 1: Create a new workbook (this is the core of create new workbook)
        Workbook workbook = new Workbook();
```

> **Miért fontos ez:** A `Workbook` osztály bármely Excel-művelet belépési pontja. Új példány létrehozásával memóriát foglalunk a munkalapok, stílusok és képletek számára – anélkül, hogy a fájlrendszert érintenénk.

---

## 2. lépés: Az első munkalap elérése

Minden új munkafüzet tartalmaz egy alapértelmezett munkalapot (neve *Sheet1*). Megkapjuk, hogy adatokat és képleteket helyezhessünk el benne.

```csharp
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tipp:** Ha több munkalapra van szükséged, egyszerűen hívd meg a `workbook.Worksheets.Add("MySheet")` metódust, és a visszaadott `Worksheet` objektummal dolgozz.

---

## 3. lépés: Képlet hozzáadása cellához – EXPAND használata

Most jön a szórakoztató rész: képlet beillesztése. Az `EXPAND` függvény tökéletes, ha egy statikus tömböt nagyobb, automatikusan kitöltött tartománnyá szeretnél alakítani.

```csharp
        // Step 3: Add formula to cell A1 using EXPAND
        // This creates a 5‑row array from the constant {1,2,3}
        worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";
```

### Hogyan működik az EXPAND képlet

| Argumentum | Jelentés |
|------------|----------|
| `{1,2,3}`  | A forrás tömb (három szám vízszintes listája) |
| `5`        | A kívánt sorok száma az eredményben |
| `1`        | A kívánt oszlopok száma (tartsd 1‑en, ha függőleges marad) |

Amikor az Excel kiértékeli ezt, egy **vertical** listát (függőleges listát) hoz létre:

```
A1: 1
A2: 2
A3: 3
A4: 0   (filled with zeros)
A5: 0
```

> **Miért használjuk az EXPAND-et?** Elkerüli a manuális másolást vagy VBA ciklusokat. A függvény dinamikusan átalakítja az adatokat, így a táblázataid robusztusabbak és könnyebben karbantarthatóak lesznek.

---

## 4. lépés: Excel munkafüzet mentése – Az eredmény megőrzése

Miután a képlet a helyén van, az utolsó lépés a munkafüzet lemezre írása. Bármely mappát választhatod, amelyhez írási jogosultságod van.

```csharp
        // Step 4: Save the workbook to view the result
        string outputPath = @"C:\Temp\ExpandFormula.xlsx";
        workbook.Save(outputPath);
    }
}
```

> **Mit fogsz látni:** Nyisd meg az `ExpandFormula.xlsx` fájlt Excelben, és az `A1` cella megjeleníti a kiterjesztett tömböt. Maga a képlet a cellában marad, így ha a forrás tömböt módosítod, a kimenet automatikusan frissül.

---

## Opcionális: A kimenet programozott ellenőrzése

Ha nem szeretnéd manuálisan megnyitni az Excelt, visszaolvashatod az értékeket, hogy megerősítsd, megfelelnek-e a vártnak.

```csharp
        // Verify values without opening Excel
        for (int row = 0; row < 5; row++)
        {
            var value = worksheet.Cells[row, 0].Value; // column 0 = A
            Console.WriteLine($"Row {row + 1}: {value}");
        }
```

A fenti futtatása kiírja:

```
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

---

## Gyakori kérdések és széljegyek

| Kérdés | Válasz |
|--------|--------|
| **Használhatom az EXPAND-et nagyobb forrás tömbbel?** | Természetesen. Csak cseréld le a `{1,2,3}`-at bármilyen állandóra vagy cellatartományra, például `EXPAND(A1:C1,10,1)`. |
| **Mi van, ha vízszintes eredményre van szükségem?** | Cseréld fel a sor/oszlop argumentumokat: `EXPAND({1,2,3},1,5)` egy 1‑soros, 5‑oszlopos eloszlást eredményez. |
| **Működik ez régebbi Excel verziókon?** | Az `EXPAND` az Excel 365/2021-től érhető el. Régebbi verziókhoz a tömböt `INDEX`/`SEQUENCE` segítségével kell szimulálni. |
| **Kell hívni a `workbook.CalculateFormula()`‑t?** | Nem. Az Aspose.Cells automatikusan kiértékeli a képleteket mentéskor, így az értékek azonnal megjelennek. |
| **Hogyan adhatok hozzá több munkalapot mentés előtt?** | Hívd meg a `workbook.Worksheets.Add("SecondSheet")`‑t, és ismételd meg a cella‑manipulációs lépéseket az új munkalapon. |

---

## Teljes működő példa

Az alábbiakban a teljes, futtatható program látható. Másold be egy konzolos alkalmazásba, állítsd be a kimeneti útvonalat, és nyomd meg a **F5**‑öt.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create new workbook
            Workbook workbook = new Workbook();

            // Access first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Add EXPAND formula to A1
            worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";

            // Optional: verify values in console
            workbook.CalculateFormula(); // ensures formulas are evaluated now
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"A{i + 1} = {worksheet.Cells[i, 0].Value}");
            }

            // Save the workbook
            string filePath = @"C:\Temp\ExpandFormula.xlsx";
            workbook.Save(filePath);
            Console.WriteLine($"Workbook saved to {filePath}");
        }
    }
}
```

**Várható kimenet a konzolon:**

```
A1 = 1
A2 = 2
A3 = 3
A4 = 0
A5 = 0
Workbook saved to C:\Temp\ExpandFormula.xlsx
```

Nyisd meg a generált fájlt, és ugyanazokat a számokat fogod látni az **A** oszlopban.

---

## Vizuális összefoglaló

![Új munkafüzet létrehozása példa](create-new-workbook.png "Képernyőkép, amely egy új munkafüzetet mutat, amely a create new workbook in C#-val lett létrehozva")

*A kép illusztrálja a frissen generált munkafüzetet az EXPAND eredménnyel.*

---

## Következtetés

Most már tudod, hogyan kell **create new workbook**, **add formula to cell**, és **save excel workbook** C#-ban. A **how to use expand** elsajátításával manuális munka nélkül generálhatsz dinamikus tömböket, és az egész folyamat lehetővé teszi, hogy **create excel file programmatically** bármilyen automatizálási forgatókönyvhöz.

Mi a következő? Próbáld meg kicserélni a konstans tömböt egy tartományhivatkozásra, kísérletezz különböző `EXPAND` dimenziókkal, vagy láncolj több képletet a munkalapok között. Ugyanez a minta működik diagramoknál, stílusoknál és még a pivot tábláknál is – ezért folytasd a felfedezést.

Ha bármilyen problémába ütköztél, hagyj megjegyzést alább. Boldog kódolást, és élvezd a programozott Excel erejét!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}