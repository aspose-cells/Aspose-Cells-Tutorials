---
category: general
date: 2026-02-15
description: Hozzon létre új Excel munkafüzetet, és tanulja meg használni az EXPAND
  függvényt, egy sorozat kibontását, valamint a kotangens kiszámítását. Emellett nézze
  meg, hogyan menthető a munkafüzet fájlba.
draft: false
keywords:
- create new excel workbook
- save workbook to file
- how to use expand
- how to expand sequence
- how to calculate cotangent
language: hu
og_description: Új Excel munkafüzet létrehozása C#-ban. Ismerje meg az EXPAND használatát,
  egy sorozat kibővítését, a kotangens kiszámítását, és a munkafüzet fájlba mentését.
og_title: Új Excel munkafüzet létrehozása C#‑ban – Teljes programozási útmutató
tags:
- C#
- Aspose.Cells
- Excel automation
title: Új Excel munkafüzet létrehozása C#-ban – Lépésről lépésre útmutató
url: /hu/net/excel-workbook/create-new-excel-workbook-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Új Excel munkafüzet létrehozása C#‑ban – Teljes programozási útmutató

Valaha is szükséged volt **új Excel munkafüzet** létrehozására kódból, és nem tudtad, hol kezdj? Nem vagy egyedül; sok fejlesztő szembesül ezzel a problémával jelentések automatizálásakor vagy adatcsővezetékek építésekor. Ebben az útmutatóban pontosan megmutatjuk, hogyan hozhatsz létre új Excel munkafüzetet, írj néhány menő képletet, majd **munkafüzetet fájlba mented** későbbi ellenőrzéshez.

Bele is merülünk a `EXPAND` függvény részleteibe, bemutatjuk **hogyan használjuk az expand-et**, hogy egy apró sorozatot nagy blokkká alakítsunk, elmagyarázzuk **hogyan bővítünk sorozatot** a gyakorlatban, és végül felfedjük **hogyan számítsuk ki a kotangenset** közvetlenül Excelben. A végére egy futtatható C# programod lesz, amelyet bármely .NET projektbe beilleszthetsz.

## Amire szükséged lesz

- **Aspose.Cells for .NET** (ingyenes próba vagy licencelt verzió) – a könyvtár, amely lehetővé teszi az Excel manipulálását Office telepítése nélkül.  
- **.NET 6+** (vagy .NET Framework 4.6+).  
- Egy egyszerű IDE, például a Visual Studio 2022, VS Code vagy Rider.  

Nem szükséges további NuGet csomag a `Aspose.Cells`-en kívül. Ha még nincs, futtasd:

```bash
dotnet add package Aspose.Cells
```

Ennyi—további beállításra nincs szükség.

## 1. lépés: Új Excel munkafüzet létrehozása

Az első dolog, amit teszünk, egy `Workbook` objektum példányosítása. Tekintsd úgy, mint egy üres vászonra, ahol minden munkalap, cella és képlet élni fog.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // default sheet is named "Sheet1"
```

> **Miért fontos:** A munkafüzet memóriában történő létrehozása azt jelenti, hogy a lemezt csak akkor érintjük, amikor kifejezetten **munkafüzetet fájlba mentünk**. Ez gyorsan tartja a műveletet, és lehetővé teszi további módosítások láncolását I/O terhelés nélkül.

## 2. lépés: Hogyan használjuk az EXPAND-et egy sorozat bővítésére

`EXPAND` egy újabb Excel függvény, amely egy kisebb tömböt egy meghatározott méretre nyújt. Példánkban egy három soros függőleges sorozattal kezdünk, és egy 5 × 5‑ös blokká alakítjuk.

```csharp
        // Step 2: Write a formula that expands a 3‑row sequence into a 5×5 block
        // The formula lives in A1 and will spill over to E5
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3),5,5)";
```

> **Magyarázat:** A `SEQUENCE(3)` `{1;2;3}`-at (függőleges tömb) ad. Az `EXPAND(...,5,5)` azt mondja az Excelnek, hogy ismételje a tömböt, amíg egy 5 soros és 5 oszlopos téglalapot nem tölt ki, A1‑től kezdve. Az eredmény egy mátrix, ahol minden oszlop ismétli az eredeti három számot, és az utolsó két sor üres, mert a forrás csak három sort tartalmaz.

### Várt kimenet

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 | 1 | 1 | 1 |
| 2 | 2 | 2 | 2 | 2 |
| 3 | 3 | 3 | 3 | 3 |
|   |   |   |   |   |
|   |   |   |   |   |

Ugyanazt a mintát fogod látni a tartományban, miután a munkafüzetet megnyitod Excelben.

## 3. lépés: Hogyan számítsuk ki a kotangenset Excelben

A legtöbb ember ismeri a `SIN`, `COS` és `TAN` függvényeket, de a `COT` egy kényelmes rövidítése a tangens reciprokának. Íme, hogyan kapjuk meg a 45°-os (ami 1) kotangenset radiánok használatával.

```csharp
        // Step 3: Write a formula that returns the cotangent of 45° (π/4 radians)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

> **Miért használjuk a COT‑ot?** A `COT` közvetlen hívása elkerüli a `1/TAN(...)`-nal járó extra osztást, így a képlet tisztább és nagy táblázatoknál valamivel gyorsabb.

## 4. lépés: Minden képlet kiértékelése

Az Aspose.Cells nem számítja ki automatikusan a képleteket, hacsak nem mondod meg neki. A `CalculateFormula` metódus kényszeríti a teljes kiértékelést, így az eredményértékek a cellákban tárolódnak.

