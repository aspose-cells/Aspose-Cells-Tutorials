---
category: general
date: 2026-03-22
description: Hogyan használjunk lambda kifejezést C#-ban Excel képletekkel való munkához.
  Tanulja meg, hogyan írjon képletet egy cellába, hogyan konvertáljon tartományt tömbbé,
  hogyan jelenítse meg a tömböt a konzolon, és hogyan számítsa ki a kotangenset Excelben.
draft: false
keywords:
- how to use lambda
- display array in console
- convert range to array
- write formula to cell
- calculate cotangent in excel
language: hu
og_description: Hogyan használjunk lambda kifejezést C#-ban az Excel képletek manipulálásához,
  a tartomány tömbbé konvertálásához, képlet írásához cellába, a tömb konzolra történő
  megjelenítéséhez, és a kotangens kiszámításához Excelben.
og_title: Hogyan használjunk lambda kifejezéseket C#-ban Excel képletekkel – lépésről
  lépésre
tags:
- C#
- Aspose.Cells
- Excel Automation
- Lambda Expressions
title: Hogyan használjuk a lambda kifejezéseket C#-ban Excel képletekkel – Teljes
  útmutató
url: /hu/net/formulas-functions/how-to-use-lambda-in-c-with-excel-formulas-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjunk lambda-t C#-ban Excel képletekkel – Teljes útmutató

Gondolkodtál már azon, **hogyan használjunk lambda-t**, amikor C#-ból automatizálod az Excelt? Nem vagy egyedül. Sok fejlesztő akad el, amikor az Excel új dinamikus tömbfüggvényeinek erejét kell kombinálni a C# `LAMBDA` képességével. A jó hír? Valójában elég egyszerű, ha látod, hogyan illeszkednek egymáshoz a részek.

Ebben az útmutatóban végigvezetünk a **képlet cellába írása**, **tartomány tömbbé konvertálása**, **tömb megjelenítése a konzolon**, és még **cotangens számítása Excelben** lépéseken, miközben megmutatjuk, **hogyan használjunk lambda-t** egy `REDUCE` híváson belül. A végére lesz egy futtatható kódrészlet, amelyet bármely .NET projektbe beilleszthetsz, amely hivatkozik az Aspose.Cells-re (vagy egy hasonló könyvtárra).

## Mit tanulhatsz meg

- Hogyan **írjunk képletet cellába** C#-ban.
- Hogyan **konvertáljunk tartományt tömbbé** az `EXPAND` függvénnyel.
- Hogyan **jelenítsünk meg egy tömböt a konzolon** a számítás után.
- Hogyan **számítsuk ki a cotangenset Excelben** a `COT` és `COTH` használatával.
- A pontos szintaxis **hogyan használjunk lambda-t** az Excel `REDUCE` függvényén belül C#-ból.

> **Előfeltétel:** Szükséged van egy friss .NET verzióra (Core 6+ vagy .NET Framework 4.7+), valamint az Aspose.Cells for .NET könyvtárra, amelyet a NuGet-en keresztül kell telepíteni.

## 1. lépés: A munkafüzet előkészítése és képlet írása cellába

Az első lépés, hogy létrehozzunk egy új munkafüzetet, és lekérjük az első munkalapot. Ezután **képletet írunk egy cellába** – ebben az esetben az `A1` tartalmazza az `EXPAND` hívás eredményét.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write formula to A1 – we’ll expand B1:C2 into a 4‑by‑5 array later
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";
```

**Miért fontos:** A képlet közvetlenül a kódból való írása lehetővé teszi, hogy helyben generálj összetett táblázatokat anélkül, hogy megnyitnád az Excelt. Emellett előkészíti a következő lépést, ahol **tartományt konvertálunk tömbbé**.

## 2. lépés: Tartomány konvertálása tömbbé az EXPAND használatával

`EXPAND` az Excel módja annak, hogy egy kis tartományt nagyobb mátrixszá alakítson. Ha a képletet az `A1`-be helyezzük, az Excel egy 4 × 5‑ös blokkot fog „kifolyatni” ebből a cellából. C#-ból nem kell manuálisan másolni az értékeket – a könyvtár elvégzi a nehéz munkát, amikor meghívjuk a `Calculate`-t.

```csharp
        // The EXPAND formula will spill into A1:E4 (4 rows × 5 columns)
        // No extra code needed – the workbook will handle the spill.