```csharp
        // Step 4: Evaluate all formulas so the results are stored in the cells
        workbook.CalculateFormula();
```

> **Tipp:** Ha sok erőforrás-igényes képleted van, átadhatsz egy `CalculationOptions` objektumot a teljesítmény finomhangolásához (pl. több szál engedélyezése).

## 5. lépés: Munkafüzet mentése fájlba

Most, hogy minden készen áll, végül **munkafüzetet fájlba mentünk**. Válassz egy mappát, amelyhez írási jogosultságod van, és adj a fájlnak egy értelmes nevet.

```csharp
        // Step 5: Save the workbook to a file for inspection
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath);
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

> **Mi történik a lemezen?** A `Save` hívás egy teljes `.xlsx` csomagot ír, amely tartalmazza az `EXPAND`‑ből származó kitöltött tömböt és a kiszámított kotangens értéket. Nyisd meg a fájlt Excelben, és látni fogod az A1‑től kezdődő 5 × 5‑ös blokkot, valamint a `1` számot a B1‑ben.

![Excel kimenet, amely a kibővített sorozatot és a kotangens értékét mutatja](excel-output.png "új excel munkafüzet példakimenet")

*Kép alt szöveg: új excel munkafüzet példakimenet*

### Gyors ellenőrzés

1. Nyisd meg az `output.xlsx` fájlt.  
2. Ellenőrizd, hogy a **A1:E5** cellák a megismételt 1‑2‑3 mintát tartalmazzák.  
3. Nézd meg a **B1**‑et – ennek `1`‑et kell mutatnia.  

Ha minden egyezik, gratulálok—sikeresen automatizáltad az Excelt!

## Hogyan bővítsünk sorozatot más helyzetekben

Miközben a fenti példa egy statikus `SEQUENCE(3)`‑t használ, könnyen helyettesítheted egy dinamikus tartománnyal vagy egy másik képlettel:

```csharp
// Expand a dynamic range from D1:D10 to a 4×4 block
worksheet.Cells["F1"].Formula = "=EXPAND(D1:D10,4,4)";
```

**Mikor érdemes használni?**  
- Helyőrző táblázatok generálása sablonokhoz.  
- Fejléc sor gyors másolása sok oszlopra.  
- Hőtérkép rácsok építése manuális másolás‑beillesztés nélkül.

## Gyakori buktatók és hogyan kerüld el őket

| Buktató | Miért fordul elő | Megoldás |
|---------|------------------|----------|
| `#VALUE!` az `EXPAND` után | A forrás tömb nem megfelelő tartomány (pl. hibákat tartalmaz) | Tisztítsd meg a forrás adatokat, vagy csomagold `IFERROR`‑be. |
| A kotangens `#DIV/0!`-t ad 0°-nál | `COT(0)` matematikailag végtelen | Véd `IF(PI()/4=0,0,COT(...))`-val. |
| A munkafüzet nincs mentve | Az útvonal érvénytelen vagy hiányzik az írási jogosultság | Használd a `Path.GetFullPath`‑t és ellenőrizd, hogy a mappa létezik. |
| A képletek nincsenek kiszámítva | `CalculateFormula` hiányzik | Mindig hívd meg a `Save` előtt. |

## Bónusz: Stílus hozzáadása (opcionális)

Ha szebb megjelenést szeretnél, a számítások után egyszerű stílust alkalmazhatsz:

```csharp
        // Apply a light gray background to the expanded block
        Style style = workbook.CreateStyle();
        style.Pattern = BackgroundType.Solid;
        style.ForegroundColor = System.Drawing.Color.LightGray;
        StyleFlag flag = new StyleFlag { CellShading = true };
        worksheet.Cells.CreateRange("A1:E5").ApplyStyle(style, flag);
```

Ez a kódrészlet opcionális, de bemutatja, hogyan kombinálhatod a **új Excel munkafüzet létrehozása** logikát a formázással egyetlen lépésben.

## Összefoglalás

Áttekintettük a teljes folyamatot:

1. **Új Excel munkafüzet** létrehozása Aspose.Cells‑szel.  
2. **Hogyan használjuk az expand-et** egy apró `SEQUENCE`‑t 5 × 5‑ös mátrixszá alakít.  
3. **Hogyan számítsuk ki a kotangenset** közvetlenül egy cellában.  
4. Kényszerítsd a számítást a `CalculateFormula`‑val.  
5. **Munkafüzet mentése fájlba** és az eredmény ellenőrzése.  

Mindez önálló, bármely friss .NET futtatókörnyezeten fut, és csak egy NuGet csomagot igényel.

## Mi a következő?

- **Dinamikus adatforrások:** Adatok lekérése adatbázisból és betáplálása az `EXPAND`‑be.  
- **Több munkalap:** Ciklus a munkalapok gyűjteményén, hogy teljes jelentéskönyvet generálj.  
- **Haladó képletek:** Fedezd fel a `LET`, `LAMBDA` vagy tömb‑alapú feltételes logikát az intelligensebb táblázatokhoz.  

Nyugodtan kísérletezz—cseréld le a `SEQUENCE` argumentumot, próbálj ki különböző szögeket a `COT`‑hoz, vagy kombináld diagramgenerálással. A lehetőségek végtelenek, ha programozottan **új Excel munkafüzetet hozol létre**.

---

*Boldog kódolást! Ha bármilyen problémába ütköztél, hagyj megjegyzést alább vagy írj nekem a Twitteren @YourHandle. Szívesen segítek.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}