```

**Hogyan használjunk lambda-t:** Még nem, de maradj velünk. Először szükségünk van az adatokra a táblázatban, majd egy lambda-val fogjuk csökkenteni őket.

## 3. lépés: LAMBDA használata a REDUCE-ben – A „Hogyan használjunk lambda-t” lényege

Az Excel 365 bevezette a `REDUCE` függvényt, amely egy **kezdeti értéket**, egy **tartományt**, és egy **LAMBDA**-t fogad, amely meghatározza, hogyan kombinálja az egyes elemeket. C#-ból egyszerűen a képlet karakterláncát adjuk meg; a lambda az Excel képletben él, nem a C# kódban.

```csharp
        // Reduce the spilled array by summing all its values.
        // This demonstrates how to use lambda inside REDUCE.
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";
```

**Magyarázat:**  
- `0` a kezdő akkumulátor (`acc`).  
- `A1:D4` a feldolgozni kívánt tartomány (a kifolyás első négy oszlopa).  
- `LAMBDA(acc, x, acc + x)` azt mondja az Excelnek, hogy minden cellát (`x`) adjon hozzá az akkumulátorhoz.  

Ez a **hogyan használjunk lambda-t** lényege az aggregációhoz egy táblázatkezelő kontextusban.

## 4. lépés: Cotangens számítása Excelben – Fokból hiperbolikusra

Ha trigonometrikus eredményekre van szükséged, az Excel `COT` és `COTH` függvényei egyszerűek. Ezeket a `G1` és `G2` cellákba helyezzük.

```csharp
        // Demonstrate trigonometric functions – cotangent and hyperbolic cotangent
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected result: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";      // Hyperbolic cotangent of 1
```

**Miért hasznos:** A **cotangens számítása Excelben** ismerete megspórolhatja a saját matematikai kód írását, különösen, ha a munkafüzetet nem‑fejlesztőkkel osztod meg.

## 5. lépés: Számítás kényszerítése és a kibővített tömb lekérése

Most azt mondjuk a munkafüzetnek, hogy értékelje ki az összes képletet, majd kinyerjük a kifolyott tömböt az `A1`-ből. Itt jön a **tömb megjelenítése a konzolon**.

```csharp
        // Force calculation of all formulas
        workbook.Calculate();

        // Retrieve the spilled array from A1 as a 2‑D object
        var expanded = worksheet.Cells["A1"].Value;

        // Pretty‑print the 2‑D array to the console
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show the result of the REDUCE lambda
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Ami látható lesz:**  
- Egy szép formázott 4 × 5‑ös mátrix, soronként nyomtatva.  
- A `REDUCE` lambda által kiszámított összeg.  
- A két cotangens érték.

Ez befejezi a folyamatot a **képlet cellába írásától** egészen a **tömb konzolon való megjelenítéséig**.

## Teljes működő példa (másolás‑beillesztés kész)

Az alábbiakban a teljes program látható, amelyet beilleszthetsz egy konzolos alkalmazásba. Ne felejtsd el először hozzáadni az `Aspose.Cells` NuGet csomagot (`dotnet add package Aspose.Cells`).

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write EXPAND formula (convert range to array)
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";

        // Step 3: Use REDUCE with LAMBDA (how to use lambda)
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";

        // Step 4: Calculate cotangent values (calculate cotangent in excel)
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";

        // Step 5: Force calculation
        workbook.Calculate();

        // Step 6: Retrieve and display the expanded array (display array in console)
        var expanded = worksheet.Cells["A1"].Value;
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show REDUCE result
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Várható konzolkimenet (az értékek a B1:C2 alapértelmezett tartalma alapján változhatnak, ami alapértelmezés szerint 0):**

```
Expanded array from A1 (4×5):
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0

Sum of A1:D4 (via REDUCE lambda): 0
Cotangent of π/4: 1
Hyperbolic cotangent of 1: 1.31303528549933
```

Nyugodtan töltsd fel a `B1:C2` tartományt saját számaiddal a futtatás előtt – a mátrix ezeknek az értékeknek a megfelelően fog megjelenni.

## Pro tippek és gyakori buktatók

- **Pro tip:** Ha a kifolyó tartományt máshol szeretnéd kezdeni, egyszerűen módosítsd a célcellát (`A1`). Az `EXPAND` függvény tiszteletben tartja a horgonyt.
- **Vigyázz:** A forrástartomány üres cellái `0`-ként jelennek meg a kifolyott tömbben, ami befolyásolhatja a `REDUCE` összegét.
- **Különleges eset:** Ha a munkafüzet olyan képleteket tartalmaz, amelyek volatilis függvényektől (pl. `NOW()`) függenek, hívd meg a `workbook.Calculate()`-t a képletek beállítása után, hogy minden naprakész legyen.
- **Teljesítményjegyzet:** Nagy kifolyások esetén fontold meg a méret korlátozását az `EXPAND` hívásban; különben több memóriát foglalhatsz, mint amire szükség van.
- **Kompatibilitás:** A `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}